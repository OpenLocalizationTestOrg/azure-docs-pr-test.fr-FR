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
ms.openlocfilehash: 1a7eb94e3c74aa0dc187a6d203ba0cf885b97c4d
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2017
---
# <a name="create-an-azure-active-directory-b2c-tenant-in-the-azure-portal"></a><span data-ttu-id="c023f-103">Créer un locataire Azure Active Directory B2C dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="c023f-103">Create an Azure Active Directory B2C tenant in the Azure portal</span></span>

<span data-ttu-id="c023f-104">Modifié par Sipi.</span><span class="sxs-lookup"><span data-stu-id="c023f-104">Edited by Sipi.</span></span>

<span data-ttu-id="c023f-105">Ce démarrage rapide vous aide à créer un locataire Microsoft Azure Active Directory (Azure AD) B2C en seulement quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="c023f-105">This Quickstart helps you create a Microsoft Azure Active Directory (Azure AD) B2C tenant in just a few minutes.</span></span> <span data-ttu-id="c023f-106">Lorsque vous avez terminé, vous disposez d’un locataire B2C pour inscrire les applications B2C.</span><span class="sxs-lookup"><span data-stu-id="c023f-106">When you're finished, you have a B2C tenant to use for registering B2C applications.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c023f-107">Composants requis</span><span class="sxs-lookup"><span data-stu-id="c023f-107">Prerequisites</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

##  <a name="log-in-to-azure"></a><span data-ttu-id="c023f-108">Connexion à Azure</span><span class="sxs-lookup"><span data-stu-id="c023f-108">Log in to Azure</span></span>

<span data-ttu-id="c023f-109">Connectez-vous au [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="c023f-109">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-ad-b2c-tenant"></a><span data-ttu-id="c023f-110">Créer un client Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="c023f-110">Create an Azure AD B2C tenant</span></span>

<span data-ttu-id="c023f-111">Les fonctionnalités B2C ne peuvent pas être activées dans vos locataires existants.</span><span class="sxs-lookup"><span data-stu-id="c023f-111">B2C features can't be enabled in your existing tenants.</span></span> <span data-ttu-id="c023f-112">Vous devez créer un locataire Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="c023f-112">You need to create an Azure AD B2C tenant.</span></span>

[!INCLUDE [active-directory-b2c-create-tenant](../../includes/active-directory-b2c-create-tenant.md)]

<span data-ttu-id="c023f-113">Félicitations, vous avez créé un locataire Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="c023f-113">Congratulations, you have created an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="c023f-114">Vous êtes administrateur général du locataire.</span><span class="sxs-lookup"><span data-stu-id="c023f-114">You are a Global Administrator of the tenant.</span></span> <span data-ttu-id="c023f-115">Vous pouvez ajouter d’autres administrateurs généraux en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="c023f-115">You can add other Global Administrators as required.</span></span> <span data-ttu-id="c023f-116">Pour basculer vers votre nouveau locataire, cliquez sur le *lien permettant de gérer votre nouveau locataire*.</span><span class="sxs-lookup"><span data-stu-id="c023f-116">To switch to your new tenant, click the *manage your new tenant link*.</span></span>

![Lien permettant de gérer votre nouveau locataire](./media/active-directory-b2c-get-started/manage-new-b2c-tenant-link.png)

> [!IMPORTANT]
> <span data-ttu-id="c023f-118">Si vous envisagez d’utiliser un client B2C pour une application de production, consultez l’article sur [les clients de mise à l’échelle pour production/clients B2C de la version préliminaire](active-directory-b2c-reference-tenant-type.md).</span><span class="sxs-lookup"><span data-stu-id="c023f-118">If you are planning to use a B2C tenant for a production app, read the article on [production-scale vs. preview B2C tenants](active-directory-b2c-reference-tenant-type.md).</span></span> <span data-ttu-id="c023f-119">Il existe des problèmes connus liés à la suppression d’un locataire B2C existant et à sa recréation sous le même nom de domaine.</span><span class="sxs-lookup"><span data-stu-id="c023f-119">There are known issues when you delete an existing B2C tenant and re-create it with the same domain name.</span></span> <span data-ttu-id="c023f-120">Vous devez créer un locataire B2C portant un nom de domaine différent.</span><span class="sxs-lookup"><span data-stu-id="c023f-120">You need to create a B2C tenant with a different domain name.</span></span>
>
>

## <a name="link-your-tenant-to-your-subscription"></a><span data-ttu-id="c023f-121">Lier votre locataire à votre abonnement</span><span class="sxs-lookup"><span data-stu-id="c023f-121">Link your tenant to your subscription</span></span>

<span data-ttu-id="c023f-122">Vous devez lier votre locataire Azure AD B2C à votre abonnement Azure pour activer toutes les fonctionnalités B2C et payer les frais d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="c023f-122">You need to link your Azure AD B2C tenant to your Azure subscription to enable all B2C functionality and pay for usage charges.</span></span> <span data-ttu-id="c023f-123">Pour plus d’informations, consultez [cet article](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="c023f-123">To learn more, read [this article](active-directory-b2c-how-to-enable-billing.md).</span></span> <span data-ttu-id="c023f-124">Si vous ne liez pas votre locataire Azure AD B2C à votre abonnement Azure, certaines fonctionnalités sont bloquées et vous voyez un message d’avertissement (« Aucun abonnement lié à ce client B2C ou à l’abonnement ne requiert votre attention. ») dans les paramètres B2C.</span><span class="sxs-lookup"><span data-stu-id="c023f-124">If you don't link your Azure AD B2C tenant to your Azure subscription, some functionality is blocked and, you see a warning message ("No Subscription linked to this B2C tenant or the Subscription needs your attention.") in the B2C settings.</span></span> <span data-ttu-id="c023f-125">Il est important d’effectuer cette étape avant de passer vos applications en production.</span><span class="sxs-lookup"><span data-stu-id="c023f-125">It is important that you take this step before you ship your apps into production.</span></span>

## <a name="easy-access-to-settings"></a><span data-ttu-id="c023f-126">Accès facile aux paramètres</span><span class="sxs-lookup"><span data-stu-id="c023f-126">Easy access to settings</span></span>

[!INCLUDE [active-directory-b2c-find-service-settings](../../includes/active-directory-b2c-find-service-settings.md)]

<span data-ttu-id="c023f-127">Vous pouvez également accéder au panneau en entrant `Azure AD B2C` dans **Rechercher des ressources** en haut du portail.</span><span class="sxs-lookup"><span data-stu-id="c023f-127">You can also access the blade by entering `Azure AD B2C` in **Search resources** at the top of the portal.</span></span> <span data-ttu-id="c023f-128">Dans la liste des résultats, sélectionnez **Azure AD B2C** pour accéder au panneau des paramètres B2C.</span><span class="sxs-lookup"><span data-stu-id="c023f-128">In the results list, select **Azure AD B2C** to access the B2C settings blade.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c023f-129">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="c023f-129">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c023f-130">Azure Active Directory B2C : inscription de votre application</span><span class="sxs-lookup"><span data-stu-id="c023f-130">Register your B2C application in a B2C tenant</span></span>](active-directory-b2c-app-registration.md)
