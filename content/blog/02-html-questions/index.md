---
title: HTML Questions
date: "2021-08-31"
description: "HTML Questions"
---

Answers to [Front-end Job Interview Questions - HTML Questions](https://github.com/h5bp/Front-end-Developer-Interview-Questions/blob/main/src/questions/html-questions.md). Although the [Front-end Interview Handbook](https://github.com/yangshun/front-end-interview-handbook/blob/master/contents/en/html-questions.md) has given answers, i'd like to answer these questions by myself to deepen by understanding.

## Table of Contents

- [What does a `doctype` do?](#what-does-a-doctype-do)
- [How do you serve a page with content in multiple languages?](#how-do-you-serve-a-page-with-content-in-multiple-languages)
- [What kind of things must you be wary of when designing or developing for multilingual sites?](#what-kind-of-things-must-you-be-wary-of-when-designing-or-developing-for-multilingual-sites)
- [What are `data-` attributes good for?](#what-are-data--attributes-good-for)
- [Consider HTML5 as an open web platform. What are the building blocks of HTML5?](#consider-html5-as-an-open-web-platform-what-are-the-building-blocks-of-html5)
- [Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.](#describe-the-difference-between-a-cookie-sessionstorage-and-localstorage)
- [Describe the difference between `<script>`, `<script async>` and `<script defer>`.](#describe-the-difference-between-script-script-async-and-script-defer)
- [Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?](#why-is-it-generally-a-good-idea-to-position-css-links-between-headhead-and-js-scripts-just-before-body-do-you-know-any-exceptions)
- [What is progressive rendering?](#what-is-progressive-rendering)
- [Why you would use a `srcset` attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.](#why-you-would-use-a-srcset-attribute-in-an-image-tag-explain-the-process-the-browser-uses-when-evaluating-the-content-of-this-attribute)
- [Have you used different HTML templating languages before?](#have-you-used-different-html-templating-languages-before)
- [What is the difference between `canvas` and `svg`?](#what-is-the-difference-between-canvas-and-svg)
- [What are empty elements in HTML?](#what-are-empty-elements-in-html)

---

### What does a `doctype` do?

- Prevent a browser from switching into so-called "quirks mode" when rendering a document.

###### References

- [https://developer.mozilla.org/en-US/docs/Glossary/Doctype](https://developer.mozilla.org/en-US/docs/Glossary/Doctype)

⬆️ [Back to top](#table-of-contents)

---

### How do you serve a page with content in multiple languages?

⬆️ [Back to top](#table-of-contents)

---

### What kind of things must you be wary of when designing or developing for multilingual sites?

- Provide `lang` attribute for `<html>` element. Help screen reading technology determine the proper language to announce.

###### References

- [https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/html)

⬆️ [Back to top](#table-of-contents)

---

### What are `data-` attributes good for?

- Allow us to store extra information on standard, semantic HTML elements.

###### References

- [https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes](https://developer.mozilla.org/en-US/docs/Learn/HTML/Howto/Use_data_attributes)

⬆️ [Back to top](#table-of-contents)

---

### Consider HTML5 as an open web platform. What are the building blocks of HTML5?

The Open Web Platform is the collection of open (royalty-free) technologies which enables the Web.

- HTML, CSS, JavaScript
- DOM
- SVG
- MathML
- Web APIs
- HTTP
- URI
- Media Accessibility Checklist

###### References

- [https://www.w3.org/wiki/Open_Web_Platform](https://www.w3.org/wiki/Open_Web_Platform)

⬆️ [Back to top](#table-of-contents)

---

### Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.


| Feature           | cookie                    | localStorage     | sessionStorage     |
| :---------------- | :------------------------ | :--------------- | :----------------- |
| Maximum data size | 4 kB                      | 5 MB             | 5MB                |
| Accessed on       | server-side & client side | client-side only | client-side only   |
| Lifetime          | specified                 | till deleted     | till tab is closed |

###### References

- [https://krishankantsinghal.medium.com/local-storage-vs-session-storage-vs-cookie-22655ff75a8](https://krishankantsinghal.medium.com/local-storage-vs-session-storage-vs-cookie-22655ff75a8)

⬆️ [Back to top](#table-of-contents)

---

### Describe the difference between `<script>`, `<script async>` and `<script defer>`.

- When a browser loads HTML and come across a `<script>` tag, it must wait for the script to download, execute the downloaded script, and only then can it continue building the DOM.
- The `<script defer>` loads "in the background", and then runs when the DOM is fully built (but before `DOMContentLoaded` event).
    - Deferred scripts keep their relative order, it means all scripts with defer attribute download in parallel, but run in order.
- The `<script async>` loads "in the background" and run when ready. The DOM and other scripts don't wait for them.
    - Load-firsr order. The script downloaded first run first.

###### References

- [https://javascript.info/script-async-defer](https://javascript.info/script-async-defer)

⬆️ [Back to top](#table-of-contents)

---

### Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?

For `<link>`,

- Download the external stylesheet resource regardless of DOM already rendered or not.
- When the page is loaded, user can see the elegant page.

For `<script>`, 

- Every time a `<script>` tag is encounted, the page must stop and wait for the code to download and execute before continuing to process the rest of the page.
- Put all `<script>` tag just before `</body>` tag ensures that the page can be alomost completely rendered before execution begins.

###### References

- [https://www.oreilly.com/library/view/high-performance-javascript/9781449382308/ch01.html](https://www.oreilly.com/library/view/high-performance-javascript/9781449382308/ch01.html)

⬆️ [Back to top](#table-of-contents)

---

### What is progressive rendering?

###### References

- [https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps](https://developer.mozilla.org/en-US/docs/Web/Progressive_web_apps)

⬆️ [Back to top](#table-of-contents)

---

### Why you would use a `srcset` attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.

- `srcset` is a string which identifies one or more image candidate strings, separated using commas, each specifying image resources to user under given circumstances.
- Each image candidate string contains an image URL and an optional width or pixel density descriptor indicates the conditions.

###### References

- [https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/srcset](https://developer.mozilla.org/en-US/docs/Web/API/HTMLImageElement/srcset)

⬆️ [Back to top](#table-of-contents)

---

### Have you used different HTML templating languages before?

lit-html

###### References

- [https://lit-html.polymer-project.org/guide](https://lit-html.polymer-project.org/guide)

⬆️ [Back to top](#table-of-contents)

---

### What is the difference between `canvas` and `svg`?

###### References

- [https://css-tricks.com/when-to-use-svg-vs-when-to-use-canvas/](https://css-tricks.com/when-to-use-svg-vs-when-to-use-canvas/)

⬆️ [Back to top](#table-of-contents)

---

### What are empty elements in HTML?

- An empty element is an element that cannot have any child notes (i.e., nested elements or text nodes).

###### References

- [https://developer.mozilla.org/en-US/docs/Glossary/Empty_element]()

⬆️ [Back to top](#table-of-contents)

---

### 元信息类标签（head, title, meta）的使用目的和配置方法

- `<meta charset="UTF-8" />` 声明文档的字符编码。
- `<meta http-equiv="X-UA-Compatible content="IE=edge" />` 覆盖 IE 的兼容性视图设置，无论浏览器如何设置，页面都会以标准模式渲染（[what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do](https://stackoverflow.com/questions/6771258/what-does-meta-http-equiv-x-ua-compatible-content-ie-edge-do)）。
- `<meta name="viewport" content="width=device-width, initial-scale=1.0" />` 可以让移动端浏览器的虚拟视口匹配设备的尺寸。移动端浏览器和桌面端浏览器不同，会在虚拟视口（virtual viewport）中渲染页面，一般渲染的页面宽度是 980px，经常会大于移动设备屏幕的宽度，然后再将页面缩小以适合屏幕的尺寸，但是这样可能会导致页面难以辨认？所以可以设置视口标签，让移动端浏览器直接按设备的屏幕宽度渲染页面（[is-the-viewport-meta-tag-really-necessary](https://stackoverflow.com/questions/14775195/is-the-viewport-meta-tag-really-necessary/14775557#14775557)）。
