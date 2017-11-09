# Tutorium - Grundlagen Datenbanken - Blatt 4

## Vorbereitungen
* Für dieses Aufgabenblatt wird die SQL-Dump-Datei `tutorium.sql` benötigt, die sich im Verzeichnis `sql` befindet.
* Die SQL-Dump-Datei wird in SQL-Plus mittels `start <Dateipfad/zur/sql-dump-datei.sql>` in die Datenbank importiert.
* Beispiele
  * Linux `start ~/Tutorium.sql`
  * Windows `start C:\Users\max.mustermann\Desktop\Tutorium.sql`

## Datenbankmodell
![Datenbankmodell](./img/datamodler_schema.png)

## Aufgaben

### Aufgabe 1
<<<<<<< HEAD
Um genauere Informationen und Prognosen mit Data Mining Werkzeugen zu schöpfen, 
ist es notwendig mehr Informationen über die registrierten Benutzer zu sammeln und zu speichern. 
Die in Zukunft gesammelten Informationen sollen in neuen Tabellen des bestehenden Datenbankmodells gespeichert werden. 
Dazu soll jedem Benutzer einen Erst- und Zweitwohnsitz zugeordnet werden. Jeder Wohnsitz besitzt eine eigene Adresse. 
Integriere in das bestehende Datenbankmodell Tabellen die den genauen Erst- und Zweitwohnsitz abbilden können. Beachte dazu die Normalisierungsformen bis 3NF - [Dokumentation](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)). Wie lautet deine SQL-Syntax um deine Erweiterung des Datenbankmodells zu implementieren?

#### Lösung
```sql
CREATE TABLE residence
(residence_id       NUMBER(5)     NOT NULL, 
PLZ       NUMBER(5)   NOT NULL, 
City      VARCHAR2    NOT NULL, 
Street     NUMBER(15,2);
=======
Um genauere Informationen und Prognosen mit Data Mining Werkzeugen zu schöpfen, ist es notwendig mehr Informationen über die registrierten Benutzer zu sammeln und zu speichern. Die in Zukunft gesammelten Informationen sollen in neuen Tabellen des bestehenden Datenbankmodells gespeichert werden. Dazu soll jedem Benutzer einen Erst- und Zweitwohnsitz zugeordnet werden. Jeder Wohnsitz besitzt eine eigene Adresse. Integriere in das bestehende Datenbankmodell Tabellen die den genauen Erst- und Zweitwohnsitz abbilden können. Beachte dazu die Normalisierungsformen bis 3NF - [Dokumentation](https://de.wikipedia.org/wiki/Normalisierung_(Datenbank)). Wie lautet deine SQL-Syntax um deine Erweiterung des Datenbankmodells zu implementieren?

#### Lösung
```sql
Deine Lösung
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2
```

### Aufgabe 2
Als App Entwickler/in für Android und iOS möchtest du dich nicht darauf verlassen, dass die Adresse exakt richtig ist und überlegst in dem Datenbankmodell noch zwei zusätzliche Attribute (X und Y Koordinate) zur genauen GPS Lokalisierung einer Tankstelle aufzunehmen. Wie lautet deine SQL-Syntax um das Datenbankmodell auf die zwei Attribute zu erweitern?

#### Lösung
```sql
<<<<<<< HEAD
ALTER TABLE gas_station 
ADD (xcoordinate Number(8,15), ycoodinate Number(8,15));

=======
Deine Lösung
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2
```

### Aufgabe 3
Welche Kunden haben im Jahr 2017 mehr als den Durchschnitt getank?

#### Lösung
```sql
<<<<<<< HEAD
SELECT AVG(LITER)
FROM RECEIPT
WHERE RECEIPT_DATE = ;

SELECT a.account_id
from receipt a
group by a.account_id


=======
Deine Lösung
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2
```

### Aufgabe 4
Ermittle, warum du INSERT-Rechte auf die Tabelle `SCOTT.EMP` und UPDATE-Rechte auf die Tabelle `SCOTT.DEPT` besitzt. Beantworte dazu schrittweise die Aufgaben von 4.1 bis 4.4.

#### Aufgabe 4.1
Wurden die Tabellen-Rechte direkt an dich bzw. an `PUBLIC` vergeben?

<<<<<<< HEAD


##### Lösung
```sql
SELECT * FROM all_tab_privs where table_schema = 'SCOTT' and table_Name = 'EMP';
SELECT * FROM all_tab_privs where table_schema = 'SCOTT' and table_Name = 'DEPT';
```
1. no rows selected
2. Wurden direkt an Public gegeben! (update)
=======
##### Lösung
```sql
Deine Lösung
```
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2

#### Aufgabe 4.2
Welche Rollen besitzt du direkt?

<<<<<<< HEAD
FH-Trier

##### Lösung
```sql
SELECT * FROM USER_ROLE_PRIVS;
=======
##### Lösung
```sql
Deine Lösung
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2
```

#### Aufgabe 4.3
Welche Rollen haben die Rollen?

<<<<<<< HEAD
FH-Trier -> WI_STUDENT

##### Lösung
```sql
select * from role_role_privs;
=======
##### Lösung
```sql
Deine Lösung
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2
```

#### Aufgabe 4.4
Haben die Rollen Rechte an `SCOTT.EMP` oder `SCOTT.DEPT`?

##### Lösung
```sql
<<<<<<< HEAD
SELECT * FROM role_role_privs where table_schema = 'SCOTT' and table_Name = 'DEPT';
=======
Deine Lösung
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2
```

### Aufgabe 5
Es soll für jede Tankstelle der Umsatz einzelner Jahre aufgelistet werden auf Basis der Daten, die Benutzer durch ihre Quittungen eingegeben haben. Sortiere erst nach Jahr und anschließend nach der Tankstelle. Beispiel:

| Jahr  | Anbieter  | Straße            | PLZ   | Stadt | Land          | Umsatz    |
| ----- | --------- | ----------------- | ----- | ----- | --------------| --------- |
| 2017  | Esso      | Triererstraße 15  | 54292 | Trier | Deutschland   | 54784.14  |
| 2017  | Shell     | Zurmainerstraße 1 | 54292 | Trier | Deutschland   | 67874.78  |
| 2016  | Esso      | Triererstraße 15  | 54292 | Trier | Deutschland   | 57412.66  |
| 2016  | Shell     | Zurmainerstraße 1 | 54292 | Trier | Deutschland   | 72478.42  |

#### Lösung
```sql
<<<<<<< HEAD
SELECT 
=======
Deine Lösung
>>>>>>> b47112e06be137c97bae02d3ff863c7d8291d1c2
```


