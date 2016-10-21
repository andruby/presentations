theme: Zurich, 5

## Unixcorn
![](unicorn-cartoon.jpg)

---

# Plan

* command
* combine
* conquer

---

# Command: cat, tail & head

```bash
# output contents of file to STDOUT
cat file
# print the last 10 lines to STDOUT
tail file
# print last 20 lines and keep following
tail -n 20 -f file
```

---

# Combine

```bash
# The pipe character connects left STDIN with right STDOUT
head -n 100 file | tail -n 10
# FIFO (named pipes)
mkfifo my_pipe
gzip -9 -c < my_pipe > out.gz &
cat file > my_pipe
rm my_pipe
```

---

# Combine

```bash
# output to file
cat file > other_file
# Dump database, zip and save to dated file
pg_dumpall | gzip -c > database_$(date +%Y-%m-%d).sql.gz
```

---

# Bonus: bcat [^1]

```bash
gem install bcat
# read the tail man page in your browser
man tail | bcat
# in .bashrc or .zshrc
export MANPAGER='col -b |bcat'
```

[^1]: Browser cat, see http://rtomayko.github.io/bcat/

---

# Command: sort & uniq

```bash
# Sort lines of a file, numerically
sort -nr file
# Only show duplicate lines once (input must be sorted)
uniq
# Count duplicate lines
uniq -c
```

---

# Command: curl

```bash
# Transfer from URL.
# Use 'copy as curl' from Chrome. Cookies!
curl 'http://localhost:3000/assets/application-...js'
-H 'Cookie: _session_id=d42df..; XSRF-TOKEN=7Kj5K..;' > app.js
```

---

# Command: netcat [^1]

```bash
# Server serves a file
cat backup.iso |  nc -l 3333
# Client downloads the file
# Show progress with pv
nc 192.168.0.1 3333 | pv -b > backup.iso
# Create partition image, send to a remote machine
dd if=/dev/hdb5 | gzip -9 | nc -l 3333
```

[^1]: https://www.g-loaded.eu/2006/11/06/netcat-a-couple-of-useful-examples/

---

# Command: ssh

```bash
# SSH tunnel
```

---

# Command: wc, ls

```bash
# Count lines
cat file | wc -l
# Count chars
cat file | wc -m
# Count words
cat file | wc -w
# Files sorted by time modified, recent last
ls -ltr
```

---

# Command: netstat

```bash
# On linux (not BSD/OS X),
# show programs listening to tcp
sudo netstat -tpl
```

---

# Command: ps, top, iotop


---

## Command: tee, sudo

---

## OS X: pbcopy, pbpaste

---

## Tool: sed

---

## Tool: awk

---

## Tool: grep

---

## Conquer

> Copy the contents of a remote file to clipboard

```bash
ssh server.com "cat /remote/file" | pbcopy
```

---

## Conquer

> Find the longest lines in a text file?

```bash
cat app.js | awk '{print length, $0}' | sort -nr | head -100 | less
```

---

## Conquer

> Transfer postgresql database in one awesome pipe

```bash
# From the receiving end
ssh server.com "pg_dumpall | gzip -6" | gunzip -c | psql
```

---

## Conquer

> Find the most used commands from your shell history

---

## Conquer

> Find the most used commands from your shell history

```bash
history | awk '{print $2}' | sort | uniq -c | sort -nr | head
```

---

# More

* https://www.tjhsst.edu/~dhyatt/superap/unixcmd.html
* https://www.tutorialspoint.com/unix/unix-useful-commands.htm
* https://www.quora.com/What-is-the-best-list-of-Unix-commands-that-I-can-stick-on-the-walls-of-my-cubicle
