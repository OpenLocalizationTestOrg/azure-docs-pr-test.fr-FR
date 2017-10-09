---
title: "l’application web sur un ordinateur Windows Server Azure aaaDjango | Documents Microsoft"
description: "Découvrez comment toohost un site Web de base Django dans Azure à l’aide d’une machine virtuelle Windows Server 2012 R2 Datacenter avec le modèle de déploiement classique hello."
services: virtual-machines-windows
documentationcenter: python
author: huguesv
manager: wpickett
editor: 
tags: azure-service-management
ms.assetid: e36484d1-afbf-47f5-b755-5e65397dc1c3
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: python
ms.topic: article
ms.date: 05/31/2017
ms.author: huvalo
ms.openlocfilehash: 55847e3c6d6769965be29077e8d4eeebad914637
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="70453-103">Application web Django Hello World sur une machine virtuelle Windows Server</span><span class="sxs-lookup"><span data-stu-id="70453-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="70453-104">Azure dispose de deux modèles de déploiement différentes pour la création et utilisation des ressources : [modèle de déploiement classique Azure Resource Manager et hello](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="70453-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and hello classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="70453-105">Cet article décrit le modèle de déploiement classique hello.</span><span class="sxs-lookup"><span data-stu-id="70453-105">This article describes hello classic deployment model.</span></span> <span data-ttu-id="70453-106">Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.</span><span class="sxs-lookup"><span data-stu-id="70453-106">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="70453-107">Ce didacticiel vous montre comment toohost un Django-site Web dans Windows Server dans des Machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="70453-107">This tutorial shows you how toohost a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="70453-108">Dans le didacticiel de hello, nous ne Supposons aucune expérience préalable de Azure.</span><span class="sxs-lookup"><span data-stu-id="70453-108">In hello tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="70453-109">Lorsque vous avez terminé le didacticiel de hello, vous pouvez avoir une application basée sur les Django et en cours d’exécution dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="70453-109">When you finish hello tutorial, you can have a Django-based application up and running in hello cloud.</span></span>

<span data-ttu-id="70453-110">Découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="70453-110">Learn how to:</span></span>

* <span data-ttu-id="70453-111">Configurer une machine virtuelle Azure de toohost Django.</span><span class="sxs-lookup"><span data-stu-id="70453-111">Set up an Azure virtual machine toohost Django.</span></span> <span data-ttu-id="70453-112">Bien que ce didacticiel explique comment toodo pour **Windows Server**, vous pouvez effectuer même hello pour un VM Linux hébergés dans Azure.</span><span class="sxs-lookup"><span data-stu-id="70453-112">Although this tutorial explains how toodo this for **Windows Server**, you can do hello same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="70453-113">Créez une application Django dans Windows.</span><span class="sxs-lookup"><span data-stu-id="70453-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="70453-114">didacticiel de Hello vous montre comment toobuild une base Hello World web application.</span><span class="sxs-lookup"><span data-stu-id="70453-114">hello tutorial shows you how toobuild a basic Hello World web application.</span></span> <span data-ttu-id="70453-115">application Hello est hébergée dans une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="70453-115">hello application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="70453-116">Hello suivant capture d’écran montre application hello terminée :</span><span class="sxs-lookup"><span data-stu-id="70453-116">hello following screenshot shows hello completed application:</span></span>

![Une fenêtre de navigateur affiche la page de hello hello world dans Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a><span data-ttu-id="70453-118">Créer et configurer une machine virtuelle Azure de toohost Django</span><span class="sxs-lookup"><span data-stu-id="70453-118">Create and set up an Azure virtual machine toohost Django</span></span>

1. <span data-ttu-id="70453-119">toocreate une machine virtuelle Azure avec hello distribution de Windows Server 2012 R2 Datacenter, consultez [créer une machine virtuelle exécutant Windows Bonjour Azure portal](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="70453-119">toocreate an Azure virtual machine with hello Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in hello Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="70453-120">Configurer Azure toodirect le trafic du port 80 de hello web tooport 80 sur l’ordinateur virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="70453-120">Set Azure toodirect port 80 traffic from hello web tooport 80 on hello virtual machine:</span></span>
   
   1. <span data-ttu-id="70453-121">Bonjour portail Azure, accédez toohello le tableau de bord et sélectionnez votre machine virtuelle qui vient d’être créé.</span><span class="sxs-lookup"><span data-stu-id="70453-121">In hello Azure portal, go toohello dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="70453-122">Cliquez sur **Points de terminaison**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="70453-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Ajout d’un point de terminaison](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="70453-124">Sur hello **ajouter le point de terminaison** page, pour **nom**, entrez **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="70453-124">On hello **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="70453-125">Définir hello publiques et privées des ports TCP trop**80**.</span><span class="sxs-lookup"><span data-stu-id="70453-125">Set hello public and private TCP ports too**80**.</span></span>

     ![Entrez le nom et définissez les ports public et privé](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="70453-127">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="70453-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="70453-128">Dans le tableau de bord hello, sélectionnez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="70453-128">In hello dashboard, select your VM.</span></span> <span data-ttu-id="70453-129">connexion tooremotely toouse protocole RDP (Remote Desktop) toohello nouvellement créé la machine virtuelle Azure, cliquez sur **connexion**.</span><span class="sxs-lookup"><span data-stu-id="70453-129">toouse Remote Desktop Protocol (RDP) tooremotely sign in toohello newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="70453-130">Hello suivant instructions supposent que vous dans la machine virtuelle de toohello correctement signé.</span><span class="sxs-lookup"><span data-stu-id="70453-130">hello following instructions assume that you signed in toohello virtual machine correctly.</span></span> <span data-ttu-id="70453-131">Elles supposent également que vous émettez des commandes dans la machine virtuelle de hello et non sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="70453-131">They also assume that you are issuing commands in hello virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="70453-132"><a id="setup"></a>Installer Python, Django et WFastCGI</span><span class="sxs-lookup"><span data-stu-id="70453-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="70453-133">toodownload à l’aide d’Internet Explorer, vous pouvez avoir tooconfigure Internet Explorer **Configuration de sécurité renforcée** paramètres.</span><span class="sxs-lookup"><span data-stu-id="70453-133">toodownload by using Internet Explorer, you might have tooconfigure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="70453-134">toodo, cliquez sur **Démarrer** > **outils d’administration** > **le Gestionnaire de serveur** > **deserveurLocal**.</span><span class="sxs-lookup"><span data-stu-id="70453-134">toodo this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="70453-135">Cliquez sur **Configuration de sécurité renforcée d’Internet Explorer**, puis sélectionnez **Désactivé**.</span><span class="sxs-lookup"><span data-stu-id="70453-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="70453-136">Installer les versions les plus récentes de Python 2.7 ou 3.4 Python de hello [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="70453-136">Install hello latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="70453-137">Installer des packages wfastcgi et django hello, l’utilisation de pip.</span><span class="sxs-lookup"><span data-stu-id="70453-137">Install hello wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="70453-138">Pour les Python 2.7, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70453-138">For Python 2.7, use hello following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="70453-139">Pour les Python 3.4, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70453-139">For Python 3.4, use hello following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="70453-140">Installer IIS avec FastCGI</span><span class="sxs-lookup"><span data-stu-id="70453-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="70453-141">Installez les services Internet (IIS, Internet Information Services) avec prise en charge de FastCGI.</span><span class="sxs-lookup"><span data-stu-id="70453-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="70453-142">Cette opération peut prendre plusieurs minutes tooexecute.</span><span class="sxs-lookup"><span data-stu-id="70453-142">This might take several minutes tooexecute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="70453-143">Créer une application Django</span><span class="sxs-lookup"><span data-stu-id="70453-143">Create a new Django application</span></span>
1. <span data-ttu-id="70453-144">Dans C:\inetpub\wwwroot, toocreate un nouveau projet Django, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70453-144">In C:\inetpub\wwwroot, toocreate a new Django project, enter hello following command:</span></span>
   
   <span data-ttu-id="70453-145">Pour les Python 2.7, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70453-145">For Python 2.7, use hello following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="70453-146">Pour les Python 3.4, utilisez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="70453-146">For Python 3.4, use hello following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![résultat de Hello de commande New-AzureService de hello](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="70453-148">Hello `django-admin` commande génère une structure de base pour les sites Web basés sur Django :</span><span class="sxs-lookup"><span data-stu-id="70453-148">hello `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="70453-149">`helloworld\manage.py` vous aide à démarrer et arrêter l’hébergement de votre site web basé sur Django.</span><span class="sxs-lookup"><span data-stu-id="70453-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="70453-150">`helloworld\helloworld\settings.py` contient les paramètres Django de votre application.</span><span class="sxs-lookup"><span data-stu-id="70453-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="70453-151">`helloworld\helloworld\urls.py`contient du code de mappage de hello entre chaque URL et sa vue.</span><span class="sxs-lookup"><span data-stu-id="70453-151">`helloworld\helloworld\urls.py` has hello mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="70453-152">Dans le répertoire de C:\inetpub\wwwroot\helloworld\helloworld hello, créez un nouveau fichier nommé views.py.</span><span class="sxs-lookup"><span data-stu-id="70453-152">In hello C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="70453-153">Ce fichier contient la vue hello qui restitue la page « hello world » de hello.</span><span class="sxs-lookup"><span data-stu-id="70453-153">This file has hello view that renders hello "hello world" page.</span></span> <span data-ttu-id="70453-154">Dans votre éditeur de code, entrez hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="70453-154">In your code editor, enter hello following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="70453-155">Remplacez contenu hello du fichier de urls.py hello hello suivant de commandes :</span><span class="sxs-lookup"><span data-stu-id="70453-155">Replace hello contents of hello urls.py file with hello following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="70453-156">Configurer IIS</span><span class="sxs-lookup"><span data-stu-id="70453-156">Set up IIS</span></span>
1. <span data-ttu-id="70453-157">Dans le fichier applicationhost.config global hello déverrouiller la section des gestionnaires hello.</span><span class="sxs-lookup"><span data-stu-id="70453-157">In hello global applicationhost.config file, unlock hello handlers section.</span></span>  <span data-ttu-id="70453-158">Ainsi, votre gestionnaire Python hello de toouse du fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="70453-158">This allows your web.config file toouse hello Python handler.</span></span> <span data-ttu-id="70453-159">Ajoutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="70453-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="70453-160">Activez WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="70453-160">Activate WFastCGI.</span></span> <span data-ttu-id="70453-161">Cela ajoute un fichier applicationhost.config global application toohello qui fait référence tooyour interpréteur exécutable et hello wfastcgi.py script Python.</span><span class="sxs-lookup"><span data-stu-id="70453-161">This adds an application toohello global applicationhost.config file, which refers tooyour Python interpreter executable and hello wfastcgi.py script.</span></span>
   
    <span data-ttu-id="70453-162">Dans Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="70453-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="70453-163">Dans Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="70453-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="70453-164">Créez un fichier web.config dans C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="70453-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="70453-165">Hello valeur Hello `scriptProcessor` attribut doit correspondre à sortie hello hello précédant l’étape.</span><span class="sxs-lookup"><span data-stu-id="70453-165">hello value of hello `scriptProcessor` attribute should match hello output from hello preceding step.</span></span> <span data-ttu-id="70453-166">Pour plus d’informations sur la configuration de wfastcgi hello, consultez [pypi wfastcgi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="70453-166">For more information about hello wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="70453-167">Dans Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="70453-167">In  Python 2.7:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python27\python.exe|C:\Python27\Lib\site-packages\wfastcgi.pyc" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
   
   <span data-ttu-id="70453-168">Dans Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="70453-168">In  Python 3.4:</span></span>
   
        <configuration>
          <appSettings>
            <add key="WSGI_HANDLER" value="django.core.handlers.wsgi.WSGIHandler()" />
            <add key="PYTHONPATH" value="C:\inetpub\wwwroot\helloworld" />
            <add key="DJANGO_SETTINGS_MODULE" value="helloworld.settings" />
          </appSettings>
          <system.webServer>
            <handlers>
                <add name="Python FastCGI" path="*" verb="*" modules="FastCgiModule" scriptProcessor="C:\Python34\python.exe|C:\Python34\Lib\site-packages\wfastcgi.py" resourceType="Unspecified" />
            </handlers>
          </system.webServer>
        </configuration>
4. <span data-ttu-id="70453-169">Mise à jour d’emplacement hello hello IIS par défaut du site Web toopoint toohello Django dossier de projet :</span><span class="sxs-lookup"><span data-stu-id="70453-169">Update hello location of hello IIS default website toopoint toohello Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="70453-170">Charger la page Web de hello dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="70453-170">Load hello webpage in your browser.</span></span>

![Une fenêtre de navigateur affiche la page de hello hello world dans Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="70453-172">Arrêter votre machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="70453-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="70453-173">Lorsque vous avez terminé ce didacticiel, nous vous recommandons d’arrêter ou de supprimer hello Azure VM, vous avez créé pour le didacticiel de hello.</span><span class="sxs-lookup"><span data-stu-id="70453-173">When you're done with this tutorial, we recommend that you shut down or remove hello Azure VM you created for hello tutorial.</span></span> <span data-ttu-id="70453-174">Cela a pour effet de libérer des ressources pour d’autres didacticiels et d’éviter de vous exposer à des frais pour l’utilisation d’Azure.</span><span class="sxs-lookup"><span data-stu-id="70453-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
