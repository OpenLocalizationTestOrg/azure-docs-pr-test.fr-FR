---
title: aaaDeploy LEMP sur un ordinateur virtuel de Linux dans Azure | Documents Microsoft
description: Didacticiel - pile LEMP installation hello un VM Linux dans Azure
services: virtual-machines-linux
documentationcenter: virtual-machines
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 08/03/2017
ms.author: danlep
ms.openlocfilehash: d8f9d84c5e9c0df4e9e985c10fe10f63a2f88214
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-a-lemp-web-server-on-an-azure-vm"></a>Installer un serveur web LEMP sur une machine virtuelle Azure
Cet article vous guide tout au long de comment toodeploy un NGINX web server, MySQL et PHP (hello LEMP de pile) sur un VM Ubuntu dans Azure. pile LEMP Hello est un autre toohello populaires [pile LAMP](tutorial-lamp-stack.md), que vous pouvez également installer dans Azure. serveur LEMP toosee hello dans action, vous pouvez éventuellement installer et configurer un site WordPress. Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Créer une VM Ubuntu (hello « L » dans la pile LEMP hello)
> * Ouvrez le port 80 pour le trafic web
> * Installer NGINX, MySQL et PHP
> * Vérifier l’installation et la configuration
> * Installation de WordPress sur le serveur LEMP hello


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Si vous choisissez tooinstall et que vous utilisez hello CLI localement, ce didacticiel nécessite que vous exécutez hello CLI d’Azure version 2.0.4 ou version ultérieure. Exécutez `az --version` version de hello toofind. Si vous avez besoin de tooinstall ou mise à niveau, consultez [installer Azure CLI 2.0]( /cli/azure/install-azure-cli). 

[!INCLUDE [virtual-machines-linux-tutorial-stack-intro.md](../../../includes/virtual-machines-linux-tutorial-stack-intro.md)]

## <a name="install-nginx-mysql-and-php"></a>Installer NGINX, MySQL et PHP

Exécutez hello commande tooupdate Ubuntu package sources suivantes et installer NGINX, MySQL et PHP. 

```bash
sudo apt update && sudo apt install nginx mysql-server php-mysql php php-fpm
```

Vous êtes invité à tooinstall hello packages et autres dépendances. Lorsque vous y êtes invité, définissez un mot de passe racine MySQL, puis sur [Entrée] toocontinue. Suivez hello restant d’invites. Ce processus installe hello minimale requise PHP les extensions nécessitées toouse PHP avec MySQL. 

![Page de mot de passe racine MySQL][1]

## <a name="verify-installation-and-configuration"></a>Vérifier l’installation et la configuration


### <a name="nginx"></a>NGINX

Vérifier la version de hello de NGINX avec hello de commande suivante :
```bash
nginx -v
```

Avec NGINX installés et le port 80 ouvrez tooyour machine virtuelle, de serveur web de hello désormais accessibles à partir de hello internet. tooview hello NGINX page d’accueil, ouvrez un navigateur web et entrez les adresse IP publique hello Hello machine virtuelle. Utilisez l’adresse IP publique de hello, vous avez utilisé tooSSH toohello machine virtuelle :

![Page par défaut de NGINX][3]


### <a name="mysql"></a>MySQL

Vérifiez la version hello de MySQL avec hello commande suivante (Notez majuscules de hello `V` paramètre) :

```bash
msql -V
```

Nous vous recommandons d’exécuter hello après l’installation de hello sécurisé toohelp script de MySQL :

```bash
mysql_secure_installation
```

Entrez votre mot de passe racine MySQL et configurer les paramètres de sécurité hello pour votre environnement.

Si vous souhaitez toocreate une base de données MySQL, ajouter des utilisateurs, ou modifier les paramètres de configuration, tooMySQL de connexion :

```bash
mysql -u root -p
```

Lorsque vous avez terminé, quittez hello mysql invite en tapant `\q`.

### <a name="php"></a>PHP

Vérifier la version de hello de PHP avec hello de commande suivante :

```bash
php -v
```

Configurer hello de toouse NGINX Gestionnaire de processus FastCGI PHP (PHP-pouces). Exécutez hello suivant les commandes tooback serveur NGINX d’origine de hello bloquer le fichier de configuration et puis modifiez le fichier d’origine de hello dans un éditeur de votre choix :

```bash
sudo cp /etc/nginx/sites-available/default /etc/nginx/sites-available/default_backup

sudo sensible-editor /etc/nginx/sites-available/default
```

Dans l’éditeur de hello, remplacez le contenu de hello de `/etc/nginx/sites-available/default` avec les éléments suivants de hello. Consultez les commentaires hello pour une explication des paramètres de hello. Remplacez hello adresse IP publique de votre machine virtuelle pour *yourPublicIPAddress*et laisser hello restant de paramètres. Puis enregistrez le fichier de hello.

```
server {
    listen 80 default_server;
    listen [::]:80 default_server;

    root /var/www/html;
    # Homepage of website is index.php
    index index.php;

    server_name yourPublicIPAddress;

    location / {
        try_files $uri $uri/ =404;
    }

    # Include FastCGI configuration for NGINX
    location ~ \.php$ {
        include snippets/fastcgi-php.conf;
        fastcgi_pass unix:/run/php/php7.0-fpm.sock;
    }
}
```

Vérifier la configuration de NGINX hello pour les erreurs de syntaxe :

```bash
sudo nginx -t
```

Si la syntaxe de hello est correcte, redémarrez NGINX avec hello commande suivante :

```bash
sudo service nginx restart
```

Si vous souhaitez davantage de tootest, créez un tooview de page PHP info rapide dans un navigateur. Hello commande suivante crée la page des informations hello PHP :

```bash
sudo sh -c 'echo "<?php phpinfo(); ?>" > /var/www/html/info.php'
```



Vous pouvez maintenant vérifier page des informations de PHP hello que vous avez créé. Ouvrez un navigateur et allez trop`http://yourPublicIPAddress/info.php`. Remplacez hello adresse IP publique de votre machine virtuelle. Il doit se présenter une image toothis similaire.

![Page d’informations PHP][2]


[!INCLUDE [virtual-machines-linux-tutorial-wordpress.md](../../../includes/virtual-machines-linux-tutorial-wordpress.md)]

## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez déployé un serveur LEMP dans Azure. Vous avez appris à effectuer les actions suivantes :

> [!div class="checklist"]
> * Créer une machine virtuelle Ubuntu
> * Ouvrez le port 80 pour le trafic web
> * Installer NGINX, MySQL et PHP
> * Vérifier l’installation et la configuration
> * Installation de WordPress sur la pile LEMP hello

Avancer toolearn de didacticiel suivant toohello comment toosecure les serveurs web avec les certificats SSL.

> [!div class="nextstepaction"]
> [Sécuriser un serveur web avec SSL](tutorial-secure-web-server.md)

[1]: ./media/tutorial-lemp-stack/configmysqlpassword-small.png
[2]: ./media/tutorial-lemp-stack/phpsuccesspage.png
[3]: ./media/tutorial-lemp-stack/nginx.png
