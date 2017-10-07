---
title: aaaUsing hello Azure CLI 1.0 avec le stockage Azure | Documents Microsoft
description: "Découvrez comment toouse hello Azure Interface de ligne (Azure) 1.0 avec toocreate de stockage Azure et gérer des comptes de stockage et de travail avec les fichiers et les objets BLOB Windows Azure. Hello CLI d’Azure est un outil inter-plateformes"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: 786f2be64875f5094f09fd6e4a47532889c3a82f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a>À l’aide de hello Azure CLI 1.0 avec le stockage Azure

## <a name="overview"></a>Vue d'ensemble

Hello CLI d’Azure fournit un ensemble d’open source d’inter-plateformes commandes sur l’utilisation de hello plateforme Azure. Il fournit la majeure partie de hello même fonctionnalité trouvée dans hello [portail Azure](https://portal.azure.com) données riches ainsi accéder aux fonctionnalités.

Dans ce guide, nous allons examiner comment toouse [Azure Interface de ligne (Azure)](../cli-install-nodejs.md) tooperform diverses tâches de développement et d’administration avec le stockage Azure. Nous vous recommandons de télécharger et installer ou mettre à niveau toohello dernière CLI d’Azure avant d’utiliser ce guide.

Ce guide suppose que vous comprenez les concepts de base hello du stockage Azure. Hello Guide d’un nombre de scripts d’utilisation de hello toodemonstrate Hello CLI d’Azure avec le stockage Azure. Être tooupdate que les variables de script hello en fonction de votre configuration avant d’exécuter chaque script.

> [!NOTE]
> guide de Hello fournit des exemples de script et commande de CLI d’Azure hello pour les comptes de stockage classiques. Consultez [Using hello CLI d’Azure pour Mac, Linux et Windows avec la gestion des ressources Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) pour les commandes CLI d’Azure pour les comptes de stockage de gestionnaire de ressources.
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a>Prise en main Azure Storage et hello CLI d’Azure dans 5 minutes
Ce guide inclut des exemples basés sur Ubuntu, mais les résultats devraient être les mêmes sur d’autres plates-formes.

**Nouvelle tooAzure :** obtenir un abonnement Microsoft Azure et un compte Microsoft associé à cet abonnement. Pour en savoir plus sur les options d’achat de Microsoft Azure, voir [Essai gratuit](https://azure.microsoft.com/pricing/free-trial/), [Options d’achat](https://azure.microsoft.com/pricing/purchase-options/) et [Offres spéciales membres](https://azure.microsoft.com/pricing/member-offers/) (pour les membres de MSDN, Microsoft Partner Network et BizSpark, ainsi que d’autres programmes Microsoft).

Pour plus d’informations sur les abonnements Azure, consultez la section [Attribution de rôles d’administrateur dans Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) .

**Une fois le compte et l’abonnement à Microsoft Azure créés :**

1. Téléchargez et installez hello CLI d’Azure suivant les instructions hello décrites dans [installation Bonjour Azure CLI](../cli-install-nodejs.md).
2. Une fois hello CLI d’Azure a été installé, vous serez en mesure de toouse hello de commande azure à partir de vos commandes de l’interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes) tooaccess hello CLI d’Azure. Hello de type _azure_ commande et vous devez voir hello suivant de sortie.

    ![Sorte de commande Microsoft Azure][Image1]
3. Dans l’interface de ligne de commande hello, tapez `azure storage` toolist toutes hello les commandes de stockage azure et obtenir une première impression de hello de fonctionnalités hello CLI d’Azure fournit. Vous pouvez taper le nom de la commande avec **-h** paramètre (par exemple, `azure storage share create -h`) toosee les détails de la syntaxe de commande.
4. Maintenant, nous donnons un script simple qui montre la base tooaccess de commandes CLI d’Azure stockage Azure. script de Hello tout d’abord vous demandera tooset deux variables de votre compte de stockage et la clé. Ensuite, hello script créer un conteneur dans ce nouveau compte de stockage et télécharger un conteneur de toothat (blob) de fichier image existant. Une fois le script de hello répertorie tous les objets BLOB dans le conteneur, elle télécharge hello toohello destination répertoire des fichiers image qui existe sur l’ordinateur local de hello.

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. Sur ce dernier, ouvrez l’éditeur de texte de votre choix (vim, par exemple). Tapez hello au-dessus de script dans votre éditeur de texte.
6. Maintenant, vous devez les variables de script tooupdate hello en fonction de vos paramètres de configuration.

   * **< Storage_account_name >** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre compte de stockage. **Important :** nom hello hello du compte de stockage doit être unique dans Azure. Il doit également inclure des minuscules uniquement.
   * **< storage_account_key >** clé d’accès hello de votre compte de stockage.
   * **< Nom_conteneur >** utiliser hello attribué dans le script de hello ou entrez un nouveau nom pour votre conteneur.
   * **< Image_to_upload >** saisir une image de tooa de chemin d’accès sur votre ordinateur local, tel que : « ~ / images/HelloWorld.png ».
   * **< Destination_folder >** Entrez un chemin d’accès tooa répertoire local toostore les fichiers téléchargés depuis le stockage Azure, telles que : « ~/downloadImages ».
7. Une fois que vous avez mis à jour les variables nécessaires hello vim, appuyez sur les combinaisons de touches `ESC`, `:`, `wq!` script de hello toosave.
8. toorun ce script, simplement type hello script nom de fichier dans la console hello bash. Une fois que ce script s’exécute, vous devez disposer d’un dossier local de destination qui inclut le fichier d’image hello téléchargé. Hello suivant capture d’écran montre un exemple de sortie :

Après l’exécution du script de hello, vous devez disposer d’un dossier local de destination qui inclut le fichier d’image hello téléchargé.

## <a name="manage-storage-accounts-with-hello-azure-cli"></a>Gérer les comptes de stockage avec hello CLI d’Azure
### <a name="connect-tooyour-azure-subscription"></a>Se connecter tooyour abonnement Azure
La plupart des commandes de stockage hello fonctionnera sans un abonnement Azure, nous vous recommandons tooconnect tooyour abonnement hello CLI d’Azure. tooconfigure hello CLI d’Azure toowork avec votre abonnement, suivez les étapes de hello dans [connecter tooan abonnement Azure à partir de hello CLI d’Azure](../xplat-cli-connect.md).

### <a name="create-a-new-storage-account"></a>Création d’un nouveau compte de stockage
Vous devrez toouse le stockage Azure, un compte de stockage. Vous pouvez créer un nouveau compte de stockage Azure une fois que vous avez configuré votre abonnement de tooyour tooconnect ordinateur.

```azurecli
azure storage account create <account_name>
```

nom de Hello de votre compte de stockage doit être comprise entre 3 et 24 caractères et utiliser des nombres et des lettres minuscules.

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a>Définir un compte Azure Storage par défaut dans les variables d’environnement
Vous pouvez disposer de plusieurs comptes de stockage dans votre abonnement. Vous pouvez choisir un d’eux et affectez-lui Bonjour variables d’environnement pour tout le stockage hello commandes Bonjour même session. Cela vous permet de toorun hello CLI d’Azure stockage commandes sans spécifier le stockage de hello compte explicitement la clé.

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Une autre façon tooset un compte de stockage par défaut utilise la chaîne de connexion. Tout d’abord obtenir la chaîne de connexion hello en commande :

```azurecli
azure storage account connectionstring show <account_name>
```

Puis copiez la chaîne de connexion de sortie hello et la définir tooenvironment variable :

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a>Créer et gérer des objets blob
Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS. Cette section part du principe que vous êtes déjà familiarisé avec les concepts de stockage d’objets Blob Azure hello. Pour obtenir des informations détaillées, consultez [Prise en main du Stockage Blob Azure à l’aide de .NET](storage-dotnet-how-to-use-blobs.md) et [Concepts de service Blob](http://msdn.microsoft.com/library/azure/dd179376.aspx).

### <a name="create-a-container"></a>Créer un conteneur
Chaque objet blob du stockage Azure doit se trouver dans un conteneur. Vous pouvez créer un conteneur privé à l’aide de hello `azure storage container create` commande :

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> Il existe trois niveaux d’accès en lecture anonyme : **Désactivé**, **Blob** et **Conteneur**. tooprevent anonyme accéder à tooblobs, le paramètre d’autorisation ensemble hello**hors**. Par défaut, hello nouveau conteneur est privé et sont accessibles uniquement par le propriétaire du compte hello. public anonyme de tooallow lire tooblob d’accéder aux ressources, mais pas toocontainer métadonnées ou toohello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**Blob**. public complet de tooallow lire tooblob d’accéder aux ressources, les métadonnées de conteneur et hello liste d’objets BLOB dans le conteneur de hello, définissez le paramètre d’autorisation hello trop**conteneur**. Pour plus d’informations, consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](storage-manage-access-to-resources.md).
>
>

### <a name="upload-a-blob-into-a-container"></a>Charger un objet blob dans un conteneur
Le service de stockage d’objets blob Azure prend en charge les objets blob de blocs et de page. Pour plus d’informations, consultez [Présentation des objets blob de blocs, des objets blob d’ajout et des objets blob de pages](http://msdn.microsoft.com/library/azure/ee691964.aspx).

tooupload objets BLOB dans tooa conteneur, vous pouvez utiliser hello `azure storage blob upload`. Par défaut, cette commande télécharge le blob de blocs tooa hello fichiers locaux. type de hello toospecify pour l’objet blob de hello, vous pouvez utiliser hello `--blobtype` paramètre.

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a>Télécharger des objets blob depuis un conteneur
Bonjour à l’exemple suivant montre comment toodownload les objets BLOB à partir d’un conteneur.

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a>Copier des objets blob
Vous pouvez copier des objets blob au sein d’un compte de stockage, ou vers des comptes de stockage et des régions et ce, de façon asynchrone.

Hello exemple suivant montre comment le BLOB toocopy à partir du stockage d’un compte tooanother. Dans cet exemple, nous créons un conteneur incluant des objets blob accessibles de manière publique et anonyme.

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

Cet exemple repose sur une copie asynchrone. Vous pouvez surveiller l’état de hello de chaque opération de copie en exécutant hello `azure storage blob copy show` opération.

Notez que l’URL source du hello fourni pour l’opération de copie hello doit être accessible publiquement, ou inclure un jeton SAP (signature d’accès partagé).

### <a name="delete-a-blob"></a>Supprimer un objet blob
toodelete un objet blob, utilisez hello commande ci-dessous :

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a>Créer et gérer des partages de fichiers
Stockage de fichiers Azure offre un stockage partagé pour les applications à l’aide du protocole SMB standard de hello. Les services cloud et les machines virtuelles Microsoft Azure, ainsi que les applications locales, peuvent partager des données de fichiers via des partages montés. Vous pouvez gérer les partages de fichiers et les données de fichier via hello CLI d’Azure. Pour plus d’informations sur le stockage de fichiers Azure, consultez [prise en main avec un stockage de fichier Azure sur Windows](storage-dotnet-how-to-use-files.md) ou [comment toouse stockage Azure files avec Linux](storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Créer un partage de fichiers
Un partage de fichiers Azure est un partage de fichiers SMB dans Microsoft Azure. Tous les répertoires et fichiers doivent être créés dans un partage de fichiers. Un compte peut contenir un nombre illimité de partages, et un partage peut stocker un nombre illimité de fichiers, les limites de capacité toohello hello du compte de stockage. Hello exemple suivant crée un partage de fichiers nommé **monsiteweb**.

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a>Créer un répertoire
Un répertoire fournit une structure hiérarchique facultative pour un partage de fichiers Microsoft Azure. Hello exemple suivant crée un répertoire nommé **myDir** dans le partage de fichiers hello.

```azurecli
azure storage directory create myshare myDir
```

Remarque : ce chemin d’accès au répertoire peut inclure plusieurs niveaux, *par exemple*: **a/b**. Cependant, vous devez vous assurer que tous les répertoires parents existent. Par exemple, pour le chemin d’accès **a/b**, vous devez créer le répertoire **a**, puis le répertoire **b**.

### <a name="upload-a-local-file-toodirectory"></a>Télécharger un fichier local de toodirectory
exemple Hello télécharge un fichier à partir de **~/temp/samplefile.txt** toohello **myDir** active. Modifier le chemin d’accès du fichier hello pour qu’il pointe tooa de fichier valide sur votre ordinateur local :

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

Notez qu’un fichier dans le partage de hello peut être jusqu'à to too1 taille.

### <a name="list-hello-files-in-hello-share-root-or-directory"></a>Liste des fichiers hello dans la racine du partage hello ou un répertoire
Vous pouvez répertorier les fichiers de hello et sous-répertoires d’une racine de partage ou un répertoire à l’aide de hello de commande suivante :

```azurecli
azure storage file list myshare myDir
```

Notez que ce nom de répertoire hello est facultatif pour l’opération de liste de hello. Si omis, la commande hello répertorie contenu hello du répertoire racine de hello du partage de hello.

### <a name="copy-files"></a>Copie des fichiers
Depuis la version 0.9.8 de CLI d’Azure, vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier. Ci-dessous, nous allons montrer comment tooperform ces copier opérations à l’aide des commandes CLI. toocopy un répertoire toohello fichier :

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

toocopy un répertoire de fichiers blob tooa :

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a>Étapes suivantes

Vous pouvez trouver la référence des commandes de la CLI Azure 1.0 pour travailler avec des ressources de stockage ici :

* [Commandes de la CLI Azure en mode Resource Manager](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [Commandes de la CLI Azure en mode Azure Service Management (ASM)](../cli-install-nodejs.md)

Peut également voulue tootry hello [Azure CLI 2.0](storage-azure-cli.md), notre CLI de nouvelle génération écrit dans Python, pour une utilisation avec le modèle de déploiement du Gestionnaire de ressources hello.

[Image1]: ./media/storage-azure-cli/azure_command.png
