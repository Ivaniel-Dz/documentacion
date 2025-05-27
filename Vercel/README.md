# Vercel
---

## ✅ OBJETIVO:

**Desplegar la rama `demo`, solo la carpeta `frontend`, usando Vercel CLI** (y que funcione al 100%).

---

## 🛠️ PASOS CLAROS

### 1. 📦 Verifica que tienes todo listo

* Tu proyecto tiene esta estructura:

  ```
  /proyecto
    /frontend   ✅ (aquí está tu app Angular o Ionic)
    /backend    ❌ (NO se desplegará)
  ```

* Tu rama `demo` **existe y está actualizada en GitHub o en local**.

* Tienes instalado Node.js y Vercel CLI:

  ```bash
  npm install -g vercel
  ```

---

### 2. 🛑 IMPORTANTE: Posiciónate en la rama `demo`

Desde la terminal:

```bash
git checkout demo
```

🔄 Asegúrate de que todos los archivos estén actualizados y que sea **la versión que quieres desplegar**.

---

### 3. 📂 Entra en la carpeta `frontend`

```bash
cd ruta/al/proyecto/frontend
```

Aquí debe estar tu `angular.json`, `ionic.config.json`, `package.json`, etc.

---

### 4. 🚀 Ejecuta el comando de despliegue

```bash
vercel --prod
```

Este comando:

* Detectará tu framework (Angular/Ionic)
* Te hará preguntas clave (y te digo qué responder abajo)
* Creará el proyecto en Vercel y lo desplegará correctamente

---

## 📋 RESPUESTAS CLAVE DURANTE EL DEPLOY

* **"Which scope should contain your project?"**
  👉 Selecciona tu cuenta personal (tu correo o nombre de usuario)

* **"Link to existing project?"**
  ❌ No

* **"What's your project's name?"**
  👉 Usa algo como `mi-app-demo`

* **"In which directory is your code located?"**
  👉 Presiona ENTER (ya estás dentro de `frontend`)

* **"Which framework?"**
  👉 Elige `Angular` (o `Other` si estás usando Ionic sin Angular puro)

* **"What is your build command?"**
  👉 Normalmente:

  ```bash
  npm run build
  ```

* **"What is your output directory?"**
  👉 Angular/Ionic normalmente genera en `dist/<nombre>`
  Por ejemplo:

  ```
  dist/frontend
  ```

  (puedes verificarlo en `angular.json > projects > frontend > architect > build > options > outputPath`)

---

### ✅ ¿Resultado?

Al finalizar, Vercel te dará una URL como:

```
https://mi-app-demo.vercel.app
```

Que corresponde a la rama `demo` y solo al contenido de la carpeta `frontend`.

---

### 🧠 ¿Y para los próximos despliegues?

Solo vuelves a entrar a `frontend/` y haces:

```bash
vercel --prod
```

✅ Sin repetir las preguntas, ya estará configurado.

---

¿Quieres que revise tu `angular.json` para decirte la ruta de salida exacta (`outputPath`) por si tienes dudas?
