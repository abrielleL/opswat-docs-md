<!-- source: https://www.opswat.com/docs/mddrive/v4.4.10/knowledge-base/errors-when-low-disc-space-due-to-engines-db -->

# Errors when starting In-Session Scan: The available space of Drive partition is low due to engines database

View as Markdown Ask ChatGPT about this page Ask Claude about this page
#### [Overview:](/docs/mddrive/v4.4.10/knowledge-base/errors-when-low-disc-space-due-to-engines-db#overview)

On a MetaDefender Drive, when running **MetaDefender Drive In-Session Scan,** there is a message saying **Low Disk Space**

In some cases, the root cause of it is because engines folder are taking up space, like in this screenshot, ESET database is occupying 2.94GB.

#### [Solutions:](/docs/mddrive/v4.4.10/knowledge-base/errors-when-low-disc-space-due-to-engines-db#solutions)

1. Create a .cmd file with following content

@echo off
setlocal EnableDelayedExpansion
rem ============================================================
rem Remove-DatabaseFolders.cmd
rem Recursively finds all folders named "database" under
rem .\CTR\engines and deletes them.
rem
rem Usage:
rem Remove-DatabaseFolders.cmd (asks for confirmation)
rem Remove-DatabaseFolders.cmd /y (no prompt)
rem Remove-DatabaseFolders.cmd /list (dry-run, list only)
rem Remove-DatabaseFolders.cmd "C:\other\root" (custom root)
rem Remove-DatabaseFolders.cmd "C:\other\root" /y (custom + no prompt)
rem ============================================================
set "ROOT=%~dp0CTR\engines"
set "AUTO=0"
set "LISTONLY=0"
:parseArgs
if "%~1"=="" goto afterArgs
if /I "%~1"=="/y" ( set "AUTO=1" & shift & goto parseArgs )
if /I "%~1"=="-y" ( set "AUTO=1" & shift & goto parseArgs )
if /I "%~1"=="/list" ( set "LISTONLY=1" & shift & goto parseArgs )
if /I "%~1"=="-list" ( set "LISTONLY=1" & shift & goto parseArgs )
if /I "%~1"=="/?" ( goto usage )
if /I "%~1"=="-h" ( goto usage )
if /I "%~1"=="--help" ( goto usage )
set "ROOT=%~1"
shift
goto parseArgs
:afterArgs
if not exist "%ROOT%" (
echo [ERROR] Root path not found: %ROOT%
exit /b 1
)
echo Searching under: %ROOT%
echo.
set "COUNT=0"
for /f "delims=" %%D in ('dir /s /b /ad "%ROOT%" 2^>nul ^| findstr /i /e "\\database"') do (
set /a COUNT+=1
set "F!COUNT!=%%D"
echo %%D
)
if "%COUNT%"=="0" (
echo No "database" folders found.
exit /b 0
)
echo.
echo Found %COUNT% "database" folder(s^).
if "%LISTONLY%"=="1" (
echo [List-only mode] No changes made.
exit /b 0
)
if "%AUTO%"=="0" (
set /p "ANSWER=Delete all listed folders? [y/N]: "
if /I not "!ANSWER!"=="y" (
echo Aborted.
exit /b 0
)
)
set "REMOVED=0"
set "FAILED=0"
for /l %%I in (1,1,%COUNT%) do (
set "TARGET=!F%%I!"
if exist "!TARGET!" (
rd /s /q "!TARGET!"
if exist "!TARGET!" (
echo [FAIL] !TARGET!
set /a FAILED+=1
) else (
echo [REMOVED] !TARGET!
set /a REMOVED+=1
)
)
)
echo.
echo Done. Removed: %REMOVED%, Failed: %FAILED%
exit /b 0
:usage
echo Usage:
echo %~nx0 - prompt before deleting under .\CTR\engines
echo %~nx0 /y - delete without prompting
echo %~nx0 /list - list matches only, do not delete
echo %~nx0 "C:\path" - use a custom root folder
echo %~nx0 "C:\path" /y - custom root, no prompt
exit /b 0

2. Copy the script to **/MetaDefender Drive (disk-label):/tools** then run the script from there

3. Say "y" (yes) when asked and your disk space is reclaimed.

4. Launch Drive In-Session again and let it download needed data
