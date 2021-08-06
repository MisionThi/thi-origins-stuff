---
title: Cooldowns
date: 2021-08-03
---

# Cooldowns
Cooldowns are an option that you can use for your powers.

<h2 style="margin-bottom: 0px;">Contents</h2>
- [Power specific cooldown](#power-specific-cooldown)
- [Global cooldown](#global-cooldown)
- [Custom cooldown](custom-cooldown)

### Power specific cooldown

<h6 style="margin-bottom: 0px;">Step 1 - Create the cooldowns</h6>
First a thing that's the same for both cooldown methods. You will have to make sure you have linked the cooldown file to your origin.
Now lets create an power file I will name mine `cooldowns_power_specific.json` you create this file in your own namespace.

Here you see how my `cooldowns_power_specific.json` looks like.

| Sub-powers | Explaination |
|------------|--------------|
| add | This sub-power checks if you have activated the cooldown, if it's active we will add 1 to the resource untill it's full. |
| 1r | This sub-power is one of the resource cooldowns. I named it `1r` this way I know it's the resource from power1, the sub power can be named anything you want. When you look at the sub-power you can see that the max of the resource 10 is in this case it means 10 seconds since the interval from `add` 20 is. When the resource reaches it's max it get reset to 0 again.<br/> The hud_render in here you can change the resource bar and the condition for when the resource should show. Right now it shows when the cooldwons is active (resource above 1). |
| 2r | This sub-power is one of the resource cooldowns. I named it `2r` this way I know it's the resource from power2, the sub power can be named anything you want. When you look at the sub-power you can see that the max of the resource 10 is in this case it means 50 seconds since the interval from `add` 20 is. When the resource reaches it's max it get reset to 0 again.<br/> The hud_render in here you can change the resource bar and the condition for when the resource should show. Right now it shows when the cooldwons is active (resource above 1). |
| ... | Like the two above you can create as many individiual cooldowns you need. Just don't forget to add it to the `add` sub-power too.

```json
# cooldowns_power_specific.json
{
    "type": "apoli:multiple",
    
    "add": {
        "type": "apoli:action_over_time",
        "entity_action": {
            "type": "apoli:and",
            "actions": [
                {
                    "type": "apoli:if_else",
                    "condition": {
                        "type": "apoli:resource",
                        "resource": "*:*_1r",
                        "comparison": ">=",
                        "compare_to": 1
                    },
                    "if_action": {
                        "type": "apoli:change_resource",
                        "resource": "*:*_1r",
                        "change": 1
                    }
                },
                {
                    "type": "apoli:if_else",
                    "condition": {
                        "type": "apoli:resource",
                        "resource": "*:*_2r",
                        "comparison": ">=",
                        "compare_to": 1
                    },
                    "if_action": {
                        "type": "apoli:change_resource",
                        "resource": "*:*_2r",
                        "change": 1
                    }
                }
            ]
        },
        "interval": 20
    },
    
    "1r": {
        "type": "apoli:resource",
        "min": 0,
        "max": 10,
        "max_action": {
            "type": "apoli:delay",
            "ticks": 20,
            "action": {
                "type": "apoli:change_resource",
                "resource": "*:*_1r",
                "change": -10
            }
        },
        "hud_render": {
            "sprite_location": "origins:textures/gui/resource_bar.png",
            "bar_index": 1,
            "should_render": true,
            "condition": {
                "type": "apoli:resource",
                "resource": "*:*_1r",
                "comparison": ">=",
                "compare_to": 1
            }
        }
    },

    "2r": {
        "type": "apoli:resource",
        "min": 0,
        "max": 50,
        "max_action": {
            "type": "apoli:delay",
            "ticks": 20,
            "action": {
                "type": "apoli:change_resource",
                "resource": "*:*_2r",
                "change": -50
            }
        },
        "hud_render": {
            "sprite_location": "origins:textures/gui/resource_bar.png",
            "bar_index": 1,
            "should_render": true,
            "condition": {
                "type": "apoli:resource",
                "resource": "*:*_2r",
                "comparison": ">=",
                "compare_to": 1
            }
        }
    }
}
```

<h6 style="margin-bottom: 0px;">Step 2 - Call the cooldowns</h6>
As you could have noticed when you were setting up the other files. There sometimes was a `apoli:execute_command` that runs `say activate cooldown` you can find those in the power_link.json and in your power.json if you used the activation-type hold and toggle if you choose for the auto deactivate option when the player scrolled. <br />
If you want to activate the cooldown you place the following command in to the `apoli:execute_command` `resource set @s thi_key_example:cooldowns_power_specific_1r 1` instead of `say activate cooldown`.


<h6 style="margin-bottom: 0px;">Step 3 - Use the cooldowns</h6>
For using the cooldown you go to the power_link.json. The only thing is that the conditions should be on different places based on the activation-type.
That's why I will show you some snipets from what you currently have and how it should be edited when using the cooldown.

<p style="margin-bottom: 0px;"><b>Push activation-type</b></p>

```json
# A snippet from power1.json
# Without cooldown condition

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
```

```json
# A snippet from power1.json
# With cooldown condition

"type": "apoli:if_else",
"condition": {
    "type": "apoli:and",
    "conditions": [
        {
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
        {      
            "type": "apoli:resource",
            "resource": "thi_key_example:cooldowns_power_specific_1r",
            "comparison": "==",
            "compare_to": 0
        }
    ]
},
```

<br />
<p style="margin-bottom: 0px;"><b>Hold activation-type</b></p>

```json
# A snippet from power2.json
# Without cooldown condition

"condition": {
    "type": "apoli:scoreboard",
    "objective": "thi_p.a",
    "comparison": "==",
    "compare_to": 2
},
```

```json
# A snippet from power2.json
# With cooldown condition

"condition": {
    "type": "apoli:and",
    "conditions": [
        {
            "type": "apoli:scoreboard",
            "objective": "thi_p.a",
            "comparison": "==",
            "compare_to": 2
        },
        {      
            "type": "apoli:resource",
            "resource": "thi_key_example:cooldowns_power_specific_2r",
            "comparison": "==",
            "compare_to": 0
        }
    ]
},
```

<br />
<p style="margin-bottom: 0px;"><b>Toggle activation-type</b></p>

```json
# A snippet from power3.json
# Without cooldown condition

"condition": {
    "type": "apoli:scoreboard",
    "objective": "thi_p.a",
    "comparison": "==",
    "compare_to": 3
},
```

```json
# A snippet from power3.json
# With cooldown condition

"condition": {
    "type": "apoli:and",
    "conditions": [
        {
            "type": "apoli:scoreboard",
            "objective": "thi_p.a",
            "comparison": "==",
            "compare_to": 3
        },
        {      
            "type": "apoli:resource",
            "resource": "thi_key_example:cooldowns_power_specific_3r",
            "comparison": "==",
            "compare_to": 0
        }
    ]
},
```

<br />

### Global cooldown
<h6 style="margin-bottom: 0px;">Step 1 - Create the cooldowns</h6>
First a thing that's the same for both cooldown methods. You will have to make sure you have linked the cooldown file to your origin.
Now lets create an power file I will name mine `cooldowns_power_global.json` you create this file in your own namespace.

Here you see how my `cooldowns_power_global.json` looks like.

| Sub-powers | Explaination |
|------------|--------------|
| change | This sub-power checks if you have activated the cooldown, if it's active we will remove 1 to the resource untill the resource reaches 0. |
| global | This sub-power is one of the resource cooldown. |


```json
# cooldowns_power_global.json
{
    "type": "apoli:multiple",
    
    "change": {
        "type": "apoli:action_over_time",
        "entity_action": {
            "type": "apoli:if_else_list",
            "actions": [
                {
                    "condition": {
                        "type": "apoli:resource",
                        "resource": "*:*_global",
                        "comparison": ">=",
                        "compare_to": 1
                    },
                    "action": {
                        "type": "apoli:change_resource",
                        "resource": "*:*_global",
                        "change": -1
                    }
                }
            ]
        },
        "interval": 20
    },
    
    "global": {
        "type": "apoli:resource",
        "min": 0,
        "max": 10,
        "hud_render": {
            "sprite_location": "origins:textures/gui/resource_bar.png",
            "bar_index": 1,
            "should_render": true,
            "condition": {
                "type": "apoli:resource",
                "resource": "*:*_global",
                "comparison": ">=",
                "compare_to": 1
            }
        }
    }
}
```

<h6 style="margin-bottom: 0px;">Step 2 - Call the cooldowns</h6>
As you could have noticed when you were setting up the other files. There sometimes was a `apoli:execute_command` that runs `say activate cooldown` you can find those in the power_link.json and in your power.json if you used the activation-type hold and toggle if you choose for the auto deactivate option when the player scrolled. <br />
If you want to activate the cooldown you place the following command in to the `apoli:execute_command` `resource set @s thi_key_example:cooldowns_power_global_global 10` instead of `say activate cooldown`.
The 10 means that the cooldown will be 10 sec before the bar reaches 0 and the powers can be used again.

<h6 style="margin-bottom: 0px;">Step 3 - Use the cooldowns</h6>
For using the cooldown you go to the power_link.json. The only thing is that the conditions should be on different places based on the activation-type.
That's why I will show you some snipets from what you currently have and how it should be edited when using the cooldown.
<p style="margin-bottom: 0px;"><b>Push activation-type</b></p>

```json
# A snippet from power1.json
# Without cooldown condition

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
```

```json
# A snippet from power1.json
# With cooldown condition

"type": "apoli:if_else",
"condition": {
    "type": "apoli:and",
    "conditions": [
        {
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
        {      
            "type": "apoli:resource",
            "resource": "thi_key_example:cooldowns_power_global_global",
            "comparison": "==",
            "compare_to": 0
        }
    ]
},
```

<br />
<p style="margin-bottom: 0px;"><b>Hold activation-type</b></p>

```json
# A snippet from power2.json
# Without cooldown condition

"condition": {
    "type": "apoli:scoreboard",
    "objective": "thi_p.a",
    "comparison": "==",
    "compare_to": 2
},
```

```json
# A snippet from power2.json
# With cooldown condition

"condition": {
    "type": "apoli:and",
    "conditions": [
        {
            "type": "apoli:scoreboard",
            "objective": "thi_p.a",
            "comparison": "==",
            "compare_to": 2
        },
        {      
            "type": "apoli:resource",
            "resource": "thi_key_example:cooldowns_power_global_global",
            "comparison": "==",
            "compare_to": 0
        }
    ]
},
```

<br />
<p style="margin-bottom: 0px;"><b>Toggle activation-type</b></p>

```json
# A snippet from power3.json
# Without cooldown condition

"condition": {
    "type": "apoli:scoreboard",
    "objective": "thi_p.a",
    "comparison": "==",
    "compare_to": 3
},
```

```json
# A snippet from power3.json
# With cooldown condition

"condition": {
    "type": "apoli:and",
    "conditions": [
        {
            "type": "apoli:scoreboard",
            "objective": "thi_p.a",
            "comparison": "==",
            "compare_to": 3
        },
        {      
            "type": "apoli:resource",
            "resource": "thi_key_example:cooldowns_power_global_global",
            "comparison": "==",
            "compare_to": 0
        }
    ]
},
```

### Custom cooldown
You can also make your own version from the cooldown system like combining the two or something completely different.
As long as you remember where to call the cooldowns and where to place the conditions.