# C program to compare two files.

## Write a C program to read contents of two files and compare them character by character. How to compare two files character by character and line by line in C programming. Logic to compare two files line by line and print difference line and column number in C program.

### Example
```
File 1

Learn C programming at Codeforwin.
Working with files and directories.

File 2

Learn C programming at Codeforwin.
Working with array and pointers.
```
### Output
```
File are not equal. 
Line: 2, column: 14
```

Step by step descriptive logic to compare two files character by character.
Input file path of two files to compare from user, store it in path1 and path2.
Open both files in r (read) mode and store their references in fPtr1 and fPtr2.
Define a function int compareFile(FILE * fPtr1, FILE * fPtr2, int * line, int * col). The function will return 0 if both files are same, otherwise returns -1. Perform all below steps inside function.
Set *line = 1 and *col = 0.
Read a character from both files and compare.
Increment *line by one and set *col = 0 if current character is new line character '\n'. If both characters are different then return -1. Otherwise, increment *col by one if both characters are same.
Repeat step 5-6 until characters from both files are matching, or file has reached end.
If both files has reached end then return 0 otherwise return -1.
### Program to compare two files

```
/**
 * C program to compare two files character by character.
 */

#include <stdio.h>
#include <stdlib.h>

/* Function declaration */
int compareFile(FILE * fPtr1, FILE * fPtr2, int * line, int * col);


int main()
{
    /* File pointer to hold reference of input file */
    FILE * fPtr1; 
    FILE * fPtr2;
    char path1[100];
    char path2[100];

    int diff;
    int line, col;


    /* Input path of files to compare */
    printf("Enter path of first file: ");
    scanf("%s", path1);
    printf("Enter path of second file: ");
    scanf("%s", path2);


    /*  Open all files to compare */
    fPtr1 = fopen(path1, "r");
    fPtr2 = fopen(path2, "r");

    /* fopen() return NULL if unable to open file in given mode. */
    if (fPtr1 == NULL || fPtr2 == NULL)
    {
        /* Unable to open file hence exit */
        printf("\nUnable to open file.\n");
        printf("Please check whether file exists and you have read privilege.\n");
        exit(EXIT_FAILURE);
    }


    /* Call function to compare file */
    diff = compareFile(fPtr1, fPtr2, &line, &col);

    if (diff == 0)
    {
        printf("\nBoth files are equal.");
    }
    else 
    {
        printf("\nFiles are not equal.\n");
        printf("Line: %d, col: %d\n", line, col);
    }


    /* Finally close files to release resources */
    fclose(fPtr1);
    fclose(fPtr2);

    return 0;
}


/**
 * Function to compare two files.
 * Returns 0 if both files are equivalent, otherwise returns
 * -1 and sets line and col where both file differ.
 */
int compareFile(FILE * fPtr1, FILE * fPtr2, int * line, int * col)
{
    char ch1, ch2;

    *line = 1;
    *col  = 0;

    do
    {
        // Input character from both files
        ch1 = fgetc(fPtr1);
        ch2 = fgetc(fPtr2);
        
        // Increment line 
        if (ch1 == '\n')
        {
            *line += 1;
            *col = 0;
        }

        // If characters are not same then return -1
        if (ch1 != ch2)
            return -1;

        *col  += 1;

    } while (ch1 != EOF && ch2 != EOF);


    /* If both files have reached end */
    if (ch1 == EOF && ch2 == EOF)
        return 0;
    else
        return -1;
}
```
File contents of data\compare1.txt
Learn C programming at Codeforwin.
Working with files and directories.
File contents of data\compare2.txt
