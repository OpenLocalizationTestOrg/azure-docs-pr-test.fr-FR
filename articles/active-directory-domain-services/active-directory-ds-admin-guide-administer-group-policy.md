---
title: "Azure Active Directory Domain Services : administrer la stratégie de groupe sur des domaines gérés | Microsoft Docs"
description: "Administrer la stratégie de groupe sur les domaines gérés par les services de domaine Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d56ebf27e3015a7f3385ac5a4ddd77ea2c88387f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-group-policy-on-an-azure-ad-domain-services-managed-domain"></a>Administrer la stratégie de groupe sur un domaine géré par les services de domaine Azure Active Directory
Azure Active Directory Domain Services inclut des objets de stratégie de groupe (GPO) intégré pour les conteneurs de « AADDC utilisateurs » et « Ordinateurs AADDC » hello. Vous pouvez personnaliser ces tooconfigure intégrés de la stratégie de groupe Stratégie de groupe sur un domaine géré de hello. En outre, les membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent créer leurs propres unités d’organisation personnalisées dans le domaine géré de hello. Ils peuvent également créer des objets stratégie de groupe personnalisé et les lier des toothese personnalisé unités d’organisation. Les utilisateurs qui appartiennent toohello 'Administrateurs du contrôleur de domaine AAD' groupe bénéficient de privilèges d’administration de stratégie de groupe sur un domaine géré de hello.

## <a name="before-you-begin"></a>Avant de commencer
tâches de hello tooperform répertoriées dans cet article, vous devez :

1. Un **abonnement Azure**valide.
2. Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.
3. **Les Services de domaine Active Directory Azure** doit être activée pour le répertoire de hello Azure AD. Si vous n’avez pas encore fait, suivez toutes les tâches de hello présentées dans hello [guide Mise en route](active-directory-ds-getting-started.md).
4. A **appartenant à un domaine un ordinateur virtuel** à partir de laquelle vous administrez hello domaine géré des Services de domaine Active Directory de Azure. Si vous n’avez pas cet un ordinateur virtuel, suivez toutes les tâches hello décrites dans l’article hello intitulé [joindre un domaine géré du tooa d’ordinateur virtuel Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Vous avez besoin des informations d’identification hello d’un **le groupe 'Administrateurs du contrôleur de domaine AAD' toohello utilisateur compte appartenant** dans votre annuaire, tooadminister stratégie de groupe pour votre domaine géré.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-group-policy-for-hello-managed-domain"></a>Tâche 1 : configurer un tooremotely appartenant à un domaine un ordinateur virtuel administrer la stratégie de groupe pour le domaine géré de hello
Domaines gérés des Services de domaine Active Directory Azure peuvent être gérés à distance à l’aide des outils d’administration Active Directory familiers tels que hello Active Directory Administrative Center (ADAC) ou Active Directory PowerShell. De même, la stratégie de groupe pour le domaine géré de hello peut être administré à distance à l’aide des outils d’administration de stratégie de groupe hello.

Administrateurs dans votre annuaire Azure AD n’ont pas de contrôleurs de privilèges tooconnect toodomain sur hello le domaine géré via le Bureau à distance. Membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent administrer stratégie de groupe pour les domaines gérés à distance. Ils peuvent utiliser les outils de la stratégie de groupe sur un domaine géré toohello jointes de l’ordinateur client Windows Server. Outils de stratégie de groupe peuvent être installés comme partie de la fonctionnalité facultative de hello gestion de stratégie de groupe sur les ordinateurs serveur et client Windows joints à un domaine géré de toohello.

tâche première Hello est tooprovision une machine virtuelle Windows Server qui est le domaine géré de toohello jointes. Pour obtenir des instructions, consultez l’article toohello intitulé [joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-group-policy-tools-on-hello-virtual-machine"></a>Tâche 2 : outils de stratégie de groupe de l’installation sur l’ordinateur virtuel de hello
Effectuer hello suivant des outils d’Administration de stratégie de groupe d’étapes tooinstall hello sur l’ordinateur virtuel de joints à un domaine hello.

1. Accédez trop**virtuels** nœud Bonjour portail Azure classic. Sélectionnez l’ordinateur virtuel de hello vous avez créé dans la tâche 1, cliquez sur **Connect** sur la barre de commandes hello bas hello de fenêtre hello.

    ![Connecter l’ordinateur virtuel de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portail classique de Hello vous invite tooopen ou enregistrer un fichier avec l’extension '.rdp', qui est utilisé tooconnect toohello virtual machine. Cliquez sur le fichier de hello lorsqu’il a terminé le téléchargement.
3. À l’invite de connexion hello, utilisez des références de hello d’un utilisateur appartenant groupe 'Administrateurs du contrôleur de domaine AAD' de toohello. Par exemple, nous utilisons 'bob@domainservicespreview.onmicrosoft.com' dans le cas présent.
4. À partir de l’écran d’accueil hello, ouvrez **le Gestionnaire de serveur**. Cliquez sur **Ajout de rôles et fonctionnalités** dans le volet central de hello de la fenêtre du Gestionnaire de serveur hello.

    ![Lancer le gestionnaire de serveur sur la machine virtuelle](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager.png)
5. Sur hello **avant de commencer** page Hello **Assistant Ajouter des rôles et fonctionnalités**, cliquez sur **suivant**.

    ![Page Avant de commencer](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-begin.png)
6. Sur hello **le Type d’Installation** page, laissez l’option hello **installation basée sur un rôle ou une fonctionnalité** activée, puis cliquez sur **suivant**.

    ![Page Type d’installation](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-type.png)
7. Sur hello **sélection du serveur** page, sélectionnez l’ordinateur virtuel en cours de hello hello pool de serveurs, puis cliquez sur **suivant**.

    ![Page Sélection du serveur](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-server.png)
8. Sur hello **rôles serveur** , cliquez sur **suivant**. Nous permet d’ignorer cette page, car nous ne sommes pas installer les rôles sur le serveur de hello.
9. Sur hello **fonctionnalités** page, sélectionnez hello **Group Policy Management** fonctionnalité.

    ![Page Fonctionnalités](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management.png)
10. Sur hello **Confirmation** , cliquez sur **installer** fonctionnalité de gestion de stratégie de groupe de hello tooinstall sur l’ordinateur virtuel de hello. Lorsque la fonctionnalité installation terminée, cliquez sur **fermer** tooexit hello **Ajout de rôles et fonctionnalités** Assistant.

    ![Page Confirmation](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-gp-management-confirmation.png)

## <a name="task-3---launch-hello-group-policy-management-console-tooadminister-group-policy"></a>Tâche 3 - lancer hello stratégie de groupe management console tooadminister stratégie de groupe
Vous pouvez utiliser la console de gestion de stratégie de groupe hello sur hello appartenant à un domaine un ordinateur virtuel tooadminister stratégie de groupe sur un domaine géré de hello.

> [!NOTE]
> Vous devez toobe un membre du groupe de hello « administrateurs de contrôleur de domaine AAD », tooadminister stratégie de groupe sur un domaine géré de hello.
>
>

1. À partir de l’écran d’accueil hello, cliquez sur **outils d’administration**. Vous devez voir hello **gestion des stratégies de groupe** console installée sur l’ordinateur virtuel de hello.

    ![Lancer la gestion des stratégies de groupe](./media/active-directory-domain-services-admin-guide/gp-management-installed.png)
2. Cliquez sur **gestion des stratégies de groupe** console de gestion des stratégies de groupe toolaunch hello.

    ![Console de stratégie de groupe](./media/active-directory-domain-services-admin-guide/gp-management-console.png)

## <a name="task-4---customize-built-in-group-policy-objects"></a>Tâche 4 : personnaliser les objets de stratégie de groupe intégrés
Il existe deux intégrés objets stratégie de groupe (GPO) - un pour les conteneurs de « Ordinateurs AADDC » et « Utilisateurs AADDC » hello dans votre domaine géré. Vous pouvez personnaliser ces stratégie de groupe de tooconfigure de stratégie de groupe sur un domaine géré de hello.

1. Bonjour **gestion des stratégies de groupe** de la console, cliquez sur tooexpand hello **forêt : contoso100.com** et **domaines** stratégies de groupe de nœuds toosee hello pour votre domaine géré.

    ![Objets de stratégie de groupe (GPO) intégrés](./media/active-directory-domain-services-admin-guide/builtin-gpos.png)
2. Vous pouvez personnaliser ces stratégies de groupe tooconfigure GPO intégrées sur votre domaine géré. Avec le bouton droit hello de stratégie de groupe, puis cliquez sur **modifier...**  toocustomize hello intégrés objet stratégie de groupe. outil d’éditeur de Configuration de stratégie de groupe Hello permet de vous toocustomize hello de stratégie de groupe.

    ![Modifier un GPO intégré](./media/active-directory-domain-services-admin-guide/edit-builtin-gpo.png)
3. Vous pouvez maintenant utiliser hello **éditeur de gestion de stratégie de groupe** tooedit hello intégrés objet stratégie de groupe de la console. Par exemple, hello suivant capture d’écran montre comment toocustomize hello intégré de stratégie de groupe « Ordinateurs AADDC ».

    ![Personnaliser un GPO](./media/active-directory-domain-services-admin-guide/gp-editor.png)

## <a name="task-5---create-a-custom-group-policy-object-gpo"></a>Tâche 5 : créer un objet de stratégie de groupe personnalisé
Vous pouvez créer ou importer vos propres objets de stratégie de groupe. Vous pouvez également lier personnalisée personnalisée tooa de stratégie de groupe unité d’organisation que vous avez créé dans votre domaine géré. Pour plus d’informations sur la création d’unités d’organisation personnalisées, consultez [Créer une unité d’organisation personnalisée sur un domaine géré](active-directory-ds-admin-guide-create-ou.md).

> [!NOTE]
> Vous devez toobe un membre du groupe de hello « administrateurs de contrôleur de domaine AAD », tooadminister stratégie de groupe sur un domaine géré de hello.
>
>

1. Bonjour **gestion des stratégies de groupe** de la console, cliquez sur tooselect votre unité d’organisation (UO) personnalisée. Avec le bouton droit hello unité d’organisation, puis cliquez sur **créer un objet GPO dans ce domaine et le lier ici...** .

    ![Créer un objet de stratégie de groupe personnalisé](./media/active-directory-domain-services-admin-guide/gp-create-gpo.png)
2. Spécifiez un nom pour le nouvel objet GPO de hello et cliquez sur **OK**.

    ![Spécifier un nom pour l’objet de stratégie de groupe](./media/active-directory-domain-services-admin-guide/gp-specify-gpo-name.png)
3. Un nouvel objet GPO est créé et lié tooyour personnalisé unité d’organisation. Avec le bouton droit hello de stratégie de groupe, puis cliquez sur **modifier...**  à partir du menu de hello.

    ![Objet de stratégie de groupe nouvellement créé](./media/active-directory-domain-services-admin-guide/gp-gpo-created.png)
4. Vous pouvez personnaliser les GPO hello qui vient d’être créé à l’aide de hello **éditeur de gestion de stratégie de groupe**.

    ![Personnaliser le nouvel objet de stratégie de groupe](./media/active-directory-domain-services-admin-guide/gp-customize-gpo.png)


Pour plus d’informations sur l’utilisation de la [Console de gestion de stratégie de groupe](https://technet.microsoft.com/library/cc753298.aspx), consultez le site Technet.

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administrer un domaine géré par les services de domaine Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
* [Console de gestion des stratégies de groupe](https://technet.microsoft.com/library/cc753298.aspx)
