---
title: "Azure Active Directory B2C : désactiver la vérification par e-mail lors de l’inscription du consommateur | Microsoft Docs"
description: "Une rubrique illustrant comment toodisable envoyer par courrier électronique vérification au cours du consommateur d’inscription dans Azure Active Directory B2C"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: 433f32b8-96d2-4113-aa82-efcf42fa9827
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/06/2017
ms.author: parakhj
ms.openlocfilehash: a8a42eddcb577725f04d70e1b1ebbebf10b5937c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="4d11a-103">Azure Active Directory B2C : désactiver la vérification par e-mail lors de l’inscription du consommateur</span><span class="sxs-lookup"><span data-stu-id="4d11a-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="4d11a-104">Lorsque activé, permet d’Azure Active Directory (Azure AD) B2C un consommateur hello toosign de capacité pour les applications en fournissant une adresse de messagerie et de création d’un compte local.</span><span class="sxs-lookup"><span data-stu-id="4d11a-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer hello ability toosign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="4d11a-105">Azure AD B2C garantit des adresses de messagerie valides en exigeant que les consommateurs tooverify leur pendant le processus d’inscription hello.</span><span class="sxs-lookup"><span data-stu-id="4d11a-105">Azure AD B2C ensures valid email addresses by requiring consumers tooverify them during hello sign-up process.</span></span> <span data-ttu-id="4d11a-106">Elle évite également d’un processus automatisé malveillant à partir de la génération des comptes factices pour les applications de hello.</span><span class="sxs-lookup"><span data-stu-id="4d11a-106">It also prevents a malicious automated process from generating fake accounts for hello applications.</span></span>

<span data-ttu-id="4d11a-107">Certains développeurs d’applications préfèrent la vérification du courrier électronique tooskip pendant le processus d’inscription hello et ont à la place des consommateurs vérifier adresse de messagerie hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="4d11a-107">Some application developers prefer tooskip email verification during hello sign-up process and instead have consumers verify hello email address later.</span></span> <span data-ttu-id="4d11a-108">toosupport cela, Azure AD B2C peut être la vérification du courrier électronique toodisable configuré.</span><span class="sxs-lookup"><span data-stu-id="4d11a-108">toosupport this, Azure AD B2C can be configured toodisable email verification.</span></span> <span data-ttu-id="4d11a-109">Cela crée un processus de connexion plus lisse et offre aux développeurs hello flexibilité toodifferentiate hello consommateurs qui ont vérifié leur adresse de messagerie à partir de ces consommateurs qui n’ont pas.</span><span class="sxs-lookup"><span data-stu-id="4d11a-109">Doing so creates a smoother sign-up process and gives developers hello flexibility toodifferentiate hello consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="4d11a-110">Par défaut, la vérification est activée pour les stratégies d’inscription.</span><span class="sxs-lookup"><span data-stu-id="4d11a-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="4d11a-111">Utilisez hello suivant les étapes tooturn désactivé :</span><span class="sxs-lookup"><span data-stu-id="4d11a-111">Use hello following steps tooturn it off:</span></span>

1. <span data-ttu-id="4d11a-112">[Suivez ces Panneau de fonctionnalités étapes toonavigate toohello B2C hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="4d11a-112">[Follow these steps toonavigate toohello B2C features blade on hello Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="4d11a-113">Cliquez sur les **stratégies d’inscription** ou les **stratégies d’inscription ou de connexion** selon la configuration de l'inscription.</span><span class="sxs-lookup"><span data-stu-id="4d11a-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="4d11a-114">Cliquez sur votre tooopen stratégie (par exemple, « B2C_1_SiUp ») il.</span><span class="sxs-lookup"><span data-stu-id="4d11a-114">Click your policy (for example, "B2C_1_SiUp") tooopen it.</span></span> <span data-ttu-id="4d11a-115">Cliquez sur **modifier** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="4d11a-115">Click **Edit** at hello top of hello blade.</span></span>
4. <span data-ttu-id="4d11a-116">Cliquez sur la fonctionnalité de **personnalisation de l’interface utilisateur de page**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="4d11a-117">Cliquez sur **page d’inscription à un compte Local**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="4d11a-118">Cliquez sur **adresse de messagerie** Bonjour **nom** colonne sous hello **des attributs d’abonnement** section.</span><span class="sxs-lookup"><span data-stu-id="4d11a-118">Click **Email Address** in hello **Name** column under hello **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="4d11a-119">Hello de bascule **exiger la vérification** option trop**non**.</span><span class="sxs-lookup"><span data-stu-id="4d11a-119">Toggle hello **Require verification** option too**No**.</span></span>
8. <span data-ttu-id="4d11a-120">Cliquez sur **OK** bas hello jusqu'à ce que vous atteigniez hello **modifier la stratégie** panneau.</span><span class="sxs-lookup"><span data-stu-id="4d11a-120">Click **OK** at hello bottom until you reach hello **Edit policy** blade.</span></span>
9. <span data-ttu-id="4d11a-121">Cliquez sur **enregistrer** haut hello du Panneau de hello.</span><span class="sxs-lookup"><span data-stu-id="4d11a-121">Click **Save** at hello top of hello blade.</span></span> <span data-ttu-id="4d11a-122">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="4d11a-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="4d11a-123">La désactivation de vérification de courrier électronique dans le processus d’inscription hello peut entraîner un toospam.</span><span class="sxs-lookup"><span data-stu-id="4d11a-123">Disabling email verification in hello sign-up process may lead toospam.</span></span> <span data-ttu-id="4d11a-124">Si vous désactivez hello par défaut, nous vous recommandons d’ajouter votre propre système de vérification.</span><span class="sxs-lookup"><span data-stu-id="4d11a-124">If you disable hello default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="4d11a-125">Nous sommes toujours ouvrir toofeedback ainsi que des suggestions !</span><span class="sxs-lookup"><span data-stu-id="4d11a-125">We are always open toofeedback and suggestions!</span></span> <span data-ttu-id="4d11a-126">Si vous rencontrez des difficultés avec cette rubrique, ou que vous avez des recommandations pour améliorer ce contenu, nous aimerions connaître votre opinion bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="4d11a-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at hello bottom of hello page.</span></span> <span data-ttu-id="4d11a-127">Pour les demandes de fonctionnalités, ajoutez-les trop[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="4d11a-127">For feature requests, add them too[UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>
