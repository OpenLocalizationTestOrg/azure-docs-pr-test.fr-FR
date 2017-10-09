---
title: aaaHow toouse PowerShell toomanage stockage de fichier Azure | Documents Microsoft
description: "Découvrez le stockage de fichiers Azure toomanage toouse PowerShell."
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
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Comment toouse PowerShell toomanage stockage Azure
Vous pouvez utiliser Azure PowerShell toocreate et gérer des partages de fichiers.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Installer les applets de commande PowerShell hello pour le stockage Azure
tooprepare toouse PowerShell, téléchargez et installez les applets de commande PowerShell Azure hello. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azureps-cmdlets-docs) Pourquoi installer instructions d’installation et de point.

> [!NOTE]
> Il est recommandé de télécharger et installer ou mettre à niveau du module Azure PowerShell toohello plus récent.
> 
> 

Ouvrez une fenêtre Azure PowerShell en cliquant sur **Démarrer** et en saisissant **Windows PowerShell**. fenêtre de PowerShell Hello charge module Azure Powershell de hello pour vous.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Création d'un contexte pour votre compte de stockage et votre clé
Créer un contexte de compte de stockage hello. contexte de Hello encapsule la clé de compte et le nom du compte de stockage hello. Pour obtenir des instructions sur la copie de votre clé de compte à partir de hello [portail Azure](https://portal.azure.com), consultez [clés d’accès afficher et copier](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Remplacez `storage-account-name` et `storage-account-key` avec votre nom de compte de stockage et de la clé Bonjour l’exemple suivant.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Création d’un partage de fichiers
Créer un nouveau partage hello, nommé `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

Vous disposez désormais d’un partage de fichier dans le stockage de fichiers. Nous allons maintenant ajouter un répertoire et un fichier.

> [!IMPORTANT]
> nom de Hello de votre partage de fichiers doit être tout en minuscules. Pour plus d’informations sur la façon de nommer des partages de fichiers et des fichiers, consultez la rubrique [Affectation de noms et références aux partages, répertoires, fichiers et métadonnées](https://msdn.microsoft.com/library/azure/dn167011.aspx).
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Créez un répertoire dans le partage de fichiers hello
Créez un répertoire dans le partage de hello. Dans l’exemple suivant de hello, hello se nomme `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Télécharger un répertoire toohello de fichier local
Télécharger un répertoire toohello de fichiers local. exemple Hello télécharge un fichier à partir de `C:\temp\Log1.txt`. Modifier le chemin d’accès du fichier hello pour qu’il pointe tooa de fichier valide sur votre ordinateur local.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Liste des fichiers dans le répertoire de hello hello
fichier hello toosee répertoire de hello, vous pouvez répertorier tous les fichiers du répertoire hello. Cette commande retourne des sous-répertoires et fichiers de hello (le cas échéant) dans le répertoire de CustomLogs hello.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile renvoie une liste de fichiers et de répertoires pour répertoire vers lequel l’objet est transmis. « Get-AzureStorageFile-partager $s » retourne une liste de fichiers et de répertoires dans le répertoire racine de hello. tooget une liste de fichiers dans un sous-répertoire, vous avez toopass hello sous-répertoire tooGet-AzureStorageFile. C’est ce que cela fait : hello première partie de commande hello toohello canal retourne une instance de répertoire du sous-répertoire de hello CustomLogs. Puis, qui est passée à Get-AzureStorageFile, qui retourne les fichiers hello et des répertoires dans CustomLogs.

## <a name="copy-files"></a>Copie des fichiers
Depuis la version 0.9.7 d’Azure PowerShell, vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier. Ci-dessous, nous allons montrer comment tooperform ces copier opérations à l’aide des applets de commande PowerShell.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

* [FAQ](../storage-files-faq.md)
* [Résolution des problèmes sur Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Résolution des problèmes sur Linux](storage-troubleshoot-linux-file-connection-problems.md)    