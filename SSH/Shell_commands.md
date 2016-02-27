## Terminal/Shell Commands


### Go to last dir - `cd -`
```
cd -
```

### Brace Expansion - `{a,b}`
```
# rename file.zip to file.zip.bak
mv file.zip {,.bak}

# reverse above
mv file.zip.bak {.bak,}
```

### Tee

```
echo 'hello' | tee hi.txt 		# Write the file and see contens on screen
``

### Repeat last command - `!!`
```
sudo !!

```

### Substitution - `^searchWord^replaceWord
```
echo one two three
^three^four
# outputs one two four
```

### Open last command in the default editor - `fc`

(The editor can be changed on the environment variables)

```
fc
```


### Listing

```
ls 		# List files
ls -A 	# List all files with .dotfiles
ls lht 	# Human friendly file sizes
```

### Working with files

```
mkdir -p nested/directory/child 		# Create directory tree
cp -a first last						# Move recursively
rm -rf folder							# Delete a dir recursively
rm -rf *								# KABOOOM!!! Never do this!!!
```

### Find

```
find /directory -name '.query'		# Find in a file name

# Find files and perform an action on each of them
find . -maxdepth 1 -type -f -name '*.zip' -exec tar {} \;
```

### Job Control
```
sleep 100 &		# & - send the task to the background
# or Ctrl+z and type bg

fg			# Bring the background task to foreground
jobs		# List all jobs
kill PID	# Kill a process by ID
pgrep name	# Find a process ID by name
```

### Search files

```
grep -i 'sometext' /var/log/boot.log	# Search for sometext, i is for case insensitive
grep -v "#" /file.txt					# Search non matching text
grep -iC 4 'sometext' /file.text 		# C prints lines of context (4 lines above and below)
grep -l root /dir/*						# Show only file names
egrep -iv 'sudo|sshd' /file.txt			# (or use -E) Search enhanced regex
-o 										# Only show matching text
```

### Redirection

On *nix systems, all devices are treated as files. And there are 3 file streams open by default.
0. stdin - The keyboard
1. stdout - The screen
2. stderr - Errors

The numbers 0, 1, 2 are file descriptors. These get reset after a command is run.

- > # Redirect
- >> # Append
- < # Input

```
echo 'hello world' > hello.txt 			# > is the redirection operator. >> Appends
echo 'hello world' 1> hello.tex 		# Same as the command above

grep "ssh" ~/process.txt 2>> ~/output.txt 	# Search and append the stderr to output.txt
```

Special devices in *nix

- `/dev/null`	# discard everything
- `/dev/full`	# Simulate a full disk (useful for testing)

```
grep "term" invalid 2>&1 | grep "file" 	# Send stderr to stdout, and then look for "file"
```

### See files

```
head file.txt 			# First lines of file
tail -f /file.txt 		# See the file in real-time
tail -f /file.txt | grep "something" # Update in realtime and filter

cut -d':' -f1 '/file.csv' 	# Delimit a file and see output
```


#### References

- http://www.tldp.org/LDP/abs/html/
- https://www.youtube.com/watch?v=4txbMcGPs1E



