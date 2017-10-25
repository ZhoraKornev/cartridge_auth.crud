Simple CRUD system based on Codeigniter using Ajax,Bootstrap,Models and MySQL // Простая система учёта техники на базе Codeigniter с системой авторизации
=============================

Данная система учёта была написана для управления базой картриджей.
Основные функции: 
- авторизация пользователей в системе
- управление уровнем доступа пользователей
- главная страница
- добавление,редактирование,удаление элементов.
- ведение журнала изменений и лога основных событий.
- русский интерфейс управления//ведения лога на русском языке

Коментарии в коде почти отсутсвуют 

![screenshot of sample](http://forum.norma4.net.ua/photoplog/images/9110/1_main.png)

> За основу взят фреймворк  [Codeigniter версии 4](https://codeigniter.com/)
  также в качестве приемлемой визуальной составляющей использован  [Bootstrap 4](http://getbootstrap.com/) и для удобства сортировки использован [DataTables ](https://datatables.net/).

Установка 
------------

Удобнее всего будет скачать архивом и распаковать.
В корне папки вы также найдете файлы базы данных с таблицами.
Установка мало чем отличается от установки CodeIgniter

Инструкции по установке:

Установка CodeIgniter проходит в четыре этапа:

    Распакуйте архив.
    Загрузите файлы и папки CodeIgniter на ваш сервер. Обычно файл index.php находится в корневой папке сайта.
    Откройте application/config/config.php файл в текстовом редакторе и установите основной (base) URL.Если вы собираетесь использовать шифрование или сессии, назначьте ключ шифрования.
    Если вы намериваетесь использовать базу данных, откройте application/config/database.php файл в текстовом редакторе и установите настройки вашей базы данных.
    
В конце всех проделаных операций вам нужно будет сконфигурировать базовый адрес,ввести данные для доступа к БД.
Файлы баз данных лежат в корне папки 

### Список файлов с описанием их функций

Проект по факту состоит из файлов контроллеров по одному на каждую функцию - один контроллер отвечает за работу с картриджами,второй - за авторизацию,третий - управляет данными пользователей,
четвертый - своибразная стартовая страница.
Под каждый контроллер свой вьювер.
Также в проект включёна папка assets в которой лежит Bootstrap,datatables,jquery.



```php
Название файла        | Содержание файла
----------------------|----------------------
phpstorm.php          | Содержит синтаксис для удобства работы с Codeigniter
assets                | Папка в которой лежит локальный Bootstrap,datatables,jquery.
Cartridge.php         | Основной контроллер управления страницами
cartridge_model.php   | Основной файл модель,основная функция - работа с базой данных
add_cartridge.php     | Файл представления для ввода даных о новом элементе
cartridge_details.php | Файл представления который строит основную таблицу с отображением всех элементов
edit_details.php      | Файл представления для редактирования даных о элементе
story_of_element.php  | Файл представления страницы истории
cartridgedb.sql       | Подготовленный файл базы данных элементов с коментариями каждого поля
story.sql             | Подготовленный файл базы данных истории с коментариями каждого поля
user_login.sql




----------------------|-----------------------
```



Требования
------------

Стандартные требования к Codeigniter

        MySQL (5.1+) via the mysql (deprecated), mysqli иpdo драйвера
        Oracle via the oci8 and pdo drivers
        PostgreSQL via the postgre  and pdo drivers
        MS SQL via the mssql, sqlsrv (только версии 2005 и выше) и pdo драйвера
        SQLite via the sqlite (версии 2), sqlite3 (версии 3) и pdo драйвера
        CUBRID via the cubrid и pdo драйвера
        Interbase/Firebird via the ibase и pdo драйвера
        ODBC via the odbc и pdo драйвера (вам следует знать что ODBC актуальна на абстрактном уровне)

Описание главной страницы 
------------

Здесь описаны значения которые отображаются в таблице/списке
Вся информация подгружается с БД.
При отсутсвии элементов в БД будет выведена надпись ***В базе данных нет записей***
[![презентация](http://forum.norma4.net.ua/photoplog/images/9110/1_presentation.png)](https://youtu.be/K_2Isi3j_Mk)
       
        Название столбца| Содержание столбца
        ----------------|-----------------------------------------------------------------------------------------------------------------------------------------------
        id              | уникальный номер элемента - берется из БД.
        Отдел-владелец  | где установлен картридж или кому он принадлежит по инвентарной базе
        Бренд           | фирма изготовитель картриджа
        Марка           | марка картриджа присвоенная производителем 	
        Код             | уникальный код картриджа//инвентраный номер
        Кто заправил    | сервисный центр производивший ремонт/заправку/восстановление
        Состояние       | техническое сотояние картриджа в работе или выведен из работы
        Примечание      | коментарии которые объясняют ту или иную ситуацию с картриджем
        Вес до          | вес до отправки в сервисный центр
        Вес после       | вес после заправки 	
        Разница в весе  | разница в весе рассчитывается авотоматически при обращении к элементу,информация об этом значении не хранится в БД
        Дата ухода      | когда был отправлен в сервисный центр 	
        Дата прихода    | когда был получен из сервисного центра 		
        Изменить        | кнопка редактирования информации о элементе 	
        Удалить         | кнопка удалить элемент из базы данных 	
        История         | кнопка перенаправляет на страницу журнала изменений произведеных с жлементом
        ВС              | в сервисе(1) или нет(0) рассчитывается автоматически когда поле Дата прихода меньше поля Дата ухода тогда присваивается значение 1 - в сервисе.
        -----------------------------------------------------------------------------------------------------------------------------------------------------------------
        


  

Описание страницы истории элемента
------------

Здесь описаны значения которые отображаются в таблице/списке на странице истории  элемента
Вся информация подгружается с БД.



![screenshot of sample](http://forum.norma4.net.ua/photoplog/images/9110/3_Screenshot-2017-10-23___________________.png)






     Название столбца        | Содержание столбца
     ------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------
     id                      | уникальный номер записи - берется из БД.
     Отдел-владелец          | где установлен картридж или кому он принадлежит по инвентарной базе
     Кто заправил            | сервисный центр производивший ремонт/заправку/восстановление
     Состояние               | техническое сотояние картриджа в работе или выведен из работы
     Вес до                  | вес до отправки в сервисный центр
     Вес после               | вес после заправки 	
     Дата ухода              | когда был отправлен в сервисный центр 	
     Дата прихода            | когда был получен из сервисного центра 		
     Дата внесения изменений | Дата внесения изменений в историю элемента или первого обращения к странице историй
   	 ------------------------------------------------------------------------------------------------------------------------------------------------------------------------  
   	 ***Примечание//Коментарии***
   	 Поле которое подгружается из БД cartridge/cartridgedb 
   	 ***Текстовый лог в котором отображаются изменения происходившие в значениях элемента***
   	 Поле которое подгружается из БД cartridge/story выбирается по старшему индексу id в БД для отображения самых последний изменений 
   	 - содержит краткую историю основных изменений: а именно пишет только ключи и информацию которая в этих ключах менялась  
   	 ***Полный текстовый журнал изменений сюда выводится информация о значениях. Было ---- Стало***
   	 Тестовое поле которое подгружается из БД cartridge/story выбирается по старшему индексу id в БД для отображения самых последний изменений.
   	 При каждом редактировании и смене данных пишет все данные до редактирования с данными которые получились после редактирования.
          	

Другие версии и будущие изменения
-----------

В следующей версии  уже реализована система регистрации и авторизации пользователей.
Эта версия не безопасна в плане валидации вводимых данных, последующие версии этим не страдают.


Оставляйте пожелания и исправления в ветке коментирования кода.

Для связи - я в [linkedin ](https://www.linkedin.com/in/сергей-обухов-703426140/).
 