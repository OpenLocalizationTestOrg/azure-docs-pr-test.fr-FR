---
title: "vue d’ensemble approfondie des plans aaaAzure du Service d’applications | Documents Microsoft"
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
ms.openlocfilehash: b384790d9e69b234ca69ac591164c48a4b6ed210
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-app-service-plans-in-depth-overview"></a><span data-ttu-id="21841-104">Présentation détaillée des plans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="21841-104">Azure App Service plans in-depth overview</span></span>

<span data-ttu-id="21841-105">Plans de Service d’application représentent collection hello de ressources physiques utilisées toohost vos applications.</span><span class="sxs-lookup"><span data-stu-id="21841-105">App Service plans represent hello collection of physical resources used toohost your apps.</span></span>

<span data-ttu-id="21841-106">Les plans App Service définissent :</span><span class="sxs-lookup"><span data-stu-id="21841-106">App Service plans define:</span></span>

- <span data-ttu-id="21841-107">Région (ouest des États-Unis, est des États-Unis, etc.)</span><span class="sxs-lookup"><span data-stu-id="21841-107">Region (West US, East US, etc.)</span></span>
- <span data-ttu-id="21841-108">Comptage (un, deux, trois instances, etc.)</span><span class="sxs-lookup"><span data-stu-id="21841-108">Scale count (one, two, three instances, etc.)</span></span>
- <span data-ttu-id="21841-109">La taille d’instance (« Petit », « Moyen », « Grand »)</span><span class="sxs-lookup"><span data-stu-id="21841-109">Instance size (Small, Medium, Large)</span></span>
- <span data-ttu-id="21841-110">Référence (SKU) (gratuit, partagé, basique, standard, premium)</span><span class="sxs-lookup"><span data-stu-id="21841-110">SKU (Free, Shared, Basic, Standard, Premium)</span></span>

<span data-ttu-id="21841-111">Les Web Apps, les Mobile Apps, les API Apps, et les Function Apps dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), fonctionnent toutes dans un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="21841-111">Web Apps, Mobile Apps, API Apps, Function Apps (or Functions), in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) all run in an App Service plan.</span></span>  <span data-ttu-id="21841-112">Applications Bonjour même abonnement et région peuvent partager un plan App Service.</span><span class="sxs-lookup"><span data-stu-id="21841-112">Apps in hello same subscription, and region can share an App Service plan.</span></span> 

<span data-ttu-id="21841-113">Toutes les applications affectées tooan **plan App Service** partagent des ressources hello qu’elle.</span><span class="sxs-lookup"><span data-stu-id="21841-113">All applications assigned tooan **App Service plan** share hello resources defined by it.</span></span> <span data-ttu-id="21841-114">Ce partage permet de réaliser des économies lors de l’hébergement de plusieurs applications dans un seul plan App Service.</span><span class="sxs-lookup"><span data-stu-id="21841-114">This sharing saves money when hosting multiple apps in a single App Service plan.</span></span>

<span data-ttu-id="21841-115">Votre **plan App Service** peut évoluer de **libre** et **Shared** références trop**base**, **Standard**, et **Premium** références (SKU), vous pouvez ainsi accéder aux ressources de la toomore et de fonctionnalités le long de hello moyen.</span><span class="sxs-lookup"><span data-stu-id="21841-115">Your **App Service plan** can scale from **Free** and **Shared** SKUs too**Basic**, **Standard**, and **Premium** SKUs giving you access toomore resources and features along hello way.</span></span>

<span data-ttu-id="21841-116">Si votre plan App Service est défini trop**base** référence (SKU) ou une version ultérieure, puis vous pouvez contrôler hello **taille** et d’augmenter le nombre de machines virtuelles de hello.</span><span class="sxs-lookup"><span data-stu-id="21841-116">If your App Service plan is set too**Basic** SKU or higher, then you can control hello **size** and scale count of hello VMs.</span></span>

<span data-ttu-id="21841-117">Par exemple, si votre plan est configuré toouse deux les instances « petite » dans le niveau de service standard hello, toutes les applications qui sont associées à ce plan s’exécuter sur les deux instances.</span><span class="sxs-lookup"><span data-stu-id="21841-117">For example, if your plan is configured toouse two "small" instances in hello standard service tier, all apps that are associated with that plan run on both instances.</span></span> <span data-ttu-id="21841-118">Les applications ont également des fonctionnalités de niveau d’accès toohello service standard.</span><span class="sxs-lookup"><span data-stu-id="21841-118">Apps also have access toohello standard service tier features.</span></span> <span data-ttu-id="21841-119">Les instances de plans sur lesquelles sont exécutées des applications sont entièrement gérées et hautement disponibles.</span><span class="sxs-lookup"><span data-stu-id="21841-119">Plan instances on which apps are running are fully managed and highly available.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21841-120">Hello **référence (SKU)** et **échelle** Hello du Service d’applications plan détermine hello coût et hello pas le numéro d’applications qu’elle contient.</span><span class="sxs-lookup"><span data-stu-id="21841-120">hello **SKU** and **Scale** of hello App Service plan determines hello cost and not hello number of apps hosted in it.</span></span>

<span data-ttu-id="21841-121">Cet article explore hello principales caractéristiques, telles que le niveau et mise à l’échelle d’un plan App Service et comment ils entrent en jeu lors de la gestion de vos applications.</span><span class="sxs-lookup"><span data-stu-id="21841-121">This article explores hello key characteristics, such as tier and scale, of an App Service plan and how they come into play while managing your apps.</span></span>

## <a name="apps-and-app-service-plans"></a><span data-ttu-id="21841-122">Applications et plans App Service</span><span class="sxs-lookup"><span data-stu-id="21841-122">Apps and App Service plans</span></span>

<span data-ttu-id="21841-123">Une application App Service ne peut être associée qu'à un seul plan App Service à la fois.</span><span class="sxs-lookup"><span data-stu-id="21841-123">An app in App Service can be associated with only one App Service plan at any given time.</span></span>

<span data-ttu-id="21841-124">Les applications et les plans sont contenus dans un **groupe de ressources**.</span><span class="sxs-lookup"><span data-stu-id="21841-124">Both apps and plans are contained in a **resource group**.</span></span> <span data-ttu-id="21841-125">Un groupe de ressources sert de limite de cycle de vie hello pour toutes les ressources qu’il contient.</span><span class="sxs-lookup"><span data-stu-id="21841-125">A resource group serves as hello lifecycle boundary for every resource that's within it.</span></span> <span data-ttu-id="21841-126">Vous pouvez utiliser toomanage de groupes de ressources tous les éléments hello d’une application.</span><span class="sxs-lookup"><span data-stu-id="21841-126">You can use resource groups toomanage all hello pieces of an application together.</span></span>

<span data-ttu-id="21841-127">Comme un seul groupe de ressources peut avoir plusieurs plans de services d’application, vous pouvez affecter à différentes applications toodifferent des ressources physiques.</span><span class="sxs-lookup"><span data-stu-id="21841-127">Because a single resource group can have multiple App Service plans, you can allocate different apps toodifferent physical resources.</span></span>

<span data-ttu-id="21841-128">Par exemple, vous pouvez répartir les ressources entre les environnements de développement, de test et de production.</span><span class="sxs-lookup"><span data-stu-id="21841-128">For example, you can separate resources among dev, test, and production environments.</span></span> <span data-ttu-id="21841-129">Avoir des environnements de production et de développement/test distincts permet d’isoler des ressources.</span><span class="sxs-lookup"><span data-stu-id="21841-129">Having separate environments for production and dev/test lets you isolate resources.</span></span> <span data-ttu-id="21841-130">De cette façon, test de charge sur une nouvelle version de vos applications n’est pas en concurrence pour hello même ressources en tant que vos applications de production, qui servent à nos clients.</span><span class="sxs-lookup"><span data-stu-id="21841-130">In this way, load testing against a new version of your apps does not compete for hello same resources as your production apps, which are serving real customers.</span></span>

<span data-ttu-id="21841-131">Lorsque vous avez plusieurs plans au sein d’un même groupe de ressources, vous pouvez également définir une application disponible pour plusieurs régions géographiques.</span><span class="sxs-lookup"><span data-stu-id="21841-131">When you have multiple plans in a single resource group, you can also define an application that spans geographical regions.</span></span>

<span data-ttu-id="21841-132">Par exemple, une application hautement disponible qui s’exécute dans deux régions inclut au moins deux plans, un pour chaque région, et une application associée à chaque plan.</span><span class="sxs-lookup"><span data-stu-id="21841-132">For example, a highly available app running in two regions includes at least two plans, one for each region, and one app associated with each plan.</span></span> <span data-ttu-id="21841-133">Dans ce cas, toutes les copies de hello d’application hello puis contenus dans un seul groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21841-133">In such a situation, all hello copies of hello app are then contained in a single resource group.</span></span> <span data-ttu-id="21841-134">Avoir un groupe de ressources avec plusieurs plans et plusieurs applications en fait toomanage facile, le contrôle et afficher l’intégrité de hello de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="21841-134">Having a resource group with multiple plans and multiple apps makes it easy toomanage, control, and view hello health of hello application.</span></span>

## <a name="create-an-app-service-plan-or-use-existing-one"></a><span data-ttu-id="21841-135">Créer un plan App Service ou utiliser un plan existant</span><span class="sxs-lookup"><span data-stu-id="21841-135">Create an App Service plan or use existing one</span></span>

<span data-ttu-id="21841-136">Lorsque vous créez une application, vous devez penser à créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="21841-136">When you create an app, you should consider creating a resource group.</span></span> <span data-ttu-id="21841-137">Sur hello autre part, si cette application est un composant pour une application plus importante, créez-le dans groupe de ressources hello qui est allouée pour cette application supérieure.</span><span class="sxs-lookup"><span data-stu-id="21841-137">On hello other hand, if this app is a component for a larger application, create it within hello resource group that's allocated for that larger application.</span></span>

<span data-ttu-id="21841-138">Si l’application hello est un entièrement nouvelle application ou une partie d’une plus grande, vous pouvez choisir toouse un toohost de plan existant qu’il ou créez-en un.</span><span class="sxs-lookup"><span data-stu-id="21841-138">Whether hello app is an altogether new application or part of a larger one, you can choose toouse an existing plan toohost it or create a new one.</span></span> <span data-ttu-id="21841-139">Cette décision relève plus d’une question de capacité et de charge attendue.</span><span class="sxs-lookup"><span data-stu-id="21841-139">This decision is more a question of capacity and expected load.</span></span>

<span data-ttu-id="21841-140">Nous vous recommandons d’isoler votre application dans un nouveau plan App Service si :</span><span class="sxs-lookup"><span data-stu-id="21841-140">We recommend isolating your app into a new App Service plan when:</span></span>

- <span data-ttu-id="21841-141">L’application consomme beaucoup de ressources.</span><span class="sxs-lookup"><span data-stu-id="21841-141">App is resource-intensive.</span></span>
- <span data-ttu-id="21841-142">Application dispose de différents facteurs d’échelle à partir de hello autres applications hébergées dans un plan existant.</span><span class="sxs-lookup"><span data-stu-id="21841-142">App has different scaling factors from hello other apps hosted in an existing plan.</span></span>
- <span data-ttu-id="21841-143">L’application a besoin de ressources dans une région géographique différente.</span><span class="sxs-lookup"><span data-stu-id="21841-143">App needs resource in a different geographical region.</span></span>

<span data-ttu-id="21841-144">De cette façon, vous pouvez allouer un nouveau jeu de ressources pour votre application et mieux contrôler vos applications.</span><span class="sxs-lookup"><span data-stu-id="21841-144">This way you can allocate a new set of resources for your app and gain greater control of your apps.</span></span>

## <a name="create-an-app-service-plan"></a><span data-ttu-id="21841-145">Créer un plan App Service</span><span class="sxs-lookup"><span data-stu-id="21841-145">Create an App Service plan</span></span>

> [!TIP]
> <span data-ttu-id="21841-146">Si vous avez un environnement App Service, vous pouvez consulter hello documentation spécifique tooApp environnements Service ici : [créer un plan de Service d’applications dans un environnement App Service](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span><span class="sxs-lookup"><span data-stu-id="21841-146">If you have an App Service Environment, you can review hello documentation specific tooApp Service Environments here: [Create an App Service plan in an App Service Environment](../app-service-web/app-service-web-how-to-create-a-web-app-in-an-ase.md#createplan)</span></span>

<span data-ttu-id="21841-147">Vous pouvez créer un plan App Service vide de hello expérience de navigation de plan de Service d’applications ou dans le cadre de la création de l’application.</span><span class="sxs-lookup"><span data-stu-id="21841-147">You can create an empty App Service plan from hello App Service plan browse experience or as part of app creation.</span></span>

<span data-ttu-id="21841-148">Bonjour [portail Azure](https://portal.azure.com), cliquez sur **nouveau** > **Web + mobile**, puis sélectionnez **Web App** ou autre type d’application de Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="21841-148">In hello [Azure portal](https://portal.azure.com), click **New** > **Web + mobile**, and then select **Web App** or other App Service app kind.</span></span>

![Créer une application Bonjour portail Azure.][createWebApp]

<span data-ttu-id="21841-150">Vous pouvez ensuite sélectionner ou créer hello plan App Service pour hello nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="21841-150">You can then select or create hello App Service plan for hello new app.</span></span>

 ![Créer un plan App Service.][createASP]

<span data-ttu-id="21841-152">toocreate un plan App Service, cliquez sur **[+] Create New**, hello de type **plan App Service** nom, puis sélectionnez un **emplacement**.</span><span class="sxs-lookup"><span data-stu-id="21841-152">toocreate an App Service plan, click **[+] Create New**, type hello **App Service plan** name, and then select an appropriate **Location**.</span></span> <span data-ttu-id="21841-153">Cliquez sur **niveau tarifaire**, puis sélectionnez un niveau de tarification approprié pour le service de hello.</span><span class="sxs-lookup"><span data-stu-id="21841-153">Click **Pricing tier**, and then select an appropriate pricing tier for hello service.</span></span> <span data-ttu-id="21841-154">Sélectionnez **afficher toutes les** tooview plus tarification options, telles que **libre** et **partagé**.</span><span class="sxs-lookup"><span data-stu-id="21841-154">Select **View all** tooview more pricing options, such as **Free** and **Shared**.</span></span> <span data-ttu-id="21841-155">Après avoir sélectionné hello niveau tarifaire, cliquez sur hello **sélectionnez** bouton.</span><span class="sxs-lookup"><span data-stu-id="21841-155">After you have selected hello pricing tier, click hello **Select** button.</span></span>

## <a name="move-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="21841-156">Déplacer un plan de Service d’applications application tooa différents</span><span class="sxs-lookup"><span data-stu-id="21841-156">Move an app tooa different App Service plan</span></span>

<span data-ttu-id="21841-157">Vous pouvez déplacer un plan de Service d’applications différentes application tooa Bonjour [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="21841-157">You can move an app tooa different App Service plan in hello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="21841-158">Vous pouvez déplacer des applications entre les plans tant que plans de hello sont Bonjour même groupe de ressources et de la région géographique.</span><span class="sxs-lookup"><span data-stu-id="21841-158">You can move apps between plans as long as hello plans are in hello same resource group and geographical region.</span></span>

<span data-ttu-id="21841-159">toomove un plan de tooanother d’application :</span><span class="sxs-lookup"><span data-stu-id="21841-159">toomove an app tooanother plan:</span></span>

- <span data-ttu-id="21841-160">Accédez application toohello que vous souhaitez toomove.</span><span class="sxs-lookup"><span data-stu-id="21841-160">Navigate toohello app that you want toomove.</span></span>
- <span data-ttu-id="21841-161">Bonjour **Menu**, recherchez hello **du Plan App Service** section.</span><span class="sxs-lookup"><span data-stu-id="21841-161">In hello **Menu**, look for hello **App Service Plan** section.</span></span>
- <span data-ttu-id="21841-162">Sélectionnez **plan App Service de modification** processus de hello toostart.</span><span class="sxs-lookup"><span data-stu-id="21841-162">Select **Change App Service plan** toostart hello process.</span></span>

<span data-ttu-id="21841-163">**Plan App Service de modification** ouvre hello **plan App Service** sélecteur.</span><span class="sxs-lookup"><span data-stu-id="21841-163">**Change App Service plan** opens hello **App Service plan** selector.</span></span> <span data-ttu-id="21841-164">À ce stade, vous pouvez choisir un toomove de plan existant cette application dans.</span><span class="sxs-lookup"><span data-stu-id="21841-164">At this point, you can pick an existing plan toomove this app into.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21841-165">l’interface utilisateur le plan App Service sélectionnez Hello est filtré par hello suivant des critères :</span><span class="sxs-lookup"><span data-stu-id="21841-165">hello select App Service plan UI is filtered by hello following criteria:</span></span>
> - <span data-ttu-id="21841-166">Existe dans hello même groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="21841-166">Exists within hello same Resource Group</span></span>
> - <span data-ttu-id="21841-167">Existe dans hello même région géographique</span><span class="sxs-lookup"><span data-stu-id="21841-167">Exists in hello same Geographical Region</span></span>
> - <span data-ttu-id="21841-168">Existe dans hello même espace Web</span><span class="sxs-lookup"><span data-stu-id="21841-168">Exists within hello same Webspace</span></span>
>
> <span data-ttu-id="21841-169">Un espace Web est une construction logique au sein d’App Service qui définit un regroupement de ressources du serveur.</span><span class="sxs-lookup"><span data-stu-id="21841-169">A Webspace is a logical construct within App Service which defines a grouping of server resources.</span></span> <span data-ttu-id="21841-170">Une région géographique (par exemple, ouest des États-Unis) contient des espaces Web de nombreux clients tooallocate de commande à l’aide du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="21841-170">A Geographical region (such as West US) contains many Webspaces in order tooallocate customers using App Service.</span></span> <span data-ttu-id="21841-171">Actuellement, les ressources du Service d’applications ne sont pas en mesure de toobe déplacé entre des espaces Web.</span><span class="sxs-lookup"><span data-stu-id="21841-171">Currently, App Service resources aren’t able toobe moved between Webspaces.</span></span>
>

![Sélecteur de plan App Service.][change]

<span data-ttu-id="21841-173">Chaque plan a son propre niveau de tarification.</span><span class="sxs-lookup"><span data-stu-id="21841-173">Each plan has its own pricing tier.</span></span> <span data-ttu-id="21841-174">Par exemple, le déplacement d’un site à partir d’un niveau Standard de niveau gratuit tooa, Active toutes les applications affectées des fonctionnalités de tooit toouse hello et ressources de niveau Standard de hello.</span><span class="sxs-lookup"><span data-stu-id="21841-174">For example, moving a site from a Free tier tooa Standard tier, enables all apps assigned tooit toouse hello features and resources of hello Standard tier.</span></span>

## <a name="clone-an-app-tooa-different-app-service-plan"></a><span data-ttu-id="21841-175">Cloner un plan de Service d’applications application tooa différents</span><span class="sxs-lookup"><span data-stu-id="21841-175">Clone an app tooa different App Service plan</span></span>

<span data-ttu-id="21841-176">Si vous souhaitez toomove hello application tooa autre région, une solution consiste à application le clonage.</span><span class="sxs-lookup"><span data-stu-id="21841-176">If you want toomove hello app tooa different region, one alternative is app cloning.</span></span> <span data-ttu-id="21841-177">Le clonage crée une copie de votre application dans un plan App Service, nouveau ou existant, dans n’importe quelle région.</span><span class="sxs-lookup"><span data-stu-id="21841-177">Cloning makes a copy of your app in a new or existing App Service plan in any region.</span></span>

<span data-ttu-id="21841-178">Vous pouvez trouver **le clonage d’application** Bonjour **outils de développement** section du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="21841-178">You can find **Clone App** in hello **Development Tools** section of hello menu.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21841-179">Pour plus d’informations sur les limites du clonage, voir [Clonage de l’application Azure App Service à l’aide du portail Azure](../app-service-web/app-service-web-app-cloning-portal.md).</span><span class="sxs-lookup"><span data-stu-id="21841-179">Cloning has some limitations that you can read about at [Azure App Service App cloning using Azure portal](../app-service-web/app-service-web-app-cloning-portal.md).</span></span>

## <a name="scale-an-app-service-plan"></a><span data-ttu-id="21841-180">Mettre à l’échelle un plan App Service</span><span class="sxs-lookup"><span data-stu-id="21841-180">Scale an App Service plan</span></span>

<span data-ttu-id="21841-181">Il existe trois façons tooscale un plan :</span><span class="sxs-lookup"><span data-stu-id="21841-181">There are three ways tooscale a plan:</span></span>

- <span data-ttu-id="21841-182">**Niveau de tarification du planning hello**.</span><span class="sxs-lookup"><span data-stu-id="21841-182">**Change hello plan’s pricing tier**.</span></span> <span data-ttu-id="21841-183">Un plan de niveau de base hello peut être convertie tooStandard, et toutes les applications affectées tooit toouse fonctionnalités hello de niveau Standard de hello.</span><span class="sxs-lookup"><span data-stu-id="21841-183">A plan in hello Basic tier can be converted tooStandard, and all apps assigned tooit toouse hello features of hello Standard tier.</span></span>
- <span data-ttu-id="21841-184">**Modifier la taille des instances du plan hello**.</span><span class="sxs-lookup"><span data-stu-id="21841-184">**Change hello plan’s instance size**.</span></span> <span data-ttu-id="21841-185">Par exemple, un plan de niveau de base hello qui utilise de petites instances peut être modifiées toouse les instances de grande taille.</span><span class="sxs-lookup"><span data-stu-id="21841-185">As an example, a plan in hello Basic tier that uses small instances can be changed toouse large instances.</span></span> <span data-ttu-id="21841-186">Toutes les applications qui sont associées à ce plan maintenant peuvent utiliser plus de mémoire hello et les ressources qui hello offres de taille plus grandes instance.</span><span class="sxs-lookup"><span data-stu-id="21841-186">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance size offers.</span></span>
- <span data-ttu-id="21841-187">**Modifier le nombre d’instances du plan hello**.</span><span class="sxs-lookup"><span data-stu-id="21841-187">**Change hello plan’s instance count**.</span></span> <span data-ttu-id="21841-188">Par exemple, un plan Standard est remonté toothree instances peut être mis à l’échelle too10 instances.</span><span class="sxs-lookup"><span data-stu-id="21841-188">For example, a Standard plan that's scaled out toothree instances can be scaled too10 instances.</span></span> <span data-ttu-id="21841-189">Un plan Premium la montée en puissance too20 instances (objet tooavailability).</span><span class="sxs-lookup"><span data-stu-id="21841-189">A Premium plan can be scaled out too20 instances (subject tooavailability).</span></span> <span data-ttu-id="21841-190">Toutes les applications qui sont associées à ce plan maintenant peuvent utiliser plus de mémoire hello et les ressources qui hello plus grande offre de nombre d’instance.</span><span class="sxs-lookup"><span data-stu-id="21841-190">All apps that are associated with that plan now can use hello additional memory and CPU resources that hello larger instance count offers.</span></span>

<span data-ttu-id="21841-191">Vous pouvez modifier hello tarification de couche et instance de la taille en cliquant sur hello **mise à l’échelle** élément sous Paramètres hello plan App Service ou application hello.</span><span class="sxs-lookup"><span data-stu-id="21841-191">You can change hello pricing tier and instance size by clicking hello **Scale Up** item under settings for either hello app or hello App Service plan.</span></span> <span data-ttu-id="21841-192">Modifications s’appliquent toohello plan App Service et concernent toutes les applications qu’il héberge.</span><span class="sxs-lookup"><span data-stu-id="21841-192">Changes apply toohello App Service plan and affect all apps that it hosts.</span></span>

 ![Définissez tooscale de valeurs d’une application.][pricingtier]

## <a name="app-service-plan-cleanup"></a><span data-ttu-id="21841-194">Nettoyage du plan App Service</span><span class="sxs-lookup"><span data-stu-id="21841-194">App Service plan cleanup</span></span>

> [!IMPORTANT]
> <span data-ttu-id="21841-195">**Plans de Service d’applications** qui n’ont aucun toothem applications associées peut toujours occasionner des frais, car ils continuent de capacité de calcul tooreserve hello.</span><span class="sxs-lookup"><span data-stu-id="21841-195">**App Service plans** that have no apps associated toothem still incur charges since they continue tooreserve hello compute capacity.</span></span>

<span data-ttu-id="21841-196">tooavoid inattendues frais, lors de l’application dernière hello est hébergée dans un plan App Service est supprimée, hello vide résultant plan App Service est également supprimé.</span><span class="sxs-lookup"><span data-stu-id="21841-196">tooavoid unexpected charges, when hello last app hosted in an App Service plan is deleted, hello resulting empty App Service plan is also deleted.</span></span>

## <a name="summary"></a><span data-ttu-id="21841-197">Résumé</span><span class="sxs-lookup"><span data-stu-id="21841-197">Summary</span></span>

<span data-ttu-id="21841-198">Les plans App Service représentent un ensemble de fonctionnalités et de capacités que vous pouvez partager entre vos différentes applications.</span><span class="sxs-lookup"><span data-stu-id="21841-198">App Service plans represent a set of features and capacity that you can share across your apps.</span></span> <span data-ttu-id="21841-199">Les plans de Service d’applications vous hello ensemble de tooa flexibilité tooallocate des applications spécifiques de ressources et optimisez votre utilisation des ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="21841-199">App Service plans give you hello flexibility tooallocate specific apps tooa set of resources and further optimize your Azure resource utilization.</span></span> <span data-ttu-id="21841-200">De cette manière, si vous souhaitez toosave money sur votre environnement de test, vous pouvez partager un plan entre plusieurs applications.</span><span class="sxs-lookup"><span data-stu-id="21841-200">This way, if you want toosave money on your testing environment, you can share a plan across multiple apps.</span></span> <span data-ttu-id="21841-201">Vous pouvez également augmenter le débit de votre environnement de production en le mettant à l'échelle dans plusieurs régions et plusieurs plans.</span><span class="sxs-lookup"><span data-stu-id="21841-201">You can also maximize throughput for your production environment by scaling it across multiple regions and plans.</span></span>

## <a name="whats-changed"></a><span data-ttu-id="21841-202">Changements apportés</span><span class="sxs-lookup"><span data-stu-id="21841-202">What's changed</span></span>

- <span data-ttu-id="21841-203">Pour une modification de toohello guide à partir de sites Web tooApp Service, consultez : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="21841-203">For a guide toohello change from Websites tooApp Service, see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

[pricingtier]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/appserviceplan-pricingtier.png
[assign]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/assing-appserviceplan.png
[change]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/change-appserviceplan.png
[createASP]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-appserviceplan.png
[createWebApp]: ./media/azure-web-sites-web-hosting-plans-in-depth-overview/create-web-app.png
