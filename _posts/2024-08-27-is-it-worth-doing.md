---
title: "Is it worth doing?"
date: 2024-08-27
---

Today, I picked up an optimization ticket from our Jira board and started working on it. Throughout the day, I couldn't stop questioning whether it was worth doing.

The ticket was related to an "N+1 Query" issue. One of our endpoints performs the same database query multiple times, which Sentry flagged as an N+1 Query. Our product owner subsequently created a ticket to address it.

I opened the Sentry issue and began investigating. I noticed that this N+1 Query occurred only twice, and only in one of the test environments. Is it really worth addressing?

I decided to debug the endpoint locally. However, debugging led to the discovery of several other minor issues, which took time to resolve. Tick tock, tick tock. Is it worth doing?

Eventually, I successfully debugged the endpoint. The issue is valid and could potentially occur in production environments as well. But I'm unsure how to optimize the endpoint. Should I inform the product owner that this issue has only occurred twice? Perhaps it's not worth the effort...

Despite my doubts, I decided to think about optimization and found a solution in about 10 minutes. I implemented a pseudocode, and the next steps were clear to me. Still, I couldn't shake the feeling that my time might have been better spent on another ticket.

At that moment, another thought reassured me. My short-term goal is to build expertise in Flask and its associated libraries. I'm not focused on mastering expectation management and prioritization right now. While I do want to develop those skills, today is not the day. This realization put me at ease.

I hope to become more aware of these thoughts in the future and focus on building skills one at a time, without overwhelming myself.
