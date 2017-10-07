---
title: "aaaAzure démarrage rapide : créer un ordinateur virtuel portail | Documents Microsoft"
description: "Démarrage rapide avec Azure - Portail pour la création d’une machine virtuelle"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 07/15/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 984a400c976e349a59f873210d6e04bcdea39e1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-portal"></a>Créer une machine virtuelle Linux avec hello portail Azure

Machines virtuelles peuvent être créés via hello portail Azure. Cette méthode fournit une interface utilisateur basée sur navigateur pour créer et configurer des machines virtuelles et toutes les ressources liées. Cette procédure de démarrage rapide via la création d’une machine virtuelle et l’installation d’un serveur Web sur hello machine virtuelle.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="create-ssh-key-pair"></a>Créer la paire de clés SSH

Vous devez une toocomplete de paire de clés SSH ce démarrage rapide. Si vous disposez déjà d’une paire de clés SSH, vous pouvez ignorer cette étape.

À partir d’une interface de l’interpréteur de commandes, exécutez la commande et suivez hello à l’écran. sortie de la commande Hello inclut le nom du fichier de clé publique de hello hello. Copier le contenu de hello du Presse-papiers de toohello hello fichier de clé publique.

```bash
ssh-keygen -t rsa -b 2048
```

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure 

Ouvrez une session dans toohello portail Azure à http://portal.azure.com.

## <a name="create-virtual-machine"></a>Create virtual machine

1. Cliquez sur hello **nouveau** bouton se trouve sur le coin supérieur gauche hello Hello portail Azure.

2. Sélectionnez **Compute**, puis sélectionnez **Ubuntu Server 16.04 LTS**. 

3. Entrez les informations de machine virtuelle hello. Dans **Type d’authentification**, sélectionnez **Clé publique SSH**. Lorsque vous collez votre clé publique SSH, prenez soin de tooremove tout espace blanc de début ou de fin. Lorsque vous avez terminé, cliquez sur **OK**.

    ![Entrez les informations de base sur votre machine virtuelle dans le panneau de portail hello](./media/quick-create-portal/create-vm-portal-basic-blade.png)

4. Sélectionnez une taille de hello machine virtuelle. Sélectionnez des tailles de plus, toosee **afficher toutes les** ou modifier hello **pris en charge le type de disque** filtre. 

    ![Capture d’écran montrant les tailles de machine virtuelle](./media/quick-create-portal/create-linux-vm-portal-sizes.png)  

5. Dans le panneau de paramètres hello, conserver les valeurs par défaut hello, puis cliquez sur **OK**.

6. Dans la page de résumé hello, cliquez sur **Ok** déploiement d’ordinateur virtuel toostart hello.

7. Hello machine virtuelle sera épinglé toohello tableau de bord de portail Azure. Une fois que la fin du déploiement de hello, panneau de résumé de machine virtuelle hello s’ouvre automatiquement.


## <a name="connect-toovirtual-machine"></a>Connecter toovirtual machine

Créer une connexion SSH avec l’ordinateur virtuel de hello.

1. Cliquez sur hello **Connect** bouton sur le panneau de machine virtuelle hello. Hello connecter bouton affiche une chaîne de connexion SSH qui peut être utilisés tooconnect toohello virtual machine.

    ![Portail 9](./media/quick-create-portal/portal-quick-start-9.png) 

2. La commande suivante d’exécution hello toocreate une session SSH. Remplacer la chaîne de connexion hello avec hello que celle que vous avez copié à partir de hello portail Azure.

```bash 
ssh azureuser@40.112.21.50
```

## <a name="install-nginx"></a>Installer NGINX

Suivante de hello utilisez bash sources de package tooupdate de script et installer le dernier package de NGINX hello. 

```bash 
#!/bin/bash

# update package source
sudo apt-get -y update

# install NGINX
sudo apt-get -y install nginx
```

Lorsque vous avez terminé, quittez la session SSH hello et retourner les propriétés de machine virtuelle hello Bonjour portail Azure.


## <a name="open-port-80-for-web-traffic"></a>Ouvrez le port 80 pour le trafic web 

Un groupe de sécurité réseau (NSG) sécurise les trafics entrant et sortant. Lorsqu’un ordinateur virtuel est créé à partir de hello portail Azure, une règle de trafic entrant est créée sur le port 22 pour les connexions SSH. Étant donné que cet ordinateur virtuel héberge un serveur Web, une règle de groupe de sécurité réseau doit toobe créé pour le port 80.

1. Sur l’ordinateur virtuel de hello, cliquez sur nom hello Hello **groupe de ressources**.
2. Sélectionnez hello **groupe de sécurité réseau**. Hello groupe de sécurité réseau peut être identifié à l’aide de hello **Type** colonne. 
3. Dans le menu de gauche hello, sous Paramètres, cliquez sur **les règles de sécurité de trafic entrant**.
4. Cliquez sur **Ajouter**.
5. Dans **Nom**, tapez **http**. Assurez-vous que **étendue du Port** a la valeur too80 et **Action** est défini trop**autoriser**. 
6. Cliquez sur **OK**.


## <a name="view-hello-nginx-welcome-page"></a>Page d’accueil de vue hello NGINX

NGINX installés et le port 80 ouvrez tooyour VM, hello webserver sont maintenant accessibles à partir de hello internet. Ouvrez un navigateur web et entrez les adresse IP publique hello Hello machine virtuelle. adresse IP publique de Hello sont accessibles sur le panneau de machine virtuelle hello Bonjour portail Azure.

![Site par défaut NGINX](./media/quick-create-cli/nginx.png) 

## <a name="clean-up-resources"></a>Supprimer des ressources

Si n’est plus nécessaire, supprimez hello groupe de ressources, ordinateur virtuel et toutes les ressources associées. toodo par conséquent, sélectionnez le groupe de ressources hello à partir du Panneau de machine virtuelle hello et cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

Dans ce guide de démarrage rapide, vous avez déployé une machine virtuelle simple ainsi qu’une règle de groupe de sécurité réseau, et installé un serveur web. toolearn en savoir plus sur les machines virtuelles, continuer toohello didacticiel pour les machines virtuelles Linux.

> [!div class="nextstepaction"]
> [Didacticiels sur les machines virtuelles Azure Linux](./tutorial-manage-vm.md)
