---
title: "Azure Active Directory B2C : désactiver la vérification par e-mail lors de l’inscription du consommateur | Microsoft Docs"
description: "Une rubrique qui montre comment désactiver la vérification par e-mail lors de l’inscription du consommateur à Azure Active Directory B2C"
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
ms.openlocfilehash: d8e44a8aade60d21734477d60bccc2bd5194436e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-b2c-disable-email-verification-during-consumer-sign-up"></a><span data-ttu-id="9dec1-103">Azure Active Directory B2C : désactiver la vérification par e-mail lors de l’inscription du consommateur</span><span class="sxs-lookup"><span data-stu-id="9dec1-103">Azure Active Directory B2C: Disable email verification during consumer sign-up</span></span>
<span data-ttu-id="9dec1-104">Lorsqu'il est activé, Azure Active Directory (Azure AD) B2C permet à un consommateur de s’inscrire à des applications en fournissant une adresse e-mail et en créant un compte local.</span><span class="sxs-lookup"><span data-stu-id="9dec1-104">When enabled, Azure Active Directory (Azure AD) B2C gives a consumer the ability to sign up for applications by providing an email address and creating a local account.</span></span> <span data-ttu-id="9dec1-105">Azure Active Directory B2C assure la validité des adresses e-mail en demandant aux consommateurs de les vérifier pendant le processus d’inscription.</span><span class="sxs-lookup"><span data-stu-id="9dec1-105">Azure AD B2C ensures valid email addresses by requiring consumers to verify them during the sign-up process.</span></span> <span data-ttu-id="9dec1-106">Cela empêche un processus malveillant automatisé de générer des faux comptes pour les applications.</span><span class="sxs-lookup"><span data-stu-id="9dec1-106">It also prevents a malicious automated process from generating fake accounts for the applications.</span></span>

<span data-ttu-id="9dec1-107">Certains développeurs d’applications préfèrent ignorer la vérification par e-mail pendant le processus d’inscription et demander aux consommateurs de vérifier l’adresse e-mail ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="9dec1-107">Some application developers prefer to skip email verification during the sign-up process and instead have consumers verify the email address later.</span></span> <span data-ttu-id="9dec1-108">Pour ce faire, Azure Active Directory B2C peut être configuré afin de désactiver la vérification par e-mail.</span><span class="sxs-lookup"><span data-stu-id="9dec1-108">To support this, Azure AD B2C can be configured to disable email verification.</span></span> <span data-ttu-id="9dec1-109">Cette opération crée un processus de connexion plus simple et offre aux développeurs la possibilité de différencier les consommateurs qui ont vérifié leur e-mail de ceux qui ne l'ont pas encore fait.</span><span class="sxs-lookup"><span data-stu-id="9dec1-109">Doing so creates a smoother sign-up process and gives developers the flexibility to differentiate the consumers that have verified their email address from those consumers that have not.</span></span>

<span data-ttu-id="9dec1-110">Par défaut, la vérification est activée pour les stratégies d’inscription.</span><span class="sxs-lookup"><span data-stu-id="9dec1-110">By default, sign-up policies have email verification turned on.</span></span> <span data-ttu-id="9dec1-111">Pour la désactiver, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9dec1-111">Use the following steps to turn it off:</span></span>

1. <span data-ttu-id="9dec1-112">[Suivez ces étapes pour accéder au panneau de fonctionnalités B2C sur le portail Azure](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span><span class="sxs-lookup"><span data-stu-id="9dec1-112">[Follow these steps to navigate to the B2C features blade on the Azure portal](active-directory-b2c-app-registration.md#navigate-to-b2c-settings).</span></span>
2. <span data-ttu-id="9dec1-113">Cliquez sur les **stratégies d’inscription** ou les **stratégies d’inscription ou de connexion** selon la configuration de l'inscription.</span><span class="sxs-lookup"><span data-stu-id="9dec1-113">Click **Sign-up policies** or **Sign-up or sign-in policies** depending on what you configured for sign-up.</span></span>
3. <span data-ttu-id="9dec1-114">Ouvrez votre inscription (par exemple, « B2C_1_SiUp ») en cliquant dessus.</span><span class="sxs-lookup"><span data-stu-id="9dec1-114">Click your policy (for example, "B2C_1_SiUp") to open it.</span></span> <span data-ttu-id="9dec1-115">Cliquez sur **Modifier** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="9dec1-115">Click **Edit** at the top of the blade.</span></span>
4. <span data-ttu-id="9dec1-116">Cliquez sur la fonctionnalité de **personnalisation de l’interface utilisateur de page**.</span><span class="sxs-lookup"><span data-stu-id="9dec1-116">Click **Page UI Customization**.</span></span>
5. <span data-ttu-id="9dec1-117">Cliquez sur **page d’inscription à un compte Local**.</span><span class="sxs-lookup"><span data-stu-id="9dec1-117">Click **Local account sign-up page**.</span></span>
6. <span data-ttu-id="9dec1-118">Cliquez sur **Adresse e-mail** dans la colonne **Nom** colonne sous la section des **attributs d’abonnement**.</span><span class="sxs-lookup"><span data-stu-id="9dec1-118">Click **Email Address** in the **Name** column under the **Sign-up attributes** section.</span></span>
7. <span data-ttu-id="9dec1-119">Définissez l’option **Exiger la vérification** sur **non**.</span><span class="sxs-lookup"><span data-stu-id="9dec1-119">Toggle the **Require verification** option to **No**.</span></span>
8. <span data-ttu-id="9dec1-120">Cliquez sur **OK** en bas jusqu'à atteindre le panneau **Modifier une stratégie**.</span><span class="sxs-lookup"><span data-stu-id="9dec1-120">Click **OK** at the bottom until you reach the **Edit policy** blade.</span></span>
9. <span data-ttu-id="9dec1-121">Cliquez sur **Enregistrer** dans la partie supérieure du panneau.</span><span class="sxs-lookup"><span data-stu-id="9dec1-121">Click **Save** at the top of the blade.</span></span> <span data-ttu-id="9dec1-122">Vous avez terminé !</span><span class="sxs-lookup"><span data-stu-id="9dec1-122">You're done!</span></span>

> [!NOTE]
> <span data-ttu-id="9dec1-123">La désactivation de la vérification par e-mail dans le processus d’inscription peut entraîner la réception de courrier indésirable.</span><span class="sxs-lookup"><span data-stu-id="9dec1-123">Disabling email verification in the sign-up process may lead to spam.</span></span> <span data-ttu-id="9dec1-124">Si vous désactivez la vérification par défaut, nous vous recommandons d’ajouter votre propre système de vérification.</span><span class="sxs-lookup"><span data-stu-id="9dec1-124">If you disable the default one, we recommend adding your own verification system.</span></span>
> 
> 

<span data-ttu-id="9dec1-125">Nous sommes ouverts aux commentaires et suggestions !</span><span class="sxs-lookup"><span data-stu-id="9dec1-125">We are always open to feedback and suggestions!</span></span> <span data-ttu-id="9dec1-126">Si vous avez des difficultés avec cette rubrique, ou si vous avez des conseils pour améliorer ce contenu, faites-nous part de vos commentaires en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="9dec1-126">If you have any difficulties with this topic, or have recommendations for improving this content, we would appreciate your feedback at the bottom of the page.</span></span> <span data-ttu-id="9dec1-127">En cas de demandes liées aux fonctionnalités, utilisez [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span><span class="sxs-lookup"><span data-stu-id="9dec1-127">For feature requests, add them to [UserVoice](https://feedback.azure.com/forums/169401-azure-active-directory/category/160596-b2c).</span></span>