# Comment installer Odoo 12 sur Debian 9 ?


## Prés-requis
- Debian 9
- PostgreSQL server
- Python (version 3.5)
- Serveur web Apache 2
- Accès SSH (Root) à la machine
- Nano


### 1. Connecter vous à votre VPS

Connectez-vous à votre VPS grace à un logiciel de connexion SSH (Tel que **Putty sur Windows** ou **OpenSSH sur Mac**).<br>
Une fois connecter, nous allons mettre à jour votre VPS grâce à ces deux commandes:<br>
```
apt-get update
apt-get upgrade
``` 
(Cela peut durer plus ou moins quelques minutes).

### 2. Installation de PostegreSQL Server
Odoo a besoin d'une base de données pour fonctionner, pour cela nous allons installer **PostegreSQL Server**:<br>
```
apt-get install postgresql -y
```
Ensuite nous allons activer **PostegreSQL** :
```
systemctl enable postgresql
```

### 3. Installer Odoo 12

Nous allons télécharger **Odoo** directement sur le **VPS**, grace à ces deux commandes:
```
wget -O - https://nightly.odoo.com/odoo.key | apt-key add -
echo "deb http://nightly.odoo.com/12.0/nightly/deb/ ./" >> /etc/apt/sources.list.d/odoo.list
```

Ensuite nous allons mettre à jour les deux paquets téléchargés (ceci peut prendre quelques minutes):
```
apt-get update
```
Après ceci, nous allons installer **Odoo 12** grace à cette commande:
```
apt-get install odoo
```
Ensuite nous allons vérifier si **Odoo 12** est bien installé:
```
systemctl status odoo
```
Et normalement, votre vps doit vous donner : (Plus ou moins)
```
● odoo.service - Odoo Open Source ERP and CRM
Loaded: loaded (/lib/systemd/system/odoo.service; enabled; vendor preset: enabled)
Active: active (running) since Wed 2019-01-01 10:00:00 CDT; 1s ago
Main PID: 10951 (odoo)
CGroup: /system.slice/odoo.service
└─10951 /usr/bin/python3 /usr/bin/odoo --config /etc/odoo/odoo.conf --logfile /var/log/odoo/odoo-server.log
```
**Odoo 12** est bien installé sur votre machine, maintenant nous allons modifiez le mot de passe administration :<br> (Si la commande n'est pas reconnue, faites : ```apt-get install nano```)
```
nano /etc/odoo/odoo.conf
```
Maintenant modifiez la ligne ```admin_passwd = StrongPassword```, par votre mot de passe.
Après ceci, relancez **Odoo 12** :
```
systemctl restart odoo
```

### 4. Connecter vous à Odoo
**Odoo 12** est maintenant disponible sur le port **8069**. (Exemple: 62.42.197.229:**8069**).

