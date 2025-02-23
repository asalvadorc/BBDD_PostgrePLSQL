# 0. DDL, DML de la BD per als exercicis.

En aquest tema també construirem molts objectes, per tant podem "boicotejar-
nos" entre nosaltres si utilitzem tots el mateix usuari.

És per això que en aquest tema tots els exemples i tots els exercicis els
farem sobre un usuari (i contrasenya) i una Base de Dades anomenada
**geo_grup_9999x** , on heu de substituir **grup** pel codi del vostre grup,
**9999** per les 4 últimes xifres del vostre DNI, i la **x** per la lletra del
vostre NIF. La connexió serà per tant:

!!!note ""
    Servidor: **89.36.214.106**

    Usuari: **geo_grup_9999x** (on **grup** és el codi del vostre grup, **9999**
    són les 4 últimes xifres del vostre DNI, i **x** la vostra lletra del NIF)

    Contrasenya: **geo_grup_9999x**(el mateix d'abans)

    Base de Dades: **geo_grup_9999x** (el mateix d'abans)

<!--
En la Base de Dades **geo_grup_9999x** ja teniu les taules de prova que estem
utilitzant: **COMARQUES** , **POBLACIONS** i **INSTITUTS**.

Per a poder desenvolupar correctament el tema, us faran falta alguns altres
objectes creats en el tema anterior, però observeu com ara no interferireu
entre vosaltres.
-->

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

