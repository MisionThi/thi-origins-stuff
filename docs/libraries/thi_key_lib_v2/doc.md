---
title: thi_key_library_v2
date: 2021-07-28
---

# Thi key library v2

What this library allows you to do is linking powers to a specific slot and key combination. 
By connecting the powers to the key library with a power number. Like this, you will be able to have up to 18 active powers at a time. 
These active powers can be switched to a different slot and key's in-game. Like that you can also switch out one power with another while being in-game. <br />

<h2 style="margin-bottom: 0px;">Contents</h2>
- [How do I use it?](#how-do-i-use-it)
- [Compatibility](#ompatibility)

## How do I use it?
**Step 1 - Downloading and placing in folder** <br />
The first step will be downloading the pack. After that, you will go into the `data` folder and copy the folder named `thi_key_libv2` and paste this folder into your own `data` folder next to your namespace.
<br />

**Step 2 - Creating power_link.json** <br />
After including the library in your datapack. You will create your own `namespace` with the folder named `powers` in it. When you have done this you will create the file `power_link.json`. Then copy the code below into it. 
After you have done this you replace the following path `thi_key_example:power_link` in the revoke command. To the path where the `power_link.json` is located.
This file only has to be created one time. In the future, we will only be adding to it.

<pre><code class="language-json hljs"># power_link.json
{
    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:multiple"</span>,

    <span class="hljs-attr">"active"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:action_over_time"</span>,
        <span class="hljs-attr">"entity_action"</span>: {
            <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:and"</span>,
            <span class="hljs-attr">"actions"</span>: [
                {
                    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
                    <span class="hljs-attr">"command"</span>: <span class="hljs-string">"function thi_key_libv2:update_slot"</span>
                },
                {
                    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:if_else_list"</span>,
                    <span class="hljs-attr">"actions"</span>: [



                    ]
                },
                {
                    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
                    <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power revoke @s <mark style="background-color: #c4c4c4">thi_key_example:power_link</mark>"</span>
                }
            ]
        },
        <span class="hljs-attr">"interval"</span>: <span class="hljs-number">1</span>
    }
}
</code></pre>
<br />
**Step 3 - Link your power_link.json** <br />
Now you will have to link your `power_link.json` to the thi_key_lib. You will link it in the `power_link.mcfunction` file. Which is located in `data/thi_key_libv2/functions/power_link.mcfunction`. <br />
In this function, you will add a power grant command with the path to your `power_link.json`. The command will look as followed `power grant @s thi_key_example:power_link`. <br /> <br />
`Note:` When adding compatibility for other packs that use the same library include their `/power grant` command too.

**Step 4 - Creating the power file** <br />
Inside the powers folder, you just created we will also create our power file. This file can also be in any amount of sub-folders as long as you know the path to it. In the example pack, I used a sub-folder named `examples` for organisation purposes.
<br />

**Step 5 - Choosing your activation method** <br />
You're able to choose between 3 different activation-types. <br />
Based on what you choose it will differ what you exactly add to the `power_link.json` and what you place in your power file. So remember which activation-type you will use for the next steps!

| Activation-type | Description |
|-----------------|-------------|
| [Push-activation](activation_push.md)  | This will activate the power ones when the key is pressed. |
| [Hold-activation](activation_hold.md) | This will activate the power while the key is being pressed. |
| [Toggle-activation](activation_toggle.md) | This will activate the power when you press the key ones and will de-activate it when you press it again. | <br />

<p></p>
**Step 6 - Creating base structure for the power** <br />
All the power files will need to be an `apoli:multiple` since the power files consists of several sub-powers. The file will consist of at least these 3 sub-powers. 
The contents of those sub-powers you can find on their respective pages based on which activation-type you have chosen. On those pages is also explain which pieces you will have to change. <br />
When you don't want to use a cooldown you can just remove the `apoli:execute_command` that runs say activate cooldown.

| Sub-power | Description |
|-----------|-------------|
| active | This sub-power indicates if the power is active even if the power still is granted. This resource is being checked in the `power file` as well as the `power_link.json`. |
| main | This sub-power turns off the power. It's only used in push-activation but I have it everywhere for consistency. |
| scroll_check | This sub-power checks if the slot has changed after the activation from the power. If so it will deactivate it. When this power isn't an `apoli:simple` you should replace the path from the revoke power command to the path from the location of the power file itself. |
| power | This sub-power can be called anything. For the example, I just named it power. With the condition, you find in this sub-power you can make your actions/power-types activate. |
<p></p>

**Step 7 - Linking the power to the power_link.json** <br />
Now we will be linking our power file and our power_link.json together. With this step, we will be able to make our activation-type of choice working.
If you look at the corresponding activation-type page of your choice you will see a piece of code with "code snippet for power_link.json" above it.
You will copy this into the `power_link.json` in the "apoli:if_else_list". See an example of this one the [example power_link page](example_power_link.md). <br />
When you are on the corresponding activation-type page you see that some parts are marked. This means that you have to change those values.
The table above explains what you will have to change the values. Since the structure differs per activation-type. <br />
When you don't want to use a cooldown you can just remove the `apoli:execute_command` that runs say activate cooldown.
<br />

**Step 8 - Cooldowns**
Cooldowns are handled a bit different than normal. Since we don't make use of the cooldown feature from `apoli:active_self` but rather from a resource.
I made two examples of how you can use them in the example pack. You can find the individual explanations with more in-depth information on the [cooldown page](cooldowns.md).
The two versions I made are a power specific one so all the powers have an individual resource, the other one is global this means all powers use the same cooldown, 
but the cooldown times can be different. <br />
See the [cooldown page](cooldowns.md) for info on how to implement this. Cooldowns aren't necessary to have, it's more an option.

**Step 9 - Linking the power in-game** <br />
When you have loaded the pack in your world, you can link the powers to a slot, key combination.
Below is the table you can find which scoreboard belongs to which slot and key combination. <br />
You would assign the power to a combination as followed: `scoreboard players set @s thi_ps00 1`. 
In this case, we place power 1 on the combination slot 0 and the primary key.

| Scoreboard | Slot | Key |
|------------|------|-----|
| thi_ps00 | 0 | Primary |
| thi_ps01 | 1 | Primary |
| thi_ps02 | 2 | Primary |
| thi_ps03 | 3 | Primary |
| thi_ps04 | 4 | Primary |
| thi_ps05 | 5 | Primary |
| thi_ps06 | 6 | Primary |
| thi_ps07 | 7 | Primary |
| thi_ps08 | 8 | Primary |
| thi_ps09 | 0 | Secondary |
| thi_ps10 | 1 | Secondary |
| thi_ps11 | 2 | Secondary |
| thi_ps12 | 3 | Secondary |
| thi_ps13 | 4 | Secondary |
| thi_ps14 | 5 | Secondary |
| thi_ps15 | 6 | Secondary |
| thi_ps16 | 7 | Secondary |
| thi_ps17 | 8 | Secondary 

**Step 10 - Power is implemented**
Now you can use your powers :D <br />
If you want to add more you can repeat steps 4 to 9.

## Compatibility
How does compatibility work you may ask? <br />
First of all, you will need to use different power numbers. I would recommend going with a high number so the risk of overlapping power numbers gets smaller.
When adding compatibility for each other packs you should both merge your power_link files. <br />
Located here: `thi_key_libv2\functions\power_link.mcfunction`