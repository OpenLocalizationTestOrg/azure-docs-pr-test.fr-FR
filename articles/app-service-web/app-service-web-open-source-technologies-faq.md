---
title: "technologies d’aaaOpen source Foire aux questions pour Azure web apps | Documents Microsoft"
description: "Obtenir elles sonttrop des réponses aux questions sur les technologies open source dans la fonctionnalité d’applications Web hello du Service d’applications Azure."
services: app-service\web
documentationcenter: 
author: genlin
manager: cshepard
editor: 
tags: top-support-issue
ms.assetid: 2fa5ee6b-51a6-4237-805f-518e6c57d11b
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 7/10/2017
ms.author: genli
ms.openlocfilehash: 35cff4f322859d25972747cf55aa7c4316381a51
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="f7979-103">FAQ sur les technologies open source pour Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="f7979-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="f7979-104">Cet article a elles sonttrop des réponses aux questions (FAQ) sur les problèmes avec les technologies open source pour hello [fonctionnalité des applications Web d’Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="f7979-104">This article has answers toofrequently asked questions (FAQs) about issues with open-source technologies for hello [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="f7979-105">Ma base de données ClearDB est hors service.</span><span class="sxs-lookup"><span data-stu-id="f7979-105">My ClearDB database is down.</span></span> <span data-ttu-id="f7979-106">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="f7979-106">How do I resolve this?</span></span>

<span data-ttu-id="f7979-107">Contactez le [support ClearDB](https://www.cleardb.com/developers/help/support) pour tout problème lié à la base de données.</span><span class="sxs-lookup"><span data-stu-id="f7979-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="f7979-108">Pour les réponses toocommon questions ClearDB, consultez [ClearDB FAQ](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="f7979-108">For answers toocommon questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-hello-portal"></a><span data-ttu-id="f7979-109">Pourquoi ma base de données ClearDB pas n’est pas répertorié dans le portail de hello ?</span><span class="sxs-lookup"><span data-stu-id="f7979-109">Why isn't my ClearDB database listed in hello portal?</span></span>

<span data-ttu-id="f7979-110">Si vous créez une base de données ClearDB Bonjour [portail Azure](http://portal.azure.com/), base de données hello n’apparaît pas dans hello [portail Azure classic](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="f7979-110">If you create a ClearDB database in hello [Azure portal](http://portal.azure.com/), hello database doesn't appear in hello [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="f7979-111">toowork contourner ce problème, vous pouvez lier manuellement votre application web de toohello de base de données.</span><span class="sxs-lookup"><span data-stu-id="f7979-111">toowork around this, you can manually link your database toohello web app.</span></span>

<span data-ttu-id="f7979-112">De même, si vous créez une base de données ClearDB Bonjour [portail Azure classic](http://manage.windowsazure.com/), vous ne voyez pas votre base de données Bonjour [portail Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f7979-112">Similarly, if you create a ClearDB database in hello [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in hello [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="f7979-113">Dans ce cas, aucune solution de contournement n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="f7979-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="f7979-114">Pour plus d’informations, consultez [FAQ sur les bases de données MySQL ClearDB avec Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="f7979-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="f7979-115">Pourquoi ma base de données ClearDB n’a-t-elle pas été migrée pendant la migration de mon abonnement ?</span><span class="sxs-lookup"><span data-stu-id="f7979-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="f7979-116">Lorsque vous effectuez la migration de ressources entre différents abonnements, certaines limitations s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="f7979-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="f7979-117">Une base de données MySQL ClearDB est un service tiers. Elle n’est donc pas migrée lors de la migration d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f7979-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="f7979-118">Si vous ne gérez pas la migration de votre base de données MySQL hello avant de migrer vos ressources Azure, votre base de données ClearDB MySQL peut être indisponible.</span><span class="sxs-lookup"><span data-stu-id="f7979-118">If you don't manage hello migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="f7979-119">tooavoid cela, tout d’abord, migrer manuellement votre base de données ClearDB et migrer hello abonnement Azure pour votre application web.</span><span class="sxs-lookup"><span data-stu-id="f7979-119">tooavoid this, first, manually migrate your ClearDB database, and then migrate hello Azure subscription for your web app.</span></span>

<span data-ttu-id="f7979-120">Pour plus d’informations, consultez [FAQ sur les bases de données MySQL ClearDB avec Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="f7979-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-tootroubleshoot-php-issues"></a><span data-ttu-id="f7979-121">Comment activer PHP journalisation des problèmes PHP tootroubleshoot ?</span><span class="sxs-lookup"><span data-stu-id="f7979-121">How do I turn on PHP logging tootroubleshoot PHP issues?</span></span>

<span data-ttu-id="f7979-122">tooturn journalisation de PHP :</span><span class="sxs-lookup"><span data-stu-id="f7979-122">tooturn on PHP logging:</span></span>

1. <span data-ttu-id="f7979-123">Connectez-vous à tooyour [site Web de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="f7979-123">Sign in tooyour [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="f7979-124">Dans le menu supérieur de hello, sélectionnez **Console de débogage** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="f7979-124">In hello top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="f7979-125">Sélectionnez hello **Site** dossier.</span><span class="sxs-lookup"><span data-stu-id="f7979-125">Select hello **Site** folder.</span></span>
4. <span data-ttu-id="f7979-126">Sélectionnez hello **wwwroot** dossier.</span><span class="sxs-lookup"><span data-stu-id="f7979-126">Select hello **wwwroot** folder.</span></span>
5. <span data-ttu-id="f7979-127">Sélectionnez hello  **+**  icône, puis sélectionnez **nouveau fichier**.</span><span class="sxs-lookup"><span data-stu-id="f7979-127">Select hello **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="f7979-128">Définir le nom de fichier hello trop**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="f7979-128">Set hello file name too**.user.ini**.</span></span>
7. <span data-ttu-id="f7979-129">Sélectionnez le crayon hello suivant trop**. user.ini**.</span><span class="sxs-lookup"><span data-stu-id="f7979-129">Select hello pencil icon next too**.user.ini**.</span></span>
8. <span data-ttu-id="f7979-130">Dans le fichier de hello, ajoutez ce code :`log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="f7979-130">In hello file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="f7979-131">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="f7979-131">Select **Save**.</span></span>
10. <span data-ttu-id="f7979-132">Sélectionnez le crayon hello suivant trop**wp-config.PHP**.</span><span class="sxs-lookup"><span data-stu-id="f7979-132">Select hello pencil icon next too**wp-config.php**.</span></span>
11. <span data-ttu-id="f7979-133">Modifiez toohello de texte hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="f7979-133">Change hello text toohello following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging too/wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings tooscreendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors tooscreenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="f7979-134">Bonjour portail Azure, dans le menu application hello web, redémarrez votre application web.</span><span class="sxs-lookup"><span data-stu-id="f7979-134">In hello Azure portal, in hello web app menu, restart your web app.</span></span>

<span data-ttu-id="f7979-135">Pour plus d’informations, consultez [Activer les journaux d’erreurs WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="f7979-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="f7979-136">Comment journaliser les erreurs d’application Python dans des applications hébergées dans App Service ?</span><span class="sxs-lookup"><span data-stu-id="f7979-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="f7979-137">erreurs d’application toocapture Python :</span><span class="sxs-lookup"><span data-stu-id="f7979-137">toocapture Python application errors:</span></span>

1. <span data-ttu-id="f7979-138">Bonjour portail Azure, dans votre application web, sélectionnez **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="f7979-138">In hello Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="f7979-139">Sur hello **paramètres** onglet, sélectionnez **paramètres de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="f7979-139">On hello **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="f7979-140">Sous **paramètres de l’application**, entrez hello suivant la paire clé/valeur :</span><span class="sxs-lookup"><span data-stu-id="f7979-140">Under **App settings**, enter hello following key/value pair:</span></span>
    * <span data-ttu-id="f7979-141">Clé : WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="f7979-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="f7979-142">Valeur : D:\home\site\wwwroot\logs.txt (entrez le nom de fichier de votre choix)</span><span class="sxs-lookup"><span data-stu-id="f7979-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="f7979-143">Vous devez maintenant voir des erreurs dans le fichier de logs.txt hello dans le dossier wwwroot de hello.</span><span class="sxs-lookup"><span data-stu-id="f7979-143">You should now see errors in hello logs.txt file in hello wwwroot folder.</span></span>

## <a name="how-do-i-change-hello-version-of-hello-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="f7979-144">Comment modifier les version hello Hello application Node.js qui est hébergée dans le Service d’applications ?</span><span class="sxs-lookup"><span data-stu-id="f7979-144">How do I change hello version of hello Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="f7979-145">version hello toochange hello application Node.js, vous pouvez utiliser une des options suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="f7979-145">toochange hello version of hello Node.js application, you can use one of hello following options:</span></span>

*   <span data-ttu-id="f7979-146">Bonjour portail Azure, utilisez **paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="f7979-146">In hello Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="f7979-147">Dans hello portail Azure, accédez à l’application web tooyour.</span><span class="sxs-lookup"><span data-stu-id="f7979-147">In hello Azure portal, go tooyour web app.</span></span>
    2. <span data-ttu-id="f7979-148">Sur hello **paramètres** panneau, sélectionnez **paramètres de l’Application**.</span><span class="sxs-lookup"><span data-stu-id="f7979-148">On hello **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="f7979-149">Dans **paramètres de l’application**, vous pouvez inclure WEBSITE_NODE_DEFAULT_VERSION en tant que clé de hello et hello version de Node.js souhaitée en tant que valeur de hello.</span><span class="sxs-lookup"><span data-stu-id="f7979-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as hello key, and hello version of Node.js you want as hello value.</span></span>
    4. <span data-ttu-id="f7979-150">Accédez tooyour [console de Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="f7979-150">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="f7979-151">toocheck hello Node.js version, entrez hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f7979-151">toocheck hello Node.js version, enter hello following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="f7979-152">Modifier le fichier de iisnode.yml hello.</span><span class="sxs-lookup"><span data-stu-id="f7979-152">Modify hello iisnode.yml file.</span></span> <span data-ttu-id="f7979-153">Version de Node.js hello modification dans le fichier de iisnode.yml hello définit uniquement l’environnement d’exécution hello qu’iisnode utilise.</span><span class="sxs-lookup"><span data-stu-id="f7979-153">Changing hello Node.js version in hello iisnode.yml file only sets hello runtime environment that iisnode uses.</span></span> <span data-ttu-id="f7979-154">Votre cmd Kudu et autres encore utiliseront version Node.js hello qui est définie dans **paramètres de l’application** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f7979-154">Your Kudu cmd and others still use hello Node.js version that is set in **App settings** in hello Azure portal.</span></span>

    <span data-ttu-id="f7979-155">tooset hello iisnode.yml créer manuellement un fichier iisnode.yml dans votre dossier racine de l’application.</span><span class="sxs-lookup"><span data-stu-id="f7979-155">tooset hello iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="f7979-156">Dans le fichier de hello, inclure hello ligne suivante :</span><span class="sxs-lookup"><span data-stu-id="f7979-156">In hello file, include hello following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="f7979-157">Fichier de iisnode.yml hello d’ensemble à l’aide de package.json durant le déploiement de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="f7979-157">Set hello iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="f7979-158">Hello, processus de déploiement du contrôle source Azure implique hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="f7979-158">hello Azure source control deployment process involves hello following steps:</span></span>
    1. <span data-ttu-id="f7979-159">Déplace le contenu toohello Azure web app.</span><span class="sxs-lookup"><span data-stu-id="f7979-159">Moves content toohello Azure web app.</span></span>
    2. <span data-ttu-id="f7979-160">Crée un script de déploiement par défaut, s’il n’existe pas (deploy.cmd, les fichiers .deployment) dans le dossier racine de hello web app.</span><span class="sxs-lookup"><span data-stu-id="f7979-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in hello web app root folder.</span></span>
    3. <span data-ttu-id="f7979-161">Exécute un script de déploiement dans lequel il crée un fichier iisnode.yml si vous indiquez hello Node.js version dans le fichier de package.json hello > moteur`"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="f7979-161">Runs a deployment script in which it creates an iisnode.yml file if you mention hello Node.js version in hello package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="f7979-162">fichier de iisnode.yml Hello a hello ligne de code suivante :</span><span class="sxs-lookup"><span data-stu-id="f7979-162">hello iisnode.yml file has hello following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-hello-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="f7979-163">Je vois le message « Erreur de l’établissement d’une connexion de base de données » de type hello dans mon application WordPress qui est hébergée dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="f7979-163">I see hello message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="f7979-164">Comment puis-je résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="f7979-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="f7979-165">Si vous voyez cette erreur dans votre application de Azure WordPress, tooenable php_errors.log et debug.log, les étapes de hello complète détaillées dans [WordPress d’activer les journaux d’erreurs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="f7979-165">If you see this error in your Azure WordPress app, tooenable php_errors.log and debug.log, complete hello steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="f7979-166">Lorsque les journaux de hello sont activées, reproduire l’erreur de hello et vérifiez hello journaux toosee si vous manquez de connexions :</span><span class="sxs-lookup"><span data-stu-id="f7979-166">When hello logs are enabled, reproduce hello error, and then check hello logs toosee if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded hello ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="f7979-167">Si vous voyez cette erreur dans vos fichiers debug.log ou php_errors.log, votre application dépasse le nombre hello de connexions.</span><span class="sxs-lookup"><span data-stu-id="f7979-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding hello number of connections.</span></span> <span data-ttu-id="f7979-168">Si vous hébergez sur ClearDB, vérifiez le nombre hello de connexions qui sont disponibles dans votre [le plan de service](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="f7979-168">If you’re hosting on ClearDB, verify hello number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="f7979-169">Comment déboguer une application Node.js hébergée dans App Service ?</span><span class="sxs-lookup"><span data-stu-id="f7979-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="f7979-170">Accédez tooyour [console de Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="f7979-170">Go tooyour [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="f7979-171">Dossier de journaux d’application accédez tooyour (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="f7979-171">Go tooyour application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="f7979-172">Dans le fichier de logging_errors.txt hello, recherchez le contenu.</span><span class="sxs-lookup"><span data-stu-id="f7979-172">In hello logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="f7979-173">Comment installer des modules Python natifs dans une application web App Service ou une application API ?</span><span class="sxs-lookup"><span data-stu-id="f7979-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="f7979-174">Certains packages ne peuvent pas être installés à l’aide de PIP dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f7979-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="f7979-175">package de Hello ne peut-être pas être disponible sur hello Python Package Index ou un compilateur peut être nécessaire (un compilateur n’est pas disponible sur l’ordinateur hello qui exécute l’application hello web dans le Service d’applications).</span><span class="sxs-lookup"><span data-stu-id="f7979-175">hello package might not be available on hello Python Package Index, or a compiler might be required (a compiler is not available on hello computer that is running hello web app in App Service).</span></span> <span data-ttu-id="f7979-176">Pour plus d’informations sur l’installation des modules natifs dans App Service Web Apps et API Apps, consultez [Installer des modules Python dans App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="f7979-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-tooapp-service-by-using-git-and-hello-new-version-of-python"></a><span data-ttu-id="f7979-177">Comment déployer un tooApp d’application Django Service à l’aide de Git et hello la nouvelle version de Python ?</span><span class="sxs-lookup"><span data-stu-id="f7979-177">How do I deploy a Django app tooApp Service by using Git and hello new version of Python?</span></span>

<span data-ttu-id="f7979-178">Pour plus d’informations sur l’installation de Django, consultez [déploiement d’un tooApp d’application Django Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="f7979-178">For information about installing Django, see [Deploying a Django app tooApp Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-hello-tomcat-log-files-located"></a><span data-ttu-id="f7979-179">Où sont hello Tomcat, ces fichiers ?</span><span class="sxs-lookup"><span data-stu-id="f7979-179">Where are hello Tomcat log files located?</span></span>

<span data-ttu-id="f7979-180">Pour les déploiements personnalisés et la Place de marché Azure :</span><span class="sxs-lookup"><span data-stu-id="f7979-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="f7979-181">Emplacement du dossier : D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="f7979-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="f7979-182">Fichiers d’intérêt :</span><span class="sxs-lookup"><span data-stu-id="f7979-182">Files of interest:</span></span>
    * <span data-ttu-id="f7979-183">catalina.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-184">host-manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-185">localhost.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-186">manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-187">site_access_log.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="f7979-188">Pour les déploiements **Paramètres de l’application** dans le portail :</span><span class="sxs-lookup"><span data-stu-id="f7979-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="f7979-189">Emplacement du dossier : D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="f7979-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="f7979-190">Fichiers d’intérêt :</span><span class="sxs-lookup"><span data-stu-id="f7979-190">Files of interest:</span></span>
    * <span data-ttu-id="f7979-191">catalina.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-192">host-manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-193">localhost.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-194">manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="f7979-195">site_access_log.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="f7979-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="f7979-196">Comment résoudre les erreurs de connexion du pilote JDBC ?</span><span class="sxs-lookup"><span data-stu-id="f7979-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="f7979-197">Vous pouvez voir hello message dans vos journaux Tomcat suivant :</span><span class="sxs-lookup"><span data-stu-id="f7979-197">You might see hello following message in your Tomcat logs:</span></span>

```
hello web application[ROOT] registered hello JDBC driver [com.mysql.jdbc.Driver] but failed toounregister it when hello web application was stopped. tooprevent a memory leak,hello JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="f7979-198">Erreur de hello tooresolve :</span><span class="sxs-lookup"><span data-stu-id="f7979-198">tooresolve hello error:</span></span>

1. <span data-ttu-id="f7979-199">Supprimer le fichier sqljdbc*.jar de hello à partir de votre dossier de bibliothèque d’applications.</span><span class="sxs-lookup"><span data-stu-id="f7979-199">Remove hello sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="f7979-200">Si vous utilisez hello Tomcat ou Azure Marketplace Tomcat serveur web personnalisé, copiez ce dossier lib de .jar fichier toohello Tomcat.</span><span class="sxs-lookup"><span data-stu-id="f7979-200">If you are using hello custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file toohello Tomcat lib folder.</span></span>
3. <span data-ttu-id="f7979-201">Si vous activez Java à partir de hello portail Azure (sélectionnez **Java 1.8** > **serveur Tomcat**), fichier de copie hello sqljdbc.* jar dans le dossier hello parallèle tooyour application.</span><span class="sxs-lookup"><span data-stu-id="f7979-201">If you are enabling Java from hello Azure portal (select **Java 1.8** > **Tomcat server**), copy hello sqljdbc.* jar file in hello folder that's parallel tooyour app.</span></span> <span data-ttu-id="f7979-202">Ensuite, ajoutez hello classpath paramètre toohello web.config fichier suivant :</span><span class="sxs-lookup"><span data-stu-id="f7979-202">Then, add hello following classpath setting toohello web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path toohello sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-toocopy-live-log-files"></a><span data-ttu-id="f7979-203">Pourquoi voir des erreurs lorsque je tente de fichiers de journal à la volée toocopy ?</span><span class="sxs-lookup"><span data-stu-id="f7979-203">Why do I see errors when I attempt toocopy live log files?</span></span>

<span data-ttu-id="f7979-204">Si vous essayez de fichiers de journal à la volée toocopy pour une application Java (par exemple, Tomcat), vous pouvez rencontrer cette erreur FTP :</span><span class="sxs-lookup"><span data-stu-id="f7979-204">If you try toocopy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
hello process cannot access hello file because it is being used by another process.
```

<span data-ttu-id="f7979-205">message d’erreur Hello peut-être varier en fonction du client de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="f7979-205">hello error message might vary, depending on hello FTP client.</span></span>

<span data-ttu-id="f7979-206">Ce problème de verrouillage concerne toutes les applications Java.</span><span class="sxs-lookup"><span data-stu-id="f7979-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="f7979-207">Kudu uniquement prend en charge le téléchargement de ce fichier lors de l’application hello est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="f7979-207">Only Kudu supports downloading this file while hello app is running.</span></span>

<span data-ttu-id="f7979-208">Arrêt application hello autorise l’accès FTP des fichiers de toothese.</span><span class="sxs-lookup"><span data-stu-id="f7979-208">Stopping hello app allows FTP access toothese files.</span></span>

<span data-ttu-id="f7979-209">Une autre solution consiste à toowrite une tâche Web qui s’exécute selon une planification et copie ces répertoire de différents fichiers tooa.</span><span class="sxs-lookup"><span data-stu-id="f7979-209">Another workaround is toowrite a WebJob that runs on a schedule and copies these files tooa different directory.</span></span> <span data-ttu-id="f7979-210">Pour un exemple de projet, consultez hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) projet.</span><span class="sxs-lookup"><span data-stu-id="f7979-210">For a sample project, see hello [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-hello-log-files-for-jetty"></a><span data-ttu-id="f7979-211">Où trouver des fichiers de journaux hello pour Jetty ?</span><span class="sxs-lookup"><span data-stu-id="f7979-211">Where do I find hello log files for Jetty?</span></span>

<span data-ttu-id="f7979-212">Pour les déploiements personnalisés et de marché, fichier de journal hello est dans le dossier de D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs hello.</span><span class="sxs-lookup"><span data-stu-id="f7979-212">For Marketplace and custom deployments, hello log file is in hello D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="f7979-213">Notez qu’emplacement du dossier hello varie selon la version hello de Jetty que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="f7979-213">Note that hello folder location depends on hello version of Jetty you are using.</span></span> <span data-ttu-id="f7979-214">Par exemple, le chemin d’accès de hello fournies ici de Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="f7979-214">For example, hello path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="f7979-215">Recherchez jetty_*AAAA_MM_JJ*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="f7979-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="f7979-216">Pour les déploiements de paramètre d’application de portail, fichier de journal hello est D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="f7979-216">For portal App Setting deployments, hello log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="f7979-217">Recherchez jetty_*AAAA_MM_JJ*.stderrout.log</span><span class="sxs-lookup"><span data-stu-id="f7979-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="f7979-218">Puis-je envoyer un e-mail à partir de mon application web Azure ?</span><span class="sxs-lookup"><span data-stu-id="f7979-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="f7979-219">App Service ne dispose pas d’une fonctionnalité de messagerie intégrée.</span><span class="sxs-lookup"><span data-stu-id="f7979-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="f7979-220">Consultez cette [discussion sur le dépassement de capacité de la file](http://stackoverflow.com/questions/17666161/sending-email-from-azure) afin d’obtenir des solutions alternatives pour envoyer un e-mail à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="f7979-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-tooanother-url"></a><span data-ttu-id="f7979-221">Pourquoi mon site WordPress ne redirige pas les URL tooanother ?</span><span class="sxs-lookup"><span data-stu-id="f7979-221">Why does my WordPress site redirect tooanother URL?</span></span>

<span data-ttu-id="f7979-222">Si vous avez récemment migré tooAzure, WordPress peut rediriger toohello ancienne URL du domaine.</span><span class="sxs-lookup"><span data-stu-id="f7979-222">If you have recently migrated tooAzure, WordPress might redirect toohello old domain URL.</span></span> <span data-ttu-id="f7979-223">Cela est dû à un paramètre dans la base de données MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="f7979-223">This is caused by a setting in hello MySQL database.</span></span>

<span data-ttu-id="f7979-224">WordPress Buddy + est une Extension de Site Azure que vous pouvez utiliser l’URL de redirection hello tooupdate directement dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="f7979-224">WordPress Buddy+ is an Azure Site Extension that you can use tooupdate hello redirection URL directly in hello database.</span></span> <span data-ttu-id="f7979-225">Pour plus d’informations sur l’utilisation de WordPress Buddy+, consultez [Outils WordPress et migration MySQL avec WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="f7979-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="f7979-226">Vous pouvez également, si vous préférez des URL de redirection hello toomanually mise à jour à l’aide de requêtes SQL ou PHPMyAdmin, consultez [WordPress : redirection des URL de toowrong](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="f7979-226">Alternatively, if you prefer toomanually update hello redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting toowrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="f7979-227">Comment modifier mon mot de passe de connexion à WordPress ?</span><span class="sxs-lookup"><span data-stu-id="f7979-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="f7979-228">Si vous avez oublié votre mot de passe de connexion de le WordPress, vous pouvez utiliser WordPress Buddy + tooupdate il.</span><span class="sxs-lookup"><span data-stu-id="f7979-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ tooupdate it.</span></span> <span data-ttu-id="f7979-229">tooreset votre mot de passe, installez hello WordPress Buddy + Extension de Site Azure et les étapes de hello puis complète décrite dans [WordPress outils et migration de MySQL avec WordPress Buddy +](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="f7979-229">tooreset your password, install hello WordPress Buddy+ Azure Site Extension, and then complete hello steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-toowordpress-how-do-i-resolve-this"></a><span data-ttu-id="f7979-230">Je ne parviens pas à se connecter tooWordPress.</span><span class="sxs-lookup"><span data-stu-id="f7979-230">I can't sign in tooWordPress.</span></span> <span data-ttu-id="f7979-231">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="f7979-231">How do I resolve this?</span></span>

<span data-ttu-id="f7979-232">Si vous ne pouvez pas accéder à WordPress après l’installation d’un plug-in, celui-ci est peut-être défectueux.</span><span class="sxs-lookup"><span data-stu-id="f7979-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="f7979-233">WordPress Buddy+ est une extension de site Azure qui peut vous aider à désactiver des plug-ins dans WordPress.</span><span class="sxs-lookup"><span data-stu-id="f7979-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="f7979-234">Pour plus d’informations, consultez [Outils WordPress et migration MySQL avec WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="f7979-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="f7979-235">Comment migrer ma base de données WordPress ?</span><span class="sxs-lookup"><span data-stu-id="f7979-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="f7979-236">Vous avez plusieurs options pour la migration hello MySQL de base de données qui est le site Web de WordPress tooyour connecté :</span><span class="sxs-lookup"><span data-stu-id="f7979-236">You have multiple options for migrating hello MySQL database that's connected tooyour WordPress website:</span></span>

* <span data-ttu-id="f7979-237">Développeurs : Hello d’utilisation [invite de commandes ou PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="f7979-237">Developers: Use hello [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="f7979-238">Utilisateurs autres que des développeurs : utilisez [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="f7979-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="f7979-239">Comment sécuriser davantage WordPress ?</span><span class="sxs-lookup"><span data-stu-id="f7979-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="f7979-240">toolearn sur les meilleures pratiques de sécurité pour WordPress, consultez [meilleures pratiques pour la sécurité de WordPress dans Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="f7979-240">toolearn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-toouse-phpmyadmin-and-i-see-hello-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="f7979-241">J’essaie de toouse PHPMyAdmin, et que je vois hello message « Accès refusé ».</span><span class="sxs-lookup"><span data-stu-id="f7979-241">I am trying toouse PHPMyAdmin, and I see hello message “Access denied.”</span></span> <span data-ttu-id="f7979-242">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="f7979-242">How do I resolve this?</span></span>

<span data-ttu-id="f7979-243">Vous pouvez rencontrer ce problème si la fonctionnalité de hello MySQL dans l’application n’est pas encore exécuté dans cette instance du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="f7979-243">You might experience this issue if hello MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="f7979-244">tooresolve hello problème, essayez de tooaccess votre site Web.</span><span class="sxs-lookup"><span data-stu-id="f7979-244">tooresolve hello issue, try tooaccess your website.</span></span> <span data-ttu-id="f7979-245">Cela démarre le processus hello requis, y compris les processus hello MySQL dans l’application.</span><span class="sxs-lookup"><span data-stu-id="f7979-245">This starts hello required processes, including hello MySQL in-app process.</span></span> <span data-ttu-id="f7979-246">tooverify que MySQL dans l’application est en cours d’exécution, dans l’Explorateur de processus, assurez-vous que mysqld.exe est répertorié dans le processus de hello.</span><span class="sxs-lookup"><span data-stu-id="f7979-246">tooverify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in hello processes.</span></span>

<span data-ttu-id="f7979-247">Après que vous être assuré que MySQL dans l’application s’exécute, essayez de toouse PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="f7979-247">After you ensure that MySQL in-app is running, try toouse PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-tooimport-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="f7979-248">J’obtiens une erreur HTTP 403 lors essayez tooimport ou exporter ma base de données MySQL dans l’application à l’aide de PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="f7979-248">I get an HTTP 403 error when I try tooimport or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="f7979-249">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="f7979-249">How do I resolve this?</span></span>

<span data-ttu-id="f7979-250">Si vous utilisez une version antérieure de Chrome, vous rencontrez sans doute un bogue connu.</span><span class="sxs-lookup"><span data-stu-id="f7979-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="f7979-251">problème de hello tooresolve, tooa mise à niveau la version plus récente de Chrome.</span><span class="sxs-lookup"><span data-stu-id="f7979-251">tooresolve hello issue, upgrade tooa newer version of Chrome.</span></span> <span data-ttu-id="f7979-252">Essayez également à l’aide d’un autre navigateur, comme Internet Explorer ou Edge, où hello ne se produit pas.</span><span class="sxs-lookup"><span data-stu-id="f7979-252">Also try using a different browser, like Internet Explorer or Edge, where hello issue does not occur.</span></span>
