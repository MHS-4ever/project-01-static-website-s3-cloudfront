## Issues Faced & Fixes

### AccessDenied (403)
- Cause: Missing S3 bucket policy
- Fix: Added s3:GetObject permission

### CloudFront XML Response
- Cause: Missing default root object
- Fix: Set index.html as the default root

### MIME Type Concerns
- Investigation showed no manual changes required
