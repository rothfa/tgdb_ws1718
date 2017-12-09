# Tutorium - Grundlagen Datenbanken - Blatt 9

## Vorbereitungen
* Für dieses Aufgabenblatt wird die SQL-Dump-Datei `tutorium.sql` benötigt, die sich im Verzeichnis `sql` befindet.
* Die SQL-Dump-Datei wird in SQL-Plus mittels `start <Dateipfad/zur/sql-dump-datei.sql>` in die Datenbank importiert.
* Beispiele
  * Linux `start ~/Tutorium.sql`
  * Windows `start C:\Users\max.mustermann\Desktop\Tutorium.sql`

## Datenbankmodell
![Datenbankmodell](./img/datamodler_schema.png)

### Aufgabe 1
Wo liegen die Vor- und Nachteile eines Trigger in Vergleich zu einer Prozedur?

#### Lösung
Ein Trigger dient zur Wahrung der Datenintegrität (Konsitenz) und zum Einfügen, Ändern, Löschen von Daten in einer Tabelle.
Ein Trigger kann z.B. vor einer Änderung ausgelöst werden um Manipulationen zu vermeiden. 
Beispiel: Bei Manipulationen des Betrags einer Rechnungsposition, wird der Gesamtbetrag der Rechnung aktualisiert.
Vorteil: Trigger lösen automatisch aus; Der Benutzer muss sich nicht über weitere Vorgänge des Updates Gedanken machen (Fehlervermeidung)
		Trigger können Bedingungen bei INSERT, UPDATE oder DELETE Befehlen überprüfen (Können Prozeduren nicht) -> Davor oder Danach!
		Trigger können in sich wiederum Trigger auslösen.
		
Nachteil: Trigger können in sich wiederum Trigger auslösen. -> Verkettung, macht Fehlersuche sehr schwierig, wenn viele Trigger hintereinander 
			ausgelöst werden

### Aufgabe 2
Wo drin unterscheidet sich der `Row Level Trigger` von einem `Statement Trigger`?

#### Lösung
A statement-level trigger will be activated once (and even if no rows are updated).
A row-level trigger will be activated a million times, once for every updated row.

### Aufgabe 3
Schaue dir den folgenden PL/SQL-Code an. Was macht er?

```sql
CREATE SEQUENCE seq_account_id
START WITH 1000
INCREMENT BY 1
MAXVALUE 99999999
CYCLE
CACHE 20;

CREATE OR REPLACE TRIGGER BIU_ACCOUNT
BEFORE INSERT OR UPDATE OF account_id ON account
FOR EACH ROW
DECLARE

BEGIN
  IF UPDATING('account_id') THEN
    RAISE_APPLICATION_ERROR(-20001, 'Die Account-ID darf nicht verändert oder frei gewählt werden!');
  END IF;

  IF INSERTING THEN
    :NEW.account_id := seq_account_id.NEXTVAL;
  END IF;
END;
/
```

#### Lösung
Es wird ein Trigger gefeuert, bevor die Account_ID geupdated wird oder eine neue eingefügt wird. 
D.h. wenn ein UPDATE der Account_ID gemacht werden sollten ,wird dies nicht möglich sein, da die ID nicht verändert oder frei gewählt werden darf. 
Wird allerdings eine neue Account ID hinzugefügt,wird diese mittels der sequence um 1 erhöht.-> Neue AccountID = die durch die Sequence 
erhöhte ID


### Aufgabe 4
Verbessere den Trigger aus Aufgabe 2 so, dass
+ wenn versucht wird einen Datensatz mit `NULL` Werten zu füllen, die alten Wert für alle Spalten, die als `NOT NULL` gekennzeichnet sind, behalten bleiben.
+ es nicht möglich ist, das die Werte für `C_DATE` und `U_DATE` in der Zukunkt liegen
+ `U_DATE` >= `C_DATE` sein muss
+ der erste Buchstabe jedes Wortes im Vor- und Nachnamen groß geschrieben wird
+ die Account-ID aus einer `SEQUENCE` entnommen wird

Nutze die Lösung der Aufgabe 2, Aufgabenblatt 8 um die Aufgabe zu lösen. Dort solltest du einige Hilfestellungen finden.

#### Lösung
```sql
CREATE SEQUENCE seq_account_id
START WITH 1000
INCREMENT BY 1
MAXVALUE 99999999
CYCLE
CACHE 20;

CREATE OR REPLACE TRIGGER BIU_ACCOUNT
BEFORE INSERT OR UPDATE OF account_id ON account
FOR EACH ROW
DECLARE

BEGIN
  IF UPDATING('account_id') THEN
    RAISE_APPLICATION_ERROR(-20001, 'Die Account-ID darf nicht verändert oder frei gewählt werden!');
  END IF;

  IF INSERTING THEN
    :NEW.account_id := seq_account_id.NEXTVAL;
  END IF;
END;

BEGIN
  IF UPDATING('account_id') THEN
    RAISE_APPLICATION_ERROR(-20001, 'Die Account-ID darf nicht verändert oder frei gewählt werden!');
  END IF;

  IF INSERTING THEN
    :NEW.account_id := seq_account_id.NEXTVAL;
  END IF;
END;
/
```

### Aufgabe 5
Angenommen der Steuersatz in Deutschland sinkt von 19% auf 17%.
+ Aktualisiere den Steuersatz von Deutschland und
+ alle Quittungen die nach dem `01.10.2017` gespeichert wurden.

#### Lösung
```sql
Deine Lösung
```

### Aufgabe 6
Liste alle Hersteller auf, die LKWs produzieren und verknüpfe diese ggfl. mit den Eigentümern.

#### Lösung
```sql
Deine Lösung
```


























