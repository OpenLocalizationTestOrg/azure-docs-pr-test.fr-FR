---
title: "Création de rapports Active Directory aaaAzure | Documents Microsoft"
description: "Fournit une vue d’ensemble de la création de rapports Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a><span data-ttu-id="5904b-103">Création de rapports Active Directory</span><span class="sxs-lookup"><span data-stu-id="5904b-103">Azure Active Directory reporting</span></span>

<span data-ttu-id="5904b-104">Les rapports Azure Active Directory vous permettent d’obtenir de précieuses informations sur le comportement de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="5904b-104">With Azure Active Directory reporting, you can gain insights into how your environment is doing.</span></span>  
<span data-ttu-id="5904b-105">les données de salutation fournie vous permet de :</span><span class="sxs-lookup"><span data-stu-id="5904b-105">hello provided data enables you to:</span></span>

- <span data-ttu-id="5904b-106">déterminer la façon dont les applications et les services sont utilisés ;</span><span class="sxs-lookup"><span data-stu-id="5904b-106">Determine how your apps and services are utilized by your users</span></span>
- <span data-ttu-id="5904b-107">Détecter les risques affectant la santé hello de votre environnement</span><span class="sxs-lookup"><span data-stu-id="5904b-107">Detect potential risks affecting hello health of your environment</span></span>
- <span data-ttu-id="5904b-108">résoudre les problèmes empêchant les utilisateurs d’effectuer leur travail.</span><span class="sxs-lookup"><span data-stu-id="5904b-108">Troubleshoot issues preventing your users from getting their work done</span></span>  

<span data-ttu-id="5904b-109">architecture de création de rapports Hello s’appuie sur deux axes principaux :</span><span class="sxs-lookup"><span data-stu-id="5904b-109">hello reporting architecture relies on two main pillars:</span></span>

- <span data-ttu-id="5904b-110">Rapports de sécurité</span><span class="sxs-lookup"><span data-stu-id="5904b-110">Security reports</span></span>
- <span data-ttu-id="5904b-111">Rapports d’activité</span><span class="sxs-lookup"><span data-stu-id="5904b-111">Activity reports</span></span>

![Reporting](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a><span data-ttu-id="5904b-113">Rapports de sécurité</span><span class="sxs-lookup"><span data-stu-id="5904b-113">Security reports</span></span>

<span data-ttu-id="5904b-114">rapports de sécurité Hello dans Azure Active Directory aident vous tooprotect identités de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="5904b-114">hello security reports in Azure Active Directory help you tooprotect your organization's identities.</span></span>  
<span data-ttu-id="5904b-115">Il existe deux types de rapports de sécurité dans Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="5904b-115">There are two types of security reports in Azure Active Directory:</span></span>

- <span data-ttu-id="5904b-116">**Les utilisateurs avec indicateur de risque** - de hello [utilisateurs signalées pour le rapport de sécurité risque](active-directory-reporting-security-user-at-risk.md), vous obtenez une vue d’ensemble des comptes d’utilisateur qui a été compromise.</span><span class="sxs-lookup"><span data-stu-id="5904b-116">**Users flagged for risk** - From hello [users flagged for risk security report](active-directory-reporting-security-user-at-risk.md), you get an overview of user accounts that might have been compromised.</span></span>

- <span data-ttu-id="5904b-117">**Connexions risquées** - avec hello [rapport de sécurité de connexion présente des risques](active-directory-reporting-security-risky-sign-ins.md), vous obtenez un indicateur pour les tentatives de connexion qui ont peut-être été exécutées par une personne est ne Hello pas légitime propriétaire d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5904b-117">**Risky sign-ins** - With hello [risky sign-in security report](active-directory-reporting-security-risky-sign-ins.md), you get an indicator for sign-in attempts that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> 

<span data-ttu-id="5904b-118">**Licence Azure AD tooaccess un rapport de sécurité avez-vous besoin ?**</span><span class="sxs-lookup"><span data-stu-id="5904b-118">**What Azure AD license do you need tooaccess a security report?**</span></span>  
<span data-ttu-id="5904b-119">Toutes les éditions d’Azure Active Directory vous indiquent les rapports de sécurité Utilisateurs avec indicateur de risque et Connexions à risque.</span><span class="sxs-lookup"><span data-stu-id="5904b-119">All editions of Azure Active Directory provide you with users flagged for risk and risky sign-ins reports.</span></span>  
<span data-ttu-id="5904b-120">Toutefois, au niveau de granularité d’un rapport du hello varie entre les éditions de hello :</span><span class="sxs-lookup"><span data-stu-id="5904b-120">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="5904b-121">Bonjour **éditions Azure Active Directory gratuit et Basic**, vous obtenez déjà une liste d’utilisateurs avec indicateur des risques et de connexions présentant un risque.</span><span class="sxs-lookup"><span data-stu-id="5904b-121">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk and risky sign-ins.</span></span> 

- <span data-ttu-id="5904b-122">Hello **Azure Active Directory Premium 1** edition étend ce modèle en vous permettant également tooexamine certains hello sous-jacent des événements à risque qui ont été détectés pour chaque rapport.</span><span class="sxs-lookup"><span data-stu-id="5904b-122">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="5904b-123">Hello **Azure Active Directory Premium 2** édition fournit des hello plus des informations détaillées sur hello sous-jacent des événements à risque et il vous permet également de stratégies de sécurité tooconfigure répondent automatiquement tooconfigured niveaux de risque.</span><span class="sxs-lookup"><span data-stu-id="5904b-123">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about hello underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>


## <a name="activity-reports"></a><span data-ttu-id="5904b-124">Rapports d’activité</span><span class="sxs-lookup"><span data-stu-id="5904b-124">Activity reports</span></span>

<span data-ttu-id="5904b-125">Il existe deux types de rapports d’activité dans Azure Active Directory :</span><span class="sxs-lookup"><span data-stu-id="5904b-125">There are two types of activity reports in Azure Active Directory:</span></span>

- <span data-ttu-id="5904b-126">**Journaux d’audit** - hello [rapport d’activité des journaux d’audit](active-directory-reporting-activity-audit-logs.md) vous fournit des toohello d’accéder à l’historique de toutes les tâches effectuées dans votre client.</span><span class="sxs-lookup"><span data-stu-id="5904b-126">**Audit logs** - hello [audit logs activity report](active-directory-reporting-activity-audit-logs.md) provides you with access toohello history of every task performed in your tenant.</span></span>

- <span data-ttu-id="5904b-127">**Connexions** - avec hello [rapport d’activité des connexions](active-directory-reporting-activity-sign-ins.md), vous pouvez déterminer qui a effectué les tâches hello signalés par le rapport de journaux d’audit hello.</span><span class="sxs-lookup"><span data-stu-id="5904b-127">**Sign-ins** -  With hello [sign-ins activity report](active-directory-reporting-activity-sign-ins.md), you can determine, who has performed hello tasks reported by hello audit logs report.</span></span>



<span data-ttu-id="5904b-128">Hello **rapport des journaux d’audit** vous fournit des enregistrements d’activités du système pour la conformité.</span><span class="sxs-lookup"><span data-stu-id="5904b-128">hello **audit logs report** provides you with records of system activities for compliance.</span></span>
<span data-ttu-id="5904b-129">Entre autres, hello fourni de données vous permet de tooaddress des scénarios courants tels que :</span><span class="sxs-lookup"><span data-stu-id="5904b-129">Amongst others, hello provided data enables you tooaddress common scenarios such as:</span></span>

- <span data-ttu-id="5904b-130">Qui fait partie de mon client a obtenu le groupe d’administration tooan accès.</span><span class="sxs-lookup"><span data-stu-id="5904b-130">Someone in my tenant got access tooan admin group.</span></span> <span data-ttu-id="5904b-131">Qui lui a fourni cet accès ?</span><span class="sxs-lookup"><span data-stu-id="5904b-131">Who gave them access?</span></span> 

- <span data-ttu-id="5904b-132">Je veux liste de hello tooknow des utilisateurs se connectant à une application spécifique, car je le récemment embarquées hello application et souhaitez tooknow si elle effectue également</span><span class="sxs-lookup"><span data-stu-id="5904b-132">I want tooknow hello list of users signing into a specific app since I recently onboarded hello app and want tooknow if it’s doing well</span></span>

- <span data-ttu-id="5904b-133">Je veux tooknow combien produisent des réinitialisations de mot de passe dans mon client</span><span class="sxs-lookup"><span data-stu-id="5904b-133">I want tooknow how many password resets are happening in my tenant</span></span>


<span data-ttu-id="5904b-134">**Licence Azure AD rapport de journaux d’audit tooaccess hello avez-vous besoin ?**</span><span class="sxs-lookup"><span data-stu-id="5904b-134">**What Azure AD license do you need tooaccess hello audit logs report?**</span></span>  
<span data-ttu-id="5904b-135">rapport de journaux d’audit Hello est disponible pour les fonctionnalités dont vous disposez des licences.</span><span class="sxs-lookup"><span data-stu-id="5904b-135">hello audit logs report is available for features for which you have licenses.</span></span> <span data-ttu-id="5904b-136">Si vous avez une licence pour une fonctionnalité spécifique, vous avez également accès toohello auditer les informations du journal pour celui-ci.</span><span class="sxs-lookup"><span data-stu-id="5904b-136">If you have a license for a specific feature, you also have access toohello audit log information for it.</span></span>

<span data-ttu-id="5904b-137">Pour plus d’informations, consultez **comparaison des fonctionnalités de disposition générale de hello, Basic, versions gratuites et Premium** dans [les fonctionnalités Azure Active Directory](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span><span class="sxs-lookup"><span data-stu-id="5904b-137">For more details, see **Comparing generally available features of hello Free, Basic, and Premium editions** in [Azure Active Directory features and capabilities](https://www.microsoft.com/cloud-platform/azure-active-directory-features).</span></span>   



<span data-ttu-id="5904b-138">Hello **rapport d’activité des connexions** Active tootoofind répond tooquestions telles que :</span><span class="sxs-lookup"><span data-stu-id="5904b-138">hello **sign-ins activity report** enables tootoofind answers tooquestions such as:</span></span>

- <span data-ttu-id="5904b-139">Quel est le modèle hello d’authentification d’un utilisateur ?</span><span class="sxs-lookup"><span data-stu-id="5904b-139">What is hello sign-in pattern of a user?</span></span>
- <span data-ttu-id="5904b-140">Combien d’utilisateurs se sont connectés au cours d’une semaine ?</span><span class="sxs-lookup"><span data-stu-id="5904b-140">How many users have users signed in over a week?</span></span>
- <span data-ttu-id="5904b-141">Quel est état hello de ces connexions ?</span><span class="sxs-lookup"><span data-stu-id="5904b-141">What’s hello status of these sign-ins?</span></span>


<span data-ttu-id="5904b-142">**Licence Azure AD faire, vous devez tooaccess hello rapport d’activité des connexions ?**</span><span class="sxs-lookup"><span data-stu-id="5904b-142">**What Azure AD license do you need tooaccess hello sign-ins activity report?**</span></span>  
<span data-ttu-id="5904b-143">tooaccess hello rapport d’activité des connexions, votre client doit avoir une licence Azure AD Premium associée.</span><span class="sxs-lookup"><span data-stu-id="5904b-143">tooaccess hello sign-ins activity report, your tenant must have an Azure AD Premium license associated with it.</span></span>


## <a name="programmatic-access"></a><span data-ttu-id="5904b-144">Accès par programme</span><span class="sxs-lookup"><span data-stu-id="5904b-144">Programmatic access</span></span>

<span data-ttu-id="5904b-145">Dans l’interface utilisateur toohello Ajout, création de rapports Azure Active Directory offre également [l’accès par programme](active-directory-reporting-api-getting-started-azure-portal.md) toohello les données de rapport.</span><span class="sxs-lookup"><span data-stu-id="5904b-145">In addition toohello user interface, Azure Active Directory reporting also provides you with [programmatic access](active-directory-reporting-api-getting-started-azure-portal.md) toohello reporting data.</span></span> <span data-ttu-id="5904b-146">données de Hello de ces rapports peuvent être très utile tooyour applications, telles que les systèmes SIEM, l’audit et les outils Business intelligence.</span><span class="sxs-lookup"><span data-stu-id="5904b-146">hello data of these reports can be very useful tooyour applications, such as SIEM systems, audit, and business intelligence tools.</span></span> <span data-ttu-id="5904b-147">Bonjour Azure AD reporting Qu'api fournit des données de toohello de l’accès par programme via un ensemble d’API REST.</span><span class="sxs-lookup"><span data-stu-id="5904b-147">hello Azure AD reporting APIs provide programmatic access toohello data through a set of REST-based APIs.</span></span> <span data-ttu-id="5904b-148">Vous pouvez appeler ces API à partir de divers outils et langages de programmation.</span><span class="sxs-lookup"><span data-stu-id="5904b-148">You can call these APIs from a variety of programming languages and tools.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="5904b-149">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5904b-149">Next steps</span></span>

<span data-ttu-id="5904b-150">Si vous souhaitez tooknow plus hello différents types de rapports dans Azure Active Directory, consultez :</span><span class="sxs-lookup"><span data-stu-id="5904b-150">If you want tooknow more about hello various report types in Azure Active Directory, see:</span></span>

- [<span data-ttu-id="5904b-151">Rapport des utilisateurs avec indicateur de risque</span><span class="sxs-lookup"><span data-stu-id="5904b-151">Users flagged for risk report</span></span>](active-directory-reporting-security-user-at-risk.md)
- [<span data-ttu-id="5904b-152">Rapport sur les connexions à risque</span><span class="sxs-lookup"><span data-stu-id="5904b-152">Risky sign-ins report</span></span>](active-directory-reporting-security-risky-sign-ins.md)
- [<span data-ttu-id="5904b-153">Rapport de journaux d’audit</span><span class="sxs-lookup"><span data-stu-id="5904b-153">Audit logs report</span></span>](active-directory-reporting-activity-audit-logs.md)
- [<span data-ttu-id="5904b-154">Rapport de journaux de connexions</span><span class="sxs-lookup"><span data-stu-id="5904b-154">Sign-ins logs report</span></span>](active-directory-reporting-activity-sign-ins.md)

<span data-ttu-id="5904b-155">Si vous souhaitez tooknow plus d’informations sur l’accès à Bonjour Bonjour à l’aide de hello API de création de rapports de données de rapport, consultez :</span><span class="sxs-lookup"><span data-stu-id="5904b-155">If you want tooknow more about accessing hello hello reporting data using hello reporting API, see:</span></span> 

- [<span data-ttu-id="5904b-156">Prise en main de hello Azure Active Directory API de création de rapports</span><span class="sxs-lookup"><span data-stu-id="5904b-156">Getting started with hello Azure Active Directory reporting API</span></span>](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png