# 1. Introducció

Una vegada vist amb suficient profunditat el SQL, anem a enfocar l'atac a una
base de dades des d'un altre punt de vista. No com un comando que l'executem i
ens dóna la resposta, sinó des d'un llenguatge procedimental, amb les
estructures de control pròpies d'aquestos (condicionals, bucles, funcions,
...), però accedint òbviament a les dades. Ara, quan fem una consulta
obtindrem un conjunt de dades al qual anomenarem **cursor** , i que segurament
l'haurem de recórrer des del principi fins al final per a fer el tractament
que siga.

La part bàsica de tot açò serà la construcció de funcions. Aquestes es poden
construir utilitzant molts llenguatges, començant per **SQL**, on agruparem
en una funció unes quantes sentències SQL o una sentència complicada. Anem a
veure algun exemple, sobre l'usuari **geo_grup_9999x** , bé des de **psql** o
bé des d'una finestra de SQL de **DBeaver** , que el que fa és sumar la
població dels pobles de la comarca passada com a paràmetre. Hem utilitzat
l'opció **CREATE OR REPLACE** , així en cas que estiga ja creada, dons la
substituirem.

    
    
    CREATE OR REPLACE FUNCTION gent_com(text) RETURNS numeric AS '
            SELECT SUM(poblacio)
                FROM POBLACIONS
                WHERE nom_c=$1;
    ' LANGUAGE SQL;

I ara, així ens dirà quina és la població de **Baix Maestrat** :

    
    
    SELECT gent_com('Baix Maestrat');

O una altra també interessant, on traurem totes les comarques amb la seua
població, utilitzant la funció anterior:

    
    
    SELECT nom_c,gent_com(nom_c)
        FROM COMARQUES;

Però on realment traurem profit és amb els llenguatges procedimentals. Podríem
triar entre molts: **C** , **Tcl** , **Perl** , **Python** , ... En aquest
curs optarem per **PL/pgSQL** (_ProceduraL PostGreSQL_).

En versions anteriors podia passar que s'haguera de preparar la Base de Dades
per a utilitzar el llenguatge. És a dir, podia passar que no estiguera
disponible el llenguatge de programació en la Base de Dades. Aleshores s'havia
d'instal·lar amb la sentència:

    
    
    CREATE PROCEDURAL LANGUAGE plpgsql;

Però **no serà el nostre cas**. Podem utilitzar sense problemes tant el
llenguatge **SQL** com el **PL/pgSQL** , que és el que realment ens interessa.



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

