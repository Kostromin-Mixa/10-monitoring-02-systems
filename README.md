1. Основные плюсы и минусы pull и push систем мониторинга: 

Плюсы PULL: 
 - Проще Контролировать достоверность и объем данных. При извлечении данных мы можем быть уверены в подлинности данных, так как сам сервер инициирует соединение. Порт, на котором доступны данные метрик, всегда прослушивается, тогда как в системах push-based используются временные соединения, которые исчезают и появляются очень быстро.
 - Проще шифровать трафик. Можно поставить обратный прокси-сервер TLS перед обычным HTTP-сервером, который обслуживает метрики, и мы могли бы использовать что-то вроде letsencrypt, чтобы автоматически получить сертификат, если это общедоступная система или сертификат от частного центра сертификации, которому доверяют все в нашей интрасети.
 - Проще извлекать данные по требованию (и отлаживать).Наличие метода pull поверх TCP (HTTP) означает, что очень легко извлекать данные по требованию и отлаживать проблемы. Это дает возможность легко различать ошибки на стороне клиента и на стороне сервера. В методе PUSH если бы мы не получали никаких метрик, то это означало бы одно из двух: с сетью что то не так или с клиентом что то не так. С помощью метода push (TCP/HTTP) мы можем проверить разницу между ними, перейдя с помощью веб-браузера к IP-адресу и порту, где мы можем найти данные метрик. Если мы получили сброс TCP-соединения, то это означает, что сеть в порядке, но с клиентом что-то не так. Если мы вообще не получили никакого ответа, это означает, что с сетью что-то не так.

Плюсы PUSH: 
 - Проще реализовать репликацию в разные точки приема. Поскольку все инициируется самим клиентом, становится проще реплицировать один и тот же трафик на разные серверы. Нам просто нужно передать его на один целевой IP-адрес.
 - Легко моделировать короткоживущие пакетные задания. 
 - Потенциально может быть более эффективным. Методы PUSH обычно используют UDP, в то время как методы PULL основаны на TCP (HTTP). Это означает, что мы потенциально можем пушить метрики более эффективно, чем пулить их.
2. Какие из ниже перечисленных систем относятся к push модели, а какие к pull? А может есть гибридные? 
 - Prometheus: pull
 - TICK: pull
 - Zabbix: push+pull
 - VictoriaMetrics: push+pull
 - Nagios: push+pull
3. 
