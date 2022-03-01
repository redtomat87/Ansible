
ДЕБАГ ОТКАЗА ОЖИДАНИЯ СЕРВЕР ЛИДЕРА НА 8008 ПОРТУ ПРИ УСТАНОВКЕ pgcluster
ПРОБЛЕМА - 
TASK [patroni : Wait for port 8008 to become open on the host] с сообщением FAILED - RETRYING: [192.168.88.17]: Check PostgreSQL is started and accepting connections on Master (1000 retries left).
РЕШЕНИЕ
На искомой ноде делаем / usr / local / bin /patrinictl —help
usr / local / bin /patrinictl  -c / etc /patroni / patroni.yml list
patronictl -c /etc /patroni /patroni.yml remove pgsql_cluster
далее еще раз повторяем postgres-cluster
и yes i am awere 
опять usr / local / bin /patrinictl  -c / etc /patroni / patroni.yml list
РЕШЕНО

ПРОБЛЕМА -
После перезагрузки отваливается консул и ноде експортер
РЕШЕНИЕ
systemctl start firewalld
РЕШЕНО

Плейбук завершился с ошибкой


В результате в кластере был только лидер.
На красных нодах patronictl показывал очень много букоф, решил проверить firewalld — он опять оказался выключенным! Включил по очереди на каждой из красных но и они залетели в кластер -


еще была ошибка TASK [patroni : Prepare PostgreSQL | data directory check result] 
fatal: [192.168.88.17]: FAILED! => {"changed": false, "msg": "Whoops! data directory /var/lib/pgsql/14/data is already initialized"}

Решилась удалением указанной директории.