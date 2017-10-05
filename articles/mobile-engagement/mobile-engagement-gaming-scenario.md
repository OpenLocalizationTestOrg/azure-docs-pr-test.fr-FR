---
title: "Mise en œuvre d’Azure Mobile Engagement avec une application de jeux"
description: "Scénario d’application de jeux pour mettre en œuvre Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 0ca35a3d634db8eb5c63afacba046a35b8a3e7ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="34e29-103">Mise en œuvre de Mobile Engagement avec une application de jeu</span><span class="sxs-lookup"><span data-stu-id="34e29-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="34e29-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="34e29-104">Overview</span></span>
<span data-ttu-id="34e29-105">Une jeune entreprise spécialisée dans les jeux a lancé un nouveau jeu de rôle/de stratégie sur le thème de la pêche.</span><span class="sxs-lookup"><span data-stu-id="34e29-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="34e29-106">Ce jeu est opérationnel depuis 6 mois.</span><span class="sxs-lookup"><span data-stu-id="34e29-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="34e29-107">Il connaît un énorme succès et a été téléchargé des millions de fois. De plus, la rétention est très élevée par rapport à d’autres applications de jeu.</span><span class="sxs-lookup"><span data-stu-id="34e29-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="34e29-108">Lors de la réunion d’examen trimestrielle, les différents intervenants estiment qu’ils doivent augmenter les revenus moyens par utilisateur (revenu moyen par abonné).</span><span class="sxs-lookup"><span data-stu-id="34e29-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="34e29-109">Des packages au sein du jeu sont disponibles sous forme d’offres spéciales.</span><span class="sxs-lookup"><span data-stu-id="34e29-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="34e29-110">Ces packages de jeu permettent aux utilisateurs de mettre à niveau l’apparence et les performances de leurs lignes de pêche et des appâts et des articles au sein du jeu.</span><span class="sxs-lookup"><span data-stu-id="34e29-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="34e29-111">Toutefois, les ventes de package sont très faibles.</span><span class="sxs-lookup"><span data-stu-id="34e29-111">However, package sales are very low.</span></span> <span data-ttu-id="34e29-112">Par conséquent, il a été décidé dans un premier temps d’analyser l’expérience client à l’aide d’un outil d’analyse, puis de développer un programme d’engagement afin d’augmenter les ventes au moyen d’une segmentation avancée.</span><span class="sxs-lookup"><span data-stu-id="34e29-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="34e29-113">En s’appuyant sur [Azure Mobile Engagement - Guide de prise en main et meilleures pratiques](mobile-engagement-getting-started-best-practices.md) , ils ont élaboré une stratégie d’engagement.</span><span class="sxs-lookup"><span data-stu-id="34e29-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="34e29-114">Objectifs et indicateurs clés de performance</span><span class="sxs-lookup"><span data-stu-id="34e29-114">Objectives and KPIs</span></span>
<span data-ttu-id="34e29-115">Les différents intervenants du jeu se réunissent.</span><span class="sxs-lookup"><span data-stu-id="34e29-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="34e29-116">Tous les intervenants sont d’accord sur un objectif principal : augmenter les ventes de packages premium de 15 %.</span><span class="sxs-lookup"><span data-stu-id="34e29-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="34e29-117">Ils créent des indicateurs clés de performance (KPI) pour mesurer et atteindre cet objectif.</span><span class="sxs-lookup"><span data-stu-id="34e29-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="34e29-118">À quel niveau de la partie ces packages sont-ils achetés ?</span><span class="sxs-lookup"><span data-stu-id="34e29-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="34e29-119">Quel est le chiffre d’affaires par utilisateur, par session, par semaine et par mois ?</span><span class="sxs-lookup"><span data-stu-id="34e29-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="34e29-120">Quels sont les types d’achats préférés ?</span><span class="sxs-lookup"><span data-stu-id="34e29-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="34e29-121">La première partie du [Guide de prise en main](mobile-engagement-getting-started-best-practices.md) explique comment définir des objectifs et des indicateurs de performance clés.</span><span class="sxs-lookup"><span data-stu-id="34e29-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="34e29-122">Une fois les indicateurs de performance clés d’entreprise définis, le responsable de produit mobile crée des indicateurs clés de performance clés pour déterminer les nouvelles tendances et rétention utilisateur.</span><span class="sxs-lookup"><span data-stu-id="34e29-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="34e29-123">Contrôler la rétention et l’utilisation pendant les intervalles suivants : quotidien, tous les 2 jours, hebdomadaire, mensuel et trimestriel</span><span class="sxs-lookup"><span data-stu-id="34e29-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="34e29-124">Nombre d’utilisateurs actifs</span><span class="sxs-lookup"><span data-stu-id="34e29-124">Active user counts</span></span>
* <span data-ttu-id="34e29-125">Évaluation de l’application dans le Windows Store</span><span class="sxs-lookup"><span data-stu-id="34e29-125">The app rating in the store</span></span>

<span data-ttu-id="34e29-126">Selon les recommandations de l’équipe informatique, les indicateurs clés de performance techniques suivants ont été ajoutés pour répondre aux questions suivantes :</span><span class="sxs-lookup"><span data-stu-id="34e29-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="34e29-127">Quel est mon parcours utilisateur (page visitée, temps passé dessus par l’utilisateur) ?</span><span class="sxs-lookup"><span data-stu-id="34e29-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="34e29-128">Quel est le nombre de pannes ou de bogues par session ?</span><span class="sxs-lookup"><span data-stu-id="34e29-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="34e29-129">Quelles sont les versions de système d’exploitation exécutées par mes utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="34e29-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="34e29-130">Quelle est la taille moyenne de l’écran de mes utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="34e29-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="34e29-131">De quels types de connectivité Internet mes utilisateurs doivent-ils disposer ?</span><span class="sxs-lookup"><span data-stu-id="34e29-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="34e29-132">Pour chaque indicateur de performance, le responsable de produit mobile spécifie les données nécessaires et l’endroit du manuel où elles se trouvent.</span><span class="sxs-lookup"><span data-stu-id="34e29-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="34e29-133">Programme d’engagement et intégration</span><span class="sxs-lookup"><span data-stu-id="34e29-133">Engagement program and integration</span></span>
<span data-ttu-id="34e29-134">Avant de réaliser un programme d’engagement avancé, le responsable de projet mobile en charge doit bien connaître la manière et les moments où les produits sont consommés par les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="34e29-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="34e29-135">Après 3 mois, le responsable de projet mobile a recueilli suffisamment de données pour améliorer ses ventes par notification Push au sein de l’application.</span><span class="sxs-lookup"><span data-stu-id="34e29-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="34e29-136">Il a notamment appris que :</span><span class="sxs-lookup"><span data-stu-id="34e29-136">He learns that:</span></span>

* <span data-ttu-id="34e29-137">Le premier achat a généralement lieu au niveau 14.</span><span class="sxs-lookup"><span data-stu-id="34e29-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="34e29-138">Dans 90 % des cas, l’achat concerne des armes légendaires de 3 $.</span><span class="sxs-lookup"><span data-stu-id="34e29-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="34e29-139">Dans 80 % des cas, les utilisateurs qui ont effectué un achat continuent avec le produit et effectuent d’autres achats.</span><span class="sxs-lookup"><span data-stu-id="34e29-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="34e29-140">Les utilisateurs qui ont réussi le niveau 20 commencent à dépenser plus de 10 $/semaine.</span><span class="sxs-lookup"><span data-stu-id="34e29-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="34e29-141">Les utilisateurs ont tendance à acheter des packages premium aux niveaux 16, 24 et 32.</span><span class="sxs-lookup"><span data-stu-id="34e29-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="34e29-142">Grâce à cette analyse, le responsable de projet mobile décide de créer des séquences de notification Push spécifiques pour augmenter les ventes d’application.</span><span class="sxs-lookup"><span data-stu-id="34e29-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="34e29-143">Il crée trois séquences Push qu’il nomme respectivement Bienvenue dans le programme, Programme commercial et Programme inactif.</span><span class="sxs-lookup"><span data-stu-id="34e29-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="34e29-144">Pour plus d’informations, reportez-vous à la [règles](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="34e29-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
