# Exercicis de tot el tema

En la Base de Dades **geo_local** :  

## **Funciones**{.azul}
 
**Ex_1** - Crea una funció anomenada **DEU_****Q** , que traga els **números del 1
al 10** i els seus **quadrats**. (Utilitza **RAISE NOTICE**).  
  
**Ex_2** - Fes una altra funció, **IMP** , que traga per pantalla els números
**imparells** del 1 al 50. (Utilitza **RAISE NOTICE**).  
  
**Ex_3** - Fes una funció anomenada **TAULA_MULT** , per a que traga la taula de
multiplicar del **paràmetre** que se li ha de passar. (Utilitza **RAISE
NOTICE**). Aquest podria ser el seu aspecte, en executar-la:

![](T7_5_e_1.png)

**Ex_4** - Fes una funció, anomenada **MAX2** , que tinga dos paràmetres
**numèrics** i que **torne el màxim** entre aquestos dos. (Ara ja **no** s'ha
d'utilitzar **RAISE NOTICE**).  
  
**Ex_5** - Utilitza l'anterior per a crear **MAX3**. Has d'utilitzar
obligatòriament la funció **MAX2**  
  
**Ex_6** - (**Voluntari**) Fes la funció **LAT_A_TEXT** , tenint en compte que ha
de quedar com en la taula **POBLACIONS**. Segurament la dificultat més gran
serà aconseguir que apareguen les cometes després dels minuts i dels segons.

## **Cursors**{.azul}

**Ex_7** - Fes una funció anomeneda **POBLACIONS_ALTES** que accepte 2 paràmetres,
el primer de tipus text que serà una comarca, i el segon numèric que serà una
altura. Ha de traure les poblacions de la comarca del primer paràmetre que són
més altes que el segon paràmetre. Mostrarem el nom de la població i l'altura.
Aquest podria ser el resultat en executar-se:

![](T7_6_Ex7.png)

**Ex_8** - Fes una funció anomenada **COMARQUES_NUMPOBLES** sense paràmetres que
traga per pantalla les comarques ordenades alfabèticament amb el número de
pobles de cadascuna

![](T7_6_Ex8.png)

**Ex_9** - Fes una funció anomenada **COMARQUES_NUMPOBLES_NUMINSTITUTS** sense
paràmetres que traga per pantalla les comarques ordenades alfabèticament amb
el número de pobles de cadascuna i el número d'instituts. En la consulta
tindrem dos dificultats:

  * Hem d'agafar totes les poblacions, fins i tot les que no tenen institut
  * Com que hem d'accedir als instituts, per a comptar els pobles haurem de comptar els pobles distints, i així si un poble té més d'un institut, no comptar-lo més d'una vegada

![](T7_6_Ex9.png)

**Ex_10** - Fes una funció anomenada **NUM_HABITANTS_COMARCA** que accepte un
paràmetre de tipus text, i torne el número d'habitants d'eixa comarca

![](T7_6_Ex10.png)

**Ex_11** - Fer la funció **COMARQUES_NUMHABITANTS** sense paràmetres per a traure
per pantalla totes les comarques i el número d'habitants. En la consulta has
d'utilitzar obligatòriament la funció anterior

![](T7_6_Ex11.png)


**Ex_12:** Crea una funció que prenga el nom d’una comarca com a paràmetre i mostre una llista de poblacions d’eixa comarca juntament amb els seus habitants.

      select lista_poblaciones_por_comarca('Racó');


      Población: Ademuz -- habitantes:1179
      Población: Casas Altas -- habitantes:149
      Población: Casas Bajas -- habitantes:195
      Población: Castielfabib -- habitantes:282
      Población: Vallanca -- habitantes:156
      Población: Torrebaja -- habitantes:429
      Población: Puebla de San Miguel -- habitantes:71


**Ex_13:** Crea una funció que mostre el nom de la comarca i la mitjana d’altura de totes les poblacions de la mateixa comarca, ordenat per comarca. Al final, retorna el nombre total de comarques.

      Comarca: Alt Vinalopó -- Promedio altura: 580.1428571428571429
      Comarca: Baix Maestrat -- Promedio altura: 316.4444444444444444
      Comarca: Baix Segura -- Promedio altura: 25.8518518518518519
      Comarca: Baix Vinalopó -- Promedio altura: 74.0000000000000000
      Comarca: Camp de Morvedre -- Promedio altura: 95.3125000000000000
      Comarca: Camp de Túria -- Promedio altura: 198.4000000000000000
      Comarca: Canal de Navarrés -- Promedio altura: 261.5000000000000000
      Comarca: Comtat -- Promedio altura: 552.4583333333333333
      Comarca: Costera -- Promedio altura: 170.6842105263157895
      Comarca: Foia de Bunyol -- Promedio altura: 361.8888888888888889
      Comarca: Horta Nord -- Promedio altura: 22.0476190476190476
      ..............................
      total comarcas:34


**Ex_14:** Crea una funció que mostre el nom de la població i la quantitat d’instituts associats, inclús les que tenen 0 instituts, ordenat pel nombre d’instituts.

      ............................
      Población: Xàtiva -- Institutos: 3
      Población: Xella -- Institutos: 0
      Población: Xeraco -- Institutos: 1
      Población: Xeresa -- Institutos: 0
      Población: Xert -- Institutos: 0
      Población: Xilxes -- Institutos: 0
      Población: Xirivella -- Institutos: 2
      Población: Xixona -- Institutos: 1
      Población: Xodos -- Institutos: 0
      Población: Yátova -- Institutos: 0
      Población: Yesa, la -- Institutos: 0
      Población: Zarra -- Institutos: 0
      Población: Zucaina -- Institutos: 0

**Ex_15:**  Crea una funció que prenga el nom d’una comarca com a paràmetre i mostre la població i l’altura de la població amb l’altura més alta.

      select altura_maxima_por_comarca('Alacantí');

      Población: Torre de les Maçanes, la --  altura máxima: 788


**Ex_16:** Crea una funció que mostre el nom i l’altura de les poblacions que tenen alçades superiors a la mitjana.

      Población: Ademuz --  altura: 660
      Población: Agost --  altura: 376
      Población: Agres --  altura: 722
      Población: Agullent --  altura: 360
      Población: Aigües --  altura: 341
      Población: Aín --  altura: 498
      Población: Albaida --  altura: 315
      Población: Albocàsser --  altura: 538
      Población: Alborache --  altura: 320

**Ex_17:** Crea una funció que prenga dos noms de províncies com a paràmetres i retorne la diferència absoluta de població entre totes dues províncies.

      select diferencia_poblacion_entre_provincias('València', 'Alacant');

      RETURN: 680.460

**Ex_18:** Crea una funció que mostre el nom de les poblacions que no tenen instituts associats en la taula instituts, ordenat per població.

      Población: Ador
      Población: Agres
      Población: Agullent
      Población: Aielo de Rugat
      Población: Aigües
      Población: Aín
      Población: Albalat dels Sorells
      Población: Albalat dels Tarongers
      Población: Albocàsser
      Población: Alborache
      Población: Albuixech
      Población: Alcalalí

**Ex_19:** Crea una funció que mostre el nom de les poblacions que tenen una població per davall de la mitjana.
      
      Promedio= 9234.0295

      Población: Ademuz habitantes: 1179
      Población: Ador habitantes: 1411
      Población: Agost habitantes: 4752
      Población: Agres habitantes: 583
      Población: Agullent habitantes: 2435
      Población: Aielo de Malferit habitantes: 4657
      Población: Aielo de Rugat habitantes: 166
      Población: Aigües habitantes: 984
      Población: Aín habitantes: 129
      Población: Albaida habitantes: 6031


**Ex_20:** Crea una funció que, donat el nom d’una població i d’una comarca, ens permeta establir la llengua per a eixa població.

      SELECT SET_LLENGUA('Almudaina','Comtat','V');

      RETURN: void

**Ex_21:** Crea una funció anomenada Densitat_centres que, donat el nom d’una comarca, ens retorne la quantitat de centres que té per unitat de superfície.

      SELECT DENSIDAD_CENTRES('Plana Alta');

      RETURN: 0.0219

**Ex_22:** La mateixa funció de l’exercici anterior però utilitzant un cursor explícit.


**Ex_23:** Crea una funció, utilitzant almenys un cursor explícit, anomenada ALTURA_MITJA, que ens permeta obtindre l’altura mitjana a què estan els centres en funció de la comarca i de la llengua de la població (aquests seran els paràmetres d’entrada).


      SELECT ALTURA_MITJA ('Comtat'.'v');

      RETURN: 455


**Ex_24:** Crea una funció, utilitzant cursors, anomenada POBLACIONS_GRANS, que donat el nom d’una comarca ens retorne els noms de les poblacions de la comarca que tenen una població superior en un 50% a la mitjana de població de la província.


      
![](T7_e13.png)
      

**Ex_25:** Crea una funció, utilitzant cursors, anomenada CENTRES_DUO, que donat el nom d’una comarca ens retorne la quantitat total de centres de les dues poblacions amb un major nombre d’habitants.


![](T7_e14.png)

**Ex_26:** Crea una funció anomenada INTRODUCIR_INSTITUTO(varchar, varchar, varchar, varchar, numeric, numeric), que accepte els paràmetres indicats, un per cada camp de la taula INSTITUTS, i que comprove:

- Que el primer paràmetre, el codi de l’institut, tinga exactament 8 caràcters i que comence per 03, 12 o 46 (els codis de província).
- Que el codi postal estiga entre 3001 i 3999, 12001 i 12999 o 46001 i 46999. Observa que cod_m no farà falta comprovar-lo, ja que és clau externa i apareixeria un error si no fora un codi de municipi existent.


## **Trigger**{.azul}

**Ex_27** - Crear un trigger anomenat **TR_ALT_POS** que controle que l'altura
d'una nova població siga estrictament positiva. La funció en la qual es basa
es pot anomenar **ALT_POS**.

**Ex_28** - Modificar l'anterior per a que ho controle també quan es tracta d'una
modificació.

**Ex_29** - Crear un trigger anomenat **TR_EXT_0_1000** que controle que l'extensió
d'un municipi (població) estiga obligatòriament entre 0 i 1000, i ha de ser
sempre, tant si s'insereix una nova població com si es modifica. Però en
aquesta ocasió, en compte de traure un error, el que farem serà modificar
aquest valor: si és major que 1000, li donarem el valor 1000, i si és negatiu
li posarem 0. Ho aconseguirem modificant **NEW.extensio** , i com la funció
del trigger torna sempre NEW, doncs agafarà el nou valor. Anomeneu a la funció
**EXT_0_1000**.

**Ex_30** - **VOLUNTARI**. En la taula POBLACIONS3 tenim controlat que la latitud
introduïda siga correcta per mig del tipus lat, però no en la taula
POBLACIONS, on és de tipus VARCHAR(50) i per tant es podria introduir una
latitud incorrecta molt fàcilment. 
Crea un trigger que controle que quan s'introdueix o es modifica la **latitud** de **POBLACIONS** siga correcta. Per a això

  * Els caràcter 1 i 2 han de ser els **graus** , que han d'estar entre 00 i 90
  * El caràcter 3 ha de ser **º**
  * Els caràcters 4 i 5 formen els **minuts** , i han d'estar entre 00 i 59
  * El caràcter 6 ha de ser **'**
  * Els caràcters 7 i 8 formen els **segons** , i han d'estar entre 00 i 59
  * El caràcter 9 ha de ser **"**
  * El caràcter 10 ha de ser **N** o **S**
  * Si no s'acompleix alguna de les restriccions anteriors, ha d'eixir un error dient que la latitud ha d'estar entre 00º00'00"N i 90º00'00"N , o entre 00º00'00"S i 90º00'00"S

**Ex_31:** Crea un trigger que, després d’una inserció, actualitze automàticament la quantitat total d’habitants en la taula provincies cada vegada que s’inserix una nova població en la taula poblacions.


**Ex_32:** Crea un trigger que evite l’actualització del nom d’una població en la taula poblacions3 si existeix la comarca.


**Ex_33:** Crea un trigger que evite la inserció d’un nou institut en la taula instituts si el codi de la població associada no existeix en la taula poblacions.


**Ex_34:** Crea un trigger, anomenat MOD_LLEN, que ens avise quan una població canvia de llengua majoritària. 

![](T7_t4.png)

**Ex_35:** Crea un trigger per a portar una auditoria de la taula INSTITUTS per a controlar totes les modificacions que es fan en la taula. Per a això, per cada operació feta introduirem una fila en la taula AUDIT_INSTITUT (crear-la prèviament si no existeix) amb la informació següent:

- num_a: és la clau principal de la taula, que serà un autonumèric (SERIAL).
- operacio: contindrà el tipus d’operació realitzada en la taula INSTITUTS, que podrà ser: INSERT, DELETE o UPDATE.
- codi_institut: codi de l’institut afectat per l’operació.
- usuari: usuari que ha realitzat l’operació; es pot obtindre amb current_user. Podríem pensar que sempre serà el mateix usuari que fa l’operació, però en realitat la pot fer qualsevol usuari que tinga permís d’accés a la Base de Dades.
- data_op: data-hora (timestamp) de l’actualització; es pot obtindre amb la funció now().

![](T7_t5.png)

En la imatge s’observa com s’han fet 3 actualitzacions des del moment de creació del trigger, l’última d’elles realitzada per l’usuari postgres.

**Ex_36:** Crea un trigger que registre automàticament en una taula d’auditoria cada vegada que s’actualitza la població en la taula poblacions, però només si la població augmenta en més d’un 10 %. En la taula es guardarà el valor de la població abans de ser actualitzada. Crear prèviament la taula audit_poblacions, si no existeix, amb la informació següent:

- cod_m: codi de població
- data: data de la modificació
- poblacio_anterior: població abans de l’actualització.


<!--
**Ex_16** - Crear els dos **operadors de comparació** que quedaven per al tipus
**lat** : **< **i **< =**

**Ex_17** - Crear la funció d'agregat **MIN** per al tipus de dades **lat**.

-->
<!--
**Ex_18** - Fes una funció en PL/pgSQL anomenada
**DENSITAT_CENTRES** que donat el nom d'una comarca ens torne la quantitat de
centres que té per unitat de superfície.

![](T7_Ex_18.png)

**Ex_19** - Fes una funció anomenada
**introduir_institut(varchar,varchar,varchar,varchar,numeric,numeric)** , que
accepte els paràmetres indicats, un per cada camp de la taula INSTITUTS, que
comprove:

  * Que el primer paràmetre, el codi de l’institut, tinga exactament 8 caràcters i que comence per 03, 12 o 46 (els codis de província)
  * Que el codi postal estiga entre 3001 i 3999, 12001 i 12999 o 46001 i 46999
  * Observa que el cod_m no caldrà comprovar-lo, ja que és clau externa i saltaria l’error si no és un codi de municipi existent

En cas que tot siga correcte, s’ha d’introduir el nou institut. En cas
contrari ha de saltar un error

**Ex_20** - Fes un trigger per a portar una auditoria de la taula
**INSTITUTS** per a controlar totes les modificacions que es fan en la taula
INSTITUTS. Per a això per cada actualització feta, introduirem una fila en la
taula nova anomenada**AUDIT_INSTITUT** (creant-la prèviament si no existeix)
amb la següent informació:

  * **num_a** : és la clau principal de la taula, que serà un autonumèric (SERIAL)
  * **operacio** : contindrà el tipus d’operació d’actualització realitzada en la taula INSTITUTS, que podrà ser: INSERT, DELETE o UPDATE
  * **codi_institut** : codi del institut afectat per l’operació d’actualització
  * **usuari** : usuari que ha realitzat l’operació d’actualització; es pot obtenir amb **current_user** ;  
podríem pensar que sempre serà el mateix usuari qui fa l’operació, però en
realitat ho pot fer tot usuari que tinga permís d’accés a la Base de Dades. En
la imatge es pot observar com l’usuari **postgres** també ha fet una operació
d’actualització

  * **data_op** : data-hora (timestamp) de l’actualització; es pot obtenir amb la funció **now()**

En la imatge s’observa com s’han fet 3 actualitzacions des del moment de
creació del trigger, l’ultima d’elles realitzada per l’usuari **postgres**.
Evidentment, la manera de comprovar-lo vosaltres és fer operacions
d'actualització i el resultat ha de ser obligatòriament deferent:

![](T7_Ex_20.png)
-->



Llicenciat sota la  [Llicència Creative Commons Reconeixement NoComercial
CompartirIgual 3.0](http://creativecommons.org/licenses/by-nc-sa/3.0/)

