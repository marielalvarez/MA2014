# MA2014
Copia de https://github.com/danotero/MA2014 para subir soluciones del equipo 3.

# Guía rápida

> **Flujo recomendado:** cada persona trabaja en **su rama**, y **siempre** antes de subir cambios: **actualiza `main` y trae esos cambios a tu rama**. Luego haces *push* a tu rama y abres un **Pull Request (PR)** en GitHub.

---

## Prerrequisitos

- Tener instalado [Git](https://git-scm.com/downloads).
- Tener acceso al repo en GitHub.
- (Opcional) Configurar tu identidad en git (solo la primera vez):

```bash
git config --global user.name "Tu Nombre"
git config --global user.email "tu_correo@ejemplo.com"
```

---

## 1) Clonar el repositorio

> Haz esto solo una vez, para obtener una copia local.

```bash
git clone https://github.com/marielalvarez/MA2014
cd MA2014
```

Verifica los *remotes*:

```bash
git remote -v   # Debe mostrar 'origin' 
```

---

## 2) Cambia tu rama personal 

```bash
# asegúrate de estar en main y actualizado
git checkout main
git pull origin main

#  cambia a tu rama
git checkout mi_rama   
```

---

## 3) Trabajar y guardar cambios

Añade y confirma tus cambios **en tu rama**:

```bash
git status
git add .                  
git commit -m "Mensaje del cambio"
```

---

## 4) **SIEMPRE** antes de subir: actualizar con `main` **sin perder tus cambios**

Hay dos caminos seguros. Usa **uno**:

### Método A — *Commit/Rebase* (limpia el historial)

1) Asegúrate de tener tus cambios **confirmados** (commits). Si no, confirma o guarda con *stash* (ver Método B).  
2) Actualiza `main` y rebasea tu rama:

```bash
# desde tu rama de trabajo 
git fetch origin

# actualiza main local
git checkout main
git pull origin main

# vuelve a tu rama y rebasea contra el main actualizado
git checkout mi_rama
git rebase main
```

Si aparece un conflicto:
```bash
# edita los archivos en conflicto, luego:
git add <archivo_resuelto>
git rebase --continue

# para abortar el rebase si te complicas:
git rebase --abort
```

### Método B — *Stash/Merge* (más simple)

Si tienes cambios **sin confirmar**, guárdalos temporalmente (*stash*), actualiza y vuelve a aplicar:

```bash
# guarda cambios sin commit (si los hay)
git stash push -m "trabajo temporal"

# actualiza main
git fetch origin
git checkout main
git pull origin main

# regresa a tu rama
git checkout humberto

# trae los cambios de main a tu rama (merge)
git merge main

# recupera lo que guardaste en stash (si hiciste stash)
git stash pop
```

> Si `stash pop` genera conflictos, resuélvelos, `git add <archivos>`, y finaliza el merge con `git commit` si es necesario.

---

## 5) Subir tus cambios a **tu rama**

```bash
# estando en tu rama 
git push origin mi-rama
```

---

## 🔀  Abrir un Pull Request (PR)

1) En GitHub, ve a la página del repo 
2) Haz clic en **Compare & pull request** (o **New pull request**)  
3) Verifica: **base = main** ← **compare = tu_rama**.  
4) Escribe un título y descripción claros.  
5) Envía el PR y aceptalo

---

## 7) Actualizar tu rama después de que `main` cambie

Cada vez que `main` reciba cambios (por PRs de otros), sincroniza:

```bash
git fetch origin
git checkout main
git pull origin main
git checkout mi-rama
# trae main a tu rama (elige UNA: rebase o merge)
git rebase main      # historial más lineal
# o
git merge main       # historial con merges
```

Resuelve conflictos si aparecen, luego:

```bash
git push             # o 'git push --force-with-lease' si rebase cambió el historial
```

> **Importante con rebase:** usa `git push --force-with-lease` (no `--force`) para evitar sobrescribir trabajo ajeno accidentalmente.

---

## Comandos rápidos (cheat sheet)

```bash


# Ciclo de trabajo
git status
git add .
git commit -m "mensaje"

# Traer main sin perder cambios (opción rebase)
git fetch origin
git checkout main && git pull origin main
git checkout mi-rama
git rebase main

# Traer main sin perder cambios (opción stash/merge)
git stash push -m "tmp"   # si tienes cambios sin confirmar
git fetch origin
git checkout main && git pull origin main
git checkout mi-rama
git merge main
git stash pop             # si hiciste stash

# Subir y PR
git push
# Luego abrir PR en GitHub: base=main, compare=<mi-rama>
```

---

