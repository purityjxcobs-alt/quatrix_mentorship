# Supplemental Module
## Regular Expressions - RegEx
### Cleaning up the phone number no to +254 format
CTrl + H to open the find panel

    \((.*)\)

#### In the replace box 

    $1

#### Explaining the symbols;

  1. \( > it is an escape paranthesis , it looks fo a literal opening bracket in yor data eg (075)

  2. ( > second bracket , it captures the group 1

  3. .* > grabs all characters trapped in the brackets 

  4. ) > Third bracket , it closes the capture group 1

  5. \) > escapes right parathesis , it matches a literal bracket that closes the number in my data 

  6. $1 > Captures the group 1 , hence it captures group 1 deletes it and overwrites it using the new format which is +254

  ### Removing the spaces and the dashes 
  Find the box and write his command : 

        ([- ]+)(?=[0-9\-]*$)

#### Explanation of each symbol;

1. [ - ] + ) > Matches any dash or space character

2. (? = > Has allowed to select the dash or space

3. [0-9] > Means any number from 0-9

4. \- > uses a backtrack to escape a dash.

5. Asteric * >  Means zero or more quantifier    which checks the no and dashes only

6. Dollar sign $ > End of the line.   

### Changing the formart to +254
Find the fnd box and put this command;

    ;(254|0)?(\d{9})$

In the replace box input this command ;

    ;+254$2

  #### Explanation of the symbols;
  ;(254|0)?(\d{9})$

  ; > Matches the literal semicolon right infront e phone no 

  254|0 > means lost for either e digits 254 or 0

  | > its a conditional symbol

  (\d{9}) > the brackets () capture group 2

  \d{9} > matches exactly 9 digits 

  $ > end of a line

  #### replace box ; ;+254$2

;+254 , drops a fresh semicolon following the new format 

$ > It is i 2 ecause it captures the group 2 inside the second set of paranthesis 

### Generating the Usernames 

Find the find box, enter this command ;
 1st command ;

     ^(\d+);(([A-Z])[a-z]+\s([A-Z])\s(([A-Z])[a-z]+));(\+\d+)$

replace command;

    $1;$2;$7;\L$3$4$5

### Explaining each symbol.
1. ^ — Line Starting of the line
2. (\d+) — Capture Group 1 , where there is the students ID digits eg (2956)
3. ; > Literal Semicolon: Matches the first data column separator.
4. ( ) — Capture Group 2 ($2) - Encloses and saves the entire full name intact e.g ,(Yannis C Atieno).
5. [A-Z]) — Capture Group 3 ($3)> Grabs only the first uppercase letter of the first name (Y) for Yannis 
6. [a-z]+ — Matches the lowercase letters in the first name (annis).
7. \s — Whitespace Character Matches the blank space separating names.8. ([A-Z]) — Capture Group 4 ($4) > Grabs the single uppercase letter of the middle initial (C).
9. \s — Whitespace Character: Matches the blank space before the last name.
10. ( ) — Capture Group 5 ($5)> Encloses the entire last name to use for the username string eg, Atieno).
11. ([A-Z]) — Capture Group 6 ($6): Captures the first uppercase letter of the last name (A). Note: We use Group 5 instead to get the full last name.
12. [a-z]+ —  Matches the remaining lowercase letters of the last name (tieno)
13. ; — Literal Semicolon: Matches the data column separator before the phone number
14. (\+\d+) — Capture Group 7 ($7)
15. Plus sign + and all the phone number digits we formated the +254
16. $ — end of line 

Replace box ;
1. $1;$2;$7; — Re-inserts your student ID, the full name, and the cleaned phone number exactly as they were, separated by clean semicolons.
2. \L —  captures  character in a lowercase form.
3. $3$4$5 — Inputs the first name initial ($3), middle initial ($4), and the full last name ($5). Because they follow \L, they print out perfectly clean in lowercase 

NB: \L -ITS NOT SUPPORTED IN VSCODE IT GETS IGNORED SO IT CHANGES THE OUTPUT TO CAPITAL LETTERS . FROM CAPITAL LETTER, WE CHANGE WITH  SMALL LETTER COMMAND ,WHICH IS ;

Find box;

    (;[a-z])([A-Z])([A-Z])([a-z]+)$

replace box;

    $1\l$2\l$3$4

### Explaining each symbol
find box;
1. ; semicolon > Matches the final semicolon right before the username.2. ([a-z]) — Capture Group 1 ($1): Grabs the first letter of the username
3. ([A-Z]) — Capture Group 2 ($2): Grabs the second letter, which is currently an uppercase middle initial (e.g., C).
4. ([A-Z]) — Capture Group 3 ($3): Grabs the third letter, which is the uppercase first letter of the last name (e.g., A).
5. ([a-z]+) — Capture Group 4 ($4): Grabs the remaining lowercase letters of the last name (e.g., tieno).
6. $ — Ensures this only changes text at the very end of the line.

replace box;
1. $1 — Puts back the lowercase y.
2. \l$2 — The lowercase \l (lowercase 'L') tells editors that support inline switching to convert just the single next character ($2) to lowercase.
3. \l$3 — Converts the next single character ($3) to lowercase.
4. $4 — Puts back the rest of the lowercase last name.

#### Using the Sed tool 
### To remove characters such as (, ), - or spaces and later change the format to +254
### Step 1 ; Remove the brackets 

    sed -E 's/\(([0-9]+)\)/\1/g' students.txt

### Explain the symbols 
1. s (///) -The substitution pattern layout.
2. \( and \): These match literal open and close brackets. 
3. ([0-9]+): () Create a Capture Group 1.
4. [0-9] matches any single number from 0 to 9.
5. + means "match one or more of the preceding item".
6. \1: Backreferece to Capture Group 1. It puts back the numbers we memorized, effectively deleting the brackets.
7. g: The global flag. It forces sed to replace every bracket it finds on the line, not just the first one.

### Step 2 ; Removing the hypens and spaces 

    sed -E 's/([- ]+)([0-9]+)$/\2/; s/([- ]+)([0-9]+)$/\2/' students.txt

### Explain the symbols 
1. ([- ]+): This is Capture Group 1. (+)-ensures it grabs one or more
2. ([0-9]+): () - This is Capture Group 2.
3. $ ; The end of line 
4. \2: Replaces the whole match with only the contents of Capture Group 2  

### step 3 ; Changing the format to +254 

    sed -E 's/\(([0-9]+)\)/\1/g; s/([- ]+)([0-9]+)$/\2/; s/([- ]+)([0-9]+)$/\2/; s/;0?([0-9]{9})$/;+254\1/; s/;254([0-9]+)$/;+254\1/' students.txt

### Explain the symbols
Initial Line in Pattern Space: 2956;Yannis C Atieno;(0775)-705-148

 1. 's/\(([0-9]+)\)/\1/g' -  It scans the text and catches (0775). The \( and \) match the brackets. The ([0-9]+) saves 0775 into memory slot \1. It deletes the brackets and drops 0775 back down.  
                output;2956;Yannis C Atieno;0775-705-148

2. FIRST `s/([- ]+)([0-9]+)$/\2/` - The $ anchor forces sed to start scanning from the absolute end of the line. It reads backward, finds the last digits 148 (([0-9]+)$), sees the hyphen - right before them (([- ]+)), and deletes that hyphen.
a. s/ - Starts the substitution command
b. ([- ]+): Capture Group 1. Matches one or more spaces or hyphens.
c. ([0-9]+): Capture Group 2. Matches one or more digits.
d. $: End of Line Anchor
e. /\2/: Replaces the entire matched pattern with only the contents of Capture Group 2 (the digits). Group 1 (the hyphens/spaces) is deleted.
                output ; 2956;Yannis C Atieno;0775-705148

3. SECOND `s/([- ]+)([0-9]+)$/\2/` - It scans from the end ($) again. Now the final number block is 705148. It sees the remaining hyphen right before it and deletes it. The spaces separating Yannis C Atieno are 100% safe because they are not at the end of the line.              
                output ; 2956;Yannis C Atieno;0775705148

 4. `s/;0?([0-9]{9})$/;+254\1/` 
      1. s/ -substitution command 
      2. ; -Matches the literal semicolon character
      3. 0? -Matches the digit 0 zero or one time.
            -This makes the leading zero optional (it matches numbers starting with 07 or just 7
       4. ()- captures group 1 hence what is inise ths parantheis is saved in memeory so that we can reuse it using \1
       5. [0-9]- set that matches any single digit from 0 to 9.
       6. {9}-  A quantifier meaning exactly 9 times
       7. $ - end of a line
       8. ;+254 the text that will be inserted 
       9. \1 - backreference to capture group 1 , it inserted the exact 9 digits that were captured in the search step .
       10. / -closes the substition command 
                 output ; 2956;Yannis C Atieno;+254775705148
                 s








