---
title: "machines virtuelles d’aaaMigrating tooAzure stockage Premium | Documents Microsoft"
description: "Migrez votre tooAzure de machines virtuelles existante stockage Premium. Premium Storage offre une prise en charge très performante et à faible latence des disques pour les charges de travail utilisant beaucoup d'E/S exécutées sur les machines virtuelles Azure."
services: storage
documentationcenter: na
author: yuemlu
manager: tadb
editor: tysonn
ms.assetid: 272250b3-fd4e-41d2-8e34-fd8cc341ec87
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: yuemlu
ms.openlocfilehash: cd812bdbe39f43fe053a998d96788045d5a43258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="migrating-tooazure-premium-storage-unmanaged-disks"></a>Migration tooAzure Premium stockage (disques non managées)

> [!NOTE]
> Cet article explique comment toomigrate une machine virtuelle qui utilise des disques standard non managé tooa ordinateur virtuel qui utilise non managée disques premium. Nous vous recommandons d’utiliser des disques de Azure géré pour les nouvelles machines virtuelles, et que vous convertissez vos disques toomanaged de disques non managé précédente. Géré les comptes de stockage sous-jacent de disques handle hello afin que vous n’êtes pas obligé. Pour plus d’informations, consultez [Vue d’ensemble d’Azure Managed Disks](storage-managed-disks-overview.md).
>

Azure Premium Storage offre une prise en charge très performante et à faible latence des disques pour les machines virtuelles exécutant des charges de travail qui utilisent beaucoup d'E/S. Vous pouvez tirer parti de la vitesse de hello et les performances de ces disques en effectuant une migration tooAzure de disques de machine virtuelle de votre application stockage Premium.

Hello de ce guide vise toohelp nouveaux utilisateurs de stockage Azure Premium mieux préparer toomake une transition en douceur de leur tooPremium système actuel stockage. guide de Hello traite des trois composants clés de hello dans ce processus :

* [Planifier la Migration de hello tooPremium stockage](#plan-the-migration-to-premium-storage)
* [Préparer et copier les disques durs virtuels (VHD) tooPremium stockage](#prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage)
* [Création d’une machine virtuelle Azure utilisant Premium Storage](#create-azure-virtual-machine-using-premium-storage)

Vous pouvez migrer des machines virtuelles à partir d’autres plateformes de tooAzure stockage Premium ou migrer des machines virtuelles Azure existantes à partir du stockage Standard tooPremium stockage. Ce guide décrit les étapes pour les deux scénarios. Suivez les étapes de hello spécifiés dans la section pertinentes de hello en fonction de votre scénario.

> [!NOTE]
> Vous pouvez consulter un aperçu des fonctionnalités et de la tarification dans [Premium Storage : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md). Nous vous recommandons de migrer n’importe quel disque de machine virtuelle nécessitant une haute IOPS tooAzure stockage Premium pour optimiser les performances hello pour votre application. Si votre disque ne nécessite pas un nombre élevé d'IOPS, vous pouvez limiter les coûts en le conservant dans le stockage Standard qui stocke les données de disque de machine virtuelle sur des disques durs et non des disques SSD.
>

Fin du processus de migration hello dans son intégralité peut nécessiter des actions supplémentaires avant et après les étapes hello fournies dans ce guide. Configuration des réseaux virtuels ou des points de terminaison ou l’apport de modifications du code au sein de l’application hello elle-même et ce qui peut nécessiter un temps d’arrêt dans votre application sont des exemples. Ces actions sont tooeach unique à l’application, et elles doivent être exécutées en même temps que les étapes de hello fournies dans cette tooPremium de transition complète guide toomake hello plus transparent possible du stockage.

## <a name="plan-the-migration-to-premium-storage"></a>Planifier la migration de hello tooPremium stockage
Cette section permet de s’assurer que vous êtes prêt toofollow étapes de migration hello dans cet article et vous aide à toomake hello meilleure décision sur les types de machine virtuelle et le disque.

### <a name="prerequisites"></a>Composants requis
* Vous aurez besoin d’un abonnement Azure. Si vous n’en avez pas, vous pouvez souscrire un abonnement pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/) d’un mois ou visiter [Tarification Azure](https://azure.microsoft.com/pricing/) pour plus d’options.
* tooexecute applets de commande PowerShell, vous aurez besoin de module de Microsoft Azure PowerShell hello. Consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview) Pourquoi installer instructions d’installation et de point.
* Lorsque vous planifiez des machines virtuelles Azure de toouse en cours d’exécution sur le stockage Premium, vous devez toouse hello machines virtuelles capables de stockage Premium. Vous pouvez utiliser des disques de Stockage Standard et Premium avec les machines virtuelles compatibles avec Premium Storage. Les disques de stockage Premium sera disponibles avec plusieurs types de machine virtuelle Bonjour futures. Pour plus d’informations sur les tailles et les types de disque de machine virtuelle Azure disponibles, consultez [Tailles des machines virtuelles](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [Tailles des services cloud](../cloud-services/cloud-services-sizes-specs.md).

### <a name="considerations"></a>Considérations
Une machine virtuelle Azure prend en charge l’attachement de plusieurs disques de stockage Premium afin que vos applications peuvent avoir jusqu'à to too256 de stockage par la machine virtuelle. Avec Premium Storage, vos applications peuvent atteindre jusqu'à 80 000 IOPS (opérations d'E/S par seconde) par machine virtuelle et un débit de disque de 2 000 Mo par seconde, avec une latence extrêmement faible pour les opérations de lecture. Vous disposez de diverses options de machines virtuelles et disques. Cette section est toohelp toofind une option qui convient le mieux à votre charge de travail.

#### <a name="vm-sizes"></a>Tailles de machine virtuelle
spécifications de taille de machine virtuelle Azure Hello sont répertoriées dans [tailles des machines virtuelles](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Passez en revue les caractéristiques de performances hello d’ordinateurs virtuels qui fonctionnent avec un stockage Premium et choisissez hello plus approprié taille de machine virtuelle qui convient le mieux à votre charge de travail. Assurez-vous qu’il y suffisamment de bande passante disponible sur votre trafic de disque de machine virtuelle toodrive hello.

#### <a name="disk-sizes"></a>Tailles du disque
Il existe cinq types de disque qui peuvent être utilisés avec votre machine virtuelle et chacun d’eux présentant des limites d’E/S par seconde et de débits spécifiques. Prenez en compte ces limites lorsqu’en choisissant le type de disque hello pour votre machine virtuelle en fonction des besoins de hello de votre application en termes de capacité, les performances, l’évolutivité, et des pics.

| Type de disque Premium  | P10   | P20   | P30            | P40            | P50            | 
|:-------------------:|:-----:|:-----:|:--------------:|:--------------:|:--------------:|
| Taille du disque           | 128 Go| 512 Go| 1024 Go (1 To) | 2 048 Go (2 To) | 4 095 Go (4 To) | 
| IOPS par disque       | 500   | 2 300  | 5 000           | 7500           | 7500           | 
| Débit par disque | 100 Mo par seconde | 150 Mo par seconde | 200 Mo par seconde | 250 Mo par seconde | 250 Mo par seconde |

En fonction de votre charge de travail, déterminez si les disques de données supplémentaires sont nécessaires pour votre machine virtuelle. Vous pouvez attacher plusieurs tooyour de disques de données persistantes machine virtuelle. Si nécessaire, vous pouvez répartir sur la capacité de hello disques tooincrease hello et les performances du volume de hello. (Découvrez ce qu’est l’entrelacement de disques [ici](storage-premium-storage-performance.md#disk-striping).) Si vous équilibrez les disques de données Stockage Premium à l’aide des [espaces de stockage][4], vous devez les configurer avec une colonne pour chaque disque utilisé. Dans le cas contraire, hello globalement les performances du volume de hello agrégés par bande peuvent être inférieure que prévu en raison de la distribution toouneven du trafic sur les disques hello. Pour les machines virtuelles Linux, vous pouvez utiliser hello *mdadm* utilitaire tooachieve hello identiques. Consultez l’article [Configuration d’un RAID logiciel sur Linux](../virtual-machines/linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) pour plus d’informations.

#### <a name="storage-account-scalability-targets"></a>Objectifs d’évolutivité de compte de stockage
Comptes de stockage Premium ont hello suivant les objectifs d’évolutivité dans Ajout toohello [évolutivité du stockage Azure et les objectifs de performances](storage-scalability-targets.md). Si les exigences de votre application dépassent les objectifs d’évolutivité hello d’un compte de stockage unique, générez votre toouse application plusieurs comptes de stockage et partitionner vos données sur ces comptes de stockage.

| Capacité totale des comptes | Bande passante totale pour un compte de stockage localement redondant |
|:--- |:--- |
| Capacité du disque : 35 To<br />Capacité d’instantané : 10 To |Les too50 les gigabits par seconde pour entrante + sortante |

Pour hello plus d’informations sur les spécifications de stockage Premium, consultez [objectifs d’évolutivité et performances lors de l’utilisation du stockage Premium](storage-premium-storage.md#scalability-and-performance-targets).

#### <a name="disk-caching-policy"></a>Stratégie de mise en cache du disque
Par défaut, la mise en cache de stratégie est *en lecture seule* pour tous les hello disques de données Premium, et *en lecture-écriture* hello Premium système d’exploitation attaché toohello machine virtuelle. Ce paramètre de configuration est recommandé tooachieve hello des performances optimales IOs de votre application. Pour les disques de données en écriture seule ou avec d'importantes opérations d'écriture (par ex., les fichiers journaux de SQL Server), désactivez la mise en cache du disque pour de meilleures performances de l'application. paramètres de cache de Hello pour les disques de données existants peuvent être mis à jour à l’aide de [Azure Portal](https://portal.azure.com) ou hello *- HostCaching* paramètre Hello *Set-AzureDataDisk* applet de commande.

#### <a name="location"></a>Lieu
Choisissez un emplacement où le stockage Azure Premium est disponible. Pour obtenir des informations à jour sur les emplacements disponibles, consultez [Services Azure par région](https://azure.microsoft.com/regions/#services) . Machines virtuelles situées dans hello même région de hello compte de stockage que les magasins hello disques pour hello VM donnera de meilleures performances que si elles figurent dans les régions séparées.

#### <a name="other-azure-vm-configuration-settings"></a>Autres paramètres de configuration de machine virtuelle Azure
Lorsque vous créez une machine virtuelle Azure, vous serez invité tooconfigure certains paramètres. N’oubliez pas, certains paramètres sont fixes pour la durée de vie hello Hello machine virtuelle, tandis que vous pouvez modifier ou ajouter d’autres plus tard. Passez en revue ces paramètres de configuration de machine virtuelle Azure et vous assurer qu’ils sont configurés correctement toomatch vos charges de travail.

### <a name="optimization"></a>Optimisation
[Azure Premium Storage : conception sous le signe de la haute performance](storage-premium-storage-performance.md) fournit des instructions pour la création d’applications hautes performances avec Azure Premium Storage. Vous pouvez suivre les instructions hello combinées avec des performances tootechnologies d’applicable meilleures de pratiques intégré utilisé par votre application.

## <a name="prepare-and-copy-virtual-hard-disks-VHDs-to-premium-storage"></a>Préparer et copier les disques durs virtuels (VHD) tooPremium stockage
Hello suivant la section fournit des instructions pour la préparation des disques durs virtuels à partir de votre machine virtuelle et la copie des disques durs virtuels tooAzure stockage.

* [Scénario 1 : « je migre existant tooAzure de machines virtuelles Azure Premium Storage. »](#scenario1)
* [Scénario 2 : « je suis migration d’ordinateurs virtuels à partir d’autres plateformes de tooAzure stockage Premium. »](#scenario2)

### <a name="prerequisites"></a>Composants requis
tooprepare hello disques durs virtuels pour la migration, vous devez :

* Un abonnement Azure, un compte de stockage et un conteneur de stockage du compte toowhich, vous pouvez copier votre disque dur virtuel. Notez que le compte de stockage de destination hello peut être un compte Standard ou Premium Storage, selon vos besoins.
* Un Bonjour de toogeneralize outil disque dur virtuel si vous envisagez de toocreate plusieurs instances de machine virtuelle à partir de celui-ci. Par exemple, sysprep pour Windows ou virt-sysprep pour Ubuntu.
* Un outil tooupload hello VHD fichier toohello compte de stockage. Consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md) ou utilisez un [Explorateur de stockage Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/03/11/windows-azure-storage-explorers-2014.aspx). Ce guide décrit la copie de votre disque dur virtuel à l’aide d’outil de AzCopy hello.

> [!NOTE]
> Si vous choisissez l’option de copie synchrone avec AzCopy, pour des performances optimales, copiez votre disque dur virtuel en exécutant un de ces outils à partir d’une machine virtuelle Azure qui se trouve dans hello même région que le compte de stockage de destination hello. Si vous copiez un disque dur virtuel à partir d’une machine virtuelle Azure se trouvant dans une autre région, les performances risquent d’être ralenties.
>
> Pour copier une grande quantité de données sur une bande passante limitée, envisagez de [à l’aide du service d’importation/exportation Azure hello données tootransfer tooBlob stockage](storage-import-export-service.md); ainsi, vous tootransfer vos données en disque dur de livraison lecteurs tooan Azure Centre de données. Vous pouvez utiliser hello Azure Import/Export service toocopy données tooa compte de stockage standard uniquement. Une fois les données de salutation dans votre compte de stockage standard, vous pouvez utiliser soit hello [API de copie d’objet Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) ou compte de stockage AzCopy tootransfer hello données tooyour premium.
>
> Notez que Microsoft Azure prend uniquement en charge les fichiers de disque dur virtuel de taille fixe. Les fichiers VHDX ou les disques durs virtuels dynamiques ne sont pas pris en charge. Si vous avez un disque dur virtuel dynamique, vous pouvez le convertir taille toofixed à l’aide de hello [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) applet de commande.
>
>

### <a name="scenario1"></a>Scénario 1 : « je migre existant tooAzure de machines virtuelles Azure Premium Storage. »
Si vous migrez existant de machines virtuelles Azure, stop hello machine virtuelle, préparer les disques durs virtuels par type hello du disque dur virtuel que vous souhaitez et copiez hello VHD avec AzCopy ou PowerShell.

Hello machine virtuelle doit toobe complètement vers le bas toomigrate un état propre. Il y aura un temps d’arrêt jusqu'à la fin de la migration hello.

#### <a name="step-1-prepare-vhds-for-migration"></a>Étape 1. Préparer des disques durs virtuels pour la migration
Si vous migrez existant tooPremium de machines virtuelles Azure Storage, votre disque dur virtuel peut être :

* Une image du système d'exploitation généralisée
* Un disque de système d’exploitation unique
* Un disque de données

Nous vous présentons ci-dessous 3 scénarios pour la préparation de vos disques durs virtuels.

##### <a name="use-a-generalized-operating-system-vhd-toocreate-multiple-vm-instances"></a>Utiliser un toocreate de disque dur virtuel du système d’exploitation généralisé plusieurs instances de machine virtuelle
Si vous téléchargez un disque dur virtuel qui sera utilisé toocreate plusieurs instances de machine virtuelle Azure génériques, vous devez tout d’abord généraliser disque dur virtuel à l’aide d’un utilitaire sysprep. Cela s’applique tooa disque dur virtuel qui est local ou dans le cloud de hello. Sysprep supprime toutes les informations spécifiques à l’ordinateur de hello disque dur virtuel.

> [!IMPORTANT]
> Réalisez un instantané ou une sauvegarde de votre machine virtuelle avant la généralisation. Arrête et désallouer l’instance de machine virtuelle hello en cours d’exécution de sysprep. Suivez les étapes ci-dessous toosysprep un disque dur virtuel du système d’exploitation Windows. Notez qu’exécutant la commande Sysprep de hello nécessitera que vous tooshut la machine virtuelle de hello. Pour plus d’informations sur Sysprep, consultez [Présentation de Sysprep](http://technet.microsoft.com/library/hh825209.aspx) ou le [Manuel de référence technique Sysprep](http://technet.microsoft.com/library/cc766049.aspx).
>
>

1. Ouvrez une fenêtre d’invite de commandes en tant qu’administrateur.
2. Entrez hello suivant tooopen de commande Sysprep :

    ```
    %windir%\system32\sysprep\sysprep.exe
    ```

3. Bonjour outil de préparation système, sélectionnez entrer le système Out-of-Box expérience OOBE (), sélectionnez hello Generalize case à cocher, sélectionnez **arrêt**, puis cliquez sur **OK**, comme illustré dans l’image hello ci-dessous. Sysprep est généraliser le système d’exploitation de hello et arrêter le système hello.

    ![][1]

Pour une VM Ubuntu, utiliser sysprep de pointeurs tooachieve hello identiques. Pour plus d’informations, consultez la page [virt-sysprep](http://manpages.ubuntu.com/manpages/precise/man1/virt-sysprep.1.html) . Voir également certains d’ouvrir la source de hello [logiciel de configuration du serveur Linux](http://www.cyberciti.biz/tips/server-provisioning-software.html) pour d’autres systèmes d’exploitation Linux.

##### <a name="use-a-unique-operating-system-vhd-toocreate-a-single-vm-instance"></a>Utilisez un toocreate de disque dur virtuel du système d’exploitation unique une seule instance de machine virtuelle
Si vous avez une application en cours d’exécution sur hello machine virtuelle qui requiert des données spécifiques de l’ordinateur hello, ne généralisez pas hello disque dur virtuel. Un disque dur virtuel non généralisé peut être utilisé toocreate une instance unique de la machine virtuelle Azure. Par exemple, si vous avez un contrôleur de domaine sur votre disque dur virtuel, l’exécution de sysprep le rend inefficace comme contrôleur de domaine. Passez en revue les applications hello exécutant votre machine virtuelle et hello l’impact de l’exécution de sysprep sur ces derniers avant la généralisation hello disque dur virtuel.

##### <a name="register-data-disk-vhd"></a>Enregistrement du disque dur virtuel de données
Si vous avez migré des disques de données dans Azure toobe, vous devez effectuer que machines virtuelles hello qui utilisent ces disques sont en cours d’arrêt des données.

Hello les étapes décrites ci-dessous tooAzure de disque dur virtuel toocopy stockage Premium et l’enregistrer comme un disque de données mis en service.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Étape 2. Créer destination hello pour votre disque dur virtuel
Créez un compte de stockage pour gérer vos disques durs virtuels. Prendre en compte les points suivants lors de la planification de l’emplacement de hello toostore vos disques durs virtuels :

* cible de Hello compte de stockage Premium.
* emplacement du compte de stockage Hello doit être identique en tant que machines virtuelles Azure capable de stockage Premium vous allez créer dans la phase finale de hello. Vous pouvez copier le nouveau compte de stockage tooa ou hello toouse de plan même compte de stockage selon vos besoins.
* Copiez et enregistrez la clé de compte de stockage hello hello destination du compte de stockage pour l’étape suivante de hello.

Pour les disques de données, vous pouvez choisir tookeep des disques de données dans un compte de stockage standard (par exemple, les disques qui ont refroidissement stockage), mais nous vous recommandons vivement déplacement de toutes les données pour le stockage de production la charge de travail toouse premium.

#### <a name="copy-vhd-with-azcopy-or-powershell"></a>Étape 3. Copie du disque dur virtuel avec AzCopy ou PowerShell
Vous devez toofind votre chemin d’accès du conteneur et le stockage tooprocess clé de compte de ces deux options. Vous trouverez le chemin d’accès au conteneur et le compte de stockage dans le **Portail Azure** > **Stockage**. URL du conteneur Hello seront comme « https://myaccount.blob.core.windows.net/mycontainer/ ».

##### <a name="option-1-copy-a-vhd-with-azcopy-asynchronous-copy"></a>Option 1 : Copie d’un disque dur virtuel avec AzCopy (copie asynchrone)
À l’aide de AzCopy, vous pouvez charger facilement hello VHD sur hello Internet. Selon la taille de hello Hello disques durs virtuels, cela peut prendre le temps. N’oubliez pas les limites des entrées/sorties comptes de stockage toocheck hello lors de l’utilisation de cette option. Pour plus d’informations, consultez [Objectifs de performance et d’évolutivité d’Azure Storage](storage-scalability-targets.md) .

1. Téléchargez et installez AzCopy à partir d’ici : [version la plus récente d’AzCopy](http://aka.ms/downloadazcopy)
2. Ouvrez Azure PowerShell et accédez toohello où AzCopy est installé.
3. Fichier de disque dur virtuel hello toocopy à partir de « Source » de la commande suivante de hello d’utilisation trop « Destination ».

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Exemple :

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /Pattern:abc.vhd
    ```

    Voici les descriptions des paramètres hello utilisés Bonjour AzCopy commande :

   * **/ Source :  *&lt;source&gt;:***  emplacement du dossier de hello ou URL de conteneur de stockage qui contient le disque dur virtuel de hello.
   * **/ SourceKey :  *&lt;clé de compte source&gt;:***  clé de compte de stockage hello source du compte de stockage.
   * **/ Dest :  *&lt;destination&gt;:***  toocopy de URL de conteneur de stockage hello disque dur virtuel.
   * **/ DestKey :  *&lt;clé de compte dest&gt;:***  clé de compte de stockage du compte de stockage de destination hello.
   * **/ Modèle :  *&lt;nom de fichier&gt;:***  spécifier le nom fichier hello de toocopy de disque dur virtuel hello.

Pour plus d’informations sur l’utilisation de AzCopy outil, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).

##### <a name="option-2-copy-a-vhd-with-powershell-synchronized-copy"></a>Option 2 : Copie d’un disque dur virtuel avec PowerShell (copie synchronisée)
Vous pouvez également copier le fichier de disque dur virtuel de hello à l’aide d’applet de commande PowerShell hello AzureStorageBlobCopy de début. Utilisez hello suivant de commande de Azure PowerShell toocopy disque dur virtuel. Remplacer les valeurs hello dans <> avec les valeurs correspondantes à partir de votre compte de stockage source et de destination. toouse cette commande, vous devez disposer d’un conteneur appelé des disques durs virtuels dans votre compte de stockage de destination. Si le conteneur de hello n’existe pas, créez-le avant d’exécuter la commande hello.

```powershell
$sourceBlobUri = <source-vhd-uri>

$sourceContext = New-AzureStorageContext  –StorageAccountName <source-account> -StorageAccountKey <source-account-key>

$destinationContext = New-AzureStorageContext  –StorageAccountName <dest-account> -StorageAccountKey <dest-account-key>

Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer <dest-container> -DestBlob <dest-disk-name> -DestContext $destinationContext
```

Exemple :

```powershell
C:\PS> $sourceBlobUri = "https://sourceaccount.blob.core.windows.net/vhds/myvhd.vhd"

C:\PS> $sourceContext = New-AzureStorageContext  –StorageAccountName "sourceaccount" -StorageAccountKey "J4zUI9T5b8gvHohkiRg"

C:\PS> $destinationContext = New-AzureStorageContext  –StorageAccountName "destaccount" -StorageAccountKey "XZTmqSGKUYFSh7zB5"

C:\PS> Start-AzureStorageBlobCopy -srcUri $sourceBlobUri -SrcContext $sourceContext -DestContainer "vhds" -DestBlob "myvhd.vhd" -DestContext $destinationContext
```

### <a name="scenario2"></a>Scénario 2 : « je suis migration d’ordinateurs virtuels à partir d’autres plateformes de tooAzure stockage Premium. »
Si vous effectuez une migration à partir d’Azure Cloud Storage tooAzure disque dur virtuel, vous devez d’abord exporter répertoire local de tooa de disque dur virtuel hello. Chemin d’accès de hello source complet du répertoire local de hello où le disque dur virtuel est stocké pratique et utiliser ensuite AzCopy tooupload il tooAzure stockage.

#### <a name="step-1-export-vhd-tooa-local-directory"></a>Étape 1. Exporter le répertoire local de tooa de disque dur virtuel
##### <a name="copy-a-vhd-from-aws"></a>Copie d’un disque dur virtuel depuis AWS
1. Si vous utilisez AWS, exportez hello EC2 instance tooa disque dur virtuel dans un compartiment Amazon S3. Suivez les étapes de hello décrites dans la documentation Amazon pour outil de l’interface de ligne de commande (CLI) d’exportation les Instances d’Amazon EC2 tooinstall hello Amazon EC2 de hello et exécuter le fichier VHD de hello-instance-export-commande Créer une tâche tooexport hello EC2 instance tooa. Être vraiment toouse **VHD** hello disque &#95; IMAGE &#95; Variable FORMAT lors de l’exécution hello **créer-instance-export-tâche** commande. Hello fichier de disque dur virtuel exporté est enregistré dans le compartiment hello Amazon S3 que vous désignez pendant le processus.

    ```
    aws ec2 create-instance-export-task --instance-id ID --target-environment TARGET_ENVIRONMENT \
      --export-to-s3-task DiskImageFormat=DISK_IMAGE_FORMAT,ContainerFormat=ova,S3Bucket=BUCKET,S3Prefix=PREFIX
    ```

2. Téléchargez le fichier de disque dur virtuel de hello de compartiment de S3 hello. Fichier de disque dur virtuel hello sélectionnez, puis **Actions** > **télécharger**.

    ![][3]

##### <a name="copy-a-vhd-from-other-non-azure-cloud"></a>Copie d’un disque dur virtuel à partir d’autres cloud hors Azure
Si vous effectuez une migration à partir d’Azure Cloud Storage tooAzure disque dur virtuel, vous devez d’abord exporter répertoire local de tooa de disque dur virtuel hello. Copiez le chemin d’accès de hello source complet du répertoire local de hello où le disque dur virtuel est stocké.

##### <a name="copy-a-vhd-from-on-premises"></a>Copie d’un disque dur virtuel en local
Si vous migrez un disque dur virtuel à partir d’un environnement sur site, vous devez le chemin d’accès de la source complet hello où le disque dur virtuel est stocké. le chemin d’accès de Hello source peut être un partage de fichier ou emplacement de serveur.

#### <a name="step-2-create-hello-destination-for-your-vhd"></a>Étape 2. Créer destination hello pour votre disque dur virtuel
Créez un compte de stockage pour gérer vos disques durs virtuels. Prendre en compte les points suivants lors de la planification de l’emplacement de hello toostore vos disques durs virtuels :

* compte de stockage Hello cible peut être un stockage standard ou premium, selon vos besoins de l’application.
* région du compte de stockage Hello doit être identique en tant que machines virtuelles Azure capable de stockage Premium vous allez créer dans la phase finale de hello. Vous pouvez copier le nouveau compte de stockage tooa ou hello toouse de plan même compte de stockage selon vos besoins.
* Copiez et enregistrez la clé de compte de stockage hello hello destination du compte de stockage pour l’étape suivante de hello.

Nous recommandons de vous déplacer toutes les données pour le stockage de production la charge de travail toouse premium.

#### <a name="step-3-upload-hello-vhd-tooazure-storage"></a>Étape 3. Télécharger le disque dur virtuel de hello tooAzure stockage
Maintenant que vous avez votre disque dur virtuel dans un répertoire local de hello, vous pouvez utiliser AzCopy ou AzurePowerShell tooupload hello .vhd fichier tooAzure stockage. Les deux options sont fournies ici :

##### <a name="option-1-using-azure-powershell-add-azurevhd-tooupload-hello-vhd-file"></a>Option 1 : À l’aide de fichier .vhd de Azure PowerShell Add-AzureVhd tooupload hello

```powershell
Add-AzureVhd [-Destination] <Uri> [-LocalFilePath] <FileInfo>
```

Un exemple <Uri>peut être ***« https://storagesample.blob.core.windows.net/mycontainer/blob1.vhd »***. Un exemple <FileInfo>peut être ***« C:\path\to\upload.vhd »***.

##### <a name="option-2-using-azcopy-tooupload-hello-vhd-file"></a>Option 2 : À l’aide de fichier .vhd de AzCopy tooupload hello
À l’aide de AzCopy, vous pouvez charger facilement hello VHD sur hello Internet. Selon la taille de hello Hello disques durs virtuels, cela peut prendre le temps. N’oubliez pas les limites des entrées/sorties comptes de stockage toocheck hello lors de l’utilisation de cette option. Pour plus d’informations, consultez [Objectifs de performance et d’évolutivité d’Azure Storage](storage-scalability-targets.md) .

1. Téléchargez et installez AzCopy à partir d’ici : [version la plus récente d’AzCopy](http://aka.ms/downloadazcopy)
2. Ouvrez Azure PowerShell et accédez toohello où AzCopy est installé.
3. Fichier de disque dur virtuel hello toocopy à partir de « Source » de la commande suivante de hello d’utilisation trop « Destination ».

    ```azcopy
    AzCopy /Source: <source> /SourceKey: <source-account-key> /Dest: <destination> /DestKey: <dest-account-key> /BlobType:page /Pattern: <file-name>
    ```

    Exemple :

    ```azcopy
    AzCopy /Source:https://sourceaccount.blob.core.windows.net/mycontainer1 /SourceKey:key1 /Dest:https://destaccount.blob.core.windows.net/mycontainer2 /DestKey:key2 /BlobType:page /Pattern:abc.vhd
    ```

    Voici les descriptions des paramètres hello utilisés Bonjour AzCopy commande :

   * **/ Source :  *&lt;source&gt;:***  emplacement du dossier de hello ou URL de conteneur de stockage qui contient le disque dur virtuel de hello.
   * **/ SourceKey :  *&lt;clé de compte source&gt;:***  clé de compte de stockage hello source du compte de stockage.
   * **/ Dest :  *&lt;destination&gt;:***  toocopy de URL de conteneur de stockage hello disque dur virtuel.
   * **/ DestKey :  *&lt;clé de compte dest&gt;:***  clé de compte de stockage du compte de stockage de destination hello.
   * **/ BlobType : page :** spécifie cette destination hello est un objet blob de pages.
   * **/ Modèle :  *&lt;nom de fichier&gt;:***  spécifier le nom fichier hello de toocopy de disque dur virtuel hello.

Pour plus d’informations sur l’utilisation de AzCopy outil, consultez [transférer des données avec l’utilitaire de ligne de commande AzCopy de hello](storage-use-azcopy.md).

##### <a name="other-options-for-uploading-a-vhd"></a>Autres options de téléchargement d’un disque dur virtuel
Vous pouvez également télécharger un compte de stockage de tooyour de disque dur virtuel à l’aide de hello suivant signifie :

* [API de copie d’un objet blob de stockage Azure](https://msdn.microsoft.com/library/azure/dd894037.aspx)
* [Téléchargement d’objets blob dans Storage Explorer](https://azurestorageexplorer.codeplex.com/)
* [Référence sur l’API REST du service Import/Export Storage](https://msdn.microsoft.com/library/dn529096.aspx)

> [!NOTE]
> Nous recommandons l’utilisation de du service d’importation/exportation si l’estimation du temps de téléchargement est de plus de 7 jours. Vous pouvez utiliser [DataTransferSpeedCalculator](https://github.com/Azure-Samples/storage-dotnet-import-export-job-management/blob/master/DataTransferSpeedCalculator.html) tooestimate les temps de hello à partir de l’unité de taille et de transfert de données.
>
> Importation/exportation peut être utilisé le compte de stockage standard toocopy tooa. Vous devez toocopy de compte de stockage toopremium de stockage standard à l’aide d’un outil tel que AzCopy.
>
>

## <a name="create-azure-virtual-machine-using-premium-storage"></a>Créer des machines virtuelles Azure à l’aide du stockage Premium
Une fois hello disque dur virtuel est un compte de stockage toohello téléchargé ou copié souhaitée, suivez les instructions de hello dans cette hello tooregister de section disque dur virtuel en tant qu’image de système d’exploitation, ou disque de système d’exploitation en fonction de votre scénario et puis créer une instance de la machine virtuelle à partir de celui-ci. disque de données Hello disque dur virtuel peut être attaché toohello machine virtuelle qui a été créé.
Un exemple de script de migration est fournie à la fin de hello de cette section. Ce script simple ne correspond pas à tous les scénarios. Vous devrez peut-être tooupdate hello script toomatch avec votre scénario spécifique. toosee si ce script s’applique tooyour scénario, consultez la section ci-dessous [un exemple de Script de Migration](#a-sample-migration-script).

### <a name="checklist"></a>Liste de contrôle
1. Attendez que tous les disques de disque dur virtuel hello copie est terminée.
2. Assurez-vous que le stockage Premium est disponible dans la région de hello que vous effectuez la migration.
3. Décidez nouvelle série VM hello, que vous allez utiliser. Il doit être un stockage Premium compatibles, et taille de hello doit être en fonction de la disponibilité de hello dans la région de hello et selon vos besoins.
4. Décidez de taille virtuelle exacte de hello, que vous allez utiliser. Taille de machine virtuelle doit toobe toosupport suffisamment grand hello différents disques de données que vous avez. Par exemple, Si vous avez 4 disques de données, hello machine virtuelle doit avoir au moins 2 cœurs. Prenez également en considération les besoins en puissance, mémoire et bande passante réseau.
5. Créer un compte Premium Storage dans la région cible hello. C’est le compte à utiliser pour hello hello nouvelle machine virtuelle.
6. Des informations VM hello en cours pratiques, y compris les listes de hello des disques et des objets BLOB de disque dur virtuel correspondant.

Préparez votre application pour les interruptions de service. toodo une nouvelle migration, vous avez toostop tout traitement hello dans le système actuel de hello. Alors seulement vous pouvez l’obtenir état tooconsistent dont vous pouvez migrer toohello nouvelle plateforme. Temps d’arrêt dépend de la quantité hello d’hello disques toomigrate.

> [!NOTE]
> Si vous créez un gestionnaire de ressources Azure VM à partir d’un disque spécialisé de disque dur virtuel, consultez trop[ce modèle](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) pour le déploiement de VM Gestionnaire de ressources à l’aide du disque existant.
>
>

### <a name="register-your-vhd"></a>Enregistrez votre disque dur virtuel.
toocreate une machine virtuelle à partir de disque dur virtuel du système d’exploitation ou tooattach un tooa de disque de données nouvelle machine virtuelle, vous devez tout d’abord les enregistrer. Suivez les étapes ci-dessous en fonction de votre scénario de disque dur virtuel.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Généralisé toocreate de disque dur virtuel du système d’exploitation de plusieurs instances de machine virtuelle Azure
Après avoir généralisé image du système d’exploitation du disque dur virtuel est chargé de compte de stockage toohello, inscrire comme une **Image de machine virtuelle Azure** afin que vous pouvez créer une ou plusieurs instances de machine virtuelle à partir de celui-ci. Utilisez hello suivant tooregister d’applets de commande PowerShell de votre disque dur virtuel comme une image de système d’exploitation de la machine virtuelle Azure. Fournir l’URL du conteneur terminée hello où le disque dur virtuel a été copié dans.

```powershell
Add-AzureVMImage -ImageName "OSImageName" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osimage.vhd" -OS Windows
```

Copiez et enregistrez le nom hello de cette nouvelle Image de machine virtuelle Azure. Dans l’exemple hello ci-dessus, il est *OSImageName*.

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Toocreate de disque dur virtuel du système d’exploitation unique une seule instance de machine virtuelle Azure
Après hello unique disque dur virtuel de système d’exploitation est téléchargés toohello stockage compte, inscrivez-vous en tant qu’un **disque de système d’exploitation Azure** afin que vous pouvez créer une instance de machine virtuelle à partir de celui-ci. Utilisez ces tooregister d’applets de commande PowerShell de votre disque dur virtuel comme un disque de système d’exploitation Azure. Fournir l’URL du conteneur terminée hello où le disque dur virtuel a été copié dans.

```powershell
Add-AzureDisk -DiskName "OSDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/osdisk.vhd" -Label "My OS Disk" -OS "Windows"
```

Copiez et enregistrez le nom hello de ce nouveau disque de système d’exploitation Azure. Dans l’exemple hello ci-dessus, il est *OSDisk*.

#### <a name="data-disk-vhd-toobe-attached-toonew-azure-vm-instances"></a>Toobe de disque dur virtuel de disque de données attaché à une ou plusieurs instances de toonew machine virtuelle Azure
Une fois hello disque de données est de disque dur virtuel téléchargé toostorage compte, enregistrer en tant qu’un disque de données Azure afin qu’il puisse être attachée tooyour nouvelle série DS, DSv2 série ou une instance de la machine virtuelle Azure de série GS.

Utilisez ces tooregister d’applets de commande PowerShell de votre disque dur virtuel en tant qu’un disque de données Azure. Fournir l’URL du conteneur terminée hello où le disque dur virtuel a été copié dans.

```powershell
Add-AzureDisk -DiskName "DataDisk" -MediaLocation "https://storageaccount.blob.core.windows.net/vhdcontainer/datadisk.vhd" -Label "My Data Disk"
```

Copiez et enregistrez le nom hello de ce nouveau disque de données Azure. Dans l’exemple hello ci-dessus, il est *DataDisk*.

### <a name="create-a-premium-storage-capable-vm"></a>Création d’un compte compatible Premium Storage
Une fois hello image de système d’exploitation ou disque de système d’exploitation sont inscrits, créez une nouvelle série DS, le dsv2 ou la machine virtuelle de série GS. Vous utiliserez image de système d’exploitation hello ou nom de disque de système d’exploitation que vous avez enregistré. Sélectionnez le type de machine virtuelle hello à partir de la couche de stockage Premium hello. Dans l’exemple ci-dessous, nous utilisons hello *Standard_DS2* taille de machine virtuelle.

> [!NOTE]
> Mettre à jour toomake de taille de disque hello qu’elle correspond à votre capacité et les exigences de performances et les tailles de disque Azure hello.
>
>

Applets de commande PowerShell suivante pour hello étape par étape ci-dessous toocreate hello nouvelle machine virtuelle. Tout d’abord, définissez les paramètres communs hello :

```powershell
$serviceName = "yourVM"
$location = "location-name" (e.g., West US)
$vmSize ="Standard_DS2"
$adminUser = "youradmin"
$adminPassword = "yourpassword"
$vmName ="yourVM"
$vmSize = "Standard_DS2"
```

Commencez par créer un service cloud dans lequel vous hébergerez vos nouvelles machines virtuelles.

```powershell
New-AzureService -ServiceName $serviceName -Location $location
```

Ensuite, selon votre scénario, créez instance de machine virtuelle Azure hello de hello Image de système d’exploitation ou disque de système d’exploitation que vous avez enregistré.

#### <a name="generalized-operating-system-vhd-toocreate-multiple-azure-vm-instances"></a>Généralisé toocreate de disque dur virtuel du système d’exploitation de plusieurs instances de machine virtuelle Azure
Créer hello un ou plusieurs des instances pour l’ordinateur virtuel Azure de série DS à l’aide de hello **Image du système d’exploitation Azure** que vous avez enregistré. Spécifiez ce nom de l’Image de système d’exploitation dans la configuration d’ordinateur virtuel hello lorsque vous créez la nouvelle machine virtuelle comme indiqué ci-dessous.

```powershell
$OSImage = Get-AzureVMImage –ImageName "OSImageName"

$vm = New-AzureVMConfig -Name $vmName –InstanceSize $vmSize -ImageName $OSImage.ImageName

Add-AzureProvisioningConfig -Windows –AdminUserName $adminUser -Password $adminPassword –VM $vm

New-AzureVM -ServiceName $serviceName -VM $vm
```

#### <a name="unique-operating-system-vhd-toocreate-a-single-azure-vm-instance"></a>Toocreate de disque dur virtuel du système d’exploitation unique une seule instance de machine virtuelle Azure
Créer une nouvelle instance de machine virtuelle Azure de série DS à l’aide de hello **disque de système d’exploitation Azure** que vous avez enregistré. Spécifiez ce nom de disque de système d’exploitation dans la configuration d’ordinateur virtuel hello lors de la création de hello nouvelle machine virtuelle comme indiqué ci-dessous.

```powershell
$OSDisk = Get-AzureDisk –DiskName "OSDisk"

$vm = New-AzureVMConfig -Name $vmName -InstanceSize $vmSize -DiskName $OSDisk.DiskName

New-AzureVM -ServiceName $serviceName –VM $vm
```

Spécifiez d’autres informations de machine virtuelle Azure, comme un service cloud, une région, un compte de stockage, un groupe à haute disponibilité et une stratégie de mise en cache. Notez qu’instance de machine virtuelle hello doit être colocalisé avec le système d’exploitation associé ou les disques de données, le compte de service, région et le stockage cloud hello sélectionné doit être dans hello même emplacement que hello sous-jacent de disques durs virtuels de ces disques.

### <a name="attach-data-disk"></a>Attacher un disque de données
Enfin, si vous avez enregistré données disque VHD, définissez-les toohello nouveau stockage Premium compatibles avec Azure VM.

Utiliser la suite PowerShell applet de commande tooattach données disque toohello nouvel ordinateur virtuel et spécifiez hello mise en cache de la stratégie. Dans l’exemple ci-dessous hello mise en cache de la stratégie est défini trop*ReadOnly*.

```powershell
$vm = Get-AzureVM -ServiceName $serviceName -Name $vmName

Add-AzureDataDisk -ImportFrom -DiskName "DataDisk" -LUN 0 –HostCaching ReadOnly –VM $vm

Update-AzureVM  -VM $vm
```

> [!NOTE]
> Il peut y avoir toosupport nécessaire des étapes supplémentaires votre application est ne pas couvert par ce guide.
>
>

### <a name="checking-and-plan-backup"></a>Vérification et planification de sauvegarde
Une fois les hello nouvel ordinateur virtuel est en cours d’exécution, l’accès à l’aide de hello même id de connexion et mot de passe est hello d’ordinateur virtuel d’origine et vérifier que tout fonctionne comme prévu. Tous les paramètres de hello, y compris les volumes de hello répartie, est présents en hello nouvelle machine virtuelle.

dernière étape de Hello est la planification de sauvegarde et de maintenance tooplan pour hello que nouvelle machine virtuelle en fonction des besoins de l’application hello.

### <a name="a-sample-migration-script"></a>Un exemple de script de migration
Si vous avez plusieurs machines virtuelles toomigrate, automation via des scripts PowerShell s’avérera utile. Voici un exemple de script qui automatise la migration hello d’une machine virtuelle. Notez que script ci-dessous n'est qu’un exemple et il existe quelques hypothèses sur les disques de machine virtuelle en cours hello. Vous devrez peut-être tooupdate hello script toomatch avec votre scénario spécifique.

les hypothèses Hello sont :

* Vous créez des machines virtuelles Azure classiques.
* Vos disques de système d’exploitation source et disques de données source sont sur le même compte de stockage et le même conteneur. Si vos disques de système d’exploitation et les disques de données ne sont pas dans hello même placer, vous pouvez utiliser AzCopy ou Azure PowerShell toocopy disques durs virtuels sur les comptes de stockage et les conteneurs. Consultez l’étape précédente de toohello : [disque dur virtuel de la copie avec AzCopy ou PowerShell](#copy-vhd-with-azcopy-or-powershell). Modification de cette toomeet script votre scénario est un autre choix, mais nous recommandons d’utiliser AzCopy ou PowerShell, car il est plus facile et plus rapide.

script d’automatisation Hello est fourni ci-dessous. Remplacer du texte avec vos informations et mettre à jour de hello script toomatch avec votre scénario spécifique.

> [!NOTE]
> À l’aide de script existant de hello ne conserve pas la configuration du réseau de votre ordinateur virtuel source hello. Vous aurez besoin des paramètres de mise en réseau toore-config hello sur vos ordinateurs virtuels migrés.
>
>

```
    <#
    .Synopsis
    This script is provided as an EXAMPLE tooshow how toomigrate a VM from a standard storage account tooa premium storage account. You can customize it according tooyour specific requirements.

    .Description
    hello script will copy hello vhds (page blobs) of hello source VM toohello new storage account.
    And then it will create a new VM from these copied vhds based on hello inputs that you specified for hello new VM.
    You can modify hello script toosatisfy your specific requirement, but please be aware of hello items specified
    in hello Terms of Use section.

    .Terms of Use
    Copyright © 2015 Microsoft Corporation.  All rights reserved.

    THIS CODE AND ANY ASSOCIATED INFORMATION ARE PROVIDED "AS IS" WITHOUT WARRANTY OF ANY KIND,
    EITHER EXPRESSED OR IMPLIED, INCLUDING BUT NOT LIMITED toohello IMPLIED WARRANTIES OF MERCHANTABILITY
    AND/OR FITNESS FOR A PARTICULAR PURPOSE. hello ENTIRE RISK OF USE, INABILITY tooUSE, OR
    RESULTS FROM hello USE OF THIS CODE REMAINS WITH hello USER.

    .Example (Save this script as Migrate-AzureVM.ps1)

    .\Migrate-AzureVM.ps1 -SourceServiceName CurrentServiceName -SourceVMName CurrentVMName –DestStorageAccount newpremiumstorageaccount -DestServiceName NewServiceName -DestVMName NewDSVMName -DestVMSize "Standard_DS2" –Location "Southeast Asia"

    .Link
    toofind more information about how tooset up Azure PowerShell, refer toohello following links.
    http://azure.microsoft.com/documentation/articles/powershell-install-configure/
    http://azure.microsoft.com/documentation/articles/storage-powershell-guide-full/
    http://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/

    #>

    Param(
    # hello cloud service name of hello VM.
    [Parameter(Mandatory = $true)]
    [string] $SourceServiceName,

    # hello VM name toocopy.
    [Parameter(Mandatory = $true)]
    [String] $SourceVMName,

    # hello destination storage account name.
    [Parameter(Mandatory = $true)]
    [String] $DestStorageAccount,

    # hello destination cloud service name
    [Parameter(Mandatory = $true)]
    [String] $DestServiceName,

    # hello destination vm name
    [Parameter(Mandatory = $true)]
    [String] $DestVMName,

    # hello destination vm size
    [Parameter(Mandatory = $true)]
    [String] $DestVMSize,

    # hello location of destination VM.
    [Parameter(Mandatory = $true)]
    [string] $Location,

    # whether or not toocopy hello os disk, hello default is only copy data disks
    [Parameter(Mandatory = $false)]
    [Bool] $DataDiskOnly = $true,

    # how frequently tooreport hello copy status in sceconds
    [Parameter(Mandatory = $false)]
    [Int32] $CopyStatusReportInterval = 15,

    # hello name suffix tooadd toonew created disks tooavoid conflict with source disk names
    [Parameter(Mandatory = $false)]
    [String]$DiskNameSuffix = "-prem"

    ) #end param

    #######################################################################
    #  Verify Azure PowerShell module and version
    #######################################################################

    #import hello Azure PowerShell module
    Write-Host "`n[WORKITEM] - Importing Azure PowerShell module" -ForegroundColor Yellow
    $azureModule = Import-Module Azure -PassThru

    if ($azureModule -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    else
    {
        #show module not found interaction and bail out
        Write-Host "[ERROR] - PowerShell module not found. Exiting." -ForegroundColor Red
        Exit
    }


    #Check hello Azure PowerShell module version
    Write-Host "`n[WORKITEM] - Checking Azure PowerShell module verion" -ForegroundColor Yellow
    If ($azureModule.Version -ge (New-Object System.Version -ArgumentList "0.8.14"))
    {
        Write-Host "`tSuccess" -ForegroundColor Green
    }
    Else
    {
        Write-Host "[ERROR] - Azure PowerShell module must be version 0.8.14 or higher. Exiting." -ForegroundColor Red
        Exit
    }

    #Check if there is an azure subscription set up in PowerShell
    Write-Host "`n[WORKITEM] - Checking Azure Subscription" -ForegroundColor Yellow
    $currentSubs = Get-AzureSubscription -Current
    if ($currentSubs -ne $null)
    {
        Write-Host "`tSuccess" -ForegroundColor Green
        Write-Host "`tYour current azure subscription in PowerShell is $($currentSubs.SubscriptionName)." -ForegroundColor Green
    }
    else
    {
        Write-Host "[ERROR] - There is no valid Azure subscription found in PowerShell. Please refer toothis article http://azure.microsoft.com/documentation/articles/powershell-install-configure/ tooconnect an Azure subscription. Exiting." -ForegroundColor Red
        Exit
    }


    #######################################################################
    #  Check if hello VM is shut down
    #  Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation.
    #  Azure does not support live migration at this time..
    #######################################################################

    if (($sourceVM = Get-AzureVM –ServiceName $SourceServiceName –Name $SourceVMName) -eq $null)
    {
        Write-Host "[ERROR] - hello source VM doesn't exist in hello current subscription. Exiting." -ForegroundColor Red
        Exit
    }

    # check if VM is shut down
    if ( $sourceVM.Status -notmatch "Stopped" )
    {
        Write-Host "[Warning] - Stopping hello VM is a required step so that hello file system is consistent when you do hello copy operation. Azure does not support live migration at this time. If you'd like toocreate a VM from a generalized image, sys-prep hello Virtual Machine before stopping it." -ForegroundColor Yellow
        $ContinueAnswer = Read-Host "`n`tDo you wish toostop $SourceVMName now? Input 'N' if you want tooshut down hello VM manually and come back later.(Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $sourceVM | Stop-AzureVM

        # wait until hello VM is shut down
        $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        while ($VMStatus -notmatch "Stopped")
        {
            Write-Host "`n[Status] - Waiting VM $vmName tooshut down" -ForegroundColor Green
            Sleep -Seconds 5
            $VMStatus = (Get-AzureVM –ServiceName $SourceServiceName –Name $vmName).Status
        }
    }

    # exporting hello sourve vm tooa configuration file, you can restore hello original VM by importing this config file
    # see more information for Import-AzureVM
    $workingDir = (Get-Location).Path
    $vmConfigurationPath = $env:HOMEPATH + "\VM-" + $SourceVMName + ".xml"
    Write-Host "`n[WORKITEM] - Exporting VM configuration too$vmConfigurationPath" -ForegroundColor Yellow
    $exportRe = $sourceVM | Export-AzureVM -Path $vmConfigurationPath


    #######################################################################
    #  Copy hello vhds of hello source vm
    #  You can choose toocopy all disks including os and data disks by specifying the
    #  parameter -DataDiskOnly toobe $false. hello default is toocopy only data disk vhds
    #  and hello new VM will boot from hello original os disk.
    #######################################################################

    $sourceOSDisk = $sourceVM.VM.OSVirtualHardDisk
    $sourceDataDisks = $sourceVM.VM.DataVirtualHardDisks

    # Get source storage account information, not considering hello data disks and os disks are in different accounts
    $sourceStorageAccountName = $sourceOSDisk.MediaLink.Host -split "\." | select -First 1
    $sourceStorageKey = (Get-AzureStorageKey -StorageAccountName $sourceStorageAccountName).Primary
    $sourceContext = New-AzureStorageContext –StorageAccountName $sourceStorageAccountName -StorageAccountKey $sourceStorageKey

    # Create destination context
    $destStorageKey = (Get-AzureStorageKey -StorageAccountName $DestStorageAccount).Primary
    $destContext = New-AzureStorageContext –StorageAccountName $DestStorageAccount -StorageAccountKey $destStorageKey

    # Create a container of vhds if it doesn't exist
    if ((Get-AzureStorageContainer -Context $destContext -Name vhds -ErrorAction SilentlyContinue) -eq $null)
    {
        Write-Host "`n[WORKITEM] - Creating a container vhds in hello destination storage account." -ForegroundColor Yellow
        New-AzureStorageContainer -Context $destContext -Name vhds
    }


    $allDisksToCopy = $sourceDataDisks
    # check if need toocopy os disk
    $sourceOSVHD = $sourceOSDisk.MediaLink.Segments[2]
    if ($DataDiskOnly)
    {
        # copy data disks only, this option requires deleting hello source VM so that dest VM can boot
        # from hello same vhd blob.
        $ContinueAnswer = Read-Host "`n`t[Warning] You chose toocopy data disks only. Moving VM requires removing hello original VM (hello disks and backing vhd files will NOT be deleted) so that hello new VM can boot from hello same vhd. This is an irreversible action. Do you wish tooproceed right now? (Y/N)"
        If ($ContinueAnswer -ne "Y") { Write-Host "`n Exiting." -ForegroundColor Red;Exit }
        $destOSVHD = Get-AzureStorageBlob -Blob $sourceOSVHD -Container vhds -Context $sourceContext
        Write-Host "`n[WORKITEM] - Removing hello original VM (hello vhd files are NOT deleted)." -ForegroundColor Yellow
        Remove-AzureVM -Name $SourceVMName -ServiceName $SourceServiceName

        Write-Host "`n[WORKITEM] - Waiting utill hello OS disk is released by source VM. This may take up tooseveral minutes."
        $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        while ($diskAttachedTo -ne $null)
        {
            Start-Sleep -Seconds 10
            $diskAttachedTo = (Get-AzureDisk -DiskName $sourceOSDisk.DiskName).AttachedTo
        }

    }
    else
    {
        # copy hello os disk vhd
        Write-Host "`n[WORKITEM] - Starting copying os disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $allDisksToCopy += @($sourceOSDisk)
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $sourceOSVHD -DestContainer vhds -DestBlob $sourceOSVHD -Context $sourceContext -DestContext $destContext -Force
        $destOSVHD = $targetBlob
    }


    # Copy all data disk vhds
    # Start all async copy requests in parallel.
    foreach($disk in $sourceDataDisks)
    {
        $blobName = $disk.MediaLink.Segments[2]
        # copy all data disks
        Write-Host "`n[WORKITEM] - Starting copying data disk $($disk.DiskName) at $(get-date)." -ForegroundColor Yellow
        $targetBlob = Start-AzureStorageBlobCopy -SrcContainer vhds -SrcBlob $blobName -DestContainer vhds -DestBlob $blobName -Context $sourceContext -DestContext $destContext -Force
        # update hello media link toopoint toohello target blob link
        $disk.MediaLink = $targetBlob.ICloudBlob.Uri.AbsoluteUri
    }

    # Wait until all vhd files are copied.
    $diskComplete = @()
    do
    {
        Write-Host "`n[WORKITEM] - Waiting for all disk copy toocomplete. Checking status every $CopyStatusReportInterval seconds." -ForegroundColor Yellow
        # check status every 30 seconds
        Sleep -Seconds $CopyStatusReportInterval
        foreach ( $disk in $allDisksToCopy)
        {
            if ($diskComplete -contains $disk)
            {
                Continue
            }
            $blobName = $disk.MediaLink.Segments[2]
            $copyState = Get-AzureStorageBlobCopyState -Blob $blobName -Container vhds -Context $destContext
            if ($copyState.Status -eq "Success")
            {
                Write-Host "`n[Status] - Success for disk copy $($disk.DiskName) at $($copyState.CompletionTime)" -ForegroundColor Green
                $diskComplete += $disk
            }
            else
            {
                if ($copyState.TotalBytes -gt 0)
                {
                    $percent = ($copyState.BytesCopied / $copyState.TotalBytes) * 100
                    Write-Host "`n[Status] - $('{0:N2}' -f $percent)% Complete for disk copy $($disk.DiskName)" -ForegroundColor Green
                }
            }
        }
    }
    while($diskComplete.Count -lt $allDisksToCopy.Count)

    #######################################################################
    #  Create a new vm
    #  hello new VM can be created from hello copied disks or hello original os disk.
    #  You can ddd your own logic here toosatisfy your specific requirements of hello vm.
    #######################################################################

    # Create a VM from hello existing os disk
    if ($DataDiskOnly)
    {
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $sourceOSDisk.DiskName
    }
    else
    {
        $newOSDisk = Add-AzureDisk -OS $sourceOSDisk.OS -DiskName ($sourceOSDisk.DiskName + $DiskNameSuffix) -MediaLocation $destOSVHD.ICloudBlob.Uri.AbsoluteUri
        $vm = New-AzureVMConfig -Name $DestVMName -InstanceSize $DestVMSize -DiskName $newOSDisk.DiskName
    }
    # Attached hello copied data disks toohello new VM
    foreach ($dataDisk in $sourceDataDisks)
    {
        # add -DiskLabel $dataDisk.DiskLabel if there are labels for disks of hello source vm
        $diskLabel = "drive" + $dataDisk.Lun
        $vm | Add-AzureDataDisk -ImportFrom -DiskLabel $diskLabel -LUN $dataDisk.Lun -MediaLocation $dataDisk.MediaLink
    }

    # Edit this if you want tooadd more custimization toohello new VM
    # $vm | Add-AzureEndpoint -Protocol tcp -LocalPort 443 -PublicPort 443 -Name 'HTTPs'
    # $vm | Set-AzureSubnet "PubSubnet","PrivSubnet"

    New-AzureVM -ServiceName $DestServiceName -VMs $vm -Location $Location
```

#### <a name="optimization"></a>Optimisation
Votre configuration actuelle de la machine virtuelle peut être personnalisée en particulier les toowork correctement avec les disques Standard. Par exemple, tooincrease hello des performances à l’aide de disques dans un volume agrégé par bandes. Par exemple, au lieu d’utiliser les 4 disques séparément sur un stockage Premium, vous pouvez être en mesure de toooptimize hello en ayant un seul disque. Optimisations, comme cette toobe besoin géré sur un cas par cas et nécessitent des étapes personnalisées après la migration de hello. En outre, notez que ce processus ne fonctionne pas bien pour les bases de données et les applications qui dépendent de disposition du disque hello définie dans le programme d’installation hello.

##### <a name="preparation"></a>Préparation
1. Hello complète Migration Simple, comme décrit dans hello à la section précédente. Les optimisations se fera sur hello nouvel ordinateur virtuel après la migration de hello.
2. Définir les nouvelles tailles de disque hello nécessaires à la configuration de hello optimisé.
3. Déterminer le mappage de hello spécifications en cours/volumes de disques toohello nouveau disque.

##### <a name="execution-steps"></a>Étapes d'exécution
1. Créer des nouveaux disques hello avec des tailles appropriées de hello sur hello VM de stockage Premium.
2. Connexion toohello machine virtuelle et copie hello données de hello actuel toohello nouveau disque du volume qui mappe le volume de toothat. Cela pour tous les volumes en cours hello nécessitant toomap tooa nouveau disque.
3. Ensuite, modifiez hello application paramètres tooswitch toohello nouveaux disques et détacher des anciens volumes de hello.

Pour le paramétrage d’application hello pour de meilleures performances de disque, consultez trop[optimisation des performances des applications](storage-premium-storage-performance.md#optimizing-application-performance).

### <a name="application-migrations"></a>Migrations des applications
Bases de données et d’autres applications complexes peuvent nécessiter des étapes spéciales, comme défini par le fournisseur d’application hello pour la migration de hello. Consultez la documentation de l’application toorespective. Par exemple, la migration des bases de données se fait généralement via des étapes de sauvegarde et de restauration.

## <a name="next-steps"></a>Étapes suivantes
Consultez hello suivant des ressources pour des scénarios spécifiques pour la migration des ordinateurs virtuels :

* [Migrer des machines virtuelles Azure entre les comptes de stockage](https://azure.microsoft.com/blog/2014/10/22/migrate-azure-virtual-machines-between-storage-accounts/)
* [Créez et téléchargez un tooAzure le disque dur virtuel de Windows Server.](../virtual-machines/windows/classic/createupload-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
* [Création et téléchargement d’un disque dur virtuel qui contient hello système d’exploitation Linux](../virtual-machines/linux/classic/create-upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2fclassic%2ftoc.json)
* [Migration d’ordinateurs virtuels à partir d’Amazon AWS tooMicrosoft Azure](http://channel9.msdn.com/Series/Migrating-Virtual-Machines-from-Amazon-AWS-to-Microsoft-Azure)

Consultez également hello suivant toolearn ressources plus d’informations sur le stockage Azure et les Machines virtuelles Azure :

* [Azure Storage](https://azure.microsoft.com/documentation/services/storage/)
* [Azure Virtual Machines](https://azure.microsoft.com/documentation/services/virtual-machines/)
* [Stockage Premium : stockage hautes performances pour les charges de travail des machines virtuelles Azure](storage-premium-storage.md)

[1]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[2]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-1.png
[3]:./media/storage-migration-to-premium-storage/migration-to-premium-storage-3.png
[4]: http://technet.microsoft.com/library/hh831739.aspx
