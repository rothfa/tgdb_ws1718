# Tutorium - Grundlagen Datenbanken - Blatt 5

## Vorbereitungen
* Für dieses Aufgabenblatt wird die SQL-Dump-Datei `01_tutorium.sql` benötigt, die sich im Verzeichnis `sql` befindet.
* Die SQL-Dump-Datei wird in SQL-Plus mittels `start <Dateipfad/zur/sql-dump-datei.sql>` in die Datenbank importiert.
* Beispiele
  * Linux `start ~/Tutorium.sql`
  * Windows `start C:\Users\max.mustermann\Desktop\Tutorium.sql`

## Datenbankmodell
![Datenbankmodell](./img/datamodler_schema.png)

## Aufgaben

### Aufgabe 1
Erstelle mit Dia oder einem anderen Werkzeug eine Abbilung der Mengen, die durch `INNER JOIN`, `RIGHT JOIN`, `LEFT JOIN` und `OUTER JOIN` gemeint sind.

#### Lösung
> Deine Lösung

INNER JOIN -> Schnittmenge in der Mitte 

SELECT column_name(s)
FROM table1
INNER JOIN table2 ON table1.column_name = table2.column_name;

RIGHT JOIN -> Schnittmenge in der Mitte + Rechter Teil

SELECT column_name(s)
FROM table1
RIGHT JOIN table2 ON table1.column_name = table2.column_name;

LEFT JOIN -> Schnittmenge in der Mitte + Linker Teil

SELECT column_name(s)
FROM table1
LEFT JOIN table2 ON table1.column_name = table2.column_name;

OUTER JOIN 

Als Spezialfälle des OUTER JOIN gibt es die JOIN-Typen LEFT JOIN, RIGHT JOIN, FULL JOIN.


### Aufgabe 2
Welche Personen haben kein Fahrzeug? Löse dies einmal mit `LEFT JOIN` und `RIGHT JOIN`.

#### Lösung
```sql
SELECT 
```
