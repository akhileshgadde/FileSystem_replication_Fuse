FUSE-REPLICATION-FS_PROTOTYPE
=============================

Simple FS prototype using FUSE that replicates a copy of the file and keeps both copies in Sync at real time.

This is the first prototype of the code that needs to implement a user level File system using FUSE that replicates files. The version 1 of present code just creates a copy of the file with extension (.bkp) to the name of actual file in the same location. When we write new information to the normal file or the backup file, the other file is also kept in sync with the changes. The idea is to use this on top of Lustre Distributed File system that currently doesn't support file level replication

P.S: This is just a protype version of the code and not intended for actual development. The code is unoptimized and bare minimal to check the feasibility of the implementation.

LIMITATIONS
------------
1. We don’t support replication of directories at this point. We could create a directory and try to write inside the directory.
2. Now, both the actual and backup files are created in the same directory. This is intended to be changed in future releases so that when this FS is mounted on Lustre, the client doesn’t see the backup files.
3. Also, only one replicated copy of the actual file is created with extension ‘.bkp’ to the original file name.
4. From Lustre point of view, the extra logic of selecting the replica in client and MDS nodes need to be implemented in the Lustre code.
5. The makefile needs to be modified, presently we directly compile the code using gcc for tfs.c and mount FUSE TFS on top of Lustre. Verified to be working.
P.S: If someone needs a clean working copy of the code to run with makefile, I would take some time and provide you a refined code.


Code Acknowledgements
----------------------
Code has been based on BBFS FS written by Joseph J. Pfeiffer, Jr., Ph.D., Emeritus Professor, New Mexico State University. It has been modified to suit our requirements of implementing a FUSE FS for replication in Lustre.

