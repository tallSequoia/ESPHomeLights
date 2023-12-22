# Christmas Decorations

## Static
A red and green coloured sstatic bar.

```
    - addressable_lambda:
        name: "Christmas Tree - Static"
        lambda: |-
          for (int i = 0; i < it.size(); i++) {
            if (i % 2 == 1) {
              it[i] = Color(255, 0, 18, 0);
            } else {
              it[i] = Color(0, 179, 44, 0);
            }
          }
```

## Fading

Red and green, fading in and out, using the current level of the dimmer to set the maximum brightness.

```
    - addressable_lambda:
        name: "Christmas Tree - Fading"
        lambda: |-
          static int cycle_duration = 2000;  // Set the duration for a full fade cycle (in milliseconds)
          const int redColor[3] = {255, 0, 18};
          const int greenColor[3] = {0, 179, 44};

          int fade = (esp_timer_get_time() / 1000) % cycle_duration; // Convert to milliseconds
          float brightness = sin((fade * 2 * M_PI) / cycle_duration) * 0.5 + 0.5; // Sinusoidal fade function

          for (int i = 0; i < it.size(); i++) {
              int red = (1 - brightness) * redColor[0];
              int green = (1 - brightness) * redColor[1];
              int blue = (1 - brightness) * redColor[2];

              if (i % 2 == 0) {
                red = brightness * greenColor[0];
                green = brightness * greenColor[1];
                blue = brightness * greenColor[2];
              }

              it[i] = Color(red, green, blue);
          }
```

## Fading - normal speed then at a slower rate

As per above, but with 10 cycles of normal (as per "Fading") speed, then five cycles at a slower speed.
You can change the values at the top to alter:
* cycle_duration - The total time for a normal cycle (in milliseconds)
* slow_cycle_factor - The rate of the fast and slow, as a percentage of the normal cycle. Should be a whole divisor (e.g. 0.5, 0.25, 0.2)

```
    - addressable_lambda:
        name: "Christmas Tree - Fading (normal then slow)"
        update_interval: 0.1s
        lambda: |-
          const static int cycle_duration = 5000;       // Set the duration for a full fade cycle (in milliseconds)
          const static float slow_cycle_factor = 0.25;  // The factor for the slow cycles

          const int redColor[3] = {255, 0, 18};
          const int greenColor[3] = {0, 179, 44};

          int fade = (esp_timer_get_time() / 1000) % (15 * cycle_duration);            // 15 cycles in total
          float fade_speed = (fade / cycle_duration) < 10 ? 1.0 : slow_cycle_factor;   // Fade speed based on the cycle count

          float brightness = sin((fade * 2 * M_PI) / (cycle_duration * fade_speed)) * 0.5 + 0.5; // Sinusoidal fade function

          for (int i = 0; i < it.size(); i++) {
            int red = (1 - brightness) * redColor[0];
            int green = (1 - brightness) * redColor[1];
            int blue = (1 - brightness) * redColor[2];

            if (i % 2 == 0) {
              red = brightness * greenColor[0];
              green = brightness * greenColor[1];
              blue = brightness * greenColor[2];
            }

            it[i] = Color(red, green, blue);
          }
```


## String lights

Acting similarly to my shop bought christmas tree lights, using four colours in pairs and mixing them up with the normal and slow speeds as per above

```
    - addressable_lambda:
        name: "Christmas Tree - Multicolour"
        update_interval: 0.1s
        lambda: |-
          static int cycle_duration = 5000;  // Set the duration for a full fade cycle (in milliseconds)
          const float fade_speed = 0.20; // Set the fade speed

          const int colorPairs[3][2][3] = {
            {{255, 0, 0}, {0, 0, 255}},      // Red and Blue
            {{0, 255, 0}, {255, 255, 0}},    // Green and Yellow
            {{0, 255, 0}, {255, 127, 0}}   // Green and Orange
          };

          int cycleIndex = (esp_timer_get_time() / 1000) % (15 * cycle_duration); // 15 cycles with 10 fast and 5 slow for each color pair

          int pairIndex = cycleIndex / cycle_duration;
          int fade = cycleIndex % cycle_duration;

          const int *currentColorPair = colorPairs[pairIndex % 3][0];
          const int *nextColorPair = colorPairs[pairIndex % 3][1];

          float fadeDuration = (pairIndex % 15) < 10 ? cycle_duration : cycle_duration * fade_speed;
          float brightness = sin((fade * 2 * M_PI) / fadeDuration) * 0.5 + 0.5;

          for (int i = 0; i < it.size(); i++) {
            int red = (1 - brightness) * currentColorPair[0];
            int green = (1 - brightness) * currentColorPair[1];
            int blue = (1 - brightness) * currentColorPair[2];

            if (i % 2 == 0) {
              red = brightness * nextColorPair[0];
              green = brightness * nextColorPair[1];
              blue = brightness * nextColorPair[2];
            }

            it[i] = Color(red, green, blue);
          }
```
