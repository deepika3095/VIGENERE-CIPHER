# VIGENERE-CIPHER
## EX. NO: 4
 

## IMPLEMETATION OF VIGENERE CIPHER
 

## AIM:

To implement the Vigenere Cipher substitution technique using C program.

## DESCRIPTION:

To encrypt, a table of alphabets can be used, termed a tabula recta, Vigenère square,or Vigenère table. It consists of the alphabet written out 26 times in differnt rows, each
 
alphabet shifted cyclically to the left compared to the previous alphabet, corresponding to the 26 possible Caesar ciphers. At different points in the encryption process, the cipher uses adifferent alphabet from one of the rows. The alphabet used at each point repeating keyword.depends on a Each row starts with a key letter. The remainder of the row holds the letters A to Z. Although there are 26 key rows shown, you will only use as many keys as there are unique letters in the key string, here just 5 keys, {L, E, M, O, N}. For successive letters of the message, we are going to take successive letters of the key string, and encipher each message letter using its corresponding key row. Choose the next letter of the key, go along that row to find the column heading that	atches the message character; the letter at the intersection of
[key-row, msg-col] is the enciphered letter.


## ALGORITHM:

STEP-1: Arrange the alphabets in row and column of a 26*26 matrix.
STEP-2: Circulate the alphabets in each row to position left such that the first letter is attached to last.
STEP-3: Repeat this process for all 26 rows and construct the final key matrix.
STEP-4: The keyword and the plain text is read from the user.
STEP-5: The characters in the keyword are repeated sequentially so as to match with that of the plain text.
STEP-6: Pick the first letter of the plain text and that of the keyword as the row indices and column indices respectively.
STEP-7: The junction character where these two meet forms the cipher character.
STEP-8: Repeat the above steps to generate the entire cipher text.


## PROGRAM
```
NAME: DEEPIKA R
REG: 212223230038
#include <stdio.h>
#include <string.h>

char keyTable[5][5];

// Function to generate key table
void generateKey(char key[]) {
    int used[26] = {0};
    int i, j, k = 0;

    // replace j with i
    for (i = 0; key[i]; i++)
        if (key[i] == 'j') key[i] = 'i';

    // fill key letters
    for (i = 0; i < strlen(key); i++) {
        if (!used[key[i] - 'a']) {
            used[key[i] - 'a'] = 1;
            keyTable[k / 5][k % 5] = key[i];
            k++;
        }
    }

    // fill remaining letters
    for (i = 0; i < 26; i++) {
        if (i + 'a' == 'j') continue;
        if (!used[i]) {
            keyTable[k / 5][k % 5] = i + 'a';
            k++;
        }
    }
}

// Function to find position of letter
void findPos(char ch, int *row, int *col) {
    if (ch == 'j') ch = 'i';
    for (int i = 0; i < 5; i++)
        for (int j = 0; j < 5; j++)
            if (keyTable[i][j] == ch) {
                *row = i;
                *col = j;
                return;
            }
}

// Encryption function
void encrypt(char text[]) {
    int i, r1, c1, r2, c2;
    for (i = 0; text[i]; i += 2) {
        if (text[i + 1] == '\0') text[i + 1] = 'x'; // pad if odd

        findPos(text[i], &r1, &c1);
        findPos(text[i + 1], &r2, &c2);

        if (r1 == r2) { // same row
            text[i] = keyTable[r1][(c1 + 1) % 5];
            text[i + 1] = keyTable[r2][(c2 + 1) % 5];
        } else if (c1 == c2) { // same column
            text[i] = keyTable[(r1 + 1) % 5][c1];
            text[i + 1] = keyTable[(r2 + 1) % 5][c2];
        } else { // rectangle rule
            text[i] = keyTable[r1][c2];
            text[i + 1] = keyTable[r2][c1];
        }
    }
}

int main() {
    char key[20] = "monarchy";
    char text[30] = "instruments";

    generateKey(key);
    encrypt(text);

    printf("Cipher Text: %s\n", text);
    return 0;
}
```
## OUTPUT
<img width="1695" height="782" alt="image" src="https://github.com/user-attachments/assets/1e11f5fb-63bb-4d6c-a8f0-f6629a1eefae" />

## RESULT
The program is executed successfully.

