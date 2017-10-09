---
title: aaaReference pour parcourir les hello portail Azure
description: "En savoir plus hello des expériences utilisateur différent pour le Service Web de l’application entre le portail de gestion hello et hello portail Azure"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a><span data-ttu-id="df198-103">Référence pour la navigation hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="df198-103">Reference for navigating hello Azure portal</span></span>
<span data-ttu-id="df198-104">Le service Sites Web Azure s’appelle désormais [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span><span class="sxs-lookup"><span data-stu-id="df198-104">Azure Websites are now called [App Service Web Apps](http://go.microsoft.com/fwlink/?LinkId=529714).</span></span> <span data-ttu-id="df198-105">Nous mettons à tous nos tooreflect documentation jour ce nom modification et tooprovide des instructions pour hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="df198-105">We're updating all of our documentation tooreflect this name change and tooprovide instructions for hello Azure Portal.</span></span> <span data-ttu-id="df198-106">Jusqu'à ce que ce processus est terminé, vous pouvez utiliser ce document comme guide pour travailler avec des applications Web dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="df198-106">Until that process is done, you can use this document as a guide for working with Web Apps in hello Azure portal.</span></span>

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a><span data-ttu-id="df198-107">futures Hello Hello portail classique Azure</span><span class="sxs-lookup"><span data-stu-id="df198-107">hello future of hello Azure Classic Portal</span></span>
<span data-ttu-id="df198-108">Pendant que vous remarquerez hello modifications sur hello portail classique Azure de la marque, ce portail est en cours de hello de remplacé par hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="df198-108">While you will notice hello branding changes on hello Azure Classic Portal, that portal is in hello process of being replaced by hello Azure Portal.</span></span> <span data-ttu-id="df198-109">Comme le portail classique de hello est périmée, focus hello pour tout nouveau développement est un décalage toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="df198-109">As hello classic portal is being phased out, hello focus for new development is shifting toohello Azure Portal.</span></span> <span data-ttu-id="df198-110">Toutes les nouvelles fonctionnalités à venir pour les applications Web proviendront Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="df198-110">All upcoming new features for Web Apps will come in hello Azure Portal.</span></span> <span data-ttu-id="df198-111">Commencer à utiliser parti de tootake portail Azure hello Hello derniers et meilleurs éléments que les applications Web ont toooffer.</span><span class="sxs-lookup"><span data-stu-id="df198-111">Start using hello Azure Portal tootake advantage of hello latest and greatest that Web Apps have toooffer.</span></span>

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a><span data-ttu-id="df198-112">Différences de disposition entre hello portail classique Azure et le portail Azure</span><span class="sxs-lookup"><span data-stu-id="df198-112">Layout differences between hello Azure Classic Portal and Azure Portal</span></span>
<span data-ttu-id="df198-113">Dans le portail classique hello, tous les hello Azure services sont répertoriés sur le côté gauche de hello.</span><span class="sxs-lookup"><span data-stu-id="df198-113">In hello classic portal, all hello Azure services are listed on hello left hand side.</span></span> <span data-ttu-id="df198-114">Navigation dans le portail classique de hello suit une structure arborescente, où vous démarrez à partir du service de hello et naviguez dans chaque élément.</span><span class="sxs-lookup"><span data-stu-id="df198-114">Navigation in hello classic portal follows a tree structure, where you start from hello service and navigate into each element.</span></span> <span data-ttu-id="df198-115">Cette structure fonctionne bien lorsque vous gérez des composants indépendants.</span><span class="sxs-lookup"><span data-stu-id="df198-115">This structure works well when managing independent components.</span></span> <span data-ttu-id="df198-116">Toutefois, les applications créées à partir d'Azure sont constituées de services interconnectés, et cette arborescence n'est pas idéale pour les collections de services.</span><span class="sxs-lookup"><span data-stu-id="df198-116">However, applications built on Azure are a collection of interconnected services, and this tree structure isn't ideal for working with collections of services.</span></span> 

<span data-ttu-id="df198-117">Hello portail Azure rend facile toobuild applications de bout en bout avec les composants à partir de plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="df198-117">hello Azure portal makes it easy toobuild applications end-to-end with components from multiple services.</span></span> <span data-ttu-id="df198-118">portail de Hello est organisée en tant que *trajets*.</span><span class="sxs-lookup"><span data-stu-id="df198-118">hello portal is organized as *journeys*.</span></span> <span data-ttu-id="df198-119">A *voyage* est une série de *panneaux*, qui sont des conteneurs pour hello différents composants.</span><span class="sxs-lookup"><span data-stu-id="df198-119">A *journey* is a series of *blades*, which are containers for hello different components.</span></span> <span data-ttu-id="df198-120">Par exemple, la configuration de montée en puissance automatique pour une application web est un *voyage* décrites plusieurs panneaux comme indiqué dans hello l’exemple suivant : hello **site web** blade (que titre du panneau n’a pas encore été mis à jour toouse Hello la terminologie nouvelle), hello **paramètres** lame et hello **montée en puissance parallèle** panneau.</span><span class="sxs-lookup"><span data-stu-id="df198-120">For example, setting up auto-scaling for a web app is a *journey* which takes you several blades as shown in hello following example: hello **web-site** blade (that blade title has not yet been updated toouse hello new terminology), hello **Settings** blade, and hello **Scale out** blade.</span></span> <span data-ttu-id="df198-121">Dans l’exemple de hello, mise à l’échelle automatique est défini toodepend sur l’utilisation du processeur, par conséquent, il est également un **pourcentage processeur** panneau.</span><span class="sxs-lookup"><span data-stu-id="df198-121">In hello example, auto scaling is being set up toodepend on CPU usage, so there is also a **CPU Percentage** blade.</span></span> <span data-ttu-id="df198-122">Hello composants hello *panneaux* sont appelés *parties*, qui se présenter comme vignettes.</span><span class="sxs-lookup"><span data-stu-id="df198-122">hello components within hello *blades* are called *parts*, which look like tiles.</span></span> 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a><span data-ttu-id="df198-123">Exemple de navigation : créer une application web</span><span class="sxs-lookup"><span data-stu-id="df198-123">Navigation example: create a web app</span></span>
<span data-ttu-id="df198-124">La création d'applications web est toujours aussi facile qu'avant.</span><span class="sxs-lookup"><span data-stu-id="df198-124">Creating new web apps is still as easy as 1-2-3.</span></span> <span data-ttu-id="df198-125">Hello suivant image affiche hello classique portail et hello portail côte-à-côte toodemonstrate qui ne disposait pas a changé dans plusieurs étapes hello nécessaire tooget de l’application web d’en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="df198-125">hello following image shows hello classic portal and hello portal side-by-side toodemonstrate that not much has changed in hello number of steps needed tooget a web app up and running.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

<span data-ttu-id="df198-126">Dans le portail de hello, vous pouvez choisir à partir des types courants de hello des applications web, y compris les applications de la galerie populaires telles que WordPress.</span><span class="sxs-lookup"><span data-stu-id="df198-126">In hello portal you can choose from hello most common types of web apps, including popular gallery applications like WordPress.</span></span> <span data-ttu-id="df198-127">Pour obtenir une liste complète des applications disponibles, visitez hello [Azure Marketplace].</span><span class="sxs-lookup"><span data-stu-id="df198-127">For a full list of available applications, visit hello [Azure Marketplace].</span></span>

<span data-ttu-id="df198-128">Lorsque vous créez une application web, vous spécifiez l’URL, le plan App Service et l’emplacement dans le portail hello simplement comme vous le feriez dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="df198-128">When you create a web app, you specify URL, App Service plan, and location in hello portal just as you do in hello classic portal.</span></span> 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

<span data-ttu-id="df198-129">En outre, portail de hello vous permet de définir d’autres paramètres communs.</span><span class="sxs-lookup"><span data-stu-id="df198-129">In addition, hello portal lets you define other common settings.</span></span> <span data-ttu-id="df198-130">Par exemple, [groupes de ressources](../azure-resource-manager/resource-group-overview.md) rendre toosee simple et de gérer des ressources Azure associées.</span><span class="sxs-lookup"><span data-stu-id="df198-130">For example, [resource groups](../azure-resource-manager/resource-group-overview.md) make it simple toosee and manage related Azure resources.</span></span> 

## <a name="navigation-example-settings-and-features"></a><span data-ttu-id="df198-131">Exemple de navigation : paramètres et fonctionnalités</span><span class="sxs-lookup"><span data-stu-id="df198-131">Navigation example: settings and features</span></span>
<span data-ttu-id="df198-132">Tous les hello paramètres et fonctionnalités sont désormais regroupées logiquement dans un panneau unique, à partir de laquelle vous pouvez accéder.</span><span class="sxs-lookup"><span data-stu-id="df198-132">All hello settings and features are now logically grouped in a single blade, from which you can navigate.</span></span>

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

<span data-ttu-id="df198-133">Par exemple, vous pouvez créer des domaines personnalisés en cliquant sur **les domaines personnalisés et SSL** Bonjour **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="df198-133">For example, you can create custom domains by clicking **Custom domains and SSL** in hello **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

<span data-ttu-id="df198-134">tooset une alerte de surveillance, cliquez sur **demandes et les erreurs** , puis **ajouter une alerte**.</span><span class="sxs-lookup"><span data-stu-id="df198-134">tooset up a monitoring alert, click **Requests and errors** and then **Add Alert**.</span></span>

![](./media/app-service-web-app-azure-portal/Monitoring.png)

<span data-ttu-id="df198-135">tooenable diagnostics, cliquez sur **les journaux de diagnostic** Bonjour **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="df198-135">tooenable diagnostics, click **Diagnostics logs** in hello **Settings** blade.</span></span>

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

<span data-ttu-id="df198-136">Cliquez sur les paramètres de l’application tooconfigure, **paramètres d’Application** Bonjour **paramètres** panneau.</span><span class="sxs-lookup"><span data-stu-id="df198-136">tooconfigure application settings, click **Application settings** in hello **Settings** blade.</span></span> 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

<span data-ttu-id="df198-137">Que le nom de marque hello, certains éléments dans le portail de hello ont été renommés ou regroupées toomake il toofind plus facilement les.</span><span class="sxs-lookup"><span data-stu-id="df198-137">Other than hello brand name, a few things in hello portal have been renamed or grouped differently toomake it easier toofind them.</span></span> <span data-ttu-id="df198-138">Par exemple, voici une capture d’écran de la page correspondante de hello pour les paramètres de l’application (**configurer**) dans le portail classique de hello.</span><span class="sxs-lookup"><span data-stu-id="df198-138">For example, below is a screenshot of hello corresponding page for app settings (**Configure**) in hello classic portal.</span></span>

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a><span data-ttu-id="df198-139">Autres ressources</span><span class="sxs-lookup"><span data-stu-id="df198-139">More Resources</span></span>
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> <span data-ttu-id="df198-141">Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="df198-141">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="df198-142">Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.</span><span class="sxs-lookup"><span data-stu-id="df198-142">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="whats-changed"></a><span data-ttu-id="df198-143">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="df198-143">What's changed</span></span>
* <span data-ttu-id="df198-144">Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="df198-144">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

