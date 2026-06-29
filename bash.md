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
- first find all files with the name Nate 

```bash
ls *_Nate_*.txt
```
Explain the symbols used;
1. ls is a list command that displays file inside your current directory 
2. `*` matches the student ID numbers 
3. `_Nate_` ensures it only grabs files where "Nate" is the standalone first name.
4. `*`  matches the middle initial and last name text.
5. `.txt` ensures you only see the data text files.
 
 * using the mv command and a bash loop of choice 
 for loop 

```bash
for file in *_Nate_*.txt; do
    mv "file" "{file/_Nate_/_Nathan_}"
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



