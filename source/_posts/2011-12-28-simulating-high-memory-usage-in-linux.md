---
layout: post
title:  "Simulating high memory usage in Linux"
date:   2011-12-28 12:01:01
comments: true
categories: discoveries
tags: linux ram
---


Doing some testing recently, I needed a way to eat up as much RAM as possible on a Linux machine. As it turned out, there are not as many ways to do that quickly and easily as one could have desired. I’ve found only two actually. The first one, using [Bash arrays](http://stackoverflow.com/questions/4964799/write-a-bash-shell-script-that-consumes-a-constant-amount-of-ram-for-a-user-defi), is quite slow. The second one, using [C malloc and memset functions](http://stackoverflow.com/questions/1865501/c-program-on-linux-to-exhaust-memory), is quite insecure because you can end up in a completely unresponsive machine (its especially important if the machine is remote). It could be extended though, to support sleeps and the amount of memory to be allocated (also I had some problems with int type overflow if specifying huge amount of RAM), but not being familiar with C, I did not want to dive deep into the problem.

Trying to google a little harder I found another way to do that, similar to the malloc+memset one — C realloc function. Actually I was lucky to find a ready-to-use code on C on unix.com (thank you pludi). The only thing the code lacked was a sleep function to sleep for some time with memory allocated. I added it and here’s what I’ve ended up with.

```c++
//#######################################
// ClearRam
// Holt sich so viel Speicher wie in der Kommandozeile angegeben (wenn möglich)
// Erstellt: 20081218 sky
//#######################################
// Updated: 2011 Andriy Yurchuk
//#######################################
// Compilation:
// $ gcc memalloc.c -o memalloc
// Usage:
// $ ./memalloc 512 15
// will allocate 512 MB of memory and keep it allocated for 15 seconds
//#######################################
 
#include <stdio.h>
#include <stdlib.h>
#include <unistd.h>
#include <signal.h>
 
unsigned char *ptr = NULL;
void sigint_handler(int);
 
int main(int argc, char **argv)
{
    unsigned long meg = 1024 * 1024;
    unsigned long i = 0;
    unsigned int toalloc = 1;
    unsigned int sleeptime = 0;
    unsigned int j = 0;
 
    if (argc == 2) {
        toalloc = atoi(argv[1]);
    }
    else if (argc == 3) {
        toalloc = atoi(argv[1]);
        sleeptime = atoi(argv[2]);
    }
 
    signal(SIGINT, sigint_handler);
 
    for (j = 0; j < toalloc; j++) {
        printf("Trying to allocate %u MB of RAM...", j + 1);
        ptr = (unsigned char *) realloc(ptr, (j + 1) * meg * sizeof(char));
        if (ptr == NULL) {
            printf("failed\n");
            free(ptr);
            return 1;
        }
        ptr[0] = 0;
        for (i = j * meg; i < (j + 1) * meg; i++) {
            ptr[i] = ptr[i - 1] + 1;
        }
        printf("success\r");
    }
    sleep(sleeptime);
    free(ptr);
    printf("\n");
    return 0;
}
 
void sigint_handler(int status)
{
    printf("\nCaught SIGINT\n");
    free(ptr);
    exit(1);
}
```
