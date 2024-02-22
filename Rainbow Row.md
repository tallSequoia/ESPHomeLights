# Rainbow row

Like the inbuilt Rainbow, but all are on at a time

Modify the update interval as needed.

```
    - addressable_lambda:
        name: "Rainbow Row"
        update_interval: 200ms
        lambda: |-
          static const float steps = 150;     // Change to make it take longer.
          static uint32_t position = 0;

          uint32_t hue = static_cast<uint32_t>(position / steps * 255.0);

          it.all() = ESPHSVColor(hue, 255, 255);

          position++;
          if (position > steps) position = 0;
```
