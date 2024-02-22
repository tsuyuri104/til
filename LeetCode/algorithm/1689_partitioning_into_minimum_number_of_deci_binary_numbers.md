# 1st
```
function minPartitions(n: string): number {
    let max: number = 0;

    for(let s of n){
        if(max < Number(s)){
            max = Number(s)
        }
    }

    return max;
};
```

- 最大の1桁の数値を返すってことに気づいたらすぐできた。
- Runtime 61ms

# 2nd
```
function minPartitions(n: string): number {
    let max: number = 0;

    for(let s of n){
        max = max < Number(s) ? Number(s) : max
    }

    return max;
};
```

- 三項演算子にしてみた。毎回代入することになったので速度が落ちた。
- Runtime 79ms

# 3rd
```
function minPartitions(n: string): number {
    let max: number = 0;

    for(let s of n){
        if(max < Number(s)){
            max = Number(s)
        }

        if(max === 9){
            break;
        }
    }

    return max;
};
```

- `max`が整数1桁最大値の9になったらループ抜けるようにしたら速度が遅くなった。
- Runtime 80ms

# 他人の回答をみて

- Math.max()使えばいいのか
