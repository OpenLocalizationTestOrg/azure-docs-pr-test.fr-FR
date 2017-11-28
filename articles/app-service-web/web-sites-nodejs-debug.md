---
title: "Débogage d’une application web Node.js dans Azure Web Service"
description: "Apprenez à déboguer une application web Node.js dans Azure Web Service."
tags: azure-portal
services: app-service\web
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: a48f906c-1a3e-43bc-ae84-7d2dde175b15
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: 5e302a4c58a171d40e43a22c34c724e868019ec8
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="how-to-debug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="fc4c0-103">Débogage d’une application web Node.js dans Azure Web Service</span><span class="sxs-lookup"><span data-stu-id="fc4c0-103">How to debug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="fc4c0-104">Azure fournit un outil de diagnostic intégré qui vous aide à déboguer les applications Node.js hébergées dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-104">Azure provides built-in diagnostics to assist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="fc4c0-105">Cet article vous explique comment activer la journalisation de stdout et de stderr, comment afficher les informations sur l'erreur dans le navigateur et comment télécharger et afficher les fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-105">In this article, you will learn how to enable logging of stdout and stderr, display error information in the browser, and how to download and view log files.</span></span>

<span data-ttu-id="fc4c0-106">Le diagnostic des applications Node.js hébergées sur Azure est fourni par [IISNode].</span><span class="sxs-lookup"><span data-stu-id="fc4c0-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="fc4c0-107">Bien que les paramètres les plus courants pour la collecte des informations de diagnostic soient abordés, cet article ne fournit pas une référence complète sur l'utilisation de IISNode.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-107">While this article discusses the most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="fc4c0-108">Pour plus d'informations sur l'utilisation de IISNode, consultez le [fichier Lisez-moi IISNode] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-108">For more information on working with IISNode, see the [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="fc4c0-109">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="fc4c0-109">Enable logging</span></span>
<span data-ttu-id="fc4c0-110">Par défaut, une application web App Service ne capture que les informations de diagnostic sur les déploiements, comme lorsque vous déployez une application Web à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="fc4c0-111">Cette information est utile si vous rencontrez un problème lors du déploiement, comme un échec lors de l'installation d'un module référencé dans **package.json**ou si vous utilisez un script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="fc4c0-112">Pour activer la journalisation des flux stdout et stderr, vous devez créer un fichier **IISNode.yml** à la racine de votre application Node.js et ajouter ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-112">To enable the logging of stdout and stderr streams, you must create an **IISNode.yml** file at the root of your Node.js application and add the following:</span></span>

    loggingEnabled: true

<span data-ttu-id="fc4c0-113">Cela active la journalisation de stderr et stdout à partir de votre application Node.js.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-113">This enables the logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="fc4c0-114">Le fichier **IISNode.yml** peut également être utilisé pour contrôler si les erreurs conviviales ou les erreurs de développement sont renvoyées au navigateur lorsqu'un échec se produit.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-114">The **IISNode.yml** file can also be used to control whether friendly errors or developer errors are returned to the browser when a failure occurs.</span></span> <span data-ttu-id="fc4c0-115">Pour activer les erreurs de développement, ajoutez la ligne suivante au fichier **IISNode.yml** :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-115">To enable developer errors, add the following line to the **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="fc4c0-116">Une fois cette option activée, IISNode renvoie les derniers 64 Ko d'informations envoyées à stderr plutôt qu'une erreur conviviale comme « une erreur de serveur interne s'est produite ».</span><span class="sxs-lookup"><span data-stu-id="fc4c0-116">Once this option is enabled, IISNode will return the last 64K of information sent to stderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="fc4c0-117">Bien que devErrorsEnabled soit utile pour diagnostiquer les problèmes lors du développement, l'activer dans un environnement de production peut entraîner l'envoi d'erreurs de développement aux utilisateurs finaux.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent to end users.</span></span>
> 
> 

<span data-ttu-id="fc4c0-118">Si le fichier **IISNode.yml** n’existe pas dans votre application, vous devez redémarrer votre application Web après la publication de l’application mise à jour.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-118">If the **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing the updated application.</span></span> <span data-ttu-id="fc4c0-119">Si vous modifiez simplement les paramètres dans un fichier **IISNode.yml** existant qui a été publié précédemment, aucun redémarrage n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="fc4c0-120">Si votre application Web a été créée à l’aide des outils de ligne en commande Azure ou des applets de commande Azure PowerShell, un fichier **IISNode.yml** par défaut est automatiquement créé.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-120">If your web app was created using the Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="fc4c0-121">Pour redémarrer l’application web, sélectionnez-la dans le [portail Azure](https://portal.azure.com), puis cliquez sur le bouton **REDÉMARRER** :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-121">To restart the web app, select the web app in the [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![bouton redémarrer][restart-button]

<span data-ttu-id="fc4c0-123">Si les outils en ligne de commande Azure sont installés dans votre environnement de développement, vous pouvez utiliser la commande suivante pour redémarrer l’application web :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-123">If the Azure Command-Line Tools are installed in your development environment, you can use the following command to restart the web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="fc4c0-124">Bien que loggingEnabled et devErrorsEnabled soient les options de configuration IISNode.yml les plus fréquemment utilisées pour la capture des informations de diagnostic, IISNode.yml peut être utilisé pour configurer diverses options pour votre environnement d'hébergement.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-124">While loggingEnabled and devErrorsEnabled are the most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used to configure a variety of options for your hosting environment.</span></span> <span data-ttu-id="fc4c0-125">Pour une liste complète des options de configuration, consultez le fichier [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml).</span><span class="sxs-lookup"><span data-stu-id="fc4c0-125">For a full list of the configuration options, see the [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="fc4c0-126">Accès aux journaux</span><span class="sxs-lookup"><span data-stu-id="fc4c0-126">Accessing logs</span></span>
<span data-ttu-id="fc4c0-127">Il existe trois manières d'accéder aux journaux de diagnostic : à l'aide du protocole FTP, en téléchargeant une archive ZIP ou via un flux live mis à jour du journal (également appelé « tail »).</span><span class="sxs-lookup"><span data-stu-id="fc4c0-127">Diagnostic logs can be accessed in three ways; Using the File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of the log (also known as a tail).</span></span> <span data-ttu-id="fc4c0-128">Le téléchargement de l'archive ZIP des fichiers journaux ou l'affichage du flux live requièrent les outils en ligne de commande Azure,</span><span class="sxs-lookup"><span data-stu-id="fc4c0-128">Downloading the Zip archive of the log files or viewing the live stream require the Azure Command-Line Tools.</span></span> <span data-ttu-id="fc4c0-129">que vous pouvez installer à l'aide de la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-129">These can be installed by using the following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="fc4c0-130">Une fois installés, ils sont accessibles à l'aide de la commande « azure ».</span><span class="sxs-lookup"><span data-stu-id="fc4c0-130">Once installed, the tools can be accessed using the 'azure' command.</span></span> <span data-ttu-id="fc4c0-131">Les outils en ligne de commande doivent d’abord être configurés pour utiliser votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-131">The command-line tools must first be configured to use your Azure subscription.</span></span> <span data-ttu-id="fc4c0-132">Pour plus d'informations sur la réalisation de cette tâche, consultez la section **Téléchargement et importation des paramètres de publication** de l'article [Utilisation des outils en ligne de commande Azure](../xplat-cli-connect.md) .</span><span class="sxs-lookup"><span data-stu-id="fc4c0-132">For information on how to accomplish this task, see the **How to download and import publish settings** section of the [How to Use The Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="fc4c0-133">FTP</span><span class="sxs-lookup"><span data-stu-id="fc4c0-133">FTP</span></span>
<span data-ttu-id="fc4c0-134">Pour accéder aux informations de diagnostic via FTP, visitez le [portail Azure](https://portal.azure.com), sélectionnez votre application web, puis sélectionnez le **TABLEAU DE BORD**.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-134">To access the diagnostic information through FTP, visit the [Azure Portal](https://portal.azure.com), select your web app, and then select the **DASHBOARD**.</span></span> <span data-ttu-id="fc4c0-135">Dans la section **liens rapides**, les liens **Journaux de diagnostic FTP** et **Journaux de diagnostic FTPS** permettent d’accéder aux journaux à l’aide du protocole FTP.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-135">In the **quick links** section, the **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access to the logs using the FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="fc4c0-136">Si vous n’avez pas encore configuré un nom d’utilisateur et un mot de passe pour le FTP ou le déploiement, vous pouvez le faire sur la page de gestion **Démarrage rapide**, en sélectionnant **Configurer les informations d’identification du déploiement**.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-136">If you have not previously configured user name and password for FTP or deployment, you can do so from the **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="fc4c0-137">L'URL FTP renvoyée dans le tableau de bord concerne le répertoire **LogFiles** , qui contient les sous-répertoires suivants :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-137">The FTP URL returned in the dashboard is for the **LogFiles** directory, which will contain the following sub-directories:</span></span>

* <span data-ttu-id="fc4c0-138">[Méthode de déploiement](web-sites-deploy.md) : si vous utilisez une méthode de déploiement comme Git, un répertoire de même nom est créé et contient les informations relatives aux déploiements.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
* <span data-ttu-id="fc4c0-139">nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).</span><span class="sxs-lookup"><span data-stu-id="fc4c0-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="fc4c0-140">Archive ZIP</span><span class="sxs-lookup"><span data-stu-id="fc4c0-140">Zip archive</span></span>
<span data-ttu-id="fc4c0-141">Pour télécharger une archive ZIP des journaux de diagnostic, utilisez la commande suivante à partir des outils en ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-141">To download a Zip archive of the diagnostic logs, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="fc4c0-142">Cela télécharge un fichier **diagnostics.zip** dans le répertoire actuel.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-142">This will download a **diagnostics.zip** in the current directory.</span></span> <span data-ttu-id="fc4c0-143">Cette archive contient la structure de répertoires suivante :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-143">This archive contains the following directory structure:</span></span>

* <span data-ttu-id="fc4c0-144">deployments : un journal des informations concernant les déploiements de votre application</span><span class="sxs-lookup"><span data-stu-id="fc4c0-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="fc4c0-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="fc4c0-145">LogFiles</span></span>
  
  * <span data-ttu-id="fc4c0-146">[Méthode de déploiement](web-sites-deploy.md) : si vous utilisez une méthode de déploiement comme Git, un répertoire de même nom est créé et contient les informations relatives aux déploiements.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of the same name will be created and will contain information related to deployments.</span></span>
  * <span data-ttu-id="fc4c0-147">nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).</span><span class="sxs-lookup"><span data-stu-id="fc4c0-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="fc4c0-148">Flux live (tail)</span><span class="sxs-lookup"><span data-stu-id="fc4c0-148">Live stream (tail)</span></span>
<span data-ttu-id="fc4c0-149">Pour afficher un flux live des informations du journal de diagnostic, utilisez la commande suivante à partir des outils en ligne de commande Azure :</span><span class="sxs-lookup"><span data-stu-id="fc4c0-149">To view a live stream of diagnostic log information, use the following command from the Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="fc4c0-150">Cela renvoie un flux d'événements de journal qui sont mis à jour lorsqu'ils se produisent sur le serveur.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-150">This will return a stream of log events that are updated as they occur on the server.</span></span> <span data-ttu-id="fc4c0-151">Ce flux renvoie les informations de déploiement ainsi que les informations relatives à stdout et stderr (lorsque loggingEnabled est défini sur true).</span><span class="sxs-lookup"><span data-stu-id="fc4c0-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="fc4c0-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="fc4c0-152">Next Steps</span></span>
<span data-ttu-id="fc4c0-153">Cet article vous a montré comment activer les informations de diagnostic pour Azure et comment y accéder.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-153">In this article you learned how to enable and access diagnostics information for Azure.</span></span> <span data-ttu-id="fc4c0-154">Bien que ces informations soient utiles pour comprendre les problèmes qui surviennent avec votre application, elles peuvent signaler un problème avec un module que vous utilisez ou la version de Node.js utilisée par App Services Web Apps qui est différente de celle utilisée dans votre environnement de déploiement.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-154">While this information is useful in understanding problems that occur with your application, it may point to a problem with a module you are using or that the version of Node.js used by App Service Web Apps is different than the one used in your deployment environment.</span></span>

<span data-ttu-id="fc4c0-155">Pour plus d'informations sur l'utilisation des modules sur Azure, consultez la page [Utilisation des modules Node.js avec les applications Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="fc4c0-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="fc4c0-156">Pour plus d'informations sur la spécification d'une version Node.js de votre application, consultez la page [Spécification d'une version de Node.js dans une application Azure].</span><span class="sxs-lookup"><span data-stu-id="fc4c0-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="fc4c0-157">Pour plus d'informations, consultez aussi le [Centre pour développeurs Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="fc4c0-157">For more information, see also the [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="fc4c0-158">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="fc4c0-158">What's changed</span></span>
* <span data-ttu-id="fc4c0-159">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="fc4c0-159">For a guide to the change from Websites to App Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="fc4c0-160">Si vous voulez vous familiariser avec Azure App Service avant d’ouvrir un compte Azure, accédez à la page [Essayer App Service](https://azure.microsoft.com/try/app-service/), où vous pourrez créer immédiatement une application web temporaire dans App Service.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-160">If you want to get started with Azure App Service before signing up for an Azure account, go to [Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="fc4c0-161">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="fc4c0-161">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="fc4c0-162">[IISNode]: https://github.com/tjanczuk/iisnode</span><span class="sxs-lookup"><span data-stu-id="fc4c0-162">[IISNode]: https://github.com/tjanczuk/iisnode</span></span>
<span data-ttu-id="fc4c0-163">[fichier Lisez-moi IISNode]: https://github.com/tjanczuk/iisnode#readme</span><span class="sxs-lookup"><span data-stu-id="fc4c0-163">[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme</span></span>
[How to Use The Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
<span data-ttu-id="fc4c0-164">[Spécification d'une version de Node.js dans une application Azure]: ../nodejs-specify-node-version-azure-apps.md</span><span class="sxs-lookup"><span data-stu-id="fc4c0-164">[Specifying a Node.js version in an Azure application]: ../nodejs-specify-node-version-azure-apps.md</span></span>

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

