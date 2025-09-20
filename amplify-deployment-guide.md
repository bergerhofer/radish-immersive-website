# AWS Amplify Deployment Guide for Radish Immersive

## Prerequisites
- GitHub account
- AWS account with appropriate permissions
- Domain `radishimmersive.com` configured in Route 53

## Step 1: Create GitHub Repository

1. **Go to GitHub.com**
2. **Click "New repository"**
3. **Repository settings**:
   - **Repository name**: `radish-immersive-website`
   - **Description**: `Radish Immersive Creative Studio Website`
   - **Visibility**: Public (required for free Amplify)
   - **Initialize**: Don't check any boxes
4. **Create repository**

## Step 2: Upload Files to GitHub

### Option A: Using GitHub Web Interface
1. **Go to your new repository**
2. **Click "uploading an existing file"**
3. **Upload all files**:
   - `index.html`
   - `insights.html`
   - `future-immersive-storytelling.html`
   - `case-study.html`
   - `styles.css`
   - `script.js`
   - `floating-radish.png`
   - `floating-radish-favicon.png`
   - `amplify.yml`
   - `package.json`
4. **Commit message**: `Initial website files`
5. **Commit changes**

### Option B: Using Git CLI
```bash
# In your project directory
git init
git add .
git commit -m "Initial website files"
git branch -M main
git remote add origin https://github.com/YOUR_USERNAME/radish-immersive-website.git
git push -u origin main
```

## Step 3: Set Up AWS Amplify

1. **Go to AWS Amplify Console**
   - Navigate to AWS Amplify service
   - Click "New app" → "Host web app"

2. **Connect Repository**
   - **Source**: GitHub
   - **Repository**: Select `radish-immersive-website`
   - **Branch**: `main`
   - **App name**: `radish-immersive-website`
   - **Environment**: `main`

3. **Build Settings**
   - **Build specification**: Use `amplify.yml` (already created)
   - **App build command**: `echo "No build needed"`
   - **Output directory**: `.` (root directory)

4. **Review and Deploy**
   - Review settings
   - Click "Save and deploy"

## Step 4: Configure Custom Domain

1. **Wait for initial deployment** (5-10 minutes)
2. **Go to Domain Management**
   - In your Amplify app, go to "Domain management"
   - Click "Add domain"

3. **Add Domain**
   - **Domain name**: `radishimmersive.com`
   - **Subdomain**: Leave empty for apex domain
   - Click "Configure domain"

4. **DNS Configuration**
   - Amplify will provide DNS records
   - Add these records to your Route 53 hosted zone:
     - **CNAME record**: `_1234567890abcdef` → `d1234567890abcdef.cloudfront.net`
     - **A record**: `@` → `123.456.789.012` (if provided)

5. **SSL Certificate**
   - Amplify will automatically request SSL certificate
   - Wait for validation (5-10 minutes)

## Step 5: Configure Redirects

1. **Go to Rewrites and Redirects**
2. **Add redirect rule**:
   - **Source address**: `https://www.radishimmersive.com`
   - **Target address**: `https://radishimmersive.com`
   - **Type**: `301 (Permanent Redirect)`

## Step 6: Test Your Site

1. **Wait for deployment** (10-15 minutes)
2. **Test URLs**:
   - `https://radishimmersive.com`
   - `https://www.radishimmersive.com` (should redirect)
   - `https://radishimmersive.com/insights.html`
   - `https://radishimmersive.com/future-immersive-storytelling.html`
   - `https://radishimmersive.com/case-study.html`

## Step 7: Set Up Automatic Deployments

1. **Go to App Settings** → **Build settings**
2. **Enable automatic deployments**:
   - **Branch**: `main`
   - **Auto-deploy**: Enabled

## Benefits of Amplify

### ✅ **Advantages**
- **Automatic deployments** on code changes
- **Built-in SSL** certificate management
- **Global CDN** via CloudFront
- **Easy domain management**
- **No server maintenance**
- **Automatic scaling**

### 💰 **Cost**
- **Free tier**: 1,000 build minutes/month
- **Hosting**: Free for static sites
- **Data transfer**: First 15GB free
- **Total**: ~$0-5/month

## Troubleshooting

### Common Issues:
1. **Build fails**: Check `amplify.yml` syntax
2. **Domain not working**: Verify DNS records in Route 53
3. **SSL issues**: Wait for certificate validation
4. **404 errors**: Check file paths and redirects

### Useful Commands:
```bash
# Check deployment status
aws amplify get-app --app-id YOUR_APP_ID

# Trigger manual deployment
aws amplify start-job --app-id YOUR_APP_ID --branch-name main --job-type RELEASE
```

## Next Steps
1. **Monitor deployments** in Amplify console
2. **Set up monitoring** with CloudWatch
3. **Configure custom headers** if needed
4. **Set up staging environment** for testing

## Success Criteria
- [ ] Site loads at `https://radishimmersive.com`
- [ ] All pages accessible
- [ ] SSL certificate valid
- [ ] www redirects to apex domain
- [ ] Mobile responsive
- [ ] All features working
- [ ] Automatic deployments enabled
