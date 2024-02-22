# Flags

1D pattern representing (ish) the flag of a (UN recognised) Country

```
# 1d flags
    - addressable_lambda:
        name: "Flag - Ireland"
        lambda: |-
            // Define the 2D array representing the pattern
            static const char array_pattern[1][41] = {"GGGGGGGGGGGGGWWWWWWWWWWWWWWOOOOOOOOOOOOO"};
            static const int startPos = (int)((it.size() - sizeof(array_pattern[0])) / 2);  // Find the start, which may be negative
            static const int length = sizeof(array_pattern[0]) < it.size() ? sizeof(array_pattern[0]) : it.size();

            // Clear all other LEDs once
            if (initial_run) {
                it.all() = Color::BLACK;
            }

            // Iterate only the ones needing change
            for (int i = 0; i < length; i++) {
                if (i + startPos >= 0) {
                    switch (array_pattern[currentRow][i]) {
                        case 'O': it[i + startPos] = Color(255, 165, 0); break;
                        case 'G': it[i + startPos] = Color(0, 255,0); break;
                        case 'W': it[i + startPos] = Color::WHITE; break;
                        default: it[i + startPos] = Color::BLACK; break;
                    }
                }
            }

    - addressable_lambda:
        name: "Flag - France"
        lambda: |-
            // Define the 2D array representing the pattern
            static const char array_pattern[1][41] = {"BBBBBBBBBBBBBWWWWWWWWWWWWWWRRRRRRRRRRRRR"};
            static const int startPos = (int)((it.size() - sizeof(array_pattern[0])) / 2);  // Find the start, which may be negative
            static const int length = sizeof(array_pattern[0]) < it.size() ? sizeof(array_pattern[0]) : it.size();

            // Clear all other LEDs once
            if (initial_run) {
                it.all() = Color::BLACK;
            }

            // Iterate only the ones needing change
            for (int i = 0; i < length; i++) {
                if (i + startPos >= 0) {
                    switch (array_pattern[currentRow][i]) {
                        case 'R': it[i + startPos] = Color(255, 0, 0);; break;
                        case 'B': it[i + startPos] = Color(0, 0, 255); break;
                        case 'W': it[i + startPos] = Color::WHITE; break;
                        default: it[i + startPos] = Color::BLACK; break;
                    }
                }
            }

    - addressable_lambda:
        name: "Flag - Germany"
        lambda: |-
            // Define the 2D array representing the pattern
            static const char array_pattern[1][41] = {"             RRRRRRRRRRRRRROOOOOOOOOOOOO"};
            static const int startPos = (int)((it.size() - sizeof(array_pattern[0])) / 2);  // Find the start, which may be negative
            static const int length = sizeof(array_pattern[0]) < it.size() ? sizeof(array_pattern[0]) : it.size();

            // Clear all other LEDs once
            if (initial_run) {
                it.all() = Color::BLACK;
            }

            // Iterate only the ones needing change
            for (int i = 0; i < length; i++) {
                if (i + startPos >= 0) {
                    switch (array_pattern[currentRow][i]) {
                        case 'R': it[i + startPos] = Color(255, 0, 0); break;
                        case 'O': it[i + startPos] = Color(255, 165, 0); break;
                        default: it[i + startPos] = Color::BLACK; break;
                    }
                }
            }

            currentRow = (currentRow + 1) % patternHeight;

    - addressable_lambda:
        name: "Flag - Italy"
        lambda: |-
            // Define the 2D array representing the pattern
            static const char array_pattern[1][41] = {"GGGGGGGGGGGGGWWWWWWWWWWWWWWRRRRRRRRRRRRR"};
            static const int startPos = (int)((it.size() - sizeof(array_pattern[0])) / 2);  // Find the start, which may be negative
            static const int length = sizeof(array_pattern[0]) < it.size() ? sizeof(array_pattern[0]) : it.size();

            // Clear all other LEDs once
            if (initial_run) {
                it.all() = Color::BLACK;
            }

            // Iterate only the ones needing change
            for (int i = 0; i < length; i++) {
                if (i + startPos >= 0) {
                    switch (array_pattern[currentRow][i]) {
                        case 'R': it[i + startPos] = Color(255, 0, 0);; break;
                        case 'G': it[i + startPos] = Color(0, 255,0); break;
                        case 'W': it[i + startPos] = Color::WHITE; break;
                        default: it[i + startPos] = Color::BLACK; break;
                    }
                }
            }

```

## Template

It's possible to make your own flag pattern as a 1d or scrolling 2d pattern using this template.

'''
    - addressable_lambda:
        name: "Flag TEMPLATE 2D"
        lambda: |-
            static const Color red = Color(255, 0, 0);
            static const Color orange = Color(255, 165, 0);
            static const Color yellow = Color(255, 255, 0);
            static const Color green = Color(0, 255,0);
            static const Color blue = Color(0, 0, 255);
            static const Color purple = Color(160, 32, 240);

            // Define the 2D array representing the pattern
            static const char array_pattern[1][41] = {"GGGGGGGGGGGGGWWWWWWWWWWWWWWRRRRRRRRRRRRR"};
            static const int patternHeight = sizeof(array_pattern) / sizeof(array_pattern[0]);

            static const int startPos = (int)((it.size() - sizeof(array_pattern[0])) / 2);  // Find the start, which may be negative
            static const int length = sizeof(array_pattern[0]) < it.size() ? sizeof(array_pattern[0]) : it.size();


            // Clear all other LEDs once
            if (initial_run) {
                it.all() = Color::BLACK;
            }

            static int currentRow = 0;

            // Iterate only the ones needing change
            for (int i = 0; i < length; i++) {
                if (i + startPos >= 0) {
                    switch (array_pattern[currentRow][i]) {
                        case 'R': it[i + startPos] = red; break;
                        case 'O': it[i + startPos] = orange; break;
                        case 'Y': it[i + startPos] = yellow; break;
                        case 'G': it[i + startPos] = green; break;
                        case 'B': it[i + startPos] = blue; break;
                        case 'P': it[i + startPos] = purple; break;
                        case 'W': it[i + startPos] = Color::WHITE; break;
                        case 'X': it[i + startPos] = current_color; break;
                        default: it[i + startPos] = Color::BLACK; break;
                    }
                }
            }

            currentRow = (currentRow + 1) % patternHeight;
```

Change the colours or add in new ones to suit. Though not useful for a flag, this also allows the X value in the template to represent the current colour selected.
