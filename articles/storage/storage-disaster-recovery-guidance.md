---
title: "toodo aaaWhat dans les cas de hello d’une panne de stockage Azure | Documents Microsoft"
description: "Le toodo dans les cas de hello d’une panne de stockage Azure"
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 8f040b0f-8926-4831-ac07-79f646f31926
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 1/19/2017
ms.author: robinsh
ms.openlocfilehash: ee7eb71311c6e453dc078ec3566267ee0c2f444a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-toodo-if-an-azure-storage-outage-occurs"></a>Le toodo en cas de panne de stockage Azure
Chez Microsoft, nous travaillons dur toomake que nos services sont toujours disponibles. Il arrive parfois que des phénomènes incontrôlables entraînent des interruptions de service non planifiés dans une ou plusieurs régions. toohelp vous gérez ces occurrences rares, nous fournissons hello suivant des instructions détaillées pour les services de stockage Azure.

## <a name="how-tooprepare"></a>Comment tooprepare
Il est essentiel pour chaque client tooprepare leur propre plan de récupération d’urgence. toorecover d’effort Hello à partir d’un compte de stockage implique généralement personnel des opérations et des procédures automatiques dans l’ordre tooreactivate vos applications dans un état de fonctionnement. Consultez toohello documentation sur Azure ci-dessous toobuild votre propre plan de récupération d’urgence :

* [Récupération d’urgence et haute disponibilité pour les applications Azure](../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md)
* [Guide technique de la résilience Azure](../resiliency/resiliency-technical-guidance.md)
* [Service Azure Site Recovery](https://azure.microsoft.com/services/site-recovery/)
* [Réplication Azure Storage](storage-redundancy.md)
* [Service Azure Backup](https://azure.microsoft.com/services/backup/)

## <a name="how-toodetect"></a>Comment toodetect
Hello recommandé hello toodetermine de façon l’état du service Azure est toosubscribe toohello [tableau de bord d’intégrité de Service Azure](https://azure.microsoft.com/status/).

## <a name="what-toodo-if-a-storage-outage-occurs"></a>Quelles toodo si une panne de stockage se produit.
Si un ou plusieurs services de stockage sont temporairement indisponibles à une ou plusieurs régions, il existe deux options pour vous tooconsider. Si vous le souhaitez données de tooyour un accès immédiat, envisagez l’Option 2.

### <a name="option-1-wait-for-recovery"></a>Option 1: attente de récupération
Dans ce cas, aucune action n’est requise de votre part. Nous travaillons soigneusement disponibilité du service Azure toorestore hello. Vous pouvez surveiller le statut de service hello sur hello [tableau de bord d’intégrité de Service Azure](https://azure.microsoft.com/status/).

### <a name="option-2-copy-data-from-secondary"></a>Option 2: copie de données à partir de la base de données secondaire
Si vous avez choisi [stockage géo-redondant d’accès en lecture (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (recommandé) pour vos comptes de stockage, vous aurez accès en lecture tooyour données à partir de la région secondaire hello. Vous pouvez utiliser des outils tels que [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md)et hello [bibliothèque de déplacement de données Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/) toocopy des données à partir de la région secondaire de hello dans un autre compte de stockage une région unimpacted et pointez votre stockage de toothat applications compte de lecture et d’écriture de disponibilité.

## <a name="what-tooexpect-if-a-storage-failover-occurs"></a>Quelles tooexpect si un basculement de stockage
Si vous avez choisi le [stockage géo-redondant (GRS)](storage-redundancy.md#geo-redundant-storage) ou le [stockage géo-redondant avec accès en lecture (RA-GRS)](storage-redundancy.md#read-access-geo-redundant-storage) (recommandé), Azure Storage conservera vos données dans deux régions (primaire et secondaire). Azure Storage conserve constamment plusieurs réplicas de vos données dans les deux régions.

Lorsqu’un sinistre régional affecte votre région primaire, nous essaierons tout d’abord service de hello toorestore dans cette région. Dépend de la nature de hello de reprise après sinistre hello et son impact, dans certains cas rares nous ne soyons pas région principale de toorestore en mesure de hello. À ce stade, nous procéderons à un basculement géographique. la réplication entre régions données Hello est un processus asynchrone qui peut impliquer un certain délai, il est donc possible que les modifications qui n’ont pas encore été répliquées toohello la région secondaire peuvent être perdu. Vous pouvez interroger hello [« Dernière heure de synchronisation » de votre compte de stockage](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/) tooget plus d’informations sur l’état de réplication hello.

Quelques points concernant l’expérience de basculement géographique de stockage hello :

* Basculement géographique de stockage sont déclenché par l’équipe du stockage Azure hello : il n’existe aucune action de client nécessaire.
* Votre service de stockage de points de terminaison pour les objets BLOB, les tables, les files d’attente et les fichiers restent hello même après le basculement de hello ; Hello entrée DNS devez tooswitch toobe mis à jour à partir de la région de hello région principale toohello secondaire.
* Avant et pendant le basculement géographique hello, vous n’avez pas accès en écriture compte de stockage tooyour en raison de l’impact de toohello de reprise après sinistre hello, mais vous pouvez toujours lire à partir de hello secondaire si votre compte de stockage a été configuré comme RA-GRS.
* Lorsque hello basculement géographique a été effectué et hello modifications DNS propagées, accès en lecture et écriture compte de stockage tooyour reprendra ; Ce paramètre pointe toowhat utilisé toobe votre point de terminaison secondaire. 
* Notez que vous aura un accès en écriture si vous avez GRS ou RA-GRS configuré pour le compte de stockage hello. 
* Vous pouvez interroger [« Temps de basculement géographique dernier » de votre compte de stockage](https://msdn.microsoft.com/library/azure/ee460802.aspx) tooget plus en détail.
* Après le basculement de hello, votre compte de stockage entièrement fonctionnera, mais dans un état « détérioré », tel qu’il est réellement hébergé dans une région autonome avec aucune possible géo-réplication. toomitigate ce risque, nous allons restaurer la région principale d’origine de hello, puis effectuez l’une géo-restauration automatique toorestore hello présents. Si la région principale d’origine de hello est irrécupérable, nous alloue une autre région secondaire.
  Pour plus d’informations sur l’infrastructure hello de la réplication géo-réplication de stockage Azure, consultez toohello article de blog de l’équipe stockage hello sur [Options de redondance et RA-GRS](https://blogs.msdn.microsoft.com/windowsazurestorage/2013/12/11/windows-azure-storage-redundancy-options-and-read-access-geo-redundant-storage/).

## <a name="best-practices-for-protecting-your-data"></a>Meilleures pratiques pour la protection de vos données
Il existe certains tooback les approches recommandées des données de votre stockage sur une base régulière.

* Disques de machine virtuelle : hello d’utilisation [service Azure Backup](https://azure.microsoft.com/services/backup/) tooback des disques de machine virtuelle hello utilisée par vos machines virtuelles Azure.
* Objets BLOB de blocs : créer un [instantané](https://msdn.microsoft.com/library/azure/hh488361.aspx) de chaque objet blob de bloc, ou copier un compte de stockage tooanother hello objets BLOB à l’aide d’une autre région [AzCopy](storage-use-azcopy.md), [Azure PowerShell](storage-powershell-guide-full.md), ou hello [ Bibliothèque de déplacement des données Azure](https://azure.microsoft.com/blog/introducing-azure-storage-data-movement-library-preview-2/).
* Utiliser des tables – [AzCopy](storage-use-azcopy.md) tooexport données de la table hello dans un autre compte de stockage dans une autre région.
* Utiliser des fichiers – [AzCopy](storage-use-azcopy.md) ou [Azure PowerShell](storage-powershell-guide-full.md) toocopy du compte de votre stockage de tooanother de fichiers dans une autre région.

Pour plus d’informations sur la création d’applications qui tirent parti de la fonctionnalité de hello RA-GRS, extrayez [conception hautement disponible d’Applications à l’aide du stockage de RA-GRS](storage-designing-ha-apps-with-ragrs.md)

