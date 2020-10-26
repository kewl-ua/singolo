## Руководство по стилю
Для того чтобы код было легко поддерживать и дополнять, важно придерживаться согласованных правил написания кода.
Общий код должен выглядеть так как будто его писал один человек.

## Настройки редактора
### Размер табуляции
Размер табуляции составляет 4 пробела.
Указать его можно в нижнем меню редактора:
![](http://i.piccy.info/i9/6d1c4ea0c236e1abb5b11eec917d4097/1603590934/64051/1402189/Snymok_ekrana_2020_10_25_v_04_00_22.png)

### Максимальная длина строки
Максимальная длина строки не должна превышать 120 символов.
Контролировать длину строки можно с помощью отслеживания позиции курсора:
![](http://i.piccy.info/i9/dec48c3d59d2539207953e1b627d20fb/1603590442/49440/1402189/Snymok_ekrana_2020_10_25_v_03_47_37.png)

## TODO
Для обозначения задач в коде можно использовать конструкцию `TODO: описание задачи`. Например:
```html
<meta name="description" content="..."> <!-- TODO: Make description -->
```
В последствии можно поставить TODO плагин для редактора и иметь список всех TODO на специальной кладке в навигаторе:
![](http://i.piccy.info/i9/d7cb63d664b7b92363f3bf6d4b03d4a3/1603596951/104162/1402192/Snymok_ekrana_2020_10_25_v_05_40_43.png)

## Статика
### Именование изображений
Каждое изображение, которое подразумевает использование только в одном компоненте именуем как component-name_index.format. Например:
`portfolio_1.jpg`

### Путь
Указывая ресурс к изображениям из SCSS помните, что путь будет браться из папки CSS, которая лежит всего на уровень ниже корня проекта.
В итоге в файле `scss/base/_fonts.scss` вместо:
```css
url: (../../fonts/Lato-Regular.ttf)
```
Нужно писать:
```css
url: (../fonts/Lato-Regulat.ttf)
```

## Комментарии
### SASS
Используем **только** [многострочные](https://developer.mozilla.org/ru/docs/Web/CSS/%D0%A2%D0%B8%D1%85%D0%B8%D0%B9) комментарии.
```scss
/* Every except of first */
& + &::before {
    content: "\00B7"; /* &middot; = · */
    display: inline-flex;
    ...
}
```

## HTML
### Именование классов
Для именования классов используем [Kebab Case](https://techrocks.ru/2018/08/09/most-common-programming-case-types/).
```html
<ul class="nav-list">
    <li class="nav-item">
        <a href="#" class="nav-link">Home</a>
    </li>
</ul>
```
Слова разделяются дефизами и пишутся строчными буквами.

### Переносы
В случае вложенности тегов ставится перенос с последующей табуляцией для обозначения уровня вложенности:
```html
 <li class="post-item">
    <img src="post.jpg" class="post-image">

    <div class="post-description">
        <h3 class="post-title">
            <a href="#" class="post-link">This is blog post title</a>
        </h3>
        <p class="post-preview">
            ...
        </p>
    </div>
</li>
```

Допускается одна вложенность на одной строке в случае если ее это декоративный тег:
```html
<h1 class="title">My name is <b class="important">John Doe</b></h1>
```

Отдельные компоненты разделяются пустой строкой:
```html
<header class="header">
    <div class="header-container">
        ...
    </div>
</header>

<main class="content">
    ....
</main>

<footer class="footer">
    ...
</footer>
```

## Стили
### CSS селекторы и правила
При написании CSS придерживаемся следующего стиля:
```css
.first-class {
    font-size: 24px;
    color: #ffffff;
    ...
}

.second-class {
    ...
}

...
```
После имени класса следует:
1.  пробел
2.  фигурная скобк
3.  перенос строки
4.  табуляция
5.  имя свойства - пробел - значение свойства - точка с запятой
...
6.  перенос на новую строку
7.  закрытие фигурной скобки
8.  перенос на новую строку

В случае  нескольких селекторов с одинаковыми правилами, после каждого селектора ставится запятая и перенос строки:
```css
.link:hover,
.link.active {
    ...
}
```

Подход в SCSS ничем не отличается от CSS. За исключением того что при обьявлении класса мы сначала перечисляем его свойства, а уже потом перечисляем его производные селекторы, разделенные пустой строкой.
```scss
.nav {
    padding: 20px 0;
    
    &-list {
        ...
    }

    &-item {
        ...
    }

    &-link {
        ...
    }
}
```

То же самое и с несколькими селекторами с одинаковыми правилами:
```scss
.nav {
    ...

    &-link {
        &:hover,
        &.active {
            ...
        }

        &-facebook {
            ...
        }
    }
}
```

### Единицы измерения
Для шрифтов испозьуем **только** rem. То есть свойства font-size и line-height должны иметь значение в rem'ах. Для всего остального допустимы любые другие единицы.
Исключением является только vw/vh в случае если это стили для responsive. Например, чтобы не указывать множество медиа-брейкпоинтов, постоянно уменьшая шрифт можно просто написать:
```scss
font-size: 1.2vh;
```

### Цвета
Цвета записываем в hex-формате без сокращенйи. То есть вместо `#fff` пишем `#ffffff`.
Если цвет прозрачный, то допускается использовать rgba() формат.

### Последовательность правил
Желателньо, но не обязательно, сначала перечислять правила для блочной модели, затем позиционирования, затем для шрифтов и уже потом фон и декоративные правила:
```scss
.box {
    display: inline-flex;
    flex-direction: column;
    width: 200px;
    border: 1px solid $grey-color-1;
    position: relative;
    font-size: 2.3rem;
    font-style: italic;
    color: $blue-color-3;
    text-transform: uppercase;
}
```

## SASS архитектура проекта
### abstracts
В папке **abstracts** хранятся неиспользуемые напрямую стили. То есть только вспомогательные вещи:
- abstracts
    - _mixins.scss - вспомогательные миксины
    - _variables.scss - переменные

### base
В папке **base** хранятся базовые стили:
- base
    - _fonts.scss - шрифты
    - _reset.scss - сброс стандартных стилей браузера
    - _tags.scss - стили тегов

### components
В папке **components** хранятся стилики компонентов. Композитные компоненты выделяются в отдельные директории и разбиваются на составляющие.
Простые компоненты описываются в одном файле. Зачастую это повторяющиеся встраиваемые компоненты, как например: иконки, заголовки, списки.
*   components
    *   header
        *   nav
            *   _item.scss
            *   _link.scss
            *   _list.scss
            *   _main.scss
        *   socials
            *   _list.scss
            *   _item.scss
            *   _link.scss
            *   _main.scss
        *   _main.scs
    *   banner
        *   ...
        *   ...
    *   portfolio
        *   ...
        *   ...
    *   _title.scss
    *   _icon.scss
    *   ...

## SASS подход к написанию компонентов
Каждую часть компонента реализовыаем как миксин, собирая все нужно в **файле-бандле**. Обычно, это _main.scss.

`nav/_item.scs`
```scss
@mixin nav-item() {
    color: $blue-color-1;
    text-transform: uppercase;

    & + & {
        margin-left: 8px;
    }
}
```
`nav/_main.scss`
```scss
@import "item";

...

.nav {
    &-item {
        @include nav-item;
    }

    &-list {
        ...
    }

    ...
}
```

Это позволит нам держать разметку чистой, не засоряя ее множеством классов в элементах, например вместо:
```html
<h1 class="title title-important title-portfolio">
```
Мы будем иметь:
```html
<h1 class="portoflio-title">
```
Так как:
`portfolio/_title.scss`
```scss
@mixin portoflio-title() {
    @include title-important($gray-color-1);
    margin-bottom: 20px;
}
```
`portfolio/_main.scss`
```scss
.portfolio {
    &-title {
        @include portfolio-title();
    }
}
```

## Медиа/Респонсив/Адаптив
Для каждого компонента у которого будут медиа-стили, создаем рядом с главным (_main.scss) файлом `_responsive.scss`.
В случае если это простой компонент (т.е. явлюящийся частью другого), то пишем для него миксин с соответствующим названием.
`scss/components/footer/copyright/_responsive.scss`
```scss
@mixin copyright-responsive() {
    @include respond-to(mobiles) {
        margin-top: 20px;
    }
}
```

Если это составной компонент (тот, который включает в себя другие), то в таком случае выглядеть он будет по подобию `_main.scss` в таких компонентах.
`scss/components/footer/_main.scss`
```scss
@import "socials/main";
@import "copyright/main";

.footer {
    background-color: $blue-color-2;

    &-inner {
        @include site-width;
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 22px 0;
    }

    &-copyright {
        @include footer-copyright;
    }

    ...
}
```

`scss/components/footer/_responsive.scss`
```scss
@import "copyright/responsive";

.footer {
    &-inner {
        @include respond-to(mobiles) {
            flex-direction: column-reverse;
        }
    }

    &-copyright {
        @include copyright-responsive;
    }
}
```

Не забываем подключить респонсив-часть компонента в отдельный банд для респонсива `scss/responsive.scss`.
```scss
/* Components */
...
@import "components/footer/responsive";
```

Медиа стили пишем только с помощью миксина `respond-to`:
```scss
@include respond-to(mobiles) {
    font-size: 1.8vw;
    margin-top: 20px;
    ...
}
```

Выглядит сложно, но это оправдано, так как таким образом мы получим отдельный скомпилированный CSS-файл только для респонсива (так как этот SASS-файл начинается без "_").
Что позволить подключать файл с респонсив стилями только тогда, когда понадобится, а не со всеми другими стилями:
`index.html`
```HTML
<link rel="stylesheet" href="css/responsive.css" media="screen and (max-width: 1279px)">
```

Также, это сводит к минимум вероятность того, что разные участники будут править один и тот же файл, создавая конфликты при слиянии.

## Слияние
### Pull requests
Перед тем как создавать pull request зайдите в настройки репозитория
![](http://i.piccy.info/i9/1d94be21a42b5f63452e2a885824d5d3/1603634221/78992/1402192/Snymok_ekrana_2020_10_25_v_16_02_08.png)

И укажите мою почту в Default reviewers
![](http://i.piccy.info/i9/4219a00b4f48db0a23012129130e92f5/1603634155/56888/1402192/61280Snymok_ekrana_2020_10_25_v_15_59_57.jpg)
