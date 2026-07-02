# Section 4: File Organization and Navigation

#### 1. Create four new directories inside .sampledata: A-F, G-L, M-R, and S-Z.

command used ;
check your directory if youre not in the specified location use;

    mkdir -p .sampledata/A-F .sampledata/G-L .sampledata/M-R .sampledata/S-Z

if youre in the specified directory .sampledata use;

    mkdir -p A-F G-L M-R S-Z

#### Explain the commands used
mkdir flag -p  - This tells mkdir to create parent directories if they do not exist .

#### 2. Move all student data files (.txt) whose first name starts with A, B, C, D, E, or F into the A-F directory
- pattern the comand follows; 

273_Beth_K_Atieno.txt

Move names starting with A through F

    mv *_[A-F][a-z]*_*.txt A-F/ 

SYMBOLS;
- asteric * _ [A-F] matches the ID and the first letter of the first name. 
- [a-z]*_ matches the rest of the first name up to the next underscore, preventing it from checking the middle or last names.

#### 3. Move all student data files (.txt) whose first name starts with G, H, I, J, K, or L into the G-L directory.

Move names starting with G through L

    mv *_[G-L][a-z]*_*.txt G-L/   

#### 4. Move all student data files (.txt) whose first name starts with M, N, O, P, Q, or R into the M-R directory.

Move names starting with M through R   

    mv *_[M-R][a-z]*_*.txt M-R/

 #### 5. Move all remaining student data files (.txt) into the S-Z directory.

  Move all reaining students S-Z (S through Z) 

    mv *_[S-Z][a-z]*_*.txt S-Z/

#### 6. Navigate into the A-F directory using a relative path from your current location (the main directory where generate_data.sh is).
-A relative path is a way to describe the location of a file or folder starting from where you are currently standing in the terminal.
Starting from the main folder

    cd ~/quatrix-mentor

following the path into A-F 

    cd .sampledata/A-F

To verify where youre 

    pwd 

expected output ;

    /home/pkinoti/quatrix-mentor/.sampledata/A-F

#### 7. From inside the A-F directory, list all files in the S-Z directory using a relative path.
Change the directory to folder A-F

    cd A-F
List file i S-Z from inside A-F

    ls ../S-Z

Explain the commands
ls - list the contents
.. - parent directory steps up out of A-F Into .sampledata
/S-Z - steps down into the S-Z folder. 

#### 8. From your current location (still inside A-F), restore all student data files (.txt) from all the categorized directories back into the main .sampledata directory.
Change or ensure your are in the directory A-F

    cd A-F
To restore all the student data files back into the main .sampledata 

    mv * ../G-L/* ../M-R/* ../S-Z/* ../


Explain the symbols
1. mv - tranfering the files to a new desitination
2. Asteric * - Matches and selects all files inside your current folder (A-F)
3. ../G-L/* - Steps up to the parent folder (..), enters the G-L directory, and selects all files inside it
4. ../M-R/* - Steps up to the parent folder, enters the M-R directory, and selects all files inside it.
5. ../S-Z/* - Steps up to the parent folder, enters the S-Z directory, and selects all files inside it.
6. ../: The final destination path. This tells the system to drop every single collected file right into the main .sampledata parent directory.

7. To verify 

        ls 

#### 9. Search/list for files for students where the last name starts with A and scored seventy-something ie 7X e.g.. 1273_Beth_K_Atieno.txt

    grep -l -E ";7[0-9]\." *_*_*_A*.txt

Explain the symbols;
1. grep -l: Displays only the names of the files that match.
2. *_*_*_A*.txt: Searches only inside files where the student's last name starts with A (like Atieno).
3. ;7[0-9]\.": Looks specifically for a semicolon, a 7, any number from 0 to 9, and a literal decimal point 
  trail followed ; English;73.3722 
   
   - use cat to display the hidden output ;


        cat 3089_Yannis_K_Atieno.txt

#### 10. Search/list for files for students who have ...@gmail.com email addresses.

    grep -l "@gmail\.com" *.txt

Another straight forward  command ;

    grep "@gmail\.com" *.txt

- This gives you the file ame nd the actual gmail address line 

Explain the symbols;
1. grep -l: Lists only the names of the files that contain a match, rather than printing the email line itself.
2. "@gmail\.com": Searches for the text @gmail.com. The backslash \. ensures the system treats the dot as a real period, not a wildcard character.
3. *.txt: Searches through all the text files in your current directory.

#### 11.Undo the restructuring of the files ie move the files from e.g. A-F,...,S-Z back to where they were before started part (c) ie where all the files were in one folder. After you're done moving, delete the empty folders.

    rmdir A-F G-L M-R S-Z

rmdir stands for remove make directory. It instantly removes the specified folders. 
 
Verify 

    ls 

- it lists the contents of your current directory where we see only our studen.txt files and the folders A-F,G-L,M-R,S-Z are no longer visible

#### 12. Rename all files with Nate to be Nathan using: i) rename command and ii) using mv command and a bash loop of your choice and other commands you deem necessary.

filename concept ;
2748_Nate_L_Chacha.txt to 2748_Nathan_L_Chacha.txt

- first find all files with the name Nate 

.sampedata folder;
```bash
ls *_Nate_*.txt
```
main directory quatrix-mentor;

```bash
ls .sampledata/*_Nate_*.txt
```

Explain the symbols used;
1. ls is a list command that displays file inside your current directory 
2. `*` matches the student ID numbers 
3. `_Nate_` ensures it only grabs files where "Nate" is the standalone first name.
4. `*`  matches the middle initial and last name text.
5. `.txt` ensures you only see the data text files.
 
 * using the mv command and a bash loop of choice 

 - for loop 
change your directory to .sampledata since the files are there

```bash
for file in *_Nate_*.txt; do
    mv "$file" "${file/_Nate_/_Nathan_}"
done
```

Explain the command ;
1. for - starts the loop block 
2. file - this is a placeholder variable name ,one can name it anything 
3. in - a separator keyword that point the loop to the target list of items it needs to process
4. ; - A command separator. It tells Linux that this line's setup is finished and allows us to put the next keyword (do) on the same line.
5. do - the keyword that signals the start of the actual action steps
6. mv - move command
7. dollar sign - looks inside the file (actual filename)
8. "" (Double Quotes) - puts together the text
9. **`"${file/_Nate_/_Nathan_}"`** - this is a bash string substitution tool
10. file - points to the current filename
11. The first forward slash (/) tells the computer to look for what follows next (_ Nate _).
12. The second forward slash (/) acts as the swap command, replacing the target text with the final string (_Nathan _).

* To prove it changed to Nathan ;

```bash
ls *_Nathan_*.txt
```

#### 13. Rename any occurrences of Nate to Nathan in all the *.txt files and in the .test.score.csv file as well.
content concept;

```text
.sampledata/2797_Nathan_W_Wambugu.txt:Name: Nate W. Wambugu
└─────────────────┬──────────────────┘ └───────────┬─────────┘
        1. THE FILENAME                       2. THE FILE CONTENT
```
* The file content .csv
check if the name Nate exists in the .csv files 

```bash
    grep -w "Nate" .test.*.csv
```
Explain the commands;
1. grep - searches for the text inside the files 
2. -w - Matches only whole words hence it will find Nate 

*Updating the spreadsheets.csv 

    sed -i 's/\bNate\b/Nathan/g' .test.*.csv

Explaining the commands;
1. sed -i - its Opens the .csv files, edits the values, and overwrites the files in-place.
2. 's/\bNate\b/Nathan/g' - the substitution where by the name Nate is changed to Nathan
3. .test.- Targets files in your current working directory that begin with a literal period
4. Asterisk *-  A wildcard symbol that matches any middle text in the filename.

*To verify;

    grep "Nathan" .sampledata/*.txt .test.*.csv

*Changing the filename .txt from Nate to Nathan
use the for loop 

```bash
for file in *_Nate_*.txt; do
    mv "file" "{file/_Nate_/_Nathan_}"
done
```
*To verify ;

    grep "Nathan" .sampledata/*.txt .test.*.csv

#### 14. Remove any files for students with the name Joan (and be careful NOT to remove those for Joanne). Remove these lines in the csv file as well.
* Remove files and CSV lines for "Joan" (NOT "Joanne")
- To prove the existance of both Joan and Joanne

```bash
ls .sampledata/*_Joan_*.txt .sampledata/*_Joanne_*.txt
```

* Removing the individual text file for Joan

```bash
rm .sampledata/*_Joan_*.txt
```
To prove it has been deleted;

```bash
    ls .sampledata/*_Joan_*.txt
```

Explaining the commands;
1. rm: Remove utility , It permanently erases specified files from the filesystem.
2. .sampledata/ - Directs the removal tool inside the target subfolder.
3. *-A wildcard matching any text pattern
4. Joan -surrounding Joan with underscores, we lock down the selection. It explicitly targets files with _Joan_ and skips files containing

* Removing Joans row from the .csv files
-To verify the rows for both Joan and Joanne 

```bash
grep -E "_(Joan|Joanne)_|;(Joan|Joanne) " .sampledata/*.txt .test.student.csv 2>/dev/null
```
Explaining the commands;

1. grep: The text-matching tool used to search inside files and print the matching lines.
2. -E: Enables Extended Regular Expressions, which enables () and other characters
3. _ (Joan|Joanne) _ -Looks for files where the filename has _Joan_ OR _Joanne_. This isolates your individual text files. | is logical or seperator
4. ;(Joan|Joanne) : Looks for rows inside the spreadsheet where a semicolon column divider is followed by exactly Joan OR Joanne then puts them aside 
5. .sampledata/*.txt: Wildcard targeting the student text records folder.
6. .test.student.csv: Targets your hidden main database sheet.
7. 2>/dev/null -Silences any minor terminal warnings to keep your presentation professional.

* Removing the name Joan from the csv files

```bash
    sed -i '/;\bJoan\b/d' .test.student.csv
```

Explaining the symbols;
1. sed: The "Stream Editor" tool used to search and modify text patterns.
2. -i: In-place flag. It tells sed to save the changes directly back into the .test.student.csv file instead of just printing the result on your screen.
3. /'...'/: Search wrappers. Everything inside the forward slashes is the pattern sed is hunting for.
4. ;: Matches the literal semicolon right before the student's name field.
5. \b: Word Boundary - ensures the name Joan is alone
6. d: Delete - It tells sed to delete any line where the search pattern is found.
7. .test.student.csv: The exact target file name in your directory.

* To verify Joan ha been removed 

```bash
    grep ';\bJoan\b' .test.student.csv
 ```   
Explain the commands;
1. grep - searches files that matches a specific pattern
2. ';\bJoan\b': The exact same search pattern used in the sed command. It looks for a semicolon, followed by the exact, whole word "Joan".
3. .test.student.csv: The target file you are searching inside.

* To check if Joanne is still there

```bash
grep ';\bJoanne\b' .test.student.csv
```
#### 15. Navigation:
i) Navigate to the G-L folder that's inside the .sampledata folder with one command.

Step 1 ; Make the G-L directory inside .sampledata 

```bash
mkdir G-L
```
To verify it exist ;
 
 ```bash
 ls 
 ```
 To navigate into the folder inside .sampledata

 ```bash
 cd quatrix-mentor
 ```

 ```bash
 cd .sampledata/G-L
 ```
 i)) Navigate to the root directory of the mentor repo with one command.

 the path ; ~/quatrix-mentor/.sampledata/G-L , we are exactly two folders deep .
  
To navigate to the root directory ;

```bash
cd ../..
```
iii) Navigate to your home directory. Show at least two ways to do this.

What is my home directory ; /home/pkinoti:

way 1;

From your home directory (ie WITHOUT navigating away from your home directory):

List the files in the .sampledata folder.

way 2;

```bash
cd ~
```
iv)From your home directory (ie WITHOUT navigating away from your home directory):
* List the files in the .sampledata folder. 

```bash
ls ~/quatrix-mentor/.sampledata
```
* List the folder and sub-folder and files structure/hierarchy of the mentor folder using just one command.

```bash
tree ~/quatrix-mentor
```
Explanation of the output;

```text
├── supplemental
│   └── README.md
└── util
    ├── data
    │   ├── counties_file
    │   ├── domain_file
    │   ├── firstname
    │   ├── lastname
    │   ├── middleinitial
    │   ├── school_type_file
    │   └── subject_file
    ├── exam_data.sh
    ├── exam_schema.sql
    ├── generate_exam_data.sh
    └── populate_exam_database.sh
```
what every part means;

1. Supplemental Documentation - the README.md is the instruction manual for the project.
2. util/data/ - The blueprint of the database. It contains the SQL commands,

    * util - is a folder helper it holds the code, scripts or data that do routine tasks   for the main project like generating data or configuring settigs 

3. Database structure 

     1)exam_schema.sql: The blueprint that builds the database tables. eg where the schools, students and test score go .

     II)exam_data.sh: The configuration settings file it puts everything where they should be .

     III) generate_exam_data.sh: The script that creates the fake data using the ingredients above from the util/data 

     IV) Populate_exam_database.sh: The script that builds the database and fills it with the fake data. eg school database


# Section 5 : Searching Data in .test.student.csv

#### 1. Display all lines from .test.student.csv where the phone number starts with 072.
* Navigate to he .test.student.csv file and see what data is there ;

```bash
head -n 5 .test.student.csv
```

Explain the cmmands;
1. Head - reads the file from the top down and displays the first ten lines
2. -n - A flag that stands for number of lines 
3. 5 - output the first five lines
4. .test.student.csv - the tagret file that head opens and read

* Scroll through the file

```bash
less .test.student.csv
```
- press q to quit

To display all lines ;

```bash
grep -E "^[^;]+;[^;]+;072" .test.student.csv
```
explain the commands;

1018; Amber C Yebo; 0726-513-152;40;153 

1. grep - searches for file 

2. -E - Extended Reqular Expression that allows other special symbols in the input

3. ^  - start at the absolute beginning of the line (the start of Column 1). 

4. [^;] - The brackets mean "match any character inside," but the ^ inside the brackets 
means "NOT". So, this matches any character that is not a semicolon. Eg the ID 1234 

5. +-means "one or more times". Combined with the previous symbol, [^;]+ matches a continuous block of text without semicolons. This represents the entire content of Column 1 (the Student ID).

6. ; -This matches the divider separating Column 1 and Column 2.

7. [^;]+ : The exact same logic repeated. It matches one or more characters that are not semicolons, safely capturing everything inside Column 2 (the Full Name).

8. ; - matching the divider separating Column 2 and Column 3.

9. 072 - The target numbers.

#### 2. Count how many students have an email address ending with @gmail.com in .test.student.csv.

```bash
grep -c "@gmail\.com$" .test.student.csv
```
Explain the commands;
1. -c - The count flag , it outputs a dinal number representing the total matches
2. "@gmail\.com$" - the regular expression earch pattern
3. \. - means its a literal period
4. dollar sign -means the absolute end of the line 

#### 3. List the full names (second field) of all students from County ID 15 in .test.student.csv.
Pattern; 

2479;Mary L Idris;0720-620-609;15;

```bash
grep -E "^[^;]+;[^;]+;[^;]+;15;" .test.student.csv
```

#### 4.Find the student ID, full name, and email address for any student whose name contains "Olivia" (case-insensitive) in .test.student.csv.
to test if olivia is in the file ;

```bash
grep -i "olivia" .test.student.csv | wc -l

```

```bash
grep -i "amber" .test.student.csv
```
Explain the command;
1. grep - searches for the name
2. flag -i - is the insensitive flag that tells grep to ignore capitalization so any form the name is written its okay
3. amber - the tagret seach
4. .test.student.csv - the target data file 

#### 5. Display the phone numbers of all students who attend School ID 50 in .test.student.csv.

Pattern ;

1509; Edward P Kimani; 0737-011-551; 11; 50;

```bash
grep -E "^[^;]+;[^;]+;[^;]+;[^;]+;50;" .test.student.csv
```
#### 6. Count the total number of students listed in .test.student.csv (excluding any header if it existed, but your script doesn't generate one).

```bash
grep -c "^" .test.student.csv
```
Explain the command;
1. grep - searches in the files
2. -c - Count flag , lists all the total matches
3. "^" : The search pattern enclosed the ^  is the regular expression that means the start of the line hence it m,atches every line in the document .

#### 7. Find all unique domain names used in student email addresses from .test.student.csv

```bash
grep -oE "[^@;]+$" .test.student.csv | sort | uniq
```
Explain the commands;
1. grep - search utility

2. -o - Only matching flag , instead of printing the whole line the flag o prints the only exact text

3. [^@;] : means any character that is not an @ sign or a semicolon ;".

4. +- A quantifier meaning "one or more times"

5. $ - The end-of-line anchor

6. | - It redirects the list of domains from grep directly into the input of the next command.

7. sort - arranges then in an alphabetic oreder 

8. uniq - its a trash cleaner hence it removed every domain that repeatd itself and prints a clea final list of the individual domain eg if 40 papers all say gmail.com it throws 39 of them and remains with one hence one unique domain name without repeats 

# Section 6: Automation with Bash Scripting

#### 1. Create a Bash script named organize_students.zsh that performs the file organization task from Section 3 (creating the A-F, G-L, M-R, S-Z directories and moving files into them). Make sure it's executable.
step 1 ; Creating the file inside .sampledata

```bash
touch organize_students.zsh
```
step 2 ; Making it executable 

```bash
chmod +x organize_students.zsh
```
Explain the command 
1. chmod - Short form for Change Mode ,it modifies the access permissions of a file
2. +x - This add executability (+) (x) permission . it gives the system permission to run the contents of the file as code
3. restore_data.zsh - target file to change to .


```bash
cat << 'EOF' > organize_students.zsh
#!/bin/zsh

# Create the alphabet folders right here in the current directory
mkdir -p A-F G-L M-R S-Z

# Loop through all text files in the current directory
for file in *.txt(N); do
    # 1. Strip the number prefix by taking everything after the first underscore
    clean_name=$(echo "$file" | cut -d'_' -f2-)
    
    # 2. Get ONLY the first character [1] of the name and force to Uppercase (U)
    first_letter=${(U)clean_name[1]}

    # 3. Move the file into the correct local folder
    case $first_letter in
        [A-F]) mv "$file" A-F/ ;;
        [G-L]) mv "$file" G-L/ ;;
        [M-R]) mv "$file" M-R/ ;;
        [S-Z]) mv "$file" S-Z/ ;;
    esac
done
EOF
```

Explaining the command;

1. cat - it reads input from the terminal screen and passes it along

2. << - The here-document redirector symbol , its tells the terminal shell to read all the line text line i type below as i input data until i type a specific closing word

3. EOF - End of File marker word 

4. (>) - The overwrite redirector ,it takes the output processed by cat and streams it dirctly into a file replacing any old test inside that file

5. organize_student.zsh - the exact name of the file being created or overwriten on your disk.

* inside the Script File
#/bin/zsh

1. #! - the Shebang pattern marker

2. /bin/zsh the system path pointing to the zsh shell executable program ,they force the computer to launch a Zsh environment to run the code bypassing bash 

3. (#) - human to read

4. mkdir -p A-F G-L M-R S-Z - making the directories 

* for file in *.txt(N); do 

1. for file in ...; do - It picks up files one by one referening each as the variable $file and runs the code

2. *- matches any text sequence 

3. .txt - only files ending with .txt

4. (N) - The Zsh NullGlob flag , if there are no .txt it forces the lop t skip instead of crashing

*  clean_name=$(echo "$file" | cut -d'_' -f2-)

1. clean_name- Creates a brand-new storage variable in memory named clean_name.

2. $( ) - runs the command inside the paranthesis first and then save he result text output into our variable

3. echo - prints data

4. $file - the initial filename

5. | - redirects the text output from the echo command and feeds it to the next command (cut) 

6. cut - slashes section out of lineof text eg 1662_James.txt it cuts the number and the underscore for it to remain clean name James.txt.

7. -d -delimeter flag - it tells cut to split the text string everywhere it finds an underscore 

8. -f2 - he field range selection flag. It extracts everything starting from the second section through the end of the text line, dropping the leading number prefix.

##### first_letter=${(U)clean_name[1]}

1. first_letter=: Sets up a storage variable named first_letter.

2. ${ ... }: The formal shell parameter expansion syntax used to securely read and edit variable data strings.

3. (U): The Zsh internal conversion flag that forces the character to become a capital uppercase letter.

4. clean_name: References the cleaned student name text string.

5. [1]: The index position brackets. In Zsh, strings start counting at index 1. This isolates only the absolute first character of the text string (e.g., J from James).

##### case $first_letter in

1. case ... in: Opens a conditional pattern matching evaluation tree structure. It reads the string value saved in $first_letter and looks for a match listed below.
eg Is J between A-F ? NO skips
   Is J between G-L ? yes 

   since they match the mv move it there 

2. $: The evaluation operator symbol. It triggers the shell to read the raw text inside a variable rather than treating the variable name as literal text.

##### [A-F]) mv "$file" A-F/ ;;

1. [A-F]: A bracket match range layout. It matches any single uppercase letter between A and F inclusive.

2. ): Marks the end of a single pattern option condition definition block.

3. mv: The move command utility. It shifts a file package location across directories.

4. "$file": The target file being moved.

5. A-F/: The folder path destination where the file is being transferred.

6. ; ; ; erminating indicator symbol. It tells the script to stop checking other patterns and skip to the end of the case tree block.

##### ESAC

The official closing indicator for a conditional case evaluation structure. It is simply the word "case" spelled backward.

#### done

The official closing loop indicator for a programmatic for loop construction block.

#### EOF

closing marker word 

Verify the script ;

```bash
./organize_students.zsh
```

To verify it worked ;

```bash
ls A-F G-L M-R S-Z
```

#### 2. Create a Bash script named find_072_phones.zsh that searches .test.student.csv for all phone numbers starting with 072 and outputs only those phone numbers to the terminal. Make it executable.
NB ; REMEMBER TO REGENRATE THE OLD DATA SINCE WEVE DELETED IT 

Step 1 ; Creating a blank file

```bash
touch find_072_phones.zsh
```
Step 2 ; write a text 

```bash
cat << 'EOF' > find_072_phones.zsh
#!/bin/zsh

grep -o -E '\b072[0-9]+\b' .test.student.csv
EOF
```

Explain the command;
1. cat << 'EOF' > find_072_phones.zsh - where we write till we see EOF

2. #!/bin/zsh: - To use zsh to read the text

3. grep - searche for the text

4. -o - only-matching the entire long line from the book

5. 072: The exact numbers we are hunting for! The phone number must start with these three digits.

6. [0-9]+: The plus (+) means "one or more." [0-9] means any digit from 0 to 9.

Step 3 ; Make the script a real program 

```bash
chmod +x find_072_phones.zsh
```

Step 4 ; Test the script to see the numbers

```bash
./find_072_phones.zsh
```

#### 3. Create a Bash script named county_student_count.zsh that takes a county ID as its first argument and outputs the number of students from that county in .test.student.csv.

Step 1 ; Create a blank file 

```bash
touch county_student_count.zsh
```

Step 2 ; write the county ID of the students 

```bash
cat << 'EOF' > county_student_count.zsh
#!/bin/zsh

COUNTY_ID="$1"

# We changed the commas to semicolons inside the pattern!
grep -c -E "(^|;)${COUNTY_ID}(;|$)" .test.student.csv
EOF
```

Explain the commands;
1. COUNTY_ID="$1" - $1 - the first word or number when you start the program so if eg ./county_student_count.zsh 10 the umber cought is 10 

2. grep -searches in the file

3. -c - counts and prints out the actual lines of text it finds

4. (^|; and (;|$) 
being that in the data our county number is written as ;100;
    
    i) ^ - start of line

    ii) $ - end of line

    iii) , - spreadsheet comma separator

    iv) | means or 
    
This ensures if your looking for eg ; county number 10 it brings the exact no not 110 or 105

5. ${COUNTY_ID} - brings back the initial number 

Step 3 ; Make it executable 

```bash
chmod +x county_student_count.zsh
```

Step 4 ; Test out the program 

```bash
./county_student_count.zsh 10
```

#### 5. Create a Bash script named restore_data.zsh that moves all student data files (.txt) from the categorized directories (A-F, G-L, etc.) back into the main .sampledata directory and then removes the empty categorized directories. Make it executable.

Step 1 ; Create a blank file 

```bash
touch restore_data.zsh
```

Step 2 ; Write a code inside the file 

```bash
cat << 'EOF' > restore_data.zsh
#!/bin/zsh

# 1. Create the main destination folder just in case it was missing
mkdir -p .sampledata

# 2. Loop through each categorized alphabet folder
for folder in A-F G-L M-R S-Z; do
    # Check if the folder actually exists before trying to look inside it
    if [[ -d "$folder" ]]; then
        # Move all .txt files from that folder back into .sampledata
        mv "$folder"/*.txt(N) .sampledata/ 2>/dev/null
        
        # Remove the folder now that it is empty
        rmdir "$folder" 2>/dev/null
    fi
done
EOF
```

Explain the commands ;

##### if [[ -d "$folder" ]]; then
* if then opens a conditional statement block
* [[  ]] - where the test condition occurs
* -d - tests whether the variable string actually point to and anctual directory 

Step 3. Making the script Executable

```bash
chmod +x restore_data.zsh
```
Step 4 . Run the program 

```bash
./restore_data.zsh
```

#### 6. Create a Bash script named full_cleanup.zsh that runs the cleanup function from generate_data.sh and then also removes all .test.*.csv files. Make it executable.

step 1 ; Creating a file

```bash
touch full_cleanup.zsh
```

Step 2 ; Write the code 

```bash
cat << 'EOF' > full_cleanup.zsh
#!/bin/zsh

# 1. Check if the file generate_data.sh actually exists before opening it
if [[ -f ./generate_data.sh ]]; then
    source ./generate_data.sh
    cleanup
fi

# 2. Quietly wipe away all the temporary test csv files
rm -f .test.*.csv(N)
EOF
```

Explain the commands;
1. if [[ -f ./generate_data.sh ]]; then
   * -f - The file exist flag , it verifs that the .sh is a real file 

2. source ./generate_data.sh 
It opens another file and memeorises the .sh so that can use them

3. cleanup This launches the specific sequence of instructions that you just imported via the source command.

4. rm -f .test.*.csv(N)
 rm - remove the file
 -f force - it forces instant deletion 
 .csv file is the target 

5. (N): The Zsh NullGlob Mask. It tells the robot: "If the test files are already deleted, just stay completely quiet and peaceful instead of shouting an error message!"

step 2 ; Make it Executable

```bash
chmod +x full_cleanup.zsh
```

step 3; run the script 

```bash
./full_cleanup.zsh
```
To verify ;

```bash
ls .test.*.csv
```
the no file directory means it .csv file has been cleaned up .