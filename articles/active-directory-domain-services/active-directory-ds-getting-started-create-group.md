---
title: "Azure Active Directory Domain Services : Créer le groupe d’administrateurs hello Azure AD DC | Documents Microsoft"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: maheshu
ms.openlocfilehash: d629ab9632ef6a45b549630999ff9a122d60c040
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-classic-portal"></a>Activer Azure Active Directory Domain Services à l’aide de hello portail Azure classic
Cet article décrit et guide à travers les tâches de configuration hello qui sont requises pour vous tooenable Azure Active Directory Services de domaine (Azure AD DS) pour votre client Azure Active Directory (Azure AD).

> [!NOTE]
> [**Essayez plutôt de nouvelle expérience de portail (aperçu) Azure hello**](active-directory-ds-getting-started.md). 
>

## <a name="task-1-create-hello-azure-ad-dc-administrators-group"></a>Tâche 1 : créer le groupe Administrateurs de contrôleur de domaine hello Azure AD
tâche première Hello est toocreate un groupe d’administration dans votre locataire Azure AD. Ce groupe d’administration spécial est appelé *AAD DC Administrators*. Membres de ce groupe bénéficient d’autorisations administratives sur les ordinateurs qui appartiennent à un domaine géré par les Services de domaine Active Directory de Azure de toohello de domaine. Sur les ordinateurs joints à un domaine, ce groupe est ajouté toohello groupe d’administrateurs. En outre, les membres de ce groupe peuvent utiliser Bureau à distance tooconnect à distance toodomain-ordinateurs joints à un.  

> [!NOTE]
> Il est inutile des autorisations administrateur de domaine ou administrateur d’entreprise sur un domaine géré hello que vous avez créé à l’aide d’Azure Active Directory Domain Services. Dans des domaines gérés, ces autorisations sont réservées par le service de hello et ne sont pas apportées toousers disponibles au sein de client de hello. Toutefois, vous pouvez utiliser hello spéciaux groupe d’administration créés dans cette tooperform de tâche de configuration certaines opérations privilégiées. Ces opérations comprennent la jonction de domaine toohello des ordinateurs, appartenant toohello groupe d’administration sur les ordinateurs joints au domaine et stratégie de groupe.
>

Dans cette tâche de configuration, vous créez le groupe d’administration hello et ajoutez un ou plusieurs utilisateurs dans votre groupe de toohello active. groupe d’administration toocreate hello pour les Services de domaine Active Directory Azure, procédez comme hello suivant :

1. Accédez toohello [portail Azure classic](https://manage.windowsazure.com).
2. Dans le volet gauche de hello, sélectionnez hello **Active Directory** bouton.
3. Sélectionnez le locataire Azure AD de hello (répertoire) pour lequel vous souhaitez tooenable Azure Active Directory Domain Services. Vous ne pouvez créer qu’un seul domaine par annuaire Azure AD.

    ![Sélectionnez un annuaire Azure AD.](./media/active-directory-domain-services-getting-started/select-aad-directory.png)
4. Sur hello **active de la version préliminaire** , cliquez sur hello **groupes** onglet.
5. Cliquez sur un client tooyour Azure AD de groupe, dans le volet de tâches hello bas hello de fenêtre hello, de tooadd **ajouter un groupe**.

    ![bouton Ajouter un groupe de Hello](./media/active-directory-domain-services-getting-started/add-group-button.png)
6. Bonjour **ajouter un groupe** boîte de dialogue zone, créez un groupe nommé **administrateurs du contrôleur de domaine AAD**, puis définissez **le Type de groupe** trop**sécurité**.

   > [!WARNING]
   > accès tooenable au sein de votre domaine géré par les Services de domaine Active Directory de Azure, créez un groupe portant ce nom exact.
   >
   >

    ![boîte de dialogue Ajouter un groupe Hello](./media/active-directory-domain-services-getting-started/create-admin-group.png)
7. Bonjour **Description** , entrez une description qui permet à d’autres toounderstand que ce groupe accorde des autorisations administratives dans Azure Active Directory Domain Services.
8. Une fois que vous avez créé le groupe de hello, cliquez sur tooview de nom de groupe hello ses propriétés.
9. les utilisateurs de tooadd en tant que membres du groupe hello, au bas de hello de fenêtre hello, cliquez sur hello **ajouter des membres** bouton.

    ![Bouton Ajouter des membres au groupe](./media/active-directory-domain-services-getting-started/add-group-members-button.png)
10. Bonjour **ajouter des membres** boîte de dialogue, sélectionnez hello utilisateurs doivent être membres de ce groupe, puis cliquez sur icône de coche de hello en hello inférieur droit.

    ![Ajouter le groupe d’utilisateurs tooadministrators](./media/active-directory-domain-services-getting-started/add-group-members.png)


## <a name="next-step"></a>Étape suivante
[Tâche 2 : Créer ou sélectionner un réseau virtuel Azure](active-directory-ds-getting-started-vnet.md)
