Сидел я однажды на региональном Аниме-фесте, смотрел как на проекторе мышкой таскают файлы и осознал что хватит это терпеть!

Миру нужна система, через которую можно одновременно показывать картинку на втором мониторе (задник), включать аудио и при необходимости включать видео вместо картинки.

На одном компьютере.

В одном приложении.

Приехал домой и начал писать **Fest Engine**. Давно хотел что-нибудь полезное назвать **Fest Engine**. Вроде норм звучит.

## Как было раньше у меня:

- AIMP для аудио на первом компе/операторе без проектора.
- Cosplay2 Timer для обратного отсчета на втором компе, который на проекторе.
- FastStone для задников на втором компе/операторе.
- Картинка феста на рабочем столе, скрытая панель задач. Копия картинки феста в FastStone, чтобы включать ее не сворачивая FastStone
- VLC для видео хитро настроенный автоматически разворачиваться на втором мониторе (обязательно нужно его закрыть на втором мониторе чтобы он именно там в следующий раз открылся при открытии файла) .
- При открытии файла из папки, чтобы добраться до которой надо убрать фокус с FastStone.

Как это в других лучше не знать... Мало кто отключает системные звуки даже, а мышка бегающая по проектору и интерфейсы винды -- это в порядке вещей.

# Как это теперь:

![так](scr.png)


## Как это работает?

- Создаём скрипт запуска на основе [Start-Sample-Fest.bat](Debug-Sample-Fest.bat). Регулярное выражение `filename_re` должно покрывать всё что от пробела после id до точки расширения.
   В самом простом виде оно выглядит так: `(?P<name>.*)`. Если у вас есть чёткая структура имён файлов, вы легко её распарсите в столбцы таблицы (названия групп образуют столбцы таблицы).
- Запускаем FestEngine и тестируем что всё работает.
- Приходим на фест (с тем же ноутом).
- Указываем какой из мониторов -- проектор.

    ![](settings.png)

- Выбираем нужную строчку, ждём объявления участника, топим **F1** -- Задник на проектор пошёл.
- Выходит участник, топим **F2** -- Звук пошёл. Если видео а не звук, то видео тоже пошло вместо задника.
- Повторяем пока есть участники.
- Профит, все любят ваш фест! Только не забудьте отслушать все материалы на предмет низкого битрейта и отсмотреть все видосы **именно на том компе который будет на фесте**. 

# На чём это зиждется?

- **Python 2** -- семый простой язык в мире, в коде разберётся даже школоло
- **wxPython** -- мощнее чем tcl/tk и более лампово чем Qt (ну не люблю я Qt)
- **VLC Python bindings** -- оказывается можно показывать видео через VLC не запуская VLC (но устанвоить всё-таки надо)

Соответственно: Linux, Windows и MacOS нативно поддерживаются сразу из коробки

# Какие ещё киллер-фичи?

- [#4](https://github.com/Himura2la/FestEngine/issues/4): Если в поле комента вписать какой-нибудь ID (например `">183 maybe"`), строчка сдублируется в нужном месте. Это удобно если участника паренесли и надо не забыть об этом. Такие строки можно удалять и обновлять комент в них изменяя комент в исходной.
- [#2](https://github.com/Himura2la/FestEngine/issues/2): Офигительный поиск. Самый минималистичный, быстрый и удобный из возможных. Есть только одно текстовое поле -- туда можно вводить что угодно, по мере ввода таблица фильтруется. Выбираем что нужно в отфильтрованной, кликаем правой кнопкой по полю поиска и переходим в полную таблицу! Чтобы не забыть выйти из фильтра, фон отфильтрованной таблицы меняет цвет.  

# В планах:

- Нарисовать замену [Cosplay2 Timer](https://vk.com/cosplay2ru?w=wall-64774987_200)
- Раскрашивать строки (подсвечивать ВЫРВИГЛАЗНО КРОВАВО КРАСНЫМ ЧТОБ БЫЛО ЗАМЕТНО С АЛЬФА ЦЕНТАВРЫ строки в которых не все файлы найдены)
- F3 для музычки на уход участника из отдельной папки.
- F4 для музычки интермедий из отдельной папки.
- Запилить все настройки в GUI, организовать их хранение и автозагрузку.
- Сделать бранч на mplayer, VLC Python bindings всё-таки сыроват.

[Подробности](https://github.com/Himura2la/FestEngine/issues)

Если ты чувствуешь в себе силу что-нибудь из этого запилить, будешь няшкой...


# Установка на Debian-based системы

[Официальный гайдъ по установке wxPython](https://github.com/wxWidgets/Phoenix/blob/master/README.rst)

Возможно не стоит ставить из pip, он у меня билдился 3.5 часа а потом вылетел с ошибкой.

```sh
sudo apt install git python2.7-dev python-wxgtk3.0-dev vlc -y
git clone --recursive https://github.com/Himura2la/FestEngine.git
cd python-vlc
sudo python setup.py install
cd ..
python main.py # pass arguments to configure your paths
```
