### Занятие 11.
Тема - планирование адресного пространства инфраструктуры.

Из интересных или ключевых моментах занятия.
1. qos ключается на свичах к примеру для телефонии, на акцесс уровне, (разумеется на роутере то же)
2. Рекомендуемая архитектура любой сети (к примеру офиса) 3-уровневая:
```
2.1. Кор - его задача это внешняя маршрутизация
2.2. Дистрибьюция - задача в объединении доступа и кора, он не занимается маршрутами кора и не имеет портов доступа
2.3. Доступ - его задача собрать всех пользователей, т.е. это у него все порты доступа и он граничит с юзером.
```
Вообще конечно 3 уровня имеются всегда, просто иногда они объединяются с целью экономии. Может вообще быть один роутер всего, но это для каких то не нагруженных и не критичных участком сети.

Ещё раз, в Кор ничего не подключается никогда, он только маршрутизирует. А в акцесс и дестрибьюшн уже да, как позволяют ресурсы.


FHRP - это группа протоколов резервирования шлюзов, в которую входят:
hsrp - виртуальный шлюз проприетарный протокол Cisco (проприетарный протокол)
vrrp - виртуальный шлюз, но уже открытый протокол (на основе hsrp)
glbp - балансировщик шлюзов, проприетарный протокол cisco (в сравнении с hsrp и vrrp, рабтает одновременно с несколькими шлюзами). Он хорош не только для распределения нагрузки, но и обслуживания одного из шлюзов.

Вообще мир идёт в сторону отказала от L2-уровня т.к. STP требует много ресурсов обслуживания. 
Придумали L3 натянуть на коммутатор L2: 
Плюс -  нет STP, везде Л3 линки и можно делать балансировку нагрузки.
Минус - нет широковещалки, для многих технологий это проблема.

Стекирование хорошаятехнология объединения свичей в один, но ни дай бог специальный кабель упадёт и ппц. На смену стекированию пришёл MLAG или vPC, там два линка + Кипалайв-линк, но проблема в том что свичей во МЛАГе может быть только 2.
MLAG (Multi-Chassis Link Aggregation) и vPC (Virtual Port Channel) — технологии для обеспечения избыточности и высокой доступности в сетях центров обработки данных.

Вырезка из сети:
```
Основные различия между MLAG и vPC:
1. Сложность реализации. MLAG — общедоступный протокол, который позволяет основным поставщикам настраивать реализацию под свои нужды. vPC — протокол для семейства коммутаторов Cisco Nexus, настраивается только на устройствах Cisco, поэтому требует больше настроек и шагов конфигурации.
2. Совместимость. Для vPC нужны коммутаторы той же модели и с той же версией NX-OS. MLAG более совместим и может быть развёрнут на разных коммутаторах разных поставщиков без строгих ограничений по модели продукта или операционной системе.
3. Поддержка многопутевых передач. vPC поддерживает не только многопутевые передачи уровня 2, но и уровня 3, что позволяет балансировать нагрузку и улучшать избыточность с помощью параллельных путей. MLAG в основном поддерживает многопутевые передачи уровня 2, но не так мощно обрабатывает многопутевой трафик.
4. Сценарии применения. vPC в основном используется в коммутаторах центра обработки данных Cisco Nexus, поэтому его сценарии применения относительно ограничены. MLAG имеет более широкую сферу применения и может использоваться не только в традиционной трёхъярусной архитектуре центра обработки данных, но и в двухъярусной архитектуре «спина-лист».
```


