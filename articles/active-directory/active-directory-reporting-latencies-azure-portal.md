---
title: "Latences de création de rapports Azure Active Directory | Microsoft Docs"
description: "Découvrir le délai nécessaire pour que les événements de rapports apparaissent dans votre portail Azure"
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
ms.openlocfilehash: 93cb0baeab8f13f81257ed1bd32ed08561c54b72
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-reporting-latencies"></a><span data-ttu-id="031c1-103">Latences de création de rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="031c1-103">Azure Active Directory reporting latencies</span></span>

<span data-ttu-id="031c1-104">Dans Azure Active Directory, la [création de rapports](active-directory-preview-explainer.md) vous permet d’obtenir toutes les informations dont vous avez besoin pour déterminer l’état de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="031c1-104">With [reporting](active-directory-preview-explainer.md) in the Azure Active Directory, you get all the information you need to determine how your environment is doing.</span></span> <span data-ttu-id="031c1-105">Le temps nécessaire pour que les données de rapport s’affichent dans le portail Azure est également appelé latence.</span><span class="sxs-lookup"><span data-stu-id="031c1-105">The amount of time it takes for reporting data to show up in the Azure portal is also known as latency.</span></span> 

<span data-ttu-id="031c1-106">Cette rubrique répertorie les informations de latence pour toutes les catégories de rapports dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="031c1-106">This topic lists the latency information for the all reporting categories in the Azure portal.</span></span> 


## <a name="activity-reports"></a><span data-ttu-id="031c1-107">Rapports d’activité</span><span class="sxs-lookup"><span data-stu-id="031c1-107">Activity reports</span></span>

<span data-ttu-id="031c1-108">Il existe deux zones de rapports d’activité :</span><span class="sxs-lookup"><span data-stu-id="031c1-108">There are two areas of activity reporting:</span></span>

- <span data-ttu-id="031c1-109">**Activités de connexion** – Informations sur l’utilisation des applications gérées et les activités de connexion des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="031c1-109">**Sign-in activities** – Information about the usage of managed applications and user sign-in activities</span></span>
- <span data-ttu-id="031c1-110">**Activités du système** – Informations sur les activités du système liées aux utilisateurs et à la gestion des groupes, à vos applications gérées et aux activités de répertoire</span><span class="sxs-lookup"><span data-stu-id="031c1-110">**Audit logs** - System activity information about users and group management, your managed applications and directory activities</span></span>

<span data-ttu-id="031c1-111">Le tableau suivant répertorie les informations de latence pour les rapports d’activité.</span><span class="sxs-lookup"><span data-stu-id="031c1-111">The following table lists the latency information for activity reports.</span></span>

| <span data-ttu-id="031c1-112">Rapport</span><span class="sxs-lookup"><span data-stu-id="031c1-112">Report</span></span> | <span data-ttu-id="031c1-113">Minimale</span><span class="sxs-lookup"><span data-stu-id="031c1-113">Minimum</span></span> | <span data-ttu-id="031c1-114">Moyenne</span><span class="sxs-lookup"><span data-stu-id="031c1-114">Average</span></span> | <span data-ttu-id="031c1-115">Maximale</span><span class="sxs-lookup"><span data-stu-id="031c1-115">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="031c1-116">Journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="031c1-116">Audit logs</span></span>             | <span data-ttu-id="031c1-117">30 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-117">30 minutes</span></span>  | <span data-ttu-id="031c1-118">45 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-118">45 Minutes</span></span> | <span data-ttu-id="031c1-119">1 heure</span><span class="sxs-lookup"><span data-stu-id="031c1-119">1 hour</span></span>     |
| <span data-ttu-id="031c1-120">Connexions</span><span class="sxs-lookup"><span data-stu-id="031c1-120">Sign-ins</span></span>               | <span data-ttu-id="031c1-121">15 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-121">15 minutes</span></span>  | <span data-ttu-id="031c1-122">15 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-122">15 minutes</span></span> | <span data-ttu-id="031c1-123">2 heures*</span><span class="sxs-lookup"><span data-stu-id="031c1-123">2 hours*</span></span>   |

>[!NOTE]
> <span data-ttu-id="031c1-124">Pour certaines données d’activité de connexion provenant d’applications Office héritées, jusqu’à 8 heures peuvent s’écouler avant que les données de rapport s’affichent.</span><span class="sxs-lookup"><span data-stu-id="031c1-124">For some sign-ins activity data coming from legacy office applications, it can take to 8 hours for the reporting data to show up.</span></span> 


## <a name="security-reports"></a><span data-ttu-id="031c1-125">Rapports de sécurité</span><span class="sxs-lookup"><span data-stu-id="031c1-125">Security reports</span></span>

<span data-ttu-id="031c1-126">Il existe deux zones de rapports de sécurité :</span><span class="sxs-lookup"><span data-stu-id="031c1-126">There are two areas of security reporting:</span></span>

- <span data-ttu-id="031c1-127">**Connexions risquées** : une connexion risquée est une tentative de connexion susceptible de provenir d’un utilisateur autre que le propriétaire légitime d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="031c1-127">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> 
- <span data-ttu-id="031c1-128">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="031c1-128">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> 

<span data-ttu-id="031c1-129">Le tableau suivant répertorie les informations de latence pour les rapports de sécurité.</span><span class="sxs-lookup"><span data-stu-id="031c1-129">The following table lists the latency information for security reports.</span></span>

| <span data-ttu-id="031c1-130">Rapport</span><span class="sxs-lookup"><span data-stu-id="031c1-130">Report</span></span> | <span data-ttu-id="031c1-131">Minimale</span><span class="sxs-lookup"><span data-stu-id="031c1-131">Minimum</span></span> | <span data-ttu-id="031c1-132">Moyenne</span><span class="sxs-lookup"><span data-stu-id="031c1-132">Average</span></span> | <span data-ttu-id="031c1-133">Maximale</span><span class="sxs-lookup"><span data-stu-id="031c1-133">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="031c1-134">Les utilisateurs à risque</span><span class="sxs-lookup"><span data-stu-id="031c1-134">Users at risk</span></span>          | <span data-ttu-id="031c1-135">5 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-135">5 minutes</span></span>   | <span data-ttu-id="031c1-136">15 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-136">15 minutes</span></span>  | <span data-ttu-id="031c1-137">2 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-137">2 hours</span></span>  |
| <span data-ttu-id="031c1-138">Connexions risquées</span><span class="sxs-lookup"><span data-stu-id="031c1-138">Risky sign-ins</span></span>         | <span data-ttu-id="031c1-139">5 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-139">5 minutes</span></span>   | <span data-ttu-id="031c1-140">15 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-140">15 minutes</span></span>  | <span data-ttu-id="031c1-141">2 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-141">2 hours</span></span>  |

## <a name="risk-events"></a><span data-ttu-id="031c1-142">Événements à risque</span><span class="sxs-lookup"><span data-stu-id="031c1-142">Risk events</span></span>

<span data-ttu-id="031c1-143">Azure Active Directory utilise les algorithmes Machine Learning et des modèles heuristiques adaptatifs pour détecter les actions suspectes liées aux comptes de votre utilisateur.</span><span class="sxs-lookup"><span data-stu-id="031c1-143">Azure Active Directory uses adaptive machine learning algorithms and heuristics to detect suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="031c1-144">Chaque action suspecte détectée est stockée dans un enregistrement appelé événement à risque.</span><span class="sxs-lookup"><span data-stu-id="031c1-144">Each detected suspicious action is stored in a record called risk event.</span></span>

<span data-ttu-id="031c1-145">Le tableau suivant répertorie les informations de latence pour les événements à risque.</span><span class="sxs-lookup"><span data-stu-id="031c1-145">The following table lists the latency information for risk events.</span></span>

| <span data-ttu-id="031c1-146">Rapport</span><span class="sxs-lookup"><span data-stu-id="031c1-146">Report</span></span> | <span data-ttu-id="031c1-147">Minimale</span><span class="sxs-lookup"><span data-stu-id="031c1-147">Minimum</span></span> | <span data-ttu-id="031c1-148">Moyenne</span><span class="sxs-lookup"><span data-stu-id="031c1-148">Average</span></span> | <span data-ttu-id="031c1-149">Maximale</span><span class="sxs-lookup"><span data-stu-id="031c1-149">Maximum</span></span> |
| :-- | --- | --- | --- |
| <span data-ttu-id="031c1-150">Connexions depuis des adresses IP anonymes</span><span class="sxs-lookup"><span data-stu-id="031c1-150">Sign-ins from anonymous IP addresses</span></span> |<span data-ttu-id="031c1-151">5 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-151">5 minutes</span></span> |<span data-ttu-id="031c1-152">15 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-152">15 Minutes</span></span> |<span data-ttu-id="031c1-153">2 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-153">2 hours</span></span> |
| <span data-ttu-id="031c1-154">Connexions depuis des emplacements non connus</span><span class="sxs-lookup"><span data-stu-id="031c1-154">Sign-ins from unfamiliar locations</span></span> |<span data-ttu-id="031c1-155">5 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-155">5 minutes</span></span> |<span data-ttu-id="031c1-156">15 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-156">15 Minutes</span></span> |<span data-ttu-id="031c1-157">2 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-157">2 hours</span></span> |
| <span data-ttu-id="031c1-158">Utilisateurs avec des informations d’identification volées</span><span class="sxs-lookup"><span data-stu-id="031c1-158">Users with leaked credentials</span></span> |<span data-ttu-id="031c1-159">2 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-159">2 hours</span></span> |<span data-ttu-id="031c1-160">4 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-160">4 hours</span></span> |<span data-ttu-id="031c1-161">8 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-161">8 hours</span></span> |
| <span data-ttu-id="031c1-162">Voyage impossible vers des emplacements inhabituels</span><span class="sxs-lookup"><span data-stu-id="031c1-162">Impossible travel to atypical locations</span></span> |<span data-ttu-id="031c1-163">5 minutes</span><span class="sxs-lookup"><span data-stu-id="031c1-163">5 minutes</span></span> |<span data-ttu-id="031c1-164">1 heure</span><span class="sxs-lookup"><span data-stu-id="031c1-164">1 hour</span></span> |<span data-ttu-id="031c1-165">8 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-165">8 hours</span></span>  |
| <span data-ttu-id="031c1-166">Connexions depuis des appareils infectés</span><span class="sxs-lookup"><span data-stu-id="031c1-166">Sign-ins from infected devices</span></span> |<span data-ttu-id="031c1-167">2 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-167">2 hours</span></span> |<span data-ttu-id="031c1-168">4 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-168">4 hours</span></span> |<span data-ttu-id="031c1-169">8 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-169">8 hours</span></span>  |
| <span data-ttu-id="031c1-170">Connexions depuis des adresses IP avec des activités suspectes</span><span class="sxs-lookup"><span data-stu-id="031c1-170">Sign-ins from IP addresses with suspicious activity</span></span> |<span data-ttu-id="031c1-171">2 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-171">2 hours</span></span> |<span data-ttu-id="031c1-172">4 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-172">4 hours</span></span> |<span data-ttu-id="031c1-173">8 heures</span><span class="sxs-lookup"><span data-stu-id="031c1-173">8 hours</span></span>  |



## <a name="next-steps"></a><span data-ttu-id="031c1-174">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="031c1-174">Next steps</span></span>

<span data-ttu-id="031c1-175">Pour en savoir plus sur les rapports d’activité dans le portail Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="031c1-175">If you want to know more about the activity reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="031c1-176">Rapports d’activité de connexion dans le portail Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="031c1-176">Sign-in activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-sign-ins.md)
- [<span data-ttu-id="031c1-177">Rapports d’activité d’audit dans le portail Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="031c1-177">Audit activity reports in the Azure Active Directory portal</span></span>](active-directory-reporting-activity-audit-logs.md)

<span data-ttu-id="031c1-178">Pour en savoir plus sur les rapports de sécurité dans le portail Azure, consultez :</span><span class="sxs-lookup"><span data-stu-id="031c1-178">If you want to know more about the security reports in the Azure portal, see:</span></span>

- [<span data-ttu-id="031c1-179">Rapport sur la sécurité des utilisateurs courant un risque dans le portail Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="031c1-179">Users at risk security report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="031c1-180">Rapport de connexions à risque dans le portail Azure Active Directory </span><span class="sxs-lookup"><span data-stu-id="031c1-180">Risky sign-ins report in the Azure Active Directory portal</span></span>](active-directory-reporting-security-risky-sign-ins.md)

<span data-ttu-id="031c1-181">Pour en savoir plus sur les événements à risque, consultez [Événements à risque dans Azure Active Directory](active-directory-reporting-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="031c1-181">If you want to know more about risk events, see [Azure Active Directory risk events](active-directory-reporting-risk-events.md).</span></span>
