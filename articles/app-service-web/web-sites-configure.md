---
title: aaaConfigure les applications web dans Azure App Service
description: "Comment tooconfigure une application web dans les Services d’application Azure"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a><span data-ttu-id="3685e-103">Configurer des applications web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="3685e-103">Configure web apps in Azure App Service</span></span>
<span data-ttu-id="3685e-104">Cette rubrique explique comment une application web à l’aide de tooconfigure hello [Azure Portal].</span><span class="sxs-lookup"><span data-stu-id="3685e-104">This topic explains how tooconfigure a web app using hello [Azure Portal].</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a><span data-ttu-id="3685e-105">Paramètres de l’application</span><span class="sxs-lookup"><span data-stu-id="3685e-105">Application settings</span></span>
1. <span data-ttu-id="3685e-106">Bonjour [Azure Portal], ouvrez Panneau hello pour l’application web de hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-106">In hello [Azure Portal], open hello blade for hello web app.</span></span>
2. <span data-ttu-id="3685e-107">Cliquez sur **Tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="3685e-107">Click **All Settings**.</span></span>
3. <span data-ttu-id="3685e-108">Cliquez sur **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="3685e-108">Click **Application Settings**.</span></span>

![Paramètres de l’application][configure01]

<span data-ttu-id="3685e-110">Hello **paramètres de l’Application** panneau a regroupées sous plusieurs catégories de paramètres.</span><span class="sxs-lookup"><span data-stu-id="3685e-110">hello **Application settings** blade has settings grouped under several categories.</span></span>

### <a name="general-settings"></a><span data-ttu-id="3685e-111">Paramètres généraux :</span><span class="sxs-lookup"><span data-stu-id="3685e-111">General settings</span></span>
<span data-ttu-id="3685e-112">**Versions d'infrastructure**.</span><span class="sxs-lookup"><span data-stu-id="3685e-112">**Framework versions**.</span></span> <span data-ttu-id="3685e-113">Définissez ces options si votre application utilise l'une de ces infrastructures :</span><span class="sxs-lookup"><span data-stu-id="3685e-113">Set these options if your app uses any these frameworks:</span></span> 

* <span data-ttu-id="3685e-114">**.NET framework**: version du .NET framework ensemble hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-114">**.NET Framework**: Set hello .NET framework version.</span></span> 
* <span data-ttu-id="3685e-115">**PHP**: définir la version PHP hello, ou **OFF** toodisable PHP.</span><span class="sxs-lookup"><span data-stu-id="3685e-115">**PHP**: Set hello PHP version, or **OFF** toodisable PHP.</span></span> 
* <span data-ttu-id="3685e-116">**Java**: une version Java hello Select ou **OFF** toodisable Java.</span><span class="sxs-lookup"><span data-stu-id="3685e-116">**Java**: Select hello Java version or **OFF** toodisable Java.</span></span> <span data-ttu-id="3685e-117">Hello d’utilisation **Web conteneur** toochoose option entre les versions de Tomcat et Jetty.</span><span class="sxs-lookup"><span data-stu-id="3685e-117">Use hello **Web Container** option toochoose between Tomcat and Jetty versions.</span></span>
* <span data-ttu-id="3685e-118">**Python**: version de Python hello Select, ou **OFF** toodisable Python.</span><span class="sxs-lookup"><span data-stu-id="3685e-118">**Python**: Select hello Python version, or **OFF** toodisable Python.</span></span>

<span data-ttu-id="3685e-119">Pour des raisons techniques, l’activation de Java pour votre application désactive les options .NET, PHP et Python hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-119">For technical reasons, enabling Java for your app disables hello .NET, PHP, and Python options.</span></span>

<span data-ttu-id="3685e-120"><a name="platform"></a>
**Plateforme**.</span><span class="sxs-lookup"><span data-stu-id="3685e-120"><a name="platform"></a>
**Platform**.</span></span> <span data-ttu-id="3685e-121">Indique si votre application web s’exécute dans un environnement 32 bits ou 64 bits.</span><span class="sxs-lookup"><span data-stu-id="3685e-121">Selects whether your web app runs in a 32-bit or 64-bit environment.</span></span> <span data-ttu-id="3685e-122">environnement de Hello 64 bits requiert le mode de base ou Standard.</span><span class="sxs-lookup"><span data-stu-id="3685e-122">hello 64-bit environment requires Basic or Standard mode.</span></span> <span data-ttu-id="3685e-123">Les modes Gratuit et Partagé s'exécutent uniquement dans un environnement 32 bits.</span><span class="sxs-lookup"><span data-stu-id="3685e-123">Free and Shared modes always run in a 32-bit environment.</span></span>

<span data-ttu-id="3685e-124">**Web Sockets**.</span><span class="sxs-lookup"><span data-stu-id="3685e-124">**Web Sockets**.</span></span> <span data-ttu-id="3685e-125">Définissez **ON** tooenable hello protocole WebSocket ; par exemple, si votre application web utilise [ASP.NET SignalR] ou [socket.io].</span><span class="sxs-lookup"><span data-stu-id="3685e-125">Set **ON** tooenable hello WebSocket protocol; for example, if your web app uses [ASP.NET SignalR] or [socket.io].</span></span>

<span data-ttu-id="3685e-126"><a name="alwayson"></a>
**Toujours actif**.</span><span class="sxs-lookup"><span data-stu-id="3685e-126"><a name="alwayson"></a>
**Always On**.</span></span> <span data-ttu-id="3685e-127">Par défaut, les applications web sont déchargées si elles sont inactives pendant un certain temps.</span><span class="sxs-lookup"><span data-stu-id="3685e-127">By default, web apps are unloaded if they are idle for some period of time.</span></span> <span data-ttu-id="3685e-128">Cela permet de préserver les ressources système de hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-128">This lets hello system conserve resources.</span></span> <span data-ttu-id="3685e-129">En mode de base ou Standard, vous pouvez activer **Always On** tookeep hello application chargée de tout temps hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-129">In Basic or Standard mode, you can enable **Always On** tookeep hello app loaded all hello time.</span></span> <span data-ttu-id="3685e-130">Si votre application exécute des tâches Web continues ou s’exécute les tâches Web déclenchées à l’aide d’une expression CRON, vous devez activer **Always On**, ou les tâches web de hello peut ne pas fonctionner de manière fiable.</span><span class="sxs-lookup"><span data-stu-id="3685e-130">If your app runs continuous WebJobs or runs WebJobs triggered using a CRON expression, you should enable **Always On**, or hello web jobs may not run reliably.</span></span>

<span data-ttu-id="3685e-131">**Version de pipeline gérée**.</span><span class="sxs-lookup"><span data-stu-id="3685e-131">**Managed Pipeline Version**.</span></span> <span data-ttu-id="3685e-132">Jeux de hello IIS [mode pipeline].</span><span class="sxs-lookup"><span data-stu-id="3685e-132">Sets hello IIS [pipeline mode].</span></span> <span data-ttu-id="3685e-133">Laissez ce paramètre défini tooIntegrated (valeur par défaut de hello) sauf si vous avez une application héritée qui requiert une version antérieure de IIS.</span><span class="sxs-lookup"><span data-stu-id="3685e-133">Leave this set tooIntegrated (hello default) unless you have a legacy app that requires an older version of IIS.</span></span>

<span data-ttu-id="3685e-134">**Basculement automatique**.</span><span class="sxs-lookup"><span data-stu-id="3685e-134">**Auto Swap**.</span></span> <span data-ttu-id="3685e-135">Si vous activez l’échange automatique pour un emplacement de déploiement, du Service d’applications échangera automatiquement l’application hello web en production lorsque vous appuyez sur un emplacement de toothat de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="3685e-135">If you enable Auto Swap for a deployment slot, App Service will automatically swap hello web app into production when you push an update toothat slot.</span></span> <span data-ttu-id="3685e-136">Pour plus d’informations, consultez [déployer toostaging les emplacements pour les applications web dans Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="3685e-136">For more information, see [Deploy toostaging slots for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span>

### <a name="debugging"></a><span data-ttu-id="3685e-137">Débogage</span><span class="sxs-lookup"><span data-stu-id="3685e-137">Debugging</span></span>
<span data-ttu-id="3685e-138">**Débogage à distance**.</span><span class="sxs-lookup"><span data-stu-id="3685e-138">**Remote Debugging**.</span></span> <span data-ttu-id="3685e-139">Active le débogage distant.</span><span class="sxs-lookup"><span data-stu-id="3685e-139">Enables remote debugging.</span></span> <span data-ttu-id="3685e-140">Lorsque activé, vous pouvez utiliser le débogueur distant de hello dans Visual Studio tooconnect directement tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="3685e-140">When enabled, you can use hello remote debugger in Visual Studio tooconnect directly tooyour web app.</span></span> <span data-ttu-id="3685e-141">Le débogage à distance reste activé pendant 48 heures.</span><span class="sxs-lookup"><span data-stu-id="3685e-141">Remote debugging will remain enabled for 48 hours.</span></span> 

### <a name="app-settings"></a><span data-ttu-id="3685e-142">Paramètres de l'application</span><span class="sxs-lookup"><span data-stu-id="3685e-142">App settings</span></span>
<span data-ttu-id="3685e-143">Cette section contient des paires nom/valeur qui seront chargées par votre application web au démarrage.</span><span class="sxs-lookup"><span data-stu-id="3685e-143">This section contains name/value pairs that you web app will load on start up.</span></span> 

* <span data-ttu-id="3685e-144">Dans le cas des applications .NET, ces paramètres sont inclus dans les `AppSettings` de votre configuration .NET au moment de l’exécution, en remplacement des paramètres existants.</span><span class="sxs-lookup"><span data-stu-id="3685e-144">For .NET apps, these settings are injected into your .NET configuration `AppSettings` at runtime, overriding existing settings.</span></span> 
* <span data-ttu-id="3685e-145">Les applications PHP, Python, Java et Node peuvent accéder à ces paramètres sous forme de variables d'environnement au moment de l'exécution.</span><span class="sxs-lookup"><span data-stu-id="3685e-145">PHP, Python, Java and Node applications can access these settings as environment variables at runtime.</span></span> <span data-ttu-id="3685e-146">Pour chaque paramètre d’application, les deux variables d’environnement sont créés ; un nom hello spécifié par l’entrée de paramètre d’application hello et l’autre avec un préfixe de APPSETTING_.</span><span class="sxs-lookup"><span data-stu-id="3685e-146">For each app setting, two environment variables are created; one with hello name specified by hello app setting entry, and another with a prefix of APPSETTING_.</span></span> <span data-ttu-id="3685e-147">Tous les deux contenir hello même valeur.</span><span class="sxs-lookup"><span data-stu-id="3685e-147">Both contain hello same value.</span></span>

### <a name="connection-strings"></a><span data-ttu-id="3685e-148">Chaînes de connexion</span><span class="sxs-lookup"><span data-stu-id="3685e-148">Connection strings</span></span>
<span data-ttu-id="3685e-149">Chaînes de connexion des ressources liées.</span><span class="sxs-lookup"><span data-stu-id="3685e-149">Connection strings for linked resources.</span></span> 

<span data-ttu-id="3685e-150">Pour les applications .NET, ces chaînes de connexion sont injectées dans votre configuration .NET `connectionStrings` paramètres lors de l’exécution, qui remplaceront les entrées existantes dont la clé de hello est hello nom de la base de données liée.</span><span class="sxs-lookup"><span data-stu-id="3685e-150">For .NET apps, these connection strings are injected into your .NET configuration `connectionStrings` settings at runtime, overriding existing entries where hello key equals hello linked database name.</span></span> 

<span data-ttu-id="3685e-151">Pour les applications PHP, Python, Java et de nœud, ces paramètres seront disponibles en tant que variables d’environnement lors de l’exécution, le préfixe avec le type de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-151">For PHP, Python, Java and Node applications, these settings will be available as environment variables at runtime, prefixed with hello connection type.</span></span> <span data-ttu-id="3685e-152">préfixes Hello de variable d’environnement sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="3685e-152">hello environment variable prefixes are as follows:</span></span> 

* <span data-ttu-id="3685e-153">SQL Server : `SQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3685e-153">SQL Server: `SQLCONNSTR_`</span></span>
* <span data-ttu-id="3685e-154">MySQL : `MYSQLCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3685e-154">MySQL: `MYSQLCONNSTR_`</span></span>
* <span data-ttu-id="3685e-155">Base de données SQL : `SQLAZURECONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3685e-155">SQL Database: `SQLAZURECONNSTR_`</span></span>
* <span data-ttu-id="3685e-156">Personnalisé : `CUSTOMCONNSTR_`</span><span class="sxs-lookup"><span data-stu-id="3685e-156">Custom: `CUSTOMCONNSTR_`</span></span>

<span data-ttu-id="3685e-157">Par exemple, si une chaîne de connexion MySql ont été nommée `connectionstring1`, il est accessible via la variable d’environnement hello `MYSQLCONNSTR_connectionString1`.</span><span class="sxs-lookup"><span data-stu-id="3685e-157">For example, if a MySql connection string were named `connectionstring1`, it would be accessed through hello environment variable `MYSQLCONNSTR_connectionString1`.</span></span>

### <a name="default-documents"></a><span data-ttu-id="3685e-158">Documents par défaut</span><span class="sxs-lookup"><span data-stu-id="3685e-158">Default documents</span></span>
<span data-ttu-id="3685e-159">document par défaut de Hello est hello web page qui s’affiche à l’URL racine de hello pour un site Web.</span><span class="sxs-lookup"><span data-stu-id="3685e-159">hello default document is hello web page that is displayed at hello root URL for a website.</span></span>  <span data-ttu-id="3685e-160">premier fichier correspondant Hello dans la liste de hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="3685e-160">hello first matching file in hello list is used.</span></span> 

<span data-ttu-id="3685e-161">Les applications web peuvent utiliser des modules qui effectuent un routage en fonction de l’URL, au lieu de proposer du contenu statique. Dans ce cas, il n’existe pas de document par défaut.</span><span class="sxs-lookup"><span data-stu-id="3685e-161">Web apps might use modules that route based on URL, rather than serving static content, in which case there is no default document as such.</span></span>    

### <a name="handler-mappings"></a><span data-ttu-id="3685e-162">Mappages de gestionnaires</span><span class="sxs-lookup"><span data-stu-id="3685e-162">Handler mappings</span></span>
<span data-ttu-id="3685e-163">Utiliser cette toohandle des processeurs zone tooadd script personnalisé requêtes pour les extensions de fichier spécifiques.</span><span class="sxs-lookup"><span data-stu-id="3685e-163">Use this area tooadd custom script processors toohandle requests for specific file extensions.</span></span> 

* <span data-ttu-id="3685e-164">**Extension**.</span><span class="sxs-lookup"><span data-stu-id="3685e-164">**Extension**.</span></span> <span data-ttu-id="3685e-165">Hello fichier extension toobe géré, telles que *.php ou handler.fcgi.</span><span class="sxs-lookup"><span data-stu-id="3685e-165">hello file extension toobe handled, such as *.php or handler.fcgi.</span></span> 
* <span data-ttu-id="3685e-166">**Chemin d'accès du processeur de script**.</span><span class="sxs-lookup"><span data-stu-id="3685e-166">**Script Processor Path**.</span></span> <span data-ttu-id="3685e-167">Hello chemin d’accès du processeur de script hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-167">hello absolute path of hello script processor.</span></span> <span data-ttu-id="3685e-168">Toofiles de demandes qui correspondent à extension de fichier hello sera traité par le processeur de script hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-168">Requests toofiles that match hello file extension will be processed by hello script processor.</span></span> <span data-ttu-id="3685e-169">Utiliser un chemin hello `D:\home\site\wwwroot` répertoire racine de l’application toorefer tooyour.</span><span class="sxs-lookup"><span data-stu-id="3685e-169">Use hello path `D:\home\site\wwwroot` toorefer tooyour app's root directory.</span></span>
* <span data-ttu-id="3685e-170">**Arguments supplémentaires**.</span><span class="sxs-lookup"><span data-stu-id="3685e-170">**Additional Arguments**.</span></span> <span data-ttu-id="3685e-171">Arguments de ligne de commande facultatifs pour le processeur de script hello</span><span class="sxs-lookup"><span data-stu-id="3685e-171">Optional command-line arguments for hello script processor</span></span> 

### <a name="virtual-applications-and-directories"></a><span data-ttu-id="3685e-172">Applications et répertoires virtuels</span><span class="sxs-lookup"><span data-stu-id="3685e-172">Virtual applications and directories</span></span>
<span data-ttu-id="3685e-173">tooconfigure des applications virtuelles et les répertoires, spécifiez chaque répertoire virtuel et sa racine du site Web relatif toohello chemin d’accès physique correspondant.</span><span class="sxs-lookup"><span data-stu-id="3685e-173">tooconfigure virtual applications and directories, specify each virtual directory and its corresponding physical path relative toohello website root.</span></span> <span data-ttu-id="3685e-174">Si vous le souhaitez, vous pouvez sélectionner hello **Application** case à cocher toomark un répertoire virtuel en tant qu’application.</span><span class="sxs-lookup"><span data-stu-id="3685e-174">Optionally, you can select hello **Application** checkbox toomark a virtual directory as an application.</span></span>

## <a name="enabling-diagnostic-logs"></a><span data-ttu-id="3685e-175">Activation des journaux de diagnostic</span><span class="sxs-lookup"><span data-stu-id="3685e-175">Enabling diagnostic logs</span></span>
<span data-ttu-id="3685e-176">journaux de diagnostic tooenable :</span><span class="sxs-lookup"><span data-stu-id="3685e-176">tooenable diagnostic logs:</span></span>

1. <span data-ttu-id="3685e-177">Dans le panneau de hello pour votre application web, cliquez sur **tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="3685e-177">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="3685e-178">Cliquez sur **Journaux de diagnostic**.</span><span class="sxs-lookup"><span data-stu-id="3685e-178">Click **Diagnostic logs**.</span></span> 

<span data-ttu-id="3685e-179">Options liées à l'écriture des journaux de diagnostic à partir d'une application web qui prend en charge la journalisation :</span><span class="sxs-lookup"><span data-stu-id="3685e-179">Options for writing diagnostic logs from a web application that supports logging:</span></span> 

* <span data-ttu-id="3685e-180">**Journalisation des applications**.</span><span class="sxs-lookup"><span data-stu-id="3685e-180">**Application Logging**.</span></span> <span data-ttu-id="3685e-181">Écrit des journaux des applications système de fichiers toohello.</span><span class="sxs-lookup"><span data-stu-id="3685e-181">Writes application logs toohello file system.</span></span> <span data-ttu-id="3685e-182">La journalisation s’étend sur une période de 12 heures.</span><span class="sxs-lookup"><span data-stu-id="3685e-182">Logging lasts for a period of 12 hours.</span></span> 

<span data-ttu-id="3685e-183">**Niveau**.</span><span class="sxs-lookup"><span data-stu-id="3685e-183">**Level**.</span></span> <span data-ttu-id="3685e-184">Lorsque la journalisation de l’application est activée, cette option spécifie la quantité de hello d’informations qui seront enregistrées (erreur, avertissement, Information ou Verbose).</span><span class="sxs-lookup"><span data-stu-id="3685e-184">When application logging is enabled, this option specifies hello amount of information that will be recorded (Error, Warning, Information, or Verbose).</span></span>

<span data-ttu-id="3685e-185">**Journalisation du serveur Web**.</span><span class="sxs-lookup"><span data-stu-id="3685e-185">**Web server logging**.</span></span> <span data-ttu-id="3685e-186">Les journaux sont enregistrés au format de fichier journal étendu hello W3C.</span><span class="sxs-lookup"><span data-stu-id="3685e-186">Logs are saved in hello W3C extended log file format.</span></span> 

<span data-ttu-id="3685e-187">**Messages d’erreur détaillés**.</span><span class="sxs-lookup"><span data-stu-id="3685e-187">**Detailed error messages**.</span></span> <span data-ttu-id="3685e-188">Enregistre des messages d’erreur détaillés dans des fichiers .htm.</span><span class="sxs-lookup"><span data-stu-id="3685e-188">Saves detailed error messages .htm files.</span></span> <span data-ttu-id="3685e-189">fichiers de Hello sont enregistrés sous /LogFiles/DetailedErrors.</span><span class="sxs-lookup"><span data-stu-id="3685e-189">hello files are saved under /LogFiles/DetailedErrors.</span></span> 

<span data-ttu-id="3685e-190">**Suivi des demandes ayant échoué**.</span><span class="sxs-lookup"><span data-stu-id="3685e-190">**Failed request tracing**.</span></span> <span data-ttu-id="3685e-191">Échec de la demandes tooXML fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="3685e-191">Logs failed requests tooXML files.</span></span> <span data-ttu-id="3685e-192">fichiers Hello sont enregistrés sous LogFiles/W3SVC*xxx*, où xxx est un identificateur unique.</span><span class="sxs-lookup"><span data-stu-id="3685e-192">hello files are saved under /LogFiles/W3SVC*xxx*, where xxx is a unique identifier.</span></span> <span data-ttu-id="3685e-193">Ce dossier contient un fichier XSL et un ou plusieurs fichiers XML.</span><span class="sxs-lookup"><span data-stu-id="3685e-193">This folder contains an XSL file and one or more XML files.</span></span> <span data-ttu-id="3685e-194">Vérifiez que hello toodownload fichier XSL, car il fournit des fonctionnalités de mise en forme et de filtrer le contenu hello des fichiers XML de hello.</span><span class="sxs-lookup"><span data-stu-id="3685e-194">Make sure toodownload hello XSL file, because it provides functionality for formatting and filtering hello contents of hello XML files.</span></span>

<span data-ttu-id="3685e-195">fichiers de journaux tooview hello, vous devez créer les informations d’identification de FTP, comme suit :</span><span class="sxs-lookup"><span data-stu-id="3685e-195">tooview hello log files, you must create FTP credentials, as follows:</span></span>

1. <span data-ttu-id="3685e-196">Dans le panneau de hello pour votre application web, cliquez sur **tous les paramètres**.</span><span class="sxs-lookup"><span data-stu-id="3685e-196">In hello blade for your web app, click **All settings**.</span></span>
2. <span data-ttu-id="3685e-197">Cliquez sur **Informations d’identification du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="3685e-197">Click **Deployment credentials**.</span></span>
3. <span data-ttu-id="3685e-198">Entrez un nom d'utilisateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="3685e-198">Enter a user name and password.</span></span>
4. <span data-ttu-id="3685e-199">Cliquez sur **Save**.</span><span class="sxs-lookup"><span data-stu-id="3685e-199">Click **Save**.</span></span>

![Définir les informations d’identification de déploiement][configure03]

<span data-ttu-id="3685e-201">nom d’utilisateur FTP Hello complet est « app\username » où *application* est le nom hello de votre application web.</span><span class="sxs-lookup"><span data-stu-id="3685e-201">hello full FTP user name is “app\username” where *app* is hello name of your web app.</span></span> <span data-ttu-id="3685e-202">Hello nom d’utilisateur est répertorié dans le panneau de l’application hello web, sous **Essentials**.</span><span class="sxs-lookup"><span data-stu-id="3685e-202">hello username is listed in hello web app blade, under **Essentials**.</span></span>  

![Informations d’identification de déploiement FTP][configure02]

## <a name="other-configuration-tasks"></a><span data-ttu-id="3685e-204">Autres tâches de configuration</span><span class="sxs-lookup"><span data-stu-id="3685e-204">Other configuration tasks</span></span>
### <a name="ssl"></a><span data-ttu-id="3685e-205">SSL</span><span class="sxs-lookup"><span data-stu-id="3685e-205">SSL</span></span>
<span data-ttu-id="3685e-206">En mode De base ou Standard, vous pouvez télécharger des certificats SSL pour un domaine personnalisé.</span><span class="sxs-lookup"><span data-stu-id="3685e-206">In Basic or Standard mode, you can upload SSL certificates for a custom domain.</span></span> <span data-ttu-id="3685e-207">Pour plus d’informations, consultez [Activer le protocole HTTPS pour une application web].</span><span class="sxs-lookup"><span data-stu-id="3685e-207">For more information, see [Enable HTTPS for a web app].</span></span> 

<span data-ttu-id="3685e-208">Cliquez sur vos certificats téléchargés, tooview **tous les paramètres** > **les domaines personnalisés et SSL**.</span><span class="sxs-lookup"><span data-stu-id="3685e-208">tooview your uploaded certificates, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="domain-names"></a><span data-ttu-id="3685e-209">Noms de domaine</span><span class="sxs-lookup"><span data-stu-id="3685e-209">Domain names</span></span>
<span data-ttu-id="3685e-210">Ajouter des noms de domaine personnalisés pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="3685e-210">Add custom domain names for your web app.</span></span> <span data-ttu-id="3685e-211">Pour plus d’informations, consultez [Configurer un nom de domaine personnalisé pour une application web dans Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="3685e-211">For more information, see [Configure a custom domain name for a web app in Azure App Service].</span></span>

<span data-ttu-id="3685e-212">Cliquez sur les noms de votre domaine, tooview **tous les paramètres** > **les domaines personnalisés et SSL**.</span><span class="sxs-lookup"><span data-stu-id="3685e-212">tooview your domain names, click **All Settings** > **Custom domains and SSL**.</span></span>

### <a name="deployments"></a><span data-ttu-id="3685e-213">Déploiements</span><span class="sxs-lookup"><span data-stu-id="3685e-213">Deployments</span></span>
* <span data-ttu-id="3685e-214">Configurer un déploiement continu</span><span class="sxs-lookup"><span data-stu-id="3685e-214">Set up continuous deployment.</span></span> <span data-ttu-id="3685e-215">Consultez [à l’aide de Git toodeploy Web Apps dans Azure App Service](web-sites-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="3685e-215">See [Using Git toodeploy Web Apps in Azure App Service](web-sites-deploy.md).</span></span>
* <span data-ttu-id="3685e-216">Emplacements de déploiement</span><span class="sxs-lookup"><span data-stu-id="3685e-216">Deployment slots.</span></span> <span data-ttu-id="3685e-217">Consultez [déployer des environnements de tooStaging pour les applications Web dans Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="3685e-217">See [Deploy tooStaging Environments for Web Apps in Azure App Service].</span></span>

<span data-ttu-id="3685e-218">Cliquez sur les emplacements de votre déploiement, tooview **tous les paramètres** > **les emplacements de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="3685e-218">tooview your deployment slots, click **All Settings** > **Deployment slots**.</span></span>

### <a name="monitoring"></a><span data-ttu-id="3685e-219">Surveillance</span><span class="sxs-lookup"><span data-stu-id="3685e-219">Monitoring</span></span>
<span data-ttu-id="3685e-220">En mode de base ou Standard, vous pouvez tester la disponibilité hello de points de terminaison HTTP ou HTTPS, à partir des emplacements de géo-distribué toothree.</span><span class="sxs-lookup"><span data-stu-id="3685e-220">In Basic or Standard mode, you can  test hello availability of HTTP or HTTPS endpoints, from up toothree geo-distributed locations.</span></span> <span data-ttu-id="3685e-221">Un test de surveillance échoue si hello code de réponse HTTP est une erreur (4xx ou 5xx) ou de réponse de hello prend plus de 30 secondes.</span><span class="sxs-lookup"><span data-stu-id="3685e-221">A monitoring test fails if hello HTTP response code is an error (4xx or 5xx) or hello response takes more than 30 seconds.</span></span> <span data-ttu-id="3685e-222">Un point de terminaison est considéré comme étant disponible si les tests d’analyse hello réussissent tous hello indiqué des emplacements.</span><span class="sxs-lookup"><span data-stu-id="3685e-222">An endpoint is considered available if hello monitoring tests succeed from all hello specified locations.</span></span> 

<span data-ttu-id="3685e-223">Pour plus d’informations, consultez [Surveillance de l’état d’un point de terminaison Web].</span><span class="sxs-lookup"><span data-stu-id="3685e-223">For more information, see [How to: Monitor web endpoint status].</span></span>

> [!NOTE]
> <span data-ttu-id="3685e-224">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications], où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="3685e-224">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service], where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="3685e-225">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="3685e-225">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3685e-226">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="3685e-226">Next steps</span></span>
* <span data-ttu-id="3685e-227">[Configuration d’un nom de domaine personnalisé dans Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="3685e-227">[Configure a custom domain name in Azure App Service]</span></span>
* <span data-ttu-id="3685e-228">[Activer le protocole HTTPS pour une application dans Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="3685e-228">[Enable HTTPS for an app in Azure App Service]</span></span>
* <span data-ttu-id="3685e-229">[Faire évoluer une application Web dans Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="3685e-229">[Scale a web app in Azure App Service]</span></span>
* <span data-ttu-id="3685e-230">[Surveiller les applications Web dans Azure App Service]</span><span class="sxs-lookup"><span data-stu-id="3685e-230">[Monitoring basics for Web Apps in Azure App Service]</span></span>

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Configuration d’un nom de domaine personnalisé dans Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[déployer des environnements de tooStaging pour les applications Web dans Azure App Service]: ./web-sites-staged-publishing.md
[Activer le protocole HTTPS pour une application dans Azure App Service]: ./app-service-web-tutorial-custom-ssl.md
[Surveillance de l’état d’un point de terminaison Web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Surveiller les applications Web dans Azure App Service]: ./web-sites-monitor.md
[mode pipeline]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Faire évoluer une application Web dans Azure App Service]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[essayez du Service d’applications]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
