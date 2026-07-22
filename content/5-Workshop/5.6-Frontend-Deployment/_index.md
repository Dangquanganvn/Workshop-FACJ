---
title: "Frontend Deployment"
date: 2024-01-01
weight: 6
chapter: false
pre: " <b> 5.6. </b> "
---

# Frontend Deployment to Amazon S3

In this section, we will host the static frontend interface of the **Fashion E-commerce Platform** using **Amazon S3 Static Website Hosting**. The frontend application is built locally using React into optimized production-ready static assets and then uploaded directly to an S3 bucket configured for public web hosting.

### Architectural Overview & Deployment Steps

1. **React Production Build:**
   - Execute production build scripts (e.g., `npm run build`) to bundle the React application into high-performance static files (`HTML`, `CSS`, and minimized JavaScript bundles).

2. **Amazon S3 Bucket Provisioning & Static Website Hosting:**
   - Create a dedicated S3 , disable block public access settings appropriately for website hosting, and enable **Static website hosting** with designated index and error documents (e.g., `index.html`).

![S3 Static Website Hosting Configuration](/images/5-Workshop/5.6-frontend/s3-website-hosting.png)
_*Figure: Amazon S3 bucket configuration and static website hosting settings.*_

1. **Uploading Build Artifacts & Interface Verification:**
   - Upload the compiled React production build files into the S3 bucket root directory, establishing the public-facing user interface for the e-commerce platform.

![Frontend Website Deployed on S3](/images/5-Workshop/5.6-frontend/frontend-deployed.png)
_*Figure: Successfully deployed React frontend user interface running on Amazon S3 static hosting.*_
