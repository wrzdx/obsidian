---
tags:
  - 1stYear
---
**Code 1:**
```C
#include <stdio.h>

int fact(int n) {
  int i = 1;
  while (n>0) {
    i*=n;
    n--;
  }
  return (n>=0?i:-1);
}

int check(int n) {
  int sum = 0;
  int i=n;
  while (1<=i) {
    sum+=fact(i%10);
    i/=10;
  }
  return sum==n;
}
int main() {
  int l,r;
  scanf("%d%d",&l,&r);
  for (l;l<r;l++) {
    if (check(l)) printf("%d\n",l);
  }
  return 1;
}
```

```C
#include <stdio.h>

int main() {
  const int MAX = 128;
  char str[MAX];
  int freq[MAX];
  int max_freq = 0;

  for (int i=0;i<MAX;i++) freq[i]=0;
  fgets(str,MAX,stdin);
  for (int j = 0; j<MAX;j++) {
    freq[str[j]]++;
    if (((str[j]>=65 && str[j]<91) || (str[j]>=97 && str[j]<123)) && max_freq<freq[str[j]]) {

      max_freq = freq[str[j]];
    }
  }

  for (int j = 65; j < 91; j++) {
    if (freq[j]) printf("%c ",j);
  }

  for (int j = 97; j < 123; j++) {
    if (freq[j]) printf("%c ",j);
  }

  printf("\n");

  for (int i=0;i<max_freq;i++) {
    for (int j = 65; j < 91; j++) {
      if (freq[j]) {
        printf("* ");
        freq[j]--;
      }
    }

    for (int j = 97; j < 123; j++) {
      if (freq[j]) {
        printf("* ");
        freq[j]--;
      }
    }
    printf("\n");
  }
  return 1;
}
```