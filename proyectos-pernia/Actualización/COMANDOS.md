**Generar tablero desde el Excel fuente**

```powershell
Set-Location "$HOME\Documents\Dashboard_Pernia"
python .\proyectos-pernia\generar_dashboard.py
```

**Publicar los cambios en GitHub**

```powershell
Set-Location "$HOME\Documents\Dashboard_Pernia"
git add .\proyectos-pernia\index.html .\proyectos-pernia\proyectos.js .\proyectos-pernia\valuaciones.js .\proyectos-pernia\documentos
git commit -m "Actualizar dashboard Proyectos Pernia"
git push origin main
```
