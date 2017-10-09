---
title: "applications personnalisées aaaHow toogrant autorisations tooa | Documents Microsoft"
description: "Comment toogrant autorisations tooyour personnalisées à l’aide de l’application hello portail Azure AD ou un paramètre d’URL"
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
ms.openlocfilehash: e43a105fff60fbf912bdf4f60260f86ee289328d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogrant-permissions-tooa-custom-developed-application"></a><span data-ttu-id="f4209-103">Comment toogrant autorisations tooa personnalisées application</span><span class="sxs-lookup"><span data-stu-id="f4209-103">How toogrant permissions tooa custom-developed application</span></span>

<span data-ttu-id="f4209-104">Si vous souhaitez toogrant consentement de manière préemptive sur votre application ou que vous rencontrez une erreur que vous n’avez pas accepté tooan application, essayez les étapes suivantes ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f4209-104">If you want toogrant consent preemptively on your app or are running into an error that you have not consented tooan app, try these steps below.</span></span>

## <a name="how-tooperform-admin-consent-for-your-application"></a><span data-ttu-id="f4209-105">Comment tooperform consentement de l’administrateur de votre application</span><span class="sxs-lookup"><span data-stu-id="f4209-105">How tooperform Admin Consent for your application</span></span>

<span data-ttu-id="f4209-106">Cela influe hello d’octroi d’application toohello de consentement pour tous les utilisateurs de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="f4209-106">This has hello effect of granting consent toohello application for all users in your organization.</span></span>

1. <span data-ttu-id="f4209-107">Accédez toohello **inscriptions d’application** panneau comme un **administrateur global**, puis sélectionnez application hello.</span><span class="sxs-lookup"><span data-stu-id="f4209-107">Navigate toohello **App Registrations** blade as a **global administrator**, then select hello app.</span></span>

2. <span data-ttu-id="f4209-108">Sélectionnez **autorisations requises**et enfin cliquez sur hello **accorder des autorisations** bouton en haut de hello du panneau des hello.</span><span class="sxs-lookup"><span data-stu-id="f4209-108">Select **Required Permissions**, and finally hit hello **Grant Permissions** button at hello top of hello blade.</span></span>

<span data-ttu-id="f4209-109">Ou bien, vous pouvez construire une demande trop*login.microsoftonline.com* avec votre application des configurations et ajoutera *& invite = admin\_consentement*.</span><span class="sxs-lookup"><span data-stu-id="f4209-109">Alternatively, you can construct a request too*login.microsoftonline.com* with your app configs and append on *&prompt=admin\_consent*.</span></span> <span data-ttu-id="f4209-110">Après la connexion avec informations d’identification d’administrateur, application hello a reçu un consentement pour tous les utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="f4209-110">After signing in with admin credentials, hello app has been granted consent for all users.</span></span>

## <a name="how-tooforce-user-consent-for-your-application"></a><span data-ttu-id="f4209-111">Comment tooforce le consentement de l’utilisateur pour votre application</span><span class="sxs-lookup"><span data-stu-id="f4209-111">How tooforce User Consent for your application</span></span>

* <span data-ttu-id="f4209-112">Ajouter sur les demandes d’authentification *& invite = consentement* qui nécessitent des utilisateurs finaux tooconsent chaque fois qu’ils s’authentifient.</span><span class="sxs-lookup"><span data-stu-id="f4209-112">Append onto auth requests *&prompt=consent* which require end users tooconsent each time they authenticate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4209-113">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f4209-113">Next steps</span></span>

[<span data-ttu-id="f4209-114">Intégration des applications et consentement tooAzureAD</span><span class="sxs-lookup"><span data-stu-id="f4209-114">Consent and Integrating Apps tooAzureAD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-integrating-applications)

[<span data-ttu-id="f4209-115">Consentement et octroi d’autorisations pour les applications convergées Azure AD v2.0</span><span class="sxs-lookup"><span data-stu-id="f4209-115">Consent and Permissioning for AzureAD v2.0 converged Apps</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-v2-scopes)<br>

[<span data-ttu-id="f4209-116">AzureAD StackOverflow</span><span class="sxs-lookup"><span data-stu-id="f4209-116">AzureAD StackOverflow</span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)
