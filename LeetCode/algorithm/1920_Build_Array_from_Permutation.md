https://note.com/tsuyuri104/n/n774f2d15e91a?magazine_key=mdb17e3fc1457

# 1回目
```
function buildArray(nums: number[]): number[] {
   let result: number[] = [];
   for (let i: number = 0; i < nums.length; i++) {
       result[i] = nums[nums[i]];
   }
   return result;
};
```

* 問題文をそのままコードにした。

# 2回目
```
function buildArray(nums: number[]): number[] {
    let result: number[] = [];
    for (let i: number = 0; i < nums.length; i++) {
        result.push(nums[nums[i]]);
    }
    return result;
};
```

* 配列に要素を追加する処理を修正。
* 速度は20ms遅くなった。
