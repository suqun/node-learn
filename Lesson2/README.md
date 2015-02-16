《Linux下安装mongodb》
==========

###Install for 64-bit Linux
*1.Download the binary files for the desired release of MongoDB.
Download the binaries from https://www.mongodb.org/downloads.

For example, to download the latest release through the shell, issue the following:

`curl -O http://downloads.mongodb.org/linux/mongodb-linux-x86_64-2.6.7.tgz`
*2.Extract the files from the downloaded archive.
For example, from a system shell, you can extract through the tar command:

`tar -zxvf mongodb-linux-x86_64-2.6.7.tgz`
*3.Copy the extracted archive to the target directory.
Copy the extracted folder to the location from which MongoDB will run.

`mkdir -p mongodb`
`cp -R -n mongodb-linux-x86_64-2.6.7/ mongodb`
*4.Ensure the location of the binaries is in the PATH variable.
The MongoDB binaries are in the bin/ directory of the archive. To ensure that the binaries are in your PATH, you can modify your PATH.

For example, you can add the following line to your shell’s rc file (e.g. ~/.bashrc):

`export PATH=<mongodb-install-directory>/bin:$PATH`
Replace <mongodb-install-directory> with the path to the extracted MongoDB archive.


 


 

[参考docs.mongodb.org](http://docs.mongodb.org/manual/tutorial/install-mongodb-on-linux/)
