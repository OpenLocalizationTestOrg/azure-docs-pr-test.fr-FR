---
title: "implémentation de Mobile Engagement aaaAzure pour l’application de jeu"
description: "Jeu tooimplement de scénario d’application Azure Mobile Engagement"
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
ms.openlocfilehash: b82b4a868a33f42e5b759e43e66103556c097f9e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="cf966-103">Mise en œuvre de Mobile Engagement avec une application de jeu</span><span class="sxs-lookup"><span data-stu-id="cf966-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="cf966-104">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cf966-104">Overview</span></span>
<span data-ttu-id="cf966-105">Une jeune entreprise spécialisée dans les jeux a lancé un nouveau jeu de rôle/de stratégie sur le thème de la pêche.</span><span class="sxs-lookup"><span data-stu-id="cf966-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="cf966-106">jeu de Hello est en cours d’exécution pendant 6 mois.</span><span class="sxs-lookup"><span data-stu-id="cf966-106">hello game has been up and running for 6 months.</span></span> <span data-ttu-id="cf966-107">Ce jeu est un succès considérable et il a des millions de téléchargements et la rétention de hello est applications de jeu de démarrage très élevé tooother comparés.</span><span class="sxs-lookup"><span data-stu-id="cf966-107">This game is a huge success, and it has millions of downloads and hello retention is very high compared tooother start-up game apps.</span></span> <span data-ttu-id="cf966-108">À la réunion de révision de tous les trimestres de hello, les parties prenantes estiment que dont ils ont besoin de chiffre d’affaires moyen tooincrease par l’utilisateur (revenu moyen par abonné).</span><span class="sxs-lookup"><span data-stu-id="cf966-108">At hello quarterly review meeting, stakeholders agree they need tooincrease average revenue per user (ARPU).</span></span> <span data-ttu-id="cf966-109">Des packages au sein du jeu sont disponibles sous forme d’offres spéciales.</span><span class="sxs-lookup"><span data-stu-id="cf966-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="cf966-110">Ces packs jeu autoriser l’apparence de hello tooupgrade les utilisateurs et les performances de leurs lignes de pêche et appâts ou de s’attaque dans le jeu de hello.</span><span class="sxs-lookup"><span data-stu-id="cf966-110">These game packs allow users tooupgrade hello appearance and performance of their fishing lines and lures or tackles in hello game.</span></span> <span data-ttu-id="cf966-111">Toutefois, les ventes de package sont très faibles.</span><span class="sxs-lookup"><span data-stu-id="cf966-111">However, package sales are very low.</span></span> <span data-ttu-id="cf966-112">Afin de déterminer leur premier tooanalyze hello de l’expérience utilisateur avec un outil analytique, et puis toodevelop un engagement programme tooincrease ventes à l’aide de gestion avancée segmentation.</span><span class="sxs-lookup"><span data-stu-id="cf966-112">So they decide first tooanalyze hello customer experience with an analytics tool, and then toodevelop an engagement program tooincrease sales using advanced segmentation.</span></span>

<span data-ttu-id="cf966-113">En fonction de hello [Azure Mobile Engagement - Guide de démarrage avec les meilleures pratiques](mobile-engagement-getting-started-best-practices.md) qu’ils génèrent une stratégie d’engagement.</span><span class="sxs-lookup"><span data-stu-id="cf966-113">Based on hello [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="cf966-114">Objectifs et indicateurs clés de performance</span><span class="sxs-lookup"><span data-stu-id="cf966-114">Objectives and KPIs</span></span>
<span data-ttu-id="cf966-115">Principales parties prenantes pour répondre aux jeux de hello.</span><span class="sxs-lookup"><span data-stu-id="cf966-115">Key stakeholders for hello game meet.</span></span> <span data-ttu-id="cf966-116">Tous les s’accorder sur un objectif principal - ventes de package tooincrease premium de 15 %.</span><span class="sxs-lookup"><span data-stu-id="cf966-116">All agree on one main objective - tooincrease premium package sales by 15%.</span></span> <span data-ttu-id="cf966-117">Ils créent lecteur et entreprise indicateurs de Performance clés (KPI) toomeasure cet objectif</span><span class="sxs-lookup"><span data-stu-id="cf966-117">They create Business Key Performance Indicators (KPIs) toomeasure and drive this objective</span></span>

* <span data-ttu-id="cf966-118">Sur quel niveau de jeu de hello ces packages sont achetés ?</span><span class="sxs-lookup"><span data-stu-id="cf966-118">On which level of hello game are these packages purchased?</span></span>
* <span data-ttu-id="cf966-119">Quel est le chiffre d’affaires hello par utilisateur, par session, par semaine et par mois ?</span><span class="sxs-lookup"><span data-stu-id="cf966-119">What is hello revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="cf966-120">Quels sont les types de fournisseur favori hello ?</span><span class="sxs-lookup"><span data-stu-id="cf966-120">What are hello favorite purchase types?</span></span>

<span data-ttu-id="cf966-121">Partie 1 sur hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explique comment toodefine hello objectifs et des indicateurs de performance clés.</span><span class="sxs-lookup"><span data-stu-id="cf966-121">Part 1 of hello [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how toodefine hello objectives and KPIs.</span></span> 

<span data-ttu-id="cf966-122">Hello de qu'indicateurs de performance clés Business est maintenant défini, hello Mobile Product Manager crée rétention et les tendances des utilisateurs nouveaux indicateurs de performance clés Engagement toodetermine.</span><span class="sxs-lookup"><span data-stu-id="cf966-122">With hello Business KPIs now defined, hello Mobile Product Manager creates Engagement KPIs toodetermine new user trends and retention.</span></span>

* <span data-ttu-id="cf966-123">Rétention de surveiller et d’utiliser le sur hello suivant des intervalles : tous les jours, toutes les 2 jours, hebdomadaire, mensuelle et tous les 3 mois</span><span class="sxs-lookup"><span data-stu-id="cf966-123">Monitor retention and use across hello following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="cf966-124">Nombre d’utilisateurs actifs</span><span class="sxs-lookup"><span data-stu-id="cf966-124">Active user counts</span></span>
* <span data-ttu-id="cf966-125">classification des applications Hello Bonjour stocker</span><span class="sxs-lookup"><span data-stu-id="cf966-125">hello app rating in hello store</span></span>

<span data-ttu-id="cf966-126">Selon les recommandations de l’équipe informatique de hello, hello suivant techniques indicateurs de performance clés ont été ajoutée hello tooanswer suivant questions :</span><span class="sxs-lookup"><span data-stu-id="cf966-126">Based on recommendations from hello IT team, hello following technical KPIs were added tooanswer hello following questions:</span></span>

* <span data-ttu-id="cf966-127">Quel est mon parcours utilisateur (page visitée, temps passé dessus par l’utilisateur) ?</span><span class="sxs-lookup"><span data-stu-id="cf966-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="cf966-128">Quel est le nombre de pannes ou de bogues par session ?</span><span class="sxs-lookup"><span data-stu-id="cf966-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="cf966-129">Quelles sont les versions de système d’exploitation exécutées par mes utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="cf966-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="cf966-130">Quelle est hello de taille moyenne de l’écran pour mes utilisateurs ?</span><span class="sxs-lookup"><span data-stu-id="cf966-130">What is hello average size of screen for my users?</span></span>
* <span data-ttu-id="cf966-131">De quels types de connectivité Internet mes utilisateurs doivent-ils disposer ?</span><span class="sxs-lookup"><span data-stu-id="cf966-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="cf966-132">Pour chaque indicateur de performance clé hello Mobile Product Manager spécifie les données de hello dont elle a besoin et où il se trouve dans son manuel.</span><span class="sxs-lookup"><span data-stu-id="cf966-132">For each KPI hello Mobile Product Manager specifies hello data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="cf966-133">Programme d’engagement et intégration</span><span class="sxs-lookup"><span data-stu-id="cf966-133">Engagement program and integration</span></span>
<span data-ttu-id="cf966-134">Avant de générer un programme engagement avancées, hello directeur du projet Mobile responsable de projet de hello doit avoir une compréhension approfondie des quand et comment les produits sont consommés par les utilisateurs de hello.</span><span class="sxs-lookup"><span data-stu-id="cf966-134">Before building an advanced engagement program, hello Mobile Project Director in charge of hello project should have a deep understanding of how and when products are consumed by hello users.</span></span>

<span data-ttu-id="cf966-135">Après 3 mois, hello directeur du projet Mobile a collecté suffisamment tooenhance données ses ventes de notification par envoi de données dans l’application.</span><span class="sxs-lookup"><span data-stu-id="cf966-135">After 3 months, hello Mobile Project Director has collected enough data tooenhance his in-app push notification sales.</span></span> <span data-ttu-id="cf966-136">Il a notamment appris que :</span><span class="sxs-lookup"><span data-stu-id="cf966-136">He learns that:</span></span>

* <span data-ttu-id="cf966-137">premier achat de Hello se produit généralement au niveau de hello 14.</span><span class="sxs-lookup"><span data-stu-id="cf966-137">hello first purchase generally happens at hello level 14.</span></span> <span data-ttu-id="cf966-138">Pour 90 % des cas, achat de hello est nouvelles armes reposant pour $3.</span><span class="sxs-lookup"><span data-stu-id="cf966-138">For 90% of those cases, hello purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="cf966-139">De 80 % des cas, les utilisateurs qui ont effectué un achat, continuez avec le produit de hello et effectuez plusieurs achats.</span><span class="sxs-lookup"><span data-stu-id="cf966-139">In 80 % of those cases, users who have made a purchase, continue with hello product and make more purchases.</span></span>
* <span data-ttu-id="cf966-140">Les utilisateurs qui ont passé le niveau hello 20, démarrer toospend plus de 10 $par semaine.</span><span class="sxs-lookup"><span data-stu-id="cf966-140">Users who have passed hello level 20, start toospend more than $10/week.</span></span>
* <span data-ttu-id="cf966-141">Les utilisateurs ont tendance à toobuy les packages premium au niveau 16, 24 et 32.</span><span class="sxs-lookup"><span data-stu-id="cf966-141">Users tend toobuy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="cf966-142">Merci d’analyse toothis hello directeur du projet Mobile décide toocreate push spécifique notification séquences tooincrease dans les ventes de l’application.</span><span class="sxs-lookup"><span data-stu-id="cf966-142">Thanks toothis analysis hello Mobile Project Director decides toocreate specific push notification sequences tooincrease in app sales.</span></span> <span data-ttu-id="cf966-143">Il crée trois séquences Push qu’il nomme respectivement Bienvenue dans le programme, Programme commercial et Programme inactif.</span><span class="sxs-lookup"><span data-stu-id="cf966-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="cf966-144">Pour plus d’informations, consultez toohello [règles](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks)![][1]</span><span class="sxs-lookup"><span data-stu-id="cf966-144">For more information refer toohello [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: ./media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->
