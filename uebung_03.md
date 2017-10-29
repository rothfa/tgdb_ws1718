# Tutorium - Grundlagen Datenbanken - Blatt 3

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
Erstelle eine `INNER JOIN` (optional `WHERE`) Abfrage um die Beziehungen zwischen den Tabellen `GAS_STATION`, `Provider`, `COUNTRY` und `ADDRESS` aufzulösen, sodass eine ähnliche Ausgabe erstellt wird wie abgebildet.

| Anbieter  | Straße            | PLZ   | Ort         | Land        | Steuer  |
| --------- | ----------------- | ----- | ----------- | ----------- | ------- |
| Shell     | Zurlaubener 1     | 54292 | Trier       | Deutschland | 0.19    |
| Esso      | Triererstraße 10  | 53937 | Hellenthal  | Deutschland | 0,19    |
| ...       | ...               | ...   | ...         | ...         | ...     |

#### Lösung
```sql
SELECT p.provider_name AS "Anbieter", gs.street AS "Straße", a.plz AS "PLZ", a.city AS "Ort", c.country_name AS "Land", c.duty_amount AS "Steuer"
FROM gas_station gs
INNER JOIN address a ON (gs.address_ID = a.address_ID)
INNER JOIN country c ON (c.country_id = gs.country_ID)
INNER JOIN provider p ON (gs.provider_ID = p.provider_ID);
```

### Aufgabe 2
Suche alle Tankstellen raus, deren Straßenname an zweiter Stelle ein `U` haben (case-insensetive). Verändere dazu die Abfrage aus Aufgabe 1. Optional für Enthusiasten, suche mittels Regulärem Ausdruck.

#### Lösung
```sql
SELECT p.provider_name 
FROM gas_station gs
INNER JOIN provider p ON (gs.provider_id = p.provider_ID)
WHERE gs.street LIKE '_u%'
OR gs.street LIKE '_U%';
```

### Aufgabe 3
Suche alle Tankstellen raus, die sich in Trier befinden.

#### Lösung
```sql
SELECT * FROM GAS_STATION WHERE ADDRESS_ID = 1 OR ADDRESS_ID = 2 OR ADDRESS_ID = 6 OR ADDRESS_ID = 11 OR ADDRESS_ID = 11;

SELECT p.provider_name AS "Anbieter", gs.street AS "Straße", a.plz AS "PLZ", a.city AS "Ort", c.country_name AS "Land", c.duty_amount AS "Steuer"
FROM gas_station gs
INNER JOIN address a ON (gs.address_ID = a.address_ID)
INNER JOIN country c ON (c.country_id = gs.country_ID)
INNER JOIN provider p ON (gs.provider_ID = p.provider_ID)
WHERE  a.city = 'TRIER';
```

#### Aufgabe 4
Füge eine fiktive Tankstelle hinzu. Sie darf auf keine bestehenden Informationen basieren. Nutze möglichst wenige SQL-Befehle. Rufe fehlende Informationen möglichst direkt ab.

#### Lösung
```sql
-- Address
INSERT INTO ADDRESS
VALUES ((SELECT MAX (ADDRESS_ID) FROM ADDRESS) + 1, '54313', 'ZEMMER');
-- Country
INSERT INTO COUNTRY
VALUES ((SELECT MAX (COUNTRY_ID) FROM COUNTRY) + 1, 'Deutschland', 0.22);
-- Provider
INSERT INTO Provider
VALUES ((SELECT MAX (Provider_ID) FROM Provider) + 1, 'BQ');
-- Provider
INSERT INTO GAS_STATION
VALUES ((SELECT MAX (GAS_STATION_ID) FROM GAS_STATION) + 1,
(SELECT PROVIDER_ID FROM PROVIDER WHERE PROVIDER_NAME = 'BQ'),
(SELECT COUNTRY_ID FROM COUNTRY WHERE COUNTRY_NAME = 'Deutschland'),
(SELECT ADDRESS_ID FROM ADDRESS WHERE CITY = 'ZEMMER');

```

### Aufgabe 5
Erstelle eine INNER JOIN (optional `WHERE`) Abfrage um die Beziehung zwischen den Tabellen `ACCOUNT`, `VEHICLE`, `VEHICLE_TYPE`, `GAS` und `PRODUCER` aufzulösen 
und zeige die Spalten `FORNAME`, `SURNAME`, `VEHICLE_TYPE_NAME`, `VERSION`, `BUILD_YEAR`, `PRODUCER_NAME` und `GAS_NAME` an. Richte SQL-Plus so ein, dass möglicht jeder Datensatz nur eine Zeile belegt.

* COLUMN <SPALTENNAME> FORMAT a<Zeichenlänge>
* COLUMN <SPALTENNAME> FORMAT <Zahlenlänge, pro Länge eine 9>
* Beispiel für eine Spalte des Datentyps `VARCHAR2`: `COLUMN SURNAME FORMAT a16`
* Beispiel für eine Spalte des Datentyps `NUMERIC`: `COLUMN SOLD_KILOMETER 9999`

#### Lösung
```sql
SELECT account.forname, account.surname, vehicle_type.vehicle_type_name, vehicle.version, vehicle.build_year, producer.producer_name, gas.gas_name
FROM vehicle 
INNER JOIN vehicle.id 
```

### Aufgabe 6
Welche Fahrzeuge wurden noch keinem Benutzer zugewiesen? Gebe über das Fahrzeug Informationen über den Typ, den Hersteller, das Modell, Baujahr und den Kraftstoff aus.

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 7
Verknüpfe eines der Autos aus Aufgabe 6 mit deinem Benutzernamen. Verwende dazu möglichst wenige SQL-Statements.

#### Lösung
```
Deine Lösung
```

### Aufgabe 8
An welcher Tankstelle wurde noch nie getankt? Gebe zu den Tankstellen die Informationen über den Standort der Tankstellen aus.

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 9
Liste alle Benutzer (Vorname und Nachname) mit Fahrzeug (Hersteller, Modell, Alias) auf, die noch nie einen Beleg hinzugefügt haben.

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 10
Liste alle Benutzer auf, die mit einem Fahrzeug schonmal im Außland tanken waren.

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 11
Wie viele Benutzer haben einen LKW registriert?

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 12
Wie viele Benutzer haben einen PKW und einen LKW registriert?

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 13
Führe den Patch `02_patch.sql`, der sich im Verzeichnis `sql` befindet, in deiner Datenbank aus. Wie lautet der Befehlt zum import?

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 14
Aktualisiere den Steuersatz aller Belege auf den Steuersatz des Landes, indem die Kunden getankt haben.

#### Lösung
```sql
Deine Lösung
```


