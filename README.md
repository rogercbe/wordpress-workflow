# Wordpress Reactiva Workflow

Guía de desarrollo de wordpress.

### Requisitos

  - VirtualBox
  - Vagrant
  - Git

Una vez se cumplen los requisitos tenemos que preparar nuestro entorno local y montar el servidor que vamos a usar con vagrant.

### Instalación del servidor

Se va a utilizar el proyecto de configuración vagrant para desarrollo wordpress [https://github.com/Varying-Vagrant-Vagrants/VVV](VVV).

Antes de instalar el box de vagrant de vvv, instalaremos 2 plugins de vagrant para agilizar algunos procesos, escribir en /etc/hosts automaticamente y autoprovision de cambios en los archivos de configuración:

```sh
$ vagrant plugin install vagrant-hostsupdater
```

```sh
$ vagrant plugin install vagrant-triggers
```

Ahora ya podemos clonar el box de vagrant de VVV donde queramos, a partir de este directorio es desde donde arracaremos el servidor e instalaremos imágenes de wordpress para desarrollar localmente nuestras páginas web.

En este ejemplo el directorio se llamará local, puedes cambiarlo a tu gusto.

```sh
$ git clone https://github.com/Varying-Vagrant-Vagrants/VVV.git local
```

Ahora ya podemos entrar en el directorio que se nos acaba de generar al clonar el repositorio y arrancar el servidor, para arrancarlo debemos ejecutar el sigiuente comando. Este proceso va a descargar e instalar todas las dependencias, redirigir puertos y arrancar una imágen del servidor, puede tardar unos minutos en terminar.
```sh
$ vagrant up
```

> Es posible que en entornos Windows pueda dar errores de permisos al escribir en el archivo hosts, se puede solucionar ejecutando el terminal como administrador o cambiando los permisos al usuario actual del archivo hosts.

Una vez terminado el proceso podemos entrar dentro de nuestro servidor mediante el comando:

```sh
$ vagrant ssh
```

Por defecto VVV añade diferentes sitios wordpress a nuestro servidor, estos son los siguientes. Podemos añadir tantos sitios como queramos (explicación más adelante).

- http://local.wordpress.dev/
- http://local.wordpress-trunk.dev/
- http://src.wordpress-develop.dev/
- http://build.wordpress-develop.dev/
- http://vvv.dev/

### Usuarios y Contraseñas

Todos los Wordpress generados comparten la misma información de usuarios y contraseñas.

```c++
// Wp Admin
Username: admin
Password: password

// MySQL DB / MySQL User
Username: db
Passwprd: db

// MySQL Root
Username: root
Password: root
```

### Añadir más sitios Wordpress

Para añadir más sitios wordpress, vamos a instalar un plugin más que nos genera una CLI para crear fácilmente instancias de Wordpress dentro de nuestro servidor y nos edita automáticamente los archivos de configuración y los archivos hosts y se provisiona automáticamente.

Dentro de la carpeta donde arrancamos el server vagrant vamos a clonar el siguiente repositorio.

```sh
$ git clone https://github.com/aliso/vvv-site-wizard.git
```

Una vez listo, podemos ejecutar el comando:

```sh
$ ./vvv-site-wizard/vvv
```

Y nos dara opciones para crear, borrar y listar instancias de wordpress en ese servidor (este comando se tiene que usar fuera de la máquina virtual, si se usa cuando se está logeado por ssh puede no funcionar). 

Una vez creamos una instancia nueva de Wordpress (tardará un rato en bootear la máquina y hacer todos los cambios) podremos empezar a desarrollar aisladamente de los demás webs que tengamos en la máquina.

