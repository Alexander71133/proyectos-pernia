# Actualizar Proyectos Pernia

El dashboard no se actualiza automáticamente cuando cambia el Excel. Ejecuta estos comandos después de sincronizar en Dropbox el libro y los documentos del proyecto.

```powershell
# Regenerar el dashboard y copiar los adjuntos desde Dropbox
Set-Location "$HOME\Documents\Dashboard_Pernia\proyectos-pernia"
python .\generar_dashboard.py
python .\src\generar_html.py

# Publicar el índice y proyectos-pernia desde la raíz del repositorio
Set-Location ..
git status
git add .\index.html .\proyectos-pernia
git diff --cached --stat
git commit -m "Actualizar dashboard Proyectos Pernia"
git push origin main
```

La carpeta `Dashboard_Pernia` es la raíz del repositorio Git y GitHub Pages busca `index.html` en esa raíz. `src\generar_html.py` crea allí el índice y deja sus recursos dentro de `proyectos-pernia`. Revisa la salida de `git status` y `git diff --cached --stat` antes de confirmar. Si `git commit` indica que no hay cambios, no hay nada nuevo que publicar.

El dashboard y los archivos de `documentos/` serán públicos si GitHub Pages está habilitado para el repositorio. No publiques archivos privados.
