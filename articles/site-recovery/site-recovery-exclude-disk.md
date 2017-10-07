---
title: "disques aaaExclude de la protection à l’aide d’Azure Site Recovery | Documents Microsoft"
description: "Explique pourquoi et comment tooexclude VM disques de la réplication pour les scénarios de tooAzure de VMware et Hyper-V tooAzure."
services: site-recovery
documentationcenter: 
author: nsoneji
manager: garavd
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2017
ms.author: nisoneji
ms.openlocfilehash: f47146bc57aeab3fce90123d0894fa86dde93417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exclude-disks-from-replication"></a>Exclure les disques de la réplication
Cet article décrit comment tooexclude disques de la réplication. Cette exclusion peut optimiser la bande passante de la réplication hello consommé ou optimiser les ressources côté cible hello qui utilisent des disques de ce type. Hello est prise en charge pour les scénarios de tooAzure de VMware et Hyper-V tooAzure.

## <a name="prerequisites"></a>Composants requis

Par défaut, tous les disques d’une machine sont répliqués. tooexclude un disque de la réplication, vous devez installer manuellement hello service mobilité sur l’ordinateur de hello avant d’activer la réplication si vous effectuez la réplication à partir de VMware tooAzure.


## <a name="why-exclude-disks-from-replication"></a>Pourquoi exclure des disques de la réplication ?
L’exclusion de disques de la réplication se révèle souvent nécessaire pour les raisons suivantes :

- données Hello sont modifiées sur le disque de hello exclu ne sont pas importantes ou n’a pas besoin de toobe répliquée.

- Souhaité toosave des ressources réseau et de stockage en ne répliquent ne pas cet évolution du code.

## <a name="what-are-hello-typical-scenarios"></a>Quels sont les scénarios classiques hello ?
Vous pouvez identifier des exemples précis de données qui sont d’excellents candidats pour l’exclusion. Par exemple écrit le fichier d’échange tooa (pagefile.sys) et fichiers de tempdb toohello de Microsoft SQL Server. En fonction de la charge de travail hello et le sous-système de stockage hello, fichier d’échange hello peut enregistrer une quantité importante d’évolution. Toutefois, la réplication des données à partir de tooAzure du site principal hello serait beaucoup de ressources. Par conséquent, vous pouvez utiliser hello après la réplication toooptimize étapes d’un ordinateur virtuel avec un disque virtuel qui possède le système d’exploitation de hello et fichier d’échange hello :

1. Fractionner disque virtuel hello en deux disques virtuels. Un disque virtuel a le système d’exploitation de hello et hello autres possède le fichier d’échange hello.
2. Exclure le disque du fichier de pagination hello de la réplication.

De même, vous pouvez utiliser les hello suivant les étapes toooptimize un disque qui possède les deux tempdb de Microsoft SQL Server hello fichier et hello du fichier de base de données système :

1. Conserver la base de données système hello et tempdb sur deux disques différents.
2. Exclure le disque de tempdb hello de la réplication.

## <a name="how-tooexclude-disks-from-replication"></a>Comment tooexclude disques de la réplication ?

### <a name="vmware-tooazure"></a>VMware tooAzure
Suivez hello [activer la réplication](site-recovery-vmware-to-azure.md) tooprotect de flux de travail une machine virtuelle à partir du portail d’Azure Site Recovery hello. Dans hello quatrième étape du flux de travail hello, utilisez hello **tooREPLICATE de disque** disques tooexclude de colonne de la réplication. Par défaut, tous les disques sont sélectionnés pour la réplication. Désactivez la case à cocher de disques que vous souhaitez tooexclude à partir de la réplication et puis exécutez hello étapes tooenable hello.

![Exclure les disques de la réplication et activer la réplication pour la restauration automatique de VMware tooAzure](./media/site-recovery-exclude-disk/v2a-enable-replication-exclude-disk1.png)


>[!NOTE]
>
> * Vous pouvez exclure uniquement les disques qui déjà hello mobilité service sont installé. Vous devez toomanually installation du service mobilité hello, hello service mobilité est uniquement installée par à l’aide du mécanisme de diffusion hello après que la réplication est activée.
> * Seuls les disques de base peuvent être exclus de la réplication. Vous ne pouvez pas exclure de système d’exploitation ni de disque dynamique.
> * Une fois la réplication activée, vous ne pouvez pas ajouter ni supprimer de disques pour la réplication. Si vous souhaitez tooadd ou excluez un disque, vous devez toodisable protection pour l’ordinateur de hello et réactivez-la.
> * Si vous excluez un disque qui est nécessaire pour une application toooperate, après le basculement tooAzure, vous devez disque de hello toocreate manuellement dans Azure afin que l’application hello répliquée permettre s’exécuter. Vous pouvez également intégrer Azure automation en un disque de récupération plan toocreate hello pendant le basculement de l’ordinateur de hello.
> * Machine virtuelle Windows : les disques que vous créez manuellement dans Azure ne sont pas restaurés automatiquement. Par exemple, si vous basculez trois disques et que vous en créez deux directement dans Azure Virtual Machines, seuls les trois disques qui ont été basculés sont restaurés automatiquement. Vous ne pouvez inclure les disques que vous avez créé manuellement dans la restauration automatique ou reprotection de local tooAzure.
> * Machine virtuelle Linux : les disques que vous créez manuellement dans Azure sont restaurés automatiquement. Par exemple, si vous basculez trois disques et créez deux disques directement dans Azure Virtual Machines, les cinq disques seront restaurés. Vous ne pouvez pas exclure de disques créés manuellement de la restauration automatique.
>

### <a name="hyper-v-tooazure"></a>Hyper-V tooAzure
Suivez hello [activer la réplication](site-recovery-hyper-v-site-to-azure.md) tooprotect de flux de travail une machine virtuelle à partir du portail d’Azure Site Recovery hello. Dans hello quatrième étape du flux de travail hello, utilisez hello **tooREPLICATE de disque** disques tooexclude de colonne de la réplication. Par défaut, tous les disques sont sélectionnés pour la réplication. Désactivez la case à cocher de disques que vous souhaitez tooexclude à partir de la réplication et puis exécutez hello étapes tooenable hello.

![Exclure les disques de la réplication et activer la réplication pour la restauration automatique de tooAzure Hyper-V](./media/site-recovery-vmm-to-azure/enable-replication6-with-exclude-disk.png)

>[!NOTE]
>
> * Seuls les disques de base peuvent être exclus de la réplication. Vous ne pouvez pas exclure les disques de système d’exploitation. Nous vous recommandons de ne pas exclure de disques dynamiques. Azure Site Recovery ne peut pas identifier le disque dur virtuel (VHD) est de base ou dynamiques dans l’ordinateur virtuel hello.  Si tous les disques de volume dynamique dépendants ne sont pas exclues, disque protégé hello devient un disque en panne sur un ordinateur virtuel de basculement et hello données sur ce disque ne sont pas accessibles.
> * Une fois la réplication activée, vous ne pouvez pas ajouter ni supprimer de disques pour la réplication. Si vous souhaitez tooadd ou excluez un disque, vous devez toodisable protection pour la machine virtuelle de hello et réactivez-la.
> * Si vous excluez un disque que nécessaire pour une application toooperate, après le basculement tooAzure vous devez disque de hello toocreate manuellement dans Azure afin que l’application hello répliquée permettre s’exécuter. Vous pouvez également intégrer Azure automation en un disque de récupération plan toocreate hello pendant le basculement de l’ordinateur de hello.
> * Les disques que vous créez manuellement dans Azure ne seront pas restaurés automatiquement. Par exemple, si vous échouer trois disques et que vous créez deux disques directement dans Azure Virtual Machines, uniquement trois disques qui ont été basculés va échouer à partir tooHyper-V Azure. Vous ne pouvez inclure des disques qui ont été créés manuellement dans la restauration automatique ou dans la réplication inverse depuis tooAzure d’Hyper-V.



## <a name="end-to-end-scenarios-of-exclude-disks"></a>Scénarios d’exclusion de disques de bout en bout
Prenons la fonctionnalité de disque deux scénarios toounderstand hello exclusion :

- Disque de base de données tempdb SQL Server
- Disque de fichier d’échange (pagefile.sys)

### <a name="exclude-hello-sql-server-tempdb-disk"></a>Exclure le disque de tempdb de SQL Server hello
Considérons l’exemple d’une machine virtuelle SQL Server dotée d’un disque de base de données tempdb pouvant être exclu.

nom de Hello du disque virtuel de hello est SalesDB.

Les disques sur un ordinateur virtuel de hello source sont les suivantes :


**Nom du disque** | **Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disque de système d’exploitation
DB-Disk1| Disk1 | D:\ | Base de données système SQL et base de données utilisateur 1
Base de données-2 (disque de hello exclus de la protection) | Disk2 | E:\ | Fichiers temporaires
Base de données-disquette n° 3 (disque de hello exclus de la protection) | Disk3 | F:\ | Base de données tempdb SQL (chemin d’accès du dossier (F:\MSSQL\Data\) < /br/>< /br/> Notez le chemin d’accès du dossier hello avant le basculement.
DB-Disk4 | Disk4 |G:\ |Base de données utilisateur 2

Étant donné que l’évolution des données sur deux disques de machine virtuelle de hello est temporaire, tout en protégeant les machines virtuelles de SalesDB hello, exclure 2 et disquette n° 3 de la réplication. Azure Site Recovery ne répliquera pas ces disques. Lors du basculement, ces disques ne sera pas présents sur l’ordinateur de virtuel basculement hello sur Azure.

Les disques sur la machine virtuelle Azure après le basculement de hello sont les suivantes :

**Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | ---
DISK0 | C:\ | Disque de système d’exploitation
Disk1 | E:\ | Stockage temporaire < /br / >< /br / > Azure ajoute ce disque et affecte la première lettre de lecteur disponible hello.
Disk2 | D:\ | Base de données système SQL et base de données utilisateur 1
Disk3 | G:\ | Base de données utilisateur 2

2 et disquette n° 3 ont été exclus de la machine virtuelle de SalesDB hello, E: étant première lettre de lecteur hello à partir de la liste des composants disponibles hello. Azure attribue un volume de stockage temporaire toohello E:. Pour tous les disques hello répliquée, lecteur hello lettres restent hello identiques.

Disquette n° 3, ce qui était hello SQL tempdb disque (chemin d’accès du dossier tempdb F:\MSSQL\Data\), a été exclu de la réplication. disque de Hello n’est pas disponible sur l’ordinateur virtuel de basculement hello. Par conséquent, hello service SQL est dans un état arrêté, et il doit le chemin d’accès de hello F:\MSSQL\Data.

Il existe deux façons toocreate ce chemin d’accès :

- Ajoutez un nouveau disque et attribuez-lui le chemin du dossier de tempdb.
- Utilisez un disque de stockage temporaire existant pour le chemin d’accès au dossier hello tempdb.

#### <a name="add-a-new-disk"></a>Ajouter un nouveau disque :

1. Notez les chemins d’accès hello de SQL tempdb.mdf et tempdb.ldf avant le basculement.
2. À partir de hello portail Azure, ajouter une disque toohello basculement machine virtuelle avec hello même ou à une taille plus que celle du disque de tempdb SQL hello source (disquette n° 3).
3. Se connecter toohello machine virtuelle Azure. À partir de la console de gestion (diskmgmt.msc) du disque hello, d’initialisation et de format hello récemment ajouté de disque.
4. Hello Assign même lettre qui était utilisé par un disque de tempdb SQL hello (F:) de lecteur.
5. Créez un dossier de tempdb sur hello le volume F: (F:\MSSQL\Data).
6. Démarrer le service SQL de hello à partir de la console de service hello.

#### <a name="use-an-existing-temporary-storage-disk-for-hello-sql-tempdb-folder-path"></a>Utilisez un disque de stockage temporaire existant pour le chemin d’accès du dossier hello SQL tempdb :

1. Ouvrez une invite de commandes.
2. Exécutez SQL Server en mode de récupération à partir de l’invite de commandes hello.

        Net start MSSQLSERVER /f / T3608

3. Exécutez hello suivant sqlcmd toochange hello tempdb toohello nouveau chemin.

        sqlcmd -A -S SalesDB        **Use your SQL DBname**
        USE master;     
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = tempdev, FILENAME = 'E:\MSSQL\tempdata\tempdb.mdf');
        GO      
        ALTER DATABASE tempdb       
        MODIFY FILE (NAME = templog, FILENAME = 'E:\MSSQL\tempdata\templog.ldf');       
        GO


4. Arrêter le service de Microsoft SQL Server hello.

        Net stop MSSQLSERVER
5. Démarrer le service de Microsoft SQL Server hello.

        Net start MSSQLSERVER

Consultez toohello suivant les indications de Azure pour le disque de stockage temporaire :

* [À l’aide de disques SSD dans les machines virtuelles Azure toostore TempDB de SQL Server et les Extensions du Pool de mémoires tampons](https://blogs.technet.microsoft.com/dataplatforminsider/2014/09/25/using-ssds-in-azure-vms-to-store-sql-server-tempdb-and-buffer-pool-extensions/)
* [Meilleures pratiques relatives aux performances de SQL Server dans les machines virtuelles Azure](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-performance)

### <a name="failback-from-azure-tooan-on-premises-host"></a>Restauration automatique (à partir de l’hôte local de tooan Azure)
Maintenant essayons de comprendre les disques hello qui sont répliqués lorsque vous basculez de l’hôte de VMware ou Hyper-V du local tooyour Azure. Les disques que vous créez manuellement dans Azure ne seront pas répliqués. Par exemple, si vous basculez trois disques et que vous en créez deux directement dans Azure Virtual Machines, seuls les trois disques qui ont été basculés seront restaurés automatiquement. Vous ne pouvez inclure des disques qui ont été créés manuellement dans la restauration automatique ou reprotection de local tooAzure. Aussi, il ne réplique pas hôtes de tooon local de disque de stockage temporaire hello.

#### <a name="failback-toooriginal-location-recovery"></a>Récupération de la restauration automatique toooriginal emplacement

Dans l’exemple précédent de hello, configuration de disque de machine virtuelle Azure hello est comme suit :

**Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | ---
DISK0 | C:\ | Disque de système d’exploitation
Disk1 | E:\ | Stockage temporaire < /br / >< /br / > Azure ajoute ce disque et affecte la première lettre de lecteur disponible hello.
Disk2 | D:\ | Base de données système SQL et base de données utilisateur 1
Disk3 | G:\ | Base de données utilisateur 2


#### <a name="vmware-tooazure"></a>VMware tooAzure
Une fois la restauration automatique terminée emplacement d’origine de toohello, configuration de disque de machine virtuelle de la restauration automatique hello n’a pas de disques exclus. Les disques qui ont été exclus de VMware tooAzure ne seront pas disponibles sur l’ordinateur virtuel de la restauration automatique hello.

Après un basculement planifié à partir de Azure local tooon VMware, les disques de machine virtuelle de VMWare hello (emplacement d’origine) sont les suivantes :

**Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | ---
DISK0 | C:\ | Disque de système d’exploitation
Disk1 | D:\ | Base de données système SQL et base de données utilisateur 1
Disk2 | G:\ | Base de données utilisateur 2

#### <a name="hyper-v-tooazure"></a>Hyper-V tooAzure
Lorsque la restauration automatique est l’emplacement d’origine de toohello, hello la restauration automatique machine virtuelle disque configuration reste hello même que celui de la configuration de disque de machine virtuelle d’origine pour Hyper-V. Les disques qui ont été exclus de tooAzure du site Hyper-V sont disponibles sur l’ordinateur virtuel de la restauration automatique hello.

Après un basculement planifié à partir du site tooon Azure Hyper-V, les disques sur l’ordinateur virtuel de Hyper-V hello (emplacement d’origine) sont les suivantes :

**Nom du disque** | **Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 |   C:\ | Disque de système d’exploitation
DB-Disk1 | Disk1 | D:\ | Base de données système SQL et base de données utilisateur 1
DB-Disk2 (disque exclu) | Disk2 | E:\ | Fichiers temporaires
DB-Disk3 (disque exclu) | Disk3 | F:\ | Base de données tempdb SQL (chemin du dossier (F:\MSSQL\Data\)
DB-Disk4 | Disk4 | G:\ | Base de données utilisateur 2


#### <a name="exclude-hello-paging-file-pagefilesys-disk"></a>Exclure le disque du fichier (pagefile.sys) hello la pagination

Considérons l’exemple d’une machine virtuelle dotée d’un disque de fichier d’échange pouvant être exclu.
Il existe deux cas.

#### <a name="case-1-hello-paging-file-is-configured-on-hello-d-drive"></a>Cas n° 1 : fichier d’échange hello est configuré sur hello lecteur D:
Voici la configuration de disque hello :


**Nom du disque** | **Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disque de système d’exploitation
(Disque de hello exclus de la protection de hello) de base de données-disque 1 | Disk1 | D:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Données utilisateur 1
DB-Disk3 | Disk3 | F:\ | Données utilisateur 2

Voici les paramètres fichier d’échange hello sur l’ordinateur virtuel de hello source :

![Paramètres du fichier d’échange sur la machine virtuelle source](./media/site-recovery-exclude-disk/pagefile-on-d-drive-sourceVM.png)


Après le basculement de l’ordinateur virtuel hello VMware tooAzure ou tooAzure de Hyper-V, les disques sur hello machine virtuelle Azure sont les suivantes :

**Nom du disque** | **Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disque de système d’exploitation
DB-Disk1 | Disk1 | D:\ | Stockage temporaire</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Données utilisateur 1
DB-Disk3 | Disk3 | F:\ | Données utilisateur 2

Étant donné que le disque 1 (d) a été exclue, D: est première lettre de lecteur hello à partir de la liste des composants disponibles hello. Azure attribue un volume de stockage temporaire toohello D:. D: étant disponible sur hello machine virtuelle Azure, le paramètre fichier d’échange hello de hello machine virtuelle reste hello même.

Voici les paramètres fichier d’échange hello sur hello machine virtuelle Azure :

![Paramètres du fichier d’échange sur la machine virtuelle Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover.png)

#### <a name="case-2-hello-paging-file-is-configured-on-another-drive-other-than-d-drive"></a>Cas 2 : le fichier d’échange hello est configuré sur un autre lecteur (autre que le lecteur D:)

Voici la configuration de disque de machine virtuelle source hello :

**Nom du disque** | **Numéro du disque du système d’exploitation invité** | **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0 | C:\ | Disque de système d’exploitation
Base de données-disque 1 (disque de hello exclus de la protection) | Disk1 | G:\ | pagefile.sys
DB-Disk2 | Disk2 | E:\ | Données utilisateur 1
DB-Disk3 | Disk3 | F:\ | Données utilisateur 2

Voici les paramètres fichier d’échange hello sur l’ordinateur virtuel de local hello :

![Paramètres du fichier sur l’ordinateur virtuel de local hello d’échange](./media/site-recovery-exclude-disk/pagefile-on-g-drive-sourceVM.png)

Après le basculement de l’ordinateur virtuel VMware/Hyper-V tooAzure hello, les disques sur hello machine virtuelle Azure sont les suivantes :

**Nom du disque**| **Numéro du disque du système d’exploitation invité**| **Lettre de lecteur** | **Type de données sur le disque de hello**
--- | --- | --- | ---
DB-Disk0-OS | DISK0  |C:\ |Disque de système d’exploitation
DB-Disk1 | Disk1 | D:\ | Stockage temporaire</br /> </br />pagefile.sys
DB-Disk2 | Disk2 | E:\ | Données utilisateur 1
DB-Disk3 | Disk3 | F:\ | Données utilisateur 2

D: étant la première lettre de lecteur hello à partir de la liste de hello disponibles, Azure affecte d : volume de stockage temporaire toohello. Pour tous les disques hello répliquée, le reste de lettre de lecteur hello hello même. Étant donné que hello G: disque n’est pas disponible, hello système utilise lecteur C: de hello pour le fichier d’échange de hello.

Voici les paramètres fichier d’échange hello sur hello machine virtuelle Azure :

![Paramètres du fichier d’échange sur la machine virtuelle Azure](./media/site-recovery-exclude-disk/pagefile-on-Azure-vm-after-failover-2.png)

## <a name="next-steps"></a>Étapes suivantes
Une fois votre déploiement configuré et effectué, pour en savoir plus sur les différents types de basculement, [cliquez ici](site-recovery-failover.md) .
