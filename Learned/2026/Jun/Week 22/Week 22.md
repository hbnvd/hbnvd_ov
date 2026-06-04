Su: 24/5/2026
Sa: 30/5/2026


# 30/05/2026
- [[Prefix Sum & Different Array]] - done, thêm link với sliding wd
- [[Sliding window]] - hiện chưa có gì;))
- Cày bài ư, should be tomorrrowwww
## bộ sinh test
```python
import sys
from random import randint

sys.stdout = open("testc1.INP", 'w')
ch = ["A", "B", "C", "D"]
for i in range(0, 10**3):
    print(ch[randint(0, 3)], end = "")


```
## Thuật toán nén ABCD 1 ~ 692b
```c
#include <stdio.h>

void fileIO() {
    #ifdef LOCAL_DEBUG
        freopen("testc1.INP", "r", stdin);
        freopen("testc1.OUT", "w", stdout);
    #endif
}

int getBit(int i, int j) {
    return (i>>j)&1;
}
int onBit(int i, int j) {
    return (i|(1<<j));
}
int offBit(int i, int j) {
    return (i&(~(1<<j)));
}
int flipBit(int i, int j) {
    return (i^(1<<j));
}

int aLen = 0, sLen = 0;
char s[100005];
int a[100005];
int main() {
    fileIO();
    
    scanf("%s\n", &s);
    // write
    int j, k;
    for (int i = 0; s[i] != '\0'; ++i) {
        ++sLen;
        
        j = i/16;
        k = (i%16)*2;
        
        if (s[i] == 'A') {
            a[j] = offBit(offBit(a[j], k), k+1);

        } else if (s[i] == 'B') {
            a[j] = offBit(onBit(a[j], k), k+1);

        } else if (s[i] == 'C') {
            a[j] = onBit(offBit(a[j], k), k+1);

        } else if (s[i] == 'D') {
            a[j] = onBit(onBit(a[j], k), k+1);
        }
    }
    aLen = (sLen/16)+1;
    if (sLen%16 == 0) --aLen;

    printf("%d\n", sLen);
    for (int i = 0; i < aLen; ++i) {
        printf("%d ", a[i]);
        // for (int j = 32-1; j >= 0; --j) {
        //     printf("%d", getBit(a[i], j));
        // }
        // printf("\n");
    }
    return 0;
}
```

## Nén ABCD 2.0 ~ 550b
- Idea 1 cải  tiến = cách chuyển từ int sang long long, bin sang hex
```c
#include <stdio.h>

void fileIO() {
    #ifdef LOCAL_DEBUG
        freopen("testc1.INP", "r", stdin);
        freopen("testc1.OUT", "w", stdout);
    #endif
}
#define ll long long

ll getBit(ll i, int j) {
    return (i>>j)&1LL;
}
ll onBit(ll i, int j) {
    return (i|(1LL<<j));
}
ll offBit(ll i, int j) {
    return (i&(~(1LL<<j)));
}
ll flipBit(ll i, int j) {
    return (i^(1LL<<j));
}

int aLen = 0, sLen = 0;
char s[100005];
ll a[100005];
int main() {
    fileIO();
    
    scanf("%s\n", &s);
    // write
    ll j, k;
    for (int i = 0; s[i] != '\0'; ++i) {
        ++sLen;
        
        j = i/32;
        k = (i%32)*2;
        
        if (s[i] == 'A') {
            a[j] = offBit(offBit(a[j], k), k+1);

        } else if (s[i] == 'B') {
            a[j] = offBit(onBit(a[j], k), k+1);

        } else if (s[i] == 'C') {
            a[j] = onBit(offBit(a[j], k), k+1);

        } else if (s[i] == 'D') {
            a[j] = onBit(onBit(a[j], k), k+1);
        }
    }
    aLen = (sLen/32)+1;
    if (sLen%32 == 0) --aLen;

    printf("%d\n", sLen);
    for (int i = 0; i < aLen; ++i) {
        printf("%016llX ", a[i]);
        // for (int j = 32-1; j >= 0; --j) {
        //     printf("%d", getBit(a[i], j));
        // }
        // printf("\n");
    }


    return 0;
}
```
## Nén ABCD 3.0 - ascii base 85 ~ 326b
```c

#include <stdio.h>

void fileIO() {
    #ifdef LOCAL_DEBUG
        freopen("testc1.INP", "r", stdin);
        freopen("testc1.OUT", "w", stdout);
    #endif
}
#define ll long long

ll getBit(ll i, int j) {
    return (i>>j)&1LL;
}
ll onBit(ll i, int j) {
    return (i|(1LL<<j));
}
ll offBit(ll i, int j) {
    return (i&(~(1LL<<j)));
}
ll flipBit(ll i, int j) {
    return (i^(1LL<<j));
}

const char BASE85_CHARS[] = 
    "0123456789ABCDEFGHIJKLMNOPQRSTUVWXYZabcdefghijklmnopqrstuvwxyz!#$%&()*+-;<=>?@^_`{|}~";

void print32BitAsBase85(unsigned int value) {
    char out[5];
    for (int i = 4; i >= 0; --i) {
        out[i] = BASE85_CHARS[value % 85];
        value /= 85;
    }
    for (int i = 0; i < 5; ++i) {
        putchar(out[i]);
    }
}

int aLen = 0, sLen = 0;
char s[1000005];
ll a[1000005];

int main() {
    fileIO();
    
    scanf("%s", s); 
    
    ll j, k;
    for (int i = 0; s[i] != '\0'; ++i) {
        ++sLen;
        
        j = i/32;
        k = (i%32)*2;
        
        if (s[i] == 'A') {
            a[j] = offBit(offBit(a[j], k), k+1);
        } else if (s[i] == 'B') {
            a[j] = offBit(onBit(a[j], k), k+1);
        } else if (s[i] == 'C') {
            a[j] = onBit(offBit(a[j], k), k+1);
        } else if (s[i] == 'D') {
            a[j] = onBit(onBit(a[j], k), k+1);
        }
    }
    aLen = (sLen/32)+1;
    if (sLen%32 == 0) --aLen;

    printf("%d\n", sLen);
    
    for (int i = 0; i < aLen; ++i) {
        unsigned int low_32 = (unsigned int)(a[i] & 0xFFFFFFFFFFFFFFLL);
        unsigned int high_32 = (unsigned int)(a[i] >> 32);
        
        print32BitAsBase85(low_32);
        print32BitAsBase85(high_32);
        
    }

    return 0;
}

```
