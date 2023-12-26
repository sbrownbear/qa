
## BeforeAll
Метод будет запускаться перед всеми тестами (настройка окружения для всех тестов в этом классе)
``````Java
@BeforeAll
static void beforeAll() {
    // Some code
}
``````
## AfterAll
Метод запускатся после всех тестов (что-то почистить за собой)
``````Java
@AfterAll
static void afterAll() {
    // Some code
}
``````

## BeforeEach
Метод запускатся перед каждым тестом (подготовить тест к запуску)
``````Java
@BeforeEach
void beforeEach() {
    // Some code
}
``````

##  AfterEach
Метод запускатся после каждого теста (что-то почистить за собой)
``````Java
@AfterEach
void afterEach() {
    // Some code
}
``````

## Disabled
Аннотация, тест не воспроизодится. Причины: минорный баг (вставили id бага), функциональность немного изменилась/не актуальна
``````Java
@Disabled("Some comment")
void successfulTest() { 
    // Some code
}
``````

## DisplayName
Аннотация, позволяющая комментировать тесты. Интегрировано с Allure
``````Java
@DisplayName("Адрес https://selenide.org должен быть в выдаче гугла по запросу 'Selenide'")
void successfulTest() { 
    // Some code
}
``````

## Test
Аннотация - метка теста (не влияет на работу теста)
``````Java
@Test
void successfulTest() { 
    // Some code
}
``````

## Tag
Аннотация позволяющая оставлять любую метку (серьезность, приоритет, API-тест, UI-тест)
``````Java
@Tag("CRITICAL")
void successfulTest() { 
    // Some code
}
``````

## Tags
Аннотация позволяющая оставлять несколько меток (серьезность, приоритет, API-тест, UI-тест)
``````Java
@Tags({@Tag("BLOCKER"), @Tag("UI_TEST")})
void successfulTest() { 
    // Some code
}
``````
## ParameterizedTest
Аннотация @ParameterizedTest - параметризованные тесты. Необходимо, чтобы выполнить тест несколько раз, но с разными аргументами. Не нужно использовать аннотацию @Test, вместо этого в таких тестах используется только аннотация @ParameterizedTest.


## Flaky
Аннотация @Flaky - для нестабильных тестов

## Allure annotations

Пример статических аннотаций
``````Java
@Test
@Feature("Issue в репозитории")
@Story("Создание Issue")
@Owner("KonoplevSA")
@Severity(SeverityLevel.BLOCKER)
@Link(value = "Testing", url = "https://testing.github.com")
@DisplayName("Создание Issue для авторизации пользователя")
public void testStaticLabels() {
        // Some code
    }
``````

Пример динамических аннотаций
``````Java
@Test
public void testDynamicLabels() {
    Allure.getLifecycle().updateTestCase(t -> t.setName("Создание Issue для авторизации пользователя"));
    Allure.feature("Issue в репозитории");
    Allure.story("Создание Issue");
    Allure.label("Owner", "KonoplevSA");
    Allure.label("Severity", SeverityLevel.BLOCKER.value());
    Allure.link("Testing", "https://testing.github.com");
}
``````