# Command Prompt

# Clear Screen

```cmd
cls
```

# Check for Admin

```cmd
@echo off

net session >nul 2>&1
if NOT %ERRORLEVEL% == 0 (
    echo Error: This program must be ran with Administrative privilages.
)

:EXIT
echo[
echo Press any key to exit...
pause >nul
```

# Get Computer Name

```cmd
@echo off

hostname|clip
hostname
goto EXIT

:EXIT
echo[
echo Press any key to exit...
pause >nul
```

# Get IP Address

```cmd
@echo off

ipconfig
goto EXIT

:EXIT
echo[
echo Press any key to exit...
pause >nul
```

# Loop All Arguments

```cmd
@echo off

goto ARGS

:ARGS
for %%a in (%*) do (
    echo %%a
)
goto EXIT

:EXIT
echo[
echo Press any key to exit...
pause >nul
```

# Usage

```cmd
@echo off

goto USAGE

:USAGE
echo Usage: %~f0
echo     Args:
echo         /d - run debug build
echo         /r - run release build (Default)
echo         /u - trigger uninstall
echo         /h - display usage
echo[
echo     *Must be ran with Administrative privilages!
goto EXIT

:EXIT
echo[
echo Press any key to exit...
pause >nul
```

# User Input For Exit
```cmd
@echo off

goto EXIT

:EXIT
echo[
echo Press any key to exit...
pause >nul
exit /b 0
```
