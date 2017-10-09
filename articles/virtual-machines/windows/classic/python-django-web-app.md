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
# <a name="django-hello-world-web-app-on-a-windows-server-vm"></a>Application web Django Hello World sur une machine virtuelle Windows Server

> [!IMPORTANT] 
> Azure dispose de deux modèles de déploiement différentes pour la création et utilisation des ressources : [modèle de déploiement classique Azure Resource Manager et hello](../../../resource-manager-deployment-model.md). Cet article décrit le modèle de déploiement classique hello. Nous recommandons que la plupart des nouveaux déploiements utilisent le modèle de gestionnaire de ressources hello.

Ce didacticiel vous montre comment toohost un Django-site Web dans Windows Server dans des Machines virtuelles Azure. Dans le didacticiel de hello, nous ne Supposons aucune expérience préalable de Azure. Lorsque vous avez terminé le didacticiel de hello, vous pouvez avoir une application basée sur les Django et en cours d’exécution dans le cloud de hello.

Découvrez comment :

* Configurer une machine virtuelle Azure de toohost Django. Bien que ce didacticiel explique comment toodo pour **Windows Server**, vous pouvez effectuer même hello pour un VM Linux hébergés dans Azure.
* Créez une application Django dans Windows.

didacticiel de Hello vous montre comment toobuild une base Hello World web application. application Hello est hébergée dans une machine virtuelle Azure.

Hello suivant capture d’écran montre application hello terminée :

![Une fenêtre de navigateur affiche la page de hello hello world dans Azure][1]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="create-and-set-up-an-azure-virtual-machine-toohost-django"></a>Créer et configurer une machine virtuelle Azure de toohost Django

1. toocreate une machine virtuelle Azure avec hello distribution de Windows Server 2012 R2 Datacenter, consultez [créer une machine virtuelle exécutant Windows Bonjour Azure portal](tutorial.md).
2. Configurer Azure toodirect le trafic du port 80 de hello web tooport 80 sur l’ordinateur virtuel de hello :
   
   1. Bonjour portail Azure, accédez toohello le tableau de bord et sélectionnez votre machine virtuelle qui vient d’être créé.
   2. Cliquez sur **Points de terminaison**, puis sur **Ajouter**.

     ![Ajout d’un point de terminaison](./media/python-django-web-app/django-helloworld-add-endpoint-new-portal.png)

   3. Sur hello **ajouter le point de terminaison** page, pour **nom**, entrez **HTTP**. Définir hello publiques et privées des ports TCP trop**80**.

     ![Entrez le nom et définissez les ports public et privé](./media/python-django-web-app/django-helloworld-add-endpoint-set-ports-new-portal.png)

   4. Cliquez sur **OK**.
     
3. Dans le tableau de bord hello, sélectionnez votre machine virtuelle. connexion tooremotely toouse protocole RDP (Remote Desktop) toohello nouvellement créé la machine virtuelle Azure, cliquez sur **connexion**.  

> [!IMPORTANT] 
> Hello suivant instructions supposent que vous dans la machine virtuelle de toohello correctement signé. Elles supposent également que vous émettez des commandes dans la machine virtuelle de hello et non sur votre ordinateur local.

## <a id="setup"></a>Installer Python, Django et WFastCGI
> [!NOTE]
> toodownload à l’aide d’Internet Explorer, vous pouvez avoir tooconfigure Internet Explorer **Configuration de sécurité renforcée** paramètres. toodo, cliquez sur **Démarrer** > **outils d’administration** > **le Gestionnaire de serveur** > **deserveurLocal**. Cliquez sur **Configuration de sécurité renforcée d’Internet Explorer**, puis sélectionnez **Désactivé**.

1. Installer les versions les plus récentes de Python 2.7 ou 3.4 Python de hello [python.org][python.org].
2. Installer des packages wfastcgi et django hello, l’utilisation de pip.
   
    Pour les Python 2.7, utilisez hello de commande suivante :
   
        c:\python27\scripts\pip install wfastcgi
        c:\python27\scripts\pip install django
   
    Pour les Python 3.4, utilisez hello de commande suivante :
   
        c:\python34\scripts\pip install wfastcgi
        c:\python34\scripts\pip install django

## <a name="install-iis-with-fastcgi"></a>Installer IIS avec FastCGI
* Installez les services Internet (IIS, Internet Information Services) avec prise en charge de FastCGI. Cette opération peut prendre plusieurs minutes tooexecute.
   
        start /wait %windir%\System32\PkgMgr.exe /iu:IIS-WebServerRole;IIS-WebServer;IIS-CommonHttpFeatures;IIS-StaticContent;IIS-DefaultDocument;IIS-DirectoryBrowsing;IIS-HttpErrors;IIS-HealthAndDiagnostics;IIS-HttpLogging;IIS-LoggingLibraries;IIS-RequestMonitor;IIS-Security;IIS-RequestFiltering;IIS-HttpCompressionStatic;IIS-WebServerManagementTools;IIS-ManagementConsole;WAS-WindowsActivationService;WAS-ProcessModel;WAS-NetFxEnvironment;WAS-ConfigurationAPI;IIS-CGI

## <a name="create-a-new-django-application"></a>Créer une application Django
1. Dans C:\inetpub\wwwroot, toocreate un nouveau projet Django, entrez hello de commande suivante :
   
   Pour les Python 2.7, utilisez hello de commande suivante :
   
       C:\Python27\Scripts\django-admin.exe startproject helloworld
   
   Pour les Python 3.4, utilisez hello de commande suivante :
   
       C:\Python34\Scripts\django-admin.exe startproject helloworld
   
   ![résultat de Hello de commande New-AzureService de hello](./media/python-django-web-app/django-helloworld-cmd-new-azure-service.png)
2. Hello `django-admin` commande génère une structure de base pour les sites Web basés sur Django :
   
   * `helloworld\manage.py` vous aide à démarrer et arrêter l’hébergement de votre site web basé sur Django.
   * `helloworld\helloworld\settings.py` contient les paramètres Django de votre application.
   * `helloworld\helloworld\urls.py`contient du code de mappage de hello entre chaque URL et sa vue.
3. Dans le répertoire de C:\inetpub\wwwroot\helloworld\helloworld hello, créez un nouveau fichier nommé views.py. Ce fichier contient la vue hello qui restitue la page « hello world » de hello. Dans votre éditeur de code, entrez hello suivant de commandes :
   
       from django.http import HttpResponse
       def home(request):
           html = "<html><body>Hello World!</body></html>"
           return HttpResponse(html)
4. Remplacez contenu hello du fichier de urls.py hello hello suivant de commandes :
   
       from django.conf.urls import patterns, url
       urlpatterns = patterns('',
           url(r'^$', 'helloworld.views.home', name='home'),
       )

## <a name="set-up-iis"></a>Configurer IIS
1. Dans le fichier applicationhost.config global hello déverrouiller la section des gestionnaires hello.  Ainsi, votre gestionnaire Python hello de toouse du fichier web.config. Ajoutez cette commande :
   
        %windir%\system32\inetsrv\appcmd unlock config -section:system.webServer/handlers
2. Activez WFastCGI. Cela ajoute un fichier applicationhost.config global application toohello qui fait référence tooyour interpréteur exécutable et hello wfastcgi.py script Python.
   
    Dans Python 2.7 :
   
        C:\python27\scripts\wfastcgi-enable
   
    Dans Python 3.4 :
   
        C:\python34\scripts\wfastcgi-enable
3. Créez un fichier web.config dans C:\inetpub\wwwroot\helloworld. Hello valeur Hello `scriptProcessor` attribut doit correspondre à sortie hello hello précédant l’étape. Pour plus d’informations sur la configuration de wfastcgi hello, consultez [pypi wfastcgi][wfastcgi].
   
   Dans Python 2.7 :
   
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
   
   Dans Python 3.4 :
   
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
4. Mise à jour d’emplacement hello hello IIS par défaut du site Web toopoint toohello Django dossier de projet :
   
        %windir%\system32\inetsrv\appcmd set vdir "Default Web Site/" -physicalPath:"C:\inetpub\wwwroot\helloworld"
5. Charger la page Web de hello dans votre navigateur.

![Une fenêtre de navigateur affiche la page de hello hello world dans Azure][1]

## <a name="shut-down-your-azure-virtual-machine"></a>Arrêter votre machine virtuelle Azure
Lorsque vous avez terminé ce didacticiel, nous vous recommandons d’arrêter ou de supprimer hello Azure VM, vous avez créé pour le didacticiel de hello. Cela a pour effet de libérer des ressources pour d’autres didacticiels et d’éviter de vous exposer à des frais pour l’utilisation d’Azure.

[1]: ./media/python-django-web-app/django-helloworld-browser-azure.png

[port80]: ./media/python-django-web-app/django-helloworld-port80.png

[Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[python.org]: https://www.python.org/downloads/
[wfastcgi]: https://pypi.python.org/pypi/wfastcgi
