# スプレッド演算子

スプレッド演算子の主な目的は、配列またはオブジェクトの要素を_展開_することです。これは例を見るのが最も分かりやすいです。

## 引数への適用\(Apply\)

一般的なユースケースは、配列を使って関数に引数を渡すことです。以前は`Function.prototype.apply`を使う必要がありました：

```typescript
function foo(x, y, z) { }
var args = [0, 1, 2];
foo.apply(null, args);
```

これを行うには、以下に示すように、引数の前に`...`を付けるだけです。

```typescript
function foo(x, y, z) { }
var args = [0, 1, 2];
foo(...args);
```

ここでは、`args`配列を前から順番に引数\(`arguments`\)に展開しています。

## 分割\(Destructuring\)

私達はこれの使い方を既に学習しました:

```typescript
var [x, y, ...remaining] = [1, 2, 3, 4];
console.log(x, y, remaining); // 1,2,[3,4]
```

これを使えば、配列の残りの要素を簡単に取得できます。

## 配列の代入

スプレッド演算子を使用すると、配列の_拡張バージョン_を別の配列に簡単に代入できます。以下の例で示します:

```typescript
var list = [1, 2];
list = [...list, 3, 4];
console.log(list); // [1,2,3,4]
```

展開された配列を任意の位置に配置できます。そして期待通りの結果を得ることができます。

```typescript
var list = [1, 2];
list = [0, ...list, 4];
console.log(list); // [0,1,2,4]
```

## オブジェクトの展開

オブジェクトを別のオブジェクトに展開することもできます。一般的なユースケースは、オリジナルに変更を加えることなくオブジェクトにプロパティを追加することです。

```typescript
const point2D = {x: 1, y: 2};
/** point2Dのプロパティと、`z`のプロパティを持った新しいオブジェクトを作成します */
const point3D = {...point2D, z: 3};
```

オブジェクトの場合、オブジェクトを展開する順序は重要です。これは`Object.assign`のように動作し、期待通りのことを行います：最初に来るものは、後で来るものによって上書きされます：

```typescript
const point2D = {x: 1, y: 2};
const anotherPoint3D = {x: 5, z: 4, ...point2D};
console.log(anotherPoint3D); // {x: 1, y: 2, z: 4}
const yetAnotherPoint3D = {...point2D, x: 5, z: 4}
console.log(yetAnotherPoint3D); // {x: 5, y: 2, z: 4}
```

別の一般的なユースケースは、シンプルな浅い拡張です。

```typescript
const foo = {a: 1, b: 2, c: 0};
const bar = {c: 1, d: 2};
/** `foo`と`bar`を結合します */
const fooBar = {...foo, ...bar};
// `fooBar`はこのようになります: {a: 1, b: 2, c: 1, d: 2}
```

## まとめ

スプレッド演算子は、JavaScriptでよく使われる`apply`の`this`の引数に分かりづらい`null`を渡さなくてもすむようになる優れた構文です。また、配列を分割したり、他の配列に代入したりする構文を使うことにより、簡潔なコードで部分配列に対する処理を行うことができます。

[Pull Request: Support spread operator in call expressions](https://github.com/Microsoft/TypeScript/pull/1931)

