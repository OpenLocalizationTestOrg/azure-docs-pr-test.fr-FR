---
title: "aaaInstall IIS sur votre première machine virtuelle de Windows | Documents Microsoft"
description: "Faire des essais avec votre première machine virtuelle de Windows par l’installation d’IIS et l’ouverture à l’aide du port 80 hello portail Azure."
keywords: 
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 6334ea45-db6b-4e08-abb5-1f98927ebc34
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/06/2016
ms.author: cynthn
ms.openlocfilehash: 7cfed6197df058c4569d111ee88961da7c6fe0b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="experiment-with-installing-a-role-on-your-windows-vm"></a>Tester l’installation d’un rôle sur votre machine virtuelle Windows
Une fois que vous avez votre première machine virtuelle (VM) haut et en cours d’exécution, vous pouvez déplacer sur tooinstalling logiciels et services. Pour ce didacticiel, nous allons toouse le Gestionnaire de serveur sur la machine virtuelle Windows Server de hello tooinstall IIS. Ensuite, nous allons créer un groupe de sécurité réseau (NSG) à l’aide du port 80 tooIIS trafic hello tooopen portail Azure. 

Si vous n’avez pas encore créé votre première machine virtuelle, vous devez revenir en arrière trop[créer votre première machine virtuelle de Windows Bonjour Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) avant de poursuivre ce didacticiel.

## <a name="make-sure-hello-vm-is-running"></a>Vérifiez que hello que machine virtuelle est en cours d’exécution
1. Ouvrez hello [portail Azure](https://portal.azure.com).
2. Dans le menu du hub hello, cliquez sur **virtuels**. Sélectionnez hello virtuels à partir de la liste de hello.
3. Si l’état de hello est **arrêté (désalloué)**, cliquez sur hello **Démarrer** bouton sur hello **Essentials** Panneau de hello machine virtuelle. Si l’état de hello est **en cours d’exécution**, vous pouvez déplacer sur l’étape suivante de toohello.

## <a name="connect-toohello-virtual-machine-and-sign-in"></a>Connecter l’ordinateur virtuel de toohello et se connecter
1. Dans le menu du hub hello, cliquez sur **virtuels**. Sélectionnez hello virtuels à partir de la liste de hello.
2. Dans le panneau hello pour la machine virtuelle de hello, cliquez sur **connexion**. Crée et télécharge un fichier de protocole Bureau à distance (fichier .rdp) qui s’apparente à un ordinateur de tooyour tooconnect contextuel. Vous pourriez bureau de tooyour fichier toosave hello pour faciliter l’accès. **Ouvrez** cette tooyour de tooconnect fichier machine virtuelle.
   
    ![Capture d’écran de hello montrant portail Azure comment tooconnect tooyour machine virtuelle](./media/hero-role/connect.png)
3. Vous obtenez un avertissement qui .rdp hello est un serveur de publication inconnu. C’est normal. Dans la fenêtre du Bureau à distance hello, cliquez sur **Connect** toocontinue.
   
    ![Capture d’écran d’un avertissement relatif à un éditeur inconnu](./media/hero-role/rdp-warn.png)
4. Dans la fenêtre de sécurité Windows hello, le nom d’utilisateur de type hello et un mot de passe pour le compte local hello que vous avez créé lorsque vous avez créé hello machine virtuelle. nom d’utilisateur Hello est entré en tant que *vmname*&#92; *nom d’utilisateur*, puis cliquez sur **OK**.
   
    ![Capture d’écran de saisie du nom d’ordinateur virtuel hello, nom d’utilisateur et mot de passe](./media/hero-role/credentials.png)
5. Vous obtenez un avertissement de certificat hello ne peut pas être vérifié. C’est normal. Cliquez sur **Oui** tooverify hello l’identité de l’ordinateur virtuel de hello et terminer la session.
   
   ![Capture d’écran montrant un message à propos de vérification d’identité hello Hello machine virtuelle](./media/hero-role/cert-warning.png)

Si vous exécutez dans tootrouble lorsque vous essayez de tooconnect, consultez [tooa de connexions de résoudre les problèmes de bureau à distance basé sur Windows Azure Virtual Machine](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="install-iis-on-your-vm"></a>Installation d’IIS sur votre machine virtuelle
Maintenant que vous êtes connecté toohello machine virtuelle, nous allons installer un rôle de serveur afin que vous pouvez faire des essais plus.

1. Si ce n’est pas déjà fait, ouvrez le **Gestionnaire de serveur** . Cliquez sur hello **Démarrer** menu, puis sur **le Gestionnaire de serveur**.
2. Dans **le Gestionnaire de serveur**, sélectionnez **serveur Local** hello volet de gauche. 
3. Dans le menu de hello, sélectionnez **gérer** > **Ajout de rôles et fonctionnalités**.
4. Dans Ajouter des rôles hello Assistant et fonctionnalités, sur hello **le Type d’Installation** choisissez **installation basée sur un rôle ou une fonctionnalité**, puis cliquez sur **suivant**.
   
    ![Onglet Capture d’écran montrant hello Assistant Ajouter des rôles et fonctionnalités de Type d’Installation](./media/hero-role/role-wizard.png)
5. Sélectionnez hello VM hello pool de serveurs, cliquez sur **suivant**.
6. Sur hello **rôles serveur** page, sélectionnez **serveur Web (IIS)**.
   
    ![Onglet Capture d’écran montrant hello Assistant Ajouter des rôles et fonctionnalités pour les rôles de serveur](./media/hero-role/add-iis.png)
7. Bonjour contextuelle sur l’ajout de fonctionnalités requises pour IIS, assurez-vous que **les outils d’administration** est sélectionné, puis cliquez sur **ajouter des fonctionnalités**. Lorsque hello contextuelle se ferme, cliquez sur **suivant** dans l’Assistant de hello.
   
    ![Capture d’écran contextuel tooconfirm ajouter le rôle IIS hello](./media/hero-role/confirm-add-feature.png)
8. Dans la page de composants hello, cliquez sur **suivant**.
9. Sur hello **rôle de serveur Web (IIS)** , cliquez sur **suivant**. 
10. Sur hello **les Services de rôle** , cliquez sur **suivant**. 
11. Sur hello **Confirmation** , cliquez sur **installer**. 
12. Lors de l’installation de hello est terminée, cliquez sur **fermer** sur l’Assistant de hello.

## <a name="open-port-80"></a>Ouverture du port 80
Dans l’ordre pour votre tooaccept de machine virtuelle du trafic entrant sur le port 80, vous devez tooadd un groupe de sécurité réseau toohello règle de trafic entrant. 

1. Ouvrez hello [portail Azure](https://portal.azure.com).
2. Dans **virtuels** sélectionnez hello machine virtuelle que vous avez créé.
3. Dans paramètres de machines virtuelles hello, sélectionnez **interfaces réseau** et puis sélectionnez hello interface réseau existante.
   
    ![Capture d’écran de configuration de machine virtuelle hello pour hello interfaces réseau](./media/hero-role/network-interface.png)
4. Dans **Essentials** pour l’interface de réseau hello, cliquez sur hello **groupe de sécurité réseau**.
   
    ![Capture d’écran de section d’Essentials hello pour l’interface de réseau hello](./media/hero-role/select-nsg.png)
5. Bonjour **Essentials** panneau pour hello groupe de sécurité réseau, vous devez disposer d’une valeur par défaut existante règle de trafic entrant **rdp par défaut autoriser** qui vous permet de toolog dans toohello machine virtuelle. Vous allez ajouter un autre trafic IIS tooallow règle de trafic entrant. Cliquez sur **Règle de sécurité de trafic entrant**.
   
    ![Capture d’écran montrant la section Essentials hello hello NSG](./media/hero-role/inbound.png)
6. Dans **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**.
   
    ![Capture d’écran hello bouton tooadd une règle de sécurité](./media/hero-role/add-rule.png)
7. Dans **Règles de sécurité de trafic entrant**, cliquez sur **Ajouter**. Type **80** dans hello la plage de ports et assurez-vous que **autoriser** est sélectionnée. Une fois ces opérations effectuées, cliquez sur **OK**.
   
    ![Capture d’écran hello bouton tooadd une règle de sécurité](./media/hero-role/port-80.png)

Pour plus d’informations sur les groupes de sécurité réseau, des règles entrantes et sortantes, consultez [autoriser un accès externe tooyour machine virtuelle en utilisant hello portail Azure](nsg-quickstart-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

## <a name="connect-toohello-default-iis-website"></a>Connecter le site Web IIS de toohello par défaut
1. Bonjour portail Azure, cliquez sur **virtuels** , puis sélectionnez votre machine virtuelle.
2. Bonjour **Essentials** panneau, copiez votre **adresse IP publique**.
   
    ![Capture d’écran montrant où toofind hello adresse IP publique de votre machine virtuelle](./media/hero-role/ipaddress.png)
3. Ouvrez un navigateur et dans la barre d’adresses hello, tapez votre adresse IP publique comme suit : http://<publicIPaddress> et cliquez sur **entrée** toogo toothat adresse.
4. Votre navigateur doit ouvrir la page web de hello par défaut IIS. Voici ce à quoi elle ressemble :
   
    ![Capture d’écran montrant la page par défaut IIS hello ressemble dans un navigateur](./media/hero-role/iis-default.png)

## <a name="next-steps"></a>Étapes suivantes
* Vous pouvez également faire des essais avec [y attacher un disque de données](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) tooyour virtuels. Les disques de données fournissent plus de stockage pour votre machine virtuelle.

