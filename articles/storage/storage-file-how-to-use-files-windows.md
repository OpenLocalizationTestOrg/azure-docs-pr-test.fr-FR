---
title: "aaaMount un partage de fichiers d’Azure et hello d’accès de partage dans Windows | Documents Microsoft"
description: "Montez un partage de fichiers d’Azure et un partage de hello d’accès dans Windows."
services: storage
documentationcenter: na
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
ms.openlocfilehash: 15ac468d9d7b8e0a195b024926ed4dd9790360d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="mount-an-azure-file-share-and-access-hello-share-in-windows"></a>Monter d’un partage de fichiers d’Azure et un partage de hello d’accès dans Windows
[Stockage de fichier Azure](storage-dotnet-how-to-use-files.md) est le système de fichiers de cloud de Microsoft toouse facile. Les partages de fichiers Azure peuvent être montés dans Windows et Windows Server. Cet article décrit trois façons différentes toomount un partage de fichiers de Azure sur Windows : avec hello fichier Explorateur de l’interface utilisateur, via PowerShell ou hello invite de commandes. 

Dans l’ordre les toomount un fichier Azure partager en dehors de hello région Azure, il est hébergé dans, telles que localement ou dans une région différente, hello du système d’exploitation doit prendre en charge SMB 3.0. 

Le partage de fichier Azure peut être monté sur une machine Azure. Le montage est réalisé en local ou sur une machine virtuelle Azure en fonction de la version du système d’exploitation. Tableau ci-dessous illustre hello 

| Version de Windows        | Version SMB |Version montable sur une machine virtuelle Azure|Version montable en local|
|------------------------|-------------|---------------------|---------------------|
| Windows 7              | SMB 2.1     | Oui                 | Non                  |
| Windows Server 2008 R2 | SMB 2.1     | Oui                 | Non                  |
| Windows 8              | SMB 3.0     | Oui                 | Oui                 |
| Windows Server 2012    | SMB 3.0     | Oui                 | Oui                 |
| Windows Server 2012 R2 | SMB 3.0     | Oui                 | Oui                 |
| Windows 10             | SMB 3.0     | Oui                 | Oui                 |

> [!Note]  
> Nous vous recommandons de prendre hello Ko la plus récente pour votre version de Windows.

## <a name="aprerequisites-for-mounting-azure-file-share-with-windows"></a></a>Conditions préalables pour le montage d’un partage de fichiers Azure avec Windows 
* **Nom de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello nom hello du compte de stockage.

* **Clé de compte de stockage**: partage d’un fichier Azure toomount, vous devez serez hello la clé primaire (ou secondaire). Actuellement, les clés SAS ne sont pas prises en charge pour le montage.

* **Assurez-vous que le port 445 est ouvert** : le Stockage Fichier Azure utilise le protocole SMB. SMB communique via le port TCP 445 - Vérifiez les toosee si votre pare-feu ne bloque pas les ports TCP 445 à partir de l’ordinateur client.

## <a name="mount-hello-azure-file-share-with-file-explorer"></a>Monter le partage de fichiers Azure hello avec l’Explorateur de fichiers
> [!Note]  
> Notez que hello suivant les instructions affichées sur Windows 10 et peuvent différer légèrement sur les versions plus anciennes. 

1. **Ouvrez l’Explorateur de fichiers**: cela est possible en l’ouvrant à partir du Menu Démarrer de hello, ou en appuyant sur le raccourci de Win + E.

2. **Accédez toohello élément de « Ce PC » sur le côté gauche de hello de fenêtre hello. Cela modifie les menus hello disponibles dans le ruban de hello. Sous le menu d’ordinateur hello, sélectionnez « Connecter un lecteur réseau »**.
    
    ![Menu déroulant de capture d’écran de hello « Connecter un lecteur réseau »](media/storage-file-how-to-use-files-windows/1_MountOnWindows10.png)

3. **Chemin d’accès de copie hello UNC du volet de « Se connecter » hello Bonjour Azure portal**: une description détaillée de toofind ces informations peuvent être trouvées comment [ici](storage-file-how-to-use-files-portal.md#connect-to-file-share).

    ![chemin d’accès UNC de Hello à partir du volet de connexion de stockage de fichier Azure hello](media/storage-file-how-to-use-files-windows/portal_netuse_connect.png)

4. **Sélectionnez la lettre de lecteur hello et entrez le chemin d’accès UNC de hello.** 
    
    ![Une capture d’écran de boîte de dialogue « Connecter un lecteur réseau » hello](media/storage-file-how-to-use-files-windows/2_MountOnWindows10.png)

5. **Hello d’utilisation avec préfixe de nom de compte de stockage `Azure\` en tant que nom d’utilisateur hello et une clé de compte de stockage en tant que mot de passe hello.**
    
    ![Une capture d’écran de la boîte de dialogue informations d’identification de réseau hello](media/storage-file-how-to-use-files-windows/3_MountOnWindows10.png)

6. **Utilisez le partage de fichiers Azure à votre guise**.
    
    ![Le partage de fichiers Azure est désormais monté.](media/storage-file-how-to-use-files-windows/4_MountOnWindows10.png)

7. **Lorsque vous toodismount prêt (ou déconnectez) partage de fichiers Azure hello, vous pouvez le faire par le bouton droit sur l’entrée hello pour partage hello sous hello « emplacements réseau » dans l’Explorateur de fichiers et en sélectionnant « Déconnecter »**.

## <a name="mount-hello-azure-file-share-with-powershell"></a>Monter le partage de fichiers Azure hello avec PowerShell
1. **Partage de fichiers Azure hello toomount de commande suivant de hello utilisation**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` avec des informations correctes hello.

    ```PowerShell
    $acctKey = ConvertTo-SecureString -String "<storage-account-key>" -AsPlainText -Force
    $credential = New-Object System.Management.Automation.PSCredential -ArgumentList "Azure\<storage-account-name>", $acctKey
    New-PSDrive -Name <desired-drive-letter> -PSProvider FileSystem -Root "\\<storage-account-name>.file.core.windows.net\<share-name>" -Credential $credential
    ```

2. **Partage de fichiers Azure hello utilisation comme vous le souhaitez**.

3. **Lorsque vous avez terminé, démontez le partage de fichiers Azure hello hello de commande suivante à l’aide de**.

    ```PowerShell
    Remove-PSDrive -Name <desired-drive-letter>
    ```

> [!Note]  
> Vous pouvez utiliser hello `-Persist` paramètre sur `New-PSDrive` toomake hello reste visible toohello hello du système d’exploitation pendant le montage de fichiers Azure partage.

## <a name="mount-hello-azure-file-share-with-command-prompt"></a>Monter le partage de fichiers Azure hello invite de commandes
1. **Partage de fichiers Azure hello toomount de commande suivant de hello utilisation**: n’oubliez pas de tooreplace `<storage-account-name>`, `<share-name>`, `<storage-account-key>`, `<desired-drive-letter>` avec des informations correctes hello.

    ```
    net use <desired-drive-letter>: \\<storage-account-name>.file.core.windows.net\<share-name> <storage-account-key> /user:Azure\<storage-account-name>
    ```

2. **Partage de fichiers Azure hello utilisation comme vous le souhaitez**.

3. **Lorsque vous avez terminé, démontez le partage de fichiers Azure hello hello de commande suivante à l’aide de**.

    ```
    net use <desired-drive-letter>: /delete
    ```

> [!Note]  
> Vous pouvez configurer hello fichier Azure partage tooautomatically se reconnecter au redémarrage par les informations d’identification hello persistantes dans Windows. Hello commande suivante rendront les informations d’identification hello :
>   ```
>   cmdkey /add:<storage-account-name>.file.core.windows.net /user:AZURE\<storage-account-name> /pass:<storage-account-key>
>   ```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage de fichiers Azure, consultez ces liens.

* [FAQ](storage-files-faq.md)
* [Dépannage](storage-troubleshoot-file-connection-problems.md)

### <a name="conceptual-articles-and-videos"></a>Vidéos et articles conceptuels
* [Stockage Fichier Azure : un système de fichiers SMB dans le cloud sans friction pour Windows et Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-azure-file-storage"></a>Outils pour le Stockage Fichier Azure
* [Utilisation d'Azure PowerShell avec Azure Storage](storage-powershell-guide-full.md)
* [Comment toouse AzCopy avec Microsoft Azure Storage](storage-use-azcopy.md)
* [À l’aide de hello CLI d’Azure avec le stockage Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Résolution des problèmes de stockage de fichiers Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="blog-posts"></a>Billets de blog :
* [Le stockage de fichiers Azure est désormais mis à la disposition générale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Dans le Stockage Fichier Azure](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Présentation de Microsoft Azure File Service](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Migration tooAzure de données fichier](https://azure.microsoft.com/blog/migrating-data-to-microsoft-azure-files/)

### <a name="reference"></a>Référence
* [Référence de la bibliothèque cliente de stockage pour .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Référence de l’API REST du service de fichiers](http://msdn.microsoft.com/library/azure/dn167006.aspx)
