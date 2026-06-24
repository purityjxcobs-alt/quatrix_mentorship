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

Move names starting with A through F

    mv *_[A-F]*.txt A-F/

    SYMBOLS;
    1 st * Matches the student ID number 
    2 nd * Matches the rest of the firstname and the last name 
    .txt Extension 

#### 3. Move all student data files (.txt) whose first name starts with G, H, I, J, K, or L into the G-L directory.

Move names starting with G through L

    mv *_[G-L]*.txt G-L/


#### 4. Move all student data files (.txt) whose first name starts with M, N, O, P, Q, or R into the M-R directory.

Move names starting with M through R   

    mv *_[M-R]*.txt M-R/

 #### 5. Move all remaining student data files (.txt) into the S-Z directory.

  Move all reaining students S-Z (S through Z) 

    mv *.txt S-Z/

#### 6. Navigate into the A-F directory using a relative path from your current location (the main directory where generate_data.sh is).
-A relative path is a way to describe the location of a file or folder starting from where you are currently standing in the terminal.
Starting from the main folder

    cd ~/quatrix-mentor

following the path into A-F 

    cd .sampledata/A-F

To verify where youre 

    pwd 

expected output ;

    /home/pkinoti/quatrix-mentor/.sampledata/.sampledata/A-F

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
    mv ../*/*.txt ..

Explain the symbols
mv - tranfering the files to a new desitination
.. - parent directory , since we are inside A-F we move to .sampledata
1st * - matches any subfoldername inside .sampledata 
2nd * - matches any file name that ends with .txt
Final .. - this is the destination path into .sampledata

To verify 

    ls 




 

