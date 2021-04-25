---
title: thi_key_library
date: 2021-04-04
---

# Thi key library

What is it does is creates the possibility to have more than two active abilities on your origin. 
With this library, you will be able to have up to 18 active powers on one origin. 
The powers will be set on a specific slot and key, for example, slot 0 and primary-key

## How do I use it?

**Step 1 - Downloading and placing in folder** <br />
The first step will be downloading the datapack off course. You will be putting the datapack in the following position: 
`.minecraft/saves/<name world>/datapacks/`. <br />
When you have placed it in your datapacks folder make sure the datapack is visible in-game. 
You will be able to check this with the following command: `/datapack list` <br />
If the pack is enabled it will be visible in the first list. <br />

**Step 2 - How you can use it with your pack** <br />
When you go into the data folder from the datapack. You will see three maps in the data folder. <br />
If you want the library in your pack you only have the copy the folder named `thi_key_library`. <br />
And the `key_layer.json` from the `data/origins/origin_layers/`. When you copy those you can use
them in your pack or you could use this datapack next to yours that would also work. <br />

**Step 3 - Custom powers activation type** <br />
You will find all the power files premade with conditions in the folder named `thi_key_example` in the data folder next to the `thi_key_library` folder.
Inside the folder named `powers`, you can find files named power1 through power18. <br >
I would recomend first choosing what activation type you want to have. <br />
See [Activation possibilities](/##activation-possibilities/) for more info on that. 

## Activation possibilities
In the library, we currently have 3 activation possibilities. We have the **push**, **push-hold** and **toggle**. 
You will have to place the conditions below in the first part from the power file. <br />
primary condition in the part named -> `activation_type_primary` <br />
Secondary condition in the part named -> `activation_type_secondary`

### Push 
With the "push" activation you can click the key ones and will the power will activate.
When you hold the key the power will still only activate ones. <br />
The conditions for it are. <br />
**Primary**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/primary/push_ones",
  "comparison": "==",
  "compare_to": 1
}
```

**Secondary**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/secondary/push_ones",
  "comparison": "==",
  "compare_to": 1
}
```
<br />

### Push-hold
With the "push-hold" activation you can hold the key and the power will deactivate once you let the key go. <br />
The conditions for it are. <br />
**Primary**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/primary/push_hold",
  "comparison": "==",
  "compare_to": 1
}
```

**Secondary**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/secondary/push_hold",
  "comparison": "==",
  "compare_to": 1
}
```
<br />

### Toggle
With the "toggle" activation you press the key ones to activate and ones to deactivate. <br />
The conditions for it are. <br />
**Primary**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/primary/toggle_convert",
  "comparison": "==",
  "compare_to": 1
}
```

**Secondary**
```json
"condition": {
  "type": "origins:resource",
  "resource": "thi_key_library:resources/secondary/toggle_convert",
  "comparison": "==",
  "compare_to": 1
}
```

