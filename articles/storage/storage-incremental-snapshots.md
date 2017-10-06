---
title: "aaaUse des instantanés incrémentiels pour la sauvegarde et récupération de disques de machine virtuelle Azure non managés | Documents Microsoft"
description: "Créer une solution personnalisée pour la sauvegarde et la récupération de vos disques de machine virtuelle Azure à l’aide d’instantanés incrémentiels."
services: storage
documentationcenter: na
author: aungoo-msft
manager: tadb
editor: tysonn
ms.assetid: 3524b987-bd65-4e35-83e7-fbc2136643e5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: aungoo
ms.openlocfilehash: 6d3e6d78e953f77a1028ac35dcde1ef046dbc3bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-unmanaged-vm-disks-with-incremental-snapshots"></a>Sauvegarder les disques de machines virtuelles Azure non gérés avec des captures instantanées incrémentielles
## <a name="overview"></a>Vue d'ensemble
Le stockage Azure fournit une fonctionnalité de hello tootake des instantanés d’objets BLOB. Instantanés capturent l’état de l’objet blob hello à ce stade dans le temps. Dans cet article, nous allons décrire comment gérer des sauvegardes de disques de machine virtuelle à l’aide d’instantanés. Vous pouvez utiliser cette méthode lorsque vous ne choisissez pas toouse sauvegarde Azure et Service de récupération et souhaits toocreate une stratégie de sauvegarde personnalisée pour vos disques de machine virtuelle.

Les disques de machine virtuelle Azure sont stockés en tant qu’objets blob de pages dans Azure Storage. Étant donné que nous parlons de stratégie de sauvegarde pour les disques de machine virtuelle dans cet article, nous avons fait référence à toosnapshots dans le contexte de hello d’objets BLOB de pages. toolearn savoir plus sur les captures instantanées, consultez trop[création d’un instantané d’un objet Blob](https://msdn.microsoft.com/library/azure/hh488361.aspx).

## <a name="what-is-a-snapshot"></a>Qu’est-ce qu’un instantané ?
Un instantané d’objet blob est une version en lecture seule d’un objet blob capturé à un instant donné. Un instantané peut être lu, copié ou supprimé, mais pas modifié. Instantanés fournissent un tooback moyen d’un objet blob, tel qu’il apparaît à un moment donné. Jusqu'à ce que le reste de la version 2015-04-05 vous aviez des captures instantanées de hello capacité toocopy complète. Avec hello REST version 2015-08-07 et versions ultérieures, vous pouvez également copier des instantanés incrémentiels.

## <a name="full-snapshot-copy"></a>Copie d’un instantané complet
Les instantanés peuvent être copiées du compte de stockage tooanother en tant que les sauvegardes de l’objet blob de base hello tookeep blob. Vous pouvez également copier un instantané sur l’objet blob de base, qui est similaire à la restauration hello blob tooan version antérieure. Lorsqu’un instantané est copié à partir d’un tooanother de compte de stockage, il occupera hello même espace en tant qu’objet blob de page de base hello. Par conséquent, la copie d’instantanés entières à partir d’un tooanother de compte de stockage sera lente et consommera également beaucoup d’espace dans le compte de stockage cible hello.

> [!NOTE]
> Si vous copiez à destination de tooanother hello objet blob de base, les instantanés hello d’objet blob de hello ne sont pas copiés en même temps. De même, si vous remplacez un objet blob de base avec une copie, instantanés associés d’objet blob de base hello ne sont pas affectés et restent intacts sous le nom de l’objet blob de base.
> 
> 

### <a name="back-up-disks-using-snapshots"></a>Sauvegarder des disques à l’aide d’instantanés
En tant qu’une stratégie de sauvegarde pour vos disques de machine virtuelle, vous pouvez prendre des instantanés périodiques de l’objet blob de disque ou la page hello et copiez-les tooanother compte de stockage à l’aide des outils tels que [Copy Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) opération ou [AzCopy](storage-use-azcopy.md). Vous pouvez copier un instantané tooa page objet blob de destination avec un nom différent. Hello résultant destination objet blob de pages est un objet blob de page accessible en écriture et pas un instantané. Plus loin dans cet article, nous décrirons les sauvegardes tootake étapes de disques de machine virtuelle à l’aide de captures instantanées.

### <a name="restore-disks-using-snapshots"></a>Restaurer des disques à l’aide d’instantanés
Lorsqu’il est toorestore temps votre version stable précédente disque tooa capturée dans un des instantanés de sauvegarde hello, vous pouvez copier un instantané sur l’objet blob de page de base hello. Une fois l’instantané d’hello blob de page de base toohello promues, hello instantané est conservé, mais sa source est remplacée par une copie qui peut être lue et modifiée. Plus loin dans cet article, nous décrirons étapes toorestore une version antérieure de votre disque à partir de son instantané.

### <a name="implementing-full-snapshot-copy"></a>Implémentation de la copie d’un instantané complet
Vous pouvez implémenter une capture instantanée complète en procédant comme suit de hello,

* Tout d’abord, prenez un instantané de hello objet blob de base à l’aide de hello [objet Blob instantané](https://msdn.microsoft.com/library/azure/ee691971.aspx) opération.
* Ensuite, copiez hello instantané tooa cible stockage compte à l’aide [Copy Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx).
* Répétez ce processus toomaintain sauvegarder votre objet blob de base.

## <a name="incremental-snapshot-copy"></a>Copie d’un instantané incrémentiel
nouvelle fonctionnalité de Hello dans [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) API fournit une quantité tooback façon mieux des instantanés hello de vos objets BLOB de pages ou de disques. Hello API retourne une liste hello des modifications entre l’objet blob de base hello et les instantanés de hello. Cela réduit la quantité de hello d’espace de stockage utilisé sur le compte de sauvegarde hello. Hello API prend en charge les objets BLOB de pages sur le stockage Premium ainsi que le stockage Standard. À l’aide de cette API, vous pouvez créer des solutions de sauvegarde plus rapides et efficaces pour les machines virtuelles Azure. Ce sera disponible avec hello REST version 2015-08-07 et versions ultérieures.

La copie d’instantané incrémentielle vous permet de toocopy à partir d’un stockage compte tooanother hello différence,

* l’objet blob de base et son instantané OU
* Les deux instantanés d’objet blob de base hello

Condition hello conditions suivantes est remplie,

* objet blob de Hello a été créé sur Jan-01-2016 ou version ultérieure.
* objet blob de Hello n’a pas été enregistré avec [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) ou [Copy Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx) entre deux instantanés.

**Remarque**: cette fonctionnalité est disponible pour les objets blob de pages Azure Standard et Premium.

Lorsque vous avez une stratégie de sauvegarde personnalisée qui utilise des instantanés, copie d’instantanés de hello à partir d’un tooanother de compte de stockage peut être très lente et consomme beaucoup d’espace de stockage. Au lieu de copier un compte de stockage de sauvegarde tooa hello intégralité de l’instantané, vous pouvez écrire la différence hello entre un blob de page sauvegarde tooa instantanés consécutifs. De cette manière, le hello toocopy et espace toostore sauvegardes est sensiblement réduite.

### <a name="implementing-incremental-snapshot-copy"></a>Implémentation de la copie d’un instantané incrémentiel
Vous pouvez implémenter la copie d’instantané incrémentielle en procédant comme suit de hello,

* Prendre un instantané de l’utilisation de base blob hello [objet Blob instantané](https://msdn.microsoft.com/library/azure/ee691971.aspx).
* Copie hello instantané toohello cible stockage de sauvegarde compte à l’aide de [Copy Blob](https://msdn.microsoft.com/library/azure/dd894037.aspx). Il s’agit d’objets blob de page sauvegarde hello. Prenez un instantané de cet objet blob de pages de sauvegarde et stockez-le dans un compte de sauvegarde.
* Prendre une autre capture instantanée de hello objet blob de base à l’aide d’objet Blob instantané.
* Obtenir la différence entre les premier et deuxième instantanés d’objet blob de base à l’aide de hello [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx). Utilisez le paramètre hello **prevsnapshot** toospecify hello hello capture instantanée différence de hello tooget avec la valeur DateTime. Lorsque ce paramètre est présent, hello réponse REST inclut uniquement les pages hello qui ont été modifiés entre l’instantané de la cible et l’instantané précédent, y compris les pages clairs.
* Utilisez [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) tooapply ces objets blob de modifications toohello page de sauvegarde.
* Enfin, prenez un instantané de l’objet blob de page sauvegarde hello et stockez-le dans le compte de stockage de sauvegarde hello.

Dans la section suivante de hello, nous allons examiner plus en détail comment vous pouvez gérer des sauvegardes de disques à l’aide de la copie d’instantané incrémentielle

## <a name="scenario"></a>Scénario
Dans cette section, nous allons décrire un scénario qui implique une stratégie de sauvegarde personnalisée pour les disques de machine virtuelle à l’aide d’instantanés.

Prenez une machine virtuelle Azure de série DS avec un disque P30 de stockage Premium attaché. disque Hello P30 appelé *mypremiumdisk* est stocké dans un compte de stockage premium appelé *mypremiumaccount*. Un compte de stockage standard appelé *mybackupstdaccount* sera utilisé pour le stockage de sauvegarde hello de *mypremiumdisk*. Nous aimerions tookeep un instantané de *mypremiumdisk* toutes les 12 heures.

toolearn sur la création de compte de stockage et des disques, consultez trop[comptes de stockage sur Azure](storage-create-storage-account.md).

toolearn sur la sauvegarde des machines virtuelles Azure, consultez trop[les sauvegardes de Plan Azure VM](../backup/backup-azure-vms-introduction.md).

## <a name="steps-toomaintain-backups-of-a-disk-using-incremental-snapshots"></a>Sauvegardes de toomaintain étapes d’un disque à l’aide d’instantanés incrémentiels
Hello étapes décrites ci-dessous seront prendre des instantanés de *mypremiumdisk* et conservez des sauvegardes hello dans *mybackupstdaccount*. Hello sauvegarde sera un objet blob de page standard appelé *mybackupstdpageblob*. Hello objet blob de pages sauvegarde reflètent toujours hello même état que l’instantané d’hello *mypremiumdisk*.

1. Tout d’abord, créer des objets blob de page sauvegarde hello pour votre disque de stockage premium. toodo cette option, prenez un instantané de *mypremiumdisk* appelé *mypremiumdisk_ss1*.
2. Copiez cette toomybackupstdaccount instantané en tant qu’objet blob de pages appelé *mybackupstdpageblob*.
3. Prenez un instantané de *mybackupstdpageblob* nommé *mybackupstdpageblob_ss1*, à l’aide de [Snapshot Blob](https://msdn.microsoft.com/library/azure/ee691971.aspx), et stockez-le dans *mybackupstdaccount*.
4. Au cours de la fenêtre de sauvegarde hello, créer un nouvel instantané de *mypremiumdisk*, par exemple *mypremiumdisk_ss2*et les stocker dans *mypremiumaccount*.
5. Obtenir les modifications incrémentielles hello entre les instantanés hello deux, *mypremiumdisk_ss2* et *mypremiumdisk_ss1*, à l’aide [GetPageRanges](https://msdn.microsoft.com/library/azure/ee691973.aspx) sur  *mypremiumdisk_ss2* avec **prevsnapshot** paramètre la valeur timestamp toohello de *mypremiumdisk_ss1*. Écrire ces blob de page de sauvegarde des modifications incrémentielles toohello *mybackupstdpageblob* dans *mybackupstdaccount*. S’il existe des plages supprimés dans les modifications incrémentielles hello, elles doivent être effacées à partir de l’objet blob de page sauvegarde hello. Utilisez [PutPage](https://msdn.microsoft.com/library/azure/ee691975.aspx) blob de page sauvegarde toohello toowrite les modifications incrémentielles.
6. Prendre un instantané de l’objet blob de page sauvegarde hello *mybackupstdpageblob*, appelé *mybackupstdpageblob_ss2*. Supprimer l’instantané précédent de hello *mypremiumdisk_ss1* à partir du compte de stockage premium.
7. Répétez les étapes 4 à 6 pour chaque fenêtre de sauvegarde. De cette façon, vous pouvez gérer les sauvegardes de *mypremiumdisk* dans un compte de stockage Standard.

![Sauvegarder un disque à l’aide d’instantanés incrémentiels](./media/storage-incremental-snapshots/storage-incremental-snapshots-1.png)

## <a name="steps-toorestore-a-disk-from-snapshots"></a>Étapes toorestore un disque d’instantanés
Hello étapes décrites ci-dessous restaure le disque premium, *mypremiumdisk* tooan instantané précédemment à partir du compte de stockage de sauvegarde hello *mybackupstdaccount*.

1. Identifiez hello point dans le temps que vous souhaitez toorestore hello premium disque. Supposons qu’est snapshot *mybackupstdpageblob_ss2*, qui est stockée dans le compte de stockage de sauvegarde hello *mybackupstdaccount*.
2. Dans mybackupstdaccount, promouvoir l’instantané d’hello *mybackupstdpageblob_ss2* en tant que nouveau blob de page de base sauvegarde hello *mybackupstdpageblobrestored*.
3. Prenez un instantané de cet objet blob de pages de sauvegarde restauré appelé *mybackupstdpageblobrestored_ss1*.
4. Objet blob de pages copie restaurée de hello *mybackupstdpageblobrestored* de *mybackupstdaccount* trop*mypremiumaccount* en tant que disque premium de la nouvelle hello  *mypremiumdiskrestored*.
5. Prenez un instantané de *mypremiumdiskrestored*, appelé *mypremiumdiskrestored_ss1* pour les futures sauvegardes incrémentielles.
6. Point de série de hello DS disque de machine virtuelle toohello restauré *mypremiumdiskrestored* et détacher hello ancien *mypremiumdisk* à partir de la machine virtuelle de hello.
7. Commencer les processus de sauvegarde hello décrites dans la section précédente pour le disque de hello restauré *mypremiumdiskrestored*, à l’aide de hello *mybackupstdpageblobrestored* en tant qu’objet blob de page sauvegarde hello.

![Restaurer un disque à partir d’instantanés](./media/storage-incremental-snapshots/storage-incremental-snapshots-2.png)

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur la création des instantanés d’un objet blob et de planification de votre infrastructure de sauvegarde de machine virtuelle à l’aide de liens hello ci-dessous.

* [Création d’un instantané d’objet blob](https://msdn.microsoft.com/library/azure/hh488361.aspx)
* [Planification de votre infrastructure de sauvegarde de machines virtuelles](../backup/backup-azure-vms-introduction.md)

