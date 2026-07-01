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