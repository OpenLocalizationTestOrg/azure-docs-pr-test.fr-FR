---
title: aaaUsing hello Azure CLI 2.0 avec le stockage Azure | Documents Microsoft
description: "Découvrez comment toouse hello Azure Interface de ligne (Azure) 2.0 avec le stockage Azure toocreate et gérer des comptes de stockage et de travail avec les fichiers et les objets BLOB Windows Azure. Bonjour Azure CLI 2.0 est un outil d’inter-plateformes écrit dans Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 14e6eb0c913676380c90a72563276245e7f08aa6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a>À l’aide de hello Azure CLI 2.0 avec le stockage Azure

Hello open source, multiplateforme Azure CLI 2.0 fournit un ensemble de commandes pour travailler avec hello plateforme Azure. Il fournit la majeure partie de hello même fonctionnalité trouvée dans hello [portail Azure](https://portal.azure.com), y compris l’accès aux données enrichi.

Dans ce guide, nous vous indiquons comment toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform plusieurs tâches, utilisation des ressources dans votre compte de stockage Azure. Nous vous recommandons de télécharger et installer ou mettre à niveau la version la plus récente toohello Hello CLI 2.0 avant d’utiliser ce guide.

exemples de Hello dans le guide de hello partent du principe utiliser hello hello shell Bash sur Ubuntu, mais autres plateformes doivent exécuter la même façon. 

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a>Composants requis
Ce guide suppose que vous comprenez les concepts de base hello du stockage Azure. Il suppose également que vous êtes en mesure de toosatisfy hello création exigences relatives aux comptes qui sont spécifiées ci-dessous pour Azure et hello service de stockage.

### <a name="accounts"></a>Comptes
* **Compte Azure** : si vous ne possédez pas encore d’abonnement Azure, [créez un compte Azure gratuit](https://azure.microsoft.com/free/).
* **Compte de stockage** : voir la section [Créer un compte de stockage](storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](storage-create-storage-account.md).

### <a name="install-hello-azure-cli-20"></a>Installer hello Azure CLI 2.0

Téléchargez et installez hello Azure CLI 2.0 en suivant les instructions hello décrites dans [installer Azure CLI 2.0](/cli/azure/install-az-cli2).

> [!TIP]
> Si vous avez des difficultés avec l’installation de hello, extraire hello [dépannage de l’Installation](/cli/azure/install-az-cli2#installation-troubleshooting) section de l’article de hello et hello [installer dépannage](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide sur GitHub.
>

## <a name="working-with-hello-cli"></a>Utilisation de hello CLI

Une fois que vous avez installé hello CLI, vous pouvez utiliser hello `az` dans vos commandes de CLI d’Azure de hello tooaccess interface de ligne de commande (interpréteur de commandes, Terminal Server, invite de commandes). Hello de type `az` commande toosee une liste complète des commandes de base hello (hello suivant l’exemple de sortie a été tronquée) :

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

Dans l’interface de ligne de commande, exécutez la commande hello `az storage --help` hello de toolist `storage` commande sous-groupes. descriptions de Hello de sous-groupes de hello fournissent une vue d’ensemble de hello de fonctionnalité hello que CLI d’Azure fournit pour travailler avec vos ressources de stockage.

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a>Se connecter hello CLI tooyour abonnement Azure

toowork des ressources de hello dans votre abonnement Azure, vous devez tout d’abord vous connecter tooyour compte Azure avec `az login`. Vous pouvez vous connecter de plusieurs façons :

* **Connexion interactive** : `az login`
* **Connexion avec nom d’utilisateur et mot de passe** : `az login -u johndoe@contoso.com -p VerySecret`
  * Ceci ne fonctionne pas avec les comptes Microsoft ou les comptes qui utilisent l’authentification multifacteur.
* **Connexion avec un principal du service** : `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`

## <a name="azure-cli-20-sample-script"></a>Exemple de script CLI 2.0 Azure

Ensuite, nous allons utiliser un script shell small qui émet quelques base toointeract de commandes Azure CLI 2.0 avec des ressources de stockage Azure. tout d’abord les script Hello crée un nouveau conteneur dans votre compte de stockage, puis télécharge un conteneur existant pour toothat fichier (comme un objet blob). Il répertorie ensuite tous les objets BLOB dans le conteneur de hello et enfin, télécharge destination de tooa hello fichier sur votre ordinateur local que vous spécifiez.

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

**Configurer et exécuter le script de hello**

1. Ouvrez l’éditeur de texte, puis copier- coller hello précédant le script dans l’éditeur de hello.

2. Ensuite, mettez à jour tooreflect de variables de script hello vos paramètres de configuration. Remplacez hello suivant des valeurs comme indiqué :

   * **\<storage_account_name\>**  nom hello de votre compte de stockage.
   * **\<storage_account_key\>**  clé d’accès primaire ou secondaire hello pour votre compte de stockage.
   * **\<nom_conteneur\>**  un nom hello nouvelle toocreate de conteneur, tel que « azure-cli-exemple-container ».
   * **\<blob_name\>**  un nom pour l’objet blob de destination hello dans le conteneur de hello.
   * **\<file_to_upload\>**  hello chemin d’accès fichier toosmall sur votre ordinateur local, tel que « ~ / images/HelloWorld.png ».
   * **\<destination_file\>**  hello chemin d’accès du fichier de destination, tel que « ~ / downloadedImage.png ».

3. Une fois que vous avez mis à jour les variables nécessaires hello, enregistrer le script de hello et quittez l’éditeur. les étapes suivantes Hello supposent que vous avez nommé votre script **my_storage_sample.sh**.

4. Marquer le script hello en tant que fichier exécutable, si nécessaire :`chmod +x my_storage_sample.sh`

5. Exécuter le script de hello. Par exemple, dans Bash : `./my_storage_sample.sh`

Vous devez voir sortie similaire toohello et hello  **\<destination_file\>**  vous avez spécifié dans hello script doit s’afficher sur votre ordinateur local.

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> Hello sortie précédente est en **table** format. Vous pouvez spécifier toouse du format de sortie en spécifiant hello `--output` argument dans vos commandes CLI, ou globalement à l’aide de la valeur `az configure`.
>

## <a name="manage-storage-accounts"></a>Gestion des comptes de stockage

### <a name="create-a-new-storage-account"></a>Création d’un nouveau compte de stockage
toouse stockage Azure, vous devez un compte de stockage. Vous pouvez créer un nouveau compte de stockage Azure une fois que vous avez configuré votre ordinateur trop[connecter tooyour abonnement](#connect-to-your-azure-subscription).

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* `--location` [Obligatoire] : emplacement. Par exemple, « États-Unis de l’Ouest ».
* `--name`[Obligatoire] : nom de compte de stockage hello. nom de Hello doit comporter 3 caractères too24 et utiliser uniquement des caractères alphanumériques en minuscules.
* `--resource-group` [Obligatoire] : nom du groupe de ressources.
* `--sku`[Obligatoire] : hello compte de stockage référence (SKU). Valeurs autorisées :
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a>Définition des variables d’environnement par défaut pour le compte de stockage Azure
Vous pouvez disposer de plusieurs comptes de stockage dans votre abonnement Azure. tooselect un d’eux toouse de stockage suivants toutes les commandes, vous pouvez définir ces variables d’environnement :

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

Une autre façon tooset un compte de stockage par défaut est à l’aide d’une chaîne de connexion. Chaîne de connexion hello hello d’abord, obtenir `show-connection-string` commande :

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

Hello de copie la sortie de chaîne de connexion, puis définir hello `AZURE_STORAGE_CONNECTION_STRING` variable d’environnement (vous devrez peut-être chaîne de connexion tooenclose hello entre guillemets) :

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> Tous les exemples de hello les sections suivantes de cet article supposent que vous avez défini hello `AZURE_STORAGE_ACCOUNT` et `AZURE_STORAGE_ACCESS_KEY` variables d’environnement.
>

## <a name="create-and-manage-blobs"></a>Créer et gérer des objets blob
Stockage d’objets Blob Azure est un service pour stocker de grandes quantités de données non structurées, telles que les données texte ou binaire, qui sont accessibles à partir de n’importe où dans le monde hello via HTTP ou HTTPS. Cette section suppose que vous êtes déjà familiarisé avec les concepts du Stockage Blob Azure. Pour obtenir des informations détaillées, consultez [Prise en main du Stockage Blob Azure à l’aide de .NET](../blobs/storage-dotnet-how-to-use-blobs.md) et [Concepts de service Blob](/rest/api/storageservices/blob-service-concepts).

### <a name="create-a-container"></a>Créer un conteneur
Chaque objet blob du stockage Azure doit se trouver dans un conteneur. Vous pouvez créer un conteneur à l’aide de hello `az storage container create` commande :

```azurecli
az storage container create --name <container_name>
```

Vous pouvez définir un des trois niveaux d’accès en lecture pour un conteneur en spécifiant hello facultatif `--public-access` argument :

* `off`(par défaut) : les données de conteneur soient privé toohello propriétaire du compte.
* `blob` : accès en lecture public pour les objets blob.
* `container`: Lecture et liste accès toohello ensemble conteneur public.

Pour plus d’informations, consultez [gérer l’accès en lecture anonyme toocontainers et les objets BLOB](../blobs/storage-manage-access-to-resources.md).

### <a name="upload-a-blob-tooa-container"></a>Télécharger un conteneur d’objets blob tooa
Le Stockage Blob Azure prend en charge les objets blob de blocs, d’ajout et de page. Téléchargement d’objets BLOB tooa conteneur à l’aide de hello `blob upload` commande :

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 Par défaut, hello `blob upload` commande télécharge les objets BLOB de toopage *.vhd fichiers ou des objets BLOB de blocs dans le cas contraire. toospecify un autre type lorsque vous téléchargez un objet blob, vous pouvez utiliser hello `--type` argument--les valeurs autorisée sont `append`, `block`, et `page`.

 Pour plus d’informations sur les types d’objets blob différents hello, consultez [objets BLOB de blocs, ajouter des objets BLOB et objets BLOB de pages](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).


### <a name="download-a-blob-from-a-container"></a>Télécharger un objet blob depuis un conteneur
Cet exemple montre comment un objet blob à partir d’un conteneur de toodownload :

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a>Répertorier les objets BLOB hello dans un conteneur

Répertorier les objets BLOB de hello dans un conteneur avec hello [liste objet blob de stockage az](/cli/azure/storage/blob#list) commande.

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a>Copier des objets blob
Vous pouvez copier des objets blob au sein d’un compte de stockage, ou vers des comptes de stockage et des régions et ce, de façon asynchrone.

Hello exemple suivant montre comment le BLOB toocopy à partir du stockage d’un compte tooanother. Nous créons d’abord un conteneur dans le compte de stockage source hello, spécifiant l’accès en lecture public pour ses objets BLOB. Ensuite, nous télécharger un conteneur de fichier toohello et pour finir, copie d’objets blob hello conteneur dans un conteneur dans le compte de stockage de destination hello.

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

Bonjour exemple ci-dessus, le conteneur de destination hello doit déjà exister dans le compte de stockage de destination hello pour hello copie opération toosucceed. En outre, hello objet blob source spécifié dans hello `--source-uri` argument doit inclure un jeton de signature (SAP) d’accès partagé, ou être accessible publiquement, comme dans cet exemple.

### <a name="delete-a-blob"></a>Supprimer un objet blob
toodelete un objet blob, utilisez hello `blob delete` commande :

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a>Créer et gérer des partages de fichiers
Stockage de fichiers Azure offre un stockage partagé pour les applications à l’aide du protocole Server Message Block (SMB) de hello. Les services cloud et les machines virtuelles Microsoft Azure, ainsi que les applications locales, peuvent partager des données de fichiers via des partages montés. Vous pouvez gérer les partages de fichiers et les données de fichier via hello CLI d’Azure. Pour plus d’informations sur le stockage de fichiers Azure, consultez [prise en main avec un stockage de fichier Azure sur Windows](../storage-dotnet-how-to-use-files.md) ou [comment toouse stockage Azure files avec Linux](../storage-how-to-use-files-linux.md).

### <a name="create-a-file-share"></a>Créer un partage de fichiers
Un partage de fichiers Azure est un partage de fichiers SMB dans Microsoft Azure. Tous les répertoires et fichiers doivent être créés dans un partage de fichiers. Un compte peut contenir un nombre illimité de partages, et un partage peut stocker un nombre illimité de fichiers, les limites de capacité toohello hello du compte de stockage. Hello exemple suivant crée un partage de fichiers nommé **monsiteweb**.

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a>Créer un répertoire
Un répertoire fournit une structure hiérarchique dans un partage de fichiers Azure. Hello exemple suivant crée un répertoire nommé **myDir** dans le partage de fichiers hello.

```azurecli
az storage directory create --name myDir --share-name myshare
```

Un chemin d’accès peut inclure plusieurs niveaux, par exemple **dir1/dir2**. Toutefois, avant de créer un sous-répertoire, vous devez vous assurer que tous les répertoires parents existent. Par exemple, pour le chemin d’accès **dir1/dir2**, vous devez créer le répertoire **dir1**, puis le répertoire **dir2**.

### <a name="upload-a-local-file-tooa-share"></a>Télécharger un partage de fichiers local de tooa
exemple Hello télécharge un fichier à partir de **~/temp/samplefile.txt** tooroot Hello **monsiteweb** partage de fichiers. Hello `--source` argument spécifie tooupload de fichier local existant hello.

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

Comme avec la création du répertoire, vous pouvez spécifier un chemin d’accès de répertoire dans hello partage tooupload hello fichier tooan répertoire existant au sein de la part d’hello :

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

Un fichier dans le partage de hello peut être jusqu'à to too1 taille.

### <a name="list-hello-files-in-a-share"></a>Liste des fichiers dans un partage de hello
Vous pouvez répertorier des fichiers et des répertoires dans un partage à l’aide de hello `az storage file list` commande :

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a>Copie des fichiers      
Vous pouvez copier un fichier de tooanother, un objet blob tooa de fichier ou un objet blob tooa fichier. Par exemple, toocopy un répertoire tooa de fichiers dans un partage différent :        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a>Étapes suivantes
Voici quelques ressources supplémentaires pour en savoir plus sur l’utilisation de hello Azure CLI 2.0.

* [Prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [Référence des commandes Azure CLI 2.0](/cli/azure)
* [Azure CLI 2.0 sur GitHub](https://github.com/Azure/azure-cli)
