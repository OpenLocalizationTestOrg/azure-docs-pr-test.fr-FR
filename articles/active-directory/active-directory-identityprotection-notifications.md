---
title: "notifications de la Protection d’identité Active Directory aaaAzure | Documents Microsoft"
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
ms.openlocfilehash: 19e62374873f034591c658a779f97d935766c612
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-identity-protection-notifications"></a><span data-ttu-id="3a4cd-104">Notifications d’Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3a4cd-104">Azure Active Directory Identity Protection notifications</span></span>
<span data-ttu-id="3a4cd-105">Azure AD Identity Protection envoie deux types de notification automatisé des e-mails toohelp que vous gérez risque d’utilisateur et les événements à risque :</span><span class="sxs-lookup"><span data-stu-id="3a4cd-105">Azure AD Identity Protection sends two types of automated notification emails toohelp you manage user risk and risk events:</span></span>

* <span data-ttu-id="3a4cd-106">E-mail d’alerte en cas d’utilisateur compromis</span><span class="sxs-lookup"><span data-stu-id="3a4cd-106">User compromised alert email</span></span>
* <span data-ttu-id="3a4cd-107">E-mail de synthèse hebdomadaire</span><span class="sxs-lookup"><span data-stu-id="3a4cd-107">Weekly digest email</span></span>

## <a name="user-compromised-alert-email"></a><span data-ttu-id="3a4cd-108">E-mail d’alerte en cas d’utilisateur compromis</span><span class="sxs-lookup"><span data-stu-id="3a4cd-108">User compromised alert email</span></span>
<span data-ttu-id="3a4cd-109">Un e-mail d’alerte en cas d’utilisateur compromis est généré lorsqu’Azure AD Identity Protection identifie un compte compromis.</span><span class="sxs-lookup"><span data-stu-id="3a4cd-109">A user compromised email alert is generated when Azure AD Identity Protection identifies an account as compromised.</span></span> <span data-ttu-id="3a4cd-110">messagerie de Hello inclut un toohello lien Qu'utilisateurs marqués en vue d’état risque dans le tableau de bord hello Identity Protection.</span><span class="sxs-lookup"><span data-stu-id="3a4cd-110">hello email includes a link toohello Users flagged for risk report in hello Identity Protection dashboard.</span></span> <span data-ttu-id="3a4cd-111">Nous vous recommandons d’examiner immédiatement les notifications des comptes compromis.</span><span class="sxs-lookup"><span data-stu-id="3a4cd-111">We recommend that you immediately investigate notifications of compromised accounts.</span></span>

## <a name="weekly-digest-email"></a><span data-ttu-id="3a4cd-112">E-mail de synthèse hebdomadaire</span><span class="sxs-lookup"><span data-stu-id="3a4cd-112">Weekly digest email</span></span>
<span data-ttu-id="3a4cd-113">e-mail de résumé hebdomadaire Hello contient un résumé des nouveaux événements de risque.</span><span class="sxs-lookup"><span data-stu-id="3a4cd-113">hello weekly digest email contains a summary of new risk events.</span></span><br>
<span data-ttu-id="3a4cd-114">Il inclut :</span><span class="sxs-lookup"><span data-stu-id="3a4cd-114">It includes:</span></span>

* <span data-ttu-id="3a4cd-115">Les utilisateurs à risque</span><span class="sxs-lookup"><span data-stu-id="3a4cd-115">Users at risk</span></span>
* <span data-ttu-id="3a4cd-116">Activités suspectes</span><span class="sxs-lookup"><span data-stu-id="3a4cd-116">Suspicious activities</span></span>
* <span data-ttu-id="3a4cd-117">Les vulnérabilités détectées</span><span class="sxs-lookup"><span data-stu-id="3a4cd-117">Detected vulnerabilities</span></span>
* <span data-ttu-id="3a4cd-118">Liens toohello liées dans la Protection de l’identité des rapports</span><span class="sxs-lookup"><span data-stu-id="3a4cd-118">Links toohello related reports in Identity Protection</span></span>

<br><span data-ttu-id="3a4cd-119">
![Mise à jour](./media/active-directory-identityprotection-notifications/400.png "mise à jour")
</span><span class="sxs-lookup"><span data-stu-id="3a4cd-119">
![Remediation](./media/active-directory-identityprotection-notifications/400.png "Remediation")
</span></span><br>

<span data-ttu-id="3a4cd-120">Vous pouvez désactiver l’envoi de l’e-mail de synthèse hebdomadaire.</span><span class="sxs-lookup"><span data-stu-id="3a4cd-120">You can switch sending a weekly digest email off.</span></span>
<br><br><span data-ttu-id="3a4cd-121">
![Risques pour l’utilisateur](./media/active-directory-identityprotection-notifications/62.png "risques pour l’utilisateur")
</span><span class="sxs-lookup"><span data-stu-id="3a4cd-121">
![User risks](./media/active-directory-identityprotection-notifications/62.png "User risks")
</span></span><br>

<span data-ttu-id="3a4cd-122">**boîte de dialogue configuration associés tooopen hello**:</span><span class="sxs-lookup"><span data-stu-id="3a4cd-122">**tooopen hello related configuration dialog**:</span></span>

1. <span data-ttu-id="3a4cd-123">Sur hello **Azure AD Identity Protection** panneau, cliquez sur **paramètres**.</span><span class="sxs-lookup"><span data-stu-id="3a4cd-123">On hello **Azure AD Identity Protection** blade, click **Settings**.</span></span>
   <br><br><span data-ttu-id="3a4cd-124">
   ![Stratégie des risques utilisateur](./media/active-directory-identityprotection-notifications/401.png "stratégie risque de l’utilisateur")
   </span><span class="sxs-lookup"><span data-stu-id="3a4cd-124">
![User risk policy](./media/active-directory-identityprotection-notifications/401.png "User risk policy")
</span></span><br>
2. <span data-ttu-id="3a4cd-125">Bonjour **général** , cliquez sur **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="3a4cd-125">In hello **General** section, click **Notifications**.</span></span>
   <br><br><span data-ttu-id="3a4cd-126">
   ![Stratégie des risques utilisateur](./media/active-directory-identityprotection-notifications/405.png "stratégie risque de l’utilisateur")
   </span><span class="sxs-lookup"><span data-stu-id="3a4cd-126">
![User risk policy](./media/active-directory-identityprotection-notifications/405.png "User risk policy")
</span></span><br>

## <a name="see-also"></a><span data-ttu-id="3a4cd-127">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="3a4cd-127">See also</span></span>
* [<span data-ttu-id="3a4cd-128">Azure Active Directory Identity Protection</span><span class="sxs-lookup"><span data-stu-id="3a4cd-128">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)
