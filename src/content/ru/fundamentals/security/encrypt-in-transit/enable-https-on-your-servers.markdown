---
title: "Включение HTTPS на ваших серверах"
description: "Вы готовы выполнить все важные шаги, чтобы включить HTTPS на ваших серверах"
updated_on: 2015-03-27
key-takeaways:
  - "Чтобы настроить ваш сервер на поддержку HTTPS, используйте инструмент конфигурирования сервера Mozilla."
  - "Регулярно тестируйте свой сайт с помощью удобного теста SSL Server Test Qualys и проверяйте, что получены оценки не ниже A или A+."
---

<p class="intro">
  Вы готовы выполнить все важные шаги, чтобы включить HTTPS на ваших серверах
</p>

{% include shared/takeaway.liquid list=page.key-takeaways %}

{% include shared/toc.liquid %}

На этом этапе необходимо принять важнейшее эксплуатационное решение:

* выделять отдельный IP-адрес для каждого имени хоста, 
с которого получает контент ваш веб-сервер, или
* использовать виртуальный хостинг на базе имен.

Если для каждого имени хоста используется отдельный IP-адрес, это замечательно! Вы можете
с легкостью поддерживать HTTP и HTTPS для всех клиентов.

Однако операторы большинства сайтов используют виртуальный хостинг на базе имен — это позволяет сохранить IP-адреса
и в общем и целом более удобно. Проблема с IE в
Windows XP и Android версии ранее 2.3 состоит в том, что они не понимают обозначение имени сервера [Server
Name Indication](https://en.wikipedia.org/wiki/Server_Name_Indication) (SNI),
которое является ключевым для виртуального хостинга на базе имен для HTTPS.

Когда-нибудь, будем надеяться, что скоро, на смену клиентам, которые не поддерживают SNI, придет
более современное программное обеспечение. Контролируйте строку агента пользователя в журналах запросов, чтобы узнать,
когда достаточное количество ваших пользователей перейдет на современное программное обеспечение. (Вы можете
решить, что ваш порог составляет, скажем &lt; 5 % или &lt; 1 % и т. п.)

Если на ваших серверах еще нет службы HTTPS, включите ее сейчас
(без перенаправления HTTP на HTTPS, см. ниже). Настройте свой веб-сервер на использование
приобретенных и установленных сертификатов. Возможно, [удобный
генератор
конфигурации Mozilla](https://mozilla.github.io/server-side-tls/ssl-config-generator/)
покажется вам полезным.

Если у вас много имен хостов/дочерних доменов, каждый из них должен использовать корректный
сертификат.

**ПРИМЕЧАНИЕ.** Операторы многих сайтов уже выполнили указанные нами шаги, но
продолжают использовать HTTPS с единственной целью перенаправлять клиентов обратно на HTTP. Если вы
так поступаете, прекратите немедленно. В следующем разделе показано, как обеспечить бесперебойную работу
HTTPS и HTTP.

**ПРИМЕЧАНИЕ.** В конце концов вы должны перенаправлять запросы HTTP на HTTPS и использовать строгую безопасность транспорта HTTP Strict
Transport Security (HSTS). Делать это на этапе процесса миграции не следует.
См. разделы "Перенаправление с HTTP на HTTPS" и "Включение строгой безопасности транспорта и использование защищенных файлов cookie".

Теперь, пока существует ваш сайт, проверяйте конфигурацию HTTPS с помощью
[удобного теста SSL Server Test Qualys](https://www.ssllabs.com/ssltest/). Ваш сайт должен получать оценку
A или A+. Любые причины более низкой оценки должны расцениваться как ошибка.
(Сегодняшний уровень A завтра превратится в B, поскольку атаки на алгоритмы и протоколы
становятся все более изощренными!)

