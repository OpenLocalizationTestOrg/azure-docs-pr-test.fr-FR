---
title: Application web Django sur une machine virtuelle Windows Server Azure | Microsoft Docs
description: "Découvrez comment héberger un site web Django dans Azure avec une machine virtuelle Windows Server 2012 R2 Datacenter à l’aide du modèle de déploiement classique."
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
ms.openlocfilehash: 283a296fb39863c2801be1093cc4f56904786abd
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a><span data-ttu-id="03a61-103">Application web Django Hello World sur une machine virtuelle Windows Server</span><span class="sxs-lookup"><span data-stu-id="03a61-103">Django Hello World web app on a Windows Server VM</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="03a61-104">Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Azure Resource Manager et le modèle de déploiement classique](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="03a61-104">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and the classic deployment model](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="03a61-105">Cet article décrit le modèle de déploiement classique.</span><span class="sxs-lookup"><span data-stu-id="03a61-105">This article describes the classic deployment model.</span></span> <span data-ttu-id="03a61-106">Pour la plupart des nouveaux déploiements, nous recommandons d’utiliser le modèle Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="03a61-106">We recommend that most new deployments use the Resource Manager model.</span></span>

<span data-ttu-id="03a61-107">Ce didacticiel vous montre comment héberger un site web Django dans Windows Server dans des machines virtuelles Azure.</span><span class="sxs-lookup"><span data-stu-id="03a61-107">This tutorial shows you how to host a Django-based website in Windows Server in Azure Virtual Machines.</span></span> <span data-ttu-id="03a61-108">Dans le didacticiel, nous ne supposons aucune expérience préalable avec Azure.</span><span class="sxs-lookup"><span data-stu-id="03a61-108">In the tutorial, we assume no prior experience with Azure.</span></span> <span data-ttu-id="03a61-109">Quand vous avez terminé le didacticiel, vous pouvez avoir une application basée sur Django opérationnelle dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="03a61-109">When you finish the tutorial, you can have a Django-based application up and running in the cloud.</span></span>

<span data-ttu-id="03a61-110">Découvrez comment :</span><span class="sxs-lookup"><span data-stu-id="03a61-110">Learn how to:</span></span>

* <span data-ttu-id="03a61-111">Configurez une machine virtuelle Azure pour héberger Django.</span><span class="sxs-lookup"><span data-stu-id="03a61-111">Set up an Azure virtual machine to host Django.</span></span> <span data-ttu-id="03a61-112">Bien que ce didacticiel explique comment procéder pour **Windows Server**, vous pouvez faire de même pour une machine virtuelle Linux hébergée dans Azure.</span><span class="sxs-lookup"><span data-stu-id="03a61-112">Although this tutorial explains how to do this for **Windows Server**, you can do the same for a Linux VM hosted in Azure.</span></span>
* <span data-ttu-id="03a61-113">Créez une application Django dans Windows.</span><span class="sxs-lookup"><span data-stu-id="03a61-113">Create a new Django application in Windows.</span></span>

<span data-ttu-id="03a61-114">Le didacticiel vous montre comment créer une application web Hello World de base.</span><span class="sxs-lookup"><span data-stu-id="03a61-114">The tutorial shows you how to build a basic Hello World web application.</span></span> <span data-ttu-id="03a61-115">L’application est hébergée sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="03a61-115">The application is hosted in an Azure virtual machine.</span></span>

<span data-ttu-id="03a61-116">La capture d’écran suivante présente l’application terminée :</span><span class="sxs-lookup"><span data-stu-id="03a61-116">The following screenshot shows the completed application:</span></span>

![Fenêtre de navigateur affichant la page Hello World dans Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-to-host-django"></a><span data-ttu-id="03a61-118">Créer et configurer une machine virtuelle Azure pour héberger Django</span><span class="sxs-lookup"><span data-stu-id="03a61-118">Create and set up an Azure virtual machine to host Django</span></span>

1. <span data-ttu-id="03a61-119">Pour créer une machine virtuelle Azure avec la distribution Windows Server 2012 R2 Datacenter, consultez [Créer une machine virtuelle exécutant Windows dans le portail Azure](tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="03a61-119">To create an Azure virtual machine with the Windows Server 2012 R2 Datacenter distribution, see [Create a virtual machine running Windows in the Azure portal](tutorial.md).</span></span>
2. <span data-ttu-id="03a61-120">Configurez Azure pour diriger le trafic du port 80 à partir du web vers le port 80 de la machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="03a61-120">Set Azure to direct port 80 traffic from the web to port 80 on the virtual machine:</span></span>
   
   1. <span data-ttu-id="03a61-121">Dans le portail Azure, accédez au tableau de bord et sélectionnez votre machine virtuelle qui vient d’être créée.</span><span class="sxs-lookup"><span data-stu-id="03a61-121">In the Azure portal, go to the dashboard and select your newly created virtual machine.</span></span>
   2. <span data-ttu-id="03a61-122">Cliquez sur **Points de terminaison**, puis sur **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="03a61-122">Click **Endpoints**, and then click **Add**.</span></span>

     ![Ajout d’un point de terminaison](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. <span data-ttu-id="03a61-124">Dans la page **Ajouter un point de terminaison**, pour **Nom**, entrez **HTTP**.</span><span class="sxs-lookup"><span data-stu-id="03a61-124">On the **Add endpoint** page, for **Name**, enter **HTTP**.</span></span> <span data-ttu-id="03a61-125">Affectez aux ports TCP public et privé la valeur **80**.</span><span class="sxs-lookup"><span data-stu-id="03a61-125">Set the public and private TCP ports to **80**.</span></span>

     ![Entrez le nom et définissez les ports public et privé](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. <span data-ttu-id="03a61-127">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="03a61-127">Click **OK**.</span></span>
     
3. <span data-ttu-id="03a61-128">Dans le tableau de bord, sélectionnez votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="03a61-128">In the dashboard, select your VM.</span></span> <span data-ttu-id="03a61-129">Pour utiliser le protocole RDP (Remote Desktop Protocol) afin de vous connecter à distance à la machine virtuelle Azure que vous venez de créer, cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="03a61-129">To use Remote Desktop Protocol (RDP) to remotely sign in to the newly created Azure virtual machine, click **Connect**.</span></span>  

> [!IMPORTANT] 
> <span data-ttu-id="03a61-130">Les instructions suivantes supposent que vous êtes connecté correctement à la machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="03a61-130">The following instructions assume that you signed in to the virtual machine correctly.</span></span> <span data-ttu-id="03a61-131">Elles supposent également que vous émettez des commandes sur la machine virtuelle et non sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="03a61-131">They also assume that you are issuing commands in the virtual machine and not on your local computer.</span></span>

## <span data-ttu-id="03a61-132"><a id="setup"> </a>Installer Python, Django et WFastCGI</span><span class="sxs-lookup"><span data-stu-id="03a61-132"><a id="setup"> </a>Install Python, Django, and WFastCGI</span></span>
> [!NOTE]
> <span data-ttu-id="03a61-133">Pour un téléchargement à l’aide d’Internet Explorer, vous devrez peut-être configurer les paramètres **Configuration de sécurité renforcée** d’Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="03a61-133">To download by using Internet Explorer, you might have to configure Internet Explorer **Enhanced Security Configuration** settings.</span></span> <span data-ttu-id="03a61-134">Pour ce faire, cliquez sur **Démarrer** > **Outils d’administration** > **Gestionnaire de serveur** > **Serveur local**.</span><span class="sxs-lookup"><span data-stu-id="03a61-134">To do this, click **Start** > **Administrative Tools** > **Server Manager** > **Local Server**.</span></span> <span data-ttu-id="03a61-135">Cliquez sur **Configuration de sécurité renforcée d’Internet Explorer**, puis sélectionnez **Désactivé**.</span><span class="sxs-lookup"><span data-stu-id="03a61-135">Click **IE Enhanced Security Configuration**, and then select **Off**.</span></span>

1. <span data-ttu-id="03a61-136">Installez les dernières versions de Python 2.7 ou Python 3.4 à partir de [python.org][python.org].</span><span class="sxs-lookup"><span data-stu-id="03a61-136">Install the latest versions of Python 2.7 or Python 3.4 from [python.org][python.org].</span></span>
2. <span data-ttu-id="03a61-137">Installez les packages wfastcgi et django packages à l'aide de pip.</span><span class="sxs-lookup"><span data-stu-id="03a61-137">Install the wfastcgi and django packages using pip.</span></span>
   
    <span data-ttu-id="03a61-138">Pour Python 2.7, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03a61-138">For Python 2.7, use the following command:</span></span>
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    <span data-ttu-id="03a61-139">Pour Python 3.4, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03a61-139">For Python 3.4, use the following command:</span></span>
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a><span data-ttu-id="03a61-140">Installer IIS avec FastCGI</span><span class="sxs-lookup"><span data-stu-id="03a61-140">Install IIS with FastCGI</span></span>
* <span data-ttu-id="03a61-141">Installez les services Internet (IIS, Internet Information Services) avec prise en charge de FastCGI.</span><span class="sxs-lookup"><span data-stu-id="03a61-141">Install Internet Information Services (IIS) with FastCGI support.</span></span> <span data-ttu-id="03a61-142">Cela peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="03a61-142">This might take several minutes to execute.</span></span>
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a><span data-ttu-id="03a61-143">Créer une application Django</span><span class="sxs-lookup"><span data-stu-id="03a61-143">Create a new Django application</span></span>
1. <span data-ttu-id="03a61-144">Dans C:\inetpub\wwwroot, entrez la commande suivante pour créer un projet Django :</span><span class="sxs-lookup"><span data-stu-id="03a61-144">In C:\inetpub\wwwroot, to create a new Django project, enter the following command:</span></span>
   
   <span data-ttu-id="03a61-145">Pour Python 2.7, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03a61-145">For Python 2.7, use the following command:</span></span>
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   <span data-ttu-id="03a61-146">Pour Python 3.4, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="03a61-146">For Python 3.4, use the following command:</span></span>
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![Résultat de la commande New-AzureService](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. <span data-ttu-id="03a61-148">La commande `django-admin` génère une structure de base pour les sites web Django :</span><span class="sxs-lookup"><span data-stu-id="03a61-148">The `django-admin` command generates a basic structure for Django-based websites:</span></span>
   
   * <span data-ttu-id="03a61-149">`helloworld\manage.py` vous permet de lancer et d’interrompre l’hébergement de votre site web Django.</span><span class="sxs-lookup"><span data-stu-id="03a61-149">`helloworld\manage.py` helps you start hosting and stop hosting your Django-based website.</span></span>
   * <span data-ttu-id="03a61-150">`helloworld\helloworld\settings.py` contient les paramètres Django de votre application.</span><span class="sxs-lookup"><span data-stu-id="03a61-150">`helloworld\helloworld\settings.py` has Django settings for your application.</span></span>
   * <span data-ttu-id="03a61-151">`helloworld\helloworld\urls.py` contient le code de mappage entre chaque URL et sa vue.</span><span class="sxs-lookup"><span data-stu-id="03a61-151">`helloworld\helloworld\urls.py` has the mapping code between each URL and its view.</span></span>
3. <span data-ttu-id="03a61-152">Créez un fichier nommé views.py dans le répertoire C:\inetpub\wwwroot\helloworld\helloworld.</span><span class="sxs-lookup"><span data-stu-id="03a61-152">In the C:\inetpub\wwwroot\helloworld\helloworld directory, create a new file named views.py.</span></span> <span data-ttu-id="03a61-153">Celui-ci contient la vue qui affiche la page « Hello World ».</span><span class="sxs-lookup"><span data-stu-id="03a61-153">This file has the view that renders the "hello world" page.</span></span> <span data-ttu-id="03a61-154">Dans votre éditeur de code, entrez les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="03a61-154">In your code editor, enter the following commands:</span></span>
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. <span data-ttu-id="03a61-155">Remplacez le contenu du fichier urls.py par les commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="03a61-155">Replace the contents of the urls.py file with the following commands:</span></span>
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a><span data-ttu-id="03a61-156">Configurer IIS</span><span class="sxs-lookup"><span data-stu-id="03a61-156">Set up IIS</span></span>
1. <span data-ttu-id="03a61-157">Déverrouillez la section des gestionnaires dans le fichier applicationhost.config global.</span><span class="sxs-lookup"><span data-stu-id="03a61-157">In the global applicationhost.config file, unlock the handlers section.</span></span>  <span data-ttu-id="03a61-158">Cela permet l’utilisation du gestionnaire Python dans votre fichier web.config.</span><span class="sxs-lookup"><span data-stu-id="03a61-158">This allows your web.config file to use the Python handler.</span></span> <span data-ttu-id="03a61-159">Ajoutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="03a61-159">Add this command:</span></span>
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. <span data-ttu-id="03a61-160">Activez WFastCGI.</span><span class="sxs-lookup"><span data-stu-id="03a61-160">Activate WFastCGI.</span></span> <span data-ttu-id="03a61-161">Cela ajoute une application au fichier applicationhost.config global qui fait référence à votre interpréteur Python exécutable et au script wfastcgi.py.</span><span class="sxs-lookup"><span data-stu-id="03a61-161">This adds an application to the global applicationhost.config file, which refers to your Python interpreter executable and the wfastcgi.py script.</span></span>
   
    <span data-ttu-id="03a61-162">Dans Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="03a61-162">In Python 2.7:</span></span>
   
        C:\python27\scripts\wfastcgi-enable
   
    <span data-ttu-id="03a61-163">Dans Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="03a61-163">In Python 3.4:</span></span>
   
        C:\python34\scripts\wfastcgi-enable
3. <span data-ttu-id="03a61-164">Créez un fichier web.config dans C:\inetpub\wwwroot\helloworld.</span><span class="sxs-lookup"><span data-stu-id="03a61-164">In C:\inetpub\wwwroot\helloworld, create a web.config file.</span></span> <span data-ttu-id="03a61-165">La valeur de l’attribut `scriptProcessor` doit correspondre à la sortie de l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="03a61-165">The value of the `scriptProcessor` attribute should match the output from the preceding step.</span></span> <span data-ttu-id="03a61-166">Pour plus d’informations sur le paramètre wfastcgi, consultez [wfastcgi sur Pypi][wfastcgi].</span><span class="sxs-lookup"><span data-stu-id="03a61-166">For more information about the wfastcgi setting, see [pypi wfastcgi][wfastcgi].</span></span>
   
   <span data-ttu-id="03a61-167">Dans Python 2.7 :</span><span class="sxs-lookup"><span data-stu-id="03a61-167">In  Python 2.7:</span></span>
   
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
   
   <span data-ttu-id="03a61-168">Dans Python 3.4 :</span><span class="sxs-lookup"><span data-stu-id="03a61-168">In  Python 3.4:</span></span>
   
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
4. <span data-ttu-id="03a61-169">Mettez à jour l’emplacement du site web IIS par défaut pour qu’il pointe vers le dossier de projet Django :</span><span class="sxs-lookup"><span data-stu-id="03a61-169">Update the location of the IIS default website to point to the Django project folder:</span></span>
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. <span data-ttu-id="03a61-170">Chargez la page web dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="03a61-170">Load the webpage in your browser.</span></span>

![Fenêtre de navigateur affichant la page Hello World dans Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a><span data-ttu-id="03a61-172">Arrêter votre machine virtuelle Azure</span><span class="sxs-lookup"><span data-stu-id="03a61-172">Shut down your Azure virtual machine</span></span>
<span data-ttu-id="03a61-173">À l’issue de ce didacticiel, nous vous recommandons d’arrêter ou de supprimer la machine virtuelle Azure que vous avez créée pour le suivre.</span><span class="sxs-lookup"><span data-stu-id="03a61-173">When you're done with this tutorial, we recommend that you shut down or remove the Azure VM you created for the tutorial.</span></span> <span data-ttu-id="03a61-174">Cela a pour effet de libérer des ressources pour d’autres didacticiels et d’éviter de vous exposer à des frais pour l’utilisation d’Azure.</span><span class="sxs-lookup"><span data-stu-id="03a61-174">This frees up resources for other tutorials, and you can avoid incurring Azure usage charges.</span></span>

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
