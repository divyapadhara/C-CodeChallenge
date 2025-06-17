# C-CodeChallenge

•	C# Code Challenge
You’re given a string of characters that simulate how someone would type a message using an old mobile phone keypad. Here's how it works:

Each number key (2–9) has a set of letters.

E.g., key 2 types A, B, or C depending on how many times it is pressed:

1 press - A

2 presses - B

3 presses - C

You must press space (' ') to pause between two characters from the same key.

'*' means backspace.
'#' means send (end of message).

•	Objective
Turn the string input (like 4433555 555666#) into the actual message (like HELLO).

•	Step-by-Step Logic Explanation
1. Create a keypad mapping
We define a dictionary that maps each key to its letters:

        {'1', ""}, 
        {'2', "ABC"},
        {'3', "DEF"},
        {'4', "GHI"},
        {'5', "JKL"},
        {'6', "MNO"},
        {'7', "PQRS"},
        {'8', "TUV"},
        {'9', "WXYZ"},
        {'0', " "}

2. Prepare to process input
A StringBuilder to collect the final result.
A temporary list currentPresses to collect repeated presses of the same key before a pause or switch.

3. Iterate through each character
We process one character at a time:

Case A: ' ' (space)
This means we finished typing a letter (after repeated key presses).

Convert the key presses in currentPresses into a letter using our map.

Clear currentPresses.

Case B: '*' (backspace)
If we have unprocessed key presses, clear them.

Else, remove the last letter from the result.

Case C: Digit ('2'–'9')
If we're still pressing the same key, just add it to currentPresses.

If it's a new key, first convert the old sequence into a letter and add it to the result, then start a new currentPresses.

4. At the end of input
The input ends with #, so we trim it out, but if we still have a currentPresses buffer left, we convert that last sequence to a letter.

5. Convert a sequence to a letter
For example:

Pressing 2 once - A
Pressing 2 twice -  B
Pressing 2 three times - C
Pressing 2 four times - cycles back to A

How to calculate?
index = (number of times key was pressed - 1) % letters.Length
Then pick the corresponding letter from the string.

•	Example Walkthrough
Input: "4433555 555666#"
Let’s break it down:

44 - press 4 twice - H
33 - press 3 twice - E
555 - press 5 three times - L
' ' - pause
555 - press 5 three times - L
666 - press 6 three times - O
Output: "HELLO"

This logic is designed to simulate how real old mobile keypads worked accurately. Handle tricky parts like:
Pauses (spaces)
Corrections (*)
Ending marker (#)

