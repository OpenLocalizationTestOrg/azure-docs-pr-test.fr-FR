---
title: Notifications de rapports Azure Active Directory
description: Comment utiliser les notifications de rapports Azure Active Directory pour signaler les connexions suspectes.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: f4632bd2af802b10c8c64972e8c605d7ad7c0eaf
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="004ff-103">Notifications de rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="004ff-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="004ff-104">Quels rapports génèrent les notifications par courrier électronique</span><span class="sxs-lookup"><span data-stu-id="004ff-104">What reports generate email notifications</span></span>
<span data-ttu-id="004ff-105">À ce stade, seul le rapport Activité de connexion anormale déclenche des notifications par courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="004ff-105">At this time, only the Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="004ff-106">Qu'est-ce qu'une « connexion anormale » ?</span><span class="sxs-lookup"><span data-stu-id="004ff-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="004ff-107">Les connexions irrégulières sont celles qui ont été identifiées par nos algorithmes d’apprentissage automatique, sur la base d'une condition de « déplacement impossible » associée à un emplacement et un périphérique de connexion anormaux.</span><span class="sxs-lookup"><span data-stu-id="004ff-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on the basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="004ff-108">Cela peut signifier qu'un pirate a essayé de se connecter à l'aide de ce compte.</span><span class="sxs-lookup"><span data-stu-id="004ff-108">This may indicate that a hacker has been trying to sign in using this account.</span></span>

## <a name="who-receives-the-email-notifications"></a><span data-ttu-id="004ff-109">Qui reçoit les notifications par courrier électronique ?</span><span class="sxs-lookup"><span data-stu-id="004ff-109">Who receives the email notifications?</span></span>
<span data-ttu-id="004ff-110">Le courrier électronique est envoyé à tous les administrateurs généraux titulaires d'une licence Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="004ff-110">The email is sent to all global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="004ff-111">Par mesure de précaution, ce courrier électronique est également envoyé sur leur adresse de messagerie de secours.</span><span class="sxs-lookup"><span data-stu-id="004ff-111">To ensure it is delivered, we send it to the admins Alternate Email Address as well.</span></span> <span data-ttu-id="004ff-112">Les administrateurs doivent inclure aad-alerts-noreply@mail.windowsazure.com dans leur liste d'expéditeurs approuvés pour ne pas rater le courrier électronique.</span><span class="sxs-lookup"><span data-stu-id="004ff-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss the email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="004ff-113">Quelle est la fréquence d’envoi de ces courriers électroniques ?</span><span class="sxs-lookup"><span data-stu-id="004ff-113">How often are these emails sent?</span></span>
<span data-ttu-id="004ff-114">Le courrier électronique est envoyé si 10 nouvelles activités de connexion anormale se produisent au cours des 30 derniers jours, ou depuis que le dernier courrier électronique a été envoyé, selon la valeur qui est inférieure.</span><span class="sxs-lookup"><span data-stu-id="004ff-114">The email is sent if 10 new irregular sign-in activities occur in the last 30 days, or since the last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-the-report-mentioned-in-the-email"></a><span data-ttu-id="004ff-115">Comment puis-je accéder au rapport mentionné dans le courrier électronique ?</span><span class="sxs-lookup"><span data-stu-id="004ff-115">How do I access the report mentioned in the email?</span></span>
<span data-ttu-id="004ff-116">Lorsque vous cliquerez sur le lien, vous serez redirigé vers la page du rapport du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="004ff-116">When you click on the link, you will be redirected to the report page within the Azure classic portal.</span></span> <span data-ttu-id="004ff-117">Pour accéder au rapport, vous devez être à la fois :</span><span class="sxs-lookup"><span data-stu-id="004ff-117">In order to access the report, you need to be both:</span></span>

* <span data-ttu-id="004ff-118">Un administrateur ou un coadministrateur de votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="004ff-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="004ff-119">Un administrateur général du répertoire, titulaire d’une licence Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="004ff-119">A global administrator in the directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="004ff-120">Pour plus d’informations, consultez la page [Éditions d’Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="004ff-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="004ff-121">Puis-je désactiver ces courriers électroniques ?</span><span class="sxs-lookup"><span data-stu-id="004ff-121">Can I turn off these emails?</span></span>
<span data-ttu-id="004ff-122">Oui, pour désactiver les notifications liées à des connexions anormales dans le portail Azure Classic, cliquez sur **Configurer**, puis sélectionnez **Désactivé** sous la rubrique **Notifications**.</span><span class="sxs-lookup"><span data-stu-id="004ff-122">Yes, to turn off notifications related to anomalous sign-ins within the Azure classic portal, click **Configure**, and then select **Disabled** under the **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="004ff-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="004ff-123">What's next</span></span>
* <span data-ttu-id="004ff-124">Curieux de savoir quels rapports de sécurité, d'audit et d'activité sont disponibles ?</span><span class="sxs-lookup"><span data-stu-id="004ff-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="004ff-125">Découvrez [Rapports de sécurité, d'audit et d'activité d'Azure AD](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="004ff-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="004ff-126">Prise en main d’Azure Active Directory Premium (AD)</span><span class="sxs-lookup"><span data-stu-id="004ff-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="004ff-127">Ajout d’une marque de société aux pages de connexion et du volet d’accès</span><span class="sxs-lookup"><span data-stu-id="004ff-127">Add company branding to your Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

