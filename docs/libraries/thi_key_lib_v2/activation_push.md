---
title: Activation push
date: 2021-07-28
---

# Push activation
The activation type push detects the key is getting pressed and then grants the power for 1 tick. After that it will get revoked inmidietly.

<h2 style="margin-bottom: 0px;">Power file</h2>
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
<h2 style="margin-bottom: 0px;">power_link file</h2>
<h4 style="margin-bottom: 0px;">Snipit from complete file w</h4>

```json
{
  "condition": {
    "type": "apoli:scoreboard",
    "objective": "thi_p.a",
    "comparison": "==",
    "compare_to": 1
  },
  "action": {
    "type": "apoli:if_else",
    "condition": {
      "type": "apoli:or",
      "conditions": [
        {
          "type": "apoli:resource",
          "resource": "thi_key_libv2:example/power1_active",
          "comparison": ">=",
          "compare_to": 1
        },
        {
          "type": "apoli:power",
          "power": "thi_key_libv2:example/power1",
          "inverted": true
        }
      ]
    },
    "if_action": {
      "type": "apoli:if_else",
      "condition": {
        "type": "apoli:scoreboard",
        "objective": "thi_p.a.t",
        "comparison": "==",
        "compare_to": 0
      },
      "if_action": {
        "type": "origins:and",
        "actions": [
          {
            "type": "apoli:execute_command",
            "command": "power grant @s thi_key_libv2:example/power1"
          },
          {    
            "type": "apoli:execute_command",
            "command": "say activate cooldown"
          }
        ]
      }
    },
    "else_action": {
      "type": "apoli:if_else",
      "condition": {
        "type": "apoli:scoreboard",
        "objective": "thi_p.a.t",
        "comparison": "==",
        "compare_to": 1
      },
      "if_action": {
        "type": "apoli:execute_command",
        "command": "power revoke @s thi_key_libv2:example/power1"
      }
    }
  }
}
```

<h4 style="margin-bottom: 0px;">Complete file</h4>

```json
{
  "type": "apoli:multiple",
  
  "active": {
    "type": "apoli:action_over_time",
    "entity_action": {
      "type": "apoli:and",
      "actions": [
        {
          "type": "apoli:execute_command",
          "command": "function thi_key_libv2:update_slot"
        },
        {
          "type": "apoli:if_else_list",
          "actions": [
            {
              "condition": {
                "type": "apoli:scoreboard",
                "objective": "thi_p.a",
                "comparison": "==",
                "compare_to": 1
              },
              "action": {
                "type": "apoli:if_else",
                "condition": {
                  "type": "apoli:or",
                  "conditions": [
                    {
                      "type": "apoli:resource",
                      "resource": "thi_key_libv2:example/power1_active",
                      "comparison": ">=",
                      "compare_to": 1
                    },
                    {
                      "type": "apoli:power",
                      "power": "thi_key_libv2:example/power1",
                      "inverted": true
                    }
                  ]
                },
                "if_action": {
                  "type": "apoli:if_else",
                  "condition": {
                    "type": "apoli:scoreboard",
                    "objective": "thi_p.a.t",
                    "comparison": "==",
                    "compare_to": 0
                  },
                  "if_action": {
                    "type": "origins:and",
                    "actions": [
                      {
                        "type": "apoli:execute_command",
                        "command": "power grant @s thi_key_libv2:example/power1"
                      },
                      {    
                        "type": "apoli:execute_command",
                        "command": "say activate cooldown"
                      }
                    ]
                  }
                },
                "else_action": {
                  "type": "apoli:if_else",
                  "condition": {
                    "type": "apoli:scoreboard",
                    "objective": "thi_p.a.t",
                    "comparison": "==",
                    "compare_to": 1
                  },
                  "if_action": {
                    "type": "apoli:execute_command",
                    "command": "power revoke @s thi_key_libv2:example/power1"
                  }
                }
              }
            }
          ]
        },
        {
          "type": "apoli:execute_command",
          "command": "power revoke @s thi_key_libv2:activate/power"
        }
      ]
    },
    "interval": 1
  }
}

```