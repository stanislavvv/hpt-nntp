# hpt-nntp
hpt-nntp simple gateway

ToDO:
-----

1) `filter.pl` -- экспорт вновь создаваемых сообщений в формат ньюсов (один файл - одно сообщение). Запуск средствами hpt в качестве фильтра.
2) `news-feeder` -- скрипт-фидер полученных сообщений в один из nntp-серверов (так как для каждого сервера он может быть свой - отдельно от скрипта-экспортера)
3) `news-suck` -- скрипт, получающий свежие сообщения от nntp-сервера (самое сложное. Здесь требуется определить, какие сообщения у ньюс-сервера свежие. Весьма вероятно, что он будет зависеть от типа сервера, потому - отдельно)
4) `news2pkt` -- конверсия сообщений из формата ньюсов в pkt (с дальнейшим размещением их в каталог inbound). Потребуется обработка как MSGID (вероятно, надо писать фидошный вариант в отдельнй заголовок), Message-Id, так и X-Comment-To, см. http://fidogate.sourceforge.net/msgid-4.html).

Примерный вариант настройки:

Добавить в `/etc/husky/config` строку:

    hptPerlFile /etc/husky/filter.pl

В результате чего каждое сообщение будет подаваться на вход `filter.pl`, что позволит экспортировать его в файл в формате ньюсов.
По крону запускается `news-feeder`, который каждый экспортированный файл будет посылать на nntp-сервер и при успехе - удалять.

В случае, если nntp-сервер будет использоваться для написания новых сообщений, по крону будут так же запускаться `news-suck` и `news2pkt`.
