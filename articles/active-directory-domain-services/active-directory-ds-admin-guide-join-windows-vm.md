---
title: "Azure Active Directory Domain Services : Joindre un domaine géré de machine virtuelle Windows Server tooa | Documents Microsoft"
description: Joindre une machine virtuelle Windows Server des Services de domaine Active Directory de tooAzure
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 74dbdb33-05db-4d47-badc-0d7bb6d0c8cb
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: 1e85833b42bd51f3b3df067d6c5b69253459bec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="join-a-windows-server-virtual-machine-tooa-managed-domain"></a>Joindre un domaine géré du tooa d’ordinateur virtuel Windows Server
> [!div class="op_single_selector"]
> * [Portail Azure Classic - Windows](active-directory-ds-admin-guide-join-windows-vm.md)
> * [PowerShell - Windows](active-directory-ds-admin-guide-join-windows-vm-classic-powershell.md)
>
>

<br>

Cet article explique comment toojoin un tooan de Windows Server 2012 R2 en cours d’exécution des Services de domaine Active Directory Azure ordinateur virtuel géré domaine, à l’aide de hello portail Azure classic.

## <a name="step-1-create-hello-windows-server-virtual-machine"></a>Étape 1 : Créer la machine virtuelle de Windows Server hello
Suivez les instructions de hello décrites dans hello [créer une machine virtuelle exécutant Windows Bonjour portail Azure classic](../virtual-machines/windows/classic/tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) didacticiel. Il est important de tooensure cet ordinateur virtuel nouvellement créé est joint toohello même réseau virtuel dans lequel vous avez activé les Services de domaine Active Directory de Azure. Hello, option de « Création rapide » ne permet pas de vous toojoin hello tooa virtuel réseau d’ordinateurs virtuels. Par conséquent, vous avez besoin d’ordinateur virtuel de toouse hello 'À partir de la galerie' option toocreate hello.

Effectuer hello suivant les étapes toocreate un réseau virtuel toohello joints à un ordinateur virtuel Windows dans lequel vous avez activé les Services de domaine Active Directory de Azure.

1. Bonjour portail Azure classic, sur la barre de commandes hello bas hello de fenêtre hello, cliquez sur **nouveau**.
2. Sous **Calculer**, cliquez sur **Machine virtuelle**, puis sur **À partir de la galerie**.
3. premier écran de Hello vous permet de **choisir une Image** pour votre machine virtuelle à partir de la liste de hello des images disponibles. Choisissez l’image appropriée de hello.

    ![Sélectionner une image](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-image.png)
4. deuxième écran de Hello vous permet de choisir un nom d’ordinateur, le taille et le nom d’utilisateur d’administration et le mot de passe. Utilisez des niveaux de hello et taille requise toorun votre application ou la charge de travail. nom d’utilisateur Hello que vous choisissez ici est un utilisateur d’administrateur local sur l’ordinateur de hello. Ne saisissez pas les informations d’identification associées à un compte d’utilisateur de domaine ici.

    ![Configurer la machine virtuelle](./media/active-directory-domain-services-admin-guide/create-windows-vm-config.png)
5. troisième écran de Hello vous permet de configurer des ressources pour la mise en réseau, stockage et la disponibilité. Veillez à sélectionner de réseau virtuel de hello dans lequel vous avez activé les Services de domaine Active Directory de Azure à partir de hello **régions ou d’affinités groupe/réseau virtuel** liste déroulante. Spécifiez un **nom DNS du Service Cloud** en fonction de la machine virtuelle de hello.

    ![Sélectionner un réseau virtuel pour la machine virtuelle](./media/active-directory-domain-services-admin-guide/create-windows-vm-select-vnet.png)

   > [!WARNING]
   > Assurez-vous que vous joignez hello machine virtuelle toohello même réseau virtuel dans lequel vous avez activé les Services de domaine Active Directory de Azure. Par conséquent, hello virtual machine peut « voir » le domaine de hello et effectuer des tâches telles que la jonction de domaine de hello. Si vous choisissez la machine virtuelle de hello toocreate dans un autre réseau virtuel, connectez-vous à ce réseau virtuel à réseau virtuel toohello dans lequel vous avez activé les Services de domaine Active Directory de Azure.
   >
   >
6. écran quatrième Hello vous permet d’installer l’Agent de machine virtuelle de hello et configurer certaines extensions disponibles de hello.

    ![Terminé](./media/active-directory-domain-services-admin-guide/create-windows-vm-done.png)
7. Après la création de la machine virtuelle de hello, portail classique de hello répertorie hello machine virtuelle sous hello **virtuels** nœud. Machine virtuelle de hello et le service cloud sont démarrées automatiquement et leur état est répertorié en tant que **en cours d’exécution**.

    ![Machine virtuelle opérationnelle](./media/active-directory-domain-services-admin-guide/create-windows-vm-running.png)

## <a name="step-2-connect-toohello-windows-server-virtual-machine-using-hello-local-administrator-account"></a>Étape 2 : Se connecter la machine virtuelle de toohello Windows Server à l’aide du compte d’administrateur local hello
Maintenant, nous connecter la machine virtuelle de Windows Server toohello nouvellement créé, toojoin il toohello domaine. Utilisez les informations d’identification de l’administrateur local hello que vous avez spécifié lors de la création d’ordinateur virtuel de hello, tooconnect tooit.

Effectuer hello suivant les étapes tooconnect toohello virtual machine.

1. Accédez trop**virtuels** nœud dans le portail classique de hello. Sélectionnez la machine virtuelle de hello vous avez créé à l’étape 1, cliquez sur **Connect** sur la barre de commandes hello bas hello de fenêtre hello.

    ![Connecter l’ordinateur virtuel de tooWindows](./media/active-directory-domain-services-admin-guide/connect-windows-vm.png)
2. portail classique de Hello vous invite tooopen ou enregistrer un fichier avec l’extension '.rdp', qui est utilisé tooconnect toohello virtual machine. Cliquez sur fichier de hello tooopen lorsqu’il a terminé le téléchargement.
3. À l’invite de connexion hello, entrez votre **informations d’identification d’administrateur local**, que vous avez spécifiés lors de la création d’ordinateur virtuel de hello. Nous avons utilisé « localhost\mahesh » dans cet exemple.

À ce stade, vous devez être connecté en toohello nouvellement créé la machine virtuelle de Windows à l’aide des informations d’identification d’administrateur. étape suivante de Hello est domaine toohello de toojoin hello machine virtuelle.

## <a name="step-3-join-hello-windows-server-virtual-machine-toohello-aad-ds-managed-domain"></a>Étape 3 : Joindre le domaine géré des toohello AAD-DS machine virtuelle Windows Server hello
Effectuer hello suivant les étapes toojoin hello domaine Windows Server machine virtuelle toohello AAD-DS managé.

1. Se connecter toohello Windows Server comme indiqué dans l’étape 2. À partir de l’écran d’accueil hello, ouvrez **le Gestionnaire de serveur**.
2. Cliquez sur **serveur Local** dans la partie gauche de la fenêtre du Gestionnaire de serveur hello hello.

    ![Lancer le gestionnaire de serveur sur la machine virtuelle](./media/active-directory-domain-services-admin-guide/join-domain-server-manager.png)
3. Cliquez sur **groupe de travail** sous hello **propriétés** section. Bonjour **propriétés système** page de propriétés, cliquez sur **modification** domaine de hello toojoin.

    ![Page Propriétés système](./media/active-directory-domain-services-admin-guide/join-domain-system-properties.png)
4. Spécifiez le nom du domaine de votre domaine géré des Services de domaine Active Directory de Azure hello Bonjour **domaine** zone de texte et cliquez sur **OK**.

    ![Spécifiez hello domaine toobe joint](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-domain.png)
5. Vous est demandée tooenter votre domaine de hello toojoin informations d’identification. Vérifiez que vous avez **spécifier hello les informations d’identification pour un toohello d’appartenant aux administrateurs du contrôleur de domaine AAD utilisateur** groupe. Seuls les membres de ce groupe ont des privilèges toojoin machines toohello domaine géré.

    ![Spécifier les informations d’identification pour la jonction au domaine](./media/active-directory-domain-services-admin-guide/join-domain-system-properties-specify-credentials.png)
6. Vous pouvez spécifier des informations d’identification, que ce soit de hello suivant façons :

   * Format UPN : spécifiez le suffixe UPN de hello hello compte d’utilisateur, tel que configuré dans Azure AD. Dans cet exemple, le suffixe UPN hello utilisateur de hello 'bob' est 'bob@domainservicespreview.onmicrosoft.com'.
   * Format de SAMAccountName : vous pouvez spécifier le nom du compte hello au format de SAMAccountName hello. Dans cet exemple, l’utilisateur hello « bob » doit tooenter 'CONTOSO100\bob'.

     > [!NOTE]
     > **Nous recommandons d’utiliser les informations d’identification du toospecify format UPN hello.** Hello SAMAccountName peut être généré automatiquement si le préfixe de nom UPN d’un utilisateur est trop long (par exemple, 'joereallylongnameuser'). Si plusieurs utilisateurs ont le même préfixe de nom UPN (par exemple, « bob ») dans votre locataire Azure AD, leur format SAMAccountName peut être généré automatiquement par le service de hello de hello. Dans ces cas, format UPN de hello peut être utilisé de manière fiable toolog toohello domaine.
     >
     >
7. Une fois que la jonction de domaine réussit, vous voyez hello suivant le message de bienvenue toohello domaine. Redémarrez la machine virtuelle hello toocomplete d’opération de jointure de domaine hello.

    ![Domaine d’accueil toohello](./media/active-directory-domain-services-admin-guide/join-domain-done.png)

## <a name="troubleshooting-domain-join"></a>Résolution des problèmes de jonction de domaine
### <a name="connectivity-issues"></a>Problèmes de connectivité
Si hello virtual machine est domaine de hello toofind impossible, consultez toohello dépannage comme suit :

* Assurez-vous que l’ordinateur virtuel hello est connecté toohello même réseau virtuel que vous avez activé les Services de domaine. Si ce n’est pas le cas, hello et ordinateur virtuel ne peut pas tooconnect toohello domaine est donc le domaine de hello toojoin impossible.
* Si hello virtual machine est un réseau virtuel de tooanother connecté, assurez-vous que ce réseau virtuel est connecté toohello réseau virtuel dans lequel vous avez activé les Services de domaine.
* Essayez de domaine de hello tooping utilisant le nom de domaine hello de hello, domaine géré (par exemple, « contoso100.com ping »). Si vous n’êtes donc impossible toodo, essayez les adresses IP tooping hello pour le domaine de hello affiché sur la page de hello où vous avez activé les Services de domaine Active Directory de Azure (par exemple, « ping 10.0.0.4 »). Si vous utilisez l’adresse IP de hello tooping en mesure, mais pas les domaine hello, DNS peut être mal configuré. Vous ne pouvez pas configuré les adresses IP hello du domaine de hello en tant que serveurs DNS pour le réseau virtuel de hello.
* Essayez de le vidage hello le cache de résolution DNS sur l’ordinateur virtuel de hello (ipconfig /flushdns).

Si vous obtenez la boîte de dialogue toohello qui vous demande pour le domaine de hello toojoin informations d’identification, vous n’avez pas de problèmes de connectivité.

### <a name="credentials-related-issues"></a>Problèmes liés aux informations d’identification
Consultez toohello comme suit si vous rencontrez des difficultés avec les informations d’identification et du domaine hello toojoin impossible.

* Essayez d’utiliser les informations d’identification du toospecify format UPN hello. Hello SAMAccountName pour votre compte peut être généré automatiquement s’il existe plusieurs utilisateurs avec hello UPN même préfixe dans votre client ou si votre préfixe UPN est trop long. Par conséquent, format de SAMAccountName hello pour votre compte peut différer attendus ou utiliser dans votre domaine local.
* Essayez les informations d’identification de hello toouse d’un compte d’utilisateur qui appartient toohello « administrateurs de contrôleur de domaine AAD » groupe toojoin machines toohello domaine géré.
* Assurez-vous d’avoir [activé la synchronisation de mot de passe](active-directory-ds-getting-started-password-sync.md) conformément aux étapes hello décrites dans le guide de prise en main de hello.
* Assurez-vous que vous utilisez hello UPN de hello utilisateur tel que configuré dans Azure AD (par exemple, 'bob@domainservicespreview.onmicrosoft.com') toosign dans.
* Assurez-vous d’avoir attendu suffisamment longtemps pour toocomplete de synchronisation de mot de passe comme spécifié dans le guide de prise en main de hello.

## <a name="related-content"></a>Contenu connexe
* [Services de domaine Azure AD : guide de prise en main](active-directory-ds-getting-started.md)
* [Administrer un domaine géré par les services de domaine Azure Active Directory](active-directory-ds-admin-guide-administer-domain.md)
