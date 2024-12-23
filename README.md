# zvm-tools
Tools for z/VM - many inspired by useful Linux commands

    +------------------+-------------------------------------------------+
    | File             | Description                                     |
    |------------------|-------------------------------------------------|
    | CFM      EXEC    | Copy file with new file mode                    |
    | CFN      EXEC    | Copy file with new file name                    |
    | CFT      EXEC    | Copy file with new file type                    |
    | COPYDISK EXEC    | Copy disk with ``FLASHCOPY`` if not ``DDR``     |
    | CPFORMAT EXEC    | Format one or more DASD and label               |
    | DIFF     EXEC    | Compare files line by line                      |
    | GREP     EXEC    | Search for patterns in files                    |
    | MAN      EXEC    | Give help on CMS/CP/XEDIT commands              |
    | QA       EXEC    | Run ``QUERY ACCESSED``                          |
    | RFN      EXEC    | Rename file changing only file name             |
    | RFT      EXEC    | Rename file changing only file type             |
    | RM       EXEC    | Remove files allowing wildcards                 |
    | SPC      EXEC    | Spool console to reader then restart            |
    | SSICMD   EXEC    | Run CP commands on multiple SSI members         |
    | WC       EXEC    | Count lines, words and bytes in files           |
    | WHICH    EXEC    | Resolve CMS/CP/XEDIT commands                   |
    | WHO      EXEC    | Show who is logged on and allow a pattern       |
    |                  |                                                 |
    | BF       XEDIT   | Move to the last page in XEDIT                  |
    | PROFFLST XEDIT   | Sets F10 to "Sort by Name" which is missing     |
    | PROFILE  XEDIT   | "This is the real thing" adapted from MAINT     |
    +------------------+-------------------------------------------------+

## REXX EXECs
Following are descriptions of each REXX EXEC.

### CALCDASD.EXEC
The ``CALCDASD EXEC`` calculates the size of all disk space. 

```
calcdasd                                             
Warning - non standard size: 31A2 has 18000 cylinders
Warning - non standard size: 3A97 has 18000 cylinders
Warning - non standard size: 3AA2 has 18000 cylinders
Number of 3390-1s    (1113 cylinders): 0             
Number of 3390-2s    (2226 cylinders): 0             
Number of 3390-3s    (3339 cylinders): 222           
Number of 3390-9s   (10017 cylinders): 76            
Number of 3390-27s  (30051 cylinders): 8             
Number of 3390-32Ks (32760 cylinders): 0             
Number of 3390-54s  (60102 cylinders): 0             
Number of 3390-64Ks (65520 cylinders): 0             
Number of 3390-As       (other sizes): 5             
                                                     
Total CP-Owned cylinders: 40068 (31.72 GiB)          
Total SYSTEM   cylinders: 1892676 (1498.22 GiB)      
```
### CFM.EXEC
The ``CFM EXEC`` copies a file just changing the file mode. 

### CFN.EXEC
The ``CFN EXEC`` copies a file just changing the file name.

### CFT.EXEC
The ``CFT EXEC`` copies a file just changing the file type.

### COPYDISK.EXEC
The ``COPYDISK EXEC`` first tries to copy a disk with ``FLASHCOPY`` and if that fails, falls back to ``DDR``.

### CPFORMAT.EXEC
The ``CPFORMAT EXEC`` formats one or more DASD volumes using ``CPFMTXA``.

### DIFF.EXEC
The ``DIFF EXEC`` compares two files and shows the results with color.
This is still *alpha* code, especially in regards to getting the code back in sync, when one line is added to one file. 

Updates will be coming.

### GREP.EXEC
The ``GREP EXEC`` searches for patterns in files.
It hasn't been tested with SFSs.

To search for strings with spaces, the pattern has to be escaped with triple double-quotes.  For example:

```
grep """parse upper arg""" * exec
```

Also, anyone know how to pass a string to REXX with spaces?  For example:
```
grep "find three words" * exec           
No files found matching THREE WORDS *  
``` 
The double quotes around the three words get *eaten*.

### MAN.EXEC
The ``MAN EXEC`` calls help for the requested command.  For example, ``man q da`` takes you to the ``CP QUERY DASD`` help screen.

### QA.EXEC
The ``QA EXEC`` simply calls ``QUERY ACCESSED`` in order to save keystrokes. 

### RFN.EXEC
The ``RFN EXEC`` renames a file only changing the file name. 

### RFT.EXEC
The `` EXEC`` renames a file only changing the file type.

### RM.EXEC
The ``RM EXEC`` allows wild cards when erasing files.

### SPC.EXEC
The ``SPC EXEC`` closes your console and sends it to the reader with a unique timestamp. 

### SSICMD.EXEC
The ``SSICMD EXEC`` runs a CP command on all members of a z/VM SSI cluster. 

### WC.EXEC
The ``WC EXEC`` counts lines, words and bytes in one or more files. 

### WHICH.EXEC
The ``WHICH EXEC`` resolves and fully qualifies CMS, CP and XEDIT commands.

The ``QUERY`` and ``SET`` commands allow for a second argument.  For example: 

```
which q disk            
QUERY DISK is a CMS command   
Ready;                  
which q da              
QUERY DASD is a CP command    
Ready;                  
which q scale           
QUERY SCALE is a XEDIT command
Ready;                  
``` 

### WHO.EXEC
The ``WHO EXEC`` 

## XEDIT Macros
Following are descriptions of each XEDIT macro.

## BF.XEDIT
The ``BF XEDIT`` macro takes you to the last screen of a file. 

### PROFFLST.XEDIT
The ``XEDIT`` macro sets PF10 to *Sort by name* to the ``FILELIST`` command.

If that could be added to the z/VM system globally, this would not be needed. 

### PROFILE.XEDIT     
The ``PROFILE XEDIT`` macro is a slightly modified copy of the one on the ``MAINT 191`` disk. 

