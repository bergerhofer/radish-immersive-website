# Radish Immersive Deployment Checklist

## Pre-Deployment
- [ ] All files are ready and tested locally
- [ ] Domain `radishimmersive.com` is active in Route 53
- [ ] AWS account has appropriate permissions
- [ ] All image files are optimized
- [ ] Favicon is working correctly

## S3 Setup
- [ ] Create S3 bucket named `radishimmersive.com`
- [ ] Enable static website hosting
- [ ] Set index document to `index.html`
- [ ] Set error document to `index.html`
- [ ] Upload all website files:
  - [ ] index.html
  - [ ] insights.html
  - [ ] future-immersive-storytelling.html
  - [ ] case-study.html
  - [ ] styles.css
  - [ ] script.js
  - [ ] floating-radish.png
  - [ ] floating-radish-favicon.png
- [ ] Apply bucket policy for public read access
- [ ] Test S3 website URL

## SSL Certificate
- [ ] Request certificate in AWS Certificate Manager
- [ ] Add domains: `radishimmersive.com` and `www.radishimmersive.com`
- [ ] Choose DNS validation
- [ ] Add validation records to Route 53
- [ ] Wait for certificate validation (5-10 minutes)

## CloudFront Distribution
- [ ] Create CloudFront distribution
- [ ] Set S3 bucket as origin
- [ ] Configure viewer protocol policy (redirect HTTP to HTTPS)
- [ ] Add alternate domain names (CNAMEs)
- [ ] Attach SSL certificate
- [ ] Set default root object to `index.html`
- [ ] Configure custom error pages (404 → index.html)
- [ ] Wait for distribution deployment (15-20 minutes)

## Route 53 Configuration
- [ ] Create A record for apex domain pointing to CloudFront
- [ ] Create CNAME record for www subdomain
- [ ] Verify DNS configuration

## Testing
- [ ] Test main site: `https://radishimmersive.com`
- [ ] Test www redirect: `https://www.radishimmersive.com`
- [ ] Test all pages:
  - [ ] Home page
  - [ ] About section
  - [ ] Insights page
  - [ ] Article page
  - [ ] Case study page
  - [ ] Contact form
- [ ] Test mobile responsiveness
- [ ] Test all internal links
- [ ] Test favicon display
- [ ] Test filter functionality on insights page

## Post-Deployment
- [ ] Monitor CloudWatch metrics
- [ ] Set up billing alerts
- [ ] Test site performance
- [ ] Verify SSL certificate is working
- [ ] Check for any console errors
- [ ] Test contact form functionality

## Optional Enhancements
- [ ] Set up CloudWatch monitoring
- [ ] Configure backup strategy
- [ ] Set up CI/CD pipeline
- [ ] Add analytics tracking
- [ ] Optimize images further
- [ ] Set up error monitoring

## Troubleshooting
- [ ] Clear CloudFront cache if needed
- [ ] Check S3 bucket permissions
- [ ] Verify Route 53 records
- [ ] Check SSL certificate status
- [ ] Monitor CloudFront logs

## Success Criteria
- [ ] Site loads at `https://radishimmersive.com`
- [ ] All pages are accessible
- [ ] SSL certificate is valid
- [ ] Mobile responsive design works
- [ ] All interactive features function
- [ ] Contact form works
- [ ] Favicon displays correctly
- [ ] No console errors
