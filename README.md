# zvm-tools
Tools for z/VM - many inspired by useful Linux commands

    +------------------+-------------------------------------------------+
    | File             | Description                                     |
    |------------------|-------------------------------------------------|
    | CALCDASD EXEC    | Calculate total DASD space and types            |
    | CALCOSA  EXEC    | Calculate free and used OSA and verify PCHIDs   |
    | CFM      EXEC    | Copy file with new file mode                    |
    | CFN      EXEC    | Copy file with new file name                    |
    | CFT      EXEC    | Copy file with new file type                    |
    | COPYDISK EXEC    | Copy disk with FLASHCOPY if not DDR             |
    | CPFORMAT EXEC    | Format one or more DASD and label               |
    | DIFF     EXEC    | Compare files line by line                      |
    | GREP     EXEC    | Search for patterns in files                    |
    | MAN      EXEC    | Give help on CMS/CP/XEDIT commands              |
    | MKVMARC  EXEC    | Make a VMARC file of these EXECs/XEDIT macros   |
    | QA       EXEC    | Run QUERY ACCESSED                              |
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
    |                  |                                                 |
    | ZVMTOOLS VMARC   | Collection of all the above tools               |
    +------------------+-------------------------------------------------+
### TO DO
#### Possible new EXECs:

    +------------------+-------------------------------------------------+
    | File             | Description                                     |
    |------------------|-------------------------------------------------|
    | HISTORY  EXEC    | Show previous commands run                      |
    | LOCATE   EXEC    | search for files on all CMS disks and SFS's     |
    |          EXEC    |                                                 |
    +------------------+-------------------------------------------------+


## REXX EXECs
Following are descriptions of each REXX EXEC.

### CALCDASD EXEC
The ``CALCDASD EXEC`` calculates the size of all disk space. 

Here is the help:
```
calcdasd -h                                    
Name:  CALCDASD EXEC - compute total disk space
Usage: CALCDASD                                
```

Here is an example of using it:

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

### CALCOSA EXEC
The ``CALCOSA EXEC`` merges free and used OSAs by ``rdev``, and verifies the CHPIDs and PCHIDs. 

Here is the help:
```
calcosa -h                                       
Name:  CALCOSA EXEC - compute OSA statistics     
Usage: CALCOSA [(v|verbose]                      
```

Here is an example of using it:

```
calcosa                                              
Rdev  UserID    Vdev  DevType  OSAtype  CHPID  PCHID   
----  ------    ----  -------  -------  -----  -----   
0340  DTCVSW1   0600  OSA      OSD      F0     NONE    
0341  DTCVSW1   0601  OSA      OSD      F0     NONE    
0342  DTCVSW1   0602  OSA      OSD      F0     NONE    
1340  DTCVSW2   0600  OSA      OSD      F1     NONE    
1341  DTCVSW2   0601  OSA      OSD      F1     NONE    
1342  DTCVSW2   0602  OSA      OSD      F1     NONE    
2340  FREE                              A0     NONE    
2341  FREE                              A0     NONE    
2342  FREE                              A0     NONE    
                                                       
Used OSAs:    6                                        
Free OSAs:    3                                        
           ----                                        
    Total:    9                                        
```

### CFM EXEC
The ``CFM EXEC`` copies a file just changing the file mode. 
Here is the help:
```
cfm -h                                                       
Name:  CFM EXEC - Copy file changing only file mode          
Usage: CFM fn1 ft1 fm1 fm2 ['('options')']                   
Where: 'fn1 ft1 fm1' is the source file:                     
       'fm2' is the target file mode                         
       'options' add to COPY command such as 'REP' or 'OLDD' 
```

For example, if you want to copy the file ``COPYDISK EXEC A`` to your B disk, you can type ``CFM B COPYDISK EXEC A``, but if your in a ``FILELIST``, you can simply type ``CFM B`` next to it, as the ``FN FT FM`` will be automatically added to the end.

### CFN EXEC
The ``CFN EXEC`` copies a file just changing the file name.

Here is the help:
```
cfn -h                                                       
Name:  CFN EXEC - Copy file changing only file name          
Usage: CFN fn2 fn1 ft1 fm1 ['('options')']                   
Where: 'fn2' is the target file name                         
       'fn1 ft1 fm1' is the source file:                     
       'options' add to COPY command such as 'REP' or 'OLDD' 
```

Here is an example of using it from within FILELIST to copy an EXEC with a new file name of ``foo``:

```
 MIKEMAC  FILELIST A0  V 169  Trunc=169 Size=50 Line=1 Col=1 Alt=0              
Cmd   Filename Filetype Fm Format Lrecl    Records     Blocks   Date     Time   
cfn foo LCOSA  EXEC     A1 V         73        233          3  2/08/25  5:48:42 
```


### CFT EXEC
The ``CFT EXEC`` copies a file just changing the file type.

Here is the help:
```
```

Here is an example of using it:

### COPYDISK EXEC
The ``COPYDISK EXEC`` first tries to copy a disk with ``FLASHCOPY`` and if that fails, falls back to ``DDR``.

Here is the help:
```
```

Here is an example of using it:

### CPFORMAT EXEC
The ``CPFORMAT EXEC`` formats one or more DASD volumes using ``CPFMTXA``.

Here is the help:
```
```

Here is an example of using it:

### DIFF EXEC
The ``DIFF EXEC`` compares two files and shows the results with color.
This is still *alpha* code, especially in regards to getting the code back in sync, when one line is added to one file. 

Updates will be coming.

Here is the help:
```
```

Here is an example of using it:

### GREP EXEC
The ``GREP EXEC`` searches for patterns in files.

To search for strings with spaces, escape the pattern with single-quotes.  For example:

Here is the help:
```
```

Here is an example of using it:

```
grep 'parse upper arg' * exec
```

### MAN EXEC
The ``MAN EXEC`` calls help for the requested command.  For example, ``man q da`` takes you to the ``CP QUERY DASD`` help screen.

Here is the help:
```
```

Here is an example of using it:

### MKVMARC EXEC
The ``MKVMARC EXEC`` creates the z/VM file ``ZVMTOOLS VMARC`` from all of these REXX EXECs and XEDIT macros.

### QA.EXEC
The ``QA EXEC`` simply calls ``QUERY ACCESSED`` to save keystrokes. 

### RFN.EXEC
The ``RFN EXEC`` renames a file only changing the file name. 

Here is the help:
```
```

Here is an example of using it:

### RFT.EXEC
The `` EXEC`` renames a file only changing the file type.

Here is the help:
```
```

Here is an example of using it:

### RM.EXEC
The ``RM EXEC`` allows wild cards when erasing files.

Here is the help:
```
```

Here is an example of using it:

### SPC.EXEC
The ``SPC EXEC`` closes your console and sends it to the reader with a unique timestamp. 

Here is the help:
```
```

Here is an example of using it:

### SSICMD.EXEC
The ``SSICMD EXEC`` runs a CP command on all members of a z/VM SSI cluster. 

Here is the help:
```
```

Here is an example of using it:

### WC.EXEC
The ``WC EXEC`` counts lines, words and bytes in one or more files. 

Here is the help:
```
```

Here is an example of using it:

### WHICH.EXEC
The ``WHICH EXEC`` resolves and fully qualifies CMS, CP and XEDIT commands.

Here is the help:
```
```

Here is an example of using it:

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
The ``WHO EXEC`` takes the output of ``QUERY NAMES``, sorts it and shows it one virtual machine per line.

It also allows for a search pattern. For example: 

```
who SSL          
SSLDCSSM - DSC   
SSL00001 - DSC   
SSL00002 - DSC   
SSL00003 - DSC   
SSL00004 - DSC   
SSL00005 - DSC   
```

## XEDIT Macros
Following are descriptions of each XEDIT macro.

## BF.XEDIT
The ``BF XEDIT`` macro takes you to the last screen of a file. 

### PROFFLST.XEDIT
Is it just me, or does the stock ``FILELIST`` command *not* have an option to sort by file name?

The ``PROFFLST XEDIT`` macro sets PF10 to *Sort by name* to the ``FILELIST`` command.

If that could be added to the z/VM system globally, this would not be needed. 

### PROFILE.XEDIT     
The ``PROFILE XEDIT`` macro is a slightly modified copy of the one on the ``MAINT 191`` disk. 

## VMARC file 
There is a compressed file of all the EXECs and XEDIT macros in the file ``ZVMTOOLS.VMARC``.

Unfortunately the ``VMARC`` tool to decompress it does not ship with z/VM. If you don't have already, it has to be installed:

- Download the VMARC MODULE from: ``https://www.vm.ibm.com/download/vmarc.module``
- Upload the file to CMS in BINARY (usually ``ftp``, then ``bin``, then ``put vmarc.module``)
- Run it through this pipeline:

```
PIPE < VMARC MODULE A | deblock cms | > VMARC MODULE A
```


