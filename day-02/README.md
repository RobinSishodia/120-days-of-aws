# Day 2: Writing a custom IAM policy from scratch

Part of my [#120DaysOfAWS](../README.md) series. **Status: draft, hands-on results to be confirmed.**

- [article.md](article.md): the write-up
- [policy-read-demo-bucket.json](policy-read-demo-bucket.json): the custom policy (read one S3 bucket only)
- [iam-policy-cheatsheet.png](iam-policy-cheatsheet.png): one-page cheat sheet
- [linkedin-caption.md](linkedin-caption.md): the LinkedIn post

## Hands-on plan

1. Create the customer managed policy `ReadDemoBucketOnly` from the JSON above.
2. Create the group `DemoBucketReaders` and attach only that policy.
3. In the Policy Simulator, test `s3:GetObject`, `s3:PutObject` and `s3:DeleteObject` on `robin-120days-demo/*`, then `s3:GetObject` on another bucket.

![IAM policy cheat sheet](iam-policy-cheatsheet.png)
