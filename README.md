# databases-101

_Добро пожаловать в «Databases 101» — это подробные заметки, охватывающие ключевые концепции баз данных от начального до среднего уровня. Материалы подойдут как новичкам, стремящимся получить прочную базу, так и более опытным пользователям, желающим освежить свои знания. Заметки охватывают такие темы, как SQL-запросы, оптимизация и производительность, транзакции и согласованность данных, и многое другое. Некоторые темы сгруппированы логически для лучшего понимания, а план, представленный ниже, поможет легко ориентироваться в представленных материалах._

## План

<details>
  <summary>Открыть полный план</summary>

### Введение в базы данных

- [Базы данных и СУБД](#базы-данных-и-субд) // TBD
- [ETL-процессы](#etl-процессы) // TBD
- [ER-диаграмма](#er-диаграмма) // TBD
- [Ключи](#ключи) // TBD
- [Нормализация и денормализация форм](#нормализация-и-денормализация-форм) // TBD
- [Схемы "звезда" и "снежинка"](#схемы-звезда-и-снежинка) // TBD

### Основы SQL

- [T-SQL](#t-sql) // TBD
- [SELECT](#select) // TBD
- [Агрегатные функции](#агрегатные-функции) // TBD
- [WHERE и HAVING](#where-и-having) // TBD
- [CASE](#case) // TBD
- [Объединения таблиц](#объединения-таблиц) // TBD
- [Вложенные запросы](#вложенные-запросы) // TBD

### Расширенные возможности SQL

- [Функции](#функции) // TBD
- [Аналитические функции](#аналитические-функции) // TBD
- [Представления](#представления) // TBD
- [Хранимые процедуры](#хранимые-процедуры) // TBD
- [Триггеры](#триггеры) // TBD

### Оптимизация и производительность

- [EXPLAIN](#explain) // TBD
- [Индексы](#индексы) // TBD
- [Партицирование](#партицирование) // TBD
- [Шардинг](#шардинг) // TBD
- [Репликация](#репликация) // TBD
- [Масштабирование](#масштабирование) // TBD
- [Кэширования](#механизмы-кэширования) // TBD

### Транзакции и согласованность данных

- [Транзакции](#транзакции) // TBD
- [ACID](#acid) // TBD
- [Уровни изоляции транзакций](#уровни-изоляции-транзакций) // TBD
- [Аномалии](#аномалии) // TBD
- [Локи](#локи) // TBD
- [MVCC](#mvcc) // TBD
- [SELECT FOR UPDATE и SELECT FOR SHARE](#select-for-update-и-select-for-share) // TBD

### Безопасность

- [Управление доступом](#управление-доступом) // TBD
- [Шифрование данных](#шифрование-данных) // TBD
- [Аудит и журналирование](#аудит-и-журналирование) // TBD

### Дополнительная информация

- [Архитектура](#архитектура) // TBD
- [Теорема CAP](#теорема-cap)

### SQL на практике

- [Справочники](#справочники)
- [Практические задания](#практические-задания)

</details>

## Введение в базы данных

## Основы SQL

## Расширенные возможности SQL

## Транзакции и согласованность данных

## Безопасность

## Дополнительная информация

### Теорема CAP

<details>
<summary>Подробнее</summary>

**Теорема CAP** (известная также как **теорема Брюера**) — эвристическое утверждение о том, что в любой реализации распределённых вычислений возможно обеспечить не более двух из трёх следующих свойств:

- **согласованность данных** (англ. consistency) — во всех вычислительных узлах в один момент времени данные не противоречат друг другу;
- **доступность** (англ. availability) — любой запрос к распределённой системе завершается откликом, однако без гарантии, что ответы всех узлов системы совпадают;
- **устойчивость к фрагментации** (англ. partition tolerance) — расщепление распределённой системы на несколько изолированных секций не приводит к некорректности отклика от каждой из секций.

<img src="./img/CAP_diagram.png" width="400" style="display:block; margin: 0 auto;" alt="Теорема CAP">

_Концепция NoSQL, в рамках которой создаются распределённые нетранзакционные системы управления базами данных, зачастую использует этот принцип в качестве обоснования неизбежности отказа от согласованности данных. Однако многими учёными и практиками теорема CAP критикуется за вольность трактовки и даже недостоверность в том смысле, в котором она распространена в сообществе._

**Следствия**

С точки зрения теоремы CAP, распределённые системы вычислений в зависимости от пары практически поддерживаемых свойств из трёх возможных распадаются на три класса — **CA**, **CP**, **AP** (при этом в рамках одной программной системы могут быть реализованы стратегии обработки различных запросов с использованием различных систем вычислений).

- В системе вычислений **класса CA** во всех узлах данные согласованы и обеспечена доступность, при этом она жертвует устойчивостью к распаду на секции. Такие системы возможны на основе технологического программного обеспечения, поддерживающего транзакционность в смысле ACID, примерами реализации таких систем вычислений могут быть решения на основе кластерных систем управления базами данных или распределённая служба каталогов LDAP.
- Система вычислений **класса CP** в каждый момент обеспечивает целостный результат и способна функционировать в условиях распада, но достигает этого в ущерб доступности: может не выдавать отклик на запрос. Устойчивость к распаду на секции требует обеспечения дублирования изменений во всех узлах программной системы, реализующей данную систему вычислений, в связи с этим отмечается практическая целесообразность использования в таких системах распределённых пессимистических блокировок для сохранения целостности.
- В системе вычислений **класса AP** не гарантируется целостность, но при этом выполнены условия доступности и устойчивости к распаду на секции. Хотя реализации систем вычислений такого рода известны задолго до формулировки принципа CAP (например, распределённые веб-кэши или DNS), рост популярности решений с этим набором свойств связывается именно с распространением теоремы CAP. Так, большинство NoSQL-систем принципиально не гарантируют целостности данных, и ссылаются на теорему CAP как на мотив такого ограничения. Задачей при построении AP-систем становится обеспечение некоторого практически целесообразного уровня целостности данных, в этом смысле про AP-системы говорят как о «целостных в конечном итоге» (англ. eventually consistent) или как о «слабо целостных» (англ. weak consistent).

**BASE-архитектура**

Во второй половине 2000-х годов сформулирован подход к построению распределённых систем, в которых требования целостности и доступности выполнены не в полной мере, названый акронимом **BASE** (от англ. Basically Available, Soft-state, Eventually consistent — базовая доступность, неустойчивое состояние, согласованность в конечном счёте), при этом такой подход напрямую противопоставляется ACID.

- Под **базовой доступностью** подразумевается такой подход к проектированию приложения, чтобы сбой в некоторых узлах приводил к отказу в обслуживании только для незначительной части сессий при сохранении доступности в большинстве случаев.
- **Неустойчивое состояние** подразумевает возможность жертвовать долговременным хранением состояния сессий (таких как промежуточные результаты выборок, информация о навигации, контексте), при этом концентрируясь на фиксации обновлений только критичных операций.
- **Согласованности в конечном счёте**, трактующейся как возможность противоречивости данных в некоторых случаях, но при обеспечении согласования в практически обозримое время, посвящено значительное количество самостоятельных исследований.

_Больше информации с примерами систем можно найти тут [Всё, что вы не знали о CAP теореме](https://habr.com/ru/articles/328792/)_

</details>

## SQL на практике

### Справочники

<details>
<summary>Подробнее</summary>

#### EN

- [W3 Schools](https://www.w3schools.com/sql/default.asp)
- [SQL Problems and solutions](http://sql-tutorial.ru/en/content.html)

#### RU

- [Интерактивный курс по SQL](https://sql-academy.org/ru/guide)
- [Справочник по функциям SQL](https://sql-academy.org/ru/handbook)
- [SQL Задачи и решения](http://sql-tutorial.ru/ru/content.html)

</details>

### Практические задания

<details>
<summary>Подробнее</summary>

#### EN

- [W3 Schools Exercises](https://www.w3schools.com/sql/sql_exercises.asp)
- [SQLBolt: Interactive Tutorial](https://sqlbolt.com/)
- [SQL exercises](https://sql-ex.ru/learn_exercises.php)

#### RU

- [SQL тренажёр](https://sql-academy.org/ru/trainer)
- [Интерактивный тренажер по SQL](https://stepik.org/course/63054/info)
- [Упражнения по SQL](https://sql-ex.ru/learn_exercises.php?LN=1)

</details>
