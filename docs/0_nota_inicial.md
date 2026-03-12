# 0. DDL, DML de la BD per als exercicis.

En aquest tema també construirem molts objectes, per tant, en lloc de fer ús d’un servidor allotjat al núvol, treballareu amb un servidor **PostgreSQL de manera local**, utilitzant contenidors **Docker**. En tot cas, seguirem utilitzant el client **DBeaver** per connectar-nos i gestionar la base de dades. Tots els exemples i tots els exercicis els farem sobre una Base de Dades anomenada **geo_local** dins de la nostra connexió **postgres_local**.


!!!note "Dins de la connexió postgres_local"
    - **Host**: localhost
    - **Port**: 5432
    - **Database**: geo_local
    - **Username**: admin
    - **Password**: admin

!!!Warning "Importante"
    Us recomane que us creeu una altra connexió per a **geo_local**. 


Ací teniu les sentències de creació dels objectes que us faran falta:

* Creació de la taula **COMARQUES**:
>
      CREATE TABLE public.comarques (
        nom_c varchar(50) NOT NULL,
        provincia varchar(25) NULL,
        CONSTRAINT cp_com PRIMARY KEY (nom_c));

* Creació de la taula **POBLACIONS**:    
>
    CREATE TABLE public.poblacions (
      cod_m numeric(5) NOT NULL,
      nom varchar(50) NOT NULL,
      poblacio numeric(6) NULL,
      extensio numeric(6, 2) NULL,
      altura numeric(4) NULL,
      longitud varchar(50) NULL,
      latitud varchar(50) NULL,
      llengua bpchar(1) NULL,
      nom_c varchar(50) NULL,
      CONSTRAINT cp_pobl PRIMARY KEY (cod_m),
      CONSTRAINT ce_pob_com FOREIGN KEY (nom_c) REFERENCES public.comarques(nom_c) ON UPDATE CASCADE);

* Creació de la taula **INSTITUTS**:    
>
      CREATE TABLE public.instituts (
        codi varchar(8) NOT NULL,
        nom varchar(60) NULL,
        adreca varchar(100) NULL,
        numero varchar(5) NULL,
        codpostal numeric(5) NULL,
        cod_m numeric(5) NULL,
        CONSTRAINT cp_ins PRIMARY KEY (codi),
        CONSTRAINT ce_ins_pob FOREIGN KEY (cod_m) REFERENCES public.poblacions(cod_m));
     

* Inserció de dades en la taula **COMARQUES**:  
>    
   [COMARQUES.sql](dades comarques.sql)    
              
* Inserció de dades en la taula **POBLACIONS**:  
>
   [POBLACIONS.sql](dades poblacions.sql) 

* Inserció de dades en la taula **INSTITUTS**:  
>
   [INSTITUTS.sql](dades instituts.sql) 

* Creació de la taula **PROVINCIES**:

>
      CREATE TABLE PROVINCIES AS  
      SELECT provincia, SUM(poblacio) AS habitants, SUM(Q) AS instituts  
        FROM (COMARQUES INNER JOIN POBLACIONS ON COMARQUES.nom_c=POBLACIONS.nom_c)  
          LEFT JOIN (SELECT cod_m, count(*) AS Q  
                      FROM INSTITUTS  
                      GROUP BY cod_m) I ON POBLACIONS.cod_m=I.cod_m  
        GROUP BY provincia;

* Creació dels dominis **hemi_lat** , **graus_lat** , i **min_seg** :

>
      CREATE DOMAIN hemi_lat AS char(1)  
        CHECK (VALUE IN ('N','S'));  
>        
      CREATE DOMAIN graus_lat AS numeric(2)  
        CHECK (VALUE BETWEEN 0 AND 90);  
>        
      CREATE DOMAIN min_seg AS numeric(2)  
        CHECK (VALUE BETWEEN 0 AND 59);

* Creació del tipus **lat** :

>
      CREATE TYPE lat AS (  
        h hemi_lat,  
        g graus_lat,  
        m min_seg,  
        s min_seg );

* Creació de la taula **POBLACIONS3** :

>
      CREATE TABLE POBLACIONS3 (  
        nom VARCHAR(50) CONSTRAINT cp_pob3 PRIMARY KEY,  
        latitud lat,  
        comarca varchar(50) );



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

