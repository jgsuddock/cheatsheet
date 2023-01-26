# Command Prompt

# Clear Screen

```bash
cls
```

# Check for Admin

```bash
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

```bash
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

```bash
@echo off

ipconfig
goto EXIT

:EXIT
echo[
echo Press any key to exit...
pause >nul
```

# Loop All Arguments

```bash
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

```bash
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