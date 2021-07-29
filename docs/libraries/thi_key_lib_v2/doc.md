---
title: thi_key_library_v2
date: 2021-07-28
---

# Thi key library v2
<br />

What this library allows you to do is linking powers to a specific slot and key combination. 
By connecting the powers to the key library with a power number. Like this, you will be able to have up to 18 active powers at a time. 
These active powers can be switched to a different slot and key's in-game. Like that you can also switch out one power with another while being in-game. <br />
<br />
## Contents
- [How do I use it?](#how-do-i-use-it)
- [Activation types](#activation-types)


## How do I use it?
**Step 1 - Downloading and placing in folder** <br />
The first step will be downloading the pack. After that, you will go into the `data` folder and copy the folder named `thi_key_libv2` and paste this folder into your own data folder next to your namespace. <br />
<br />
**Step 2 - Connecting powers to the key library** <br />
tesr

<br />
## Activation types
- [Push activation](#push-activation) <br />
- [Hold activation](#hold--activation) <br />
- [Toggle activation](#toggle-activation) <br />
- [Toggle activation¹](#toggle-activation) <br /> 

We have four different activation types at the moment. 
When deciding your activation type you will need to place different pieces of code in 2 different locations. In the `power file` and your `power_link file`. The combination of those two pieces will create the activation type. <br />
¹ The power doesn't get turned off when you scroll <br />
<br />


#### Hold activation
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
<br />

#### Toggle activation
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
<br />

#### Toggle activation
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


## Compatibility