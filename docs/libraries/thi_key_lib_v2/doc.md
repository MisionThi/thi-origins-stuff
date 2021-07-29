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
- [Activation types](#activation-types)

## How do I use it?
**Step 1 - Downloading and placing in folder** <br />
The first step will be downloading the pack. After that, you will go into the `data` folder and copy the folder named `thi_key_libv2` and paste this folder into your own data folder next to your namespace. <br />
<br />
**Step 2 - Connecting powers to the key library** <br />
test


## Activation types
- [Push activation](activation_push.md) <br />
- [Hold activation](activation_hold.md) <br />
- [Toggle activation](activation_toggle.md) <br />

We have four different activation types at the moment. 
When deciding your activation type you will need to place different pieces of code in 2 different locations. In the `power file` and your `power_link file`. The combination of those two pieces will create the activation type. <br />

<h4 style="margin-bottom: 0px;">power file</h4>
First of all, all the power files are recommended to be an `apoli:multiple` since that makes the activation process a lot easier!
In the `apoli:multiple` you have first the `active` sub-power underneath that you have the `main`, `scroll_check` and last you can create the sub-powers that you use to make something happen.
More in-depth information on how to add it you can find on the individual pages from the [activation types](#activation-types).

<h4 style="margin-bottom: 0px;">power_link file</h4>
For every power you want to add to you have to add an piece of code in the `apoli:if_else_list`. You only have to edit little parts of this. This explained more indept on the individual pages from the [activation types](#activation-types).

## Compatibility