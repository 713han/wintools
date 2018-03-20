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