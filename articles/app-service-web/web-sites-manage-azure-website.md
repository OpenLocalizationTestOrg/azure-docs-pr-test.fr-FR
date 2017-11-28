---
title: "Gérer une application web dans Azure App Service"
description: "Liens vers des ressources permettant de gérer une application web dans Azure App Service."
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
ms.openlocfilehash: 9e19618a1b24bbdf3163ddfc3423c5c932dcd7af
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a><span data-ttu-id="f9e41-103">Gérer une application web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="f9e41-103">Manage a web app in Azure App Service</span></span>
<span data-ttu-id="f9e41-104">Cette rubrique contient des liens vers des ressources permettant de gérer une application web dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="f9e41-104">This topic contains links to resources for managing a web app in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="f9e41-105">La gestion englobe toutes les tâches nécessaires au bon fonctionnement de votre application web.</span><span class="sxs-lookup"><span data-stu-id="f9e41-105">Management includes all of the tasks that keep your web app running smoothly.</span></span> 

<span data-ttu-id="f9e41-106">Pendant la durée de vie d’une application web, vous effectuez différentes tâches de gestion, depuis le déploiement initial jusqu’au fonctionnement normal, en passant par la maintenance et les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="f9e41-106">Over the lifetime of a web app, you will perform different management tasks, as you move from initial deployment to normal operation, maintenance, and updates.</span></span>

<span data-ttu-id="f9e41-107">De nombreuses tâches de gestion d’application web peuvent être effectuées dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="f9e41-107">Many web app management tasks can be performed in the Azure Portal.</span></span>

## <a name="before-you-deploy-your-web-app-to-production"></a><span data-ttu-id="f9e41-108">Avant de déployer votre application web en production</span><span class="sxs-lookup"><span data-stu-id="f9e41-108">Before you deploy your web app to production</span></span>
### <a name="choose-a-tier"></a><span data-ttu-id="f9e41-109">Choisir un niveau</span><span class="sxs-lookup"><span data-stu-id="f9e41-109">Choose a tier</span></span>
<span data-ttu-id="f9e41-110">Azure App Service est disponibles en cinq niveaux : Gratuit, Partagé, De base, Standard et Premium.</span><span class="sxs-lookup"><span data-stu-id="f9e41-110">Azure App Service is offered in five tiers: Free, Shared, Basic, Standard, and Premium.</span></span> <span data-ttu-id="f9e41-111">Pour plus d'informations sur les fonctionnalités et la tarification de chaque niveau, consultez les [détails de tarification](https://azure.microsoft.com/pricing/details/app-service/).</span><span class="sxs-lookup"><span data-stu-id="f9e41-111">For information about the features and pricing for each tier, see [Pricing details](https://azure.microsoft.com/pricing/details/app-service/).</span></span> 

* <span data-ttu-id="f9e41-112">[plans App Service](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) vous permettent de regrouper plusieurs applications web sous le même niveau.</span><span class="sxs-lookup"><span data-stu-id="f9e41-112">[App Service plans](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) let you group multiple web apps under the same tier.</span></span>
* <span data-ttu-id="f9e41-113">Vous avez toujours la possibilité de [changer de niveau](web-sites-scale.md) après avoir créé l’application web.</span><span class="sxs-lookup"><span data-stu-id="f9e41-113">You can always [switch tiers](web-sites-scale.md) after you create your web app.</span></span>

### <a name="configuration"></a><span data-ttu-id="f9e41-114">Configuration</span><span class="sxs-lookup"><span data-stu-id="f9e41-114">Configuration</span></span>
<span data-ttu-id="f9e41-115">Utilisez le [portail Azure](https://portal.azure.com/) pour définir différentes options de configuration.</span><span class="sxs-lookup"><span data-stu-id="f9e41-115">Use the [Azure Portal](https://portal.azure.com/) to set various configuration options.</span></span> <span data-ttu-id="f9e41-116">Pour plus d’informations, consultez la page [Configurer des applications web dans Azure App Service](web-sites-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-116">For details, see [Configure web apps in Azure App Service](web-sites-configure.md).</span></span> <span data-ttu-id="f9e41-117">Voici une liste de vérification rapide :</span><span class="sxs-lookup"><span data-stu-id="f9e41-117">Here is a quick checklist:</span></span>

* <span data-ttu-id="f9e41-118">Sélectionnez **Versions exécutables** pour .NET, PHP, Java ou Python, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="f9e41-118">Select **runtime versions** for .NET, PHP, Java, or Python, if needed.</span></span>
* <span data-ttu-id="f9e41-119">Activez **WebSockets** si votre site web utilise ce protocole.</span><span class="sxs-lookup"><span data-stu-id="f9e41-119">Enable **WebSockets** if your web app uses the WebSocket protocol.</span></span> <span data-ttu-id="f9e41-120">(Ceci inclut les applications qui utilisent [ASP.NET SignalR](http://www.asp.net/signalr) ou [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span><span class="sxs-lookup"><span data-stu-id="f9e41-120">(This includes apps that use [ASP.NET SignalR](http://www.asp.net/signalr) or [socket.io](web-sites-nodejs-chat-app-socketio.md).)</span></span>
* <span data-ttu-id="f9e41-121">Exécutez-vous des tâches Web continues ?</span><span class="sxs-lookup"><span data-stu-id="f9e41-121">Are you running continuous web jobs?</span></span> <span data-ttu-id="f9e41-122">Si tel est le cas, activez l'option **Toujours activé**.</span><span class="sxs-lookup"><span data-stu-id="f9e41-122">If so, enable **Always On**.</span></span>
* <span data-ttu-id="f9e41-123">Définissez le **document par défaut**, par exemple index.html.</span><span class="sxs-lookup"><span data-stu-id="f9e41-123">Set the **default document**, such as index.html.</span></span>

<span data-ttu-id="f9e41-124">Outre ces paramètres de configuration de base, vous pouvez configurer ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="f9e41-124">In addition to these basic configuration settings, you may want to configure the following:</span></span>

* <span data-ttu-id="f9e41-125">**SSL (Secure Socket Layer)** .</span><span class="sxs-lookup"><span data-stu-id="f9e41-125">**Secure Socket Layer (SSL)** encryption.</span></span> <span data-ttu-id="f9e41-126">Pour utiliser le chiffrement SSL avec un nom de domaine personnalisé, vous devez obtenir un certificat SSL et configurer votre application Web pour l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="f9e41-126">To use SSL with a custom domain name, you must get an SSL certificate and configure your web app to use it.</span></span> <span data-ttu-id="f9e41-127">Consultez la page [Activer le protocole HTTPS pour une application web dans Azure App Service](app-service-web-tutorial-custom-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-127">See [Enable HTTPS for a web app in Azure App Service](app-service-web-tutorial-custom-ssl.md).</span></span>
* <span data-ttu-id="f9e41-128">**Nom de domaine personnalisé.**</span><span class="sxs-lookup"><span data-stu-id="f9e41-128">**Custom domain name.**</span></span> <span data-ttu-id="f9e41-129">Votre application web a automatiquement un sous-domaine sous azurewebsites.net.</span><span class="sxs-lookup"><span data-stu-id="f9e41-129">Your web app automatically has a subdomain under azurewebsites.net.</span></span> <span data-ttu-id="f9e41-130">Vous pouvez lui associer un nom de domaine personnalisé, par exemple contoso.com.</span><span class="sxs-lookup"><span data-stu-id="f9e41-130">You can associate a custom domain name, such as contoso.com.</span></span> <span data-ttu-id="f9e41-131">Consultez la page [Configurer un nom de domaine personnalisé dans Azure App Service](app-service-web-tutorial-custom-domain.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-131">See [Configure a custom domain name in Azure App Service](app-service-web-tutorial-custom-domain.md).</span></span>

<span data-ttu-id="f9e41-132">Configuration spécifique à la langue :</span><span class="sxs-lookup"><span data-stu-id="f9e41-132">Language-specific configuration:</span></span>

* <span data-ttu-id="f9e41-133">**PHP**: [configurez PHP dans Azure App Service Web Apps](web-sites-php-configure.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-133">**PHP**: [Configure PHP in Azure App Service Web Apps](web-sites-php-configure.md).</span></span>
* <span data-ttu-id="f9e41-134">**Python**: [configurez Python dans Azure App Service Web Apps](web-sites-python-configure.md)</span><span class="sxs-lookup"><span data-stu-id="f9e41-134">**Python**: [Configuring Python with Azure App Service Web Apps](web-sites-python-configure.md)</span></span>

## <a name="while-your-web-app-is-running"></a><span data-ttu-id="f9e41-135">Pendant l’exécution de votre application web</span><span class="sxs-lookup"><span data-stu-id="f9e41-135">While your web app is running</span></span>
<span data-ttu-id="f9e41-136">Lorsque votre application web est en cours d’exécution, vérifiez qu’elle est disponible et qu’elle s’adapte au volume du trafic utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f9e41-136">While your web app is running, you want to make sure it is available, and that it scales to meet user traffic.</span></span> <span data-ttu-id="f9e41-137">Vous pouvez également résoudre les erreurs.</span><span class="sxs-lookup"><span data-stu-id="f9e41-137">You may also need to troubleshoot errors.</span></span>

### <a name="monitoring"></a><span data-ttu-id="f9e41-138">Analyse</span><span class="sxs-lookup"><span data-stu-id="f9e41-138">Monitoring</span></span>
* <span data-ttu-id="f9e41-139">Via le portail Azure, vous pouvez [ajouter des mesures de performances](web-sites-monitor.md) comme l’utilisation du processeur et le nombre de demandes de clients.</span><span class="sxs-lookup"><span data-stu-id="f9e41-139">Through the Azure Portal, you can [add performance metrics](web-sites-monitor.md) such as CPU usage and number of client requests.</span></span>
* <span data-ttu-id="f9e41-140">[Mettez votre application web à l’échelle](web-sites-scale.md) en fonction du trafic.</span><span class="sxs-lookup"><span data-stu-id="f9e41-140">[Scale your web app](web-sites-scale.md) in response to traffic.</span></span> <span data-ttu-id="f9e41-141">Suivant l'option choisie, vous pouvez mettre à l'échelle le nombre de machines virtuelles et/ou la taille des instances de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="f9e41-141">Depending on your tier, you can scale the number of VMs and/or the size of the VM instances.</span></span> <span data-ttu-id="f9e41-142">Dans les niveaux Standard et Premium, vous pouvez également configurer la mise à l’échelle automatique, qui fait évoluer votre application automatiquement soit à une planification définie, soit en fonction de la charge.</span><span class="sxs-lookup"><span data-stu-id="f9e41-142">In the Standard and Premium tiers, you can also set up autoscaling, so your web app scales automatically, either on a fixed schedule, or in response to load.</span></span>  

### <a name="backups"></a><span data-ttu-id="f9e41-143">Sauvegardes</span><span class="sxs-lookup"><span data-stu-id="f9e41-143">Backups</span></span>
* <span data-ttu-id="f9e41-144">Configurez les [sauvegardes automatiques](web-sites-backup.md) de votre application web.</span><span class="sxs-lookup"><span data-stu-id="f9e41-144">Set [automatic backups](web-sites-backup.md) of your web app.</span></span> <span data-ttu-id="f9e41-145">Pour en savoir plus sur les sauvegardes, regardez [cette vidéo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span><span class="sxs-lookup"><span data-stu-id="f9e41-145">Learn more about backups in [this video](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).</span></span>
* <span data-ttu-id="f9e41-146">Découvrez les options de [récupération de base de données](../sql-database/sql-database-business-continuity.md) dans la base de données Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="f9e41-146">Learn about the options for [database recovery](../sql-database/sql-database-business-continuity.md) in Azure SQL Database.</span></span>

### <a name="troubleshooting"></a><span data-ttu-id="f9e41-147">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="f9e41-147">Troubleshooting</span></span>
* <span data-ttu-id="f9e41-148">Si une erreur survient, vous pouvez [résoudre les problèmes dans Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)en utilisant des journaux de diagnostic et le débogage réel dans le cloud.</span><span class="sxs-lookup"><span data-stu-id="f9e41-148">If something goes wrong, you can [troubleshoot in Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), using diagnostic logs and live debugging in the cloud.</span></span> 
* <span data-ttu-id="f9e41-149">En dehors de Visual Studio, il existe différentes manières de recueillir les journaux de diagnostic.</span><span class="sxs-lookup"><span data-stu-id="f9e41-149">Outside of Visual Studio, there are various ways to collect diagnostic logs.</span></span> <span data-ttu-id="f9e41-150">Consultez la page [Activer la journalisation des diagnostics pour les applications web dans Azure App Service](web-sites-enable-diagnostic-log.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-150">See [Enable diagnostics logging for web apps in Azure App Service](web-sites-enable-diagnostic-log.md).</span></span>
* <span data-ttu-id="f9e41-151">Pour les applications Node.js, consultez la page [Débogage d’une application Node.js dans Azure Web Sites](web-sites-nodejs-debug.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-151">For Node.js applications, see [How to debug a Node.js web app in Azure App Service](web-sites-nodejs-debug.md).</span></span>

### <a name="restoring-data"></a><span data-ttu-id="f9e41-152">Restauration de données</span><span class="sxs-lookup"><span data-stu-id="f9e41-152">Restoring Data</span></span>
* <span data-ttu-id="f9e41-153">[Restaurez](web-sites-restore.md) une application Web qui a été précédemment sauvegardée.</span><span class="sxs-lookup"><span data-stu-id="f9e41-153">[Restore](web-sites-restore.md) a web app that was previously backed up.</span></span>

## <a name="when-you-update-your-web-app"></a><span data-ttu-id="f9e41-154">Lors de la mise à jour de votre application Web</span><span class="sxs-lookup"><span data-stu-id="f9e41-154">When you update your web app</span></span>
<span data-ttu-id="f9e41-155">Si vous n'avez pas activé les sauvegardes automatiques, vous pouvez créer une [sauvegarde manuelle](web-sites-backup.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-155">If you have not enabled automatic backups, you can create a [manual backup](web-sites-backup.md).</span></span>

<span data-ttu-id="f9e41-156">Envisagez d'utiliser le [déploiement intermédiaire](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="f9e41-156">Consider using [staged deployment](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="f9e41-157">Cette option vous permet de publier des mises à jour pour un déploiement intermédiaire qui s'exécute parallèlement à votre déploiement de production.</span><span class="sxs-lookup"><span data-stu-id="f9e41-157">This option lets you publish updates to a staging deployment that runs side-by-side with your production deployment.</span></span> 


<!-- Anchors. -->

[Before you deploy your site to production]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


