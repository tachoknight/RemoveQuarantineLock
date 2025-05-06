# RemoveQuarantineLock
Workflow to remove the quarantine lock from files for macOS.
## Purpose
Developers have a lot of programs that are not notorized, Java web apps like `.war` files, for example. These are files that I created and know are not malicious, but trying to open them in anything on macOS results in getting a dialog like:

![Not allowed](https://github.com/tachoknight/RemoveQuarantineLock/blob/main/lock.png)

So I decided to write a [Quick Action](https://support.apple.com/guide/automator/use-quick-action-workflows-aut73234890a/mac) in Automator to make it easy to disable the quarantine lock on any file.

## Installation
Simply place **Remove quarantine lock.workflow** in the `~/Library/Services` directory. 

## Usage
Right-click on the file in question, then select "Services", then choose "Remove quarantine lock" from the "Quick Actions" menu item. There is no output; the file will now be usable.

## How It Works
The workflow is three steps:

1. Workflow receives the selected file
2. Run AppleScript to get the absolute path of the selected file in standard Unix format. This was taken _directly_ from [my GetAbsolutePath workflow](https://github.com/tachoknight/GetAbsolutePath/tree/master).
3. Run a one-line shell script that actually disables the quarantine lock. The command it runs is:

	`xattr -d com.apple.quarantine $1`

	where `$1` is the filename with path from step 2.	

