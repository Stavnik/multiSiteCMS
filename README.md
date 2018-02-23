<p align="center">
    <a href="https://github.com/yiisoft" target="_blank">
        <img src="https://avatars0.githubusercontent.com/u/993323" height="100px">
    </a>
    <h1 align="center">Заготовка для простой CMS на основе Yii 2 Basic Template</h1>
</p>

Зависимости
------------
Минимальная версия php - 7.1, база данных - MySql

Особенности
------------
1. Данная CMS изначально спроектирована для работы с несколькими сайтами в рамках одного web приложения. Т.е. одна админ панель, и одна БД, для нескольких сайтов с похожим функционалом (multiSite).
2. Реализовано разделение на слои. Основной рабочий код в каталоге core. Репозитории работают только с БД, модели форм отвечают только за формы, сервисы работают с контроллерами. Вся логика приложения только в сервисах, которые или возвращают результат контроллеру, или выкидывают исключения.
3. В основе работы приложения лежит паттерн DI. Зависимости описаны в файле config/bootstrap/SetUp.php

Установка
------------
<code>composer create-project ale10257/multi-site-cms my-directory</code>

Начало работы
------------
1. В каталоге с приложением переименовать файл config/db-test.php в config/db.php, прописать параметры подключения к базе данных MySql, и последовательно выполнить команды:

   <code>php yii migrate</code>

   <code>php yii init</code>
   
   При инициализации приложения будет предложено ввести логин, пароль, email для суперпользователя с ролью root
   
2. Создать тестовый домен, например, test.loc, в качестве корневой директории прописать /path/your/application/web/startSite. После инициализации перейти по адресу: test.loc/admin/login, и залогиниться в админке.

Соглашение о константах
------------
Все web директории для сайтов расположены в каталоге web установленного приложения. Например, изначально в папке web есть директория startSite с демо данными. В каталоге web/startSite - единственная точка входа на сайт (и в админ панель, и на фронтэнд) - файл index.php. В данном файле объявлены две глобальные константы SITE_ROOT_NAME и UPLOAD_DIR: 

<code>defined('SITE_ROOT_NAME') or define('SITE_ROOT_NAME', 'startSite');</code>  
<code>defined('UPLOAD_DIR') or define('UPLOAD_DIR', 'uploads');</code>

Для корректной работы приложения следующие каталоги должны быть названы так же, как константа SITE_ROOT_NAME, (например, если вы присвоили значение test): 
1. Web каталог web/test должен существовать.
2. Конфигурационные файлы должно находиться в папке config/test
3. Контроллеры и представления должны находиться в папке sites/test

Константа UPLOAD_DIR определяет название каталога для загружаемых файлов. По умолчанию 'uploads'. Каталог uploads создается автоматически, при первой загрузке какого-либо файла в web директорию.

Как добавить еще один домен в приложение
------------

В каталоге с приложением выполнить команду:

<code>php yii create-domain</code>

Вам будет предложено определить значение константы SITE_ROOT_NAME и имя приложения (домена) - Application Name.

Предположим, что вы определили значение константы SITE_ROOT_NAME как test.

Результат работы команды php yii create-domain:

1. В папке config приложения будет создан каталог config/test
2. В папке sites приложения будет создан каталог sites/test
2. В папке web приложения будет создан каталог web/test

Также необходимо создать новый домен, прописать корневую директорию (/path/your/application/web/test) для созданного домена в вашем web сервере (apache, или ngnix), и перезапустить web сервер, например: sudo service apache2 restart.

Как удалить домен в приложении
------------

В каталоге с приложением выполнить команду:

<code>php yii delete-domain</code>

Вам будет предложено ввести значение константы SITE_ROOT_NAME.

Демо версия 23.02.18г. не работает. Работы на сервере.
------------

Демо версия приложения
------------

http://kulagin-alex.ru

Вход в админ панель управления сайтом: http://kulagin-alex.ru/admin/login

Login: demo

Password: 123456
