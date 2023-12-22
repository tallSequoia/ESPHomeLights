# Esphome Lights
Addressable lambda code for light effects in ESPHome.

These have been collected from various sources - no intent to take away from their initial creators is intended and please let me know so that I can provide apprporiate attribution.

# To use

e.g. for the Police Scroll effect
```
 - platform: esp32_rmt_led_strip
    chipset: SK6812
    rgb_order: GRB
    is_rgbw: True
    pin: GPIO21
    num_leds: 24
    rmt_channel: 1
    name: "LED Strip"
    effects:
    - addressable_lambda:
        name: "Police Scroll"
        update_interval: 50ms
        lambda: |-
          static uint16_t pos = 0;
          if (pos < it.size() / 2) {
            it.range(pos, pos + it.size() / 2) = Color(255, 0, 0);       //fill red
            it.range(0, pos) = Color(0, 0, 255);                         //fill blue
            it.range(pos + it.size() / 2, it.size()) = Color(0, 0, 255); //fill blue
          } else {
            it.range(pos - it.size() / 2, pos) = Color(0, 0, 255);       //fill blue
            it.range(0, pos - it.size() / 2) = Color(255, 0, 0);         //fill red
            it.range(pos, it.size()) = Color(255, 0, 0);                 //fill red
          }
          pos++;
          if (pos >= it.size()) pos = 0; //rollover

```

# Creating your own

One of the ways I have found to create these is to use Chat GPT (https://chat.openai.com/). The current free tier, using Chat GPT 3.5, has proven to be fairly reliable at creating them, thoguh it takes a few iterations and some understanding is of use. Ask for an `addressable_lambda for ESPHome`.
