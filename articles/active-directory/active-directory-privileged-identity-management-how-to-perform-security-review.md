---
title: "aaaHow tooperform une vérification de l’accès | Documents Microsoft"
description: "Découvrez comment tooperform un réexamen avec hello application d’Azure Privileged Identity Management."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 49ee2feb-7d2e-4acf-82c1-40ff23062862
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: billmath
ms.custom: pim
ms.openlocfilehash: 301a5e9f97b68fedfbf4954e0bd7dadb7f0fc510
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooperform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="e2b58-103">Comment tooperform un accès passez en revue dans Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="e2b58-103">How tooperform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="e2b58-104">Azure Active Directory (AD) Privileged Identity Management simplifie comment gérer les entreprises tooresources accès privilégié dans Azure AD et autres services en ligne Microsoft comme Office 365 ou Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="e2b58-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access tooresources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="e2b58-105">Si vous êtes affecté le rôle d’administrateur de tooan, l’administrateur de votre organisation rôle privilégié peut vous demander de tooregularly confirmer que vous devez toujours ce rôle pour votre travail.</span><span class="sxs-lookup"><span data-stu-id="e2b58-105">If you are assigned tooan administrative role, your organization's privileged role administrator may ask you tooregularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="e2b58-106">Vous pouvez obtenir un message électronique contenant un lien, ou vous pouvez accéder droite toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="e2b58-106">You might get an email that includes a link, or you can go straight toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="e2b58-107">Suivez les étapes de hello dans cette tooperform article automatique examiner vos rôles sont affectés.</span><span class="sxs-lookup"><span data-stu-id="e2b58-107">Follow hello steps in this article tooperform a self-review of your assigned roles.</span></span>

<span data-ttu-id="e2b58-108">Si vous êtes un administrateur de rôle privilégié intéressé par accès révisions, obtenir plus de détails à [façon toostart examiner un accès](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="e2b58-108">If you're a privileged role administrator interested in access reviews, get more details at [How toostart an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-hello-privileged-identity-management-application"></a><span data-ttu-id="e2b58-109">Ajouter une application de Privileged Identity Management hello</span><span class="sxs-lookup"><span data-stu-id="e2b58-109">Add hello Privileged Identity Management application</span></span>
<span data-ttu-id="e2b58-110">Vous pouvez utiliser l’application de gestion d’identité privilégié (PIM) hello Azure AD Bonjour [portail Azure](https://portal.azure.com/) tooperform les examiner.</span><span class="sxs-lookup"><span data-stu-id="e2b58-110">You can use hello Azure AD Privileged Identity Management (PIM) application in hello [Azure portal](https://portal.azure.com/) tooperform your review.</span></span>  <span data-ttu-id="e2b58-111">Si vous n’avez application Azure AD Privileged Identity Management de hello sur votre portail, suivez ces tooget étapes a démarré.</span><span class="sxs-lookup"><span data-stu-id="e2b58-111">If you don't have hello Azure AD Privileged Identity Management application on your portal, follow these steps tooget started.</span></span>

1. <span data-ttu-id="e2b58-112">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e2b58-112">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="e2b58-113">Sélectionnez votre nom d’utilisateur dans hello coin supérieur droit de hello portail Azure et répertoire hello sélectionnez où vous allez être fonctionne.</span><span class="sxs-lookup"><span data-stu-id="e2b58-113">Select your username in hello upper right-hand corner of hello Azure portal, and select hello directory where you will you be operating.</span></span>
3. <span data-ttu-id="e2b58-114">Sélectionnez **davantage de services** et utiliser toosearch de zone de texte de filtre hello pour **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="e2b58-114">Select **More services** and use hello Filter textbox toosearch for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="e2b58-115">Vérifiez **code confidentiel toodashboard** puis cliquez sur **créer**.</span><span class="sxs-lookup"><span data-stu-id="e2b58-115">Check **Pin toodashboard** and then click **Create**.</span></span> <span data-ttu-id="e2b58-116">Hello application de Privileged Identity Management s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="e2b58-116">hello Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="e2b58-117">Approuver ou refuser l'accès</span><span class="sxs-lookup"><span data-stu-id="e2b58-117">Approve or deny access</span></span>
<span data-ttu-id="e2b58-118">Lorsque vous approuvez ou refusez l’accès, vous indiquez simplement réviseur de hello si vous utilisez toujours ce rôle ou non.</span><span class="sxs-lookup"><span data-stu-id="e2b58-118">When you approve or deny access, you're just telling hello reviewer whether you still use this role or not.</span></span> <span data-ttu-id="e2b58-119">Choisissez **approuver** si vous souhaitez que toostay dans le rôle de hello, ou **Deny** si vous ne devez hello accès plus.</span><span class="sxs-lookup"><span data-stu-id="e2b58-119">Choose **Approve** if you want toostay in hello role, or **Deny** if you don't need hello access anymore.</span></span> <span data-ttu-id="e2b58-120">Votre état ne changera pas tout de suite, jusqu'à ce que le réviseur de hello applique les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="e2b58-120">Your status won't change right away, until hello reviewer applies hello results.</span></span>
<span data-ttu-id="e2b58-121">Suivez ces étapes toofind et terminer la vérification de l’accès hello :</span><span class="sxs-lookup"><span data-stu-id="e2b58-121">Follow these steps toofind and complete hello access review:</span></span>

1. <span data-ttu-id="e2b58-122">Bonjour application PIM, sélectionnez **révision d’un accès privilégié**.</span><span class="sxs-lookup"><span data-stu-id="e2b58-122">In hello PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="e2b58-123">Si vous disposez de toutes les révisions en attente d’accès, ils apparaissent Bonjour Qu'azure AD Access passe en revue le panneau.</span><span class="sxs-lookup"><span data-stu-id="e2b58-123">If you have any pending access reviews, they appear in hello Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="e2b58-124">Sélectionnez la révision hello souhaité toocomplete.</span><span class="sxs-lookup"><span data-stu-id="e2b58-124">Select hello review you want toocomplete.</span></span>
3. <span data-ttu-id="e2b58-125">Sauf si vous avez créé la révision de hello, vous apparaissez comme hello uniquement l’utilisateur en cours de révision de hello.</span><span class="sxs-lookup"><span data-stu-id="e2b58-125">Unless you created hello review, you appear as hello only user in hello review.</span></span> <span data-ttu-id="e2b58-126">Sélectionnez le nom de tooyour suivant hello case à cocher.</span><span class="sxs-lookup"><span data-stu-id="e2b58-126">Select hello check mark next tooyour name.</span></span>
4. <span data-ttu-id="e2b58-127">Choisissez **Approuver** ou **Refuser**.</span><span class="sxs-lookup"><span data-stu-id="e2b58-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="e2b58-128">Vous devrez peut-être tooinclude raison de votre décision Bonjour **fournir une raison** zone de texte.</span><span class="sxs-lookup"><span data-stu-id="e2b58-128">You may need tooinclude a reason for your decision in hello **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="e2b58-129">Fermer hello **rôles Azure AD** panneau.</span><span class="sxs-lookup"><span data-stu-id="e2b58-129">Close hello **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="e2b58-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e2b58-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
