# 1st

```
function findThePrefixCommonArray(A: number[], B: number[]): number[] {
  const C: number[] = [];
  const maxLength = A.length;

  for (let i = 0; i < maxLength; i++) {
    const aChar = A[i];
    const bChar = B[i];

    const aHadSeen = A.slice(0, i + 1);
    const bHadSeen = B.slice(0, i + 1);

    const aHasB = bHadSeen.includes(aChar);
    const bHasA = aHadSeen.includes(bChar);

    let ret = 0;
    if (aHasB) {
      ret += 1;
    }
    if (bHasA) {
      ret += 1;
    }
    if (aChar === bChar) {
      ret += 1;
    }

    ret += C[i] ?? 0;
    C.push(ret);
  }

  return C;
}
```

- コードで表現するのが難しかった
- Runtime 108ms

# 2nd

```
function findThePrefixCommonArray(A: number[], B: number[]): number[] {
    const C: number[] = [];
    const maxLength = A.length;

    for (let i = 0; i < maxLength; i++) {
        const aChar = A[i];
        const bChar = B[i];

        let ret = C[i - 1] ?? 0;
        if (B.slice(0, i).includes(aChar)) {
            ret += 1;
        }
        if (A.slice(0, i).includes(bChar)) {
            ret += 1;
        }
        if (aChar === bChar) {
            ret += 1;
        }

        C.push(ret);
    }

    return C;
}
```

- マイベスト
- 使用する変数の数を削減したけど速度に変化ほぼなし
- Runtime 100ms

# 3rd

```
function findThePrefixCommonArray(A: number[], B: number[]): number[] {
    const C: number[] = [];
    const maxLength = A.length;
    const aHasSeen: number[] = [];
    const bHasSeen: number[] = [];

    for (let i = 0; i < maxLength; i++) {
        const aChar = A[i];
        const bChar = B[i];

        let ret = C[i - 1] ?? 0;

        if (bHasSeen.includes(aChar)) {
            ret += 1;
        }
        if (aHasSeen.includes(bChar)) {
            ret += 1;
        }
        if (aChar === bChar) {
            ret += 1;
        }

        C.push(ret);

        aHasSeen.push(aChar);
        bHasSeen.push(bChar);
    }

    return C;
}
```

- `slice`処理を減らしてみたら遅くなった。

# 4th

```
function findThePrefixCommonArray(A: number[], B: number[]): number[] {
    const C: number[] = [];
    const maxLength = A.length;

    for (let i = 0; i < maxLength; i++) {
        const aChar = A[i];
        const bChar = B[i];

        let ret = (C[i - 1] ?? 0)
            + (B.slice(0, i).includes(aChar) ? 1 : 0)
            + (A.slice(0, i).includes(bChar) ? 1 : 0)
            + (aChar === bChar ? 1 : 0);

        C.push(ret);
    }

    return C;
}
```

- 計算をまとめてみた。
- 考え方変えた方がよさそう。
