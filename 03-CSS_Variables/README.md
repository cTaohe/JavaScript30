## CSS Varibales
用 JS 和 CSS 實現拖動滑軸時，改變邊框、模糊和顏色。

## 步驟
1. 利用 CSS variable `:root` 定義變數。
2. JS 使用 `addEventListener` 監聽事件，來更新 CSS 變數。

## JS
* dataset 來取得 HTML 上的自定義元素的屬性。
* 使用 forEach 遍歷每個 input
* 使用 `setProperty` 來改變 CSS style。 [連結](https://developer.mozilla.org/en-US/docs/Web/API/CSSStyleDeclaration/setProperty)
```html
<input id="spacing" type="range" name="spacing" min="10" max="200" value="10" data-sizing="px">
```
```JS
function handleUpdate() {
  const suffix = this.dataset.sizing || ''; //px
  document.documentElement.style.setProperty(`--${this.name}`, this.value + suffix);
}

inputs.forEach(input => input.addEventListener('change', handleUpdate));
```
style.setProperty()
等同於style.cssPropertyName
```js
style.setProperty('padding', '15px');
/* 等同於 */
style.padding = '15px';
```
## CSS
[:root](https://developer.mozilla.org/en-US/docs/Web/CSS/:root)

[Custom properties](https://developer.mozilla.org/en-US/docs/Web/CSS/Using_CSS_custom_properties)自定義變數使用:`color: var(--main-color);`

[filter: blur](https://developer.mozilla.org/en-US/docs/Web/CSS/filter):高斯模糊，還可以改變色相跟灰階等等功能。

```CSS
:root {
      --base: #ffc600;
      --spacing: 10px;
      --blur: 10px;
    }
img {
      padding: var(--spacing);
      background: var(--base);
      filter: blur(var(--blur));
    }
```
