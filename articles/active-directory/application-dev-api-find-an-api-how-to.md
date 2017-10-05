---
title: "Comment rechercher une API spécifique requise pour une application personnalisée | Microsoft Docs"
description: "Comment configurer les autorisations dont vous avez besoin pour accéder à une API particulière dans l’application Azure AD que vous avez développée"
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
ms.openlocfilehash: e0c07fd030339d025894520500d2cd948d31af45
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-find-a-specific-api-needed-for-a-custom-developed-application"></a><span data-ttu-id="30e6b-103">Comment rechercher une API spécifique requise pour une application personnalisée</span><span class="sxs-lookup"><span data-stu-id="30e6b-103">How to find a specific API needed for a custom-developed application</span></span>

<span data-ttu-id="30e6b-104">L’accès aux API suppose de configurer les étendues d’accès et les rôles.</span><span class="sxs-lookup"><span data-stu-id="30e6b-104">Access to APIs require configuration of access scopes and roles.</span></span> <span data-ttu-id="30e6b-105">Si vous souhaitez exposer aux applications clientes les API web de vos applications de ressources, vous devez configurer les étendues d’accès et les rôles de l’API.</span><span class="sxs-lookup"><span data-stu-id="30e6b-105">If you want to expose your resource application web APIs to client applications, you need to configure access scopes and roles for the API.</span></span> <span data-ttu-id="30e6b-106">Si vous voulez qu’une application cliente puisse accéder à une API web, vous devez configurer les autorisations d’accès à l’API lors de l’inscription de l’application.</span><span class="sxs-lookup"><span data-stu-id="30e6b-106">If you want a client application to access a web API, you need to configure permissions to access the API in the app registration.</span></span>

## <a name="configuring-a-resource-application-to-expose-web-apis"></a><span data-ttu-id="30e6b-107">Configuration d’une application de ressource pour exposer les API web</span><span class="sxs-lookup"><span data-stu-id="30e6b-107">Configuring a resource application to expose web APIs</span></span>

<span data-ttu-id="30e6b-108">Lorsque vous exposez vos API web, l’API s’affiche dans la liste **Sélectionner une API** lorsque vous ajoutez des autorisations à l’inscription d’une application.</span><span class="sxs-lookup"><span data-stu-id="30e6b-108">When you expose your web API, the API be displayed in the **Select an API** list when adding permissions to an app registration.</span></span> <span data-ttu-id="30e6b-109">Pour ajouter des étendues d’accès, suivez les étapes décrites dans [Ajout d’étendues d’accès à votre application de ressources](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span><span class="sxs-lookup"><span data-stu-id="30e6b-109">To add access scopes, follow the steps outlined in [adding access scopes to your resource application](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#adding-access-scopes-to-your-resource-application).</span></span>

## <a name="configuring-a-client-application-to-access-web-apis"></a><span data-ttu-id="30e6b-110">Configuration d’une application cliente pour accéder aux API web</span><span class="sxs-lookup"><span data-stu-id="30e6b-110">Configuring a client application to access web APIs</span></span>

<span data-ttu-id="30e6b-111">Lorsque vous ajoutez des autorisations à l’inscription de votre application, vous pouvez **ajouter un accès à l’API** à des API web exposées.</span><span class="sxs-lookup"><span data-stu-id="30e6b-111">When you add permissions to your app registration, you can **add API access** to exposed web APIs.</span></span> <span data-ttu-id="30e6b-112">Pour accéder aux API web, suivez les étapes décrites dans la section [Pour ajouter des informations d’identification ou des autorisations pour accéder aux API web](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="30e6b-112">To access web APIs, follow the steps outlined in [add credentials or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-credentials-or-permissions-to-access-web-apis).</span></span>

## <a name="next-steps"></a><span data-ttu-id="30e6b-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="30e6b-113">Next steps</span></span>

-   [<span data-ttu-id="30e6b-114">Intégration d’applications dans Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30e6b-114">Integrating applications with Azure Active Directory</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications)

-   [<span data-ttu-id="30e6b-115">Connaître le manifeste d’application Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="30e6b-115">Understanding the Azure Active Directory application manifest</span></span>](https://docs.microsoft.com/azure/active-directory/develop/active-directory-application-manifest)


