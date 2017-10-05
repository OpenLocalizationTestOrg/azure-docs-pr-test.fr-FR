---
title: "Rapports d’activité de connexion dans le portail Azure Active Directory | Microsoft Docs"
description: "Présentation des rapports d’activité de connexion dans le portail Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 4b18127b-d1d0-4bdc-8f9c-6a4c991c5f75
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: b9e61950654ba427b09dd608d354589a0804aaa5
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="sign-in-activity-reports-in-the-azure-active-directory-portal"></a><span data-ttu-id="4468b-103">Rapports d’activité de connexion dans le portail Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4468b-103">Sign-in activity reports in the Azure Active Directory portal</span></span>

<span data-ttu-id="4468b-104">Grâce à la fonction de création de rapports Azure Active Directory (Azure AD) dans le [portail Azure](https://portal.azure.com), vous pouvez obtenir les informations dont vous avez besoin pour évaluer l’état de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="4468b-104">With Azure Active Directory (Azure AD) reporting in the [Azure portal](https://portal.azure.com), you can get the information you need to determine how your environment is doing.</span></span>

<span data-ttu-id="4468b-105">L’architecture de création de rapports dans Azure Active Directory comprend les composants suivants :</span><span class="sxs-lookup"><span data-stu-id="4468b-105">The reporting architecture in Azure Active Directory consists of the following components:</span></span>

- <span data-ttu-id="4468b-106">**Activité**</span><span class="sxs-lookup"><span data-stu-id="4468b-106">**Activity**</span></span> 
    - <span data-ttu-id="4468b-107">**Activités de connexion** – Informations sur l’utilisation des applications gérées et les activités de connexion des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4468b-107">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="4468b-108">**Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire.</span><span class="sxs-lookup"><span data-stu-id="4468b-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="4468b-109">**Sécurité**</span><span class="sxs-lookup"><span data-stu-id="4468b-109">**Security**</span></span> 
    - <span data-ttu-id="4468b-110">**Connexions risquées** : une connexion risquée est une tentative de connexion susceptible de provenir d’un utilisateur autre que le propriétaire légitime d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4468b-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="4468b-111">Pour en savoir plus, consultez Connexions risquées.</span><span class="sxs-lookup"><span data-stu-id="4468b-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="4468b-112">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="4468b-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="4468b-113">Pour en savoir plus, consultez Utilisateurs avec indicateur de risque.</span><span class="sxs-lookup"><span data-stu-id="4468b-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="4468b-114">Cette rubrique vous donne une vue d’ensemble des activités de connexion.</span><span class="sxs-lookup"><span data-stu-id="4468b-114">This topic gives you an overview of the sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="4468b-115">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="4468b-115">Pre-requisite</span></span>

### <a name="who-can-access-the-data"></a><span data-ttu-id="4468b-116">Qui peut accéder aux données ?</span><span class="sxs-lookup"><span data-stu-id="4468b-116">Who can access the data?</span></span>
* <span data-ttu-id="4468b-117">Utilisateurs ayant le rôle d’administrateur de sécurité ou de lecteur de la sécurité</span><span class="sxs-lookup"><span data-stu-id="4468b-117">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="4468b-118">Administrateurs généraux</span><span class="sxs-lookup"><span data-stu-id="4468b-118">Global Admins</span></span>
* <span data-ttu-id="4468b-119">Tous les utilisateurs (non administrateurs) peuvent accéder à leurs propres connexions</span><span class="sxs-lookup"><span data-stu-id="4468b-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-to-access-sign-in-activity"></a><span data-ttu-id="4468b-120">De quelle licence Azure AD avez-vous besoin pour accéder à l’activité de connexion ?</span><span class="sxs-lookup"><span data-stu-id="4468b-120">What Azure AD license do you need to access sign-in activity?</span></span>
* <span data-ttu-id="4468b-121">Votre client doit avoir une licence Azure AD Premium associée pour afficher tous les rapports d’activités de connexion.</span><span class="sxs-lookup"><span data-stu-id="4468b-121">Your tenant must have an Azure AD Premium license associated with it to see the all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="4468b-122">Activités de connexion</span><span class="sxs-lookup"><span data-stu-id="4468b-122">Signs-in activities</span></span>

<span data-ttu-id="4468b-123">Avec les informations fournies par le rapport sur les connexions des utilisateurs, trouvez des réponses aux questions telles que :</span><span class="sxs-lookup"><span data-stu-id="4468b-123">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

* <span data-ttu-id="4468b-124">Quel est le modèle de connexion d’un utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="4468b-124">What is the sign-in pattern of a user?</span></span>
* <span data-ttu-id="4468b-125">Combien d’utilisateurs se sont connectés au cours d’une semaine ?</span><span class="sxs-lookup"><span data-stu-id="4468b-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="4468b-126">Quel est l’état de ces connexions ?</span><span class="sxs-lookup"><span data-stu-id="4468b-126">What’s the status of these sign-ins?</span></span>

<span data-ttu-id="4468b-127">La zone **Connexions** de la section Activité de **Azure Active** constitue votre premier point d’entrée pour toutes les activités de connexion.</span><span class="sxs-lookup"><span data-stu-id="4468b-127">Your first entry point to all sign-in activities data is **Sign-ins** in the Activity section of **Azure Active**.</span></span>


<span data-ttu-id="4468b-128">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/61.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="4468b-129">Un journal d’audit inclut un mode Liste par défaut, qui indique :</span><span class="sxs-lookup"><span data-stu-id="4468b-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="4468b-130">l’utilisateur associé ;</span><span class="sxs-lookup"><span data-stu-id="4468b-130">the related user</span></span>
- <span data-ttu-id="4468b-131">l’application à laquelle l’utilisateur est connecté ;</span><span class="sxs-lookup"><span data-stu-id="4468b-131">the application the user has signed-in to</span></span>
- <span data-ttu-id="4468b-132">l’état de la connexion ;</span><span class="sxs-lookup"><span data-stu-id="4468b-132">the sign-in status</span></span>
- <span data-ttu-id="4468b-133">l’heure de la connexion.</span><span class="sxs-lookup"><span data-stu-id="4468b-133">the sign-in time</span></span>

<span data-ttu-id="4468b-134">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/41.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-135">Vous pouvez personnaliser le mode Liste en cliquant sur **Colonnes** dans la barre d’outils.</span><span class="sxs-lookup"><span data-stu-id="4468b-135">You can customize the list view by clicking **Columns** in the toolbar.</span></span>

<span data-ttu-id="4468b-136">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/19.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-137">Cela vous permet d’afficher des champs supplémentaires, ou de supprimer des champs qui sont déjà affichés.</span><span class="sxs-lookup"><span data-stu-id="4468b-137">This enables you to display additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="4468b-138">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/42.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-139">En cliquant sur un élément dans le mode Liste, vous pouvez obtenir toutes les informations disponibles le concernant.</span><span class="sxs-lookup"><span data-stu-id="4468b-139">By clicking an item in the list view, you get all available details about it.</span></span>

<span data-ttu-id="4468b-140">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/43.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="4468b-141">Filtrage des activités de connexion</span><span class="sxs-lookup"><span data-stu-id="4468b-141">Filtering sign-in activities</span></span>

<span data-ttu-id="4468b-142">Pour limiter les données transmises à un niveau qui vous convient, vous pouvez filtrer les données de connexion à l’aide des champs suivants :</span><span class="sxs-lookup"><span data-stu-id="4468b-142">To narrow down the reported data to a level that works for you, you can filter the sign-ins data using the following fields:</span></span>

- <span data-ttu-id="4468b-143">Intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="4468b-143">Time interval</span></span>
- <span data-ttu-id="4468b-144">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="4468b-144">User</span></span>
- <span data-ttu-id="4468b-145">Application</span><span class="sxs-lookup"><span data-stu-id="4468b-145">Application</span></span>
- <span data-ttu-id="4468b-146">Client</span><span class="sxs-lookup"><span data-stu-id="4468b-146">Client</span></span>
- <span data-ttu-id="4468b-147">État de la connexion</span><span class="sxs-lookup"><span data-stu-id="4468b-147">Sign-in status</span></span>

<span data-ttu-id="4468b-148">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/44.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="4468b-149">Le filtre **Intervalle de temps** vous permet de définir un intervalle de temps pour les données renvoyées.</span><span class="sxs-lookup"><span data-stu-id="4468b-149">The **time interval** filter enables to you to define a timeframe for the returned data.</span></span>  
<span data-ttu-id="4468b-150">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="4468b-150">Possible values are:</span></span>

- <span data-ttu-id="4468b-151">1 mois</span><span class="sxs-lookup"><span data-stu-id="4468b-151">1 month</span></span>
- <span data-ttu-id="4468b-152">7 jours</span><span class="sxs-lookup"><span data-stu-id="4468b-152">7 days</span></span>
- <span data-ttu-id="4468b-153">24 heures</span><span class="sxs-lookup"><span data-stu-id="4468b-153">24 hours</span></span>
- <span data-ttu-id="4468b-154">Personnalisée</span><span class="sxs-lookup"><span data-stu-id="4468b-154">Custom</span></span>

<span data-ttu-id="4468b-155">Lorsque vous sélectionnez une plage personnalisée, vous pouvez configurer une heure de début et une heure de fin.</span><span class="sxs-lookup"><span data-stu-id="4468b-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="4468b-156">Le filtre **Utilisateur** vous permet de spécifier le nom ou le nom d’utilisateur principal de l’utilisateur qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="4468b-156">The **user** filter enables you to specify the name or the user principal name (UPN) of the user you care about.</span></span>

<span data-ttu-id="4468b-157">Le filtre **Application** vous permet de spécifier le nom de l’application qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="4468b-157">The **application** filter enables you to specify the name of the application you care about.</span></span>

<span data-ttu-id="4468b-158">Le filtre **Client** vous permet de spécifier des informations sur l’appareil qui vous intéresse.</span><span class="sxs-lookup"><span data-stu-id="4468b-158">The **client** filter enables you to specify information about the device you care about.</span></span>

<span data-ttu-id="4468b-159">Le filtre **État de la connexion** vous permet de sélectionner l’un des filtres suivants :</span><span class="sxs-lookup"><span data-stu-id="4468b-159">The **sign-in status** filter enables you to select one of the following filter:</span></span>

- <span data-ttu-id="4468b-160">Tout</span><span class="sxs-lookup"><span data-stu-id="4468b-160">All</span></span>
- <span data-ttu-id="4468b-161">Succès</span><span class="sxs-lookup"><span data-stu-id="4468b-161">Success</span></span>
- <span data-ttu-id="4468b-162">Échec</span><span class="sxs-lookup"><span data-stu-id="4468b-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="4468b-163">Raccourcis relatifs aux activités de connexion</span><span class="sxs-lookup"><span data-stu-id="4468b-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="4468b-164">En plus d’Azure Active Directory, le portail Azure vous offre deux autres points d’entrée pour les données sur les activités de connexion :</span><span class="sxs-lookup"><span data-stu-id="4468b-164">In addition to Azure Active Directory, the Azure portal provides you with two additional entry points to sign-in activities data:</span></span>

- <span data-ttu-id="4468b-165">Utilisateurs et groupes</span><span class="sxs-lookup"><span data-stu-id="4468b-165">Users and groups</span></span>
- <span data-ttu-id="4468b-166">Applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="4468b-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="4468b-167">Activités de connexion des utilisateurs et des groupes</span><span class="sxs-lookup"><span data-stu-id="4468b-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="4468b-168">Avec les informations fournies par le rapport sur les connexions des utilisateurs, trouvez des réponses aux questions telles que :</span><span class="sxs-lookup"><span data-stu-id="4468b-168">With the information provided by the user sign-in report, you find answers to questions such as:</span></span>

- <span data-ttu-id="4468b-169">Quel est le modèle de connexion d’un utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="4468b-169">What is the sign-in pattern of a user?</span></span>
- <span data-ttu-id="4468b-170">Combien d’utilisateurs se sont connectés au cours d’une semaine ?</span><span class="sxs-lookup"><span data-stu-id="4468b-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="4468b-171">Quel est l’état de ces connexions ?</span><span class="sxs-lookup"><span data-stu-id="4468b-171">What’s the status of these sign-ins?</span></span>



<span data-ttu-id="4468b-172">Votre point d’entrée pour ces données est le graphique des connexions des utilisateurs dans la section **Overview** (Vue d’ensemble) sous **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="4468b-172">Your entry point to this data is the user sign-in graph in the **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="4468b-173">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/45.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-174">Le graphique des connexions des utilisateurs affiche les agrégations hebdomadaires des connexions de tous les utilisateurs au cours d’une période donnée.</span><span class="sxs-lookup"><span data-stu-id="4468b-174">The user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="4468b-175">La valeur par défaut de cette période est de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="4468b-175">The default for the time period is 30 days.</span></span>

<span data-ttu-id="4468b-176">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/46.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-177">Lorsque vous cliquez sur un jour dans le graphique des connexions, vous obtenez une liste détaillée des activités de connexion correspondantes.</span><span class="sxs-lookup"><span data-stu-id="4468b-177">When you click on a day in the sign-in graph, you get a detailed list of the sign-in activities for this day.</span></span>

<span data-ttu-id="4468b-178">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/41.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-179">Chaque ligne dans la liste des activités de connexion vous fournit des informations détaillées sur la connexion sélectionnée, par exemple :</span><span class="sxs-lookup"><span data-stu-id="4468b-179">Each row in the sign-in activities list gives you the detailed information about the selected sign-in such as:</span></span>

* <span data-ttu-id="4468b-180">Qui s’est connecté ?</span><span class="sxs-lookup"><span data-stu-id="4468b-180">Who has signed in?</span></span>
* <span data-ttu-id="4468b-181">Qui a l’UPN associé ?</span><span class="sxs-lookup"><span data-stu-id="4468b-181">What was the related UPN?</span></span>
* <span data-ttu-id="4468b-182">Quelle application a été la cible de la connexion ?</span><span class="sxs-lookup"><span data-stu-id="4468b-182">What application was the target of the sign-in?</span></span>
* <span data-ttu-id="4468b-183">Quelle est l’adresse IP de la connexion ?</span><span class="sxs-lookup"><span data-stu-id="4468b-183">What is the IP address of the sign-in?</span></span>
* <span data-ttu-id="4468b-184">Quel est l’état de la connexion ?</span><span class="sxs-lookup"><span data-stu-id="4468b-184">What was the status of the sign-in?</span></span>

<span data-ttu-id="4468b-185">L’option **Connexions** vous fournit une vue d’ensemble complète de toutes les connexions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="4468b-185">The **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="4468b-186">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/51.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="4468b-187">Utilisation des applications gérées</span><span class="sxs-lookup"><span data-stu-id="4468b-187">Usage of managed applications</span></span>

<span data-ttu-id="4468b-188">En disposant d’une vue centrée sur les applications de vos données de connexion, vous pouvez répondre aux questions telles que :</span><span class="sxs-lookup"><span data-stu-id="4468b-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="4468b-189">Qui utilise mes applications ?</span><span class="sxs-lookup"><span data-stu-id="4468b-189">Who is using my applications?</span></span>
* <span data-ttu-id="4468b-190">Quelles sont les 3 principales applications dans votre organisation ?</span><span class="sxs-lookup"><span data-stu-id="4468b-190">What are the top 3 applications in your organization?</span></span>
* <span data-ttu-id="4468b-191">J’ai récemment déployé une application.</span><span class="sxs-lookup"><span data-stu-id="4468b-191">I have recently rolled out an application.</span></span> <span data-ttu-id="4468b-192">Comment se comporte-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="4468b-192">How is it doing?</span></span>

<span data-ttu-id="4468b-193">Les 3 principales applications de votre organisation dans le rapport sur les 30 derniers jours apparaissant dans la section **Vue d’ensemble** sous **Enterprise applications** (Applications d’entreprise) constituent votre point d’entrée.</span><span class="sxs-lookup"><span data-stu-id="4468b-193">Your entry point to this data is the top 3 applications in your organization within the last 30 days report in the **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="4468b-194">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/64.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-195">Le graphique d’utilisation des applications affiche les agrégations hebdomadaires des connexions pour vos 3 principales applications au cours d’une période donnée.</span><span class="sxs-lookup"><span data-stu-id="4468b-195">The app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="4468b-196">La valeur par défaut de cette période est de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="4468b-196">The default for the time period is 30 days.</span></span>

<span data-ttu-id="4468b-197">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/47.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="4468b-198">Si vous le souhaitez, vous pouvez définir la focalisation sur une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="4468b-198">If you want to, you can set the focus on a specific application.</span></span>


<span data-ttu-id="4468b-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="4468b-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="4468b-200">Lorsque vous cliquez sur un jour dans le graphique d’utilisation des applications, vous obtenez une liste détaillée des activités de connexion.</span><span class="sxs-lookup"><span data-stu-id="4468b-200">When you click on a day in the app usage graph, you get a detailed list of the sign-in activities.</span></span>


<span data-ttu-id="4468b-201">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/48.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="4468b-202">L’option **Connexions** vous fournit une vue d’ensemble complète de tous les événements de connexion à vos applications.</span><span class="sxs-lookup"><span data-stu-id="4468b-202">The **Sign-ins** option gives you a complete overview of all sign-in events to your applications.</span></span>

<span data-ttu-id="4468b-203">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/49.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="4468b-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="4468b-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4468b-204">Next steps</span></span>

<span data-ttu-id="4468b-205">Pour en savoir plus sur les codes d’erreur de l’activité des connexions, voir [Codes d’erreur des rapports d’activité des connexions dans le portail Azure Active Directory](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="4468b-205">If you want to know more about sign-in activity error codes, see the [Sign-in activity report error codes in the Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

