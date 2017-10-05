---
title: "Affecter des utilisateurs à un domaine personnalisé dans Azure Active Directory | Microsoft Docs"
description: "Comment remplir un domaine personnalisé dans Azure Active Directory avec des comptes d'utilisateur."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 39cb54a6637088c35c6aef864a804c24803f48ba
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="assign-users-to-a-custom-domain"></a><span data-ttu-id="393f3-103">Affecter des utilisateurs à un domaine personnalisé</span><span class="sxs-lookup"><span data-stu-id="393f3-103">Assign users to a custom domain</span></span>
<span data-ttu-id="393f3-104">Après avoir ajouté votre domaine personnalisé à Azure Active Directory, vous devez ajouter les comptes d'utilisateur pour ce domaine afin de pouvoir les authentifier.</span><span class="sxs-lookup"><span data-stu-id="393f3-104">After you have added your custom domain to Azure Active Directory, you must add the user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="393f3-105">Microsoft recommande de gérer Azure AD à l’aide du [Centre d’administration Azure AD](https://aad.portal.azure.com) dans le portail Azure au lieu d’utiliser le portail Azure classique référencé dans cet article.</span><span class="sxs-lookup"><span data-stu-id="393f3-105">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> <span data-ttu-id="393f3-106">Pour savoir comment gérer vos noms de domaine dans le centre d’administration Azure AD, consultez la section [Gestion des noms de domaines personnalisés dans Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="393f3-106">For how to manage your domain names in the Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="393f3-107">Utilisateurs synchronisés à partir d’un répertoire local</span><span class="sxs-lookup"><span data-stu-id="393f3-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="393f3-108">Si vous avez déjà configuré une connexion entre un domaine Active Directory local et Azure Active Directory, la synchronisation peut remplir les comptes.</span><span class="sxs-lookup"><span data-stu-id="393f3-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate the accounts.</span></span> <span data-ttu-id="393f3-109">Pour plus d'informations sur la synchronisation d’Azure Active Directory avec votre domaine Active Directory local, consultez [Intégration de vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="393f3-109">For more information on how to synchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-the-cloud"></a><span data-ttu-id="393f3-110">Utilisateurs ajoutés et gérés dans le cloud</span><span class="sxs-lookup"><span data-stu-id="393f3-110">Users added and managed in the cloud</span></span>
<span data-ttu-id="393f3-111">Pour modifier le domaine d'un compte d'utilisateur existant :</span><span class="sxs-lookup"><span data-stu-id="393f3-111">To change the domain for an existing user account:</span></span>

1. <span data-ttu-id="393f3-112">Ouvrez le portail Azure Classic à l'aide d'un compte administrateur global ou administrateur d'utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="393f3-112">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="393f3-113">Ouvrez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="393f3-113">Open your directory.</span></span>
3. <span data-ttu-id="393f3-114">Cliquez sur l’onglet **Utilisateurs** .</span><span class="sxs-lookup"><span data-stu-id="393f3-114">Select the **Users** tab.</span></span>
4. <span data-ttu-id="393f3-115">Sélectionnez l'utilisateur dans la liste.</span><span class="sxs-lookup"><span data-stu-id="393f3-115">Select the user from the list.</span></span>
5. <span data-ttu-id="393f3-116">Modifiez le domaine de l'utilisateur, puis sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="393f3-116">Change the domain for the user, and then select **Save**.</span></span>

<span data-ttu-id="393f3-117">Vous pouvez également utiliser [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou [l’API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="393f3-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or the [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="393f3-118">Sélectionner un domaine personnalisé lors de la création d'un nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="393f3-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="393f3-119">Ouvrez le portail Azure Classic à l'aide d'un compte administrateur global ou administrateur d'utilisateurs.</span><span class="sxs-lookup"><span data-stu-id="393f3-119">Open the Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="393f3-120">Ouvrez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="393f3-120">Open your directory.</span></span>
3. <span data-ttu-id="393f3-121">Cliquez sur l’onglet **Utilisateurs** .</span><span class="sxs-lookup"><span data-stu-id="393f3-121">Select the **Users** tab.</span></span>
4. <span data-ttu-id="393f3-122">Dans la barre de commandes, sélectionnez **Ajouter**.</span><span class="sxs-lookup"><span data-stu-id="393f3-122">In the command bar, select **Add**.</span></span>
5. <span data-ttu-id="393f3-123">Lorsque vous ajoutez le nom d'utilisateur, choisissez le domaine personnalisé dans la liste des domaines.</span><span class="sxs-lookup"><span data-stu-id="393f3-123">When you add the user name, choose the custom domain from the domain list.</span></span>
6. <span data-ttu-id="393f3-124">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="393f3-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="393f3-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="393f3-125">Next steps</span></span>
* [<span data-ttu-id="393f3-126">Utilisation de noms de domaine personnalisés pour simplifier l’expérience de connexion pour vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="393f3-126">Using custom domain names to simplify the sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="393f3-127">Gérer les noms de domaine personnalisés</span><span class="sxs-lookup"><span data-stu-id="393f3-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="393f3-128">En savoir plus sur les concepts de gestion de domaine dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="393f3-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

