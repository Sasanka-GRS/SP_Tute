# Question - 1: Reversing File

The code is in the file named **q1.c** in the current folder. 

## Execute instructions:

```
gcc q1.c
./a.out <path_to_file>
```

## Assumptions: 

1. No spaces are given in the path to the file. If spaces exist, they are preceded by '\'.
2. The current path for the code, that is, the current working diretory and the file name together do not exceed **1000** characters in length.
3. The code will throw an error if the directory called 'Assignment' is already created in the directory where this code is executed, but won't stop execution and will continue further executions.

## Code Explanation

1. In the ```int main()``` function, the arguments argc and argv denote the number of arguments and the obtained arguments on the terminal during code execution.
2. Lines 18-25 deal with creating a new directory called 'Assignment' with permission set 0700 (read,write,execute permission for user and no permissions for group and others) using the ```chdir()```  command and error handling using ```perror()```. The perror() is triggered even if the directory already exists.
3. The path of the current working directory is stored for further use in the code using ```getcwd()``` command.
4. ```chdir()``` is used to open the directory where the file to be read exists.
5. Lines 58-62 are triggered if no path is given as the input argument.
6. Lines 65-90 deal with extracting the path for the directory from the given path to the file.
7. Lines 95-110 extract the name of the file to open and also creates the name of the new file to be created as 1_<old_file_name>.
8. Then, we create the new file with permission set 0600 (read,write permission for user and no permissions for group and others) as well as open the given file (in read only format) whose contents must be reversed, both using ```open()``` command with different arguments.
9. Reading from the file is done using ```read()``` command, and writing to the file using the ```write()``` command.
10. Lines 152-192 are for the case when the size of the file is greater than the maxSize (=10KB) where the file is read, reversed and written using a sliding window of lenght = maxSize. The logic works as follows:
  - A set of characters of length = maxSize is read from the back of the file, it is reversed and appended to the new file.
  - Once this is done, the window is moved left by length = maxSize and again the same process continues and the reversed string is appended at the back of the new file. This operation is repeated for ```int n = size/maxSize;``` times so as to cover the whole file size.
  - 1 specific case to deal with includes the case when the number of characters in the file to be read from is not a multiple of the maxSize. In this case, there would be some ```int r = size%maxSize;``` charcters left over which can be read separately character by character and written.
11. Lines 194-214 are for the case when the size of the file is less than or equal to the maxSize (=10KB) where the file is read and written character by character. The logic works as follows:
  - A character is read from the back of the file and is appended to the file.
  - Now, the preceding character is read and is appended to the file, until all characters are read and written.
12. The percentage of completion is printed dynamically using the '\r' escape sequence useful for replacing and fflush(stdout) which flushes the last line of the output each time. The percentage in integers is converted to string using ```sprintf()``` command and is written to the terminal using the ```write()``` command with first argument as 1. Lines 208-211 show how this is done.

## Results

1. A new folder called 'Assignment' is created in the same place where the code is run (if not previously existing).
2. A new file called '1_<name_old_file>' is created inside the previously created directory (if not previously existing, else it is replaced (truncated)).
3. The dynamic percentages for the reversing processes is printed on the command line. For a 1GB file, the code takes approximately 45sec to complete execution and the dynamic percentage (in integer values from 0-100%) can be observed, while for a smaller sized file (length < maxSize), it takes less than a second to complete and thus the dynamic percentage change cannot be observed though specified in the code.

## Sample Output

```
Percentage Completed - 
100%
```

# Question - 2: Reversing Specific Portionals of File

The code is in the file named **q2.c** in the current folder.

## Execute instructions:

```
gcc q2.c
./a.out <path_to_file> start_index end_index
```

## Assumptions: 

1. No spaces are given in the path to the file. If spaces exist, they are preceded by '\'.
2. The current patg for the code, that is, the current working diretory and the file name together do not exceed **1000** characters in length.
3. The code will throw an error if the directory called 'Assignment' is already created in the directory where this code is executed, but won't stop execution and will continue further executions.
4. If no path is given and file name is given, the code automatically assumes the file to exist in the existing directory (where the code is run).
5. If no inputs are given for the start_index and end_index, the code reverses the whole file just like in the previous task.
6. Assumed that start_index <= end_index.

## Code Explanation

1. Reversing algorithm is same as in the previous task but in this task, the file is divided into 3 different parts and different operations are carried on these parts. Steps 1-9 from previous task are carried out as such, similarly.
2. The algorithm is split into 3 parts:
  - First reversal - The part of the file from start to start_index is assumed to be one file and the reversing algorithm in the previous task is run.
  - First copy - The part of the file from start_index to end_index is assumed to be one file and is copied as such into the output file and appended.
  - Second reversal - The part of the file from end_index to end is assumed to be one file and a small variant (with changed start indices) of the reversing algorithm in the previous task is run.
3. Rest of the code is similar to the previous task. This task is just a variant of the previous task.

## Results

1. A new folder called 'Assignment' is created in the same place where the code is run (if not previously existing).
2. A new file called '2_<name_old_file>' is created inside the previously created directory (if not previously existing, else it is replaced (truncated)).
3. The dynamic percentages for the partial reversing processes is printed on the command line. For a 1GB file, the code takes approximately 45sec to complete execution and the dynamic percentage (in integer values from 0-100%) can be observed, while for a smaller sized file (length < maxSize), it takes less than a second to complete and thus the dynamic percentage change cannot be observed though specified in the code.

## Sample Output

```
Percentage Completed - 
100%
```

# Question - 3: Verifying Reversal and Permissions

The code is in the file named **q3.c** in the current folder. 

## Execute instructions:

```
gcc q3.c
./a.out <path_to_new_file> <path_to_old_file> <path_to_directory>
```

## Assumptions: 

1. No spaces are given in the path to the file. If spaces exist, they are preceded by '\'.
2. The current path for the code, that is, the diretory and the file name together do not exceed **1000** characters in length.
3. The code will throw an error if the directory called 'Assignment' is already created in the directory where this code is executed, but won't stop execution and will continue further executions.
4. If no path is given and file name is given, the code automatically assumes the files to exist in the existing directory (where the code is run).

## Code Explanation

1. Firstly we do ```chdir()``` into the given directory path to check if the directory has been created, which is printed if created or not. If created, we move forward.
2. The procedure to extract the names and directories separately from the given paths is done for both the given files using similar methods used in previous tasks.
3. Once the files are opened using ```open()``` command in read only format, first check is the size of the files, if they are not the same, we directly print that the files aren't reverse of each other. Then, we read both the files character by character, one from the front and onee from the back and compare if both values are the same. If not same, we break right there to print that the files are not reverse of each other.
4. Further, we use ```stat()``` command to get the permissions information of the newfile, oldfile and the directory. This is done by performing **AND** operation of the instance stat_mode of the previously declared struct stat variables for the files and the directory, with the pre-defined identifiers for USER, GROUP and OTHERS permissions, as given below, and finally print them in the required format.
```
  User Read Permission      - S_IRUSR
  User Write Permission     - S_IWUSR
  User Execute Permission   - S_IXUSR
  Group Read Permission     - S_IRGRP
  Group Write Permission    - S_IWGRP
  Group Execute Permission  - S_IXGRP
  Others Read Permission    - S_IROTH
  Others Write Permission   - S_IWOTH
  Others Execute Permission - S_IXOTH
```

## Results

1. Checked if the directory given in the path is created.
2. Checked if the files given in the paths are reverse of each other.
3. Permissions for both files and directory are printed.
4. Useful for checking the reversal in first task.

## Sample Output

```
Directory is created: Yes
Whether file contents are reversed in newfile: Yes
User has read permissions on newfile: Yes
User has write permissions on newfile: Yes
User has execute permissions on newfile: No
Group has read permissions on newfile: No
Group has write permissions on newfile: No
Group has execute permissions on newfile: No
Others has read permissions on newfile: No
Group has write permissions on newfile: No
Others has execute permissions on newfile: No
User has read permissions on oldfile: Yes
User has write permissions on oldfile: Yes
User has execute permissions on oldfile: No
Group has read permissions on oldfile: No
Group has write permissions on oldfile: No
Group has execute permissions on oldfile: No
Others has read permissions on oldfile: No
Group has write permissions on oldfile: No
Others has execute permissions on oldfile: No
User has read permissions on directory: Yes
User has write permissions on directory: Yes
User has execute permissions on directory: Yes
Group has read permissions on directory: No
Group has write permissions on directory: No
Group has execute permissions on directory: No
Others has read permissions on directory: No
Group has write permissions on directory: No
Others has execute permissions on directory: No
```
