# Tutorium - Grundlagen Datenbanken - Blatt 8

## Vorbereitungen
* Für dieses Aufgabenblatt wird die SQL-Dump-Datei `tutorium.sql` benötigt, die sich im Verzeichnis `sql` befindet.
* Die SQL-Dump-Datei wird in SQL-Plus mittels `start <Dateipfad/zur/sql-dump-datei.sql>` in die Datenbank importiert.
* Beispiele
  * Linux `start ~/Tutorium.sql`
  * Windows `start C:\Users\max.mustermann\Desktop\Tutorium.sql`

## Datenbankmodell
![Datenbankmodell](./img/datamodler_schema.png)

### Aufgabe 1
Erstelle eine Prozedur, die das anlegen von Benutzern durch übergabe von Parametern ermöglicht.

#### Lösung
```sql

CREATE OR REPLACE PROCEDURE add_user(v_surname IN VARCHAR2, v_forename IN VARCHAR2, v_email IN VARCHAR2, v_cdate IN DATE, v_udate IN DATE) 
AS
 
BEGIN
		INSERT INTO ACCOUNT (account_id, surname, forename, email, c_date, u_date)
		VALUES ((SELECT MAX (ACCOUNT_ID) FROM ACCOUNT)+1,v_surname, v_forename,v_email,v_cdate, v_udate);
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    RAISE_APPLICATION_ERROR(-20008, 'Schon vorhanden ');
  WHEN OTHERS THEN
    RAISE_APPLICATION_ERROR(-20010, 'Unbekannter Fehler'||
      SUBSTR(SQLERRM,1,80));
END;
/

```

### Aufgabe 2
Erstelle eine Prozedur, die das erstellen von Quittungen ermöglicht.  
Fange entsprechende übergebene Parameter auf `NULL` oder ` ` ab und gebe eine Meldung aus. Ergänze eventuell Parameter die `NULL` sind mit Informationen die sich durch Abfragen abrufen lassen. 
Berücksichtige die Fehlerbehandlung und mögliche Constraints die gebrochen werden könnten!

#### Lösung
```sql
CREATE OR REPLACE PROCEDURE add_receipt(v_account_id IN NUMBER, v_acc_vehic_id IN NUMBER, v_duty_amount IN NUMBER, v_gasid IN NUMBER, v_gasstationid IN NUMBER, v_pricel IN NUMBER, v_kilometer IN NUMBER, v_liter IN NUMBER, v_receiptdate IN DATE, v_cdate IN DATE, v_udate IN DATE) 
AS
 
BEGIN
		INSERT INTO RECEIPT(receipt_id, account_id, acc_vehic_id, duty_amount, gas_id, gas_station_id, price_l,kilometer, liter, receipt_date, c_date, u_date)
		VALUES ((SELECT MAX (receipt_id) FROM receipt)+1,v_account_id, v_acc_vehic_id,v_duty_amount,v_gasid, v_gasstationid,v_pricel,v_kilometer,v_liter,v_receiptdate, v_cdate,v_udate);
		
IF  v_account_id IS NULL OR v_account_id = ' ' THEN
	DBMS_OUTPUT.PUT_LINE('Keine AccountID eingegeben. Bitte erneut versuchen');
	ELSIF v_acc_vehic_id IS NULL OR v_acc_vehic_id = ' ' THEN
	DBMS_OUTPUT.PUT_LINE('Keine acc_vehic_id eingegeben. Bitte erneut versuchen');
	ELSE
	DBMS_OUTPUT.PUT_LINE('Anderer Fehler');	
END IF;
EXCEPTION
  WHEN NO_DATA_FOUND THEN
    RAISE_APPLICATION_ERROR(-20008, 'Schon vorhanden ');
  WHEN OTHERS THEN
    RAISE_APPLICATION_ERROR(-20010, 'Unbekannter Fehler'|| SUBSTR(SQLERRM,1,80));
END;
/
```

