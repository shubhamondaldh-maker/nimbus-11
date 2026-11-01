---
title: "Postgres indexes we wish we had added earlier"
description: "Three missing indexes that caused our slowest queries."
pubDate: 2026-10-08
author: "Nimbus Engineering"
tags: ["postgres", "performance"]
---

A dashboard page was taking 4 seconds to load. EXPLAIN ANALYZE showed a sequential scan on a table with 2 million rows. One composite index brought it down to 40 milliseconds. We later found two more of the same pattern.

The lesson: check your slowest queries before you check your cache.
