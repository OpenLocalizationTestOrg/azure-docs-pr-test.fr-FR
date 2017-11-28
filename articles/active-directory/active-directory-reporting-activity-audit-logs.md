---
title: "rapports d’activité d’aaaAudit dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "Introduction toohello auditer les rapports d’activité dans le portail d’Azure Active Directory hello"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: a1f93126-77d1-4345-ab7d-561066041161
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/19/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 1567673f5030fc707b017c069f2ba7587962e5cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="audit-activity-reports-in-hello-azure-active-directory-portal"></a><span data-ttu-id="e8bc7-103">Rapports d’activité dans le portail d’Azure Active Directory hello d’audit</span><span class="sxs-lookup"><span data-stu-id="e8bc7-103">Audit activity reports in hello Azure Active Directory portal</span></span> 

<span data-ttu-id="e8bc7-104">Les rapports dans Azure Active Directory (Azure AD), vous pouvez obtenir des informations de hello vous devez toodetermine faire de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-104">With reporting in Azure Active Directory (Azure AD), you can get hello information you need toodetermine how your environment is doing.</span></span>

<span data-ttu-id="e8bc7-105">Hello architecture reporting dans Azure AD se compose de hello suivant des composants :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-105">hello reporting architecture in Azure AD consists of hello following components:</span></span>

- <span data-ttu-id="e8bc7-106">**Activité**</span><span class="sxs-lookup"><span data-stu-id="e8bc7-106">**Activity**</span></span> 
    - <span data-ttu-id="e8bc7-107">**Activités de connexion** – informations sur l’utilisation de hello des applications gérées et les activités d’authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="e8bc7-107">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
    - <span data-ttu-id="e8bc7-108">**Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-108">**Audit logs** - System activity information about users and group management, your managed applications and directory activities.</span></span>
- <span data-ttu-id="e8bc7-109">**Sécurité**</span><span class="sxs-lookup"><span data-stu-id="e8bc7-109">**Security**</span></span> 
    - <span data-ttu-id="e8bc7-110">**Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-110">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="e8bc7-111">Pour en savoir plus, consultez Connexions risquées.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-111">For more details, see Risky sign-ins.</span></span>
    - <span data-ttu-id="e8bc7-112">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-112">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="e8bc7-113">Pour en savoir plus, consultez Utilisateurs avec indicateur de risque.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-113">For more details, see Users flagged for risk.</span></span>

<span data-ttu-id="e8bc7-114">Cette rubrique donne une vue d’ensemble des activités d’audit hello.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-114">This topic gives you an overview of hello audit activities.</span></span>
 
## <a name="who-can-access-hello-data"></a><span data-ttu-id="e8bc7-115">Qui peut accéder à des données de salutation ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-115">Who can access hello data?</span></span>
* <span data-ttu-id="e8bc7-116">Utilisateurs dans le rôle d’administrateur de la sécurité ou de sécurité Reader hello</span><span class="sxs-lookup"><span data-stu-id="e8bc7-116">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="e8bc7-117">Administrateurs généraux</span><span class="sxs-lookup"><span data-stu-id="e8bc7-117">Global Admins</span></span>
* <span data-ttu-id="e8bc7-118">Les utilisateurs individuels (non administrateurs) peuvent voir leurs propres activités</span><span class="sxs-lookup"><span data-stu-id="e8bc7-118">Individual users (non-admins) can see their own activities</span></span>


## <a name="audit-logs"></a><span data-ttu-id="e8bc7-119">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="e8bc7-119">Audit logs</span></span>

<span data-ttu-id="e8bc7-120">journaux d’audit de Hello dans Azure Active Directory fournissent des enregistrements d’activités du système pour la conformité.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-120">hello audit logs in Azure Active Directory provide records of system activities for compliance.</span></span>  
<span data-ttu-id="e8bc7-121">Votre première tooall de point d’entrée l’audit des données est **journaux d’Audit** Bonjour **activité** section de **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-121">Your first entry point tooall auditing data is **Audit logs** in hello **Activity** section of **Azure Active Directory**.</span></span>

<span data-ttu-id="e8bc7-122">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/61.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-122">![Audit logs](./media/active-directory-reporting-activity-audit-logs/61.png "Audit logs")</span></span>

<span data-ttu-id="e8bc7-123">Un journal d’audit inclut un mode Liste par défaut, qui indique :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-123">An audit log has a default list view that shows:</span></span>

- <span data-ttu-id="e8bc7-124">date de Hello et l’heure de l’occurrence de hello</span><span class="sxs-lookup"><span data-stu-id="e8bc7-124">hello date and time of hello occurrence</span></span>
- <span data-ttu-id="e8bc7-125">Hello initiateur / acteur (*qui*) d’une activité</span><span class="sxs-lookup"><span data-stu-id="e8bc7-125">hello initiator / actor (*who*) of an activity</span></span> 
- <span data-ttu-id="e8bc7-126">Hello d’activité (*que*)</span><span class="sxs-lookup"><span data-stu-id="e8bc7-126">hello activity (*what*)</span></span> 
- <span data-ttu-id="e8bc7-127">cible de Hello</span><span class="sxs-lookup"><span data-stu-id="e8bc7-127">hello target</span></span>

<span data-ttu-id="e8bc7-128">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/18.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-128">![Audit logs](./media/active-directory-reporting-activity-audit-logs/18.png "Audit logs")</span></span>

<span data-ttu-id="e8bc7-129">Vous pouvez personnaliser l’affichage de liste hello en cliquant sur **colonnes** dans la barre d’outils hello.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-129">You can customize hello list view by clicking **Columns** in hello toolbar.</span></span>

<span data-ttu-id="e8bc7-130">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/19.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-130">![Audit logs](./media/active-directory-reporting-activity-audit-logs/19.png "Audit logs")</span></span>

<span data-ttu-id="e8bc7-131">Cela vous permet de toodisplay des champs supplémentaires ou supprimer des champs qui sont déjà affichés.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-131">This enables you toodisplay additional fields or remove fields that are already displayed.</span></span>

<span data-ttu-id="e8bc7-132">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/21.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-132">![Audit logs](./media/active-directory-reporting-activity-audit-logs/21.png "Audit logs")</span></span>


<span data-ttu-id="e8bc7-133">En cliquant sur un élément dans la vue de liste hello, vous obtenez toutes les informations disponibles à ce sujet.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-133">By clicking an item in hello list view, you get all available details about it.</span></span>

<span data-ttu-id="e8bc7-134">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/22.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-134">![Audit logs](./media/active-directory-reporting-activity-audit-logs/22.png "Audit logs")</span></span>


## <a name="filtering-audit-logs"></a><span data-ttu-id="e8bc7-135">Filtrage des journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="e8bc7-135">Filtering audit logs</span></span>

<span data-ttu-id="e8bc7-136">toonarrow bas hello signalés au niveau de tooa de données que fonctionne pour vous, vous pouvez filtrer les données d’audit hello hello suivant des champs à l’aide de :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-136">toonarrow down hello reported data tooa level that works for you, you can filter hello audit data using hello following fields:</span></span>

- <span data-ttu-id="e8bc7-137">Plage de dates</span><span class="sxs-lookup"><span data-stu-id="e8bc7-137">Date range</span></span>
- <span data-ttu-id="e8bc7-138">Initié par (intervenant)</span><span class="sxs-lookup"><span data-stu-id="e8bc7-138">Initiated by (Actor)</span></span>
- <span data-ttu-id="e8bc7-139">Catégorie</span><span class="sxs-lookup"><span data-stu-id="e8bc7-139">Category</span></span>
- <span data-ttu-id="e8bc7-140">Type de ressource d’activité</span><span class="sxs-lookup"><span data-stu-id="e8bc7-140">Activity resource type</span></span>
- <span data-ttu-id="e8bc7-141">Activité</span><span class="sxs-lookup"><span data-stu-id="e8bc7-141">Activity</span></span>

<span data-ttu-id="e8bc7-142">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/23.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-142">![Audit logs](./media/active-directory-reporting-activity-audit-logs/23.png "Audit logs")</span></span>


<span data-ttu-id="e8bc7-143">Hello **plage de dates** filtre active tooyou toodefine un laps de temps pour hello a retourné des données.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-143">hello **date range** filter enables tooyou toodefine a timeframe for hello returned data.</span></span>  
<span data-ttu-id="e8bc7-144">Les valeurs possibles sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-144">Possible values are:</span></span>

- <span data-ttu-id="e8bc7-145">1 mois</span><span class="sxs-lookup"><span data-stu-id="e8bc7-145">1 month</span></span>
- <span data-ttu-id="e8bc7-146">7 jours</span><span class="sxs-lookup"><span data-stu-id="e8bc7-146">7 days</span></span>
- <span data-ttu-id="e8bc7-147">24 heures</span><span class="sxs-lookup"><span data-stu-id="e8bc7-147">24 hours</span></span>
- <span data-ttu-id="e8bc7-148">Personnalisée</span><span class="sxs-lookup"><span data-stu-id="e8bc7-148">Custom</span></span>

<span data-ttu-id="e8bc7-149">Lorsque vous sélectionnez une plage personnalisée, vous pouvez configurer une heure de début et une heure de fin.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-149">When you select a custom timeframe, you can configure a start time and an end time.</span></span>

<span data-ttu-id="e8bc7-150">Hello **initié par** filtre permet de vous toodefine les nom d’un acteur ou son nom principal universel (UPN).</span><span class="sxs-lookup"><span data-stu-id="e8bc7-150">hello **initiated by** filter enables you toodefine an actor's name or its universal principal name (UPN).</span></span>

<span data-ttu-id="e8bc7-151">Hello **catégorie** filtre vous permet de tooselect un Hello suivant filtre :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-151">hello **category** filter enables you tooselect one of hello following filter:</span></span>

- <span data-ttu-id="e8bc7-152">Tout</span><span class="sxs-lookup"><span data-stu-id="e8bc7-152">All</span></span>
- <span data-ttu-id="e8bc7-153">Catégorie principale</span><span class="sxs-lookup"><span data-stu-id="e8bc7-153">Core category</span></span>
- <span data-ttu-id="e8bc7-154">Répertoire principal</span><span class="sxs-lookup"><span data-stu-id="e8bc7-154">Core directory</span></span>
- <span data-ttu-id="e8bc7-155">Gestion des mots de passe en libre-service</span><span class="sxs-lookup"><span data-stu-id="e8bc7-155">Self-service password management</span></span>
- <span data-ttu-id="e8bc7-156">Gestion des groupes en libre service</span><span class="sxs-lookup"><span data-stu-id="e8bc7-156">Self-service group management</span></span>
- <span data-ttu-id="e8bc7-157">Approvisionnement de comptes - Substitution de mot de passe automatique</span><span class="sxs-lookup"><span data-stu-id="e8bc7-157">Account provisioning- Automated password rollover</span></span>
- <span data-ttu-id="e8bc7-158">Utilisateurs invités</span><span class="sxs-lookup"><span data-stu-id="e8bc7-158">Invited users</span></span>
- <span data-ttu-id="e8bc7-159">Service MIM</span><span class="sxs-lookup"><span data-stu-id="e8bc7-159">MIM service</span></span>
- <span data-ttu-id="e8bc7-160">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="e8bc7-160">Identity Protection</span></span>
- <span data-ttu-id="e8bc7-161">B2C</span><span class="sxs-lookup"><span data-stu-id="e8bc7-161">B2C</span></span>

<span data-ttu-id="e8bc7-162">Hello **type de ressource d’activité** filtre vous permet de tooselect filtre les valeurs hello suivantes :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-162">hello **activity resource type** filter enables you tooselect one of hello following filters:</span></span>

- <span data-ttu-id="e8bc7-163">Tout</span><span class="sxs-lookup"><span data-stu-id="e8bc7-163">All</span></span> 
- <span data-ttu-id="e8bc7-164">Groupe</span><span class="sxs-lookup"><span data-stu-id="e8bc7-164">Group</span></span>
- <span data-ttu-id="e8bc7-165">Répertoire</span><span class="sxs-lookup"><span data-stu-id="e8bc7-165">Directory</span></span>
- <span data-ttu-id="e8bc7-166">Utilisateur</span><span class="sxs-lookup"><span data-stu-id="e8bc7-166">User</span></span>
- <span data-ttu-id="e8bc7-167">Application</span><span class="sxs-lookup"><span data-stu-id="e8bc7-167">Application</span></span>
- <span data-ttu-id="e8bc7-168">Stratégie</span><span class="sxs-lookup"><span data-stu-id="e8bc7-168">Policy</span></span>
- <span data-ttu-id="e8bc7-169">Appareil</span><span class="sxs-lookup"><span data-stu-id="e8bc7-169">Device</span></span>
- <span data-ttu-id="e8bc7-170">Autres</span><span class="sxs-lookup"><span data-stu-id="e8bc7-170">Other</span></span>

<span data-ttu-id="e8bc7-171">Lorsque vous sélectionnez **groupe** en tant que **type de ressource d’activité**, vous obtenez des tooalso une catégorie de filtre supplémentaires qui vous permet de fournir un **Source**:</span><span class="sxs-lookup"><span data-stu-id="e8bc7-171">When you select **Group** as **activity resource type**, you get an additional filter category that enables you tooalso provide a **Source**:</span></span>

- <span data-ttu-id="e8bc7-172">Azure AD</span><span class="sxs-lookup"><span data-stu-id="e8bc7-172">Azure AD</span></span>
- <span data-ttu-id="e8bc7-173">O365</span><span class="sxs-lookup"><span data-stu-id="e8bc7-173">O365</span></span>


<span data-ttu-id="e8bc7-174">Hello **activité** filtre est basé sur la catégorie de hello et sélection du type de ressource activité vous apporter.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-174">hello **activity** filter is based on hello category and Activity resource type selection you make.</span></span> <span data-ttu-id="e8bc7-175">Vous pouvez sélectionner une activité spécifique toosee ou tous.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-175">You can select a specific activity you want toosee or choose all.</span></span> 

<span data-ttu-id="e8bc7-176">Vous pouvez obtenir liste hello de toutes les activités d’Audit à l’aide de hello API Graph https://graph.windows.net/$ tenantdomain/activités/auditActivityTypes ? api-version = beta, où $tenantdomain = votre nom de domaine ou consultez l’article de toohello [rapport d’audit événements](active-directory-reporting-audit-events.md).</span><span class="sxs-lookup"><span data-stu-id="e8bc7-176">You can get hello list of all Audit Activities using hello Graph API https://graph.windows.net/$tenantdomain/activities/auditActivityTypes?api-version=beta, where $tenantdomain = your domain name or refer toohello article [audit report events](active-directory-reporting-audit-events.md).</span></span>


## <a name="audit-logs-shortcuts"></a><span data-ttu-id="e8bc7-177">Raccourcis de journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="e8bc7-177">Audit logs shortcuts</span></span>

<span data-ttu-id="e8bc7-178">En outre trop**Azure Active Directory**, hello portail Azure vous offre deux points d’entrée supplémentaires tooaudit données :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-178">In addition too**Azure Active Directory**, hello Azure portal provides you with two additional entry points tooaudit data:</span></span>

- <span data-ttu-id="e8bc7-179">Utilisateurs et groupes</span><span class="sxs-lookup"><span data-stu-id="e8bc7-179">Users and groups</span></span>
- <span data-ttu-id="e8bc7-180">Applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="e8bc7-180">Enterprise applications</span></span>

### <a name="users-and-groups-audit-logs"></a><span data-ttu-id="e8bc7-181">Journaux d’audit des utilisateurs et des groupes</span><span class="sxs-lookup"><span data-stu-id="e8bc7-181">Users and groups audit logs</span></span>

<span data-ttu-id="e8bc7-182">Avec l’utilisateur et d’audit basées sur le groupe de rapports, vous pouvez obtenir tooquestions réponses telles que :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-182">With user and group-based audit reports, you can get answers tooquestions such as:</span></span>

- <span data-ttu-id="e8bc7-183">Quels types de mises à jour ont été les utilisateurs hello appliqués ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-183">What types of updates have been applied hello users?</span></span>

- <span data-ttu-id="e8bc7-184">Combien d’utilisateurs ont été modifiés ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-184">How many users were changed?</span></span>

- <span data-ttu-id="e8bc7-185">Combien de mots de passe ont été modifiés ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-185">How many passwords were changed?</span></span>

- <span data-ttu-id="e8bc7-186">Qu’a fait un administrateur dans un répertoire ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-186">What has an administrator done in a directory?</span></span>

- <span data-ttu-id="e8bc7-187">Quelles sont les groupes hello qui ont été ajoutés ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-187">What are hello groups that have been added?</span></span>

- <span data-ttu-id="e8bc7-188">Existe-t-il des groupes comportant des modifications d’adhésion ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-188">Are there groups with membership changes?</span></span>

- <span data-ttu-id="e8bc7-189">Les propriétaires de hello du groupe ont été modifiés ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-189">Have hello owners of group been changed?</span></span>

- <span data-ttu-id="e8bc7-190">Les licences ont été attribuées à un utilisateur ou groupe de tooa ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-190">What licenses have been assigned tooa group or a user?</span></span>

<span data-ttu-id="e8bc7-191">Si vous souhaitez simplement tooreview données toousers connexes et les groupes d’audit, vous trouverez une vue filtrée sous **journaux d’Audit** Bonjour **activité** section Hello **utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-191">If you just want tooreview auditing data that is related toousers and groups, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Users and Groups**.</span></span> <span data-ttu-id="e8bc7-192">Dans ce point d’entrée, **Utilisateurs et groupes** est présélectionné comme **Type de ressource d’activité**.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-192">This entry point has **Users and groups** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="e8bc7-193">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/93.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-193">![Audit logs](./media/active-directory-reporting-activity-audit-logs/93.png "Audit logs")</span></span>

### <a name="enterprise-applications-audit-logs"></a><span data-ttu-id="e8bc7-194">Journaux d’audit d’applications d’entreprise</span><span class="sxs-lookup"><span data-stu-id="e8bc7-194">Enterprise applications audit logs</span></span>

<span data-ttu-id="e8bc7-195">Rapports d’audit avec basée sur l’application, vous pouvez obtenir des tooquestions réponses telles que :</span><span class="sxs-lookup"><span data-stu-id="e8bc7-195">With application-based audit reports, you can get answers tooquestions such as:</span></span>

* <span data-ttu-id="e8bc7-196">Quelles sont les applications hello qui ont été ajoutées ou mis à jour ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-196">What are hello applications that have been added or updated?</span></span>
* <span data-ttu-id="e8bc7-197">Quelles sont les applications hello qui ont été supprimées ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-197">What are hello applications that have been removed?</span></span>
* <span data-ttu-id="e8bc7-198">Le principal du service d’une application a-t-il été modifié ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-198">Has a service principle for an application changed?</span></span>
* <span data-ttu-id="e8bc7-199">Les noms de hello des applications ont été modifiés ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-199">Have hello names of applications been changed?</span></span>
* <span data-ttu-id="e8bc7-200">Qui a donné son consentement tooan application ?</span><span class="sxs-lookup"><span data-stu-id="e8bc7-200">Who gave consent tooan application?</span></span>

<span data-ttu-id="e8bc7-201">Si vous souhaitez simplement tooreview l’audit des données connexes tooyour applications, vous trouverez une vue filtrée sous **journaux d’Audit** Bonjour **activité** section Hello **des applications d’entreprise**  panneau.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-201">If you just want tooreview auditing data that is related tooyour applications, you can find a filtered view under **Audit logs** in hello **Activity** section of hello **Enterprise applications** blade.</span></span> <span data-ttu-id="e8bc7-202">Dans ce point d’entrée, **Applications d’entreprise** est présélectionné comme **Type de ressource d’activité**.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-202">This entry point has **Enterprise applications** as preselected **Activity Resource Type**.</span></span>

<span data-ttu-id="e8bc7-203">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/134.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-203">![Audit logs](./media/active-directory-reporting-activity-audit-logs/134.png "Audit logs")</span></span>

<span data-ttu-id="e8bc7-204">Vous pouvez filtrer cet affichage le plus bas toojust **groupes** ou simplement **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="e8bc7-204">You can filter this view further down toojust **groups** or just **users**.</span></span>

<span data-ttu-id="e8bc7-205">![Journaux d’audit](./media/active-directory-reporting-activity-audit-logs/25.png "Journaux d’Audit")</span><span class="sxs-lookup"><span data-stu-id="e8bc7-205">![Audit logs](./media/active-directory-reporting-activity-audit-logs/25.png "Audit logs")</span></span>


## <a name="next-steps"></a><span data-ttu-id="e8bc7-206">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e8bc7-206">Next steps</span></span>

<span data-ttu-id="e8bc7-207">Pour une vue d’ensemble de la création de rapports, consultez hello [reporting d’Azure Active Directory](active-directory-reporting-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e8bc7-207">For an overview of reporting, see hello [Azure Active Directory reporting](active-directory-reporting-azure-portal.md).</span></span>

