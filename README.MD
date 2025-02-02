# Работа с Evernote

Данные скрипты помогут настроить работу с API разработчика Evernote.

- `list_notebooks.py` - выводит названия и ID блокнотов (необходимо для настроек).
- `add_note2journal.py` - копирует шаблонную запись в выбранный блокнот. 
- `dump_inbox.py` - выводит содержимое блокнота под входящие имейлы.

## Установка

Для работы требуется python версии 3.

Настройте  [переменные окружения ](https://docs.python-guide.org/dev/virtualenvs/) для изоляции проекта.

Установите необходмые пакеты `pip`.

```
> pip install -r requirements.txt
```

### Переменные окружения

Создайте пустой файл `.env`.

Создайте аккаунт [в песочнице](https://sandbox.evernote.com).
Получите [токен разработчика](https://sandbox.evernote.com/api/DeveloperToken.action)

`EVERNOTE_PERSONAL_TOKEN` - токен разработчика.

`INBOX_NOTEBOOK_GUID` - блокнот по умолчанию, на который приходит электронная почта.
Создайте блокнот, нажмите "i" и пометьте блокнот "по умолчанию". 
Зайдите в [настройки аккаунта](https://sandbox.evernote.com/Settings.action) и внизу скопируйте email с которого письма будут попадать в блокнот по умолчанию.
Он выглядит как **ххх.ххх@sandbox.evernote.com** 
Отправьте на этот имейл себе тестовое письмо.

Создайте еще один блокнот и шаблонную запись в нем.
Запустите скрипт.
```
python list_notebooks.py
```

Скопируйте оттуда GUID блокнота, в который вы планируете копировать шаблонные записи.

`JOURNAL_NOTEBOOK_GUID` - полученный в предудущем шаге GUID скопируйте в эту переменную файла '.env'.
Можно так же найти этот GUID в адресной строке после буквы 'b'.
`JOURNAL_TEMPLATE_NOTE_GUID` - GUID шаблонной записи, можно найти в строчке адреса после буквы 'n'.


Таким образом, файл '.env' будет иметь такой вид:
```
EVERNOTE_PERSONAL_TOKEN = 'токен разработчика'

JOURNAL_NOTEBOOK_GUID = 'GUID полученный через list_notebooks.py'
JOURNAL_TEMPLATE_NOTE_GUID = 'Шаблонная запись'
INBOX_NOTEBOOK_GUID = 'Ящик для имейлов по умолчанию'
INBOX_NOTES_COUNT = Количество записей из блокнота по умолчанию для вывода. По умолчанию - 10
```

## Как использовать


```
> python list_notebooks.py
```
выводит названия и ID блокнотов (необходимо для настроек).

```
> python add_note2journal.py
```

копирует шаблонную запись в выбранный блокнот.
Может принимать аргументы на вход:

- Дату в формате: `%Y-%m-%d`
- Можно задать дельту дате в формате +Х - посчитается дата и день недели.
- Если не передавать аргумент, подставит текущую дату.


```
> python3 add_note2journal.py 2022-05-28
Title Context is:
{
    "date": "2022-05-28", 
    "dow": "Суббота"
}
Note created: 2022-05-28 Суббота
Done

> python3 add_note2journal.py +4        
Title Context is:
{
    "date": "2022-06-01",
    "dow": "среда"
}
Note created: Королевская ватрушка, рецепт
```

Вывести имейлы из блокнота по умолчанию:

```
> python3 dump_inbox.py
```

По умолчанию выведется 10 записей. Параметр можно менять в файле '.env'

#  Цели проекта

Проект создан в рамках образовательного курса [dvmn.org](https://dvmn.org/)