---
title: "Why we moved our CI from 25 minutes to 6"
description: "How caching and test splitting cut our pipeline time."
pubDate: 2026-10-01
author: "Nimbus Engineering"
tags: ["ci", "devops"]
---

Our pipeline used to take 25 minutes, and developers stopped waiting for it. We fixed three things. First, we cached dependencies between runs. Second, we split our tests across four parallel jobs. Third, we stopped building Docker images for branches that only changed docs.

The result is a 6 minute pipeline and noticeably fewer "I'll merge it anyway" moments.
