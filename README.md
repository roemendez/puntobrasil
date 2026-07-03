# Punto Brassil · Sistema de Gestión

Mini sistema web de inventario, ventas, clientes y abonos para joyería.  
Tecnologías: HTML + CSS + JavaScript puro · Firebase Firestore · SheetJS

---

## Estructura de archivos

```
punto-brassil/
├── index.html              ← La aplicación completa
├── firebase.json           ← Configuración Firebase Hosting
├── .firebaserc             ← ID del proyecto Firebase (editar)
├── firestore.rules         ← Reglas de seguridad Firestore
├── firestore.indexes.json  ← Índices de Firestore
├── .gitignore
└── README.md
```

---

## PASO 1 — Crear el proyecto en Firebase

1. Entra a [console.firebase.google.com](https://console.firebase.google.com)
2. Haz clic en **"Agregar proyecto"**
3. Escribe el nombre del proyecto: `punto-brassil` (o el que prefieras)
4. Desactiva Google Analytics si no lo necesitas → **Crear proyecto**
5. Espera que se cree (unos segundos)

---

## PASO 2 — Activar Firestore

1. En el menú izquierdo: **Compilación → Firestore Database**
2. Clic en **"Crear base de datos"**
3. Elige **"Empezar en modo de prueba"** → Siguiente
4. Elige la ubicación más cercana a Chile: **`us-central1`** o **`southamerica-east1`**
5. Clic en **"Listo"**

---

## PASO 3 — Obtener la configuración de Firebase

1. En Firebase Console, clic en el ícono ⚙️ **Configuración del proyecto**
2. Baja hasta **"Tus apps"** → Clic en **`</>`** (Web)
3. Registra la app con el nombre `punto-brassil`
4. Copia el bloque `firebaseConfig` que aparece, se ve así:

```javascript
const firebaseConfig = {
  apiKey: "AIzaSy...",
  authDomain: "punto-brassil.firebaseapp.com",
  projectId: "punto-brassil",
  storageBucket: "punto-brassil.appspot.com",
  messagingSenderId: "123456789",
  appId: "1:123456789:web:abc123"
};
```

5. Abre `index.html` con un editor de texto (VSCode, Notepad++, etc.)
6. Busca el bloque `firebaseConfig` cerca del inicio del `<script>`
7. **Reemplaza** los valores `"PEGA_AQUI_..."` con tus valores reales
8. Guarda el archivo

---

## PASO 4 — Instalar herramientas (solo una vez)

Necesitas tener instalado:
- **Node.js** → [nodejs.org](https://nodejs.org) (descarga la versión LTS)
- **Git** → [git-scm.com](https://git-scm.com)

Luego instala Firebase CLI:
```bash
npm install -g firebase-tools
```

Verifica que funcione:
```bash
firebase --version
```

---

## PASO 5 — Subir a GitHub

### 5a. Crear repositorio en GitHub
1. Entra a [github.com](https://github.com)
2. Clic en **"New repository"**
3. Nombre: `punto-brassil`
4. Visibilidad: **Private** (recomendado, son datos de negocio)
5. NO marques "Add README" (ya tienes uno)
6. Clic en **"Create repository"**

### 5b. Subir los archivos desde terminal

Abre una terminal (PowerShell en Windows, Terminal en Mac/Linux) en la carpeta del proyecto:

```bash
# Inicializar Git
git init

# Agregar todos los archivos
git add .

# Primer commit
git commit -m "Punto Brassil v3 - Sistema completo"

# Conectar con GitHub (reemplaza TU_USUARIO con tu usuario de GitHub)
git remote add origin https://github.com/TU_USUARIO/punto-brassil.git

# Subir
git branch -M main
git push -u origin main
```

GitHub te pedirá tu usuario y contraseña (o token de acceso personal).

---

## PASO 6 — Desplegar en Firebase Hosting

```bash
# Iniciar sesión en Firebase
firebase login

# Conectar el proyecto local con tu proyecto Firebase
# (reemplaza punto-brassil con el ID real de tu proyecto)
firebase use punto-brassil

# Desplegar la app y las reglas de Firestore
firebase deploy
```

Al terminar verás una URL como:
```
✓ Deploy complete!
Hosting URL: https://punto-brassil.web.app
```

Esa es tu URL pública. ¡La app ya está en línea!

---

## PASO 7 — (Opcional) Activar GitHub Pages como alternativa gratuita

Si prefieres usar GitHub Pages en lugar de Firebase Hosting:

1. En tu repositorio de GitHub → **Settings → Pages**
2. Source: **"Deploy from a branch"**
3. Branch: **main** / Folder: **/ (root)**
4. Clic en **Save**
5. Tu app estará disponible en: `https://TU_USUARIO.github.io/punto-brassil`

> Nota: Con GitHub Pages el `index.html` se sirve igual. Firebase Firestore sigue funcionando porque es una API externa.

---

## Actualizar la app después de cambios

Cada vez que modifiques `index.html`:

```bash
# Guardar cambios en Git
git add .
git commit -m "Describe qué cambiaste"
git push

# Redesplegar en Firebase (si usas Firebase Hosting)
firebase deploy --only hosting
```

---

## Estructura de Firestore

Los datos se guardan automáticamente en estas colecciones:

| Colección | Contenido |
|-----------|-----------|
| `/config/parametros` | Parámetros de cálculo (tipo de cambio, márgenes, etc.) |
| `/config/negocio` | Datos del negocio y plantillas de mensajes |
| `/inventario/{sku}` | Piezas de joyería |
| `/clientes/{clienteId}` | Clientes |
| `/ventas/{ventaId}` | Ventas con estado de pago |
| `/abonos/{abonoId}` | Abonos registrados |
| `/movimientos_stock/{id}` | Historial de movimientos de stock |
| `/movimientos_financieros/{id}` | Historial financiero |

---

## Solución de problemas

**La app dice "Modo local" y no guarda en Firebase**  
→ Verifica que pegaste bien el `firebaseConfig` en `index.html`. No deben quedar valores `"PEGA_AQUI_..."`.

**Error de permisos en Firestore**  
→ Verifica que las reglas en `firestore.rules` están desplegadas (`firebase deploy --only firestore:rules`).

**No carga el Excel importado**  
→ El archivo Excel debe tener las hojas con los nombres exactos: `ENCHAPADASORO BRASIL`, `PLATA CHILE`, `ACERO ORO CHINA`.

**Error al hacer `git push`**  
→ Es posible que GitHub requiera un token de acceso personal en vez de contraseña. Créalo en: GitHub → Settings → Developer settings → Personal access tokens → Tokens (classic) → Generate new token (scope: `repo`).

---

## Contacto y soporte

Sistema desarrollado para **Punto Brassil**.  
Para modificaciones o soporte, guarda este README junto con tu archivo `index.html`.
