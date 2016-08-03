# [Boomstarter](https://boomstarter.ru)

В качестве второго объекта анализа сайта на предмет его оптимизации я выбрал сайт крупнейшей в России краудфандинговой платформы - Бумстартер.

- [HTML](#html)
- [CSS](#css)
- [JavaScript](#javascript)
- [Изображения](#изображения)
- [Доступность](#доступность)

### HTML

Как и в предыдущем случае HTML код веб-страницы не сжат, что, пожалуй, не очень хорошо.

### CSS

CSS сжат из рук вон плохо. Код изобилует большим количеством не очень приятных мелочей:

1. Несокращённые HEX-цвета: `#333333`, `#eeeeee`, `#999999`

2. Ещё раз цвета: `color: white`

3. Кавычки, которые можно было бы опустить: `background-image:url("/assets/compass/icon-sprite.png")`

4. Большие изображения заинлайненные в `base64`

5. Подобный каскадный ужас:

```css
.profile .popup.donate #pay-method .method-descriprion>li.phone fieldset input[type=text]
#phone-code,.profile .popup.donate #pay-method .method-descriprion>li.phone fieldset
input[type=text]#phone-code-qiwi,.profile .popup.donate #pay-method .method-descriprion>li
.phone fieldset input[type=text]#phone-code-ter,.profile .popup.donate #pay-method
.method-descriprion>li.qiwi fieldset input[type=text]#phone-code,.profile .popup.donate
#pay-method .method-descriprion>li.qiwi fieldset input[type=text]#phone-code-qiwi,.profile
.popup.donate #pay-method .method-descriprion>li.qiwi fieldset input[type=text]#phone-code-ter,
.profile .popup.donate #pay-method .method-descriprion>li.terminal fieldset input[type=text]
#phone-code,.profile .popup.donate #pay-method .method-descriprion>li.terminal fieldset
input[type=text]#phone-code-qiwi,.profile .popup.donate #pay-method .method-descriprion>li
.terminal fieldset input[type=text]#phone-code-ter,.profile .popup.donate #pay-method
.carrier-descriprion>li.phone fieldset input[type=text]#phone-code,.profile .popup.donate
#pay-method .carrier-descriprion>li.phone fieldset input[type=text]#phone-code-qiwi,.profile
.popup.donate #pay-method .carrier-descriprion>li.phone fieldset input[type=text]#phone-code-ter,
.profile .popup.donate #pay-method .carrier-descriprion>li.qiwi fieldset input[type=text]
#phone-code,.profile .popup.donate #pay-method .carrier-descriprion>li.qiwi fieldset
input[type=text]#phone-code-qiwi,.profile .popup.donate #pay-method .carrier-descriprion>li
.qiwi fieldset input[type=text]#phone-code-ter,.profile .popup.donate #pay-method
.carrier-descriprion>li.terminal fieldset input[type=text]#phone-code,.profile .popup.donate
#pay-method .carrier-descriprion>li.terminal fieldset input[type=text]#phone-code-qiwi,.profile
.popup.donate #pay-method .carrier-descriprion>li.terminal fieldset input[type=text]#phone-code-ter,
.profile .popup.donate #carrier-info .method-descriprion>li.phone fieldset input[type=text]
#phone-code,.profile .popup.donate #carrier-info .method-descriprion>li.phone fieldset
input[type=text]#phone-code-qiwi,.profile .popup.donate #carrier-info .method-descriprion>
li.phone fieldset input[type=text]#phone-code-ter,.profile .popup.donate #carrier-info
.method-descriprion>li.qiwi fieldset input[type=text]#phone-code,.profile .popup.donate
#carrier-info .method-descriprion>li.qiwi fieldset input[type=text]#phone-code-qiwi,.profile
.popup.donate #carrier-info .method-descriprion>li.qiwi fieldset input[type=text]#phone-code-ter,
.profile .popup.donate #carrier-info .method-descriprion>li.terminal fieldset input[type=text]
#phone-code,.profile .popup.donate #carrier-info .method-descriprion>li.terminal fieldset
input[type=text]#phone-code-qiwi,.profile .popup.donate #carrier-info .method-descriprion>li
.terminal fieldset input[type=text]#phone-code-ter,.profile .popup.donate #carrier-info
.carrier-descriprion>li.phone fieldset input[type=text]#phone-code,.profile .popup.donate
#carrier-info .carrier-descriprion>li.phone fieldset input[type=text]#phone-code-qiwi,.profile
.popup.donate #carrier-info .carrier-descriprion>li.phone fieldset input[type=text]#phone-code-ter,
.profile .popup.donate #carrier-info .carrier-descriprion>li.qiwi fieldset input[type=text]#phone-code,
.profile .popup.donate #carrier-info .carrier-descriprion>li.qiwi fieldset input[type=text]#phone-code-qiwi,
.profile .popup.donate #carrier-info .carrier-descriprion>li.qiwi fieldset input[type=text]#phone-code-ter,
.profile .popup.donate #carrier-info .carrier-descriprion>li.terminal fieldset input[type=text]#phone-code,
.profile .popup.donate #carrier-info .carrier-descriprion>li.terminal fieldset input[type=text]
#phone-code-qiwi,.profile .popup.donate #carrier-info .carrier-descriprion>li.terminal fieldset
input[type=text]#phone-code-ter
{
  margin-left:10px;
}
```

*... до тучи прочего*

Опять же вытягивается целый иконочный шрифт ради вставки 4 иконок, которые следовало бы вытащить из шрифтов.

Снова много неиспользуемых CSS правил.

![](https://cloud.githubusercontent.com/assets/5698350/17378457/b993910a-59c6-11e6-9447-30a28d08f5da.png)

### JavaScript

Несколько скриптов блокируют загрузку HTML документа:

```html
<script data-rocketsrc="/assets/application-28ed29d068879d5d4ac43d1acd126339bae699225625915644efe8f041f66f8c.js" type="text/rocketscript"></script>
<script data-rocketsrc="/assets/vendor/adfox/adfox.asyn.code.ver3-f6eab9fa6297a3b065b575ce69c7ac21bff30f0831fc5fe1b0fa1a9031a3e1ee.js" type="text/rocketscript"></script>
```

Скрипты необходимо объединить, дабы уменьшить количество запросов к серверу. Сами скрипты грузятся не асинхронно, нет `aync` и `defer`.

### Изображения

Изображения не обрезаются и грузятся в большом размере, не смотря на то, что на любом девайсе размер показываемого изображения строго фиксирован средствами CSS.

![](https://cloud.githubusercontent.com/assets/5698350/17378980/ee55974c-59c8-11e6-9eec-3360fa962e28.png)

Многие изображения неоптимизированы.

Маленькие картинки с логотипами кураторов краудфандинговых проектов (не меняющихся уже который год), следовало бы объединить в единый спрайт, дабы сократить количество запросов к серверу и уменьшить объём изображений.

![](https://cloud.githubusercontent.com/assets/5698350/17379095/81f7405e-59c9-11e6-87ac-878c9c1fa19c.png)

### Доступность

Что касается доступности сайта проекта, то прежде всего хочется отметить, что сайт неоптимизирован для мобильных устройств вообще, не смотря даже на то, что там зачем-то используется даже сетка Бутстрапа.

![](https://cloud.githubusercontent.com/assets/5698350/17378685/975b50f4-59c7-11e6-81e3-16919f9c1cf3.png)

Сжатия содержимого веб-страницы с помощью gzip и deflate нет, а ведь это позволило бы сократить объём передаваемых данных на 66%.

Кеширование не используется, время ответа сервера достаточно высокое.

Всё грустно.

:anguished:
