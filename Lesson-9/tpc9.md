# Class 9 - TP Assignment

## Group 14

### Question P1.1

  When running the said programs written in different languages, and passing more numbers than the space the program allocated, we get different behaviors from each
the programs:

- Python program: Throws exception "IndexError: list assignment index out of range".

- Java program: Throws exception "Exception in thread "main"java.lang.ArrayIndexOutOfBoundsException".

- C++ program: Program ends with Segmentation Fault.



### Question P1.2

- RootExploit.c

  This program is vulnerable to a buffer overflow attack due to the fact that the function "gets" does not check the input size, which allows
input longer than the specified size to be passed. As the array "buff" has size 4, inserting anything longer than that will result in said
buffer overflow (image included in the same directory as this report), allowing to gain root/admin permissions.


- 0-simple.c

  This program has the same vulnerability of the previous analyzed program. However, due to the stack organization, input just 1 unit longer than the size (64) of
the array where the input is being saved is not enough this time. To exploit this vulnerability we pass an input quite longer than 64 and we get the message "YOU WIN!!!"
(image also in the same directory as this report).


### Question P1.3

  The vulnerability found in this program refers to the fact that it does not limit the amount of bytes the user can read information out of where he should be allowed to.
This means that the user can read information out of the stack because the only limitation is the number of characters he passes as input. In the image shown (in the same directory as
the report) we tested with a high value (200) and we can see that it reads much more than the phrase given as input.


### Question P1.4

Since the virtual machine uses UNIX operating system and UNIX is a little-endian system, where the least significant byte is placed at the lowest memory address.
We used a debugger so that we get to know exactly at which byte the variable control will change its value, so to obtain the desired value of 0x61626364 which is abcd
in ASCII and get the congratulations message, it is necessary to write any string of the discovered number bytes and then concatenate it with dcba so we can let the most
significant byte to be stored in the last memory position. (image in repository)

### Question P1.5

```C
#include <stdio.h>
#include <string.h>
#include <stdlib.h>

int main(int argc, char **argv) {
    char *dummy = (char *) malloc (sizeof(char) * 10);
    char *readonly = (char *) malloc (sizeof(char) * 10);

    strcpy(readonly, "laranjas");
	// If the string is larger than the buffer size, we truncate the string
 	// with the size of the buffer. We do this by placing the character that
	// represents the end of a string in position that has the same size of
 	// the buffer in the string

	if(sizeof(argv[1]) > 10 ) {
      argv[10] = '\0'
    }

    strcpy(dummy, argv[1]);
  printf("%s\n", readonly);

}
```


### Question P1.6

```C
/* stack.c */
/* This program has a buffer overflow vulnerability. */
/* Our task is to exploit this vulnerability */
#include <stdlib.h>
#include <stdio.h>
#include <string.h>
int bof(char *str)
{
	char buffer[24];
	/* The following statement has a buffer overflow problem */

	// If the string is larger than the buffer size, we truncate the string
 	// with the size of the buffer. We do this by placing the character that
	// represents the end of a string in position that has the same size of
 	// the buffer in the string

	if(sizeof(str) > 24 ) {
      str[24] = '\0'
    }

	strcpy(buffer, str);
	return 1;
}
```
