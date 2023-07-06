# Test-Konfigurationen für das Grooming des Publisher

## Shell-Befehl zum Ausführen der Tests

    ./start-gretl.sh --docker-image sogis/gretl:latest --job-directory $PWD --info | tee $PWD/.log/log.txt

(Im Verzeichnis des build.gradle ausführen)

## Testfälle

* Duplikate in Jahr / Monat / Woche
    * Ältere Stände im vorletzten Jahr wird gelöscht
    * Älteres Stände im vorletzten Monat wird gelöscht
    * Älteres Stände in der vorletzten Woche wird gelöscht
* Einzelstände in Jahr / Monat / Woche
    * Drei Testfälle um sicherzustellen, dass der vorhandene einzene Stand bestehen bleibt.
* Übergang Tag / Woche
    * 10 Tage lang Daily / danach Weekly
* Übergang Woche / Monat
    * 6 Wochen weekly, danach monthly
* Test der produktiven Groom-Konfiguration