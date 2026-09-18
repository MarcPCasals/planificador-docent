# Especificació funcional acordada — Planificació, Agenda i Mode aula

Data de consolidació: 18 de setembre de 2026

## 1. Finalitat i estat del document

Aquest document reuneix les decisions funcionals preses abans de començar la implementació. Ha de servir com a font de veritat per evitar que es perdi cap funció de les aplicacions antigues i per preparar, més endavant, un pla d'acció ordenat.

Encara no és el pla d'implementació. Les decisions marcades com a acordades defineixen el producte; l'últim apartat recull les qüestions que encara cal acabar de decidir.

Documents complementaris:

- `AUDITORIA-INICIAL.md`: inventari fidel de l'Agenda Docent i el Programador Docent actuals.
- `docs/INFRAESTRUCTURA.md`: situació dels repositoris i projectes Firebase.
- Plantilles de referència facilitades pel docent:
  - `Instruccions UP Taller- Gener 2023.docx.pdf`;
  - `Icones UP - Abril 2023.docx`;
  - `Còpia de Plantilla_seqüència_taller-2023.docx`;
  - exemple complet `Taller 1.1 CFN.docx`.

## 2. Decisió principal de producte

Planificació, Agenda i Mode aula formaran part d'AvaluaPro com a mòduls diferenciats. No seran dues aplicacions definitives obligades a sincronitzar constantment alumnat, grups, absències, diagnòstics, tasques i constància.

La integració funcional no implica carregar-ho tot alhora. Cada mòdul carregarà només les dades necessàries:

- l'inici carrega la jornada d'avui, els grups i els recordatoris necessaris;
- l'Agenda carrega el període consultat;
- Programació carrega la UP seleccionada;
- l'històric es carrega quan el docent el consulta;
- Mode aula carrega el grup i la sessió corresponents.

El repositori i Firebase `planificador-docent` es conservaran com a espai de definició, desenvolupament i proves. La incorporació a les dades reals d'AvaluaPro només es farà després d'un pilot validat.

## 3. Terminologia i jerarquia

- **UT — Unitat Temporal:** període del curs semblant a un trimestre. El docent configura cada inici de curs les dates d'inici i final de cada UT, perquè poden canviar anualment.
- **UP — Unitat de Programació:** document de programació pedagògica que conté la seqüència ideal d'activitats.
- **Sessió de calendari:** classe concreta d'un grup en una data i hora.
- **Aplicació real:** allò que finalment ha passat amb una UP en un grup concret.

Jerarquia acordada:

```text
Curs acadèmic
└── UT — Unitat Temporal
    └── UP — Unitat de Programació
        ├── informació general
        ├── competències, aprenentatges, criteris i indicadors
        ├── fases i subfases
        └── activitats
            └── aplicació a les sessions reals de cada grup
```

## 4. Espais principals de l'aplicació

La navegació principal mantindrà AvaluaPro cohesionat:

- **Agenda** serà una entrada principal i obrirà la pantalla Avui.
- **Programació** serà una entrada principal separada.
- **Avaluació, Seguiment i Estadístiques** continuaran agrupats com en l'AvaluaPro actual.
- **Tutoria** continuarà sent un botó diferenciat.
- El grup actiu es mantindrà visible a la capçalera, amb el seu color.
- Hi haurà l'opció **Tots els grups** per consultar la jornada i els recordatoris generals.

### 4.1 Avui

Serà la pantalla inicial d'Agenda. No substituirà la pantalla general d'AvaluaPro ni apareixerà fora d'Agenda. Mostrarà:

- sessions del dia;
- pròxima classe;
- materials que cal preparar;
- recordatoris d'avui i dels tres dies següents, encara que no coincideixin amb una classe d'avui;
- recuperacions pendents;
- tasques rellevants;
- accés ràpid a la setmana completa i a la cronologia de cada grup.

### 4.2 Programació

Contindrà la seqüència pedagògica ideal i substituirà el Programador Docent antic. Permetrà construir una UP completa, flexible i reordenable, amb el mateix contingut que direcció espera trobar en una programació.

L'editor tindrà tres zones:

- esquerra: esquema de fases i activitats;
- centre: contingut de l'activitat seleccionada;
- dreta: resum, indicadors, adaptacions i avisos.

La zona dreta es podrà amagar per ampliar l'espai d'edició.

### 4.3 Agenda

Contindrà l'adaptació real de les UP per a cada grup, data i hora. El docent podrà canviar l'ordre, eliminar activitats per a un grup, afegir-ne, dividir-les i reajustar-les sense perdre la UP base.

### 4.4 Mode aula

Serà la pantalla operativa durant una classe. Reunirà en un mateix lloc les activitats i l'alumnat, amb accés ràpid a assistència, tasques, adaptacions, comportament, materials, notes i recordatoris.

## 5. Funcions de les aplicacions antigues que s'han de preservar

Cap funció útil de l'Agenda Docent o del Programador Docent s'ha de perdre durant la migració. Com a mínim s'han de conservar o millorar:

- inici de sessió i persistència al núvol;
- configuració del curs acadèmic;
- grups i colors identificatius;
- horari setmanal i durada de cada franja;
- sessions de 60, 90 i 120 minuts, i durades extraordinàries configurables;
- setmanes no lectives, festius, dies especials i motius;
- classes extraordinàries;
- vista diària, setmanal, calendari i cronologia per grup;
- fases, sessions i activitats reordenables;
- activitats amb durada prevista;
- materials, enllaços d'alumnat i de docent;
- notes de preparació i observacions posteriors;
- còpia d'activitats i sessions entre dates, grups i UP;
- activitats inacabades que passen a la sessió següent;
- cancel·lació d'una classe i reprogramació del contingut;
- recordatoris i radar de pendents;
- importació massiva amb previsualització;
- exportacions i còpies de seguretat;
- historial de desfer i refer quan sigui segur;
- vista de progrés per grup;
- migració verificable de les dades antigues.

L'intercanvi fràgil de dades entre les dues aplicacions antigues no es conservarà: Programació, Agenda i Mode aula treballaran sobre les mateixes entitats.

## 6. Contingut de la UP

La UP ha de permetre introduir i consultar, com a mínim:

- codi, nivell i títol;
- UT i curs acadèmic;
- situació o pregunta complexa;
- proposta de producció o producte;
- llengua de vehiculació;
- competències;
- aprenentatges esperats;
- criteris d'avaluació;
- indicadors d'avaluació;
- recursos de competències específiques i transversals;
- fets i conceptes;
- procediments;
- actituds i valors;
- fases de preparació, resolució i tancament;
- subfases pedagògiques flexibles i reordenables;
- activitat i descripció;
- atenció a la diversitat;
- comentaris per a l'aplicació;
- temps previst;
- materials per al docent i l'alumnat;
- agrupament i espai;
- indicadors associats;
- total de temps de cada fase i total de la UP.

Les subfases no seran una seqüència rígida: es podran repetir, fusionar i moure d'acord amb la necessitat pedagògica.

La vista d'edició utilitzarà una interfície clara i actual. No cal imitar visualment la taula Word mentre s'edita, però direcció podrà consultar tots els mateixos apartats.

## 7. Versions anuals i biblioteca històrica

- Cada curs es podrà crear una còpia nova d'una UP anterior.
- Les versions dels cursos anteriors es conservaran intactes.
- El docent podrà modificar la versió nova sense por de perdre activitats antigues.
- Serà fàcil buscar i copiar una activitat d'una UP de cursos anteriors.
- En copiar-la es conservaran descripció, durada, materials, adaptacions i indicadors.
- La còpia podrà recordar discretament de quina UP i curs provenia.
- Les programacions històriques només es carregaran quan es consultin.

## 8. UP base i aplicació per grups

Una mateixa UP base es podrà utilitzar amb diversos grups. Cada grup tindrà una Agenda pròpia i podrà avançar a un ritme diferent.

Quan el docent canviï una activitat des de l'Agenda d'un grup, podrà escollir:

1. aplicar el canvi només a aquell grup;
2. modificar també la UP base;
3. aplicar-lo al grup actual i proposar-lo als altres grups vinculats.

La programació ideal i l'aplicació real quedaran relacionades, però no es confondran.

## 9. Enviament de la UP a l'Agenda

Hi haurà dues maneres de treballar:

### 9.1 Assignació progressiva

És l'opció preferida inicialment pel docent. Permetrà anar incorporant activitats o blocs a l'Agenda a mesura que la programació es concreta.

### 9.2 Distribució automàtica completa

L'aplicació podrà:

1. llegir l'horari del grup;
2. llegir la durada de les sessions;
3. repartir les activitats segons els minuts previstos;
4. saltar festius i dies no lectius;
5. mostrar una previsualització;
6. permetre moure, dividir o eliminar propostes;
7. crear les sessions només després de la confirmació del docent.

Una activitat de 120 minuts continuarà sent una única activitat pedagògica, encara que es distribueixi en dues sessions de 60 minuts. Les parts conservaran el vincle amb l'activitat original.

## 10. Pressupost de temps

La durada disponible de cada sessió vindrà de l'horari, amb possibilitat d'excepcions.

Per defecte es reservaran cinc minuts de marge:

- sessió de 60 minuts: 55 minuts programables;
- sessió de 90 minuts: 85 minuts programables;
- sessió de 120 minuts: 115 minuts programables.

Cada sessió mostrarà:

- minuts programats;
- durada disponible;
- avís visual quan s'apropa o supera el límit.

Els llindars acordats són:

- verd: fins al 85% del temps programable;
- taronja: del 86% al 100%;
- vermell: quan se supera el 100%.

Si una activitat o continuació supera el temps disponible, el docent podrà:

1. mantenir la sobrecàrrega;
2. seleccionar què passa a la sessió següent.

L'aplicació podrà proposar les activitats finals que convindria moure, però no farà el canvi sense confirmació.

Les desviacions de temps real respecte del previst seran visibles per direcció com a part de l'aplicació real.

### 10.1 Temporitzador opcional

- Cada activitat temporitzada podrà activar un compte enrere amb un botó.
- No farà cap so.
- En arribar a zero continuarà comptant en positiu per mostrar l'excés.
- En aturar-lo, el temps real passarà automàticament al resum.
- El docent podrà indicar que l'activitat havia acabat abans de prémer el botó.
- Hi haurà botons ràpids `Fa 1`, `Fa 2`, `Fa 5` i `Fa 10 minuts`, més l'opció **Altre**.
- Finalitzar una activitat deixarà la següent preparada, però el nou temporitzador només començarà quan el docent premi **Comença**.

### 10.2 Elements de la cronologia

Una sessió podrà contenir tres tipus d'elements:

1. **Activitat:** pot tenir temps, materials, adaptacions i seguiment.
2. **Indicació:** recordatori breu sense temps, com ara «Agafar la bata».
3. **Pausa o transició:** pot tenir temps, però no és una activitat pedagògica.

Els elements sense temporització:

- apareixeran en l'ordre correcte dins de la cronologia;
- no sumaran minuts;
- no afectaran el color del pressupost de temps;
- es podran marcar com a completats.

No es crearà una biblioteca d'indicacions reutilitzables.

## 11. Activitats fetes i continuacions

Per reduir al màxim les accions durant la classe:

- una activitat es considerarà feta si el docent ha obert Mode aula i no indica cap excepció;
- no s'utilitzaran estats de pendent o en curs durant la classe;
- l'acció principal per a una activitat inacabada serà **Continuarà**;
- si Mode aula no s'ha obert, l'aplicació no donarà la sessió automàticament per feta i demanarà què ha passat;
- una continuació es proposarà al començament de la pròxima sessió;
- si provoca sobrecàrrega, es podrà mantenir o reajustar la seqüència.

## 12. Mode aula

### 12.1 Activació contextual

- Cinc minuts abans de la classe apareixerà un avís per obrir Mode aula.
- L'aplicació no canviarà de pantalla sense avisar.
- Durant la classe es mantindrà la vista del grup i la sessió.
- En acabar, tornarà al resum del dia després del tancament o deixarà un pendent si cal revisar alguna cosa.

Exemple d'avís:

> 1r D comença a les 9.30. Tens 3 activitats, 2 materials i una tasca de seguiment preparada. Obrir Mode aula.

### 12.2 Contingut simultani

La pantalla mostrarà simultàniament:

- activitats, durades i materials;
- alumnat del grup;
- assistència;
- adaptacions de l'activitat;
- tasques de seguiment;
- registres de comportament;
- notes i recordatoris.

La prioritat de disseny serà l'ordinador. L'iPad tindrà una versió més compacta, però conservarà totes les accions essencials.

El flux de l'alumnat serà:

1. En entrar, activitats i llista d'alumnes apareixen simultàniament.
2. El docent passa i confirma la llista.
3. Després, els noms passen a un segon pla per deixar més espai a les activitats.
4. Un botó torna a obrir el panell de l'alumnat per registrar absència, sortida, comportament o altres accions individuals.
5. Un altre botó obre el seguiment de tasques quan la sessió conté activitats que generen evidència.

### 12.3 Resum final

El resum final només necessita mostrar:

- alumnat absent o que ha marxat;
- tasques pendents;
- recordatoris creats;
- camp opcional de reflexió o notes.

No cal repetir les activitats que s'han fet correctament.

## 13. Cancel·lació d'una classe

L'acció **No s'ha fet la classe**:

- demanarà opcionalment el motiu;
- traslladarà les activitats a la pròxima sessió;
- conservarà materials i adaptacions;
- reajustarà la resta de sessions després de la confirmació;
- quedarà reflectida en l'aplicació real que pot consultar direcció.

## 14. Assistència, sortida i recuperació

Només es necessita distingir:

- absència completa;
- sortida a mitja sessió.

No es registraran retards.

### 14.1 Absència completa

- Se selecciona l'alumne.
- Les activitats recuperables de la sessió apareixen seleccionades per defecte.
- El docent pot desmarcar les que no cal recuperar.

### 14.2 Sortida a mitja sessió

- Es prem el botó de sortida.
- Se selecciona l'alumne.
- El docent selecciona directament les activitats que s'ha perdut.

### 14.3 Conseqüències

- Les activitats marcades queden associades a l'alumne.
- Si una activitat és una tasca per entregar, queda automàticament pendent.
- Una absència justificada no compta com una tasca no feta per a la constància.
- Es crea un recordatori per a la pròxima sessió.
- Quan la tasca es recupera, el recordatori actiu desapareix.
- Es conserva l'historial i la data de recuperació.

## 15. Text de correu per copiar

AvaluaPro no enviarà correus ni gestionarà destinataris. Només prepararà un text editable perquè el docent el copiï i l'enganxi al seu correu habitual.

Hi haurà dues plantilles:

1. absència completa;
2. sortida a mitja sessió.

El text podrà incloure:

- nom de pila de l'alumne;
- data i assignatura;
- activitats seleccionades;
- tasques que cal entregar;
- data límit, si existeix;
- pròxima sessió;
- materials i enllaços vinculats;
- espai per afegir una nota.

Si el registre té format `COGNOMS, Nom`, s'utilitzarà només el nom. Es preveu un camp opcional de nom habitual.

Abans de copiar, el docent podrà editar el text i eliminar activitats, materials o fragments.

## 16. Tasques i constància

Una activitat de la programació es podrà marcar com a activitat que genera seguiment o evidència de constància.

- A Mode aula apareixerà preparada, sense crear encara un resultat negatiu.
- La tasca s'activarà quan es confirmi que realment s'ha treballat.
- Una activitat prevista però ajornada no afectarà la constància.
- El docent podrà decidir si una activitat llarga genera una única evidència final o registres parcials per sessió.
- El valor predeterminat serà una única evidència al final de l'activitat.
- La graella permetrà registrar l'estat dels alumnes des de Mode aula sense anar a una altra pantalla.

## 17. Comportament i notes

Durant Mode aula, el docent podrà seleccionar un alumne i registrar un comportament. El registre:

- quedarà associat a l'alumne, grup, UP, sessió, data i hora;
- s'integrarà en el registre i les estadístiques d'AvaluaPro;
- no serà visible per direcció dins de la programació;
- podrà incloure una nota privada.

S'utilitzaran les mateixes categories de comportament que ja existeixen a AvaluaPro. Apareixeran com a botons ràpids per evitar text lliure innecessari i mantenir registres homogenis. Es podran seleccionar diversos alumnes i aplicar-los el mateix registre.

Hi haurà dos tipus de notes de sessió:

- **Reflexió pedagògica:** visible per direcció com a part de l'aplicació real.
- **Nota privada:** només visible per al docent autoritzat.

La selecció múltiple no impedirà revisar o completar després cada registre individual.

### 17.1 Revisió posterior d'una activitat

Després de fer una activitat, el botó **Revisar** permetrà modificar o afegir:

- temps real;
- comentari d'aplicació;
- reflexió pedagògica;
- materials que han faltat;
- adaptacions que han funcionat o no;
- recomanació de conservar, modificar o retirar l'activitat el curs següent.

Els camps buits no generaran cap registre.

La UP actual mostrarà en vermell les activitats que han durat més del previst, amb comparació per grup. Aquesta desviació serà visible per direcció.

Quan es prepari la versió del curs següent, AvaluaPro proposarà millores basades en:

- temps previst i temps real;
- activitats que sovint han continuat;
- activitats descartades en algun grup;
- materials que han generat problemes o avisos;
- adaptacions valorades com a útils;
- comentaris de revisió.

Les propostes es podran acceptar una a una o aplicar conjuntament després de seleccionar-les. Per defecte, la revisió real no modificarà silenciosament la UP base actual: generarà una proposta per a la versió següent, llevat que el docent decideixi aplicar-la immediatament.

## 18. Atenció a la diversitat

La incorporació de mesures serà voluntària. A cada activitat hi haurà una acció per definir com s'atendrà la diversitat.

El flux serà:

1. mostrar les necessitats presents al grup;
2. oferir les mesures associades de la biblioteca d'AvaluaPro;
3. mostrar els alumnes relacionats amb cada mesura;
4. permetre seleccionar les mesures i els alumnes;
5. mostrar una previsualització del text que s'incorporarà a la programació;
6. recordar la mesura a Mode aula quan arribi aquella activitat.

Les mesures provenen de la biblioteca. Els diagnòstics complets i les notes personals no es copiaran a la programació ni es mostraran a direcció.

Exemple de recordatori a Mode aula:

> Activitat 4: donar la pauta fragmentada als alumnes seleccionats.

## 19. Materials i preparació

Els materials podran marcar-se com a:

- material de consulta;
- material que ha de portar l'alumnat;
- material que ha de preparar el docent;
- material que cal imprimir;
- material que cal comprar;
- espai o reserva necessària.

Els materials de preparació generaran una llista de comprovació. El docent podrà marcar cada element com a preparat.

L'avís apareixerà el dia anterior per defecte. Cada material podrà tenir una data d'avís diferent configurada manualment.

Els pendents continuaran visibles a Avui; els elements completats quedaran registrats sense molestar.

## 20. Accés de direcció

Cada docent decidirà quina programació comparteix i introduirà el correu de la persona que hi pot accedir.

La persona convidada:

- haurà d'iniciar sessió amb el compte autoritzat;
- podrà visualitzar i interactuar amb la vista: navegar, filtrar, desplegar, consultar i exportar;
- no podrà modificar la programació;
- podrà veure esborranys; no cal un procés formal de publicació;
- podrà veure la UP i la seva aplicació real als grups;
- no podrà llegir notes personals ni incidències individuals;
- no podrà obtenir diagnòstics complets a través de Programació.

Disposarà de dues formes de consulta:

- una vista interactiva de lectura per navegar, filtrar i consultar l'aplicació real;
- una **Vista de document** amb l'estructura formal de la plantilla per visualitzar o imprimir.

No s'utilitzaran enllaços públics. L'autorització s'aplicarà també a les regles de Firestore, no només a la interfície.

## 21. Seguretat i regles de Firebase

Caldrà ampliar i reorganitzar les regles de Firebase abans d'incorporar les dades noves.

Les regles hauran de distingir, com a mínim:

- propietari i editors autoritzats;
- convidats de només lectura per programació concreta;
- programació i aplicació real visibles per direcció;
- notes privades només per al docent autoritzat;
- incidències i diagnòstics sota els permisos actuals d'AvaluaPro;
- absències, tasques i comportaments associats a l'alumnat correcte;
- denegació de lectures globals o per simple coincidència de domini de correu.

Cada regla nova tindrà proves d'accés permès i d'accés denegat.

## 22. Sincronització i rendiment

La incorporació dels mòduls no es farà afegint totes les dades a la càrrega global actual d'AvaluaPro.

Condicions acordades:

- dades desades primer localment i cua persistent fins a confirmació de Firebase;
- càrrega per mòdul, UT, UP, grup i interval de dates;
- cap document gegant amb tota la programació;
- històrics carregats sota demanda;
- còpies de seguretat per mòdul i curs quan sigui convenient;
- estat de sincronització honest;
- prova real autenticada de desament i recàrrega abans del pilot;
- prova inicial amb una sola UP i un sol grup.

## 23. Disseny visual

La nova experiència mantindrà cohesió amb AvaluaPro:

- tipografia i llenguatge visual compartits;
- fons clars i targetes blanques;
- navegació visible;
- informació densa però ordenada;
- colors amb significat i suport textual;
- botons prou grans per a iPad;
- accions importants no dependents de passar el cursor;
- alternativa a l'arrossegament quan sigui necessari;
- Mode aula optimitzat per ordinador i iPad;
- mòbil amb operativa reduïda i ràpida.

Les fases de preparació, resolució i tancament tindran colors suaus i fixos, coherents amb la paleta d'AvaluaPro. El color del grup continuarà sent la referència principal per identificar la classe.

## 24. Migració i protecció del llegat

- L'Agenda Docent i el Programador Docent antics es conservaran intactes durant la transició.
- Abans de migrar es faran exportacions verificables.
- La migració tindrà previsualització, recompte, informe d'errors i possibilitat de reversió.
- Es conservaran l'origen i la versió dels elements migrats.
- Es validarà primer una UP completa.
- No s'eliminarà ni substituirà informació antiga silenciosament.

## 25. Límits ja decidits

- L'aplicació no enviarà correus.
- No hi haurà enllaços públics per consultar programacions.
- Direcció no podrà modificar les programacions compartides.
- Direcció no veurà notes privades ni incidències individuals des d'aquest mòdul.
- Les absències justificades no es convertiran en tasques no fetes.
- Una classe no oberta a Mode aula no es marcarà automàticament com a realitzada.
- Els canvis de grup no alteraran la UP base sense decisió del docent.
- Les dades històriques no es carregaran totes en iniciar l'aplicació.

## 26. Decisions encara obertes

Aquestes qüestions s'han de resoldre abans de redactar el pla d'acció definitiu:

1. Detall visual final de cada pantalla i comportament en diferents resolucions.
2. Model tècnic definitiu de col·leccions, permisos, càrrega selectiva i còpies.
3. Pla de migració concret de les dades antigues.
4. Ordre de desenvolupament, pilots, proves i desplegament.
5. Com es configuraran i reutilitzaran horaris entre cursos acadèmics.
6. Quins indicadors i resums comparatius tindrà Agenda per detectar desviacions entre grups i UP.
