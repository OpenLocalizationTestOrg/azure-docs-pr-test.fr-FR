---
title: aaaAdd nouveaux utilisateurs tooAzure Active Directory | Documents Microsoft
description: Explique comment tooadd de nouveaux utilisateurs dans Azure Active Directory.
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
ms.openlocfilehash: 6ca413c84a7a5238a30fd26fc751d687d827b24a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-new-users-tooazure-active-directory"></a><span data-ttu-id="70e33-103">Démarrage rapide : Ajouter de nouveaux utilisateurs tooAzure Active Directory</span><span class="sxs-lookup"><span data-stu-id="70e33-103">Quickstart: Add new users tooAzure Active Directory</span></span>
<span data-ttu-id="70e33-104">Cet article explique comment tooadd les nouveaux utilisateurs de votre organisation Bonjour Azure Active Directory (Azure AD) une à la fois à l’aide de hello portail Azure ou en synchronisant votre utilisateur de Windows Server Active Directory local compte données.</span><span class="sxs-lookup"><span data-stu-id="70e33-104">This article explains how tooadd new users in your organization in hello Azure Active Directory (Azure AD) one at a time using hello Azure portal or by synchronizing your on-premises Windows Server AD user account data.</span></span> 

## <a name="add-cloud-based-users"></a><span data-ttu-id="70e33-105">Ajouter des utilisateurs basés sur le cloud</span><span class="sxs-lookup"><span data-stu-id="70e33-105">Add cloud-based users</span></span>
1. <span data-ttu-id="70e33-106">Connectez-vous à toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="70e33-106">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="70e33-107">Sélectionnez **Azure Active Directory**, puis **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70e33-107">Select **Azure Active Directory** and then **Users and groups**.</span></span>
3. <span data-ttu-id="70e33-108">Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les utilisateurs**, puis sélectionnez **nouvel utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="70e33-108">On hello **Users and groups** blade, select **All users**, and then select **New user**.</span></span>
   <span data-ttu-id="70e33-109">![En sélectionnant Ajouter une commande hello](./media/add-users-azure-active-directory/add-user.png)</span><span class="sxs-lookup"><span data-stu-id="70e33-109">![Selecting hello Add command](./media/add-users-azure-active-directory/add-user.png)</span></span>
4. <span data-ttu-id="70e33-110">Entrez les détails pour l’utilisateur de hello, tel que **nom** et **nom d’utilisateur**.</span><span class="sxs-lookup"><span data-stu-id="70e33-110">Enter details for hello user, such as **Name** and **User name**.</span></span> <span data-ttu-id="70e33-111">Hello partie nom de domaine du nom d’utilisateur hello doit être hello initiale par défaut domaine nom « [nom de domaine].onmicrosoft.com » ou vérifié, non fédérées [nom de domaine personnalisé](add-custom-domain.md) tels que « contoso.com ».</span><span class="sxs-lookup"><span data-stu-id="70e33-111">hello domain name portion of hello user name must either be hello initial default domain name "[domain name].onmicrosoft.com" or a verified, non-federated [custom domain name](add-custom-domain.md) such as "contoso.com."</span></span>
5. <span data-ttu-id="70e33-112">Copie ou sinon hello de Remarque utilisateur mot de passe généré afin que vous pouvez fournir toohello utilisateur une fois ce processus terminé.</span><span class="sxs-lookup"><span data-stu-id="70e33-112">Copy or otherwise note hello generated user password so that you can provide it toohello user after this process is complete.</span></span>
6. <span data-ttu-id="70e33-113">Si vous le souhaitez, vous pouvez ouvrir et remplissez les informations de hello Bonjour **profil** panneau, hello **groupes** panneau ou hello **rôle d’annuaire** panneau pour l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="70e33-113">Optionally, you can open and fill out hello information in hello **Profile** blade, hello **Groups** blade, or hello **Directory role** blade for hello user.</span></span> <span data-ttu-id="70e33-114">Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md).</span><span class="sxs-lookup"><span data-stu-id="70e33-114">For more information about user and administrator roles, see [Assigning administrator roles in Azure AD](active-directory-assign-admin-roles.md).</span></span>
7. <span data-ttu-id="70e33-115">Sur hello **utilisateur** panneau, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="70e33-115">On hello **User** blade, select **Create**.</span></span>
8. <span data-ttu-id="70e33-116">Distribuer en toute sécurité hello généré un mot de passe toohello nouvel utilisateur afin que hello utilisateur peut se connecter.</span><span class="sxs-lookup"><span data-stu-id="70e33-116">Securely distribute hello generated password toohello new user so that hello user can sign in.</span></span>

> [!TIP]
> <span data-ttu-id="70e33-117">Vous pouvez également synchroniser les données de compte d’utilisateur à partir de Windows Server AD local.</span><span class="sxs-lookup"><span data-stu-id="70e33-117">You can also synchronize user account data from on-premises Windows Server AD.</span></span> <span data-ttu-id="70e33-118">Solutions d’identité de Microsoft sont réparties entre locaux et des fonctions nuage, de création d’une identité d’utilisateur unique pour l’authentification et d’autorisation des ressources tooall, indépendamment de l’emplacement.</span><span class="sxs-lookup"><span data-stu-id="70e33-118">Microsoft’s identity solutions span on-premises and cloud-based capabilities, creating a single user identity for authentication and authorization tooall resources, regardless of location.</span></span> <span data-ttu-id="70e33-119">Nous appelons cette identité « identité hybride ».</span><span class="sxs-lookup"><span data-stu-id="70e33-119">We call this Hybrid Identity.</span></span> <span data-ttu-id="70e33-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) peut être utilisé toointegrate vos répertoires locaux avec Azure Active Directory pour les scénarios d’identité hybride.</span><span class="sxs-lookup"><span data-stu-id="70e33-120">[Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) can be used toointegrate your on-premises directories with Azure Active Directory for hybrid identity scenarios.</span></span> <span data-ttu-id="70e33-121">Cela vous permet de tooprovide une identité commune pour vos utilisateurs pour les applications Office 365, Azure et SaaS intégrée à Azure AD.</span><span class="sxs-lookup"><span data-stu-id="70e33-121">This allows you tooprovide a common identity for your users for Office 365, Azure, and SaaS applications integrated with Azure AD.</span></span> 

## <a name="delete-users-from-azure-ad"></a><span data-ttu-id="70e33-122">Supprimer des utilisateurs d’Azure AD</span><span class="sxs-lookup"><span data-stu-id="70e33-122">Delete users from Azure AD</span></span>
1. <span data-ttu-id="70e33-123">Connectez-vous à toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.</span><span class="sxs-lookup"><span data-stu-id="70e33-123">Sign in toohello [Azure Active Directory admin center](https://aad.portal.azure.com) with an account that's a global admin for hello directory.</span></span>
2. <span data-ttu-id="70e33-124">Sélectionnez **Utilisateurs et groupes**.</span><span class="sxs-lookup"><span data-stu-id="70e33-124">Select **Users and groups**.</span></span>
3. <span data-ttu-id="70e33-125">Sur hello **utilisateurs et groupes** panneau, toodelete d’utilisateur hello select à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="70e33-125">On hello **Users and groups** blade, select hello user toodelete from hello list.</span></span> 
4. <span data-ttu-id="70e33-126">Dans le panneau hello pour l’utilisateur sélectionné de hello, sélectionnez **vue d’ensemble**, puis, dans la barre de commandes hello, sélectionnez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="70e33-126">On hello blade for hello selected user, select **Overview**, and then in hello command bar, select **Delete**.</span></span>
   <span data-ttu-id="70e33-127">![En sélectionnant Ajouter une commande hello](./media/add-users-azure-active-directory/delete-user.png)</span><span class="sxs-lookup"><span data-stu-id="70e33-127">![Selecting hello Add command](./media/add-users-azure-active-directory/delete-user.png)</span></span>


### <a name="learn-more"></a><span data-ttu-id="70e33-128">En savoir plus</span><span class="sxs-lookup"><span data-stu-id="70e33-128">Learn more</span></span> 
* [<span data-ttu-id="70e33-129">Ajouter un utilisateur externe</span><span class="sxs-lookup"><span data-stu-id="70e33-129">Add an external user</span></span>](active-directory-users-create-external-azure-portal.md)

* [<span data-ttu-id="70e33-130">Affecter un rôle d’utilisateur tooa dans Azure AD</span><span class="sxs-lookup"><span data-stu-id="70e33-130">Assign a user tooa role in your Azure AD</span></span>](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a><span data-ttu-id="70e33-131">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="70e33-131">Next steps</span></span>
<span data-ttu-id="70e33-132">Ce guide de démarrage rapide, vous avez appris comment tooadd nouveaux utilisateurs tooAzure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="70e33-132">In this quickstart, you’ve learned how tooadd new users tooAzure AD Premium.</span></span> 

<span data-ttu-id="70e33-133">Vous pouvez utiliser hello suivant le lien toocreate un nouvel utilisateur dans Azure AD à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="70e33-133">You can use hello following link toocreate a new user in Azure AD from hello Azure portal.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="70e33-134">Ajouter des utilisateurs tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="70e33-134">Add users tooAzure AD</span></span>](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
