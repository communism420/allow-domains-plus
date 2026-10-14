# Поможем провайдерам

Поможем провайдерам блокировать запрещённое и снизим нагрузку на их оборудование.

Самостоятельно заблокируем ресурсы у себя. Зарубежные сервисы пусть знают, что их ресурсы никому не нужны, а железо провайдера пусть отдохнёт.

Я вдохновился благой идеей помощи построению суверенного Рунета от проекта [allow-domains](https://github.com/itdoginfo/allow-domains).

Здесь списки для раздельного туннелирования. Что перечислено в файле, уходит в VPN. Всё остальное идёт напрямую.

## Файлы

| Файл | Строк | Что внутри |
| --- | ---: | --- |
| [russia-block-domains.lst](russia-block-domains.lst) | 1797291 | полный список доменов, по одному на строку |
| [russia-block-podkop.lst](russia-block-podkop.lst) | 8955 | краткий список доменов для Podkop |
| [russia-block-ipv4.lst](russia-block-ipv4.lst) | 19677 | адреса и подсети IPv4 |
| [russia-block-ipv6.lst](russia-block-ipv6.lst) | 3445 | адреса и подсети IPv6 |

[russia-block-podkop.lst](russia-block-podkop.lst) — краткая версия доменов. Она для [Podkop](https://github.com/itdoginfo/podkop) и его форков и переделок вроде [Tachyon](https://github.com/Dushnilin/tachyon), которые не тянут большие списки доменов. В ней имена из подборок сервисов и категорий, а также популярные заблокированные площадки и их зеркала, в первую очередь взрослые сайты. Размер оставлен таким, чтобы sing-box на роутере собрал одно правило и не завис: полный реестр из 1797291 имён в одно правило не помещается. Российских сервисов из списка исключений там нет: Яндекс, VK, Mail.ru, Одноклассники, Wildberries, Ozon, банки, Госуслуги, МТС, DNS, Ситилинк. Полный реестр остаётся в `russia-block-domains.lst`, уже без этих же доменов.

Повторы убраны. Домены отсортированы по алфавиту, адреса — по порядку сети. Строка с точкой в начале, например `.ua`, означает всю зону, а не один сайт.

Подсеть записана как CIDR (`91.108.56.0/22`). Адрес без маски — это один хост.

## Чего в списках нет

Сюда не попало то, что в туннель отправлять не нужно:

- частные, локальные и служебные сети, loopback, multicast и заглушки вроде `0.0.0.0` и `123.123.123.123`;
- российские сети банков, магазинов, Госуслуг, VK, Яндекса и провайдеров;
- общая простыня «все адреса подряд».

В кратком `russia-block-podkop.lst` нет реестра заблокированных доменов целиком: там 1797291 имён, и Podkop с его переделками собирают такой `.lst` в одно правило. Для них оставлены имена из подборок сервисов и категорий и добавлены популярные заблокированные площадки, в первую очередь взрослые сайты и зеркала.

Российские домены из `list-exclude.txt` убраны из обоих доменных списков. Это Яндекс, VK, Mail.ru, Одноклассники, Wildberries, Ozon, банки, Госуслуги и соседние российские сервисы. Заблокированные сайты на `.ru` вроде `rutracker.ru` в списках остаются.

Публичные DNS вроде `1.1.1.1` и `8.8.8.8` в IP-списках есть. Если DNS уже ходит через AmneziaDNS или другой резолвер на VPS, эти адреса в маршрутах не обязательны.

## Откуда собрано

В этой помощи провайдерам использованы списки из таких проектов:

- [itdoginfo/allow-domains](https://github.com/itdoginfo/allow-domains)
- [zapretgui](https://git.zapret.moe/zapretdiscordyoutube/zapretgui)

Полный список доменов собран ещё и из открытых списков имён, заблокированных в России. Одинаковый домен оставлен один раз. В краткий список для Podkop эти простыни не добавлялись.

Реестр и его зеркала:

- [antifilter.download, domains.lst](https://antifilter.download/list/domains.lst)
- [community.antifilter.download, domains.lst](https://community.antifilter.download/list/domains.lst)
- [zapret-info/z-i, dump.csv.gz](https://raw.githubusercontent.com/zapret-info/z-i/master/dump.csv.gz)
- [zapret-info/z-i, nxdomain.txt](https://raw.githubusercontent.com/zapret-info/z-i/master/nxdomain.txt)
- [bol-van/rulist, reestr_hostname.txt](https://raw.githubusercontent.com/bol-van/rulist/master/reestr_hostname.txt)
- [RussiaFancyLists, чёрный список доменов](https://raw.githubusercontent.com/Noktomezo/RussiaFancyLists/main/lists/blacklist/domains/full.lst)
- [Re:filter, domains_all.lst](https://raw.githubusercontent.com/1andrevich/Re-filter-lists/main/domains_all.lst)
- [Re:filter, ooni_domains.lst](https://raw.githubusercontent.com/1andrevich/Re-filter-lists/main/ooni_domains.lst)
- [sevcator/zapret-lists, reestr_filtered.txt](https://raw.githubusercontent.com/sevcator/zapret-lists/main/reestr_filtered.txt)
- [mi1su/domain_list, all_domains.lst](https://github.com/mi1su/domain_list/releases/latest/download/all_domains.lst)

Имена, которые сами закрыты с российских адресов, и соседние подборки:

- [Re:filter, community.lst](https://raw.githubusercontent.com/1andrevich/Re-filter-lists/main/community.lst)
- [itdoginfo/allow-domains, Russia inside](https://raw.githubusercontent.com/itdoginfo/allow-domains/main/Russia/inside-raw.lst)
- [RussiaFancyLists, geoblock](https://raw.githubusercontent.com/Noktomezo/RussiaFancyLists/main/lists/geoblock/full.lst)
- [dartraiden/no-russia-hosts](https://raw.githubusercontent.com/dartraiden/no-russia-hosts/master/hosts.txt)
- [medvedeff-true/ru-gaming-blocklist](https://raw.githubusercontent.com/medvedeff-true/ru-gaming-blocklist/main/medvedeff-game-list-all.txt)

Из них и из соседних подборок собраны общие файлы: домены отдельно, IPv4 отдельно, IPv6 отдельно. Краткий доменный список — отдельный файл для Podkop.

## Как подставлять

Ссылка ниже копируется целиком: это адрес самого файла, его можно вставить в настройки роутера.

Podkop и его форки и переделки вроде Tachyon — краткий список доменов:

```
https://raw.githubusercontent.com/communism420/allow-domains-plus/main/russia-block-podkop.lst
```

Клиент тянет большой список доменов:

```
https://raw.githubusercontent.com/communism420/allow-domains-plus/main/russia-block-domains.lst
```

Клиент умеет только маршруты — IPv4:

```
https://raw.githubusercontent.com/communism420/allow-domains-plus/main/russia-block-ipv4.lst
```

IPv6, если он нужен, отдельным файлом:

```
https://raw.githubusercontent.com/communism420/allow-domains-plus/main/russia-block-ipv6.lst
```

Не подставляйте эти файлы вместо `0.0.0.0/0`. Это не полный туннель и не список «запретить всё».
