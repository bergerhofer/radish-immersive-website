# AWS Deployment Guide for Radish Immersive

## Prerequisites
- AWS Account with appropriate permissions
- Domain `radishimmersive.com` configured in Route 53
- All website files ready for upload

## Step 1: Create S3 Bucket

1. **Go to S3 Console**
   - Navigate to AWS S3 service
   - Click "Create bucket"

2. **Bucket Configuration**
   - **Bucket name**: `radishimmersive.com`
   - **Region**: Choose closest to your users (e.g., us-east-1)
   - **Block Public Access**: Uncheck "Block all public access"
   - **Bucket Versioning**: Disabled (for static sites)
   - **Default encryption**: Disabled

3. **Create Bucket**

## Step 2: Enable Static Website Hosting

1. **Select your bucket** (`radishimmersive.com`)
2. **Go to Properties tab**
3. **Scroll to "Static website hosting"**
4. **Click "Edit"**
5. **Configure**:
   - **Static website hosting**: Enable
   - **Hosting type**: Host a static website
   - **Index document**: `index.html`
   - **Error document**: `index.html` (for SPA routing)
6. **Save changes**

## Step 3: Upload Website Files

1. **Go to Objects tab**
2. **Click "Upload"**
3. **Add files**:
   - `index.html`
   - `insights.html`
   - `future-immersive-storytelling.html`
   - `case-study.html`
   - `styles.css`
   - `script.js`
   - `floating-radish.png`
   - `floating-radish-favicon.png`
4. **Upload all files**

## Step 4: Configure Bucket Policy

1. **Go to Permissions tab**
2. **Scroll to "Bucket policy"**
3. **Click "Edit"**
4. **Add this policy**:

```json
{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Sid": "PublicReadGetObject",
            "Effect": "Allow",
            "Principal": "*",
            "Action": "s3:GetObject",
            "Resource": "arn:aws:s3:::radishimmersive.com/*"
        }
    ]
}
```

5. **Save changes**

## Step 5: Request SSL Certificate

1. **Go to AWS Certificate Manager**
2. **Request a certificate**
3. **Choose "Request a public certificate"**
4. **Add domain names**:
   - `radishimmersive.com`
   - `www.radishimmersive.com`
5. **Choose DNS validation**
6. **Add validation records to Route 53**
7. **Wait for validation** (5-10 minutes)

## Step 6: Create CloudFront Distribution

1. **Go to CloudFront Console**
2. **Create distribution**
3. **Configure**:
   - **Origin Domain**: Select your S3 bucket
   - **Origin Path**: Leave empty
   - **Viewer Protocol Policy**: Redirect HTTP to HTTPS
   - **Allowed HTTP Methods**: GET, HEAD, OPTIONS, PUT, POST, PATCH, DELETE
   - **Cache Policy**: Managed-CachingDisabled
   - **Origin Request Policy**: Managed-CORS-S3Origin
   - **Response Headers Policy**: Managed-SecurityHeadersPolicy
   - **Alternate Domain Names (CNAMEs)**:
     - `radishimmersive.com`
     - `www.radishimmersive.com`
   - **SSL Certificate**: Select your certificate
   - **Default Root Object**: `index.html`

4. **Create Distribution**
5. **Wait for deployment** (15-20 minutes)

## Step 7: Configure Route 53

1. **Go to Route 53 Console**
2. **Select your hosted zone** (`radishimmersive.com`)
3. **Create records**:

   **A Record (apex domain)**:
   - **Record name**: Leave empty
   - **Record type**: A
   - **Alias**: Yes
   - **Route traffic to**: CloudFront distribution
   - **Select distribution**: Your CloudFront distribution

   **CNAME Record (www subdomain)**:
   - **Record name**: `www`
   - **Record type**: CNAME
   - **Value**: `radishimmersive.com`

## Step 8: Test Your Site

1. **Wait for DNS propagation** (up to 48 hours)
2. **Test URLs**:
   - `https://radishimmersive.com`
   - `https://www.radishimmersive.com`
   - `https://radishimmersive.com/insights.html`
   - `https://radishimmersive.com/future-immersive-storytelling.html`
   - `https://radishimmersive.com/case-study.html`

## Step 9: Optional - Set Up Redirects

1. **In CloudFront Console**
2. **Go to your distribution**
3. **Error Pages tab**
4. **Create custom error response**:
   - **HTTP Error Code**: 404
   - **Error Caching Minimum TTL**: 0
   - **Customize Error Response**: Yes
   - **Response Page Path**: `/index.html`
   - **HTTP Response Code**: 200

## Troubleshooting

### Common Issues:
1. **403 Forbidden**: Check bucket policy
2. **404 Not Found**: Verify file uploads and CloudFront cache
3. **SSL Issues**: Wait for certificate validation
4. **DNS Issues**: Wait for propagation

### Cache Issues:
- Clear CloudFront cache after updates
- Use CloudFront invalidation for immediate changes

## Cost Estimation
- **S3**: ~$1-5/month
- **CloudFront**: ~$1-10/month  
- **Route 53**: ~$0.50/month
- **Certificate Manager**: Free
- **Total**: ~$2.50-15.50/month

## Next Steps
1. Set up monitoring with CloudWatch
2. Configure backup strategy
3. Set up CI/CD pipeline for updates
4. Monitor performance and costs
