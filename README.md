### CmdLets
1. [Add-Content](#add-content)
2. [Clear-Content](#clear-content)
3. [Compare-Object](#compare-object)
4. [Copy-Item](#copy-item)
5. [ForEach-Object](#foreach-object)
6. [Format-List](#format-list)
7. [Get-ChildItem](#get-childitem)
8. [Get-Clipboard](#get-clipboard)
9. [Get-Command](#get-command)
10. [Get-Content](#get-content)
11. [Get-Date](#get-date)
12. [Get-Location](#get-location)
13. [Group-Object](#group-object)
14. [Invoke-Item](#invoke-item)
15. [Measure-Object](#measure-object)
16. [Move-Item](#move-item)
17. [New-Item](#new-item)
18. [Out-File](#out-file)
19. [Remove-Item](#remove-item)
20. [Rename-Item](#rename-item)
21. [Select-Object](#select-object)
22. [Select-String](#select-string)
23. [Set-Clipboard](#set-clipboard)
24. [Set-Content](#set-content)
25. [Set-Location](#set-location)
26. [Sort-Object](#sort-object)
27. [Tee-Object](#tee-object)
28. [Test-Path](#test-path)
29. [Where-Object](#where-object)
30. [Write-Host](#write-host)

| PowerShell command | description |
|:---:|:---|
| `CTRL + c` | Kills the current process |
| `Clear-Host` `clear` `cls` | Clears the PowerShell Console |
| `start cmd` | Opens cmd.exe in the current directory |
| `start powershell` | Opens PowerShell in the current directory |
| `start notepad` | Opens notepad.exe |
| `start .` | Opens the current directory |
| `start ..` | Opens the parent folder of current directory |
| `start \` | Opens the root folder of current directory, *(eg. C:\\)* |
| `C:` | Switch the directory to **C:** |
| `D:` | Switch the directory to **D:** |
| `mkdir FolderA FolderB` | Creates 2 new folders of the name "FolderA" and "FolderB" in the current directory |
| `mkdir "Folder A" "Folder B"` | Creates 2 new folders of the name "Folder A" and "Folder B" in the current directory |
| `$a = "hello world"` | Declares the `$a` variable |
| `$a` | Prints out the value of `$a` variable |

###### [#top](#cmdlets)
###### New-Item
| `New-Item` `ni` | description |
|:---:|:---|
| `New-Item file.txt` | Creates new file *file.txt* in the current directory |
| `New-Item file.txt -type file` | Creates new file *file.txt* in the current directory |
| `New-Item css -type directory` | Creates new *css* folder in the current directory |
| `New-Item css.files -type directory` | Creates new *css.files* folder in the current directory |
| `New-Item file.txt -force` | Replaces the existing *file.txt* file in the current directory |
| `New-Item "folder A\file.txt"` | Creates new file *file.txt* in the *folder A* folder of the current directory |
| `New-Item "modules\js modules" -type directory` | Creates the new folder *js modules* in the new folder *modules* in the current directory |
| `New-Item ..\file.txt` | Creates new file *file.txt* in the parent folder of the current directory |
| `New-Item ..\css` | Creates new folder *css* in the parent folder of the current directory |
| `New-Item .gitignore -value "node_modules"` | Creates new file *.gitignore* with defined value |

###### [#top](#cmdlets)
###### Rename-Item
| `Rename-Item` `rni` `ren` | description |
|:---:|:---|
| `Rename-Item -path main.js -newname bundled.js` | Renames the *main.js* into the *bundled.js* |
| `Rename-Item main.js bundled.js` | Renames the *main.js* into the *bundled.js* |
| `Rename-Item media.css media.scss` | Changes the extension of the *media.css* file into the *media.scss* file |
| `Get-ChildItem "public" -file \| ForEach-Object {$_ \| Rename-Item -newname "$($_.basename)_copy$($_.extension)"}` | Adds *"_copy"* at the end of the name of each file in the *public* folder |
| `Get-ChildItem "styles\*.css" \| rename-item -newname {"$($_.basename).scss"}` | Changes the extension of each *.css* file into *.scss* in the *styles* folder |

###### [#top](#cmdlets)
###### Remove-Item
| `Remove-Item` `ri` `rd` `erase` `rm` `rmdir` `del` | description |
|:---:|:---|
| `Remove-Item test.txt` | Removes *test.txt* file from the current location |
| `Remove-Item public\*` | Removes all files and folders inside *public* folder. If the *public* folder contains subfolders, the **prompt** will be shown to comfirm deletion |
| `Remove-Item public\* -recurse` | Removes all files and folders inside *public* folder. If the *public* folder contains subfolders, the **prompt** will **not** be shown to comfirm deletion |
| `Remove-Item public\*.*` | Removes only files in the *public* folder |
| `Remove-Item *.* -force` | Removes **all files** in the current location, including **readonly** and **hidden** files |
| `Remove-Item public\* -recurse -exclude *.css` | Removes all files in the *public* folder and all its subfolders, except the *.css* files. It **remains** the subfolders that contain *.css* files |
| `Remove-Item media\* -inlude *.gif,*.ico` | Removes **only** *.gif* and *.ico* files from *media* folder |
| `Remove-Item media\* -include *.css,*.scss -exclude font*`  | Removes **only** *.css* and *.scss* files from *media* folder, but **remains** *.css* and *.scss* files that names begin with *font* |
| `Remove-Item media\* -include *.css,*.scss -exclude font* -whatIf` | Returns the information *(instead of removing any items)* which items would be removed if we called this command without `-whatIf` parameter |
| `Get-ChildItem -file -recurse \| Where-Object {$_.attributes -match "hidden"} \| Remove-Item -force` | Removes all **hidden files** from the current location |

###### [#top](#cmdlets)
###### Copy-Item
| `Copy-Item` `cpi` `cp` `copy` | description |
|:---:|:---|
| `Copy-Item file.txt "folder A"` | Copies the *file.txt* file from the current directory to the *folder A* folder |
| `Copy-Item file.txt ..` | Copies the *file.txt* file from the current directory to the parent folder |
| `Copy-Item "templates\main.txt" "html\main.html"` | Replaces the content of *main.html* with the content of *main.txt* |
| `Copy-Item file.txt media.css` | Replaces the content of *media.css* with the content of *file.txt* |
| `Copy-Item modules\* js` | Copies all files and **empty folders** *(without content)* from the *modules* folder to the *js* folder |
| `Copy-Item modules\* js -recurse` | Copies all files and **folders with content** from the *modules* folder to the *js* folder |
| `Copy-Item modules\*.js js` | Copies all *.js* files from the *modules* folder to the *js* folder |
| `Copy-Item *.* js` | Copies all **files** *(regardless the extension)* to the *js* folder |
| `Copy-Item tests public -recurse` | Copies *tests* folder to the *public* folder |

###### [#top](#cmdlets)
###### Move-Item
| `Move-Item` `mi` `mv` `move` | description |
|:---:|:---|
| `Move-Item main.js public` | Moves the *main.js* file to the *public* folder |
| `Move-Item scripts\*.ts typescript` | Moves all *.ts* files to the *typescript* folder |
| `Move-Item dev\package.json .` | Moves *package.json* file to the current location |
| `Move-Item ajax.js scripts -force` | Moves *ajax.js* to the *scripts* folder. If the *ajax.js* file exists in the *scripts* folder, its content is replaced by the moving file's content. |
| `Move-Item parsed.js scripts\main.js` | Moves the *parsed.js* file to the *scripts* folders and renames it to *main.js* |
| `Move-Item uglified.js scripts\main.js -force` | If *main.js* file exists in the *scripts* folders, its content is replaced by the moving file's content |
| `Move-Item scripts public` | Moves the *scripts* folder with its all elements to the *public* folder |
| `Move-Item parsed public\scripts` | If the *scripts* folder does not exist, it moves *parsed* folder to the *public* folder and renames it to *scripts* |
| `Move-Item ".\*\*" allfiles` | Moves all items from all folders *(two levels down)* in the current location to the *allfiles* folder |
| `Get-ChildItem -file -recurse \| Move-Item -destination "allfiles"` | Moves all files from all folders in the current location to the *allfiles* folder |

###### [#top](#cmdlets)
###### Add-Content
| `Add-Content` `ac` | description |
|:---:|:---|
| `Add-Content file.txt "some new content"` | Adds extra content at the end of the last line in the *file.txt* |
| `Add-Content new_file.txt "some new content"` | Creates *new_file.txt* with the content |
| `Add-Content *.txt "new content"` | Adds extra content to each *.txt* file in the current directory |
| `Add-Content a* "new content"` | Adds extra content to each file in which the name begins with *a* letter |
| `Add-Content file?.js "new content"` | Adds extra content to *fileA.js*, *fileB.js*, *file1.js*, *file5.js*, etc. |
| `Add-Content file??.js "new content"` | Adds extra content to *fileAA.js*, *fileAB.js*, *file15.js*, *file06.js*, etc. |
| `Add-Content file*.js "new content"` | Adds extra content to *fileA.js*, *fileB.js*, *fileABC.js*, *file0234567.js*, etc. |
| `Add-Content *.* "new content"` | Adds extra content to **each file** in the current directory |
| ``Add-Content file.txt "`nextra text"`` | Adds extra content at the **new line** in the *file.txt* |
| ``Add-Content file.txt "extra`ttext"`` | Adds extra content with the **horizontal tab** in the *file.txt* |
| ``Add-Content file.txt "some `"quoted`" text"`` | Adds extra content with **quotes** in the *file.txt* |
| ``Add-Content file.txt 'some `'quoted`' text'`` | Adds extra content with **quotes** in the *file.txt* |

###### [#top](#cmdlets)
###### Set-Content
| `Set-Content` `sc` | description |
|:---:|:---|
| `Set-Content test.txt -value "hello world"` | Replaces the content of *test.txt* file with the new content |
| `Get-Date \| Set-Content test_time.txt` | Replaces the content of *test_time.txt* with the current date |
| `Set-Content new_file.txt "hello world"` | Replaces the content of *new_file.txt* *(or creates new_file.txt if not exists)* with the new content |
| `Get-Content main.js \| ForEach-Object {$_ -replace "new Error","new TypeError"} \| Set-Content parsed.js` | Gets the content of *main.js* and saves changed content in *parsed.js* file |
| `Get-Content main.js \| ForEach-Object {$_ -replace "//.*",""} \| Set-Content parsed.js` | Gets the content of *main.js* and saves the new content with all comments removed in *parsed.js* file |

###### [#top](#cmdlets)
###### Get-Content
| `Get-Content` `gc` `type` `cat` | description |
|:---:|:---|
| `Get-Content css\layout.css` | Displays the content of *layout.css* file |
| `Get-Content css\layout.css -totalcount 5` | Displays the first 5 lines of the content of *layout.css* file |
| `Get-Content css\layout.css \| Select-Object -first 5` | Displays the first 5 lines of the content of *layout.css* file |
| `Get-Content css\*.css -first 1 \| Set-Content css\first_lines.txt ` | Gets the first line of each *.css* file and store them in the *first_lines.txt* file |
| `(Get-Content css\layout.css)[0].length` | Returns the length of the first line of the *layout.css* file |
| `(get-content scripts\main.js \| where-object {$_.length -eq 0} \| measure-object).count` | Returns the number of empty lines in the *main.js* file |

###### [#top](#cmdlets)
###### Clear-Content
| `Clear-Content` `clc` | description |
|:---:|:---|
| `Clear-Content file.txt` | Erases the whole content of *file.txt* |
| `Clear-Content *.txt` | Erases the whole content of each *.txt* file in the current directory |
| `Clear-Content a*` | Erases the whole content of each file in which the name begins with *a* letter |
| `Clear-Content file?.js` | Erases the whole content of *fileA.js*, *fileB.js*, *file1.js*, *file5.js*, etc.|
| `Clear-Content file??.js` | Erases the whole content of *fileAA.js*, *fileAB.js*, *file15.js*, *file06.js*, etc.|
| `Clear-Content file*.js` | Erases the whole content of *fileA.js*, *fileB.js*, *fileABC.js*, *file0234567.js*, etc.|
| `Clear-Content *.*` | Erases the whole content of **each file** in the current directory|

###### [#top](#cmdlets)
###### Select-String
| `Select-String` `sls` | description |
|:---:|:---|
| `"hello world" \| Select-String "world"` | Returns the line(s), where the word *"world"* has been found |
| `"hello world" \| Select-String "world" -quiet` | Returns **True**, what means that at least one word *"world"* has been found |
| `Select-String -path "logs\*.txt" -pattern "failure"` | Checks, whether there is any occurance of *"failure"* in any of *.txt* files in *logs* folder. If so, it returns the list of files and lines that contain pattern |
| ``"this is line 1`nthis is line 2" \| Select-String "`n" -quiet`` | Returns **True**, what means that at least one **new line character** has been found |
| `Get-Process \| Select-String "chrome" -quiet` | Returns true, if the list of processes contains *"chrome"*, or does nothing *(if any "chrome" word has been found, the **false** is not returned)* |
| `Get-Content scripts\main.js \| Select-String "module.exports"` | Returns the line(s), where the sentence *"module.exports"* has been found|
|`Get-Content logs.txt \| Select-String "disabled" -quiet -casesensitive`|Returns true, if the content of *logs.txt* file contains at least one occurance of *"disabled"* *(lower and upper case matters)*|
| `(get-alias).displayname \| select-string "copy-item"` | Returns all **aliases** that matches *"copy-item"* |
| `(Get-ChildItem "C:\Windows\Fonts").fullname \| Select-String "bold"` | Returns the list of paths of all system fonts that contain *"bold"* in the file name |

###### [#top](#cmdlets)
###### Get-ChildItem
| `Get-ChildItem` `gci` `ls` `dir` | description |
|:---:|:---|
| `Get-ChildItem` | Returns information about the objects in the current location |
| `Get-ChildItem public -directory` | Returns information about **folders** in the *public* folder |
| `Get-ChildItem public -file` | Returns information about **files** in the *public* folder |
| `(Get-ChildItem public -file).length` | Returns the number of any files in the *public* folder |
| `Get-ChildItem -recurse` | Returns information about the objects in the current location and all its subfolders |
| `Get-ChildItem public\js` | Returns information about the objects in the *js* folder |
| `Get-ChildItem scripts\*.js` | Returns information about all *.js* files in the *scripts* folder |
| `Get-ChildItem scripts\* -include *.js,*.css` | Returns information **only** about the *.js* and *.css* files in the *scripts* folder |
| `Get-ChildItem scripts\* -include *.*` | Returns information **only** about any **files** in the *scripts* folder |
| `Get-ChildItem scripts\*.* -recurse -exclude *.css` | Returns information about any **files** in the *scripts* folder and its subfolders **except** *.css* files |
| `Get-ChildItem @("css","js")` | Returns information about the objects in the *css* and *js* folders |
| `Get-ChildItem -file -recurse \| Where-Object {$_.attributes -match "readonly"}` | Returns all files in the current location and all subfolders, that have *readolny* attribute set|
| `Get-ChildItem -file -recurse \| Where-Object {$_.attributes -match "hidden"}` | Returns all files in the current location and all subfolders, that have *hidden* attribute set|
| `Get-ChildItem -file -recurse \| Select-Object directory,name` | Returns all files in the current location with names and paths |

###### [#top](#cmdlets)
###### Test-Path
| `Test-Path` | description |
|:---:|:---|
| `Test-Path "public\styles\main.scss"` | Checks if the *main.scss* file exists in the *styles* folder and returns **true** or **false** |
| `Test-path public\styles` | Checks if the *styles* folder exists in the *public* folder and returns **true** or **false** |
| `Test-Path "C:\","D:\","E:\"` | Checks if the listed locations exist and returns list of **true** and **false** results for each path|
| `Test-Path scripts\*.js` | Checks if any *.js* file exists in the *scripts* folder and returns **true** or **false**  |
| `Test-Path $env:appdata\npm` | Checks if the *npm* folder exists in the *roaming* folder |

###### [#top](#cmdlets)
###### Compare-Object
| `Compare-Object` `diff` | description |
|:---:|:---|
| `Compare-Object $a $b` | Compares the content of two variables and returns the differences between each line |
| `Compare-Object @(1,2,3,4) @(1,2,0,4)` | Compares the content of two arrays and returns the differences between each item |
| `Compare-Object $(Get-Content fileA.txt) $(Get-Content fileB.txt)` | Compares the content of *fileA.txt* and *fileB.txt* and returns the differences between each line|
| `Compare-Object $a $b -includeequal` | Compares the content of two variables and returns line-by-line comparison, including equal lines, signed as **`==`** |
| `Compare-Object $a $b -includeequal -excludedifferent` | Compares the content of two variables and returns **only equals** |

###### [#top](#cmdlets)
###### Group-Object
| `Group-Object` `group` | description |
|:---:|:---|
| `Get-Service \| Group-Object Status` | Returns `Get-Service` items grouped by the *Status* property |
| `Get-Service \| Group-Object Status,StartType` | Returns `Get-Service` in the groups of the same *Status* and *StartType* properties' values |
| `Get-ChildItem public\*.* \| Group-Object extension` | Returns `Get-ChildItem` files from the *public* folder grouped by the *extension* property |
| `Get-ChildItem public \| Group-Object extension \| Select-Object Name,Count` | Returns the number *(count property)* of the files of particular extension in the *public* folder |
| `Get-ChildItem public \| Group-Object extension \| Select-Object Name,Count \| Sort-Object Count -descending` | Returns the number *(count property)* of the files of particular extension in the *public* folder *(from the largest to the smallest number)* |

###### [#top](#cmdlets)
###### Where-Object
| `Where-Object` `?` `where` | description |
|:---:|:---|
| `Get-Service \| Where-Object -property status -eq "stopped"` | Returns the list of all services that are currently stopped *(in which the value of status property **equals** "Stopped")* |
| `Get-ChildItem \| Where-Object name -like "*.js"` | Returns the list of all *.js* files *(wildcard characters)* |
| `Get-ChildItem \| Where-Object {$_.name -like "*.js"}` | Returns the list of all *.js* files *(wildcard characters)* |
| `Get-ChildItem \| ? name -like "*.js"` | Returns the list of all *.js* files *(wildcard characters)* |
| `Get-ChildItem \| ? name -notlike "*— copy*"` | Returns the list of all files without *"— copy"* in its name *(wildcard characters)* |
| `Get-ChildItem -file \| Where-Object -property extension -eq ".js"` | Returns the list of all files with *.js* extension |
| `Get-ChildItem -file \| Where-Object -property extension -like ".js"` | Returns the list of all files with *.js* extension *(wildcard characters)* |
| `Get-ChildItem -file \| Where-Object -property extension -match ".js"` | Returns the list of all files with *.js* extension *(regular expression)* |
| `Get-Childitem -file \| ? extension -ne ".js"` | Returns the list of all files that **are not** *.js* files |
| `Get-ChildItem -file \| Where-Object -property length -gt 0` | Returns the list of all files in which the size is **greater than** 0 |
| `Get-ChildItem -file \| Where-Object -property length -eq 0` | Returns the list of empty files *(in which the length property **equals** 0)* |
| `Get-ChildItem scripts\*.* \| Where-Object -property name -like "m*"` | Returns the list of all files that name begins with *m* *(wildcard characters)* |
| `Get-ChildItem -file \| ? name -like "m*.js"` | Returns the list of *.js* files that name begins with *m* *(wildcard characters)* |
| `Get-ChildItem -file \| ? {$_.name -like "a*" -and $_.extension -eq ".js"}` | Returns the list of *.js* files that name begins with *a* |
| `Get-ChildItem -file \| ? {($_.name -like "a*" -or $_.name -like "c*") -and ($_.extension -eq ".js" -or $_.extension -eq ".ts")}` | Returns the list of *.js* and *.ts* files that name begins with *a* or *c* |
| `Get-ChildItem \| ? {($_.length -gt 0) -and ($_.length -le 5000)}` | Returns the list of all files with the size **greater than** *0* **and lower or equal to** *5kb*|
| `Get-ChildItem styles\*.css \| Where-Object -property name -match "^p.*"` | Returns the list of *.css* files that name begins with *p* *(regular expression)* |
| `Get-ChildItem \| Group-Object extension \| Where-Object -property count -ge 4` | Returns the list of groups of **4 or more** files of particular extension in the current location |
| `Get-Process \| Where-Object -property processname -like "*host*"` | Returns the list of processes that contain *"host"* in the process name *(wildcard characters)* |
| `Get-Process \| Where-Object -property processname -match "host"` | Returns the list of processes that contain *"host"* in the process name *(regular expression)* |
| `Get-ChildItem -directory \| Where-Object {(Get-ChildItem $_).length -eq 0}` | Returns the list of empty folders in the current location |
|`Get-ChildItem *.js \| Where-Object {(Get-Content $_).length -le 100}`| Returns the list of *.js* files that contain **100 or less** lines |
| `Get-ChildItem -file \| ? {($_.lastwritetime \| Get-Date) -lt ("01.01.2017 12:00" \| Get-Date)}` | Returns the list of files that were edited prior to *January 1st 2017 12:00*  |

###### [#top](#cmdlets)
###### ForEach-Object
| `ForEach-Object` `foreach` `%` | description |
|:---:|:---|
| `Get-Content ajax.js \| ForEach-Object {$_ -replace ".*","//$($_)"} \| Set-Content parsed.js` | Comments out each line of *ajax.js* file and stores new content in the *parsed.js* file |
| `Get-Content main.js \| ForEach-Object {$_ -replace "new Error","new TypeError"} \| Set-Content parsed.js` | Gets the content of the *main.js* file and saves changed content in the *parsed.js* file |
| `Get-Content main.js \| ForEach-Object {$_ -replace "//.*",""} \| Set-Content parsed.js` | Gets the content of the *main.js* and saves the new content with all comments removed in the *parsed.js* file |
| `Get-ChildItem "public" -file \| ForEach-Object {$_ \| Rename-Item -newname "$($_.basename)_copy$($_.extension)"}` | Adds *"_copy"* at the end of the name of each file in the *public* folder |
| `Get-ChildItem dist\*.* -file -recurse -force \| ForEach-Object {$_.attributes = "hidden"}` | Hides all files in the *dist* folder |

###### [#top](#cmdlets)
###### Measure-Object
| `Measure-Object` `measure` | description |
|:---:|:---|
| `Get-ChildItem public -file \| Select-Object name,length \| Measure-Object length -sum -min -max -ave` | Returns the statistics object for all files in the *public* folder *(based on the file size values)*. Indicates the **number of scores**, the **minimal**, **maximal** and **average** file size and the **sum** of all file sizes.  |

###### [#top](#cmdlets)
###### Sort-Object
| `Sort-Object` `sort` | description |
|:---:|:---|
| `Get-ChildItem css \| Sort-Object name` | Sorts `Get-ChildItem`'s returned data by name |
| `Get-ChildItem css \| Sort-Object name -descending` | Sorts `Get-ChildItem`'s returned data by name in descending order|
| `Get-ChildItem css \| Sort-Object extension,name` | Sorts `Get-ChildItem`'s returned data by multiple properties, first by extension, then by name |
| `Get-ChildItem css \| Sort-Object extension,name -descending` | Sorts `Get-ChildItem`'s returned data by multiple properties, first by extension, then by name, both in descending order |
| `Get-ChildItem ajax\*.json \| Sort-Object length -descending` | Lists the largest `Get-ChildItem`'s returned *.json* files first, and the smallest ones last |

###### [#top](#cmdlets)
###### Select-Object
| `Select-Object` `select` | description |
|:---:|:---|
| `Get-ChildItem scripts \| Sort-Object length \| Select-Object name,length` | Returns `Get-ChildItem` sorted data table with **only** *name* and *length* property |
| `Get-ChildItem scripts\*.js \| Select-Object *Name*,length` | Returns `Get-ChildItem` *.js* files with all properties that include *"Name"* *(eg. PSChildName, BaseName, FullName, Name)* and with *length* property |
| `Get-ChildItem scripts\*.* \| Sort-Object length -descending \| Select-Object -first 5` | Returns `Get-ChildItem` 5 files of the largest size |
| `Get-ChildItem scripts\*.* \| Sort-Object length -descending \| Select-Object -last 5` | Returns `Get-ChildItem` 5 files of the smallest size |
| `Get-ChildItem css\*.css \| Sort-Object name \| Select-Object name -first 1` | Returns `Get-ChildItem` first *(in the alphabetical order)* *.css* file from the *css* folder  |
| `Get-ChildItem scripts \| Select-Object *` | Returns `Get-ChildItem` items from the *scripts* folder with **all properties** and values *(if there is too much data to display the table, it will be **displayed as a list**)* |
| `Get-ChildItem scripts \| Select-Object * -exclude VersionInfo,FullName` | Returns `Get-ChildItem` items from the *scripts* folder with **all properties** and values **except** *VersionInfo* and *FullName* properties |
| `Get-ChildItem scripts \| Select-Object * -exclude *Time*` | Returns `Get-ChildItem` items from the *scripts* folder with **all properties** and values **except** all properties that include *"Time"*, *(eg. CreationTime, LastWriteTime, LastWriteTimeUtc)* |

###### [#top](#cmdlets)
###### Format-List
| `Format-List` `fl` | description |
|:---:|:---|
| `Get-Service \| Format-List` | Displays `Get-Service` returned data **always as a list** |
| `Get-ChildItem \| Format-List` | Displays `Get-ChildItem` returned data as a list |
| `Get-ChildItem scripts \| Sort-Object extension \| Format-List ` | Displays `Get-ChildItem` returned and sorted data as a list |
| `Get-ChildItem scripts \| Sort-Object extension \| Select-Object name,length \| Format-List` | Displays `Get-ChildItem` returned and sorted files' names and sizes as a list |
| `Get-ChildItem public \| Group-Object extension \| Format-List` | Displays `Get-ChildItem` returned items grouped by extension as a list |
| `Get-ChildItem scripts \| Format-List *` | Displays `Get-ChildItem` returned items with **all properties** as a list |
| `Get-ChildItem scripts \| Format-List Last*` | Displays `Get-ChildItem` returned items with properties that begin with *Last* *(eg. LastAccessTime, LastWriteTime)* as a list |
| `Get-ChildItem scripts \| Format-List name,length` | Displays `Get-ChildItem` returned items with *name* and *length* property |

###### [#top](#cmdlets)
###### Write-Host
| `Write-Host` | description |
|:---:|:---|
| `Write-Host "hello world!"` | Displays the output message in the PowerShell console |
| `Write-Host (node tests)` | Displays the output of the *tests.js* file execution in the PowerShell console |
| `Write-Host "hello " -nonewline; Write-Host "world!"` | Displays two output messages **without line break** |
| `Write-Host "hello world!" -foregroundcolor darkblue -backgroundcolor yellow` | Displays the output message in the PowerShell console with the blue text color and the yellow background color. Possible colors: *[Black, DarkBlue, DarkGreen, DarkCyan, DarkRed, DarkMagenta, DarkYellow, Gray, DarkGray, Blue, Green, Cyan, Red, Magenta, Yellow, White]* |
|`Write-Host "this is inline " -nonewline; Write-Host "error " -foregroundcolor red -nonewline; Write-Host "text!"`|Displays the output message with the different styles used in one line|

###### [#top](#cmdlets)
###### Out-File
| `Out-File` | description |
|:---:|:---|
| `Out-File -inputobject "hello world!" -filepath output.txt` | Stores the output content in the *output.txt* file|
| `"hello world!" \| Out-File output.txt` | Stores the output content in the *output.txt* file|
| `node tests \| Out-File test_results.txt` | Stores the output of the *tests.js* file execution in the *test_results.txt* file |
| `npm ls -g \| Out-File global_modules.txt` | Stores the returned list of globally installed modules via npm in the *global_modules.txt* file|
| `Get-Process \| Out-File proc.txt -width 150` | Stores the list of processes in the *proc.txt* file and determines the maximum length of each line to 150 characters *(longer lines will be truncated)* |
| `Get-ChildItem -file \| Select-Object name,length,directory \| format-list * \| Out-File dirs.txt` | Creates the list of files in the current location and stores it in the *dirs.txt* file |
| `Get-Content paths.txt \| ForEach-Object {$_ -replace "Users\\some_user","Users\user_123"} \| Out-File "new_user.txt"` | Stores the output in the *new_user.txt* file rather than displaying it on the screen |

###### [#top](#cmdlets)
###### Tee-Object
| `Tee-Object` `tee` | description |
|:---:|:---|
| `Get-Process \| Tee-Object process.txt` | Displays the output content in the PowerShell console and then stores it in the *process.txt* file |
| `node run \| Tee-Object return.txt` | Displays the output content of the *run.js* file execution and then stores it in the *return.txt* file |
| `Get-Content logs.txt \| Tee-Object logs_copy.txt` | Displays the output content of the *logs.txt* file and then stores it in the *logs_copy.txt* file |

###### [#top](#cmdlets)
###### Get-Location
| `Get-Location` `gl` `pwd` | description |
|:---:|:---|
| `Get-Location` | Returns the current location |

###### [#top](#cmdlets)
###### Set-Location
| `Set-Location` `cd` `sl` `chdir` | description |
|:---:|:---|
| `Set-Location ..` | Switches the current location to the **parent folder** |
| `Set-Location ..\..` | Switches the current location to the folder **two levels top** |
| `Set-Location \` | Switches the current location to the **drive root folder** |
| `Set-Location ".\public"` | Switches the current location to the *public* folder *(the child folder of the current location)* |
| `Set-Location public` | Switches the current location to the *public* folder *(the child folder of the current location)* |
| `Set-Location dirA\dirB` | Switches the current location to the *dirB* folder *(two levels down)* |
| `Set-Location "dir A\dir B"` | Switches the current location to the *dir B* folder *(two levels down)* |
| `Set-Location alias:\` | Switches the current location to the Windows PowerShell drive for **aliases** |
| `Set-Location env:\` | Switches the current location to the Windows PowerShell drive for **environment variables** |
| `Set-Location $HOME` | Switches the current location to the *C:\Users\user* |
| `Set-Location $env:appdata` | Switches the current location to the *C:\Users\user\AppData\Roaming* |
| `Set-Location $env:localappdata` | Switches the current location to the *C:\Users\user\AppData\Local* |
| `Set-Location $env:systemdrive\` | Switches the current location to the *C:\\* |
| `Set-Location $env:systemroot` | Switches the current location to the *C:\Windows* |
| `Set-Location $env:programfiles` | Switches the current location to the *C:\Program Files* |
| `Set-Location HKCU:\` | Switches the current location to the *HKEY_CURRENT_USER* |
| `Set-Location HKLM:\` | Switches the current location to the *HKEY_LOCAL_MACHINE* |

###### [#top](#cmdlets)
###### Get-Clipboard
| `Get-Clipboard` `gcb` | description |
|:---:|:---|
| `Get-Clipboard` | Gets the current clipboard entry |

###### [#top](#cmdlets)
###### Set-Clipboard
| `Set-Clipboard` `scb` | description |
|:---:|:---|
| `Set-Clipboard -value "Copied text"` | Sets the current clipboard entry to the new value |
| `Get-Content clipboard.txt \| Set-Clipboard` | Gets the content of *clipboard.txt* file and sets it as the current clipboard entry |

###### [#top](#cmdlets)
###### Get-Command
| `Get-Command` `gcm` | description |
|:---:|:---|
| `Get-Command` | Returns the data of **all** Windows PowerShell cmdlets |
| `Get-Command \| Select-Object name` | Returns only the **names** of **all** Windows PowerShell cmdlets |
| `Get-Command \| Format-List *` | Returns **all** data of **all** Windows PowerShell cmdlets as a list |
| `Get-Command \| Select-Object name,verb,noun` | Returns the *verb-* and *-noun* of all Windows PowerShell cmdlets, that build the *verb-noun* name of cmdlet |
| `Get-Command Get-ChildItem \| Format-List *` | Returns all data of `Get-ChildItem` cmdlet |
| `(Get-Command New-Item).parameters.keys` | Returns the list of all parameters's names of `New-Item` cmdlet |
| `Get-Command Get-*` | Returns the list of `cmdlet`s in which the name begins with *Get-* |
| `Get-Command @("Get-*","Set-*")` | Returns the list of `cmdlet`s in which the name begins with *Get-* or *Set-* |

###### [#top](#cmdlets)
###### Get-Date
| `Get-Date` | description |
|:---:|:---|
| `Get-Date` | Returns the **current date and time** in PowerShell console |
| `Get-Date -displayhint date` | Returns the **current date** in PowerShell console |
| `Get-Date -displayhint time` | Returns the **current time** in PowerShell console |
| `Get-Date 15.05.2017` | Returns the *date and time* *(15th May 2017 00:00:00)* |
| `Get-Date 15/05/2017` | Returns the *date and time* *(15th May 2017 00:00:00)* |
| `Get-Date "15.05.2017 15:00"` | Returns the *date and time* *(15th May 2017 15:00:00)* |
| `Get-Date "15.05.2017 15:30:25"` | Returns the *date and time* *(15th May 2017 15:30:25)* |
| `Get-Date "15.05.2017 3:30 AM"` | Returns the *date and time* *(15th May 2017 3:30:00)* |
| `Get-Date "15.05.2017 3:30 PM"` | Returns the *date and time* *(15th May 2017 15:30:00)* |
| `(Get-Date "15.05.2017 15:30:10").AddSeconds(14)` | Returns the *date and time* *(15th May 2017 15:30:24)* |
| `(Get-Date "15.05.2017 15:30:10").AddMinutes(7)` | Returns the *date and time* *(15th May 2017 15:37:10)* |
| `(Get-Date "15.05.2017 15:30:10").AddHours(3)` | Returns the *date and time* *(15th May 2017 18:30:10)* |
| `(Get-Date "15.05.2017 15:30:10").AddDays(1000)` | Returns the *date and time* *(9th February 2020 15:30:10)* |
| `(Get-Date "15.05.2017 15:30:10").AddMonths(15)` | Returns the *date and time* *(15th August 2018 15:30:10)* |
| `(Get-Date "15.05.2017 15:30:10").AddYears(2)` | Returns the *date and time* *(15th May 2019 15:30:10)* |
| `(Get-Date "15.05.2017 15:30:10").AddDays(2).AddMinutes(5)` | Returns the *date and time* *(17th May 2017 15:35:10)* |
| `(Get-Date "15.05.2017 15:30:10").AddMinutes(5).AddMinutes(5)` | Returns the *date and time* *(15th May 2017 15:40:10)* |

###### [#top](#cmdlets)
###### Invoke-Item
| `Invoke-Item` `ii` | description |
|:---:|:---|
| `Invoke-Item "C:\windows\system32\calc.exe"` | Runs the Calculator |
| `Invoke-Item "files\*.txt"` | Opens all *.txt* files from the *files* folder |
| `Invoke-Item "docs\*.xls"` | Opens all *Excel* files from the *docs* folder |
| `Invoke-Item files\* -exclude *.exe`| Opens all files in the *files* folder, except for *.exe* files |
| `Invoke-Item files\* -include *.docx,*.xlsx -exclude *admin*`|Opens *Word* and *Excel* files, except for the files that contain *"admin"* in its name|

###### [#top](#cmdlets)
