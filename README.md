# Cas04
Kodovi sa casa 25.3.2023

CREATE TABLE PROIZVOD (
	ID_PROIZVOD SERIAL PRIMARY KEY,  /*SERIAL SAM DODAJE ID */
	NAZIV VARCHAR (30),
	CENA FLOAT,
	KOLICINA INTEGER
);

INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA ) VALUES ('KAFA',250.50,20); /* ZBOG SERIAL-A*/
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('PAPRIKA',150,50);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA ) VALUES('HLEB',90,20);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('MLEKO',280.50,100);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('JOGURT',154.25,650);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('CIPS',120.3,630);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('PASTETA',800.5,10);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('LUK',50,120);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('MILKA',170.25,220);
INSERT INTO PROIZVOD (NAZIV,CENA,KOLICINA )VALUES('SMOKI',50,50);

SELECT * FROM PROIZVOD

#zadatak1

import psycopg2 as psycopg2

con=psycopg2.connect    #pravi vezu sa bazom
(
database='PRODAVNICA',
user='postgres',
password='itoip',
host='localhost',
port='5432'
)
cursor_obj=con.cursor()    #pravi objekat cursor_con
cursor_obj.execute('SELECT * FROM PROIZVOD')    #prosledjuje naredbu bazi
result=cursor_obj.fetchall()                    # ispisuje rezultate i vraća u promenjivu
con.close()
print(result)
print(result[1][2])
for i in result:
    print('ID Proizvoda:',i[0])
    print('Naziv:',i[1])
    print('Cena:',i[2])
    print('Kolicina:',i[3])
    print('\n')

#zadatak2
import psycopg2 as psycopg2

try:                        # pocetak provere greške u programu 
    con=psycopg2.connect(
    database='PRODAVNICA',
    user='postgres',
    password='itoip',
    host='localhost',
    port='5432'
    )
    cursor=con.cursor()
    cursor.execute('''SELECT *         
                    FROM PROIZVOD 
                    WHERE NAZIV LIKE 'S%'
                    ''')
    result=cursor.fetchall() 
    for i in result:
        print("================")
        print ('ID',i[0])
        print ('Naziv',i[1])
        print ('Cena',i[2])
        print ('Kolicina',i[3])
    
except (Exception,psycopg2.Error) as e:
    print("Error",e)

finally:                # izvršava bez obzira na grešku
    if con:
        con.close()     # zatvara ako je otvorena


zadatak 3
mport psycopg2 as psycopg2

try:
    a=input("Unesite slovo: ")
    con=psycopg2.connect(
    database='PRODAVNICA',
    user='postgres',
    password='itoip',
    host='localhost',
    port='5432'
    )
    cursor=con.cursor()
    cursor.execute('''SELECT *         
                    FROM PROIZVOD 
                    WHERE NAZIV LIKE '{}%'
                    '''.format(a))
    result=cursor.fetchall() 
    for i in result:
        print("================")
        print ('ID',i[0])
        print ('Naziv',i[1])
        print ('Cena',i[2])
        print ('Kolicina',i[3])
    
except (Exception,psycopg2.Error) as e:
    print("Error",e)

finally:                # izvršava bez obzira na grešku
    if con:
        con.close()     # zatvara ako je otvorena
   

    




