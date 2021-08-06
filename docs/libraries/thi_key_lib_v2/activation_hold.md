---
title: Hold activation-type
date: 2021-08-02
---

# Hold activation
The activation type hold detects if the key is getting pressed and then grants the power and revokes the power again when the key is being released.

<h3 style="margin-bottom: 0px;">Power file</h3>
The parts that are highlighted are the parts you should change. <br />
The structure of the file is as following:

| Sub-powers | Description |
|------------|-------------|
| `active` | This part indicates if the power is active when the power is still granted but not yet revoked. This is also the part which we will be checking for to see if the power is active as well in the <u>power.json</u> as the <u>power_link.json</u>. |
| `main` | This part will disable the power directly when it has been run once. |
| `scroll_check` | This part checks if the player scrolls away from the slot where they activated the power and automatically turns it off. In this sub-power, you should change the path of the revoke command to your path. |
| `power` | This is the part where you make your power do something. The power can be named whatever you want and there can be multiple. The condition you see in this power we use to check if the power is active or not. 

<pre><code class="language-json hljs"># power2.json
  {
  <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:multiple"</span>,

  <span class="hljs-attr">"active"</span>: {
    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:resource"</span>,
    <span class="hljs-attr">"min"</span>: <span class="hljs-number">0</span>,
    <span class="hljs-attr">"max"</span>: <span class="hljs-number">3</span>,
    <span class="hljs-attr">"start_value"</span>: <span class="hljs-number">3</span>,
    <span class="hljs-attr">"hud_render"</span>: {
        <span class="hljs-attr">"should_render"</span>: <span class="hljs-literal">false</span>
    }
  },

  <span class="hljs-attr">"main"</span>: {
    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:simple"</span>,
    <span class="hljs-attr">"condition"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:resource"</span>,
      <span class="hljs-attr">"resource"</span>: <span class="hljs-string">"*:*_active"</span>,
      <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"=="</span>,
      <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">3</span>
    }
  },

  <span class="hljs-attr">"scroll_check"</span>: {
    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:action_over_time"</span>,
    <span class="hljs-attr">"entity_action"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:and"</span>,
      <span class="hljs-attr">"actions"</span>: [
        {
          <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
          <span class="hljs-attr">"command"</span>: <span class="hljs-string">"function thi_key_libv2:check_slot"</span>
        },
        {
          <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:if_else"</span>,
          <span class="hljs-attr">"condition"</span>: {
            <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:command"</span>,
            <span class="hljs-attr">"command"</span>: <span class="hljs-string">"execute unless score @s thi_sl = @s thi_sl.n"</span>,
            <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"=="</span>,
            <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">1</span>
          },
          <span class="hljs-attr">"if_action"</span>: {
            <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:and"</span>,
            <span class="hljs-attr">"actions"</span>: [
              {
                <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
                <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power revoke @s <mark style="background-color: #c4c4c4">thi_key_example:examples/power2</mark>"</span>
              },
              {    
                <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
                <span class="hljs-attr">"command"</span>: <span class="hljs-string">"<mark style="background-color: #c4c4c4">say activate cooldown</mark>"</span>
              }
            ]
          }
        }
      ]
    },
    <span class="hljs-attr">"interval"</span>: <span class="hljs-number">1</span>
  },

  <span class="hljs-attr">"power"</span>: {
    <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:action_over_time"</span>,
    <span class="hljs-attr">"entity_action"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
      <span class="hljs-attr">"command"</span>: <span class="hljs-string">"say power 2 active"</span>
    },
    <span class="hljs-attr">"interval"</span>: <span class="hljs-number">1</span>,
    <span class="hljs-attr">"condition"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:resource"</span>,
      <span class="hljs-attr">"resource"</span>: <span class="hljs-string">"*:*_active"</span>,
      <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"&gt;="</span>,
      <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number">1</span>
    }
  }
}
</code></pre>

<h3 style="margin-bottom: 0px;">Code snipit for power_link.json</h3>
The parts that are highlighted are the parts you should change.

| Part | How to change |
|------|---------------|
| `2` | This is the power number from your power. All powers need to have a different power number! |
| `"thi_key_example:examples/power2"` | This part checks if the power is already granted, this way it knows if it should revoke or grant the power. You should change this part to the path of your power file. |
| `"power grant @s thi_key_example:examples/power2"` | This grants the power. You should change this part to the path of your power file. |
| `"power revoke @s thi_key_example:examples/power2"` | This revokes the power. You should change this part to the path of your power file. |
| `"say activate cooldown"` | Here you can trigger the cooldown. [More on cooldowns.](cooldowns.md) |

<pre><code class="language-json hljs"># power_link.json
  {
    <span class="hljs-attr">"condition"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:scoreboard"</span>,
      <span class="hljs-attr">"objective"</span>: <span class="hljs-string">"thi_p.a"</span>,
      <span class="hljs-attr">"comparison"</span>: <span class="hljs-string">"=="</span>,
      <span class="hljs-attr">"compare_to"</span>: <span class="hljs-number"><mark style="background-color: #c4c4c4">2</mark></span>
    },
    <span class="hljs-attr">"action"</span>: {
      <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:if_else"</span>,
      <span class="hljs-attr">"condition"</span>: {
        <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:power"</span>,
        <span class="hljs-attr">"power"</span>: <span class="hljs-string">"<mark style="background-color: #c4c4c4">thi_key_example:examples/power2</mark>"</span>,
        <span class="hljs-attr">"inverted"</span>: <span class="hljs-literal">true</span>
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
          <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
          <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power grant @s <mark style="background-color: #c4c4c4">thi_key_example:examples/power2</mark>"</span>
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
          <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:and"</span>,
          <span class="hljs-attr">"actions"</span>: [
            {
              <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
              <span class="hljs-attr">"command"</span>: <span class="hljs-string">"power revoke @s <mark style="background-color: #c4c4c4">thi_key_example:examples/power2</mark>"</span>
            },
            {    
              <span class="hljs-attr">"type"</span>: <span class="hljs-string">"apoli:execute_command"</span>,
              <span class="hljs-attr">"command"</span>: <span class="hljs-string">"<mark style="background-color: #c4c4c4">say activate cooldown</mark>"</span>
            }
          ]
        }
      }
    }
  }
</code></pre>