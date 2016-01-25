# GO-BBB
Code snippets for Beaglebone Black using GO language

# Compiling GO projects for Beaglebone Black

Finding the make.bash tool in Ubuntu:
```
user@computer:~$ cd /usr/local/go/src/
all.bash          clean.bash  debug     html      log            net        run.bat    syscall
all.bat           clean.bat   encoding  image     make.bash      os         run.rc     testing
all.rc            clean.rc    errors    index     make.bat       path       runtime    text
androidtest.bash  cmd         expvar    internal  Make.dist      race.bash  sort       time
archive           compress    flag      io        make.rc        race.bat   strconv    unicode
bufio             container   fmt       lib9      math           reflect    strings    unsafe
builtin           crypto      go        libbio    mime           regexp     sudo.bash
bytes             database    hash      liblink   nacltest.bash  run.bash   sync
user@computer:/usr/local/go/src$
```
Preparing the environment to cross-compile GO applications for ARM:
```
user@computer:/usr/local/go/src$ sudo GOOS=linux GOARCH=arm ./make.bash --no-clean
# Building C bootstrap tool.
cmd/dist

# Building compilers and Go bootstrap tool for host, linux/am64
.
.
.
Installed Go for linux/amd64 in /usr/local/go
Installed commands in /usr/local/go/bin
user@computer:/usr/local/go/src$
```
Creating an application example hello world:
```
user@computer:~$ mkdir go-examples && cd go-examples
user@computer:~/go-examples$ cat > hello-world.go << EOF
> package main
>
> import "fmt"
>
> func main() {
>     fmt.Println("Hello", "World!")
> }
> EOF
user@computer:~/go-examples$
```
Compiling the hello-world.go application:
```
user@computer:~/go-examples$ ls
hello-world.go
user@computer:~/go-examples$ GOOS=linux GOARCH=arm GOARM=7 go build hello-world.go
user@computer:~/go-examples$
user@computer:~/go-examples$ ls
hello-world hello-world.go
user@computer:~/go-examples$
```
Checking whether the application was compiled for ARM:
```
user@computer:~/go-examples$ file hello-world
hello-world: ELF 32-bit LSB executable, ARM, version 1 (SYSV), statically linked, not stripped
user@computer:~/go-examples$
```
Copying the compiled application to Beaglebone Black:
```
user@computer:~/go-examples$ scp hello-world root@ip-address:/home/root/
root@ip's password:
.
.
.
user@computer:~/go-examples$
```
Connecting in the Beaglebone Black via SSH:
```
user@computer:~/go-examples$ ssh root@ip-address:
root@ip-address's password:
rooot@beaglebone:# chmod +x hello-world
rooot@beaglebone:# ./hello-world
Hello World!
rooot@beaglebone:# 
```
