---
title: aaaAzure Notifications de rapports Active Directory
description: "Comment toouse hello notifications de création de rapports Azure Active Directory pour l’authentification suspectes ins."
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
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a><span data-ttu-id="5b043-103">Notifications de rapports Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5b043-103">Azure Active Directory Reporting Notifications</span></span>
## <a name="what-reports-generate-email-notifications"></a><span data-ttu-id="5b043-104">Quels rapports génèrent les notifications par courrier électronique</span><span class="sxs-lookup"><span data-stu-id="5b043-104">What reports generate email notifications</span></span>
<span data-ttu-id="5b043-105">À ce stade, uniquement hello anormales dans les déclencheurs de rapport d’activité de messagerie des notifications.</span><span class="sxs-lookup"><span data-stu-id="5b043-105">At this time, only hello Irregular Sign in Activity report triggers email notifications.</span></span>

## <a name="what-is-an-irregular-sign-in"></a><span data-ttu-id="5b043-106">Qu'est-ce qu'une « connexion anormale » ?</span><span class="sxs-lookup"><span data-stu-id="5b043-106">What is an "Irregular Sign in"?</span></span>
<span data-ttu-id="5b043-107">Connexions anormales sont celles qui ont été identifiées par nos algorithmes, sur la base de hello d’une condition « voyage impossible » associée à un emplacement de connexion anormal et le dispositif d’apprentissage.</span><span class="sxs-lookup"><span data-stu-id="5b043-107">Irregular sign-ins are those that have been identified by our machine learning algorithms, on hello basis of an "impossible travel" condition combined with an anomalous sign-in location and device.</span></span> <span data-ttu-id="5b043-108">Cela peut indiquer qu’un pirate a essayé de toosign en utilisant ce compte.</span><span class="sxs-lookup"><span data-stu-id="5b043-108">This may indicate that a hacker has been trying toosign in using this account.</span></span>

## <a name="who-receives-hello-email-notifications"></a><span data-ttu-id="5b043-109">Qui reçoit des notifications par courrier électronique de hello ?</span><span class="sxs-lookup"><span data-stu-id="5b043-109">Who receives hello email notifications?</span></span>
<span data-ttu-id="5b043-110">messagerie de Hello est envoyée tooall les administrateurs généraux titulaires d’une licence Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="5b043-110">hello email is sent tooall global admins who have been assigned an Active Directory Premium license.</span></span> <span data-ttu-id="5b043-111">tooensure qu'il est remis, nous envoyer ainsi toohello administrateurs autre adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="5b043-111">tooensure it is delivered, we send it toohello admins Alternate Email Address as well.</span></span> <span data-ttu-id="5b043-112">Administrateurs doivent inclure aad-alerts-noreply@mail.windowsazure.com dans leur liste d’expéditeurs fiables pour ne pas manquer par courrier électronique hello.</span><span class="sxs-lookup"><span data-stu-id="5b043-112">Admins should include aad-alerts-noreply@mail.windowsazure.com in their safe senders list so they don’t miss hello email.</span></span>

## <a name="how-often-are-these-emails-sent"></a><span data-ttu-id="5b043-113">Quelle est la fréquence d’envoi de ces courriers électroniques ?</span><span class="sxs-lookup"><span data-stu-id="5b043-113">How often are these emails sent?</span></span>
<span data-ttu-id="5b043-114">courrier électronique de Hello est envoyé si 10 nouvelle irrégulières connectez-vous activités se produisent dans hello 30 derniers jours, ou depuis le dernier courrier électronique de hello a été envoyé, si elle est inférieure.</span><span class="sxs-lookup"><span data-stu-id="5b043-114">hello email is sent if 10 new irregular sign-in activities occur in hello last 30 days, or since hello last email was sent, whichever is less.</span></span>

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a><span data-ttu-id="5b043-115">Comment accéder aux rapports hello mentionné par courrier électronique hello ?</span><span class="sxs-lookup"><span data-stu-id="5b043-115">How do I access hello report mentioned in hello email?</span></span>
<span data-ttu-id="5b043-116">Lorsque vous cliquez sur le lien de hello, vous serez redirigé toohello page de rapport dans hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="5b043-116">When you click on hello link, you will be redirected toohello report page within hello Azure classic portal.</span></span> <span data-ttu-id="5b043-117">Dans l’ordre tooaccess hello rapport, vous devez toobe les deux :</span><span class="sxs-lookup"><span data-stu-id="5b043-117">In order tooaccess hello report, you need toobe both:</span></span>

* <span data-ttu-id="5b043-118">Un administrateur ou un coadministrateur de votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="5b043-118">An admin or co-admin of your Azure subscription</span></span>
* <span data-ttu-id="5b043-119">Un administrateur global dans le répertoire de hello et attribué une licence Active Directory Premium.</span><span class="sxs-lookup"><span data-stu-id="5b043-119">A global administrator in hello directory, and assigned an Active Directory Premium license.</span></span> <span data-ttu-id="5b043-120">Pour plus d’informations, consultez la page [Éditions d’Azure Active Directory](active-directory-editions.md).</span><span class="sxs-lookup"><span data-stu-id="5b043-120">For more information, see [Azure Active Directory editions](active-directory-editions.md).</span></span>

## <a name="can-i-turn-off-these-emails"></a><span data-ttu-id="5b043-121">Puis-je désactiver ces courriers électroniques ?</span><span class="sxs-lookup"><span data-stu-id="5b043-121">Can I turn off these emails?</span></span>
<span data-ttu-id="5b043-122">Oui, tooturn notifications liées connexions tooanomalous dans hello portail Azure classic, cliquez sur **configurer**, puis sélectionnez **désactivé** sous hello **Notifications**section.</span><span class="sxs-lookup"><span data-stu-id="5b043-122">Yes, tooturn off notifications related tooanomalous sign-ins within hello Azure classic portal, click **Configure**, and then select **Disabled** under hello **Notifications** section.</span></span>

## <a name="whats-next"></a><span data-ttu-id="5b043-123">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5b043-123">What's next</span></span>
* <span data-ttu-id="5b043-124">Curieux de savoir quels rapports de sécurité, d'audit et d'activité sont disponibles ?</span><span class="sxs-lookup"><span data-stu-id="5b043-124">Curious about what security, audit, and activity reports are available?</span></span> <span data-ttu-id="5b043-125">Découvrez [Rapports de sécurité, d'audit et d'activité d'Azure AD](active-directory-view-access-usage-reports.md)</span><span class="sxs-lookup"><span data-stu-id="5b043-125">Check out [Azure AD Security, Audit, and Activity Reports](active-directory-view-access-usage-reports.md)</span></span>
* [<span data-ttu-id="5b043-126">Prise en main d’Azure Active Directory Premium (AD)</span><span class="sxs-lookup"><span data-stu-id="5b043-126">Getting started with Azure Active Directory Premium</span></span>](active-directory-get-started-premium.md)
* [<span data-ttu-id="5b043-127">Ajouter des logos tooyour pages de connexion et du volet d’accès de la société</span><span class="sxs-lookup"><span data-stu-id="5b043-127">Add company branding tooyour Sign In and Access Panel pages</span></span>](active-directory-add-company-branding.md)

