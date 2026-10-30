# Day 2/120 – #120DaysOfAWS: Writing a Custom IAM Policy from Scratch

On Day 1 I used an AWS managed policy (`ReadOnlyAccess`). It works, but it's broad. Today I wrote my own policy that allows exactly one thing: reading one S3 bucket and nothing else. That's least privilege in practice.

## Anatomy of an IAM policy

```json
{
  "Version": "2012-10-17",
  "Statement": [
    {
      "Sid": "ReadOneBucketOnly",
      "Effect": "Allow",
      "Action": ["s3:GetObject", "s3:ListBucket"],
      "Resource": [
        "arn:aws:s3:::robin-120days-demo",
        "arn:aws:s3:::robin-120days-demo/*"
      ]
    }
  ]
}
```

- **Version:** always `2012-10-17`, the current policy language version.
- **Statement:** one or more permission rules.
- **Sid:** an optional label so humans can tell statements apart.
- **Effect:** `Allow` or `Deny`.
- **Action:** the API calls the rule covers, written as `service:Action`.
- **Resource:** the ARN of what the actions apply to.
- **Condition (optional):** extra rules such as source IP, MFA required or a time window.

## Why two Resource lines?

Bucket-level actions like `s3:ListBucket` apply to the bucket ARN. Object-level actions like `s3:GetObject` apply to the objects inside it, which is why the second ARN ends in `/*`. Missing one of the two is a very common reason a "correct" policy still gets denied.

## What I did hands-on today

- Created a customer managed policy called `ReadDemoBucketOnly` using the JSON editor.
- Created a user group `DemoBucketReaders` and attached only that policy.
- Tested it in the **Policy Simulator**:
  - `s3:GetObject` on `robin-120days-demo/*` was **Allowed**.
  - `s3:PutObject` and `s3:DeleteObject` on the same bucket were **Denied** (implicit deny).
  - `s3:GetObject` on a different bucket was **Denied**, which shows the policy is scoped by resource.

## Common mistakes to avoid

1. `"Action": "*"` or `"Resource": "*"` on a statement that doesn't need it.
2. Forgetting the bucket ARN versus the object ARN (`/*`).
3. Copying a policy from the internet without reading every line.
4. Testing in production first instead of using the Policy Simulator.

## 3 habits I'm keeping

1. Start with no permissions and add one action at a time.
2. Scope the Resource to a specific ARN, not a wildcard.
3. Test every new policy in the Policy Simulator before attaching it to real users.

Tomorrow (Day 3): IAM roles and how services like EC2 get temporary credentials.
