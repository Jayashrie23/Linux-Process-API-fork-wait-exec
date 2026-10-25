# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls

```
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <sys/wait.h>

int main() {
    int pid = fork();

    if (pid == 0) {
        printf("I am child, my PID is %d\n", getpid());
        printf("My parent PID is: %d\n", getppid());
        sleep(2);
    } else {
        printf("I am parent, my PID is %d\n", getpid());
        wait(NULL);
    }

    return 0;
}
```
##OUTPUT
<img width="981" height="312" alt="Screenshot 2026-10-25 113552" src="https://github.com/user-attachments/assets/143b46ae-dfb3-4675-8083-aed9f0a6b57d" />



## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family

```
#include <stdio.h>
#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;

    printf("Running ps with execl\n");
    fflush(stdout);

    if (fork() == 0) {
        execl("ps", "ps", "-f", (char *)NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);

    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }

    printf("Running ps with execlp (without full path)\n");
    fflush(stdout);

    if (fork() == 0) {
        execlp("ps", "ps", "-f", (char *)NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);

    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }

    printf("Done.\n");
    return 0;
}
```
##OUTPUT

<img width="880" height="305" alt="Screenshot 2026-10-25 122724" src="https://github.com/user-attachments/assets/f40c3ca6-fd5e-4e4e-b259-0008622363f0" />


# RESULT:
The programs are executed successfully.
