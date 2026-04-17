# 🌐 Secure Static Site Hosting on AWS (S3 + CloudFront)

![AWS Architecture Badge](https://img.shields.io/badge/AWS-S3%20%7C%20CloudFront-orange?style=for-the-badge&logo=amazon-aws)
![HTTPS Enabled Badge](https://img.shields.io/badge/HTTPS-Enabled-brightgreen?style=for-the-badge&logo=cloudflare)
![CDN Supported Badge](https://img.shields.io/badge/CDN-Supported-blue?style=for-the-badge&logo=jsdelivr)

--- [GO TO WEBSITE](https://amzn-s3-aws-notes.s3.ca-central-1.amazonaws.com/aws-cheatsheet.html?X-Amz-Algorithm=AWS4-HMAC-SHA256&X-Amz-Content-Sha256=UNSIGNED-PAYLOAD&X-Amz-Credential=ASIAYPQMKRTKICJ2ZU3G%2F20260417%2Fca-central-1%2Fs3%2Faws4_request&X-Amz-Date=20260417T211831Z&X-Amz-Expires=300&X-Amz-Security-Token=IQoJb3JpZ2luX2VjEBUaDGNhLWNlbnRyYWwtMSJIMEYCIQDwAudJwUW%2FYcrefMT4rOPuKQd0JWSAs%2BH66Cg8IDAARAIhAKvOjj4R4umxqF8Ke%2B9DnpaNzFZwnIOvNJkhXX40ZMKCKvoCCN7%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEQABoMNTgzMDY3NjY3NjY4IgyjWjlTp%2BeO6M96JvUqzgLajid5cLqX9q4UGHMfPmnoA3oRb1HiK0ZQ6ZsP3HF6bH7JFgq33bZ7IvT2G981lboXLGMmenf2OVqkIxlhJHYvQ1iQVxeWCCG%2BxFu2mN7DI%2BUhNsnxE0gtgVWkJtY6qFtvMtP7EE%2BMFvcLhuNE0QxfaBU7U6qWivoGmGgYdVG1LPFKLJoNavTUwW3v4%2BLvmOiuj%2BVHvxggYDcHh83XR0GfhiWmlRdCrDeGoPWQHr5gKQgzCxZ%2FtofYhjLpvm8eVNTn86%2FDL9bPhi%2BfTEvzyMWmD18NdKUgBbMxfhTd4IdAC3TVWuZmCkAUo%2FcAILUC%2Fda6Ta%2FF2bI6H%2BJ1KPIlXwhAZXHx%2B22IC0w1UO%2FImlpVNP65jV8RyKiTiIWubi0ab00ylSg2tAOVpAfUQD%2FY9dCTXFwojhAj3vYsHDhc58fjgwPdPnEi%2B9drLTJOlB0eMM6nis8GOqwCLcbcMNcZ8SPB2m%2FpHn3Q7%2Bq2hw078EBzXGRZ4pIYVgaWytLNw1zu79zZ9a8PORZFMFxU0qvgAEXbRHU%2B4KntHPHlaQMp2Mi%2FE0Wvmz4jNxs0LH8Pj9%2BxNy4n%2B0WyPF0ULtEp5e5%2BuyvGzIZLLZYiUbmvWVCJyzs73rM7Lrm9%2FEQzIcr7LxSbWqwyR8yXiQ1PT39yZGv8LAaGayaXjJP7P%2Bc81lOi2dYYVjFbYqqywEyfmf0cX8qrAUyxlGrp8kpt5BLbOE2MpUnd1ntDK4Ikv%2BJbOAbCDvPPadoRcNk395z%2FB97jRtAMvr%2Fwm6NtwpuTAPRpT%2FRczn75lpn2h3S%2BvEelIDUHp6EYFGYLszroxBrraKsFc%2BW5RiBWobn6oCHV1a%2FGpDk2ZdIa%2FrpO&X-Amz-Signature=d6de0172151858c46ec68a54ebad6db6fcc0cee4f4e4435b1ad72989d34026b1&X-Amz-SignedHeaders=host&response-content-disposition=inline)

## 🚀 Overview

This project demonstrates a robust and secure method for hosting static websites on Amazon Web Services (AWS) using a combination of **Amazon S3** for storage and **Amazon CloudFront** as a Content Delivery Network (CDN). The primary goal is to ensure optimal performance, global accessibility, and enhanced security by keeping the S3 bucket private.

---

## ✨ Key Features

*   **🔒 Enhanced Security:** S3 bucket remains private, preventing direct public access and minimizing exposure to threats.
*   **⚡ Blazing Fast Performance:** Leverages CloudFront's global edge network for content caching, reducing latency and improving load times for users worldwide.
*   **✅ Automatic HTTPS:** CloudFront automatically provisions and manages SSL certificates, ensuring secure communication (HTTPS) without manual configuration.
*   **💸 Cost-Effective:** Utilizes highly scalable and economical AWS services suitable for projects of all sizes.
*   **🔄 Version Control (Optional but Recommended):** S3 Bucket Versioning can be enabled to protect against accidental deletions or overwrites, providing a robust recovery mechanism.

---

## 🏛️ Architecture

The solution employs a classic AWS static website hosting pattern:

1.  **Amazon S3:** Stores all static website assets (HTML, CSS, JavaScript, images) in a private S3 bucket. Public access is entirely blocked.
2.  **Amazon CloudFront:** Acts as the CDN, caching content at edge locations globally. It serves as the single entry point for users accessing the website.
3.  **Origin Access Control (OAC):** A secure mechanism that allows CloudFront to fetch content from the private S3 bucket, preventing direct S3 access from the internet.

```
       +-------------------+        +---------------------------------+        +---------------------+
       |   End User (Web)  |        |    Amazon CloudFront (CDN)    |        |  Amazon S3 (Private)  |
       +---------+---------+        +--------------+----------------+        +-----------+-----------+
                 |                                 |                                    |
                 | HTTP/HTTPS                      | Secure Connection (OAC)            | Static Assets
                 +-------------------------------->+----------------------------------->+
                                                   | Cache Misses                       |
                                                   |                                    |
                                                   |<-----------------------------------+
                                                   |
                                                   |
                                                   +----> Cached Content to End User
```

_**[Optional: Replace the ASCII diagram above with a professional diagram created using tools like draw.io, Lucidchart, or Excalidraw, and link it here.]**_
[Link to Architecture Diagram Here (e.g., `architecture.png`)]

---

## 🚀 Setup & Deployment

Follow these high-level steps to deploy your static website:

### Prerequisites

*   An AWS account with appropriate permissions to create S3 buckets and CloudFront distributions.
*   Your static website files (e.g., `index.html`, `style.css`, `script.js`).

### 1. Prepare your S3 Bucket

1.  **Create an S3 Bucket:** Create a new S3 bucket (or use an existing one) in your desired AWS region.
2.  **Upload Website Files:** Upload all your static website files to the root of this S3 bucket. Ensure your main page is named `index.html`.
3.  **Block Public Access:** Navigate to your S3 bucket's **Permissions** tab. Ensure **"Block all public access"** is **enabled**. This is crucial for security.
4.  **(Optional but Recommended) Enable Versioning:** On the **Properties** tab, enable **"Bucket Versioning"** to protect against accidental deletions.

### 2. Create CloudFront Distribution

1.  Go to the **CloudFront Console** and click **"Create distribution"**.
2.  **Origin Domain:** Select your S3 bucket from the dropdown list.
3.  **Origin Access:** Choose **"Origin access control settings (recommended)"**.
    *   Click **"Create control setting"** and accept the defaults.
4.  **Viewer Protocol Policy:** Set to **"Redirect HTTP to HTTPS"** for secure access.
5.  **Default Root Object:** Enter `index.html` (or your main entry point file).
6.  Leave other settings as default or configure as needed (e.g., WAF, custom CNAME).
7.  Click **"Create distribution"**.

### 3. Update S3 Bucket Policy

After creating the CloudFront distribution, you *must* grant it permission to access your private S3 bucket.

1.  On the CloudFront distribution details page, you will see a **yellow banner** prompting you to update your S3 bucket policy.
2.  Click the **"Copy policy"** button provided in the banner.
3.  Go back to your S3 bucket's **Permissions** tab.
4.  Under the **"Bucket policy"** section, click **"Edit"**.
5.  Paste the copied policy JSON into the editor, replacing any existing content.
    *   **Example Policy (generated by CloudFront):**
        ```json
        {
            "Version": "2008-10-17",
            "Id": "PolicyForCloudFrontPrivateContent",
            "Statement": [
                {
                    "Sid": "AllowCloudFrontServicePrincipal",
                    "Effect": "Allow",
                    "Principal": {
                        "Service": "cloudfront.amazonaws.com"
                    },
                    "Action": "s3:GetObject",
                    "Resource": "arn:aws:s3:::YOUR_BUCKET_NAME/*",
                    "Condition": {
                        "StringEquals": {
                            "AWS:SourceArn": "arn:aws:cloudfront::YOUR_ACCOUNT_ID:distribution/YOUR_CLOUDFRONT_DISTRIBUTION_ID"
                        }
                    }
                }
            ]
        }
        ```
        *(Note: `YOUR_BUCKET_NAME`, `YOUR_ACCOUNT_ID`, and `YOUR_CLOUDFRONT_DISTRIBUTION_ID` will be automatically populated by CloudFront when you copy the policy.)*
6.  Click **"Save changes"**.

### 4. Test Your Website

1.  Wait for your CloudFront distribution's status to change from "Deploying" to **"Enabled"** (this can take 5-10 minutes).
2.  Copy the **"Distribution domain name"** (e.g., `d1234abcd.cloudfront.net`) from the CloudFront console.
3.  Paste this URL into your web browser. Your secure static site should now be live!

_**[Optional: Add a screenshot of your live website here!]**_
[Link to Live Site Screenshot Here (e.g., `live-site.png`)]

---

## ⚠️ Important Considerations

*   **Cost:** While S3 and CloudFront are cost-effective, be mindful of data transfer out charges, especially if your site has many large assets or high traffic. Utilize S3 lifecycle rules for versioned objects to manage costs.
*   **Cache Invalidation:** If you update your website files, CloudFront might continue serving the old cached version. You may need to create a **cache invalidation** in CloudFront to force it to fetch the new content from S3.
*   **Custom Domains:** For a professional look, you'll want to configure a custom domain (e.g., `www.yourdomain.com`) with Route 53 and link it to your CloudFront distribution.

---

## 🛠️ Troubleshooting

*   **`403 Forbidden` Error:**
    *   Ensure your S3 bucket policy correctly grants `s3:GetObject` permission to your CloudFront OAC.
    *   Verify that "Block all public access" is **enabled** on your S3 bucket.
    *   Check that the CloudFront distribution is fully "Enabled."
*   **`404 Not Found` Error:**
    *   Confirm your `index.html` (or specified default root object) is present in the **root** of your S3 bucket.
    *   Check for typos in the "Default Root Object" setting in CloudFront.
*   **Content Not Updating:**
    *   Perform a **cache invalidation** in CloudFront for the changed paths (e.g., `/*` for all files).

---

## 🤝 Contributing

Feel free to suggest improvements or add more details to this README.md!

---

## 📄 License

This project is open-sourced under the MIT License. See the [LICENSE](LICENSE) file for details.
