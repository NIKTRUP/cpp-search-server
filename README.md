# cpp-search-server
Программа обеспечивает поиск документов по ключевым словам и ранжирование результатов по статистической мере TF-IDF. Поддерживает функциональность минус-слов и стоп-слов. Создание и обработка очереди запросов. Возможность работы в многопоточном режиме.

## Работа с классом поискового сервера:

Создание экземпляра класса SearchServer.В конструктор передаётся строка с стоп-словами, разделенными пробелами. Вместо строки можно передавать произвольный контейнер (с последовательным доступом к элементам с возможностью использования в for-range цикле)

### Обзор методов:
  1. Метод **AddDocument** добавляет документы для поиска. В метод передаётся id документа, статус, рейтинг, и сам документ в формате строки.
  2. Метод **MatchDocument** производит матчинг запроса и документа по id.
  3. Метод **RemoveDocument** производит удаление документа по id.
  4. Метод **GetWordFrequencies** возвращает все слова и их частоту встречаемости в документе по его id.
  5. Метод **GetDocumentCount** возвращает количество документов на сервере.
  6. Метод **FindTopDocuments** возвращает вектор документов, согласно соответствию переданным ключевым словам. Результаты отсортированы по статистической мере TF-IDF. Возможна дополнительная фильтрация документов по id, статусу и рейтингу. Метод реализован как в однопоточной так и в многпоточной версии.

### Обзор классов:
1. Класс **RequestQueue** реализует хранение истории запросов к поисковому серверу. При этом общее кол-во хранимых запросов не превышает заданного значения. При добавлении новых запросов - они замещают самые старые запросы в очереди.

2. Класс **Paginator** обеспечивает выдачу документов постранично.

### Обзор функций:
Функции **ProcessQueries** и **ProcessQueriesJoined** обеспечивают параллельное исполнение нескольких запросов к поисковой системе.

## Системные требования
Компилятор С++ с поддержкой стандарта C++17 или новее.
Для сборки многопоточных версий методов необходим Intel TBB.

## TODO:
Написать Cmake файл для сборки проекта. Сделать GUI с использованием QT для работы с поисковым сервером.
