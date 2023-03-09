* mountが実行されるのは、該当コンポーネントの描写時。
    ```a-component.blade.php
    <livewire:b-component></b-component>
    @if ($flag)
        <livewire:c-component></c-component>
    @endif
    ```
    Bコンポーネントの描写は、Aコンポートを描写するときと同じタイミングのため、mountマウントのタイミングも同じ。
    Cコンポーネントの描写は、$flagの値がtrueのときとなる。
    そのため、BコンポーネントとCコンポーネントのmountのタイミングが異なる可能性がある。
* ComponentのプロパティにEloquent型を設定するとrenderの度にEloquentの値が最新のデータに変わる。そのため、楽観的排他制御のためのタイムスタンプを保持するには不向き。
