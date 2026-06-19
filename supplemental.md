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

    ([- ]+)(?=\d*$)

    



