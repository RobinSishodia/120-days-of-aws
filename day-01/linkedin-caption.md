Day 1/120 of #120DaysOfAWS ✅

Every AWS action goes through one question: is this identity allowed to do this? That's IAM, so that's where I'm starting.

Today I created a ReadOnlyTeam group with the ReadOnlyAccess policy and tested it in the Policy Simulator:
✔ s3:GetObject → Allowed
✘ s3:DeleteObject → Denied (implicit deny)

My admin user got "Allowed" for both. Same actions, different policies, different answer. That's why least privilege matters.

Full write-up + cheat sheet 👇
https://sishodiarobin.hashnode.dev/day-1-120-120daysofaws-iam-the-front-door-to-everything-in-aws

Tomorrow (Day 2): writing a custom IAM policy from scratch.

#AWS #120DaysOfAWS #IAM #CloudSecurity #AWSCommunity #LearningInPublic #CloudComputing
