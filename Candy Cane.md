# Candy Cane

A red and blue striped colour bar.

```
    - addressable_lambda:
        name: "Police scroll"
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
