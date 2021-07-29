---
title: Activation push
date: 2021-07-28
---

# Push activation
The activation type push detects the key is getting pressed and then grants the power for 1 tick. After that it will get revoked inmidietly.

<h3 style="margin-bottom: 0px;">Power file</h3>
The structre of the file is as followed: <br />

| power | Description |
|-------|-------------|
| `active` | This part indicates if the power is active when the power is still granted but not yet revoked. This is also the part which we will be checking for to see if the power is active aswell in the <u>power.json</u> as the <u>power_link.json</u>. |
| `main` | This part will disable the power directly when it has been run ones. |
| `scroll_check` | In this case does the power nothing but I keep it in there for consistency so all the activation-types have the same powers in the multiple. |
| `power` | This is the part where you make your power do something. The power can be named whatever you want and there can be multiple. The condition you see in this power we use to check if the power is active yes or no. |
 

```json
{
  "type": "apoli:multiple",
  
  "active": {
    "type": "apoli:resource",
    "min": 0,
    "max": 3,
    "start_value": 3,
    "hud_render": {
        "should_render": false
    }
  },
  
  "main": {
    "type": "apoli:action_over_time",
    "rising_action": {
      "type": "apoli:change_resource",
      "resource": "*:*_active",
      "change": -3
    },
    "interval": 1,
    "condition": {
      "type": "apoli:resource",
      "resource": "*:*_active",
      "comparison": "==",
      "compare_to": 3
    }
  },
  
  "scroll_check": {
    "type": "apoli:simple"
  },
  
  "power": {
    "type": "apoli:action_over_time",
    "entity_action": {
      "type": "apoli:execute_command",
      "command": "say power 1 active"
    },
    "interval": 1,
    "condition": {
      "type": "apoli:resource",
      "resource": "*:*_active",
      "comparison": "==",
      "compare_to": 3
    }
  }
}
```
<br />
<h3 style="margin-bottom: 0px;">power_link file</h3>
<h6 style="margin-bottom: 0px;">Snipit from complete file</h6>

<pre><code class="hljs json">{
  <span class="hljs-attr">"condition"</span>: {
    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:scoreboard"</span>,
    <span class="hljs-attr">"objective"</span>: <span class="hljs-string">"thi_p.a"</span>,
    <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"=="</span>,
    <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">1</span>
  },
  <span class="hljs-attr">"action"</span>: {
    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:if_else"</span>,
    <span class="hljs-attr">"condition"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:or"</span>,
      <span class="hljs-attr">"conditions"</span>: [
        {
          <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:resource"</span>,
          <span class="hljs-attr">"resource"</span>: <span class="hljs-string">"thi_key_libv2:example/power1_active"</span>,
          <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"&gt;="</span>,
          <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">1</span>
        },
        {
          <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:power"</span>,
          <span class="hljs-attr">"power"</span>: <span class="hljs-string">"thi_key_libv2:example/power1"</span>,
          <span class="hljs-attr">"inverted"</span>: <span class="hljs-literal">true</span>
        }
      ]
    },
    <span class="hljs-attr">"if_action"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:if_else"</span>,
      <span class="hljs-attr">"condition"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:scoreboard"</span>,
        <span class="hljs-attr">"objective"</span>: <span class="hljs-string">"thi_p.a.t"</span>,
        <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"=="</span>,
        <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">0</span>
      },
      <span class="hljs-attr">"if_action"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"origins:and"</span>,
        <span class="hljs-attr">"actions"</span>: [
          {
            <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
            <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power grant @s thi_key_libv2:example/power1"</span>
          },
          {    
            <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
            <span class="hljs-attr">"command"</span>: <span class="hljs-string">"say activate cooldown"</span>
          }
        ]
      }
    },
    <span class="hljs-attr">"else_action"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:if_else"</span>,
      <span class="hljs-attr">"condition"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:scoreboard"</span>,
        <span class="hljs-attr">"objective"</span>: <span class="hljs-string">"thi_p.a.t"</span>,
        <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"=="</span>,
        <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">1</span>
      },
      <span class="hljs-attr">"if_action"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
        <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power revoke @s thi_key_libv2:example/power1"</span>
      }
    }
  }
}
</code></pre>
