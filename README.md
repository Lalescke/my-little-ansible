# L'incroyable My Little Ansible de Aleksandar et Raphaël | ETNA


## FR


Il est souvent long de configurer des serveurs tout neufs, et il faut parfois répéter de nombreuses mêmes commandes sur toutes les machines en même temps à la suite d'une nouvelle installation ou d'une grosse mise à jour.

Ce projet est une implémentation d'un outil Infrastructure as Code (IaC) inspiré d'Ansible et développé en Python. Il permet de configurer et gérer des serveurs linux de manière déclarative à l'aide de scripts Python, et le tout en SSH !

<br>

## Installation du programme

Le programme est packagé. Pour l'installer, il suffit de récupérer le code, et d'éxecuter les commandes suivantes depuis la racine du dossier :

```
pip install requirements.txt
python setup.py install
```

<br>

## Comment lancer le le programme ?

Pour lancer le programme, toujours à la source du dossier, lancer la commande suivante :

```
mla -f todos.yml -i inventory.yml
```

Il est également possible de lancer le programme en mode debug afin d'activer les stack traces avec la commande :

```
mla -f todos.yml -i inventory.yml --debug
```


<br>

## Comment utiliser le programme ?

Comme nous avons pu le voir, la commande de lancement prends en argument deux élements : un **todos.yml** et un **inventory.yml**.

Ces deux éléments se présentent de la façon suivante :

<br>

## Connexion SSH ?

Il Faut avoir une connexion SSH de préparée avec la VM et un user avec les droits suffisants. Remplir le inventory.yml à la racine du projet avec l'IP, le port, le username et le password.  

<br>

### Le todos.yaml 

C'est la liste des modifications à effectuer. Le programme, à son lancement, va parser la liste des 'to do', et exectuer les 'modules' qui lui sont attribués. 

Voici la liste des modules disponibles :

- **copy** pour copier des fichiers ou dossiers
- **template** pour templater des fichiers
- **service** pour administrer les services systemd
- **sysctl** qui permet de modifier les paramètres kernel
- **apt** pour administrer l'installation et la désinstallation des paquets APT
- **command** pour exécuter des commandes arbitraires sur les hosts

Voici la synthaxe des 6 modules dans le même ordre :

```
# COPY - NO BACKUP
- module: copy
  params:
    src: "source_a_copier"
    dest: "destination_de_la_copie"

# COPY - WITH BACKUP
- module: copy
  params:
    src: "source_a_copier"
    dest: "destination_de_la_copie"
    backup: true           # Active le backup, désactivé si vide ou false

# TEMPLATE
- module: template
  params:
    src: "fichier_a_templater"
    dest: "contenu_a_copier"
    vars:
      listen_port: "mon_port"
      server_name: "mon_serveur"

# SERVICE
- module: service
  params:
    name: "nom_du_service"
    state: started/restarted/stopped/enabled/disabled

- module: service
  params:
    name: docker
    state: restarted

# SYSCTL
- module: sysctl
  params:
    attribute: "attribut_a_modifier"
    value: "nouvelle_valeur"
    permanent: true/false   #True = modif permanente / False = non permanent

# APT
- module: apt
  params:
    name: "nom_du_package"
    state: present/absent   #present = install / absent = uninstall

# COMMAND
- module: command
  params:
    command: "ma_commande_shell"
```

<br>

### Le inventory.yaml 

Il s'agit de la liste des serveurs sur lesquels les actions seront effectuées.

La synthaxe se présente comme ceci :

```
hosts:
    server1:
        ssh_address: "ip_du_serveur"
        ssh_port: "port_du_serveur"
        ssh_user: "utilisateur"
        ssh_password: "mot_de_passe"
        ssh_key_file: "clé_ssh"
    server2:
        ssh_address: "ip_du_serveur"
        ssh_port: "port_du_serveur"
    server3:
         ...
```

## ENG

It often takes a long time to configure brand new servers, and you sometimes have to repeat many of the same commands on all machines at the same time following a new installation or a major update.

This project is an implementation of an Infrastructure as Code (IaC) tool inspired by Ansible and developed in Python. It allows you to configure and manage Linux servers declaratively using Python scripts, and all in SSH!

<br>

## Installing the program

The program is packaged. To install it, simply retrieve the code, and execute the following commands from the root of the folder:

```
pip install requirements.txt
python setup.py install
```

<br>

## How to launch the program?

To launch the program, still at the source of the folder, run the following command:

```
mla -f todos.yml -i inventory.yml
```

It is also possible to launch the program in debug mode in order to activate stack traces with the command:

```
mla -f todos.yml -i inventory.yml --debug
```


<br>

## How to use the program?

As we have seen, the launch command takes two elements as arguments: a **todos.yml** and an **inventory.yml**.

These two elements appear as follows:

<br>

## SSH connection?

You must have an SSH connection prepared with the VM and a user with sufficient rights. Populate the inventory.yml at the root of the project with the IP, port, username and password.

<br>

### The todos.yaml

This is the list of modifications to be made. The program, when launched, will parse the 'to do' list, and execute the 'modules' assigned to it.

Here is the list of available modules:

- **copy** to copy files or folders
- **template** to template files
- **service** to administer systemd services
- **sysctl** which allows you to modify kernel parameters
- **apt** to manage the installation and uninstallation of APT packages
- **command** to execute arbitrary commands on hosts

Here is the syntax of the 6 modules in the same order:

```
# COPY - NO BACKUP
- module: copy
  params:
    src: "source_a_copier"
    dest: "destination_de_la_copie"

# COPY - WITH BACKUP
- module: copy
  params:
    src: "source_a_copier"
    dest: "destination_de_la_copie"
    backup: true           # Active le backup, désactivé si vide ou false

# TEMPLATE
- module: template
  params:
    src: "fichier_a_templater"
    dest: "contenu_a_copier"
    vars:
      listen_port: "mon_port"
      server_name: "mon_serveur"

# SERVICE
- module: service
  params:
    name: "nom_du_service"
    state: started/restarted/stopped/enabled/disabled

- module: service
  params:
    name: docker
    state: restarted

# SYSCTL
- module: sysctl
  params:
    attribute: "attribut_a_modifier"
    value: "nouvelle_valeur"
    permanent: true/false   #True = modif permanente / False = non permanent

# APT
- module: apt
  params:
    name: "nom_du_package"
    state: present/absent   #present = install / absent = uninstall

# COMMAND
- module: command
  params:
    command: "ma_commande_shell"
```

### The inventory.yaml

This is the list of servers on which the actions will be performed.

The syntax looks like this:

```
hosts:
    server1:
        ssh_address: "ip_du_serveur"
        ssh_port: "port_du_serveur"
        ssh_user: "utilisateur"
        ssh_password: "mot_de_passe"
        ssh_key_file: "clé_ssh"
    server2:
        ssh_address: "ip_du_serveur"
        ssh_port: "port_du_serveur"
    server3:
         ...
```