---
title: "Ajout de nouveaux utilisateurs à Azure Active Directory | Microsoft Docs"
description: "Explique comment ajouter de nouveaux utilisateurs à Azure Active Directory."
services: active-directory
documentationcenter: 
author: jeffgilb
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 13a7d2d3b991206c45e66872b590bc27a224eead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="quickstart-add-new-users-to-azure-active-directory"></a><span data-ttu-id="7f951-103">Démarrage rapide : Ajouter de nouveaux utilisateurs à Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7f951-103">Quickstart: Add new users to Azure Active Directory</span></span>
<span data-ttu-id="7f951-104">Cet article explique comment ajouter, un à la fois, de nouveaux utilisateurs de votre organisation à Azure Active Directory (Azure AD) à l’aide du portail Azure ou en synchronisant vos données de compte d’utilisateur Windows Server AD local.</span><span class="sxs-lookup"><span data-stu-id="7f951-104">This article explains how to add new users in your organization in the Azure Active Directory (Azure AD) one at a time using the Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="7f951-105">Ajouter des utilisateurs basés sur le cloud</span><span class="sxs-lookup"><span data-stu-id="7f951-105">Add cloud-based users</span></span>
1. <span data-ttu-id="7f951-106">Connectez-vous au [centre d’administration Azure Active Directory](https://aad.portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="7f951-106">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7f951-107">Sélectionnez **Azure Active Directory**, puis **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7f951-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="7f951-108">Dans le panneau **Utilisateurs et groupes**, sélectionnez **Tous les utilisateurs**, puis sélectionnez **Nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="7f951-108">On the **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="7f951-109">![Sélection de la commande Ajouter](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="7f951-109">![Selecting the Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="7f951-110">Entrez les détails de l’utilisateur, dont son **nom** et son **nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="7f951-110">Enter details for the user, such as **Name** and **User name**.</span></span> <span data-ttu-id="7f951-111">La partie du nom de domaine du nom d’utilisateur doit être le nom de domaine initial par défaut, « [nom de domaine].onmicrosoft.com », ou un [nom de domaine personnalisé](add-custom-domain.md) vérifié, non fédéré, comme « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="7f951-111">The domain name portion of the user name must either be the initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="7f951-112">Copiez ou notez d’une autre façon le mot de passe généré de sorte à pouvoir le fournir à l’utilisateur une fois ce processus terminé.</span><span class="sxs-lookup"><span data-stu-id="7f951-112">Copy or otherwise note the generated user password so that you can provide it to the user after this process is complete.</span></span>
6. <span data-ttu-id="7f951-113">Si vous le souhaitez, vous pouvez ouvrir et remplir les informations dans le panneau **Profil**, le panneau **Groupes** ou le panneau **Rôle de répertoire** pour l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="7f951-113">Optionally, you can open and fill out the information in the **Profile** blade, the **Groups** blade, or the **Directory role** blade for the user.</span></span> <span data-ttu-id="7f951-114">Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="7f951-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="7f951-115">Dans le panneau **Utilisateur**, sélectionnez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="7f951-115">On the **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="7f951-116">Distribuez de manière sécurisée le mot de passe généré au nouvel utilisateur afin qu’il puisse se connecter.</span><span class="sxs-lookup"><span data-stu-id="7f951-116">Securely distribute the generated password to the new user so that the user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="7f951-117">Vous pouvez également synchroniser les données de compte d’utilisateur à partir de Windows Server AD local.</span><span class="sxs-lookup"><span data-stu-id="7f951-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="7f951-118">Les solutions d'identité de Microsoft regroupent des fonctionnalités, locales et cloud, de création d'une identité d'utilisateur unique pour l'authentification et l'autorisation d'accès à toutes les ressources, indépendamment de l'emplacement.</span><span class="sxs-lookup"><span data-stu-id="7f951-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization to all resources, regardless of location.</span></span> <span data-ttu-id="7f951-119">Nous appelons cette identité « identité hybride ».</span><span class="sxs-lookup"><span data-stu-id="7f951-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="7f951-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) peut également être utilisé pour intégrer vos répertoires locaux à Azure Active Directory pour les scénarios d’identité hybride.</span><span class="sxs-lookup"><span data-stu-id="7f951-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used to integrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="7f951-121">Cela vous permet de fournir une identité commune à vos utilisateurs pour les applications Office 365, Azure et SaaS intégrées à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7f951-121">This allows you to provide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="7f951-122">Supprimer des utilisateurs d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f951-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="7f951-123">Connectez-vous au [centre d’administration Azure Active Directory](https://aad.portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.</span><span class="sxs-lookup"><span data-stu-id="7f951-123">Sign in to the [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for the directory.</span></span>
2. <span data-ttu-id="7f951-124">Sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="7f951-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="7f951-125">Dans le panneau **Utilisateurs et groupes**, sélectionnez l’utilisateur à supprimer dans la liste.</span><span class="sxs-lookup"><span data-stu-id="7f951-125">On the **Users and groups** blade, select the user to delete from the list.</span></span> 
4. <span data-ttu-id="7f951-126">Dans le panneau de l’utilisateur sélectionné, sélectionnez **Vue d’ensemble**, puis, dans la barre de commandes, sélectionnez **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="7f951-126">On the blade for the selected user, select **Overview**, and then in the command bar, select **Delete**.</span></span>
   <span data-ttu-id="7f951-127">![Sélection de la commande Ajouter](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="7f951-127">![Selecting the Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="7f951-128">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="7f951-128">Learn more</span></span> 
* [<span data-ttu-id="7f951-129">Ajouter un utilisateur externe</span><span class="sxs-lookup"><span data-stu-id="7f951-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="7f951-130">Affecter un utilisateur à un rôle dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f951-130">Assign a user to a role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="7f951-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="7f951-131">Next steps</span></span>
<span data-ttu-id="7f951-132">Dans ce guide de démarrage rapide, vous avez appris comment ajouter de nouveaux utilisateurs à Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="7f951-132">In this quickstart, you’ve learned how to add new users to Azure AD Premium.</span></span> 

<span data-ttu-id="7f951-133">Vous pouvez utiliser le lien suivant pour créer un nouvel utilisateur dans Azure AD à partir du portail Azure.</span><span class="sxs-lookup"><span data-stu-id="7f951-133">You can use the following link to create a new user in Azure AD from the Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f951-134">Ajouter des utilisateurs dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="7f951-134">Add users to Azure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 