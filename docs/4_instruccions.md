# 4. Instruccions

!!!note "Nota"
    Les instruccions que van a continuació encara no les podrem practicar, perquè
    han de formar part d'alguna funció. Les podrem practicar a partir de la
    pregunta següent

  * **Assignació** : es pot fer de dues maneres

    * Directa, amb l’operador **:=** (a := 10; b := a * 0.5; )
    * Assignar el resultat d’una consulta (una única fila) a una variable o variables amb **INTO**. INTO pot anar abans o després de les columnes seleccionades:

>     SELECT Max(altura) INTO a FROM POBLACIONS;
>  
>     SELECT INTO a Max(altura) FROM POBLACIONS;
>  
>     SELECT Max(altura),Min(altura),Avg(altura) INTO a,b,c
>         FROM POBLACIONS;

  * **Condicional**

  >
        IF condició
             THEN
                 Sentències;
             [ELSE
                 sentències;]
         END IF;

 També es pot utilitzar **ELSIF** que equival a un ELSE seguit de IF.
 D'aquesta manera només hi haurà un END IF al final. És la cosa més pareguda
 al CASE.
  
>      IF condició1
>          THEN Sentències1;
>      ELSIF condició2
>          THEN Sentències2;
>      ELSE
>          Sentències3;
>      END IF;

  * **Bucles** : s’aconsegueixen per mig de **LOOP ...... END LOOP;**

  > * **Bucle incondicional**
 
  >       
        LOOP
              Sentències
        END LOOP;

tal i com està, el bucle és infinit; per eixir **EXIT** o **EXIT WHEN cond**

  > * **Bucle FOR**

  >        
        FOR variable IN [REVERSE] valor_mín .. valor_màx LOOP
              Sentències
        END LOOP;

La variable comptador no s'ha de declarar i només té validesa dins del bucle.

  

  >  * **Bucle WHILE**
      
  >   
        WHILE condició LOOP
            Sentències
        END LOOP;

  * **Sentències SQL** : es poden executar sense problema totes aquelles sentències que no tornen cap resultat (INSERT, UPDATE, DELETE, CREATE TABLE, ...). La sentència SELECT, que sí que torna un valor s'ha d'utilitzar amb la clàusula INTO (com ja hem vist), o dins de PERFORM (com ara veurem).

  * **Execució d'altres funcions**. En moltes ocasions ens farà falta executar una altra funció. Si aquesta torna un valor la posarem dins d'una sentència (assignació, en una condició, ...). Però i si no torna cap valor? El mateix podríem dir d'una sentència SELECT (encara que la utilitat d'açò és més dubtosa). Ho farem per mig de PERFORM, que executa una sentència, ignorant el possible valor tornat per aquesta.

**Per exemple** (recordeu que **loc_pobl,** la funció creada en la pregunta
anterior, no torna cap valor, sinó que ho trau per pantalla):

    
        PERFORM loc_pobl('Aín');
    
        PERFORM (SELECT * FROM POBLACIONS);

  * **Execució en forma dinàmica**. Hi haurà ocasions en que la sentència SQL la voldrem construir en temps d'execució, és a dir de forma dinàmica. Això ens ho permet **EXECUTE** , que el que fa es passar la cadena de caràcters que va a continuació al motor SQL.

**Per exemple:**

    
        EXECUTE 'SELECT ' || $2 || ' FROM ' || $1;

De moment no fa res, perquè el resultat de la sentència es perd, però ja
veurem més avant la seua aplicació. Un altre exemple, on esborraríem les files
d'una taula on un camp coincideix amb un valor (tot passat com a paràmetres):

    
        EXECUTE 'DELETE FROM ' || $1 || ' WHERE ' || $2 || ' = ' || $3;



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

