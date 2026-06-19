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





