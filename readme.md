# Test-Konfigurationen für das Grooming des Publisher

## Shell-Befehl zum Ausführen der Tests

    ./start-gretl.sh --docker-image sogis/gretl:latest --job-directory $PWD --info | tee $PWD/.log/log.txt

(Im Verzeichnis des build.gradle ausführen)

## Testfälle

* Ausdünnung innerhalb Jahr / Monat / Woche
    * Nur Jüngster innnerhalb des vorletzten Jahres bleibt erhalten =>  **nicht OK**, über Jahresgrenze nimmt es pro Jahr den jüngsten Tag pro Jahr. Kann ev. gelöst werden indem man die Definition anpasst.
    ```
      Prüft alle > 365 und > 730 Tage => Problem Jahreswechsel:
     {
        "grooming": {
           "yearly": {
              "from": 366,
              "to": 731
          }
        }
     }
   ```
     ```
     Das File am Tag 365 bleibt erhalten:
     {
        "grooming": {
           "yearly": {
              "from": 365,
              "to": 366
          }
        }
     }
     ```
     ```
     Das File am Tag 730 bleibt erhalten:
     {
        "grooming": {
           "yearly": {
              "from": 730,
              "to": 731
          }
        }
     }
     ```
    * Nur Jüngster innerhalb des vorletzten Monats bleibt erhalten
    * Nur Jüngster in der vorletzten Woche bleibt erhalten
    * Nur Jüngster in den letzten Wochen über Monatsgrenze => **nicht OK**, über Monatsgrenze nimmt es pro Monat den jüngsten Tag pro Woche. (Beispiel 31.07. / 01.08.2023)
* Einzelstände in Jahr / Monat / Woche
    * Drei Testfälle um sicherzustellen, dass der vorhandene einzene Stand bestehen bleibt.
* Übergang Tag / Woche
    * 10 Tage lang Daily / danach Weekly => **OK**
    * 10 Tage lang Daily => **OK**
    * letzten 14 Tage 1x pro Woche => **OK**
* Übergang Woche / Monat
    * 6 Wochen weekly, danach monthly => **OK**
* Test der produktiven Groom-Konfiguration
