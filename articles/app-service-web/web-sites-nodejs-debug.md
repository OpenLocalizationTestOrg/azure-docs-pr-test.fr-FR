---
title: aaaHow toodebug application web Node.js dans Azure App Service
description: "Découvrez comment toodebug un Node.js web application dans Azure App Service."
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
ms.openlocfilehash: 888ec5c3f92cfc3aeea4ea86005b9b6a0d1306ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodebug-a-nodejs-web-app-in-azure-app-service"></a><span data-ttu-id="b273f-103">Comment toodebug un Node.js web application dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="b273f-103">How toodebug a Node.js web app in Azure App Service</span></span>
<span data-ttu-id="b273f-104">Azure fournit tooassist diagnostics intégrés avec le débogage des applications Node.js hébergées dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) les applications Web.</span><span class="sxs-lookup"><span data-stu-id="b273f-104">Azure provides built-in diagnostics tooassist with debugging Node.js applications hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="b273f-105">Dans cet article, vous allez apprendre comment journalisation tooenable de stdout et stderr, afficher les informations d’erreur dans le navigateur de hello et comment toodownload et affichage des fichiers journaux.</span><span class="sxs-lookup"><span data-stu-id="b273f-105">In this article, you will learn how tooenable logging of stdout and stderr, display error information in hello browser, and how toodownload and view log files.</span></span>

<span data-ttu-id="b273f-106">Le diagnostic des applications Node.js hébergées sur Azure est fourni par [IISNode].</span><span class="sxs-lookup"><span data-stu-id="b273f-106">Diagnostics for Node.js applications hosted on Azure is provided by [IISNode].</span></span> <span data-ttu-id="b273f-107">Alors que cet article décrit les paramètres les plus courants hello pour la collecte des informations de diagnostic, il ne fournit pas une référence complète pour l’utilisation des IISNode.</span><span class="sxs-lookup"><span data-stu-id="b273f-107">While this article discusses hello most common settings for gathering diagnostics information, it does not provide a complete reference for working with IISNode.</span></span> <span data-ttu-id="b273f-108">Pour plus d’informations sur l’utilisation de IISNode, consultez hello [IISNode Readme] sur GitHub.</span><span class="sxs-lookup"><span data-stu-id="b273f-108">For more information on working with IISNode, see hello [IISNode Readme] on GitHub.</span></span>

<a id="enablelogging"></a>

## <a name="enable-logging"></a><span data-ttu-id="b273f-109">Activation de la journalisation</span><span class="sxs-lookup"><span data-stu-id="b273f-109">Enable logging</span></span>
<span data-ttu-id="b273f-110">Par défaut, une application web App Service ne capture que les informations de diagnostic sur les déploiements, comme lorsque vous déployez une application Web à l’aide de Git.</span><span class="sxs-lookup"><span data-stu-id="b273f-110">By default, an App Service web app only captures diagnostic information about deployments, such as when you deploy a web app using Git.</span></span> <span data-ttu-id="b273f-111">Cette information est utile si vous rencontrez un problème lors du déploiement, comme un échec lors de l'installation d'un module référencé dans **package.json**ou si vous utilisez un script de déploiement personnalisé.</span><span class="sxs-lookup"><span data-stu-id="b273f-111">This information is useful if you are having problems during deployment, such as a failure when installing a module referenced in **package.json**, or if you are using a custom deployment script.</span></span>

<span data-ttu-id="b273f-112">tooenable hello journalisation de flux stdout et stderr, vous devez créer un **IISNode.yml** de fichiers à votre application Node.js racine hello et ajoutez hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="b273f-112">tooenable hello logging of stdout and stderr streams, you must create an **IISNode.yml** file at hello root of your Node.js application and add hello following:</span></span>

    loggingEnabled: true

<span data-ttu-id="b273f-113">Cela permet la journalisation de stderr et stdout à partir de votre application Node.js hello.</span><span class="sxs-lookup"><span data-stu-id="b273f-113">This enables hello logging of stderr and stdout from your Node.js application.</span></span>

<span data-ttu-id="b273f-114">Hello **IISNode.yml** fichier peut également être utilisé toocontrol si simplifié des erreurs ou des erreurs des développeurs sont renvoyées toohello navigateur lorsqu’une erreur se produit.</span><span class="sxs-lookup"><span data-stu-id="b273f-114">hello **IISNode.yml** file can also be used toocontrol whether friendly errors or developer errors are returned toohello browser when a failure occurs.</span></span> <span data-ttu-id="b273f-115">erreurs des développeurs tooenable, ajouter hello suivant ligne toohello **IISNode.yml** fichier :</span><span class="sxs-lookup"><span data-stu-id="b273f-115">tooenable developer errors, add hello following line toohello **IISNode.yml** file:</span></span>

    devErrorsEnabled: true

<span data-ttu-id="b273f-116">Une fois cette option est activée, IISNode renvoie hello dernière 64 Ko, des informations envoyées toostderr au lieu d’une erreur conviviale tel que « une erreur interne s’est produite ».</span><span class="sxs-lookup"><span data-stu-id="b273f-116">Once this option is enabled, IISNode will return hello last 64K of information sent toostderr instead of a friendly error such as "an internal server error occurred".</span></span>

> [!NOTE]
> <span data-ttu-id="b273f-117">DevErrorsEnabled est utile lors du diagnostic de problèmes au cours du développement, son activation dans un environnement de production peut entraîner des erreurs de développement envoyés tooend utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="b273f-117">While devErrorsEnabled is useful when diagnosing problems during development, enabling it in a production environment may result in development errors being sent tooend users.</span></span>
> 
> 

<span data-ttu-id="b273f-118">Si hello **IISNode.yml** fichier n’existe pas déjà dans votre application, vous devez redémarrer votre application web après la publication d’application hello mis à jour.</span><span class="sxs-lookup"><span data-stu-id="b273f-118">If hello **IISNode.yml** file did not already exist within your application, you must restart your web app after publishing hello updated application.</span></span> <span data-ttu-id="b273f-119">Si vous modifiez simplement les paramètres dans un fichier **IISNode.yml** existant qui a été publié précédemment, aucun redémarrage n'est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b273f-119">If you are simply changing settings in an existing **IISNode.yml** file that has previously been published, no restart is required.</span></span>

> [!NOTE]
> <span data-ttu-id="b273f-120">Si votre application web a été créée à l’aide des outils de ligne de commande Azure hello ou des applets de commande PowerShell de Azure, une valeur par défaut **IISNode.yml** fichier est créé automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b273f-120">If your web app was created using hello Azure Command-Line Tools or Azure PowerShell Cmdlets, a default **IISNode.yml** file is automatically created.</span></span>
> 
> 

<span data-ttu-id="b273f-121">toorestart hello web application, une application web de hello sélectionnez Bonjour [Azure Portal](https://portal.azure.com), puis cliquez sur **redémarrer** bouton :</span><span class="sxs-lookup"><span data-stu-id="b273f-121">toorestart hello web app, select hello web app in hello [Azure Portal](https://portal.azure.com), and then click **RESTART** button:</span></span>

![bouton redémarrer][restart-button]

<span data-ttu-id="b273f-123">Si les outils de ligne de commande Azure hello sont installés dans votre environnement de développement, vous pouvez utiliser hello suivant commande toorestart hello web app :</span><span class="sxs-lookup"><span data-stu-id="b273f-123">If hello Azure Command-Line Tools are installed in your development environment, you can use hello following command toorestart hello web app:</span></span>

    azure site restart [sitename]

> [!NOTE]
> <span data-ttu-id="b273f-124">LoggingEnabled et devErrorsEnabled sont des options de configuration IISNode.yml hello couramment utilisé pour capturer des informations de diagnostic, IISNode.yml peut être utilisé tooconfigure diverses options pour votre environnement d’hébergement.</span><span class="sxs-lookup"><span data-stu-id="b273f-124">While loggingEnabled and devErrorsEnabled are hello most commonly used IISNode.yml configuration options for capturing diagnostic information, IISNode.yml can be used tooconfigure a variety of options for your hosting environment.</span></span> <span data-ttu-id="b273f-125">Pour obtenir une liste complète des options de configuration hello, consultez hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) fichier.</span><span class="sxs-lookup"><span data-stu-id="b273f-125">For a full list of hello configuration options, see hello [iisnode_schema.xml](https://github.com/tjanczuk/iisnode/blob/master/src/config/iisnode_schema.xml) file.</span></span>
> 
> 

<a id="viewlogs"></a>

## <a name="accessing-logs"></a><span data-ttu-id="b273f-126">Accès aux journaux</span><span class="sxs-lookup"><span data-stu-id="b273f-126">Accessing logs</span></span>
<span data-ttu-id="b273f-127">Journaux de diagnostic sont accessibles de trois manières ; À l’aide de hello Transfer protocole FTP (File), télécharger une archive Zip, ou comme une mise à jour de flux de données du journal de hello (également appelé une fin).</span><span class="sxs-lookup"><span data-stu-id="b273f-127">Diagnostic logs can be accessed in three ways; Using hello File Transfer Protocol (FTP), downloading a Zip archive, or as a live updated stream of hello log (also known as a tail).</span></span> <span data-ttu-id="b273f-128">Téléchargement de l’archive Zip des fichiers journaux de hello hello ou la consultation des flux live de hello nécessitent outils de ligne de commande Azure hello.</span><span class="sxs-lookup"><span data-stu-id="b273f-128">Downloading hello Zip archive of hello log files or viewing hello live stream require hello Azure Command-Line Tools.</span></span> <span data-ttu-id="b273f-129">Elles peuvent être installées à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="b273f-129">These can be installed by using hello following command:</span></span>

    npm install azure-cli -g

<span data-ttu-id="b273f-130">Une fois installé, les outils hello est accessible à l’aide de la commande hello 'azure'.</span><span class="sxs-lookup"><span data-stu-id="b273f-130">Once installed, hello tools can be accessed using hello 'azure' command.</span></span> <span data-ttu-id="b273f-131">outils de ligne de commande de Hello doit d’abord être configuré toouse votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="b273f-131">hello command-line tools must first be configured toouse your Azure subscription.</span></span> <span data-ttu-id="b273f-132">Pour plus d’informations sur comment tooaccomplish cette tâche, consultez hello **comment toodownload et importation de paramètres de publication** section Hello [comment tooUse hello de ligne de commande de Windows Azure Tools](../xplat-cli-connect.md) l’article.</span><span class="sxs-lookup"><span data-stu-id="b273f-132">For information on how tooaccomplish this task, see hello **How toodownload and import publish settings** section of hello [How tooUse hello Azure Command-Line Tools](../xplat-cli-connect.md) article.</span></span>

### <a name="ftp"></a><span data-ttu-id="b273f-133">FTP</span><span class="sxs-lookup"><span data-stu-id="b273f-133">FTP</span></span>
<span data-ttu-id="b273f-134">informations de diagnostic hello tooaccess via FTP, visitez hello [Azure Portal](https://portal.azure.com), sélectionnez votre application web, puis hello **tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="b273f-134">tooaccess hello diagnostic information through FTP, visit hello [Azure Portal](https://portal.azure.com), select your web app, and then select hello **DASHBOARD**.</span></span> <span data-ttu-id="b273f-135">Bonjour **liens rapides** section hello **journaux de DIAGNOSTIC FTP** et **journaux de DIAGNOSTIC FTPS** liens fournissent des journaux de toohello d’accès à l’aide du protocole de hello FTP.</span><span class="sxs-lookup"><span data-stu-id="b273f-135">In hello **quick links** section, hello **FTP DIAGNOSTIC LOGS** and **FTPS DIAGNOSTIC LOGS** links provide access toohello logs using hello FTP protocol.</span></span>

> [!NOTE]
> <span data-ttu-id="b273f-136">Si vous n’avez pas précédemment configuré nom d’utilisateur et mot de passe pour le déploiement ou FTP, vous pouvez le faire à partir de hello **Quickstart** page de gestion en sélectionnant **configurer les informations d’identification de déploiement**.</span><span class="sxs-lookup"><span data-stu-id="b273f-136">If you have not previously configured user name and password for FTP or deployment, you can do so from hello **Quickstart** management page by selecting **Set up deployment credentials**.</span></span>
> 
> 

<span data-ttu-id="b273f-137">Hello URL FTP retournées dans le tableau de bord hello concerne hello **LogFiles** répertoire qui contiendra hello suivant sous-répertoires :</span><span class="sxs-lookup"><span data-stu-id="b273f-137">hello FTP URL returned in hello dashboard is for hello **LogFiles** directory, which will contain hello following sub-directories:</span></span>

* <span data-ttu-id="b273f-138">[Méthode de déploiement](web-sites-deploy.md) -si vous utilisez une méthode de déploiement tels que Git, un répertoire de même nom est créé et qu’il contienne des informations de hello liées toodeployments.</span><span class="sxs-lookup"><span data-stu-id="b273f-138">[Deployment Method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
* <span data-ttu-id="b273f-139">nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).</span><span class="sxs-lookup"><span data-stu-id="b273f-139">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="zip-archive"></a><span data-ttu-id="b273f-140">Archive ZIP</span><span class="sxs-lookup"><span data-stu-id="b273f-140">Zip archive</span></span>
<span data-ttu-id="b273f-141">toodownload une archive Zip des journaux de diagnostic hello, de hello utilisez commande suivante à partir des outils de ligne de commande Azure hello :</span><span class="sxs-lookup"><span data-stu-id="b273f-141">toodownload a Zip archive of hello diagnostic logs, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log download [sitename]

<span data-ttu-id="b273f-142">Cette commande télécharge un **diagnostics.zip** hello répertoire en cours.</span><span class="sxs-lookup"><span data-stu-id="b273f-142">This will download a **diagnostics.zip** in hello current directory.</span></span> <span data-ttu-id="b273f-143">Cette archive contient hello suivant la structure de répertoires :</span><span class="sxs-lookup"><span data-stu-id="b273f-143">This archive contains hello following directory structure:</span></span>

* <span data-ttu-id="b273f-144">deployments : un journal des informations concernant les déploiements de votre application</span><span class="sxs-lookup"><span data-stu-id="b273f-144">deployments - A log of information about deployments of your application</span></span>
* <span data-ttu-id="b273f-145">LogFiles</span><span class="sxs-lookup"><span data-stu-id="b273f-145">LogFiles</span></span>
  
  * <span data-ttu-id="b273f-146">[Méthode de déploiement](web-sites-deploy.md) -si vous utilisez une méthode de déploiement tels que Git, un répertoire de même nom est créé et qu’il contienne des informations de hello liées toodeployments.</span><span class="sxs-lookup"><span data-stu-id="b273f-146">[Deployment method](web-sites-deploy.md) - If you use a deployment method such as Git, a directory of hello same name will be created and will contain information related toodeployments.</span></span>
  * <span data-ttu-id="b273f-147">nodejs : les informations stdout et stderr capturées à partir de toutes les instances de votre application (lorsque loggingEnabled est défini sur true).</span><span class="sxs-lookup"><span data-stu-id="b273f-147">nodejs - Stdout and stderr information captured from all instances of your application (when loggingEnabled is true.)</span></span>

### <a name="live-stream-tail"></a><span data-ttu-id="b273f-148">Flux live (tail)</span><span class="sxs-lookup"><span data-stu-id="b273f-148">Live stream (tail)</span></span>
<span data-ttu-id="b273f-149">tooview un flux en direct des informations du journal de diagnostic, hello utilisez commande suivante à partir des outils de ligne de commande Azure hello :</span><span class="sxs-lookup"><span data-stu-id="b273f-149">tooview a live stream of diagnostic log information, use hello following command from hello Azure Command-Line Tools:</span></span>

    azure site log tail [sitename]

<span data-ttu-id="b273f-150">Cette méthode retourne un flux de données de journaux d’événements sont mis à jour lorsqu’elles se produisent sur le serveur de hello.</span><span class="sxs-lookup"><span data-stu-id="b273f-150">This will return a stream of log events that are updated as they occur on hello server.</span></span> <span data-ttu-id="b273f-151">Ce flux renvoie les informations de déploiement ainsi que les informations relatives à stdout et stderr (lorsque loggingEnabled est défini sur true).</span><span class="sxs-lookup"><span data-stu-id="b273f-151">This stream will return deployment information as well as stdout and stderr information (when loggingEnabled is true.)</span></span>

<a id="nextsteps"></a>

## <a name="next-steps"></a><span data-ttu-id="b273f-152">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b273f-152">Next Steps</span></span>
<span data-ttu-id="b273f-153">Dans cet article vous avez appris comment tooenable et accès aux informations de diagnostic pour Azure.</span><span class="sxs-lookup"><span data-stu-id="b273f-153">In this article you learned how tooenable and access diagnostics information for Azure.</span></span> <span data-ttu-id="b273f-154">Alors que ces informations sont utiles dans les problèmes de présentation qui se produisent avec votre application, il peut pointer problème tooa avec un module que vous utilisez ou que la version de Node.js utilisé par l’application de Service Web Apps hello est différente de celle hello celui utilisé dans votre déploiement environnement.</span><span class="sxs-lookup"><span data-stu-id="b273f-154">While this information is useful in understanding problems that occur with your application, it may point tooa problem with a module you are using or that hello version of Node.js used by App Service Web Apps is different than hello one used in your deployment environment.</span></span>

<span data-ttu-id="b273f-155">Pour plus d'informations sur l'utilisation des modules sur Azure, consultez la page [Utilisation des modules Node.js avec les applications Azure](../nodejs-use-node-modules-azure-apps.md).</span><span class="sxs-lookup"><span data-stu-id="b273f-155">For information in working with modules on Azure, see [Using Node.js Modules with Azure Applications](../nodejs-use-node-modules-azure-apps.md).</span></span>

<span data-ttu-id="b273f-156">Pour plus d'informations sur la spécification d'une version Node.js de votre application, consultez la page [Spécification d'une version de Node.js dans une application Azure].</span><span class="sxs-lookup"><span data-stu-id="b273f-156">For information on specifying a Node.js version for your application, see [Specifying a Node.js version in an Azure application].</span></span>

<span data-ttu-id="b273f-157">Pour plus d’informations, consultez également hello [centre de développement Node.js](/develop/nodejs/).</span><span class="sxs-lookup"><span data-stu-id="b273f-157">For more information, see also hello [Node.js Developer Center](/develop/nodejs/).</span></span>

## <a name="whats-changed"></a><span data-ttu-id="b273f-158">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="b273f-158">What's changed</span></span>
* <span data-ttu-id="b273f-159">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="b273f-159">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

> [!NOTE]
> <span data-ttu-id="b273f-160">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="b273f-160">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="b273f-161">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="b273f-161">No credit cards required; no commitments.</span></span>
> 
> 

[IISNode]: https://github.com/tjanczuk/iisnode
[IISNode Readme]: https://github.com/tjanczuk/iisnode#readme
[How tooUse hello Azure Command-Line Interface]:../cli-install-nodejs.md
[Using Node.js Modules with Azure Applications]: ../nodejs-use-node-modules-azure-apps.md
[Spécification d'une version de Node.js dans une application Azure]: ../nodejs-specify-node-version-azure-apps.md

[restart-button]: ./media/web-sites-nodejs-debug/restartbutton.png

