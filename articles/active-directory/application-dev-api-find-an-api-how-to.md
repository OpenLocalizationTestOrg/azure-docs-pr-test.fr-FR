---
title: "aaaHow toofind une API spécifique est nécessaire pour une application personnalisée | Documents Microsoft"
description: "Comment tooconfigure hello autorisations tooaccess une API particulière dans votre développement application Azure AD"
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
ms.openlocfilehash: 7331129204d8b34b4ef9671749bd702f893768ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toofind-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="50780-103">Comment toofind une API spécifique est nécessaire pour une application personnalisée</span><span class="sxs-lookup"><span data-stu-id="50780-103">How toofind a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="50780-104">Accès tooAPIs nécessite la configuration des étendues d’accès et des rôles.</span><span class="sxs-lookup"><span data-stu-id="50780-104">Access tooAPIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="50780-105">Si vous souhaitez tooexpose vos ressources d’applications web API tooclient applications, vous devez tooconfigure accès étendues et des rôles pour hello API.</span><span class="sxs-lookup"><span data-stu-id="50780-105">If you want tooexpose your resource application web APIs tooclient applications, you need tooconfigure access scopes and roles for hello API.</span></span> <span data-ttu-id="50780-106">Si vous souhaitez un tooaccess d’application client une API web, vous devez tooconfigure autorisations tooaccess hello API dans l’inscription d’une application hello.</span><span class="sxs-lookup"><span data-stu-id="50780-106">If you want a client application tooaccess a web API, you need tooconfigure permissions tooaccess hello API in hello app registration.</span></span>

## <a name="configuring-a-resource-application-tooexpose-web-apis"></a><span data-ttu-id="50780-107">Configuration d’un site web tooexpose d’application de ressource API</span><span class="sxs-lookup"><span data-stu-id="50780-107">Configuring a resource application tooexpose web APIs</span></span>

<span data-ttu-id="50780-108">Lorsque vous exposez votre API web, hello API affichera Bonjour **sélectionner une API** liste lors de l’ajout d’inscription d’une application tooan autorisations.</span><span class="sxs-lookup"><span data-stu-id="50780-108">When you expose your web API, hello API be displayed in hello **Select an API** list when adding permissions tooan app registration.</span></span> <span data-ttu-id="50780-109">étendues d’accès tooadd, suivez les instructions de hello dans [Ajout d’accès étendues application de ressource tooyour](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="50780-109">tooadd access scopes, follow hello steps outlined in [adding access scopes tooyour resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-tooaccess-web-apis"></a><span data-ttu-id="50780-110">Configuration d’un ordinateur client application tooaccess web API</span><span class="sxs-lookup"><span data-stu-id="50780-110">Configuring a client application tooaccess web APIs</span></span>

<span data-ttu-id="50780-111">Lorsque vous ajoutez d’inscription d’une application tooyour autorisations, vous pouvez **ajouter l’accès aux API** tooexposed web API.</span><span class="sxs-lookup"><span data-stu-id="50780-111">When you add permissions tooyour app registration, you can **add API access** tooexposed web APIs.</span></span> <span data-ttu-id="50780-112">tooaccess API web, suivez les étapes de hello décrites dans [ajoutez tooaccess des informations d’identification ou des autorisations web API](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="50780-112">tooaccess web APIs, follow hello steps outlined in [add credentials or permissions tooaccess web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="50780-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="50780-113">Next steps</span></span>

-   [<span data-ttu-id="50780-114">Intégration d’applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50780-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="50780-115">Présentation de manifeste de l’application hello Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="50780-115">Understanding hello Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


