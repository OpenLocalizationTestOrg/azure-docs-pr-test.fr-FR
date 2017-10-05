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
# <a name="quickstart-add-new-users-to-azure-active-directory"></a>Démarrage rapide : Ajouter de nouveaux utilisateurs à Azure Active Directory
Cet article explique comment ajouter, un à la fois, de nouveaux utilisateurs de votre organisation à Azure Active Directory (Azure AD) à l’aide du portail Azure ou en synchronisant vos données de compte d’utilisateur Windows Server AD local. 

## <a name="add-cloud-based-users"></a>Ajouter des utilisateurs basés sur le cloud
1. Connectez-vous au [centre d’administration Azure Active Directory](https://aad.portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.
2. Sélectionnez **Azure Active Directory**, puis **Utilisateurs et groupes**.
3. Dans le panneau **Utilisateurs et groupes**, sélectionnez **Tous les utilisateurs**, puis sélectionnez **Nouvel utilisateur**.
   ![Sélection de la commande Ajouter](./media/add-users-azure-active-directory/add-user.png)
4. Entrez les détails de l’utilisateur, dont son **nom** et son **nom d’utilisateur**. La partie du nom de domaine du nom d’utilisateur doit être le nom de domaine initial par défaut, « [nom de domaine].onmicrosoft.com », ou un [nom de domaine personnalisé](add-custom-domain.md) vérifié, non fédéré, comme « contoso.com ».
5. Copiez ou notez d’une autre façon le mot de passe généré de sorte à pouvoir le fournir à l’utilisateur une fois ce processus terminé.
6. Si vous le souhaitez, vous pouvez ouvrir et remplir les informations dans le panneau **Profil**, le panneau **Groupes** ou le panneau **Rôle de répertoire** pour l’utilisateur. Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md).
7. Dans le panneau **Utilisateur**, sélectionnez **Créer**.
8. Distribuez de manière sécurisée le mot de passe généré au nouvel utilisateur afin qu’il puisse se connecter.

> [!TIP]
> Vous pouvez également synchroniser les données de compte d’utilisateur à partir de Windows Server AD local. Les solutions d'identité de Microsoft regroupent des fonctionnalités, locales et cloud, de création d'une identité d'utilisateur unique pour l'authentification et l'autorisation d'accès à toutes les ressources, indépendamment de l'emplacement. Nous appelons cette identité « identité hybride ». [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) peut également être utilisé pour intégrer vos répertoires locaux à Azure Active Directory pour les scénarios d’identité hybride. Cela vous permet de fournir une identité commune à vos utilisateurs pour les applications Office 365, Azure et SaaS intégrées à Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Supprimer des utilisateurs d’Azure AD
1. Connectez-vous au [centre d’administration Azure Active Directory](https://aad.portal.azure.com) en utilisant un compte d’administrateur général pour le répertoire.
2. Sélectionnez **Utilisateurs et groupes**.
3. Dans le panneau **Utilisateurs et groupes**, sélectionnez l’utilisateur à supprimer dans la liste. 
4. Dans le panneau de l’utilisateur sélectionné, sélectionnez **Vue d’ensemble**, puis, dans la barre de commandes, sélectionnez **Supprimer**.
   ![Sélection de la commande Ajouter](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>En savoir plus 
* [Ajouter un utilisateur externe](active-directory-users-create-external-azure-portal.md)

* [Affecter un utilisateur à un rôle dans Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Étapes suivantes
Dans ce guide de démarrage rapide, vous avez appris comment ajouter de nouveaux utilisateurs à Azure AD Premium. 

Vous pouvez utiliser le lien suivant pour créer un nouvel utilisateur dans Azure AD à partir du portail Azure.

> [!div class="nextstepaction"]
> [Ajouter des utilisateurs dans Azure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 