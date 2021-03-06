# Общая информация -- скрипты

В данной папке есть три скрипта:
1. Daily_parsing
2. Weekly_parsing
3. Make_weekly_charts


Скрипт 1 нужно выполнять каждый день с интервалом в сутки.
Каждое раннее утро пятницы нужно выполнять все три скрипта -- в порядке, указанном выше. 
Такое время запуска скриптов связано с тем, что spotify и youtube, два единственных ресурса с собственными недельными чартами, считают неделей именно интервал пятница-четверг. Поэтому логично синхронизировать все чарты с ними.

# Общая информация -- файлы

В данной папке есть файлы следующих типов:
1. all_название стриминга.csv - это базы данных, куда сохраняется вся история парсингов ежедневных (или еженедельных для спотифая и ютуба) чартов
2. all_название стриминга_weekly.csv - это базы данных, куда (для всех платформ кроме ютуба и спотифая) сохраняются все "искусственные" еженедельные чарты
3. current_название стриминга_html.html - это актуальная версия еженедельного чарта для данного стриминга в формате html
4. current_full_html.html - это конечный html файл, в котором собраны все файлы предыдущего типа. "предназначен" для просмотра всего в одном месте в браузере

# Подробнее о каждом скрипте

1. Daily_parsing
- должен запускаться каждый день один раз в сутки
- осуществляет парсинг ежедневных чартов
-- через API: Deezer
-- через requests: Apple Music, Yandex
-- через selenium: VK

- на выходе:
-- обновляет уже хранящиеся данные в csv файлах каждого стриминга, лежащие в корневой директории
-- all_deezer.csv, all_apple.csv, all_yandex.csv, all_vk.csv

-----------------

2. Weekly_parsing
- осуществляет парсинг еженедельных чартов
-- через requests: Spotify
-- через selenium: Youtube
-- -- внимание: парсится именно чарт Top Tracks, т.к. он уже включает в себя Top Music Videos (см. подробнее https://support.google.com/youtube/answer/9014376?hl=en)

- должен запускаться каждую неделю один раз в неделю
-- и Youtube, и spotify начинают неделю в пятницу и заканчивают в четверг
-- поэтому запускать данный скрипт надо ранним утром в пятницу

- на выходе:
-- обновляет уже хранящиеся данные в csv файлах каждого стриминга, лежащие в корневой директории
----  all_spotify.csv, all_youtube.csv
-- сохраняет html файл со свежим чартом прошедшей недели для обоих стримингов
---- current_youtube_html.html, current_spotify_html.html

------------------

3. Make_weekly_charts

- выдает еженедельные чарты стримингов, усредняя ежедневные чарты за 7 дней 
-- стриминги: Apple Music, VK, Deezer, Yandex
- должен запускаться один раз в неделю ранним утром пятницы после Weekly_parsing.py

-соединяет получающиеся чарты в единый html файл для публикации на сайте (включая "настоящие" еженедельные чарты)

-на выходе:
- обновляет csv файлы с соответствующими еженедельными чартами 4-x стримингов
-- all_vk_weekly.csv, и т.д.
- сохраняет в корневую директорию html файлы с новыми еженедельными чартами
-- current_vk_weekly.html и т.д.
- сохраняет в корневую директорию итоговый html файл, состоящий из всех html чартов недели, соединенных друг с другом 
-- current_full_html.html


