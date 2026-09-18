# Infraestructura prevista

Aquest document registra els serveis creats per al projecte. No implica que l'aplicació, les regles ni el desplegament ja estiguin configurats.

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

- Estructura definitiva de l'aplicació.
- Firebase Authentication i proveïdor Google.
- Firestore i model de col·leccions.
- Regles de seguretat pròpies.
- Índexs de Firestore.
- Hosting i domini de producció.
- Entorn local i variables de configuració.
- Contracte d'integració amb AvaluaPro.

No s'ha de reutilitzar el projecte Firebase `eines-docents` ni el projecte `avaluapro` per a les dades del Planificador.

