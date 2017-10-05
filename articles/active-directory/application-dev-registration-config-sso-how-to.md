---
title: Guide pratique pour configurer une nouvelle application multilocataire | Microsoft Docs
description: "Comment configurer l’authentification unique pour une application personnalisée que vous développez et inscrivez dans Azure AD."
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
ms.openlocfilehash: 0fdc58d82d9cd2e7edac33cc5af4b98d2fd06c56
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-a-new-multi-tenant-application"></a><span data-ttu-id="503ee-103">Guide pratique pour configurer une nouvelle application multilocataire</span><span class="sxs-lookup"><span data-stu-id="503ee-103">How to configure a new multi-tenant application</span></span>

<span data-ttu-id="503ee-104">L’authentification unique (SSO) fédérée dans votre application est automatiquement activée dans le cadre d’une fédération via Azure AD pour OpenID Connect, SAML 2.0 ou WS-Fed.</span><span class="sxs-lookup"><span data-stu-id="503ee-104">Enabling federated single sign-on (SSO) in your app is automatically enabled when federating through Azure AD for OpenID Connect, SAML 2.0, or WS-Fed.</span></span> <span data-ttu-id="503ee-105">Si vos utilisateurs finaux doivent se connecter malgré une session en cours dans Azure AD, il est probable que votre application soit mal configurée.</span><span class="sxs-lookup"><span data-stu-id="503ee-105">If your end users are having to sign in despite already having an existing session with Azure AD, it’s likely your app may be misconfigured.</span></span>

* <span data-ttu-id="503ee-106">Si vous utilisez la bibliothèque ADAL/MSAL, assurez-vous que le paramètre **PromptBehavior** est défini sur **Automatique** plutôt que sur **Toujours**.</span><span class="sxs-lookup"><span data-stu-id="503ee-106">If you’re using ADAL/MSAL, make sure you have **PromptBehavior** set to **Auto** rather than **Always**.</span></span>

* <span data-ttu-id="503ee-107">Si vous créez une application mobile, vous aurez peut-être besoin de configurations supplémentaires pour activer une authentification unique avec ou sans répartiteur.</span><span class="sxs-lookup"><span data-stu-id="503ee-107">If you’re building a mobile app, you may need additional configurations to enable brokered or non-brokered SSO.</span></span>

<span data-ttu-id="503ee-108">Pour Android, consultez la page [Activation de l’authentification unique entre applications sur Android à l’aide de la bibliothèque ADAL](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span><span class="sxs-lookup"><span data-stu-id="503ee-108">For Android, see [Enabling Cross App SSO in Android](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android).</span></span><br>

<span data-ttu-id="503ee-109">Pour iOS, consultez la page [Activation d’une authentification unique entre applications sur iOS à l’aide de la bibliothèque ADAL](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span><span class="sxs-lookup"><span data-stu-id="503ee-109">For iOS, see [Enabling Cross App SSO in iOS](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios).</span></span>

## <a name="next-steps"></a><span data-ttu-id="503ee-110">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="503ee-110">Next steps</span></span>

[<span data-ttu-id="503ee-111">Qu’est-ce que l’accès aux applications et l’authentification unique avec Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="503ee-111">Azure AD SSO</span></span>](https://docs.microsoft.com/azure/active-directory/active-directory-appssoaccess-whatis)<br>

[<span data-ttu-id="503ee-112">Activation de l’authentification unique entre applications sur Android à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="503ee-112">Enabling Cross App SSO in Android</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-android)<br>

[<span data-ttu-id="503ee-113">Activation de l’authentification unique entre applications sur iOS à l’aide de la bibliothèque ADAL</span><span class="sxs-lookup"><span data-stu-id="503ee-113">Enabling Cross App SSO in iOS</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-sso-ios)<br>

[<span data-ttu-id="503ee-114">Intégration d’applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="503ee-114">Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)<br>

[<span data-ttu-id="503ee-115">Étendues, autorisations et consentement dans le point de terminaison Azure Active Directory v2.0</span><span class="sxs-lookup"><span data-stu-id="503ee-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="503ee-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="503ee-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
