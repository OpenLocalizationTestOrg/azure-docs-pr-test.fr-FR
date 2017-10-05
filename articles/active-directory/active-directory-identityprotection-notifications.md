---
title: "Notifications d’Azure Active Directory Identity Protection | Microsoft Docs"
description: "Découvrez comment les notifications prennent en charge vos activités d’examen."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gestion d’applications, sécurité, risque, niveau de risque, vulnérabilité, stratégie de sécurité"
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 65ca79b9-4da1-4d5b-bebd-eda776cc32c7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 079d16bbf75cd2b3b94269d684e1ae1a0e6aa967
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="f646e-104">Notifications d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f646e-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="f646e-105">Azure AD Identity Protection envoie deux types d’e-mails de notification automatisés pour vous aider à gérer le risque des utilisateurs et les événements à risque :</span><span class="sxs-lookup"><span data-stu-id="f646e-105">Azure AD Identity Protection sends two types of automated notification emails to help you manage user risk and risk events:</span></span>

* <span data-ttu-id="f646e-106">E-mail d’alerte en cas d’utilisateur compromis</span><span class="sxs-lookup"><span data-stu-id="f646e-106">User compromised alert email</span></span>
* <span data-ttu-id="f646e-107">E-mail de synthèse hebdomadaire</span><span class="sxs-lookup"><span data-stu-id="f646e-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="f646e-108">E-mail d’alerte en cas d’utilisateur compromis</span><span class="sxs-lookup"><span data-stu-id="f646e-108">User compromised alert email</span></span>
<span data-ttu-id="f646e-109">Un e-mail d’alerte en cas d’utilisateur compromis est généré lorsqu’Azure AD Identity Protection identifie un compte compromis.</span><span class="sxs-lookup"><span data-stu-id="f646e-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="f646e-110">Cet e-mail inclut un lien vers le rapport Utilisateurs associés à un indicateur de risque dans le tableau de bord d’Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="f646e-110">The email includes a link to the Users flagged for risk report in the Identity Protection dashboard.</span></span> <span data-ttu-id="f646e-111">Nous vous recommandons d’examiner immédiatement les notifications des comptes compromis.</span><span class="sxs-lookup"><span data-stu-id="f646e-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="f646e-112">E-mail de synthèse hebdomadaire</span><span class="sxs-lookup"><span data-stu-id="f646e-112">Weekly digest email</span></span>
<span data-ttu-id="f646e-113">L’e-mail de synthèse hebdomadaire contient un récapitulatif des nouveaux événements à risque.</span><span class="sxs-lookup"><span data-stu-id="f646e-113">The weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="f646e-114">Il inclut :</span><span class="sxs-lookup"><span data-stu-id="f646e-114">It includes:</span></span>

* <span data-ttu-id="f646e-115">Les utilisateurs à risque</span><span class="sxs-lookup"><span data-stu-id="f646e-115">Users at risk</span></span>
* <span data-ttu-id="f646e-116">Activités suspectes</span><span class="sxs-lookup"><span data-stu-id="f646e-116">Suspicious activities</span></span>
* <span data-ttu-id="f646e-117">Les vulnérabilités détectées</span><span class="sxs-lookup"><span data-stu-id="f646e-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="f646e-118">Des liens vers les rapports connexes dans Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f646e-118">Links to the related reports in Identity Protection</span></span>

<br><span data-ttu-id="f646e-119">
![Mise à jour](./media/active-directory-identityprotection-notifications/400.png "mise à jour")
</span><span class="sxs-lookup"><span data-stu-id="f646e-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="f646e-120">Vous pouvez désactiver l’envoi de l’e-mail de synthèse hebdomadaire.</span><span class="sxs-lookup"><span data-stu-id="f646e-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="f646e-121">
![Risques pour l’utilisateur](./media/active-directory-identityprotection-notifications/62.png "risques pour l’utilisateur")
</span><span class="sxs-lookup"><span data-stu-id="f646e-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="f646e-122">**Pour ouvrir la boîte de dialogue de configuration connexe**:</span><span class="sxs-lookup"><span data-stu-id="f646e-122">**To open the related configuration dialog**:</span></span>

1. <span data-ttu-id="f646e-123">Dans le panneau **Azure AD Identity Protection**, cliquez sur **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="f646e-123">On the **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="f646e-124">
   ![Stratégie des risques utilisateur](./media/active-directory-identityprotection-notifications/401.png "stratégie risque de l’utilisateur")
   </span><span class="sxs-lookup"><span data-stu-id="f646e-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="f646e-125">Dans la section **Général**, cliquez sur **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="f646e-125">In the **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="f646e-126">
   ![Stratégie des risques utilisateur](./media/active-directory-identityprotection-notifications/405.png "stratégie risque de l’utilisateur")
   </span><span class="sxs-lookup"><span data-stu-id="f646e-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="f646e-127">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="f646e-127">See also</span></span>
* [<span data-ttu-id="f646e-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="f646e-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
