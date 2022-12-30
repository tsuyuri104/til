https://note.com/tsuyuri104/n/ne64d98b164b0?magazine_key=mdb17e3fc1457

# 1回目
```
function finalValueAfterOperations(operations: string[]): number {
    let x: number = 0;

    operations.forEach((op: string) => {

        if (op === "X++" || op === "++X") {
            x += 1;
        }

        if (op === "X--" || op === "--X") {
            x -= 1;
        }

    });

    return x;
};
```

* 問題文をそのままコード化

# 2回目
```
function finalValueAfterOperations(operations: string[]): number {
    let x: number = 0;

    operations.forEach((op: string) => {

        if (op.includes("++")) {
            x += 1;
        }

        if (op.includes("--")) {
            x -= 1;
        }

    });

    return x;
};
```

* マイベスト。
* 判定条件を変更。Xを含めず記号の部分だけで判定するようにした。
* 10ms早くなった。

# 3回目
```
function finalValueAfterOperations(operations: string[]): number {
    let x: number = 0;

    operations.forEach((op: string) => {

        if (op.includes("++")) {
            x++;
        }

        if (op.includes("--")) {
            x--;
        }

    });

    return x;
};
```

* 加算、減算方法を変更。
* 50ms遅くなった。
