# VS Code Live Share + Jupyter Notebooks: Guía para Equipos (Nivel Básico)

## ✨ Inicio Rápido Paso a Paso

### 👩‍💼 Anfitriona:

1. **Abre VS Code directamente en la carpeta del proyecto** (`File > Open Folder` o desde terminal).
2. Si no estás trabajando exclusivamente con notebooks, asegúrate de tener instaladas las extensiones "Python" y "Jupyter" desde el panel de extensiones (por lo general ya vienen instaladas si usas VS Code para Python).
3. En la barra lateral izquierda, haz clic en el ícono de **Live Share** (una flecha curva en círculo).
4. Haz clic en **"Start collaboration session (Read/Write)"** para iniciar la sesión.
5. Comparte el link generado con tu equipo. Asegúrate de que sea el enlace de tipo **Read/Write** y que las invitadas acepten los permisos.
6. Abre el notebook `.ipynb` del proyecto.
7. Ejecuta `Live Share: Share Jupyter Server` desde la paleta de comandos (`Ctrl + Shift + P`).
8. Verifica que el **kernel esté seleccionado y funcionando** (parte superior derecha del notebook).
9. **Ejecuta las primeras celdas con los `import` y configuraciones iniciales.**
10. **Guarda frecuentemente el notebook** (`Ctrl + S`) — sólo la anfitriona puede guardar archivos y hacer `git add / commit / push` al repositorio.

### 👧 Invitadas:

1. Abre VS Code.
2. Si es tu primera vez, instala la extensión "Live Share" desde el panel de extensiones.
3. Haz clic en el enlace que te envió tu compañera (la anfitriona).
4. Se abrirá VS Code y te unirás a la sesión. Asegúrate de aceptar los permisos de edición si se solicitan.
5. Desde el panel de Live Share, abre el archivo `.ipynb` que la anfitriona comparte.
6. Puedes **editar código y markdown**, pero **no necesitas seleccionar ningún kernel**.
7. Si ves un aviso de "Detectando kernel...", ignóralo — **sólo la anfitriona ejecuta las celdas**.

### 📌 Nota sobre la Interfaz de Live Share:

* El panel está en la **barra lateral izquierda** (icono de flecha curva con círculo).
* Puedes abrirlo para:

  * Ver quién está conectado
  * Acceder a los archivos compartidos
  * Finalizar la sesión
  * Compartir terminal o kernel (anfitriona)

---

## ✅ Mejores Prácticas

| Tarea                                 | Quién lo Hace      | Notas                                                    |
| ------------------------------------- | ------------------ | -------------------------------------------------------- |
| Estar en carpeta del proyecto         | Anfitriona         | Importante para que se compartan los archivos correctos  |
| Ejecutar celdas de `import` al inicio | Anfitriona         | Prepara el entorno para todas                            |
| Ejecutar celdas                       | Anfitriona         | Las invitadas no pueden ejecutar, solo ver resultados    |
| Compartir kernel de Jupyter           | Anfitriona         | Usar `Live Share: Share Jupyter Server`                  |
| Seleccionar/activar kernel            | Anfitriona         | Verificar que el notebook funcione antes de invitar      |
| Editar código o markdown              | Todas              | La colaboración en tiempo real funciona bien             |
| Detener/interrumpir kernel            | Solo la anfitriona | Usar `Jupyter: Interrupt Kernel` desde la paleta         |
| Seleccionar kernel (invitada)         | No necesario       | No afecta la ejecución; el kernel es el de la anfitriona |
| Guardar el trabajo                    | Solo la anfitriona | Debe guardar y subir los cambios a GitHub                |

---

## ⚡ Problemas Comunes + Soluciones

### ❌ Las invitadas no pueden ejecutar celdas (se quedan cargando)

* **Causa:** Sólo la anfitriona puede ejecutar celdas
* **Solución:** La anfitriona debe ejecutar las celdas y compartir los resultados

### ❌ El kernel está en "Detectando" o no conecta

* **Causa:** Error de VS Code o entorno Python incorrecto
* **Solución:** La anfitriona debe:

  * Seleccionar el entorno correcto (`Python: Select Interpreter`)
  * Instalar `jupyter`, `ipykernel` en ese entorno
  * Ejecutar `python -m ipykernel install --user`
  * Reiniciar VS Code y volver a intentar

### ❌ No se puede detener una celda en ejecución

* **Causa:** Invitada intenta interrumpir
* **Solución:** Solo la anfitriona puede detener/interrumpir el kernel

  * Usar el botón de la barra o `Jupyter: Interrupt Kernel`

### ❌ Las invitadas no ven resultados

* **Causa:** Kernel no compartido
* **Solución:** La anfitriona debe ejecutar `Live Share: Share Jupyter Server`

---

## 💡 Consejos para una Sesión Exitosa

* La anfitriona debe probar el notebook **sola primero** para verificar que el kernel funciona
* Siempre **compartir el servidor Jupyter** antes de que las invitadas intenten ejecutar o ver algo
* Usar llamada de voz o chat (Zoom, Discord) para coordinar tareas
* Guardar y hacer commit en Git después de la sesión para evitar pérdidas
* Evitar salidas muy pesadas (gráficas grandes, muchas impresiones) con varias invitadas conectadas

---

## 📜 Extras

Para más estabilidad, considera usar archivos `.py` en lugar de `.ipynb` cuando hay problemas con el kernel.

También puedes ejecutar notebooks localmente y compartir versiones estáticas en PDF o Markdown si la ejecución en tiempo real no es esencial.
