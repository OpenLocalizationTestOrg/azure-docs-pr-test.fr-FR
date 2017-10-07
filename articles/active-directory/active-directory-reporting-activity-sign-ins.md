---
title: "rapports aaaSign sur l’activité dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "Présentation des rapports toosign sur l’activité dans le portail d’Azure Active Directory hello"
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
ms.openlocfilehash: 49590d625a08d7dc189a629b89bab2261c2b4780
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="23aae-103">Rapports d’activité de connexion dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="23aae-103">Sign-in activity reports in hello Azure Active Directory portal</span></span>

<span data-ttu-id="23aae-104">Avec Azure Active Directory (Azure AD) reporting Bonjour [portail Azure](https://portal.azure.com), vous pouvez obtenir des informations de hello nécessaires toodetermine faire de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="23aae-104">With Azure Active Directory (Azure AD) reporting in hello [Azure portal](https://portal.azure.com), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="23aae-105">Hello architecture des rapports dans Azure Active Directory se compose de hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="23aae-105">hello reporting architecture in Azure Active Directory consists of hello following components:</span></span>

- <span data-ttu-id="23aae-106">**Activité**</span><span class="sxs-lookup"><span data-stu-id="23aae-106">**Activity**</span></span> 
    - <span data-ttu-id="23aae-107">**Activités de connexion** – informations sur l’utilisation de hello des applications gérées et les activités d’authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="23aae-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="23aae-108">**Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire.</span><span class="sxs-lookup"><span data-stu-id="23aae-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="23aae-109">**Sécurité**</span><span class="sxs-lookup"><span data-stu-id="23aae-109">**Security**</span></span> 
    - <span data-ttu-id="23aae-110">**Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="23aae-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="23aae-111">Pour en savoir plus, consultez Connexions risquées.</span><span class="sxs-lookup"><span data-stu-id="23aae-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="23aae-112">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="23aae-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="23aae-113">Pour en savoir plus, consultez Utilisateurs avec indicateur de risque.</span><span class="sxs-lookup"><span data-stu-id="23aae-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="23aae-114">Cette rubrique donne une vue d’ensemble d’activités de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="23aae-114">This topic gives you an overview of hello sign-in activities.</span></span>

## <a name="pre-requisite"></a><span data-ttu-id="23aae-115">Conditions préalables</span><span class="sxs-lookup"><span data-stu-id="23aae-115">Pre-requisite</span></span>

### <a name="who-can-access-hello-data"></a><span data-ttu-id="23aae-116">Qui peut accéder à des données de salutation ?</span><span class="sxs-lookup"><span data-stu-id="23aae-116">Who can access hello data?</span></span>
* <span data-ttu-id="23aae-117">Utilisateurs dans le rôle d’administrateur de la sécurité ou de sécurité Reader hello</span><span class="sxs-lookup"><span data-stu-id="23aae-117">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="23aae-118">Administrateurs généraux</span><span class="sxs-lookup"><span data-stu-id="23aae-118">Global Admins</span></span>
* <span data-ttu-id="23aae-119">Tous les utilisateurs (non administrateurs) peuvent accéder à leurs propres connexions</span><span class="sxs-lookup"><span data-stu-id="23aae-119">Any user (non-admins) can access their own sign-ins</span></span> 

### <a name="what-azure-ad-license-do-you-need-tooaccess-sign-in-activity"></a><span data-ttu-id="23aae-120">Licence Azure AD tooaccess activités avez-vous besoin ?</span><span class="sxs-lookup"><span data-stu-id="23aae-120">What Azure AD license do you need tooaccess sign-in activity?</span></span>
* <span data-ttu-id="23aae-121">Votre client doit avoir une licence Azure AD Premium associée toosee hello tout signe-rapport activité</span><span class="sxs-lookup"><span data-stu-id="23aae-121">Your tenant must have an Azure AD Premium license associated with it toosee hello all up sign-in activity report</span></span>


## <a name="signs-in-activities"></a><span data-ttu-id="23aae-122">Activités de connexion</span><span class="sxs-lookup"><span data-stu-id="23aae-122">Signs-in activities</span></span>

<span data-ttu-id="23aae-123">Informations hello fournies par le rapport d’authentification de l’utilisateur du hello, trouver tooquestions réponses telles que :</span><span class="sxs-lookup"><span data-stu-id="23aae-123">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

* <span data-ttu-id="23aae-124">Quel est le modèle hello d’authentification d’un utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="23aae-124">What is hello sign-in pattern of a user?</span></span>
* <span data-ttu-id="23aae-125">Combien d’utilisateurs se sont connectés au cours d’une semaine ?</span><span class="sxs-lookup"><span data-stu-id="23aae-125">How many users have users signed in over a week?</span></span>
* <span data-ttu-id="23aae-126">Quel est état hello de ces connexions ?</span><span class="sxs-lookup"><span data-stu-id="23aae-126">What’s hello status of these sign-ins?</span></span>

<span data-ttu-id="23aae-127">Votre première entrée tooall de point de connexion activités données **connexions** dans la section d’activité de hello **Azure Active**.</span><span class="sxs-lookup"><span data-stu-id="23aae-127">Your first entry point tooall sign-in activities data is **Sign-ins** in hello Activity section of **Azure Active**.</span></span>


<span data-ttu-id="23aae-128">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/61.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-128">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/61.png "Sign-in activity")</span></span>


<span data-ttu-id="23aae-129">Un journal d’audit inclut un mode Liste par défaut, qui indique :</span><span class="sxs-lookup"><span data-stu-id="23aae-129">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="23aae-130">utilisateur Hello</span><span class="sxs-lookup"><span data-stu-id="23aae-130">hello related user</span></span>
- <span data-ttu-id="23aae-131">Hello application hello l’utilisateur a connecté-de</span><span class="sxs-lookup"><span data-stu-id="23aae-131">hello application hello user has signed-in to</span></span>
- <span data-ttu-id="23aae-132">état de la connexion Hello</span><span class="sxs-lookup"><span data-stu-id="23aae-132">hello sign-in status</span></span>
- <span data-ttu-id="23aae-133">temps de connexion Hello</span><span class="sxs-lookup"><span data-stu-id="23aae-133">hello sign-in time</span></span>

<span data-ttu-id="23aae-134">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/41.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-134">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-135">Vous pouvez personnaliser l’affichage de liste hello en cliquant sur **colonnes** dans la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="23aae-135">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="23aae-136">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/19.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-136">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/19.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-137">Cela vous permet de toodisplay des champs supplémentaires ou supprimer des champs qui sont déjà affichés.</span><span class="sxs-lookup"><span data-stu-id="23aae-137">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="23aae-138">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/42.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-138">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/42.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-139">En cliquant sur un élément dans la vue de liste hello, vous obtenez toutes les informations disponibles à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="23aae-139">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="23aae-140">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/43.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-140">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/43.png "Sign-in activity")</span></span>


## <a name="filtering-sign-in-activities"></a><span data-ttu-id="23aae-141">Filtrage des activités de connexion</span><span class="sxs-lookup"><span data-stu-id="23aae-141">Filtering sign-in activities</span></span>

<span data-ttu-id="23aae-142">toonarrow bas hello signalés au niveau de tooa de données que fonctionne pour vous, vous pouvez filtrer les données de connexions hello hello suivant des champs à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="23aae-142">toonarrow down hello reported data tooa level that works for you, you can filter hello sign-ins data using hello following fields:</span></span>

- <span data-ttu-id="23aae-143">Intervalle de temps</span><span class="sxs-lookup"><span data-stu-id="23aae-143">Time interval</span></span>
- <span data-ttu-id="23aae-144">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="23aae-144">User</span></span>
- <span data-ttu-id="23aae-145">Application</span><span class="sxs-lookup"><span data-stu-id="23aae-145">Application</span></span>
- <span data-ttu-id="23aae-146">Client</span><span class="sxs-lookup"><span data-stu-id="23aae-146">Client</span></span>
- <span data-ttu-id="23aae-147">État de la connexion</span><span class="sxs-lookup"><span data-stu-id="23aae-147">Sign-in status</span></span>

<span data-ttu-id="23aae-148">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/44.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-148">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/44.png "Sign-in activity")</span></span>


<span data-ttu-id="23aae-149">Hello **intervalle de temps** filtre active tooyou toodefine un laps de temps pour hello a retourné des données.</span><span class="sxs-lookup"><span data-stu-id="23aae-149">hello **time interval** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="23aae-150">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="23aae-150">Possible values are:</span></span>

- <span data-ttu-id="23aae-151">1 mois</span><span class="sxs-lookup"><span data-stu-id="23aae-151">1 month</span></span>
- <span data-ttu-id="23aae-152">7 jours</span><span class="sxs-lookup"><span data-stu-id="23aae-152">7 days</span></span>
- <span data-ttu-id="23aae-153">24 heures</span><span class="sxs-lookup"><span data-stu-id="23aae-153">24 hours</span></span>
- <span data-ttu-id="23aae-154">Personnalisée</span><span class="sxs-lookup"><span data-stu-id="23aae-154">Custom</span></span>

<span data-ttu-id="23aae-155">Lorsque vous sélectionnez une plage personnalisée, vous pouvez configurer une heure de début et une heure de fin.</span><span class="sxs-lookup"><span data-stu-id="23aae-155">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="23aae-156">Hello **utilisateur** filtre vous permet de nom de hello toospecify ou hello nom d’utilisateur principal (UPN) de l’utilisateur hello vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="23aae-156">hello **user** filter enables you toospecify hello name or hello user principal name (UPN) of hello user you care about.</span></span>

<span data-ttu-id="23aae-157">Hello **application** filtre vous permet de nom de hello toospecify de l’application hello vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="23aae-157">hello **application** filter enables you toospecify hello name of hello application you care about.</span></span>

<span data-ttu-id="23aae-158">Hello **client** filtre vous permet de toospecify d’informations sur les appareils hello vous intéressent.</span><span class="sxs-lookup"><span data-stu-id="23aae-158">hello **client** filter enables you toospecify information about hello device you care about.</span></span>

<span data-ttu-id="23aae-159">Hello **état de la connexion** filtre vous permet de tooselect un Hello suivant filtre :</span><span class="sxs-lookup"><span data-stu-id="23aae-159">hello **sign-in status** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="23aae-160">Tout</span><span class="sxs-lookup"><span data-stu-id="23aae-160">All</span></span>
- <span data-ttu-id="23aae-161">Succès</span><span class="sxs-lookup"><span data-stu-id="23aae-161">Success</span></span>
- <span data-ttu-id="23aae-162">Échec</span><span class="sxs-lookup"><span data-stu-id="23aae-162">Failure</span></span>


## <a name="sign-in-activities-shortcuts"></a><span data-ttu-id="23aae-163">Raccourcis relatifs aux activités de connexion</span><span class="sxs-lookup"><span data-stu-id="23aae-163">Sign-in activities shortcuts</span></span>

<span data-ttu-id="23aae-164">En outre tooAzure Active Directory, hello portail Azure vous offre deux entrée supplémentaire points activités toosign de données :</span><span class="sxs-lookup"><span data-stu-id="23aae-164">In addition tooAzure Active Directory, hello Azure portal provides you with two additional entry points toosign-in activities data:</span></span>

- <span data-ttu-id="23aae-165">Utilisateurs et groupes</span><span class="sxs-lookup"><span data-stu-id="23aae-165">Users and groups</span></span>
- <span data-ttu-id="23aae-166">Applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="23aae-166">Enterprise applications</span></span>


### <a name="users-and-groups-sign-ins-activities"></a><span data-ttu-id="23aae-167">Activités de connexion des utilisateurs et des groupes</span><span class="sxs-lookup"><span data-stu-id="23aae-167">Users and groups sign-ins activities</span></span>

<span data-ttu-id="23aae-168">Informations hello fournies par le rapport d’authentification de l’utilisateur du hello, trouver tooquestions réponses telles que :</span><span class="sxs-lookup"><span data-stu-id="23aae-168">With hello information provided by hello user sign-in report, you find answers tooquestions such as:</span></span>

- <span data-ttu-id="23aae-169">Quel est le modèle hello d’authentification d’un utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="23aae-169">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="23aae-170">Combien d’utilisateurs se sont connectés au cours d’une semaine ?</span><span class="sxs-lookup"><span data-stu-id="23aae-170">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="23aae-171">Quel est état hello de ces connexions ?</span><span class="sxs-lookup"><span data-stu-id="23aae-171">What’s hello status of these sign-ins?</span></span>



<span data-ttu-id="23aae-172">Vos données de toothis de point d’entrée sont hello utilisateur connectez-vous graphique Bonjour **vue d’ensemble** sous **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="23aae-172">Your entry point toothis data is hello user sign-in graph in hello **Overview** section under **Users and groups**.</span></span>

<span data-ttu-id="23aae-173">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/45.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-173">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/45.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-174">graphique d’ouverture de session utilisateur Hello montre agrégations hebdomadaire de la connexion ins pour tous les utilisateurs dans une période donnée.</span><span class="sxs-lookup"><span data-stu-id="23aae-174">hello user sign-in graph shows weekly aggregations of sign ins for all users in a given time period.</span></span> <span data-ttu-id="23aae-175">valeur par défaut de Hello pour hello laps de temps est de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="23aae-175">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="23aae-176">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/46.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-176">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/46.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-177">Lorsque vous cliquez sur un jour dans hello connectez-vous graphique, vous obtenez une liste détaillée des activités de connexion hello pour ce jour.</span><span class="sxs-lookup"><span data-stu-id="23aae-177">When you click on a day in hello sign-in graph, you get a detailed list of hello sign-in activities for this day.</span></span>

<span data-ttu-id="23aae-178">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/41.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-178">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/41.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-179">Chaque ligne de hello connectez-vous activités liste donne que vous hello des informations détaillées sur hello sélectionné connectez-vous comme :</span><span class="sxs-lookup"><span data-stu-id="23aae-179">Each row in hello sign-in activities list gives you hello detailed information about hello selected sign-in such as:</span></span>

* <span data-ttu-id="23aae-180">Qui s’est connecté ?</span><span class="sxs-lookup"><span data-stu-id="23aae-180">Who has signed in?</span></span>
* <span data-ttu-id="23aae-181">Quel était hello liées UPN ?</span><span class="sxs-lookup"><span data-stu-id="23aae-181">What was hello related UPN?</span></span>
* <span data-ttu-id="23aae-182">Quelle application a été hello cible hello connectez-vous ?</span><span class="sxs-lookup"><span data-stu-id="23aae-182">What application was hello target of hello sign-in?</span></span>
* <span data-ttu-id="23aae-183">Nouveautés d’adresse IP de hello de la connexion au hello ?</span><span class="sxs-lookup"><span data-stu-id="23aae-183">What is hello IP address of hello sign-in?</span></span>
* <span data-ttu-id="23aae-184">Quel était le statut hello de la connexion au hello ?</span><span class="sxs-lookup"><span data-stu-id="23aae-184">What was hello status of hello sign-in?</span></span>

<span data-ttu-id="23aae-185">Hello **connexions** vous donne une vue d’ensemble complète de toutes les connexions utilisateur.</span><span class="sxs-lookup"><span data-stu-id="23aae-185">hello **Sign-ins** option gives you a complete overview of all user sign-ins.</span></span>

<span data-ttu-id="23aae-186">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/51.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-186">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/51.png "Sign-in activity")</span></span>



## <a name="usage-of-managed-applications"></a><span data-ttu-id="23aae-187">Utilisation des applications gérées</span><span class="sxs-lookup"><span data-stu-id="23aae-187">Usage of managed applications</span></span>

<span data-ttu-id="23aae-188">En disposant d’une vue centrée sur les applications de vos données de connexion, vous pouvez répondre aux questions telles que :</span><span class="sxs-lookup"><span data-stu-id="23aae-188">With an application-centric view of your sign-in data, you can answer questions such as:</span></span>

* <span data-ttu-id="23aae-189">Qui utilise mes applications ?</span><span class="sxs-lookup"><span data-stu-id="23aae-189">Who is using my applications?</span></span>
* <span data-ttu-id="23aae-190">Quelles sont les principales 3 applications hello dans votre organisation ?</span><span class="sxs-lookup"><span data-stu-id="23aae-190">What are hello top 3 applications in your organization?</span></span>
* <span data-ttu-id="23aae-191">J’ai récemment déployé une application.</span><span class="sxs-lookup"><span data-stu-id="23aae-191">I have recently rolled out an application.</span></span> <span data-ttu-id="23aae-192">Comment se comporte-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="23aae-192">How is it doing?</span></span>

<span data-ttu-id="23aae-193">Vos données de toothis de point d’entrée sont hello supérieur 3 applications dans votre organisation dans le dernier rapport de 30 jours hello Bonjour **vue d’ensemble** sous **des applications d’entreprise**.</span><span class="sxs-lookup"><span data-stu-id="23aae-193">Your entry point toothis data is hello top 3 applications in your organization within hello last 30 days report in hello **Overview** section under **Enterprise applications**.</span></span>

<span data-ttu-id="23aae-194">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/64.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-194">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/64.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-195">Hello application utilisation graphique agrégations hebdomadaires de connexions pour vos applications haut 3 dans un laps de temps donné.</span><span class="sxs-lookup"><span data-stu-id="23aae-195">hello app usage graph weekly aggregations of sign ins for your top 3 applications in a given time period.</span></span> <span data-ttu-id="23aae-196">valeur par défaut de Hello pour hello laps de temps est de 30 jours.</span><span class="sxs-lookup"><span data-stu-id="23aae-196">hello default for hello time period is 30 days.</span></span>

<span data-ttu-id="23aae-197">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/47.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-197">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/47.png "Sign-in activity")</span></span>

<span data-ttu-id="23aae-198">Si vous le souhaitez, vous pouvez définir le focus de hello sur une application spécifique.</span><span class="sxs-lookup"><span data-stu-id="23aae-198">If you want to, you can set hello focus on a specific application.</span></span>


<span data-ttu-id="23aae-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span><span class="sxs-lookup"><span data-stu-id="23aae-199">![Reporting](./media/active-directory-reporting-activity-sign-ins/single_spp_usage_graph.png "Reporting")</span></span>

<span data-ttu-id="23aae-200">Lorsque vous cliquez sur le graphique d’utilisation application hello par jour, vous obtenez une liste détaillée des activités de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="23aae-200">When you click on a day in hello app usage graph, you get a detailed list of hello sign-in activities.</span></span>


<span data-ttu-id="23aae-201">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/48.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-201">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/48.png "Sign-in activity")</span></span>


<span data-ttu-id="23aae-202">Hello **connexions** vous donne une vue d’ensemble complète de toutes les applications de tooyour d’événements de connexion.</span><span class="sxs-lookup"><span data-stu-id="23aae-202">hello **Sign-ins** option gives you a complete overview of all sign-in events tooyour applications.</span></span>

<span data-ttu-id="23aae-203">![Activité de connexion](./media/active-directory-reporting-activity-sign-ins/49.png "Activité de connexion")</span><span class="sxs-lookup"><span data-stu-id="23aae-203">![Sign-in activity](./media/active-directory-reporting-activity-sign-ins/49.png "Sign-in activity")</span></span>



## <a name="next-steps"></a><span data-ttu-id="23aae-204">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="23aae-204">Next steps</span></span>

<span data-ttu-id="23aae-205">Si vous souhaitez tooknow plus d’informations sur les codes d’erreur activité de connexion, consultez hello [connexion activité rapport codes d’erreur portail d’Azure Active Directory hello](active-directory-reporting-activity-sign-ins-errors.md).</span><span class="sxs-lookup"><span data-stu-id="23aae-205">If you want tooknow more about sign-in activity error codes, see hello [Sign-in activity report error codes in hello Azure Active Directory portal](active-directory-reporting-activity-sign-ins-errors.md).</span></span>

