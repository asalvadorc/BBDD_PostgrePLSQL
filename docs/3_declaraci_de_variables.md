# 3. Declaració de variables

S'han de declarar totes (excepte les variables comptador dels bucles FOR, com
ja veurem en el seu moment) en el bloc **DECLARE** i els tipus vàlids són els
de SQL (NUMERIC, CHAR, DATE, ...). També es poden declarar de subtipus
definits per l’usuari, com per exemple **lat**.

Aquesta és la sintaxi de declaració de variables:

        
    nom [CONSTANT] tipus [NOT NULL] [{DEFAULT | :=}expressió];

Com veiem, i de forma opcional podem definir les variables com a:

  * **Constants** , i aleshores el seu contingut no podrà variar (haurà de tenir valor inicial).

  * **No nul·les** , i aleshores una assignació del valor nul donarà un error (haurà de tenir valor inicial).

  * **Amb un valor inicial** (a les variables declarades com a constants només se'ls podran donar valors amb aquesta clàusula).

**Per exemple**:

        
    DECLARE
        v1 VARCHAR;
        v2 CONSTANT TEXT := 'Hola';
        v3 NUMERIC(5) := 0;
        v4 DATE NOT NULL DEFAULT '7-7-77';
        v5 lat;
        vec6 NUMERIC(5)[];

Si tenim, com en l'últim exemple, una variable que és d'un tipus compost, la
manera d'accedir a un camp serà separant la variable i el camp per un punt:
**v5.h**. Ara no farà falta posar la variable entre parèntesis, com ens tocava
fer en les sentències SQL.

L'àmbit de les variables és el bloc on es declaren i els blocs "fills", és a
dir aquells blocs definits dins del bloc on està definida la variable. Si
se'ls dóna un valor inicial, aquest valor s'assigna cada vegada que s'entra
dins del bloc (no al principi de l'execució de la funció). Això pot ser
important, ja que en la mateixa execució de la funció si s'entra més d'una
vegada en el bloc, pot tenir resultats diferents.

Per exemple: Utilitzem la funció que ja tenim creada **gent_com** (població de
la comarca especificada). La utilitzem per a inicialitzar una variable en el
DECLARE, i executem aquest bloc dues vegades. Només ens queda canviar la
comarca entre les dues passades.

    
    
    CREATE OR REPLACE FUNCTION moltes_pobl() RETURNS void AS $cos$
    DECLARE aux text := 'Marina Alta';
    BEGIN
    FOR i IN 1..2 LOOP
        DECLARE
            n numeric := gent_com(aux);
        BEGIN
            RAISE NOTICE 'Comarca %: % habitants',aux,n;
        END;
        IF i=1 THEN
            aux:='Marina Baixa';
        END IF;
    END LOOP;
    END; $cos$
    LANGUAGE 'plpgsql';

I per a veure el resultat:

    
    
    SELECT moltes_pobl();

Recordeu que el resultat que traiem amb **RAISE NOTICE** es veu en la pestanya
de **Messages**.

Com veurem un poc més avant, a les funcions se'ls poden passar paràmetres,
però en el moment de definir-los tenim l'opció de posar només de quin tipus
són. La manera de nomenar-los dins de la funció, d'aquesta manera, és **$1** ,
**$2** , ... Per a no haver d'utilitzar uns noms tan impersonals, podem posar
àlies en la zona de declaració:

    
    
    CREATE OR REPLACE FUNCTION iva(numeric) RETURNS numeric AS '
    BEGIN
        RETURN $1 * 0.16;
    END; ' LANGUAGE plpgsql;
    
---
   
    SELECT iva(200);

Ja que estem en la zona de declaració de variables, anem a acabar de comentar
la manera de definir variables.

  * **%TYPE** permet definir variables del tipus equivalent a una altra variable (**v1 v2%TYPE;**).

> La utilitat real és que jo puc definir una variable del mateix tipus que un
> camp d'una determinada taula, i no cal que recorde de quin tipus era aquell.
> Per exemple:
>  

>     v_lat poblacions.lat%TYPE;

  * **%ROWTYPE** : la variable serà de tipus **fila** de la taula esmentada.

> Podrem utilitzar la variable amb camps, ja que equival a tota la fila.
>  
>  
>     CREATE OR REPLACE FUNCTION loc_pobl(text) RETURNS void AS $cos$
>     DECLARE f poblacions%ROWTYPE;
>     BEGIN
>         SELECT * INTO f FROM POBLACIONS WHERE nom=$1;
>         RAISE NOTICE 'Població: %',f.nom;
>         RAISE NOTICE 'Latitud: %',f.latitud;
>         RAISE NOTICE 'Longitud: %',f.longitud;
>     END; $cos$
>     LANGUAGE 'plpgsql';
>  
>  
>     SELECT loc_pobl('Llucena');  
>     

  * **RECORD** és també de tipus **fila** , però agafa la seua estructura en el moment d'efectuar-se la sentència select. És per tant molt més versàtil.

>
>     CREATE OR REPLACE FUNCTION loc_pobl_2(text) RETURNS void AS $cos$
>     DECLARE f RECORD;
>     BEGIN
>         SELECT * INTO f FROM POBLACIONS WHERE nom=$1;
>         RAISE NOTICE 'Població: %',f.nom;
>         RAISE NOTICE 'Latitud: %',f.latitud;
>         RAISE NOTICE 'Longitud: %',f.longitud;
>     END; $cos$
>     LANGUAGE 'plpgsql';
>  
>  
>     SELECT loc_pobl_2('Llucena');



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

