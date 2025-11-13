---
date: 2025-11-07
tags:
    - 
hubs:
    - "[[]]"
---

# 2025-11-07-redshift-access-commands-to-role

CREATE ROLE rs_access;

GRANT USAGE ON SCHEMA public TO ROLE rs_access;

GRANT SELECT ON ALL TABLES IN SCHEMA public TO ROLE rs_access;
