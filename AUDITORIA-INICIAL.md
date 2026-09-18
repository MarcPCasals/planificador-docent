# Auditoria funcional inicial — Planificador Docent

Data de revisió: 18 de setembre de 2026

## 0. Abast i estat dels projectes

S'han revisat en mode només lectura:

- `/Users/marc/GitHub/MarcBook/Altres/agenda-docent.html`
- `/Users/marc/GitHub/MarcBook/Altres/programador.html`
- els fitxers indicats d'AvaluaPro a `/Users/marc/Documents/projectes/avaluapro`

No s'ha modificat cap aplicació antiga, cap dada real, cap projecte Firebase, cap regla de seguretat ni cap desplegament.

La carpeta nova s'ha creat a:

`/Users/marc/Documents/projectes/planificador-docent`

En el moment de la revisió és una carpeta nova sense repositori Git. No s'ha inicialitzat el repositori perquè la primera fase demana auditar i acordar l'arquitectura abans de construir.

Els dos fitxers antics revisats no tenen canvis locals. El repositori MarcBook és a `main`, sincronitzat amb `origin/main`, amb una carpeta no relacionada `c2/` sense seguiment. AvaluaPro és a `main`, sincronitzat amb `origin/main`, i té captures no relacionades dins `tmp/`; s'han preservat.

### Límit de l'evidència visual

La inspecció visual amb el navegador integrat ha quedat bloquejada per la política de seguretat del navegador tant per a la còpia local com per a GitHub Pages. Per tant, aquest document és una auditoria funcional exhaustiva basada en el codi actual i no una auditoria visual validada amb captures. Abans de dissenyar pantalles noves convé fer una segona passada visual autenticada.

## 1. Inventari fidel d'Agenda Docent

### 1.1 Accés, càrrega i persistència

- Inici i tancament de sessió amb Google.
- Projecte Firebase antic compartit: `eines-docents`.
- Càrrega de la configuració principal des de `agenda_docent/{uid}`.
- Càrrega de cada setmana des de `agenda_docent_weeks/{uid}/weeks/{weekId}`.
- Guardat de la configuració, radar, setmanes no lectives i recordatoris.
- Guardat de cada setmana com a document separat.
- Còpies internes al núvol i metadada de l'última còpia automàtica.
- Exportació manual de totes les dades a JSON.
- Importació manual d'un JSON complet, amb neteja de configuració i horari.
- Historial intern de còpies i descàrrega d'una versió concreta.
- Reinicialització completa des de la interfície.

### 1.2 Configuració inicial

- Nom del docent.
- Any d'inici del curs escolar.
- Tema visual de l'aplicació.
- Creació i eliminació de grups/classes.
- Color identificatiu de cada grup, editable també després de crear-lo.
- Dates de finalització de les UT, ordenades cronològicament.
- Horari setmanal de dilluns a divendres.
- Assignació d'un grup a cada franja.
- Sessions d'1 h, 1 h 30 min o 2 h, amb detecció de solapaments.
- Variant horària específica per a VIP/Música, amb el pati avançat.
- Neteja automàtica de referències d'horari que ja no són vàlides.

### 1.3 Tauler anual i mensual

- Navegació mensual pel calendari de setmanes del curs.
- Accés a cada setmana.
- Indicació de setmana actual o següent segons el dia.
- Marcatge de setmanes de vacances/no lectives.
- Indicació de les UT que acaben en una setmana.
- Càlcul del progrés temporal del curs.
- Accés a una vista cronològica per classe.
- Resum de tasques d'avui, demà i cap de setmana.
- Radar global de pendents amb data.
- Possibilitat de completar, consultar l'historial i eliminar entrades del radar.
- Recordatoris globals amb data i hora.
- Enllaços configurables a programacions externes.
- Enllaç al seguiment de tasques.
- Accés a configuració, importació, exportació, còpies i reinicialització.

### 1.4 Planificació setmanal

- Navegació a la setmana anterior o següent, saltant setmanes no lectives.
- Vista de dilluns a divendres i opció de mostrar dissabte i diumenge.
- Horari ordinari combinat amb classes extraordinàries de la setmana.
- Marcatge d'un dia concret com a no lectiu i registre del motiu.
- Afegir i eliminar classes extraordinàries.
- Activitats per sessió amb text, minuts i ordre editable.
- Reordenació d'activitats arrossegant.
- Enganxat intel·ligent d'una llista d'activitats.
- Càlcul del temps total de la sessió.
- Marcatge d'una activitat com a feta, no feta o inacabada.
- Trasllat automàtic d'una activitat no feta/inacabada a la propera sessió del grup.
- Marcatge de sessió com a `NO ES FA CLASSE`, amb motiu.
- Trasllat de totes les activitats d'una classe cancel·lada a la propera sessió.
- Camp de revisió posterior de la sessió.
- Notes de preparació per activitat.
- Observacions de resultat per activitat.
- Notes generals de la sessió.
- Materials en text lliure.
- Enllaços amb títol, URL, còpia al portapapers i reordenació.
- Bloc de notes d'una sessió i bloc de notes del dia complet.
- Recordatoris vinculats a una data.
- Copiar tot el contingut d'una sessió a la següent del mateix grup, a la següent d'un altre grup o a un espai manual.
- En copiar, conserva tasques, temps, notes, materials, enllaços i observacions; reinicia l'estat de les activitats copiades.
- Desfer i refer canvis dins la vista.
- Netejar el contingut d'una sessió.
- Exportar una taula al portapapers.
- Intent d'exportació cap al Programador Docent.

### 1.5 Vista cronològica d'una classe

- Recorregut de totes les sessions d'un grup al llarg de les setmanes.
- Filtre per UT segons les dates de finalització configurades.
- Numeració consecutiva de sessions lectives.
- Inclusió visual dels dies no lectius i classes cancel·lades.
- Edició de les mateixes activitats, temps, estats, notes, materials i observacions que a la vista setmanal.
- Materials fixos de la classe.
- Copiar sessions entre dates o grups.
- Enganxat intel·ligent.
- Desfer i refer canvis que afecten diverses setmanes.
- Exportació d'un rang concret de sessions.
- Intent d'enviament del rang al Programador Docent.

### 1.6 Importació des del Programador

- Rep una unitat i un conjunt de sessions.
- Detecta classes candidates pel nom.
- Permet seleccionar una o diverses classes de destinació.
- Permet seleccionar una UT de destinació i una data d'inici.
- Calcula prèviament quants espais lliures hi ha per classe.
- Evita per defecte festius, classes cancel·lades i sessions amb contingut.
- Mostra quantes sessions s'inseriran i quantes quedaran sense espai.
- Pot sobreescriure sessions existents només després d'una confirmació explícita amb la llista afectada.
- Converteix activitats del Programador en activitats de l'Agenda.
- Converteix el detall d'activitat en nota de preparació.
- Converteix el comentari de l'activitat en observació posterior.
- Separa materials sense URL i enllaços amb URL.
- Limita cada sessió importada a un màxim de 10 activitats.

## 2. Inventari fidel de Programador Docent

### 2.1 Accés, persistència i recuperació

- Inici i tancament de sessió amb Google.
- Projecte Firebase antic compartit: `eines-docents`.
- Un document principal a `programador_docent/{uid}`.
- Guardat automàtic al núvol amb retard de 2 segons.
- Bloqueig d'un guardat buit o anterior a la càrrega completa.
- Prevenció bàsica d'escriptures simultànies.
- Còpia JSON local descarregable.
- Còpia manual al núvol.
- Intent de còpia automàtica diària.
- Historial de còpies al núvol, amb màxim aproximat de 20.
- Firma simple d'integritat de la còpia.
- Descàrrega i restauració d'una còpia concreta.
- Còpia preventiva abans d'una restauració.
- Avís de recuperació quan l'espai carregat és buit i hi ha còpies disponibles.
- Importació manual d'un JSON complet.
- Migració interna de formats antics de sessions i materials.
- Desfer i refer durant la sessió d'edició.

### 2.2 Estructura de programació

- Diversos cursos, reordenables arrossegant.
- Nom del curs editable en línia.
- Diverses UT per curs.
- Nom de la UT editable en línia.
- Tres fases inicials: preparació, resolució i integració.
- Creació, canvi de nom, plegat i eliminació de fases.
- Creació i eliminació de sessions.
- Reordenació de sessions, també entre fases.
- Marcatge d'una sessió com a completada o pendent.
- Progrés de la UT calculat per sessions completades.
- Reinicialització només dels estats de la UT.
- Reinicialització completa de la UT.
- Plegar o desplegar tots els detalls.

### 2.3 Contingut de les sessions

- Activitats amb:
  - títol/text;
  - temps estimat;
  - detall ric amb negreta i cursiva;
  - resposta al repte;
  - observació/comentari propi;
  - estat de detall plegat o desplegat.
- Reordenació d'activitats dins d'una sessió.
- Moviment d'activitats entre sessions.
- Suma automàtica del temps total de la sessió.
- Materials amb:
  - nom;
  - enllaç principal/alumnat;
  - enllaç de versió docent.
- Enganxar URL des del portapapers.
- Observació general de sessió quan no hi ha activitats.
- Observacions separades per activitat quan sí que n'hi ha.

### 2.4 Materials, imports i exports

- Materials transversals/fixos de la UT.
- Importació massiva enganxant una taula d'Excel o Numbers.
- Graella de quatre columnes: sessió, activitat, material i comentaris.
- Elecció de la fase de destinació abans d'importar.
- Exportació d'un curs i una UT a XLSX.
- L'XLSX conté número de sessió, fase, activitats, materials, comentaris i estat.
- Enviament de tota la UT o d'un rang de sessions a l'Agenda.
- URL de l'Agenda configurable i recordada al navegador.

## 3. Matriu de decisió

| Capacitat | Conservar | Unificar | Millorar | Duplicat / eliminar | Falta |
|---|---|---|---|---|---|
| Cursos, grups i assignatures | Sí | Un únic catàleg | Separar clarament curs, grup i assignatura | Eliminar noms lliures duplicats entre apps | Identificadors estables |
| UT i fases | Sí | Programació i Agenda han de llegir la mateixa UT | Dates, ordre i progrés per grup | Eliminar còpia de noms per text | Plantilles i vinculació entre grups |
| Sessions | Sí, prioritat màxima | Una sola sessió canònica | Separar pla de sessió i ocurrència real | Eliminar import/export intern de sessions | Estat real complet i historial |
| Activitats i temps | Sí | Mateixes activitats a Programació, Agenda i Avui | Temps previst i real; continuacions | Eliminar conversió JSON↔text↔HTML | Identificadors i ordre persistents |
| Materials i enllaços | Sí | Un sol model | Públic alumne/docent, tipus i permisos | Unificar `materials`, `links`, `teacherUrl` | Biblioteca reutilitzable |
| Observacions | Sí | Preparació i resultat visibles al lloc correcte | Diferenciar previsió, incidència i reflexió | Evitar `comments`, `notes`, `review` amb significat solapat | Historial de canvis |
| Horari | Sí | L'Agenda consumeix l'horari del mateix projecte | Excepcions, canvis i durades flexibles | Eliminar dues variants rígides incrustades al codi | Vigència per períodes |
| Calendari i festius | Sí | Una font temporal única | Festius, setmanes especials, excepcions | Eliminar derivacions duplicades | Importació/calendari institucional opcional |
| Classes extraordinàries | Sí | Com a esdeveniment de calendari | Motiu, durada i grup | — | Reprogramació explícita |
| No feta / inacabada | Sí | Convertir en resultat real estructurat | Activitats completades i pendents, continuació traçable | Eliminar marques visuals com a font de veritat | `feta parcialment`, `ajornada`, `cancel·lada`, `substituïda` |
| Copiar sessions | Sí | Una ordre de duplicació comuna | Vista prèvia i destí clar | Eliminar tres implementacions semblants | Vincle opcional amb la sessió origen |
| Vista per classe | Sí | Forma part de Programació/Agenda | Comparació previst-real i retard acumulat | — | Indicadors de desviació per grup |
| Vista Avui | — | Nou espai principal | Operativa, ràpida i contextual | — | És una peça nova prioritària |
| Recordatoris/radar | Sí | Un únic sistema | Context, data/hora, sessió/grup, estat | Unificar radar i recordatoris | Prioritat i recurrència opcional |
| Desfer/refer | Sí | Un mecanisme transversal | Historial limitat i segur | Eliminar històries independents per pantalla | Registre d'operacions |
| Còpies de seguretat | Sí | Una política única | Restauració amb vista prèvia | Eliminar mecanismes diferents i promeses excessives | Versió d'esquema i validació formal |
| Importació Excel | Sí | Un importador | Previsualització i mapatge de columnes | — | Informe d'errors per fila |
| Enviament entre apps antigues | Només per migrar | Substituir per dades internes directes | — | Eliminar `window.open`, `postMessage`, HTML i `localStorage` com a sincronització | Importador de transició |
| Integració AvaluaPro | No copiar dades sensibles | Enllaç contextual i resum mínim | Consentiment i revocació | No donar accés general a Firestore | Contracte, vinculacions i endpoint limitat |

## 4. Recorregut actual de les dades

### 4.1 Dins del Programador

1. Firebase carrega `{ courses }` d'un únic document.
2. `migrateData` adapta formats antics.
3. React manté tota l'estructura en memòria.
4. Cada canvi actualitza l'historial de desfer/refer, prepara una còpia JSON i programa un guardat al núvol.
5. Curs → UT → fase → sessió → activitats/materials és una jerarquia incrustada.

### 4.2 Programador → Agenda

1. El docent tria tota la UT o un rang numèric.
2. El Programador aplana totes les fases en una sola numeració consecutiva.
3. Construeix un missatge `IMPORT_SESSIONS` amb curs, UT i sessions.
4. Desa el missatge a `localStorage` amb la clau `agenda_pending_import`.
5. Obre l'Agenda en una pestanya nova.
6. Tres segons després intenta enviar el mateix missatge amb `postMessage`.
7. L'Agenda llegeix `localStorage` quan Firebase acaba de carregar o rep el missatge.
8. L'Agenda elimina immediatament el pendent de `localStorage` i obre el modal de previsualització.
9. El docent tria classes, UT i data inicial.
10. Les sessions s'insereixen cronològicament als primers espais compatibles.

Dades que arriben: activitats, temps, detall, comentari d'activitat, materials i URL principal.

Dades que es perden o no s'apliquen bé: fase original, resposta al repte, URL docent del material, comentari general de sessió, estat completat i activitats més enllà de les deu primeres.

### 4.3 Agenda → Programador

1. L'Agenda converteix sessions a files HTML.
2. Crea un missatge `SYNC_TABLE` amb curs, UT, fase i HTML.
3. Només el desa a `window.pendingSyncPayload` de la pestanya de l'Agenda.
4. Obre el Programador en una pestanya nova.
5. El Programador actual envia `PROGRAMACIO_READY` a la finestra origen, però l'Agenda no té cap receptor per respondre.
6. El Programador actual tampoc té cap receptor de `SYNC_TABLE`; només escolta `IMPORT_SESSIONS`.

Conclusió: en la versió actual revisada, el flux Agenda → Programador no només és fràgil; està funcionalment desconnectat.

## 5. Per què fallen les importacions i exportacions

### Errors estructurals confirmats

1. **Protocols incompatibles.** Agenda envia `SYNC_TABLE`; Programador escolta `IMPORT_SESSIONS`.
2. **La dada queda a la finestra equivocada.** `window.pendingSyncPayload` viu a l'Agenda i la nova pestanya no la llegeix.
3. **Handshake incomplet.** Programador anuncia `PROGRAMACIO_READY`, però Agenda no escolta ni respon.
4. **Dependència del mateix origen.** `localStorage` només es comparteix si les dues pàgines tenen exactament el mateix origen. Deixarà de servir quan el Planificador tingui domini/desplegament propi.
5. **Cursa temporal.** Un retard fix de tres segons no garanteix que Firebase i React ja estiguin preparats.
6. **Sense confirmació de recepció.** L'emissor no sap si el receptor ha validat, importat o guardat les dades.
7. **El pendent s'esborra massa aviat.** Agenda elimina `agenda_pending_import` abans que el docent confirmi i abans del guardat final.
8. **Sense idempotència.** El mateix missatge pot arribar per `localStorage` i `postMessage`; hi ha protecció parcial de modal, però no un identificador d'operació persistent.
9. **Identificació per text.** Curs i UT es busquen pel nom. Accents, espais, lletres de grup o canvis de nom poden crear destinacions equivocades.
10. **Aplanament de fases.** Enviar un rang global elimina la fase d'origen de cada sessió.
11. **Conversió amb pèrdua.** HTML i text lliure no poden conservar tots els camps estructurats.
12. **Contracte no versionat.** No hi ha `schemaVersion`, compatibilitat declarada ni migració del missatge.
13. **Risc de seguretat.** Programador envia a `*`; Agenda accepta `IMPORT_SESSIONS` sense comprovar l'origen. El contingut HTML també seria un canal inadequat per a dades no confiables.
14. **Guardat global i tardà.** Les aplicacions depenen de l'estat complet en memòria i de guardats asíncrons; tancar una pestanya o encadenar canvis pot deixar dubtes sobre què s'ha confirmat al núvol.

## 6. Model unificat proposat

La decisió principal és aquesta: **Programació, Agenda i Avui no han de tenir còpies de la sessió. Han de ser tres vistes de les mateixes entitats.**

### 6.1 Entitats

#### Curs acadèmic (`academicYear`)

- `id`
- `label` (ex. `2026-2027`)
- `startsOn`, `endsOn`
- `timezone`
- `status`

#### Nivell/curs (`courseLevel`)

- `id`
- `name` (ex. `2n ESO`)
- `order`

No s'ha de confondre amb el grup concret.

#### Grup (`group`)

- `id`
- `academicYearId`
- `courseLevelId`
- `name` (ex. `2n B`)
- `color`
- `externalLinks.avaluaproClassId` només després d'una vinculació explícita

#### Assignatura (`subject`)

- `id`
- `name`
- `color` opcional

#### Docència (`teachingAssignment`)

Uneix docent, grup, assignatura i curs acadèmic.

- `id`
- `academicYearId`
- `groupId`
- `subjectId`
- `teacherUid`
- `active`

#### UT (`unit`)

- `id`
- `teachingAssignmentId` o plantilla compartida
- `code`, `title`
- `order`
- `plannedStartsOn`, `plannedEndsOn`
- `status`
- `externalLinks.avaluaproUtId` opcional

#### Fase (`phase`)

- `id`
- `unitId`
- `name`
- `order`
- `color` opcional

#### Sessió planificada (`sessionPlan`)

- `id`
- `unitId`
- `phaseId`
- `title`
- `order`
- `plannedDurationMinutes`
- `preparationNotes`
- `version`
- `sourceSessionId` opcional si és una còpia

#### Activitat (`activity`)

- `id`
- `sessionPlanId`
- `order`
- `title`
- `details`
- `challengeResponse`
- `plannedMinutes`
- `teacherNotes`

#### Material (`material`)

- `id`
- `scope`: `unit`, `session` o `activity`
- `scopeId`
- `title`
- `type`
- `studentUrl`
- `teacherUrl`
- `notes`

#### Regla d'horari (`timetableRule`)

- `id`
- `teachingAssignmentId`
- `weekday`
- `startsAt`, `endsAt`
- `validFrom`, `validUntil`

Permet canviar l'horari a mig curs sense reescriure el passat.

#### Esdeveniment de calendari (`calendarEvent`)

- `id`
- `teachingAssignmentId`
- `startsAt`, `endsAt`
- `kind`: `class`, `extraClass`, `holiday`, `specialWeek`, `other`
- `sessionPlanId` opcional
- `sourceTimetableRuleId` opcional
- `status`: `scheduled`, `moved`, `cancelled`

És la connexió entre Programació i Agenda: calendaritzar una sessió significa assignar el seu `sessionPlanId` a un esdeveniment.

#### Resultat real (`sessionOutcome`)

- `id`
- `calendarEventId`
- `sessionPlanId`
- `groupId`
- `status`: `planned`, `done`, `partial`, `postponed`, `cancelled`, `replaced`
- `completedActivityIds`
- `pendingActivityIds`
- `actualMinutes` opcional
- `reflection`
- `replacementDescription` opcional
- `continuedInSessionPlanId` opcional
- `recordedAt`, `recordedBy`

El resultat pertany a l'ocurrència i al grup. Això evita marcar com a “feta” per a 2n B una sessió que només s'ha impartit a 2n A.

#### Recordatori (`reminder`)

- `id`
- `dueAt`
- `text`
- `status`
- `contextType`, `contextId`
- `priority`

#### Vinculació externa (`integrationLink`)

- `id`
- `provider`: `avaluapro`
- `localType`, `localId`
- `externalType`, `externalId`
- `linkedBy`, `linkedAt`
- `status`

### 6.2 Regles del model

- Els noms són presentació; les relacions sempre usen identificadors.
- Una sessió no es mou copiant text: es modifica el seu esdeveniment o se'n crea una continuació vinculada.
- Les activitats pendents conserven l'origen i poden passar a una continuació sense perdre el resultat de la sessió anterior.
- El progrés previst es calcula amb `sessionPlan`; el progrés real, amb `calendarEvent` + `sessionOutcome`.
- Els materials conserven explícitament versió d'alumnat i versió docent.
- Qualsevol importació ha de tenir `schemaVersion`, identificador d'operació i informe de validació.

## 7. Navegació proposada

### Avui — pantalla inicial

- Capçalera amb data, estat de sincronització i recordatoris.
- Targeta per cada classe del dia: hora, grup, UT, sessió, activitats i minuts.
- Materials i enllaços directes.
- Accions ràpides: començar, obrir AvaluaPro, marcar resultat, afegir nota.
- Avisos mínims d'AvaluaPro, sense noms ni motius sensibles en la vista general.
- Al final de la classe: `Feta`, `Parcial`, `Ajornada`, `Cancel·lada` o `Substituïda`.

### Agenda

- Vistes dia, setmana i calendari.
- Horari recurrent i excepcions reals.
- Arrossegar una sessió planificada a una data.
- Moure o copiar amb una previsualització de l'efecte.
- Festius, setmanes especials i classes extraordinàries.
- Diferència visible entre sessió prevista, impartida i pendent.

### Programació

- Selector de grup/assignatura i UT.
- Fases i sessions ordenades.
- Activitats, temps, materials, enllaços i notes.
- Columna o indicador de calendari per saber quan està prevista cada sessió.
- Comparació per grup: previst, realitzat, pendent i desviació acumulada.

### Navegació secundària

- Recursos/materials.
- Recordatoris.
- Integracions, inclosa la vinculació amb AvaluaPro.
- Configuració, còpies i importació.

En iPad i ordinador, les tres entrades principals han de ser sempre visibles. En mòbil es pot prioritzar Avui i deixar edicions complexes per a una pantalla més gran.

## 8. Contracte inicial amb AvaluaPro

### 8.1 Fase 1: només obertura contextual

El Planificador desa vinculacions explícites entre:

- grup local ↔ `classId` d'AvaluaPro;
- UT local ↔ `utId` d'AvaluaPro.

En obrir AvaluaPro, el contracte de navegació proposat és:

`https://.../avaluapro/?class=<id>&ut=<id>&mode=<evaluation|tracking|students|tutoring>&action=<optional>`

AvaluaPro encara no interpreta aquests paràmetres; actualment només llegeix paràmetres de formularis públics. Caldrà implementar i validar aquest receptor en una fase posterior.

Condicions:

- acceptar només modes coneguts;
- validar que el grup i la UT pertanyen a l'usuari autenticat;
- ignorar identificadors no autoritzats;
- no incloure noms d'alumnes ni dades sensibles a l'URL;
- si falta la vinculació, obrir un diàleg de vinculació, no endevinar pel nom.

### 8.2 Fase 2: resum mínim abans de classe

Resposta permesa per grup:

```json
{
  "schemaVersion": 1,
  "classId": "...",
  "generatedAt": "...",
  "counts": {
    "studentsRequiringFollowUp": 3,
    "pendingTutoringReminders": 1,
    "incidentsToReview": 1
  },
  "links": {
    "tracking": "...",
    "tutoring": "..."
  }
}
```

No ha d'incloure noms, diagnòstics, notes personals, dades familiars, informació mèdica, motius tutorials ni text d'incidències.

### 8.3 Seguretat de la vinculació

- No confiar que el mateix compte Google tingui el mateix UID als dos projectes Firebase.
- Vinculació iniciada pel docent i confirmada als dos costats.
- Token d'un sol ús, curt i signat per completar la vinculació.
- Desar només identificadors i estat de consentiment.
- Accés a resums mitjançant una funció/API limitada d'AvaluaPro, no mitjançant lectura general del seu Firestore.
- Token curt per petició, audiència i origen validats, límit de freqüència i registre d'accés.
- Revocació visible des de totes dues aplicacions.
- Firestore del Planificador sense cap còpia de les col·leccions d'alumnes d'AvaluaPro.

### 8.4 Accions selectives futures

Cada acció ha de ser explícita i separada:

- crear una tasca de seguiment;
- obrir assistència;
- obrir una graella d'avaluació;
- vincular una activitat d'avaluació;
- obrir el registre del grup.

Les escriptures futures han d'usar un contracte versionat amb previsualització, confirmació, identificador idempotent i resposta d'èxit/error. No s'ha de crear una sincronització massiva bidireccional.

## 9. Pla de migració

1. **Congelar el contracte antic.** No canviar formats ni esborrar dades mentre s'inventaria.
2. **Exportar còpies verificables.** Obtenir un JSON d'Agenda, un JSON de Programador i un inventari de Firestore per usuari.
3. **Detectar versions.** Classificar sessions antigues amb `activity/material` de text i sessions modernes amb arrays.
4. **Construir el mapa.** Relacionar curs, grup, assignatura, UT i fase amb identificadors nous.
5. **Previsualitzar.** Mostrar recomptes abans d'importar: cursos, grups, UT, fases, sessions, activitats, materials, enllaços, recordatoris i setmanes.
6. **Informar incompatibilitats.** Noms duplicats, UT sense data, classes no trobades, URL invàlides, sessions sense fase i camps truncats.
7. **Importar a un espai nou.** Cap importació substitueix silenciosament dades existents.
8. **Conservar origen.** Cada entitat migrada guarda `legacySource`, `legacyId` i la versió del format.
9. **Validar.** Comparar recomptes, mostres de contingut, ordre, temps totals i enllaços; produir un informe descarregable.
10. **Permetre desfer.** Importació agrupada per `migrationRunId`, eliminable sense afectar dades creades després.
11. **Pilotar amb una UT.** Validar una UT completa a Programació, Agenda i Avui abans de migrar-ho tot.
12. **Mantenir el llegat.** Agenda i Programador antics continuen disponibles en només lectura durant la transició.

## 10. Pla d'implementació per fases

### Fase 0 — Decisions i prototip funcional

- Validar aquest model amb casos reals.
- Dibuixar els fluxos Avui, Agenda i Programació.
- Decidir què és una plantilla compartida i què és específic de cada grup.
- Definir estats i transicions del resultat real.

### Fase 1 — Fonaments

- Repositori propi.
- Vite + React amb estructura modular.
- Projecte Firebase propi.
- Autenticació, model de dades i regles per propietari.
- Sincronització amb estat honest i cua local segura.
- Còpies versionades.

### Fase 2 — Programació

- Cursos, grups, assignatures i UT.
- Fases, sessions, activitats i materials.
- Ordenació, còpia i importació amb previsualització.

### Fase 3 — Agenda

- Horari recurrent.
- Calendari, festius i excepcions.
- Assignació directa de `sessionPlan` a `calendarEvent`.
- Vistes setmana i grup.

### Fase 4 — Avui i resultat real

- Pantalla operativa del dia.
- Estats complets de sessió.
- Activitats completades i pendents.
- Continuacions i reajust del progrés.
- Comparació previst/real per grup i UT.

### Fase 5 — Migració

- Importadors d'Agenda i Programador.
- Execució en sec, informe i reversió.
- Pilot amb una UT i després migració completa.

### Fase 6 — AvaluaPro: navegació contextual

- Vinculacions de grup i UT.
- Receptor de deep links a AvaluaPro.
- Accés directe a seguiment, avaluació, alumnat o tutoria.

### Fase 7 — AvaluaPro: resums mínims i accions selectives

- API limitada de comptadors.
- Consentiment, revocació i auditoria.
- Accions puntuals i idempotents.

## 11. Prioritats i decisions pendents

Les decisions que convé prendre abans de començar a programar són:

1. Si una UT és pròpia de cada grup o pot néixer d'una plantilla compartida entre grups.
2. Si una edició de la sessió planificada després d'impartir-la modifica el passat o crea una versió nova. Es recomana versionar.
3. Com es crea una continuació: sessió nova automàtica o proposta que el docent confirma.
4. Quins camps formen part del resultat real mínim obligatori.
5. Quin nivell de funcionament sense connexió és imprescindible.
6. Quant temps es mantindran accessibles les aplicacions antigues després de la migració.

## 12. Riscos d'ús i accessibilitat detectables al codi antic

- Moltes accions destructives depenen de diàlegs natius i missatges genèrics.
- Hi ha controls implementats com a `div` clicables, poc fiables amb teclat i lector de pantalla.
- Diverses accions només apareixen en passar el cursor, cosa problemàtica en iPad.
- La reordenació per arrossegament no té una alternativa clara de teclat.
- Alguns botons són molt petits o només mostren una icona.
- L'estat es comunica sovint amb color, ratllat o subratllat.
- Camps editables en línia no sempre tenen una etiqueta accessible visible.
- Les taules molt amples depenen del desplaçament horitzontal.

Aquests punts són riscos derivats de la implementació. Cal validar-los visualment i amb teclat en una sessió posterior abans de convertir-los en conclusions d'accessibilitat definitives.
