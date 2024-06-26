# Тестовое задание для отбора на Летнюю ИТ-школу КРОК по разработке

## Условие задания
Однажды теплым летним вечером вас посетила идея разработать свое расширение для браузера для построения ссылочного графа. Что это означает на практике — ваше расширение активируется на какой-либо web-странице сайта, определяет список уникальных внешних ссылок, после чего повторяет алгоритм для каждой ссылки. Максимальная глубина поиска, визуализация собранных данных и прочие вопросы вы сочли вторичными, а начать решено было с малого — с обходчика страниц, который бы находил уникальные ссылки.

В процессе проектирования вы решили немного упростить ваш mvp и в итоге поставили себе задачу следующим образом: реализовать поиск всех уникальных ресурсов (доменов) в рамках страницы, на которые есть ссылки. При этом, формулируя задачу, вы сделали следующие допущения:
- Доменом считается запись вида example.com;
- Поддомен, например, sub.example.com,  считается отдельным ресурсом;
- Протокол (при наличии) не имеет значения.

Требования к реализации:
1. Реализация должна содержать, как минимум, одну процедуру (функцию/метод), отвечающую за поиск уникальных ресурсов, и должна быть описана в readme.md в соответствии с чек-листом;
2. В качестве входных данных программа использует реальный html-файл (page.html)	, считав который, начинает выполнять поиск;
3. Процедура (функция/метод) поиска должна возвращать строку в формате json следующего формата:
   - {«sites»: [«mail.ru», «rbc.ru», «ria.ru»]}
4. Найденные в соответствии с условием задачи домены должны выводиться в нижнем регистре без указания протокола и «www» в алфавитном порядке.

## Автор решения
Егоров Артём Олегович
## Описание реализации
Идея решения - парсить html-документ (`HtmlDocument htmlDocument`) для поления списка всех тэгов `a`, которые имеют атрибут `href`. Проанализировать каждый элемент списка (`HtmlNodeCollection listNodes`) на налачие доменного имени. Если таковое имеется, то добавляем доменное имя в множество уникальных элементов (`SelectedSites setDomains`). Для сохранения результата работы функции используется отдельный класс `SelectedSites`, имеющий в себе свойство `SortedSet Sites` (`SortedSet` используется для хранения доменов в лексикографическом порядке)

Подробнее:
   1. Метод ParseLinksAsync принимает путь к HTML-документу, загружает его, а затем асинхронно разбирает содержимое, извлекая все ссылки `<a>` с атрибутом `href`.
   2. Для каждой ссылки извлекается домен, и если он не пустой, преобразуется в URI и проверяется на наличие префикса "www.".
   3. Уникальные домены добавляются в объект `SelectedSites`, а затем сериализуются в формат JSON.

### Про библиотеку HtmlAgilityPack

[HtmlAgilityPack](https://github.com/zzzprojects/html-agility-pack) - библиотека для парсинга html-документов с открым исходным кодом. Разрабатывается под лицензией MIT, которая не восприщает использование её в коммерческих продуктах. 

[Подробнее про MIT](https://mit-license.org/)
## Инструкция по сборке и запуску решения
1. Сборка решения LinksParses:
   1. Переходим в директорию LinksParser
   2. Выполняет в терминале `dotnet build`
2. Тестирование решения:
   1. Переходим в директорию Test
   2. Выполняем в терминале `dotnet test`