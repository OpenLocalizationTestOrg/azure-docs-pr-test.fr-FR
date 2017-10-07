---
title: "Stockage Premium de performances aaaHigh et Azure des disques gérés pour les machines virtuelles | Documents Microsoft"
description: "En savoir plus sur le stockage Premium hautes performances et les disques gérés pour les machines virtuelles Azure. Les machines virtuelles Azure des séries DS, DSv2 et GS prennent en charge le stockage Premium."
services: storage
documentationcenter: 
author: ramankumarlive
manager: aungoo-msft
editor: tysonn
ms.assetid: e2a20625-6224-4187-8401-abadc8f1de91
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: ramankum
ms.openlocfilehash: 2474fa75116fe394672fde48520441fa80cf434f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="high-performance-premium-storage-and-managed-disks-for-vms"></a>Stockage Premium hautes performances et disques gérés pour machines virtuelles
Le stockage Premium Azure offre une prise en charge très performante et à faible latence des disques pour les machines virtuelles avec des charges de travail qui utilisent beaucoup d’entrée/sortie (E/S). Les disques de machine virtuelle qui utilisent le stockage Premium stockent les données sur des disques SSD. tootake parti de la vitesse de hello et les performances des disques de stockage premium, vous pouvez migrer tooPremium de disques de machine virtuelle existante stockage.

Dans Azure, vous pouvez attacher plusieurs tooa disques de stockage premium machine virtuelle. À l’aide de plusieurs disques permet à vos applications jusqu'à too256 to de stockage par machine virtuelle. Stockage Premium, vos applications peuvent atteindre 80 000 opérations d’e/s par seconde (IOPS) par machine virtuelle et un débit de disque de configuration too2, 000 mégaoctets par seconde (Mbits/s) par machine virtuelle. Les opérations de lecture offrent une latence très faible.

Stockage Premium, Azure offre la possibilité de hello tootruly décalage courbes d’élévation et applications d’entreprise exigeantes comme Dynamics AX, Dynamics CRM, Exchange Server, SAP Business Suite et SharePoint cloud toohello de batteries de serveurs. Vous pouvez exécuter des charges de travail de bases de données intensives et exigeantes dans des applications comme SQL Server, Oracle, MongoDB, MySQL et Redis, qui nécessitent continuellement des performances élevées et une faible latence.

> [!NOTE]
> Hello des performances optimales pour votre application, nous vous recommandons de migrer n’importe quel disque de machine virtuelle nécessitant une haute IOPS tooPremium stockage. Si votre disque ne nécessite pas une valeur élevée d’E/S par seconde, vous pouvez limiter les coûts en le maintenant en Stockage Azure standard. Dans le cadre d’un stockage standard, les données de disque des machines virtuelles sont stockées sur des disques durs au lieu de disques SSD.
> 

Azure propose des disques de stockage premium toocreate de deux manières pour les machines virtuelles :

* **Disques non gérés**

    méthode d’origine Hello est les disques toouse non managée. Un disque non managé, vous permet de gérer les comptes de stockage hello utiliser des fichiers de disque dur virtuel (VHD) de hello toostore qui correspondent tooyour les disques de machine virtuelle. Les fichiers VHD sont stockés en tant qu’objets blob de pages dans les comptes de stockage Azure. 

* **Disques gérés**

    Lorsque vous choisissez [disques gérés d’Azure](storage-managed-disks-overview.md), Azure gère les comptes de stockage hello que vous utilisez pour vos disques de machine virtuelle. Vous spécifiez le type de disque de hello (Premium ou Standard) et la taille de hello du disque hello dont vous avez besoin. Azure crée et gère les disques de hello pour vous. Vous n’avez pas tooworry à placer les disques de hello dans plusieurs tooensure de comptes de stockage vous restez dans les limites d’extensibilité pour vos comptes de stockage. Azure gère cela à votre place.

Nous vous recommandons de choisir les disques gérés, parti tootake de leurs nombreuses fonctionnalités.

tooget a démarré avec un stockage Premium, [créer gratuitement un compte Azure](https://azure.microsoft.com/pricing/free-trial/). 

Pour plus d’informations sur la migration de votre tooPremium de machines virtuelles stockage existant, consultez [convertir une machine virtuelle Windows à partir de disques toomanaged de disques non managé](../virtual-machines/virtual-machines-windows-convert-unmanaged-to-managed-disks.md) ou [convertir un VM Linux à partir de disques toomanaged de disques non managé](../virtual-machines/linux/convert-unmanaged-to-managed-disks.md).

> [!NOTE]
> Le stockage Premium est disponible dans la plupart des régions. Pour la liste des régions disponibles, hello dans [des services Azure par région](https://azure.microsoft.com/regions/#services), examinez les régions hello dans lequel pris en charge les machines virtuelles de taille de la série de prise en charge Premium (série DS, DSV2-series, GS-série et les machines virtuelles de série Fs) sont pris en charge.
> 

## <a name="features"></a>Caractéristiques

Voici quelques-unes des fonctionnalités hello du stockage Premium :

* **Disques de stockage Premium**

    Disques de machine virtuelle Premium stockage prend en charge qui peuvent être joint toospecific taille-série machines virtuelles. Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS, Ls et Fs. Sept tailles de disque différentes vous sont proposées : P4 (32 Go), P6 (64 Go), P10 (128 Go), P20 (512 Go), P30 (1024 Go), P40 (2048 Go), P50 (4095 Go). Les tailles de disque P4 et P6 ne sont actuellement prises en charge que par Managed Disks. Chaque taille de disque a ses propres spécifications en matière de performances. Selon les exigences de votre application, vous pouvez attacher un ou plusieurs disques tooyour machine virtuelle. Nous allons décrire les spécifications hello plus en détail dans [cibles de l’évolutivité et les performances de stockage Premium](#scalability-and-performance-targets).

* **Objets blob de pages Premium**

    Le stockage Premium prend en charge les objets blob de pages. Page de l’utilisation des objets BLOB toostore des disques persistants, non managé pour les machines virtuelles dans un stockage Premium. Contrairement au stockage Azure standard, le stockage Premium ne prend pas en charge les objets blob de blocs, les objets blob d’ajout, les fichiers, les tables ou les files d’attente. Objets BLOB de pages Premium prend en charge les tailles de six P10 tooP50 et P60 (8191GiB). Objet blob de pages P60 Premium n’est pas pris en charge toobe attaché en tant que disques de machine virtuelle. 

    Tout objet placé dans un compte de stockage Premium est un objet blob de pages. objet blob de pages Hello aligne tooone Hello pris en charge des tailles mis en service. C’est pourquoi un compte premium storage n’est pas destiné toobe utilisé toostore des blobs minuscule.

* **Compte de stockage Premium**

    toostart avec le stockage Premium, créez un compte de stockage premium pour les disques non managés. Bonjour [portail Azure](https://portal.azure.com), toocreate un compte premium storage, choisissez hello **Premium** niveau de performances. Sélectionnez hello **stockage localement redondant (LRS)** l’option de réplication. Vous pouvez également créer un compte de stockage premium en définissant le type de hello trop**Premium_LRS** dans un des emplacements suivants de hello :
    * [API REST de stockage](https://docs.microsoft.com/rest/api/storageservices/Azure-Storage-Services-REST-API-Reference) (version 2014-02-14 ou version ultérieure)
    * [API REST de Gestion des services](http://msdn.microsoft.com/library/azure/ee460799.aspx) (version 2014-10-01 ou version ultérieure ; pour les déploiements classiques d’Azure)
    * [API REST du fournisseur de ressources Stockage Azure](https://docs.microsoft.com/rest/api/storagerp) (pour les déploiements Azure Resource Manager)
    * [Azure PowerShell](../powershell-install-configure.md) (version 0.8.10 ou version ultérieure)

    toolearn sur les limites de compte de stockage premium, consultez [cibles de l’évolutivité et les performances de stockage Premium](#premium-storage-scalability-and-performance-targets).

* **Stockage Premium localement redondant**

    Un compte de stockage premium prend en charge le stockage uniquement localement redondant en tant qu’option de réplication hello. Stockage localement redondant conserve trois copies des données de salutation au sein d’une seule région. Pour la récupération d’urgence régionale, vous devez sauvegarder vos disques de machines virtuelles dans une autre région à l’aide de [Sauvegarde Azure](../backup/backup-introduction-to-azure-backup.md). Vous devez également utiliser un compte de stockage géo-redondant (GRS) en tant que le coffre de sauvegarde hello. 

    Azure utilise votre compte de stockage comme conteneur pour vos disques non gérés. Lorsque vous créez une machine virtuelle Azure de série DS, DSv2, GS ou Fs avec des disques non gérés et que vous sélectionnez un compte de stockage Premium, votre système d’exploitation et les disques de données sont stockés dans ce compte de stockage.

## <a name="supported-vms"></a>Machines virtuelles prises en charge
Le stockage Premium prend en charge les machines virtuelles des séries DS, DSv2, GS, Ls et Fs. Vous pouvez utiliser des disques de stockage Standard et Premium avec ces types de machines virtuelles. Vous ne pouvez pas utiliser des disques de stockage Premium avec des séries de machines virtuelles qui ne sont pas compatibles avec le stockage Premium.

Pour plus d’informations sur les types et les tailles de machines virtuelles dans Azure pour Windows, consultez [Tailles des machines virtuelles Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Pour plus d’informations sur les types et les tailles de machines virtuelles dans Azure pour Linux, consultez [Tailles des machines virtuelles Linux](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Voici quelques-unes des fonctionnalités de hello de hello série DS, DSv2-series, GS, série Ls-série et les machines virtuelles de série Fs :

* **Service cloud**

    Vous pouvez ajouter des machines virtuelles de série DS tooa cloud service qui a uniquement des machines virtuelles série DS. N’ajoutez pas de machines virtuelles de série DS tooan service cloud existant qui a un type autre que les machines virtuelles de série DS. Vous pouvez migrer vos disques durs virtuels tooa nouveau service cloud existant qui s’exécute uniquement la série DS des machines virtuelles. Si vous souhaitez toouse hello même adresse IP virtuelle pour hello nouveau service cloud qui héberge vos machines virtuelles à la série DS, utilisez [adresses IP réservées](../virtual-network/virtual-networks-instance-level-public-ip.md). Machines virtuelles de série GS peuvent être ajoutés de service cloud existant tooan qui a uniquement des machines virtuelles GS-series.

* **Disque de système d’exploitation**

    Vous pouvez configurer votre toouse d’ordinateur virtuel de stockage Premium une prime ou un disque de système d’exploitation standard. Hello meilleure expérience utilisateur, nous recommandons à l’aide d’un disque de système d’exploitation basé sur le stockage Premium.

* **Disques de données**

    Vous pouvez utiliser premium et les disques standards dans hello même machine virtuelle de stockage Premium. Stockage Premium, vous pouvez configurer une machine virtuelle et attacher plusieurs toohello de disques de données persistantes machine virtuelle. Si nécessaire, la capacité de hello tooincrease et les performances du volume de hello, vous pouvez distribuer sur vos disques.

    > [!NOTE]
    > Si vous équilibrez les disques de données de stockage Premium à l’aide des [espaces de stockage](http://technet.microsoft.com/library/hh831739.aspx), configurez les espaces de stockage avec 1 colonne pour chaque disque utilisé. Dans le cas contraire, globalement les performances du volume de hello agrégés par bande peuvent être inférieure que prévu en raison d’une distribution inégale du trafic sur les disques hello. Par défaut, dans le Gestionnaire de serveur, vous pouvez définir des colonnes pour les disques de too8. Si vous avez plus de 8 disques, utilisez le volume de hello toocreate PowerShell. Spécifier le nombre de hello de colonnes manuellement. Sinon, hello Gestionnaire de serveur UI continue toouse 8 colonnes, même si vous avez d’autres disques. Par exemple, si vous disposez de 32 disques dans un agrégat unique, spécifiez 32 colonnes. nombre de hello toospecify de colonnes hello utilise de disque virtuel, Bonjour [New-VirtualDisk](http://technet.microsoft.com/library/hh848643.aspx) applet de commande PowerShell, utilisez hello *NumberOfColumns* paramètre. Pour plus d’informations, consultez [Vue d’ensemble des espaces de stockage](http://technet.microsoft.com/library/hh831739.aspx) et [FAQ sur les espaces de stockage](http://social.technet.microsoft.com/wiki/contents/articles/11382.storage-spaces-frequently-asked-questions-faq.aspx).
    >
    > 

* **Cache**

    Machines virtuelles de série de taille hello qui prennent en charge le stockage Premium propose unique mise en cache des niveaux élevés de débit et la latence. Hello mise en cache de la capacité dépasse les performances sous-jacent du disque de stockage premium. Vous pouvez définir le disque hello mise en cache de stratégie sur les disques de stockage premium trop**ReadOnly**, **ReadWrite**, ou **aucun**. stratégie de mise en cache de disque par défaut Hello est **ReadOnly** pour tous les disques de données premium, et **ReadWrite** pour les disques du système d’exploitation. Pour obtenir des performances optimales pour votre application, utilisez hello corriger les paramètres du cache. Par exemple, pour les disques de données de lectures ou en lecture seule, tels que les fichiers de données SQL Server, définissez disque hello mise en cache de stratégie trop**ReadOnly**. Pour les disques de données nombre élevé de l’écriture ou en écriture seule, tels que les fichiers du journal de SQL Server, définissez disque hello mise en cache de stratégie trop**aucun**. toolearn savoir plus sur l’optimisation de la conception de stockage Premium, consultez [conception pour des performances avec un stockage Premium](storage-premium-storage-performance.md).

* **Analyse**

    tooanalyze des performances de machine virtuelle à l’aide de disques dans le stockage Premium, activer les diagnostics de machine virtuelle Bonjour [portail Azure](https://portal.azure.com). Pour plus d’informations, consultez [Contrôle des machines virtuelles Microsoft Azure avec l’extension Azure Diagnostics](https://azure.microsoft.com/blog/2014/09/02/windows-azure-virtual-machine-monitoring-with-wad-extension/). 

    performances du disque toosee, utilisez basée sur le système d’exploitation outils tels que [Analyseur de performances Windows](https://technet.microsoft.com/library/cc749249.aspx) pour les machines virtuelles Windows et hello [iostat](http://linux.die.net/man/1/iostat) commande pour les machines virtuelles Linux.

* **Performances et limites de mise à l’échelle des machines virtuelles**

    Chaque taille de stockage Premium-prise en charge la machine virtuelle a des limites de l’échelle et les spécifications de performances pour les e/s, la bande passante et hello nombre de disques pouvant être joints par machine virtuelle. Lorsque vous utilisez des disques de stockage premium avec des machines virtuelles, assurez-vous qu’il y a suffisamment de IOPS et de bande passante sur le trafic de disque de machine virtuelle toodrive.

    Par exemple, une machine virtuelle STANDARD_DS1 a une bande passante dédiée de 32 Mo/s pour le trafic des disques de stockage Premium. Un disque de stockage Premium P10 peut fournir 100 Mo/s de bande passante. Si un disque de stockage premium P10 est attaché toothis machine virtuelle, elle peut être uniquement des too32 Mo/s. Elle ne peut pas utiliser hello que maximale 100 Mo/s disque P10 hello peut fournir.

    Actuellement, hello plus grande VM Bonjour série DS est hello Standard_DS15_v2. Hello Standard_DS15_v2 peut fournir des too960 Mo/s sur tous les disques. Hello plus grande VM Bonjour GS-série est hello Standard_GS5. Hello Standard_GS5 peut fournir des too2, 000 Mo/s sur tous les disques.

    Notez que ces limites s’appliquent uniquement au trafic de disques. Ces limites n’incluent pas le trafic réseau et les présences dans le cache. Une bande passante distincte est disponible pour le trafic réseau de machines virtuelles. La bande passante pour le trafic réseau est différente de la bande passante hello dédié utilisée par les disques de stockage premium.

    Pour hello dernières informations sur les e/s maximal et le débit (bande passante) pour les machines virtuelles de prise en charge de stockage Premium, consultez [tailles de machine virtuelle Windows](../virtual-machines/virtual-machines-windows-sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) ou [tailles de Linux VM](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

    Pour plus d’informations sur les disques de stockage premium et leurs limites de débit et d’e/s, consultez le tableau de hello dans la section suivante de hello.

## <a name="scalability-and-performance-targets"></a>Cibles de performance et d’évolutivité
Dans cette section, nous décrivons tooconsider de cibles de performances et évolutivité hello lorsque vous utilisez le stockage Premium.

Comptes de stockage Premium ont hello les cibles d’extensibilité suivantes :

| Capacité totale des comptes | Bande passante totale pour un compte de stockage localement redondant |
| --- | --- | 
| Capacité du disque : 35 To <br>Capacité d’instantané : 10 To | Les too50 les gigabits par seconde pour entrant<sup>1</sup> + sortant<sup>2</sup> |

<sup>1</sup> toutes les données (demandes) qui sont envoyées de compte de stockage tooa

<sup>2</sup> Toutes les données (réponses) reçues d’un compte de stockage

Pour plus d’informations, consultez [Objectifs d’extensibilité et de performances de stockage Azure](storage-scalability-targets.md).

Si vous utilisez des comptes de stockage premium pour les disques non managés et que votre application dépasse les objectifs d’évolutivité hello d’un seul compte de stockage, vous pourriez toomigrate toomanaged disques. Si vous ne souhaitez pas toomigrate toomanaged disques, générez votre application toouse plusieurs comptes de stockage. Ensuite, partitionnez vos données sur ces comptes de stockage. Par exemple, si vous souhaitez que les disques de 51-to tooattach entre plusieurs machines virtuelles, bien les répartir sur deux comptes de stockage. 35 To est limite hello pour un compte de stockage premium unique. Vérifiez qu’un compte de stockage Premium n’a jamais plus de 35 To de disques configurés.

### <a name="premium-storage-disk-limits"></a>Limites des disques de stockage Premium
Lorsque vous configurer un disque de stockage premium, taille hello du disque de hello détermine hello IOPS maximal et le débit (bande passante). Azure propose sept types de disques de stockage premium : P4 (Managed Disks uniquement), P6 (Managed Disks uniquement), P10, P20, P30, P40 et P50. Chaque type de disque de stockage Premium a des limites d’E/S par seconde et de débit spécifiques. Hello tableau suivant décrit les limites pour les types de disque hello :

| Type de disque Premium  | P4    | P6    | P10   | P20   | P30   | P40   | P50   | 
|---------------------|-------|-------|-------|-------|-------|-------|-------|
| Taille du disque           | 32 Go| 64 Go| 128 Go| 512 Go            | 1024 Go (1 To)    | 2 048 Go (2 To)    | 4 095 Go (4 To)    | 
| IOPS par disque       | 120   | 240   | 500   | 2 300              | 5 000              | 7500              | 7500              | 
| Débit par disque | 25 Mo par seconde  | 50 Mo par seconde  | 100 Mo par seconde | 150 Mo par seconde | 200 Mo par seconde | 250 Mo par seconde | 250 Mo par seconde | 

> [!NOTE]
> Assurez-vous que la bande passante suffisante est disponible sur le trafic de disque toodrive de machine virtuelle, comme décrit dans [stockage Premium-prise en charge les machines virtuelles](#premium-storage-supported-vms). Sinon, votre débit de disque et des IOPS est contraint toolower valeurs. Débit maximal et des IOPS sont basées sur les limites de machine virtuelle hello, pas sur les limites de disque hello décrites dans le tableau précédent de hello.  
> 
> 

Voici certains tooknow points importants sur les cibles de l’évolutivité et les performances de stockage Premium :

* **Capacité allouée et performances**

    Lorsque vous configurez un disque de stockage premium, contrairement à un stockage standard, vous avez la garantie hello capacité, l’e/s et un débit de ce disque. Par exemple, si vous créez un disque P50, Azure configure une capacité de stockage de 4095 Go, 7500 E/S par seconde et un débit de 250 Mo/s pour ce disque. Votre application peut utiliser tout ou partie de la capacité de hello et de performances.

* **Taille du disque**

    Mappages Azure hello toohello (arrondi) de taille de disque plus proche de l’option de disque de stockage premium, tel que spécifié dans la table hello Bonjour précédant la section. Par exemple, une taille de disque de 100 Go correspond à l’option P10. Il peut effectuer too500 IOPS, avec des too100 débit en Mo/s. De même, une taille de disque de 400 Go correspond à l’option P20. Il peut effectuer des too2, 300 e/s, avec un débit 150 Mo/s.
    
    > [!NOTE]
    > Vous pouvez facilement agrandir hello disques existants. Par exemple, vous pourriez taille de hello tooincrease d’un disque de 30 Go too128 Go, ou même too1 to. Ou, vous souhaiterez tooconvert votre tooa P30 sur le disque P20 car vous avez besoin de plus de capacité ou plus d’e/s et le débit. 
    > 
 
* **Taille des E/S**

    taille de Hello d’une e/s est de 256 Ko. Si les données hello transférées sont inférieure à 256 Ko, il est considéré comme 1 unité d’e/s. Les tailles d’E/S supérieures sont divisées en plusieurs unités d’E/S de 256 Ko. Par exemple, 1 100 Ko d’E/S correspondent à 5 unités d’E/S.

* **Débit**

    limite de débit Hello inclut des écritures toohello disque, et il inclut les opérations de lecture de disque qui ne sont pas pris en charge à partir du cache de hello. Par exemple, un disque P10 offre un débit de 100 Mo/s. Quelques exemples de débit valid pour un disque P10 sont présentés dans hello tableau suivant :

    | Débit maximum par disque P10 | Lectures à partir du disque non mises en cache | Les écritures non mises en cache toodisk |
    | --- | --- | --- |
    | 100 Mo/s | 100 Mo/s | 0 |
    | 100 Mo/s | 0 | 100 Mo/s |
    | 100 Mo/s | 60 Mo/s | 40 Mo/s |

* **Présences dans le cache**

    Présences dans le cache n’êtes pas limités par hello allouée IOPS ou débit du disque de hello. Par exemple, lorsque vous utilisez un disque de données avec un **ReadOnly** paramètre de cache sur un ordinateur virtuel qui est pris en charge par le stockage Premium, les lectures sont servies à partir du cache de hello n’est pas sujet toohello IOPS et caps de débit du disque de hello. Si la charge de travail hello d’un disque est essentiellement lit, vous risquez d’obtenir un débit très élevé. cache de Hello est sujet tooseparate e/s et les limites de débit à hello niveau de la machine virtuelle, en fonction de hello taille de machine virtuelle. Les machines virtuelles DS exécutent environ 4 000 E/S par seconde et ont un débit de 33 Mo/s par cœur pour les E/S du cache et du disque SSD local. Les machines virtuelles GS ont une limite de 5 000 E/S par seconde et un débit de 50 Mo/s par cœur pour les E/S du cache et du disque SSD local. 

## <a name="throttling"></a>Limitation
La limitation peut se produire, si votre application IOPS ou le débit dépasse les limites de hello alloué pour un disque de stockage premium. La limitation peut également se produire si votre trafic disque total sur tous les disques sur la machine virtuelle de hello dépasse la limite de bande passante disque hello disponible pour hello machine virtuelle. tooavoid la limitation, nous vous recommandons de limiter nombre hello de demandes d’e/s de disque de hello en attente. Utilisez une limite basée sur les objectifs de l’évolutivité et les performances de disque hello que vous avez configuré et sur toohello disponible de la bande passante disque hello machine virtuelle.  

Votre application peut obtenir la latence la plus faible de hello lorsqu’elle est conçue de limitation tooavoid. Toutefois, si hello nombre de demandes d’e/s de disque de hello en attente est trop petite, votre application ne tirent pas parti de hello niveaux IOPS et le débit maximum qui sont disponibles toohello disque.

Hello suivant exemples montrent comment toocalculate la limitation de niveaux. Tous les calculs sont basés sur une taille d’unité d’E/S de 256 Ko.

### <a name="example-1"></a>Exemple 1
Votre application a traité 495 unités d’E/S d’une taille de 16 Ko par seconde sur un disque P10. unités d’e/s de Hello sont comptabilisées comme 495 IOPS. Si vous essayez d’une e/s de 2 Mo dans hello même seconde, total hello d’unités d’e/s est égale too495 + 8 IOPS. C’est parce qu’e/s de 2 Mo = 256 Ko/2 048 Ko = 8 d’e/s, unités, lors de la taille d’unité d’e/s de hello est de 256 Ko. Étant donné que la somme hello 495 + 8 dépasse la limite de IOPS 500 hello pour le disque de hello, la limitation se produit.

### <a name="example-2"></a>Exemple 2
Votre application a traité 400 unités d’E/S de 256 Ko sur un disque P10. la bande passante totale Hello consommée est (400 &#215; 256) / 1 024 Ko = 100 MB/s. Un disque P10 a une limite de débit de 100 Mo/s. Si votre application essaie tooperform davantage d’opérations d’e/s dans ce deuxième, elle est limitée, car il dépasse la limite de hello allouée.

### <a name="example-3"></a>Exemple 3
Vous avez une machine virtuelle DS4 avec deux disques P30. Chaque disque P30 peut gérer un débit de 200 Mo/s. Toutefois, une machine virtuelle DS4 a une bande passante disque maximale de 256 Mo/s. Vous ne peut pas de lecteur à la fois débit maximal de disques attachés toohello sur cet ordinateur virtuel de DS4 à hello même temps. tooresolve, vous pouvez supporter le trafic de 200 Mo/s sur un disque et 56 Mo/s sur hello autre disque. Si somme hello de votre trafic disque dépasse 256 Mo/s, le trafic de disque est limité.

> [!NOTE]
> Si votre trafic disque se compose principalement de petite taille d’e/s, votre application probablement atteignez limite d’IOPS hello avant la limite de débit hello. Toutefois, si le trafic de disque hello se compose principalement de grande taille d’e/s, votre application probable est atteint limite de débit hello tout d’abord, au lieu de la limite d’IOPS hello. Vous pouvez optimiser les E/S par seconde et la capacité de débit de votre application à l’aide des tailles d’E/S optimales. En outre, vous pouvez limiter nombre hello de demandes en attente d’e/s pour un disque.
> 

toolearn en savoir plus sur la conception pour optimiser les performances en utilisant un stockage Premium, consultez [conception pour des performances avec un stockage Premium](storage-premium-storage-performance.md).

## <a name="snapshots-and-copy-blob"></a>Captures instantanées et copie d’objets blob

toohello service de stockage, les fichiers de disque dur virtuel hello est un objet blob de pages. Vous pouvez prendre des instantanés d’objets BLOB de pages et les copier tooanother emplacement, comme tooa autre compte de stockage.

### <a name="unmanaged-disks"></a>Disques non gérés

Créer [instantanés incrémentiels](storage-incremental-snapshots.md) pour les disques premium non managé hello la même façon que vous utilisez des instantanés de stockage standard. Stockage Premium prend en charge le stockage uniquement localement redondant en tant qu’option de réplication hello. Nous vous recommandons de créer des instantanés puis copiez le compte de stockage standard géo-redondant tooa hello instantanés. Pour plus d’informations, consultez [Options de redondance du stockage Azure](storage-redundancy.md).

Si un disque est attaché tooa machine virtuelle, certaines opérations d’API sur le disque de hello ne sont pas autorisées. Par exemple, vous ne pouvez pas effectuer une [Copy Blob](/rest/api/storageservices/Copy-Blob) opération sur cet objet blob si hello disque est attaché tooa machine virtuelle. Au lieu de cela, créez tout d’abord un instantané de cet objet blob à l’aide de hello [objet Blob instantané](/rest/api/storageservices/Snapshot-Blob) API REST. Puis, exécutez hello [Copy Blob](/rest/api/storageservices/Copy-Blob) Hello de hello instantané toocopy disque attaché. Vous pouvez également détacher un disque de hello et puis effectuez les opérations nécessaires.

Hello suivant limites s’appliquent instantanés d’objet blob de stockage de toopremium :

| Limites de stockage Premium | Valeur |
| --- | --- |
| Nombre maximal d’instantanés par objet blob | 100 |
| Capacité du compte de stockage pour les instantanés<br>(Inclut uniquement les données des instantanés. N’inclut pas celles d’un objet blob de base.) | 10 To |
| Intervalle de temps minimal entre deux instantanés consécutifs | 10 minutes |

toomaintain copies géo-redondant de vos captures instantanées, vous pouvez copier des instantanés à partir d’un compte de stockage standard géo-redondant premium storage compte tooa à l’aide de AzCopy ou copie d’objets Blob. Pour plus d’informations, consultez [transférer des données à l’utilitaire de ligne de commande hello AzCopy](storage-use-azcopy.md) et [Copy Blob](/rest/api/storageservices/Copy-Blob).

Pour plus d’informations sur l’exécution d’opérations REST sur les objets blob de pages dans les comptes de stockage Premium, consultez [Opérations de service blob avec le stockage Premium Azure ](http://go.microsoft.com/fwlink/?LinkId=521969).

### <a name="managed-disks"></a>Disques gérés

Un instantané d’un disque géré est une copie en lecture seule de disque géré de hello. instantané de Hello est stocké comme un disque géré standard. Actuellement, les [instantanés incrémentiels](storage-incremental-snapshots.md) ne sont pas pris en charge pour les disques gérés. toolearn tootake un instantané d’un disque géré, voir [créer une copie d’un disque dur virtuel stocké comme Azure géré disque à l’aide d’instantanés gérés dans Windows](../virtual-machines/virtual-machines-windows-snapshot-copy-managed-disk.md) ou [créer une copie d’un disque dur virtuel stocké comme Azure géré disque à l’aide de gérés instantanés dans Linux](../virtual-machines/linux/snapshot-copy-managed-disk.md).

Si un disque managé est attaché tooa machine virtuelle, certaines opérations d’API sur le disque de hello ne sont pas autorisées. Par exemple, vous ne peut pas générer un tooperform de signature (SAP) d’accès partagé une opération de copie pendant les disque hello attaché tooa machine virtuelle. Au lieu de cela, tout d’abord créer un instantané du disque de hello, puis copier hello d’instantané de hello. Ou bien, vous pouvez détacher un disque de hello et puis générer une opération de copie SAS tooperform hello.


## <a name="premium-storage-for-linux-vms"></a>Stockage Premium pour les machines virtuelles Linux
Vous pouvez utiliser hello suivant toohelp informations que permet de paramétrer vos machines virtuelles de Linux dans le stockage Premium :

évolutivité de tooachieve cible dans un stockage Premium, pour l’ensemble de tous les disques de stockage premium avec cache trop**ReadOnly** ou **aucun**, vous devez désactiver « barrières » lorsque vous montez le système de fichiers hello. Vous n’avez pas besoin barrières dans ce scénario, car hello écrit toopremium les disques de stockage sont durables pour ces paramètres de cache. Lors de la demande d’écriture hello s’est correctement déroulée, les données ont été écrites toohello les magasin persistant. toodisable « barrières », utilisez une des méthodes suivantes de hello. Choisissez un hello pour votre système de fichiers :
  
* Pour **reiserFS**, toodisable barrières, utilisez hello `barrier=none` option de montage. (les barrières tooenable, utilisez `barrier=flush`.)
* Pour **ext3/ext4**, toodisable barrières, utilisez hello `barrier=0` option de montage. (les barrières tooenable, utilisez `barrier=1`.)
* Pour **XFS**, toodisable barrières, utilisez hello `nobarrier` option de montage. (les barrières tooenable, utilisez `barrier`.)
* Pour les disques de stockage premium avec cache défini trop**ReadWrite**, activer les barrières de durabilité de l’écriture.
* Toopersist des étiquettes de volume après le redémarrage de hello machine virtuelle, vous devez mettre à jour/etc/fstab avec hello identificateur unique universel (UUID) références toohello disques. Pour plus d’informations, consultez [ajouter un tooa disque géré Linux VM](../virtual-machines/linux/add-disk.md).

Hello suivant les distributions Linux ont été validée pour le stockage Azure Premium. Pour meilleures performances et la stabilité avec le stockage Premium, nous recommandons que vous mettez à niveau votre tooone de machines virtuelles de ces versions, au minimum (ou tooa version ultérieure). Certaines des hello requérir hello dernière Integration Services Linux (LIS), version 4.0, pour Azure. toodownload et installer une distribution, et suivre le lien de hello répertorié dans hello tableau suivant. Nous ajoutons une liste des images toohello que nous avons terminé la validation. Notez que nos validations indiquent que les performances varient pour chaque image. Les performances dépendent des caractéristiques de la charge de travail et de vos paramètres d’image. Chaque image est optimisée pour des charges de travail particulières.

| Distribution | Version | Noyau pris en charge | Détails |
| --- | --- | --- | --- |
| Ubuntu | 12.04 | 3.2.0-75.110+ | Ubuntu-12_04_5-LTS-amd64-Server-20150119-en-us-30GB |
| Ubuntu | 14.04 | 3.13.0-44.73+ | Ubuntu-14_04_1-LTS-amd64-Server-20150123-en-us-30GB |
| Debian | 7.x, 8.x | 3.16.7-ckt4-1+ | &nbsp; |
| SUSE | SLES 12| 3.12.36-38.1+| suse-sles-12-priority-v20150213 <br> suse-sles-12-v20150213 |
| SUSE | SLES 11 SP4 | 3.0.101-0.63.1+ | &nbsp; |
| CoreOS | 584.0.0+| 3.18.4+ | CoreOS 584.0.0 |
| CentOS | 6.5, 6.6, 6.7, 7.0 | &nbsp; | [LIS4 requis](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Consultez la section suivante de hello* |
| CentOS | 7.1+ | 3.10.0-229.1.2.el7+ | [LIS4 recommandé](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) <br> *Consultez la section suivante de hello* |
| Red Hat Enterprise Linux (RHEL) | 6.8+, 7.2+ | &nbsp; | &nbsp; |
| Oracle | 6.0+, 7.2+ | &nbsp; | UEK4 ou RHCK |
| Oracle | 7.0-7.1 | &nbsp; | UEK4 ou RHCK avec [LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |
| Oracle | 6.4-6.7 | &nbsp; | UEK4 ou RHCK avec [LIS 4.1+](http://go.microsoft.com/fwlink/?LinkID=403033&clcid=0x409) |


### <a name="lis-drivers-for-openlogic-centos"></a>Pilotes LIS pour Openlogic CentOS

Si vous exécutez OpenLogic CentOS VM, exécutez hello commande tooinstall hello les derniers pilotes :

```
sudo rpm -e hypervkvpd  ## (Might return an error if not installed. That's OK.)
sudo yum install microsoft-hyper-v
```

tooactivate hello nouveaux pilotes, redémarrer hello.

## <a name="pricing-and-billing"></a>Tarification et facturation

Lorsque vous utilisez le stockage Premium, hello suivant des considérations relatives à la facturation s’appliquent :

* **Taille de disque de stockage Premium et de l’objet blob**

    Facturation d’un disque de stockage premium ou d’un objet blob dépend de la taille de hello mis en service de disque de hello ou un objet blob. Mappages Azure hello toohello taille approvisionnée (arrondi) plus proche de l’option de disque de stockage premium. Pour plus d’informations, consultez le tableau de hello dans [cibles de l’évolutivité et les performances de stockage Premium](#premium-storage-scalability-and-performance-targets). Chaque tooa de mappages de disque pris en charge configuré la taille du disque et est facturée en conséquence. Facturation pour n’importe quel disque approvisionné est calculé au prorata toutes les heures à l’aide de prix mensuel de hello pour l’offre de stockage Premium hello. Par exemple, si vous configuré un disque P10 et supprimiez après 20 heures, vous êtes facturé pour hello P10 offre au prorata too20 heures. Il s’agit, quelle que soit la quantité hello de données réelles écrites toohello disque ou hello IOPS et le débit utilisé.

* **Captures instantanées de disques non gérés Premium**

    Captures instantanées sur des disques premium non managée sont facturées pour une capacité supplémentaire hello utilisée par les instantanés de hello. Pour plus d’informations sur les captures instantanées, consultez [Créer un instantané d’objet blob](/rest/api/storageservices/Snapshot-Blob).

* **Captures instantanées de disques gérés Premium**

    Un instantané d’un disque géré est une copie en lecture seule du disque de hello. disque de Hello est stocké comme un disque géré standard. Frais instantané même hello comme une norme géré disque. Par exemple, si vous prenez un instantané d’un disque géré 128 Go premium, hello d’instantané de hello coûte disque géré standard de 128 Go tooa équivalent.  

* **Transferts de données sortantes**

    Les [Transferts de données sortantes](https://azure.microsoft.com/pricing/details/data-transfers/) (données sortant des centres de données Azure) sont facturés en fonction de la bande passante utilisée.

Pour plus d’informations sur la tarification du stockage Premium, les machines virtuelles prises en charge par le stockage Premium et les disques gérés, consultez ces articles :

* [Tarification du stockage Azure](https://azure.microsoft.com/pricing/details/storage/)
* [Tarification des machines virtuelles](https://azure.microsoft.com/pricing/details/virtual-machines/)
* [Tarification des disques gérés](https://azure.microsoft.com/pricing/details/managed-disks/)

## <a name="azure-backup-support"></a>Support Sauvegarde Azure 

Pour la récupération d’urgence régionale, vous devez sauvegarder vos disques de machines virtuelles dans une autre région à l’aide de [Sauvegarde Azure](../backup/backup-introduction-to-azure-backup.md) et d’un compte de stockage GRS comme coffre de sauvegarde.

toocreate un travail de sauvegarde avec les sauvegardes basées sur le temps, restauration facile de machine virtuelle et des stratégies de rétention de sauvegarde, utilisez Azure Backup. Vous pouvez utiliser la sauvegarde avec des disques gérés et non gérés. Pour plus d’informations, consultez [Sauvegarde Azure de machines virtuelles avec des disques non gérés](../backup/backup-azure-vms-first-look-arm.md) et [Sauvegarde Azure de machines virtuelles avec des disques gérés](../backup/backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). 

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur le stockage Premium, consultez hello suivant des articles.

### <a name="design-and-implement-with-premium-storage"></a>Conception et implémentation avec le stockage Premium
* [Conception optimisée pour les performances avec le stockage Premium](storage-premium-storage-performance.md)
* [Opérations de stockage Blob avec le stockage Premium](http://go.microsoft.com/fwlink/?LinkId=521969)

### <a name="operational-guidance"></a>Instructions d’utilisation
* [Migrer tooAzure stockage Premium](storage-migration-to-premium-storage.md)

### <a name="blog-posts"></a>Billets de blog :
* [Mise à la disposition générale du stockage Premium Azure](https://azure.microsoft.com/blog/azure-premium-storage-now-generally-available-2/)
* [Annonce hello GS-series : ajout de stockage Premium toohello de prise en charge de plus grande de machines virtuelles dans hello cloud public](https://azure.microsoft.com/blog/azure-has-the-most-powerful-vms-in-the-public-cloud/)
