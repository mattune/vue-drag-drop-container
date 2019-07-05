# vue-drag-drop-container

ファイル参照をドラッグ＆ドロップできるようにするコンポーネント。

[DEMO](https://mattune.github.io/vue-drag-drop-container/)

## 導入方法
1. /src/components/DragDrop.vue を任意の場所に追加。

## 使用方法
```html
<DragDrop/>
```

### オプション
```html
<DragDrop multiple="multiple"/>
```
→複数ファイルの場合はmultipleを追加。

```html
<DragDrop required/>
```
→requiredは自由に選択可能。

```html
<DragDrop name="uploadfile" multiple="multiple" @checkResult="getResult"/>
```
→@checkResultは親コンポーネントのメソッドを指定可能。空でも可。
