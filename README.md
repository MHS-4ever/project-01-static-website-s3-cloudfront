## 📌 Project Overview
This project demonstrates the deployment of a high-performance, globally distributed static web application using **Amazon S3** and **Amazon CloudFront**. 

To simulate a real-world scenario involving heavy assets and complex file structures, I deployed a **Unity WebGL** build. This project focuses on production-ready configurations, troubleshooting permission bottlenecks, and optimizing content delivery while remaining within the **AWS Free Tier**.

## 🎯 Objectives
*   Host static web assets in a highly available environment (**Amazon S3**).
*   Implement global content delivery with low latency using **Amazon CloudFront (CDN)**.
*   Configure **IAM Bucket Policies** for secure and precise access control.
*   Debug and resolve common deployment blockers (403 Forbidden, XML Root issues).
*   Document a production-style workflow for portfolio demonstration.

## 🧩 Architecture
The application follows a standard serverless static hosting pattern:

`User Browser` ➔ `CloudFront Edge Location` ➔ `Amazon S3 (Origin)`

*   **Amazon S3:** Acts as the origin server storing HTML, WASM, and JS assets.
*   **Amazon CloudFront:** Functions as the CDN to cache content globally.
*   **Bucket Policy:** Defines who can read the objects.

---

## 🛠️ Tech Stack
*   **Storage:** Amazon S3
*   **CDN:** Amazon CloudFront
*   **Security:** AWS IAM (Bucket Policies)
*   **Frontend:** Unity WebGL (HTML5/WASM)

---

## 🚀 Implementation Journey

### 1. S3 Environment Setup
*   Created bucket: `hasnain-aws-unity-webgl-build` in `us-east-1`.
*   Uploaded the Unity build directory structure, including the `Build/` and `TemplateData/` folders.
*   Initial configuration involved disabling "Block All Public Access" to allow for policy-based entry.

### 2. Troubleshooting & Technical Fixes
Deploying complex assets like Unity WebGL often results in configuration hurdles. Below are the key issues identified and resolved:

#### 🛑 Issue #1: CloudFront AccessDenied (403)
*   **The Problem:** Accessing the CloudFront URL resulted in a 403 Forbidden error.
*   **The Root Cause:** The S3 bucket was private by default and lacked a policy allowing CloudFront/Public to fetch objects.
*   **The Fix:** Applied a JSON Bucket Policy allowing `s3:GetObject` permissions. [View Policy](./policies/s3-bucket-policy.json)

#### 🛑 Issue #2: XML Response at Root URL
*   **The Problem:** Navigating to the root domain showed an S3 XML file list instead of the website.
*   **The Root Cause:** CloudFront did not know which file to serve first (Missing Default Root Object).
*   **The Fix:** Configured the **Default Root Object** in CloudFront settings to `index.html`.

#### 🔍 MIME Type Investigation
*   **Investigation:** Checked if manual MIME types (like `application/wasm`) were needed for Unity.
*   **Result:** Verified via Browser DevTools that modern AWS/S3 deployments automatically detect and serve the correct MIME types for Unity WebGL, requiring no manual overrides.

---

## 📁 Repository Structure
```text
project-01-static-website-s3-cloudfront/
├── architecture/           # Architecture diagrams
├── policies/               # S3 Bucket Policy JSON files
├── notes/                  # Detailed troubleshooting logs
└── screenshots/            # Evidence of deployment & AWS console settings
```

---

## ✅ Final Results
*   **Global Latency:** Content is served from the nearest Edge location via CloudFront.
*   **Zero Errors:** Clean console with no WASM compile failures or CORS issues.
*   **Resume Ready:** Successfully implemented a project that balances cost-efficiency with performance.

## 🔐 Security Note
*For the purpose of this learning lab, the bucket uses a **Public Read Policy**. In a strict production environment, I recommend using **CloudFront Origin Access Control (OAC)** to keep the S3 bucket completely private, ensuring users can only access content through the CDN.*
