---
title: "aaaTutorial - hello d’utilisation du SDK de traitement par lots Azure pour Python | Documents Microsoft"
description: "Découvrez les concepts de base hello de traitement par lots Azure et créer une solution simple à l’aide de Python."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: 42cae157-d43d-47f8-88f5-486ccfd334f4
ms.service: batch
ms.devlang: python
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c4d5152aeef31848c50a7f2aae5e7a7e0e1e9535
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-batch-sdk-for-python"></a>Prise en main hello lot SDK pour Python

> [!div class="op_single_selector"]
> * [.NET](batch-dotnet-get-started.md)
> * [Python](batch-python-tutorial.md)
> * [Node.JS](batch-nodejs-get-started.md)
>
>

Principes fondamentaux de hello [Azure Batch] [ azure_batch] et hello [lot Python] [ py_azure_sdk] client comme une petite application de traitement par lots écrite dans Python les sujets abordés. Nous allons comment deux exemples scripts utilisez hello lot service tooprocess une charge de travail parallèle sur les ordinateurs virtuels Linux dans le cloud de hello et comment ils interagissent avec [Azure Storage](../storage/common/storage-introduction.md) intermédiaire de fichier et l’extraction. Vous allez en savoir un flux de travail courant lot application acquérir une compréhension de base du hello principaux composants du lot telles que les travaux, les tâches, les pools et nœuds de calcul.

![Flux de travail de la solution Batch (de base)][11]<br/>

## <a name="prerequisites"></a>Composants requis
Cet article suppose que vous avez acquis une connaissance pratique de Python et que vous êtes familiarisé avec Linux. Il suppose également que vous êtes en mesure de toosatisfy hello création exigences relatives aux comptes qui sont spécifiées ci-dessous pour Azure et hello lot et les services de stockage.

### <a name="accounts"></a>Comptes
* **Compte Azure** : si vous ne possédez pas encore d’abonnement Azure, [créez un compte Azure gratuit][azure_free_account].
* **Compte Batch**: une fois que vous disposez d’un abonnement Azure, [créez un compte Azure Batch](batch-account-create-portal.md).
* **Compte de stockage** : voir la section [Créer un compte de stockage](../storage/common/storage-create-storage-account.md#create-a-storage-account) de l’article [À propos des comptes de stockage Azure](../storage/common/storage-create-storage-account.md).

### <a name="code-sample"></a>Exemple de code
didacticiel de Python Hello [exemple de code] [ github_article_samples] est un des hello de nombreux exemples de code de lot trouvés dans hello [exemples de traitement par lots azure] [ github_samples] référentiel sur GitHub. Vous pouvez télécharger tous les exemples de hello en cliquant sur **Clone ou téléchargement > ZIP de téléchargement** sur la page d’accueil de référentiel hello, ou en cliquant sur hello [azure-lot-exemples-master.zip] [ github_samples_zip]lien direct. Une fois que vous avez extrait le contenu hello du fichier ZIP de hello, scripts hello deux pour ce didacticiel sont trouvent dans hello `article_samples` active :

`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_client.py`<br/>
`/azure-batch-samples/Python/Batch/article_samples/python_tutorial_task.py`

### <a name="python-environment"></a>Environnement Python
toorun hello *python_tutorial_client.py* exemple de script sur votre station de travail locale, vous devez un **interpréteur Python** compatible avec la version **2.7** ou **3.3 +**. script de Hello a été testé sur Linux et Windows.

### <a name="cryptography-dependencies"></a>dépendances de chiffrement
Vous devez installer les dépendances hello pour hello [cryptographie] [ crypto] bibliothèque, requis par hello `azure-batch` et `azure-storage` packages Python. Effectuez l’une des hello suit les opérations appropriées pour votre plateforme, ou consultez toohello [installation de chiffrement] [ crypto_install] pour plus d’informations :

* Ubuntu

    `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython-dev python-dev`
* CentOS

    `yum update && yum install -y gcc openssl-devel libffi-devel python-devel`
* SLES/OpenSUSE

    `zypper ref && zypper -n in libopenssl-dev libffi48-devel python-devel`
* Windows

    `pip install cryptography`

> [!NOTE]
> Si l’installation de Python 3.3 + sur Linux, utilisez équivalents de python3 hello pour les dépendances de Python hello. Par exemple, sur Ubuntu : `apt-get update && apt-get install -y build-essential libssl-dev libffi-dev libpython3-dev python3-dev`
>
>

### <a name="azure-packages"></a>Packages Azure
Ensuite, installez hello **Azure Batch** et **Azure Storage** packages Python. Vous pouvez installer les deux packages à l’aide de **pip** et hello *requirements.txt* est disponible ici :

`/azure-batch-samples/Python/Batch/requirements.txt`

Problème suivant **pip** les packages tooinstall hello lot et le stockage de la commande :

`pip install -r requirements.txt`

Vous pouvez également installer hello [par lots azure] [ pypi_batch] et [le stockage azure] [ pypi_storage] Python packages manuellement :

`pip install azure-batch`<br/>
`pip install azure-storage`

> [!TIP]
> Si vous utilisez un compte non privilégié, vous devrez peut-être tooprefix vos commandes avec `sudo`. Par exemple, `sudo pip install -r requirements.txt`. Pour plus d’informations sur l’installation des packages Python, voir [Installing Packages][pypi_install] (Installation des packages) sur python.org.
>
>

## <a name="batch-python-tutorial-code-sample"></a>Exemple de code de didacticiel Python Batch
exemple de code du didacticiel Hello Python de lot se compose de deux scripts Python et plusieurs fichiers de données.

* **python_tutorial_client.py**: interagit avec tooexecute de services de stockage et de traitement par lots hello une charge de travail parallèle sur les nœuds de calcul (machines virtuelles). Hello *python_tutorial_client.py* script s’exécute sur votre station de travail locale.
* **python_tutorial_task.py**: script hello qui s’exécute sur les nœuds de calcul dans Azure tooperform travail hello. Dans l’exemple hello, *python_tutorial_task.py* analyse hello texte dans un fichier téléchargé depuis le stockage Azure (fichier d’entrée de hello). Ensuite, il génère un fichier texte (fichier de sortie hello) qui contient une liste de mots de trois premières hello qui s’affichent dans le fichier d’entrée de hello. Une fois qu’il crée le fichier de sortie hello, *python_tutorial_task.py* téléchargements hello fichier tooAzure stockage. Cela rend disponible pour le script de client toohello de téléchargement en cours d’exécution sur votre station de travail. Hello *python_tutorial_task.py* script s’exécute en parallèle sur plusieurs nœuds de calcul dans hello service Batch.
* **./Data/taskdata\*.txt**: ces trois fichiers texte fournissent une entrée de hello pour les nœuds de calcul tâches hello qui s’exécutent sur hello.

Hello suivant schéma illustre les opérations principales hello qui sont effectuées par les scripts de client et de la tâche hello. Ce flux de travail de base est caractéristique de nombreuses solutions de calcul créées avec Batch. Pendant qu’il ne présente pas toutes les fonctionnalités disponibles dans hello service Batch, presque tous les scénarios de traitement par lots inclut des parties de ce flux de travail.

![Exemple de flux de travail Batch][8]<br/>

[**Étape 1.**](#step-1-create-storage-containers) Créer des **conteneurs** dans le Stockage Blob Azure.<br/>
[**Étape 2.**](#step-2-upload-task-script-and-data-files) Téléchargez toocontainers de fichiers de script et d’entrée de tâche.<br/>
[**Étape 3.**](#step-3-create-batch-pool) Créer un **pool** Batch.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**3a.** Hello pool **StartTask** téléchargements hello tâche script (python_tutorial_task.py) toonodes dès qu’ils rejoignent le pool de hello.<br/>
[**Étape 4.**](#step-4-create-batch-job) Créer un **travail** Batch.<br/>
[**Étape 5.**](#step-5-add-tasks-to-job) Ajouter **tâches** toohello travail.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**5a.** les tâches de Hello sont planifiée tooexecute sur les nœuds.<br/>
    &nbsp;&nbsp;&nbsp;&nbsp;**5b.** Chaque tâche télécharge ses données d’entrée depuis Stockage Azure, puis commence l’exécution.<br/>
[**Étape 6.**](#step-6-monitor-tasks) Surveiller les tâches.<br/>
  &nbsp;&nbsp;&nbsp;&nbsp;**6a.** Comme les tâches sont effectuées, ils téléchargent leur tooAzure de données de sortie stockage.<br/>
[**Étape 7.**](#step-7-download-task-output) Télécharger la sortie des tâches à partir de Storage.

Comme indiqué précédemment, certaines solutions Batch ne suivent pas exactement cette procédure et peuvent exécuter de nombreuses autres opérations ; toutefois, cet exemple illustre les processus fréquemment inclus dans une solution Batch.

## <a name="prepare-client-script"></a>Préparer le script client
Avant d’exécuter les exemples hello, ajoutez vos informations d’identification de compte de stockage et de traitement par lots trop*python_tutorial_client.py*. Si vous n’avez pas déjà fait, ouvrez les fichier hello dans votre hello Favoris d’éditeur et de mise à jour de lignes avec vos informations d’identification suivantes.

```python
# Update hello Batch and Storage account credential strings below with hello values
# unique tooyour accounts. These are used when constructing connection strings
# for hello Batch and Storage client objects.

# Batch account credentials
BATCH_ACCOUNT_NAME = ""
BATCH_ACCOUNT_KEY = ""
BATCH_ACCOUNT_URL = ""

# Storage account credentials
STORAGE_ACCOUNT_NAME = ""
STORAGE_ACCOUNT_KEY = ""
```

Vous pouvez trouver vos informations d’identification compte Batch et de stockage dans le panneau de compte hello de chaque service Bonjour [portail Azure][azure_portal]:

![Traitement par lots les informations d’identification dans le portail de hello][9]
![informations d’identification de stockage dans le portail de hello][10]<br/>

Bonjour les sections suivantes, nous analysons les étapes hello utilisés par hello scripts tooprocess une charge de travail Bonjour service Batch. Nous vous encourageons toorefer régulièrement toohello des scripts dans votre éditeur pendant que vous progressez via rest hello d’article de hello.

Accédez toohello ligne dans **python_tutorial_client.py** toostart à l’étape 1 :

```python
if __name__ == '__main__':
```

## <a name="step-1-create-storage-containers"></a>Étape 1 : créer des conteneurs de stockage
![Créer des conteneurs dans le service Stockage Azure][1]
<br/>

Batch prend en charge l’interaction avec Azure Storage. Les conteneurs dans votre compte de stockage fournissent des fichiers de hello requis par les tâches de hello qui s’exécutent dans votre compte Batch. les conteneurs de Hello fournissent également des données de sortie de hello toostore sur place qui produisent des tâches de hello. Hello première hello *python_tutorial_client.py* du script est créer trois conteneurs dans [stockage d’objets Blob Azure](../storage/common/storage-introduction.md#blob-storage):

* **application**: ce conteneur stockera hello Python script exécuté par les tâches de hello, *python_tutorial_task.py*.
* **d’entrée**: tâches téléchargera tooprocess de fichiers de données hello hello *d’entrée* conteneur.
* **sortie**: lorsque les tâches de terminer le traitement du fichier d’entrée, ils téléchargeront hello résultats toohello *sortie* conteneur.

Dans l’ordre des toointeract avec un stockage de compte et de créer des conteneurs, nous utilisons hello [le stockage azure] [ pypi_storage] package toocreate un [BlockBlobService] [ py_blockblobservice] objet : hello « client de l’objet blob. » Ensuite, nous créons trois conteneurs hello compte de stockage à l’aide du client de blob hello.

```python
import azure.storage.blob as azureblob

# Create hello blob client, for use in obtaining references to
# blob storage containers and uploading files toocontainers.
blob_client = azureblob.BlockBlobService(
    account_name=STORAGE_ACCOUNT_NAME,
    account_key=STORAGE_ACCOUNT_KEY)

# Use hello blob client toocreate hello containers in Azure Storage if they
# don't yet exist.
APP_CONTAINER_NAME = 'application'
INPUT_CONTAINER_NAME = 'input'
OUTPUT_CONTAINER_NAME = 'output'
blob_client.create_container(APP_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(INPUT_CONTAINER_NAME, fail_on_exist=False)
blob_client.create_container(OUTPUT_CONTAINER_NAME, fail_on_exist=False)
```

Une fois que les conteneurs hello ont été créées, application hello peut maintenant télécharger des fichiers de hello qui seront utilisés par les tâches hello.

> [!TIP]
> [Comment toouse le stockage Blob Azure à partir de Python](../storage/blobs/storage-python-how-to-use-blob-storage.md) fournit une bonne vue d’ensemble de l’utilisation de conteneurs Azure Storage et les objets BLOB. Il doit être haut hello de votre liste de lecture commencer à utiliser avec le lot.
>
>

## <a name="step-2-upload-task-script-and-data-files"></a>Étape 2 : charger les scripts de tâche et les fichiers de données
![Tâche de chargement d’application et d’entrée (données) des fichiers toocontainers][2]
<br/>

Dans le fichier de hello Téléchargez opération, *python_tutorial_client.py* définit tout d’abord les collections de **application** et **d’entrée** chemins d’accès de fichiers tels qu’ils existent sur l’ordinateur local de hello. Puis il les télécharge ces conteneurs toohello de fichiers que vous avez créé à l’étape précédente de hello.

```python
# Paths toohello task script. This script will be executed by hello tasks that
# run on hello compute nodes.
application_file_paths = [os.path.realpath('python_tutorial_task.py')]

# hello collection of data files that are toobe processed by hello tasks.
input_file_paths = [os.path.realpath('./data/taskdata1.txt'),
                    os.path.realpath('./data/taskdata2.txt'),
                    os.path.realpath('./data/taskdata3.txt')]

# Upload hello application script tooAzure Storage. This is hello script that
# will process hello data files, and is executed by each of hello tasks on the
# compute nodes.
application_files = [
    upload_file_to_container(blob_client, APP_CONTAINER_NAME, file_path)
    for file_path in application_file_paths]

# Upload hello data files. This is hello data that will be processed by each of
# hello tasks executed on hello compute nodes in hello pool.
input_files = [
    upload_file_to_container(blob_client, INPUT_CONTAINER_NAME, file_path)
    for file_path in input_file_paths]
```

À l’aide de la compréhension de la liste, hello `upload_file_to_container` fonction est appelée pour chaque fichier dans les collections de hello et deux [ResourceFile] [ py_resource_file] collections sont remplies. Hello `upload_file_to_container` fonction apparaît ci-dessous :

```python
def upload_file_to_container(block_blob_client, container_name, path):
    """
    Uploads a local file tooan Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param str container_name: hello name of hello Azure Blob storage container.
    :param str file_path: hello local path toohello file.
    :rtype: `azure.batch.models.ResourceFile`
    :return: A ResourceFile initialized with a SAS URL appropriate for Batch
    tasks.
    """

    import datetime
    import azure.storage.blob as azureblob
    import azure.batch.models as batchmodels

    blob_name = os.path.basename(path)

    print('Uploading file {} toocontainer [{}]...'.format(path,
                                                          container_name))

    block_blob_client.create_blob_from_path(container_name,
                                            blob_name,
                                            file_path)

    sas_token = block_blob_client.generate_blob_shared_access_signature(
        container_name,
        blob_name,
        permission=azureblob.BlobPermissions.READ,
        expiry=datetime.datetime.utcnow() + datetime.timedelta(hours=2))

    sas_url = block_blob_client.make_blob_url(container_name,
                                              blob_name,
                                              sas_token=sas_token)

    return batchmodels.ResourceFile(file_path=blob_name,
                                    blob_source=sas_url)
```

### <a name="resourcefiles"></a>Objets ResourceFile
A [ResourceFile] [ py_resource_file] fournit des tâches dans un lot avec fichier de tooa hello URL dans le stockage Azure qui est téléchargé tooa nœud de calcul avant l’exécution de cette tâche. Hello [ResourceFile][py_resource_file]. **blob_source** propriété spécifie une URL complète du fichier de hello hello telle qu’elle existe dans le stockage Azure. URL de Hello peut-être également inclure une signature d’accès partagé (SAS) qui fournit un accès sécurisé toohello fichier. La propriété *ResourceFiles* est utilisée par la plupart des types de tâches dans Batch :

* [CloudTask][py_task]
* [StartTask][py_starttask]
* [JobPreparationTask][py_jobpreptask]
* [JobReleaseTask][py_jobreltask]

Cet exemple n’utilise pas de type hello JobPreparationTask ou JobReleaseTask les types de tâches, mais vous pouvez en savoir plus sur les [nœuds de calcul des tâches de préparation et l’achèvement de projet sur Azure Batch exécuter](batch-job-prep-release.md).

### <a name="shared-access-signature-sas"></a>Signature d’accès partagé (SAP)
Signatures d’accès partagé sont des chaînes qui fournissent un accès sécurisé toocontainers et objets BLOB dans le stockage Azure. Hello *python_tutorial_client.py* script utilise les deux objets blob et les signatures d’accès partagé de conteneur et montre comment tooobtain ces partagés accéder aux chaînes de signature à partir de hello service de stockage.

* **Signatures d’accès partagé d’objets BLOB**: utilise des StartTask du pool hello blob signatures d’accès partagé lorsqu’il télécharge hello tâche script et l’entrée des fichiers de données à partir du stockage (voir [étape 3](#step-3-create-batch-pool) ci-dessous). Hello `upload_file_to_container` fonctionner dans *python_tutorial_client.py* contient le code hello qui obtient la signature d’accès partagé de l’objet blob. Il le fait en appelant [BlockBlobService.make_blob_url] [ py_make_blob_url] dans le module de stockage hello.
* **Signature d’accès partagé de conteneur**: que chaque tâche a terminé son travail sur le nœud de calcul hello, il télécharge sa toohello de fichier de sortie *sortie* conteneur dans le stockage Azure. toodo, *python_tutorial_task.py* utilise une signature d’accès partagé de conteneur qui fournit un accès en écriture toohello conteneur. Hello `get_container_sas_token` fonctionner dans *python_tutorial_client.py* Obtient la signature d’accès partagé du conteneur hello, qui est ensuite passée en tant que tâches de toohello un argument de ligne de commande. Étape 5 de #, [travail de tooa tâches ajouter](#step-5-add-tasks-to-job), traite de l’utilisation de hello de SAP de conteneur hello.

> [!TIP]
> Extraction de série en deux parties hello sur les signatures d’accès partagé, [partie 1 : modèle de présentation hello SAP](../storage/common/storage-dotnet-shared-access-signature-part-1.md) et [partie 2 : créer et utiliser une SAP avec hello service Blob](../storage/blobs/storage-dotnet-shared-access-signature-part-2.md), toolearn plus de fournir un accès sécurisé toodata dans votre compte de stockage.
>
>

## <a name="step-3-create-batch-pool"></a>Étape 3 : créer le pool Batch
![Créer un pool Batch][3]
<br/>

Un **pool** Batch est une collection de nœuds de calcul (machines virtuelles) sur lequel Batch exécute les tâches d’un travail.

Une fois qu’il télécharge hello tâche script et les données de fichiers toohello compte de stockage, *python_tutorial_client.py* démarre son interaction avec le service de traitement par lots hello à l’aide du module de traitement par lots Python hello. toodo, un [BatchServiceClient] [ py_batchserviceclient] est créé :

```python
# Create a Batch service client. We'll now be interacting with hello Batch
# service in addition tooStorage.
credentials = batchauth.SharedKeyCredentials(BATCH_ACCOUNT_NAME,
                                             BATCH_ACCOUNT_KEY)

batch_client = batch.BatchServiceClient(
    credentials,
    base_url=BATCH_ACCOUNT_URL)
```

Ensuite, un pool de nœuds de calcul est créé dans hello compte Batch avec un appel trop`create_pool`.

```python
def create_pool(batch_service_client, pool_id,
                resource_files, publisher, offer, sku):
    """
    Creates a pool of compute nodes with hello specified OS settings.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str pool_id: An ID for hello new pool.
    :param list resource_files: A collection of resource files for hello pool's
    start task.
    :param str publisher: Marketplace image publisher
    :param str offer: Marketplace image offer
    :param str sku: Marketplace image sku
    """
    print('Creating pool [{}]...'.format(pool_id))

    # Create a new pool of Linux compute nodes using an Azure Virtual Machines
    # Marketplace image. For more information about creating pools of Linux
    # nodes, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/

    # Specify hello commands for hello pool's start task. hello start task is run
    # on each node as it joins hello pool, and when it's rebooted or re-imaged.
    # We use hello start task tooprep hello node for running our task script.
    task_commands = [
        # Copy hello python_tutorial_task.py script toohello "shared" directory
        # that all tasks that run on hello node have access to.
        'cp -r $AZ_BATCH_TASK_WORKING_DIR/* $AZ_BATCH_NODE_SHARED_DIR',
        # Install pip and hello dependencies for cryptography
        'apt-get update',
        'apt-get -y install python-pip',
        'apt-get -y install build-essential libssl-dev libffi-dev python-dev',
        # Install hello azure-storage module so that hello task script can access
        # Azure Blob storage
        'pip install azure-storage']

    # Get hello node agent SKU and image reference for hello virtual machine
    # configuration.
    # For more information about hello virtual machine configuration, see:
    # https://azure.microsoft.com/documentation/articles/batch-linux-nodes/
    sku_to_use, image_ref_to_use = \
        common.helpers.select_latest_verified_vm_image_with_node_agent_sku(
            batch_service_client, publisher, offer, sku)

    new_pool = batch.models.PoolAddParameter(
        id=pool_id,
        virtual_machine_configuration=batchmodels.VirtualMachineConfiguration(
            image_reference=image_ref_to_use,
            node_agent_sku_id=sku_to_use),
        vm_size=_POOL_VM_SIZE,
        target_dedicated=_POOL_NODE_COUNT,
        start_task=batch.models.StartTask(
            command_line=
            common.helpers.wrap_commands_in_shell('linux', task_commands),
            run_elevated=True,
            wait_for_success=True,
            resource_files=resource_files),
        )

    try:
        batch_service_client.pool.add(new_pool)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Lorsque vous créez un pool, vous définissez un [PoolAddParameter] [ py_pooladdparam] qui spécifie plusieurs propriétés pour le pool de hello :

* **ID** de pool de hello (*id* - requis)<p/>Comme pour la plupart des entités dans Batch, votre nouveau pool doit avoir un ID unique au sein de votre compte Batch. Votre code fait référence à l’aide de son ID de pool de toothis, et c’est la façon dont vous identifiez pool hello Bonjour Azure [portal][azure_portal].
* **Nombre de nœuds de calcul** (*target_dedicated* - obligatoire)<p/>Cette propriété spécifie le nombre de machines virtuelles doivent être déployés dans le pool de hello. Il est important toonote que tous les comptes de traitement par lots ont une valeur par défaut **quota** que limites hello nombre de **cœurs** (et par conséquent, les nœuds de calcul) dans un compte de traitement par lots. Vous trouverez les quotas par défaut hello et obtenir des instructions sur la façon de trop[un quota de](batch-quota-limit.md#increase-a-quota) (par exemple, le nombre maximal de hello de cœurs dans votre compte Batch) dans [Quotas et limites pour hello service Azure Batch](batch-quota-limit.md). Si vous vous demandez pourquoi votre pool n’atteint pas plus de X nœuds, Ce quota de base peut être la cause de hello.
* **Système d’exploitation** pour les nœuds (*virtual_machine_configuration***ou***cloud_service_configuration* - obligatoire)<p/>Dans *python_tutorial_client.py*, nous créons un pool de nœuds Linux à l’aide de [VirtualMachineConfiguration][py_vm_config]. Hello `select_latest_verified_vm_image_with_node_agent_sku` fonctionner dans `common.helpers` simplifie l’utilisation de [Azure Marketplace de Machines virtuelles] [ vm_marketplace] images. Pour plus d’informations sur l’utilisation des images du Marketplace, voir [Configurer des nœuds de calcul Linux dans des pools Azure Batch](batch-linux-nodes.md) .
* **Taille des nœuds de calcul** (*vm_size* - obligatoire)<p/>Étant donné que nous spécifions des nœuds Linux pour notre [VirtualMachineConfiguration][py_vm_config], nous spécifions une taille de machine virtuelle (`STANDARD_A1` dans cet exemple) parmi les [tailles des machines virtuelles dans Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Pour plus d’informations, voir [Configurer des nœuds de calcul Linux dans des pools Azure Batch](batch-linux-nodes.md) .
* **Tâche de démarrage** (*start_task* : non obligatoire)<p/>En même temps que hello au-dessus des propriétés d’un nœud physique, vous pouvez également spécifier un [StartTask] [ py_starttask] pour le pool hello (il n’est pas obligatoire). Hello StartTask s’exécute sur chaque nœud de ce nœud rejoint le pool de hello, chaque fois qu’un nœud est redémarré. Hello StartTask est particulièrement utile pour la préparation des nœuds de calcul pour l’exécution de hello de tâches, telles que l’installation d’applications hello qui exécutent des tâches.<p/>Dans cet exemple d’application, hello StartTask copie les fichiers de hello qu’il télécharge à partir du stockage (qui sont spécifié à l’aide de hello StartTask **resource_files** propriété) à partir de hello StartTask *répertoire de travail* toohello *partagé* Active toutes les tâches en cours d’exécution sur le nœud de hello peuvent accéder. Pour l’essentiel, cette copie `python_tutorial_task.py` toohello répertoire partagé sur chaque nœud comme nœud de hello rejoint le pool de hello, afin que toutes les tâches qui s’exécutent sur le nœud de hello puissent y accéder.

Vous pouvez remarquer hello appel toohello `wrap_commands_in_shell` fonction d’assistance. Cette fonction prend une collection de commandes distinctes et crée une ligne de commande unique adaptée à la propriété de ligne de commande d’une tâche.

Remarquables dans l’extrait de code hello ci-dessus est également utiliser deux variables d’environnement Bonjour hello **lettre** propriété Hello StartTask : `AZ_BATCH_TASK_WORKING_DIR` et `AZ_BATCH_NODE_SHARED_DIR`. Chaque nœud de calcul au sein d’un pool de traitement par lots est automatiquement configuré avec plusieurs variables d’environnement qui sont tooBatch spécifique. Tout processus qui est exécutée par une tâche a des variables d’environnement toothese accès.

> [!TIP]
> toofind plus d’informations sur les variables d’environnement hello qui sont disponibles sur les nœuds de calcul dans un pool de traitement par lots, ainsi que les informations sur les répertoires de travail tâche, consultez **paramètres d’environnement pour les tâches** et **fichiers et répertoires**  Bonjour [vue d’ensemble des fonctionnalités de traitement par lots Azure](batch-api-basics.md).
>
>

## <a name="step-4-create-batch-job"></a>Étape 4 : créer un travail Batch
![Créer un travail Batch][4]<br/>

Un **travail** Batch constitue un ensemble de tâches et est associé à un pool de nœuds de calcul. tâches de Hello dans un travail s’exécutent sur les nœuds de calcul du pool hello associé.

Vous pouvez utiliser une tâche pour l’organisation et le suivi des tâches dans les charges de travail, mais également pour imposer certaines contraintes--par exemple hello durée d’exécution pour le travail de hello (et par extension, ses tâches) et priorité des travaux dans les tâches de tooother de relation dans hello compte Batch. Dans cet exemple, toutefois, les travaux de hello est associé uniquement à pool hello qui a été créé à l’étape 3 de #. Aucune propriété supplémentaire n’est configurée.

Tous les travaux Batch sont associés à un pool spécifique. Cette association indique les nœuds d’exécutent des tâches du travail hello sur. Vous spécifiez un pool de hello à l’aide de hello [PoolInformation] [ py_poolinfo] propriété, comme indiqué dans l’extrait de code hello ci-dessous.

```python
def create_job(batch_service_client, job_id, pool_id):
    """
    Creates a job with hello specified ID, associated with hello specified pool.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID for hello job.
    :param str pool_id: hello ID for hello pool.
    """
    print('Creating job [{}]...'.format(job_id))

    job = batch.models.JobAddParameter(
        job_id,
        batch.models.PoolInformation(pool_id=pool_id))

    try:
        batch_service_client.job.add(job)
    except batchmodels.batch_error.BatchErrorException as err:
        print_batch_exception(err)
        raise
```

Maintenant qu’un travail a été créé, les tâches sont ajoutées travail hello de tooperform.

## <a name="step-5-add-tasks-toojob"></a>Étape 5 : Ajouter des tâches toojob
![Ajouter des tâches toojob][5]<br/>
*(1) tâches sont ajoutés toohello travail, tâches de hello (2) sont planifiée toorun sur les nœuds et les tâches hello (3) téléchargement tooprocess de fichiers de données hello*

Lot **tâches** sont des nœuds de calcul hello unités de travail individuelles qui s’exécutent sur hello. Une tâche a une ligne de commande et exécute les scripts hello ou exécutables que vous spécifiez dans cette ligne de commande.

tooactually effectuer un travail, de tâches doivent être ajoutées à une tâche tooa. Chaque [CloudTask] [ py_task] est configuré avec une propriété de ligne de commande et [ResourceFiles] [ py_resource_file] (comme avec la tâche de début du pool hello) que hello tâche télécharge toohello nœud avant sa ligne de commande est exécutée automatiquement. Dans l’exemple hello, chaque tâche traite un seul fichier. Par conséquent, sa collection ResourceFiles contient un seul élément.

```python
def add_tasks(batch_service_client, job_id, input_files,
              output_container_name, output_container_sas_token):
    """
    Adds a task for each input file in hello collection toohello specified job.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello ID of hello job toowhich tooadd hello tasks.
    :param list input_files: A collection of input files. One task will be
     created for each input file.
    :param output_container_name: hello ID of an Azure Blob storage container to
    which hello tasks will upload their results.
    :param output_container_sas_token: A SAS token granting write access to
    hello specified Azure Blob storage container.
    """

    print('Adding {} tasks toojob [{}]...'.format(len(input_files), job_id))

    tasks = list()

    for input_file in input_files:

        command = ['python $AZ_BATCH_NODE_SHARED_DIR/python_tutorial_task.py '
                   '--filepath {} --numwords {} --storageaccount {} '
                   '--storagecontainer {} --sastoken "{}"'.format(
                    input_file.file_path,
                    '3',
                    _STORAGE_ACCOUNT_NAME,
                    output_container_name,
                    output_container_sas_token)]

        tasks.append(batch.models.TaskAddParameter(
                'topNtask{}'.format(input_files.index(input_file)),
                wrap_commands_in_shell('linux', command),
                resource_files=[input_file]
                )
        )

    batch_service_client.task.add_collection(job_id, tasks)
```

> [!IMPORTANT]
> Lorsque leur accès aux variables d’environnement telles que `$AZ_BATCH_NODE_SHARED_DIR` ou exécuter une application introuvable dans du nœud hello `PATH`, lignes de commande de tâche doit appeler hello interface explicitement, comme avec `/bin/sh -c MyTaskApplication $MY_ENV_VAR`. Cette exigence n’est pas nécessaire si vos tâches exécutent une application dans du nœud hello `PATH` et ne font pas référence à des variables d’environnement.
>
>

Au sein de hello `for` boucle dans l’extrait de code hello ci-dessus, vous pouvez voir que la ligne de commande hello pour la tâche hello est construite avec cinq arguments de ligne de commande qui sont passés trop*python_tutorial_task.py*:

1. **FilePath**: il s’agit hello chemin d’accès local toohello fichier tel qu’il existe sur le nœud de hello. Lorsque hello objet ResourceFile dans `upload_file_to_container` a été créé à l’étape 2 ci-dessus, le nom de fichier hello a été utilisée pour cette propriété (hello `file_path` paramètre hello ResourceFile constructeur). Cela indique que hello fichier se trouve dans hello même nœud hello en tant que répertoire *python_tutorial_task.py*.
2. **NUMWORDS**: haut de hello *N* mots doivent être écrits en fichier de sortie toohello.
3. **storageaccount**: nom hello Hello compte de stockage qui est propriétaire du résultat de la tâche hello conteneur toowhich hello doit être téléchargé.
4. **storagecontainer**: nom de hello Hello de toowhich de conteneur de stockage hello sortie de fichiers doivent être téléchargés.
5. **sastoken**: signature hello accès partagé (SAP) qui fournit un accès en écriture toohello **sortie** conteneur dans le stockage Azure. Hello *python_tutorial_task.py* script utilise cette signature d’accès partagé lorsque crée sa référence BlockBlobService. Cela fournit un accès en écriture toohello conteneur sans nécessiter une clé d’accès pour le compte de stockage hello.

```python
# NOTE: Taken from python_tutorial_task.py

# Create hello blob client using hello container's SAS token.
# This allows us toocreate a client that provides write
# access only toohello container.
blob_client = azureblob.BlockBlobService(account_name=args.storageaccount,
                                         sas_token=args.sastoken)
```

## <a name="step-6-monitor-tasks"></a>Étape 6 : surveiller les tâches
![Surveiller les tâches][6]<br/>
*Hello tâches hello moniteurs (1) pour l’état d’achèvement et les tâches hello (2) téléchargement tooAzure de données de résultat stockage*

Lorsque les tâches sont ajoutées tooa travail, ils sont en file d’attente et planifiés pour l’exécution sur des nœuds de calcul dans le pool hello associé hello travail automatiquement. Selon les paramètres que vous spécifiez hello, lot gère queuing à toutes les tâches, la planification, une nouvelle tentative et autres tâches d’administration de tâche pour vous.

Il existe de nombreuses approches toomonitoring exécution de la tâche. Hello `wait_for_tasks_to_complete` fonctionner dans *python_tutorial_client.py* fournit un exemple simple de tâches de surveillance pour un certain état, dans ce cas, hello [terminé] [ py_taskstate] état.

```python
def wait_for_tasks_to_complete(batch_service_client, job_id, timeout):
    """
    Returns when all tasks in hello specified job reach hello Completed state.

    :param batch_service_client: A Batch service client.
    :type batch_service_client: `azure.batch.BatchServiceClient`
    :param str job_id: hello id of hello job whose tasks should be toomonitored.
    :param timedelta timeout: hello duration toowait for task completion. If all
    tasks in hello specified job do not reach Completed state within this time
    period, an exception will be raised.
    """
    timeout_expiration = datetime.datetime.now() + timeout

    print("Monitoring all tasks for 'Completed' state, timeout in {}..."
          .format(timeout), end='')

    while datetime.datetime.now() < timeout_expiration:
        print('.', end='')
        sys.stdout.flush()
        tasks = batch_service_client.task.list(job_id)

        incomplete_tasks = [task for task in tasks if
                            task.state != batchmodels.TaskState.completed]
        if not incomplete_tasks:
            print()
            return True
        else:
            time.sleep(1)

    print()
    raise RuntimeError("ERROR: Tasks did not reach 'Completed' state within "
                       "timeout period of " + str(timeout))
```

## <a name="step-7-download-task-output"></a>Étape 7 : télécharger la sortie des tâches
![Télécharger la sortie des tâches à partir du service Stockage][7]<br/>

Maintenant que hello tâche terminée, sortie hello des tâches de hello peut être téléchargé depuis le stockage Azure. Cette opération s’effectue avec un appel trop`download_blobs_from_container` dans *python_tutorial_client.py*:

```python
def download_blobs_from_container(block_blob_client,
                                  container_name, directory_path):
    """
    Downloads all blobs from hello specified Azure Blob storage container.

    :param block_blob_client: A blob service client.
    :type block_blob_client: `azure.storage.blob.BlockBlobService`
    :param container_name: hello Azure Blob storage container from which to
     download files.
    :param directory_path: hello local directory toowhich toodownload hello files.
    """
    print('Downloading all files from container [{}]...'.format(
        container_name))

    container_blobs = block_blob_client.list_blobs(container_name)

    for blob in container_blobs.items:
        destination_file_path = os.path.join(directory_path, blob.name)

        block_blob_client.get_blob_to_path(container_name,
                                           blob.name,
                                           destination_file_path)

        print('  Downloaded blob [{}] from container [{}] too{}'.format(
            blob.name,
            container_name,
            destination_file_path))

    print('  Download complete!')
```

> [!NOTE]
> Hello appel trop`download_blobs_from_container` dans *python_tutorial_client.py* Spécifie que les fichiers hello doivent être téléchargé tooyour répertoire de base. Pensez toomodify libre cette sortie d’emplacement.
>
>

## <a name="step-8-delete-containers"></a>Étape 8 : supprimer les conteneurs
Vous êtes facturé pour les données qui résident dans le stockage Azure, il est toujours un tooremove recommandé que tous les objets BLOB qui ne sont plus nécessaires pour vos traitements par lots. Dans *python_tutorial_client.py*, cette opération s’effectue avec trois appels trop[BlockBlobService.delete_container][py_delete_container]:

```python
# Clean up storage resources
print('Deleting containers...')
blob_client.delete_container(app_container_name)
blob_client.delete_container(input_container_name)
blob_client.delete_container(output_container_name)
```

## <a name="step-9-delete-hello-job-and-hello-pool"></a>Étape 9 : Supprimer le travail de hello et pool de hello
À l’étape finale de hello, vous êtes le pool de travail et hello de hello toodelete demandées qui ont été créés par hello *python_tutorial_client.py* script. Bien que vous ne soyez pas facturé pour les travaux et les tâches à proprement parler, les nœuds de calcul vous *sont* facturés. Par conséquent, nous vous conseillons d’affecter les nœuds uniquement en fonction des besoins. La suppression des pools inutilisés peut être incluse dans votre processus de maintenance.

Hello BatchServiceClient [JobOperations] [ py_job] et [PoolOperations] [ py_pool] ont tous deux des méthodes de suppression correspondantes, qui sont appelé si vous confirmez la suppression :

```python
# Clean up Batch resources (if hello user so chooses).
if query_yes_no('Delete job?') == 'yes':
    batch_client.job.delete(_JOB_ID)

if query_yes_no('Delete pool?') == 'yes':
    batch_client.pool.delete(_POOL_ID)
```

> [!IMPORTANT]
> N’oubliez pas que les ressources de calcul vous sont facturées et que la suppression des pools inutilisés vous permet de réduire les coûts. En outre, n’oubliez pas que la suppression d’un pool supprime tous les nœuds de calcul dans ce pool, et que toutes les données sur les nœuds hello seront irrécupérables après la suppression d’un pool de hello.
>
>

## <a name="run-hello-sample-script"></a>Exécutez le script d’exemple hello
Lorsque vous exécutez hello *python_tutorial_client.py* script à partir du didacticiel de hello [exemple de code][github_article_samples], la sortie de console hello est similaire toohello suivant. Il existe une pause à `Monitoring all tasks for 'Completed' state, timeout in 0:20:00...` tandis que les nœuds de calcul du pool hello sont créés, démarré, et la tâche de démarrage du pool hello hello commandes est exécutées. Hello d’utilisation [portail Azure] [ azure_portal] toomonitor votre pool, nœuds de calcul, tâche et pendant et après l’exécution des tâches. Hello d’utilisation [portail Azure] [ azure_portal] ou hello [Microsoft Azure Storage Explorer] [ storage_explorer] tooview les ressources de stockage hello (conteneurs et objets BLOB) qui sont créés par l’application hello.

> [!TIP]
> Exécutez hello *python_tutorial_client.py* script à partir de hello `azure-batch-samples/Python/Batch/article_samples` active. Il utilise un chemin d’accès relatif pour hello `common.helpers` importation du module, vous voyez `ImportError: No module named 'common'` si vous n’exécutez pas script hello à partir de ce répertoire.
>
>

Temps d’exécution par défaut est **environ 5 à 7 minutes** lorsque vous exécutez exemple hello dans sa configuration par défaut.

```
Sample start: 2016-05-20 22:47:10

Uploading file /home/user/py_tutorial/python_tutorial_task.py toocontainer [application]...
Uploading file /home/user/py_tutorial/data/taskdata1.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata2.txt toocontainer [input]...
Uploading file /home/user/py_tutorial/data/taskdata3.txt toocontainer [input]...
Creating pool [PythonTutorialPool]...
Creating job [PythonTutorialJob]...
Adding 3 tasks toojob [PythonTutorialJob]...
Monitoring all tasks for 'Completed' state, timeout in 0:20:00..........................................................................
  Success! All tasks reached hello 'Completed' state within hello specified timeout period.
Downloading all files from container [output]...
  Downloaded blob [taskdata1_OUTPUT.txt] from container [output] too/home/user/taskdata1_OUTPUT.txt
  Downloaded blob [taskdata2_OUTPUT.txt] from container [output] too/home/user/taskdata2_OUTPUT.txt
  Downloaded blob [taskdata3_OUTPUT.txt] from container [output] too/home/user/taskdata3_OUTPUT.txt
  Download complete!
Deleting containers...

Sample end: 2016-05-20 22:53:12
Elapsed time: 0:06:02

Delete job? [Y/n]
Delete pool? [Y/n]

Press ENTER tooexit...
```

## <a name="next-steps"></a>Étapes suivantes
Estimez les modifications toomake libre trop*python_tutorial_client.py* et *python_tutorial_task.py* tooexperiment avec différents scénarios de calcul. Par exemple, essayez d’ajouter un délai d’exécution trop*python_tutorial_task.py* toosimulate longue des tâches et les surveiller dans le portail de hello. Essayez d’ajouter des tâches plus ou en ajustant de nombre hello de nœuds de calcul. Ajouter toocheck logique pour autoriser l’utilisation de hello de durée d’exécution de toospeed pool existant

Maintenant que vous êtes familiarisé avec les flux de travail de base hello d’une solution de traitement par lots, il est toodig de temps dans toohello des fonctionnalités supplémentaires de hello service Batch.

* Hello de révision [les fonctionnalités de présentation d’Azure Batch](batch-api-basics.md) article, nous vous recommandons de si vous êtes de nouveau service toohello.
* Démarrer sur hello autres articles de développement de lot sous **développement approfondie** Bonjour [cursus lot][batch_learning_path].
* Extraire une implémentation différente du traitement de charge de travail hello « N premiers mots » traitement par lots Bonjour [TopNWords] [ github_topnwords] exemple.

[azure_batch]: https://azure.microsoft.com/services/batch/
[azure_free_account]: https://azure.microsoft.com/free/
[azure_portal]: https://portal.azure.com
[batch_learning_path]: https://azure.microsoft.com/documentation/learning-paths/batch/
[blog_linux]: http://blogs.technet.com/b/windowshpc/archive/2016/03/30/introducing-linux-support-on-azure-batch.aspx
[crypto]: https://cryptography.io/en/latest/
[crypto_install]: https://cryptography.io/en/latest/installation/
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_zip]: https://github.com/Azure/azure-batch-samples/archive/master.zip
[github_topnwords]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/TopNWords
[github_article_samples]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/article_samples

[nuget_packagemgr]: https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c
[nuget_restore]: https://docs.nuget.org/consume/package-restore/msbuild-integrated#enabling-package-restore-during-build

[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_batchserviceclient]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.html#azure.batch.BatchServiceClient
[py_blockblobservice]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.blockblobservice.html#azure.storage.blob.blockblobservice.BlockBlobService
[py_cloudtask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_cs_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudServiceConfiguration
[py_delete_container]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.delete_container
[py_gen_blob_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_blob_shared_access_signature
[py_gen_container_sas]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.generate_container_shared_access_signature
[py_image_ref]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/latest/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_job]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.JobOperations
[py_jobpreptask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobPreparationTask
[py_jobreltask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.JobReleaseTask
[py_list_skus]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[py_make_blob_url]: http://azure.github.io/azure-storage-python/ref/azure.storage.blob.baseblobservice.html#azure.storage.blob.baseblobservice.BaseBlobService.make_blob_url
[py_pool]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.operations.html#azure.batch.operations.PoolOperations
[py_pooladdparam]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolAddParameter
[py_poolinfo]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.PoolInformation
[py_resource_file]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.ResourceFile
[py_samples_github]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch/
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_starttask]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.StartTask
[py_task]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.CloudTask
[py_taskstate]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.TaskState
[py_vm_config]: http://azure-sdk-for-python.readthedocs.io/en/latest/ref/azure.batch.models.html#azure.batch.models.VirtualMachineConfiguration
[pypi_batch]: https://pypi.python.org/pypi/azure-batch
[pypi_storage]: https://pypi.python.org/pypi/azure-storage
[pypi_install]: https://packaging.python.org/installing/
[storage_explorer]: http://storageexplorer.com/
[visual_studio]: https://www.visualstudio.com/products/vs-2015-product-editions
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/

[1]: ./media/batch-python-tutorial/batch_workflow_01_sm.png "Créer des conteneurs dans le Stockage Azure"
[2]: ./media/batch-python-tutorial/batch_workflow_02_sm.png "Tâche de chargement d’application et d’entrée (données) des fichiers toocontainers"
[3]: ./media/batch-python-tutorial/batch_workflow_03_sm.png "Créer un pool Batch"
[4]: ./media/batch-python-tutorial/batch_workflow_04_sm.png "Créer un travail Batch"
[5]: ./media/batch-python-tutorial/batch_workflow_05_sm.png "Ajouter des tâches toojob"
[6]: ./media/batch-python-tutorial/batch_workflow_06_sm.png "Surveiller les tâches"
[7]: ./media/batch-python-tutorial/batch_workflow_07_sm.png "Télécharger la sortie des tâches à partir de Storage"
[8]: ./media/batch-python-tutorial/batch_workflow_sm.png "Flux de travail de la solution Batch (diagramme complet)"
[9]: ./media/batch-python-tutorial/credentials_batch_sm.png "Informations d’identification de compte Batch dans le portail"
[10]: ./media/batch-python-tutorial/credentials_storage_sm.png "Informations d’identification de compte de stockage dans le portail"
[11]: ./media/batch-python-tutorial/batch_workflow_minimal_sm.png "Flux de travail de la solution Batch (diagramme minimal)"
