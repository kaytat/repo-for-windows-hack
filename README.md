repo-for-windows-hack
=====================

Hack for the `repo` script in Android so that it can somewhat be used on Windows

# Apologies #
Sometimes 'repo' means a git repository.  Other times it means the `repo` script.

# Description #
This github repo only contains one file, which is a patch file that will allow the `repo` python script from the Android project to run on Windows.  The current working Windows environment is Windows XP with Python 2.7.  I've tested the patched `repo` with cmd.exe, MINGW32 that comes with the installation of the Github Windows client, and Cygwin.

This patch only has two goals:

1. `repo init -u https://github.com/kaytat/stoker.git -m default.xml` succeeds
2. `repo sync` is able to pull down code

All the other `repo` commands have not been tested.  And I haven't tested the `-jNUM` option.

The basic strategy is to replace all `os.symlink` calls with `shutil.copyfile` calls.

# How to use#
The steps below copy `repo` and then patch it.

1. Make sure you have python 2.7 installed on Windows and your PATH is updated so that `python.exe` is found

2. Make sure `git` is in your path.  This should be automatic if you installed the new github windows client.

3. Save the patch locally to your hard-drive

    Go to `https://raw.github.com/kaytat/repo-for-windows-hack/master/v1.12.2.patch`

    Save this file as `c:\v1.12.2.patch`
 
4. Clone the repo source

        c:\>mkdir repowin
        c:\>cd repowin
        c:\repowin>git clone https://gerrit.googlesource.com/git-repo

5. Apply the patch to v1.12.2

        c:\repowin>cd git-repo
        c:\repowin\git-repo>git checkout -b mybranch v1.12.2
        c:\repowin\git-repo>git apply c:\v1.12.2.patch

      The checkout command is necessary to make sure the patch is applied to version 1.12.2 of `repo`

At this point, the local copy of `repo` has been patched and you should be able to pull down code.

# Example #
In the example of the Stoker code:

    c:\>mkdir stoker
    c:\>cd stoker
    c:\stoker>python c:\repowin\git-repo\repo init -u https://github.com/kaytat/stoker.git -m default.xml
    c:\stoker>python c:\repowin\git-repo\repo sync
    
# Why bother? #
All the Stoker development has been on Windows.

But I wanted to take advantage of github.

And to take advantage of github, I figured I should follow the convention where each git repo contains a separate project.

But since there are multiple git repos and git submodules really confused me, I figured `repo` would be the best way around this.

I didn't realize `repo` wasn't supported on Windows.

And thus this little effort.

Good luck.
