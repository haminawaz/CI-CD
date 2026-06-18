# What is WSL?

- WSL (Windows Subsystem for Linux) is a compatibility layer in Windows that lets you run a real Linux system _inside_ Windows.

## WSL Commands

```
wsl           # Open default Linux
wsl -l        # Show installed Linux systems
wsl -l -v     # show systems + status + version
wsl -d <name> # This means “Start a specific Linux system” e.g wsl -d Ubuntu
```

## Basic commands

```
pwd      # Shows current directory
ls       # Lists files/folders in current directory
ls -l    # You will see something like: `-rw-r--r-- 1 dev dev 20 file.txt`
- `-rw-r--r--` → permissions
- First `dev` → owner
- Second `dev` → group
- `r` = read, `w` = write, `x` = execute
- `-rw-r--r--` → Means: owner → read + write / others → read only
whoami   # Shows your Linux username (Short form of “who am I”)
hostname # Show name of the machine
uname -a # Shows Linux kernel version, System architecture and OS details
```

## Directories Commands

```
mkdir <folder-name>      # Create Folder (Short form of “make directory”)
cd <folder-name>         # Enter in a specific folder
touch <file-name>        # Create empty file
cp <filename> <filename> # Copy one file data to rewrite in another file (if file not created then also create file)
mv <filename> <filename> # Move or rename
grep "query" <filename>  # Search text in a file
rm <filename>            # Remove / Delete file
rm -r <folder name>      # Remove / Delete folder
find                     # Shows all files in the directory
find -name "<filename>"  # Shows searched file directory
find -name "*.<ext>"     # Searched all files with that extension like "*.md"
```

## Files Commands

```
echo "Hello linux server" > basic-file.md  # Write/Overwrite text into file **>** overwrites file
echo "Hello linux server" >> basic-file.md # >> = add new line instead of replacing
cat <filename>                             # Display full file content
tail <filename>                            # shows last 10 lines of the file
tail -f <filename>                         # keep watching file for new updates. This simulates real logs
```

## Change-Mode (chmod) Commands

| permissions | Numeric (Octal) | Meaning                   |
| :---------: | :-------------: | ------------------------- |
| r           | 4               | Read (view file)          |
| w           | 2               | Write (edit file)         |
| x           | 1               | Execute (run file/script) |

| Symbol |  Meaning         |
| :----: |  --------------- |
| u      |  User (owner)    |
| g      |  group           |
| o      |  others          |
| a      |  all (u + g + o) |

| permissions  | Meaning                       | Numeric (Octal) |
| :----------: | ----------------------------- | :-------------: |
| rwx          | Full permission `means owner` | 4 + 2 + 1 = 7   |
| rw-          | Read + write                  | 4 + 2 + 0 = 6   |
| r-x          | Read + Run `means group`      | 4 + 1 + 0 = 5   |
| r--          | Read Only `means others`      | 4 + 0 + 0 = 4   |
| ---          | No access                     | 0 + 0 + 0 = 0   |

| Operator | Meaning              |
| :------: | -------------------- |
| +        | Add permission       |
| -        | Remove permission    |
| =        | set exact permission |

```
chmod [who][operator][permissions] <filename> # Basic syntax
chmod u+x <filename>                          # Give execute permission to owner
chmod g-w <filename>                          # Remove write permission from group
chmod a+r <filename>                          # Gave read permission to all users
chmod u=rwx,g=rx,o=r <filename>               # Set exact permissions
chmod 755 <filename> # Set full permission to owner wile group and others contain (execute + run)
```

## Process Commands

```
ps                        # Show running processes for current user and terminal only and gave basic detail 
- PID → Process ID
- TTY → Terminal
- TIME → CPU time used
- CMD → Command name
ps aux                    # Show running process for all user in entire system and gave detailed view
ps aux | grep <something> # Show all running processes, then filter all lines that contain that something e.g node.
top                       # Shows real-time CPU/memory usage just like like Task Manager in Windows
kill <PID>                # Kill a process
kill [signal] <PID>       # Kill a process with som singals
```

| Signal    | Number | Meaning                 |
| --------- | ------ | ----------------------- |
| `SIGTERM` | 15     | Graceful stop (default) |
| `SIGKILL` | 9      | Force kill immediately  |
| `SIGSTOP` | 19     | Pause process           |
| `SIGCONT` | 18     | Resume paused process   |

## Journalctl (logs) Commands

```
journalctl               # view all system logs
journalctl -f            # view real time logs
journalctl --since today # Show logs for today
journalctl -n 50         # Show last 50 lines
journalctl -u <service>  # show logs for a specific service like nginx
journalctl -b            # Show logs since boot
journalctl -b -1         # Show previous boot logs
journalctl -p err        # Show only errors
```

## Ports Commands

```
ss -tuln                 # See open ports
- t = TCP
- u = UDP
- l = listening ports
- n = numeric output
ss -tuln | grep <port-num>       # Check a specific port
```

## CI/CD Commands

```
sudo                           # full form as "Super User DO" or simply runs a command as administrator (root).
sudo apt-get update            # It refreshes the available package list like check what versions are available
sudo apt-get install <service> # Download and install specific service e.g Git
sudo apt-get remove <service>  # Remove a specific service e.g Git

curl [options] <url>                 # talks to web servers like browser without a GUI
curl https://google.com              # This downloads and prints the HTML of the website
curl -I https://google.com           # Show only response headers
curl -O <url>/<filename>             # Saves file with original name e.g https://google.com/file.html

**API curl**
curl https://jsonplaceholder.typicode.com/todos/1              # Get API request
curl https://jsonplaceholder.typicode.com/todos/1 > <filename> # Create file and add api data or rewrite response data 

cat <filename>            # read a file and show output in terminal
cat <filename> <filename> # read both files and show output of both in terminal by concatination
cat > <filename>          # Create a file, then you can wrote anything in terminal and press CTRL + D to save
```

