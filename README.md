![header](https://capsule-render.vercel.app/api?type=venom&height=300&color=gradient&text=MODHELPS%20DEV&desc=разработка%20помощника&descAlignY=61&descAlign=68&fontColor=1)

Инфологи;

	Лог заходов/выходов игроков (скрытый ip во время спека никак не влияет) логи с 2020 года. 
	В файле 350к строк, ищет информацию за секунду/полторы, максимальное кол-ва строк 1000 дабы не словить долгую задержку, больше ставить не пробовал.
	
	Лог Варнингов, логи с 19.07.2024 года.
	Лог смены ников с начала 24 года.

	/log - заход/выход игроков.
	/logname - лог смены ников.
	/logwar - лог варнингов.
	
Горячие клавиши;

	По стандарту на ответ в пм задана клавиша F1, ее можно сменить в настройках, выбор из нескольких вариантов.
	При поступлении пм вам придет уведомление "Нажмите F1 для ответа на сообщение" После нажатия откроется диалоговое окно с информацией от получателя, в строку введите желаемый ответ игроку который вам написал в пм.
	
	Если игрок напишет жалобу на игрока, можно дать быстрый ответ,  после нажатия клавиши "F3" откроется диалоговое окно где можно ввести желаемый ответ, в конце вашего ответа будет добавлено - "Приятной игры на GalaxY."
	
	Для быстрого принятия репорта нажмите "F4", вы сразу перейдете в слежку за игроком на которого подали жалобу, а игроку который написал жалобу - "Ваша жалоба рассматривается" (В настройках можно включить доп. информацию за следящим, вам в чат напишет его последние ники, последние заходы. (Это по желанию, можно не включать.)
	
	Если игрок Вам напишет в пм о просьбе выдать ноль хп, телепортироватся к нему, или телепортировать его к себе - достаточно нажать клавишу "BackSpade" Вам откроется диалоговое окно с выбором действий. В будущем будут дополнятся функций взаимодействий.

Ответ игроку на репорт;

	/ac - Жалоба рассматривается
	/at - жалоба рассмотрена 
	/jb - оставьте жалобу на форум
	
	Для редактирования ответа:
	
	/setac
	/setat
	/setjb
	
	
Система отыгранных часов;

	/exp - проверить сколько вы отыграли на сервере (получено экспи).
	/expdel - обнулить счетчик.
	
Система Реконнекта;

	/rec 1 - Переподключиться к серверу (Задержка указана в настройках /mh - Настройки Реконнекта (указать время в секундах))
	Автоматический перезаход при "Server closed the connection."   "You are banned from this server." 
	
Система автологина;

	При первом использовании скрипта у вас не будет задан пароль от аккаунта, 
	для автозахода на сервере укажите пароль в настройках /mh - "Установить автологин"
	
Система телепорта;

	Для телепорта по метка на карте установите метку на карте и пропишите команду /tpp.
	Для телепорта в интерьер, зайдите в меню - /mh - "Телепорт меню" - Не полный список, будет дополнятся.
	Для телепорта игроков по пм (tpme) /mh - "Активировать телепорт к вам".
	Для телепорта игрока к вам с выдачей хп (Для дм на аммо) /mh - "Активировать дм на аммо с выдаче хп".
	
Система выключения показа действий модераторов;

	Для отключения показа, зайдите в меню /mh - "Вкл/Выкл показ действий модераторов".
	
Система выдачи хп в радиусе (стрима);

	/mh - "Выдача хп в радиусе" - Выдает хп от 0 до 160 в ридиусе.
	
Система спека;

	Для включения, выключения вх в спеке /mh - Вкл/Выкл Wh в спеке.
	Для включения, выключения заходов игроков в спеке /mh - "Показ IP в спеке" (Полезно при записи видео)
	
Система редактирования времени и причины наказания;

	Для редактирования времени наказания введите команду - /settime((f)mat)((f)osk)((f)caps) и тд.
	Для редактирования причины - /set((f)mat)((f)osk)((f)caps) и тд.
