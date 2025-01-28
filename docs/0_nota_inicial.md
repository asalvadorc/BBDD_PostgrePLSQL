# 0. Nota inicial

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

En la Base de Dades **geo_grup_9999x** ja teniu les taules de prova que estem
utilitzant: **COMARQUES** , **POBLACIONS** i **INSTITUTS**.

Per a poder desenvolupar correctament el tema, us faran falta alguns altres
objectes creats en el tema anterior, però observeu com ara no interferireu
entre vosaltres.

Ací teniu les sentències de creació dels objectes que us faran falta:

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
      
    CREATE DOMAIN graus_lat AS numeric(2)  
      CHECK (VALUE BETWEEN 0 AND 90);  
      
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

