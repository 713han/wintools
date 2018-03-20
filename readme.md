# windows batch script for backup

```
SETLOCAL
set log_time=%date:~0,4%-%date:~5,2%-%date:~8,2%
set log_path=G:\Log\Sync

IF NOT EXIST %log_path% (
	mkdir %log_path%
)

CALL :sync D:\, F:\disk_D, %log_path%\%log_time%_D.log
CALL :sync E:\, F:\disk_E, %log_path%\%log_time%_E.log

EXIT /B %ERRORLEVEL%

:sync
IF EXIST %~3 (
	"C:\Program Files (x86)\Windows Resource Kits\Tools\robocopy.exe" %~1 %~2 /mir /xa:sh /w:3 /r:1 /v /np /log+:%~3
) ELSE (
 	"C:\Program Files (x86)\Windows Resource Kits\Tools\robocopy.exe" %~1 %~2 /mir /xa:sh /w:3 /r:1 /v /np /log:%~3
)

attrib -s -h %~2
EXIT /B 0
```

- [Windows 10 version of Robocopy - issues with /MIR (does not recognize existing files)](https://social.technet.microsoft.com/Forums/ie/en-US/d2d63487-34c8-4fc2-8907-b2efd4316d62/windows-10-version-of-robocopy-issues-with-mir-does-not-recognize-existing-files?forum=win10itprogeneral) 
- [Windows Server 2003 Resource Kit Tools](https://www.microsoft.com/en-us/download/details.aspx?id=17657)