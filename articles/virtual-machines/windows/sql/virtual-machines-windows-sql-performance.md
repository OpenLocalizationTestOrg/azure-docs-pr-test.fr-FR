---
title: aaaPerformance les meilleures pratiques pour SQL Server dans Azure | Documents Microsoft
description: "Présente les meilleures pratiques pour optimiser les performances de SQL Server dans Microsoft Azure Virtual Machines."
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a0c85092-2113-4982-b73a-4e80160bac36
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 06/27/2017
ms.author: jroth
ms.openlocfilehash: 42ec9fbeb2dec3a654b93bbd08d666369835ee73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-best-practices-for-sql-server-in-azure-virtual-machines"></a>Meilleures pratiques relatives aux performances de SQL Server dans les machines virtuelles Azure

## <a name="overview"></a>Vue d'ensemble

Cette rubrique présente les meilleures pratiques pour optimiser les performances de SQL Server dans la machine virtuelle Microsoft Azure. Lors de l’exécution de SQL Server dans des Machines virtuelles Azure, nous vous conseillons de continuer à l’aide de hello des performances de base de données même paramétrage des options qui sont applicable tooSQL Server dans un environnement de serveur local. Toutefois, les performances de hello de base de données relationnelle dans un cloud public dépendent de nombreux facteurs, telles que la taille d’une machine virtuelle, configuration hello hello de disques de données hello.

Lors de la création d’images de SQL Server, [prendre en compte la configuration de vos machines virtuelles dans le portail Azure de hello](virtual-machines-windows-portal-sql-server-provision.md). Machines virtuelles SQL Server configuré dans hello portail avec le Gestionnaire de ressources implémente toutes ces meilleures pratiques, y compris la configuration de stockage hello.

Cet article se concentre sur l’obtention de hello *meilleures* performances pour SQL Server sur des machines virtuelles Azure. Si votre charge de travail est moindre, vous n’aurez peut-être pas besoin de toutes les optimisations suivantes. Tenez compte de vos besoins de performances et de vos modèles de charges de travail lors de l’évaluation de ces recommandations.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="quick-check-list"></a>Liste de vérification rapide

Hello Voici une liste de vérification rapide pour optimiser les performances de SQL Server sur des Machines virtuelles Azure :

| Domaine | Optimisations |
| --- | --- |
| [Taille de la machine virtuelle](#vm-size-guidance) |[Édition SQL Enterprise DS3](../../virtual-machines-windows-sizes-memory.md) ou supérieure.<br/><br/>[DS2](../../virtual-machines-windows-sizes-memory.md) ou supérieure pour SQL Server Standard Edition ou SQL Server Web Edition. |
| [Stockage](#storage-guidance) |Utiliser [Premium Storage](../../../storage/common/storage-premium-storage.md). Le stockage standard n’est recommandé que pour le développement et le test.<br/><br/>Conserver hello [compte de stockage](../../../storage/common/storage-create-storage-account.md) et la machine virtuelle SQL Server dans hello même région.<br/><br/>Désactiver Azure [stockage géo-redondant](../../../storage/common/storage-redundancy.md) (géo-réplication) sur le compte de stockage hello. |
| [Disques](#disks-guidance) |Utilisez au moins 2 [disques P30](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) (1 pour les fichiers journaux ; 1 pour les fichiers de données et TempDB).<br/><br/>Éviter d’utiliser des disques de système d’exploitation ou temporaires pour le stockage ou la journalisation des bases de données.<br/><br/>Activer le cache de lecture des disques hello hébergeant les fichiers de données hello et TempDB.<br/><br/>N’activez pas la mise en cache sur les disques qui héberge le fichier journal de hello.<br/><br/>Important : Arrêter le service SQL Server de hello lors de la modification des paramètres de cache de hello pour un disque de machine virtuelle Azure.<br/><br/>Distribuez le débit d’e/s tooget augmenté à des disques Azure données plusieurs.<br/><br/>Formatez avec des tailles d’allocation documentées. |
| [E/S](#io-guidance) |Activez la compression des pages de base de données.<br/><br/>Activer l’initialisation de fichiers instantanée pour les fichiers de données.<br/><br/>Limiter ou désactiver la croissance automatique sur la base de données hello.<br/><br/>Désactiver la réduction automatique sur la base de données hello.<br/><br/>Déplacer tous les disques toodata de bases de données, y compris les bases de données système.<br/><br/>Déplacez SQL Server erreur suivi et journaux fichier répertoires toodata disques.<br/><br/>Configurez les emplacements par défaut du fichier de sauvegarde et du fichier de base de données.<br/><br/>Activer les pages verrouillées.<br/><br/>Appliquez les correctifs de performances de SQL Server. |
| [Fonctionnalités spécifiques](#feature-specific-guidance) |Sauvegarder directement tooblob stockage. |

Pour plus d’informations sur *comment* et *pourquoi* toomake ces optimisations, passez en revue les détails de hello et les instructions fournies dans les sections suivantes.

## <a name="vm-size-guidance"></a>Conseils liés à la taille des machines virtuelles

Pour les applications sensibles aux performances, il est recommandé d’utiliser suivant de hello [tailles de machines virtuelles](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json):

* **SQL Server Enterprise Edition**: DS3 ou supérieure
* **SQL Server Standard Edition ou SQL Server Web Edition**: DS2 ou supérieure

## <a name="storage-guidance"></a>Conseils liés au stockage

Les machines virtuelles de série DS (ainsi que des séries DSv2 et GS) prennent en charge le [stockage Premium](../../../storage/common/storage-premium-storage.md). L’option Premium Storage est recommandée pour toutes les charges de travail de production.

> [!WARNING]
> L’option Standard Storage possède différents temps de latence et une bande passante variable. Elle est recommandée uniquement pour les charges de travail de développement/de test. Les charges de production doivent utiliser Premium Storage.

En outre, nous vous recommandons de créer votre compte de stockage Azure Bonjour même centre de données que vos délais de transfert tooreduce des machines virtuelles SQL Server. Lors de la création d’un compte de stockage, désactivez la géo-réplication, étant donné que la cohérence de l’ordre d’écriture sur différents disques n’est pas garantie. Envisagez plutôt de configurer une technologie de récupération d’urgence de SQL Server entre deux centres de données Azure. Pour plus d’informations, consultez [Haute disponibilité et récupération d’urgence pour SQL Server dans Azure Virtual Machines](virtual-machines-windows-sql-high-availability-dr.md).

## <a name="disks-guidance"></a>Conseils liés aux disques

Il existe trois types de disques principaux sur une machine virtuelle Azure :

* **Disque de système d’exploitation**: lorsque vous créez une Machine virtuelle Azure, la plateforme de hello attachera au moins un disque (appelé hello **C** lecteur) toohello machine virtuelle pour le disque du système d’exploitation. Ce disque est un disque dur virtuel (VHD) stocké en tant qu’objet blob de pages dans le stockage.
* **Disque temporaire**: les Machines virtuelles Azure contiennent un autre disque appelé disque temporaire de hello (étiquetés comme hello **D**: lecteur). Il s’agit d’un disque sur le nœud hello qui peut être utilisé pour l’espace de travail.
* **Disques de données**: vous pouvez également attacher des disques supplémentaires tooyour virtual machine en tant que disques de données, et ces seront stockées dans le stockage en tant qu’objets BLOB de pages.

Hello sections suivantes décrivent des recommandations pour l’utilisation de ces différents disques.

### <a name="operating-system-disk"></a>Disque de système d’exploitation

Un disque de système d’exploitation est un disque dur virtuel (VHD) que vous pouvez amorcer et monter comme version d’exécution d’un système d’exploitation. Il est désigné par la lettre de lecteur **C**.

Valeur par défaut de la mise en cache de la stratégie sur le disque du système d’exploitation hello est **en lecture/écriture**. Pour les applications sensibles aux performances, nous vous recommandons d’utiliser des disques de données au lieu de disque de système d’exploitation hello. Consultez la section de hello sur des disques de données ci-dessous.

### <a name="temporary-disk"></a>Disque temporaire

Hello disque temporaire, désigné comme hello **D**: disque, n’est pas persistante tooAzure stockage d’objets blob. Ne stockez pas vos fichiers de base de données utilisateur ou les fichiers journaux des transactions utilisateur sur hello **D**: lecteur.

Pour la série D, série Dv2 et machines virtuelles de série G, lecteur temporaire de hello sur ces ordinateurs virtuels est basé sur le disque SSD. Si votre charge de travail utilise de façon intensive TempDB (par exemple, pour les objets temporaires ou des jointures complexes), le stockage de TempDB sur hello **D** lecteur peut entraîner un débit plus élevé TempDB et diminuer la latence de TempDB.

Pour les machines virtuelles qui prennent en charge le stockage Premium (de série DS, DSv2 et GS), nous vous recommandons de stocker TempDB sur un disque qui prend en charge le stockage Premium avec la mise en cache en lecture activée. Il existe une recommandation de toothis exception ; Si votre utilisation de TempDB est gourmandes en écriture, vous pouvez obtenir les meilleures performances en stockant TempDB hello local **D** lecteur, qui est également basée sur SSD sur ces tailles de machine.

### <a name="data-disks"></a>Disques de données

* **Utiliser des disques de données pour les données et fichiers journaux**: au minimum, utilisez 2 stockage Premium [P30 disques](../../../storage/common/storage-premium-storage.md#scalability-and-performance-targets) où un seul disque contient l’ou les fichiers journaux hello et hello autres contient les données de salutation et les fichiers de TempDB. Chaque disque de stockage Premium fournit un nombre d’IOPs et de bande passante (Mo/s) en fonction de sa taille, comme décrit dans l’article suivant de hello : [à l’aide de stockage Premium pour les disques](../../../storage/common/storage-premium-storage.md).

* **Entrelacement de disques**: pour augmenter le débit, vous pouvez ajouter des disques de données supplémentaires et utiliser l’entrelacement de disques. nombre de hello toodetermine de disques de données, vous devez tooanalyze hello d’e/s et de bande passante requise pour vos fichiers journaux et de vos données et les fichiers de TempDB. Notez que les différentes tailles de machine virtuelle ont des limites différentes sur nombre hello IOPs et bande passante de la prise en charge, consultez les tableaux de hello sur les e/s par [taille de machine virtuelle](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Utilisez hello instructions :

  * Pour Windows 8 et Windows Server 2012 ou version ultérieure, utilisez [des espaces de stockage](https://technet.microsoft.com/library/hh831739.aspx) par hello instructions :

      1. Ensemble hello entrelacer (taille de bande) too64 Ko (65 536 octets) pour les charges de travail OLTP et 256 Ko (262 144 octets) pour l’impact sur les performances des charges de travail tooavoid en raison d’un mauvais alignement toopartition d’entreposage de données. Ces paramètres doivent être définis avec PowerShell.
      1. Nombre de colonnes définies = nombre de disques physiques. Utilisez PowerShell lorsque vous configurez plus de 8 disques (et non l’interface utilisateur du gestionnaire de serveur). 

    Par exemple, hello suivant PowerShell crée un pool de stockage avec hello entrelacer taille too64 Ko et hello le nombre de colonnes too2 :

    ```powershell
    $PoolCount = Get-PhysicalDisk -CanPool $True
    $PhysicalDisks = Get-PhysicalDisk | Where-Object {$_.FriendlyName -like "*2" -or $_.FriendlyName -like "*3"}

    New-StoragePool -FriendlyName "DataFiles" -StorageSubsystemFriendlyName "Storage Spaces*" -PhysicalDisks $PhysicalDisks | New-VirtualDisk -FriendlyName "DataFiles" -Interleave 65536 -NumberOfColumns 2 -ResiliencySettingName simple –UseMaximumSize |Initialize-Disk -PartitionStyle GPT -PassThru |New-Partition -AssignDriveLetter -UseMaximumSize |Format-Volume -FileSystem NTFS -NewFileSystemLabel "DataDisks" -AllocationUnitSize 65536 -Confirm:$false 
    ```

  * Pour Windows 2008 R2 ou version antérieure, vous pouvez utiliser des disques dynamiques (volumes du système d’exploitation agrégés par bandes) et taille de bande hello est toujours de 64 Ko. Remarque : cette option est déconseillée à partir des versions Windows 8/Windows Server 2012. Pour plus d’informations, consultez déclaration de prise en charge hello [Service de disque virtuel est en transition tooWindows API de gestion de stockage](https://msdn.microsoft.com/library/windows/desktop/hh848071.aspx).

  * Si votre charge de travail ne génère pas intensivement de journaux et ne nécessite pas d’opérations d’E/S par seconde dédiées, vous pouvez configurer un seul pool de stockage. Sinon, créez deux pools de stockage, un pour l’ou les fichiers journaux hello et un autre pool de stockage pour les fichiers de données hello et TempDB. Déterminer le nombre de hello de disques associés à chaque pool de stockage en fonction de vos attentes en matière de charge. N’oubliez pas que les différentes tailles de machines virtuelles autorisent différents nombres de disques de données attachés. Pour plus d’informations, consultez [Tailles des machines virtuelles](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

  * Si vous n’utilisez pas le stockage Premium (scénarios de développement/test), hello est recommandé de nombre maximal de hello tooadd de disques de données pris en charge par votre [taille de machine virtuelle](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et utiliser l’agrégation de disques.

* **Stratégie de mise en cache**: les disques de données pour le stockage Premium, activer le cache de lecture sur les disques de données hello d’hébergement seulement vos fichiers de données et de TempDB. Si vous n’utilisez pas Premium Storage, n’activez aucune mise en cache sur les disques de données. Pour obtenir des instructions sur la configuration de la mise en cache du disque, consultez hello rubriques suivantes : [Set-AzureOSDisk](https://msdn.microsoft.com/library/azure/jj152847) et [Set-AzureDataDisk](https://msdn.microsoft.com/library/azure/jj152851.aspx).

  > [!WARNING]
  > Arrêter le service SQL Server de hello lorsque vous modifiez le paramètre de cache hello Azure VM disques tooavoid hello risque en tête une altération de la base de données.

* **Taille d’unité d’allocation NTFS**: lors du formatage de disque de données hello, il est recommandé d’utiliser une taille d’unité d’allocation de 64 Ko pour les données et fichiers journaux ainsi que de TempDB.

* **Meilleures pratiques de gestion de disque**: lors de la suppression d’un disque de données ou la modification de son cache de type, arrêtez le service de SQL Server de hello pendant la modification de hello. Lorsque les paramètres de mise en cache de hello sont modifiées sur le disque du système d’exploitation de hello, Azure arrête hello machine virtuelle, modifie le type de cache hello et redémarre hello machine virtuelle. Lorsque les paramètres de cache hello d’un disque de données sont modifiées, hello VM n’est pas arrêtée, mais disque de données hello est détaché hello VM pendant hello modifier et puis rattachée.

  > [!WARNING]
  > Hello toostop de défaillance du service SQL Server pendant ces opérations peut endommager la base de données.

## <a name="io-guidance"></a>Recommandations liées aux E/S

* Hello meilleurs résultats avec stockage Premium sont obtenus quand vous parallélisez votre application et les demandes. Stockage Premium est conçu pour les scénarios où la profondeur de file d’attente d’e/s hello est supérieur à 1, voir peu ou pas des gains de performances pour les demandes de série monothread (même si elles sont beaucoup de stockage). Par exemple, cela peut affecter les résultats du test de monothread hello des outils d’analyse de performances, telles que SQLIO.

* Envisagez d’utiliser un [compression des pages de base de données](https://msdn.microsoft.com/library/cc280449.aspx) , car elle peut améliorer les performances de charges de travail gourmandes en E/S. Toutefois, la compression des données hello peut augmenter la consommation de processeur hello sur le serveur de base de données hello.

* Envisagez d’activer la durée de hello du tooreduce d’initialisation instantanée des fichiers requis pour l’allocation de fichier initial. tootake parti de l’initialisation instantanée des fichiers, vous accordez hello compte de service SQL Server (MSSQLSERVER) avec l’autorisation SE_MANAGE_VOLUME_NAME et l’ajouter toohello **effectuer des tâches de Maintenance de Volume** stratégie de sécurité. Si vous utilisez une image de plateforme SQL Server pour Azure, compte de service par défaut hello (NT Service\MSSQLSERVER) n’est pas ajouté toohello **effectuer des tâches de Maintenance de Volume** stratégie de sécurité. En d’autres termes, l’initialisation instantanée des fichiers n’est pas activée dans une image de plateforme SQL Server pour Azure. Après l’ajout de toohello de compte de service de SQL Server hello **effectuer des tâches de Maintenance de Volume** stratégie de sécurité, redémarrez le service SQL Server hello. Des considérations de sécurité liées à l’utilisation de cette fonctionnalité peuvent exister. Pour plus d’informations, consultez [Initialisation des fichiers de base de données](https://msdn.microsoft.com/library/ms175935.aspx).

* **croissance automatique** est considéré comme toobe simplement une éventualité de croissance. Ne gérez pas la croissance de vos données et journaux quotidiennement avec la croissance automatique. Si la croissance automatique est utilisée, augmentez préalablement le fichier hello à l’aide du commutateur taille hello.

* Assurez-vous que **autoshrink** est justifié tooavoid désactivé qui peut nuire aux performances.

* Déplacer tous les disques toodata de bases de données, y compris les bases de données système. Pour plus d’informations, consultez [Déplacer des bases de données système](https://msdn.microsoft.com/library/ms345408.aspx).

* Déplacez SQL Server erreur suivi et journaux fichier répertoires toodata disques. Cette opération peut être effectuée dans le Gestionnaire de configuration SQL Server en double-cliquant sur l’instance de SQL Server et en sélectionnant des propriétés. Hello erreur suivi et journaux fichier paramètres peuvent être modifiés dans hello **paramètres de démarrage** hello onglet répertoire de vidage est spécifié dans hello **avancé** hello onglet suivant capture d’écran montre en quoi toolook pour paramètre de démarrage du journal d’erreur de Hello.

    ![Capture d’écran du journal des erreurs SQL](./media/virtual-machines-windows-sql-performance/sql_server_error_log_location.png)

* Configurez les emplacements par défaut du fichier de sauvegarde et du fichier de base de données. Utilisez les recommandations hello dans cette rubrique, puis apportez des modifications de hello dans la fenêtre de propriétés de serveur hello. Pour obtenir des instructions, consultez [hello afficher ou modifier les emplacements par défaut pour les données et les fichiers de journaux (SQL Server Management Studio)](https://msdn.microsoft.com/library/dd206993.aspx). Hello capture d’écran suivante montre où toomake ces modifications.

    ![Journal des données et fichiers de sauvegarde SQL](./media/virtual-machines-windows-sql-performance/sql_server_default_data_log_backup_locations.png)
* Activer verrouillée pages tooreduce e/s et toutes les activités de la pagination. Pour plus d’informations, consultez [activer hello Lock Pages in Memory (Option) (Windows)](https://msdn.microsoft.com/library/ms190730.aspx).

* Si vous exécutez SQL Server 2012, installez la mise à jour cumulative 10 Service Pack 1. Cette mise à jour contient correctif hello pour des performances d’e/s médiocres lorsque vous exécutez une sélection dans une instruction de table temporaire dans SQL Server 2012. Pour plus d’informations, consultez cet [article de la Base de connaissances](http://support.microsoft.com/kb/2958012).

* Envisagez de compresser tous les fichiers de données lors des transferts vers et depuis Azure.

## <a name="feature-specific-guidance"></a>Recommandations liées aux fonctionnalités spécifiques

Certains déploiements peuvent bénéficier de plus grands avantages en termes de performances à l’aide de techniques de configuration avancées. Hello liste suivante présente certaines fonctionnalités de SQL Server qui peuvent vous aider à améliorer les performances tooachieve :

* **Les sauvegardes tooAzure**: lorsque vous effectuez des sauvegardes pour SQL Server s’exécutant dans des machines virtuelles, vous pouvez utiliser [tooURL de sauvegarde SQL Server](https://msdn.microsoft.com/library/dn435916.aspx). Cette fonctionnalité est disponible à partir de SQL Server 2012 SP1 CU2 et recommandée pour la sauvegarde des disques de données toohello attaché. Lorsque vous sauvegarde/restauration vers/depuis le stockage Azure, suivez les recommandations de hello fournies au [meilleures pratiques de sauvegarde de SQL Server tooURL et de résolution des problèmes et de restauration à partir de sauvegardes stockées dans le stockage Azure](https://msdn.microsoft.com/library/jj919149.aspx). Vous pouvez également automatiser ces sauvegardes en utilisant la [Sauvegarde automatisée pour SQL Server dans les machines virtuelles Azure](virtual-machines-windows-sql-automated-backup.md).

    TooSQL préalable Server 2012, vous pouvez utiliser [tooAzure de sauvegarde SQL Server outil](https://www.microsoft.com/download/details.aspx?id=40740). Cet outil peut aider le débit de sauvegarde tooincrease à l’aide de plusieurs cibles de la bande de sauvegarde.

* **Fichiers de données SQL Server dans Azure**: cette nouvelle fonctionnalité, nommée [Fichiers de données SQL Server dans Azure](https://msdn.microsoft.com/library/dn385720.aspx), est disponible à partir de SQL Server 2014. L’exécution de SQL Server avec des fichiers de données dans Azure offre des caractéristiques de performances comparables à l’utilisation de disques de données Azure.

## <a name="next-steps"></a>Étapes suivantes

Pour les meilleures pratiques de sécurité, consultez [Considérations relatives à la sécurité de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-security.md).

Consultez d’autres rubriques relatives aux machines virtuelles avec SQL Server à la page [Vue d’ensemble de SQL Server sur les machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).
