# Infraestructura prevista

Aquest document registra els serveis creats per al projecte. No implica que l'aplicació, les regles ni el desplegament ja estiguin configurats. La decisió funcional posterior és que Planificació, Agenda i Mode aula acabin formant part d'AvaluaPro; el projecte `planificador-docent` servirà inicialment per definir i provar els mòduls sense posar en risc les dades reals.

## GitHub

- Repositori: `MarcPCasals/planificador-docent`
- URL: <https://github.com/MarcPCasals/planificador-docent>
- Branca prevista: `main`

## Firebase

- Project ID: `planificador-docent`
- Auth domain: `planificador-docent.firebaseapp.com`
- Storage bucket: `planificador-docent.firebasestorage.app`
- Messaging sender ID: `293346837907`
- App ID: `1:293346837907:web:6f2a282a9e5fd0c09f5466`
- Measurement ID: `G-R56K0MTDFY`

### Authentication

- Proveïdor inicial: Google.
- Política d'accés acordada: qualsevol compte de Google.
- No es limitarà l'accés al domini `educand.ad`.
- Cada usuari només podrà accedir al seu propi espai de dades mitjançant les regles de Firestore.

Dominis que cal autoritzar per al Planificador:

- `planificador-docent.firebaseapp.com`
- `planificador-docent.web.app`
- `localhost` durant el desenvolupament
- `127.0.0.1` durant el desenvolupament

AvaluaPro no s'ha d'afegir ara als dominis autoritzats del Planificador. Aquest Firebase es manté com a entorn separat de desenvolupament i proves mentre es defineix la incorporació final a AvaluaPro.

Configuració web facilitada:

```js
import { initializeApp } from 'firebase/app'
import { getAnalytics } from 'firebase/analytics'

const firebaseConfig = {
  apiKey: 'AIzaSyDWikHcy7M15hqwxbxTcZvfMtFiq2y8S5I',
  authDomain: 'planificador-docent.firebaseapp.com',
  projectId: 'planificador-docent',
  storageBucket: 'planificador-docent.firebasestorage.app',
  messagingSenderId: '293346837907',
  appId: '1:293346837907:web:6f2a282a9e5fd0c09f5466',
  measurementId: 'G-R56K0MTDFY',
}

const app = initializeApp(firebaseConfig)
const analytics = getAnalytics(app)
```

## Encara pendent de decidir i configurar

- Estructura tècnica definitiva dels mòduls dins d'AvaluaPro.
- Activació i verificació del proveïdor Google a Firebase Authentication.
- Firestore i model de col·leccions.
- Regles de seguretat pròpies.
- Índexs de Firestore.
- Hosting i domini de producció.
- Entorn local i variables de configuració.
- Estratègia de pilot, migració i incorporació a AvaluaPro.

No s'ha de reutilitzar el projecte Firebase antic `eines-docents`. El projecte `avaluapro` només rebrà les dades definitives després del pilot, amb càrrega selectiva, regles provades i una migració explícita.
