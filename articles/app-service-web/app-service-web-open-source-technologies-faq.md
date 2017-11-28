---
title: FAQ sur les technologies open source pour Azure Web Apps | Microsoft Docs
description: "Découvrez les réponses aux questions fréquemment posées sur les technologies open source de la fonctionnalité Web Apps d’Azure App Service."
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
ms.openlocfilehash: d37b53242c0b231d83425a59ecbe50216216a95b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="open-source-technologies-faqs-for-web-apps-in-azure"></a><span data-ttu-id="77f43-103">FAQ sur les technologies open source pour Azure Web Apps</span><span class="sxs-lookup"><span data-stu-id="77f43-103">Open-source technologies FAQs for Web Apps in Azure</span></span>

<span data-ttu-id="77f43-104">Cet article contient des réponses aux questions fréquemment posées sur les problèmes liés aux technologies open source de la [fonctionnalité Web Apps d’Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span><span class="sxs-lookup"><span data-stu-id="77f43-104">This article has answers to frequently asked questions (FAQs) about issues with open-source technologies for the [Web Apps feature of Azure App Service](https://azure.microsoft.com/services/app-service/web/).</span></span>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="my-cleardb-database-is-down-how-do-i-resolve-this"></a><span data-ttu-id="77f43-105">Ma base de données ClearDB est hors service.</span><span class="sxs-lookup"><span data-stu-id="77f43-105">My ClearDB database is down.</span></span> <span data-ttu-id="77f43-106">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="77f43-106">How do I resolve this?</span></span>

<span data-ttu-id="77f43-107">Contactez le [support ClearDB](https://www.cleardb.com/developers/help/support) pour tout problème lié à la base de données.</span><span class="sxs-lookup"><span data-stu-id="77f43-107">For database-related issues, contact [ClearDB support](https://www.cleardb.com/developers/help/support).</span></span> 

<span data-ttu-id="77f43-108">Pour obtenir des réponses aux questions courantes sur ClearDB, consultez le [FAQ ClearDB](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="77f43-108">For answers to common questions about ClearDB, see [ClearDB FAQs](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-isnt-my-cleardb-database-listed-in-the-portal"></a><span data-ttu-id="77f43-109">Pourquoi ma base de données ClearDB n’est-elle pas répertoriée dans le portail ?</span><span class="sxs-lookup"><span data-stu-id="77f43-109">Why isn't my ClearDB database listed in the portal?</span></span>

<span data-ttu-id="77f43-110">Si vous créez une base de données ClearDB dans le [portail Azure](http://portal.azure.com/), celle-ci ne s’affiche pas dans le [portail Azure Classic](http://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="77f43-110">If you create a ClearDB database in the [Azure portal](http://portal.azure.com/), the database doesn't appear in the [Azure classic portal](http://manage.windowsazure.com/).</span></span> <span data-ttu-id="77f43-111">Pour contourner ce problème, vous pouvez associer manuellement votre base de données à l’application web.</span><span class="sxs-lookup"><span data-stu-id="77f43-111">To work around this, you can manually link your database to the web app.</span></span>

<span data-ttu-id="77f43-112">De même, si vous créez une base de données ClearDB dans le [portail Azure Classic](http://manage.windowsazure.com/), celle-ci ne s’affiche pas dans le [portail Azure](http://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="77f43-112">Similarly, if you create a ClearDB database in the [Azure classic portal](http://manage.windowsazure.com/),  you won't see your database in the [Azure portal](http://portal.azure.com/).</span></span> <span data-ttu-id="77f43-113">Dans ce cas, aucune solution de contournement n’est disponible.</span><span class="sxs-lookup"><span data-stu-id="77f43-113">In this case, no workaround is available.</span></span> 

<span data-ttu-id="77f43-114">Pour plus d’informations, consultez [FAQ sur les bases de données MySQL ClearDB avec Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="77f43-114">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="why-wasnt-my-cleardb-database-migrated-during-my-subscription-migration"></a><span data-ttu-id="77f43-115">Pourquoi ma base de données ClearDB n’a-t-elle pas été migrée pendant la migration de mon abonnement ?</span><span class="sxs-lookup"><span data-stu-id="77f43-115">Why wasn't my ClearDB database migrated during my subscription migration?</span></span>

<span data-ttu-id="77f43-116">Lorsque vous effectuez la migration de ressources entre différents abonnements, certaines limitations s’appliquent.</span><span class="sxs-lookup"><span data-stu-id="77f43-116">When you perform resource migration across subscriptions, some limitations apply.</span></span> <span data-ttu-id="77f43-117">Une base de données MySQL ClearDB est un service tiers. Elle n’est donc pas migrée lors de la migration d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="77f43-117">A ClearDB MySQL database is a third-party service and is not migrated during an Azure subscription migration.</span></span>

<span data-ttu-id="77f43-118">Si vous ne gérez pas la migration de votre base de données MySQL avant la migration des ressources Azure, votre base de données MySQL ClearDB pourrait ne plus être disponible.</span><span class="sxs-lookup"><span data-stu-id="77f43-118">If you don't manage the migration of your MySQL database before you migrate your Azure resources, your ClearDB MySQL database might be unavailable.</span></span> <span data-ttu-id="77f43-119">Pour éviter cela, commencez par migrer manuellement votre base de données ClearDB, puis migrez l’abonnement Azure de votre application web.</span><span class="sxs-lookup"><span data-stu-id="77f43-119">To avoid this, first, manually migrate your ClearDB database, and then migrate the Azure subscription for your web app.</span></span>

<span data-ttu-id="77f43-120">Pour plus d’informations, consultez [FAQ sur les bases de données MySQL ClearDB avec Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span><span class="sxs-lookup"><span data-stu-id="77f43-120">For more information, see [FAQs for ClearDB MySQL databases with Azure App Service](https://docs.microsoft.com/azure/store-cleardb-faq/).</span></span>

## <a name="how-do-i-turn-on-php-logging-to-troubleshoot-php-issues"></a><span data-ttu-id="77f43-121">Comment activer la journalisation PHP pour résoudre les problèmes PHP ?</span><span class="sxs-lookup"><span data-stu-id="77f43-121">How do I turn on PHP logging to troubleshoot PHP issues?</span></span>

<span data-ttu-id="77f43-122">Pour activer la journalisation PHP :</span><span class="sxs-lookup"><span data-stu-id="77f43-122">To turn on PHP logging:</span></span>

1. <span data-ttu-id="77f43-123">Connectez-vous à votre [site web Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="77f43-123">Sign in to your [Kudu website](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
2. <span data-ttu-id="77f43-124">Dans le menu principal, sélectionnez **Console de débogage** > **CMD**.</span><span class="sxs-lookup"><span data-stu-id="77f43-124">In the top menu, select **Debug Console** > **CMD**.</span></span>
3. <span data-ttu-id="77f43-125">Sélectionnez le dossier **Site**.</span><span class="sxs-lookup"><span data-stu-id="77f43-125">Select the **Site** folder.</span></span>
4. <span data-ttu-id="77f43-126">Sélectionnez le dossier **wwwroot**.</span><span class="sxs-lookup"><span data-stu-id="77f43-126">Select the **wwwroot** folder.</span></span>
5. <span data-ttu-id="77f43-127">Sélectionnez l’icône **+**, puis sélectionnez **Nouveau fichier**.</span><span class="sxs-lookup"><span data-stu-id="77f43-127">Select the **+** icon, and then select **New File**.</span></span>
6. <span data-ttu-id="77f43-128">Définissez le nom de fichier sur **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="77f43-128">Set the file name to **.user.ini**.</span></span>
7. <span data-ttu-id="77f43-129">Sélectionnez l’icône du crayon en regard de **.user.ini**.</span><span class="sxs-lookup"><span data-stu-id="77f43-129">Select the pencil icon next to **.user.ini**.</span></span>
8. <span data-ttu-id="77f43-130">Dans le fichier, ajoutez ce code : `log_errors=on`</span><span class="sxs-lookup"><span data-stu-id="77f43-130">In the file, add this code: `log_errors=on`</span></span>
9. <span data-ttu-id="77f43-131">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="77f43-131">Select **Save**.</span></span>
10. <span data-ttu-id="77f43-132">Sélectionnez l’icône du crayon en regard de **wp-config.php**.</span><span class="sxs-lookup"><span data-stu-id="77f43-132">Select the pencil icon next to **wp-config.php**.</span></span>
11. <span data-ttu-id="77f43-133">Remplacez le texte par le code suivant :</span><span class="sxs-lookup"><span data-stu-id="77f43-133">Change the text to the following code:</span></span>
   ```
   //Enable WP_DEBUG modedefine('WP_DEBUG', true);//Enable debug logging to /wp-content/debug.logdefine('WP_DEBUG_LOG', true);
   //Supress errors and warnings to screendefine('WP_DEBUG_DISPLAY', false);//Supress PHP errors to screenini_set('display_errors', 0);
   ```
12. <span data-ttu-id="77f43-134">Dans le portail Azure, dans le menu de l’application web, redémarrez votre application web.</span><span class="sxs-lookup"><span data-stu-id="77f43-134">In the Azure portal, in the web app menu, restart your web app.</span></span>

<span data-ttu-id="77f43-135">Pour plus d’informations, consultez [Activer les journaux d’erreurs WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span><span class="sxs-lookup"><span data-stu-id="77f43-135">For more information, see [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

## <a name="how-do-i-log-python-application-errors-in-apps-that-are-hosted-in-app-service"></a><span data-ttu-id="77f43-136">Comment journaliser les erreurs d’application Python dans des applications hébergées dans App Service ?</span><span class="sxs-lookup"><span data-stu-id="77f43-136">How do I log Python application errors in apps that are hosted in App Service?</span></span>

<span data-ttu-id="77f43-137">Pour capturer les erreurs d’application Python :</span><span class="sxs-lookup"><span data-stu-id="77f43-137">To capture Python application errors:</span></span>

1. <span data-ttu-id="77f43-138">Dans le portail Azure, dans votre application web, sélectionnez **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="77f43-138">In the Azure portal, in your web app, select **Settings**.</span></span>
2. <span data-ttu-id="77f43-139">Sous l’onglet **Paramètres**, sélectionnez **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="77f43-139">On the **Settings** tab, select **Application settings**.</span></span>
3. <span data-ttu-id="77f43-140">Sous **Paramètres de l’application**, entrez la paire clé/valeur suivante :</span><span class="sxs-lookup"><span data-stu-id="77f43-140">Under **App settings**, enter the following key/value pair:</span></span>
    * <span data-ttu-id="77f43-141">Clé : WSGI_LOG</span><span class="sxs-lookup"><span data-stu-id="77f43-141">Key : WSGI_LOG</span></span>
    * <span data-ttu-id="77f43-142">Valeur : D:\home\site\wwwroot\logs.txt (entrez le nom de fichier de votre choix)</span><span class="sxs-lookup"><span data-stu-id="77f43-142">Value : D:\home\site\wwwroot\logs.txt (enter your choice of file name)</span></span>

<span data-ttu-id="77f43-143">Les erreurs doivent maintenant être journalisées dans le fichier logs.txt du dossier wwwroot.</span><span class="sxs-lookup"><span data-stu-id="77f43-143">You should now see errors in the logs.txt file in the wwwroot folder.</span></span>

## <a name="how-do-i-change-the-version-of-the-nodejs-application-that-is-hosted-in-app-service"></a><span data-ttu-id="77f43-144">Comment modifier la version de l’application Node.js hébergée dans App Service ?</span><span class="sxs-lookup"><span data-stu-id="77f43-144">How do I change the version of the Node.js application that is hosted in App Service?</span></span>

<span data-ttu-id="77f43-145">Pour modifier la version de l’application Node.js, vous pouvez utiliser l’une des options suivantes :</span><span class="sxs-lookup"><span data-stu-id="77f43-145">To change the version of the Node.js application, you can use one of the following options:</span></span>

*   <span data-ttu-id="77f43-146">Dans le portail Azure, utilisez **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="77f43-146">In the Azure portal, use **App settings**.</span></span>
    1. <span data-ttu-id="77f43-147">Dans le portail Azure, accédez à votre application web.</span><span class="sxs-lookup"><span data-stu-id="77f43-147">In the Azure portal, go to your web app.</span></span>
    2. <span data-ttu-id="77f43-148">Dans le panneau **Paramètres**, sélectionnez **Paramètres de l’application**.</span><span class="sxs-lookup"><span data-stu-id="77f43-148">On the **Settings** blade, select **Application settings**.</span></span>
    3. <span data-ttu-id="77f43-149">Dans **Paramètres de l’application**, vous pouvez inclure WEBSITE_NODE_DEFAULT_VERSION en tant que clé et la version de Node.js souhaitée en tant que valeur.</span><span class="sxs-lookup"><span data-stu-id="77f43-149">In **App settings**, you can include WEBSITE_NODE_DEFAULT_VERSION as the key, and the version of Node.js you want as the value.</span></span>
    4. <span data-ttu-id="77f43-150">Accédez à votre [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net).</span><span class="sxs-lookup"><span data-stu-id="77f43-150">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net).</span></span>
    5. <span data-ttu-id="77f43-151">Pour vérifier la version de Node.js, entrez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="77f43-151">To check the Node.js version, enter the following command:</span></span>  
   ```
   node -v
   ```
*   <span data-ttu-id="77f43-152">Modifiez le fichier iisnode.yml.</span><span class="sxs-lookup"><span data-stu-id="77f43-152">Modify the iisnode.yml file.</span></span> <span data-ttu-id="77f43-153">La modification de la version de Node.js dans le fichier iisnode.yml configure uniquement l’environnement d’exécution utilisé par iisnode.</span><span class="sxs-lookup"><span data-stu-id="77f43-153">Changing the Node.js version in the iisnode.yml file only sets the runtime environment that iisnode uses.</span></span> <span data-ttu-id="77f43-154">Votre cmd Kudu et le reste utilisent toujours la version de Node.js définie sous **Paramètres de l’application** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="77f43-154">Your Kudu cmd and others still use the Node.js version that is set in **App settings** in the Azure portal.</span></span>

    <span data-ttu-id="77f43-155">Pour définir le fichier iisnode.yml manuellement, créez un fichier iisnode.yml dans le dossier racine de votre application.</span><span class="sxs-lookup"><span data-stu-id="77f43-155">To set the iisnode.yml manually, create an iisnode.yml file in your app root folder.</span></span> <span data-ttu-id="77f43-156">Incluez la ligne suivante dans le fichier :</span><span class="sxs-lookup"><span data-stu-id="77f43-156">In the file, include the following line:</span></span>
   ```
   nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
   ```
   
*   <span data-ttu-id="77f43-157">Définissez le fichier iisnode.yml à l’aide de package.json durant le déploiement de contrôle de code source.</span><span class="sxs-lookup"><span data-stu-id="77f43-157">Set the iisnode.yml file by using package.json during source control deployment.</span></span>
    <span data-ttu-id="77f43-158">Le processus de déploiement de contrôle de code source Azure implique les étapes suivantes :</span><span class="sxs-lookup"><span data-stu-id="77f43-158">The Azure source control deployment process involves the following steps:</span></span>
    1. <span data-ttu-id="77f43-159">Déplace le contenu vers l’application web Azure.</span><span class="sxs-lookup"><span data-stu-id="77f43-159">Moves content to the Azure web app.</span></span>
    2. <span data-ttu-id="77f43-160">Crée un script de déploiement par défaut, s’il n’en existe pas (fichiers deploy.cmd, .deployment) dans le dossier racine de l’application web.</span><span class="sxs-lookup"><span data-stu-id="77f43-160">Creates a default deployment script, if there isn’t one (deploy.cmd, .deployment files) in the web app root folder.</span></span>
    3. <span data-ttu-id="77f43-161">Exécute un script de déploiement dans lequel il crée un fichier iisnode.yml si vous indiquez la version de Node.js dans le fichier package.json > moteur `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span><span class="sxs-lookup"><span data-stu-id="77f43-161">Runs a deployment script in which it creates an iisnode.yml file if you mention the Node.js version in the package.json file > engine `"engines": {"node": "5.9.1","npm": "3.7.3"}`</span></span>
    4. <span data-ttu-id="77f43-162">Le fichier iisnode.yml contient la ligne de code suivante :</span><span class="sxs-lookup"><span data-stu-id="77f43-162">The iisnode.yml file has the following line of code:</span></span>
        ```
        nodeProcessCommandLine: "D:\Program Files (x86)\nodejs\5.9.1\node.exe"
        ```

## <a name="i-see-the-message-error-establishing-a-database-connection-in-my-wordpress-app-thats-hosted-in-app-service-how-do-i-troubleshoot-this"></a><span data-ttu-id="77f43-163">Le message « Erreur lors de l’établissement d’une connexion à la base de données » s’affiche dans mon application WordPress qui est hébergée dans App Service.</span><span class="sxs-lookup"><span data-stu-id="77f43-163">I see the message "Error establishing a database connection" in my WordPress app that's hosted in App Service.</span></span> <span data-ttu-id="77f43-164">Comment puis-je résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="77f43-164">How do I troubleshoot this?</span></span>

<span data-ttu-id="77f43-165">Si cette erreur s’affiche dans votre application Azure WordPress, exécutez les étapes détaillées dans [Activer les journaux d’erreurs WordPress](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/) pour activer php_errors.log et debug.log.</span><span class="sxs-lookup"><span data-stu-id="77f43-165">If you see this error in your Azure WordPress app, to enable php_errors.log and debug.log, complete the steps detailed in [Enable WordPress error logs](https://blogs.msdn.microsoft.com/azureossds/2015/10/09/logging-php-errors-in-wordpress-2/).</span></span>

<span data-ttu-id="77f43-166">Lorsque les journaux sont activés, reproduisez l’erreur, puis vérifiez les journaux pour voir si le nombre de connexions disponible est épuisé :</span><span class="sxs-lookup"><span data-stu-id="77f43-166">When the logs are enabled, reproduce the error, and then check the logs to see if you are running out of connections:</span></span>
```
[09-Oct-2015 00:03:13 UTC] PHP Warning: mysqli_real_connect(): (HY000/1226): User ‘abcdefghijk79' has exceeded the ‘max_user_connections’ resource (current value: 4) in D:\home\site\wwwroot\wp-includes\wp-db.php on line 1454
```

<span data-ttu-id="77f43-167">Si cette erreur s’affiche dans vos fichiers debug.log ou php_errors.log, votre application dépasse le nombre de connexions.</span><span class="sxs-lookup"><span data-stu-id="77f43-167">If you see this error in your debug.log or php_errors.log files, your app is exceeding the number of connections.</span></span> <span data-ttu-id="77f43-168">Si l’hébergement s’effectue sur ClearDB, vérifiez le nombre de connexions disponibles dans votre [plan de service](https://www.cleardb.com/pricing.view).</span><span class="sxs-lookup"><span data-stu-id="77f43-168">If you’re hosting on ClearDB, verify the number of connections that are available in your [service plan](https://www.cleardb.com/pricing.view).</span></span>

## <a name="how-do-i-debug-a-nodejs-app-thats-hosted-in-app-service"></a><span data-ttu-id="77f43-169">Comment déboguer une application Node.js hébergée dans App Service ?</span><span class="sxs-lookup"><span data-stu-id="77f43-169">How do I debug a Node.js app that's hosted in App Service?</span></span>

1.  <span data-ttu-id="77f43-170">Accédez à votre [console Kudu](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span><span class="sxs-lookup"><span data-stu-id="77f43-170">Go to your [Kudu console](https://*yourwebsitename*.scm.azurewebsites.net/DebugConsole).</span></span>
2.  <span data-ttu-id="77f43-171">Accédez à votre dossier de journaux d’application (D:\home\LogFiles\Application).</span><span class="sxs-lookup"><span data-stu-id="77f43-171">Go to your application logs folder (D:\home\LogFiles\Application).</span></span>
3.  <span data-ttu-id="77f43-172">Vérifiez le contenu du fichier logging_errors.txt.</span><span class="sxs-lookup"><span data-stu-id="77f43-172">In the logging_errors.txt file, check for content.</span></span>

## <a name="how-do-i-install-native-python-modules-in-an-app-service-web-app-or-api-app"></a><span data-ttu-id="77f43-173">Comment installer des modules Python natifs dans une application web App Service ou une application API ?</span><span class="sxs-lookup"><span data-stu-id="77f43-173">How do I install native Python modules in an App Service web app or API app?</span></span>

<span data-ttu-id="77f43-174">Certains packages ne peuvent pas être installés à l’aide de PIP dans Azure.</span><span class="sxs-lookup"><span data-stu-id="77f43-174">Some packages might not install by using pip in Azure.</span></span> <span data-ttu-id="77f43-175">Le package n’est peut-être pas disponible dans l’index de package Python ou un compilateur peut être nécessaire (aucun compilateur n’est disponible sur l’ordinateur qui exécute l’application web dans App Service).</span><span class="sxs-lookup"><span data-stu-id="77f43-175">The package might not be available on the Python Package Index, or a compiler might be required (a compiler is not available on the computer that is running the web app in App Service).</span></span> <span data-ttu-id="77f43-176">Pour plus d’informations sur l’installation des modules natifs dans App Service Web Apps et API Apps, consultez [Installer des modules Python dans App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span><span class="sxs-lookup"><span data-stu-id="77f43-176">For information about installing native modules in App Service web apps and API apps, see [Install Python modules in App Service](https://blogs.msdn.microsoft.com/azureossds/2015/06/29/install-native-python-modules-on-azure-web-apps-api-apps/).</span></span>

## <a name="how-do-i-deploy-a-django-app-to-app-service-by-using-git-and-the-new-version-of-python"></a><span data-ttu-id="77f43-177">Comment déployer une application Django dans App Service à l’aide de Git et de la nouvelle version de Python ?</span><span class="sxs-lookup"><span data-stu-id="77f43-177">How do I deploy a Django app to App Service by using Git and the new version of Python?</span></span>

<span data-ttu-id="77f43-178">Pour plus d’informations sur l’installation de Django, consultez [Déploiement d’une application Django dans App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span><span class="sxs-lookup"><span data-stu-id="77f43-178">For information about installing Django, see [Deploying a Django app to App Service](https://blogs.msdn.microsoft.com/azureossds/2016/08/25/deploying-django-app-to-azure-app-services-using-git-and-new-version-of-python/).</span></span>

## <a name="where-are-the-tomcat-log-files-located"></a><span data-ttu-id="77f43-179">Où se trouvent les fichiers journaux Tomcat ?</span><span class="sxs-lookup"><span data-stu-id="77f43-179">Where are the Tomcat log files located?</span></span>

<span data-ttu-id="77f43-180">Pour les déploiements personnalisés et la Place de marché Azure :</span><span class="sxs-lookup"><span data-stu-id="77f43-180">For Azure Marketplace and custom deployments:</span></span>

* <span data-ttu-id="77f43-181">Emplacement du dossier : D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span><span class="sxs-lookup"><span data-stu-id="77f43-181">Folder location: D:\home\site\wwwroot\bin\apache-tomcat-8.0.33\logs</span></span>
* <span data-ttu-id="77f43-182">Fichiers d’intérêt :</span><span class="sxs-lookup"><span data-stu-id="77f43-182">Files of interest:</span></span>
    * <span data-ttu-id="77f43-183">catalina.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-183">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-184">host-manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-184">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-185">localhost.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-185">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-186">manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-186">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-187">site_access_log.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-187">site_access_log.*yyyy-mm-dd*.log</span></span>


<span data-ttu-id="77f43-188">Pour les déploiements **Paramètres de l’application** dans le portail :</span><span class="sxs-lookup"><span data-stu-id="77f43-188">For portal **App settings** deployments:</span></span>

* <span data-ttu-id="77f43-189">Emplacement du dossier : D:\home\LogFiles</span><span class="sxs-lookup"><span data-stu-id="77f43-189">Folder location: D:\home\LogFiles</span></span>
* <span data-ttu-id="77f43-190">Fichiers d’intérêt :</span><span class="sxs-lookup"><span data-stu-id="77f43-190">Files of interest:</span></span>
    * <span data-ttu-id="77f43-191">catalina.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-191">catalina.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-192">host-manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-192">host-manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-193">localhost.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-193">localhost.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-194">manager.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-194">manager.*yyyy-mm-dd*.log</span></span>
    * <span data-ttu-id="77f43-195">site_access_log.*aaaa-mm-jj*.log</span><span class="sxs-lookup"><span data-stu-id="77f43-195">site_access_log.*yyyy-mm-dd*.log</span></span>

## <a name="how-do-i-troubleshoot-jdbc-driver-connection-errors"></a><span data-ttu-id="77f43-196">Comment résoudre les erreurs de connexion du pilote JDBC ?</span><span class="sxs-lookup"><span data-stu-id="77f43-196">How do I troubleshoot JDBC driver connection errors?</span></span>

<span data-ttu-id="77f43-197">Le message suivant peut s’afficher dans vos journaux Tomcat :</span><span class="sxs-lookup"><span data-stu-id="77f43-197">You might see the following message in your Tomcat logs:</span></span>

```
The web application[ROOT] registered the JDBC driver [com.mysql.jdbc.Driver] but failed to unregister it when the web application was stopped. To prevent a memory leak,the JDBC Driver has been forcibly unregistered
```

<span data-ttu-id="77f43-198">Pour résoudre l’erreur :</span><span class="sxs-lookup"><span data-stu-id="77f43-198">To resolve the error:</span></span>

1. <span data-ttu-id="77f43-199">Supprimez le fichier sqljdbc*.jar du dossier app/lib.</span><span class="sxs-lookup"><span data-stu-id="77f43-199">Remove the sqljdbc*.jar file from your app/lib folder.</span></span>
2. <span data-ttu-id="77f43-200">Si vous utilisez le serveur web Tomcat ou Place de marché Azure Tomcat personnalisé, copiez ce fichier .jar dans le dossier lib de Tomcat.</span><span class="sxs-lookup"><span data-stu-id="77f43-200">If you are using the custom Tomcat or Azure Marketplace Tomcat web server, copy this .jar file to the Tomcat lib folder.</span></span>
3. <span data-ttu-id="77f43-201">Si vous activez Java à partir du portail Azure (sélectionnez **Java 1.8** > **Serveur Tomcat**), copiez le fichier sqljdbc.*jar dans le dossier parallèle à votre application.</span><span class="sxs-lookup"><span data-stu-id="77f43-201">If you are enabling Java from the Azure portal (select **Java 1.8** > **Tomcat server**), copy the sqljdbc.* jar file in the folder that's parallel to your app.</span></span> <span data-ttu-id="77f43-202">Ensuite, ajoutez le paramètre classpath suivant au fichier web.config :</span><span class="sxs-lookup"><span data-stu-id="77f43-202">Then, add the following classpath setting to the web.config file:</span></span>

    ```
    <httpPlatform>
    <environmentVariables>
    <environmentVariablename ="JAVA_OPTS" value=" -Djava.net.preferIPv4Stack=true
    -Xms128M -classpath %CLASSPATH%;[Path to the sqljdbc*.jarfile]" />
    </environmentVariables>
    </httpPlatform>
    ```

## <a name="why-do-i-see-errors-when-i-attempt-to-copy-live-log-files"></a><span data-ttu-id="77f43-203">Pourquoi des erreurs s’affichent lorsque j’essaye de copier des fichiers journaux en direct ?</span><span class="sxs-lookup"><span data-stu-id="77f43-203">Why do I see errors when I attempt to copy live log files?</span></span>

<span data-ttu-id="77f43-204">Si vous essayez de copier des fichiers journaux en direct pour une application Java (par exemple, Tomcat), cette erreur FTP peut s’afficher :</span><span class="sxs-lookup"><span data-stu-id="77f43-204">If you try to copy live log files for a Java app (for example, Tomcat), you might see this FTP error:</span></span>

```
Error transferring file [filename] Copying files from remote side failed.
    
The process cannot access the file because it is being used by another process.
```

<span data-ttu-id="77f43-205">Le message d’erreur peut varier, selon le client FTP.</span><span class="sxs-lookup"><span data-stu-id="77f43-205">The error message might vary, depending on the FTP client.</span></span>

<span data-ttu-id="77f43-206">Ce problème de verrouillage concerne toutes les applications Java.</span><span class="sxs-lookup"><span data-stu-id="77f43-206">All Java apps have this locking issue.</span></span> <span data-ttu-id="77f43-207">Seul Kudu prend en charge le téléchargement de ce fichier pendant l’exécution de l’application.</span><span class="sxs-lookup"><span data-stu-id="77f43-207">Only Kudu supports downloading this file while the app is running.</span></span>

<span data-ttu-id="77f43-208">Le fait d’arrêter l’application permet à FTP d’accéder à ces fichiers.</span><span class="sxs-lookup"><span data-stu-id="77f43-208">Stopping the app allows FTP access to these files.</span></span>

<span data-ttu-id="77f43-209">Une autre solution consiste à écrire une tâche web qui s’exécute selon une planification et copie ces fichiers dans un répertoire différent.</span><span class="sxs-lookup"><span data-stu-id="77f43-209">Another workaround is to write a WebJob that runs on a schedule and copies these files to a different directory.</span></span> <span data-ttu-id="77f43-210">Pour obtenir un exemple, consultez le projet [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob).</span><span class="sxs-lookup"><span data-stu-id="77f43-210">For a sample project, see the [CopyLogsJob](https://github.com/kamilsykora/CopyLogsJob) project.</span></span>

## <a name="where-do-i-find-the-log-files-for-jetty"></a><span data-ttu-id="77f43-211">Où trouver les fichiers journaux pour Jetty ?</span><span class="sxs-lookup"><span data-stu-id="77f43-211">Where do I find the log files for Jetty?</span></span>

<span data-ttu-id="77f43-212">Pour les déploiements personnalisés et Place de marché Azure, le fichier journal se trouve dans le dossier D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs.</span><span class="sxs-lookup"><span data-stu-id="77f43-212">For Marketplace and custom deployments, the log file is in the D:\home\site\wwwroot\bin\jetty-distribution-9.1.2.v20140210\logs folder.</span></span> <span data-ttu-id="77f43-213">Notez que l’emplacement du dossier dépend de la version de Jetty que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="77f43-213">Note that the folder location depends on the version of Jetty you are using.</span></span> <span data-ttu-id="77f43-214">Par exemple, le chemin d’accès fourni ici s’applique à Jetty 9.1.2.</span><span class="sxs-lookup"><span data-stu-id="77f43-214">For example, the path provided here is for Jetty 9.1.2.</span></span> <span data-ttu-id="77f43-215">Recherchez jetty_*AAAA_MM_JJ*.stderrout.log.</span><span class="sxs-lookup"><span data-stu-id="77f43-215">Look for jetty_*YYYY_MM_DD*.stderrout.log.</span></span>

<span data-ttu-id="77f43-216">Pour les déploiements Paramètre de l’application dans le portail, le fichier journal se trouve sous D:\home\LogFiles.</span><span class="sxs-lookup"><span data-stu-id="77f43-216">For portal App Setting deployments, the log file is in D:\home\LogFiles.</span></span> <span data-ttu-id="77f43-217">Recherchez jetty_*AAAA_MM_JJ*.stderrout.log</span><span class="sxs-lookup"><span data-stu-id="77f43-217">Look for jetty_*YYYY_MM_DD*.stderrout.log</span></span>

## <a name="can-i-send-email-from-my-azure-web-app"></a><span data-ttu-id="77f43-218">Puis-je envoyer un e-mail à partir de mon application web Azure ?</span><span class="sxs-lookup"><span data-stu-id="77f43-218">Can I send email from my Azure web app?</span></span>

<span data-ttu-id="77f43-219">App Service ne dispose pas d’une fonctionnalité de messagerie intégrée.</span><span class="sxs-lookup"><span data-stu-id="77f43-219">App Service doesn't have a built-in email feature.</span></span> <span data-ttu-id="77f43-220">Consultez cette [discussion sur le dépassement de capacité de la file](http://stackoverflow.com/questions/17666161/sending-email-from-azure) afin d’obtenir des solutions alternatives pour envoyer un e-mail à partir de votre application.</span><span class="sxs-lookup"><span data-stu-id="77f43-220">For some good alternatives for sending email from your app, see this [Stack Overflow discussion](http://stackoverflow.com/questions/17666161/sending-email-from-azure).</span></span>

## <a name="why-does-my-wordpress-site-redirect-to-another-url"></a><span data-ttu-id="77f43-221">Pourquoi mon site WordPress me redirige-t-il vers une autre URL ?</span><span class="sxs-lookup"><span data-stu-id="77f43-221">Why does my WordPress site redirect to another URL?</span></span>

<span data-ttu-id="77f43-222">Si vous avez récemment migré vers Azure, il est possible que WordPress vous redirige vers l’ancienne URL du domaine.</span><span class="sxs-lookup"><span data-stu-id="77f43-222">If you have recently migrated to Azure, WordPress might redirect to the old domain URL.</span></span> <span data-ttu-id="77f43-223">Cela est dû à un paramètre dans la base de données MySQL.</span><span class="sxs-lookup"><span data-stu-id="77f43-223">This is caused by a setting in the MySQL database.</span></span>

<span data-ttu-id="77f43-224">WordPress Buddy+ est une extension de site Azure que vous pouvez utiliser pour mettre à jour l’URL de redirection directement dans la base de données.</span><span class="sxs-lookup"><span data-stu-id="77f43-224">WordPress Buddy+ is an Azure Site Extension that you can use to update the redirection URL directly in the database.</span></span> <span data-ttu-id="77f43-225">Pour plus d’informations sur l’utilisation de WordPress Buddy+, consultez [Outils WordPress et migration MySQL avec WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="77f43-225">For more information about using WordPress Buddy+, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

<span data-ttu-id="77f43-226">Ou si vous préférez mettre à jour manuellement l’URL de redirection à l’aide de requêtes SQL ou PHPMyAdmin, consultez [WordPress : redirection vers une URL incorrecte](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span><span class="sxs-lookup"><span data-stu-id="77f43-226">Alternatively, if you prefer to manually update the redirection URL by using SQL queries or PHPMyAdmin, see [WordPress: Redirecting to wrong URL](https://blogs.msdn.microsoft.com/azureossds/2016/07/12/wordpress-redirecting-to-wrong-url/).</span></span>

## <a name="how-do-i-change-my-wordpress-sign-in-password"></a><span data-ttu-id="77f43-227">Comment modifier mon mot de passe de connexion à WordPress ?</span><span class="sxs-lookup"><span data-stu-id="77f43-227">How do I change my WordPress sign-in password?</span></span>

<span data-ttu-id="77f43-228">Si vous avez oublié votre mot de passe de connexion à WordPress, vous pouvez utiliser WordPress Buddy+ pour le mettre à jour.</span><span class="sxs-lookup"><span data-stu-id="77f43-228">If you have forgotten your WordPress sign-in password, you can use WordPress Buddy+ to update it.</span></span> <span data-ttu-id="77f43-229">Pour réinitialiser votre mot de passe, installez l’extension de site Azure WordPress Buddy+, puis effectuez les étapes décrites dans [Outils WordPress et migration MySQL avec WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="77f43-229">To reset your password, install the WordPress Buddy+ Azure Site Extension, and then complete the steps described in [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="i-cant-sign-in-to-wordpress-how-do-i-resolve-this"></a><span data-ttu-id="77f43-230">Je ne peux pas me connecter à WordPress.</span><span class="sxs-lookup"><span data-stu-id="77f43-230">I can't sign in to WordPress.</span></span> <span data-ttu-id="77f43-231">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="77f43-231">How do I resolve this?</span></span>

<span data-ttu-id="77f43-232">Si vous ne pouvez pas accéder à WordPress après l’installation d’un plug-in, celui-ci est peut-être défectueux.</span><span class="sxs-lookup"><span data-stu-id="77f43-232">If you find yourself locked out of WordPress after recently installing a plugin, you might have a faulty plugin.</span></span> <span data-ttu-id="77f43-233">WordPress Buddy+ est une extension de site Azure qui peut vous aider à désactiver des plug-ins dans WordPress.</span><span class="sxs-lookup"><span data-stu-id="77f43-233">WordPress Buddy+ is an Azure Site Extension that can help you disable plugins in WordPress.</span></span> <span data-ttu-id="77f43-234">Pour plus d’informations, consultez [Outils WordPress et migration MySQL avec WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span><span class="sxs-lookup"><span data-stu-id="77f43-234">For more information, see [WordPress tools and MySQL migration with WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/).</span></span>

## <a name="how-do-i-migrate-my-wordpress-database"></a><span data-ttu-id="77f43-235">Comment migrer ma base de données WordPress ?</span><span class="sxs-lookup"><span data-stu-id="77f43-235">How do I migrate my WordPress database?</span></span>

<span data-ttu-id="77f43-236">Vous disposez de plusieurs options pour migrer la base de données MySQL connectée à votre site web WordPress :</span><span class="sxs-lookup"><span data-stu-id="77f43-236">You have multiple options for migrating the MySQL database that's connected to your WordPress website:</span></span>

* <span data-ttu-id="77f43-237">Développeurs : utilisez [l’invite de commandes ou PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span><span class="sxs-lookup"><span data-stu-id="77f43-237">Developers: Use the [command prompt or PHPMyAdmin](https://blogs.msdn.microsoft.com/azureossds/2016/03/02/migrating-data-between-mysql-databases-using-kudu-console-azure-app-service/)</span></span>
* <span data-ttu-id="77f43-238">Utilisateurs autres que des développeurs : utilisez [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span><span class="sxs-lookup"><span data-stu-id="77f43-238">Non-developers: Use [WordPress Buddy+](https://blogs.msdn.microsoft.com/azureossds/2016/12/21/wordpress-tools-and-mysql-migration-with-wordpress-buddy/)</span></span>

## <a name="how-do-i-help-make-wordpress-more-secure"></a><span data-ttu-id="77f43-239">Comment sécuriser davantage WordPress ?</span><span class="sxs-lookup"><span data-stu-id="77f43-239">How do I help make WordPress more secure?</span></span>

<span data-ttu-id="77f43-240">Pour en savoir plus sur les meilleures pratiques de sécurité pour WordPress, consultez [Meilleures pratiques relatives à la sécurité de WordPress dans Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span><span class="sxs-lookup"><span data-stu-id="77f43-240">To learn about security best practices for WordPress, see [Best practices for WordPress security in Azure](https://blogs.msdn.microsoft.com/azureossds/2016/12/26/best-practices-for-wordpress-security-on-azure/).</span></span>

## <a name="i-am-trying-to-use-phpmyadmin-and-i-see-the-message-access-denied-how-do-i-resolve-this"></a><span data-ttu-id="77f43-241">J’essaye d’utiliser PHPMyAdmin et le message « Accès refusé » s’affiche.</span><span class="sxs-lookup"><span data-stu-id="77f43-241">I am trying to use PHPMyAdmin, and I see the message “Access denied.”</span></span> <span data-ttu-id="77f43-242">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="77f43-242">How do I resolve this?</span></span>

<span data-ttu-id="77f43-243">Vous pouvez rencontrer ce problème si la fonctionnalité MySQL dans l’application n’est pas encore exécutée dans cette instance d’App Service.</span><span class="sxs-lookup"><span data-stu-id="77f43-243">You might experience this issue if the MySQL in-app feature isn't running yet in this App Service instance.</span></span> <span data-ttu-id="77f43-244">Pour résoudre ce problème, essayez d’accéder à votre site web.</span><span class="sxs-lookup"><span data-stu-id="77f43-244">To resolve the issue, try to access your website.</span></span> <span data-ttu-id="77f43-245">Ceci démarre les processus requis, notamment le processus MySQL dans l’application.</span><span class="sxs-lookup"><span data-stu-id="77f43-245">This starts the required processes, including the MySQL in-app process.</span></span> <span data-ttu-id="77f43-246">Pour vérifier que MySQL dans l’application est en cours d’exécution, vérifiez que mysqld.exe est répertorié dans les processus dans l’Explorateur de processus.</span><span class="sxs-lookup"><span data-stu-id="77f43-246">To verify that MySQL in-app is running, in Process Explorer, ensure that mysqld.exe is listed in the processes.</span></span>

<span data-ttu-id="77f43-247">Après vous être assuré que MySQL dans l’application est en cours d’exécution, essayez d’utiliser PHPMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="77f43-247">After you ensure that MySQL in-app is running, try to use PHPMyAdmin.</span></span>

## <a name="i-get-an-http-403-error-when-i-try-to-import-or-export-my-mysql-in-app-database-by-using-phpmyadmin-how-do-i-resolve-this"></a><span data-ttu-id="77f43-248">J’obtiens une erreur HTTP 403 lorsque j’essaie d’importer ou d’exporter ma base de données MySQL dans l’application à l’aide de PHPMyadmin.</span><span class="sxs-lookup"><span data-stu-id="77f43-248">I get an HTTP 403 error when I try to import or export my MySQL in-app database by using PHPMyadmin.</span></span> <span data-ttu-id="77f43-249">Comment résoudre ce problème ?</span><span class="sxs-lookup"><span data-stu-id="77f43-249">How do I resolve this?</span></span>

<span data-ttu-id="77f43-250">Si vous utilisez une version antérieure de Chrome, vous rencontrez sans doute un bogue connu.</span><span class="sxs-lookup"><span data-stu-id="77f43-250">If you are using an older version of Chrome, you might be experiencing a known bug.</span></span> <span data-ttu-id="77f43-251">Pour résoudre ce problème, mettez à niveau vers une version plus récente de Chrome.</span><span class="sxs-lookup"><span data-stu-id="77f43-251">To resolve the issue, upgrade to a newer version of Chrome.</span></span> <span data-ttu-id="77f43-252">Essayez également d’utiliser un autre navigateur, comme Internet Explorer ou Edge, dans lequel le problème ne se produit pas.</span><span class="sxs-lookup"><span data-stu-id="77f43-252">Also try using a different browser, like Internet Explorer or Edge, where the issue does not occur.</span></span>
