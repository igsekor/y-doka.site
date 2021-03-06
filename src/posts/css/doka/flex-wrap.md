---
title: "flex-wrap"
name: flex-wrap
author: ABatickaya
co-authors:
designers:
contributors:
summary:
  - перенос на новую строку
  - flexbox
---

## Кратко

Флекс-элементы по умолчанию стараются уместиться в одну строку, даже если размер им не позволяет.

Чтобы изменить это поведение свойству `flex-wrap` нужно задать свойство, отличное от `nowrap`.

## Пример

Флекс-элементы, вложенные во флекс-контейнер с классом `container`, не будут переноситься на новую строку ни при каких обстоятельствах. Всегда будут стоять в одну строку.

```css
.container {
  display: flex;
  flex-wrap: nowrap;
}
```

## Как это понять

Внутри флекс-контейнера элементы располагаются вдоль основной оси. Стандартным поведением считается расположение элементов в одну строку.

Если вы позволяете элементам переноситься на новую строку, изменив стандартное значение свойства `flex-wrap`, то для каждой строки будут созданы дополнительные основные оси. Каждая строка будет вести себя как отдельный флекс-контейнер, но с общим управлением.

## Как пишется

По умолчанию значение у свойства `flex-wrap` установлено `nowrap`. В следствии флекс-элементы помещаются в одну строку и не переносятся на новую строку, даже если не влезают в размеры родителя.

Установив значение `wrap` мы можем изменить это поведение и флекс-элементы будут иметь возможность соскочить на новую строку, если не влезают в одну линию в рамках родителя.

Ещё одно возможное значение — `wrap-reverse`. В этом случае элементы будут располагаться снизу вверх, заполнив собой сперва нижнюю строку, а те, что не влезли, перепрыгнут на строку выше.

![Пример свойства flex-wrap](/assets/images/posts/flexbox-guide/flexbox___06.png)

## Подсказки

💡 Ситуация, когда сумма размеров элементов превышает размер родителя, называется _переполнение контейнера_. Именно это произойдёт, если вы не разрешите флекс-элементам переноситься на новую строку.

:::callout 📝
Полный список свойств флексбоксов можно посмотреть в [гайде по flexbox](/css/long/flexbox-guide/).
:::

{% include "authors/ABatickaya/author.njk" %}
