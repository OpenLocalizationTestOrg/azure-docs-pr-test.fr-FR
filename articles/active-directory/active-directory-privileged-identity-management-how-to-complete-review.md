---
title: "aaaHow toocomplete une vérification de l’accès | Documents Microsoft"
description: "Une fois que vous avez démarré une vérification de l’accès dans Azure AD Privileged Identity Management, découvrez comment toocomplete il et vue hello résultats"
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
ms.openlocfilehash: f99ddf3ebcf80b51110326064d584f33d8e1679a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocomplete-an-access-review-in-azure-ad-privileged-identity-management"></a><span data-ttu-id="5e2f7-103">Comment toocomplete un accès passez en revue dans Azure AD Privileged Identity Management</span><span class="sxs-lookup"><span data-stu-id="5e2f7-103">How toocomplete an access review in Azure AD Privileged Identity Management</span></span>
<span data-ttu-id="5e2f7-104">Les administrateurs de rôle privilégié peuvent examiner un accès privilégié une fois qu’une [révision de la sécurité a été démarrée](active-directory-privileged-identity-management-how-to-start-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="5e2f7-104">Privileged role administrators can review privileged access once a [security review has been started](active-directory-privileged-identity-management-how-to-start-security-review.md).</span></span> <span data-ttu-id="5e2f7-105">Azure AD Privileged Identity Management (PIM) envoie automatiquement un message électronique demandant aux utilisateurs tooreview leur accès.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-105">Azure AD Privileged Identity Management (PIM) will automatically send an email prompting users tooreview their access.</span></span> <span data-ttu-id="5e2f7-106">Si un utilisateur n’a pas reçu un message électronique, vous pouvez envoyer les instructions de hello [façon tooperform examiner une sécurité](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span><span class="sxs-lookup"><span data-stu-id="5e2f7-106">If a user did not get an email, you can send them hello instructions in [how tooperform a security review](active-directory-privileged-identity-management-how-to-perform-security-review.md).</span></span>

<span data-ttu-id="5e2f7-107">Après la période de révision de sécurité hello ou tous les utilisateurs de hello ont terminé leurs examiner automatique, suivez les étapes de hello dans cette revue de hello toomanage article et afficher les résultats de hello.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-107">After hello security review period is over, or all hello users have finished their self-review, follow hello steps in this article toomanage hello review and see hello results.</span></span>

## <a name="manage-security-reviews"></a><span data-ttu-id="5e2f7-108">Gérer les révisions de sécurité</span><span class="sxs-lookup"><span data-stu-id="5e2f7-108">Manage security reviews</span></span>
1. <span data-ttu-id="5e2f7-109">Accédez toohello [portail Azure](https://portal.azure.com/) et sélectionnez hello **Azure AD Privileged Identity Management** application sur votre tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-109">Go toohello [Azure portal](https://portal.azure.com/) and select hello **Azure AD Privileged Identity Management** application on your dashboard.</span></span>
2. <span data-ttu-id="5e2f7-110">Sélectionnez hello **accès révisions** section du tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-110">Select hello **Access reviews** section of hello dashboard.</span></span>
3. <span data-ttu-id="5e2f7-111">Sélectionnez la vérification de l’accès hello que vous souhaitez toomanage.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-111">Select hello access review that you want toomanage.</span></span>

<span data-ttu-id="5e2f7-112">Sur le panneau des détails de vérification de l’accès hello, il existe un nombre options pour la gestion de cette révision.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-112">On hello access review's detail blade there are a number options for managing that review.</span></span>

![Boutons de révision d’accès PIM - capture d’écran][1]

### <a name="remind"></a><span data-ttu-id="5e2f7-114">Rappeler</span><span class="sxs-lookup"><span data-stu-id="5e2f7-114">Remind</span></span>
<span data-ttu-id="5e2f7-115">Si une vérification de l’accès est configurée afin que les utilisateurs de hello examiner eux-mêmes, hello **rappeler** bouton envoie une notification.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-115">If an access review is set up so that hello users review themselves, hello **Remind** button sends out a notification.</span></span> 

### <a name="stop"></a><span data-ttu-id="5e2f7-116">Arrêter</span><span class="sxs-lookup"><span data-stu-id="5e2f7-116">Stop</span></span>
<span data-ttu-id="5e2f7-117">Toutes les révisions d’accès ont une date de fin, mais vous pouvez utiliser hello **arrêter** bouton toofinish il tôt.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-117">All access reviews have an end date, but you can use hello **Stop** button toofinish it early.</span></span> <span data-ttu-id="5e2f7-118">Tous les utilisateurs n’ont pas été vérifiées à ce stade, ils ne sont pas en mesure de tooafter vous arrêtez la révision de hello.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-118">If any users haven't been reviewed by this time, they won't be able tooafter you stop hello review.</span></span> <span data-ttu-id="5e2f7-119">Vous ne pouvez pas redémarrer une révision arrêtée.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-119">You cannot restart a review after it's been stopped.</span></span>

### <a name="apply"></a><span data-ttu-id="5e2f7-120">Appliquer</span><span class="sxs-lookup"><span data-stu-id="5e2f7-120">Apply</span></span>
<span data-ttu-id="5e2f7-121">Au terme d’une vérification de l’accès, soit parce que vous atteint la date de fin hello ou s’est arrêté manuellement, hello **appliquer** bouton implémente résultat hello de revue de hello.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-121">After an access review is completed, either because you reached hello end date or stopped it manually, hello **Apply** button implements hello outcome of hello review.</span></span> <span data-ttu-id="5e2f7-122">Si accès un utilisateur l’a été refusé dans la révision de hello, il s’agit d’étape hello qui va supprimer leur attribution de rôle.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-122">If a user's access was denied in hello review, this is hello step that will remove their role assignment.</span></span>  

### <a name="export"></a><span data-ttu-id="5e2f7-123">Exportation</span><span class="sxs-lookup"><span data-stu-id="5e2f7-123">Export</span></span>
<span data-ttu-id="5e2f7-124">Si vous souhaitez les résultats de hello tooapply de révision de sécurité hello manuellement, vous pouvez exporter la révision de hello.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-124">If you want tooapply hello results of hello security review manually, you can export hello review.</span></span> <span data-ttu-id="5e2f7-125">Hello **exporter** bouton démarre le téléchargement d’un fichier CSV.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-125">hello **Export** button will start downloading a CSV file.</span></span> <span data-ttu-id="5e2f7-126">Vous pouvez gérer les résultats de hello dans Excel ou d’autres programmes qui s’ouvrent les fichiers CSV.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-126">You can manage hello results in Excel or other programs that open CSV files.</span></span>

### <a name="delete"></a><span data-ttu-id="5e2f7-127">Supprimer</span><span class="sxs-lookup"><span data-stu-id="5e2f7-127">Delete</span></span>
<span data-ttu-id="5e2f7-128">Si vous n’êtes pas intéressé par hello examiner les autres, supprimez-le.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-128">If you are not interested in hello review any further, delete it.</span></span> <span data-ttu-id="5e2f7-129">Hello **supprimer** bouton supprime hello révision hello application PIM.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-129">hello **Delete** button removes hello review from hello PIM application.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5e2f7-130">Pas obtenir un avertissement avant que la suppression se produit, vous devez donc vous assurer que vous souhaitez toodelete passez en revue.</span><span class="sxs-lookup"><span data-stu-id="5e2f7-130">You will not get a warning before deletion occurs, so be sure that you want toodelete that review.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5e2f7-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5e2f7-131">Next steps</span></span>
[!INCLUDE [active-directory-privileged-identity-management-toc](../../includes/active-directory-privileged-identity-management-toc.md)]

<!--Image references-->

[1]: ./media/active-directory-privileged-identity-management-how-to-complete-review/PIM_review_buttons.png
