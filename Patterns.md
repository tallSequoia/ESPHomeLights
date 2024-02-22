# Half on

Turn the lights on in patterns, e.g. to save energy, using the currently selected colour and brightness

```
    - addressable_lambda:
        name: "Pattern - 20% One"
        lambda: |-
          const char* pattern = "X    ";
          for (int i = 0; i < it.size(); i++) {
            if (pattern[i % strlen(pattern)] == 'X') {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }

    - addressable_lambda:
        name: "Pattern - 25% One"
        lambda: |-
          const char* pattern = "X   ";
          for (int i = 0; i < it.size(); i++) {
            if (pattern[i % strlen(pattern)] == 'X') {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }

    - addressable_lambda:
        name: "Pattern - 33% One"
        lambda: |-
          const char* pattern = "X  ";
          for (int i = 0; i < it.size(); i++) {
            if (pattern[i % strlen(pattern)] == 'X') {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }

    - addressable_lambda:
        name: "Pattern - 50% One"
        lambda: |-
          for (int i = 0; i < it.size(); i++) {
            if (i % 2 == 1) {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }

    - addressable_lambda:
        name: "Pattern - 50% Two"
        lambda: |-
          const char* pattern = "XX  ";
          for (int i = 0; i < it.size(); i++) {
            if (pattern[i % strlen(pattern)] == 'X') {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }

    - addressable_lambda:
        name: "Pattern - 50% Three"
        lambda: |-
          const char* pattern = "XXX   ";
          for (int i = 0; i < it.size(); i++) {
            if (pattern[i % strlen(pattern)] == 'X') {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }

    - addressable_lambda:
        name: "Pattern - 75% Three"
        lambda: |-
          const char* pattern = "XXX ";
          for (int i = 0; i < it.size(); i++) {
            if (pattern[i % strlen(pattern)] == 'X') {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }

    - addressable_lambda:
        name: "Pattern - One, two, three and back"
        lambda: |-
          const char* pattern = "X XX XXX XX ";
          for (int i = 0; i < it.size(); i++) {
            if (pattern[i % strlen(pattern)] == 'X') {
              it[i] = current_color;
            } else {
              it[i] = Color::BLACK;
            }
          }          

```
