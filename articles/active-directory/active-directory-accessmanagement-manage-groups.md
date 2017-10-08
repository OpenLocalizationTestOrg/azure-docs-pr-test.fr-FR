---
title: groupes aaaManaging dans Azure Active Directory | Documents Microsoft
description: "Comment toocreate et gérer des groupes toomanage Azure utilisateurs à l’aide d’Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: d1f5451c-3807-423c-8bac-2822d27b893f
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/24/2017
ms.author: curtand
ms.reviewer: kairaz.contractor
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 9bee224655639740b3dd99983892b30c3c537aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="managing-groups-in-azure-active-directory"></a>Gestion des groupes dans Azure Active Directory
> [!div class="op_single_selector"]
> * [portail Azure](active-directory-groups-create-azure-portal.md)
> * [Portail Azure Classic](active-directory-accessmanagement-manage-groups.md)
> * [PowerShell](active-directory-accessmanagement-groups-settings-v2-cmdlets.md)
>
>

Une des fonctionnalités de hello de gestion des utilisateurs Azure Active Directory (Azure AD) est de groupes de toocreate hello possibilité d’utilisateurs. Vous utilisez un groupe tooperform gestion des tâches telles que l’affectation de licences ou autorisations nombre tooa d’utilisateurs à la fois. Vous pouvez également utiliser des groupes l’autorisation accès tooassign de

* Ressources telles que les objets dans le répertoire de hello
* Répertoire des ressources toohello externes tels que les applications SaaS, les services Azure, les sites SharePoint ou les ressources locales

En outre, un propriétaire de la ressource peut également affecter groupe accès tooa ressource tooan Azure AD appartenant à une autre personne. Cette affectation accorde à ses membres hello d’une ressource groupe accès toohello. Ensuite, propriétaire hello du groupe de hello gère l’appartenance au groupe de hello. En réalité, hello propriétaire délégués toohello propriétaire de la ressource de hello hello autorisation tooassign utilisateurs tootheir ressource du groupe de.

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour la façon dont les groupes toomanage dans le centre d’administration hello Azure AD, consultez [créer un groupe et ajouter des membres dans Azure Active Directory](active-directory-groups-create-azure-portal.md).

## <a name="how-do-i-create-a-group"></a>Comment créer un groupe ?
Selon toowhich de services hello que votre organisation est abonnée, vous pouvez créer un groupe à l’aide de valeurs hello suivantes :

* Hello portail Azure classic
* portail du compte Hello Office 365
* portail de compte Windows Intune Hello

Nous allons décrire des tâches effectue Bonjour portail Azure classic. Pour plus d’informations sur l’utilisation des portails de non-Azure toomanage votre annuaire Azure AD, consultez [administrer votre annuaire Azure AD](active-directory-administer.md).

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis sélectionnez le nom hello du répertoire de hello pour votre organisation.
2. Sélectionnez hello **groupes** onglet.
3. Sélectionnez **Ajouter un groupe**.
4. Bonjour **ajouter un groupe** fenêtre, spécifiez le nom de hello et hello description d’un groupe.

## <a name="how-do-i-add-or-remove-individual-users-in-a-security-group"></a>Comment ajouter ou supprimer des utilisateurs individuels dans un groupe de sécurité ?
**tooadd un groupe de tooa utilisateur individuel**

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis sélectionnez le nom hello du répertoire de hello pour votre organisation.
2. Sélectionnez hello **groupes** onglet.
3. Ouvrez toowhich de groupe hello tooadd membres. Ouvrir hello **membres** onglet Hello sélectionné groupe si elle n'affiche pas déjà.
4. Sélectionnez **Ajouter des membres**.
5. Sur hello **ajouter des membres** page, le nom hello select de l’utilisateur de hello ou un groupe que vous souhaitez tooadd en tant que membre de ce groupe. Assurez-vous que ce nom est ajouté toohello **sélectionnés** volet.

**tooremove un utilisateur individuel à partir d’un groupe**

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis sélectionnez le nom hello du répertoire de hello pour votre organisation.
2. Sélectionnez hello **groupes** onglet.
3. Groupe hello ouvert à partir de laquelle vous souhaitez que les membres de tooremove.
4. Sélectionnez hello **membres** onglet, le nom hello sélectionnez du membre hello que vous souhaitez tooremove à partir de ce groupe, puis cliquez sur **supprimer**.
5. Confirmer l’invite hello tooremove ce membre du groupe de hello.

## <a name="how-can-i-manage-hello-membership-of-a-group-dynamically"></a>Comment puis-je gérer dynamiquement l’appartenance de hello d’un groupe ?
Dans Azure AD, vous pouvez très facilement configurer un toodetermine règle simple que les utilisateurs qui sont membres de toobe du groupe de hello. Une règle simple est une règle qui ne fait qu’une seule comparaison. Par exemple, si un groupe est affecté tooa application SaaS, vous pouvez configurer une règle tooadd utilisateurs avec un titre de « Commercial ». Cette règle accorde ensuite l’accès toothis SaaS tooall utilisateurs avec cette fonction dans votre annuaire.

Lorsque tous les attributs d’une modification de l’utilisateur, système de hello prend la valeur toutes les règles de groupe dynamique dans un toosee active si la modification d’attribut hello d’utilisateur de hello déclencherait n’importe quel groupe ajoute ou supprime. Si un utilisateur répond à une règle sur un groupe, ils sont ajoutés en tant que membre toothat groupe. Si elles ne répondent plus aux règles hello d’un groupe, de qu'ils sont membres, ils sont supprimés en tant que membres de ce groupe.

> [!NOTE]
> Vous pouvez définir une règle d’appartenance dynamique sur les groupes de sécurité ou Office 365. Appartenances aux groupes imbriqués ne sont pas actuellement pris en charge pour l’affectation basée sur le groupe tooapplications.
>
> Appartenance dynamique à des groupes nécessite un toobe de licence Azure AD Premium assigné à
>
> * administrateur Hello qui gère la règle hello sur un groupe
> * Tous les membres du groupe de hello
>
>

**appartenance dynamique de tooenable pour un groupe**

1. Bonjour [portail Azure classic](https://manage.windowsazure.com), sélectionnez **Active Directory**, puis sélectionnez le nom hello du répertoire de hello pour votre organisation.
2. Sélectionnez hello **groupes** onglet et groupe ouvert hello tooedit.
3. Sélectionnez hello **configurer** onglet, puis définissez **activer les appartenances dynamiques** trop**Oui**.
4. Configurer une seule règle simple pour hello groupe toocontrol appartenance dynamique fonctionne pour ce groupe. Vérifiez que hello **ajouter des utilisateurs où** option est sélectionnée, puis sélectionnez une propriété de l’utilisateur à partir de la liste hello (par exemple, département, jobTitle, etc.),
5. Ensuite, sélectionnez une condition (Non égal à, Égal à, Ne commence pas par, Commence par, Ne contient pas, Contient, Ne correspond pas, Correspond).
6. Spécifiez une valeur de comparaison pour la propriété hello sélectionné de l’utilisateur.

toolearn comment toocreate *avancées* règles (qui peut contenir plusieurs comparaisons) pour l’appartenance au groupe dynamique, consultez [à l’aide des attributs toocreate des règles avancées](active-directory-accessmanagement-groups-with-advanced-rules.md).

## <a name="additional-information"></a>Informations supplémentaires
Ces articles fournissent des informations supplémentaires sur Azure Active Directory.

* [La gestion des accès tooresources avec les groupes Azure Active Directory](active-directory-manage-groups.md)
* [Configuration des paramètres de groupe avec les applets de commande Azure Active Directory](active-directory-accessmanagement-groups-settings-cmdlets.md)
* [Index d’articles pour la gestion des applications dans Azure Active Directory](active-directory-apps-index.md)
* [Qu’est-ce qu’Azure Active Directory ?](active-directory-whatis.md)
* [Intégration des identités locales dans Azure Active Directory](active-directory-aadconnect.md)
