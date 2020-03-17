## Array Cardio Day 1
熟悉 filter() map() reduce() sort() split() includes()


## 問題

1. Filter the list of inventors for those who were born in the 1500's
2. Give us an array of the inventors first and last names
3. Sort the inventors by birthdate, oldest to youngest
4. How many years did all the inventors live all together?
5. Sort the inventors by years lived
6. create a list of Boulevards in Paris that contain 'de' anywhere in the name
7. Sort the people alphabetically by last name
8. Sum up the instances of each of these

## JS
1. filter()
將傳入的 array 按照條件做篩選，返回結果回 true 的值。
[Array.prototype.filter()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/filter)

2. map()
產生一個 new array 並把結果返還，會訪問每個元素，可以將元素組合成需要的條件後返還。
[Array.prototype.map()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

3. sort(function (a, b) {})
in-place 的排序方式，可以節省內存空間，但是為不穩定排序(需要特別注意)，所以最好在裡面加上條件來使用。
```js
const hello = Array.property.sort((a, b) => {
  if (a > b) {  // a 大於 b 返回 true， a 放在 b 後面
    return 1
  }
  if (a < b) { // a 小於 b 返回 false， a 放在 b 前面
    return -1
  }
  return 0 //比對相等
})
console.log(hello) //預設的樣子升序排列
```
[Array.prototype.sort()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort)

4. reduce()
第一個參數是累加，第二個參數是下一個，第三個參數表示 index, 四為整個 array, 會後可以設定一個預設 value。
```js
arr.reduce(callback( accumulator, currentValue[, index[, array]] )[, initialValue])
// 計算 invnetors 的總年齡
// 加總 recdue
// 算出 inventor 的年齡
// 累加器和當前的數字相加。
```
```js
let totalYear = 0
for (let i = 0; i < inventors.length; i++) {
  totalYear += inventors.passed - inventors.year
}
```
[Array.prototype.reduce()](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)

5. 第五題和第三題相同，多了年齡加總。

也可以做個 map 加總年紀，確認再使用了 sort() 是否有錯誤
```js
const age = inventors.map(inventor => {
      const age = inventor.passed - inventor.year
      inventor.age = age
      return inventor
    })
    const oldest = age.sort((a, b) => {
      const last = a.passed - a.year
      const next = b.passed - b.year
      return last > next ? -1 : 1
    })
    console.log(oldest)
```
6. Array.from() map() filter() includes()

* Array.from() 返還一個 new，做淺拷貝 array-like 或物件。
* includes() 比對字串時，返還 ture/false ，含有的內容會顯示 ture。
* filter() + includes() 可以做文字篩選。

7. sort() split()
需要將字串 split 開來，所以使用 split(', ') 作為關鍵字，拆開後再比對。

8. reduce()
做 array element 的統計。
```js
const data = ['car', 'car', 'truck', 'truck', 'bike', 'walk', 'car', 'van', 'bike', 'walk', 'car', 'van', 'car', 'truck'];
    const transpotation = data.reduce((a, b) => {
      if (!a[b]) {
        a[b] = 0
      }
      a[b]++
      return a
    }, {})
    console.log(transpotation)
```
最近有遇到一個類似的問題，請你實踐一個可以統計字串中字母個數或統計最多字母數的涵式。
```js
  var str = "aaaabbbccccddfgh";
  const array = str.split('') //轉成 array 或者 str.match(/[a-zA-z]/g, '')
  const counter = array.reduce((a, b) => {
    if (!a[b]) {
      a[b] = 0
    }
    a[b]++
    return a
  }, {})
  console.log(counter)
```
另外這題可以參考 [這裡](https://github.com/guahsu/JavaScript30/tree/master/04_Array-Cardio-Day-1)
```js
const strCnt = people.reduce(function (obj, item) {
  const itemStr = item.match(/[a-zA-Z]/g, '');
  itemStr.forEach(str => {
    if (!obj[str]) {
      obj[str] = 0;
    }
      obj[str]++
  })
  return obj;
}, {});
console.log(strCnt);
```
