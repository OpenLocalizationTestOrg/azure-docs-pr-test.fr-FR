---
title: "aaaUsers signalées pour le rapport de sécurité risque dans le portail d’Azure Active Directory hello | Documents Microsoft"
description: "En savoir plus sur les utilisateurs hello signalées pour le rapport de sécurité risque dans le portail d’Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a><span data-ttu-id="b3a9b-103">Utilisateurs marqués en vue d’état de sécurité risque dans le portail d’Azure Active Directory hello</span><span class="sxs-lookup"><span data-stu-id="b3a9b-103">Users flagged for risk security report in hello Azure Active Directory portal</span></span>

<span data-ttu-id="b3a9b-104">Avec les rapports de sécurité hello Bonjour Azure Active Directory (Azure AD), vous pouvez obtenir probabilité hello de comptes d’utilisateur compromis dans votre environnement.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-104">With hello security reports in hello Azure Active Directory (Azure AD), you can gain insights into hello probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="b3a9b-105">Azure Active Directory détecte les actions suspectes qui sont des comptes d’utilisateur tooyour connexes.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-105">Azure Active Directory detects suspicious actions that are related tooyour user accounts.</span></span> <span data-ttu-id="b3a9b-106">Pour chaque action détectée, un enregistrement appelé *événement à risque* est créé.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="b3a9b-107">Pour plus d’informations, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="b3a9b-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="b3a9b-108">Hello détecté risque toocalculate utilisé :</span><span class="sxs-lookup"><span data-stu-id="b3a9b-108">hello detected risk events are used toocalculate:</span></span>

- <span data-ttu-id="b3a9b-109">**Connexions risquées** -un risque de connexion est un indicateur pour une tentative de connexion qui ont peut-être été exécutée par une personne qui n’est pas propriétaire de légitime hello d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not hello legitimate owner of a user account.</span></span> <span data-ttu-id="b3a9b-110">Pour plus d’informations, consultez [Connexions risquées](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="b3a9b-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="b3a9b-111">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="b3a9b-112">Pour plus d’informations, consultez [Utilisateurs avec indicateur de risque](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="b3a9b-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="b3a9b-113">Bonjour portail Azure, vous pouvez trouver hello la sécurité des rapports sur hello **Azure Active Directory** panneau Bonjour **sécurité** section.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-113">In hello Azure portal, you can find hello security reports on hello **Azure Active Directory** blade in hello **Security** section.</span></span>  

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a><span data-ttu-id="b3a9b-115">Licence Azure AD tooaccess un rapport de sécurité avez-vous besoin ?</span><span class="sxs-lookup"><span data-stu-id="b3a9b-115">What Azure AD license do you need tooaccess a security report?</span></span>  

<span data-ttu-id="b3a9b-116">Toutes les éditions d’Azure Active Directory vous indiquent les rapports d’utilisateurs associés à un indicateur de risque.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="b3a9b-117">Toutefois, au niveau de granularité d’un rapport du hello varie entre les éditions de hello :</span><span class="sxs-lookup"><span data-stu-id="b3a9b-117">However, hello level of report granularity varies between hello editions:</span></span> 

- <span data-ttu-id="b3a9b-118">Bonjour **éditions Azure Active Directory gratuit et Basic**, vous obtenez déjà une liste d’utilisateurs avec indicateur de risque.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-118">In hello **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="b3a9b-119">Hello **Azure Active Directory Premium 1** edition étend ce modèle en vous permettant également tooexamine certains hello sous-jacent des événements à risque qui ont été détectés pour chaque rapport.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-119">hello **Azure Active Directory Premium 1** edition extends this model by also enabling you tooexamine some of hello underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="b3a9b-120">Hello **Azure Active Directory Premium 2** vous offre une édition hello des informations plus détaillées sur tous les événements à risque sous-jacent et vous permet de stratégies de sécurité tooconfigure répondre automatiquement aux risques de tooconfigured niveaux.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-120">hello **Azure Active Directory Premium 2** edition provides you with hello most detailed information about all underlying risk events and enables you tooconfigure security policies that automatically respond tooconfigured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="b3a9b-121">Édition Azure Active Directory gratuite et de base</span><span class="sxs-lookup"><span data-stu-id="b3a9b-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="b3a9b-122">utilisateurs Hello signalées pour le rapport des risques dans les éditions gratuites et de base du Azure Active Directory hello vous fournit une liste des comptes d’utilisateur qui ont peut-être été compromis.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-122">hello users flagged for risk report in hello Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="b3a9b-124">Sélection d’un utilisateur ouvre lame hello utilisateur connexes.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-124">Selecting a user opens hello related user data blade.</span></span>
<span data-ttu-id="b3a9b-125">Pour les utilisateurs qui sont exposés, vous pouvez consulter les hello historique de l’utilisateur de connexion et réinitialiser le mot de passe de hello si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-125">For users that are at risk, you can review hello user’s sign-in history and reset hello password if necessary.</span></span>

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="b3a9b-127">Cette boîte de dialogue fournit une option permettant de :</span><span class="sxs-lookup"><span data-stu-id="b3a9b-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="b3a9b-128">Télécharger des rapports de hello</span><span class="sxs-lookup"><span data-stu-id="b3a9b-128">Download hello report</span></span>

- <span data-ttu-id="b3a9b-129">Rechercher des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="b3a9b-129">Search users</span></span>

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="b3a9b-131">Éditions Premium d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="b3a9b-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="b3a9b-132">les utilisateurs Hello signalées pour le rapport des risques dans les éditions premium hello Azure Active Directory vous offre :</span><span class="sxs-lookup"><span data-stu-id="b3a9b-132">hello users flagged for risk report in hello Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="b3a9b-133">Une [liste des comptes d’utilisateurs](active-directory-identityprotection.md#users-flagged-for-risk) qui ont peut-être été compromis</span><span class="sxs-lookup"><span data-stu-id="b3a9b-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="b3a9b-134">Agrégé des informations sur hello [risque de types d’événements](active-directory-identity-protection-risk-events.md) qui ont été détectées</span><span class="sxs-lookup"><span data-stu-id="b3a9b-134">Aggregated information about hello [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="b3a9b-135">Un rapport de hello toodownload option</span><span class="sxs-lookup"><span data-stu-id="b3a9b-135">An option toodownload hello report</span></span>

- <span data-ttu-id="b3a9b-136">Une option tooconfigure un [stratégie de mise à jour risque d’utilisateur](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="b3a9b-136">An option tooconfigure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="b3a9b-138">Lorsque vous sélectionnez un utilisateur, vous obtenez une vue de rapport détaillé pour cet utilisateur qui vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="b3a9b-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="b3a9b-139">Ouvrez hello que permet d’afficher toutes les connexions</span><span class="sxs-lookup"><span data-stu-id="b3a9b-139">Open hello All sign-ins view</span></span>

- <span data-ttu-id="b3a9b-140">Réinitialiser le mot de passe de l’utilisateur hello</span><span class="sxs-lookup"><span data-stu-id="b3a9b-140">Reset hello user's password</span></span>

- <span data-ttu-id="b3a9b-141">Ignorer tous les événements</span><span class="sxs-lookup"><span data-stu-id="b3a9b-141">Dismiss all events</span></span>

- <span data-ttu-id="b3a9b-142">Examiner les événements à risque signalé pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-142">Investigate reported risk events for hello user.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="b3a9b-144">tooinvestigate un événement à risque, sélectionnez-en un dans hello de hello liste tooopen **détails** panneau pour cet événement risque.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-144">tooinvestigate a risk event, select one from hello list tooopen hello **Details** blade for this risk event.</span></span> <span data-ttu-id="b3a9b-145">Sur hello **détails** panneau, vous avez hello option tooeither [fermeture manuelle d’un événement à risque](active-directory-identityprotection.md#closing-risk-events-manually) ou réactiver un événement risque fermé manuellement.</span><span class="sxs-lookup"><span data-stu-id="b3a9b-145">On hello **Details** blade, you have hello option tooeither [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="b3a9b-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3a9b-147">Next steps</span></span>

- <span data-ttu-id="b3a9b-148">Pour en savoir plus sur Azure Active Directory Identity Protection, voir [Protection de l’identité Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="b3a9b-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

