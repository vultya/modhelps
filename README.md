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

{
  "log": {
    "level": "warn",
    "output": "box.log",
    "timestamp": true
  },
  "dns": {
    "servers": [
      {
        "tag": "dns-remote",
        "address": "udp://1.1.1.1",
        "address_resolver": "dns-direct"
      },
      {
        "tag": "dns-trick-direct",
        "address": "https://sky.rethinkdns.com/",
        "detour": "direct-fragment"
      },
      {
        "tag": "dns-direct",
        "address": "1.1.1.1",
        "address_resolver": "dns-local",
        "detour": "direct"
      },
      {
        "tag": "dns-local",
        "address": "local",
        "detour": "direct"
      },
      {
        "tag": "dns-block",
        "address": "rcode://success"
      }
    ],
    "rules": [
      {
        "domain": "yahoo.com",
        "server": "dns-direct"
      },
      {
        "domain": "connectivitycheck.gstatic.com",
        "server": "dns-remote",
        "rewrite_ttl": 3000
      },
      {
        "domain_suffix": ".ru",
        "server": "dns-direct"
      },
      {
        "rule_set": [
          "geoip-ru",
          "geosite-ru"
        ],
        "server": "dns-direct"
      }
    ],
    "final": "dns-remote",
    "static_ips": {
      "sky.rethinkdns.com": [
        "104.17.147.22",
        "104.17.148.22",
        "172.67.214.246",
        "104.21.83.62",
        "2a06:98c1:3121::2",
        "2a06:98c1:3120::2"
      ]
    },
    "independent_cache": true
  },
  "inbounds": [
    {
      "type": "tun",
      "tag": "tun-in",
      "mtu": 9000,
      "inet4_address": "172.19.0.1/28",
      "inet6_address": "fdfe:dcba:9876::1/126",
      "auto_route": true,
      "strict_route": true,
      "endpoint_independent_nat": true,
      "stack": "mixed",
      "sniff": true,
      "sniff_override_destination": true
    },
    {
      "type": "mixed",
      "tag": "mixed-in",
      "listen": "127.0.0.1",
      "listen_port": 12334,
      "sniff": true,
      "sniff_override_destination": true
    },
    {
      "type": "direct",
      "tag": "dns-in",
      "listen": "127.0.0.1",
      "listen_port": 16450
    }
  ],
  "outbounds": [
    {
      "type": "selector",
      "tag": "select",
      "outbounds": [
        "auto",
        "VLESS-Nikita § 0",
        "http § 1"
      ],
      "default": "auto"
    },
    {
      "type": "urltest",
      "tag": "auto",
      "outbounds": [
        "VLESS-Nikita § 0",
        "http § 1"
      ],
      "url": "http://connectivitycheck.gstatic.com/generate_204",
      "interval": "10m0s",
      "tolerance": 1,
      "idle_timeout": "30m0s"
    },
    {
      "type": "vless",
      "tag": "VLESS-Nikita § 0",
      "server": "147.45.180.66",
      "server_port": 443,
      "uuid": "d8bb8fcb-bac1-4666-b256-13d8df42465b",
      "tls": {
        "enabled": true,
        "server_name": "yahoo.com",
        "utls": {
          "enabled": true,
          "fingerprint": "chrome"
        },
        "reality": {
          "enabled": true,
          "public_key": "3yfP3lhey4qzSHr073j-RJkLpKCkLQwZ8ygoGg5eHG4",
          "short_id": "c31ca33a"
        }
      },
      "packet_encoding": "xudp"
    },
    {
      "type": "http",
      "tag": "http § 1",
      "server": "yahoo.com",
      "server_port": 0
    },
    {
      "type": "dns",
      "tag": "dns-out"
    },
    {
      "type": "direct",
      "tag": "direct"
    },
    {
      "type": "direct",
      "tag": "direct-fragment",
      "tls_fragment": {
        "enabled": true,
        "size": "10-30",
        "sleep": "2-8"
      }
    },
    {
      "type": "direct",
      "tag": "bypass"
    },
    {
      "type": "block",
      "tag": "block"
    }
  ],
  "route": {
    "rules": [
      {
        "inbound": "dns-in",
        "outbound": "dns-out"
      },
      {
        "port": 53,
        "outbound": "dns-out"
      },
      {
        "process_name": [
          "Hiddify",
          "Hiddify.exe",
          "HiddifyCli",
          "HiddifyCli.exe"
        ],
        "outbound": "bypass"
      },
      {
        "domain_suffix": ".ru",
        "outbound": "direct"
      },
      {
        "rule_set": [
          "geoip-ru",
          "geosite-ru"
        ],
        "outbound": "direct"
      }
    ],
    "rule_set": [
      {
        "type": "remote",
        "tag": "geoip-ru",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/hiddify/hiddify-geo/rule-set/country/geoip-ru.srs",
        "update_interval": "120h0m0s"
      },
      {
        "type": "remote",
        "tag": "geosite-ru",
        "format": "binary",
        "url": "https://raw.githubusercontent.com/hiddify/hiddify-geo/rule-set/country/geosite-ru.srs",
        "update_interval": "120h0m0s"
      }
    ],
    "final": "select",
    "auto_detect_interface": true,
    "override_android_vpn": true
  },
  "experimental": {
    "cache_file": {
      "enabled": true,
      "path": "clash.db"
    },
    "clash_api": {
      "external_controller": "127.0.0.1:16756",
      "secret": "9chLVQ9furuL4hLj"
    }
  }
}


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
