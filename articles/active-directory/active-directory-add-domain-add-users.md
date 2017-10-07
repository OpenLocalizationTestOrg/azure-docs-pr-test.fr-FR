---
title: "domaine personnalisé tooa utilisateurs aaaAssign dans Azure Active Directory | Documents Microsoft"
description: "Comment toopopulate un domaine personnalisé dans Azure Active Directory avec des comptes d’utilisateur."
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
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a><span data-ttu-id="b3db7-103">Affecter les utilisateurs domaine personnalisé tooa</span><span class="sxs-lookup"><span data-stu-id="b3db7-103">Assign users tooa custom domain</span></span>
<span data-ttu-id="b3db7-104">Après avoir ajouté votre tooAzure personnalisé de domaine Active Directory, vous devez ajouter les comptes d’utilisateur hello pour ce domaine afin que vous puissiez commencer à authentifier les.</span><span class="sxs-lookup"><span data-stu-id="b3db7-104">After you have added your custom domain tooAzure Active Directory, you must add hello user accounts for this domain so that you can begin authenticating them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3db7-105">Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article.</span><span class="sxs-lookup"><span data-stu-id="b3db7-105">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> <span data-ttu-id="b3db7-106">Pour comment toomanage vos noms de domaine dans le centre d’administration hello Azure AD, consultez [la gestion des noms de domaines personnalisés dans Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b3db7-106">For how toomanage your domain names in hello Azure AD admin center, see [Managing custom domain names in your Azure Active Directory](active-directory-domains-manage-azure-portal.md).</span></span>

## <a name="users-synced-from-a-on-premises-directory"></a><span data-ttu-id="b3db7-107">Utilisateurs synchronisés à partir d’un répertoire local</span><span class="sxs-lookup"><span data-stu-id="b3db7-107">Users synced from a on-premises directory</span></span>
<span data-ttu-id="b3db7-108">Si vous avez déjà configuré une connexion entre votre service Active Directory et Azure Active Directory, synchronisation peut remplir les comptes hello.</span><span class="sxs-lookup"><span data-stu-id="b3db7-108">If you have already set up a connection between your on-premises Active Directory and Azure Active Directory, synchronization can populate hello accounts.</span></span> <span data-ttu-id="b3db7-109">Pour plus d’informations sur comment toosynchronize Azure Active Directory avec votre Active Directory local, consultez [intégrer vos identités locales avec Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="b3db7-109">For more information on how toosynchronize Azure Active Directory with your on-premises Active Directory, see [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>

## <a name="users-added-and-managed-in-hello-cloud"></a><span data-ttu-id="b3db7-110">Les utilisateurs ajoutés et gérés dans le cloud de hello</span><span class="sxs-lookup"><span data-stu-id="b3db7-110">Users added and managed in hello cloud</span></span>
<span data-ttu-id="b3db7-111">domaine de hello toochange pour un compte d’utilisateur :</span><span class="sxs-lookup"><span data-stu-id="b3db7-111">toochange hello domain for an existing user account:</span></span>

1. <span data-ttu-id="b3db7-112">Ouvrez hello portail Azure classic à l’aide d’un compte qui est un administrateur global ou un administrateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3db7-112">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="b3db7-113">Ouvrez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="b3db7-113">Open your directory.</span></span>
3. <span data-ttu-id="b3db7-114">Sélectionnez hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="b3db7-114">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="b3db7-115">Sélectionnez l’utilisateur de hello à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="b3db7-115">Select hello user from hello list.</span></span>
5. <span data-ttu-id="b3db7-116">Modifier le domaine hello pour l’utilisateur de hello et sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b3db7-116">Change hello domain for hello user, and then select **Save**.</span></span>

<span data-ttu-id="b3db7-117">Cela peut également être effectuée à l’aide [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span><span class="sxs-lookup"><span data-stu-id="b3db7-117">This can also be done using [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) or hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).</span></span>

## <a name="select-a-custom-domain-when-creating-a-new-user"></a><span data-ttu-id="b3db7-118">Sélectionner un domaine personnalisé lors de la création d'un nouvel utilisateur</span><span class="sxs-lookup"><span data-stu-id="b3db7-118">Select a custom domain when creating a new user</span></span>
1. <span data-ttu-id="b3db7-119">Ouvrez hello portail Azure classic à l’aide d’un compte qui est un administrateur global ou un administrateur de l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="b3db7-119">Open hello Azure classic portal using an account that is a global admin or a user admin.</span></span>
2. <span data-ttu-id="b3db7-120">Ouvrez votre annuaire.</span><span class="sxs-lookup"><span data-stu-id="b3db7-120">Open your directory.</span></span>
3. <span data-ttu-id="b3db7-121">Sélectionnez hello **utilisateurs** onglet.</span><span class="sxs-lookup"><span data-stu-id="b3db7-121">Select hello **Users** tab.</span></span>
4. <span data-ttu-id="b3db7-122">Dans la barre de commandes hello, sélectionnez **ajouter**.</span><span class="sxs-lookup"><span data-stu-id="b3db7-122">In hello command bar, select **Add**.</span></span>
5. <span data-ttu-id="b3db7-123">Lorsque vous ajoutez le nom d’utilisateur hello, choisissez le domaine personnalisé de hello à partir de la liste des domaines hello.</span><span class="sxs-lookup"><span data-stu-id="b3db7-123">When you add hello user name, choose hello custom domain from hello domain list.</span></span>
6. <span data-ttu-id="b3db7-124">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b3db7-124">Select **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b3db7-125">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b3db7-125">Next steps</span></span>
* [<span data-ttu-id="b3db7-126">À l’aide du domaine personnalisé noms toosimplify hello expérience de connexion pour vos utilisateurs</span><span class="sxs-lookup"><span data-stu-id="b3db7-126">Using custom domain names toosimplify hello sign-in experience for your users</span></span>](active-directory-add-domain.md)
* [<span data-ttu-id="b3db7-127">Gérer les noms de domaine personnalisés</span><span class="sxs-lookup"><span data-stu-id="b3db7-127">Manage custom domain names</span></span>](active-directory-add-manage-domain-names.md)
* [<span data-ttu-id="b3db7-128">En savoir plus sur les concepts de gestion de domaine dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="b3db7-128">Learn about domain management concepts in Azure AD</span></span>](active-directory-add-domain-concepts.md)

