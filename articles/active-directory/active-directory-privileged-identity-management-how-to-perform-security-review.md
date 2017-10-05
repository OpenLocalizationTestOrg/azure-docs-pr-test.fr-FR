---
title: "Exécution d’une révision d’accès | Microsoft Docs"
description: "Découvrez comment effectuer une révision avec l'application Azure Privileged Identity Management."
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
ms.openlocfilehash: a98ed60221eeba1d9c92df846aeae2deafb8ae60
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-perform-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="11753-103">Comment effectuer une révision de l’accès dans Azure AD Privileged Identity Management ?</span><span class="sxs-lookup"><span data-stu-id="11753-103">How to perform an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="11753-104">Le service Azure Active Directory (AD) Privileged Identity Management simplifie la gestion par les entreprises de l’accès privilégié aux ressources dans Azure AD et d’autres services en ligne Microsoft tels qu’Office 365 ou que Microsoft Intune.</span><span class="sxs-lookup"><span data-stu-id="11753-104">Azure Active Directory (AD) Privileged Identity Management simplifies how enterprises manage privileged access to resources in Azure AD and other Microsoft online services like Office 365 or Microsoft Intune.</span></span>  

<span data-ttu-id="11753-105">Si vous êtes affecté à un rôle d’administrateur, l’administrateur de rôle privilégié de votre organisation peut vous demander de confirmer régulièrement que vous avez toujours besoin de ce rôle pour votre travail.</span><span class="sxs-lookup"><span data-stu-id="11753-105">If you are assigned to an administrative role, your organization's privileged role administrator may ask you to regularly confirm that you still need that role for your job.</span></span> <span data-ttu-id="11753-106">Vous pouvez recevoir un e-mail contenant un lien ou accéder directement au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="11753-106">You might get an email that includes a link, or you can go straight to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="11753-107">Suivez les étapes décrites dans cet article pour effectuer un auto-examen de vos rôles attribués.</span><span class="sxs-lookup"><span data-stu-id="11753-107">Follow the steps in this article to perform a self-review of your assigned roles.</span></span>

<span data-ttu-id="11753-108">Si vous êtes un administrateur de rôle privilégié intéressé par les révisions d’accès, consultez [Comment démarrer une révision de sécurité](active-directory-privileged-identity-management-how-to-start-security-review.md)pour plus de détails.</span><span class="sxs-lookup"><span data-stu-id="11753-108">If you're a privileged role administrator interested in access reviews, get more details at [How to start an access review](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span>

## <a name="add-the-privileged-identity-management-application"></a><span data-ttu-id="11753-109">Ajout de l’application Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="11753-109">Add the Privileged Identity Management application</span></span>
<span data-ttu-id="11753-110">Vous pouvez utiliser l'application Azure AD Privileged Identity Management (PIM) dans le [portail Azure](https://portal.azure.com/) pour effectuer votre révision.</span><span class="sxs-lookup"><span data-stu-id="11753-110">You can use the Azure AD Privileged Identity Management (PIM) application in the [Azure portal](https://portal.azure.com/) to perform your review.</span></span>  <span data-ttu-id="11753-111">Si vous n'avez pas l'application Azure AD Privileged Identity Management sur votre portail, procédez comme suit pour commencer.</span><span class="sxs-lookup"><span data-stu-id="11753-111">If you don't have the Azure AD Privileged Identity Management application on your portal, follow these steps to get started.</span></span>

1. <span data-ttu-id="11753-112">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="11753-112">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="11753-113">Sélectionnez votre nom d’utilisateur dans le coin supérieur droit du portail Azure, puis choisissez le répertoire que vous allez utiliser.</span><span class="sxs-lookup"><span data-stu-id="11753-113">Select your username in the upper right-hand corner of the Azure portal, and select the directory where you will you be operating.</span></span>
3. <span data-ttu-id="11753-114">Sélectionnez **Plus de services** et utilisez la zone de texte Filtre pour rechercher **Azure AD Privileged Identity Management**.</span><span class="sxs-lookup"><span data-stu-id="11753-114">Select **More services** and use the Filter textbox to search for **Azure AD Privileged Identity Management**.</span></span>
4. <span data-ttu-id="11753-115">Cochez **Épingler au tableau de bord**, puis cliquez sur **Créer**.</span><span class="sxs-lookup"><span data-stu-id="11753-115">Check **Pin to dashboard** and then click **Create**.</span></span> <span data-ttu-id="11753-116">L’application Privileged Identity Management s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="11753-116">The Privileged Identity Management application will open.</span></span>

## <a name="approve-or-deny-access"></a><span data-ttu-id="11753-117">Approuver ou refuser l'accès</span><span class="sxs-lookup"><span data-stu-id="11753-117">Approve or deny access</span></span>
<span data-ttu-id="11753-118">Lorsque vous acceptez ou refusez l’accès, vous indiquez simplement au réviseur si vous utilisez toujours ce rôle ou non.</span><span class="sxs-lookup"><span data-stu-id="11753-118">When you approve or deny access, you're just telling the reviewer whether you still use this role or not.</span></span> <span data-ttu-id="11753-119">Choisissez **Approuver** si vous souhaitez conserver le rôle, ou **Refuser** si vous n’avez plus besoin de l’accès.</span><span class="sxs-lookup"><span data-stu-id="11753-119">Choose **Approve** if you want to stay in the role, or **Deny** if you don't need the access anymore.</span></span> <span data-ttu-id="11753-120">Votre état ne change pas tout de suite car le réviseur doit d’abord appliquer les résultats.</span><span class="sxs-lookup"><span data-stu-id="11753-120">Your status won't change right away, until the reviewer applies the results.</span></span>
<span data-ttu-id="11753-121">Procédez comme suit pour rechercher et terminer la révision de l’accès :</span><span class="sxs-lookup"><span data-stu-id="11753-121">Follow these steps to find and complete the access review:</span></span>

1. <span data-ttu-id="11753-122">Dans l’application PIM, sélectionnez **Réviser un accès privilégié**.</span><span class="sxs-lookup"><span data-stu-id="11753-122">In the PIM application, select **Review privileged access**.</span></span> <span data-ttu-id="11753-123">Si vous avez des révisions d’accès en attente, ces révisions apparaissent dans le panneau des révisions d’accès Azure AD.</span><span class="sxs-lookup"><span data-stu-id="11753-123">If you have any pending access reviews, they appear in the Azure AD Access reviews blade.</span></span>
2. <span data-ttu-id="11753-124">Sélectionnez la révision à terminer.</span><span class="sxs-lookup"><span data-stu-id="11753-124">Select the review you want to complete.</span></span>
3. <span data-ttu-id="11753-125">Sauf si vous avez créé la révision, vous serez l’unique utilisateur de cette révision.</span><span class="sxs-lookup"><span data-stu-id="11753-125">Unless you created the review, you appear as the only user in the review.</span></span> <span data-ttu-id="11753-126">Cochez la case en regard de votre nom.</span><span class="sxs-lookup"><span data-stu-id="11753-126">Select the check mark next to your name.</span></span>
4. <span data-ttu-id="11753-127">Choisissez **Approuver** ou **Refuser**.</span><span class="sxs-lookup"><span data-stu-id="11753-127">Choose either **Approve** or **Deny**.</span></span> <span data-ttu-id="11753-128">Vous devrez peut-être motiver votre choix dans la zone de texte **Indiquez une raison** .</span><span class="sxs-lookup"><span data-stu-id="11753-128">You may need to include a reason for your decision in the **Provide a reason** text box.</span></span>  
5. <span data-ttu-id="11753-129">Fermez le panneau **Réviser les rôles Azure AD** .</span><span class="sxs-lookup"><span data-stu-id="11753-129">Close the **Review Azure AD roles** blade.</span></span>

<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->
## <a name="next-steps"></a><span data-ttu-id="11753-130">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="11753-130">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-configure/PIM_EnablePim.png
