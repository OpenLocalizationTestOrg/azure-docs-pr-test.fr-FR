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
# <a name="quickstart-add-new-users-tooazure-active-directory"></a>Démarrage rapide : Ajouter de nouveaux utilisateurs tooAzure Active Directory
Cet article explique comment tooadd les nouveaux utilisateurs de votre organisation Bonjour Azure Active Directory (Azure AD) une à la fois à l’aide de hello portail Azure ou en synchronisant votre utilisateur de Windows Server Active Directory local compte données. 

## <a name="add-cloud-based-users"></a>Ajouter des utilisateurs basés sur le cloud
1. Connectez-vous à toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **Azure Active Directory**, puis **Utilisateurs et groupes**.
3. Sur hello **utilisateurs et groupes** panneau, sélectionnez **tous les utilisateurs**, puis sélectionnez **nouvel utilisateur**.
   ![En sélectionnant Ajouter une commande hello](./media/add-users-azure-active-directory/add-user.png)
4. Entrez les détails pour l’utilisateur de hello, tel que **nom** et **nom d’utilisateur**. Hello partie nom de domaine du nom d’utilisateur hello doit être hello initiale par défaut domaine nom « [nom de domaine].onmicrosoft.com » ou vérifié, non fédérées [nom de domaine personnalisé](add-custom-domain.md) tels que « contoso.com ».
5. Copie ou sinon hello de Remarque utilisateur mot de passe généré afin que vous pouvez fournir toohello utilisateur une fois ce processus terminé.
6. Si vous le souhaitez, vous pouvez ouvrir et remplissez les informations de hello Bonjour **profil** panneau, hello **groupes** panneau ou hello **rôle d’annuaire** panneau pour l’utilisateur de hello. Pour plus d’informations sur les utilisateurs et les rôles d’administrateur, consultez la page [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md).
7. Sur hello **utilisateur** panneau, sélectionnez **créer**.
8. Distribuer en toute sécurité hello généré un mot de passe toohello nouvel utilisateur afin que hello utilisateur peut se connecter.

> [!TIP]
> Vous pouvez également synchroniser les données de compte d’utilisateur à partir de Windows Server AD local. Solutions d’identité de Microsoft sont réparties entre locaux et des fonctions nuage, de création d’une identité d’utilisateur unique pour l’authentification et d’autorisation des ressources tooall, indépendamment de l’emplacement. Nous appelons cette identité « identité hybride ». [Azure AD Connect](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect) peut être utilisé toointegrate vos répertoires locaux avec Azure Active Directory pour les scénarios d’identité hybride. Cela vous permet de tooprovide une identité commune pour vos utilisateurs pour les applications Office 365, Azure et SaaS intégrée à Azure AD. 

## <a name="delete-users-from-azure-ad"></a>Supprimer des utilisateurs d’Azure AD
1. Connectez-vous à toohello [centre d’administration Active Directory de Azure](https://aad.portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **Utilisateurs et groupes**.
3. Sur hello **utilisateurs et groupes** panneau, toodelete d’utilisateur hello select à partir de la liste de hello. 
4. Dans le panneau hello pour l’utilisateur sélectionné de hello, sélectionnez **vue d’ensemble**, puis, dans la barre de commandes hello, sélectionnez **supprimer**.
   ![En sélectionnant Ajouter une commande hello](./media/add-users-azure-active-directory/delete-user.png)


### <a name="learn-more"></a>En savoir plus 
* [Ajouter un utilisateur externe](active-directory-users-create-external-azure-portal.md)

* [Affecter un rôle d’utilisateur tooa dans Azure AD](active-directory-users-assign-role-azure-portal.md)

## <a name="next-steps"></a>Étapes suivantes
Ce guide de démarrage rapide, vous avez appris comment tooadd nouveaux utilisateurs tooAzure AD Premium. 

Vous pouvez utiliser hello suivant le lien toocreate un nouvel utilisateur dans Azure AD à partir de hello portail Azure.

> [!div class="nextstepaction"]
> [Ajouter des utilisateurs tooAzure AD](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/UserManagementMenuBlade/All users) 
