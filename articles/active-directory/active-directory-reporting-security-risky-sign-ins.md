---
title: "rapport des connexions aaaRisky dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "En savoir plus sur les rapports de connexions risquée hello dans le portail d’Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="e1394-103">Rapport des connexions présentant un risque dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="e1394-103">Risky sign-ins report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="e1394-104">Avec les rapports de sécurité hello dans Azure Active Directory (Azure AD) vous pouvez obtenir probabilité hello de comptes d’utilisateur compromis dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="e1394-104">With hello security reports in Azure Active Directory (Azure AD) you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="e1394-105">Azure AD détecte les actions suspectes qui sont des comptes d’utilisateur tooyour connexes.</span><span class="sxs-lookup"><span data-stu-id="e1394-105">Azure AD detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="e1394-106">Pour chaque action détectée, un enregistrement appelé *événement à risque* est créé.</span><span class="sxs-lookup"><span data-stu-id="e1394-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="e1394-107">Pour en savoir plus, voir [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="e1394-107">For more details, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="e1394-108">Hello détecté risque toocalculate utilisé :</span><span class="sxs-lookup"><span data-stu-id="e1394-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="e1394-109">**Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="e1394-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="e1394-110">Pour en savoir plus, voir [Connexions risquées](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="e1394-110">For more details, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="e1394-111">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="e1394-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="e1394-112">Pour en savoir plus, voir [Utilisateurs avec indicateur de risque](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="e1394-112">For more details, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="e1394-113">Dans [hello portail Azure](https://portal.azure.com), vous pouvez trouver hello la sécurité des rapports sur hello **Azure Active Directory** panneau Bonjour **sécurité** section.</span><span class="sxs-lookup"><span data-stu-id="e1394-113">In [hello Azure portal](https://portal.azure.com), you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span> 

![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="e1394-115">Licence Azure AD tooaccess un rapport de sécurité avez-vous besoin ?</span><span class="sxs-lookup"><span data-stu-id="e1394-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="e1394-116">Toutes les éditions d’Azure Active Directory vous indiquent les rapports de connexions risquées.</span><span class="sxs-lookup"><span data-stu-id="e1394-116">All editions of Azure Active Directory provide you with risky sign-ins reports.</span></span>  
<span data-ttu-id="e1394-117">Toutefois, au niveau de granularité d’un rapport du hello varie entre les éditions de hello :</span><span class="sxs-lookup"><span data-stu-id="e1394-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="e1394-118">Bonjour **éditions Azure Active Directory gratuit et Basic**, vous obtenez déjà une liste de connexions présentant un risque.</span><span class="sxs-lookup"><span data-stu-id="e1394-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of risky sign-ins.</span></span> 

- <span data-ttu-id="e1394-119">Hello **Azure Active Directory Premium 1** edition étend ce modèle en vous permettant également tooexamine certains hello sous-jacent des événements à risque qui ont été détectés pour chaque rapport.</span><span class="sxs-lookup"><span data-stu-id="e1394-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="e1394-120">Hello **Azure Active Directory Premium 2** édition fournit des hello plus des informations détaillées sur tous les événements à risque sous-jacent et il vous permet également de stratégies de sécurité tooconfigure répondent automatiquement tooconfigured niveaux de risque.</span><span class="sxs-lookup"><span data-stu-id="e1394-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and it also enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="e1394-121">Édition Azure Active Directory gratuite et de base</span><span class="sxs-lookup"><span data-stu-id="e1394-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="e1394-122">Hello Azure Active Directory gratuit et les éditions de base fournissent une liste de risquée connexions qui ont été détectées pour vos utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="e1394-122">hello Azure Active Directory free and basic editions provide you with a list of risky sign-ins that have been detected for your users.</span></span> <span data-ttu-id="e1394-123">Ce rapport répertorie :</span><span class="sxs-lookup"><span data-stu-id="e1394-123">This report lists:</span></span>

- <span data-ttu-id="e1394-124">**Utilisateur** hello - nom de l’utilisateur hello qui a été utilisé pendant l’opération de connexion hello</span><span class="sxs-lookup"><span data-stu-id="e1394-124">**User** - hello name of hello user that was used during hello sign-in operation</span></span>
- <span data-ttu-id="e1394-125">**IP** -hello l’adresse IP du périphérique hello qui a été utilisé tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1394-125">**IP** - hello IP address of hello device that was used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="e1394-126">**Emplacement** -emplacement de hello utilisé tooconnect tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1394-126">**Location** - hello location used tooconnect tooAzure Active Directory</span></span>
- <span data-ttu-id="e1394-127">**L’heure** -hello heure hello connectez-vous</span><span class="sxs-lookup"><span data-stu-id="e1394-127">**Sign-in time** - hello time when hello sign-in was performed</span></span>
- <span data-ttu-id="e1394-128">**État** -hello l’état de la connexion au hello</span><span class="sxs-lookup"><span data-stu-id="e1394-128">**Status** - hello status of hello sign-in</span></span>


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/01.png)

<span data-ttu-id="e1394-130">Selon votre examen de hello risquée connectez-vous, vous pouvez fournir des commentaires tooAzure Active Directory sous forme de hello suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="e1394-130">Based on your investigation of hello risky sign-in, you can provide feedback tooAzure Active Directory in form of hello following actions:</span></span>

- <span data-ttu-id="e1394-131">Résoudre</span><span class="sxs-lookup"><span data-stu-id="e1394-131">Resolve</span></span>
- <span data-ttu-id="e1394-132">Marquer comme faux positif</span><span class="sxs-lookup"><span data-stu-id="e1394-132">Mark as false positive</span></span>
- <span data-ttu-id="e1394-133">Ignorer</span><span class="sxs-lookup"><span data-stu-id="e1394-133">Ignore</span></span>
- <span data-ttu-id="e1394-134">Réactiver</span><span class="sxs-lookup"><span data-stu-id="e1394-134">Reactivate</span></span>

![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/21.png)

<span data-ttu-id="e1394-136">Pour en savoir plus, voir [Fermeture manuelle des événements à risque](active-directory-identityprotection.md#closing-risk-events-manually).</span><span class="sxs-lookup"><span data-stu-id="e1394-136">For more details, see [Closing risk events manually](active-directory-identityprotection.md#closing-risk-events-manually).</span></span>

<span data-ttu-id="e1394-137">Ce rapport fournit une option permettant de :</span><span class="sxs-lookup"><span data-stu-id="e1394-137">This report provides you with an option to:</span></span>

- <span data-ttu-id="e1394-138">Rechercher des ressources</span><span class="sxs-lookup"><span data-stu-id="e1394-138">Searh resources</span></span>
- <span data-ttu-id="e1394-139">Télécharger des données de rapport hello</span><span class="sxs-lookup"><span data-stu-id="e1394-139">Download hello report data</span></span>


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="e1394-141">Éditions Premium d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e1394-141">Azure Active Directory premium editions</span></span>

<span data-ttu-id="e1394-142">rapport des connexions risquée Hello dans les éditions premium hello Azure Active Directory vous offre :</span><span class="sxs-lookup"><span data-stu-id="e1394-142">hello risky sign-ins report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="e1394-143">Agrégé des informations sur hello [risque de types d’événements](active-directory-identity-protection-risk-events.md) qui ont été détectées</span><span class="sxs-lookup"><span data-stu-id="e1394-143">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="e1394-144">Un rapport de hello toodownload option</span><span class="sxs-lookup"><span data-stu-id="e1394-144">An option toodownload hello report</span></span>


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/456.png)


<span data-ttu-id="e1394-146">Lorsque vous sélectionnez un événement à risque, vous obtenez une vue de rapport détaillé pour cet événement à risque qui vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1394-146">When you select a risk event, you get a detailed report view for this risk event that enables you to:</span></span>

- <span data-ttu-id="e1394-147">Une option tooconfigure un [stratégie de mise à jour risque d’utilisateur](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="e1394-147">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  

- <span data-ttu-id="e1394-148">Passez en revue la chronologie de la détection de hello pour un événement à risque hello</span><span class="sxs-lookup"><span data-stu-id="e1394-148">Review hello detection timeline for hello risk event</span></span>  

- <span data-ttu-id="e1394-149">Passer en revue la liste des utilisateurs pour lesquels cet événement à risque a été détecté</span><span class="sxs-lookup"><span data-stu-id="e1394-149">Review a list of users for which this risk event has been detected</span></span>

- <span data-ttu-id="e1394-150">[Fermer manuellement les événements à risque](active-directory-identityprotection.md#closing-risk-events-manually) ou réactiver un événement à risque fermé manuellement.</span><span class="sxs-lookup"><span data-stu-id="e1394-150">[Manually close risk events](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/457.png)

<span data-ttu-id="e1394-152">Lorsque vous sélectionnez un utilisateur, vous obtenez une vue de rapport détaillé pour cet utilisateur qui vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="e1394-152">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="e1394-153">Ouvrez hello que permet d’afficher toutes les connexions</span><span class="sxs-lookup"><span data-stu-id="e1394-153">Open hello All sign-ins view</span></span>

- <span data-ttu-id="e1394-154">Réinitialiser le mot de passe de l’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="e1394-154">Reset hello user's password</span></span>

- <span data-ttu-id="e1394-155">Ignorer tous les événements</span><span class="sxs-lookup"><span data-stu-id="e1394-155">Dismiss all events</span></span>

- <span data-ttu-id="e1394-156">Examiner les événements à risque signalé pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="e1394-156">Investigate reported risk events for hello user.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/324.png)


<span data-ttu-id="e1394-158">tooinvestigate un événement à risque, sélectionnez-en un dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="e1394-158">tooinvestigate a risk event, select one from hello list.</span></span>  
<span data-ttu-id="e1394-159">Cette opération ouvre hello **détails** panneau pour cet événement risque.</span><span class="sxs-lookup"><span data-stu-id="e1394-159">This opens hello **Details** blade for this risk event.</span></span> <span data-ttu-id="e1394-160">Sur hello **détails** panneau, vous avez hello option tooeither [fermeture manuelle d’un événement à risque](active-directory-identityprotection.md#closing-risk-events-manually) ou réactiver un événement risque fermé manuellement.</span><span class="sxs-lookup"><span data-stu-id="e1394-160">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a><span data-ttu-id="e1394-162">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e1394-162">Next steps</span></span>

- <span data-ttu-id="e1394-163">Pour en savoir plus sur Azure Active Directory Identity Protection, voir [Protection de l’identité Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="e1394-163">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

