# Project 1 — Static Website Hosting on AWS (S3 + CloudFront)

## Unity WebGL Static Website Deployment (Case Study)

---

## 📌 Overview

This project demonstrates how to deploy a **static web application** on AWS using **Amazon S3** and **Amazon CloudFront**, following **AWS Free Tier–friendly** and **production-aware** practices.

A Unity WebGL build was used as the static asset set to simulate a real-world, asset-heavy web application.

---

## 🎯 Objectives

- Host a static website using Amazon S3
- Deliver content globally using Amazon CloudFront (CDN)
- Understand and apply S3 bucket policies
- Debug and resolve real AWS permission issues
- Follow a production-style deployment workflow (not a copy-paste tutorial)

---

## 📁 Repository Structure

project-01-static-website-s3-cloudfront/
├── README.md
├── architecture/
│ └── s3-cloudfront-architecture.png
├── policies/
│ └── s3-bucket-policy.json
├── notes/
│ └── issues-and-fixes.md
└── screenshots/
├── s3-bucket-objects.png
├── bucket-policy.png
├── cloudfront-settings.png
└── app-running.png

yaml
Copy code

---

## 🧩 Architecture

![Architecture Diagram](architecture/s3-cloudfront-architecture.png)

User Browser → CloudFront (CDN) → Amazon S3 (Static Assets)

yaml
Copy code

- **Amazon S3** stores static files (HTML, JS, WASM, asset folders)
- **CloudFront** delivers content globally with low latency
- **Bucket policy** enables read access for the hosted content

---

## 🛠️ AWS Services Used

- **Amazon S3** — Static file storage
- **Amazon CloudFront** — Global CDN distribution
- **AWS IAM** — Access control using bucket policies

All resources were deployed within **AWS Free Tier limits**.

---

## 🚀 Implementation Steps

### 1️⃣ S3 Bucket Setup

- Created an S3 bucket: `hasnain-aws-unity-webgl-build`
- Region: `us-east-1`
- Uploaded Unity WebGL build:
  - `index.html`
  - `Build/`
  - `TemplateData/`

---

### 2️⃣ Public Access Configuration

- Disabled **Block All Public Access**
- Applied a read-only **bucket policy** to allow object reads

Bucket policy is stored in this repo as code:

- `policies/s3-bucket-policy.json`

---

### 3️⃣ Issue #1 — CloudFront AccessDenied (403)

**Problem:**  
CloudFront URL returned `403 AccessDenied`.

**Root Cause:**  
S3 bucket had no policy allowing `s3:GetObject`.

**Fix:**  
Added a read-only bucket policy to allow object access.

---

### 4️⃣ Issue #2 — XML Response at CloudFront Root

**Problem:**  
CloudFront returned an XML message instead of loading the site.

**Root Cause:**  
CloudFront had no **Default Root Object** configured.

**Fix:**  
Set Default Root Object to:

index.html

yaml
Copy code

---

### 5️⃣ Final Validation

- Site loads via CloudFront successfully
- Unity WebGL game renders correctly
- No browser console errors:
  - AccessDenied
  - CORS issues
  - WASM compile failures
  - MIME blocking

---

## 🔍 MIME Type Investigation

Older Unity WebGL guides mention manually configuring MIME types.

After verifying:
- S3 object metadata
- CloudFront delivery behavior
- Browser developer tools

➡️ No manual MIME configuration was required for modern Unity WebGL builds.

---

## ✅ Outcome

- Fully functional static website hosted on **S3**
- Delivered globally via **CloudFront**
- Debugged real permission + configuration issues
- Free Tier–friendly implementation

---

## 🔐 Security Note

This project uses a **public S3 bucket** for simplicity and learning purposes.

In later projects, a **private S3 bucket with CloudFront Origin Access Control (OAC)** is implemented to follow stricter production security best practices.

---

## 📸 Screenshots

Add screenshots to the `/screenshots` folder and reference them here:

- S3 bucket objects
- Bucket policy
- CloudFront distribution settings
- Application running in browser

---

## 📌 Resume Highlights

- Deployed a static web application using Amazon S3 and CloudFront with global CDN delivery
- Diagnosed and resolved S3 `AccessDenied (403)` issues using bucket policies
- Configured CloudFront default root object for correct application routing
- Validated deployment using browser developer tools
- Designed a Free Tier–optimized AWS static hosting solution

---

## 🏷️ Tags

AWS · S3 · CloudFront · Static Website · CDN · IAM · DevOps Portfolio