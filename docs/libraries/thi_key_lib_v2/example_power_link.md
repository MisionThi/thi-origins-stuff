---
title: power_link.json example
date: 2021-08-02
---

# power_link.json
The file where we link the powers to.

<h3 style="margin-bottom: 0px;">Empty version</h3>

```json
# power_link.json
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
                        
                    ]
                },
                {
                    "type": "apoli:execute_command",
                    "command": "power revoke @s thi_key_example:power_link"
                }
            ]
        },
        "interval": 1
    }
}
```

<h3 style="margin-bottom: 0px;">Filled version</h3>
This file can also be found in the example pack.

```json
# power_link.json
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
                                            "resource": "thi_key_example:examples/power1_active",
                                            "comparison": ">=",
                                            "compare_to": 1
                                        },
                                        {
                                            "type": "apoli:power",
                                            "power": "thi_key_example:examples/power1",
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
                                        "type": "apoli:and",
                                        "actions": [
                                            {
                                                "type": "apoli:execute_command",
                                                "command": "power grant @s thi_key_example:examples/power1"
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
                                        "command": "power revoke @s thi_key_example:examples/power1"
                                    }
                                }
                            }
                        },
                        
                        {
                            "condition": {
                                "type": "apoli:scoreboard",
                                "objective": "thi_p.a",
                                "comparison": "==",
                                "compare_to": 2
                            },
                            "action": {
                                "type": "apoli:if_else",
                                "condition": {
                                    "type": "apoli:power",
                                    "power": "thi_key_example:examples/power2",
                                    "inverted": true
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
                                        "type": "apoli:execute_command",
                                        "command": "power grant @s thi_key_example:examples/power2"
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
                                        "type": "apoli:and",
                                        "actions": [
                                            {
                                                "type": "apoli:execute_command",
                                                "command": "power revoke @s thi_key_example:examples/power2"
                                            },
                                            {    
                                                "type": "apoli:execute_command",
                                                "command": "say activate cooldown"
                                            }
                                        ]
                                    }
                                }
                            }
                        },
                        
                        {
                            "condition": {
                                "type": "apoli:scoreboard",
                                "objective": "thi_p.a",
                                "comparison": "==",
                                "compare_to": 3
                            },
                            "action": {
                                "type": "apoli:if_else",
                                "condition": {
                                    "type": "apoli:scoreboard",
                                    "objective": "thi_p.a.t",
                                    "comparison": "==",
                                    "compare_to": 0
                                },
                                "if_action": {
                                    "type": "apoli:if_else",
                                    "condition": {
                                        "type": "apoli:power",
                                        "power": "thi_key_example:examples/power3",
                                        "inverted": true
                                    },
                                    "if_action": {
                                        "type": "apoli:execute_command",
                                        "command": "power grant @s thi_key_example:examples/power3"
                                    },
                                    "else_action": {
                                        "type": "apoli:and",
                                        "actions": [
                                            {
                                                "type": "apoli:execute_command",
                                                "command": "power revoke @s thi_key_example:examples/power3"
                                            },
                                            {    
                                                "type": "apoli:execute_command",
                                                "command": "say activate cooldown"
                                            }
                                        ]
                                    }
                                }
                            }
                        },
                        {
                            "condition": {
                                "type": "apoli:scoreboard",
                                "objective": "thi_p.a",
                                "comparison": "==",
                                "compare_to": 4
                            },
                            "action": {
                                "type": "apoli:if_else",
                                "condition": {
                                    "type": "apoli:scoreboard",
                                    "objective": "thi_p.a.t",
                                    "comparison": "==",
                                    "compare_to": 0
                                },
                                "if_action": {
                                    "type": "apoli:if_else",
                                    "condition": {
                                        "type": "apoli:power",
                                        "power": "thi_key_example:examples/power4",
                                        "inverted": true
                                    },
                                    "if_action": {
                                        "type": "apoli:execute_command",
                                        "command": "power grant @s thi_key_example:examples/power4"
                                    },
                                    "else_action": {
                                        "type": "apoli:and",
                                        "actions": [
                                            {
                                                "type": "apoli:execute_command",
                                                "command": "power revoke @s thi_key_example:examples/power4"
                                            },
                                            {    
                                                "type": "apoli:execute_command",
                                                "command": "say activate cooldown"
                                            }
                                        ]
                                    }
                                }
                            }
                        }
                    ]
                },
                {
                    "type": "apoli:execute_command",
                    "command": "power revoke @s thi_key_example:power_link"
                }
            ]
        },
        "interval": 1
    }
}
```