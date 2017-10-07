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
# <a name="django-hello-world-web-app-on-a-linux-vm"></a><span data-ttu-id="7ad95-103">Application web Django Hello World sur une machine virtuelle Linux</span><span class="sxs-lookup"><span data-stu-id="7ad95-103">Django Hello World web app on a Linux VM</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7ad95-104">Windows</span><span class="sxs-lookup"><span data-stu-id="7ad95-104">Windows</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
> * [<span data-ttu-id="7ad95-105">Mac/Linux</span><span class="sxs-lookup"><span data-stu-id="7ad95-105">Mac/Linux</span></span>](../windows/classic/python-django-web-app.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
> 
> 

<br>

<span data-ttu-id="7ad95-106">Ce didacticiel vous montre comment toohost un site Web de base Django dans Linux dans des Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad95-106">This tutorial shows you how toohost a Django-based website in Linux in Azure Virtual Machines.</span></span> <span data-ttu-id="7ad95-107">Dans le didacticiel de hello, nous ne Supposons aucune expérience préalable de Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad95-107">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="7ad95-108">Lorsque vous avez terminé le didacticiel de hello, vous pouvez avoir une application basée sur les Django et en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="7ad95-108">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="7ad95-109">Découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="7ad95-109">Learn how to:</span></span>

* <span data-ttu-id="7ad95-110">Configurer une machine virtuelle Azure de toohost Django.</span><span class="sxs-lookup"><span data-stu-id="7ad95-110">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="7ad95-111">Bien que ce didacticiel explique comment toodo pour **Linux**, vous pouvez effectuer même hello pour un ordinateur Windows Server hébergé dans Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad95-111">Although this tutorial explains how toodo this for **Linux**, you can do hello same for a Windows Server VM hosted in Azure.</span></span> 
* <span data-ttu-id="7ad95-112">Créez une application Django dans Linux.</span><span class="sxs-lookup"><span data-stu-id="7ad95-112">Create a new Django application in Linux.</span></span>

<span data-ttu-id="7ad95-113">didacticiel de Hello vous montre comment toobuild une base Hello World web application.</span><span class="sxs-lookup"><span data-stu-id="7ad95-113">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="7ad95-114">application Hello est hébergée dans une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad95-114">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="7ad95-115">Hello suivant capture d’écran montre application hello terminée :</span><span class="sxs-lookup"><span data-stu-id="7ad95-115">hello following screenshot shows hello completed application:</span></span>

![Une fenêtre de navigateur affiche la page de Hello World hello dans Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

[!INCLUDE [create-account-and-vms-note](../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="7ad95-117">Créer et configurer une machine virtuelle Azure de toohost Django</span><span class="sxs-lookup"><span data-stu-id="7ad95-117">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="7ad95-118">toocreate une machine virtuelle Azure avec hello distribution d’Ubuntu Server 14.04 LTS, consultez [créer une machine virtuelle Linux Bonjour Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ad95-118">toocreate an Azure virtual machine with hello Ubuntu Server 14.04 LTS distribution, see [Create a Linux virtual machine in hello Azure portal](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7ad95-119">Vous pouvez également choisir un authentification par de mot de passe au lieu d’utiliser une clé publique SSH.</span><span class="sxs-lookup"><span data-stu-id="7ad95-119">You also can choose password authentication instead of using an SSH public key.</span></span>
2. <span data-ttu-id="7ad95-120">tooedit hello réseau sécurité groupe tooallow entrant HTTP trafic tooport 80, consultez [créer des groupes de sécurité réseau Bonjour Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span><span class="sxs-lookup"><span data-stu-id="7ad95-120">tooedit hello network security group tooallow incoming HTTP traffic tooport 80, see [Create network security groups in hello Azure portal](../../virtual-network/virtual-networks-create-nsg-arm-pportal.md).</span></span>
3. <span data-ttu-id="7ad95-121">(Facultatif) Par défaut, votre nouvelle machine virtuelle n’a pas de nom de domaine complet (FQDN).</span><span class="sxs-lookup"><span data-stu-id="7ad95-121">(Optional) By default, your new virtual machine doesn't have a fully qualified domain name (FQDN).</span></span>  <span data-ttu-id="7ad95-122">toocreate une machine virtuelle avec un nom de domaine complet, consultez [création d’un nom de domaine complet dans hello portail Azure pour une machine virtuelle Windows](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7ad95-122">toocreate a VM with an FQDN, see [Create an FQDN in hello Azure portal for a Windows VM](../windows/portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="7ad95-123">Cette étape n’est pas requise pour l’achèvement de ce didacticiel.</span><span class="sxs-lookup"><span data-stu-id="7ad95-123">This step is not required for completing this tutorial.</span></span>

## <span data-ttu-id="7ad95-124"><a id="setup"></a>Configuration d’environnement de développement hello</span><span class="sxs-lookup"><span data-stu-id="7ad95-124"><a id="setup"> </a>Set up hello development environment</span></span>
> [!NOTE]
> <span data-ttu-id="7ad95-125">Si vous avez besoin de tooinstall Python ou que vous souhaitez que les bibliothèques clientes toouse hello, consultez hello [guide d’installation de Python](../../python-how-to-install.md).</span><span class="sxs-lookup"><span data-stu-id="7ad95-125">If you need tooinstall Python or want toouse hello client libraries, see hello [Python installation guide](../../python-how-to-install.md).</span></span>

<span data-ttu-id="7ad95-126">Hello Ubuntu Linux VM a Python 2.7 préinstallés, mais il n’est fourni avec Apache ou Django.</span><span class="sxs-lookup"><span data-stu-id="7ad95-126">hello Ubuntu Linux VM has Python 2.7 preinstalled, but it doesn't come with Apache or Django.</span></span> <span data-ttu-id="7ad95-127">Hello suivant les étapes tooconnect tooyour machine virtuelle et d’installer Apache et Django :</span><span class="sxs-lookup"><span data-stu-id="7ad95-127">Complete hello following steps tooconnect tooyour VM and install Apache and Django:</span></span>

1. <span data-ttu-id="7ad95-128">Ouvrez une nouvelle fenêtre de terminal.</span><span class="sxs-lookup"><span data-stu-id="7ad95-128">Open a new Terminal window.</span></span>
2. <span data-ttu-id="7ad95-129">tooconnect toohello machine virtuelle Azure, entrez hello commande suivante.</span><span class="sxs-lookup"><span data-stu-id="7ad95-129">tooconnect toohello Azure VM, enter hello following command.</span></span> <span data-ttu-id="7ad95-130">Si vous n’avez pas créé un nom de domaine complet, vous pouvez vous connecter à l’aide de hello adresse IP publique qui est affiché dans la machine virtuelle de hello résumé Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad95-130">If you didn't create an FQDN, you can connect by using hello public IP address that's displayed in hello virtual machine summary in hello Azure portal.</span></span>
   
       $ ssh yourusername@yourVmUrl
3. <span data-ttu-id="7ad95-131">tooinstall Django, entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7ad95-131">tooinstall Django, enter hello following commands:</span></span>
   
       $ sudo apt-get install python-setuptools python-pip
       $ sudo pip install django
4. <span data-ttu-id="7ad95-132">tooinstall Apache avec mod-wsgi sous, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7ad95-132">tooinstall Apache with mod-wsgi, enter hello following command:</span></span>
   
       $ sudo apt-get install apache2 libapache2-mod-wsgi

## <a name="create-a-new-django-app"></a><span data-ttu-id="7ad95-133">Créer une application Django</span><span class="sxs-lookup"><span data-stu-id="7ad95-133">Create a new Django app</span></span>
1. <span data-ttu-id="7ad95-134">toouse tooaccess SSH votre machine virtuelle, la fenêtre de Terminal ouverte hello que vous avez utilisé dans hello précédant la section.</span><span class="sxs-lookup"><span data-stu-id="7ad95-134">toouse SSH tooaccess your VM, open hello Terminal window you used in hello preceding section.</span></span>
2. <span data-ttu-id="7ad95-135">toocreate un nouveau projet Django, entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7ad95-135">toocreate a new Django project, enter hello following commands:</span></span>
   
       $ cd /var/www
       $ sudo django-admin.py startproject helloworld
   
   <span data-ttu-id="7ad95-136">Hello `django-admin.py` script génère une structure de base pour les sites Web basés sur Django :</span><span class="sxs-lookup"><span data-stu-id="7ad95-136">hello `django-admin.py` script generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="7ad95-137">`helloworld/manage.py` vous aide à démarrer et arrêter l’hébergement de votre site web basé sur Django.</span><span class="sxs-lookup"><span data-stu-id="7ad95-137">`helloworld/manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="7ad95-138">`helloworld/helloworld/settings.py` contient les paramètres Django de votre application.</span><span class="sxs-lookup"><span data-stu-id="7ad95-138">`helloworld/helloworld/settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="7ad95-139">`helloworld/helloworld/urls.py`contient du code de mappage de hello entre chaque URL et sa vue.</span><span class="sxs-lookup"><span data-stu-id="7ad95-139">`helloworld/helloworld/urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="7ad95-140">Dans le répertoire de /var/www/helloworld/helloworld hello, créez un nouveau fichier nommé views.py.</span><span class="sxs-lookup"><span data-stu-id="7ad95-140">In hello /var/www/helloworld/helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="7ad95-141">Ce fichier contient la vue hello qui restitue la page « hello world » de hello.</span><span class="sxs-lookup"><span data-stu-id="7ad95-141">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="7ad95-142">Dans votre éditeur de code, entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7ad95-142">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="7ad95-143">Remplacez contenu hello du fichier de urls.py hello hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="7ad95-143">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-apache"></a><span data-ttu-id="7ad95-144">Configurer Apache</span><span class="sxs-lookup"><span data-stu-id="7ad95-144">Set up Apache</span></span>
1. <span data-ttu-id="7ad95-145">Dans le dossier de /etc/apache2/sites-available/helloworld.conf hello, créez un fichier de configuration d’hôte virtuel Apache.</span><span class="sxs-lookup"><span data-stu-id="7ad95-145">In hello /etc/apache2/sites-available/helloworld.conf folder, create an Apache virtual host configuration file.</span></span> <span data-ttu-id="7ad95-146">Définissez toohello de contenu hello valeurs suivantes.</span><span class="sxs-lookup"><span data-stu-id="7ad95-146">Set hello contents toohello following values.</span></span> <span data-ttu-id="7ad95-147">Remplacez *Nomov* par nom d’ordinateur hello vous utilisez hello (par exemple, *pyubuntu*).</span><span class="sxs-lookup"><span data-stu-id="7ad95-147">Replace *yourVmName* with hello actual name of hello machine you are using (for example, *pyubuntu*).</span></span>
   
       <VirtualHost *:80>
       ServerName yourVmName
       </VirtualHost>
       WSGIScriptAlias / /var/www/helloworld/helloworld/wsgi.py
       WSGIPythonPath /var/www/helloworld
2. <span data-ttu-id="7ad95-148">site hello tooactivate, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7ad95-148">tooactivate hello site, use hello following command:</span></span>
   
       $ sudo a2ensite helloworld
3. <span data-ttu-id="7ad95-149">toorestart Apache, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="7ad95-149">toorestart Apache, use hello following command:</span></span>
   
       $ sudo service apache2 reload
4. <span data-ttu-id="7ad95-150">Charger la page Web de hello dans votre navigateur :</span><span class="sxs-lookup"><span data-stu-id="7ad95-150">Load hello webpage in your browser:</span></span>
   
   ![Une fenêtre de navigateur affiche la page de hello hello world dans Azure](./media/python-django-web-app/mac-linux-django-helloworld-browser.png)

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="7ad95-152">Arrêter votre machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="7ad95-152">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="7ad95-153">Lorsque vous avez terminé ce didacticiel, nous vous recommandons d’arrêter ou de supprimer hello Azure VM, vous avez créé pour le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="7ad95-153">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="7ad95-154">Cela a pour effet de libérer des ressources pour d’autres didacticiels et d’éviter de vous exposer à des frais pour l’utilisation d’Azure.</span><span class="sxs-lookup"><span data-stu-id="7ad95-154">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

