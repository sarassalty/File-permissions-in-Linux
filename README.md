# File permissions in Linux

> [!NOTE]
> This exercise is a component of the [Google Cybersecurity Professional Certificate](https://www.coursera.org/professional-certificates/google-cybersecurity) program. It's designed as a simulated scenario to solidify my understanding of "Tools of the Trade: Linux and SQL."

## Project description
This project models a real-world security scenario where a security professional manages file and directory permissions. Using Linux command-line tools like chmod, I’ll review current permissions, identify security risks, and adjust settings to meet security standards. This helps protect confidential research data and ensure the system integrity.
```
researcher2@823274a7ed46:~$ cd projects
researcher2@823274a7ed46:~/projects$ ls -l
total 20
drwx--x--x 2 researcher2 research_team 4096 Dec 20 14:24 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Dec 20 14:24 project_k.txt
-rw-r--r-- 1 researcher2 research_team   46 Dec 20 14:24 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 project_t.txt
researcher2@823274a7ed46:~/projects$ ls -a
.  ..  drafts  .project_x.txt  project_k.txt  project_m.txt  project_r.txt  project_t.txt
researcher2@823274a7ed46:~/projects$ chmod o-w project_k.txt
researcher2@823274a7ed46:~/projects$ chmod g-r project_m.txt
researcher2@823274a7ed46:~/projects$ ls -la
total 32
drwxr-x--x 3 researcher2 research_team 4096 Dec 20 14:24 .
drwxr-xr-x 3 researcher2 research_team 4096 Dec 20 15:11 ..
drwx--x--x 2 researcher2 research_team 4096 Dec 20 14:24 drafts
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 .project_x.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 project_k.txt
-rw-r--r-- 1 researcher2 research_team   46 Dec 20 14:24 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 project_t.txt
researcher2@823274a7ed46:~/projects$ chmod u-w,g+r,g+w .project_x.txt
researcher2@823274a7ed46:~/projects$ chmod g-x drafts 
```

## Check file and directory details
I used the ls -l command to display the list of the permissions set for files and subdirectories in the projects directory.

```
researcher2@823274a7ed46:~/projects$ ls -l
total 20
drwx--x--x 2 researcher2 research_team 4096 Dec 20 14:24 drafts
-rw-rw-rw- 1 researcher2 research_team   46 Dec 20 14:24 project_k.txt
-rw-r--r-- 1 researcher2 research_team   46 Dec 20 14:24 project_m.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 project_r.txt
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 project_t.txt
```

## Describe the permissions string

```
-rw-r--r-- 1 researcher2 research_team   46 Dec 20 14:24 project_m.txt
```

In this output for ```project_m.txt```, the 10-character string describes the permissions of a file that the types of owners have. 
 + The hyphen (```-```) at the start of the line indicates it’s a file, if it had a d it’d indicate that it’s a directory.
 + The first block is ```rw-``` and it indicates the first type of owner, which is the user and owner of the file. The permissions are read (``` r ```), write (``` w ```), and the hyphen at the end means that the user doesn’t have the permission to execute (``` x ```)
 + The second block is ```r--``` and it indicates the second type of owner, which is the group, and this is a larger group that the owner of the file is part of. The group, in this case, only has the permission to read (``` r ```), because it shows a hyphen instead of a ```w``` (write) and a hyphen instead of an ```x``` (execute).
 + The third block is ```---``` and it indicates the third type of owner, which is other, and this is all the users on the system. Other, in this case, doesn’t have any permissions because it shows a hyphen instead of an  ```r``` (read), a hyphen instead of a ```w``` (write) and a hyphen instead of an ```x``` (execute).


## Change file permissions

```
researcher2@823274a7ed46:~/projects$ chmod o-w project_k.txt
```

The organization does not allow others to have write access to any files, so I changed the permissions of the ```project_k.txt``` file, removing the write access for others with this command: ```chmod o-w project_k.txt```. 
The ```chmod``` command requires two arguments. The first argument indicates how to change permissions, and the second argument indicates the file or directory that you want to change permissions for. Using the symbolic mode, first I have to input who I want to change permissions from, in this case, ```o``` stands for other. Then, I input an operator to indicate the action (```+```: add, ```-```: remove,```=```: set). Also, I specify the permission (```r```: read, ```w```: write, ```x```: execute). Finally, I put the name of the file/directory.


## Change file permissions on a hidden file

```
-rw-rw-r-- 1 researcher2 research_team   46 Dec 20 14:24 .project_x.txt
```
```
researcher2@823274a7ed46:~/projects$ chmod u-w,g+r,g+w .project_x.txt
```

The research team has archived ```.project_x.txt```, which is why it’s a hidden file. This file should not have write permissions for anyone, but the user and group should be able to read the file. 
To change the permissions I used the ```chmod``` command. I only removed the permission to write from the user because it already had the permission to read. Then, added the permission to read for the group, and removed the permission to write.
Because it was a hidden file I had to add a period at the beginning of the name of the file.


## Change directory permissions

```
drwx--x--x 2 researcher2 research_team 4096 Dec 20 14:24 drafts
```
```
researcher2@823274a7ed46:~/projects$ chmod g-x drafts 
```
The files and directories in the projects directory belong to the ```researcher2``` user. Only ```researcher2``` should be allowed to access the ```drafts``` directory and its contents. 
To change the directory permissions I used the ```chmod``` command, removing the execute (```x```) permission from the group, leaving all the permissions for the user.


## Summary
In this project, I conducted a detailed security review and adjusted permissions. Using Linux command-line tools (```ls -l```, ```ls -a```, ```ls -la```, and ```chmod```), I ensured that the file and directory permissions followed security policies, protecting sensitive research data and reducing risks. 



