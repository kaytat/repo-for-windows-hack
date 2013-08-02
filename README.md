repo-for-windows-hack
=====================

Hack for the repo script in Android so that it can somewhat be used on Windows

This repo only contains one file, which is a patch file that will allow the repo python script from the Android project to run on Windows.  The current working Windows environment is Windows XP with Python 2.7.  I've tested the patched repo with raw cmd.exe, MINGW32 that comes with the installation of the Github Windows client, and Cygwin.

This patch only has two goals:
1) 'repo init -u https://github.com/something/something -m something.xml' succeeds
2) 'repo sync' is able to pull down code

All the other repo commands have not been tested.  And I haven't tested the '-jNUM' option.

The basic strategy is to replace all os.symlink calls with shutil.copyfile calls.

How to use:
1) Make sure you have python 2.7 installed on Windows and your path is updated so that python.exe is found
2) Make sure git is in your path (automatic if you installed the new github windows client)
3) Clone the repo source
c:\>mkdir repowin
c:\>cd repowin
c:\>git clone https://gerrit.googlesource.com/git-repo
4)
