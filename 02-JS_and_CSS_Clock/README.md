## JS and CSS Clock
練習時鐘效果

## 步驟
1. 設定時鐘樣式，CSS 指針角度的動畫，使用 transform: rotate(0deg); 來達成。
2. 設定 function setDate() 的函式，取得時間
3. 利用取得的時間計算指針角度。
4. 使用 setInterval() 更新 CSS 動畫。

## JS
使用到 `new setDate()` 取得當前時間。再利用`getSeconds()`、`getMinutes()`、`getHours()`取得秒、分、時。
```js
const now = new Date();
const second = now.getSeconds();
```
計算指針角度
```js
const secondsDegrees = (second / 60) * 360 + 90;
```
使用 `setInterval(callback, time)` 設定執行間格。

## CSS
* `transform: rotate(0deg)` 角度設定。 
* `transform-origin: 100%` 設定物件中心點。
* `transition: property time;` 漸變物件屬性和時間。
* `transition-timing-function` 貝茲曲線計算動畫轉場效果。
[連結](https://developer.mozilla.org/en-US/docs/Web/CSS/transition)

```css
.hand {
      width: 50%;
      height: 6px;
      background: black;
      position: absolute;
      top: 50%;
      transform: rotate(90deg); /* 歸0 */
      transform-origin: 100%;
      transition: all .05s;
      transition-timing-function: cubic-bezier(0.1, 2.7, 0.58, 1);
    }
```

時鐘設定
```css
.clock {
      width: 30rem;
      height: 30rem;
      border: 20px solid white; /* 白框 */
      border-radius: 50%; /* 圓形時鐘 */
      margin: 50px auto; 
      position: relative; /* 設定子層指定為 relative */
      padding: 2rem;
    }
```

## 影片結尾
作者提到在原本在歸零的時候，會有點奇怪的樣式，是因為在設定上我們是從 transition: rotate(90deg); 做轉場設定。當角度大變成到小的時候，會被認為是往前的效果。

在另一個[教學影片](https://www.youtube.com/watch?v=Ki0XXrlKlHY)中，發現只要從另外一個角度去設定指針 CSS 設定即使不做另外的處理也不會有這個案例的問題發生。

```css
.hand {
      height: 50%;
      width: 6px;
      background: black;
      position: absolute;
      left: 50%;
      transform-origin: bottom;
    }
```
```js
 function setDate() {
      const now = new Date();

      const second = now.getSeconds();
      const secondsDegrees = (second / 60) * 360;
      secondHand.style.transform = `rotate(${secondsDegrees}deg)`

      const mins = now.getMinutes();
      const minsDegrees = ((mins / 60) * 360) + ((second / 60) * 6);
      minHand.style.transform = `rotate(${minsDegrees}deg)`

      const hour = now.getHours();
      const hourDegrees = (hour / 12) * 360 + ((mins / 60) * 30);
      hourHand.style.transform = `rotate(${hourDegrees}deg)`
    }
```