# Supplemental Module
## Regular Expressions - RegEx
### Cleaning up the phone number no to +254 format
ctrl + H TO open the fid panel

    \((.*)\)

In the replace box 

    $1

  \( > it is anescape paranthesis , it looks fo a literal opening bracket in yor data eg (075)

  ( > second bracket , it captures the group 1

  .* > grabs all characters trapped in the brackets 

  ) > Third bracket , it closes the capture group 1

  \) > escapes right parathesis , it matches a literal bracket that closes the number in my data 

  $1 > Captures the group 1 , hence it caputers 1 delete itand overwrites it usinga a clean digits 

  ### Removing the spaces and the dashes 
  find the box and write his command : 

    ([- ]+)(?=[0-9\-]*$)


 #### Explanation of each symbol;

 [ - ] + ) : Matches any dash or space character

(? = (Has allowed to select the dash or space)

[0-9\-] Means any no from 0-9

\- - uses a backtrack to escape a dash.

Asteric , Zero or more quantifier which checks the no and dashes only

$ > End of the line.   

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





