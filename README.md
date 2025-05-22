
# 🌐 Hosting a Static Website on Amazon Simple Storage Service(S3)

## 📌 Project Overview
This project demonstrates how to host a static website (HTML + assets) on **Amazon S3**, leveraging its scalability, security, and cost-efficiency.

**Key Achievements**:
- Created an S3 bucket in **Africa (Cape Town)** region.
- Enabled static website hosting with public access.
- Resolved `403 Forbidden` errors via ACL permissions.

⏳ **Time Spent**: 1–2 hours

---

## 🛠️ Technologies Used
- **AWS Services**: S3 (Simple Storage Service)
- **Files**: `index.html`, image assets (ZIP)

---

## 📂 Step-by-Step Setup

### 1️⃣ Create an S3 Bucket
1. Go to the AWS Management Console.
2. Navigate to **S3** and click **Create bucket**.
3. Enter a **unique bucket name** (e.g., `nextwork-website-project-iancliff`).
4. Choose a region (e.g., `Africa (Cape Town)`).
5. Leave other settings default and click **Create bucket**.

### 2️⃣ Upload Website Files
1. Upload `index.html` and your images (unzipped) to the bucket.
2. Example folder structure:
    ```bash
    nextwork-website-project-iancliff/
    ├── index.html
    └── images/
        ├── logo.png
        └── banner.jpg
    ```

### 3️⃣ Enable Static Website Hosting
1. Go to your S3 bucket → **Properties** tab.
2. Scroll to **Static website hosting** → Click **Edit**.
3. Choose:
    - **Hosting type**: _Host a static website_
    - **Index document**: `index.html`
4. Click **Save changes**.
5. AWS will generate a **bucket endpoint URL** like:  
   `http://your-bucket.s3-website-af-south-1.amazonaws.com`

### 4️⃣ Configure Permissions

#### A. Disable “Block Public Access”
1. Go to the **Permissions** tab.
2. Click **Edit** next to **Block Public Access**.
3. Uncheck all boxes.
4. Click **Save changes**.

#### B. Add a Bucket Policy
1. In the **Permissions** tab, click **Bucket Policy**.
2. Paste the following JSON (replace `your-bucket-name`):
    ```json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": "*",
          "Action": "s3:GetObject",
          "Resource": "arn:aws:s3:::your-bucket-name/*"
        }
      ]
    }
    ```

#### C. Make Objects Public
1. Go to the **Objects** list in your bucket.
2. Select all files → Click **Actions** → **Make public**.

### 5️⃣ Access Your Website
- Open the **bucket endpoint URL** in a browser.
- You should now see your static website.

🖼️ *Images/Web Hosting 4.png*

---

## 🚨 Troubleshooting Common Issues

### ❌ 403 Forbidden Error
- **Cause**: Public access blocked or permissions not configured.
- **Solution**:
    - Ensure **Block Public Access** is disabled.
    - Ensure **bucket policy** allows `s3:GetObject`.
    - Ensure all files are marked **public**.

### ❌ NoSuchKey Error
- **Cause**: `index.html` is missing or misnamed.
- **Solution**: Re-upload and verify the document name.

### ❌ Mixed Content Errors (Images or CSS not loading)
- **Cause**: Using `http://` or incorrect paths.
- **Solution**: Use **relative paths** or `https://`.

---

## 📜 Final Notes
- Amazon S3 (Simple Storage Service) is an object storage service by AWS that
 allows you to store and retrieve any amount of data from anywhere on the web.
 Useful because it combines high scalability, security, and cost-efficiency,
 making it adaptable.

---

## 🔗 References
- [AWS S3 Static Website Hosting Docs](https://docs.aws.amazon.com/AmazonS3/latest/userguide/WebsiteHosting.html)
