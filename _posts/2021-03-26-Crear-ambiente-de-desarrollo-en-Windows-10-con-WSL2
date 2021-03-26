# Crear ambiente de desarrollo en Windows 10 con WSL2 (Ubuntu estandar)
Crear-ambiente-de-desarrollo-en-Windows-10-con-WSL2 (Ubuntu estandar)
## Instalar Visual Studio Code
1. Ingresar a https://code.visualstudio.com/download
2. Descargar versión para Windows
3. Instalar

## Instalar Docker Desktop con WSL2
### Instalar y configuarar Docker Desktop
1. Ingresar en https://www.docker.com/products/docker-desktop
2. Descargar Docker Desktop
3. Ir a carpede Descarga
4. Hacer click depecho en archivo "Docker Desktop Installer.exe"
5. Seleccionar "Ejecutar como administrador"
6. Click en "Sí" para permitir que Docker haga cambios
7. Abrir Windows PowerShell como administrador
8. Para cambiar la versión de WSL a 2 ejecutar
```shell=
wsl.exe --set-default-version 2
```
9. En caso de error visitar documentación de [Microsoft](https://docs.microsoft.com/es-es/windows/wsl/install-win10#step-4---download-the-linux-kernel-update-package)
10. Cerrar Windows PowerShell
11. Abrir [Microsoft Store](https://aka.ms/wslstore)
12. Buscar Ubuntu
13. Instalar Ubuntu, sin versión
14. Abrir Docker Desktop
15. Abrir configuración de Docker en engranaje en barra superior
16. Ir a apartado "Resources", luego a "WSL INTEGRATION"
17. Habilitar opción "Enable integration with my default WSL distro"
18. Habilitar "Ubuntu"
19. Click en botón "Apply & Restart"
20. Listo

### Integrar Docker Desktop con Visual Studio Code
1. Instalar [Remote - WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
2. Reiniciar Visual Studio Code

### Disponibilizar Puertos de WSL en LAN
- [WSL en LAN](https://hackmd.io/LpTirNriTuaBzxxnWRApJg)

## Instalar Windows Terminal
### Instalar terminal
1. Abrir [Microsoft Store](https://aka.ms/wslstore)
2. Buscar Windows Terminal
3. Instalar Windows Terminal
4. Abrir Windows Terminal
5. Abrir Settings de Windows Terminal
6. Cambiar valor de "defaultProfile" por el valor de "guid" del perfil de terminal que desee

### Instalar Oh My Zsh para WSL
1. Actualizar terminal
```shell=
sudo apt update
```
2. Instalar Oh My Zsh
```shell=
sudo apt install git zsh -y
```
3. Habilitar Oh My Zsh en terminal
```shell=
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
4. Editar directorio de inicio
```shell=
nano ~/.zshrc
```
5. Ir al final del archivo y agregar ruta de inicio
```shell=
# directorio de inicio
cd ~/repos
```
