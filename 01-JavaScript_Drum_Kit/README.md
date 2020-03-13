## Drum kit
藉由敲擊特定字母產生特定聲音。

## 解決目標
* 設置監聽事件，監聽特定字母 keydown 事件。
* 當鍵盤特定字母被點擊時，播放相對應的音效。
* 音效撥放時，須設定 audio.currentTime 為 0，使音效可以快速重複撥放。
* 當鍵盤特定字母被點擊時，產生 CSS 動畫相對應變化。
* 點擊結束後，移除動畫。

## JS
`addEventListener` 監聽 `keydown` 事件，取得 keyCode 值對對應到 data-key，使 div 和 audio 產生相對應事件。

```js
function playSound(e) {
  const audio = document.querySelector(`audio[data-key]="${e.keyCode}"`);
  const key = document.querySelector(`.key[data-key]="${e.keyCode}"`);
  if (!audio) return;
  key.classList.add('playing'); //增加 CSS
  audio.currentTime = 0; //音效時間重置
  audio.play(); //播放音效
}

window.addEventListener('keydown', playSound); //監聽keydown事件
```

設置監聽已經變化的效果，並移除效果。
```js
function removeTransition(e) {
  if (e.propertyName !== 'transform') return;
  e.target.classList.remove('playing');
  // or this.classList.remove('playing');
}

const keys = document.querySelectorAll('.key');
keys.forEach(key => key.addEventListner('transitionend'), removeTransition) // 監聽每個變化的.key
```
## CSS

flex 置中效果
```css
.keys {
  display: flex;
  flex: 1;
  align-items: center;  /* 垂直置中 */
  justify-content: center;  /* 水平置中 */
}
```

transition 轉場效果
* transition-property
* transition-duration
* transition-timing-function
* transition-delay
```css
 .key {
   transition: all .07s ease;
 }
```
設置 pseudo css
```css
 .playing {
   transform: scale(1.1); //改變大小
 }
```
可以參考: [MDN](https://developer.mozilla.org/en-US/docs/Web/CSS/transform)
