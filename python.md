# Python Programming

## Initial Questions

1. ### Is Python a programming language or a scripting language?

#### * Its both , Why is a "script language" is usually a short program written to automate simple, repetitive tasks . Because Python executes code line-by-line (interpreted) without needing a long manual compilation  

#### * Why its a programming language , It has support for the object oriented programming ,heavy and data structure . Hence, it is used to build masive complex softare architecutures 

2. ### What is pip?

#### * Pip Installs Packages , it is the default package manager for Python, used to install and manage additional libraries and dependencies that are not included in the Python standard library

#### * is Python's package manager, but almost every modern language has its own "App Store" to download code written by other people.

### 2a ) Core commands used 

### 1. To check versions 

```bash
pip --version
```
### 2. Install package

#### * Downloads and installs the latest version of a library.

```bash
pip install package_name
```

### 3. Specific version

```bash
pip install package_name==1.5
```

### 4. Upgrade package


```bash
pip install --upgrade package_name
```

### 5. Uninstall package

```bash
pip uninstall package_name
```

### 6. List packages

```bash
pip list
```

### 3 . What is a Virtual Environment or simply referred to as venv with regards to Python?

#### * Python uses venv to keep project files isolated.

### 4 . How does one check the current version of Python installed on their PC?

```bash
pip --version
```

# Creating the Virtual Environment 

1. ### Instlling the python on the local linux 

```bash
sudo apt update && sudo apt install python3-pip python3-venv -y

```

2. ### Creating the environment 

```bash
python3 -m venv ~/.venv/quatrix-mentorship
```

3. ### Activate it 

```bash
source ~/.venv/quatrix-mentorship/bin/activate
```

4. ### Install Numpy to avoid errors

```bash
pip install numpy
```

#### * Numerical Python (numpy) - it is a tool that allows Python to handle massive amounts of numbers and math extremely fast.
