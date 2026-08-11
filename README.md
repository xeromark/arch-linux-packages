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

## ⚙️ Preparativos en una instalación limpia

En un sistema Arch Linux recién instalado, el helper de AUR (`paru`) no viene incluido. Es necesario compilarlo primero para poder instalar el resto de la lista.

1. Instalar las dependencias de compilación:
   ```bash
   sudo pacman -S --needed base-devel git
   ```
2. Clonar y compilar `paru`:
   ```bash
   git clone https://aur.archlinux.org/paru.git
   cd paru
   makepkg -si
   cd ..
   ```
   *(Nota: Para futuras compilaciones de paquetes pesados o herramientas de desarrollo que den problemas en los tests, recuerda que puedes usar herramientas adicionales o flags como `--nocheck` según lo requieras).*

---

## Instalar paquetes

Una vez que `paru` está configurado, puedes restaurar todo tu entorno de una sola vez:

```bash
paru -S --needed - < pkglist.txt
```

*(El flag `--needed` evita reinstalar paquetes que ya se encuentren presentes en el sistema).*

---

## 💾 Respaldar configuraciones (Dotfiles)

**Importante:** La lista de paquetes solo instala los programas base. Para conservar tu entorno exacto, debes respaldar tus configuraciones. Esto incluye tus atajos personalizados de Dolphin, las preferencias de KDE Plasma, los scripts con `kwriteconfig6` para el foco de ventanas dinámico, la distribución física de tu teclado (ISO Español) y los entornos de tus modelos de IA o motores gráficos.

Directorios clave a respaldar de forma manual o usando herramientas como Git/Stow:
* `~/.config/` (Contiene la mayoría de las configuraciones del entorno de escritorio y aplicaciones).
* `~/.local/share/` (Contiene datos locales de usuario).
* `~/.bashrc` o `~/.zshrc` (Tus alias y variables de entorno).

---

## Mantenimiento

**Limpiar paquetes huérfanos (dependencias que ya no se usan):**

```bash
sudo pacman -Rns $(pacman -Qtdq)
```
