# Test-Konfigurationen für das Grooming des Publisher

## Shell-Befehl zum Ausführen der Tests

    ./start-gretl.sh --docker-image sogis/gretl:latest --job-directory $PWD --info | tee $PWD/.log/log.txt

(Im Verzeichnis des build.gradle ausführen)

## Testfälle

* Ausdünnung innerhalb Jahr / Monat / Woche
    * Nur Jüngster innnerhalb des vorletzten Jahres bleibt erhalten => Davon ausgehend dass das Jahr 365 Tage hat. => **nicht OK**, über Jahresgrenze (31.12. / 01.01). Sonst **OK**.
    * Nur Jüngster innerhalb des vorletzten Monats bleibt erhalten => Davon ausgehen dass der Monat 30 Tage hat. => **nicht OK**, über Monatsgrenze. Rest **OK**.
    * Nur Jüngster in der vorletzten Woche bleibt erhalten => **nicht OK**, über Monatsgrenze nimmt es pro Monat und vorletzte Woche das jüngste Datum. Sonst **OK**.
    * Nur Jüngster in den letzten Wochen über Monatsgrenze => **nicht OK**, über Monatsgrenze nimmt es pro Monat den jüngsten Tag pro Woche. (Beispiel 31.07. / 01.08.2023). Sonst **OK**.
* Einzelstände in Jahr / Monat / Woche
    * Drei Testfälle um sicherzustellen, dass der vorhandene einzene Stand bestehen bleibt.
* Übergang Tag / Woche
    * 10 Tage lang Daily / danach Weekly => **OK**
    * 10 Tage lang Daily => **OK**
    * letzten 14 Tage 1x pro Woche => **OK**
* Übergang Woche / Monat
    * 6 Wochen weekly, danach monthly => **OK**
* Test der produktiven Groom-Konfiguration => **OK**
