---
title: "Azure Active Directory Domain Services : guide d’administration | Microsoft Docs"
description: "Créer une UO sur des domaines gérés par les services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 52602ad8-2b93-4082-8487-427bdcfa8126
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: ce7539e5d5c7c1bf9505ef229f2d31d84c00da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-organizational-unit-ou-on-an-azure-ad-domain-services-managed-domain"></a>Créer une UO sur un domaine géré par les services de domaine Azure Active Directory
Les domaines gérés par les services de domaine Azure Active Directory incluent deux conteneurs intégrés, appelés « Ordinateurs AADDC » et « Utilisateurs AADDC », respectivement. Hello 'AADDC ordinateurs' conteneur a des objets ordinateur pour tous les ordinateurs qui sont joints à un domaine géré de toohello. conteneur des « Utilisateurs AADDC » Hello comprend des utilisateurs et groupes dans le locataire Azure AD de hello. Il peut parfois être des comptes de service nécessaires toocreate hello géré domaine toodeploy des charges de travail. Pour cela, vous pouvez créer une unité d’organisation personnalisé (OU) sur un domaine géré de hello et créer des comptes de service dans cette unité d’organisation. Cet article vous montre comment toocreate une unité d’organisation dans votre domaine géré.

## <a name="before-you-begin"></a>Avant de commencer
tâches de hello tooperform répertoriées dans cet article, vous devez :

1. Un **abonnement Azure**valide.
2. Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.
3. **Les Services de domaine Active Directory Azure** doit être activée pour le répertoire de hello Azure AD. Si vous n’avez pas encore fait, suivez toutes les tâches de hello présentées dans hello [guide Mise en route](active-directory-ds-getting-started.md).
4. Un ordinateur virtuel à un domaine à partir duquel vous administrez hello Azure AD les Services de domaine gérés domaine. Si vous n’avez pas cet un ordinateur virtuel, suivez toutes les tâches hello décrites dans l’article hello intitulé [joindre un domaine géré du tooa d’ordinateur virtuel Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Vous avez besoin des informations d’identification hello d’un **le groupe 'Administrateurs du contrôleur de domaine AAD' toohello utilisateur compte appartenant** dans votre annuaire, toocreate une unité d’organisation personnalisée sur votre domaine géré.

## <a name="install-ad-administration-tools-on-a-domain-joined-virtual-machine-for-remote-administration"></a>Installer les outils d’administration Active Directory sur une machine virtuelle jointe à un domaine à des fins de gestion à distance
Domaines gérés des Services de domaine Active Directory Azure peuvent être gérés à distance à l’aide des outils d’administration Active Directory familiers tels que hello Active Directory Administrative Center (ADAC) ou Active Directory PowerShell. Les administrateurs clients ne disposent pas de contrôleurs de privilèges tooconnect toodomain sur hello le domaine géré via le Bureau à distance. tooadminister hello domaine géré, installez la fonctionnalité des outils administration hello AD sur un domaine géré de toohello joints à un ordinateur virtuel. Consultez l’article toohello intitulé [administrer un domaine géré des Services de domaine Active Directory de Azure](active-directory-ds-admin-guide-administer-domain.md) pour obtenir des instructions.

## <a name="create-an-organizational-unit-on-hello-managed-domain"></a>Créer une unité d’organisation sur un domaine géré de hello
Maintenant que les outils d’administration hello Active Directory sont installés sur hello domaine joints à un ordinateur virtuel, nous pouvons utiliser une unité d’organisation toocreate de ces outils sur le domaine de hello géré. Effectuez hello comme suit :

> [!NOTE]
> Uniquement les membres du groupe de « Administrateurs de contrôleur de domaine AAD » hello ont hello toocreate des privilèges requis, une unité d’organisation personnalisée. Veillez à effectuer hello en tant qu’utilisateur qui appartient le groupe de toothis comme suit.
>
>

1. À partir de l’écran d’accueil hello, cliquez sur **outils d’administration**. Vous devez voir les outils d’administration hello AD installés sur l’ordinateur virtuel de hello.

    ![Outils d’administration installés sur le serveur](./media/active-directory-domain-services-admin-guide/install-rsat-admin-tools-installed.png)
2. Cliquez sur **Centre d’administration Active Directory**.

    ![Centre d'administration Active Directory](./media/active-directory-domain-services-admin-guide/adac-overview.png)
3. domaine de hello tooview, cliquez sur le nom de domaine hello dans le volet de gauche hello (par exemple, « contoso100.com »).

    ![ADAC - Affichage du domaine](./media/active-directory-domain-services-admin-guide/create-ou-adac-overview.png)
4. Sur le côté droit de hello **tâches** volet, cliquez sur **nouveau** sous le nœud de nom de domaine hello. Dans cet exemple, nous cliquons sur **nouveau** sous le nœud de 'contoso100(local)' hello sur droite hello **tâches** volet.

    ![ADAC - Nouvelle unité d’organisation](./media/active-directory-domain-services-admin-guide/create-ou-adac-new-ou.png)
5. Vous devez voir hello option toocreate une unité d’organisation. Cliquez sur **unité d’organisation** toolaunch hello **créer une unité d’organisation** boîte de dialogue.
6. Bonjour **créer une unité d’organisation** boîte de dialogue, spécifiez un **nom** pour hello nouvelle unité d’organisation. Fournir une brève description de l’unité d’organisation de hello. Vous pouvez également définir hello **géré par** champ hello unité d’organisation. toocreate hello d’unité d’organisation personnalisée, cliquez sur **OK**.

    ![ADAC - Boîte de dialogue Créer une unité d’organisation](./media/active-directory-domain-services-admin-guide/create-ou-dialog.png)
7. Hello nouvellement créé unité d’organisation doit maintenant apparaître dans hello centre d’administration Active Directory (ADAC).

    ![ADAC - Unité d’organisation créée](./media/active-directory-domain-services-admin-guide/create-ou-done.png)

## <a name="permissionssecurity-for-newly-created-ous"></a>Sécurité/autorisations associées aux nouvelles unités d’organisation
Par défaut, l’utilisateur hello (membre du groupe de hello « administrateurs de contrôleur de domaine AAD ») qui a créé le hello unité d’organisation personnalisée bénéficie des privilèges d’administrateur (contrôle total) sur hello unité d’organisation. Hello utilisateur peut ensuite continuez et accorder aux utilisateurs de privilèges tooother ou au groupe de « Administrateurs de contrôleur de domaine AAD » toohello comme vous le souhaitez. Comme indiqué dans hello suivant capture d’écran, hello utilisateur 'bob@domainservicespreview.onmicrosoft.com' auquel nouvelle unité d’organisation 'MyCustomOU' hello créé est accordée à un contrôle total sur elle.

 ![ADAC - Sécurité de la nouvelle UO](./media/active-directory-domain-services-admin-guide/create-ou-permissions.png)

## <a name="notes-on-administering-custom-ous"></a>Remarques sur l’administration des unités d’organisation (UO) personnalisées
Maintenant que vous avez créé une UO personnalisée, vous pouvez créer des utilisateurs, des groupes, des ordinateurs et des comptes de service dans cette dernière. Impossible de déplacer les utilisateurs ou groupes de hello les unités d’organisation toocustom 'Utilisateurs AADDC' unité d’organisation.

> [!WARNING]
> Les comptes de service, groupes, objets ordinateur et comptes d’utilisateur que vous créez dans un UO personnalisée ne sont pas disponible sur votre client Azure AD. En d’autres termes, ces objets ne s’affichent pas à l’aide des API d’Azure AD Graph hello ou Bonjour interface utilisateur Azure AD. Ces objets sont uniquement disponibles dans votre domaine géré par les services de domaine Azure AD.
>
>

## <a name="related-content"></a>Contenu connexe
* [Administrer un domaine géré par les services de domaine Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
* [Configurer la stratégie de groupe sur un domaine géré](active-directory-ds-admin-guide-administer-group-policy.md)
* [Centre d’administration Active Directory : Prise en main](https://technet.microsoft.com/library/dd560651.aspx)
* [Guide pas à pas des comptes de service (éventuellement en anglais)](https://technet.microsoft.com/library/dd548356.aspx)
