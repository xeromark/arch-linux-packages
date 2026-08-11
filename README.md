# arch-linux-packages

Una lista de paquetes que uso para mi sistema Arch Linux, pensada para respaldar y desplegar rápidamente mi entorno.

---

## Exportar paquetes

Para generar o actualizar la lista con todos los paquetes instalados explícitamente en el sistema:

```bash
pacman -Qqe > pkglist.txt
```

> **Tip:** Si prefieres separar los paquetes de repositorios oficiales de los del AUR:
> - **Oficiales:** `pacman -Qqen > pkglist-native.txt`
> - **AUR:** `pacman -Qqem > pkglist-aur.txt`

---

## Instalar paquetes

Para restaurar el entorno en un sistema limpio o sincronizar la lista:

```bash
paru -S --needed - < pkglist.txt
```

*(El flag `--needed` evita reinstalar paquetes que ya se encuentren presentes en el sistema).*

---

## Mantenimiento

**Limpiar paquetes huérfanos (dependencias que ya no se usan):**

```bash
sudo pacman -Rns $(pacman -Qtdq)
```
