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
12. [a-z]+ —  Matches the remaining lowercase letters of the last name (tieno).
13. ; — Literal Semicolon: Matches the data column separator before the phone number
14. (\+\d+) — Capture Group 7 ($7): Matches and saves the literal + and all the phone number digits you cleaned in the previous step eg,  (+254775705148)
$ — end of line 

Replace box ;
1. $1;$2;$7; — Re-inserts your student ID, the full name, and the cleaned phone number exactly as they were, separated by clean semicolons.
2. \L —  captures  character in a lowercase form.
3. $3$4$5 — Inputs the first name initial ($3), middle initial ($4), and the full last name ($5). Because they follow \L, they print out perfectly clean in lowercase 

NB: \L -ITS NOT SUPPORTED IN VSCODE IT GETS IGNORED SO IT CHANGES THE OUTPUT TO CAPITAL LETTERS . FROM CAPITAL LETTER, WE CHANGE WITH  SMALL LETTER COMMAND ,WHICH IS ;

Find box;

    (;[a-z])([A-Z])([A-Z])([a-z]+)$

    Replace box ;
    
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