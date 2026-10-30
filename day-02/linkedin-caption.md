Day 2/120 of #120DaysOfAWS ✅

Yesterday I used an AWS managed policy. Today I wrote my own, one that allows exactly one thing: reading a single S3 bucket.

What I learned:
🔹 A policy is just Version, Statement, Effect, Action and Resource (plus an optional Condition)
🔹 Bucket actions use the bucket ARN, object actions need the /* ARN, and missing one is a classic reason a "correct" policy gets denied
🔹 Scope the Resource to a specific ARN, never "*" unless you must

I tested it in the Policy Simulator:
✔ GetObject on my bucket → Allowed
✘ PutObject / DeleteObject on my bucket → Denied
✘ GetObject on another bucket → Denied

Full write-up + cheat sheet 👇
https://sishodiarobin.hashnode.dev/day-2-120-120daysofaws-writing-a-custom-iam-policy-from-scratch

Tomorrow (Day 3): IAM roles and temporary credentials.

#AWS #120DaysOfAWS #IAM #CloudSecurity #LeastPrivilege #AWSCommunity #LearningInPublic
