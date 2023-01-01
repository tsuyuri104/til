https://note.com/tsuyuri104/n/nb634a2ef1392?magazine_key=mdb17e3fc1457

# 1回目
```
function twoSum(nums: number[], target: number): number[] {

    let ret: number[] = [];


    nums.forEach((x: number, i: number) => {

        nums.forEach((y: number, j: number) => {

            if (j === i) {
                return;
            }

            if (x + y !== target) {
                return;
            }

            if (!ret.includes(i)) {
                ret.push(i);
            }

            if (!ret.includes(j)) {
                ret.push(j);
            }
        });

    });


    return ret;
};
```

* ループ処理が入れ子で、配列の配列の要素数の2乗行っているため、処理回数に無駄がある。

# 2回目
```
function twoSum(nums: number[], target: number): number[] {

    let ret: number[] = [];
    let isFinded: boolean = false;

    nums.forEach((x: number, i: number) => {

        if (isFinded) {
            return false;
        }

        nums.forEach((y: number, j: number) => {

            if (j === i) {
                return true;
            }

            if (x + y !== target) {
                return true;
            }

            ret.push(i);
            ret.push(j);
            isFinded = true;

            return false;
        });
    });

    return ret;
};
```

* ループ回数は変わらないが、外側のループで、ペア見つけた場合は処理しない判定を追加した。ループ実行回数は変わらないため、改善はなし。

# 3回目
```
function twoSum(nums: number[], target: number): number[] {

    let ret: number[] = [];
    let isFounded: boolean = false;

    nums.forEach((x: number, i: number) => {

        if (isFounded) {
            return false;
        }

        for (let j: number = i + 1; j < nums.length; j++) {
            if (x + nums[j] === target) {
                ret.push(i);
                ret.push(j);
                isFounded = true;
                return false;
            }
        }
    });


    return ret;
};
```

* マイベスト
* ヒント動画見た結果。検証済みのペアを再検証しないことで、実行回数が減り、速度が速くなった。

# 4回目
```
function twoSum(nums: number[], target: number): number[] {

    let ret: number[] = [];
    nums.forEach((x: number, i: number) => {
        const k: number = nums.findIndex((y, j) => y === target - x && j >= i + 1);
        if (k > -1) {
            ret.push(i, k);
            return false;
        }
    });


    return ret;
};
```

* 発見フラグを使用したくない、繰り返し処理を入れ子にしたくないので、再挑戦。
* 繰り返し処理の代わりにfindIndexを使用したけど、対して速くならなかった。
