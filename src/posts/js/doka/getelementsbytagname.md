---
title: "getElementsByTagName()"
name: getelementsbytagname
author: N_Lopin
co-authors:
designers:
contributors:
summary:
---

## Кратко

Метод определен для объекта `document` и любого HTML-элемента (`Element`) страницы. Позволяет найти все элементы с заданным тегом среди дочерних. Возвращает похожую на массив HTMLCollection с найденными элементами. Если элементов не нашлось, то коллекция будет пустая, то есть с размером 0.

## Пример

Метод принимает один параметр — название тега в виде строки. Например, `div`, `form`, `h5`

```html
<html>
  <head></head>
  <body>
    <div id="title">
      <h1>Привет, незнакомец!</h1>
      <p>Это параграф дочерний и для div, и для body</p>
    </div>
    <p>Это параграф, дочерний для body</p>
    <script>
      let pFromBody = document.getElementsByTagName("p")
      console.log(pFromBody.length) // напечатает 2, так как поиск ведется по всей странице

      let divEl = document.getElementById("title")
      // ищем параграфы внутри div:
      let pFromDiv = divEl.getElementsByTagName("p")
      console.log(pFromDiv.length) // напечатает 1, так как внутри div только один p

      // ищем несуществующий элемент
      let spanFromBody = document.getElementsByTagName("span")
      console.log(spanFromBody.length) // напечатает 0
    </script>
  </body>
</html>
```

Динамический пример, в котором поиск ведется по кликнутому блоку:

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="js,result" data-user="Lopinopulos" data-slug-hash="LoZaJp" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="Как работает getElementsByTagName">
  <span>See the Pen <a href="https://codepen.io/Lopinopulos/pen/LoZaJp">
  Как работает getElementsByTagName</a> by Nikolai Lopin (<a href="https://codepen.io/Lopinopulos">@Lopinopulos</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>

## Как это понять

Метод работает с DOM, который связан с HTML разметкой. Каждый HTML-элемент имеет родительские и дочерние элементы:

- Родительские элементы — это элементы, внутри которых находится элемент. В примере выше у элемента `h1` есть два родительских элемента — `div` и `body`.
- Дочерние элементы — это элементы, которые содержит текущий элемент. Они могут быть, а могут не быть. Например, для тега `body` все элементы страницы дочерние. У `h1` дочерний элемент — текст внутри тега.

Если работаешь с корнем страницы, объектом `document`, то поиск идет по всем элементам страницы (т.е. от `body`), если от конкретного элемента, то поиск идет только по всем дочерним.

Так как мы заранее не знаем, сколько элементов с искомым тегом найдется, то метод возвращает коллекцию элементов.

## В работе

{% include "authors/n_lopin/in-work.njk" %}

🛠 Поиск по тегам нужен нечасто.

🛠 Для поиска вообще всех элементов в качестве аргумента нужно передать строку `'*'`, ее называют wildcard.

🛠 Метод возвращает живую коллекцию. Это означает, что коллекция будет автоматически обновляться, если на странице появятся подходящие элементы:

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="js,result" data-user="Lopinopulos" data-slug-hash="xNOBow" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="xNOBow">
  <span>See the Pen <a href="https://codepen.io/Lopinopulos/pen/xNOBow">
  xNOBow</a> by Nikolai Lopin (<a href="https://codepen.io/Lopinopulos">@Lopinopulos</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

🛠 Не спеши, когда пишешь циклы над `HTMLCollection`. Так как коллекция живая, то цикл может стать бесконечным в тех случаях, когда на страницу добавляются и удаляются подходящие под поиск элементы.

🛠 Скрипты, которые работают с HTML видят только ту разметку, которую уже распарсил браузер. Браузер парсит HTML сверху вниз. Если ваш скрипт находится вверху страницы, то он не найдет элементы ниже в странице — браузер их еще не увидел и ничего о них не знает. Поэтому скрипты либо подключают в конце страницы, либо [подписываются на событие](/js/doka/event-load-and-domcontentloaded/) `DOMContent​Loaded`, которое сигнализирует о том, что браузер распарсил весь HTML.

{% include "authors/n_lopin/author.njk" %}
