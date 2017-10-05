---
title: "Créer des rôles web et des rôles de travail Azure pour PHP | Microsoft Docs"
description: "Guide pour la création de rôles web et de travail PHP dans un service cloud Azure et pour la configuration du runtime PHP."
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
ms.openlocfilehash: 214fdcfe20f3fa4ebcbe41308404f8b7e7d15310
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-create-php-web-and-worker-roles"></a><span data-ttu-id="b6f98-103">Création de rôles web et de travail PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-103">How to create PHP web and worker roles</span></span>
## <a name="overview"></a><span data-ttu-id="b6f98-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="b6f98-104">Overview</span></span>
<span data-ttu-id="b6f98-105">Ce guide vous montre comment créer des rôles web et de travail PHP dans un environnement de développement Windows, choisir une version spécifique de PHP à partir des versions « intégrées » disponibles, modifier la configuration de PHP, activer les extensions et effectuer un déploiement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f98-105">This guide will show you how to create PHP web or worker roles in a Windows development environment, choose a specific version of PHP from the "built-in" versions available, change the PHP configuration, enable extensions, and finally, deploy to Azure.</span></span> <span data-ttu-id="b6f98-106">Il décrit également la façon de configurer un rôle web et de travail afin d'utiliser un runtime PHP (avec une configuration et des extensions personnalisées) que vous fournissez.</span><span class="sxs-lookup"><span data-stu-id="b6f98-106">It also describes how to configure a web or worker role to use a PHP runtime (with custom configuration and extensions) that you provide.</span></span>

## <a name="what-are-php-web-and-worker-roles"></a><span data-ttu-id="b6f98-107">Présentation des rôles web et de travail PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-107">What are PHP web and worker roles?</span></span>
<span data-ttu-id="b6f98-108">Azure propose trois modèles de calcul pour l’exécution d’applications : Azure App Service, Azure Virtual Machines et Azure Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="b6f98-108">Azure provides three compute models for running applications: Azure App Service, Azure Virtual Machines, and Azure Cloud Services.</span></span> <span data-ttu-id="b6f98-109">Ils prennent tous les trois en charge PHP.</span><span class="sxs-lookup"><span data-stu-id="b6f98-109">All three models support PHP.</span></span> <span data-ttu-id="b6f98-110">Cloud Services, qui inclut les rôles web et de travail, offre une *plateforme PaaS (platform as a service)*.</span><span class="sxs-lookup"><span data-stu-id="b6f98-110">Cloud Services, which includes web and worker roles, provides *platform as a service (PaaS)*.</span></span> <span data-ttu-id="b6f98-111">Dans un service cloud, un rôle web fournit un serveur web IIS (Internet Information Services) dédié pour héberger les applications web frontales.</span><span class="sxs-lookup"><span data-stu-id="b6f98-111">Within a cloud service, a web role provides a dedicated Internet Information Services (IIS) web server to host front-end web applications.</span></span> <span data-ttu-id="b6f98-112">Un rôle de travail peut exécuter des tâches asynchrones, sur le long terme ou perpétuelles, indépendamment des entrées ou des interactions de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b6f98-112">A worker role can run asynchronous, long-running or perpetual tasks independent of user interaction or input.</span></span>

<span data-ttu-id="b6f98-113">Pour plus d’informations, consultez [Calcul des options d’hébergement fournies par Azure](cloud-services/cloud-services-choose-me.md).</span><span class="sxs-lookup"><span data-stu-id="b6f98-113">For more information about these options, see [Compute hosting options provided by Azure](cloud-services/cloud-services-choose-me.md).</span></span>

## <a name="download-the-azure-sdk-for-php"></a><span data-ttu-id="b6f98-114">Téléchargement du Kit de développement logiciel (SDK) Azure pour PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-114">Download the Azure SDK for PHP</span></span>
<span data-ttu-id="b6f98-115">Le [Kit de développement logiciel (SDK) Azure pour PHP] est constitué de plusieurs composants.</span><span class="sxs-lookup"><span data-stu-id="b6f98-115">The [Azure SDK for PHP] consists of several components.</span></span> <span data-ttu-id="b6f98-116">Cet article fait référence à deux d’entre eux : Azure PowerShell et les émulateurs Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f98-116">This article will use two of them: Azure PowerShell and the Azure emulators.</span></span> <span data-ttu-id="b6f98-117">Ceux-ci peuvent être installés par le biais de Microsoft Web Platform Installer :</span><span class="sxs-lookup"><span data-stu-id="b6f98-117">These two components can be installed via the Microsoft Web Platform Installer.</span></span> <span data-ttu-id="b6f98-118">Pour plus d’informations, consultez la rubrique [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6f98-118">For more information, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="create-a-cloud-services-project"></a><span data-ttu-id="b6f98-119">Création d'un projet Cloud Services</span><span class="sxs-lookup"><span data-stu-id="b6f98-119">Create a Cloud Services project</span></span>
<span data-ttu-id="b6f98-120">La première étape de la création d’un rôle web ou de travail PHP consiste à créer un projet de service Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f98-120">The first step in creating a PHP web or worker role is to create an Azure Service project.</span></span> <span data-ttu-id="b6f98-121">Celui-ci fait office de conteneur logique pour les rôles web et de travail, et contient les fichiers de [définition de service (.csdef)] et de [configuration de service (.cscfg)] du projet.</span><span class="sxs-lookup"><span data-stu-id="b6f98-121">an Azure Service project serves as a logical container for web and worker roles, and it contains the project's [service definition (.csdef)] and [service configuration (.cscfg)] files.</span></span>

<span data-ttu-id="b6f98-122">Pour créer un projet de service Azure, exécutez Azure PowerShell en tant qu’administrateur et exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b6f98-122">To create a new Azure Service project, run Azure PowerShell as an administrator, and execute the following command:</span></span>

    PS C:\>New-AzureServiceProject myProject

<span data-ttu-id="b6f98-123">Cette commande crée un répertoire (`myProject`) dans lequel vous pouvez ajouter des rôles web et de travail.</span><span class="sxs-lookup"><span data-stu-id="b6f98-123">This command will create a new directory (`myProject`) to which you can add web and worker roles.</span></span>

## <a name="add-php-web-or-worker-roles"></a><span data-ttu-id="b6f98-124">Ajout de rôles web et de travail PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-124">Add PHP web or worker roles</span></span>
<span data-ttu-id="b6f98-125">Pour ajouter un rôle web PHP à un projet, exécutez la commande suivante à partir du répertoire racine du projet :</span><span class="sxs-lookup"><span data-stu-id="b6f98-125">To add a PHP web role to a project, run the following command from within the project's root directory:</span></span>

    PS C:\myProject> Add-AzurePHPWebRole roleName

<span data-ttu-id="b6f98-126">Pour un rôle de travail, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b6f98-126">For a worker role, use this command:</span></span>

    PS C:\myProject> Add-AzurePHPWorkerRole roleName

> [!NOTE]
> <span data-ttu-id="b6f98-127">Le paramètre `roleName` est facultatif.</span><span class="sxs-lookup"><span data-stu-id="b6f98-127">The `roleName` parameter is optional.</span></span> <span data-ttu-id="b6f98-128">S'il est omis, le nom du rôle est généré automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b6f98-128">If it is omitted, the role name will be automatically generated.</span></span> <span data-ttu-id="b6f98-129">Le premier rôle web créé est `WebRole1`, le second `WebRole2`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="b6f98-129">The first web role created will be `WebRole1`, the second will be `WebRole2`, and so on.</span></span> <span data-ttu-id="b6f98-130">Le premier rôle de travail créé est `WorkerRole1`, le second `WorkerRole2`, et ainsi de suite.</span><span class="sxs-lookup"><span data-stu-id="b6f98-130">The first worker role created will be `WorkerRole1`, the second will be `WorkerRole2`, and so on.</span></span>
>
>

## <a name="specify-the-built-in-php-version"></a><span data-ttu-id="b6f98-131">Spécification de la version intégrée de PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-131">Specify the built-in PHP version</span></span>
<span data-ttu-id="b6f98-132">Lorsque vous ajoutez un rôle Web ou de travail PHP à un projet, les fichiers de configuration du projet sont modifiés de façon à ce que PHP soit installé sur chaque instance Web ou de travail de votre application lors de son déploiement.</span><span class="sxs-lookup"><span data-stu-id="b6f98-132">When you add a PHP web or worker role to a project, the project's configuration files are modified so that PHP will be installed on each web or worker instance of your application when it is deployed.</span></span> <span data-ttu-id="b6f98-133">Pour afficher la version de PHP qui sera installée par défaut, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b6f98-133">To see the version of PHP that will be installed by default, run the following command:</span></span>

    PS C:\myProject> Get-AzureServiceProjectRoleRuntime

<span data-ttu-id="b6f98-134">Le résultat de la commande ci-dessus sera similaire à celui qui figure ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b6f98-134">The output from the command above will look similar to what is shown below.</span></span> <span data-ttu-id="b6f98-135">Dans cet exemple, l’indicateur `IsDefault` est défini sur `true` pour PHP 5.3.17, ce qui indique qu’il s’agit de la version PHP par défaut installée.</span><span class="sxs-lookup"><span data-stu-id="b6f98-135">In this example, the `IsDefault` flag is set to `true` for PHP 5.3.17, indicating that it will be the default PHP version installed.</span></span>

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

<span data-ttu-id="b6f98-136">Vous pouvez définir la version exécutable de PHP sur l'une des versions PHP qui sont répertoriées.</span><span class="sxs-lookup"><span data-stu-id="b6f98-136">You can set the PHP runtime version to any of the PHP versions that are listed.</span></span> <span data-ttu-id="b6f98-137">Par exemple, pour configurer la version de PHP (pour un rôle avec le nom `roleName`) sur 5.4.0, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b6f98-137">For example, to set the PHP version (for a role with the name `roleName`) to 5.4.0, use the following command:</span></span>

    PS C:\myProject> Set-AzureServiceProjectRole roleName php 5.4.0

> [!NOTE]
> <span data-ttu-id="b6f98-138">Les versions PHP disponibles peuvent changer à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="b6f98-138">Available PHP versions may change in the future.</span></span>
>
>

## <a name="customize-the-built-in-php-runtime"></a><span data-ttu-id="b6f98-139">Personnalisation du runtime PHP intégré</span><span class="sxs-lookup"><span data-stu-id="b6f98-139">Customize the built-in PHP runtime</span></span>
<span data-ttu-id="b6f98-140">Vous disposez d’un contrôle total sur la configuration du runtime PHP qui est installée lorsque vous suivez les étapes ci-dessus, y compris la modification des paramètres `php.ini` et l’activation des extensions.</span><span class="sxs-lookup"><span data-stu-id="b6f98-140">You have complete control over the configuration of the PHP runtime that is installed when you follow the steps above, including modification of `php.ini` settings and enabling of extensions.</span></span>

<span data-ttu-id="b6f98-141">Pour personnaliser le runtime PHP intégré, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6f98-141">To customize the built-in PHP runtime, follow these steps:</span></span>

1. <span data-ttu-id="b6f98-142">Ajoutez un nouveau dossier, intitulé `php`, dans le répertoire `bin` de votre rôle web.</span><span class="sxs-lookup"><span data-stu-id="b6f98-142">Add a new folder, named `php`, to the `bin` directory of your web role.</span></span> <span data-ttu-id="b6f98-143">Pour un rôle de travail, ajoutez-le dans le répertoire racine du rôle.</span><span class="sxs-lookup"><span data-stu-id="b6f98-143">For a worker role, add it to the role's root directory.</span></span>
2. <span data-ttu-id="b6f98-144">Dans le dossier `php`, créez un autre dossier intitulé `ext`.</span><span class="sxs-lookup"><span data-stu-id="b6f98-144">In the `php` folder, create another folder called `ext`.</span></span> <span data-ttu-id="b6f98-145">Insérez dans ce dossier tous les fichiers d’extension `.dll` (par exemple, `php_mongo.dll`) que vous voulez activer.</span><span class="sxs-lookup"><span data-stu-id="b6f98-145">Put any `.dll` extension files (e.g., `php_mongo.dll`) that you want to enable in this folder.</span></span>
3. <span data-ttu-id="b6f98-146">Ajoutez un fichier `php.ini` dans le dossier `php`.</span><span class="sxs-lookup"><span data-stu-id="b6f98-146">Add a `php.ini` file to the `php` folder.</span></span> <span data-ttu-id="b6f98-147">Activez les extensions personnalisées et définissez les directives PHP que vous voulez dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="b6f98-147">Enable any custom extensions and set any PHP directives in this file.</span></span> <span data-ttu-id="b6f98-148">Par exemple, si vous voulez activer `display_errors` et l’extension `php_mongo.dll`, le contenu de votre fichier `php.ini` se présente comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6f98-148">For example, if you wanted to turn `display_errors` on and enable the `php_mongo.dll` extension, the contents of your `php.ini` file would be as follows:</span></span>

        display_errors=On
        extension=php_mongo.dll

> [!NOTE]
> <span data-ttu-id="b6f98-149">Tout paramètre non explicitement défini dans le fichier `php.ini` que vous fournissez est automatiquement défini sur sa valeur par défaut.</span><span class="sxs-lookup"><span data-stu-id="b6f98-149">Any settings that you don't explicitly set in the `php.ini` file that you provide will automatically be set to their default values.</span></span> <span data-ttu-id="b6f98-150">Toutefois, gardez à l’esprit que vous pouvez ajouter un fichier `php.ini` complet.</span><span class="sxs-lookup"><span data-stu-id="b6f98-150">However, keep in mind that you can add a complete `php.ini` file.</span></span>
>
>

## <a name="use-your-own-php-runtime"></a><span data-ttu-id="b6f98-151">Utilisation de votre propre runtime PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-151">Use your own PHP runtime</span></span>
<span data-ttu-id="b6f98-152">Dans certains cas, au lieu de sélectionner un runtime PHP intégré et de le configurer comme indiqué ci-dessus, vous pouvez fournir votre propre runtime PHP.</span><span class="sxs-lookup"><span data-stu-id="b6f98-152">In some cases, instead of selecting a built-in PHP runtime and configuring it as described above, you may want to provide your own PHP runtime.</span></span> <span data-ttu-id="b6f98-153">Par exemple, vous pouvez utiliser le même runtime PHP dans un rôle web ou de travail que vous utilisez dans votre environnement de développement,</span><span class="sxs-lookup"><span data-stu-id="b6f98-153">For example, you can use the same PHP runtime in a web or worker role that you use in your development environment.</span></span> <span data-ttu-id="b6f98-154">ce qui permet de s’assurer que l’application ne change pas de comportement dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="b6f98-154">This makes it easier to ensure that the application will not change behavior in your production environment.</span></span>

### <a name="configure-a-web-role-to-use-your-own-php-runtime"></a><span data-ttu-id="b6f98-155">Configurer un rôle web pour utiliser votre propre runtime PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-155">Configure a web role to use your own PHP runtime</span></span>
<span data-ttu-id="b6f98-156">Pour configurer un rôle web pour utiliser un runtime PHP que vous fournissez, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6f98-156">To configure a web role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="b6f98-157">Créez un projet de service Azure et ajoutez un rôle web PHP comme indiqué précédemment dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="b6f98-157">Create an Azure Service project and add a PHP web role as described previously in this topic.</span></span>
2. <span data-ttu-id="b6f98-158">Créez un dossier `php` dans le dossier `bin` se trouvant dans le répertoire racine de votre rôle web, puis ajoutez votre runtime PHP (tous les fichiers binaires, fichiers de configuration, sous-dossiers, etc.) dans le dossier `php`.</span><span class="sxs-lookup"><span data-stu-id="b6f98-158">Create a `php` folder in the `bin` folder that is in your web role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="b6f98-159">(FACULTATIF) Si votre runtime PHP utilise les [pilotes Microsoft SQL Server pour PHP][sqlsrv drivers], vous devez configurer votre rôle web pour installer [SQL Server Native Client 2012][sql native client], une fois mis en service.</span><span class="sxs-lookup"><span data-stu-id="b6f98-159">(OPTIONAL) If your PHP runtime uses the [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your web role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="b6f98-160">Pour cela, ajoutez le [programme d’installation x64 sqlncli.msi] dans le dossier `bin` du répertoire racine de votre rôle web.</span><span class="sxs-lookup"><span data-stu-id="b6f98-160">To do this, add the [sqlncli.msi x64 installer] to the `bin` folder in your web role's root directory.</span></span> <span data-ttu-id="b6f98-161">Le script de démarrage décrit à l'étape suivante exécutera en silence le programme d'installation lorsque le rôle sera mis en service.</span><span class="sxs-lookup"><span data-stu-id="b6f98-161">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="b6f98-162">Si votre runtime PHP n'utilise pas les pilotes Microsoft SQL Server pour PHP, vous pouvez supprimer la ligne suivante dans le script figurant à l'étape suivante :</span><span class="sxs-lookup"><span data-stu-id="b6f98-162">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="b6f98-163">Définissez une tâche de démarrage configurant [Internet Information Services (IIS)][iis.net] afin d’utiliser votre runtime PHP pour gérer les demandes de pages `.php`.</span><span class="sxs-lookup"><span data-stu-id="b6f98-163">Define a startup task that configures [Internet Information Services (IIS)][iis.net] to use your PHP runtime to handle requests for `.php` pages.</span></span> <span data-ttu-id="b6f98-164">Pour cela, ouvrez le fichier `setup_web.cmd` (dans le fichier `bin` du répertoire racine de votre rôle web) dans un éditeur de texte et remplacez son contenu par le script suivant :</span><span class="sxs-lookup"><span data-stu-id="b6f98-164">To do this, open the `setup_web.cmd` file (in the `bin` file of your web role's root directory) in a text editor and replace its contents with the following script:</span></span>

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
5. <span data-ttu-id="b6f98-165">Ajoutez vos fichiers d'application dans le répertoire racine de votre rôle web.</span><span class="sxs-lookup"><span data-stu-id="b6f98-165">Add your application files to your web role's root directory.</span></span> <span data-ttu-id="b6f98-166">Il s'agira du répertoire racine du serveur web.</span><span class="sxs-lookup"><span data-stu-id="b6f98-166">This will be the web server's root directory.</span></span>
6. <span data-ttu-id="b6f98-167">Publiez votre application en procédant comme indiqué dans la section [Publication de votre application](#publish-your-application) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b6f98-167">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

> [!NOTE]
> <span data-ttu-id="b6f98-168">Il est possible de supprimer le script `download.ps1` (dans le dossier `bin` du répertoire racine du rôle web) une fois que vous avez suivi les étapes ci-dessus permettant d’utiliser votre propre runtime PHP.</span><span class="sxs-lookup"><span data-stu-id="b6f98-168">The `download.ps1` script (in the `bin` folder of the web role's root directory) can be deleted after you follow the steps described above for using your own PHP runtime.</span></span>
>
>

### <a name="configure-a-worker-role-to-use-your-own-php-runtime"></a><span data-ttu-id="b6f98-169">Configurer un rôle de travail pour utiliser votre propre runtime PHP</span><span class="sxs-lookup"><span data-stu-id="b6f98-169">Configure a worker role to use your own PHP runtime</span></span>
<span data-ttu-id="b6f98-170">Pour configurer un rôle de travail pour utiliser un runtime PHP que vous fournissez, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="b6f98-170">To configure a worker role to use a PHP runtime that you provide, follow these steps:</span></span>

1. <span data-ttu-id="b6f98-171">Créez un projet de service Azure et ajoutez un rôle de travail PHP comme indiqué précédemment dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="b6f98-171">Create an Azure Service project and add a PHP worker role as described previously in this topic.</span></span>
2. <span data-ttu-id="b6f98-172">Créez un dossier `php` dans le répertoire racine du rôle de travail, puis ajoutez votre runtime PHP (tous les fichiers binaires, fichiers de configuration, sous-dossiers, etc.) dans le dossier `php`.</span><span class="sxs-lookup"><span data-stu-id="b6f98-172">Create a `php` folder in the worker role's root directory, and then add your PHP runtime (all binaries, configuration files, subfolders, etc.) to the `php` folder.</span></span>
3. <span data-ttu-id="b6f98-173">(FACULTATIF) Si votre runtime PHP utilise les [pilotes Microsoft SQL Server pour PHP][sqlsrv drivers], une fois le rôle de travail mis en service, il vous faudra le configurer pour installer [SQL Server Native Client 2012][sql native client].</span><span class="sxs-lookup"><span data-stu-id="b6f98-173">(OPTIONAL) If your PHP runtime uses [Microsoft Drivers for PHP for SQL Server][sqlsrv drivers], you will need to configure your worker role to install [SQL Server Native Client 2012][sql native client] when it is provisioned.</span></span> <span data-ttu-id="b6f98-174">Pour cela, ajoutez le [programme d’installation x64 sqlncli.msi] dans le répertoire racine du rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="b6f98-174">To do this, add the [sqlncli.msi x64 installer] to the worker role's root directory.</span></span> <span data-ttu-id="b6f98-175">Le script de démarrage décrit à l'étape suivante exécutera en silence le programme d'installation lorsque le rôle sera mis en service.</span><span class="sxs-lookup"><span data-stu-id="b6f98-175">The startup script described in the next step will silently run the installer when the role is provisioned.</span></span> <span data-ttu-id="b6f98-176">Si votre runtime PHP n'utilise pas les pilotes Microsoft SQL Server pour PHP, vous pouvez supprimer la ligne suivante dans le script figurant à l'étape suivante :</span><span class="sxs-lookup"><span data-stu-id="b6f98-176">If your PHP runtime does not use the Microsoft Drivers for PHP for SQL Server, you can remove the following line from the script shown in the next step:</span></span>

        msiexec /i sqlncli.msi /qn IACCEPTSQLNCLILICENSETERMS=YES
4. <span data-ttu-id="b6f98-177">Définissez une tâche de démarrage ajoutant votre exécutable `php.exe` à l’environnement PATH du rôle de travail une fois ce dernier mis en service.</span><span class="sxs-lookup"><span data-stu-id="b6f98-177">Define a startup task that adds your `php.exe` executable to the worker role's PATH environment variable when the role is provisioned.</span></span> <span data-ttu-id="b6f98-178">Pour cela, ouvrez le fichier `setup_worker.cmd` (dans le répertoire racine de votre rôle de travail) dans un éditeur de texte et remplacez son contenu par le script suivant :</span><span class="sxs-lookup"><span data-stu-id="b6f98-178">To do this, open the `setup_worker.cmd` file (in the worker role's root directory) in a text editor and replace its contents with the following script:</span></span>

    ```cmd
    @echo on

    cd "%~dp0"

    echo Granting permissions for Network Service to the web root directory...
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
5. <span data-ttu-id="b6f98-179">Ajoutez vos fichiers d'application dans le répertoire racine de votre rôle de travail.</span><span class="sxs-lookup"><span data-stu-id="b6f98-179">Add your application files to your worker role's root directory.</span></span>
6. <span data-ttu-id="b6f98-180">Publiez votre application en procédant comme indiqué dans la section [Publication de votre application](#publish-your-application) ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="b6f98-180">Publish your application as described in the [Publish your application](#publish-your-application) section below.</span></span>

## <a name="run-your-application-in-the-compute-and-storage-emulators"></a><span data-ttu-id="b6f98-181">Exécuter votre application dans les émulateurs de calcul et de stockage</span><span class="sxs-lookup"><span data-stu-id="b6f98-181">Run your application in the compute and storage emulators</span></span>
<span data-ttu-id="b6f98-182">Les émulateurs Azure fournissent un environnement local dans lequel vous pouvez tester votre application Azure avant de la déployer sur le cloud.</span><span class="sxs-lookup"><span data-stu-id="b6f98-182">The Azure emulators provide a local environment in which you can test your Azure application before you deploy it to the cloud.</span></span> <span data-ttu-id="b6f98-183">Il y a quelques différences entre les émulateurs et l'environnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b6f98-183">There are some differences between the emulators and the Azure environment.</span></span> <span data-ttu-id="b6f98-184">Pour mieux comprendre cela, consultez [Utilisation de l’émulateur de stockage Azure pour le développement et le test](storage/common/storage-use-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="b6f98-184">To understand this better, see [Use the Azure storage emulator for development and testing](storage/common/storage-use-emulator.md).</span></span>

<span data-ttu-id="b6f98-185">Notez que PHP doit être installé en local pour pouvoir utiliser l’émulateur de calcul.</span><span class="sxs-lookup"><span data-stu-id="b6f98-185">Note that you must have PHP installed locally to use the compute emulator.</span></span> <span data-ttu-id="b6f98-186">Ce dernier utilise votre installation locale de PHP pour exécuter votre application.</span><span class="sxs-lookup"><span data-stu-id="b6f98-186">The compute emulator will use your local PHP installation to run your application.</span></span>

<span data-ttu-id="b6f98-187">Pour exécuter votre projet dans les émulateurs, exécutez la commande suivante à partir du répertoire racine de votre projet :</span><span class="sxs-lookup"><span data-stu-id="b6f98-187">To run your project in the emulators, execute the following command from your project's root directory:</span></span>

    PS C:\MyProject> Start-AzureEmulator

<span data-ttu-id="b6f98-188">Vous verrez une sortie semblable à ceci :</span><span class="sxs-lookup"><span data-stu-id="b6f98-188">You will see output similar to this:</span></span>

    Creating local package...
    Starting Emulator...
    Role is running at http://127.0.0.1:81
    Started

<span data-ttu-id="b6f98-189">Pour voir votre application exécutée dans l’émulateur, ouvrez un navigateur web et accédez à l’adresse locale illustrée dans le résultat (`http://127.0.0.1:81` dans l’exemple ci-dessus).</span><span class="sxs-lookup"><span data-stu-id="b6f98-189">You can see your application running in the emulator by opening a web browser and browsing to the local address shown in the output (`http://127.0.0.1:81` in the example output above).</span></span>

<span data-ttu-id="b6f98-190">Pour arrêter les émulateurs, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b6f98-190">To stop the emulators, execute this command:</span></span>

    PS C:\MyProject> Stop-AzureEmulator

## <a name="publish-your-application"></a><span data-ttu-id="b6f98-191">Publication de votre application</span><span class="sxs-lookup"><span data-stu-id="b6f98-191">Publish your application</span></span>
<span data-ttu-id="b6f98-192">Pour publier votre application, vous devez d’abord importer vos paramètres de publication en utilisant l’applet de commande [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b6f98-192">To publish your application, you need to first import your publish settings by using the [Import-AzurePublishSettingsFile](https://msdn.microsoft.com/library/azure/dn790370.aspx) cmdlet.</span></span> <span data-ttu-id="b6f98-193">Vous pouvez ensuite publier votre application à l’aide de l’applet de commande [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) .</span><span class="sxs-lookup"><span data-stu-id="b6f98-193">Then you can publish your application by using the [Publish-AzureServiceProject](https://msdn.microsoft.com/library/azure/dn495166.aspx) cmdlet.</span></span> <span data-ttu-id="b6f98-194">Pour plus d’informations sur la connexion, consultez [Installation et configuration d’Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="b6f98-194">For information about signing in, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6f98-195">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6f98-195">Next steps</span></span>
<span data-ttu-id="b6f98-196">Pour plus d’informations, consultez le [Centre pour développeurs PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="b6f98-196">For more information, see the [PHP Developer Center](/develop/php/).</span></span>

[Kit de développement logiciel (SDK) Azure pour PHP]: /develop/php/common-tasks/download-php-sdk/
[install ps and emulators]: http://go.microsoft.com/fwlink/p/?linkid=320376&clcid=0x409
[définition de service (.csdef)]: http://msdn.microsoft.com/library/windowsazure/ee758711.aspx
[configuration de service (.cscfg)]: http://msdn.microsoft.com/library/windowsazure/ee758710.aspx
[iis.net]: http://www.iis.net/
[sql native client]: http://msdn.microsoft.com/sqlserver/aa937733.aspx
[sqlsrv drivers]: http://php.net/sqlsrv
[programme d’installation x64 sqlncli.msi]: http://go.microsoft.com/fwlink/?LinkID=239648
