<!-- This file has been generated automatically by the following script -->
<!-- C:\Christophe\Repository\writing-documentation\concat-md\concat-md.ps1 -->
<!-- So don't modify this file manually but run the tool once more instead -->

<!-- Last refresh date: 2020-04-25 10:43:19 -->

<!-- below, content of ./index.md -->

# Bash

![Banner](./images/banner.png)

<!-- table-of-contents - start -->
* [Bash on ms-dos](#bash-on-ms-dos)
    * [Run bash from Windows 10](#run-bash-from-windows-10)
       * [Add an alias](#add-an-alias)
       * [Possible problems](#possible-problems)
* [Bash with git bash](#bash-with-git-bash)
<!-- table-of-contents - end -->

<!-- below, content of ./dos/readme.md -->

## Bash on ms-dos

<!-- below, content of ./dos/windows_10/readme.md -->

### Run bash from Windows 10

If you get trouble by running `bash` from a command prompt, specify the full path like this:

```bash
"C:\Program Files\Git\bin\bash.exe" yourscript.sh
```

It should works now.

#### Add an alias

Don't want to specify each time the full path? Just create an alias.

Edit your system variables by running the `Edit system environment variables` program (i.e. click on the `Start` button then start to type `Edit system...`).

Click on the `Path` in the **system variable** area (see screen capture below).

![edit_path](./dos/windows_10/images/edit_path.png)

Add a new folder at the very first position. *I've chosen to create such folder: `C:\Christophe\Repository\aliases\` on my side.*

![add_to_path](./dos/windows_10/images/add_to_path.png)

**Note: make sure the alias folder is at the first position to have the priority to any other command having the same name.**

Go now to your aliases folder and add a new file called `bash.cmd` and edit the file. Type the following content:

```bash
@echo off
REM cls  -- Don't clear the screen, need to keep it for batch operations
REM And make sure to return the exit code
"C:\Program Files\Git\bin\bash.exe" %*

set errorcode=%ERRORLEVEL%

IF %errorcode% NEQ 0 (
    echo     [31mERROR - The bash script has returned an error %errorcode%[0m
    echo     [31mThe command line was:[0m
    echo.
    echo     [31m"C:\Program Files\Git\bin\bash.exe" %*[0m
    echo.
)

EXIT /B %errorcode
```

Since you've modified your `PATH` variable, close any command prompt screen and start a new one.

Now, by just typing `bash` it should works.

#### Possible problems

By just running `bash` from the command prompt, you can get this error:

```text
Windows Subsystem for Linux has no installed distributions.
Distributions can be installed by visiting the Microsoft Store:
https://aka.ms/wslstore
```

Note: the default `bash` interpreter is located in the `C:\Windows\System32\` folder

<!-- below, content of ./git/readme.md -->

## Bash with git bash

If you want to use git bash, you must follow these steps:

* Download [Git for Windows](https://gitforwindows.org)
* Install it.
* Execute this command in your power shell console as an administrator:

```bash
$files = (Get-ChildItem 'C:\Program Files\Git\usr\bin\*.exe').FullName

$files.ForEach({Set-ProcessMitigation $_ -Disable ForceRelocateImages})
```

* Edit your system variables by running the `Edit system environment variables` program (i.e. click on the `Start` button then start to type `Edit system...`).
* Click on the `Path` in the **system variable** area (see screen capture below).

    ![edit_path](./git/images/edit_path.png)

* Move the git command folder before system32
* Execute git as an administrator
