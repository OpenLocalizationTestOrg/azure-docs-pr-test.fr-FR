---
title: "démarrage rapide du Cloud Shell (version préliminaire) aaaAzure | Documents Microsoft"
description: "Démarrage rapide pour hello Azure Cloud Shell"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: juluk
ms.openlocfilehash: e60700b92c10c331910dd8bb3c627fe1a024091c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-for-using-hello-azure-cloud-shell"></a>Démarrage rapide pour l’utilisation de hello Azure Cloud Shell

Ce document décrit en détail comment toouse hello Azure Cloud Shell Bonjour [portail Azure](https://ms.portal.azure.com/).

## <a name="start-cloud-shell"></a>Démarrer Cloud Shell
1. Lancez **Cloud Shell** à partir du volet de navigation supérieur hello Hello portail Azure <br>
![](media/shell-icon.png)
2. Sélectionnez un abonnement toocreate un compte de stockage et le partage de fichiers Azure
3. Sélectionnez Créer le stockage

> [!TIP]
> Vous êtes authentifié automatiquement pour Azure CLI 2.0 dans chaque session.

### <a name="set-your-subscription"></a>Définissez votre abonnement
1. Répertoriez les événements auxquels vous avez accès : <br>
`az account list`
2. Définissez votre abonnement préféré : <br>
`az account set --subscription my-subscription-name`

> [!TIP]
> Votre abonnement sera mémorisé pour les sessions ultérieures avec `/home/<user>/.azure/azureProfile.json`.

### <a name="create-a-resource-group"></a>Créer un groupe de ressources
Créez un nouveau groupe de ressources dans WestUS nommé « MyRG » : <br>
`az group create -l westus -n MyRG` <br>

### <a name="create-a-linux-vm"></a>Créer une machine virtuelle Linux
Créez une machine virtuelle Ubuntu dans votre nouveau groupe de ressources. Hello Azure CLI 2.0 créera les clés SSH et hello de configuration machine virtuelle avec eux. <br>
`az vm create -n my_vm_name -g MyRG --image UbuntuLTS --generate-ssh-keys`

> [!NOTE]
> Hello tooauthenticate de clés publiques et privées utilisées votre machine virtuelle sont placés dans `/User/.ssh/id_rsa` et `/User/.ssh/id_rsa.pub` par Azure CLI 2.0 par défaut. Votre dossier .ssh est conservé dans l’image de 5 Go de votre partage de fichiers Azure attaché.

Votre nom d’utilisateur sur cette machine virtuelle sera votre nom d’utilisateur utilisé dans Cloud Shell ($User@Azure:).

### <a name="ssh-into-your-linux-vm"></a>Se connecter avec SSH à votre machine virtuelle Linux
1. Recherchez le nom de votre machine virtuelle dans la barre de recherche du portail Azure hello
2. Cliquez sur « Connexion », puis exécutez : `ssh username@ipaddress`

![](media/sshcmd-copy.png)

Lors de la création de la connexion SSH hello, vous devez voir invite de bienvenue Ubuntu hello.
![](media/ubuntu-welcome.png)

## <a name="cleaning-up"></a>Nettoyage 
Supprimez votre groupe de ressources et toutes les ressources qu’il contient : <br>
Exécutez `az group delete -n MyRG`.

## <a name="next-steps"></a>Étapes suivantes
[En savoir plus sur le stockage persistant sur Cloud Shell](persisting-shell-storage.md) <br>
[En savoir plus sur Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) <br>
[En savoir plus sur le stockage de fichiers Azure](../storage/files/storage-files-introduction.md) <br>