---
title: ECMAScript 2015 (ES6) и выше
layout: docs.hbs
---

# ECMAScript 2015 (ES6) и выше

Node.js строится на современных версиях [V8](https://v8.dev/). Базируясь на последних
выпусках этого движка, мы обеспечиваем поддержку новых функций из
[спецификации JavaScript ECMA-262](http://www.ecma-international.org/publications/standards/Ecma-262.htm)
своевременно предоставляя их разработчикам Node.js, а также улучшая производительность и стабильность.

Весь функционал ECMAScript 2015 (ES6) разделен на три группы: **поставляемый (shipping)**,
**подготовленный (staged)** и **в процессе (in progress)**:

* Весь **поставляемый** функционал, который V8 считает стабильным, включен **по умолчанию в Node.js**
  и **НЕ** нуждается в дополнительных конфигурациях и флагах.
* **Подготовленный** функционал, это список почти готовых внедрений, который еще не утвержден
  командой V8 как стабильный, и требует дополнительный флаг `--harmony`.
* Функционал под знаком **в процессе** может быть активирован индивидуально, с помощью соответствующего
  флага гармонизации, хотя это крайне нежелательно, кроме как для целей тестирования. Примечание: 
  эти флаги доступны в V8 и могут измениться без уведомления об их устаревании.

## Какие функции поставляются с какой версией Node.js по умолчанию?

На сайте [node.green](http://node.green) представлен отличный обзор поддерживаемого функционала
ECMAScript в различных версиях Node.js на основе таблицы сравнения kangax.

## Какие функции в процессе?

Новые функции постоянно добавляются в движок V8. Вообще говоря, ожидайте, что они появятся
в будущем выпуске Node.js, хотя точных дат неизвестно.

Вы можете узнать функционал *в процессе*, доступный в каждом выпуске Node.js, используя аргумент
`--v8-options`. Обратите внимание, что это неполные и, возможно, некорректные функции V8, поэтому
используйте их на свой страх и риск:

```bash
node --v8-options | grep "in progress"
```

## А как насчет производительности конкретного функционала?

Команда V8 постоянно работает над улучшением производительности новых языковых функций, чтобы в
конечном итоге достичь равенства со своими транспилированными или нативными аналогами в EcmaScript 5
или более ранних версиях. Текущий прогресс отслеживается на веб-сайте [six-speed](https://fhinkel.github.io/six-speed),
который показывает производительность функций ES2015 и ESNext по сравнению с их родными аналогами ES5.

Работа по оптимизации функций, представленных в ES2015 и более поздних версиях, координируется с помощью
[плана производительности](https://docs.google.com/document/d/1EA9EbfnydAmmU_lM8R_uEMQ-U_v4l9zulePSBkeYWmY),
где команда V8 собирает и координирует сферы, требующие улучшения, и разрабатывает документы для решения этих проблем.

## Моя инфраструктура настроена с использованием флага --harmony. Должен ли я удалить его?

Текущее поведение флага `--harmony` на Node.js состоит в том, чтобы включать только **подготовленный** функционал.
В конце концов, теперь это синоним `--es_staging`. Как упомянуто выше, это законченные функции, которые еще не считаются
стабильными. Если вы беспокоитесь о безопасности использования таких функций, особенно в производственных средах, рассмотрите
возможность выключения этого флага до тех пор, пока требуемые функции не перейдут в стадию "по умолчанию" на V8 и, следовательно,
на Node.js. Если вы оставите его включенным, вы должны быть готовы к дальнейшим обновлениям Node.js, которые могут сломать ваш код,
если V8 изменит свою семантику, чтобы более точно следовать стандарту.

## Как мне узнать, какая версия V8 поставляется с определенной версией Node.js?

Node.js предоставляет простой способ перечисления всех зависимостей и соответствующих версий, которые поставляются
с конкретным бинарным файлом через глобальный объект `process`. В случае с двигателем V8 введите следующее в своем
терминале, чтобы узнать его версию:

```bash
node -p process.versions.v8
```
