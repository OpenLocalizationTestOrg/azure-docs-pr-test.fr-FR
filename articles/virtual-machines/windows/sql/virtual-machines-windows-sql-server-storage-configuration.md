---
title: configuration aaaStorage pour les machines virtuelles SQL Server | Documents Microsoft
description: "Cette rubrique décrit comment Azure configure le stockage pour les machines virtuelles SQL Server lors de la configuration (modèle de déploiement Resource Manager). Elle explique également comment vous pouvez configurer le stockage pour vos machines virtuelles SQL Server existantes."
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>Configuration du stockage pour les machines virtuelles SQL Server
Lorsque vous configurez une image de machine virtuelle SQL Server dans Azure, hello portail permet de tooautomate votre configuration de stockage. Cela inclut l’attachement de stockage toohello machine virtuelle, qui effectue cette tooSQL accessible du stockage serveur et de configuration toooptimize pour vos besoins spécifiques.

Cette rubrique explique comment Azure configure le stockage pour vos machines virtuelles SQL Server à la fois lors de la configuration et pour les machines virtuelles existantes. Cette configuration est basée sur hello [bonnes pratiques de performance](virtual-machines-windows-sql-performance.md) pour les machines virtuelles Azure exécutant SQL Server.

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>Composants requis
toouse hello automatisée des paramètres de configuration de stockage, votre machine virtuelle nécessite hello suivant caractéristiques :

* Configurée avec une [image de galerie SQL Server](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing);
* Utilise hello [modèle de déploiement de gestionnaire de ressources](../../../azure-resource-manager/resource-manager-deployment-model.md).
* Utilise [Premium Storage](../../../storage/common/storage-premium-storage.md).

## <a name="new-vms"></a>Nouvelles machines virtuelles
Hello sections suivantes décrivent comment stockage tooconfigure de nouveaux ordinateurs virtuels SQL Server.

### <a name="azure-portal"></a>Portail Azure
Lors de la configuration d’une machine virtuelle de Azure à l’aide d’une image de la galerie de SQL Server, vous pouvez choisir tooautomatically configurer le stockage de hello pour votre nouvelle machine virtuelle. Vous spécifiez la taille de stockage de hello, des limites de performances et le type de charge de travail. Hello capture d’écran suivante montre Panneau de configuration de stockage hello utilisé pendant SQL VM de configuration.

![Configuration du stockage des machines virtuelles SQL Server lors de la configuration](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

En fonction de vos choix, Azure effectue hello suivant des tâches de configuration de stockage après la création d’hello machine virtuelle :

* Crée et attache la machine virtuelle des toohello de disques premium storage data.
* Configure hello données disques toobe accessible tooSQL Server.
* Configure les disques de données hello dans un stockage pool basée sur hello spécifié (IOPS et débit) taille et les performances requises.
* Associe le pool de stockage hello avec un nouveau lecteur sur l’ordinateur virtuel de hello.
* Optimise ce nouveau lecteur en fonction du type de charge de travail que vous avez spécifié (entrepôt de données, traitement transactionnel ou général).

Pour plus d’informations sur la façon dont Azure configure les paramètres de stockage, consultez hello [section de configuration de stockage](#storage-configuration). Pour connaître la procédure complète de toocreate une machine virtuelle SQL Server dans hello portail Azure, voir [hello approvisionnement didacticiel](virtual-machines-windows-portal-sql-server-provision.md).

### <a name="resource-manage-templates"></a>Modèles Resource Manager
Si vous utilisez hello suivant des modèles du Gestionnaire de ressources, les deux disques de données premium sont attachés par défaut, sans aucune configuration de pool de stockage. Toutefois, vous pouvez personnaliser ces modèles toochange hello différents disques de données premium sont toohello joint l’ordinateur virtuel.

* [Créer des machines virtuelles avec sauvegarde automatisée](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [Créer des machines virtuelles avec mise à jour corrective automatisée](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [Créer des machines virtuelles avec AKV Integration](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>Machines virtuelles existantes
Pour SQL Server des machines virtuelles existantes, vous pouvez modifier certains paramètres de stockage Bonjour portail Azure. Sélectionnez votre machine virtuelle, accédez toohello zone des paramètres, puis sélectionnez la Configuration de SQL Server. Panneau de Configuration SQL Server Hello affiche hello Active l’utilisation du stockage de votre machine virtuelle. Tous les lecteurs qui existent sur votre machine virtuelle apparaissent dans ce graphique. Pour chaque lecteur, espace de stockage hello s’affiche dans les quatre sections :

* Données SQL
* Journal SQL
* Autre (stockage non-SQL)
* Disponible

![Configurer le stockage pour les machines virtuelles SQL Server existantes](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure hello stockage tooadd un nouveau lecteur ou étendre un disque existant, cliquez sur hello modifier au-dessus du graphique de hello.

options de configuration Hello que vous voyez varie selon que vous avez utilisé cette fonctionnalité avant. Lorsque vous utilisez pour hello la première fois, vous pouvez spécifier vos besoins de stockage pour un nouveau lecteur. Si vous avez utilisé précédemment cet toocreate fonctionnalité un lecteur, vous pouvez choisir tooextend du stockage.

### <a name="use-for-hello-first-time"></a>Utilisation pour hello première fois
Si elle est la première fois à l’aide de cette fonctionnalité, vous pouvez spécifier hello des limites de taille et les performances de stockage pour un nouveau lecteur. Cette expérience est similaire toowhat que vous visualiserez au moment de l’approvisionnement. Hello principale différence est que vous n’êtes pas autorisé type de charge de travail toospecify hello. Cette restriction empêche interrompre toute configuration de SQL Server existante sur l’ordinateur virtuel de hello.

![Configurer les curseurs de stockage SQL Server](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Azure crée un nouveau lecteur, en fonction de vos spécifications. Dans ce scénario, Azure effectue hello suivant de tâches de configuration de stockage :

* Crée et attache la machine virtuelle des toohello de disques premium storage data.
* Configure hello données disques toobe accessible tooSQL Server.
* Configure les disques de données hello dans un stockage pool basée sur hello spécifié (IOPS et débit) taille et les performances requises.
* Associe le pool de stockage hello avec un nouveau lecteur sur l’ordinateur virtuel de hello.

Pour plus d’informations sur la façon dont Azure configure les paramètres de stockage, consultez hello [section de configuration de stockage](#storage-configuration).

### <a name="add-a-new-drive"></a>Ajout d’un nouveau lecteur
Si vous avez déjà configuré le stockage sur votre machine virtuelle SQL Server, l’extension du stockage donne accès à deux nouvelles options. Hello première option est tooadd un nouveau disque, ce qui peut augmenter le niveau de performance hello de votre machine virtuelle.

![Ajouter un nouveau tooa de lecteur SQL VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

Toutefois, après avoir ajouté le lecteur de hello, vous devez effectuer une augmentation des performances configuration manuel supplémentaire tooachieve hello.

### <a name="extend-hello-drive"></a>Étendez le lecteur de hello
Bonjour autre option pour le stockage de développement est lecteur existant de tooextend hello. Cette option augmente hello de stockage disponible pour votre disque, mais elle n’augmente pas les performances. Avec les pools de stockage, vous ne pouvez pas modifier le nombre hello de colonnes après la création de pool de stockage hello. nombre Hello de colonnes détermine le nombre hello des écritures parallèles, qui peuvent être réparties sur les disques de données hello. Par conséquent, les disques de données ajoutés ne peuvent pas augmenter les performances. Ils peuvent uniquement fournir plus de stockage pour les données hello en cours d’écriture. Cette limitation signifie également que, lorsque vous étendez le lecteur de hello, nombre hello de colonnes détermine le nombre minimal de hello de disques de données que vous pouvez ajouter. Par conséquent, si vous créez un pool de stockage avec des disques de données de quatre, hello nombre de colonnes est également quatre. Chaque fois que vous étendez le stockage hello, vous devez ajouter des disques de données au moins quatre.

![Étendre un lecteur d’une machine virtuelle SQL](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>Configuration du stockage
Cette section fournit une référence pour les modifications de configuration de stockage hello Azure effectue automatiquement pendant VM SQL de configuration ou de la configuration Bonjour portail Azure.

* Si vous avez sélectionné moins de deux téraoctets de stockage pour votre machine virtuelle, Azure ne crée pas de pool de stockage.
* Si vous avez sélectionné au moins deux téraoctets de stockage pour votre machine virtuelle, Azure configure un pool de stockage. section suivante de Hello de cette rubrique fournit des détails de hello de configuration du pool de stockage hello.
* La configuration automatique du stockage utilise toujours des disques de données P30 [Premium Storage](../../../storage/common/storage-premium-storage.md) . Par conséquent, il existe un mappage 1:1 entre votre nombre sélectionné de téraoctets et hello de disques de données associé tooyour machine virtuelle.

Pour plus d’informations de tarification, consultez hello [tarification du stockage](https://azure.microsoft.com/pricing/details/storage) page hello **le stockage sur disque** onglet.

### <a name="creation-of-hello-storage-pool"></a>Création d’un pool de stockage hello
Azure utilise hello suivant de pool de stockage de paramètres toocreate hello de machines virtuelles SQL Server.

| Paramètre | Valeur |
| --- | --- |
| Taille de l’entrelacement |256 Ko (entrepôt de données) ; 64 Ko (transactionnel) |
| Tailles du disque |1 To chacun |
| Cache |Lire |
| Taille d'allocation |Taille d'unité d'allocation NTFS = 64 Ko |
| Initialisation instantanée des fichiers |Activé |
| Verrouillage des pages en mémoire |Activé |
| Récupérer |Récupération simple (sans résilience) |
| Nombre de colonnes |Nombre de disques de données<sup>1</sup> |
| Emplacement de TempDB |Stocké sur les disques de données<sup>2</sup> |

<sup>1</sup> après la création de pool de stockage hello, vous ne pouvez pas modifier le nombre hello de colonnes dans le pool de stockage hello.

<sup>2</sup> ce paramètre s’applique uniquement toohello premier lecteur vous créez à l’aide de la fonctionnalité de configuration de stockage hello.

## <a name="workload-optimization-settings"></a>Paramètres d’optimisation de la charge de travail
Hello tableau suivant décrit hello trois charges de travail type options disponibles et leurs optimisations correspondantes :

| Type de charge de travail | Description | Optimisations |
| --- | --- | --- |
| **Généralités** |Paramètre par défaut qui prend en charge la plupart des charges de travail |Aucun |
| **Traitement transactionnel** |Optimise le stockage hello pour les charges de travail OLTP classique de la base de données |Indicateur de trace 1117<br/>Indicateur de trace 1118 |
| **Entrepôt de données** |Optimise le stockage hello pour les charges de travail d’analyse et de création de rapports |Indicateur de trace 610<br/>Indicateur de trace 1117 |

> [!NOTE]
> Vous pouvez uniquement spécifier type de charge de travail hello lorsque vous configurez un ordinateur virtuel SQL en la sélectionnant dans l’étape de configuration de stockage hello.
>
>

## <a name="next-steps"></a>Étapes suivantes
Pour les autres rubriques connexes toorunning SQL Server dans des machines virtuelles Azure, consultez [SQL Server sur des Machines virtuelles Azure](virtual-machines-windows-sql-server-iaas-overview.md).
