# Lab Report 1
---




**What happens when I do no arguments for:**
---

# `cd`:

Starting at `/home`:
```
[user@sahara ~]$ cd
[user@sahara ~]$
```
Starting from `/home/lecture1`:
```
[user@sahara ~/lecture1]$ cd
[user@sahara ~]$ 
```
Prior to using the `cd` command, I set the directory to `/home/lecture1`. After running the `cd` command, without any arguments, it brought us back to `/home`. HoIver, if you were to do this while already at `/home`, nothing would occur as you already at home.

# `ls`:

Starting from `/home/lecture1`:
```
[user@sahara ~/lecture1]$ ls
Hello.class  Hello.java  messages  README
```
I set the starting directory at `/home/lecture1` (Was `/home` prior). After running `ls`, I see all the files that exist within `/lecture1`.

# `cat`:

Starting from `/home`:
```
[user@sahara ~/lecture1]$ cat

```
After running `cat` without any arguements, you dont get an output because the `cat` command requires an arguement. In other words, you get an "error".

**What happens when I run each command with a path to a directory as an argument:**
---

# `cd`:

Starting at `/home`:
```
[user@sahara ~]$ `cd` lecture1/
[user@sahara ~/lecture1]$
```
When running `cd` with a directory as an argument, in this case, `lecture1/`, I notice the directory change from `/home` to `/home/lecture1`.

# `ls`:

Starting at `/home`:
```
[user@sahara ~]$ ls lecture1/
Hello.class  Hello.java  messages  README
```
After running ls with a directory as an argument, I notice that we are now able to view the contents of the specified directory without actually being in that directory. In this case, we were able to look into `/home/lecture1` by being in `/home`.

# `cat`:

Starting from `/home`:
```
[user@sahara ~]$ `cat`lecture1/
cat: lecture1/: Is a directory
```
After running `cat` with a directory as an argument, I noticed that we get an error stating that `lecture1/` (the directory I used as the argument) was a directory. This is because the `cat` command uses files as the argument, not directories.

**What happens when I run each command with a path to a file as an argument**
---

# `cd`:

Starting from `/home/lecture1/messages`:
```
[user@sahara ~/lecture1/messages]$ `cd` en-us.txt 
bash: cd: en-us.txt: Not a directory
```
Prior to changing the directory, it started off as `/home`. After running `cd` with a path to a file (`en-us.txt`) as an argument, I would recieve an error stating that `en-us.txt` is not a directory. This is because the command `cd` requires a directory as its argument, not a file.

# `ls`:

Starting from `/home/lecture1/messages`:
```
[user@sahara ~/lecture1/messages]$ ls en-us.txt 
en-us.txt
[user@sahara ~/lecture1/messages]$ ls jp-jpn.txt 
jp-jpn.txt
```
Prior to changing the directory, it started off as `/home`. After running ls twice, using different files as its arguments, I would recieve the name of the file I put as the argument. This is because there is no more contents in its path, making the file the final item in the path.

# `cat`:

Starting from `/home/lecture1/messages`:
```
[user@sahara ~/lecture1/messages]$ `cat`jp-jpn.txt 
こんにちは世界！
[user@sahara ~/lecture1/messages]$ `cat`en-us.txt 
Hello World!
```
Prior to changing the directory, it started off as `/home`. After running `cat` twice, using different files as its arguments, I would recieve the contents inside the file that I used as the argument. 




