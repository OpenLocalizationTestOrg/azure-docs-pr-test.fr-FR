---
title: "Azure Active Directory B2C : création d’un client Azure Active Directory B2C | Microsoft Docs"
description: Une rubrique sur comment toocreate un Active Directory B2C du Azure locataire
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: patricka
ms.assetid: eec4d418-453f-4755-8b30-5ed997841b56
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.topic: article
ms.devlang: na
ms.date: 06/07/2017
ms.author: swkrish
ms.openlocfilehash: e8b257d66c1f66ffb84f5d3d21b30b42eddcbac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-hello-azure-portal"></a><span data-ttu-id="7443d-103">Créer un locataire Azure Active Directory B2C Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="7443d-103">Create an Azure Active Directory B2C tenant in hello Azure portal</span></span>

<span data-ttu-id="7443d-104">Modifié par Sipi.</span><span class="sxs-lookup"><span data-stu-id="7443d-104">Edited by Sipi.</span></span>

<span data-ttu-id="7443d-105">Ce démarrage rapide vous aide à créer un locataire Microsoft Azure Active Directory (Azure AD) B2C en seulement quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="7443d-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="7443d-106">Lorsque vous avez terminé, vous avez un toouse du locataire B2C pour inscrire les applications B2C.</span><span class="sxs-lookup"><span data-stu-id="7443d-106">When you're finished, you have a B2C tenant toouse for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7443d-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="7443d-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-tooazure"></a><span data-ttu-id="7443d-108">Connectez-vous à tooAzure</span><span class="sxs-lookup"><span data-stu-id="7443d-108">Log in tooAzure</span></span>

<span data-ttu-id="7443d-109">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="7443d-109">Log in toohello [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="7443d-110">Créer un client Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="7443d-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="7443d-111">Les fonctionnalités B2C ne peuvent pas être activées dans vos locataires existants.</span><span class="sxs-lookup"><span data-stu-id="7443d-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="7443d-112">Vous devez toocreate un locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7443d-112">You need toocreate an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="7443d-113">Félicitations, vous avez créé un locataire Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="7443d-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="7443d-114">Vous êtes un administrateur Global du client de hello.</span><span class="sxs-lookup"><span data-stu-id="7443d-114">You are a Global Administrator of hello tenant.</span></span> <span data-ttu-id="7443d-115">Vous pouvez ajouter d’autres administrateurs généraux en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="7443d-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="7443d-116">tooyour tooswitch nouveau client, cliquez sur hello *gérer votre nouvelle liaison de client*.</span><span class="sxs-lookup"><span data-stu-id="7443d-116">tooswitch tooyour new tenant, click hello *manage your new tenant link*.</span></span>

![Lien permettant de gérer votre nouveau locataire](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="7443d-118">Si vous envisagez de toouse un locataire B2C pour une application de production, lisez l’article de hello sur [production à l’échelle par rapport aux locataires de la version préliminaire B2C](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="7443d-118">If you are planning toouse a B2C tenant for a production app, read hello article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="7443d-119">Il sont problèmes connus lorsque vous supprimez un B2C existant du locataire et recréez-la avec hello même nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="7443d-119">There are known issues when you delete an existing B2C tenant and re-create it with hello same domain name.</span></span> <span data-ttu-id="7443d-120">Vous devez toocreate un locataire B2C avec un nom de domaine différent.</span><span class="sxs-lookup"><span data-stu-id="7443d-120">You need toocreate a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-tooyour-subscription"></a><span data-ttu-id="7443d-121">Lier votre abonnement de tooyour client</span><span class="sxs-lookup"><span data-stu-id="7443d-121">Link your tenant tooyour subscription</span></span>

<span data-ttu-id="7443d-122">Vous devez toolink votre B2C de AD Azure locataire tooyour abonnement Azure tooenable toutes les fonctionnalités B2C et payer des frais d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="7443d-122">You need toolink your Azure AD B2C tenant tooyour Azure subscription tooenable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="7443d-123">toolearn plus, lisez [cet article](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="7443d-123">toolearn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="7443d-124">Si vous ne liez pas votre tooyour de locataire Azure AD B2C abonnement Azure, certaines fonctionnalités sont bloquée et, vous voyez un message d’avertissement (« aucun abonnement liés toothis B2C locataire ou hello abonnement ne nécessite votre attention. ») dans les paramètres de hello B2C.</span><span class="sxs-lookup"><span data-stu-id="7443d-124">If you don't link your Azure AD B2C tenant tooyour Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked toothis B2C tenant or hello Subscription needs your attention.") in hello B2C settings.</span></span> <span data-ttu-id="7443d-125">Il est important d’effectuer cette étape avant de passer vos applications en production.</span><span class="sxs-lookup"><span data-stu-id="7443d-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-toosettings"></a><span data-ttu-id="7443d-126">Un accès facile toosettings</span><span class="sxs-lookup"><span data-stu-id="7443d-126">Easy access toosettings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="7443d-127">Vous pouvez également accéder à panneau de hello en entrant `Azure AD B2C` dans **recherche les ressources** haut hello du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="7443d-127">You can also access hello blade by entering `Azure AD B2C` in **Search resources** at hello top of hello portal.</span></span> <span data-ttu-id="7443d-128">Dans la liste des résultats hello, sélectionnez **Azure AD B2C** tooaccess hello Panneau de paramètres B2C.</span><span class="sxs-lookup"><span data-stu-id="7443d-128">In hello results list, select **Azure AD B2C** tooaccess hello B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7443d-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7443d-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7443d-130">Azure Active Directory B2C : inscription de votre application</span><span class="sxs-lookup"><span data-stu-id="7443d-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
