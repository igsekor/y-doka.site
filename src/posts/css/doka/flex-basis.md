---
title: "flex-basis"
name: flex-basis
author: ABatickaya
co-authors:
designers:
contributors:
summary:
  - размер флекс-элементов
  - flexbox
---

## Кратко

Свойство `flex-basis` указывает на размер элемента до того, как свободное место будет распределено (см. [`flex-grow`](/css/doka/flex-grow/)).

## Пример

При отрисовке страницы элементу `.item` сперва будет задан размер по основной оси в 250 пикселей. Уже потом будут применяться правила [роста](/css/doka/flex-grow/) и [сжатия](/css/doka/flex-shrink/).

```css
.container {
  display: flex;
}

.item {
  flex-basis: 250px;
}
```

## Как это понять

У флекс-элементов размеры по основной и поперечной осям приоритетнее чем ширина (`width`) и высота (`height`). Это связано с идеей гибкости структуры, лежащей в основе модели флексбоксов.

## Как пишется

Значением может быть размер в любых относительных или абсолютных единицах: `20rem`, `5vw`, `250px`.

А также можно использовать ключевое слово `auto` (значение по умолчанию). В этом случае при расчёте размера элемента будут приниматься во внимание значения свойств `width`, `max-width`, `min-width` или аналогичные свойства высоты. Зависит от того, в каком направлении идёт основная ось.

Если никакие размеры не заданы, а свойству `flex-basis` установлено значение `auto`, то элемент занимает столько пространства, сколько нужно для отображения контента.

## Подсказки

💡 Значение `flex-basis` более приоритетно, чем значения свойств `width` или `height` (в зависимости от направления основной оси).

:::callout 📝
Полный список свойств флексбоксов можно посмотреть в [гайде по flexbox](/css/long/flexbox-guide/).
:::

{% include "authors/ABatickaya/author.njk" %}
