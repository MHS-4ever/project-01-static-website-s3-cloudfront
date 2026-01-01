# Issues and Fixes — Project 1

## Issue 1: AccessDenied (403)

**Service:** CloudFront / S3  
**Cause:** Missing S3 bucket policy  
**Fix:** Added s3:GetObject permission via bucket policy

---

## Issue 2: XML Error at CloudFront Root

**Service:** CloudFront  
**Cause:** Default root object not configured  
**Fix:** Set `index.html` as default root object

---

## Issue 3: MIME Type Concerns

**Investigation:**
- Reviewed S3 object metadata
- Checked browser console logs
- Verified Unity WebGL output

**Result:**  
No manual MIME type configuration was required.
