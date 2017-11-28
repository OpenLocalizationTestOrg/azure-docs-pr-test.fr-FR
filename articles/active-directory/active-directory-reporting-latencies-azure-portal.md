---
title: "latences de création de rapports Active Directory aaaAzure | Documents Microsoft"
description: "En savoir plus sur la quantité de hello de temps que nécessaire pour remonter des rapports tooshow d’événements dans votre portail Azure"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 9b88958d-94a2-4f4b-a18c-616f0617a24e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi;dhanyahk
ms.reviewer: dhanyahk
ms.openlocfilehash: eee959331262ba59b313dd038cb54699dbef48a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="b1ccd-103">Latences de création de rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b1ccd-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="b1ccd-104">Avec [reporting](active-directory-preview-explainer.md) Bonjour Azure Active Directory, vous obtenez toutes les informations de hello nécessaires toodetermine faire de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-104">With [reporting](active-directory-preview-explainer.md) in hello Azure Active Directory, you get all hello information you need toodetermine how your environment is doing.</span></span> <span data-ttu-id="b1ccd-105">Hello durée que nécessaire pour les rapports tooshow données haut Bonjour portail Azure est également appelé latence.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-105">hello amount of time it takes for reporting data tooshow up in hello Azure portal is also known as latency.</span></span> 

<span data-ttu-id="b1ccd-106">Cette rubrique répertorie les informations de latence hello pour hello toutes les catégories de rapports Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-106">This topic lists hello latency information for hello all reporting categories in hello Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="b1ccd-107">Rapports d’activité</span><span class="sxs-lookup"><span data-stu-id="b1ccd-107">Activity reports</span></span>

<span data-ttu-id="b1ccd-108">Il existe deux zones de rapports d’activité :</span><span class="sxs-lookup"><span data-stu-id="b1ccd-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="b1ccd-109">**Activités de connexion** – informations sur l’utilisation de hello des applications gérées et les activités d’authentification des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="b1ccd-109">**Sign-in activities** – Information about hello usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="b1ccd-110">**Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire</span><span class="sxs-lookup"><span data-stu-id="b1ccd-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="b1ccd-111">Hello tableau suivant répertorie les informations de latence hello pour les rapports d’activité.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-111">hello following table lists hello latency information for activity reports.</span></span>

| <span data-ttu-id="b1ccd-112">Rapport</span><span class="sxs-lookup"><span data-stu-id="b1ccd-112">Report</span></span> | <span data-ttu-id="b1ccd-113">Minimale</span><span class="sxs-lookup"><span data-stu-id="b1ccd-113">Minimum</span></span> | <span data-ttu-id="b1ccd-114">Moyenne</span><span class="sxs-lookup"><span data-stu-id="b1ccd-114">Average</span></span> | <span data-ttu-id="b1ccd-115">Maximale</span><span class="sxs-lookup"><span data-stu-id="b1ccd-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b1ccd-116">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="b1ccd-116">Audit logs</span></span>             | <span data-ttu-id="b1ccd-117">30 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-117">30 minutes</span></span>  | <span data-ttu-id="b1ccd-118">45 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-118">45 Minutes</span></span> | <span data-ttu-id="b1ccd-119">1 heure</span><span class="sxs-lookup"><span data-stu-id="b1ccd-119">1 hour</span></span>     |
| <span data-ttu-id="b1ccd-120">Connexions</span><span class="sxs-lookup"><span data-stu-id="b1ccd-120">Sign-ins</span></span>               | <span data-ttu-id="b1ccd-121">15 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-121">15 minutes</span></span>  | <span data-ttu-id="b1ccd-122">15 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-122">15 minutes</span></span> | <span data-ttu-id="b1ccd-123">2 heures*</span><span class="sxs-lookup"><span data-stu-id="b1ccd-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="b1ccd-124">Pour certaines données d’activité des connexions provenant d’applications office hérité, il peut prendre des heures de too8 pour hello remonter des rapports tooshow de données.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-124">For some sign-ins activity data coming from legacy office applications, it can take too8 hours for hello reporting data tooshow up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="b1ccd-125">Rapports de sécurité</span><span class="sxs-lookup"><span data-stu-id="b1ccd-125">Security reports</span></span>

<span data-ttu-id="b1ccd-126">Il existe deux zones de rapports de sécurité :</span><span class="sxs-lookup"><span data-stu-id="b1ccd-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="b1ccd-127">**Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 
- <span data-ttu-id="b1ccd-128">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="b1ccd-129">Hello tableau suivant répertorie les informations de latence hello pour les rapports de sécurité.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-129">hello following table lists hello latency information for security reports.</span></span>

| <span data-ttu-id="b1ccd-130">Rapport</span><span class="sxs-lookup"><span data-stu-id="b1ccd-130">Report</span></span> | <span data-ttu-id="b1ccd-131">Minimale</span><span class="sxs-lookup"><span data-stu-id="b1ccd-131">Minimum</span></span> | <span data-ttu-id="b1ccd-132">Moyenne</span><span class="sxs-lookup"><span data-stu-id="b1ccd-132">Average</span></span> | <span data-ttu-id="b1ccd-133">Maximale</span><span class="sxs-lookup"><span data-stu-id="b1ccd-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b1ccd-134">Les utilisateurs à risque</span><span class="sxs-lookup"><span data-stu-id="b1ccd-134">Users at risk</span></span>          | <span data-ttu-id="b1ccd-135">5 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-135">5 minutes</span></span>   | <span data-ttu-id="b1ccd-136">15 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-136">15 minutes</span></span>  | <span data-ttu-id="b1ccd-137">2 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-137">2 hours</span></span>  |
| <span data-ttu-id="b1ccd-138">Connexions risquées</span><span class="sxs-lookup"><span data-stu-id="b1ccd-138">Risky sign-ins</span></span>         | <span data-ttu-id="b1ccd-139">5 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-139">5 minutes</span></span>   | <span data-ttu-id="b1ccd-140">15 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-140">15 minutes</span></span>  | <span data-ttu-id="b1ccd-141">2 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="b1ccd-142">Événements à risque</span><span class="sxs-lookup"><span data-stu-id="b1ccd-142">Risk events</span></span>

<span data-ttu-id="b1ccd-143">Azure Active Directory utilise des algorithmes et des paramètres heuristiques actions suspectes toodetect qui sont des comptes d’utilisateur associés tooyour d’apprentissage adaptatif.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics toodetect suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="b1ccd-144">Chaque action suspecte détectée est stockée dans un enregistrement appelé événement à risque.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="b1ccd-145">Hello tableau suivant répertorie les informations de latence hello pour les événements à risque.</span><span class="sxs-lookup"><span data-stu-id="b1ccd-145">hello following table lists hello latency information for risk events.</span></span>

| <span data-ttu-id="b1ccd-146">Rapport</span><span class="sxs-lookup"><span data-stu-id="b1ccd-146">Report</span></span> | <span data-ttu-id="b1ccd-147">Minimale</span><span class="sxs-lookup"><span data-stu-id="b1ccd-147">Minimum</span></span> | <span data-ttu-id="b1ccd-148">Moyenne</span><span class="sxs-lookup"><span data-stu-id="b1ccd-148">Average</span></span> | <span data-ttu-id="b1ccd-149">Maximale</span><span class="sxs-lookup"><span data-stu-id="b1ccd-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="b1ccd-150">Connexions depuis des adresses IP anonymes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="b1ccd-151">5 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-151">5 minutes</span></span> |<span data-ttu-id="b1ccd-152">15 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-152">15 Minutes</span></span> |<span data-ttu-id="b1ccd-153">2 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-153">2 hours</span></span> |
| <span data-ttu-id="b1ccd-154">Connexions depuis des emplacements non connus</span><span class="sxs-lookup"><span data-stu-id="b1ccd-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="b1ccd-155">5 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-155">5 minutes</span></span> |<span data-ttu-id="b1ccd-156">15 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-156">15 Minutes</span></span> |<span data-ttu-id="b1ccd-157">2 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-157">2 hours</span></span> |
| <span data-ttu-id="b1ccd-158">Utilisateurs avec des informations d’identification volées</span><span class="sxs-lookup"><span data-stu-id="b1ccd-158">Users with leaked credentials</span></span> |<span data-ttu-id="b1ccd-159">2 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-159">2 hours</span></span> |<span data-ttu-id="b1ccd-160">4 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-160">4 hours</span></span> |<span data-ttu-id="b1ccd-161">8 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-161">8 hours</span></span> |
| <span data-ttu-id="b1ccd-162">Voyage Impossible tooatypical emplacements</span><span class="sxs-lookup"><span data-stu-id="b1ccd-162">Impossible travel tooatypical locations</span></span> |<span data-ttu-id="b1ccd-163">5 minutes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-163">5 minutes</span></span> |<span data-ttu-id="b1ccd-164">1 heure</span><span class="sxs-lookup"><span data-stu-id="b1ccd-164">1 hour</span></span> |<span data-ttu-id="b1ccd-165">8 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-165">8 hours</span></span>  |
| <span data-ttu-id="b1ccd-166">Connexions depuis des appareils infectés</span><span class="sxs-lookup"><span data-stu-id="b1ccd-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="b1ccd-167">2 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-167">2 hours</span></span> |<span data-ttu-id="b1ccd-168">4 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-168">4 hours</span></span> |<span data-ttu-id="b1ccd-169">8 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-169">8 hours</span></span>  |
| <span data-ttu-id="b1ccd-170">Connexions depuis des adresses IP avec des activités suspectes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="b1ccd-171">2 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-171">2 hours</span></span> |<span data-ttu-id="b1ccd-172">4 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-172">4 hours</span></span> |<span data-ttu-id="b1ccd-173">8 heures</span><span class="sxs-lookup"><span data-stu-id="b1ccd-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="b1ccd-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b1ccd-174">Next steps</span></span>

<span data-ttu-id="b1ccd-175">Si vous souhaitez tooknow plus d’informations sur les rapports d’activité hello Bonjour portail Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="b1ccd-175">If you want tooknow more about hello activity reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="b1ccd-176">Rapports d’activité de connexion dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b1ccd-176">Sign-in activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="b1ccd-177">Rapports d’activité dans le portail d’Azure Active Directory hello d’audit</span><span class="sxs-lookup"><span data-stu-id="b1ccd-177">Audit activity reports in hello Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="b1ccd-178">Si vous souhaitez tooknow plus d’informations sur les rapports de sécurité hello Bonjour portail Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="b1ccd-178">If you want tooknow more about hello security reports in hello Azure portal, see:</span></span>

- [<span data-ttu-id="b1ccd-179">Utilisateurs sur les rapports de sécurité risque dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b1ccd-179">Users at risk security report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="b1ccd-180">Rapport des connexions présentant un risque dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b1ccd-180">Risky sign-ins report in hello Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="b1ccd-181">Si vous souhaitez tooknow plus d’informations sur les événements à risque, consultez [événements à risque Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="b1ccd-181">If you want tooknow more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
