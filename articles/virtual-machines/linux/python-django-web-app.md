---
title: "application web d’aaaPython avec Django sur une machine virtuelle Linux de Azure | Documents Microsoft"
description: "Découvrez comment toohost un Django web application dans Azure à l’aide d’un VM Linux."
services: virtual-machines-linux
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-resource-manager
ms.assetid: 00ad4c2c-4316-4f9a-913f-f7f49b158db7
ms.service: virtual-machines-linux
ms.workload: web
ms.tgt_pltfrm: vm-linux
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 520c47e19e8ffb4bb866f70772d506ddf76e242c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-linux-vm"></a>Application web Django Hello World sur une machine virtuelle Linux
> [!div class="op_single_selector"]
> * [Windows](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [Mac/Linux](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

Ce didacticiel vous montre comment toohost un site Web de base Django dans Linux dans des Machines virtuelles Azure. Dans le didacticiel de hello, nous ne Supposons aucune expérience préalable de Azure. Lorsque vous avez terminé le didacticiel de hello, vous pouvez avoir une application basée sur les Django et en cours d’exécution dans le cloud de hello.

Découvrez comment :

* Configurer une machine virtuelle Azure de toohost Django. Bien que ce didacticiel explique comment toodo pour **Linux**, vous pouvez effectuer même hello pour un ordinateur Windows Server hébergé dans Azure. 
* Créez une application Django dans Linux.

didacticiel de Hello vous montre comment toobuild une base Hello World web application. application Hello est hébergée dans une machine virtuelle Azure.

Hello suivant capture d’écran montre application hello terminée :

![Une fenêtre de navigateur affiche la page de Hello World hello dans Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Créer et configurer une machine virtuelle Azure de toohost Django

1. toocreate une machine virtuelle Azure avec hello distribution d’Ubuntu Server 14.04 LTS, consultez [créer une machine virtuelle Linux Bonjour Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Vous pouvez également choisir un authentification par de mot de passe au lieu d’utiliser une clé publique SSH.
2. tooedit hello réseau sécurité groupe tooallow entrant HTTP trafic tooport 80, consultez [créer des groupes de sécurité réseau Bonjour Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).
3. (Facultatif) Par défaut, votre nouvelle machine virtuelle n’a pas de nom de domaine complet (FQDN).  toocreate une machine virtuelle avec un nom de domaine complet, consultez [création d’un nom de domaine complet dans hello portail Azure pour une machine virtuelle Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Cette étape n’est pas requise pour l’achèvement de ce didacticiel.

## <a id="setup"></a>Configuration d’environnement de développement hello
> [!NOTE]
> Si vous avez besoin de tooinstall Python ou que vous souhaitez que les bibliothèques clientes toouse hello, consultez hello [guide d’installation de Python](../../python-how-to-install.md).

Hello Ubuntu Linux VM a Python 2.7 préinstallés, mais il n’est fourni avec Apache ou Django. Hello suivant les étapes tooconnect tooyour machine virtuelle et d’installer Apache et Django :

1. Ouvrez une nouvelle fenêtre de terminal.
2. tooconnect toohello machine virtuelle Azure, entrez hello commande suivante. Si vous n’avez pas créé un nom de domaine complet, vous pouvez vous connecter à l’aide de hello adresse IP publique qui est affiché dans la machine virtuelle de hello résumé Bonjour portail Azure.
   
       $ ssh yourusername@yourVmUrl
3. tooinstall Django, entrez hello suivant de commandes :
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. tooinstall Apache avec mod-wsgi sous, entrez hello de commande suivante :
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a>Créer une application Django
1. toouse tooaccess SSH votre machine virtuelle, la fenêtre de Terminal ouverte hello que vous avez utilisé dans hello précédant la section.
2. toocreate un nouveau projet Django, entrez hello suivant de commandes :
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   Hello `django-admin.py` script génère une structure de base pour les sites Web basés sur Django :
   
   * `helloworld/manage.py` vous aide à démarrer et arrêter l’hébergement de votre site web basé sur Django.
   * `helloworld/helloworld/settings.py` contient les paramètres Django de votre application.
   * `helloworld/helloworld/urls.py`contient du code de mappage de hello entre chaque URL et sa vue.
3. Dans le répertoire de /var/www/helloworld/helloworld hello, créez un nouveau fichier nommé views.py. Ce fichier contient la vue hello qui restitue la page « hello world » de hello. Dans votre éditeur de code, entrez hello suivant de commandes :
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Remplacez contenu hello du fichier de urls.py hello hello suivant de commandes :
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a>Configurer Apache
1. Dans le dossier de /etc/apache2/sites-available/helloworld.conf hello, créez un fichier de configuration d’hôte virtuel Apache. Définissez toohello de contenu hello valeurs suivantes. Remplacez *Nomov* par nom d’ordinateur hello vous utilisez hello (par exemple, *pyubuntu*).
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. site hello tooactivate, hello utilisez commande suivante :
   
       $ sudo a2ensite helloworld
3. toorestart Apache, utilisez hello de commande suivante :
   
       $ sudo service apache2 reload
4. Charger la page Web de hello dans votre navigateur :
   
   ![Une fenêtre de navigateur affiche la page de hello hello world dans Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a>Arrêter votre machine virtuelle Azure
Lorsque vous avez terminé ce didacticiel, nous vous recommandons d’arrêter ou de supprimer hello Azure VM, vous avez créé pour le didacticiel de hello. Cela a pour effet de libérer des ressources pour d’autres didacticiels et d’éviter de vous exposer à des frais pour l’utilisation d’Azure.

