---
title: point de terminaison aaaAzure Active Directory v2.0 | Documents Microsoft
description: "Une présentation toobuilding des applications avec Microsoft Account et Azure Active Directory connectez-vous."
services: active-directory
documentationcenter: 
author: dstrockis
manager: mbaldwin
editor: 
ms.assetid: 2dee579f-fdf6-474b-bc2c-016c931eaa27
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ae5946b02c50ae5a6137dc1decae66c96647e875
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sign-in-microsoft-account--azure-ad-users-in-a-single-app"></a><span data-ttu-id="e0f63-103">Connecter les utilisateurs de compte Microsoft et d’Azure AD dans une même application</span><span class="sxs-lookup"><span data-stu-id="e0f63-103">Sign-in Microsoft Account & Azure AD users in a single app</span></span>
<span data-ttu-id="e0f63-104">Bonjour passé, un développeur d’application qui voulaient toosupport les deux comptes personnels de Microsoft et des comptes à partir d’Azure Active Directory a été toointegrate requise avec deux systèmes distincts.</span><span class="sxs-lookup"><span data-stu-id="e0f63-104">In hello past, an app developer who wanted toosupport both personal Microsoft accounts and work accounts from Azure Active Directory was required toointegrate with two separate systems.</span></span>  <span data-ttu-id="e0f63-105">Hello **point de terminaison Azure AD v2.0** introduit une nouvelle version d’API d’authentification qui vous permet de toosign dans les deux types de comptes à l’aide d’une intégration simple.</span><span class="sxs-lookup"><span data-stu-id="e0f63-105">hello **Azure AD v2.0 endpoint** introduces a new authentication API version that enables you toosign in both types of accounts using one simple integration.</span></span>  <span data-ttu-id="e0f63-106">Applications qui utilisent le point de terminaison hello v2.0 peuvent également consommer API REST hello [Microsoft Graph](https://graph.microsoft.io) à l’aide d’un type de compte.</span><span class="sxs-lookup"><span data-stu-id="e0f63-106">Apps that use hello v2.0 endpoint can also consume REST APIs from hello [Microsoft Graph](https://graph.microsoft.io) using either type of account.</span></span>

## <a name="getting-started"></a><span data-ttu-id="e0f63-107">Mise en route</span><span class="sxs-lookup"><span data-stu-id="e0f63-107">Getting Started</span></span>
<span data-ttu-id="e0f63-108">Choisissez votre plateforme favoris hello suivant liste toobuild une application à l’aide de notre bibliothèques open source et les infrastructures.</span><span class="sxs-lookup"><span data-stu-id="e0f63-108">Choose your favorite platform from hello following list toobuild an app using our open source libraries & frameworks.</span></span>  <span data-ttu-id="e0f63-109">Vous pouvez également utiliser notre toosend de documentation de protocole OAuth 2.0 et OpenID Connect et recevoir des messages de protocole directement sans l’aide d’une bibliothèque d’authentification.</span><span class="sxs-lookup"><span data-stu-id="e0f63-109">Alternatively, you can use our OAuth 2.0 & OpenID Connect protocol documentation toosend & receive protocol messages directly without using an auth library.</span></span>

<br />

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

## <a name="whats-new"></a><span data-ttu-id="e0f63-110">Nouveautés</span><span class="sxs-lookup"><span data-stu-id="e0f63-110">What's New</span></span>
<span data-ttu-id="e0f63-111">informations Hello ici seront utiles pour comprendre ce qui est et ce qui n’est pas possible avec le point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="e0f63-111">hello information here will be useful in understanding what is & what isn't possible with hello v2.0 endpoint.</span></span>

* <span data-ttu-id="e0f63-112">En savoir plus sur hello [types d’applications que vous pouvez générer avec le point de terminaison hello v2.0](active-directory-v2-flows.md).</span><span class="sxs-lookup"><span data-stu-id="e0f63-112">Learn about hello [types of apps you can build with hello v2.0 endpoint](active-directory-v2-flows.md).</span></span>
* <span data-ttu-id="e0f63-113">Comprendre hello [limitations, les restrictions et les contraintes](active-directory-v2-limitations.md) avec point de terminaison hello v2.0.</span><span class="sxs-lookup"><span data-stu-id="e0f63-113">Understand hello [limitations, restrictions, and constraints](active-directory-v2-limitations.md) with hello v2.0 endpoint.</span></span>
* <span data-ttu-id="e0f63-114">Consultez cette présentation vidéo de point de terminaison hello v2.0 :</span><span class="sxs-lookup"><span data-stu-id="e0f63-114">Check out this overview video for hello v2.0 endpoint:</span></span>

>[!VIDEO https://channel9.msdn.com/Events/Build/2017/P4031/player]

## <a name="reference"></a><span data-ttu-id="e0f63-115">Référence</span><span class="sxs-lookup"><span data-stu-id="e0f63-115">Reference</span></span>
<span data-ttu-id="e0f63-116">Ces liens peuvent être utiles pour l’exploration de plateforme hello en profondeur :</span><span class="sxs-lookup"><span data-stu-id="e0f63-116">These links will be useful for exploring hello platform in depth:</span></span>

* [<span data-ttu-id="e0f63-117">Référence sur le protocole v2.0</span><span class="sxs-lookup"><span data-stu-id="e0f63-117">v2.0 Protocol Reference</span></span>](active-directory-v2-protocols.md)
* [<span data-ttu-id="e0f63-118">Référence sur le jeton v2.0</span><span class="sxs-lookup"><span data-stu-id="e0f63-118">v2.0 Token Reference</span></span>](active-directory-v2-tokens.md)
* [<span data-ttu-id="e0f63-119">Référence de la bibliothèque v2.0</span><span class="sxs-lookup"><span data-stu-id="e0f63-119">v2.0 Library Reference</span></span>](active-directory-v2-libraries.md)
* [<span data-ttu-id="e0f63-120">Étendues et consentement dans le point de terminaison hello v2.0</span><span class="sxs-lookup"><span data-stu-id="e0f63-120">Scopes and Consent in hello v2.0 endpoint</span></span>](active-directory-v2-scopes.md)
* [<span data-ttu-id="e0f63-121">Hello Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="e0f63-121">hello Microsoft Graph</span></span>](https://graph.microsoft.io)

## <a name="help--support"></a><span data-ttu-id="e0f63-122">Aide et support</span><span class="sxs-lookup"><span data-stu-id="e0f63-122">Help & Support</span></span>
<span data-ttu-id="e0f63-123">Il s’agit hello meilleurs emplacements tooget aide avec le développement sur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="e0f63-123">These are hello best places tooget help with developing on Azure Active Directory.</span></span>

* [<span data-ttu-id="e0f63-124">Balises `azure-active-directory` et `adal` de Stack Overflow</span><span class="sxs-lookup"><span data-stu-id="e0f63-124">Stack Overflow's `azure-active-directory` and `adal` tags</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory+or+adal)
* [<span data-ttu-id="e0f63-125">Commentaires sur Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e0f63-125">Feedback on Azure Active Directory</span></span>](https://feedback.azure.com/forums/169401-azure-active-directory/category/164757-developer-experiences)


> [!NOTE]
> <span data-ttu-id="e0f63-126">Si vous devez uniquement toosign dans des comptes professionnels et scolaires à partir d’Azure Active Directory, vous devez commencer par notre [guide du développeur Azure AD](active-directory-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="e0f63-126">If you only need toosign in work and school accounts from Azure Active Directory, you should start with our [Azure AD developer's guide](active-directory-developers-guide.md).</span></span>  <span data-ttu-id="e0f63-127">point de terminaison Hello v2.0 est destiné à être utilisé par les développeurs qui doivent explicitement toosign dans des comptes personnels Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e0f63-127">hello v2.0 endpoint is intended for use by developers who explicitly need toosign in Microsoft personal accounts.</span></span>

