---
title: Push activation-type
date: 2021-08-02
---

# Push activation
The push activation-type runs the power ones when the key is pressed.

<h3 style="margin-bottom: 0px;">Power file</h3>
The structre of the file is as followed: 

| Sub-powers | Description |
|------------|-------------|
| `active` | This part indicates if the power is active when the power is still granted but not yet revoked. This is also the part which we will be checking for to see if the power is active as well in the <u>power.json</u> as the <u>power_link.json</u>. |
| `main` | This part will disable the power directly when it has been run once. |
| `scroll_check` | In this case, does the power nothing but I keep it in there for consistency so all the activation-types have the same powers in the multiple. |
| `power` | This is the part where you make your power do something. The power can be named whatever you want and there can be multiple. The condition you see in this power we use to check if the power is active or not. 

```json
# power1.json
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

<h3 style="margin-bottom: 0px;">Code snipit for power_link.json</h3>
The parts that are highlighted are the parts you should change.

| Part | How to change |
|------|---------------|
| `1` | This is the power number from your power. All powers need to have a different power number! |
| `"thi_key_example:examples/power1_active"` | This part checks if the power is still active. You will have to change the part before `_active` to the path of your power file. |
| `"thi_key_example:examples/power1"` | This part checks if the power is already granted, this way it knows if it should revoke or grant the power. You should change this part to the path of your power file. |
| `"power grant @s thi_key_example:examples/power1"` | This grants the power. You should change this part to the path of your power file. |
| `"say activate cooldown"` | Here you can trigger the cooldown. [More on cooldowns.](cooldowns.md) |
| `"power revoke @s thi_key_example:examples/power1"` | This revokes the power. You should change this part to the path of your power file. |

<pre><code class="language-json hljs"># power_link.json
  {
    <span class="hljs-attr">"condition"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:scoreboard"</span>,
        <span class="hljs-attr">"objective"</span>: <span class="hljs-string">"thi_p.a"</span>,
        <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"=="</span>,
        <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number"><mark style="background-color: #c4c4c4">1</mark></span>
    },
    <span class="hljs-attr">"action"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:if_else"</span>,
        <span class="hljs-attr">"condition"</span>: {
            <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:or"</span>,
            <span class="hljs-attr">"conditions"</span>: [
                {
                    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:resource"</span>,
                    <span class="hljs-attr">"resource"</span>: <span class="hljs-string">"<mark style="background-color: #c4c4c4">thi_key_example:examples/power1</mark>_active"</span>,
                    <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"&gt;="</span>,
                    <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">1</span>
                },
                {
                    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:power"</span>,
                    <span class="hljs-attr">"power"</span>: <span class="hljs-string">"<mark style="background-color: #c4c4c4">thi_key_example:examples/power1</mark>"</span>,
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
                <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:and"</span>,
                <span class="hljs-attr">"actions"</span>: [
                    {
                        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
                        <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power grant @s <mark style="background-color: #c4c4c4">thi_key_example:examples/power1</mark>"</span>
                    },
                    {    
                        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
                        <span class="hljs-attr">"command"</span>: <span class="hljs-string">"<mark style="background-color: #c4c4c4">say activate cooldown</mark>"</span>
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
                <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power revoke @s <mark style="background-color: #c4c4c4">thi_key_example:examples/power1</mark>"</span>
            }
        }
    }
}
</code></pre>