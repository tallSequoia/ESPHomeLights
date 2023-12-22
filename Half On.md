# Half on

Turn every other light on, using the currently selected colour and brightness

```
    - addressable_lambda:
        name: "Half on"
        lambda: |-
          for (int i = 0; i < it.size(); i++) {
          if (i % 2 == 1) {
            it[i] = current_color;
          } else {
            it[i] = Color(0, 0, 0, 0);
          }
        }
```
