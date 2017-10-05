---
title: "Compléter une révision de sécurité | Microsoft Docs"
description: "Après avoir démarré une vérification d’accès dans Azure AD Privileged Identity Management, découvrez comment la compléter et afficher les résultats"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: abc2d3dd-afd5-42cf-8a17-6c11f5674c35
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/06/2017
ms.author: kgremban
ms.custom: pim
ms.openlocfilehash: ca2a1c7c287e4cf6b1b50cfb0068861b6f525596
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-complete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="0d1dc-103">Comment effectuer une révision de l’accès dans Azure AD Privileged Identity Management ?</span><span class="sxs-lookup"><span data-stu-id="0d1dc-103">How to complete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="0d1dc-104">Les administrateurs de rôle privilégié peuvent examiner un accès privilégié une fois qu’une [révision de la sécurité a été démarrée](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="0d1dc-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="0d1dc-105">Azure AD Privileged Identity Management (PIM) envoie automatiquement un e-mail demandant aux utilisateurs d'examiner leur accès.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users to review their access.</span></span> <span data-ttu-id="0d1dc-106">Si un utilisateur n'a pas reçu d’e-mail, vous pouvez lui envoyer les instructions dans [comment effectuer une révision de sécurité](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="0d1dc-106">If a user did not get an email, you can send them the instructions in [how to perform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="0d1dc-107">Après la période de révision de sécurité, ou après que tous les utilisateurs ont terminé leur auto-examen, suivez les étapes décrites dans cet article pour gérer la révision et afficher les résultats.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-107">After the security review period is over, or all the users have finished their self-review, follow the steps in this article to manage the review and see the results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="0d1dc-108">Gérer les révisions de sécurité</span><span class="sxs-lookup"><span data-stu-id="0d1dc-108">Manage security reviews</span></span>
1. <span data-ttu-id="0d1dc-109">Accédez à la [portail Azure](https://portal.azure.com/) et sélectionnez l’application **Azure AD Privileged Identity Management** sur votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-109">Go to the [Azure portal](https://portal.azure.com/) and select the **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="0d1dc-110">Sélectionnez la section **Révisions de l’accès** du tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-110">Select the **Access reviews** section of the dashboard.</span></span>
3. <span data-ttu-id="0d1dc-111">Sélectionnez la révision d’accès que vous souhaitez gérer.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-111">Select the access review that you want to manage.</span></span>

<span data-ttu-id="0d1dc-112">Le panneau de détails de la révision d’accès comporte plusieurs options pour la gestion de cette révision.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-112">On the access review's detail blade there are a number options for managing that review.</span></span>

![Boutons de révision d’accès PIM - capture d’écran][1]

### <a name="remind"></a><span data-ttu-id="0d1dc-114">Rappeler</span><span class="sxs-lookup"><span data-stu-id="0d1dc-114">Remind</span></span>
<span data-ttu-id="0d1dc-115">Si une vérification de l’accès est configurée de sorte que les utilisateurs doivent eux-mêmes la réviser, le bouton **Rappeler** envoie une notification.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-115">If an access review is set up so that the users review themselves, the **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="0d1dc-116">Arrêter</span><span class="sxs-lookup"><span data-stu-id="0d1dc-116">Stop</span></span>
<span data-ttu-id="0d1dc-117">Toutes les révisions d’accès ont une date de fin, mais vous pouvez utiliser le bouton **Arrêter** pour les terminer plus tôt.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-117">All access reviews have an end date, but you can use the **Stop** button to finish it early.</span></span> <span data-ttu-id="0d1dc-118">Si les utilisateurs n’ont pas été révisés à cette date, ils ne pourront plus le faire une fois la révision arrêtée.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-118">If any users haven't been reviewed by this time, they won't be able to after you stop the review.</span></span> <span data-ttu-id="0d1dc-119">Vous ne pouvez pas redémarrer une révision arrêtée.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="0d1dc-120">Appliquer</span><span class="sxs-lookup"><span data-stu-id="0d1dc-120">Apply</span></span>
<span data-ttu-id="0d1dc-121">Lorsqu’une vérification de l’accès est terminé, soit parce qu’elle a atteint la date de fin ou après un arrêt manuel, le bouton **Appliquer** implémente le résultat de la révision.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-121">After an access review is completed, either because you reached the end date or stopped it manually, the **Apply** button implements the outcome of the review.</span></span> <span data-ttu-id="0d1dc-122">Si l’accès d’un utilisateur a été refusé lors de la révision, cette étape supprimera l’affectation de son rôle.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-122">If a user's access was denied in the review, this is the step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="0d1dc-123">Exportation</span><span class="sxs-lookup"><span data-stu-id="0d1dc-123">Export</span></span>
<span data-ttu-id="0d1dc-124">Si vous souhaitez appliquer manuellement les résultats de la révision de sécurité, vous pouvez exporter la révision.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-124">If you want to apply the results of the security review manually, you can export the review.</span></span> <span data-ttu-id="0d1dc-125">Le bouton **Exporter** fait démarrer le téléchargement d'un fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-125">The **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="0d1dc-126">Vous pouvez gérer les résultats dans Excel ou d'autres programmes qui s'ouvrent les fichiers CSV.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-126">You can manage the results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="0d1dc-127">Supprimer</span><span class="sxs-lookup"><span data-stu-id="0d1dc-127">Delete</span></span>
<span data-ttu-id="0d1dc-128">Si vous n'êtes plus intéressé par la révision, supprimez-la.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-128">If you are not interested in the review any further, delete it.</span></span> <span data-ttu-id="0d1dc-129">Le bouton **Supprimer** permet de supprimer la révision de l'application PIM.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-129">The **Delete** button removes the review from the PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0d1dc-130">La suppression ayant lieu sans affichage préalable d’un avertissement, assurez-vous que vous voulez supprimer cette révision.</span><span class="sxs-lookup"><span data-stu-id="0d1dc-130">You will not get a warning before deletion occurs, so be sure that you want to delete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0d1dc-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0d1dc-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
