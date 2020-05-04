# Class 10 - TP Assignment

## Group 14

### Question P1.1.1

  In the case that the values of the are too small or too big, this can cause them to fall outside of the range of the data type, which may lead to undefined
behavior and security breaches. Being x and y of type size_t (which is an unsigned int) and being this value used to define the memory to allocate, if the value
passed is too big (considering that x and y do not undergo any type of security check) this may lead to an integer overflow. This causes less memory to be allocated than
what was supposed to, which may allow to write in memory not allocated for that purpose.


### Question P1.1.2

```C
int main() {
    char* matriz;
    vulneravel(matriz, 1111111111111, 1111111111111, 0);

}

```

### Question P1.1.3

  There will be a Segmentation Fault, saying that malloc() can't allocate the intended region.


### Question P1.2.1

  The vulnerability presented here is that of Integer Underflow, which means that there is the danger of the value being lower than it is allowed to.
The obvious example here is that of the taken value being zero (of variable tamanho), which will lead tamanho_real to have a negative value. This is a problem
because size_t can not represent negative values, leading to integer underflow.

### Question P1.2.2

To demonstrate said vulnerability it's only necessary to pass the size argument with value zero.

```C
int main(){
    char* boom = “something something\n”;
    vulneravel(boom,0);  
}
```


### Question P1.2.3

  The error that occurs is, yet again, Segmentation Fault.


### Question P1.2.4

  The changes made prevent integer overflows/underflows and any consequent Segmentation Fault.

```C
#include <stdio.h>

#include <stdlib.h>

#include <string.h>



const int MAX_SIZE = 2048;

const int MIN_SIZE = 0;



void vulneravel (char *origem, size_t tamanho) {

    size_t tamanho_real;

    char * destino;


    if (tamanho < MAX_SIZE && tamanho > MIN_SIZE) {
        tamanho_real = tamanho - 1; // Não copiar \0 de origem para destino
        destino = (char*) malloc(tamanho_real);
        memcpy(destino, origem, tamanho_real);

      }



}



int main() {

    vulneravel("something qer", 0);

}
```
