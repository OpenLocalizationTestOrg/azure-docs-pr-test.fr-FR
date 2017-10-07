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
# <a name="how-toocreate-php-web-and-worker-roles"></a><span data-ttu-id="2307b-103">Comment toocreate PHP rôles de travail</span><span class="sxs-lookup"><span data-stu-id="2307b-103">How toocreate PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="2307b-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="2307b-104">Overview</span></span>
<span data-ttu-id="2307b-105">Ce guide vous montrera comment toocreate PHP web ou travail rôles dans un environnement de développement Windows, choisissez une version spécifique de PHP hello « intégrées » versions disponibles, modifier la configuration de PHP hello, activer les extensions d’et enfin, déployer tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2307b-105">This guide will show you how toocreate PHP web or worker roles in a Windows development environment, choose a specific version of PHP from hello "built-in" versions available, change hello PHP configuration, enable extensions, and finally, deploy tooAzure.</span></span> <span data-ttu-id="2307b-106">Elle décrit également comment tooconfigure un rôle web ou travail toouse un runtime PHP (avec la configuration personnalisée et extensions) que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="2307b-106">It also describes how tooconfigure a web or worker role toouse a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="2307b-107">Présentation des rôles web et de travail PHP</span><span class="sxs-lookup"><span data-stu-id="2307b-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="2307b-108">Azure propose trois modèles de calcul pour l’exécution d’applications : Azure App Service, Azure Virtual Machines et Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="2307b-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="2307b-109">Ils prennent tous les trois en charge PHP.</span><span class="sxs-lookup"><span data-stu-id="2307b-109">All three models support PHP.</span></span> <span data-ttu-id="2307b-110">Cloud Services, qui inclut les rôles web et de travail, offre une *plateforme PaaS (platform as a service)*.</span><span class="sxs-lookup"><span data-stu-id="2307b-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="2307b-111">Dans un service cloud, un rôle web fournit un serveur web Internet Information Services (IIS) dédié serveur toohost d’applications web frontal.</span><span class="sxs-lookup"><span data-stu-id="2307b-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server toohost front-end web applications.</span></span> <span data-ttu-id="2307b-112">Un rôle de travail peut exécuter des tâches asynchrones, sur le long terme ou perpétuelles, indépendamment des entrées ou des interactions de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="2307b-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="2307b-113">Pour plus d’informations, consultez [Calcul des options d’hébergement fournies par Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="2307b-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-hello-azure-sdk-for-php"></a><span data-ttu-id="2307b-114">Télécharger hello Azure SDK pour PHP</span><span class="sxs-lookup"><span data-stu-id="2307b-114">Download hello Azure SDK for PHP</span></span>
<span data-ttu-id="2307b-115">Hello [Azure SDK pour PHP] se compose de plusieurs composants.</span><span class="sxs-lookup"><span data-stu-id="2307b-115">hello [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="2307b-116">Cet article utilise deux d'entre eux : Azure PowerShell et hello émulateurs Azure.</span><span class="sxs-lookup"><span data-stu-id="2307b-116">This article will use two of them: Azure PowerShell and hello Azure emulators.</span></span> <span data-ttu-id="2307b-117">Ces deux composants peuvent être installés via hello Microsoft Web Platform Installer.</span><span class="sxs-lookup"><span data-stu-id="2307b-117">These two components can be installed via hello Microsoft Web Platform Installer.</span></span> <span data-ttu-id="2307b-118">Pour plus d’informations, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2307b-118">For more information, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="2307b-119">Création d'un projet Cloud Services</span><span class="sxs-lookup"><span data-stu-id="2307b-119">Create a Cloud Services project</span></span>
<span data-ttu-id="2307b-120">Hello première étape de création d’un rôle web ou de travail PHP est toocreate un projet de Service Azure.</span><span class="sxs-lookup"><span data-stu-id="2307b-120">hello first step in creating a PHP web or worker role is toocreate an Azure Service project.</span></span> <span data-ttu-id="2307b-121">un projet de Service Azure sert comme un conteneur logique pour les rôles web et de travail, et il contient du projet hello [(.csdef) de définition de service] et [configuration du service (.cscfg)] fichiers.</span><span class="sxs-lookup"><span data-stu-id="2307b-121">an Azure Service project serves as a logical container for web and worker roles, and it contains hello project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="2307b-122">toocreate un nouveau projet de Service Azure, exécutez Azure PowerShell en tant qu’administrateur et exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2307b-122">toocreate a new Azure Service project, run Azure PowerShell as an administrator, and execute hello following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="2307b-123">Cette commande crée un nouveau répertoire (`myProject`) toowhich, vous pouvez ajouter des rôles web et worker.</span><span class="sxs-lookup"><span data-stu-id="2307b-123">This command will create a new directory (`myProject`) toowhich you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="2307b-124">Ajout de rôles web et de travail PHP</span><span class="sxs-lookup"><span data-stu-id="2307b-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="2307b-125">tooadd un projet tooa PHP de rôle web, exécutez hello commande à partir de dans le répertoire racine du projet hello suivante :</span><span class="sxs-lookup"><span data-stu-id="2307b-125">tooadd a PHP web role tooa project, run hello following command from within hello project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="2307b-126">Pour un rôle de travail, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2307b-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="2307b-127">Hello `roleName` paramètre est facultatif.</span><span class="sxs-lookup"><span data-stu-id="2307b-127">hello `roleName` parameter is optional.</span></span> <span data-ttu-id="2307b-128">S’il est omis, le nom de rôle hello sera généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="2307b-128">If it is omitted, hello role name will be automatically generated.</span></span> <span data-ttu-id="2307b-129">créé le rôle web premier Hello sera `WebRole1`, hello second sera `WebRole2`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="2307b-129">hello first web role created will be `WebRole1`, hello second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="2307b-130">premier rôle de travail Hello créé sera `WorkerRole1`, hello second sera `WorkerRole2`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="2307b-130">hello first worker role created will be `WorkerRole1`, hello second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-hello-built-in-php-version"></a><span data-ttu-id="2307b-131">Spécifiez la version PHP hello intégrée</span><span class="sxs-lookup"><span data-stu-id="2307b-131">Specify hello built-in PHP version</span></span>
<span data-ttu-id="2307b-132">Lorsque vous ajoutez un projet de tooa de rôle web ou de travail PHP, les fichiers de configuration du projet hello sont modifiées afin que PHP est installé sur chaque instance du web ou de travail de votre application lorsqu’elle est déployée.</span><span class="sxs-lookup"><span data-stu-id="2307b-132">When you add a PHP web or worker role tooa project, hello project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="2307b-133">version de hello toosee de PHP est installé par défaut, exécutez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2307b-133">toosee hello version of PHP that will be installed by default, run hello following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="2307b-134">Hello sortie à partir de la commande hello ci-dessus ressemble toowhat est indiqué ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2307b-134">hello output from hello command above will look similar toowhat is shown below.</span></span> <span data-ttu-id="2307b-135">Dans cet exemple, hello `IsDefault` est défini trop`true` pour PHP 5.3.17, indiquant qu’il sera la version PHP par défaut hello installée.</span><span class="sxs-lookup"><span data-stu-id="2307b-135">In this example, hello `IsDefault` flag is set too`true` for PHP 5.3.17, indicating that it will be hello default PHP version installed.</span></span>

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

<span data-ttu-id="2307b-136">Vous pouvez définir hello PHP runtime version tooany des versions PHP hello répertoriés.</span><span class="sxs-lookup"><span data-stu-id="2307b-136">You can set hello PHP runtime version tooany of hello PHP versions that are listed.</span></span> <span data-ttu-id="2307b-137">Par exemple, la version tooset hello PHP (pour un rôle avec le nom de hello `roleName`) too5.4.0, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2307b-137">For example, tooset hello PHP version (for a role with hello name `roleName`) too5.4.0, use hello following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="2307b-138">Les versions PHP disponibles peuvent changer Bonjour futures.</span><span class="sxs-lookup"><span data-stu-id="2307b-138">Available PHP versions may change in hello future.</span></span>
>
>

## <a name="customize-hello-built-in-php-runtime"></a><span data-ttu-id="2307b-139">Personnaliser le runtime PHP intégré de hello</span><span class="sxs-lookup"><span data-stu-id="2307b-139">Customize hello built-in PHP runtime</span></span>
<span data-ttu-id="2307b-140">Vous avez un contrôle complet sur la configuration de hello du runtime PHP hello qui est installé lorsque vous suivez les étapes de hello ci-dessus, y compris la modification de `php.ini` paramètres et l’activation des extensions.</span><span class="sxs-lookup"><span data-stu-id="2307b-140">You have complete control over hello configuration of hello PHP runtime that is installed when you follow hello steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="2307b-141">toocustomize hello intégré runtime PHP, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2307b-141">toocustomize hello built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="2307b-142">Ajouter un nouveau dossier, nommé `php`, toohello `bin` répertoire de votre rôle web.</span><span class="sxs-lookup"><span data-stu-id="2307b-142">Add a new folder, named `php`, toohello `bin` directory of your web role.</span></span> <span data-ttu-id="2307b-143">Pour un rôle de travail, ajoutez-le répertoire du rôle toohello.</span><span class="sxs-lookup"><span data-stu-id="2307b-143">For a worker role, add it toohello role's root directory.</span></span>
2. <span data-ttu-id="2307b-144">Bonjour `php` dossier, créez un autre dossier appelé `ext`.</span><span class="sxs-lookup"><span data-stu-id="2307b-144">In hello `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="2307b-145">Placez aucune `.dll` des fichiers d’extension (par exemple, `php_mongo.dll`) que vous souhaitez tooenable dans ce dossier.</span><span class="sxs-lookup"><span data-stu-id="2307b-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want tooenable in this folder.</span></span>
3. <span data-ttu-id="2307b-146">Ajouter un `php.ini` fichier toohello `php` dossier.</span><span class="sxs-lookup"><span data-stu-id="2307b-146">Add a `php.ini` file toohello `php` folder.</span></span> <span data-ttu-id="2307b-147">Activez les extensions personnalisées et définissez les directives PHP que vous voulez dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="2307b-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="2307b-148">Par exemple, si vous souhaitiez tooturn `display_errors` sur et activer hello `php_mongo.dll` extension, le contenu de hello de votre `php.ini` fichier serait comme suit :</span><span class="sxs-lookup"><span data-stu-id="2307b-148">For example, if you wanted tooturn `display_errors` on and enable hello `php_mongo.dll` extension, hello contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="2307b-149">Tous les paramètres que vous ne définissez pas explicitement Bonjour `php.ini` fichier que vous fournissez automatiquement va être définie tootheir les valeurs par défaut.</span><span class="sxs-lookup"><span data-stu-id="2307b-149">Any settings that you don't explicitly set in hello `php.ini` file that you provide will automatically be set tootheir default values.</span></span> <span data-ttu-id="2307b-150">Toutefois, gardez à l’esprit que vous pouvez ajouter un fichier `php.ini` complet.</span><span class="sxs-lookup"><span data-stu-id="2307b-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="2307b-151">Utilisation de votre propre runtime PHP</span><span class="sxs-lookup"><span data-stu-id="2307b-151">Use your own PHP runtime</span></span>
<span data-ttu-id="2307b-152">Dans certains cas, au lieu de la sélection d’un runtime PHP intégré et le configurer comme décrit ci-dessus, vous souhaiterez tooprovide votre propre runtime PHP.</span><span class="sxs-lookup"><span data-stu-id="2307b-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want tooprovide your own PHP runtime.</span></span> <span data-ttu-id="2307b-153">Par exemple, vous pouvez utiliser hello même runtime PHP dans un rôle web ou de travail que vous utilisez dans votre environnement de développement.</span><span class="sxs-lookup"><span data-stu-id="2307b-153">For example, you can use hello same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="2307b-154">Il est ainsi plus facile tooensure qu’application hello ne changera pas de comportement dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="2307b-154">This makes it easier tooensure that hello application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-toouse-your-own-php-runtime"></a><span data-ttu-id="2307b-155">Configurer un toouse de rôle web de votre propre runtime PHP</span><span class="sxs-lookup"><span data-stu-id="2307b-155">Configure a web role toouse your own PHP runtime</span></span>
<span data-ttu-id="2307b-156">tooconfigure un toouse de rôle web un runtime PHP que vous fournissez, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2307b-156">tooconfigure a web role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="2307b-157">Créez un projet de service Azure et ajoutez un rôle web PHP comme indiqué précédemment dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="2307b-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="2307b-158">Créer un `php` dossier Bonjour `bin` dossier qui est dans le répertoire racine de votre rôle de serveur web, puis ajoutez votre toohello de runtime (tous les fichiers binaires, fichiers de configuration, les sous-dossiers, etc.) PHP `php` dossier.</span><span class="sxs-lookup"><span data-stu-id="2307b-158">Create a `php` folder in hello `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="2307b-159">(FACULTATIF) Si le runtime PHP utilise hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], vous devez tooconfigure votre tooinstall de rôle web [SQL Server Native Client 2012] [ sql native client] lorsqu’il est configuré.</span><span class="sxs-lookup"><span data-stu-id="2307b-159">(OPTIONAL) If your PHP runtime uses hello [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your web role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="2307b-160">toodo, ajouter hello [programme d’installation de sqlncli.msi x64] toohello `bin` dossier dans le répertoire racine de votre rôle de serveur web.</span><span class="sxs-lookup"><span data-stu-id="2307b-160">toodo this, add hello [sqlncli.msi x64 installer] toohello `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="2307b-161">script de démarrage Hello décrit à l’étape suivante de hello exécutera en mode silencieux le programme d’installation de hello lors de la configuration de rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="2307b-161">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="2307b-162">Si le runtime PHP n’utilise pas hello Microsoft Drivers for PHP pour SQL Server, vous pouvez supprimer hello ligne suivante à partir du script hello indiqué dans l’étape suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="2307b-162">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="2307b-163">Définir une tâche de démarrage qui configure [Internet Information Services (IIS)] [ iis.net] toouse les demandes concernant votre toohandle du runtime PHP `.php` pages.</span><span class="sxs-lookup"><span data-stu-id="2307b-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] toouse your PHP runtime toohandle requests for `.php` pages.</span></span> <span data-ttu-id="2307b-164">toodo, ouvrez hello `setup_web.cmd` fichier (Bonjour `bin` fichier du répertoire racine de votre rôle de serveur web) dans un éditeur de texte et la remplacer son contenu avec hello suite de script :</span><span class="sxs-lookup"><span data-stu-id="2307b-164">toodo this, open hello `setup_web.cmd` file (in hello `bin` file of your web role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="2307b-165">Ajoutez le répertoire racine de l’application fichiers tooyour web de votre rôle.</span><span class="sxs-lookup"><span data-stu-id="2307b-165">Add your application files tooyour web role's root directory.</span></span> <span data-ttu-id="2307b-166">Ce sera le répertoire racine du serveur hello web.</span><span class="sxs-lookup"><span data-stu-id="2307b-166">This will be hello web server's root directory.</span></span>
6. <span data-ttu-id="2307b-167">Publier votre application comme décrit dans hello [publier votre application](#publish-your-application) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2307b-167">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="2307b-168">Hello `download.ps1` script (Bonjour `bin` dossier du répertoire racine de hello rôle de serveur web) peut être supprimé après avoir suivi les étapes hello décrites ci-dessus pour l’utilisation de votre propre runtime PHP.</span><span class="sxs-lookup"><span data-stu-id="2307b-168">hello `download.ps1` script (in hello `bin` folder of hello web role's root directory) can be deleted after you follow hello steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-toouse-your-own-php-runtime"></a><span data-ttu-id="2307b-169">Configurer un toouse de rôle de travail de votre propre runtime PHP</span><span class="sxs-lookup"><span data-stu-id="2307b-169">Configure a worker role toouse your own PHP runtime</span></span>
<span data-ttu-id="2307b-170">tooconfigure un toouse de rôle de travail un runtime PHP que vous fournissez, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="2307b-170">tooconfigure a worker role toouse a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="2307b-171">Créez un projet de service Azure et ajoutez un rôle de travail PHP comme indiqué précédemment dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="2307b-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="2307b-172">Créer un `php` dossier dans le répertoire racine de rôle de travail hello, puis ajoutez votre toohello de runtime (tous les fichiers binaires, fichiers de configuration, les sous-dossiers, etc.) PHP `php` dossier.</span><span class="sxs-lookup"><span data-stu-id="2307b-172">Create a `php` folder in hello worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) toohello `php` folder.</span></span>
3. <span data-ttu-id="2307b-173">(FACULTATIF) Si le runtime PHP utilise [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], vous devez tooconfigure votre tooinstall de rôle de travail [SQL Server Native Client 2012] [ sql native client] lorsqu’il est configuré.</span><span class="sxs-lookup"><span data-stu-id="2307b-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need tooconfigure your worker role tooinstall [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="2307b-174">toodo, ajouter hello [programme d’installation de sqlncli.msi x64] répertoire du rôle de travail toohello.</span><span class="sxs-lookup"><span data-stu-id="2307b-174">toodo this, add hello [sqlncli.msi x64 installer] toohello worker role's root directory.</span></span> <span data-ttu-id="2307b-175">script de démarrage Hello décrit à l’étape suivante de hello exécutera en mode silencieux le programme d’installation de hello lors de la configuration de rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="2307b-175">hello startup script described in hello next step will silently run hello installer when hello role is provisioned.</span></span> <span data-ttu-id="2307b-176">Si le runtime PHP n’utilise pas hello Microsoft Drivers for PHP pour SQL Server, vous pouvez supprimer hello ligne suivante à partir du script hello indiqué dans l’étape suivante de hello :</span><span class="sxs-lookup"><span data-stu-id="2307b-176">If your PHP runtime does not use hello Microsoft Drivers for PHP for SQL Server, you can remove hello following line from hello script shown in hello next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="2307b-177">Définir une tâche de démarrage qui ajoute votre `php.exe` variable d’environnement du chemin d’accès du rôle de travail exécutable toohello lors de la configuration de rôle de hello.</span><span class="sxs-lookup"><span data-stu-id="2307b-177">Define a startup task that adds your `php.exe` executable toohello worker role's PATH environment variable when hello role is provisioned.</span></span> <span data-ttu-id="2307b-178">toodo, ouvrez hello `setup_worker.cmd` (dans le répertoire de racine du rôle de travail hello) dans un éditeur de texte et remplacez son contenu par hello script suivant :</span><span class="sxs-lookup"><span data-stu-id="2307b-178">toodo this, open hello `setup_worker.cmd` file (in hello worker role's root directory) in a text editor and replace its contents with hello following script:</span></span>

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
5. <span data-ttu-id="2307b-179">Ajoutez le répertoire racine de votre application fichiers tooyour du rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="2307b-179">Add your application files tooyour worker role's root directory.</span></span>
6. <span data-ttu-id="2307b-180">Publier votre application comme décrit dans hello [publier votre application](#publish-your-application) section ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="2307b-180">Publish your application as described in hello [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-hello-compute-and-storage-emulators"></a><span data-ttu-id="2307b-181">Exécutez votre application Bonjour émulateurs de calcul et de stockage</span><span class="sxs-lookup"><span data-stu-id="2307b-181">Run your application in hello compute and storage emulators</span></span>
<span data-ttu-id="2307b-182">Hello émulateurs Azure fournissent un environnement local dans lequel vous pouvez tester votre application Windows Azure avant de le déployer toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="2307b-182">hello Azure emulators provide a local environment in which you can test your Azure application before you deploy it toohello cloud.</span></span> <span data-ttu-id="2307b-183">Il existe quelques différences entre les émulateurs hello et hello environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="2307b-183">There are some differences between hello emulators and hello Azure environment.</span></span> <span data-ttu-id="2307b-184">toounderstand cela de plus, consultez [utiliser l’émulateur de stockage Azure hello pour le développement et test](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="2307b-184">toounderstand this better, see [Use hello Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="2307b-185">Notez que vous devez avoir PHP installé localement émulateur de calcul toouse hello.</span><span class="sxs-lookup"><span data-stu-id="2307b-185">Note that you must have PHP installed locally toouse hello compute emulator.</span></span> <span data-ttu-id="2307b-186">émulateur de calcul Hello utilisera votre local toorun d’installation PHP à votre application.</span><span class="sxs-lookup"><span data-stu-id="2307b-186">hello compute emulator will use your local PHP installation toorun your application.</span></span>

<span data-ttu-id="2307b-187">l’exécution de votre projet dans les émulateurs hello, toorun hello après une commande à partir du répertoire racine de votre projet :</span><span class="sxs-lookup"><span data-stu-id="2307b-187">toorun your project in hello emulators, execute hello following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="2307b-188">Vous verrez toothis similaire de sortie :</span><span class="sxs-lookup"><span data-stu-id="2307b-188">You will see output similar toothis:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="2307b-189">Vous pouvez voir votre application en cours d’exécution dans l’émulateur de hello en ouvrant un navigateur web et en parcourant les adresses locales toohello indiqué dans la sortie de hello (`http://127.0.0.1:81` dans la sortie de l’exemple hello ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="2307b-189">You can see your application running in hello emulator by opening a web browser and browsing toohello local address shown in hello output (`http://127.0.0.1:81` in hello example output above).</span></span>

<span data-ttu-id="2307b-190">les émulateurs hello toostop, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2307b-190">toostop hello emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="2307b-191">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="2307b-191">Publish your application</span></span>
<span data-ttu-id="2307b-192">toopublish votre application, vous devez toofirst importer vos paramètres de publication à l’aide de hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="2307b-192">toopublish your application, you need toofirst import your publish settings by using hello [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="2307b-193">Ensuite, vous pouvez publier votre application à l’aide de hello [AzureServiceProject de publication](https://msdn.microsoft.com/library/azure/dn495166.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="2307b-193">Then you can publish your application by using hello [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="2307b-194">Pour plus d’informations sur la connexion, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2307b-194">For information about signing in, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2307b-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2307b-195">Next steps</span></span>
<span data-ttu-id="2307b-196">Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="2307b-196">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

[Azure SDK pour PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[(.csdef) de définition de service]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuration du service (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[programme d’installation de sqlncli.msi x64]: http://go.microsoft.com/fwlink/?LinkID=239648
