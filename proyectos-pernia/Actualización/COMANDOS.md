```powershell
Set-Location "$HOME\Documents\Dashboard_Pernia\proyectos-pernia"
python .\generar_dashboard.py
if ($LASTEXITCODE -ne 0) { throw "Falló la generación." }

Set-Location ..
git diff --cached --quiet
if ($LASTEXITCODE -ne 0) { throw "Hay cambios preparados. Revísalos antes de continuar." }
git add .\index.html .\proyectos-pernia\proyectos.js .\proyectos-pernia\documentos
if ($LASTEXITCODE -ne 0) { throw "Falló git add." }
git diff --cached --check
if ($LASTEXITCODE -ne 0) { throw "Hay errores en los cambios preparados." }
git diff --cached --stat
git diff --cached --name-status
$confirmar = Read-Host "¿Confirmas publicar estos archivos? Escribe S para continuar"
if ($confirmar -ne "S") { throw "Publicación cancelada." }

git commit -m "Actualizar dashboard Proyectos Pernia"
if ($LASTEXITCODE -ne 0) { throw "Falló el commit." }
git push origin main
if ($LASTEXITCODE -ne 0) { throw "Falló el envío a GitHub." }
```
