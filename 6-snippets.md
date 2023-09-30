# Selenide
Фреймворк для автоматизированного тестирования веб-приложений на основе Selenium WebDriver. Отмечается, что данный фреймворк более простой в использовании и содержит много автоматизированных процессов.

### Подключаем Selenide:

````java
dependencies {
testImplementation 'com.codeborne:selenide:6.4.0'
}
````

# Для работы с браузером

### Открытие страницы:
````java
// Абсолютный путь
open("https://google.com");

// Относительный путь
open("/customer/orders");

// Прохождение браузерных окон авторизации
open("/", AuthenticationType.BASIC,
new BasicAuthCredentials("user", "password"));
````

### Кнопки навигации:
````java
// Кнопка назад
Selenide.back();

// Кнопка обновить страницу
Selenide.refresh();
````

### Очистка данных:
````java
// Очистка файлов куки
Selenide.clearBrowserCookies();

// Очистка Local Storage
Selenide.clearBrowserLocalStorage();

// Очистка Session Storage.
executeJavaScript("sessionStorage.clear();");
// После обновить страницу командой Selenide.refresh();

// Просмотр кук - DevTools, Application, Storage, Local Storage, Session Storage.
````

### Браузерные всплывающие окна (alert):
````java
// Подтверждение во всплывающих окнах
Selenide.confirm();

// Отмена во всплывающих окнах
Selenide.dismiss();
````

### Управление окнами (вкладками):
````java
// Закрыть активную вкладку
Selenide.closeWindow();

// Закрыть все вкладки (браузер, ожидаемо, тоже закроется)
Selenide.closeWebDriver();
````

### Переключение между фреймами страницы:
````java
// Переход во фрейм по имени или селктору
Selenide.switchTo().frame("new");

// Переход во фрейм по умолчанию 
Selenide.switchTo().defaultContent();
````

````java
Selenide.switchTo().window("The Internet"); // Перемещаться по окнам в браузере.
````

````java
// Создаем куки. Какие ставить куки, помогут разработчики.
// open("http://testserver/empty.txt") - сначало открываем любой файл на нашем сервере.
var cookie = new Cookie("foo", "bar");
WebDriverRunner.getWebDriver().manage().addCookie(cookie); // Установка кук.
// После обновить страницу командой Selenide.refresh(); - опционально.
// open("http://testserver/recommendation") - открывает то, что хотели проверить.
````
Selenide запускает браузер в режиме инкогнито по умолчанию.

# Селекторы
Селекторы обозначаются с помощью символа доллара — $. Но в языке Kotlin этот символ зарезервирован для внутреннего использования, поэтому вместо него следует использовать ключевое слово element.

### Поиск элемента по селектору:
````java
$("div").click(); // Первый вариант
element("div").click(); // Второй вариант

// Если нужен не первый n-ый div, то можно указать его индекс
// Важно помнить, что нумерация начинается с нуля
// В примере найдется третий div
$("div", 2).click();
````

### Поиск элемента по икспасу:
````java
$x("//h1/div").click(); // Вариант первый.
$(byXpath("//h1/div")).click(); // Вариант второй.
// $(‘div’).$x(‘.//h1’); Поиск по селектору, после по икспасу.
````

### Поиск по тексту:
````java
// Поиск по полной строке (полное совпадение)
$(byText("full text")).click();

// Поиск по подстроке (частиное совпаление)
$(withText("ull tex")).click();
````

### Поиск по тегу и тексту одновременно:
````java
// Полная строка (полное совпадение)
$(byTagAndText("div","full text"));

// Подстрока (частиное совпаление)
$(withTagAndText("div","ull text"));
````

### Поиск по DOM:
````java
// По родителю
$("").parent();

// Поиск по дочерним элементам (сверху вниз)
$("").sibling(1);

// То же, что и sibling, но снизу вверх
$("").preceding(1);

// Ищет предков элемента снизу вверх
$("").closest("div");

// То же, что и closest
$("").ancestor("div");

// Поиск по псевдоселекторам
$("div:last-child");
````

````java
$("div").$("h1").find(byText("abc")).click(); // Поиск div, внутри div ищем h1, внутри
// h1 ищем текст "abc" find = $. Find работает только со второго поиска по элементу.
````

### Опциональный поиск:

Используется очень редко
````java
// Поиск по атрибуту – квадратные скобки
$(byAttribute("abc", "x")).click(); // Вариант первый
$("[abc=x]").click(); // Вариант второй

// Поиск по ID элемента – решетка
$(byId("mytext")).click(); // Вариант первый
$("#mytext").click(); // Вариант второй

// Поиск по Class Name – точка
$(byClassName("red")).click(); // Вариант первый
$(".red").click(); // Вариант второй
````

# Команды

### Мышка:
````java
// Клик по элементу
$("").click();

// Двойной клик
$("").doubleClick();

// Клик ПКМ
$("").contextClick();

// Подвести курсор
$("").hover();
````

### Текстовые поля:
````java
// Очистить поле и поместить значение
$("").setValue("text");

// Не очищать поле и поместить значение. Добавит текст к существующему
$("").append("text");

// Очистить поле (не всегда срабатывает). Есть фреймворки, где команда не работает
$("").clear();

// Очистить поле путем помещения в поле пустой строки. Аналог clear (говорят что нет разницы)
$("").setValue("");
````

### Клавиши:
````java
// Нажать клавишу на конкретном элементе
$("div").sendKeys("c");

// Нажать клавишу во всем приложении, без каких-либо привязок к элементу
actions().sendKeys("c").perform();

// Последовательности клавиш. Комбинация клавиш (Ctrl + F)
actions().sendKeys(Keys.chord(Keys.CONTROL, "f")).perform();

// Пример применения клавиши по тегу html (вся страница)
$("html").sendKeys(Keys.chord(Keys.CONTROL, "f"));
````

Часто используют
````java
// Нажать Enter
$("").pressEnter();

// Нажать Esc
$("").pressEscape();

// Нажать Tab
$("").pressTab();
````

### Сложные комбинации: Начинаются команды методом actions(), а заканчиваются perform()
````java
// Подвинуть курсор к элементу, кликнуть и держать, передвинуть по X и Y, отпустить кнопку мыши
actions().moveToElement($("div")).clickAndHold().moveByOffset(300, 200).release().perform();
````

Старые html экшены. С современными фреймворками может не работать
````java
// Дропдауны
$("").selectOption("dropdown_option");

// Радиобокс
$("").selectRadio("radio_options"); 
````

## Проверки
````java
$("").shouldBe(visible); // Элемент должен быть видимым. Вариант первый
$("").shouldNotBe(visible); // Элемент не должен быть видимым. Вариант первый
$("").shouldHave(text("abc")); // Элемент должен быть видимым. Вариант второй
$("").shouldNotHave(text("abc")); // Элемент не должен быть видимым. Вариант второй
$("").should(appear); // Элемент должен быть видимым. Вариант третий
$("").shouldNot(appear); // Элемент не должен быть видимым. Вариант третий
````

### Увеличить или уменьшить timeout (таймаут). Кастомная настройка таймаута
````java
$("").shouldBe(visible, Duration.ofSeconds(30)); // Элемент должен быть видимым в течении 30 секунд
````

# Условия проверок
Внутри каждого assert должно быть условия
````java
// 80% всех проверок это $("").shouldBe(visible); или $("").shouldHave(text("abc"));
// Видимый/скрытый элемент
$("").shouldBe(visible); // Элемент должен быть видимым
$("").shouldBe(hidden); // Элемент должен быть скрыт
````

### Условия содержания текста
````java
// Поиск по подстроке (частичное совпадение). Без регистра
$("").shouldHave(text("abc"));

// Поиск полного совпадения. Без регистра
$("").shouldHave(exactText("abc"));

// Поиск с учетом регистра по подстроке (частичное совпадение)
$("").shouldHave(textCaseSensitive("abc"));

// Поиск полного совпадения с учетом регистра
$("").shouldHave(exactTextCaseSensitive("abc"));

// Сложные условия
$("").should(matchText("[0-9]abc$")); // Например проверка почты. Используется редко.
````

### CSS
````java
// Проверка класса
$("").shouldHave(cssClass("red"));

// Проверка элемента
$("").shouldHave(cssValue("font-size", "12")); // Настоящее свойство элемента (Elements, Computed)
````

````java
// Поля ввода
$("").shouldHave(value("25")); // Проверка текста. Ввели в поисковую строку тектст и проверили что оно совпадает (не полностью)
$("").shouldHave(exactValue("25")); // Проверка текста. Ввели в поисковую строку тектст и проверили что оно совпадает (полностью)
$("").shouldBe(empty); // Поле пустое
````

````java
// Атрибуты
$("").shouldHave(attribute("disabled")); // Поиск элемента по атрибутам
$("").shouldHave(attribute("name", "example")); // Поиск элемента по значению
$("").shouldHave(attributeMatching("name", "[0-9]abc$")); // Проверка атрибута сложно. Используется редко
````

````java
// Чекбоксы/Checkbox
$("").shouldBe(checked); // Стоит галочка
$("").shouldNotBe(checked); // Не стоит галочка
````

````java
// Проверка нахождения элемента в DOM, при этом пользователь может его не видеть
$("").should(exist); // Используется редко
````

````java
// Поиск осуществляется по атрибуту. Может не работать. Используется редко
$("").shouldBe(disabled); // Кнопка (button) не кликабельна
$("").shouldBe(enabled); // Кнопка (button) кликабельна
````

# Коллекции

Коллекции обозначаются двойным знаком доллара — `$$`. В Kotlin следует использовать ключевое слово `elements`.

### Пример:
````java
$$("div"); // Поиск по селектору. Ничего не делает. Должно быть действие, например: $$("div").first().click();
elements("div"); // Поиск по икспасу
````

### Фильтрации:
````java
$$("div").filterBy(text("123")).shouldHave(size(1)); // Поиск удовлетворяющий условия (filterBy)
$$("div").excludeWith(text("123")).shouldHave(size(1)); // Поиск не удовлетворяющий условия (excludeWith). Выбрасывает все элементы "123"
````

### Навигация:
````java
// Первый
$$("div").first().click(); // Сводит из коллекции в один элемент. Поиск первого элемента. Вариант первый
elements("div").first().click(); // Вариант второй.

// Последний
$$("div").last().click(); // Сводит из коллекции в один элемент. Поиск последнего элемента

// По номеру
$$("div").get(1).click(); // Поиск второго элемента. Начинается с 0. Вариант первый

$("div", 1).click(); // Вариант второй.
$$("div").findBy(text("123")).click(); // Ищет первый элемент. Комбинация filterBy и first.
````

### Проверки коллекций. Assertions:
````java
// Размер
$$("").shouldHave(size(0)); // Проверка размера. В данном примере коллекция пустая
// То же, что выше
$$("").shouldBe(CollectionCondition.empty); // Проверка размера
````

````java
// Подтекст
$$("").shouldHave(texts("Alfa", "Beta", "Gamma"));
// Текст с полным соответствием
$$("").shouldHave(exactTexts("Alfa", "Beta", "Gamma"));
````

````java
// Текст без учета порядка
$$("").shouldHave(textsInAnyOrder("Beta", "Gamma", "Alfa"));
$$("").shouldHave(exactTextsCaseSensitiveInAnyOrder("Beta", "Gamma", "Alfa"));
````

````java
// Поиск конкретного элемента по тексту
$$("").shouldHave(itemWithText("Gamma"));
````

````java
// Проверка размера коллекции
$$("").shouldHave(sizeGreaterThan(0)); // Размер коллекции больше 0
$$("").shouldHave(sizeGreaterThanOrEqual(1)); // Размер коллекции больше 1
$$("").shouldHave(sizeLessThan(3)); // Размер коллекции меньше 3
$$("").shouldHave(sizeLessThanOrEqual(2)); // Размер коллекции меньше 2
````

# JavaScript
````java
// Запуск
executeJavaScript("alert('selenide')");

// Запуск с аргументами
executeJavaScript("alert(arguments[0]+arguments[1])", "abc", 12);

// Запуск с аргументами и возвращением результата
long fortytwo = executeJavaScript("return arguments[0]*arguments[1];", 6, 7);
````

# Файлы
Стоит помнить про обработку ошибок, иначе могут быт непредвиденные результаты выполнения теста.
````java
// Скачать файл, работает только с <a href="..">
File file1 = $("a.fileLink").download();

// Скачать файл, более простой вариант. Работает всегда. Чаще используют. Возможно проблемы с Grid/Selenoid.
File file2 = $("div").download(DownloadOptions.using(FileDownloadMode.FOLDER));
````

````java
// Загрузить файл
File file = new File("src/test/resources/readme.txt");
$("#file-upload").uploadFile(file); // Загрузка файла на сайт

// Вариант второй
$("#file-upload").uploadFromClasspath("readme.txt");

// Файлы обычно на сайт не загружаются сами
// И загрузку надо подтвердить нажатием кнопки
$("uploadButton").click();
````