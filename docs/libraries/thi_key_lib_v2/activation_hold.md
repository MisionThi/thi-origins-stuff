---
title: Activation hold
date: 2021-07-28
---

# Hold activation
<br />

**Power file**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/secondary/toggle_convert",
  "comparison": "==",
  "compare_to": 1
}
```
<br />
**Power_link file**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/secondary/toggle_convert",
  "comparison": "==",
  "compare_to": 1
}
```