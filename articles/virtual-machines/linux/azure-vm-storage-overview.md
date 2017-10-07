---
title: aaaAzure Azure Storage et les machines virtuelles Linux | Documents Microsoft
description: "Décrit le Stockage Standard et Premium Azure, ainsi que l’utilisation des disques gérés et non gérés avec des machines virtuelles Linux."
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: 
ms.assetid: d364c69e-0bd1-4f80-9838-bbc0a95af48c
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 2/7/2017
ms.author: rasquill
ms.openlocfilehash: d34441698a4e59721847685099e5fb3aa378c597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux-vm-storage"></a>Stockage des machines virtuelles Azure et Linux
Stockage Azure est la solution de stockage cloud hello pour les applications modernes qui s’appuient sur la durabilité, disponibilité et évolutivité toomeet hello aux besoins de leurs clients.  En outre toomaking il possible pour de nouveaux scénarios développeurs toobuild applications à grande échelle toosupport, le stockage Azure fournit également foundation de stockage hello pour les Machines virtuelles Azure.

## <a name="managed-disks"></a>Managed Disks

Machines virtuelles Azure sont désormais disponibles en utilisant [disques gérés d’Azure](../windows/managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), ce qui permet de vous toocreate vos machines virtuelles sans créer ni gérer aucun [comptes de stockage Azure](../../storage/common/storage-introduction.md) vous-même. Vous spécifiez si vous souhaitez Premium ou Standard de stockage et de disque de hello quelle doivent être, et Azure crée des disques de machine virtuelle hello pour vous. Les machines virtuelles intégrant des disques gérés offrent de nombreux avantages, notamment :

- Une extensibilité automatique. Azure crée des disques hello et gère hello toosupport de stockage sous-jacente des too10, des disques 000 par abonnement.
- Une fiabilité accrue avec les groupes à haute disponibilité. Azure garantit que les disques de machine virtuelle sont automatiquement isolés les uns des autres au sein des groupes à haute disponibilité.
- Un meilleur contrôle d’accès. Les disques gérés offrent un large choix d’options de [contrôle d’accès en fonction du rôle (RBAC) d’Azure](../../active-directory/role-based-access-control-what-is.md).

La tarification des disques gérés est différente de celle des disques non gérés. Pour en savoir plus, consultez la rubrique relative à la [tarification et à la facturation des disques gérés](../windows/managed-disks-overview.md#pricing-and-billing).

Vous pouvez convertir des machines virtuelles existantes qui utilisent des disques toouse géré de disques non managé avec [az vm convertir](/cli/azure/vm#convert). Pour plus d’informations, consultez [comment tooconvert un VM Linux du code non disques des disques gérés tooAzure](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Impossible de convertir un disque non managé vers un disque géré si disque non managé de hello est dans un compte de stockage, ou à tout moment, a été chiffré à l’aide [chiffrement de Service de stockage Azure (SSE)](../../storage/common/storage-service-encryption.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). les étapes suivantes de Hello en détail comment tootooconvert non managée disques ou qui ont été apportées, dans un compte de stockage chiffrée :

- Copier (VHD) du disque dur virtuel hello avec [début de copie az stockage blob](/cli/azure/storage/blob/copy#start) compte de stockage tooa qui n’a jamais été activée pour le chiffrement de Service de stockage Azure.
- Créez une machine virtuelle qui utilise des disques gérés et spécifiez ce fichier de disque dur virtuel lors de la création avec la commande [az vm create](/cli/azure/vm#create), ou
- Attacher hello copié le disque dur virtuel avec [attacher de disque de machine virtuelle az](/cli/azure/vm/disk#attach) tooa exécutant la machine virtuelle avec des disques gérés.


## <a name="azure-storage-standard-and-premium"></a>Stockage Azure : Standard et Premium
Que vous utilisiez des disques gérés ou non gérés, les machines virtuelles Azure peuvent intégrer des disques de stockage Standard ou Premium. Lorsque vous utilisez toochoose de portail hello votre machine virtuelle, vous devez basculer une liste déroulante sur hello **notions de base** écran tooview disques standard et premium. Lorsque des lecteurs basculé tooSSD, seul le stockage premium activée de machines virtuelles seront affichera, par SSD.  Lorsque tooHDD basculé, soutenus par la rotation des disques de machines virtuelles compatibles standard de stockage sont affichés, ainsi que le stockage premium soutenus par SSD de machines virtuelles.

Lors de la création d’une machine virtuelle à partir de hello `azure-cli` vous pouvez choisir entre standard et premium lors du choix de taille de machine virtuelle hello via hello `-z` ou `--vm-size` cli indicateur.

## <a name="creating-a-vm-with-a-managed-disk"></a>Création d’une machine virtuelle avec un disque géré

exemple Hello requiert hello Azure CLI 2.0, que vous pouvez [installer ici](/cli/azure/install-azure-cli).

Commencez par créer un Bonjour de toomanage de groupe de ressources ressources avec [création de groupe de az](/cli/azure/group#create):

```azurecli
az group create --location westus --name myResourceGroup
```

Créer maintenant hello machine virtuelle avec [az vm créer](/cli/azure/vm#create). Spécifiez un argument `--public-ip-address-dns-name` unique, car `mypublicdns` est probablement pris.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns
```

Hello l’exemple précédent crée un ordinateur virtuel avec un disque géré dans un compte de stockage Standard. toouse un compte de stockage Premium, ajouter hello `--storage-sku Premium_LRS` argument, comme hello l’exemple suivant :

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --public-ip-address-dns-name mypublicdns \
    --storage-sku Premium_LRS
```

## <a name="standard-storage"></a>Stockage Standard
Le stockage Azure Standard est un type de stockage par défaut de hello.  Le Stockage Standard est rentable tout en étant performant.  

## <a name="premium-storage"></a>Stockage Premium
Azure Premium Storage offre une prise en charge très performante et à faible latence des disques pour les machines virtuelles exécutant des charges de travail qui utilisent beaucoup d'E/S. Les disques de machine virtuelle qui utilisent Premium Storage stockent les données sur des disques SSD. Vous pouvez migrer tooAzure de disques de machine virtuelle de votre application parti de tootake de stockage Premium de vitesse de hello et les performances de ces disques.

Caractéristiques du Stockage Premium :

* Les disques de stockage Premium : Stockage Azure Premium prend en charge les disques de machine virtuelle qui peuvent être attaché tooDS, DSv2 ou GS série Azure VMs.
* Objet Blob de pages Premium : Stockage Premium prend en charge les objets BLOB Azure de pages, qui sont des disques persistants de toohold utilisé pour les Machines virtuelles Azure (VM).
* Le stockage Premium localement redondant : Un compte de stockage Premium prend uniquement localement redondant stockage (LRS) en tant qu’option de réplication hello et conserve trois copies de données de salutation au sein d’une seule région.
* [Stockage Premium](../../storage/common/storage-premium-storage.md)

## <a name="premium-storage-supported-vms"></a>Machines virtuelles non prises en charge par le Stockage Premium
Le Stockage Premium prend en charge les machines virtuelles Azure des séries DS, DSv2, GS et Fs. Vous pouvez utiliser des disques de Stockage Standard et Premium avec les machines virtuelles prises en charge par le Stockage Premium. Mais vous ne pouvez pas utiliser des disques de stockage Premium avec des séries de machines virtuelles non compatibles avec le Stockage Premium.

Voici les Distributions de Linux hello nous validé avec le stockage Premium.

| Distribution | Version | Noyau pris en charge |
| --- | --- | --- |
| Ubuntu |12.04 |3.2.0-75.110+ |
| Ubuntu |14.04 |3.13.0-44.73+ |
| Debian |7.x, 8.x |3.16.7-ckt4-1+ |
| SLES |SLES 12 |3.12.36-38.1+ |
| SLES |SLES 11 SP4 |3.0.101-0.63.1+ |
| CoreOS |584.0.0+ |3.18.4+ |
| Centos |6.5, 6.6, 6.7, 7.0, 7.1 |3.10.0-229.1.2.el7+ |
| RHEL |6.8+, 7.2+ | |

## <a name="azure-file-storage"></a>Présentation du stockage de fichiers
Stockage de fichiers Azure offre des partages de fichiers dans le cloud hello à l’aide du protocole SMB standard de hello. Avec les fichiers Azure, vous pouvez migrer des applications d’entreprise qui s’appuient sur tooAzure de serveurs de fichiers. Les applications exécutées dans Azure permettent de monter facilement des partages de fichiers à partir de machines virtuelles Azure exécutées sous Linux. Et avec la version la plus récente hello de stockage de fichiers, vous pouvez également monter un partage de fichiers à partir d’une application locale qui prend en charge SMB 3.0.  Étant donné que les partages de fichiers sont des partages SMB, vous pouvez y accéder via les API de système de fichiers standard.

Stockage de fichiers est créé sur hello même technologie que le stockage Blob, Table et de file d’attente pour le stockage de fichiers offre hello disponibilité, la durabilité, l’extensibilité et à redondance géographique qui est intégrée à la plate-forme de stockage Azure hello. Pour plus d’informations sur les objectifs et les limites des performances du Stockage Fichier, consultez Objectifs d’évolutivité et de performances du Stockage Azure.

* [Comment toouse stockage Azure files avec Linux](../../storage/files/storage-how-to-use-files-linux.md)

## <a name="hot-storage"></a>Stockage chaud
niveau de stockage à chaud Azure Hello est optimisé pour le stockage des données fréquemment sollicitées.  Le stockage à chaud est de type de stockage par défaut hello pour les magasins d’objets blob.

## <a name="cool-storage"></a>Stockage à froid
couche de stockage froid Azure Hello est optimisé pour le stockage des données qui sont rarement sollicitées et à long terme. Parmi les exemples d’utilisation du stockage à froid, citons les sauvegardes, le contenu multimédia, les données scientifiques, la conformité et les données d’archivage. En général, toutes les données auxquelles vous accédez rarement sont des candidats idéaux au stockage à froid.

|  | niveau de stockage chaud | niveau de stockage froid |
|:--- |:---:|:---:|
| Availability |99,9 % |99 % |
| Disponibilité (lectures RA-GRS) |99,99 % |99,9 % |
| Frais d'utilisation |Coûts de stockage supérieurs |Coûts de stockage inférieurs |
| Accès inférieur |Accès supérieur | |
| et coûts de transaction |et coûts de transaction | |

## <a name="redundancy"></a>Redondance
Hello dans votre compte de stockage est toujours de Microsoft Azure répliquées tooensure durabilité et une haute disponibilité, réunion hello SLA du stockage Azure, même en face de hello de défaillances matérielles temporaires.

Lorsque vous créez un compte de stockage, vous devez sélectionner une de hello options de réplication suivantes :

* Stockage localement redondant (LRS)
* Stockage redondant dans une zone (ZRS)
* Stockage géo-redondant (GRS)
* Stockage géo-redondant avec accès en lecture (RA-GRS)

### <a name="locally-redundant-storage"></a>Stockage localement redondant
Stockage localement redondant (LRS) réplique vos données au sein de la région de hello dans lequel vous avez créé votre compte de stockage. toomaximize durabilité, chaque demande adressée aux données dans votre compte de stockage est répliquée trois fois. Ces trois réplicas se trouvent dans des domaines d’erreur et de mise à niveau distincts.  Une demande retourne correctement uniquement une fois qu’elle a été écrite tooall trois réplicas.

### <a name="zone-redundant-storage"></a>Stockage redondant dans une zone
Stockage à redondance de zone (ZRS) réplique vos données sur deux toothree installations, dans un ou deux régions, en fournissant une durabilité élevée au stockage LRS. Si votre compte de stockage a ZRS est activé, vos données sont durables, même dans les cas de hello de défaillance sur l’une des installations de hello.

### <a name="geo-redundant-storage"></a>Stockage géo-redondant
Stockage géo-redondant (GRS) réplique vos données tooa région secondaire des centaines de miles en dehors de la région principale de hello. Si votre compte de stockage GRS est activé, vos données sont durables même en cas de hello de panne régionale totale ou de sinistre quels Bonjour la région principale n’est pas récupérable.

### <a name="read-access-geo-redundant-storage"></a>Stockage géo-redondant avec accès en lecture
Stockage de géo-redondant avec accès en lecture (RA-GRS) optimise la disponibilité de votre compte de stockage, en fournissant des données de toohello d’accès en lecture seule dans l’emplacement secondaire de hello, en outre la réplication entre deux régions toohello fournie par GRS. Dans l’événement hello que les données deviennent indisponibles dans la région principale de hello, votre application peut lire des données à partir de la région secondaire hello.

Pour une présentation approfondie de la redondance du Stockage Azure, consultez :

* [Réplication Azure Storage](../../storage/common/storage-redundancy.md)

## <a name="scalability"></a>Extensibilité
Le stockage Azure est très évolutif, donc vous pouvez stocker et traiter des centaines de téraoctets de données toosupport hello big de scénarios de données requis par une analyse scientifique et financière et les applications de support. Ou vous pouvez stocker hello petites quantités de données requises pour un site Web de petite entreprise. Chaque fois que vos besoins se situent, vous payez uniquement pour les données hello que vous stockez. Azure Storage stocke actuellement des dizaines de billions d'objets client uniques et traite en moyenne des millions de requêtes par seconde.

Pour les comptes de stockage Standard : un compte de stockage Standard a un taux de demandes total maximal de 20 000 opérations d’E/S par seconde. Hello total IOPS sur tous vos disques de machine virtuelle dans un compte de stockage standard ne doit pas dépasser cette limite.

Pour les comptes de stockage Premium : un compte de stockage Premium a un débit total maximum de 50 Gbit/s. débit total de Hello dans l’ensemble de vos disques de machine virtuelle ne doit pas dépasser cette limite.

## <a name="availability"></a>Disponibilité
Nous garantissons qu’au moins 99,99 % (99,9 % pour le niveau d’accès froid) du temps de hello, nous seront des processus demande des données tooread avec succès à partir de comptes de stockage redondants de géo-accès en lecture (RA-GRS), sous réserve que l’échec de tentatives tooread des données à partir de la région principale de hello une nouvelle tentative sur la région secondaire hello.

Nous garantissons qu’au moins 99,9 % (99 % pour le niveau d’accès froid) du temps de hello, nous allons correctement les données tooread traitent les demandes de stockage localement redondant (LRS), stockage redondant de Zone (ZRS) et les comptes de stockage redondants de géo-réplication (GRS).

Nous garantissons qu’au moins 99,9 % (99 % pour le niveau d’accès froid) du temps de hello, nous allons correctement traitent les requêtes toowrite données tooLocally stockage redondant (LRS), Zone Redundant Storage (ZRS), géo-réplication redondante comptes de stockage (GRS) et des accès en lecture-redondante Comptes de stockage (RA-GRS).

* [Contrat SLA Azure pour le stockage](https://azure.microsoft.com/support/legal/sla/storage/v1_1/)

## <a name="regions"></a>Régions
Azure est généralement disponible dans les 30 régions monde hello et a annoncé pour 4 autres régions. Expansion géographique est une priorité pour Azure, car il permet de nos performances tooachieve clients et il prend en charge leurs besoins et les préférences concernant l’emplacement des données.  Azures dernière région toolaunch est en Allemagne.

Hello Microsoft Cloud Allemagne inclut un toohello option différenciés Microsoft Cloud services déjà disponibles en Europe, création d’augmentation des possibilités de l’innovation et croissance économique pour les partenaires de réglementation et les clients en Allemagne, Hello Union européenne (UE) et hello Association européenne de libre échange (AELE).

Les données de client dans les centres de données nouvelle Magdeburg et Frankfort, sont gérées sous contrôle de code hello d’un tiers de confiance de données, T-Systems International, une société allemande indépendante et une filiale de Deutsche Telekom. Des services cloud commerciaux de Microsoft dans les centres de données respectent les données tooGerman la gestion des réglementations et fournir aux clients des options supplémentaires de comment et où les données sont traitées.

* [Carte des régions Azure](https://azure.microsoft.com/regions/)

## <a name="security"></a>Sécurité
Le stockage Azure fournit un ensemble complet des fonctionnalités de sécurité qui en permettent aux développeurs de toobuild des applications sécurisées. compte de stockage Hello lui-même peut être sécurisé à l’aide du contrôle d’accès en fonction du rôle et Azure Active Directory. Les données peuvent être sécurisées en transit entre une application et Azure au moyen du chiffrement côté client, de HTTPS ou de SMB 3.0. Donnée peut être définie toobe automatiquement chiffré tooAzure stockage à l’aide du chiffrement de Service de stockage (SSE) lors de l’écriture. Les disques du système d’exploitation et les données utilisées par les ordinateurs virtuels peuvent être définies toobe chiffré à l’aide du chiffrement de disque Azure. Accès délégué toohello les objets de données dans le stockage Azure peuvent être accordées à l’aide de Signatures d’accès partagé.

### <a name="management-plane-security"></a>Sécurité du plan de gestion
plan de gestion Hello compose de hello ressources utilisées toomanage à votre compte de stockage. Dans cette section, nous parlerons de modèle de déploiement du Gestionnaire de ressources Azure hello et comment accéder à des comptes de stockage tooyour toocontrol de contrôle d’accès en fonction du rôle (RBAC) toouse. Nous aborderons également la gestion des clés de votre compte de stockage et comment tooregenerate les.

### <a name="data-plane-security"></a>Sécurité du plan de données
Dans cette section, nous allons examiner autorisant l’accès toohello les objets de données réelles dans votre compte de stockage, tels que les objets BLOB, les fichiers, les files d’attente et les tables, à l’aide de stratégies d’accès stockée et de Signatures d’accès partagé. Nous évoquerons à la fois les signatures d’accès partagé (SAP) au niveau des services et les signatures d’accès partagé au niveau des comptes. Nous verrons comment toolimit accéder à adresse IP spécifique de tooa (ou la plage d’adresses IP), le protocole de hello toolimit utilisé tooHTTPS et découvrez comment toorevoke une Signature d’accès partagé sans attendre tooexpire.

## <a name="encryption-in-transit"></a>Chiffrement en transit
Cette section explique comment les données toosecure lorsque vous le transférez dans ou hors d’Azure Storage. Nous parlerons hello recommandé d’utiliser de chiffrement hello et HTTPS utilisé par SMB 3.0 pour les partages de fichiers Azure. Nous allons également au chiffrement côté Client, ce qui vous permet de tooencrypt hello données avant leur transfert vers le stockage dans une application cliente et toodecrypt hello après leur transfert hors stockage.

## <a name="encryption-at-rest"></a>Chiffrement au repos
Nous aborderons le chiffrement de Service de stockage (SSE), et comment vous pouvez l’activer pour un compte de stockage, vos objets BLOB de blocs, objets BLOB de pages, ce qui entraîne et ajouter des objets BLOB automatiquement chiffrée tooAzure stockage lors de l’écriture. Nous examinerons également comment vous pouvez utiliser le chiffrement de disque Azure et Explorer les différences de base hello et les cas de chiffrement de disque et SSE et le chiffrement côté Client. Nous nous pencherons brièvement sur la conformité aux normes FIPS des ordinateurs de l’administration américaine.

* [Guide de sécurité du Stockage Azure](../../storage/common/storage-security-guide.md)

## <a name="temporary-disk"></a>Disque temporaire
Chaque machine virtuelle contient un disque temporaire. disque temporaire de Hello fournit le stockage à court terme pour les applications et les processus et données du magasin prévue tooonly tels que des fichiers d’échange. Données sur le disque temporaire de hello peuvent être perdues pendant un [événement de maintenance](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json#understand-vm-reboots---maintenance-vs-downtime) ou lorsque vous [redéployer une machine virtuelle](redeploy-to-new-node.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Lors du redémarrage de hello machine virtuelle standard données hello sur lecteur temporaire de hello doivent rendre persistant.

Sur les ordinateurs virtuels Linux, hello disque est généralement **/dev/sdb** et est formaté et monté trop**/mnt** par hello Linux Agent Azure. taille de Hello du disque temporaire de hello varie selon la taille hello de machine virtuelle de hello. Pour plus d’informations, consultez [Taille des machines virtuelles Linux](sizes.md).

Pour plus d’informations sur la façon dont Azure utilise le disque temporaire de hello, consultez [présentation lecteur temporaire de hello sur des Machines virtuelles Microsoft Azure](https://blogs.msdn.microsoft.com/mast/2013/12/06/understanding-the-temporary-drive-on-windows-azure-virtual-machines/)

## <a name="cost-savings"></a>Réduction des coûts
* [Coût de stockage](https://azure.microsoft.com/pricing/details/storage/)
* [Calcul des coûts de stockage](https://azure.microsoft.com/pricing/calculator/?service=storage)

## <a name="storage-limits"></a>Limites de stockage
* [Limites de service de stockage](../../azure-subscription-service-limits.md#storage-limits)
