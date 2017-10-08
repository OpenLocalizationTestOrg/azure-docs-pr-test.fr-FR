---
title: "aaaHow tooconfigure une application mutualisée | Documents Microsoft"
description: "Comment tooconfigure l’authentification unique pour une application personnalisée vous développez et l’inscription auprès d’Azure AD."
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 4d3499d8885933516d6597fa9f87bcf88cd5a428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-a-new-multi-tenant-application"></a><span data-ttu-id="4f048-103">Comment tooconfigure une application mutualisée</span><span class="sxs-lookup"><span data-stu-id="4f048-103">How tooconfigure a new multi-tenant application</span></span>

<span data-ttu-id="4f048-104">L’authentification unique (SSO) fédérée dans votre application est automatiquement activée dans le cadre d’une fédération via Azure AD pour OpenID Connect, SAML 2.0 ou WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="4f048-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="4f048-105">Si vos utilisateurs finaux rencontrent toosign en dépit de déjà une session existante avec Azure AD, il est probable que votre application peut être mal configurée.</span><span class="sxs-lookup"><span data-stu-id="4f048-105">If your end users are having toosign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="4f048-106">Si vous utilisez la bibliothèque ADAL/MSAL, assurez-vous que vous disposez **PromptBehavior** défini trop**automatique** plutôt que **toujours**.</span><span class="sxs-lookup"><span data-stu-id="4f048-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set too**Auto** rather than **Always**.</span></span>

* <span data-ttu-id="4f048-107">Si vous générez une application mobile, vous devrez peut-être tooenable répartie ou SSO non répartie des configurations supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="4f048-107">If you’re building a mobile app, you may need additional configurations tooenable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="4f048-108">Pour Android, consultez la page [Activation de l’authentification unique entre applications sur Android à l’aide de la bibliothèque ADAL](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="4f048-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="4f048-109">Pour iOS, consultez la page [Activation d’une authentification unique entre applications sur iOS à l’aide de la bibliothèque ADAL](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="4f048-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f048-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4f048-110">Next steps</span></span>

[<span data-ttu-id="4f048-111">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="4f048-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="4f048-112">Activation de l’authentification unique entre applications sur Android à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="4f048-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="4f048-113">Activation de l’authentification unique entre applications sur iOS à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="4f048-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="4f048-114">Intégration d’applications tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="4f048-114">Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="4f048-115">Consentement et octroi d’autorisations pour les applications convergées Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="4f048-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="4f048-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="4f048-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
