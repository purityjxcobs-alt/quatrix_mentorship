# Module: Bash/Zsh 101 – Learning the Basics

## 1. Core Shell Concepts & Relevance

### Why the Command-Line Interface (CLI) is Crucial
*   **Server Administration:** Production environments typically run **"headless"** (without a monitor or graphical interface) to save system CPU and RAM. All upgrades, patches, and configurations must be handled via text.
*   **File Manipulations:** Running massive batch actions (like mass renaming, sorting, or structural sweeping) takes seconds with a single line of text.
*   **Automation Using Scripting:** CLI actions can easily be written into script files (`.sh` or `.zsh`) to execute repetitive maintenance or data pipelines automatically without human intervention.

### Concept Questions & Answers

#### **What is Bash? What alternatives are there to Bash?**
**Bash** (Bourne Again SHell) is an interactive command language interpreter and text wrapper interface for Unix and Linux operating systems. It parses the commands you type and instructs the computer's kernel to act on them.
*   *Alternatives:* `sh` (Bourne Shell), `zsh` (Z Shell), `fish` (Friendly Interactive Shell), `ksh` (Korn Shell), and `dash`.

#### **What is Zsh?**
**Zsh** is a powerful, highly customizable evolution of Bash. It incorporates the core features of Bash while natively adding advanced quality-of-life upgrades such as context-aware tab auto-completion, contextual spelling correction, shared command histories across active windows, and extensive themes (via frameworks like Oh My Zsh). It is the default shell on modern macOS installations.

#### **Why use an "archaic dark screen" instead of modern Graphical User Interfaces (UIs)?**
While graphical UIs excel at basic visual inspections and mouse navigation, they fall short for professional engineering and system workflows because:
1.  **UIs Cannot Be Easily Automated:** You cannot reliably record mouse-clicks or drag-and-drop operations into an automated backend script to run safely at midnight.
2.  **Scale and Speed Constraints:** Dragging 5,000 specific files out of a directory containing 100,000 items will freeze or crash a visual file explorer window. A single targeted command filters and moves them instantly.

---

## 2. File System Architecture & Navigation Paths

###  Navigation Questions & Answers

#### **What is a user's home directory? How does one navigate to it quickly?**
The **home directory** is a user’s isolated personal sandbox storage layout. Regular users lack permission to modify root operating system configurations but retain full administrative rights within their home folder.
*   **Linux Path:** `/home/yourusername`
*   **macOS Path:** `/Users/yourusername`
*   **Quick Navigation Shortcuts:** Type `cd` with no parameters and hit Enter, or execute `cd ~` (the tilde character `~` is the universal shorthand symbol for your home folder).

### Understanding Paths

All elements in a Linux file system live underneath a single base folder called the **Root Directory**, denoted simply by a single forward slash (`/`).

*   **Absolute Path:** Specifies the complete, uncompromising route mapped all the way from the base root directory (`/`). It always begins with a forward slash.
    *   *Example:* `/home/jdoe/Documents/git/mentor`
*   **Relative Path:** Specifies a location **relative to your current terminal position**. It does *not* begin with a forward slash.
    *   *Example:* If your terminal is sitting inside `/home/jdoe`, the relative path is simply `Documents/git/mentor`.
*   **Directory Shorthand Notation:**
    *   `.` (Single period): Represents the directory you are currently standing in.
    *   `..` (Double period): Represents the parent directory (moves your path one folder step backward).

---

##  3. Command Reference & Explanations

###  Standard Navigation and Inspection

#### **`ls` (List)**
Displays the names of files and directories within a target path.
*   `ls` *(No arguments)*: Lists visible items in the current workspace.
*   `ls -l`: Activates the **long listing format**, displaying detailed file attributes.
*   `ls -a`: Forces the display of **all files**, including hidden system/configuration files (any item beginning with a dot, like `.git` or `.bashrc`).
*   `ls -la` (or `ls -al`): Combines flags to cleanly display long-list details for every file, including hidden items.
*   `ls Documents/git/mentor`: Explores the contents of a targeted path parameter instead of the current working directory.

>  **Decoding the Long Listing Format (`ls -l` columns output):**
> Target example: `drwxr-xr-x 2 jdoe jdoe 4096 Apr 9 19:53 bash`
> 
> 1. **Column 1 (`drwxr-xr-x`): Type & Permissions.** 
>    * First slot indicates file type: `d` = Directory/Folder; `-` = Standard File.
>    * Next 9 slots map out security rights split into 3 groups of 3 characters (`r`=read, `w`=write, `x`=execute): Owner rights (`rwx`), Group rights (`r-x`), and Public/World rights (`r-x`).
> 2. **Column 2 (`2`): Hard Link Count.** The number of hard links pointing down to this file asset.
> 3. **Column 3 (`jdoe`): File Owner.** The username of the account that controls the resource.
> 4. **Column 4 (`jdoe`): Group Owner.** The user-group assigned to the file.
> 5. **Column 5 (`4096`): File Size.** The size footprint recorded strictly in bytes.
> 6. **Column 6 (`Apr 9 19:53`): Timestamp.** The exact date and time this resource was last altered.
> 7. **Column 7 (`bash`): Name.** The physical name of the file or directory.

#### **Test Question Solutions (Using flags from `man ls`):**
*   *List only folders in the current folder using the long listing format:*
    ```bash
    ls -ld */
    ```
*   *List all files/folders (including hidden) sorted by newest first (oldest at the bottom):*
    ```bash
    ls -lat
    ```

#### **`cd` (Change Directory)**
Alters your active terminal location to a new folder path parameter.
*   `cd` *(No arguments)*: Instantly brings you back to your profile's home directory (`~`).
*   `cd Documents/git/mentor/`: Moves you deep down into the specified subfolder path.
*   `cd ..`: Steps you back out into the parent container directory.

#### **`pwd` (Print Working Directory)**
Outputs the absolute structural path of the folder you are currently standing inside.

#### **`man` (Manual)**
The built-in documentation reader interface.
*   *Example:* Running `man ls` opens the explicit manual user guide detailing all functional features for the `ls` engine.

---

###  Data Filtering & Extraction

#### **`grep` (Global Regular Expression Print)**
Scans text documents line-by-line, instantly outputting rows containing a precise match string pattern.
*   *Example:* `grep Nate ~/Documents/git/mentor/.test.student.csv` isolates and outputs only the rows containing the name "Nate" within that specific hidden spreadsheet.

---

### ⚖️ The Output Matrix: Reading Content Differently
It is vital to use the correct tool based on the scale of the document you are reading:

| Command | Operational Mechanism | Best Use Case |
| :--- | :--- | :--- |
| **`cat`** | Dumps the entire contents of a file directly onto the terminal screen sequentially. | Small files (e.g., viewing a short configuration). *Avoid using on massive logs.* |
| **`less`** | Opens an interactive reader screen allowing you to scroll, page, or search text dynamically. | Large files and massive databases. Press `/` to search text and `q` to close. |
| **`head`** | Extracts and prints strictly the **first 10 lines** from the very top of a target document. | Quickly checking header columns or metadata setups at the start of logs. |
| **`tail`** | Extracts and prints strictly the **last 10 lines** from the basement floor of a target document. | Checking recent server activity or error crashes at the end of log outputs. |

*   *Wildcard Output Example (`cat data/*`):* Tells the engine to dynamically merge and stream every file nested inside the data directory onto your screen simultaneously.

---

### File Manipulation & Searching

#### **`cp` (Copy)**
Creates an identical duplicate of a source document or directory array and outputs it to a defined target path.
*   *Example with Wildcard characters:* `cp ~/Documents/git/mentor/.sampledata/31??_* ~/Documents/bash-sandbox/test_folder`
    *   The `?` token represents exactly *one* wildcard character, and `*` matches *any* string of characters.
*   **The `-r` Recursive Option:** `cp -r source/ destination/`
    *   Mandatory flag when copying folders. It forces the system to dive down into the directory and duplicate all files, folders, and inner structures nested inside it.

#### **`find` (Locate Files)**
Actively crawls down structural system directories to track down resources matching distinct attribute requirements.
*   *Example 1:* `find ~/Documents/ -type f -name '*Zippy*'` ➡️ Searches your Documents space exclusively for standard files (`-type f`) carrying the phrase "Zippy" anywhere in their name string.
*   *Example 2:* `find ~/Documents/git/ -type d -name '*-*'` ➡️ Restricts the search layout to directory blocks (`-type d`) that contain a hyphen symbol in their name.

---

### Glossary of Essential Commands

*   **`history` \***: Pulls up a numbered log of every terminal command executed in your user session.
*   **`echo` \***: Evaluates arguments and prints strings of text directly onto the standard terminal window stream.
*   **`mkdir` \***: Creates a fresh, empty directory workspace container at a chosen location (e.g., `mkdir project_folder`).
*   **`mv` \***: Moves a file or folder to a new location. Also serves as the standard tool to **rename** files.
*   **`rm`**: Destroys files completely. Using `rm -r` deletes entire directory configurations. *(Caution: Terminal deletions skip the Trash bin and are permanent).

##  4. Advanced Commands, Pipes & Wildcards

###  Deep-Dive Command Reference

#### **`sed` (Stream Editor)**
Parses, filters, and transforms streams of text dynamically. It alters text within files line-by-line without opening a visual text application window.

#### **`vi` / `vim`**
Terminal-native, keyboard-driven text editors. `vim` (Vi Improved) provides upgrades like syntax highlighting.
*   *Troubleshooting:* If `vi` fails to execute, install the updated variant by running:
    ```bash
    sudo apt install vim
    ```

#### **`ssh-keygen`**
Generates high-level cryptographic secure authentication parameter tokens (the Private/Public SSH key matrices) used for passwordless login security.

#### **`tree`**
Outputs a visual structural tree schematic displaying all subdirectories and file hierarchies nested inside your current folder path.

#### **`scp` (Secure Copy)**
Transfers files securely back and forth between distinct network computers using standard SSH connections.

#### **`rsync` (Remote Sync)**
A powerful file sync tool that analyzes the destination folder and copies **only the differences** (modified file bytes) between source and target, maximizing transmission efficiency.

#### **`awk`**
A robust pattern scanning and data extraction language used frequently to isolate and edit individual structural data columns from standard output files.

#### **`unzip`**
Decompresses standard `.zip` archive files, restoring them back to standard operational directory formats.

#### **`tar` (Tape Archive)**
Combines multiple files and full structural directory trees into a single archive file block (`.tar`), or compiles heavily compressed archives (`.tar.gz`).

#### **`wget`**
A non-interactive network downloader utility used to pull files, applications, and assets down directly from web URLs.

#### **`curl` (Client URL)**
Transfers data to or from a network server using various protocols (HTTP, HTTPS, FTP). It is highly versatile and used to interact with data APIs or post server information.

#### **`printf`**
Formats and prints string text to the console window layout with advanced alignment controls compared to standard `echo`.

---

###  5. Advanced Mechanics: Pipes & Wildcards

### The Pipe Operator (`|`)
The pipe takes the screen output from the command running on its left and passes it directly as the input text data stream for the command on its right. You can stitch several pipes together sequentially to build deep analytical data filters.

*   *Example Workflow:*
    ```bash
    history | grep find
    ```
    *Explanation:* The shell first gathers your total command history list. Instead of dumping thousands of rows onto your view, the pipe catches that text and hands it to `grep find`, which filters and displays only the historical lines containing the word "find".

---

### Wildcard Matching Mechanisms
Wildcards are structural shortcuts used to select groups of files or directories based on character patterns.

#### **1. The Asterisk Wildcard (`*`)**
Matches **any string of characters** of any length, including zero characters.

*   `ls *`: Lists every file and folder in the current active directory.
*   `ls s*`: Filters for items starting strictly with the character `s`.
*   `ls *l`: Filters for items that end with the letter `l`.
*   `ls *pp*`: Isolates items that contain the dual characters `pp` anywhere within their name.
*   `ls -lda ~/Documents/git/mentor/*l*`: Deep searches the specific path target folder for files or subdirectories containing the letter `l` anywhere in their titles.

#### **2. The Question Mark Wildcard (`?`)**
Matches exactly **one individual character slot**.
*   `ls -lda ~/Documents/git/mentor/????`: Selects folders inside the mentor directory whose names are composed of **exactly four characters**.
*   `ls -la ~/Documents/git/mentor/.sampledata/31??_*`: Targets items starting with `31`, followed by exactly *any two characters*, followed by an underscore (`_`), and ending with *any text configuration* whatsoever (`*`).

>  **Usage Flexibility:** Wildcards are universal shell attributes. They work inside almost any execution tool, including `ls`, `cp`, `mv`, and `rm`.
> 
> *Example Workflow:*
> ```bash
> mv ~/Documents/git/mentor/.sampledata/31??_* ~/Documents/bash-sandbox/test_folder
> ```
> *Explanation:* The engine evaluates the pattern match criteria, harvests all matching files starting with "31" and a trailing underscore, and moves them out into the `test_folder` path target.


---

## 6. Files, Folders, Permissions & Home Directory

###  Concept Questions & Answers

#### **How do you differentiate and list only files or only directories?**
When inspecting layout attributes with `ls -l`, look at the very first character of the line string:
*   `d` = Directory/Folder
*   `-` = Standard File

*   **Command to list only directories in the current folder:**
    ```bash
    ls -ld */
    ```
*   **Command to list only files in the current folder:**
    ```bash
    find . -maxdepth 1 -type f
    ```

#### **What are user groups and file/folder permissions?**
Linux security segments permission controls into three structural groupings:
1.  **User (`u`):** The individual account that owns the file node.
2.  **Group (`g`):** A cluster of accounts sharing identical access rights to the asset.
3.  **Others (`o`):** The public world (anyone who is not the owner and not in the group).

Each group possesses three authorization toggles: **Read (`r`)**, **Write (`w`)**, and **Execute (`x`)**.

#### **How do you set file permissions?**
Use the **`chmod`** (Change Mode) command.
*   *Symbolic approach:* `chmod g+w assignment.txt` (Adds Write access to the Group layer).
*   *Numeric/Octal approach:* `chmod 755 script.sh` (Owner gets full `rwx`=7, Group and Others get read/execute `r-x`=5).

#### **How do you set ownership of files or folders?**
Use the **`chown`** (Change Owner) command, preceded by `sudo`:
```bash
sudo chown username:groupname filename
```

#### **What are hidden files?**
Any file or directory folder whose filename begins with a period (`.`). They store application preferences and repository tracking maps. To reveal them, you must append the `-a` option flag to `ls`.

#### **Home Directory Breakdown**
*   **Definition:** A user's secure personal playground space within the OS file architecture.
*   **Absolute Paths:** `/home/username` on Linux systems; `/Users/username` on macOS devices.
*   **Shorthand Alias:** The tilde character (`~`).

---

##  7. Comprehensive Practical Task & Question Solutions

>  **Prerequisite Action:** Run `./util/generate_exam_data.sh` inside the workspace to deploy the hidden tracking data arrays (`.sampledata/` directory and `.test.student.csv` index files).

###  Section 1: Using ONLY `ls` with Wildcards (`*`, `?`)
*No pipes (`|`) or `grep` operations allowed. All commands act directly on target paths.*

#### 1. List all student data files (`.txt` files) in the `.sampledata` directory.
```bash
ls .sampledata/*.txt
```
*   *Explanation:* Matches any filename inside the `.sampledata` directory that terminates with the extension string `.txt`.

#### 2. List all student data files where the student ID starts with 10 and ends with any two digits.
```bash
ls .sampledata/10??_*.txt
```
*   *Explanation:* The two `?` characters mandate exactly two arbitrary numerical slots following "10", followed by an underscore separator and wildcard name trailing pattern.

#### 3. List all student data files where the student ID starts with 10 and ends with either 2 or 7.
*Note: Standard wildcards cannot do logical OR operations within a single `?` selector. You must run two separate explicit arguments inside the query line.*
```bash
ls .sampledata/10?2_*.txt .sampledata/10?7_*.txt
```
*   *Explanation:* Evaluates the pattern pool twice—once matching IDs ending in 2, and once matching IDs ending in 7.

#### 4. List all student data files where the student ID is between 1100 and 1199.
```bash
ls .sampledata/11??_*.txt
```
*   *Explanation:* Restricts the leading digits to "11" and uses two single-character wildcard placeholders to map out numbers from 00 to 99.

#### 5. List all student data files where the student's first name starts with 'A' or 'B'.
```bash
ls .sampledata/*_A*_.txt .sampledata/*_B*_.txt
```
*   *Explanation:* Given the filename format `Id_FirstName_MiddleInitial_LastName.txt`, this queries for an arbitrary ID sequence, followed by an underscore, catching first names leading with "A" or "B".

#### 6. List all student data files where the student's middle initial is 'Z'.
```bash
ls .sampledata/*_*_Z_*.txt
```
*   *Explanation:* Uses positional separators (underscores) to skip the ID and First Name, isolating files containing "Z" exactly inside the middle initial field.

#### 7. List all student data files where the student ID is between 1200 and 1299.
```bash
ls .sampledata/12??_*.txt
```

#### 8. List all student data files where the student ID is between 1300 and 1399.
```bash
ls .sampledata/13??_*.txt
```

#### 9. List all student data files where the student ID is between 1400 and 1499.
```bash
ls .sampledata/14??_*.txt
```

#### 10. List all student data files where the student ID ends with a 0.
```bash
ls .sampledata/*0_*.txt
```
*   *Explanation:* Finds files where the character immediately preceding the first underscore separator is a zero (`0`).

#### 11. List all student data files where the student ID ends with a 5.
```bash
ls .sampledata/*5_*.txt
```

#### 12. List all student data files where the third digit of the student ID is 2.
```bash
ls .sampledata/??2?_*.txt
```
*   *Explanation:* Skips the first two digits using `??`, forces the third slot to be a `2`, and allows any single character in the fourth slot.

#### 13. List all student data files where the third digit of the student ID is 2 AND their middle initial is L.
```bash
ls .sampledata/??2?_*_L_*.txt
```
*   *Explanation:* Combines the third-digit ID positional matching filter with the third-column middle initial indicator structure.

#### 14. List all student data files where the fourth digit of the student ID is 5.
```bash
ls .sampledata/???5_*.txt
```

#### 15. List all student data files where the second digit of the student ID is 0.
```bash
ls .sampledata/?0??_*.txt
```

#### 16. List all student data files where the last digit of the student ID is 9.
```bash
ls .sampledata/*9_*.txt
```

#### 17. List all student data files where the student ID is between 1000 and 1009.
```bash
ls .sampledata/100?_*.txt
```

#### 18. List all student data files where the first name starts with 'N'.
```bash
ls .sampledata/*_N*
```

#### 19. List all student data files where the first name starts with 'O'.
```bash
ls .sampledata/*_O*
```

#### 20. List all student data files where the first name starts with 'P'.
```bash
ls .sampledata/*_P*
```

#### 21. List all student data files where the first name starts with 'Z'.
```bash
ls .sampledata/*_Z*
```

#### 22. List all student data files where the middle initial is 'C'.
```bash
ls .sampledata/*_*_C_*.txt
```

#### 23. List all student data files where the middle initial is 'K'.
```bash
ls .sampledata/*_*_K_*.txt
```

#### 24. List all student data files where the middle initial is 'L'.
```bash
ls .sampledata/*_*_L_*.txt
```

#### 25. List all student data files where the middle initial is 'P'.
```bash
ls .sampledata/*_*_P_*.txt
```

#### 26. List all student data files where the last name starts with 'R'.
```bash
ls .sampledata/*_*_*_R*.txt
```
*   *Explanation:* Uses three leading wildcard fields and underscores to jump past ID, First Name, and Middle Initial segments, targeting last names starting with "R".

#### 27. List all student data files where the last name starts with 'M'.
```bash
ls .sampledata/*_*_*_M*.txt
```

#### 28. List all student data files where the last name starts with 'Y'.
```bash
ls .sampledata/*_*_*_Y*.txt
```

#### 29. List all student data files where the last name ends with 'u'.
```bash
ls .sampledata/*_*_*_*u.txt
```
*   *Explanation:* Ensures that the character immediately preceding the file extension dot is a lowercase `u`.

#### 30. List all student data files where the last name contains 'on'.
```bash
ls .sampledata/*_*_*_*on*.txt
```
*   *Explanation:* Targets files where the sequence `on` falls anywhere inside the final last name segment block.

#### 31. List all student data files where the student ID is between 1050 and 1059 AND the first name starts with 'A'.
```bash
ls .sampledata/105?_A*_.txt
```

#### 32. List all student data files where the student ID is between 1110 and 1119 AND the middle initial is 'K'.
```bash
ls .sampledata/111?_*_K_*.txt
```

#### 33. List the student data file for 'Alice Smith' (exact first and last name, any middle initial).
```bash
ls .sampledata/*_Alice_?_Smith.txt
```

#### 34. List all student data files where the first name starts with 'C' AND the middle initial is 'D'.
```bash
ls .sampledata/*_C*_D_*.txt
```
*   **Explanation:** Leverages positional underscores (`_`) mapping the `Id_FirstName_MiddleInitial_LastName.txt` format. It filters for any ID prefix, handles first names starting with "C" using `C*`, isolates "D" as the full middle initial field, and allows any last name.

#### 35. List all student data files where the student ID is 10?? (any two digits after 10) AND the last name ends with 's'.
```bash
ls .sampledata/10??_*_*_*s.txt
```
*   **Explanation:** Restricts the ID block prefix to "10" followed by exactly two arbitrary digit positions (`??`). The trailing structural wildcards step past the first and middle name fields, matching files where the last character before the `.txt` extension is a lowercase "s".

---

##  Section 2: Use grep, find for Advanced Search

#### 36. Find all student data files (.txt) that contain the word "Mathematics" (case-sensitive).
```bash
grep -l "Mathematics" .sampledata/*.txt
```
*   **Command Explanation:** `grep` scans for text matches inside files. The `-l` flag overrides standard line dumping, instructing the engine to cleanly print only the **filenames** of documents that contain the phrase.

#### 37. Find all student data files (.txt) where the student's email address ends with @hotmail.com.
```bash
grep -l "@hotmail.com" .sampledata/*.txt
```
*   **Command Explanation:** Traverses all student profile logs inside `.sampledata/`, isolating and printing the paths of files containing hotmail entries.

#### 38. Count how many student data files contain the phrase "CountyNum: 1".
```bash
grep -l "CountyNum: 1" .sampledata/*.txt | wc -l
```
*   **Command Explanation:** `grep -l` lists out unique filenames that hold a match. This text stream of file names is then passed via a pipe (`|`) to `wc -l` (Word Count - Lines), which counts the total lines to return the exact number of matching files.

#### 39. List the names (full path) of all student data files (.txt) that have a score of 99 for any subject.
```bash
grep -l "score: 99" .sampledata/*.txt
```
*   **Command Explanation:** Scans inside the nested documentation profiles and filters out paths for any records displaying a maximum score value of 99.

#### 40. Find all student data files (.txt) that contain the name "Alice" (case-insensitive).
```bash
grep -il "Alice" .sampledata/*.txt
```
*   **Command Explanation:** Appends the `-i` flag option to instruct `grep` to ignore uppercase/lowercase boundaries entirely, matching string variants like "alice", "Alice", or "ALICE".

#### 41. Find all student data files (.txt) that were created within the last 24 hours (assuming you just ran generate_data.sh).
```bash
find .sampledata/ -type f -name "*.txt" -mmin -1440
```
*   **Command Explanation:** `find` searches directory hierarchies. `-type f` restricts it to actual files (ignoring subfolders), `-name "*.txt"` isolates text profiles, and `-mmin -1440` uses minute calculations (24 hours × 60 minutes = 1440) to filter for files modified *less than* 24 hours ago.

#### 42. Find all student data files (.txt) that are larger than 200 bytes.
```bash
find .sampledata/ -type f -name "*.txt" -size +200c
```
*   **Command Explanation:** The specialized flag `-size +200c` targets files whose data footprint strictly exceeds 200 bytes (the suffix character `c` explicitly designates bytes in find system calculations).

#### 43. Find all .csv files in the current directory that contain the word "Nairobi".
```bash
grep -l "Nairobi" *.csv
```
*   **Command Explanation:** Isolates regional index data maps (`.test.student.csv`, etc.) sitting directly within your primary working folder path.

#### 44. List all student IDs (the 4-digit number) from student data files that have "Physics" listed as a subject.
```bash
grep -l "Physics" .sampledata/*.txt | awk -F'/' '{print $NF}' | cut -d'_' -f1
```
*   **Command Explanation:** This command pipeline maps out three structural phases:
    1.  `grep -l "Physics"` isolates matching path names (e.g., `.sampledata/1024_Jane_M_Doe.txt`).
    2.  `awk -F'/' '{print $NF}'` breaks the path apart at the forward slashes and extracts just the final element (the raw filename: `1024_Jane_M_Doe.txt`).
    3.  `cut -d'_' -f1` isolates field 1 relative to the first underscore separator, pulling the exact 4-digit student ID.

#### 45. Find all student data files (.txt) that contain the word "Email:" AND "CountyNum: 5".
```bash
grep -l "Email:" .sampledata/*.txt | xargs grep -l "CountyNum: 5"
```
*   **Command Explanation:** Direct sequential piping fails here because `grep` requires file parameters, not raw text. `xargs` bridges this gap: it gathers the file list produced by the first `grep` command and passes it forward as direct arguments for the second `grep` verification.

---

##  Section 3: Use sed or perl only for Advanced Text Manipulation

>  **Reference Check:** Complete the *Supplemental RegEx & vi* module prior to editing. Avoid appending the `-i` (in-place) operational flag unless you intend to alter underlying data stores permanently.

### Core Example Breakdowns
*   **Example A:** `sed -n -E "s/(^11.*)/\1/gp" .test.student.csv`
    *   `-n`: Suppresses standard console text echoes. Only processes explicit print requests.
    *   `-E`: Directs the parser engine to use Extended Regular Expression operations.
    *   `s/pattern/replacement/gp`: Triggers substitutions. The `g` flag applies it globally across the row, and `p` prints the resulting line structure.
*   **Example B:** `sed -n -E "s/(^22[0-9][^;]*;)([^;]*;)(.*;)(.*@.*)$/\1\2\4/gp" .test.student.csv`
    *   `[^;]*;`: Dynamically matches all text fields up to the next structural semicolon delimiter column.
    *   `\1\2\4`: Extracts specific capture groupings, throwing away unnecessary index text.

---

###  Exercise Solutions

#### 46. Print out all students with ID starting with 33...
```bash
sed -n -E "/^33[0-9]+/p" .test.student.csv
```
*   **Command Explanation:** Leverages pattern matching blocks. The format `/^33[0-9]+/` checks for rows starting explicitly with "33" followed immediately by valid numeric ID strings. If matched, the trailing `p` command outputs the targeted text line to the console.

#### 47. Find all students from county #44 (Ensure that students from school #44 are not accidentally included unless they are from county #44) and display their phone numbers without the hyphen.
```bash
sed -n -E "s/(^[0-9]+;[^;]+;)([0-9]{3})-([0-9]{3})-([0-9]{4});(44;.*)$/\1\2\3\4;\5/p" .test.student.csv
```

*   **Deep-Dive Structural Breakdown:**
    To accurately isolate the columns from the raw data pattern (`ID;Name;Phone;SchoolID;CountyID;Email`), we map out **5 individual capture groups**:
    1.  `([0-9]+;[^;]+;)`  **Group 1:** Captures the starting Student ID and Full Name string columns alongside their separating semicolons.
    2.  `([0-9]{3})-([0-9]{3})-([0-9]{4})` **Groups 2, 3, and 4:** Splits up the target phone number. Group 2 captures the 3-digit area code, Group 3 captures the 3-digit prefix, and Group 4 captures the final 4 digits. The literal hyphens (`-`) sitting between the groups are left outside the parentheses, targeting them for removal.
    3.  `;(44;.*)$` **Group 5:** Confirms the next column array contains exactly County code `44`, followed by any trailing data characters (the student email field) up to the end of the line (`$`). This safety anchor prevents matching a school code of 44 if the county code is different.
    4.  `\1\2\3\4;\5` **The Replacement Array:** Re-assembles the line structure by calling the groups back in sequence. By printing groups 2, 3, and 4 back-to-back without placing characters between them, the original raw hyphens are stripped out completely.


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
do it in the main directory quatrix-mentor

```bash
touch restore_data.zsh
```

Step 2 ; Write a code inside the file 

```bash
cat << 'EOF' > restore_data.zsh
cat << 'EOF' > restore_data.zsh
#!/bin/bash

# 1. Ensure the main .sampledata directory exists
mkdir -p .sampledata

# 2. Pull all .txt files out of the categories and into the root of .sampledata
mv .sampledata/*/*.txt .sampledata/ 2>/dev/null

# 3. Completely delete the empty category folders
rmdir .sampledata/A-F .sampledata/G-L .sampledata/M-R .sampledata/S-Z 2>/dev/null

echo "SUCCESS: Categories deleted. Files restored flatly into .sampledata!"
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
 to prove they have been removed from the main directory ;
 
```bash
ls -d A-F G-L M-R S-Z
```
to verify the categories are gone

```bash
ls -F .sampledata
```
the flag -F - classify , it ads a speciall trailing symbol to the end of the name to show what kind of files they are . 

#### 6. Create a Bash script named full_cleanup.zsh that runs the cleanup function from generate_data.sh and then also removes all .test.*.csv files. Make it executable.
to prove that the .csv file is there before deleting ;

```bash
ls -la
```

step 1 ; Creating a file

```bash
touch full_cleanup.zsh
```

Step 2 ; Write the code 

```bash
cat << 'EOF' > full_cleanup.zsh
#!/bin/bash
# 1. Check if the file generate_data.sh actually exists before opening it
if [[ -f ./generate_data.sh ]]; then
    source ./generate_data.sh cleanup
fi
# 2. Quietly wipe away all the temporary test csv files
rm -f .test.*.csv
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

to verify in the main directory as well ;


```bash
ls -la
```
### 6. How do you comment out an SQL line so that it is ignored by the SQL engine?

#### Single - Line comments 

```bash
-- This entire line is ignored by the SQL engine
SELECT * FROM users; -- This trailing comment is also ignored

```
#### Multi- Line comments 
```bash
/* This is a multi-line comment.
   The engine will completely skip 
   all of these lines. */
SELECT * FROM products;
```

Explanation ;

1. Use -- to cross out the rest of one single line.

2. Use /* and */ to cross out a whole paragraph.
