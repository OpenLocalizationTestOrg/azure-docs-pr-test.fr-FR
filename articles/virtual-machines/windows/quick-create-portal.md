---
title: "aaaAzure démarrage rapide : créer un portail de machine virtuelle Windows | Documents Microsoft"
description: "Démarrage rapide avec Azure - Portail pour la création d’une machine virtuelle Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 5646ad51244db6d214c0121d1f7cc45c59f9a78b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-portal"></a>Créer une machine virtuelle Windows avec hello portail Azure

Machines virtuelles peuvent être créés via hello portail Azure. Cette méthode fournit une interface utilisateur basée sur navigateur pour créer et configurer des machines virtuelles et toutes les ressources liées. Cette procédure de démarrage rapide via la création d’une machine virtuelle et l’installation d’un serveur Web sur hello machine virtuelle.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure

Ouvrez une session dans toohello portail Azure à http://portal.azure.com.

## <a name="create-virtual-machine"></a>Create virtual machine

1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2. Sélectionnez **Compute**, puis **Windows Server 2016 Datacenter**. 

3. Entrez les informations de machine virtuelle hello. nom d’utilisateur Hello et le mot de passe entré ici est toolog utilisé dans la machine virtuelle de toohello. Lorsque vous avez terminé, cliquez sur **OK**.

    ![Entrez les informations de base sur votre machine virtuelle dans le panneau de portail hello](./media/quick-create-portal/create-windows-vm-portal-basic-blade.png)  

4. Sélectionnez une taille de hello machine virtuelle. Sélectionnez des tailles de plus, toosee **afficher toutes les** ou modifier hello **pris en charge le type de disque** filtre. 

    ![Capture d’écran montrant les tailles de machine virtuelle](./media/quick-create-portal/create-windows-vm-portal-sizes.png)  

5. Dans le panneau de paramètres hello, conserver les valeurs par défaut hello, puis cliquez sur **OK**.

6. Dans la page de résumé hello, cliquez sur **Ok** déploiement d’ordinateur virtuel toostart hello.

7. Hello machine virtuelle sera épinglé toohello tableau de bord de portail Azure. Une fois que la fin du déploiement de hello, panneau de résumé de machine virtuelle hello s’ouvre automatiquement.


## <a name="connect-toovirtual-machine"></a>Connecter toovirtual machine

Créer un ordinateur virtuel de toohello connexion Bureau à distance.

1. Cliquez sur hello **Connect** bouton sur les propriétés d’ordinateur virtuel hello. Un fichier de protocole Remote Desktop Protocol (fichier .rdp) est créé et téléchargé.

    ![Portail 9](./media/quick-create-portal/quick-create-portal/portal-quick-start-9.png) 

2. tooconnect tooyour machine virtuelle, ouvrez hello téléchargé le fichier RDP. À l’invite, cliquez sur **Se connecter**. Sur un Mac, vous avez besoin d’un client RDP telles [Client Bureau à distance](https://itunes.apple.com/us/app/microsoft-remote-desktop/id715768417?mt=12) de hello Mac App Store.

3. Entrez le nom d’utilisateur hello et le mot de passe spécifié lors de la création d’ordinateur virtuel de hello, puis cliquez sur **Ok**.

4. Vous pouvez recevoir un avertissement de certificat au cours du processus de connexion hello. Cliquez sur **Oui** ou **continuer** tooproceed avec une connexion hello.


## <a name="install-iis-using-powershell"></a>Installation de IIS à l’aide de PowerShell

Sur l’ordinateur virtuel de hello, démarrez une session PowerShell et exécutez hello suivant tooinstall de commande IIS.

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

Lorsque vous avez terminé, quittez la session RDP de hello et retourner les propriétés de machine virtuelle hello Bonjour portail Azure.

## <a name="open-port-80-for-web-traffic"></a>Ouvrez le port 80 pour le trafic web 

Un groupe de sécurité réseau (NSG) sécurise les trafics entrant et sortant. Lorsqu’un ordinateur virtuel est créé à partir de hello portail Azure, une règle de trafic entrant est créée sur le port 3389 pour les connexions RDP. Étant donné que cet ordinateur virtuel héberge un serveur Web, une règle de groupe de sécurité réseau doit toobe créé pour le port 80.

1. Sur l’ordinateur virtuel de hello, cliquez sur nom hello Hello **groupe de ressources**.
2. Sélectionnez hello **groupe de sécurité réseau**. Hello groupe de sécurité réseau peut être identifié à l’aide de hello **Type** colonne. 
3. Dans le menu de gauche hello, sous Paramètres, cliquez sur **les règles de sécurité de trafic entrant**.
4. Cliquez sur **Ajouter**.
5. Dans **Nom**, tapez **http**. Assurez-vous que **étendue du Port** a la valeur too80 et **Action** est défini trop**autoriser**. 
6. Cliquez sur **OK**.


## <a name="view-hello-iis-welcome-page"></a>Hello d’affichage page d’accueil IIS

Avec IIS installé et le port 80 ouvrir tooyour VM, hello webserver sont maintenant accessibles à partir de hello internet. Ouvrez un navigateur web et entrez les adresse IP publique hello Hello machine virtuelle. adresse IP publique de Hello sont accessibles sur le panneau de machine virtuelle hello Bonjour portail Azure.

![Site IIS par défaut](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Supprimer des ressources

Si n’est plus nécessaire, supprimez hello groupe de ressources, ordinateur virtuel et toutes les ressources associées. toodo par conséquent, sélectionnez le groupe de ressources hello à partir du Panneau de machine virtuelle hello et cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web. toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Windows.

> [!div class="nextstepaction"]
> [Didacticiels sur les machines virtuelles Azure Windows](./tutorial-manage-vm.md)
