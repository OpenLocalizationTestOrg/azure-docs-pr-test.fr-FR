---
title: "Octroyer des autorisations à une application personnalisée | Microsoft Docs"
description: "Comment octroyer des autorisations à votre application personnalisée à l’aide du portail Azure AD ou d’un paramètre d’URL"
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
ms.openlocfilehash: 336b945929f80e1a566f7cf71b40fd799a98c12d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-grant-permissions-to-a-custom-developed-application"></a><span data-ttu-id="d01f8-103">Octroyer des autorisations à une application personnalisée</span><span class="sxs-lookup"><span data-stu-id="d01f8-103">How to grant permissions to a custom-developed application</span></span>

<span data-ttu-id="d01f8-104">Si vous souhaitez octroyer un consentement de façon préventive sur votre application ou que vous rencontrez une erreur indiquant que vous n’avez pas donné votre consentement pour une application, essayez les étapes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="d01f8-104">If you want to grant consent preemptively on your app or are running into an error that you have not consented to an app, try these steps below.</span></span>

## <a name="how-to-perform-admin-consent-for-your-application"></a><span data-ttu-id="d01f8-105">Donner un consentement d’administrateur pour une application</span><span class="sxs-lookup"><span data-stu-id="d01f8-105">How to perform Admin Consent for your application</span></span>

<span data-ttu-id="d01f8-106">Cette opération a pour effet d’accorder un consentement à l’application pour tous les utilisateurs de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="d01f8-106">This has the effect of granting consent to the application for all users in your organization.</span></span>

1. <span data-ttu-id="d01f8-107">Accédez au panneau **Inscriptions d’applications** en tant qu’**administrateur général**, puis sélectionnez l’application.</span><span class="sxs-lookup"><span data-stu-id="d01f8-107">Navigate to the **App Registrations** blade as a **global administrator**, then select the app.</span></span>

2. <span data-ttu-id="d01f8-108">Sélectionnez **Autorisations requises** et appuyez sur le bouton **Accorder des autorisations** en haut du panneau.</span><span class="sxs-lookup"><span data-stu-id="d01f8-108">Select **Required Permissions**, and finally hit the **Grant Permissions** button at the top of the blade.</span></span>

<span data-ttu-id="d01f8-109">Vous pouvez également créer une demande que vous envoyez à *login.microsoftonline.com* avec les configurations de votre application, à laquelle vous ajoutez *&prompt=admin\_consent*.</span><span class="sxs-lookup"><span data-stu-id="d01f8-109">Alternatively, you can construct a request to *login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="d01f8-110">Une fois que la connexion a été effectuée avec les informations d’identification d’administrateur, l’application reçoit le consentement pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="d01f8-110">After signing in with admin credentials, the app has been granted consent for all users.</span></span>

## <a name="how-to-force-user-consent-for-your-application"></a><span data-ttu-id="d01f8-111">Forcer le consentement d’utilisateur pour votre application</span><span class="sxs-lookup"><span data-stu-id="d01f8-111">How to force User Consent for your application</span></span>

* <span data-ttu-id="d01f8-112">Ajoutez des demandes d’authentification *&prompt=consent* qui nécessitent que les utilisateurs finaux donnent leur consentement chaque fois qu’ils s’authentifient.</span><span class="sxs-lookup"><span data-stu-id="d01f8-112">Append onto auth requests *&prompt=consent* which require end users to consent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d01f8-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d01f8-113">Next steps</span></span>

[<span data-ttu-id="d01f8-114">Consentement et intégration d’applications pour Azure AD</span><span class="sxs-lookup"><span data-stu-id="d01f8-114">Consent and Integrating Apps to AzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="d01f8-115">Consentement et octroi d’autorisations pour les applications convergées Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="d01f8-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="d01f8-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="d01f8-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
