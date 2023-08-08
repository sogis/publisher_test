# Test-Konfigurationen für das Grooming des Publisher

## Shell-Befehl zum Ausführen der Tests

    ./start-gretl.sh --docker-image sogis/gretl:latest --job-directory $PWD --info | tee $PWD/.log/log.txt

(Im Verzeichnis des build.gradle ausführen)

## Testfälle

* Ausdünnung innerhalb Jahr / Monat / Woche
    * Nur Jüngster innnerhalb des vorletzten Jahres bleibt erhalten
    * Nur Jüngster innerhalb des vorletzten Monats bleibt erhalten
    * Nur Jüngster in der vorletzten Woche bleibt erhalten
    * Nur Jüngster in den letzten Wochen über Monatsgrenze => **nicht OK**, über Monatsgrenze nimmt es pro Monat den jüngsten Tag pro Woche. (Beispiel 31.07. / 01.08.2023)
* Einzelstände in Jahr / Monat / Woche
    * Drei Testfälle um sicherzustellen, dass der vorhandene einzene Stand bestehen bleibt.
* Übergang Tag / Woche
    * 10 Tage lang Daily / danach Weekly
* Übergang Woche / Monat
    * 6 Wochen weekly, danach monthly
* Test der produktiven Groom-Konfiguration
