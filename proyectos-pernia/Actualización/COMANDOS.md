## Ver cambios localmente

```powershell
Set-Location "$HOME\Documents\Dashboard_Pernia\proyectos-pernia"
python .\generar_dashboard.py
if ($LASTEXITCODE -ne 0) { throw "Falló la generación." }

Set-Location ..
Start-Process python -ArgumentList "-m http.server 8000" -WorkingDirectory "$HOME\Documents\Dashboard_Pernia"
Start-Sleep -Seconds 2
Start-Process "http://localhost:8000"
```

## Hacer commit y publicar

```powershell
Set-Location "$HOME\Documents\Dashboard_Pernia"
git add .\index.html .\proyectos-pernia\proyectos.js .\proyectos-pernia\documentos

if (git diff --cached --quiet) {
    Write-Host "No hay cambios para confirmar."
} else {
    git commit -m "Actualizar dashboard Proyectos Pernia"
    if ($LASTEXITCODE -eq 0) { git push origin main }
}
```
