# Передача контекста Customer Service

## Цель текущей задачи

Передать контекст учебного проекта в новую сессию Codex в IntelliJ IDEA. Текущий этап обучения посвящён Context Management. В этой сессии изучили репозиторий и согласовали предварительные решения для Customer Service. Реализацию пользователь пока отложил.

## Подтверждённое состояние проекта

- В репозитории минимальный Maven-проект `com.example:customer-service:0.0.1-SNAPSHOT`. В `pom.xml` заданы Java 21, Spring Boot 3.5.16, Spring MVC, Spring Data JPA, H2 в runtime scope и JUnit Jupiter через `spring-boot-starter-test`.
- В Java-коде есть точка входа `CustomerServiceApplication` и один тест `contextLoads` с `@SpringBootTest`. Модель клиента, repositories, сервисы, контроллеры и API ещё отсутствуют.
- Проектные инструкции находятся в корне, `src/main` и `src/test`. Перед работой проверь `AGENTS.override.md` и `AGENTS.md` в каждом каталоге по пути к целевому файлу и учти приоритет ближайших правил. Для production-кода заданы отдельные API DTO, constructor injection и транзакции на уровне сервисной операции. Для тестов используются JUnit Jupiter и синтетические данные.

## Предварительные архитектурные решения

Внутреннее кодовое название инициативы — **Project Blue Falcon**.

В сессии согласовали следующие решения. Все четыре пока имеют предварительный статус и ожидают реализации.

- Использовать `UUID` для идентификаторов клиентов.
- Удалять клиентов через Soft Delete.
- Использовать Optimistic Locking для конкурентных обновлений.
- Обеспечить уникальность email клиента без учёта регистра.

Правила повторного использования email после Soft Delete и способ сигнализировать о конфликте версий пока не согласованы.

## Выполненные действия

- Провели read-only обзор POM, Java-кода, теста, инструкций, `PROGRESS.md` и двух конспектов. Сверили состояние каркаса по файлам перед подготовкой handoff.
- На первом занятии создали каркас и провели статическое ревью. На втором проверили область действия вложенных `AGENTS.md` и приоритет `AGENTS.override.md`.
- В рамках передачи контекста добавили только этот документ. Commit и push не выполнялись.

## Незавершённые проверки и известные блокеры

- Работу перенесли с корпоративного MacBook на личный ноутбук с Windows. Наличие и версии Java, JDK и Maven, выбор JDK командой Maven, доступность сети и состояние Maven-кэша на Windows пока не проверены.
- На MacBook `mvn -o verify` на JDK 21 остановился до компиляции на попытке записи в Maven-кэш. В том же кэше отсутствовал как минимум `spring-boot-starter-data-jpa:3.5.16`. Состояние кэша и ограничения записи на Windows предстоит проверить отдельно.
- Компиляция, выполнение `contextLoads`, упаковка JAR и запуск приложения остаются неподтверждёнными.

## Следующие шаги

1. В PowerShell из корня проекта выполнить `java -version`, `javac -version` и `mvn -version`. Убедиться, что Maven использует JDK 21. При расхождении проверить `JAVA_HOME` и порядок каталогов в `PATH`.
2. Запустить `mvn verify` на JDK 21 в рамках разрешений новой сессии. Если доступ к зависимостям или кэшу заблокирован, зафиксировать фактическую причину. После успешной сборки запустить JAR, подтвердить старт встроенного веб-сервера и остановить приложение.
3. После разрешения на реализацию согласовать открытые вопросы по Soft Delete, email и конфликтам версий, затем подготовить план изменений и проверок. Следующие учебные темы после Context Management — Skills и Subagents.

## Ключевые файлы

- [AGENTS.md](AGENTS.md), [src/main/AGENTS.md](src/main/AGENTS.md), [src/test/AGENTS.md](src/test/AGENTS.md) — общий workflow и правила production-кода и тестов.
- [pom.xml](pom.xml) — версии, зависимости и плагины сборки.
- [CustomerServiceApplication.java](src/main/java/com/example/customerservice/CustomerServiceApplication.java) и [CustomerServiceApplicationTests.java](src/test/java/com/example/customerservice/CustomerServiceApplicationTests.java) — точка входа и тест загрузки контекста.
- [PROGRESS.md](PROGRESS.md), [занятие 1](training/lesson-01.md) и [занятие 2](training/lesson-02.md) — прогресс обучения, результаты проверки на macOS и эксперименты с инструкциями.
