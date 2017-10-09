---
title: aaaConfigure PHP dans Azure App Service Web Apps | Documents Microsoft
description: "Découvrez comment tooconfigure hello installation de PHP par défaut ou ajouter une installation de PHP personnalisée pour les applications Web dans Azure App Service."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a><span data-ttu-id="9a744-103">Configurer PHP dans Azure App Service Web Apps</span><span class="sxs-lookup"><span data-stu-id="9a744-103">Configure PHP in Azure App Service Web Apps</span></span>
## <a name="introduction"></a><span data-ttu-id="9a744-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="9a744-104">Introduction</span></span>
<span data-ttu-id="9a744-105">Ce guide vous explique comment tooconfigure hello intégré runtime PHP pour les applications Web dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), fournir un runtime PHP personnalisé et activer les extensions.</span><span class="sxs-lookup"><span data-stu-id="9a744-105">This guide will show you how tooconfigure hello built-in PHP runtime for Web Apps in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), provide a custom PHP runtime, and enable extensions.</span></span> <span data-ttu-id="9a744-106">toouse du Service d’applications, inscrivez-vous hello [version d’évaluation gratuite].</span><span class="sxs-lookup"><span data-stu-id="9a744-106">toouse App Service, sign up for hello [free trial].</span></span> <span data-ttu-id="9a744-107">tooget hello plus à partir de ce guide, vous devez d’abord créer une application web PHP dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="9a744-107">tooget hello most from this guide, you should first create a PHP web app in App Service.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a><span data-ttu-id="9a744-108">Comment : modifier hello intégrés PHP la version</span><span class="sxs-lookup"><span data-stu-id="9a744-108">How to: Change hello built-in PHP version</span></span>
<span data-ttu-id="9a744-109">Par défaut, PHP 5.5 est installé et immédiatement utilisable lorsque vous créez une application web App Service.</span><span class="sxs-lookup"><span data-stu-id="9a744-109">By default, PHP 5.5 is installed and immediately available for use when you create an App Service web app.</span></span> <span data-ttu-id="9a744-110">Hello la meilleure façon toosee hello version disponible révision sa configuration par défaut, et extensions activées hello est toodeploy un script qui appelle hello [phpinfo()] (fonction).</span><span class="sxs-lookup"><span data-stu-id="9a744-110">hello best way toosee hello available release revision, its default configuration, and hello enabled extensions is toodeploy a script that calls hello [phpinfo()] function.</span></span>

<span data-ttu-id="9a744-111">Les versions PHP 5.6 et PHP 7.0 sont également disponibles, mais ne sont pas activées par défaut.</span><span class="sxs-lookup"><span data-stu-id="9a744-111">PHP 5.6 and PHP 7.0 versions are also available, but not enabled by default.</span></span> <span data-ttu-id="9a744-112">tooupdate hello version de PHP, suivez une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="9a744-112">tooupdate hello PHP version, follow one of these methods:</span></span>

### <a name="azure-portal"></a><span data-ttu-id="9a744-113">Portail Azure</span><span class="sxs-lookup"><span data-stu-id="9a744-113">Azure Portal</span></span>
1. <span data-ttu-id="9a744-114">Parcourir l’application web tooyour hello [Azure Portal](https://portal.azure.com) , puis cliquez sur hello **paramètres** bouton.</span><span class="sxs-lookup"><span data-stu-id="9a744-114">Browse tooyour web app in hello [Azure Portal](https://portal.azure.com) and click on hello **Settings** button.</span></span>
   
    ![Paramètres d’application web][settings-button]
2. <span data-ttu-id="9a744-116">À partir de hello **paramètres** panneau sélectionner **paramètres de l’Application** et choisissez la nouvelle version PHP hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-116">From hello **Settings** blade select **Application Settings** and choose hello new PHP version.</span></span>
   
    ![Paramètres de l’application][application-settings]
3. <span data-ttu-id="9a744-118">Cliquez sur hello **enregistrer** bouton haut hello hello **paramètres de l’application Web** panneau.</span><span class="sxs-lookup"><span data-stu-id="9a744-118">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Enregistrer les paramètres de configuration][save-button]

### <a name="azure-powershell-windows"></a><span data-ttu-id="9a744-120">Azure PowerShell (Windows)</span><span class="sxs-lookup"><span data-stu-id="9a744-120">Azure PowerShell (Windows)</span></span>
1. <span data-ttu-id="9a744-121">Ouvrez Azure PowerShell et compte de connexion tooyour :</span><span class="sxs-lookup"><span data-stu-id="9a744-121">Open Azure PowerShell, and login tooyour account:</span></span>
   
        PS C:\> Login-AzureRmAccount
2. <span data-ttu-id="9a744-122">Définir la version PHP hello pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-122">Set hello PHP version for hello web app.</span></span>
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. <span data-ttu-id="9a744-123">version de PHP Hello est maintenant définie.</span><span class="sxs-lookup"><span data-stu-id="9a744-123">hello PHP version is now set.</span></span> <span data-ttu-id="9a744-124">Vous pouvez confirmer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="9a744-124">You can confirm these settings:</span></span>
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a><span data-ttu-id="9a744-125">Interface en ligne de commande Azure (Linux, Mac et Windows)</span><span class="sxs-lookup"><span data-stu-id="9a744-125">Azure Command-Line Interface (Linux, Mac, Windows)</span></span>
<span data-ttu-id="9a744-126">toouse hello Interface de ligne de commande Azure, vous devez avoir **Node.js** installé sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="9a744-126">toouse hello Azure Command-Line Interface, you must have **Node.js** installed on your computer.</span></span>

1. <span data-ttu-id="9a744-127">Ouvrez Terminal Server et compte de connexion tooyour.</span><span class="sxs-lookup"><span data-stu-id="9a744-127">Open Terminal, and login tooyour account.</span></span>
   
        azure login
2. <span data-ttu-id="9a744-128">Définir la version PHP hello pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-128">Set hello PHP version for hello web app.</span></span>
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. <span data-ttu-id="9a744-129">version de PHP Hello est maintenant définie.</span><span class="sxs-lookup"><span data-stu-id="9a744-129">hello PHP version is now set.</span></span> <span data-ttu-id="9a744-130">Vous pouvez confirmer les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="9a744-130">You can confirm these settings:</span></span>
   
        azure site show {app-name}

> [!NOTE] 
> <span data-ttu-id="9a744-131">Hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commandes équivalente toohello ci-dessus sont :</span><span class="sxs-lookup"><span data-stu-id="9a744-131">hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commands that are equivalent toohello above are:</span></span>
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a><span data-ttu-id="9a744-132">Comment : modifier les configurations de PHP hello intégrées</span><span class="sxs-lookup"><span data-stu-id="9a744-132">How to: Change hello built-in PHP configurations</span></span>
<span data-ttu-id="9a744-133">Pour n’importe quel runtime PHP intégré, vous pouvez modifier les options de configuration hello en suivant les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9a744-133">For any built-in PHP runtime, you can change any of hello configuration options by following hello steps below.</span></span> <span data-ttu-id="9a744-134">(Pour plus d’informations sur les directives de php.ini, consultez la page [Liste des directives du php.ini].)</span><span class="sxs-lookup"><span data-stu-id="9a744-134">(For information about php.ini directives, see [List of php.ini directives].)</span></span>

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a><span data-ttu-id="9a744-135">Modification des paramètres de configuration PHP\_INI\_USER, PHP\_INI\_PERDIR et PHP\_INI\_ALL</span><span class="sxs-lookup"><span data-stu-id="9a744-135">Changing PHP\_INI\_USER, PHP\_INI\_PERDIR, PHP\_INI\_ALL configuration settings</span></span>
1. <span data-ttu-id="9a744-136">Ajouter un [. user.ini] tooyour répertoire racine des fichiers.</span><span class="sxs-lookup"><span data-stu-id="9a744-136">Add a [.user.ini] file tooyour root directory.</span></span>
2. <span data-ttu-id="9a744-137">Ajouter des toohello des paramètres de configuration `.user.ini` à l’aide du fichier hello la même syntaxe que vous utiliseriez dans un `php.ini` fichier.</span><span class="sxs-lookup"><span data-stu-id="9a744-137">Add configuration settings toohello `.user.ini` file using hello same syntax you would use in a `php.ini` file.</span></span> <span data-ttu-id="9a744-138">Par exemple, si vous souhaitiez tooturn hello `display_errors` paramètre et définissez `upload_max_filesize` définition too10M, votre `.user.ini` fichier contient ce texte :</span><span class="sxs-lookup"><span data-stu-id="9a744-138">For example, if you wanted tooturn hello `display_errors` setting on and set `upload_max_filesize` setting too10M, your `.user.ini` file would contain this text:</span></span>
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. <span data-ttu-id="9a744-139">Déployez votre application web.</span><span class="sxs-lookup"><span data-stu-id="9a744-139">Deploy your web app.</span></span>
4. <span data-ttu-id="9a744-140">Redémarrage de l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-140">Restart hello web app.</span></span> <span data-ttu-id="9a744-141">(Le redémarrage est nécessaire, car la fréquence de hello avec quels PHP lit `.user.ini` fichiers est régie par hello `user_ini.cache_ttl` paramètre, qui est un paramètre de niveau système et 300 secondes (5 minutes) par défaut.</span><span class="sxs-lookup"><span data-stu-id="9a744-141">(Restarting is necessary because hello frequency with which PHP reads `.user.ini` files is governed by hello `user_ini.cache_ttl` setting, which is a system level setting and is 300 seconds (5 minutes) by default.</span></span> <span data-ttu-id="9a744-142">Redémarrer l’application web hello force tooread hello nouveau les paramètres PHP dans hello `.user.ini` fichier.)</span><span class="sxs-lookup"><span data-stu-id="9a744-142">Restarting hello web app forces PHP tooread hello new settings in hello `.user.ini` file.)</span></span>

<span data-ttu-id="9a744-143">En tant qu’un autre toousing un `.user.ini` fichier, vous pouvez utiliser hello [ini_set()] fonction scripts tooset options de configuration qui ne sont pas les directives au niveau du système.</span><span class="sxs-lookup"><span data-stu-id="9a744-143">As an alternative toousing a `.user.ini` file, you can use hello [ini_set()] function in scripts tooset configuration options that are not system-level directives.</span></span>

### <a name="changing-phpinisystem-configuration-settings"></a><span data-ttu-id="9a744-144">Modification des paramètres de configuration PHP\_INI\_SYSTEM</span><span class="sxs-lookup"><span data-stu-id="9a744-144">Changing PHP\_INI\_SYSTEM configuration settings</span></span>
1. <span data-ttu-id="9a744-145">Ajouter une application Web de tooyour paramètre d’application avec la clé de hello `PHP_INI_SCAN_DIR` et la valeur`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="9a744-145">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
2. <span data-ttu-id="9a744-146">Créer un `settings.ini` de fichiers à l’aide de la Console de Kudu (http://&lt;-nom du site&gt;. scm.azurewebsite.net) Bonjour `d:\home\site\ini` active.</span><span class="sxs-lookup"><span data-stu-id="9a744-146">Create an `settings.ini` file using Kudu Console (http://&lt;site-name&gt;.scm.azurewebsite.net) in hello `d:\home\site\ini` directory.</span></span>
3. <span data-ttu-id="9a744-147">Ajouter des toohello des paramètres de configuration `settings.ini` à l’aide du fichier hello la même syntaxe que dans un fichier php.ini.</span><span class="sxs-lookup"><span data-stu-id="9a744-147">Add configuration settings toohello `settings.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="9a744-148">Par exemple, si vous souhaitiez toopoint hello `curl.cainfo` définition tooa `*.crt` de fichiers et de définir 'wincache.maxfilesize' paramètre too512K, votre `settings.ini` fichier contient ce texte :</span><span class="sxs-lookup"><span data-stu-id="9a744-148">For example, if you wanted toopoint hello `curl.cainfo` setting tooa `*.crt` file and set 'wincache.maxfilesize' setting too512K, your `settings.ini` file would contain this text:</span></span>
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. <span data-ttu-id="9a744-149">Redémarrez vos modifications de hello tooload application Web.</span><span class="sxs-lookup"><span data-stu-id="9a744-149">Restart your Web App tooload hello changes.</span></span>

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a><span data-ttu-id="9a744-150">Comment : activer les extensions dans hello par défaut du runtime PHP</span><span class="sxs-lookup"><span data-stu-id="9a744-150">How to: Enable extensions in hello default PHP runtime</span></span>
<span data-ttu-id="9a744-151">Comme indiqué dans la section précédente de hello, version PHP de hello meilleure manière toosee hello par défaut, sa configuration par défaut et hello activé extensions est toodeploy un script qui appelle [phpinfo()].</span><span class="sxs-lookup"><span data-stu-id="9a744-151">As noted in hello previous section, hello best way toosee hello default PHP version, its default configuration, and hello enabled extensions is toodeploy a script that calls [phpinfo()].</span></span> <span data-ttu-id="9a744-152">tooenable des extensions supplémentaires, suivez les étapes de hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="9a744-152">tooenable additional extensions, follow hello steps below:</span></span>

### <a name="configure-via-ini-settings"></a><span data-ttu-id="9a744-153">Configuration par des paramètres ini</span><span class="sxs-lookup"><span data-stu-id="9a744-153">Configure via ini settings</span></span>
1. <span data-ttu-id="9a744-154">Ajouter un `ext` Active toohello `d:\home\site` active.</span><span class="sxs-lookup"><span data-stu-id="9a744-154">Add a `ext` directory toohello `d:\home\site` directory.</span></span>
2. <span data-ttu-id="9a744-155">Put `.dll` des fichiers d’extension Bonjour `ext` répertoire (par exemple, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="9a744-155">Put `.dll` extension files in hello `ext` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="9a744-156">Assurez-vous que les extensions de hello sont compatibles avec la version par défaut de PHP et sont VC9 et est non thread-safe (nts) compatible.</span><span class="sxs-lookup"><span data-stu-id="9a744-156">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="9a744-157">Ajouter une application Web de tooyour paramètre d’application avec la clé de hello `PHP_INI_SCAN_DIR` et la valeur`d:\home\site\ini`</span><span class="sxs-lookup"><span data-stu-id="9a744-157">Add an App Setting tooyour Web App with hello key `PHP_INI_SCAN_DIR` and value `d:\home\site\ini`</span></span>
4. <span data-ttu-id="9a744-158">Dans `d:\home\site\ini`, créez un fichier `ini` appelé `extensions.ini`.</span><span class="sxs-lookup"><span data-stu-id="9a744-158">Create an `ini` file in `d:\home\site\ini` called `extensions.ini`.</span></span>
5. <span data-ttu-id="9a744-159">Ajouter des toohello des paramètres de configuration `extensions.ini` à l’aide du fichier hello la même syntaxe que dans un fichier php.ini.</span><span class="sxs-lookup"><span data-stu-id="9a744-159">Add configuration settings toohello `extensions.ini` file using hello same syntax you would use in a php.ini file.</span></span> <span data-ttu-id="9a744-160">Par exemple, si vous souhaitiez tooenable hello MongoDB et XDebug les extensions, votre `extensions.ini` fichier contient ce texte :</span><span class="sxs-lookup"><span data-stu-id="9a744-160">For example, if you wanted tooenable hello MongoDB and XDebug extensions, your `extensions.ini` file would contain this text:</span></span>
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. <span data-ttu-id="9a744-161">Redémarrez vos modifications de hello tooload application Web.</span><span class="sxs-lookup"><span data-stu-id="9a744-161">Restart your Web App tooload hello changes.</span></span>

### <a name="configure-via-app-setting"></a><span data-ttu-id="9a744-162">Configuration par un paramètre d’application</span><span class="sxs-lookup"><span data-stu-id="9a744-162">Configure via App Setting</span></span>
1. <span data-ttu-id="9a744-163">Ajouter un `bin` répertoire racine de toohello active.</span><span class="sxs-lookup"><span data-stu-id="9a744-163">Add a `bin` directory toohello root directory.</span></span>
2. <span data-ttu-id="9a744-164">Put `.dll` des fichiers d’extension Bonjour `bin` répertoire (par exemple, `php_xdebug.dll`).</span><span class="sxs-lookup"><span data-stu-id="9a744-164">Put `.dll` extension files in hello `bin` directory (for example, `php_xdebug.dll`).</span></span> <span data-ttu-id="9a744-165">Assurez-vous que les extensions de hello sont compatibles avec la version par défaut de PHP et sont VC9 et est non thread-safe (nts) compatible.</span><span class="sxs-lookup"><span data-stu-id="9a744-165">Make sure that hello extensions are compatible with default version of PHP and are VC9 and non-thread-safe (nts) compatible.</span></span>
3. <span data-ttu-id="9a744-166">Déployez votre application web.</span><span class="sxs-lookup"><span data-stu-id="9a744-166">Deploy your web app.</span></span>
4. <span data-ttu-id="9a744-167">Parcourir l’application web tooyour hello portail Azure, puis cliquez sur hello **paramètres** bouton.</span><span class="sxs-lookup"><span data-stu-id="9a744-167">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Paramètres d’application web][settings-button]
5. <span data-ttu-id="9a744-169">À partir de hello **paramètres** panneau sélectionner **paramètres de l’Application** et faites défiler toohello **paramètres de l’application** section.</span><span class="sxs-lookup"><span data-stu-id="9a744-169">From hello **Settings** blade select **Application Settings** and scroll toohello **App settings** section.</span></span>
6. <span data-ttu-id="9a744-170">Bonjour **paramètres de l’application** en créant un **PHP_EXTENSIONS** clé.</span><span class="sxs-lookup"><span data-stu-id="9a744-170">In hello **App settings** section, create a **PHP_EXTENSIONS** key.</span></span> <span data-ttu-id="9a744-171">valeur Hello pour cette clé serait une racine du chemin relatif toowebsite : **bin\your-ext-fichier**.</span><span class="sxs-lookup"><span data-stu-id="9a744-171">hello value for this key would be a path relative toowebsite root: **bin\your-ext-file**.</span></span>
   
    ![Activer une extension dans les paramètres d'application][php-extensions]
7. <span data-ttu-id="9a744-173">Cliquez sur hello **enregistrer** bouton haut hello hello **paramètres de l’application Web** panneau.</span><span class="sxs-lookup"><span data-stu-id="9a744-173">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Enregistrer les paramètres de configuration][save-button]

<span data-ttu-id="9a744-175">Les extensions Zend sont également prises en charge à l’aide d’une clé **PHP_ZENDEXTENSIONS**.</span><span class="sxs-lookup"><span data-stu-id="9a744-175">Zend extensions are also supported by using a **PHP_ZENDEXTENSIONS** key.</span></span> <span data-ttu-id="9a744-176">tooenable plusieurs extensions, inclure une liste séparée par des virgules de `.dll` fichiers pour la valeur du paramètre d’application hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-176">tooenable multiple extensions, include a comma-separated list of `.dll` files for hello app setting value.</span></span>

## <a name="how-to-use-a-custom-php-runtime"></a><span data-ttu-id="9a744-177">Utilisation d’un runtime PHP personnalisé</span><span class="sxs-lookup"><span data-stu-id="9a744-177">How to: Use a custom PHP runtime</span></span>
<span data-ttu-id="9a744-178">Au lieu de l’exécution PHP par défaut hello, application de Service Web Apps permet un runtime PHP, vous devez fournir tooexecute scripts PHP.</span><span class="sxs-lookup"><span data-stu-id="9a744-178">Instead of hello default PHP runtime, App Service Web Apps can use a PHP runtime that you provide tooexecute PHP scripts.</span></span> <span data-ttu-id="9a744-179">Hello runtime que vous fournissez peut être configuré par un `php.ini` fichier que vous fournissez également.</span><span class="sxs-lookup"><span data-stu-id="9a744-179">hello runtime that you provide can be configured by a `php.ini` file that you also provide.</span></span> <span data-ttu-id="9a744-180">toouse un runtime PHP personnalisé avec des applications Web, suivez les étapes de hello ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="9a744-180">toouse a custom PHP runtime with Web Apps, follow hello steps below.</span></span>

1. <span data-ttu-id="9a744-181">Obtenez une version de PHP pour Windows, compatible avec NTS (Non-Thread-Safe), VC9 ou VC11.</span><span class="sxs-lookup"><span data-stu-id="9a744-181">Obtain a non-thread-safe, VC9 or VC11 compatible version of PHP for Windows.</span></span> <span data-ttu-id="9a744-182">Les versions récentes de PHP pour Windows sont disponibles à l’adresse suivante : [http://windows.php.net/download/].</span><span class="sxs-lookup"><span data-stu-id="9a744-182">Recent releases of PHP for Windows can be found here: [http://windows.php.net/download/].</span></span> <span data-ttu-id="9a744-183">Les versions plus anciennes sont accessibles dans l’archive hello ici : [http://windows.php.net/downloads/releases/archives/].</span><span class="sxs-lookup"><span data-stu-id="9a744-183">Older releases can be found in hello archive here: [http://windows.php.net/downloads/releases/archives/].</span></span>
2. <span data-ttu-id="9a744-184">Modifier hello `php.ini` fichier pour le runtime.</span><span class="sxs-lookup"><span data-stu-id="9a744-184">Modify hello `php.ini` file for your runtime.</span></span> <span data-ttu-id="9a744-185">Notez que tout paramètre de configuration correspondant à une directive de niveau système uniquement est ignoré par Web Apps.</span><span class="sxs-lookup"><span data-stu-id="9a744-185">Note that any configuration settings that are system-level-only directives will be ignored by Web Apps.</span></span> <span data-ttu-id="9a744-186">Pour plus d'informations sur les directives de niveau système uniquement, consultez la page [Liste des directives du php.ini].</span><span class="sxs-lookup"><span data-stu-id="9a744-186">(For information about system-level-only directives, see [List of php.ini directives]).</span></span>
3. <span data-ttu-id="9a744-187">Si vous le souhaitez, ajoutez des extensions tooyour PHP runtime et les activer dans hello `php.ini` fichier.</span><span class="sxs-lookup"><span data-stu-id="9a744-187">Optionally, add extensions tooyour PHP runtime and enable them in hello `php.ini` file.</span></span>
4. <span data-ttu-id="9a744-188">Ajouter un `bin` répertoire tooyour racine répertoire et put hello qui contient votre runtime PHP qu’il contient (par exemple, `bin\php`).</span><span class="sxs-lookup"><span data-stu-id="9a744-188">Add a `bin` directory tooyour root directory, and put hello directory that contains your PHP runtime in it (for example, `bin\php`).</span></span>
5. <span data-ttu-id="9a744-189">Déployez votre application web.</span><span class="sxs-lookup"><span data-stu-id="9a744-189">Deploy your web app.</span></span>
6. <span data-ttu-id="9a744-190">Parcourir l’application web tooyour hello portail Azure, puis cliquez sur hello **paramètres** bouton.</span><span class="sxs-lookup"><span data-stu-id="9a744-190">Browse tooyour web app in hello Azure Portal and click on hello **Settings** button.</span></span>
   
    ![Paramètres d’application web][settings-button]
7. <span data-ttu-id="9a744-192">À partir de hello **paramètres** panneau sélectionner **paramètres de l’Application** et faites défiler toohello **mappages de gestionnaires** section.</span><span class="sxs-lookup"><span data-stu-id="9a744-192">From hello **Settings** blade select **Application Settings** and scroll toohello **Handler mappings** section.</span></span> <span data-ttu-id="9a744-193">Ajouter `*.php` toohello Extension de champ et ajouter hello chemin d’accès toohello `php-cgi.exe` exécutable.</span><span class="sxs-lookup"><span data-stu-id="9a744-193">Add `*.php` toohello Extension field and add hello path toohello `php-cgi.exe` executable.</span></span> <span data-ttu-id="9a744-194">Si vous placez votre runtime PHP dans hello `bin` répertoire racine hello de votre application, chemin d’accès de hello sera `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span><span class="sxs-lookup"><span data-stu-id="9a744-194">If you put your PHP runtime in hello `bin` directory in hello root of you application, hello path will be `D:\home\site\wwwroot\bin\php\php-cgi.exe`.</span></span>
   
    ![Indiquer le gestionnaire dans les mappages][handler-mappings]
8. <span data-ttu-id="9a744-196">Cliquez sur hello **enregistrer** bouton haut hello hello **paramètres de l’application Web** panneau.</span><span class="sxs-lookup"><span data-stu-id="9a744-196">Click hello **Save** button at hello top of hello **Web app settings** blade.</span></span>
   
    ![Enregistrer les paramètres de configuration][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a><span data-ttu-id="9a744-198">Activation de l’automatisation du Compositeur dans Azure</span><span class="sxs-lookup"><span data-stu-id="9a744-198">How to: Enable Composer automation in Azure</span></span>
<span data-ttu-id="9a744-199">Par défaut, App Service ne fait rien avec composer.json, si vous en avez un dans votre projet PHP.</span><span class="sxs-lookup"><span data-stu-id="9a744-199">By default, App Service doesn't do anything with composer.json, if you have one in your PHP project.</span></span> <span data-ttu-id="9a744-200">Si vous utilisez [déploiement Git](app-service-deploy-local-git.md), vous pouvez activer composer.json du traitement au cours `git push` par activation de l’extension de Composer hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-200">If you use [Git deployment](app-service-deploy-local-git.md), you can enable composer.json processing during `git push` by enabling hello Composer extension.</span></span>

> [!NOTE]
> <span data-ttu-id="9a744-201">Vous pouvez [voter pour la prise en charge haut de gamme de Compositeur dans App Service ici](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span><span class="sxs-lookup"><span data-stu-id="9a744-201">You can [vote for first-class Composer support in App Service here](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!</span></span>
> 
> 

1. <span data-ttu-id="9a744-202">Dans votre PHP web lame l’application hello [portail Azure](https://portal.azure.com), cliquez sur **outils** > **Extensions**.</span><span class="sxs-lookup"><span data-stu-id="9a744-202">In your PHP web app's blade in hello [Azure portal](https://portal.azure.com), click **Tools** > **Extensions**.</span></span>
   
    ![Azure Portal Paramètres Panneau tooenable automation Composer dans Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. <span data-ttu-id="9a744-204">Cliquez sur **Ajouter** puis sur **Compositeur**.</span><span class="sxs-lookup"><span data-stu-id="9a744-204">Click **Add**, then click **Composer**.</span></span>
   
    ![Ajouter l’automation de Composer Composer extension tooenable dans Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. <span data-ttu-id="9a744-206">Cliquez sur **OK** tooaccept les conditions juridiques.</span><span class="sxs-lookup"><span data-stu-id="9a744-206">Click **OK** tooaccept legal terms.</span></span> <span data-ttu-id="9a744-207">Cliquez sur **OK** à nouveau les extension tooadd hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-207">Click **OK** again tooadd hello extension.</span></span>
   
    <span data-ttu-id="9a744-208">Hello **extensions installées** panneau affiche désormais les extensions de Composer hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-208">hello **Installed extensions** blade will now show hello Composer extension.</span></span>  
    <span data-ttu-id="9a744-209">![Accepter l’automation de Composer tooenable juridiques dans Azure](./media/web-sites-php-configure/composer-extension-view.png)</span><span class="sxs-lookup"><span data-stu-id="9a744-209">![Accept legal terms tooenable Composer automation in Azure](./media/web-sites-php-configure/composer-extension-view.png)</span></span>
4. <span data-ttu-id="9a744-210">À présent, effectuer `git add`, `git commit`, et `git push` comme dans la section précédente de hello.</span><span class="sxs-lookup"><span data-stu-id="9a744-210">Now, perform `git add`, `git commit`, and `git push` like in hello previous section.</span></span> <span data-ttu-id="9a744-211">Vous verrez alors que Compositeur installe des interdépendances définies dans composer.json.</span><span class="sxs-lookup"><span data-stu-id="9a744-211">You'll now see that Composer is installing dependencies defined in composer.json.</span></span>
   
    ![Déploiement Git avec automatisation du Compositeur dans Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a><span data-ttu-id="9a744-213">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9a744-213">Next steps</span></span>
<span data-ttu-id="9a744-214">Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="9a744-214">For more information, see hello [PHP Developer Center](/develop/php/).</span></span>

> [!NOTE]
> <span data-ttu-id="9a744-215">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="9a744-215">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="9a744-216">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="9a744-216">No credit cards required; no commitments.</span></span>
> 
> 

[version d’évaluation gratuite]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[Liste des directives du php.ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

