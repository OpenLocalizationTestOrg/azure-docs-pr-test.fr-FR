---
title: "Présentation détaillée des plans Azure App Service | Microsoft Docs"
description: "Découvrez comment fonctionnent les plans Azure App Service et comment ils peuvent améliorer votre gestion."
keywords: "app service, azure app service, mise à l'échelle, évolutif, plan app service, coût d'app service"
services: app-service
documentationcenter: 
author: btardif
manager: erikre
editor: 
ms.assetid: dea3f41e-cf35-481b-a6bc-33d7fc9d01b1
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: byvinyal
ms.openlocfilehash: f97be571d104e3cc1c6ee732886fa7133ba0dc83
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="61c3c-104">Présentation détaillée des plans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="61c3c-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="61c3c-105">Les plans App Service représentent la collection des ressources physiques utilisées pour héberger vos applications.</span><span class="sxs-lookup"><span data-stu-id="61c3c-105">App Service plans represent the collection of physical resources used to host your apps.</span></span>

<span data-ttu-id="61c3c-106">Les plans App Service définissent :</span><span class="sxs-lookup"><span data-stu-id="61c3c-106">App Service plans define:</span></span>

- <span data-ttu-id="61c3c-107">Région (ouest des États-Unis, est des États-Unis, etc.)</span><span class="sxs-lookup"><span data-stu-id="61c3c-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="61c3c-108">Comptage (un, deux, trois instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="61c3c-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="61c3c-109">La taille d’instance (« Petit », « Moyen », « Grand »)</span><span class="sxs-lookup"><span data-stu-id="61c3c-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="61c3c-110">Référence (SKU) (gratuit, partagé, basique, standard, premium)</span><span class="sxs-lookup"><span data-stu-id="61c3c-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="61c3c-111">Les Web Apps, les Mobile Apps, les API Apps, et les Function Apps dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), fonctionnent toutes dans un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="61c3c-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="61c3c-112">Les applications dans le même abonnement et la même région peuvent partager un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="61c3c-112">Apps in the same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="61c3c-113">Toutes les applications affectées à un **plan App Service** partagent les ressources que celui-ci définit.</span><span class="sxs-lookup"><span data-stu-id="61c3c-113">All applications assigned to an **App Service plan** share the resources defined by it.</span></span> <span data-ttu-id="61c3c-114">Ce partage permet de réaliser des économies lors de l’hébergement de plusieurs applications dans un seul plan App Service.</span><span class="sxs-lookup"><span data-stu-id="61c3c-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="61c3c-115">Votre **plan App Service** peut évoluer des références (SKU) **gratuit** ou **partagé** vers **base**, **standard** ou **premium**, ce qui vous donne accès à plus de ressources et de fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="61c3c-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs to **Basic**, **Standard**, and **Premium** SKUs giving you access to more resources and features along the way.</span></span>

<span data-ttu-id="61c3c-116">Si votre plan App Service est défini sur la référence (SKU) **De base** ou une référence supérieure, vous pouvez contrôler la **taille** et augmenter le nombre des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="61c3c-116">If your App Service plan is set to **Basic** SKU or higher, then you can control the **size** and scale count of the VMs.</span></span>

<span data-ttu-id="61c3c-117">Par exemple, si votre plan est configuré pour utiliser deux « petites » instances d’un niveau de service standard, toutes les applications associées à ce plan sont exécutées sur ces deux instances.</span><span class="sxs-lookup"><span data-stu-id="61c3c-117">For example, if your plan is configured to use two "small" instances in the standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="61c3c-118">Les applications ont également accès aux fonctionnalités du niveau de service standard.</span><span class="sxs-lookup"><span data-stu-id="61c3c-118">Apps also have access to the standard service tier features.</span></span> <span data-ttu-id="61c3c-119">Les instances de plans sur lesquelles sont exécutées des applications sont entièrement gérées et hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="61c3c-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61c3c-120">La **Référence (SKU)** et **l’Échelle** du plan App Service déterminent le coût et non le nombre d’applications hébergées.</span><span class="sxs-lookup"><span data-stu-id="61c3c-120">The **SKU** and **Scale** of the App Service plan determines the cost and not the number of apps hosted in it.</span></span>

<span data-ttu-id="61c3c-121">Cet article présente les principales caractéristiques telles que le niveau et l’échelle d’un plan App Service, et comment elles entrent en jeu lors de la gestion de vos applications.</span><span class="sxs-lookup"><span data-stu-id="61c3c-121">This article explores the key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="61c3c-122">Applications et plans App Service</span><span class="sxs-lookup"><span data-stu-id="61c3c-122">Apps and App Service plans</span></span>

<span data-ttu-id="61c3c-123">Une application App Service ne peut être associée qu'à un seul plan App Service à la fois.</span><span class="sxs-lookup"><span data-stu-id="61c3c-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="61c3c-124">Les applications et les plans sont contenus dans un **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="61c3c-125">Un groupe de ressources sert de limite de cycle de vie pour chaque ressource qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="61c3c-125">A resource group serves as the lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="61c3c-126">Vous pouvez utiliser des groupes de ressources pour gérer toutes les parties d’une application en même temps.</span><span class="sxs-lookup"><span data-stu-id="61c3c-126">You can use resource groups to manage all the pieces of an application together.</span></span>

<span data-ttu-id="61c3c-127">Étant donné qu’un seul groupe de ressources peut disposer de plusieurs plans App Service, vous pouvez allouer différentes applications à différentes ressources physiques.</span><span class="sxs-lookup"><span data-stu-id="61c3c-127">Because a single resource group can have multiple App Service plans, you can allocate different apps to different physical resources.</span></span>

<span data-ttu-id="61c3c-128">Par exemple, vous pouvez répartir les ressources entre les environnements de développement, de test et de production.</span><span class="sxs-lookup"><span data-stu-id="61c3c-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="61c3c-129">Avoir des environnements de production et de développement/test distincts permet d’isoler des ressources.</span><span class="sxs-lookup"><span data-stu-id="61c3c-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="61c3c-130">De cette façon, les tests de charge d’une nouvelle version de vos applications ne font pas appel aux mêmes ressources que les applications de production qui sont distribuées aux clients réels.</span><span class="sxs-lookup"><span data-stu-id="61c3c-130">In this way, load testing against a new version of your apps does not compete for the same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="61c3c-131">Lorsque vous avez plusieurs plans au sein d’un même groupe de ressources, vous pouvez également définir une application disponible pour plusieurs régions géographiques.</span><span class="sxs-lookup"><span data-stu-id="61c3c-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="61c3c-132">Par exemple, une application hautement disponible qui s’exécute dans deux régions inclut au moins deux plans, un pour chaque région, et une application associée à chaque plan.</span><span class="sxs-lookup"><span data-stu-id="61c3c-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="61c3c-133">Dans ce cas, toutes les copies de l’application appartiennent à un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61c3c-133">In such a situation, all the copies of the app are then contained in a single resource group.</span></span> <span data-ttu-id="61c3c-134">Le fait de disposer d’un groupe de ressources avec plusieurs plans et plusieurs applications facilite la gestion, le contrôle et l’affichage de l’intégrité de l’application.</span><span class="sxs-lookup"><span data-stu-id="61c3c-134">Having a resource group with multiple plans and multiple apps makes it easy to manage, control, and view the health of the application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="61c3c-135">Créer un plan App Service ou utiliser un plan existant</span><span class="sxs-lookup"><span data-stu-id="61c3c-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="61c3c-136">Lorsque vous créez une application, vous devez penser à créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="61c3c-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="61c3c-137">En revanche, si l’application est un composant d’une application plus importante, créez-la au sein du groupe de ressources alloué pour l’application en question.</span><span class="sxs-lookup"><span data-stu-id="61c3c-137">On the other hand, if this app is a component for a larger application, create it within the resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="61c3c-138">Que l’application soit autonome ou fasse partie d’une autre application, vous pouvez choisir d’utiliser un plan existant pour l’héberger ou bien en créer un.</span><span class="sxs-lookup"><span data-stu-id="61c3c-138">Whether the app is an altogether new application or part of a larger one, you can choose to use an existing plan to host it or create a new one.</span></span> <span data-ttu-id="61c3c-139">Cette décision relève plus d’une question de capacité et de charge attendue.</span><span class="sxs-lookup"><span data-stu-id="61c3c-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="61c3c-140">Nous vous recommandons d’isoler votre application dans un nouveau plan App Service si :</span><span class="sxs-lookup"><span data-stu-id="61c3c-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="61c3c-141">L’application consomme beaucoup de ressources.</span><span class="sxs-lookup"><span data-stu-id="61c3c-141">App is resource-intensive.</span></span>
- <span data-ttu-id="61c3c-142">L’application a différents facteurs d’échelle par rapport aux autres applications hébergées dans un plan existant.</span><span class="sxs-lookup"><span data-stu-id="61c3c-142">App has different scaling factors from the other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="61c3c-143">L’application a besoin de ressources dans une région géographique différente.</span><span class="sxs-lookup"><span data-stu-id="61c3c-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="61c3c-144">De cette façon, vous pouvez allouer un nouveau jeu de ressources pour votre application et mieux contrôler vos applications.</span><span class="sxs-lookup"><span data-stu-id="61c3c-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="61c3c-145">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="61c3c-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="61c3c-146">Si vous disposez d’un environnement App Service, vous pouvez consulter la documentation spécifique aux environnements App Service ici : [Créer un plan App Service dans un environnement App Service](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="61c3c-146">If you have an App Service Environment, you can review the documentation specific to App Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="61c3c-147">Vous pouvez créer un plan App Service vide à partir de l’expérience de navigation du plan App Service ou dans le cadre de la création d’applications.</span><span class="sxs-lookup"><span data-stu-id="61c3c-147">You can create an empty App Service plan from the App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="61c3c-148">Dans le [portail Azure](https://portal.azure.com), cliquez sur **Nouveau** > **Web et mobilité**, puis sélectionnez **Application web** ou tout autre type d’application App Service.</span><span class="sxs-lookup"><span data-stu-id="61c3c-148">In the [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Créer une application dans le portail Azure.][createWebApp]

<span data-ttu-id="61c3c-150">Vous pouvez ensuite sélectionner ou créer le plan App Service pour la nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="61c3c-150">You can then select or create the App Service plan for the new app.</span></span>

 ![Créer un plan App Service.][createASP]

<span data-ttu-id="61c3c-152">Pour créer un plan App Service, cliquez sur **[+] Créer nouveau**, saisissez le nom du **plan App Service**, puis sélectionnez un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-152">To create an App Service plan, click **[+] Create New**, type the **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="61c3c-153">Cliquez sur **Niveau de tarification**, puis sélectionnez un niveau de tarification approprié pour le service.</span><span class="sxs-lookup"><span data-stu-id="61c3c-153">Click **Pricing tier**, and then select an appropriate pricing tier for the service.</span></span> <span data-ttu-id="61c3c-154">Sélectionnez **Afficher tout** pour afficher davantage d’options de tarification, telles que **Gratuit** et **Partagé**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-154">Select **View all** to view more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="61c3c-155">Une fois que vous avez sélectionné le niveau de tarification, cliquez sur le bouton **Sélectionner** .</span><span class="sxs-lookup"><span data-stu-id="61c3c-155">After you have selected the pricing tier, click the **Select** button.</span></span>

## <a name="move-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="61c3c-156">Déplacer une application vers un autre plan App Service</span><span class="sxs-lookup"><span data-stu-id="61c3c-156">Move an app to a different App Service plan</span></span>

<span data-ttu-id="61c3c-157">Vous pouvez déplacer une application vers un autre plan App Service depuis le [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="61c3c-157">You can move an app to a different App Service plan in the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="61c3c-158">Vous pouvez déplacer les applications d’un plan à l’autre tant que les plans se trouvent dans le même groupe de ressources et dans la même région géographique.</span><span class="sxs-lookup"><span data-stu-id="61c3c-158">You can move apps between plans as long as the plans are in the same resource group and geographical region.</span></span>

<span data-ttu-id="61c3c-159">Pour déplacer une application vers un autre plan :</span><span class="sxs-lookup"><span data-stu-id="61c3c-159">To move an app to another plan:</span></span>

- <span data-ttu-id="61c3c-160">Accédez à l’application à déplacer.</span><span class="sxs-lookup"><span data-stu-id="61c3c-160">Navigate to the app that you want to move.</span></span>
- <span data-ttu-id="61c3c-161">Dans le **Menu**, recherchez la section **Plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-161">In the **Menu**, look for the **App Service Plan** section.</span></span>
- <span data-ttu-id="61c3c-162">Sélectionnez **Changer le plan App Service** pour démarrer le processus.</span><span class="sxs-lookup"><span data-stu-id="61c3c-162">Select **Change App Service plan** to start the process.</span></span>

<span data-ttu-id="61c3c-163">**Modifier le Plan App Service** ouvre le sélecteur de **plan App Service**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-163">**Change App Service plan** opens the **App Service plan** selector.</span></span> <span data-ttu-id="61c3c-164">À ce stade, vous pouvez choisir un plan existant vers lequel déplacer cette application.</span><span class="sxs-lookup"><span data-stu-id="61c3c-164">At this point, you can pick an existing plan to move this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61c3c-165">L’interface utilisateur du plan App Service sélectionné est filtré selon les critères suivants :</span><span class="sxs-lookup"><span data-stu-id="61c3c-165">The select App Service plan UI is filtered by the following criteria:</span></span>
> - <span data-ttu-id="61c3c-166">Il existe dans le même groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="61c3c-166">Exists within the same Resource Group</span></span>
> - <span data-ttu-id="61c3c-167">Il existe dans la même région géographique</span><span class="sxs-lookup"><span data-stu-id="61c3c-167">Exists in the same Geographical Region</span></span>
> - <span data-ttu-id="61c3c-168">Il existe dans le même espace Web</span><span class="sxs-lookup"><span data-stu-id="61c3c-168">Exists within the same Webspace</span></span>
>
> <span data-ttu-id="61c3c-169">Un espace Web est une construction logique au sein d’App Service qui définit un regroupement de ressources du serveur.</span><span class="sxs-lookup"><span data-stu-id="61c3c-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="61c3c-170">Une région géographique (par exemple, ouest des États-Unis) contient plusieurs espaces Web pour allouer des clients à l’aide d’App Service.</span><span class="sxs-lookup"><span data-stu-id="61c3c-170">A Geographical region (such as West US) contains many Webspaces in order to allocate customers using App Service.</span></span> <span data-ttu-id="61c3c-171">Actuellement, les ressources App Service ne sont pas en mesure de vous déplacer entre des espaces Web.</span><span class="sxs-lookup"><span data-stu-id="61c3c-171">Currently, App Service resources aren’t able to be moved between Webspaces.</span></span>
>

![Sélecteur de plan App Service.][change]

<span data-ttu-id="61c3c-173">Chaque plan a son propre niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="61c3c-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="61c3c-174">Par exemple, quand vous déplacez un site du niveau Gratuit au niveau Standard, toutes les applications affectées peuvent utiliser les fonctionnalités et ressources du niveau Standard.</span><span class="sxs-lookup"><span data-stu-id="61c3c-174">For example, moving a site from a Free tier to a Standard tier, enables all apps assigned to it to use the features and resources of the Standard tier.</span></span>

## <a name="clone-an-app-to-a-different-app-service-plan"></a><span data-ttu-id="61c3c-175">Cloner une application vers un autre plan App Service</span><span class="sxs-lookup"><span data-stu-id="61c3c-175">Clone an app to a different App Service plan</span></span>

<span data-ttu-id="61c3c-176">Si vous souhaitez déplacer l'application vers une autre région, vous pouvez également utiliser le clonage d’application.</span><span class="sxs-lookup"><span data-stu-id="61c3c-176">If you want to move the app to a different region, one alternative is app cloning.</span></span> <span data-ttu-id="61c3c-177">Le clonage crée une copie de votre application dans un plan App Service, nouveau ou existant, dans n’importe quelle région.</span><span class="sxs-lookup"><span data-stu-id="61c3c-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="61c3c-178">La commande **Cloner l’application** figure dans la section **Outils de développement** du menu.</span><span class="sxs-lookup"><span data-stu-id="61c3c-178">You can find **Clone App** in the **Development Tools** section of the menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61c3c-179">Pour plus d’informations sur les limites du clonage, voir [Clonage de l’application Azure App Service à l’aide du portail Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="61c3c-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="61c3c-180">Mettre à l’échelle un plan App Service</span><span class="sxs-lookup"><span data-stu-id="61c3c-180">Scale an App Service plan</span></span>

<span data-ttu-id="61c3c-181">Il existe trois façons de mettre à l'échelle un plan :</span><span class="sxs-lookup"><span data-stu-id="61c3c-181">There are three ways to scale a plan:</span></span>

- <span data-ttu-id="61c3c-182">**Modifier le niveau de tarification du plan**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-182">**Change the plan’s pricing tier**.</span></span> <span data-ttu-id="61c3c-183">Un plan au niveau de base peut être converti en plan Standard, et toutes les applications concernées peuvent alors utiliser les fonctionnalités du niveau Standard.</span><span class="sxs-lookup"><span data-stu-id="61c3c-183">A plan in the Basic tier can be converted to Standard, and all apps assigned to it to use the features of the Standard tier.</span></span>
- <span data-ttu-id="61c3c-184">**Modifier la taille des instances du plan**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-184">**Change the plan’s instance size**.</span></span> <span data-ttu-id="61c3c-185">Par exemple, un plan associé au niveau de tarification De base et utilisant des petites instances peut être modifié pour utiliser de grandes instances.</span><span class="sxs-lookup"><span data-stu-id="61c3c-185">As an example, a plan in the Basic tier that uses small instances can be changed to use large instances.</span></span> <span data-ttu-id="61c3c-186">Toutes les applications associées à ce plan peuvent dans ce cas utiliser la mémoire supplémentaire et des ressources processeur offertes par l’instance la plus grande.</span><span class="sxs-lookup"><span data-stu-id="61c3c-186">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance size offers.</span></span>
- <span data-ttu-id="61c3c-187">**Modifier le nombre d’instances du plan**.</span><span class="sxs-lookup"><span data-stu-id="61c3c-187">**Change the plan’s instance count**.</span></span> <span data-ttu-id="61c3c-188">Par exemple, un plan Standard réparti sur trois instances peut évoluer vers 10 instances.</span><span class="sxs-lookup"><span data-stu-id="61c3c-188">For example, a Standard plan that's scaled out to three instances can be scaled to 10 instances.</span></span> <span data-ttu-id="61c3c-189">Un plan Premium peut comporter jusqu’à 20 instances (selon la disponibilité).</span><span class="sxs-lookup"><span data-stu-id="61c3c-189">A Premium plan can be scaled out to 20 instances (subject to availability).</span></span> <span data-ttu-id="61c3c-190">Toutes les applications associées à ce plan peuvent dans ce cas utiliser la mémoire supplémentaire et des ressources processeur offertes par le plus grand nombre d’instances.</span><span class="sxs-lookup"><span data-stu-id="61c3c-190">All apps that are associated with that plan now can use the additional memory and CPU resources that the larger instance count offers.</span></span>

<span data-ttu-id="61c3c-191">Vous pouvez modifier le niveau tarifaire et la taille de l’instance en cliquant sur l’élément **Montée en puissance** sous les paramètres du plan de l’application ou du plan App Service.</span><span class="sxs-lookup"><span data-stu-id="61c3c-191">You can change the pricing tier and instance size by clicking the **Scale Up** item under settings for either the app or the App Service plan.</span></span> <span data-ttu-id="61c3c-192">Les modifications s’appliquent au plan App Service et affectent toutes les applications hébergées par celui-ci.</span><span class="sxs-lookup"><span data-stu-id="61c3c-192">Changes apply to the App Service plan and affect all apps that it hosts.</span></span>

 ![Définir des valeurs pour la montée en puissance d’une application.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="61c3c-194">Nettoyage du plan App Service</span><span class="sxs-lookup"><span data-stu-id="61c3c-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61c3c-195">Les **plans App Service** auxquels aucune application n’est associée impliquent tout de même des frais, car ils continuent à réserver la capacité de calcul.</span><span class="sxs-lookup"><span data-stu-id="61c3c-195">**App Service plans** that have no apps associated to them still incur charges since they continue to reserve the compute capacity.</span></span>

<span data-ttu-id="61c3c-196">Pour éviter des frais inattendus, lorsque la dernière application hébergée dans un plan App Service est supprimée, le plan App Service vide qui en résulte est également supprimé.</span><span class="sxs-lookup"><span data-stu-id="61c3c-196">To avoid unexpected charges, when the last app hosted in an App Service plan is deleted, the resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="61c3c-197">Résumé</span><span class="sxs-lookup"><span data-stu-id="61c3c-197">Summary</span></span>

<span data-ttu-id="61c3c-198">Les plans App Service représentent un ensemble de fonctionnalités et de capacités que vous pouvez partager entre vos différentes applications.</span><span class="sxs-lookup"><span data-stu-id="61c3c-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="61c3c-199">Les plans App Service vous donnent la possibilité d’allouer des applications spécifiques à un ensemble de ressources, et d’optimiser davantage l’utilisation des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="61c3c-199">App Service plans give you the flexibility to allocate specific apps to a set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="61c3c-200">Ainsi, si vous souhaitez faire des économies sur votre environnement de test, vous pouvez partager un même plan entre plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="61c3c-200">This way, if you want to save money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="61c3c-201">Vous pouvez également augmenter le débit de votre environnement de production en le mettant à l'échelle dans plusieurs régions et plusieurs plans.</span><span class="sxs-lookup"><span data-stu-id="61c3c-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="61c3c-202">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="61c3c-202">What's changed</span></span>

- <span data-ttu-id="61c3c-203">Pour obtenir un guide présentant les modifications apportées dans le cadre de la transition entre Sites Web et App Service, consultez la page : [Azure App Service et les services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="61c3c-203">For a guide to the change from Websites to App Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
