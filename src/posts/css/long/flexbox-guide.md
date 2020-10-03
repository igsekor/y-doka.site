---
title: flexbox-гайд
name: flexbox-guide
section: css
type: long
tags:
 - cssLong
 - post
article: post
---
## Что это?

Долгое время веб существовал в статичном виде. Сайты разрабатывались и просматривались только на экранах мониторов стационарных компьютеров. В масштабах истории совсем недавно у нас появилось огромное разнообразие различных экранов — от мобильных телефонов, до телевизоров — на которых мы можем взаимодействовать с сайтами. Отсюда появилась необходимость в гибких системах раскладки.

Идея флексбоксов появилась ещё в 2009 году и по сей день этот стандарт развивается и прорабатывается. Основная идея флексов — гибкое распределение места между элементами, гибкая расстановка, выравнивание, гибкое управление. Ключевое слово **гибкое**, что и отражено в названии (*flex — англ. гибко*).

## Основные термины

- **флекс-контейнер**: элемент, к которому применяется свойство `display: flex`. Вложенные в него элементы начинают подчиняться правилам раскладки флексов.
- **флекс-элемент**: элемент вложенный, во флекс-контейнер.

![/assets/images/posts/flexbox-guide/1177F296-DD03-40B6-826F-413A5A8D3AFE.jpeg](/assets/images/posts/flexbox-guide/1177F296-DD03-40B6-826F-413A5A8D3AFE.jpeg)

- **основная ось**: основная направляющая флекс-контейнера, вдоль которой располагаются флекс-элементы
- **дополнительная (побочная, перпендикулярная) ось**: ось, идущая перпендикулярно основной. Позже вы поймёте для чего она нужна.

![/assets/images/posts/flexbox-guide/B98E7056-C0EA-42A7-9E92-44D3D37E362A.jpeg](/assets/images/posts/flexbox-guide/B98E7056-C0EA-42A7-9E92-44D3D37E362A.jpeg)

- **начало / конец основной оси**: точки в начале и в конце основной оси соответственно. Это пригодится нам для выравнивания флекс-элементов.
- **начало / конец дополнительной оси**: точки в начале и в конце дополнительной оси соответственно.

![/assets/images/posts/flexbox-guide/D5C64D4D-32A9-4E40-AE76-2F7776DCD0C2.jpeg](/assets/images/posts/flexbox-guide/D5C64D4D-32A9-4E40-AE76-2F7776DCD0C2.jpeg)

- **размер по основной оси (основной размер)**: размер флекс-элемента вдоль основной оси. Это может быть ширина или высота в зависимости от направления основной оси.
- **размер по дополнительной оси (дополнительный размер)**: размер флекс-элемента вдоль дополнительной оси. Это может быть ширина или высота в зависимости от направления дополнительной оси. Этот размер всегда перпендикулярен основному размеру. Если основной размер это ширина, то дополнительный размер это высота и наоборот.

![/assets/images/posts/flexbox-guide/4B25D8DF-ED2A-4ADD-93EE-99521CAA27AB.jpeg](/assets/images/posts/flexbox-guide/4B25D8DF-ED2A-4ADD-93EE-99521CAA27AB.jpeg)

## Свойства флекс-контейнера

### `display`

```css
.container {
	display: flex;
}
```

Когда мы задаём какому-то элементу значение `flex` для свойства `display` мы превращаем этот элемент в флекс-контейнер. Внутри него начинает действовать флекс контекст, его дочерние элементы начинают подчиняться свойствам флексбокса.

Снаружи флекс-контейнер выглядит как блочный элемент — занимает всю ширину родителя, следующие за ним элементы в разметке переносятся на новую строку.

```css
.container {
	display: inline-flex;
}
```

Если контейнеру задано значение `inline-flex`, то снаружи он начинает вести себя как строчный (инлайн) элемент — размеры зависят только от внутреннего контента, встаёт в строку с другими элементами. Внутри это ровно такой же флекс-контейнер, как и при предыдущем значении.

### `flex-direction`

Свойство управления направлением основной и дополнительной осей.

```css
.container {
	display: flex;
	flex-direction: row;
}
```

Возможные значения:

- `row` (значение по умолчанию) — основная ось идёт горизонтально слева направо, дополнительная ось идёт вертикально сверху вниз.
- `row-reverse` — основная ось идёт горизонтально справа налево, дополнительная ось идёт вертикально сверху вниз.
- `column` — основная ось идёт вертикально сверху вниз, дополнительная ось идёт горизонтально слева направо.
- `column-reverse` — основная ось идёт вертикально снизу вверх, дополнительная ось идёт горизонтально слева направо.

![/assets/images/posts/flexbox-guide/EB15A49C-5B77-4806-880E-8600D2B4EF7D.jpeg](/assets/images/posts/flexbox-guide/EB15A49C-5B77-4806-880E-8600D2B4EF7D.jpeg)

Важный момент: на сайтах с начертанием справа налево, например, на сайте на арабском языке, для значений `row` и `row-reverse` основная ось будет идти в обратном направлении. Для значений `column` и `column-revers` своё направление поменяет дополнительная ось.

### `flex-wrap`

```css
.container {
	display: flex;
	flex-wrap: nowrap;
}
```

По умолчанию значение у свойства `flex-wrap` установлено `nowrap`. В следствии флекс-элементы помещаются (или пытаются уместиться) в одну строку и не переносятся на новую строку даже если не влезают в размеры родителя.

Установив значение `wrap` мы можем изменить это поведение и флекс-элементы будут иметь возможность соскочить на новую строку, если не влезают в одну линию в рамках родителя.

Ещё одно возможное значение — `wrap-reverse` — в этом случае элементы будут располагаться снизу вверх, заполнив собой сперва нижнюю строку, а те, что не влезли, перепрыгнут на строку выше.

![/assets/images/posts/flexbox-guide/D4B6EF21-75AE-4F69-A374-0EEC1448B326.jpeg](/assets/images/posts/flexbox-guide/D4B6EF21-75AE-4F69-A374-0EEC1448B326.jpeg)

### `flex-flow`

Это свойство-шорткат для одновременного определения значений свойств `flex-direction` и `flex-wrap`.

```css
.container {
	display: flex;
	flex-flow: column wrap;
}

/* или */

.container {
	display: flex;
	flex-flow: row nowrap;
}
```

Как и со всеми шорткатами, с этим стоит быть осторожным. Хоть он и позволяет экономить пару строк кода, но в случае переопределения одного из значений придётся переписывать свойство целиком, повторяя второе значение, которое не меняется. В этот момент проще было бы иметь два отдельных свойства и менять значения отдельно.

### `justify-content`

```css
.container {
	display: flex;
	justify-content: space-between;
}
```

Свойство позволяет выравнивать флекс-элементы внутри флекс-контейнера по основной оси.

**Возможные значения:**

- `flex-start` (значение по умолчанию) — элементы прижимаются к краю, в котором начинается основная ось.
- `flex-end` — элементы прижимаются к краю, в котором основная ось заканчивается.
- `start` — элементы прижимаются к тому краю, откуда начинается чтение того языка, на котором отображается сайт. Например, для русского языка элементы прижмутся к левому краю при горизонтальной основной оси, а для арабского языка — к правому краю.
- `end` — элементы прижимаются к краю, противоположному началу направления чтения на том языке, на котором отображается сайт. Например, при горизонтальной основной оси на русском языке элементы прижмутся к правому краю.
- `left` — элементы прижмутся к левому краю родителя. В случае, если указано свойство `flex-direction: column`, то значение срабатывает как `start`.
- `right` — элементы прижмутся к правому краю. В случае, если указано свойство `flex-direction: column`, то значение срабатывает как `start`.
- `center` — элементы выстраиваются по центру родителя.
- `space-between` — крайние элементы прижимаются к краям родителя, оставшиеся выстраиваются внутри контейнера равномерно так, чтобы между ними были одинаковые отступы.
- `space-around` — свободное пространство будет поделено между элементами так, чтобы справа и слева каждый элемент имел одинаковые отступы.
- `space-evenly` — свободное место будет распределено так, чтобы расстояние между любыми двумя элементами было одинаковым и расстояние от крайних элементов до края было таким же.

Стоит обратить внимание, что с некоторыми значениями есть трудности:

1. Значение `space-between` поддерживается не во всех версиях Edge.
2. Значения `start` / `left` / `right` / `end` до сих пор не реализованы в Chrome.

Лучше периодически сверяться с 🔗 [Can I use](https://caniuse.com/#search=justify-content%20flex).

### `align-items`

```css
.container {
	display: flex;
	align-items: center;
}
```

Свойство выравнивания элементов внутри контейнера по дополнительной оси.

Возможные значения:

- `stretch` (значение по умолчанию) — элементы растягиваются вдоль дополнительной оси так, чтобы заполнить всего родителя. Это очень удобно, если делаете двухколоночный макет. Раньше приходилось колхозными способами добиваться одинаковой высоты, а теперь достаточно сделать контейнер флексом и колонки по умолчанию будут одной высоты.
- `flex-start` / `start` — элементы выстраиваются у начала дополнительной оси. Разница между ними лишь в том, что второе значение «уважает» направление чтения выбранного языка.
- `flex-end` / `end` — элементы выстраиваются у конца дополнительной оси. Разница между первым и вторым значениями аналогична предыдущему пункту.
- `center` — элементы выстраиваются по центру дополнительной оси.
- `baseline` — вот тут может быть сложно понять сразу. Элементы выравниваются по нижней линии текста. Собственно именно она называется «базовой линией» — baseline.

Вот вам демка чтобы было понятнее. Обратите внимание, что вне зависимости от размера шрифта все блоки выравниваются по нижней линии первой строки.

<p class="codepen" data-height="265" data-theme-id="light" data-default-tab="html,result" data-user="solarrust" data-slug-hash="PoNOyJm" style="height: 265px; box-sizing: border-box; display: flex; align-items: center; justify-content: center; border: 2px solid; margin: 1em 0; padding: 1em;" data-pen-title="PoNOyJm">
  <span>See the Pen <a href="https://codepen.io/solarrust/pen/PoNOyJm">
  PoNOyJm</a> by Alena (<a href="https://codepen.io/solarrust">@solarrust</a>)
  on <a href="https://codepen.io">CodePen</a>.</span>
</p>
<script async src="https://static.codepen.io/assets/embed/ei.js"></script>

### `align-content`

```css
.container {
	display: flex;
	align-content: center;
}
```

Свойство распределяет свободное пространство по дополнительной оси между строками флекс-элементов. Предположим, у вас 11 элементов на 3 строках. Если размер родителя по дополнительной оси позволяет, то при помощи `align-content` можно распределять строчки элементов, сверху, снизу, по центру или равномерно.

Не имеет видимого значения, если элементы располагаются в одну строку.

Возможные значения:

- `stretch` (значение по умолчанию) — строки растягиваются одинаково так, чтобы занять всё доступное пространство родителя.
- `flex-start` / `start` — все строки располагаются у начала дополнительной оси. Первое значение не зависит от режима чтения текущего языка в то время как второе значение *смотрит* на него.
- `flex-end` / `end` — все строки располагаются у конца дополнительной оси. `end` смотрит на режим чтения текущего языка.
- `center` — строки выравниваются по центру родителя.
- `space-between` — первая строка прижимается к началу дополнительной оси, последняя — к концу дополнительной оси, а остальные располагаются так, чтобы свободное пространство было поделено на отступы между ними равномерно.
- `space-around` — отступы у каждой строки равнозначны отступам у любой другой строки.
- `space-evenly` — отступы между строками и от краёв родителя одинаковые.

## Свойства флекс-элемента

### `order`

```css
.container {
	display: flex;
}

.item {
	order: 3;
}
```

При помощи свойства `order`  можно менять порядок отображения флекс-элементов внутри флекс-контейнера.

По умолчанию элементы отображаются в том порядке, в котором они расположены в разметке. По умолчанию значение свойства `order` равно 0. Но это свойство позволяет переставлять их местами.

Значение задаётся в виде целого отрицательного или положительного числа. Элементы встают по возрастающей.

![/assets/images/posts/flexbox-guide/9D5816FA-3145-4C1E-AAD2-09BADE56FCFC.jpeg](/assets/images/posts/flexbox-guide/9D5816FA-3145-4C1E-AAD2-09BADE56FCFC.jpeg)

### `flex-grow`

```css
.container {
	display: flex;
}

.item {
	flex-grow: 1;
}
```

Это свойство указывает, может ли и на сколько вырастать флекс-элемент при наличии свободного места. По умолчанию значение равно 0. Значением может быть любое положительное целое число (включая 0).

Если у всех флекс-элементов будет прописано `flex-grow: 1`, то свободное пространство в контейнере будет равномерно распределено между ними всеми.

Если при этом одному из элементов мы зададим `flex-grow: 2`, то он постарается *отжать* себе в два раза больше свободного места, чем его соседи.

### `flex-shrink`

```css
.container {
	display: flex;
}

.item {
	flex-shrink: 3;
}
```

Свойство `flex-shrink` полностью противоположно свойству `flex-grow`. Если в контейнере не хватает места для расположения всех элементов без изменения размеров, то свойство `flex-shrink` указывает в каких пропорциях элемент будет уменьшаться.

Чем больше значение у этого свойства, тем быстрее элемент будет сжиматься по сравнению с соседями, имеющими меньшее значение.

Значение по умолчанию — 1. Значением может быть любое целое положительное число (включая 0).

Два предыдущих свойства работают с пропорциональным разделением пространства, не с конкретными размерами. Они довольно непростые, даже опытный разработчик не всегда знает, как они в точности работают.
Загляни в конец статьи, если хочешь подробнее почитать о каждом из них.

### `flex-basis`

```css
.container {
	display: flex;
}

.item {
	flex-basis: 250px;
}
```

Свойство `flex-basis` указывает на размер элемента до того, как свободное место будет распределено (см. [flex-grow]()).

Значением может быть размер в любых относительных или абсолютных единицах: `20rem`, `5vw`, `250px`. А также можно использовать ключевое слово `auto` (значение по умолчанию). В этом случае при расчёте размера элемента будут приниматься во внимание значения свойств `width` / `max-width` / `min-width` или аналогичные свойства высоты. Зависит от того, в каком направлении идёт основная ось.

Если никакие размеры не заданы, а свойству `flex-basis` установлено значение `auto`, то элемент занимает столько пространства, сколько нужно для отображения контента.

### `flex`

```css
.container {
	display: flex;
}

.item {
	flex: 1 1 auto;
}
```

Свойство-шорткат, с помощью которого можно указать значение трёх свойств одновременно: `flex-grow`, `flex-shrink` и `flex-basis`. Первое значение является обязательным, остальные опциональны.

Значение по умолчанию: `0 1 auto`, что расшифровывается как `flex-grow: 0`, `flex-shrink: 1`, `flex-basis: auto`.

Возможные значения:

```css
/* 0 0 auto */
flex: none;

/* Одно значение, число без единиц: flex-grow */
flex: 2;

/* Одно значение, ширина/высота: flex-basis */
flex: 10em;
flex: 30px;
flex: auto;
flex: content;

/* Два значения: flex-grow | flex-basis */
flex: 1 30px;

/* Два значения: flex-grow | flex-shrink */
flex: 2 2;

/* Три значения: flex-grow | flex-shrink | flex-basis */
flex: 2 2 10%;

/* Глобальные значения */
flex: inherit;
flex: initial;
flex: unset;
```

### `align-self`

```css
.container {
	display: flex;
	align-items: flex-start;
}

.item {
	align-self: flex-end;
}
```

При помощи этого свойства можно выровнять один или несколько элементов иначе, чем задано у родительского элемента. Например, в коде выше у родителя задано выравнивание вложенных элементов по верхнему краю родителя. А для элемента с классом `.item` мы задаём выравнивание по нижнему краю.

### Ссылки

1. [Как реально работает `flex-grow`](https://medium.com/@stasonmars/%D0%BA%D0%B0%D0%BA-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%B5%D1%82-flex-grow-%D0%B2-css-%D0%BF%D0%BE%D0%B4%D1%80%D0%BE%D0%B1%D0%BD%D0%BE%D0%B5-%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-557d406be844)
2. [Как реально работает `flex-shrink`](https://medium.com/@stasonmars/%D0%BA%D0%B0%D0%BA-%D1%80%D0%B0%D0%B1%D0%BE%D1%82%D0%B0%D0%B5%D1%82-flex-shrink-%D0%B2-css-%D0%BF%D0%BE%D0%B4%D1%80%D0%BE%D0%B1%D0%BD%D0%BE%D0%B5-%D1%80%D1%83%D0%BA%D0%BE%D0%B2%D0%BE%D0%B4%D1%81%D1%82%D0%B2%D0%BE-c41e40767194)
3. [Песочница Флексбоксов](https://yoksel.github.io/flex-cheatsheet/)
4. [Game: Flexbox Froggy](https://flexboxfroggy.com/#ru)
5. [Game: Flexbox Defense](http://www.flexboxdefense.com/)
6. [Game: Flexbox Ducky](https://courses.cs.washington.edu/courses/cse154/flexboxducky/)
7. [Курс по Флексбоксам от Wes Bos](https://flexbox.io/)

## Классные фишки

### 🛠 Алёна, frontend-дева

🛠  Раньше было затруднительно прижать футер к нижнему краю экрана вне зависимости от количества контента на странице. Приходилось идти на всякие ухищрения и городить костыли. Теперь с появлением флексов всё стало просто как два пальца.

Оборачиваем всю страницу в блок, делаем его флекс-контейнером, внутрь вкладываем хэдер, мейн и футер. Родителю задаём `flex-direction: column` чтобы блоки встали друг под другом, а не в ряд, и `min-height: 100vh` чтобы он занимал как минимум всю высоту экрана. Мейну задаём `flex: 1` и вуа-ля! Центральный блок страницы будет всегда растягиваться на всё доступное свободное пространство. Из-за этого блок всегда будет прижиматься к нижнему краю страницы. При этом, если контента в мейне будет больше чем на один экран, то он растянется и подстроится, ничего не сломается.

🛠 Частой проблемой в вёрстке до появления флексбоксов было вертикальное выравнивание блока внутри родителя. Использовались хаки с трансформом, отступами, высотой строки и прочие костыли.

Теперь же всё делается в три строки:

1. Родителя делаем флекс-контейнером
2. Задаём ему выравнивание по основной оси по центру `justify-content: center`
3. Задаём ему выравнивание по дополнительной оси по центру `align-items: center`

Получаем выровненный по центру вложенный блок.

### 🛠 Егор, front-end ниндзя

Цель крутого front-end'ера решать задачи бизнеса, а не писать много кода. центрирование блока внутри родителя можно сократить до двух строк:

1. Родителя сделать flex-контейнером
2. Дочернему элементу задать `margin: auto`

Ждём сокращение кода до одной строки =)

## В работе

### 🛠 *Егор, front-end ниндзя*

Во время работы стоит быть особенно внимательным со свойствами, которые меняют внешнее расположение элементов внутри flex-контейнера: например `flex-direction: row-reverse` или `column-reverse`, а так же свойством `order`.

Дело в том, что контент меняет свое расположение только CSS-свойствами, а значит в теле сайта элементы окажутся в том порядке, в котором вы их написали в HTML-файле. Позаботьтесь о людях, которые пользуются "скринридерами", и не пользуйтесь исправлением положения элементов на странице CSS-свойствами без крайней необходимости.