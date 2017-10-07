---
title: "aaaData des stratégies d’accès dans la série de temps Azure Insights | Documents Microsoft"
description: "Dans ce didacticiel, vous apprendre les stratégies d’accès données toomanage temps série Insights"
keywords: 
services: time-series-insights
documentationcenter: 
author: op-ravi
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/01/2017
ms.author: omravi
ms.openlocfilehash: f286d26c8c5c851c523e9384760dc4b10711fa3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-data-access-tooa-time-series-insights-environment-using-azure-portal"></a><span data-ttu-id="5023e-103">Accorder l’environnement d’un aperçu en temps série tooa accès aux données à l’aide du portail Azure</span><span class="sxs-lookup"><span data-stu-id="5023e-103">Grant data access tooa Time Series Insights environment using Azure portal</span></span>

<span data-ttu-id="5023e-104">Les environnements Time Series Insights comprennent deux types indépendants des stratégies d’accès :</span><span class="sxs-lookup"><span data-stu-id="5023e-104">Time Series Insights environments have two independent types of access policies:</span></span>

* <span data-ttu-id="5023e-105">Stratégies d’accès de gestion</span><span class="sxs-lookup"><span data-stu-id="5023e-105">Management access policies</span></span>
* <span data-ttu-id="5023e-106">Stratégies d’accès aux données</span><span class="sxs-lookup"><span data-stu-id="5023e-106">Data access policies</span></span>

<span data-ttu-id="5023e-107">Ces deux stratégies accordent aux principaux Azure Active Directory (utilisateurs et applications) diverses autorisations sur un environnement spécifique.</span><span class="sxs-lookup"><span data-stu-id="5023e-107">Both policies grant Azure Active Directory principals (users and apps) various permissions on a particular environment.</span></span> <span data-ttu-id="5023e-108">Hello principaux (utilisateurs et applications) doit appartenir toohello active directory (ou « tenant Azure ») associés à abonnement hello contenant l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-108">hello principals (users and apps) must belong toohello active directory (or “Azure tenant”) associated with hello subscription containing hello environment.</span></span>

<span data-ttu-id="5023e-109">Stratégies de gestion des accès accordent configuration toohello connexes d’autorisations de l’environnement de hello, telles que</span><span class="sxs-lookup"><span data-stu-id="5023e-109">Management access policies grant permissions related toohello configuration of hello environment, such as</span></span>
*   <span data-ttu-id="5023e-110">Création et suppression de l’environnement hello, sources d’événements, référencent des jeux de données, et</span><span class="sxs-lookup"><span data-stu-id="5023e-110">Creation and deletion of hello environment, event sources, reference data sets, and</span></span>
*   <span data-ttu-id="5023e-111">Gestion des stratégies d’accès données hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-111">Management of hello data access policies.</span></span>

<span data-ttu-id="5023e-112">Stratégies d’accès aux données accorder des autorisations tooissue des requêtes, manipulent les données de référence dans l’environnement de hello et partagent des requêtes enregistrées et perspectives associées hello environnement.</span><span class="sxs-lookup"><span data-stu-id="5023e-112">Data access policies grant permissions tooissue data queries, manipulate reference data in hello environment, and share saved queries and perspectives associated with hello environment.</span></span>

<span data-ttu-id="5023e-113">Hello deux types de stratégies d’autoriser une séparation claire entre toohello gestion de l’accès de l’environnement de hello et accéder aux données de toohello au sein de l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-113">hello two kinds of policies allow clear separation between access toohello management of hello environment and access toohello data inside hello environment.</span></span> <span data-ttu-id="5023e-114">Par exemple, il est possible toosetup un environnement telles que hello propriétaire/créateur de l’environnement de hello est supprimé de l’accès aux données hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-114">For example, it is possible toosetup an environment such that hello owner/creator of hello environment is removed from hello data access.</span></span> <span data-ttu-id="5023e-115">Ainsi que les utilisateurs et les services qui sont autorisés à tooread des données à partir de l’environnement de hello peut bénéficier sans configuration toohello d’accès de l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-115">As well as users and services that are allowed tooread data from hello environment may be granted no access toohello configuration of hello environment.</span></span>

## <a name="grant-data-access"></a><span data-ttu-id="5023e-116">Accorder l’accès aux données</span><span class="sxs-lookup"><span data-stu-id="5023e-116">Grant data access</span></span>
<span data-ttu-id="5023e-117">Hello étapes suivantes montrent comment d’accès aux données de toogrant pour un utilisateur principal :</span><span class="sxs-lookup"><span data-stu-id="5023e-117">hello following steps show how toogrant data access for a user principal:</span></span>

1.  <span data-ttu-id="5023e-118">Connectez-vous à toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="5023e-118">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2.  <span data-ttu-id="5023e-119">Cliquez sur « Toutes les ressources » dans le menu hello hello situé à gauche de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="5023e-119">Click “All resources” in hello menu on hello left side of hello Azure portal.</span></span>
3.  <span data-ttu-id="5023e-120">Sélectionnez votre environnement Time Series Insights.</span><span class="sxs-lookup"><span data-stu-id="5023e-120">Select your Time Series Insights environment.</span></span>

  ![Gérer la source de temps série Insights hello - environnement](media/data-access/getstarted-grant-data-access1.png)

4.  <span data-ttu-id="5023e-122">Sélectionnez « Accès au plan de données », puis cliquez sur « Ajouter »</span><span class="sxs-lookup"><span data-stu-id="5023e-122">Select “Data Plane Access”, click “Add”</span></span>

  ![Gérer la source de temps série Insights hello - ajouter](media/data-access/getstarted-grant-data-access2.png)

5.  <span data-ttu-id="5023e-124">Cliquez sur « Sélectionner un utilisateur ».</span><span class="sxs-lookup"><span data-stu-id="5023e-124">Click “Select user”.</span></span>
6.  <span data-ttu-id="5023e-125">Recherchez et sélectionnez l’utilisateur par courrier électronique de hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-125">Search and select user by hello email.</span></span>
7.  <span data-ttu-id="5023e-126">Cliquez sur « Sélectionner » dans le panneau « Sélectionner un utilisateur ».</span><span class="sxs-lookup"><span data-stu-id="5023e-126">Click “Select” in “Select User” blade.</span></span>

  ![Gérer la source de temps série Insights hello - sélectionnez l’utilisateur](media/data-access/getstarted-grant-data-access3.png)

8.  <span data-ttu-id="5023e-128">Cliquez sur « Sélectionner un rôle ».</span><span class="sxs-lookup"><span data-stu-id="5023e-128">Click “Select role”.</span></span>
9.  <span data-ttu-id="5023e-129">Sélectionnez « Contributeur » si vous souhaitez que les données de référence toochange tooallow utilisateur et de partagez des requêtes enregistrées et perspectives avec d’autres utilisateurs de l’environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-129">Select “Contributor” if you want tooallow user toochange reference data and share saved queries and perspectives with other users of hello environment.</span></span> <span data-ttu-id="5023e-130">Dans le cas contraire, sélectionner des données de requête « Lecture » tooallow utilisateur dans l’environnement de hello et enregistrer des requêtes personnelles (non partagés) dans un environnement de hello.</span><span class="sxs-lookup"><span data-stu-id="5023e-130">Otherwise select “Reader” tooallow user query data in hello environment and save personal (not shared) queries in hello environment.</span></span>
10. <span data-ttu-id="5023e-131">Dans le panneau de « Sélectionner un rôle » hello, cliquez sur « Ok ».</span><span class="sxs-lookup"><span data-stu-id="5023e-131">Click “Ok” in hello “Select Role” blade.</span></span>

  ![Gérer la source de temps série Insights hello - sélectionner un rôle](media/data-access/getstarted-grant-data-access4.png)

11. <span data-ttu-id="5023e-133">Dans le panneau de « Rôle d’utilisateur de sélectionner » hello, cliquez sur « Ok ».</span><span class="sxs-lookup"><span data-stu-id="5023e-133">Click “Ok” in hello “Select User Role” blade.</span></span>
12. <span data-ttu-id="5023e-134">Ce qui suit doit s’afficher :</span><span class="sxs-lookup"><span data-stu-id="5023e-134">You should see:</span></span>

  ![Gérer la source de temps série Insights hello - résultats](media/data-access/getstarted-grant-data-access5.png)

## <a name="next-steps"></a><span data-ttu-id="5023e-136">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5023e-136">Next steps</span></span>

* [<span data-ttu-id="5023e-137">Créer une source d’événement</span><span class="sxs-lookup"><span data-stu-id="5023e-137">Create an event source</span></span>](time-series-insights-add-event-source.md)
* <span data-ttu-id="5023e-138">[Envoyer des événements](time-series-insights-send-events.md) toohello source d’événement</span><span class="sxs-lookup"><span data-stu-id="5023e-138">[Send events](time-series-insights-send-events.md) toohello event source</span></span>
* <span data-ttu-id="5023e-139">Afficher votre environnement dans le [Portail Time Series Insights](https://insights.timeseries.azure.com)</span><span class="sxs-lookup"><span data-stu-id="5023e-139">View your environment in [Time Series Insights Portal](https://insights.timeseries.azure.com)</span></span>
