---
title: "Rapport sur la sécurité des utilisateurs avec indicateur de risque dans le portail Azure Active Directory | Microsoft Docs"
description: "En savoir plus sur le rapport sur la sécurité des utilisateurs avec indicateur de risque dans le portail Azure Active Directory"
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
ms.openlocfilehash: 04f15384a7cd0fa03300acdf159d371569ecf9fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="users-flagged-for-risk-security-report-in-the-azure-active-directory-portal"></a><span data-ttu-id="f81cd-103">Rapport sur la sécurité des utilisateurs avec indicateur de risque dans le portail Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f81cd-103">Users flagged for risk security report in the Azure Active Directory portal</span></span>

<span data-ttu-id="f81cd-104">Grâce aux rapports sur la sécurité dans Azure Active Directory (Azure AD), vous pouvez obtenir des informations sur les risques de compromission des comptes d’utilisateur au sein de votre environnement.</span><span class="sxs-lookup"><span data-stu-id="f81cd-104">With the security reports in the Azure Active Directory (Azure AD), you can gain insights into the probability of compromised user accounts in your environment.</span></span> 

<span data-ttu-id="f81cd-105">Azure Active Directory détecte les actions suspectes liées aux comptes des utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f81cd-105">Azure Active Directory detects suspicious actions that are related to your user accounts.</span></span> <span data-ttu-id="f81cd-106">Pour chaque action détectée, un enregistrement appelé *événement à risque* est créé.</span><span class="sxs-lookup"><span data-stu-id="f81cd-106">For each detected action, a record called *risk event* is created.</span></span> <span data-ttu-id="f81cd-107">Pour plus d’informations, consultez [Événements à risque dans Azure Active Directory](active-directory-identity-protection-risk-events.md).</span><span class="sxs-lookup"><span data-stu-id="f81cd-107">For more information, see [Azure Active Directory risk events](active-directory-identity-protection-risk-events.md).</span></span> 

<span data-ttu-id="f81cd-108">Les événements à risque détectés sont utilisés pour déterminer les valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81cd-108">The detected risk events are used to calculate:</span></span>

- <span data-ttu-id="f81cd-109">**Connexions risquées** : une connexion risquée est une tentative de connexion susceptible de provenir d’un utilisateur autre que le propriétaire légitime d’un compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f81cd-109">**Risky sign-ins** - A risky sign-in is an indicator for a sign-in attempt that might have been performed by someone who is not the legitimate owner of a user account.</span></span> <span data-ttu-id="f81cd-110">Pour plus d’informations, consultez [Connexions risquées](active-directory-identityprotection.md#risky-sign-ins).</span><span class="sxs-lookup"><span data-stu-id="f81cd-110">For more information, see [Risky sign-ins](active-directory-identityprotection.md#risky-sign-ins).</span></span> 

- <span data-ttu-id="f81cd-111">**Utilisateurs avec indicateur de risque** : il s’agit d’un compte d’utilisateur susceptible d’être compromis.</span><span class="sxs-lookup"><span data-stu-id="f81cd-111">**Users flagged for risk** - A risky user is an indicator for a user account that might have been compromised.</span></span> <span data-ttu-id="f81cd-112">Pour plus d’informations, consultez [Utilisateurs avec indicateur de risque](active-directory-identityprotection.md#users-flagged-for-risk).</span><span class="sxs-lookup"><span data-stu-id="f81cd-112">For more information, see [Users flagged for risk](active-directory-identityprotection.md#users-flagged-for-risk).</span></span>  

<span data-ttu-id="f81cd-113">Dans le portail Azure, vous trouverez les rapports de sécurité dans le panneau **Azure Active Directory** dans la section **Sécurité**.</span><span class="sxs-lookup"><span data-stu-id="f81cd-113">In the Azure portal, you can find the security reports on the **Azure Active Directory** blade in the **Security** section.</span></span>  

![les connexions risquées.](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-to-access-a-security-report"></a><span data-ttu-id="f81cd-115">De quelle licence Azure AD avez-vous besoin pour accéder à un rapport de sécurité ?</span><span class="sxs-lookup"><span data-stu-id="f81cd-115">What Azure AD license do you need to access a security report?</span></span>  

<span data-ttu-id="f81cd-116">Toutes les éditions d’Azure Active Directory vous indiquent les rapports d’utilisateurs associés à un indicateur de risque.</span><span class="sxs-lookup"><span data-stu-id="f81cd-116">All editions of Azure Active Directory provide you with users flagged for risk reports.</span></span>  
<span data-ttu-id="f81cd-117">Toutefois, le niveau de granularité d’un rapport varie entre les éditions :</span><span class="sxs-lookup"><span data-stu-id="f81cd-117">However, the level of report granularity varies between the editions:</span></span> 

- <span data-ttu-id="f81cd-118">Dans les **éditions Azure Active Directory Free et Basic**, vous obtenez déjà la liste des utilisateurs associés à un indicateur de risque.</span><span class="sxs-lookup"><span data-stu-id="f81cd-118">In the **Azure Active Directory Free and Basic editions**, you already get a list of users flagged for risk.</span></span> 

- <span data-ttu-id="f81cd-119">L’édition **Azure Active Directory Premium 1** étend ce modèle en vous permettant également d’examiner certains événements à risque sous-jacent qui ont été détectés pour chaque rapport.</span><span class="sxs-lookup"><span data-stu-id="f81cd-119">The **Azure Active Directory Premium 1** edition extends this model by also enabling you to examine some of the underlying risk events that have been detected for each report.</span></span> 

- <span data-ttu-id="f81cd-120">L’édition **Azure Active Directory Premium 2** vous fournit les informations les plus détaillées sur tous les événements à risque sous-jacent. Elle vous permet de configurer des stratégies de sécurité répondant automatiquement aux niveaux de risque configurés.</span><span class="sxs-lookup"><span data-stu-id="f81cd-120">The **Azure Active Directory Premium 2** edition provides you with the most detailed information about all underlying risk events and enables you to configure security policies that automatically respond to configured risk levels.</span></span>



## <a name="azure-active-directory-free-and-basic-edition"></a><span data-ttu-id="f81cd-121">Édition Azure Active Directory gratuite et de base</span><span class="sxs-lookup"><span data-stu-id="f81cd-121">Azure Active Directory free and basic edition</span></span>

<span data-ttu-id="f81cd-122">Le rapport sur les utilisateurs avec indicateur de risque dans les éditions gratuites et de base d’Azure Active Directory vous fournit une liste de comptes d’utilisateurs qui ont peut-être été compromis.</span><span class="sxs-lookup"><span data-stu-id="f81cd-122">The users flagged for risk report in the Azure Active Directory free and basic editions provides you with a list of user accounts that may have been compromised.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/03.png)

<span data-ttu-id="f81cd-124">La sélection d’un utilisateur ouvre le panneau des données utilisateur correspondant.</span><span class="sxs-lookup"><span data-stu-id="f81cd-124">Selecting a user opens the related user data blade.</span></span>
<span data-ttu-id="f81cd-125">Vous pouvez vérifier l’historique des connexions d’un utilisateur à risque et réinitialiser son mot de passe, le cas échéant.</span><span class="sxs-lookup"><span data-stu-id="f81cd-125">For users that are at risk, you can review the user’s sign-in history and reset the password if necessary.</span></span>

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/46.png)


<span data-ttu-id="f81cd-127">Cette boîte de dialogue fournit une option permettant de :</span><span class="sxs-lookup"><span data-stu-id="f81cd-127">This dialog provides you with an option to:</span></span>

- <span data-ttu-id="f81cd-128">Télécharger le rapport</span><span class="sxs-lookup"><span data-stu-id="f81cd-128">Download the report</span></span>

- <span data-ttu-id="f81cd-129">Rechercher des utilisateurs</span><span class="sxs-lookup"><span data-stu-id="f81cd-129">Search users</span></span>

![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a><span data-ttu-id="f81cd-131">Éditions Premium d’Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="f81cd-131">Azure Active Directory premium editions</span></span>

<span data-ttu-id="f81cd-132">Le rapport sur les utilisateurs avec indicateur de risque dans les éditions Premium d’Azure Active Directory vous fournit les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81cd-132">The users flagged for risk report in the Azure Active Directory premium editions provides you with:</span></span>

- <span data-ttu-id="f81cd-133">Une [liste des comptes d’utilisateurs](active-directory-identityprotection.md#users-flagged-for-risk) qui ont peut-être été compromis</span><span class="sxs-lookup"><span data-stu-id="f81cd-133">A [list of user accounts](active-directory-identityprotection.md#users-flagged-for-risk) that may have been compromised</span></span> 

- <span data-ttu-id="f81cd-134">Informations agrégées sur les [types d’événements à risque](active-directory-identity-protection-risk-events.md) qui ont été détectés</span><span class="sxs-lookup"><span data-stu-id="f81cd-134">Aggregated information about the [risk event types](active-directory-identity-protection-risk-events.md) that have been detected</span></span>

- <span data-ttu-id="f81cd-135">Une option pour télécharger le rapport</span><span class="sxs-lookup"><span data-stu-id="f81cd-135">An option to download the report</span></span>

- <span data-ttu-id="f81cd-136">Une option pour configurer une [stratégie de résolution du risque utilisateur](active-directory-identityprotection.md#user-risk-security-policy)</span><span class="sxs-lookup"><span data-stu-id="f81cd-136">An option to configure a [user risk remediation policy](active-directory-identityprotection.md#user-risk-security-policy)</span></span>  


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/71.png)

<span data-ttu-id="f81cd-138">Lorsque vous sélectionnez un utilisateur, vous obtenez une vue de rapport détaillé pour cet utilisateur qui vous permet d’effectuer les opérations suivantes :</span><span class="sxs-lookup"><span data-stu-id="f81cd-138">When you select a user, you get a detailed report view for this user that enables you to:</span></span>

- <span data-ttu-id="f81cd-139">Ouvrir la vue Toutes les connexions</span><span class="sxs-lookup"><span data-stu-id="f81cd-139">Open the All sign-ins view</span></span>

- <span data-ttu-id="f81cd-140">Réinitialisez le mot de passe de l'utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f81cd-140">Reset the user's password</span></span>

- <span data-ttu-id="f81cd-141">Ignorer tous les événements</span><span class="sxs-lookup"><span data-stu-id="f81cd-141">Dismiss all events</span></span>

- <span data-ttu-id="f81cd-142">Analysez les événements à risque signalés pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f81cd-142">Investigate reported risk events for the user.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/324.png)


<span data-ttu-id="f81cd-144">Pour analyser un événement à risque, sélectionnez-en un depuis la liste pour ouvrir le panneau **Détails** de cet événement à risque.</span><span class="sxs-lookup"><span data-stu-id="f81cd-144">To investigate a risk event, select one from the list to open the **Details** blade for this risk event.</span></span> <span data-ttu-id="f81cd-145">Dans le panneau **Détails**, vous avez le choix entre [fermer manuelle un événement à risque](active-directory-identityprotection.md#closing-risk-events-manually) ou réactiver un événement à risque fermé manuellement.</span><span class="sxs-lookup"><span data-stu-id="f81cd-145">On the **Details** blade, you have the option to either [manually close a risk event](active-directory-identityprotection.md#closing-risk-events-manually) or reactivate a manually closed risk event.</span></span> 


![Connexions risquées](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a><span data-ttu-id="f81cd-147">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f81cd-147">Next steps</span></span>

- <span data-ttu-id="f81cd-148">Pour en savoir plus sur Azure Active Directory Identity Protection, voir [Protection de l’identité Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="f81cd-148">For more information about Azure Active Directory Identity Protection, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

