---
title: "Version préliminaire des services de domaine Azure Active Directory : administrer DNS sur des domaines gérés | Microsoft Docs"
description: "Administrer DNS sur les domaines gérés par les services de domaine Azure Active Directory"
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
ms.openlocfilehash: f2085283649eadd3c9e89f708b0eecf10b2d7d70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="administer-dns-on-an-azure-ad-domain-services-managed-domain"></a>Gérer le serveur DNS sur un domaine géré par les services de domaine Azure Active Directory
Azure Active Directory Domain Services inclut un serveur DNS (résolution de nom de domaine) qui fournit la résolution DNS pour le domaine géré de hello. Parfois, vous devrez peut-être tooconfigure DNS sur le domaine de hello géré. Vous devrez peut-être toocreate les enregistrements DNS pour les ordinateurs qui ne sont pas toohello joint à un domaine, configurez les adresses IP virtuelles pour des équilibreurs de charge ou configurer des redirecteurs DNS externes. Pour cette raison, les utilisateurs qui appartiennent toohello 'Administrateurs du contrôleur de domaine AAD' groupe bénéficient des privilèges d’administration DNS sur un domaine géré de hello.

## <a name="before-you-begin"></a>Avant de commencer
tâches de hello tooperform répertoriées dans cet article, vous devez :

1. Un **abonnement Azure**valide.
2. Un **répertoire Azure AD** , synchronisé avec un répertoire local ou un répertoire cloud uniquement.
3. **Les Services de domaine Active Directory Azure** doit être activée pour le répertoire de hello Azure AD. Si vous n’avez pas encore fait, suivez toutes les tâches de hello présentées dans hello [guide Mise en route](active-directory-ds-getting-started.md).
4. A **appartenant à un domaine un ordinateur virtuel** à partir de laquelle vous administrez hello domaine géré des Services de domaine Active Directory de Azure. Si vous n’avez pas cet un ordinateur virtuel, suivez toutes les tâches hello décrites dans l’article hello intitulé [joindre un domaine géré du tooa d’ordinateur virtuel Windows](active-directory-ds-admin-guide-join-windows-vm.md).
5. Vous avez besoin des informations d’identification hello d’un **le groupe 'Administrateurs du contrôleur de domaine AAD' toohello utilisateur compte appartenant** dans votre annuaire, tooadminister DNS pour votre domaine géré.

<br>

## <a name="task-1---provision-a-domain-joined-virtual-machine-tooremotely-administer-dns-for-hello-managed-domain"></a>Tâche 1 : configurer un tooremotely appartenant à un domaine un ordinateur virtuel administrer le DNS pour le domaine géré de hello
Domaines gérés des Services de domaine Active Directory Azure peuvent être gérés à distance à l’aide des outils d’administration Active Directory familiers tels que hello Active Directory Administrative Center (ADAC) ou Active Directory PowerShell. De même, DNS pour le domaine géré de hello peut être administré à distance à l’aide des outils d’administration de serveur DNS hello.

Administrateurs dans votre annuaire Azure AD n’ont pas de contrôleurs de privilèges tooconnect toodomain sur hello le domaine géré via le Bureau à distance. Membres hello ' AAD contrôleur de domaine » du groupe des administrateurs peuvent gérer DNS pour les domaines gérés à distance à l’aide des outils de serveur DNS à partir d’un ordinateur client Windows Server qui est le domaine géré de toohello jointes. Outils de serveur DNS peuvent être installés dans le cadre de la fonctionnalité facultative de hello outils d’Administration de serveur distant (RSAT) sur Windows Server et les ordinateurs clients joints à un domaine de toohello géré.

tâche première Hello est tooprovision une machine virtuelle Windows Server qui est le domaine géré de toohello jointes. Pour obtenir des instructions, consultez l’article toohello intitulé [joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server](active-directory-ds-admin-guide-join-windows-vm.md).

## <a name="task-2---install-dns-server-tools-on-hello-virtual-machine"></a>Tâche 2 - Outils d’installer un serveur DNS sur l’ordinateur virtuel de hello
Effectuer hello suivant les étapes tooinstall hello DNS outils d’Administration sur l’ordinateur virtuel de joints à un domaine hello. Pour en savoir plus sur [l’installation et l’utilisation des Outils d’administration de serveur distant](https://technet.microsoft.com/library/hh831501.aspx), voir TechNet.

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
9. Sur hello **fonctionnalités** , cliquez sur tooexpand hello **outils d’Administration de serveur distant** nœud puis cliquez sur tooexpand hello **outils d’Administration de rôles** nœud. Sélectionnez **outils du serveur DNS** fonctionnalité à partir de la liste de hello des outils d’administration de rôles.

    ![Page Fonctionnalités](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-tools.png)
10. Sur hello **Confirmation** , cliquez sur **installer** des fonctionnalités des outils de serveur DNS hello tooinstall sur l’ordinateur virtuel de hello. Lorsque la fonctionnalité installation terminée, cliquez sur **fermer** tooexit hello **Ajout de rôles et fonctionnalités** Assistant.

    ![Page Confirmation](./media/active-directory-domain-services-admin-guide/install-rsat-server-manager-add-roles-dns-confirmation.png)

## <a name="task-3---launch-hello-dns-management-console-tooadminister-dns"></a>Tâche 3 - lancer hello DNS management console tooadminister DNS
Maintenant que la fonctionnalité est installée sur les outils du serveur DNS hello hello virtuels joints à un domaine, nous pouvons utiliser hello DNS outils tooadminister DNS sur le domaine de hello géré.

> [!NOTE]
> Vous devez toobe un membre du groupe de hello « administrateurs de contrôleur de domaine AAD », tooadminister DNS sur un domaine géré de hello.
>
>

1. À partir de l’écran d’accueil hello, cliquez sur **outils d’administration**. Vous devez voir hello **DNS** console installée sur l’ordinateur virtuel de hello.

    ![Outils d’administration - Console DNS](./media/active-directory-domain-services-admin-guide/install-rsat-dns-tools-installed.png)
2. Cliquez sur **DNS** console de gestion DNS toolaunch hello.
3. Bonjour **connecter tooDNS Server** boîte de dialogue, cliquez sur option hello intitulée **hello suite ordinateur**et entrez le nom de domaine DNS hello de hello, domaine géré (par exemple, « contoso100.com »).

    ![Console DNS - se connecter toodomain](./media/active-directory-domain-services-admin-guide/dns-console-connect-to-domain.png)
4. Hello DNS Console connecte toohello les domaine géré.

    ![Console DNS - Administration du domaine](./media/active-directory-domain-services-admin-guide/dns-console-managed-domain.png)
5. Vous pouvez maintenant utiliser des entrées DNS tooadd hello DNS console sur les ordinateurs d’un réseau virtuel de hello dans lequel vous avez activé les Services de domaine AAD.

> [!WARNING]
> Soyez prudent lors de l’administration de DNS pour hello gérés à l’aide des outils d’administration DNS de domaine. Vérifiez que vous avez **ne pas supprimer ou modifier les enregistrements DNS intégrés hello qui sont utilisés par les Services de domaine dans le domaine de hello**. Les enregistrements DNS intégrés incluent les enregistrements DNS de domaine, les enregistrements de serveur de noms et d’autres enregistrements utilisés pour le lieu du contrôleur de domaine. Si vous modifiez ces enregistrements, les services de domaine sont interrompues sur le réseau virtuel de hello.
>
>

Consultez hello [outils DNS de l’article sur Technet](https://technet.microsoft.com/library/cc753579.aspx) pour plus d’informations sur la gestion DNS.

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Joindre un domaine des Services de domaine Active Directory de Azure géré tooan de machine virtuelle Windows Server](active-directory-ds-admin-guide-join-windows-vm.md)
* [Administrer un domaine géré par les services de domaine Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
* [Outils d’administration DNS](https://technet.microsoft.com/library/cc753579.aspx)
