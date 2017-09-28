---
title: "Azure Active Directory B2C : création d’un client Azure Active Directory B2C | Microsoft Docs"
description: "Rubrique sur la création d’un client Azure Active Directory B2C"
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
ms.openlocfilehash: 8a1d4935397f59e5813afc6f04559e471187a779
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="65f0b-103">Créer un locataire Azure Active Directory B2C dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="65f0b-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="65f0b-104">Ce démarrage rapide vous aide à créer un locataire Microsoft Azure Active Directory (Azure AD) B2C en seulement quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="65f0b-104">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="65f0b-105">Lorsque vous avez terminé, vous disposez d’un locataire B2C pour inscrire les applications B2C.</span><span class="sxs-lookup"><span data-stu-id="65f0b-105">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="65f0b-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="65f0b-106">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="65f0b-107">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="65f0b-107">Log in to Azure</span></span>

<span data-ttu-id="65f0b-108">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="65f0b-108">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="65f0b-109">Créer un client Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="65f0b-109">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="65f0b-110">Les fonctionnalités B2C ne peuvent pas être activées dans vos locataires existants.</span><span class="sxs-lookup"><span data-stu-id="65f0b-110">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="65f0b-111">Vous devez créer un locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="65f0b-111">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="65f0b-112">Félicitations, vous avez créé un locataire Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="65f0b-112">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="65f0b-113">Vous êtes administrateur général du locataire.</span><span class="sxs-lookup"><span data-stu-id="65f0b-113">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="65f0b-114">Vous pouvez ajouter d’autres administrateurs généraux en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="65f0b-114">You can add other Global Administrators as required.</span></span> <span data-ttu-id="65f0b-115">Pour basculer vers votre nouveau locataire, cliquez sur le *lien permettant de gérer votre nouveau locataire*.</span><span class="sxs-lookup"><span data-stu-id="65f0b-115">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Lien permettant de gérer votre nouveau locataire](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="65f0b-117">Si vous envisagez d’utiliser un client B2C pour une application de production, consultez l’article sur [les clients de mise à l’échelle pour production/clients B2C de la version préliminaire](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="65f0b-117">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="65f0b-118">Il existe des problèmes connus liés à la suppression d’un locataire B2C existant et à sa recréation sous le même nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="65f0b-118">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="65f0b-119">Vous devez créer un locataire B2C portant un nom de domaine différent.</span><span class="sxs-lookup"><span data-stu-id="65f0b-119">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="65f0b-120">Lier votre locataire à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="65f0b-120">Link your tenant to your subscription</span></span>

<span data-ttu-id="65f0b-121">Vous devez lier votre locataire Azure AD B2C à votre abonnement Azure pour activer toutes les fonctionnalités B2C et payer les frais d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="65f0b-121">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="65f0b-122">Pour plus d’informations, consultez [cet article](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="65f0b-122">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="65f0b-123">Si vous ne liez pas votre locataire Azure AD B2C à votre abonnement Azure, certaines fonctionnalités sont bloquées et vous voyez un message d’avertissement (« Aucun abonnement lié à ce client B2C ou à l’abonnement ne requiert votre attention. ») dans les paramètres B2C.</span><span class="sxs-lookup"><span data-stu-id="65f0b-123">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="65f0b-124">Il est important d’effectuer cette étape avant de passer vos applications en production.</span><span class="sxs-lookup"><span data-stu-id="65f0b-124">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="65f0b-125">Accès facile aux paramètres</span><span class="sxs-lookup"><span data-stu-id="65f0b-125">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="65f0b-126">Vous pouvez également accéder au panneau en entrant `Azure AD B2C` dans **Rechercher des ressources** en haut du portail.</span><span class="sxs-lookup"><span data-stu-id="65f0b-126">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="65f0b-127">Dans la liste des résultats, sélectionnez **Azure AD B2C** pour accéder au panneau des paramètres B2C.</span><span class="sxs-lookup"><span data-stu-id="65f0b-127">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65f0b-128">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="65f0b-128">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="65f0b-129">Azure Active Directory B2C : inscription de votre application</span><span class="sxs-lookup"><span data-stu-id="65f0b-129">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)