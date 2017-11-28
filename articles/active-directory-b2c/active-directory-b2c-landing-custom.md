---
title: "Azure Active Directory B2C : Page d’accueil des stratégies personnalisées | Microsoft Docs"
description: "Développement d’applications accessibles aux consommateurs avec Azure Active DirectoryB2C à l’aide de stratégies personnalisées"
services: active-directory-b2c
documentationcenter: 
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f2079f53-a637-4f2d-b3a0-61a9647ad433
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 5/06/2017
ms.author: parakhj
ms.openlocfilehash: 28a39f282488b81fc9e2ab7841b5f2cb4cd58715
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-b2c-sign-up-and-sign-in-consumers-in-your-applications-using-custom-policies"></a><span data-ttu-id="f41c6-103">Azure Active Directory B2C : Inscription et connexion de consommateurs à vos applications avec des stratégies personnalisées</span><span class="sxs-lookup"><span data-stu-id="f41c6-103">Azure Active Directory B2C: Sign up and sign in consumers in your applications using custom policies</span></span>
<span data-ttu-id="f41c6-104">Les stratégies personnalisées sont des fichiers de configuration qui définissent le comportement de hello de votre locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f41c6-104">Custom policies are configuration files that define hello behavior of your Azure AD B2C tenant.</span></span> <span data-ttu-id="f41c6-105">Ils peuvent être entièrement modifié par un toocomplete de développeur d’identité un nombre illimité de proche de tâches.</span><span class="sxs-lookup"><span data-stu-id="f41c6-105">They can be fully edited by an identity developer toocomplete a near unlimited number of tasks.</span></span>

## <a name="how-tooarticles"></a><span data-ttu-id="f41c6-106">Tooarticles de procédure</span><span class="sxs-lookup"><span data-stu-id="f41c6-106">How-tooarticles</span></span>
<span data-ttu-id="f41c6-107">Découvrez comment les fonctionnalités Azure Active Directory B2C spécifiques toouse :</span><span class="sxs-lookup"><span data-stu-id="f41c6-107">Learn how toouse specific Azure Active Directory B2C features:</span></span>

* [<span data-ttu-id="f41c6-108">Prise en main</span><span class="sxs-lookup"><span data-stu-id="f41c6-108">Get Started</span></span>](active-directory-b2c-overview-custom.md)
* <span data-ttu-id="f41c6-109">Configurer les fournisseurs OIDC comme [Azure AD](active-directory-b2c-setup-aad-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f41c6-109">Configure OIDC Providers such as [Azure AD](active-directory-b2c-setup-aad-custom.md).</span></span>
* <span data-ttu-id="f41c6-110">Configurer les fournisseurs SAML comme [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f41c6-110">Configure SAML Providers such as [Salesforce](active-directory-b2c-setup-sf-app-custom.md).</span></span>
* <span data-ttu-id="f41c6-111">Intégration des API RESTful</span><span class="sxs-lookup"><span data-stu-id="f41c6-111">Integrate RESTful APIs:</span></span>
    * <span data-ttu-id="f41c6-112">[Obtenir des revendications supplémentaires](active-directory-b2c-rest-api-step-custom.md)</span><span class="sxs-lookup"><span data-stu-id="f41c6-112">[Obtain additional claims](active-directory-b2c-rest-api-step-custom.md).</span></span>
    * <span data-ttu-id="f41c6-113">[Valider les entrées utilisateur](active-directory-b2c-rest-api-validation-custom.md)</span><span class="sxs-lookup"><span data-stu-id="f41c6-113">[Validate user input](active-directory-b2c-rest-api-validation-custom.md).</span></span>
* <span data-ttu-id="f41c6-114">Personnaliser la connexion :</span><span class="sxs-lookup"><span data-stu-id="f41c6-114">Customize Login:</span></span>
    * [<span data-ttu-id="f41c6-115">Configurer des entrées d’utilisateur</span><span class="sxs-lookup"><span data-stu-id="f41c6-115">Configure User Input</span></span>](active-directory-b2c-configure-signup-self-asserted-custom.md)
    * [<span data-ttu-id="f41c6-116">Personnaliser l’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="f41c6-116">Customize UI</span></span>](active-directory-b2c-ui-customization-custom.md)
    * [<span data-ttu-id="f41c6-117">Personnaliser le jeton</span><span class="sxs-lookup"><span data-stu-id="f41c6-117">Customize Token</span></span>](active-directory-b2c-reference-manage-sso-and-token-configuration.md)
* <span data-ttu-id="f41c6-118">Résoudre les problèmes en [collectant les journaux à l’aide d’Application Insights](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="f41c6-118">Troubleshoot by [collecting logs using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="whats-new"></a><span data-ttu-id="f41c6-119">Nouveautés</span><span class="sxs-lookup"><span data-stu-id="f41c6-119">What's new</span></span>
<span data-ttu-id="f41c6-120">Revenez souvent toolearn sur les futures modifications toohello Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="f41c6-120">Check back here often toolearn about future changes toohello Azure Active Directory B2C.</span></span> <span data-ttu-id="f41c6-121">Nous communiquerons également les mises à jour sur Tweeter via @AzureAD.</span><span class="sxs-lookup"><span data-stu-id="f41c6-121">We'll also tweet about any updates by using @AzureAD.</span></span>



