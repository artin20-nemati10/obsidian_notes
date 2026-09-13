
# Hard Links
- Each hard linked file fhas the same physical file location.
- hard links remain linkedeven if original files are moved.
- linkkd have actual file contents.
- Removing any link doesn'taffect other links.
- We cannot create a hard link for a directory to avoid recursive loops.
- The size of any of the hard link files same as original file.
- The disadvantage of the hard link is that it cannot be crated for files on different file systems and it cannot be created for special files or directories.
``` 
ln file_1 Hard_Link_1
ln file_2 hard_link_2
```
---
# What is Inod
 - An inod is a file data structurethat stores informationabout files except name and data.
 - Datea is sorted on disk in the form of fixed-size blocks If file exceeds a standard block, Linux will find next available segment to store the rest of your file from nodes.
 - Inods don't contaion actual data it storres the diles metadata including po  
 -  