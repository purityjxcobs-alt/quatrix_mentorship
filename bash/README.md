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


#  # Bash Scripting Definition & Concept Questions

### Q1: What is a "Shell" in the context of Linux/Unix operating systems?
* **A.** A hardware component that manages memory allocation.
* **B.** A command-line interpreter that provides a user interface for interacting with the operating system kernel.
* **C.** A security firewall that blocks unauthorized network access.
* **D.** A compiler that transforms source code into executable binary files.
* **Correct Answer: B**

---

### Q2: Define the term "Idempotency" as it applies to Bash scripting.
* **A.** The ability of a script to execute faster every time it is run.
* **B.** A property where running a script multiple times produces the same system state as running it once, without causing unintended side effects.
* **C.** The process of converting text strings into integer variables automatically.
* **D.** A critical runtime error caused by infinite loops inside nested functions.
* **Correct Answer: B**

---

### Q3: What is the main structural difference between a Shell Variable and an Environment Variable?
* **A.** Shell variables store only numbers, while environment variables store only text.
* **B.** Shell variables are written in lowercase, while environment variables must be uppercase.
* **C.** Shell variables are local to the current shell instance, whereas environment variables are passed down to child processes and subshells.
* **D.** Shell variables are saved permanently on the hard drive, while environment variables disappear when a command finishes.
* **Correct Answer: C**

---

### Q4: Match the standard I/O stream to its correct file descriptor number:
* **1.** `stdin` (Standard Input) -> **File Descriptor:** `0`
* **2.** `stdout` (Standard Output) -> **File Descriptor:** `1`
* **3.** `stderr` (Standard Error) -> **File Descriptor:** `2`

---

### Q5: What does the command `2>&1` accomplish in a Bash command-line execution?
* **A.** It doubles the execution speed of the background process.
* **B.** It redirects Standard Error (stderr) to the same destination as Standard Output (stdout).
* **C.** It forces the script to prompt the user for input twice before continuing.
* **D.** It exits the program immediately with an error status code of 2.
* **Correct Answer: B**

---

### Q6: Fill in the Blank
To read a line of input from the user via standard input and assign it to a variable named `USER_INPUT`, you use the built-in command named `________`.
* **Correct Answer:** `read` (e.g., `read USER_INPUT`)

---

### Q7: What is the meaning of a `0` exit status vs a non-zero exit status (e.g., `1`, `127`, `2`)?
* **A.** `0` means the program failed; non-zero means it succeeded perfectly.
* **B.** `0` means the script completed successfully; non-zero codes indicate specific errors or execution failures.
* **C.** `0` means the script is running in background mode; non-zero means foreground mode.
* **D.** there is no difference; the numbers are randomly chosen by the system kernel.
* **Correct Answer: B**

---

### Q8: What does the flag `-z` test for when used inside a conditional bracket expression like `if [ -z "$MY_VAR" ]`?
* **A.** It checks if the file named `MY_VAR` is zipped/compressed.
* **B.** It checks if the integer variable equals zero.
* **C.** It checks if the string variable is empty (has a length of zero).
* **D.** It checks if the system process has zero background threads.
* **Correct Answer: C**

---

### Q9: True or False
In Bash, arrays can store a mix of integers and strings, and they are zero-indexed, meaning the first element is accessed using `${array[0]}`.
* **Correct Answer:** **True**

---

### Q10: What is the purpose of the `alias` command in a Bash environment?
* **A.** To temporarily change the username of the logged-in user.
* **B.** To create a shortcut name or alternative string that stands for a longer command or sequence of commands.
* **C.** To hide the directory path from displaying in the terminal prompt.
* **D.** To encrypt the source code of a plaintext script file.
* **Correct Answer: B**

# Additional Bash Scripting & Linux Command Questions

### Q11: What is the main difference between the `exit` command and the `return` command in Bash?
* **A.** `exit` terminates the entire script execution, while `return` exits a function and hands control back to the caller.
* **B.** `exit` is used for successful completions, while `return` is only used for errors.
* **C.** `exit` can only return text strings, while `return` can only return integers.
* **D.** They are exact synonyms and can be used interchangeably in any part of a script.
* **Correct Answer: A**

---

### Q12: Which utility is best suited for searching specific text patterns within files using regular expressions?
* **A.** `sed`
* **B.** `grep`
* **C.** `awk`
* **D.** `find`
* **Correct Answer: B**

---

### Q13: In a Bash script conditional statement, what is the purpose of the `&&` short-circuit operator?
* **A.** It executes the second command only if the first command fails (returns a non-zero exit status).
* **B.** It executes both commands simultaneously in separate background threads.
* **C.** It executes the second command only if the first command succeeds (returns a `0` exit status).
* **D.** It acts as a mathematical operator that multiplies two numbers together.
* **Correct Answer: C**

---

### Q14: What command would you use to change the permissions of a script so that the owner can execute it?
* **A.** `chown +x script.sh`
* **B.** `chmod +x script.sh`
* **C.** `chperm 755 script.sh`
* **D.** `umask +x script.sh`
* **Correct Answer: B**

---

### Q15: Fill in the Blank
To process a text file line-by-line and easily extract specific columns of data (such as printing just the 3rd column), the `________` text-processing utility is most commonly recommended.
* **Correct Answer:** `awk` (e.g., `awk '{print $3}' file.txt`)

---

### Q16: What happens if you run a script using `source script.sh` (or `. script.sh`) instead of `./script.sh`?
* **A.** The script runs inside a separate child process, protecting the current shell's environment variables.
* **B.** The script runs inside the current shell's process, allowing it to modify the current shell's variables and environment directly.
* **C.** The script is compiled into temporary machine code before running.
* **D.** The shell runs the script in safe mode without administrative privileges.
* **Correct Answer: B**

---

### Q17: What does the flag `-d` test for when used inside a conditional bracket expression like `if [ -d "$PATH_VAR" ]`?
* **A.** It checks if the specified path points to an active disk drive.
* **B.** It checks if the specified path exists and is a directory.
* **C.** It checks if the file has deleted data fragments.
* **D.** It checks if the variable is defined in the system registry.
* **Correct Answer: B**

---

### Q18: Which structural component is used in Bash to handle multi-way branching based on pattern matching (similar to a switch-case statement in other languages)?
* **A.** `if ... elif ... else`
* **B.** `case ... esac`
* **C.** `select ... done`
* **D.** `switch ... case`
* **Correct Answer: B**

---

### Q19: What is the purpose of the special variable `$!` in Bash?
* **A.** It holds the process ID (PID) of the most recently executed background job.
* **B.** It forces the script to crash immediately as an intentional panic signal.
* **C.** It contains the error message text generated by the last failed command.
* **D.** It expands to the absolute path of the global configuration profile.
* **Correct Answer: A**

---

### Q20: What does the command `sed -i 's/apple/banana/g' fruit.txt` do?
* **A.** It prints lines containing the word "apple" from `fruit.txt` to the terminal screen.
* **B.** It creates a new file called `banana.txt` filled with references to apples.
* **C.** It searches for the word "apple" and changes it to "banana" everywhere inside the file `fruit.txt`, saving the changes directly in place.
* **D.** It deletes every line in `fruit.txt` that contains the word "banana".
* **Correct Answer: C**
# Comprehensive Bash Question Pool: Detailed Explanations & Rationales

---

## Category 1: Environment, Shebang, & Execution

### Q21: What happens if a Bash script does NOT include a shebang line (`#!/bin/bash`) at the top?
* **Correct Answer: C**
* **Why C is correct:** Without an explicit shebang directive, the operating system kernel falls back to executing the script using the default active shell of the user who initiated the command (often `sh`, `dash`, or `zsh`). If your script contains "Bashisms" (syntax specific only to Bash), it will crash or behave unpredictably.
* **Why other options are incorrect:** 
  * **A is wrong:** The OS will still attempt to read the file as plain text line-by-line; it does not throw an immediate panic or refuse to execute.
  * **B is wrong:** Linux shells are strictly interpreters; they lack the ability to magically compile an uncompiled text script into a binary executable file like C.
  * **D is wrong:** Security encryption is never triggered automatically by the absence of file syntax markers.

### Q22: What is the purpose of the `PATH` environment variable in Linux?
* **Correct Answer: B**
* **Why B is correct:** `PATH` is a colon-separated list of system directories. When you type a command like `ls` or `mkdir`, the shell searches these directories from left to right to locate the corresponding executable binary file.
* **Why other options are incorrect:**
  * **A is wrong:** The path to the user's home directory is stored in the `$HOME` variable, not `$PATH`.
  * **C is wrong:** Terminal command history is stored in the memory buffer and written to files like `~/.bash_history`.
  * **D is wrong:** Network routing maps are managed by the kernel routing tables (`netstat` or `ip route`), completely independent of environment configuration variables.

### Q23: What does the command `export MY_VAR` accomplish?
* **Correct Answer: C**
* **Why C is correct:** By default, standard shell variables are local and restricted strictly to the current shell process instance. Using `export` flags the variable so that any child processes, external commands, or subshells spawned from this shell inherit the variable.
* **Why other options are incorrect:**
  * **A is wrong:** `export` only alters volatile runtime memory. To make a variable permanent, you must append it textually to a startup file like `~/.bashrc`.
  * **B is wrong:** It shares data downstream to local software forks, not across networked computers.
  * **D is wrong:** To clear a variable from memory, the `unset` command must be used.

### Q24: What is the difference between `./my_script.sh` and `source ./my_script.sh`?
* **Correct Answer: A**
* **Why A is correct:** Running a script with `./` forks a brand-new, isolated child shell process. Running a script with `source` (or the `.` dot command) evaluates the script lines directly inside your *current* shell process environment, meaning any variables or aliases created inside the script persist after it finishes.
* **Why other options are incorrect:**
  * **B is wrong:** Neither command compiles code; they both execute the script lines purely through sequential interpretation.
  * **C is wrong:** They alter process environments entirely differently, making them fundamentally distinct operations.
  * **D is wrong:** Execution privileges rely entirely on standard Linux file permissions (`chmod`), not on whether you source or call a script.

---

## Category 2: Variables, Parameters, & String Expansion

### Q25: How do you properly access the length (number of characters) of a string stored in a variable named `STR`?
* **Correct Answer: A**
* **Why A is correct:** The hash/pound prefix (`#`) placed right before the variable name inside curly braces `${#VAR}` is the precise native parameter expansion syntax Bash utilizes to count character lengths.
* **Why other options are incorrect:**
  * **B is wrong:** Object-oriented dot notation properties (like `.length` or `.size`) do not exist in Bash.
  * **C & D are wrong:** Neither `length` nor `count` are native built-in functions or structural keywords in Bash logic.

### Q26: What is the operational difference between the special parameters `$*` and `$@` when wrapped in double quotes?
* **Correct Answer: B**
* **Why B is correct:** When encapsulated in double quotes, `"$*"` flattens all passed parameters into one singular giant text string separated by spaces (or the first character of your `$IFS`). Conversely, `"$@"` breaks arguments apart into individual, cleanly separated strings, preserving literal parameter blocks even if they contain spaces.
* **Why other options are incorrect:**
  * **A is wrong:** This reverses the behavioral rules; `"$@"` is what accurately preserves distinct argument separations.
  * **C is wrong:** Counting parameters requires the `$#` parameter.
  * **D is wrong:** They exhibit wildly different mechanics during loop processing, meaning they are absolutely not identical.

### Q27: What is the output of the following block of code?
```bash
VAR="OpenOLAT"
echo '${VAR}'
```
* **Correct Answer: C**
* **Why C is correct:** Single literal quotes (`'...'`) aggressively suppress all underlying shell interpretations. They treat every character between them exactly as literal text, preventing the dollar sign from triggering variable expansion.
* **Why other options are incorrect:**
  * **A & B are wrong:** Variable expansion (`OpenOLAT`) only occurs if you use double quotes (`"..."`) or no quotes at all.
  * **D is wrong:** Passing literal text to `echo` will never cause a critical runtime evaluation script failure.

### Q28: Which configuration file is read and executed when a non-login interactive Bash shell starts up?
* **Correct Answer: C**
* **Why C is correct:** Non-login interactive shells (like opening a new standard terminal window while already logged into your desktop GUI) explicitly load the user's localized `~/.bashrc` file to set up environment structures.
* **Why other options are incorrect:**
  * **A & B are wrong:** `/etc/profile` and `~/.bash_profile` are explicitly reserved for initial system initialization during **login** shell sequences (e.g., initial SSH access or terminal text logins).
  * **D is wrong:** `~/.bash_logout` runs exclusively when an active shell session is completely closed or killed.

---

## Category 3: Conditional Logic & File Testing

### Q29: Which flag inside a conditional test statement checks if a file exists and has a size greater than zero bytes?
* **Correct Answer: B**
* **Why B is correct:** The `-s` operator specifically runs a dual verification check: it returns true if the targeted file exists and its size size evaluation is actively greater than zero bytes (i.e., it is not empty).
* **Why other options are incorrect:**
  * **A is wrong:** The `-e` flag only checks if a file exists, regardless of whether it contains data or is completely empty.
  * **C is wrong:** The `-f` flag verifies if the target is a regular file (as opposed to a folder or device path).
  * **D is wrong:** The `-d` flag specifically evaluates whether the target path points to a directory.

### Q30: What operator is used to check if two text strings are NOT equal in a standard Bash test block?
* **A.** `-ne`
* **B.** `!=`
* **Correct Answer: B**
* **Why B is correct:** In Bash conditional parsing frameworks, `!=` is the designated operator used to evaluate string inequalities.
* **Why other options are incorrect:**
  * **A is wrong:** The `-ne` operator is strictly for **numeric integer** inequality evaluation. Using it on strings can break your script.
  * **C is wrong:** Strict identity operators like `!==` belong to JavaScript/TypeScript paradigms and do not exist in Bash.
  * **D is wrong:** `-not` is invalid conditional syntax inside classic evaluation brackets.

### Q31: What is the fundamental difference between the operators `-eq` and `==` inside conditional statements?
* **Correct Answer: A**
* **Why A is correct:** Bash is strictly typed towards strings by default. Therefore, it uses explicit textual flags like `-eq`, `-ne`, `-lt`, and `-gt` for arithmetic integer processing, while saving operators like `==` and `!=` for exact character-matching string routines.
* **Why other options are incorrect:**
  * **B is wrong:** This completely swaps their designated functional roles.
  * **C is wrong:** Swapping them leads to serious bugs (e.g., matching string text using an arithmetic flag throws standard syntax errors).
  * **D is wrong:** Boolean values in Bash are simulated via command exit codes (`0` or `1`); neither flag handles raw boolean evaluation fields.

### Q32: What will be the output of this script segment?
```bash
if [ 5 -gt 10 ] || [ 2 -eq 2 ]; then
    echo "Condition Met"
else
    echo "Condition Failed"
fi
```
* **Correct Answer: B**
* **Why B is correct:** The logical `||` operator represents an **OR** condition. Even though the first test evaluates to false (`5` is not greater than `10`), the second test evaluates to true (`2` is equal to `2`). Because at least one side is true, the entire conditional statement passes.
* **Why other options are incorrect:**
  * **A is wrong:** The block will only fall back to the `else` sequence if *both* surrounding conditional expressions evaluate to false.
  * **C & D are wrong:** The formatting of this block utilizes perfectly valid, standard Bash bracket notation grammar rules.

---

## Category 4: Streams, Redirection, & Pipes

### Q33: What is the difference between `>` and `>>` when redirecting output to a file?
* **Correct Answer: B**
* **Why B is correct:** A single angle bracket `>` truncates and completely overwrites any pre-existing text inside the file. A double angle bracket `>>` targets the bottom EOF index and safely appends your stream data without wiping out older modifications.


# ```markdown
# Bash Complete Notes — Everything Discussed

> A full compilation of all topics, commands, flags, characters, examples, practice questions, and alternatives covered in this chat.
> Copy this entire file into VS Code or GitHub as your notes.

---

## Table of Contents

1. [The `ls` Command](#1-the-ls-command)
2. [Finding Files by Character Count](#2-finding-files-by-character-count)
3. [`ls *9*` — What It Really Means](#3-ls-9--what-it-really-means)
4. [Downloading Files with `wget` and Saving with a New Name](#4-downloading-files-with-wget-and-saving-with-a-new-name)
5. [The `tar` Command — Full Q&A](#5-the-tar-command--full-qa)
6. [Copying a File — `cp`](#6-copying-a-file--cp)
7. [Moving a File — `mv`](#7-moving-a-file--mv)
8. [Using `man` (Manual Pages)](#8-using-man-manual-pages)
9. [Finding Files with 9, 10, 14, 16 Characters](#9-finding-files-with-9-10-14-16-characters)
10. [Seven Crucial Takeaways for the Test](#10-seven-crucial-takeaways-for-the-test)
11. [Practice Question Sets](#11-practice-question-sets)
12. [Alternatives to `history`](#12-alternatives-to-history)
13. [Keeping Your Directory Clean While Testing](#13-keeping-your-directory-clean-while-testing)
14. [Multiple Ways to Get the Same Output](#14-multiple-ways-to-get-the-same-output)
15. [Case-Insensitive `grep` (`-i`)](#15-case-insensitive-grep--i)
16. [Files Starting with `d` and Ending with `.log`](#16-files-starting-with-d-and-ending-with-log)
17. [Fill-in-the-Blank Rules](#17-fill-in-the-blank-rules)
18. [Spacing & Formatting Rules](#18-spacing--formatting-rules)
19. [`sudo` Decision Table](#19-sudo-decision-table)
20. [`echo` and Newlines](#20-echo-and-newlines)
21. [Complete Command Reference (All Commands + Flags)](#21-complete-command-reference-all-commands--flags)
22. [Wildcards / Glob Characters](#22-wildcards--glob-characters)
23. [Regex Characters (grep, find, awk)](#23-regex-characters-grep-find-awk)
24. [Redirection & Operators](#24-redirection--operators)
25. [Quick Reference Cheat Sheet](#25-quick-reference-cheat-sheet)

---

## 1. The `ls` Command

`ls` lists directory contents. It does **not** have a built-in flag for filename length.

| Flag | Meaning |
|------|---------|
| `-l` | Long format (permissions, size, date) |
| `-a` | Show hidden files (starting with `.`) |
| `-1` | One file per line |
| `-d` | List the directory itself, not its contents |
| `-h` | Human-readable sizes (KB, MB) |
| `-t` | Sort by modification time |
| `-r` | Reverse order |
| `-S` | Sort by size |
| `-R` | Recursive |

**Examples:**
```bash
ls                    # list files
ls -la                # all files, long format
ls -d ?????????       # files with exactly 9 characters
ls -d1 ?????????      # same, one per line
ls d*.log             # starts with d, ends with .log
ls *.txt              # ends with .txt
ls -lh                # long format with human sizes
```

---

## 2. Finding Files by Character Count

Use the shell wildcard `?`, which matches **exactly one** character.

**Nine `?` marks** match filenames with exactly 9 characters:

```bash
ls -d ????????? 2>/dev/null
```

Count how many match:

```bash
ls -d ????????? 2>/dev/null | wc -l
```

If the number is greater than `0`, there are files/directories with 9-character names.

For regular files only, including hidden files, in the current directory:

```bash
find . -maxdepth 1 -type f -name '?????????' -print
```

Count them:

```bash
find . -maxdepth 1 -type f -name '?????????' | wc -l
```

Remove `-maxdepth 1` if you want to search recursively.

If you meant **file size is 9 characters/bytes**:

```bash
find . -maxdepth 1 -type f -size 9c
```

---

## 3. `ls *9*` — What It Really Means

`ls *9*` does **not** mean "filenames with 9 characters."

In shell globbing:

- `*` = any number of characters, including zero
- `?` = exactly one character

So:

```bash
ls -d *9*
```

lists any filename that **contains the digit `9`** anywhere, e.g.:

```text
file9.txt
999999999999
abc9
9lives
```

It does **not** check length. For example, `999999999999` has 12 characters but still matches `*9*`.

To list filenames with **exactly 9 characters**, use nine `?` marks:

```bash
ls -d ????????? 2>/dev/null
```

Summary:

- `ls *9*` → names containing the character `9`
- `ls -d ?????????` → names that are exactly 9 characters long

---

## 4. Downloading Files with `wget` and Saving with a New Name

Use `wget -O` to save the download under the name you want:

```bash
wget -O myfile.zip "https://example.com/somefile.zip"
```

- `-O myfile.zip` = save as `myfile.zip`
- It is a capital letter **O**, not zero.

Then unzip it:

```bash
unzip myfile.zip
```

If you want to extract it into a specific folder name:

```bash
unzip myfile.zip -d myfolder
```

Full one-liner:

```bash
wget -O myfile.zip "https://example.com/somefile.zip" && unzip myfile.zip -d myfolder
```

If it's a `.tar.gz` instead of `.zip`:

```bash
wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz -C myfolder
```

If you don't use `-O`, `wget` saves it using the filename from the URL.

**Difference between `-O` and `-o`:**

- `wget -O` (capital O) = save the downloaded file with this name.
- `wget -o` (lowercase o) = write the log output to this file.

```bash
wget -O myfile.zip "https://example.com/file.zip"    # saves the file as myfile.zip
wget -o log.txt "https://example.com/file.zip"       # saves download log to log.txt
```

---

## 5. The `tar` Command — Full Q&A

Your command:

```bash
wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz -C myfolder
```

The tar part is:

```bash
tar -xzf myfile.tar.gz -C myfolder
```

### Basic Meaning

- **Q:** What does `tar` stand for?
  **A:** Tape Archive.
- **Q:** What does the tar part of the command do?
  **A:** It extracts the gzip-compressed tar archive `myfile.tar.gz` into the directory `myfolder`.
- **Q:** What does `-x` mean? **A:** Extract.
- **Q:** What does `-z` mean? **A:** Use gzip compression/decompression.
- **Q:** What does `-f` mean? **A:** Use a file as the archive. The archive filename follows immediately.
- **Q:** What does `-C` mean? **A:** Change to the given directory before extracting.
- **Q:** Why is `-f` usually written last in `-xzf`?
  **A:** Because `-f` expects the archive filename as its argument. So `-xzf myfile.tar.gz` means `-x -z -f myfile.tar.gz`.

### `-C` Directory Questions

- **Q:** Does `-C myfolder` create `myfolder` if it does not exist?
  **A:** No. The directory must already exist, or tar will fail.
- **Q:** How do you create the directory first?
  **A:** `mkdir -p myfolder && tar -xzf myfile.tar.gz -C myfolder`
- **Q:** What happens if `myfolder` does not exist?
  **A:** `tar` exits with an error such as `Cannot chdir: No such file or directory`.
- **Q:** How do you extract into the current directory instead?
  **A:** `tar -xzf myfile.tar.gz`
- **Q:** What if the folder name has spaces? **A:** Quote it:
  `tar -xzf myfile.tar.gz -C "my folder"`

### Listing and Checking

- **Q:** How do you list the contents without extracting?
  **A:** `tar -tzf myfile.tar.gz`
- **Q:** What does `-t` mean? **A:** List/table of contents.
- **Q:** How do you extract with verbose output?
  **A:** `tar -xzvf myfile.tar.gz -C myfolder`
- **Q:** What does `-v` mean? **A:** Verbose — show files as they are processed.

### Other Archive Types

- `.tar.bz2` → `tar -xjf myfile.tar.bz2 -C myfolder`
- `.tar.xz` → `tar -xJf myfile.tar.xz -C myfolder`
- `.tar` → `tar -xf myfile.tar -C myfolder`

- **Q:** Difference between `-z`, `-j`, and `-J`?
  **A:** `-z` = gzip, `-j` = bzip2, `-J` = xz.

### Creating Archives

- **Q:** How do you create a `.tar.gz` archive?
  **A:** `tar -czf archive.tar.gz myfolder`
- **Q:** What does `-c` mean? **A:** Create a new archive.
- **Q:** What does `-czf` mean? **A:** Create a gzip-compressed tar archive with the filename that follows.

### Specific File Extraction

- **Q:** How do you extract only one file?
  **A:** `tar -xzf myfile.tar.gz -C myfolder path/inside/archive/file.txt`
- **Q:** How do you extract a file to stdout?
  **A:** `tar -xOzf myfile.tar.gz path/inside/archive/file.txt`

Note: In `tar`, `-O` means "to stdout". In `wget`, `-O` means "output filename". They are different.

### Common Trick Questions

- **Q:** Is `tar -xzf` the same as `unzip`?
  **A:** No. `unzip` is for `.zip` files. `tar -xzf` is for `.tar.gz`/`.tgz` files.
- **Q:** What does `&&` mean in the full command?
  **A:** Run the `tar` command only if `wget` succeeds.
- **Q:** What happens if `wget` fails? **A:** The `tar` command will not run because of `&&`.
- **Q:** What does `wget -O myfile.tar.gz` do? **A:** Saves the downloaded file as `myfile.tar.gz`.
- **Q:** Difference between `wget -O` and `wget -o`?
  **A:** `-O` = output filename; `-o` = log file.
- **Q:** Does `tar` overwrite existing files by default?
  **A:** Yes, generally it overwrites unless you use options like `--keep-old-files`.
- **Q:** How do you preserve permissions?
  **A:** `tar -xzpvf myfile.tar.gz -C myfolder`
- **Q:** What does `--strip-components=1` do?
  **A:** It removes the first directory level when extracting.
  Example: `tar -xzf myfile.tar.gz -C myfolder --strip-components=1`

### Most Likely Short-Answer Question

> **Q:** What does `tar -xzf myfile.tar.gz -C myfolder` do?

**Answer:**

> It extracts the gzip-compressed tar archive `myfile.tar.gz` into the existing directory `myfolder`.
> `-x` = extract, `-z` = gzip, `-f` = archive file, `-C` = change to directory before extracting.

---

## 6. Copying a File — `cp`

Pattern:

```bash
cp <source> <destination>
```

Copy a file and save it under a new name:

```bash
cp /path/to/original/file.txt /path/to/new/file.txt
```

**Examples:**

```bash
cp original.txt newfile.txt                          # same folder, new name
cp /home/user/original.txt /home/user/backup/new.txt # different folder, new name
cp original.txt /home/user/backup/                   # same name, into folder
cp -r /path/to/source_dir /path/to/destination_dir   # copy directory
```

| Flag | Meaning |
|------|---------|
| `-r` | Recursive (for directories) |
| `-v` | Verbose |
| `-i` | Ask before overwrite |
| `-p` | Preserve permissions/timestamps |
| `-n` | Never overwrite |
| `-u` | Copy only if newer |

For another computer/server, use `scp`:

```bash
scp user@remote_host:/path/to/original.txt /local/path/newfile.txt
```

---

## 7. Moving a File — `mv`

Pattern:

```bash
mv <source> <destination>
```

**Rename a file (same folder):**

```bash
mv original.txt newfile.txt
```

**Move a file to another folder (same name):**

```bash
mv original.txt /home/user/backup/
```

**Move and rename at the same time:**

```bash
mv /home/user/original.txt /home/user/backup/newfile.txt
```

**Move a directory:**

```bash
mv /path/to/source_dir /path/to/destination_dir
```

No `-r` needed for `mv` — unlike `cp`.

| Flag | Meaning |
|------|---------|
| `-v` | Verbose |
| `-i` | Ask before overwrite |
| `-n` | Never overwrite |
| `-u` | Move only if newer |

Summary:

- `cp source newfile` → copy
- `mv source newfile` → move/rename

Move to another computer:

```bash
scp original.txt user@remote_host:/path/to/destination/newfile.txt
rm original.txt
```

Or use `rsync` with `--remove-source-files`:

```bash
rsync -av --remove-source-files original.txt user@remote_host:/path/to/destination/
```

---

## 8. Using `man` (Manual Pages)

Open the manual page for a command:

```bash
man <command>
```

**Examples:**

```bash
man ls
man cp
man mv
man tar
man wget
```

### Navigating Inside a Man Page

- `Space` or `Page Down` — next page
- `b` or `Page Up` — previous page
- `↑` / `↓` — scroll line by line
- `/word` — search for `word`
- `n` — next search match
- `N` — previous search match
- `g` — go to top
- `G` — go to bottom
- `q` — quit

### Man Sections

| Section | Meaning |
|---------|---------|
| 1 | User commands |
| 2 | System calls |
| 3 | Library functions |
| 4 | Devices |
| 5 | File formats |
| 6 | Games |
| 7 | Miscellaneous |
| 8 | System administration |

Open a specific section:

```bash
man 5 passwd
man 1 passwd
```

### Searching Man Pages

```bash
man -k password       # search by keyword
apropos password      # same
man -f ls             # short description
whatis ls             # same
man -a passwd         # all sections
man -w ls             # show file path
```

### Quick Help

```bash
ls --help
cp --help
tar --help
```

Learn about `man` itself:

```bash
man man
```

---

## 9. Finding Files with 9, 10, 14, 16 Characters

Using `ls` in your home directory:

```bash
cd ~
ls -d1 ????????? ?????????? ?????????????? ???????????????? 2>/dev/null
```

Breakdown:

| Pattern | Characters |
|---------|------------|
| `?????????` | 9 |
| `??????????` | 10 |
| `??????????????` | 14 |
| `????????????????` | 16 |

- `-d` → list the directory name itself, not its contents
- `-1` → one file per line
- `2>/dev/null` → hide "No such file" errors

If you also want **hidden files**, use `find`:

```bash
find ~ -maxdepth 1 -type f \( \
  -name '?????????' -o \
  -name '??????????' -o \
  -name '????????????????' -o \
  -name '??????????????' \
\) -printf '%f\n'
```

---

## 10. Seven Crucial Takeaways for the Test

1. **Test Your Commands in the Terminal First.**
   Using the command line to verify your logic before submitting is the single best way to catch syntax errors. If a test question requires modifying a restricted folder (like `/usr/bin`), replicate the structure in a location you own (e.g., `~/Documents`), test your command until it works, and then update the final path in your answer.
   (Also ask yourself: why don't you have access to those folders in the first place?)
   However, if you have to test simple commands, it could use up valuable time.

2. **Leverage the `man` Pages.**
   The `man` command is your built-in cheat sheet. If you haven't been using it regularly, read up on how to navigate manual pages and practice looking up options today.

3. **Create Test Files for Verification.**
   If a question asks how to find or list files matching a pattern (e.g., files ending in `.txt`), take 10 seconds to `touch` a few test files in a safe directory and verify your wildcard/glob syntax.

4. **Understand `sudo` Before Using It.**
   Blindly adding `sudo` to commands indicates a lack of understanding regarding Linux permissions. Review when root privilege is actually required versus when standard user permissions suffice.

5. **Stop Using Your Home Directory for Testing.**
   Testing risky or destructive commands directly in `~` is dangerous and messy. Always `mkdir` a dedicated temporary folder for sandbox testing.

6. **Watch Your Spacing and Formatting.**
   Automated grading is strict. Unnecessary leading or trailing spaces (e.g., `"ls "` instead of `"ls"`) can mark a correct command wrong. Conversely, missing mandatory spaces (e.g., `"ls-la"` instead of `"ls -la"`) is invalid syntax. If a question asks "how do you `cp` all directories: `cp ___`" and you answer `cp *`, then you could also get it wrong instead of answering only `*`. You only need to fill the blank, not repeat the `cp` part.

7. **Practice `wget` Scenarios & Utilize Shell History.**
   Practice real-world `wget` downloads today. During the test, rely on your shell history (`history` command or up arrow) to quickly recall and adapt complex flags you've already verified.

---

## 11. Practice Question Sets

### Section A: Testing Commands First

**Q1.** You need to find all `.txt` files in `/usr/bin` and copy them to `/usr/bin/backup`. Why can't you test this directly in `/usr/bin`?

**Answer:** Because `/usr/bin` is owned by `root`. A normal user does not have write permission there. Test in a folder you own first.

```bash
mkdir -p ~/Documents/practice/usr_bin
cd ~/Documents/practice/usr_bin
touch file1.txt file2.txt file3.log
mkdir backup
find . -name "*.txt" -exec cp {} backup/ \;
ls backup/
```

**Q2.** Test this in `~/Documents/practice` before submitting: *Find all files ending in `.log` in `/var/log` and move them to `/var/log/old`.*

```bash
mkdir -p ~/Documents/practice/var_log/old
cd ~/Documents/practice/var_log
touch a.log b.log c.txt d.log
find . -name "*.log" -exec mv {} old/ \;
ls old/
```

Final answer:

```bash
find /var/log -name "*.log" -exec mv {} /var/log/old/ \;
```

### Section B: Man Pages

**Q3.** Open the manual page for `cp`.

```bash
man cp
```

**Q4.** Inside a man page, search for "recursive".

Type `/recursive`, press Enter. `n` for next, `N` for previous.

**Q5.** Open section 5 of the `passwd` man page.

```bash
man 5 passwd
```

**Q6.** One-line description of `ls`.

```bash
whatis ls
# or
man -f ls
```

**Q7.** Search all man pages for "password".

```bash
man -k password
# or
apropos password
```

### Section C: Creating Test Files

**Q8.** List all files ending in `.txt`.

```bash
mkdir -p ~/Documents/practice/globtest
cd ~/Documents/practice/globtest
touch file1.txt file2.txt notes.md image.png
ls *.txt
```

**Q9.** List files with exactly 9 characters.

```bash
ls -d ????????? 2>/dev/null
```

**Q10.** List files starting with `report` and ending with `.pdf`.

```bash
touch report1.pdf report2.pdf report3.txt other.pdf
ls report*.pdf
```

### Section D: Understanding `sudo`

**Q11.** Which needs `sudo`?
a) `ls /usr/bin` b) `cp file.txt /usr/bin/` c) `cat /etc/passwd` d) `mkdir /usr/bin/newfolder`

**Answer:** b and d need `sudo`.

**Q12.** Do you need `sudo` to copy to `~/Documents`? **No.**

**Q13.** Why does `sudo ls /root` work but `ls /root` fails?

**Answer:** `/root` has permissions like `dr-xr-x---` — only root can read it. `sudo` temporarily gives root privileges.

### Section E: Sandbox Testing

**Q14.** What's wrong with `rm -rf *` in your home directory?

**Answer:** It deletes **everything** in your current directory. Always `mkdir` a sandbox first.

**Q15.** Write commands to create a safe sandbox, add test files, and clean up.

```bash
mkdir -p ~/Documents/sandbox
cd ~/Documents/sandbox
touch a.txt b.txt c.log
ls
cd ~
rm -rf ~/Documents/sandbox
```

### Section F: Spacing & Formatting

**Q16.** `cp ___ /backup` — copy all files. **Answer:** `*` (not `cp *`)

**Q17.** Is `ls-la` valid? **No.** Correct: `ls -la`

**Q18.** Is `ls ` (trailing space) the same as `ls`? Functionally yes, but grading may mark it wrong.

**Q19.** `mv ___ /tmp` — move all `.log` files. **Answer:** `*.log`

**Q20.** Which is correct?
a) `tar -xzf file.tar.gz -C myfolder`
b) `tar-xzf file.tar.gz -C myfolder`
c) `tar -xzf file.tar.gz -C  myfolder`
d) `tar -xzf file.tar.gz -C myfolder `

**Answer:** a)

### Section G: `wget` Scenarios

**Q21.** Download and save as `myfile.zip`.

```bash
wget -O myfile.zip "https://example.com/file.zip"
```

**Q22.** Download and extract a `.tar.gz` into `myfolder`.

```bash
mkdir -p myfolder
wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz -C myfolder
```

**Q23.** Difference between `wget -O` and `wget -o`?

- `-O` (capital) = output filename.
- `-o` (lowercase) = log file.

**Q24.** Rerun an earlier command quickly.

Use `history | grep wget`, then `!123`. Or just press `Ctrl+R` and type `wget`.

**Q25.** Download, extract, and list in one line.

```bash
mkdir -p myfolder && wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz -C myfolder && ls myfolder
```

### Section H: Mixed

**Q26.** List all files in home directory with exactly 14 characters, including hidden.

```bash
find ~ -maxdepth 1 -type f -name '??????????????' -printf '%f\n'
```

**Q27.** Copy all `.conf` files from `/etc` to `~/backup_conf`. Need `sudo`? **No.**

```bash
mkdir -p ~/backup_conf
cp /etc/*.conf ~/backup_conf/
```

**Q28.** What does this do?

```bash
wget -O data.tar.gz "https://example.com/data.tar.gz" && tar -xzf data.tar.gz -C ~/Documents/sandbox
```

**Answer:** Downloads `data.tar.gz`, then extracts it into `~/Documents/sandbox`. The folder must already exist.

**Q29.** `mv ___ /tmp/old` — move all `.bak` files. **Answer:** `*.bak`

**Q30.** Why is testing in `~/Documents/sandbox` better than `~`?

- Keeps home clean.
- Prevents accidental deletion.
- Lets you safely use destructive commands.
- Mirrors restricted folders without `sudo`.

---

## 12. Alternatives to `history`

| Method | How to use | Example |
|--------|-----------|---------|
| **Up arrow** | Press `↑` repeatedly | Cycles through previous commands |
| **Ctrl + R** | Press `Ctrl+R`, type part of command | Reverse search — fastest |
| **`!!`** | Run the last command again | `sudo !!` reruns last with sudo |
| **`!n`** | Run command number `n` | `!42` |
| **`!string`** | Run last command starting with `string` | `!wget` |
| **`!?string?`** | Run last command containing `string` | `!?tar?` |
| **`fc -l`** | List recent commands | Similar to history |
| **`fc`** | Open last command in editor | Fix and rerun |
| **`alias`** | Create shortcuts | `alias dl='wget -O'` |
| **Tab completion** | Press `Tab` to autocomplete | Saves typing |
| **Script file** | Save commands to `.sh` | `./myscript.sh` |
| **`script` command** | Log entire session | `script session.log` |

**Ctrl+R is the best alternative to `history`.**

```bash
# Press Ctrl+R, then type:
wget
# Shows the last wget command. Press Ctrl+R again for older ones.
# Press Enter to run, or arrow keys to edit first.
```

---

## 13. Keeping Your Directory Clean While Testing

| Method | Command | Why |
|--------|---------|-----|
| **Subshell** | `(cd /tmp && command)` | Runs in a subshell — original directory unchanged |
| **`pushd`/`popd`** | `pushd /tmp` ... `popd` | Saves your place and returns |
| **`cd -`** | `cd -` | Toggles between two directories |
| **`mktemp -d`** | `tmp=$(mktemp -d)` | Creates a unique temp directory |
| **`trap` cleanup** | `trap 'rm -rf $tmp' EXIT` | Auto-deletes temp dir when script ends |
| **Sandbox folder** | `mkdir -p ~/Documents/sandbox` | Dedicated safe space |
| **`cd ~`** | `cd ~` | Return home instantly |
| **`cd /tmp`** | `cd /tmp` | Use system temp for scratch work |

**Subshell example (cleanest method):**

```bash
(cd /tmp && touch a.txt b.txt && ls *.txt)
# You are still in your original directory after this runs
pwd
```

**mktemp with auto-cleanup:**

```bash
tmp=$(mktemp -d)
cd "$tmp"
touch test1 test2
ls
cd ~
rm -rf "$tmp"
```

**pushd/popd example:**

```bash
pushd /tmp
touch a.txt b.txt
ls *.txt
popd
# Back to where you started
```

---

## 14. Multiple Ways to Get the Same Output

### 14.1 List files with exactly 9 characters

```bash
# Method 1: ls with glob (simplest)
ls -d ????????? 2>/dev/null

# Method 2: find
find . -maxdepth 1 -name '?????????' -printf '%f\n'

# Method 3: ls piped to grep
ls | grep -E '^.{9}$'

# Method 4: ls piped to awk
ls | awk 'length($0)==9'

# Method 5: printf with glob
printf '%s\n' ?????????

# Method 6: for loop
for f in ?????????; do echo "$f"; done

# Method 7: find with regex
find . -maxdepth 1 -regextype posix-extended -regex '.*/[^/]{9}'
```

### 14.2 List files ending in `.txt`

```bash
# Method 1: glob (simplest)
ls *.txt

# Method 2: find
find . -maxdepth 1 -name '*.txt'

# Method 3: grep
ls | grep '\.txt$'

# Method 4: printf
printf '%s\n' *.txt

# Method 5: for loop
for f in *.txt; do echo "$f"; done

# Method 6: find with type filter
find . -maxdepth 1 -type f -name '*.txt' -printf '%f\n'
```

### 14.3 Files that start with `d` and end with `.log`

```bash
# Method 1: ls glob
ls d*.log

# Method 2: find
find . -maxdepth 1 -name 'd*.log'

# Method 3: grep
ls | grep '^d.*\.log$'

# Method 4: grep -E
ls | grep -E '^d.*\.log$'

# Method 5: awk
ls | awk '/^d.*\.log$/'

# Method 6: printf
printf '%s\n' d*.log

# Method 7: for loop
for f in d*.log; do echo "$f"; done

# Method 8: find with regex
find . -maxdepth 1 -regextype posix-extended -regex '.*/d[^/]*\.log'

# Method 9: compgen
compgen -G 'd*.log'

# Method 10: case-insensitive find
find . -maxdepth 1 -type f -iname 'd*.log' -printf '%f\n'
```

### 14.4 Copy a file to a new name

```bash
cp original.txt newfile.txt
cp -v original.txt newfile.txt
cat original.txt > newfile.txt
install -m 644 original.txt newfile.txt
rsync -a original.txt newfile.txt
dd if=original.txt of=newfile.txt
tee newfile.txt < original.txt
```

### 14.5 Move / rename a file

```bash
mv original.txt newfile.txt
cp original.txt newfile.txt && rm original.txt
rsync -a --remove-source-files original.txt newfile.txt
mv -v original.txt newfile.txt
mv -n original.txt newfile.txt
```

### 14.6 Download with a new name

```bash
wget -O myfile.zip "https://example.com/file.zip"
curl -o myfile.zip "https://example.com/file.zip"
curl -L -o myfile.zip "https://example.com/file.zip"
wget "https://example.com/file.zip" && mv file.zip myfile.zip
curl "https://example.com/file.zip" > myfile.zip
```

### 14.7 Download and extract tar.gz into a folder

```bash
# Method 1: wget -O + tar -C
mkdir -p myfolder
wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz -C myfolder

# Method 2: curl + tar --directory
mkdir -p myfolder
curl -o myfile.tar.gz "https://example.com/somefile.tar.gz" && tar -xzf myfile.tar.gz --directory=myfolder

# Method 3: cd into folder first
mkdir -p myfolder
wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && cd myfolder && tar -xzf ../myfile.tar.gz

# Method 4: pipe directly
mkdir -p myfolder
curl -L "https://example.com/somefile.tar.gz" | tar -xzf - -C myfolder

# Method 5: gunzip pipe
mkdir -p myfolder
wget -O - "https://example.com/somefile.tar.gz" | gunzip | tar -xf - -C myfolder

# Method 6: zcat pipe
mkdir -p myfolder
wget -O myfile.tar.gz "https://example.com/somefile.tar.gz" && zcat myfile.tar.gz | tar -xf - -C myfolder
```

### 14.8 Combined (9, 10, 14, 16 characters)

```bash
# Method 1: ls with multiple globs
ls -d1 ????????? ?????????? ?????????????? ???????????????? 2>/dev/null

# Method 2: find with -o
find ~ -maxdepth 1 \( -name '?????????' -o -name '??????????' -o -name '??????????????' -o -name '????????????????' \) -printf '%f\n'

# Method 3: ls piped to grep
ls | grep -E '^.{9}$|^.{10}$|^.{14}$|^.{16}$'

# Method 4: ls piped to awk
ls | awk 'length==9 || length==10 || length==14 || length==16'

# Method 5: for loop with case
for f in *; do
  n=${#f}
  case $n in
    9|10|14|16) echo "$f" ;;
  esac
done
```

---

## 15. Case-Insensitive `grep` (`-i`)

Flag for case-insensitive matching:

```bash
grep -i "pattern"
# or
grep --ignore-case "pattern"
```

Combined with extended regex:

```bash
grep -iE "pattern"
```

### Examples

```bash
ls | grep -i '\.txt$'                 # files ending .txt (any case)
ls | grep -i 'report'                 # contains "report" (any case)
ls | grep -iE '^.{9}$'                # exactly 9 chars
ls | grep -i '_'                      # contains underscore
ls | grep -iE '^.{9}$|^.{10}$|^.{14}$|^.{16}$'   # multiple lengths
ls | grep -iE '\.(txt|log)$'          # .txt or .log
```

### Case-Insensitive with `find`

```bash
find . -maxdepth 1 -type f -iname '*.txt'
find . -maxdepth 1 -type f -iname '*report*'
find . -maxdepth 1 -type f \( -iname '*.txt' -o -iname '*.log' \)
```

### Summary Table

| Task | Standard | Case-insensitive grep | Case-insensitive find |
|------|----------|-----------------------|------------------------|
| Files ending `.txt` | `ls *.txt` | `ls \| grep -i '\.txt$'` | `find . -iname '*.txt'` |
| Contains "report" | `ls *report*` | `ls \| grep -i 'report'` | `find . -iname '*report*'` |
| Exactly 9 chars | `ls -d ?????????` | `ls \| grep -iE '^.{9}$'` | `find . -name '?????????'` |
| Contains underscore | `ls *_*` | `ls \| grep -i '_'` | `find . -name '*_*'` |
| Multiple extensions | `ls *.{txt,log}` | `ls \| grep -iE '\.(txt\|log)$'` | `find . \( -iname '*.txt' -o -iname '*.log' \)` |

**Key points:**

- `grep -i` = ignore case.
- `grep -iE` = ignore case + extended regex.
- `find -iname` = case-insensitive filename search.
- `ls` globs are **not** case-insensitive by default.
- In fill-in-the-blank, only write `-i` or `-iE`, not `grep -i`.

---

## 16. Files Starting with `d` and Ending with `.log`

First, correction about your glob:

```bash
ls d*.log*
```

This matches: **starts with `d`**, then anything, then `.log`, then anything.

So it matches `data.log`, `data.log.txt`, `d.log`, `debug.log.bak`.

If you want **starts with `d` AND ends with `.log` exactly**:

```bash
ls d*.log
```

No trailing `*`. That is the cleanest, test-ready answer.

### All the Ways

**Method 1: `ls` glob (simplest)**

```bash
ls d*.log
ls d*.log 2>/dev/null
```

**Method 2: `find`**

```bash
find . -maxdepth 1 -type f -name 'd*.log' -printf '%f\n'
find . -maxdepth 1 -name 'd*.log'
```

**Method 3: `ls` piped to `grep`**

```bash
ls | grep '^d.*\.log$'
ls | grep -i '^d.*\.log$'
```

**Method 4: `ls | grep -E`**

```bash
ls | grep -E '^d.*\.log$'
```

**Method 5: `awk`**

```bash
ls | awk '/^d.*\.log$/'
ls | awk '$0 ~ /^d.*\.log$/'
```

**Method 6: `printf`**

```bash
printf '%s\n' d*.log
```

**Method 7: `for` loop**

```bash
for f in d*.log; do echo "$f"; done
```

**Method 8: `find` with regex**

```bash
find . -maxdepth 1 -regextype posix-extended -regex '.*/d[^/]*\.log'
```

**Method 9: `compgen`**

```bash
compgen -G 'd*.log'
```

**Method 10: case-insensitive `find`**

```bash
find . -maxdepth 1 -type f -iname 'd*.log' -printf '%f\n'
```

### Side-by-Side

| Method | Command |
|--------|---------|
| 1 | `ls d*.log` |
| 2 | `find . -maxdepth 1 -name 'd*.log'` |
| 3 | `ls \| grep '^d.*\.log$'` |
| 4 | `ls \| grep -E '^d.*\.log$'` |
| 5 | `ls \| awk '/^d.*\.log$/'` |
| 6 | `printf '%s\n' d*.log` |
| 7 | `for f in d*.log; do echo "$f"; done` |
| 8 | `find . -regextype posix-extended -regex '.*/d[^/]*\.log'` |
| 9 | `compgen -G 'd*.log'` |
| 10 | `find . -iname 'd*.log'` |

### Key Distinction

| Pattern | Meaning | Matches `data.log.txt`? |
|---------|---------|--------------------------|
| `d*.log` | starts d, ends `.log` | ❌ No |
| `d*.log*` | starts d, contains `.log` | ✅ Yes |

---

## 17. Fill-in-the-Blank Rules

| Question | Answer | NOT |
|----------|--------|-----|
| `cp ___ /backup` | `*` | `cp *` |
| `mv ___ /tmp/old` | `*.bak` | `mv *.bak` |
| `tar ___ file.tar.gz` | `-xzf` | `tar -xzf` |
| `ls ___` (9 chars) | `?????????` | `ls ?????????` |
| `ls \| grep ___ '^.{9}$'` | `-E` or `-iE` | `grep -E` |
| `ls ___` (start d, end .log) | `d*.log` | `ls d*.log` |

---

## 18. Spacing & Formatting Rules

| Correct | Wrong | Why |
|---------|-------|-----|
| `ls -la` | `ls-la` | Missing space |
| `ls` | `ls ` | Trailing space |
| `tar -xzf f.tar.gz -C dir` | `tar -xzf f.tar.gz -C  dir` | Double space |
| `cp a b` | `cp  a  b` | Extra spaces |
| `grep -i 'x'` | `grep  -i  'x'` | Extra spaces |

---

## 19. `sudo` Decision Table

| Task | Need sudo? |
|------|------------|
| `ls /usr/bin` | No |
| `cat /etc/passwd` | No |
| `cp file /usr/bin/` | Yes |
| `mkdir /usr/bin/new` | Yes |
| `ls /root` | Yes |
| `cp file ~/Documents/` | No |
| `rm ~/file.txt` | No |

---

## 20. `echo` and Newlines

`echo` prints a newline by default.

```bash
echo "Hello World "
```

Output:

```
Hello World 
```

Cursor moves to the next line.

**Use straight quotes `"`, not curly quotes `“ ”`.**

If you want **no** newline:

```bash
echo -n "Hello World "
```

If you want an **extra** newline:

```bash
echo -e "Hello World \n"
printf "Hello World \n"
echo "Hello World "
echo
```

| Command | Output |
|---------|--------|
| `echo "Hello World "` | `Hello World ` + newline (default) |
| `echo -n "Hello World "` | `Hello World ` with **no** newline |
| `echo -e "Hello World \n"` | `Hello World ` + newline + extra newline |
| `printf "Hello World \n"` | `Hello World ` + newline |

---

## 21. Complete Command Reference (All Commands + Flags)

### `ls`

| Flag | Meaning |
|------|---------|
| `-l` | Long format |
| `-a` | Show hidden files |
| `-1` | One file per line |
| `-d` | List directory itself |
| `-h` | Human-readable |
| `-t` | Sort by time |
| `-r` | Reverse |
| `-S` | Sort by size |
| `-R` | Recursive |

### `cp`

| Flag | Meaning |
|------|---------|
| `-r` | Recursive |
| `-v` | Verbose |
| `-i` | Ask before overwrite |
| `-p` | Preserve permissions |
| `-n` | Never overwrite |
| `-u` | Copy if newer |

### `mv`

| Flag | Meaning |
|------|---------|
| `-v` | Verbose |
| `-i` | Ask before overwrite |
| `-n` | Never overwrite |
| `-u` | Move if newer |

### `rm`

| Flag | Meaning |
|------|---------|
| `-r` | Recursive |
| `-f` | Force |
| `-i` | Interactive |
| `-v` | Verbose |

### `mkdir`

| Flag | Meaning |
|------|---------|
| `-p` | Create parents |
| `-v` | Verbose |

### `find`

| Flag | Meaning |
|------|---------|
| `-name` | Match name (case-sensitive) |
| `-iname` | Match name (case-insensitive) |
| `-type f` | Regular files |
| `-type d` | Directories |
| `-maxdepth N` | Limit depth |
| `-printf` | Custom output |
| `-exec` | Run command on results |
| `-size` | Match size |
| `-regex` | Regex |
| `-regextype` | Regex dialect |
| `-o` | OR |

### `grep`

| Flag | Meaning |
|------|---------|
| `-i` | Case-insensitive |
| `-E` | Extended regex |
| `-r` | Recursive |
| `-v` | Invert |
| `-n` | Line numbers |
| `-l` | Filenames only |
| `-w` | Whole word |
| `-c` | Count |

### `wget`

| Flag | Meaning |
|------|---------|
| `-O` | Output filename (capital O) |
| `-o` | Log file (lowercase o) |
| `-c` | Continue download |
| `-q` | Quiet |

### `curl`

| Flag | Meaning |
|------|---------|
| `-o` | Output file |
| `-L` | Follow redirects |
| `-O` | Use remote filename |

### `tar`

| Flag | Meaning |
|------|---------|
| `-c` | Create |
| `-x` | Extract |
| `-t` | List |
| `-z` | gzip |
| `-j` | bzip2 |
| `-J` | xz |
| `-f` | Filename (last) |
| `-v` | Verbose |
| `-C` | Change directory |
| `-p` | Preserve permissions |
| `-O` | Stdout |
| `--strip-components=N` | Strip N dirs |

### `man`

| Flag | Meaning |
|------|---------|
| `-k` | Search keyword |
| `-f` | One-line description |
| `-a` | All sections |
| `-w` | Show path |
| `N` | Section number |

### `rsync`

| Flag | Meaning |
|------|---------|
| `-a` | Archive |
| `-v` | Verbose |
| `--remove-source-files` | Delete source after copy |

### `shopt`

| Flag | Meaning |
|------|---------|
| `-s nullglob` | Empty glob returns nothing |
| `-s nocaseglob` | Case-insensitive globbing |

### Other Commands

- `cd ~`, `cd -`, `cd ..`
- `pwd`
- `touch file.txt`
- `echo "text"`, `echo -n`, `echo -e`
- `cat file.txt`
- `chmod 644 file.txt`
- `pushd /tmp`, `popd`
- `mktemp -d`
- `trap 'rm -rf "$tmp"' EXIT`
- `install -m 644 a b`
- `dd if=a of=b`
- `tee newfile.txt < original.txt`
- `script session.log`
- `compgen -G '?????????'`
- `printf '%s\n' d*.log`
- `whatis ls`
- `apropos password`
- `history`
- `sudo command`
- `scp user@host:/path/file ./newfile`

---

## 22. Wildcards / Glob Characters

| Char | Meaning | Example | Matches |
|------|---------|---------|---------|
| `*` | Any number of characters (0+) | `*.txt` | `a.txt`, `notes.txt` |
| `?` | Exactly one character | `?????????` | any 9-char name |
| `[abc]` | Any one of a, b, c | `file[123].txt` | `file1.txt`, `file2.txt` |
| `[a-z]` | Range | `file[a-z].txt` | `filea.txt` |
| `[!abc]` | Not a, b, c | `file[!0-9].txt` | `filea.txt` |
| `{a,b}` | Brace expansion | `*.{txt,log}` | `.txt` or `.log` |
| `~` | Home directory | `~/Documents` | `/home/user/Documents` |

---

## 23. Regex Characters (grep, find, awk)

| Char | Meaning | Example |
|------|---------|---------|
| `^` | Start of line | `^d` = starts with d |
| `$` | End of line | `\.log$` = ends with .log |
| `.` | Any single character | `d.*` |
| `\.` | Literal dot | `\.log` |
| `.*` | Any characters | `d.*\.log$` |
| `\|` | OR | `txt\|log` |
| `{n}` | Exactly n times | `^.{9}$` = exactly 9 chars |
| `[abc]` | Character class | `[0-9]` = digit |
| `[^abc]` | Negated class | `[^0-9]` = non-digit |
| `+` | One or more | `d+` |
| `?` | Zero or one | `colou?r` |
| `\` | Escape | `\.` |
| `()` | Group | `(txt\|log)` |

---

## 24. Redirection & Operators

| Char | Meaning | Example |
|------|---------|---------|
| `>` | Redirect stdout (overwrite) | `ls > out.txt` |
| `>>` | Append stdout | `ls >> out.txt` |
| `<` | Redirect stdin | `cat < file.txt` |
| `2>` | Redirect stderr | `cmd 2> err.txt` |
| `2>/dev/null` | Discard errors | `ls x 2>/dev/null` |
| `2>&1` | stderr to stdout | `cmd > out.txt 2>&1` |
| `\|` | Pipe | `ls \| grep txt` |
| `&&` | Run next if success | `wget ... && tar ...` |
| `\|\|` | Run next if failure | `cmd1 \|\| echo fail` |
| `;` | Run sequentially | `cmd1 ; cmd2` |
| `&` | Background | `cmd &` |
| `$( )` | Command substitution | `tmp=$(mktemp -d)` |
| `` ` ` `` | Command substitution (old) | `` tmp=`mktemp -d` `` |
| `!` | History / negate | `!!`, `!wget` |
| `#` | Comment | `# comment` |
| `/` | Path separator | `/usr/bin` |
| `-` | Flag prefix / stdin | `ls -l`, `tar -` |
| `--` | Long flag | `--help` |
| `.` | Current directory | `./script.sh` |
| `..` | Parent directory | `cd ..` |
| `~` | Home | `cd ~` |
| `'...'` | Literal string | `'*.txt'` |
| `"..."` | String with expansion | `"$HOME"` |
| `\` | Escape next char | `\.` |

**Glob vs literal:**

```bash
ls *.txt              # glob expands → lists files
ls '*.txt'            # literal → tries to find file named "*.txt"
ls "*.txt"            # same as single quotes here
```

---

## 25. Quick Reference Cheat Sheet

| Task | Command |
|------|---------|
| Read manual | `man <command>` |
| Search man | `man -k <word>` |
| One-line description | `whatis <command>` |
| Exactly 9 characters | `ls -d ????????? 2>/dev/null` |
| Files ending `.txt` | `ls *.txt` |
| Files starting d, ending .log | `ls d*.log` |
| Copy | `cp source dest` |
| Move/rename | `mv source dest` |
| Copy directory | `cp -r source dest` |
| Download with new name | `wget -O newname URL` |
| Download + extract | `wget -O file.tar.gz URL && tar -xzf file.tar.gz -C folder` |
| Create sandbox | `mkdir -p ~/Documents/sandbox` |
| Check history | `history \| grep wget` |
| Run last command | `!!` or up arrow |
| Reverse search | `Ctrl+R` |
| Only use sudo when | writing to system folders like `/usr/bin`, `/etc`, `/var` |
| Case-insensitive grep | `grep -i "pattern"` |
| Case-insensitive + regex | `grep -iE "pattern"` |
| Find case-insensitive | `find . -iname '*.txt'` |
| Exactly 9 chars (grep) | `ls \| grep -E '^.{9}$'` |
| Exactly 9 chars (awk) | `ls \| awk 'length==9'` |
| Multiple lengths | `ls \| grep -E '^.{9}$\|^.{10}$\|^.{14}$\|^.{16}$'` |
| Subshell (stay clean) | `(cd /tmp && cmd)` |
| Auto-cleanup | `tmp=$(mktemp -d); trap 'rm -rf $tmp' EXIT` |
| Print with newline | `echo "text"` |
| Print without newline | `echo -n "text"` |
| Print extra newline | `echo -e "text\n"` |

---

Yes. I found the **200-question Bash Fundamentals quiz** you uploaded. I’ll give you the **question followed directly by the correct answer**, in the same order as your uploaded test. :chatgpt-content-reference{index="0"}

## Bash Fundamentals — 200 Questions and Answers

1. To search for files named `config.json` within `/etc/nginx`, use `find /etc/nginx -name ___`.  
**Answer:** `config.json`

2. To view the manual page for the `ls` command, type `___ ls`.  
**Answer:** `man`

3. To create a directory named `modules` inside `/usr/share`, use `mkdir /usr/share/___`.  
**Answer:** `modules`

4. Which `tar` command creates a gzipped archive of `my_project` while excluding `node_modules`?  
**Answer:** `tar -czf project.tar.gz --exclude=node_modules my_project/`

5. To recall and re-execute a previous command, use the `___` command, then press the Up arrow.  
**Answer:** `history`

6. To display the manual page for `wget`, type `man ___`.  
**Answer:** `wget`

7. What is the purpose of `tree -L 2`?  
**Answer:** To list directories and files up to 2 levels deep.

8. To list files beginning with `d` and ending in `.log`, use `ls d*.log` or `ls ___`.  
**Answer:** `d*.log`

9. To extract `backup.tar` compressed with bzip2, use `tar -xjf ___`.  
**Answer:** `backup.tar`

10. To extract `website.tar.bz2` to `/var/www`, use `tar -xjf website.tar.bz2 -C ___`.  
**Answer:** `/var/www`

11. To extract `website.tar.gz` to `/var/www/html`, use `tar -xzf website.tar.gz -C ___`.  
**Answer:** `/var/www/html`

12. To remove `old_report.doc` without confirmation, use `rm ___ old_report.doc`.  
**Answer:** `-f`

13. To display the last 250 lines of `access.log`, use `tail -n ___ access.log`.  
**Answer:** `250`

14. To copy `config.txt` to `config_backup.txt`, use `cp config.txt ___`.  
**Answer:** `config_backup.txt`

15. To remove `temp_data` and all its contents without prompting, use `rm -rf ___`.  
**Answer:** `temp_data`

16. To change to your home directory, you can type `cd` or `cd ___`.  
**Answer:** `~`

17. To download `https://www.example.com/data.csv` with its original filename, use `wget ___`.  
**Answer:** `https://www.example.com/data.csv`

18. To remove `temp_report.csv` without confirmation, use `rm ___ temp_report.csv`.  
**Answer:** `-f`

19. To search for `install.log` inside `/var/log`, use `find /var/log -name ___`.  
**Answer:** `install.log`

20. To copy `document.txt` to `doc_copy.txt`, use `cp document.txt ___`.  
**Answer:** `doc_copy.txt`

21. To find `"failed login"` in `auth.log` and show 10 lines after each match, use `grep -A 10 "failed login" ___`.  
**Answer:** `auth.log`

22. To list files having exactly five characters in their name, use `ls ___`.  
**Answer:** `?????`

23. To search for `.bak` files in `/home/user/documents`, use `find /home/user/documents -name ___`.  
**Answer:** `*.bak`

24. To move `config.yaml` to `~/settings`, use `mv config.yaml ___/settings/`.  
**Answer:** `~`

25. To remove `temp_image.png` without confirmation, use `rm ___ temp_image.png`.  
**Answer:** `-f`

26. To copy the `docs` directory and its contents to `~/backups/`, use `cp -r docs ___`.  
**Answer:** `~/backups/`

27. Which `wget` option resumes a partially downloaded file?  
**Answer:** `-c` or `--continue`

28. To list files beginning with `r` and ending in `.txt`, use `ls r*.txt` or `ls ___`.  
**Answer:** `r*.txt`

29. To download an FTP file and save it as `app.zip`, use `wget -O app.zip ___`.  
**Answer:** `ftp://example.com/software.zip`

30. Which `ls` option sorts files by modification time with newest first?  
**Answer:** `ls -t`

31. To display the manual page for `rm`, type `man ___`.  
**Answer:** `rm`

32. What does `ssh-keygen -t rsa` do?  
**Answer:** Generates an SSH key pair using the RSA algorithm.

33. To copy `document.docx` to `~/reports/`, use `cp document.docx ___/reports/`.  
**Answer:** `~`

34. To create `config_files` inside `/etc`, use `mkdir /etc/___`.  
**Answer:** `config_files`

35. To search for `database.sql` inside `/opt/app`, use `find /opt/app -name ___`.  
**Answer:** `database.sql`

36. To find `"warning"` in `messages.log` and display 2 lines before and after, use `grep -C 2 "warning" ___`.  
**Answer:** `messages.log`

37. Which `cp` option asks before overwriting a file?  
**Answer:** `-i` or `--interactive`

38. To list files having exactly nine characters in their name, use `ls ___`.  
**Answer:** `?????????`

39. To search for `"warning"` case-insensitively and show 2 lines before and after, use `grep -i -C 2 "warning" ___`.  
**Answer:** `debug.log`

40. Which command displays previously executed commands?  
**Answer:** `history`

41. Replace `old_value` with `new_value` and print the result without modifying the original file.  
**Answer:** `cat data.csv | sed 's/old_value/new_value/g'`

42. Which `sort` option sorts in reverse order?  
**Answer:** `-r`

43. Which command writes the current shell history to `~/.bash_history`?  
**Answer:** `history -w`

44. To search for `index.php` in `/var/www/html`, use `find /var/www/html -name ___`.  
**Answer:** `index.php`

45. To create `uploads` inside `/var/www/html`, use `mkdir /var/www/html/___`.  
**Answer:** `uploads`

46. To list files beginning with `b` and ending in `.bak`, use `ls b*.bak` or `ls ___`.  
**Answer:** `b*.bak`

47. To change to the root directory, use `cd ___`.  
**Answer:** `/`

48. To search for `config.json` inside `/etc`, use `find /etc -name ___`.  
**Answer:** `config.json`

49. To list files modified today using `grep`, you could use `ls -l | grep "___"`.  
**Answer:** The current date/day, e.g. `24`

50. To list regular `.txt` files, use `ls -p | grep -v / | grep ___`.  
**Answer:** `\.txt$`

51. To copy `report.txt` to the `backups` directory, use `cp report.txt ___`.  
**Answer:** `backups/`

52. Which `wget` option saves a download under a different filename?  
**Answer:** `-O`

53. To create `temp_backup` inside `/var/log`, use `mkdir /var/log/___`.  
**Answer:** `temp_backup`

54. To display the first 20 lines of `kern.log`, use `head -n ___ kern.log`.  
**Answer:** `20`

55. To download `setup.sh` using its original name, use `wget ___`.  
**Answer:** `http://example.com/setup.sh`

56. To search for `"error"` case-insensitively in `syslog` and show 3 lines before and after, use `grep -i -C 3 "error" ___`.  
**Answer:** `syslog`

57. Which command displays the full path of the current directory?  
**Answer:** `pwd`

58. What does `tree` do without options?  
**Answer:** Lists the current directory and subdirectories in a tree-like format.

59. To display the manual page for `mkdir`, type `man ___`.  
**Answer:** `mkdir`

60. In `man`, which character searches forward?  
**Answer:** `/` followed by the search word

61. To search for `"warning"` case-insensitively in `syslog` and show 10 lines after each match, use `grep -i -A 10 "warning" ___`.  
**Answer:** `syslog`

62. To download `file.zip` as `my_download.zip`, use `wget -O my_download.zip ___`.  
**Answer:** `https://secure.example.com/file.zip`

63. To create `configs` inside `/etc`, use `mkdir /etc/___`.  
**Answer:** `configs`

64. To display the last 50 lines of `server.log`, use `tail -n ___ server.log`.  
**Answer:** `50`

65. To find lines containing digits in `numbers.txt`, use `grep "___" numbers.txt`.  
**Answer:** `[0-9]`

66. To list `.gz` files in `/var/log`, use `ls /var/log/___`.  
**Answer:** `*.gz`

67. To remove `temp_image.jpeg` without confirmation, use `rm ___ temp_image.jpeg`.  
**Answer:** `-f`

68. To search for `logs.txt` inside `/var/log`, use `find /var/log -name ___`.  
**Answer:** `logs.txt`

69. Which `mv` command moves all `.bak` files into `old_files`?  
**Answer:** `mv *.bak old_files/`

70. To search for `"connection"` case-insensitively and show 1 line before and after, use `grep -i -C 1 "connection" ___`.  
**Answer:** `network.log`

71. To remove `temp_logs.tar.gz` without confirmation, use `rm ___ temp_logs.tar.gz`.  
**Answer:** `-f`

72. To remove `temp_document.docx` without confirmation, use `rm ___ temp_document.docx`.  
**Answer:** `-f`

73. To list files with exactly seven characters followed by `.log`, use `ls ???????.log` or `ls ___`.  
**Answer:** `???????.log`

74. To create `temp_files` two levels above the current directory, use `mkdir ___/temp_files`.  
**Answer:** `../..`

75. To download `data.csv` as `sales_data.csv`, use `wget -O sales_data.csv ___`.  
**Answer:** `http://example.com/data.csv`

76. To display the last 50 lines of `syslog`, use `tail -n ___ syslog`.  
**Answer:** `50`

77. Which `ls` commands display hidden files?  
**Answer:** `ls -a` and `ls -al`

78. To list files having exactly fourteen characters, use `ls ___`.  
**Answer:** `??????????????`

79. To change directly to `/etc`, use `cd ___`.  
**Answer:** `/etc`

80. To search for `"connection"` case-insensitively and show 5 lines before each match, use `grep -i -B 5 "connection" ___`.  
**Answer:** `network.log`

81. To list files having exactly fifteen characters, use `ls ___`.  
**Answer:** `???????????????`

82. To search for `"connection refused"` and show 1 line before and after, use `grep -C 1 "connection refused" ___`.  
**Answer:** `network.log`

83. To display the first 10 lines of `messages.log`, use `head -n ___ messages.log`.  
**Answer:** `10`

84. To list files beginning with `f`, followed by exactly two characters, then `.txt`, use `ls f??.txt` or `ls ___`.  
**Answer:** `f??.txt`

85. To search history for commands containing `config` and display them page by page, use `history | grep 'config' | ___`.  
**Answer:** `less`

86. To display the first 10 lines of `ls -l`, use `ls -l | ___ -n 10`.  
**Answer:** `head`

87. To copy `report.docx` to `final_report.docx`, use `cp report.docx ___`.  
**Answer:** `final_report.docx`

88. What is the main difference between `cat` and `less`?  
**Answer:** `cat` displays the entire file at once, while `less` allows pagination and navigation.

89. Which commands can find `"warning"` or `"error"` using regular expressions?  
**Answer:** `grep -E "warning|error" system.log` or `grep "warning\|error" system.log`

90. To download `archive.tar.gz` as `my_archive.tar.gz`, use `wget -O my_archive.tar.gz ___`.  
**Answer:** `http://example.com/archive.tar.gz`

91. To search for `"error"` case-sensitively and show 1 line before and after, use `grep -C 1 "error" ___`.  
**Answer:** `syslog`

92. To display the manual page for `ls`, type `man ___`.  
**Answer:** `ls`

93. To list files beginning with `d` and ending with `.csv`, use `ls d*.csv` or `ls ___`.  
**Answer:** `d*.csv`

94. To move `old_config.txt` to `new_config.txt`, use `mv old_config.txt ___`.  
**Answer:** `new_config.txt`

95. Which symbol pipes one command's output into another command?  
**Answer:** `|`

96. To clear the current shell's entire history list, use `history -___`.  
**Answer:** `-c` → `history -c`

97. To list files having exactly three characters, use `ls ___`.  
**Answer:** `???`

98. To list all `.bak` files, use `ls ___`.  
**Answer:** `*.bak`

99. To list files beginning with `t` and ending with `.txt`, use `ls t*.txt` or `ls ___`.  
**Answer:** `t*.txt`

100. To search for `"failed login"` and show 1 line before and after, use `grep -C 1 "failed login" ___`.  
**Answer:** `auth.log`

101. To list files having exactly two characters, use `ls ___`.  
**Answer:** `??`

102. Which command creates a temporary alias `c` for `clear`?  
**Answer:** `alias c='clear'`

103. To extract `backup.tar` compressed with bzip2, use `tar -xjf ___`.  
**Answer:** `backup.tar`

104. To copy `presentation.pptx` to `final_presentation.pptx`, use `cp presentation.pptx ___`.  
**Answer:** `final_presentation.pptx`

105. To create an SSH key pair without a passphrase, use `ssh-keygen -P ___`.  
**Answer:** `""`

106. To copy `/etc/config.txt` to the current directory, use `cp /etc/config.txt ___`.  
**Answer:** `.`

107. Which command creates a permanent alias `ll` for `ls -l` when placed in `.bashrc`?  
**Answer:** `alias ll='ls -l'`

108. To display the manual page for `find`, type `man ___`.  
**Answer:** `find`

109. To display the manual page for `tail`, type `man ___`.  
**Answer:** `tail`

110. Which `ssh` option forwards a local port to a remote port?  
**Answer:** `-L`

111. To copy `config.json` to `config_prod.json`, use `cp config.json ___`.  
**Answer:** `config_prod.json`

112. To list the contents of `app.tar.gz` without extracting, use `tar -tzf ___`.  
**Answer:** `app.tar.gz`

113. To list files with exactly two characters ending in `.md`, use `ls ??.md` or `ls ___`.  
**Answer:** `??.md`

114. To display the last 50 lines of `auth.log`, use `tail -n ___ auth.log`.  
**Answer:** `50`

115. To extract `software.tar.bz2`, use `tar -xjf ___`.  
**Answer:** `software.tar.bz2`

116. To list files having exactly ten characters, use `ls ___`.  
**Answer:** `??????????`

117. To list files beginning with `a` and ending with `e`, use `ls a*e` or `ls ___`.  
**Answer:** `a*e`

118. To display the current working directory, use the `___` command.  
**Answer:** `pwd`

119. To search for `config.yaml` inside `/etc`, use `find /etc -name ___`.  
**Answer:** `config.yaml`

120. To list the contents of `archive.tar.gz` without extracting, use `tar -tzf ___`.  
**Answer:** `archive.tar.gz`

121. To view the first 10 lines of `error.log`, use `___ error.log`.  
**Answer:** `head -n 10`

122. To create `temp_data` inside `/tmp`, use `mkdir /tmp/___`.  
**Answer:** `temp_data`

123. To list files having exactly four characters, use `ls ___`.  
**Answer:** `????`

124. Which history option reads the history file?  
**Answer:** `history -r`

125. To display the current date and time using `echo`, use `echo "Current time: $(___)"`.  
**Answer:** `date`

126. To copy `report.xlsx` to `financial_report.xlsx`, use `cp report.xlsx ___`.  
**Answer:** `financial_report.xlsx`

127. To display the manual page for `head`, type `man ___`.  
**Answer:** `head`

128. Which commands can create `documents/reports` even when `documents` doesn't exist?  
**Answer:** `mkdir -p documents/reports` or `mkdir --parents documents/reports`

129. To search for `"error"` case-insensitively and show 2 lines before, use `grep -i -B 2 "error" ___`.  
**Answer:** `syslog`

130. To display the first 25 lines of `syslog`, use `head -n ___ syslog`.  
**Answer:** `25`

131. To search for `"warning"` and display 5 lines after each match, use `grep -A 5 "warning" ___`.  
**Answer:** `messages.log`

132. To remove the alias `ll`, use the `___ ll` command.  
**Answer:** `unalias`

133. To delete lines 5–10 from `document.txt`, use `sed '5,10___' document.txt`.  
**Answer:** `d`

134. To extract `archive.tar.xz` to `/opt/archive`, use `tar -xJf archive.tar.xz -C ___`.  
**Answer:** `/opt/archive`

135. Which command is best for viewing a very large file without loading it all at once?  
**Answer:** `less`

136. To create `scripts` inside `/home/user`, use `mkdir /home/user/___`.  
**Answer:** `scripts`

137. To copy `notes.txt` to `notes_backup.txt`, use `cp notes.txt ___`.  
**Answer:** `notes_backup.txt`

138. To display the manual page for `pwd`, type `man ___`.  
**Answer:** `pwd`

139. To list files beginning with `d` and ending with `.txt`, use `ls d*.txt` or `ls ___`.  
**Answer:** `d*.txt`

140. To extract `archive.tar.gz` to `/opt/backup`, use `tar -xzf archive.tar.gz -C ___`.  
**Answer:** `/opt/backup`

141. To display the manual page for `grep`, type `man ___`.  
**Answer:** `grep`

142. To extract `project.tar.gz` to the current directory, use `tar -xzf ___`.  
**Answer:** `project.tar.gz`

143. To display the last 20 lines of `messages.log`, use `tail -n ___ messages.log`.  
**Answer:** `20`

144. To download `data.txt` as `raw_data.txt`, use `wget -O raw_data.txt ___`.  
**Answer:** `http://example.com/data.txt`

145. To count lines in `data.csv`, use `wc -l ___`.  
**Answer:** `data.csv`

146. To download `latest.tar.gz` as `latest_app.tar.gz`, use `wget -O latest_app.tar.gz ___`.  
**Answer:** `http://example.com/latest.tar.gz`

147. To display only the first 10 lines of `ls -l`, use `ls -l | ___ -n 10`.  
**Answer:** `head`

148. To display the contents of `data` and its subdirectories in long-listing format, use `ls -l ___`.  
**Answer:** `-R data` / `ls -lR data`

149. To search for `database.sql` inside `/var/lib/postgresql`, use `find /var/lib/postgresql -name ___`.  
**Answer:** `database.sql`

150. Which `diff` commands show differences in unified format?  
**Answer:** `diff -u file1.txt file2.txt` or `diff --unified file1.txt file2.txt`

151. To remove `temp_dir` and all its contents, use `rm -rf ___`.  
**Answer:** `temp_dir`

152. What is the purpose of `man`?  
**Answer:** To display the manual page for a command and provide information about its usage and options.

153. To search for `error` in all `.log` files, use `grep 'error' ___`.  
**Answer:** `*.log`

154. To display the manual page for `tree`, type `man ___`.  
**Answer:** `tree`

155. To list files with one character followed by `.log`, use `ls ?.log` or `ls ___`.  
**Answer:** `?.log`

156. To copy `document.pdf` to the `archive` directory, use `cp document.pdf ___`.  
**Answer:** `archive/`

157. To display environment variables, use `printenv` or `echo ___`.  
**Answer:** `$` followed by the variable name, e.g. `$PATH`

158. To search for `"permission denied"` and show 2 lines before and after, use `grep -C 2 "permission denied" ___`.  
**Answer:** `syslog`

159. What does `wget` do by default when no output filename is specified?  
**Answer:** Saves the file with its original name in the current directory.

160. To search for `access.log` inside `/var/log/nginx`, use `find /var/log/nginx -name ___`.  
**Answer:** `access.log`

161. To display the last 10 lines of `auth.log`, use `tail -n ___ auth.log`.  
**Answer:** `10`

162. To copy `report.csv` to `sales_report.csv`, use `cp report.csv ___`.  
**Answer:** `sales_report.csv`

163. To list files beginning with `s` and ending in `.txt`, use `ls s*.txt` or `ls ___`.  
**Answer:** `s*.txt`

164. To remove `old_data` and everything inside it, use `rm -rf ___`.  
**Answer:** `old_data`

165. To display the last 20 lines of `syslog`, use `tail -n ___ syslog`.  
**Answer:** `20`

166. Which grep command finds `user` followed by exactly one digit?  
**Answer:** `grep "user[0-9]" accounts.log`

167. To create `test_area` inside `/tmp`, use `mkdir /tmp/___`.  
**Answer:** `test_area`

168. To remove `temp_file.log` without confirmation, use `rm ___ temp_file.log`.  
**Answer:** `-f`

169. To display the manual page for `grep`, type `man ___`.  
**Answer:** `grep`

170. To list all `.pdf` files, use `ls ___`.  
**Answer:** `*.pdf`

171. To list files containing `data` anywhere in their name, use `ls ___`.  
**Answer:** `*data*`

172. To create `web_content` inside `/var/www`, use `mkdir /var/www/___`.  
**Answer:** `web_content`

173. To search for `database.db` inside `/var/lib`, use `find /var/lib -name ___`.  
**Answer:** `database.db`

174. To search for `script.sh` inside `~/bin`, use `find ~/bin -name ___`.  
**Answer:** `script.sh`

175. To display the manual page for `man`, type `man ___`.  
**Answer:** `man`

176. To search for `database.sqlite` inside `/var/lib`, use `find /var/lib -name ___`.  
**Answer:** `database.sqlite`

177. To copy `image.jpg` to `image_copy.jpg`, use `cp image.jpg ___`.  
**Answer:** `image_copy.jpg`

178. To list files starting with `a` and having `b` as their third character, use `ls a?b*` or `ls ___`.  
**Answer:** `a?b*`

179. To search for `"critical"` case-insensitively and show 1 line before and after, use `grep -i -C 1 "critical" ___`.  
**Answer:** `syslog`

180. Which command displays previously executed commands?  
**Answer:** `history`

181. To download `software.zip` using its original name, use `wget ___`.  
**Answer:** `http://example.com/software.zip`

182. To display the last 5 lines of `syslog`, use `tail -n ___ syslog`.  
**Answer:** `5`

183. To search for `error.log` inside `/var/log/apache2`, use `find /var/log/apache2 -name ___`.  
**Answer:** `error.log`

184. To download `manual.pdf` with its original name, use `wget ___`.  
**Answer:** `http://example.com/docs/manual.pdf`

185. To list files having exactly six characters, use `ls ___`.  
**Answer:** `??????`

186. To remove `old_archive.zip` without confirmation, use `rm ___ old_archive.zip`.  
**Answer:** `-f`

187. To display the first 20 lines of `kern.log`, use `head -n ___ kern.log`.  
**Answer:** `20`

188. To create `downloads` inside your home directory, use `mkdir ___/downloads`.  
**Answer:** `~`

189. Which `tar` command creates a compressed `.tar.gz` archive of `my_project`?  
**Answer:** `tar -czvf my_project.tar.gz my_project/`  
(`tar -czf` is also valid if verbose output is not required.)

190. To view the last 10 lines of `system.log`, use `___ system.log`.  
**Answer:** `tail -n 10`

191. What is the purpose of `cat file.txt | head -n 5`?  
**Answer:** To display the first 5 lines of `file.txt`.

192. To display the first 100 lines of `access.log`, use `head -n ___ access.log`.  
**Answer:** `100`

193. To search for `data.csv` inside `~/Downloads`, use `find ~/Downloads -name ___`.  
**Answer:** `data.csv`

194. To list files having exactly seven characters, use `ls ___`.  
**Answer:** `???????`

195. Which `tar` options extract files and show verbose output?  
**Answer:** `-xvf`  
(`--extract --verbose --file` is also valid.)

196. To create `data` inside `/var/lib`, use `mkdir /var/lib/___`.  
**Answer:** `data`

197. To download `archive.zip` as `downloaded_archive.zip`, use `wget -O downloaded_archive.zip ___`.  
**Answer:** `http://files.example.com/archive.zip`

198. Which commands can create an empty directory named `my_folder`?  
**Answer:** `mkdir my_folder` and `mkdir -p my_folder`

199. To remove `old_data.json` without confirmation, use `rm ___ old_data.json`.  
**Answer:** `-f`

200. What does `ssh-keygen -p` do?  
**Answer:** Changes the passphrase of an existing private key.

**You now have all 200 questions with their answers in order.**