Комментарии по запуску через Docker:

1. Для начала нужно скачать проект `git clone https://github.com/Ioloman/KINETICA_test_task.git`. Если Вы ранее использовали Laravel Sail и у Вас в Docker есть том sailmysql, то это название необходимо поменять в исходном файле. Объявляется он в файле docker-compose.yml на строке 78 и используется на строке 30.
2. Далее нужно установить зависимости. Самый удобный, на мой взгляд, способ - запустить контейнеры `docker-compose up -d` и скачать зависимости композером контейнера `docker exec -it <app_container> composer update`. Скорее всего названием контейнера с приложением <app_container> будет "kinetica_test_task_laravel.test_1".
3. Далее можно использовать Sail. Нужно перезагрузить контейнеры: `docker-compose down` и `./vendor/bin/sail up -d`. Последний шаг - миграция `./vendor/bin/sail artisan migrate`. Сайт должен быть доступен на localhost.
4. Если Sail не работает. Перезагрузка контейнеров - `docker-compose restart` и миграция - `docker exec -it <app_container> php artisan migrate`

В проекте использовались Laravel 8.40, Bootstrap 5, jQuery, tinyMCE как редактор текста, сборка - laravel-mix (API для webpack). Для разработки применялись Docker Desktop + WSL 2 + Visual Code. По времени потрачено примерно 4 вечера.
Есть регистрация, вход. После входа перебрасывает в личный кабинет. Там список постов пользователя. На главной странице есть кнопка "Создать запись". По нажатию на неё выскакивает модальное окно с текстовым редактором и кнопкой "Опубликовать". Также на главной странице список постов по 10 штук на странице. У постов выведены 3 последних комментария, если имеются. По названию поста можно перейти на отдельную страницу поста, там вся информация, все комментарии, можно написать комментарий. Изменение и удаление реализовывать не стал. Добавление постов и комментариев реализовано с помощью ajax + jQuery.
