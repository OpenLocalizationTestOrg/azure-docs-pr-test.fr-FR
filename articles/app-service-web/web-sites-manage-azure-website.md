---
title: aaaManage une application web dans Azure App Service
description: "Tooresources de liens pour la gestion d’une application web dans Azure App Service."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="dc002-103">Gérer une application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dc002-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="dc002-104">Cette rubrique contient des tooresources de liens pour la gestion d’une application web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="dc002-104">This topic contains links tooresources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="dc002-105">La gestion inclut toutes les tâches hello qui maintenir votre application web fonctionne correctement.</span><span class="sxs-lookup"><span data-stu-id="dc002-105">Management includes all of hello tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="dc002-106">Sur la durée de vie hello d’une application web, vous effectuerez des différentes tâches de gestion, que vous passez de l’opération toonormal de déploiement initial, la maintenance et les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="dc002-106">Over hello lifetime of a web app, you will perform different management tasks, as you move from initial deployment toonormal operation, maintenance, and updates.</span></span>

<span data-ttu-id="dc002-107">Plusieurs tâches de gestion d’application web peuvent être effectuées dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="dc002-107">Many web app management tasks can be performed in hello Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-tooproduction"></a><span data-ttu-id="dc002-108">Avant de déployer votre tooproduction d’application web</span><span class="sxs-lookup"><span data-stu-id="dc002-108">Before you deploy your web app tooproduction</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="dc002-109">Choisir un niveau</span><span class="sxs-lookup"><span data-stu-id="dc002-109">Choose a tier</span></span>
<span data-ttu-id="dc002-110">Azure App Service est disponibles en cinq niveaux : Gratuit, Partagé, De base, Standard et Premium.</span><span class="sxs-lookup"><span data-stu-id="dc002-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="dc002-111">Pour plus d’informations sur les fonctions hello et pour chaque niveau de tarification, consultez [tarification](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="dc002-111">For information about hello features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="dc002-112">[Plans de Service d’applications](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) vous permet de regrouper plusieurs applications web sous hello même niveau.</span><span class="sxs-lookup"><span data-stu-id="dc002-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under hello same tier.</span></span>
* <span data-ttu-id="dc002-113">Vous avez toujours la possibilité de [changer de niveau](web-sites-scale.md) après avoir créé l’application web.</span><span class="sxs-lookup"><span data-stu-id="dc002-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="dc002-114">Configuration</span><span class="sxs-lookup"><span data-stu-id="dc002-114">Configuration</span></span>
<span data-ttu-id="dc002-115">Hello d’utilisation [Azure Portal](https://portal.azure.com/) tooset différentes options de configuration.</span><span class="sxs-lookup"><span data-stu-id="dc002-115">Use hello [Azure Portal](https://portal.azure.com/) tooset various configuration options.</span></span> <span data-ttu-id="dc002-116">Pour plus d’informations, consultez la page [Configurer des applications web dans Azure App Service](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="dc002-117">Voici une liste de vérification rapide :</span><span class="sxs-lookup"><span data-stu-id="dc002-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="dc002-118">Sélectionnez **Versions exécutables** pour .NET, PHP, Java ou Python, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="dc002-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="dc002-119">Activer **WebSockets** si votre application web utilise le protocole WebSocket de hello.</span><span class="sxs-lookup"><span data-stu-id="dc002-119">Enable **WebSockets** if your web app uses hello WebSocket protocol.</span></span> <span data-ttu-id="dc002-120">(Ceci inclut les applications qui utilisent [ASP.NET SignalR](http://www.asp.net/signalr) ou [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="dc002-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="dc002-121">Exécutez-vous des tâches Web continues ?</span><span class="sxs-lookup"><span data-stu-id="dc002-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="dc002-122">Si tel est le cas, activez l'option **Toujours activé**.</span><span class="sxs-lookup"><span data-stu-id="dc002-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="dc002-123">Ensemble hello **document par défaut**, tel que index.html.</span><span class="sxs-lookup"><span data-stu-id="dc002-123">Set hello **default document**, such as index.html.</span></span>

<span data-ttu-id="dc002-124">Dans les paramètres de configuration de base de toothese de plus, vous souhaiterez suivant de hello tooconfigure :</span><span class="sxs-lookup"><span data-stu-id="dc002-124">In addition toothese basic configuration settings, you may want tooconfigure hello following:</span></span>

* <span data-ttu-id="dc002-125">**SSL (Secure Socket Layer)** .</span><span class="sxs-lookup"><span data-stu-id="dc002-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="dc002-126">toouse SSL avec un nom de domaine personnalisé, vous devez obtenir une connexion SSL de certificat et de configurer votre toouse d’application web il.</span><span class="sxs-lookup"><span data-stu-id="dc002-126">toouse SSL with a custom domain name, you must get an SSL certificate and configure your web app toouse it.</span></span> <span data-ttu-id="dc002-127">Consultez la page [Activer le protocole HTTPS pour une application web dans Azure App Service](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="dc002-128">**Nom de domaine personnalisé.**</span><span class="sxs-lookup"><span data-stu-id="dc002-128">**Custom domain name.**</span></span> <span data-ttu-id="dc002-129">Votre application web a automatiquement un sous-domaine sous azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="dc002-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="dc002-130">Vous pouvez lui associer un nom de domaine personnalisé, par exemple contoso.com. Consultez la page [Configurer un nom de domaine personnalisé dans Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-130">You can associate a custom domain name, such as contoso.com. See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="dc002-131">Configuration spécifique à la langue :</span><span class="sxs-lookup"><span data-stu-id="dc002-131">Language-specific configuration:</span></span>

* <span data-ttu-id="dc002-132">**PHP**: [configurez PHP dans Azure App Service Web Apps](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-132">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="dc002-133">**Python**: [configurez Python dans Azure App Service Web Apps](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="dc002-133">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="dc002-134">Pendant l’exécution de votre application web</span><span class="sxs-lookup"><span data-stu-id="dc002-134">While your web app is running</span></span>
<span data-ttu-id="dc002-135">Pendant l’exécution de votre application web, vous souhaitez toomake qu’il est disponible, et qu’il met à l’échelle toomeet le trafic des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="dc002-135">While your web app is running, you want toomake sure it is available, and that it scales toomeet user traffic.</span></span> <span data-ttu-id="dc002-136">Vous devez également les erreurs tootroubleshoot.</span><span class="sxs-lookup"><span data-stu-id="dc002-136">You may also need tootroubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="dc002-137">Surveillance</span><span class="sxs-lookup"><span data-stu-id="dc002-137">Monitoring</span></span>
* <span data-ttu-id="dc002-138">Via hello portail Azure, vous pouvez [ajouter des métriques de performances](web-sites-monitor.md) telles que l’utilisation du processeur et le nombre de demandes client.</span><span class="sxs-lookup"><span data-stu-id="dc002-138">Through hello Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="dc002-139">[Mettre à l’échelle votre application web](web-sites-scale.md) dans tootraffic de réponse.</span><span class="sxs-lookup"><span data-stu-id="dc002-139">[Scale your web app](web-sites-scale.md) in response tootraffic.</span></span> <span data-ttu-id="dc002-140">Selon votre niveau, vous pouvez adapter le nombre de hello d’ordinateurs virtuels et/ou de la taille de hello des instances de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="dc002-140">Depending on your tier, you can scale hello number of VMs and/or hello size of hello VM instances.</span></span> <span data-ttu-id="dc002-141">Dans hello Standard et les niveaux Premium, vous pouvez également configurer échelle, afin de votre application web s’adapte automatiquement, selon une planification fixe, soit dans tooload de réponse.</span><span class="sxs-lookup"><span data-stu-id="dc002-141">In hello Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response tooload.</span></span>  

### <a name="backups"></a><span data-ttu-id="dc002-142">Sauvegardes</span><span class="sxs-lookup"><span data-stu-id="dc002-142">Backups</span></span>
* <span data-ttu-id="dc002-143">Configurez les [sauvegardes automatiques](web-sites-backup.md) de votre application web.</span><span class="sxs-lookup"><span data-stu-id="dc002-143">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="dc002-144">Pour en savoir plus sur les sauvegardes, regardez [cette vidéo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="dc002-144">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="dc002-145">En savoir plus sur les options de hello pour [récupération de base de données](../sql-database/sql-database-business-continuity.md) dans la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dc002-145">Learn about hello options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="dc002-146">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="dc002-146">Troubleshooting</span></span>
* <span data-ttu-id="dc002-147">Si une erreur survient, vous pouvez [dépanner dans Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), à l’aide des journaux de diagnostic et de débogage dans le cloud de hello.</span><span class="sxs-lookup"><span data-stu-id="dc002-147">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in hello cloud.</span></span> 
* <span data-ttu-id="dc002-148">En dehors de Visual Studio, il existe différentes façons toocollect des journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="dc002-148">Outside of Visual Studio, there are various ways toocollect diagnostic logs.</span></span> <span data-ttu-id="dc002-149">Consultez la page [Activer la journalisation des diagnostics pour les applications web dans Azure App Service](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-149">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="dc002-150">Pour les applications Node.js, consultez [comment toodebug un Node.js web application dans Azure App Service](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-150">For Node.js applications, see [How toodebug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="dc002-151">Restauration de données</span><span class="sxs-lookup"><span data-stu-id="dc002-151">Restoring Data</span></span>
* <span data-ttu-id="dc002-152">[Restaurez](web-sites-restore.md) une application Web qui a été précédemment sauvegardée.</span><span class="sxs-lookup"><span data-stu-id="dc002-152">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="dc002-153">Lors de la mise à jour de votre application Web</span><span class="sxs-lookup"><span data-stu-id="dc002-153">When you update your web app</span></span>
<span data-ttu-id="dc002-154">Si vous n'avez pas activé les sauvegardes automatiques, vous pouvez créer une [sauvegarde manuelle](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-154">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="dc002-155">Envisagez d'utiliser le [déploiement intermédiaire](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="dc002-155">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="dc002-156">Cette option vous permet de publier des mises à jour les tooa mise en lots de déploiement qui s’exécute côte à côte avec votre déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="dc002-156">This option lets you publish updates tooa staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


