---
title: "aaaCreate Azure rôles web et de travail pour PHP | Documents Microsoft"
description: "Un guide toocreating PHP rôles web et de travail dans un service cloud Azure et exécution PHP configuration hello."
services: 
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9f7ccda0-bd96-4f7b-a7af-fb279a9e975b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 04a6e8c9c379cb0f854645941b6bc7d614bb91f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-php-web-and-worker-roles"></a>Comment toocreate PHP rôles de travail
## <a name="overview"></a>Vue d'ensemble
Ce guide vous montrera comment toocreate PHP web ou travail rôles dans un environnement de développement Windows, choisissez une version spécifique de PHP hello « intégrées » versions disponibles, modifier la configuration de PHP hello, activer les extensions d’et enfin, déployer tooAzure. Elle décrit également comment tooconfigure un rôle web ou travail toouse un runtime PHP (avec la configuration personnalisée et extensions) que vous fournissez.

## <a name="what-are-php-web-and-worker-roles"></a>Présentation des rôles web et de travail PHP
Azure propose trois modèles de calcul pour l’exécution d’applications : Azure App Service, Azure Virtual Machines et Azure Cloud Services. Ils prennent tous les trois en charge PHP. Cloud Services, qui inclut les rôles web et de travail, offre une *plateforme PaaS (platform as a service)*. Dans un service cloud, un rôle web fournit un serveur web Internet Information Services (IIS) dédié serveur toohost d’applications web frontal. Un rôle de travail peut exécuter des tâches asynchrones, sur le long terme ou perpétuelles, indépendamment des entrées ou des interactions de l’utilisateur.

Pour plus d’informations, consultez [Calcul des options d’hébergement fournies par Azure](cloud-services/cloud-services-choose-me.md).

## <a name="download-hello-azure-sdk-for-php"></a>Télécharger hello Azure SDK pour PHP
Hello [Azure SDK pour PHP] se compose de plusieurs composants. Cet article utilise deux d'entre eux : Azure PowerShell et hello émulateurs Azure. Ces deux composants peuvent être installés via hello Microsoft Web Platform Installer. Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="create-a-cloud-services-project"></a>Création d'un projet Cloud Services
Hello première étape de création d’un rôle web ou de travail PHP est toocreate un projet de Service Azure. un projet de Service Azure sert comme un conteneur logique pour les rôles web et de travail, et il contient du projet hello [(.csdef) de définition de service] et [configuration du service (.cscfg)] fichiers.

toocreate un nouveau projet de Service Azure, exécutez Azure PowerShell en tant qu’administrateur et exécutez hello de commande suivante :

    PS C:\>New-AzureServiceProject myProject

Cette commande crée un nouveau répertoire (`myProject`) toowhich, vous pouvez ajouter des rôles web et worker.

## <a name="add-php-web-or-worker-roles"></a>Ajout de rôles web et de travail PHP
tooadd un projet tooa PHP de rôle web, exécutez hello commande à partir de dans le répertoire racine du projet hello suivante :

    PS C:\myProject> Add-AzurePHPWebRole roleName

Pour un rôle de travail, utilisez la commande suivante :

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> Hello `roleName` paramètre est facultatif. S’il est omis, le nom de rôle hello sera généré automatiquement. créé le rôle web premier Hello sera `WebRole1`, hello second sera `WebRole2`, et ainsi de suite. premier rôle de travail Hello créé sera `WorkerRole1`, hello second sera `WorkerRole2`, et ainsi de suite.
>
>

## <a name="specify-hello-built-in-php-version"></a>Spécifiez la version PHP hello intégrée
Lorsque vous ajoutez un projet de tooa de rôle web ou de travail PHP, les fichiers de configuration du projet hello sont modifiées afin que PHP est installé sur chaque instance du web ou de travail de votre application lorsqu’elle est déployée. version de hello toosee de PHP est installé par défaut, exécutez hello de commande suivante :

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

Hello sortie à partir de la commande hello ci-dessus ressemble toowhat est indiqué ci-dessous. Dans cet exemple, hello `IsDefault` est défini trop`true` pour PHP 5.3.17, indiquant qu’il sera la version PHP par défaut hello installée.

```
Runtime Version     PackageUri                      IsDefault
------- -------     ----------                      ---------
Node 0.6.17         http://nodertncu.blob.core...   False
Node 0.6.20         http://nodertncu.blob.core...   True
Node 0.8.4          http://nodertncu.blob.core...   False
IISNode 0.1.21      http://nodertncu.blob.core...   True
Cache 1.8.0         http://nodertncu.blob.core...   True
PHP 5.3.17          http://nodertncu.blob.core...   True
PHP 5.4.0           http://nodertncu.blob.core...   False
```

Vous pouvez définir hello PHP runtime version tooany des versions PHP hello répertoriés. Par exemple, la version tooset hello PHP (pour un rôle avec le nom de hello `roleName`) too5.4.0, hello utilisez commande suivante :

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> Les versions PHP disponibles peuvent changer Bonjour futures.
>
>

## <a name="customize-hello-built-in-php-runtime"></a>Personnaliser le runtime PHP intégré de hello
Vous avez un contrôle complet sur la configuration de hello du runtime PHP hello qui est installé lorsque vous suivez les étapes de hello ci-dessus, y compris la modification de `php.ini` paramètres et l’activation des extensions.

toocustomize hello intégré runtime PHP, procédez comme suit :

1. Ajouter un nouveau dossier, nommé `php`, toohello `bin` répertoire de votre rôle web. Pour un rôle de travail, ajoutez-le répertoire du rôle toohello.
2. Bonjour `php` dossier, créez un autre dossier appelé `ext`. Placez aucune `.dll` des fichiers d’extension (par exemple, `php_mongo.dll`) que vous souhaitez tooenable dans ce dossier.
3. Ajouter un `php.ini` fichier toohello `php` dossier. Activez les extensions personnalisées et définissez les directives PHP que vous voulez dans ce fichier. Par exemple, si vous souhaitiez tooturn `display_errors` sur et activer hello `php_mongo.dll` extension, le contenu de hello de votre `php.ini` fichier serait comme suit :

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> Tous les paramètres que vous ne définissez pas explicitement Bonjour `php.ini` fichier que vous fournissez automatiquement va être définie tootheir les valeurs par défaut. Toutefois, gardez à l’esprit que vous pouvez ajouter un fichier `php.ini` complet.
>
>

## <a name="use-your-own-php-runtime"></a>Utilisation de votre propre runtime PHP
Dans certains cas, au lieu de la sélection d’un runtime PHP intégré et le configurer comme décrit ci-dessus, vous souhaiterez tooprovide votre propre runtime PHP. Par exemple, vous pouvez utiliser hello même runtime PHP dans un rôle web ou de travail que vous utilisez dans votre environnement de développement. Il est ainsi plus facile tooensure qu’application hello ne changera pas de comportement dans votre environnement de production.

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a>Configurer un toouse de rôle web de votre propre runtime PHP
tooconfigure un toouse de rôle web un runtime PHP que vous fournissez, procédez comme suit :

1. Créez un projet de service Azure et ajoutez un rôle web PHP comme indiqué précédemment dans cette rubrique.
2. Créer un `php` dossier Bonjour `bin` dossier qui est dans le répertoire racine de votre rôle de serveur web, puis ajoutez votre toohello de runtime (tous les fichiers binaires, fichiers de configuration, les sous-dossiers, etc.) PHP `php` dossier.
3. (FACULTATIF) Si le runtime PHP utilise hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], vous devez tooconfigure votre tooinstall de rôle web [SQL Server Native Client 2012] [ sql native client] lorsqu’il est configuré. toodo, ajouter hello [programme d’installation de sqlncli.msi x64] toohello `bin` dossier dans le répertoire racine de votre rôle de serveur web. script de démarrage Hello décrit à l’étape suivante de hello exécutera en mode silencieux le programme d’installation de hello lors de la configuration de rôle de hello. Si le runtime PHP n’utilise pas hello Microsoft Drivers for PHP pour SQL Server, vous pouvez supprimer hello ligne suivante à partir du script hello indiqué dans l’étape suivante de hello :

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Définir une tâche de démarrage qui configure [Internet Information Services (IIS)] [ iis.net] toouse les demandes concernant votre toohandle du runtime PHP `.php` pages. toodo, ouvrez hello `setup_web.cmd` fichier (Bonjour `bin` fichier du répertoire racine de votre rôle de serveur web) dans un éditeur de texte et la remplacer son contenu avec hello suite de script :

    ```cmd
    @ECHO ON
    cd "%~dp0"

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    SET PHP_FULL_PATH=%~dp0php\php-cgi.exe
    SET NEW_PATH=%PATH%;%RoleRoot%\base\x86

    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%',maxInstances='12',idleTimeout='60000',activityTimeout='3600',requestTimeout='60000',instanceMaxRequests='10000',protocol='NamedPipe',flushNamedPipe='False']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PATH',value='%NEW_PATH%']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /+"[fullPath='%PHP_FULL_PATH%'].environmentVariables.[name='PHP_FCGI_MAX_REQUESTS',value='10000']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/handlers /+"[name='PHP',path='*.php',verb='GET,HEAD,POST',modules='FastCgiModule',scriptProcessor='%PHP_FULL_PATH%',resourceType='Either',requireAccess='Script']" /commit:apphost
    %WINDIR%\system32\inetsrv\appcmd.exe set config -section:system.webServer/fastCgi /"[fullPath='%PHP_FULL_PATH%'].queueLength:50000"
    ```
5. Ajoutez le répertoire racine de l’application fichiers tooyour web de votre rôle. Ce sera le répertoire racine du serveur hello web.
6. Publier votre application comme décrit dans hello [publier votre application](#publish-your-application) section ci-dessous.

> [!NOTE]
> Hello `download.ps1` script (Bonjour `bin` dossier du répertoire racine de hello rôle de serveur web) peut être supprimé après avoir suivi les étapes hello décrites ci-dessus pour l’utilisation de votre propre runtime PHP.
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a>Configurer un toouse de rôle de travail de votre propre runtime PHP
tooconfigure un toouse de rôle de travail un runtime PHP que vous fournissez, procédez comme suit :

1. Créez un projet de service Azure et ajoutez un rôle de travail PHP comme indiqué précédemment dans cette rubrique.
2. Créer un `php` dossier dans le répertoire racine de rôle de travail hello, puis ajoutez votre toohello de runtime (tous les fichiers binaires, fichiers de configuration, les sous-dossiers, etc.) PHP `php` dossier.
3. (FACULTATIF) Si le runtime PHP utilise [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], vous devez tooconfigure votre tooinstall de rôle de travail [SQL Server Native Client 2012] [ sql native client] lorsqu’il est configuré. toodo, ajouter hello [programme d’installation de sqlncli.msi x64] répertoire du rôle de travail toohello. script de démarrage Hello décrit à l’étape suivante de hello exécutera en mode silencieux le programme d’installation de hello lors de la configuration de rôle de hello. Si le runtime PHP n’utilise pas hello Microsoft Drivers for PHP pour SQL Server, vous pouvez supprimer hello ligne suivante à partir du script hello indiqué dans l’étape suivante de hello :

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. Définir une tâche de démarrage qui ajoute votre `php.exe` variable d’environnement du chemin d’accès du rôle de travail exécutable toohello lors de la configuration de rôle de hello. toodo, ouvrez hello `setup_worker.cmd` (dans le répertoire de racine du rôle de travail hello) dans un éditeur de texte et remplacez son contenu par hello script suivant :

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service toohello web root directory...
    icacls ..\ /grant "Network Service":(OI)(CI)W
    if %ERRORLEVEL% neq 0 goto error
    echo OK

    if "%EMULATED%"=="true" exit /b 0

    msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES

    setx Path "%PATH%;%~dp0php" /M

    if %ERRORLEVEL% neq 0 goto error

    echo SUCCESS
    exit /b 0

    :error

    echo FAILED
    exit /b -1
    ```
5. Ajoutez le répertoire racine de votre application fichiers tooyour du rôle de travail.
6. Publier votre application comme décrit dans hello [publier votre application](#publish-your-application) section ci-dessous.

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a>Exécutez votre application Bonjour émulateurs de calcul et de stockage
Hello émulateurs Azure fournissent un environnement local dans lequel vous pouvez tester votre application Windows Azure avant de le déployer toohello cloud. Il existe quelques différences entre les émulateurs hello et hello environnement Azure. toounderstand cela de plus, consultez [utiliser l’émulateur de stockage Azure hello pour le développement et test](storage/common/storage-use-emulator.md).

Notez que vous devez avoir PHP installé localement émulateur de calcul toouse hello. émulateur de calcul Hello utilisera votre local toorun d’installation PHP à votre application.

l’exécution de votre projet dans les émulateurs hello, toorun hello après une commande à partir du répertoire racine de votre projet :

    PS C:\MyProject> Start-AzureEmulator

Vous verrez toothis similaire de sortie :

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

Vous pouvez voir votre application en cours d’exécution dans l’émulateur de hello en ouvrant un navigateur web et en parcourant les adresses locales toohello indiqué dans la sortie de hello (`http://127.0.0.1:81` dans la sortie de l’exemple hello ci-dessus).

les émulateurs hello toostop, exécutez la commande suivante :

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a>Publication de votre application
toopublish votre application, vous devez toofirst importer vos paramètres de publication à l’aide de hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) applet de commande. Ensuite, vous pouvez publier votre application à l’aide de hello [AzureServiceProject de publication](https://msdn.microsoft.com/library/azure/dn495166.aspx) applet de commande. Pour plus d’informations sur la connexion, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).

[Azure SDK pour PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[(.csdef) de définition de service]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuration du service (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[programme d’installation de sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
