---
title: aaaHow toocreate un partage de fichiers Azure | Documents Microsoft
description: "Comment toocreate un Azure partage de fichiers dans le stockage de fichiers Azure à l’aide de hello portail Azure, PowerShell et hello CLI d’Azure."
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Création d’un partage de fichiers dans le Stockage Fichier Azure
Vous pouvez créer des partages de fichiers Azure à l’aide de [portail Azure](https://portal.azure.com/), hello applets de commande PowerShell de stockage Azure, hello des bibliothèques clientes de stockage Azure ou hello API REST de stockage Azure. Dans ce didacticiel, vous allez apprendre :
* [Comment toocreate un fichier Azure partager à l’aide de hello portail Azure](#Create file share through hello Portal)
* [Comment toocreate un Azure de partage de fichiers à l’aide de Powershell](#Create file share using PowerShell)
* [Comment toocreate un Azure de partage de fichiers à l’aide de CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Composants requis
toocreate un partage de fichiers Azure, vous pouvez utiliser un compte de stockage existe déjà, ou [créer un nouveau compte de stockage Azure](storage-create-storage-account.md). toocreate un partage de fichiers Azure avec PowerShell, vous devez clé de compte hello et le nom de votre compte de stockage... Si vous envisagez de toouse Powershell ou CLI, vous devez clé de compte de stockage.

## <a name="create-file-share-through-hello-portal"></a>Créer le partage de fichiers via hello portail
1. **Panneau de compte tooStorage accédez sur le portail Azure**:    
    ![Panneau Compte de stockage](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **Cliquez sur Ajouter un partage de fichiers** :    
    ![Cliquez sur hello ajouter le bouton de partage de fichier](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **Indiquez le nom et le quota. Actuellement, la limite de quota maximum est 5 To** :    
    ![Fournir un nom et un quota de votre choix pour le nouveau partage de fichiers hello](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **Affichez votre nouveau partage de fichiers** : ![Affichez votre nouveau partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **Importez un fichier** : ![Importez un fichier](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **Parcourez le partage de fichiers et gérez vos répertoires et vos fichiers** : ![Parcourez le partage de fichiers](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Création d’un partage de fichiers via PowerShell
tooprepare toouse PowerShell, téléchargez et installez les applets de commande PowerShell Azure hello. Consultez [comment tooinstall et configurer Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) Pourquoi installer instructions d’installation et de point.

> [!Note]  
> Il est recommandé de télécharger et installer ou mettre à niveau du module Azure PowerShell toohello plus récent.

1. **Créer un contexte pour votre compte de stockage et de la clé** contexte de hello encapsule la clé de compte et le nom du compte de stockage hello. Pour obtenir des instructions sur la copie de votre clé de compte à partir du [portail Azure](https://portal.azure.com/), voir [Afficher et copier les clés d’accès de stockage](storage-create-storage-account.md#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Créez un nouveau partage de fichiers** :    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> nom de Hello de votre partage de fichiers doit être tout en minuscules. Pour plus d’informations sur la façon de nommer des partages de fichiers et des fichiers, consultez la rubrique [Affectation de noms et références aux partages, répertoires, fichiers et métadonnées](https://msdn.microsoft.com/library/azure/dn167011.aspx).

## <a name="create-file-share-through-command-line-interface-cli"></a>Création d’un partage de fichiers via l’Interface de ligne de commande (CLI)
1. **tooprepare toouse une Interface de ligne de commande (CLI), téléchargez et installez les hello CLI d’Azure.**  
    Consultez [Installation d’Azure CLI 2.0](/cli/azure/install-az-cli2.md) et [Prise en main d’Azure CLI 2.0](/cli/azure/get-started-with-azure-cli.md).

2. **Créer un compte de stockage de chaîne de connexion toohello où vous souhaitez partager de hello toocreate.**  
    Remplacez ```<storage-account>``` et ```<resource_group>``` avec votre compte nom et la ressource de groupe de stockage Bonjour l’exemple suivant.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Créez le partage de fichiers**.
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Étapes suivantes
* [Connexion et montage du partage de fichiers – Windows](storage-file-how-to-use-files-windows.md)
* [Connexion et montage du partage de fichiers – Linux](storage-how-to-use-files-linux.md)
* [Connexion et montage du partage de fichiers – MacOS](storage-file-how-to-use-files-mac.md)

Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

* [FAQ](storage-files-faq.md)
* [Dépannage](storage-troubleshoot-file-connection-problems.md)