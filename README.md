# 5 characters to extend gitigonre functionality to selectively include specified patterns only

## The `.gitignore` file contains the 5 characters (including new line) to allow gitignore to include only patterns specified.
To do so, simply add the 2 lines at the top of your `.gitignore` file, then use `!\<pattern\>` to selectively include any gitignore pattern.
Presedance rules work as normal.

Note that this is **merely an extension of gitignore functionality without taking away any**.\
You can still use the same patterns as normal gitignore to ignore patterns after you have included some.\
You can also select the included files to stage using `git add`.\
`git status` will only show included files matching patterns in the `.gitignore` file.


# Usage

## Including `.gitignore` and individual files, directories and file extensions, and ignoring afterwards
```
*
!*/

# gitignore
!.gitignore

# individual files
!<path to file>

# file extensions
!*.<extension>

# directories
!<directory>/

# ignoring as usual
<pattern to ignore>
```


# Motivation

I have only recently started using git for version control (one week from writing) seriously, but have always found it troublling that `git add *` would add unintended (mostly generated) files.
The solution is of course `.gitignore`.
You specify the files to ignore and now git will not track them.
Though this works fine for well structured projects, with generated and temporary file located or named approiately, I would much prefer adding selected files.

The probelm is now you need to add files individually using `git add`, which becomes impractical for large projects with many changes here and there.
So I came up with this `.gitignore` file to filter the files git can track.

I hope this can help version control to become more versitle and safe, reduce the hassle of setting up a proper `.gitignore` file, as well as accidently staging unintended files.

## Disclaimer: I am not an expert of git or gitignore, the following is merely my understanding

# Explaination

- gitignore cannot see files or directories after the parent directory is ignored.
- gitignore pattern searching works recurrsively (very not sure, but seems to be the case)
- git does not track directories, but files

Combining the observations, the solution is to ignore files only, and not directories.
Unfortunately, gitignore can only specify directories using a trailing `/`.

So the solution is to ignoring all files using `*`, then include all directories using `!*/`.
This allows gitignore to ignore all files, without ignoring directories, recurrsively.

# Potential problems

This might need git to search all directories (and maybe all files), which might slow down git.