---
title: "aaaCopy activité guide des performances et paramétrage | Documents Microsoft"
description: "Découvrez les principaux facteurs qui affectent les performances de hello de déplacement des données dans Azure Data Factory lorsque vous utilisez l’activité de copie."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 4b9a6a4f-8cf5-4e0a-a06f-8133a2b7bc58
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jingwang
ms.openlocfilehash: b0fb5a76c34752d07e8ddfffbb799a05fb5d6be6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-activity-performance-and-tuning-guide"></a>Guide sur les performances et le réglage de l’activité de copie
L’activité de copie Azure Data Factory offre une solution de chargement de données de premier ordre, sécurisée, fiable et hautes performances. Il vous toocopy des dizaines de téraoctets de données tous les jours entre une grande variété de cloud et banques de données locale. Performances de chargement des données d’accélérée ultra-rapides sont tooensure clé, vous pouvez vous concentrer sur le problème de « big data » hello core : création de solutions d’analytique avancée et l’obtention des informations détaillées à partir de toutes les données.

Azure fournit un ensemble d’échelle de l’entreprise solutions d’entrepôt de données de stockage et données, et l’activité de copie offre une expérience tooconfigure facile et configuration de chargement de données hautement optimisées. Avec une seule activité de copie, vous pouvez obtenir ce qui suit :

* Chargement de données dans **Azure SQL Data Warehouse** à **1,2 Gbits/s**. Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.
* Chargement de données dans le **stockage des objets blob Azure** à **1,0 Gbit/s**
* Chargement de données dans **Azure Data Lake Store** à **1,0 Gbit/s**

Cet article explique :

* [Numéros de référence des performances](#performance-reference) pour la prise en charge toohelp banques de données source et le récepteur vous planifiez votre projet ;
* Fonctionnalités peuvent dynamiser hello débit dans différents scénarios, y compris [unités de déplacement des données en nuage](#cloud-data-movement-units), [parallèles copie](#parallel-copy), et [intermédiaire copie](#staged-copy);
* [Conseils de réglage des performances](#performance-tuning-steps) sur comment tootune hello performances et hello facteurs clés qui peuvent affecter les performances en copie.

> [!NOTE]
> Si vous n’êtes pas familiarisé avec l’activité de copie, voir [Déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md) avant de lire cet article.
>

## <a name="performance-reference"></a>Performances de référence

En tant que référence, tableau ci-dessous présente nombre de débit de copie hello en Mbits/s pour hello donné paires source et le récepteur basés sur les tests internes. À des fins de comparaison, il montre également comment les différents paramètres [d’unités de déplacement des données cloud](#cloud-data-movement-units) ou [d’évolutivité de la passerelle de gestion des données](data-factory-data-management-gateway-high-availability-scalability.md) (plusieurs nœuds de passerelle) peuvent améliorer les performances de copie.

![Matrice des performances](./media/data-factory-copy-activity-performance/CopyPerfRef.png)


**Points toonote :**
* Débit est calculé à l’aide de hello formule suivante : [taille des données lues à partir de la source] / [activité de copie de durée d’exécution].
* numéros de référence des performances Hello dans la table de hello ont été mesurés à l’aide de [TPC-H](http://www.tpc.org/tpch/) jeu de données dans une activité de copie unique s’exécuter.
* Dans les magasins de données Azure, hello source et le récepteur sont Bonjour même région Azure.
* Pour la copie hybride entre locaux et cloud magasins de données, chaque nœud de passerelle était en cours d’exécution sur un ordinateur qui a été séparé hello magasin de données local avec sous spécification. Lorsqu’une activité unique était en cours d’exécution sur la passerelle, opération de copie hello consommée uniquement une petite partie de l’ordinateur de test hello du processeur, la mémoire ou la bande passante réseau. Pour en savoir plus, voir [Considérations relatives à la passerelle de gestion des données](#considerations-for-data-management-gateway).
    <table>
    <tr>
        <td>UC</td>
        <td>32 cœurs 2,20 GHz Intel Xeon E5-2660 v2</td>
    </tr>
    <tr>
        <td>Mémoire</td>
        <td>128 Go</td>
    </tr>
    <tr>
        <td>Réseau</td>
        <td>Interface Internet : 10 Gbits/s ; interface intranet : 40 Gbits/s</td>
    </tr>
    </table>


> [!TIP]
> Vous pouvez obtenir un débit plus élevé grâce à plus d’unités de déplacement de données (DMUs) que hello par défaut DMUs maximales, qui est 32 pour une activité de copie de vers cloud s’exécuter. Par exemple, avec 100 unités DMU, vous pouvez copier des données depuis Azure Blob vers Azure Data Lake Store à **1,0 Go/s**. Consultez hello [unités de déplacement des données en nuage](#cloud-data-movement-units) pour plus d’informations sur cette fonctionnalité et sur hello les scénarios pris en charge. Contact [prise en charge Azure](https://azure.microsoft.com/support/) toorequest DMUs plus.

## <a name="parallel-copy"></a>Copie en parallèle
Vous pouvez lire la source de données à partir de hello ou écrire la destination des données toohello **en parallèle dans une activité de copie exécuter**. Cette fonctionnalité améliore le débit d’une opération de copie hello et réduit hello durée toomove données.

Ce paramètre est différent de hello **concurrency** propriété dans la définition d’activité hello. Hello **concurrency** propriété détermine le nombre de hello de **simultanées activité de copie s’exécute** tooprocess des données à partir de windows de l’activité différente (1 h too2 AM, 2 AM too3, 3 AM too4 AM, et ainsi de suite). Cette fonctionnalité est utile lorsque vous effectuez une charge historique. fonctionnalité de copie en parallèle Hello s’applique tooa **unique activité exécuter**.

Examinons un exemple de scénario. Dans l’exemple suivant de hello, plusieurs tranches de hello passée doivent toobe traité. Data Factory exécute une instance de l’activité de copie (une exécution d’activité) pour chaque tranche :

* la tranche de données à partir de la fenêtre d’activité première hello Hello (1 h too2 suis) == > exécution de l’activité 1
* la tranche de données à partir de la fenêtre d’activité deuxième hello Hello (2 AM too3 suis) == > activité exécutée 2
* la tranche de données à partir de la fenêtre d’activité deuxième hello Hello (3 AM too4 suis) == > activité exécuter 3

Et ainsi de suite.

Dans cet exemple, lorsque hello **concurrency** a la valeur too2, **activité exécutée 1** et **activité exécutée 2** copier les données à partir de deux fenêtres de l’activité **simultanément**  tooimprove les performances de déplacement de données. Toutefois, si plusieurs fichiers sont associés à activité exécuter 1, le service de déplacement de données hello copie les fichiers à partir d’un seul fichier hello source toohello destination à la fois.

### <a name="cloud-data-movement-units"></a>Unités de déplacement de données cloud
A **unité de déplacement des données de cloud (DMU)** est une mesure qui représente la puissance hello (il s’agit d’une combinaison de l’UC, la mémoire et l’allocation des ressources réseau) d’une seule unité dans la fabrique de données. Une unité de déplacement de données peut être utilisée dans une opération de copie cloud-cloud, mais pas dans une copie hybride.

Par défaut, la fabrique de données utilise un tooperform DMU cloud unique une seule activité de copie s’exécuter. toooverride cette valeur par défaut, spécifiez une valeur pour hello **cloudDataMovementUnits** propriété comme suit. Pour plus d’informations sur le niveau de gain de performance de hello que vous pouvez obtenir lorsque vous configurez plusieurs unités pour une source de copie spécifique et le récepteur, consultez hello [référence des performances](#performance-reference).

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "cloudDataMovementUnits": 32
        }
    }
]
```
Hello **valeurs autorisées** pour hello **cloudDataMovementUnits** propriété sont 1 (valeur par défaut), 2, 4, 8, 16, 32. Hello **nombre réel de cloud DMUs** que l’opération de copie hello utilise au moment de l’exécution est égale tooor inférieure à hello configuré en fonction de votre modèle de données.

> [!NOTE]
> Si vous avez besoin de plus d’unités de déplacement de données cloud pour un débit plus élevé, contactez le [support Azure](https://azure.microsoft.com/support/). Définition de 8 et versions ultérieures actuellement fonctionnent uniquement lorsque vous **copier plusieurs fichiers à partir de l’objet Blob stockage/Data Lake Store/Amazon S3/cloud FTP/cloud SFTP tooBlob stockage/Data Lake Store/et Azure SQL Database**.
>

### <a name="parallelcopies"></a>parallelCopies
Vous pouvez utiliser hello **parallelCopies** parallélisme de hello tooindicate propriété que vous souhaitez toouse d’activité de copie. Vous pouvez considérer cette propriété en tant que le nombre maximal de hello des threads au sein de l’activité de copie qui peut lire à partir de votre source ou écrire des magasins de données récepteur tooyour en parallèle.

Pour chaque activité de copie s’exécuter, Data Factory détermine le nombre hello de parallèle copie toouse toocopy données à partir de la banque de données source hello et magasin de données de destination toohello. nombre de copies parallèles qu’il utilise par défaut de Hello dépend de type hello de source et le récepteur que vous utilisez.  

| Source et récepteur | Nombre de copie en parallèle par défaut déterminé par le service |
| --- | --- |
| Copie de données entre les magasins basés sur fichier (stockage des objets blob ; Data Lake Store ; Amazon S3 ; un système de fichiers local ; un HDFS local) |Entre 1 et 32. Taille hello de fichiers de hello et nombre de hello d’unités de déplacement des données de cloud (DMUs) dépend des données toocopy utilisés entre les deux banques de données cloud ou configuration physique de hello de hello ordinateur passerelle utilisée pour une copie hybride (toocopy données tooor à partir d’une banque de données locale ). |
| Copier des données à partir de **toutes les données source stocker tooAzure le stockage de Table** |4 |
| Toutes les autres paires de source et de récepteur |1 |

En règle générale, par défaut hello doit vous fournir débit hello. Toutefois, toocontrol hello de charge sur les ordinateurs qui hébergent vos magasins de données, ou des performances de copie tootune, vous pouvez choisir la valeur par défaut de hello toooverride et spécifiez une valeur pour hello **parallelCopies** propriété. valeur de Hello doit être compris entre 1 et 32 (tous deux inclus). Au moment de l’exécution, pour de meilleures performances de hello, l’activité de copie utilise une valeur qui est inférieure ou égale valeur toohello que vous définissez.

```json
"activities":[  
    {
        "name": "Sample copy activity",
        "description": "",
        "type": "Copy",
        "inputs": [{ "name": "InputDataset" }],
        "outputs": [{ "name": "OutputDataset" }],
        "typeProperties": {
            "source": {
                "type": "BlobSource",
            },
            "sink": {
                "type": "AzureDataLakeStoreSink"
            },
            "parallelCopies": 8
        }
    }
]
```
Points toonote :

* Lorsque vous copiez des données entre des magasins basés sur des fichiers, hello **parallelCopies** déterminer le parallélisme hello au niveau du fichier hello. Hello de segmentation dans un seul fichier passerait sous en toute transparence et automatiquement, et il est conçu toouse hello meilleures approprié taille de segment pour une banque de données source donnée de type tooload dans tooparallelCopies parallèles et orthogonales. nombre réel de Hello de copies parallèles hello données mouvement service utilise pour l’opération de copie hello en cours d’exécution n’est pas plus de numéro hello des fichiers. Si le comportement de copie hello est **mergeFile**, l’activité de copie ne peut pas tirer parti du parallélisme au niveau du fichier.
* Lorsque vous spécifiez une valeur pour hello **parallelCopies** propriété, envisagez d’augmenter de charge hello de vos magasins de données source et le récepteur, toogateway s’il s’agit d’une copie hybride. Cela produit en particulier lorsque vous avez plusieurs activités ou les exécutions simultanées de hello mêmes activités qui s’exécutent sur hello même magasin de données. Si vous remarquez que le magasin de données hello ou passerelle est surchargé avec une charge hello, diminuer hello **parallelCopies** charge de valeur toorelieve hello.
* Lorsque vous copiez des données à partir de magasins qui ne sont pas toostores basée sur des fichiers qui sont basés sur le fichier, le service de déplacement de données hello ignore hello **parallelCopies** propriété. Même si le parallélisme est spécifié, il n’est pas appliqué dans ce cas.

> [!NOTE]
> Vous devez utiliser hello de passerelle de gestion des données version 1.11 ou version ultérieure toouse **parallelCopies** fonctionnalité lorsque vous effectuez une copie hybride.
>
>

toobetter ces deux propriétés et tooenhance votre débit de déplacement des données, voir hello [exemples de cas d’usage](#case-study-use-parallel-copy). Vous n’avez pas besoin de tooconfigure **parallelCopies** parti tootake du comportement par défaut de hello. Si vous configurez **parallelCopies** et que la valeur est trop basse, plusieurs unités de déplacement de données cloud ne peuvent pas être pleinement utilisées.  

### <a name="billing-impact"></a>Impact sur la facturation
Il a **important** tooremember qui vous sont facturés en fonction hello le temps total d’opération de copie hello. Si un travail de copie utilisé tootake une heure avec l’unité d’un cloud et maintenant il prend 15 minutes avec quatre unités de cloud, hello globale facture reste presque hello identiques. Par exemple, vous utilisez quatre unités cloud. première unité de cloud Hello consacre à 10 minutes, hello un deuxième, 10 minutes, hello un tiers, 5 minutes, hello une quatrième, 5 minutes, toutes dans une activité de copie s’exécuter. Vous êtes facturé pour le temps hello copie total (le déplacement des données), qui est de 10 + 10 + 5 + 5 = 30 minutes. L’utilisation de **parallelCopies** n’affecte pas la facturation.

## <a name="staged-copy"></a>copie intermédiaire
Lorsque vous copiez des données à partir d’un magasin de données de source données magasin tooa récepteur, vous pouvez choisir toouse stockage d’objets Blob comme magasin de mise en lots intermédiaire. Mise en lots est particulièrement utile dans hello suivant cas :

1. **Vous voulez tooingest des données à partir de différentes banques de données dans l’entrepôt de données SQL via PolyBase**. SQL Data Warehouse utilise PolyBase comme un tooload à débit élevé mécanisme une grande quantité de données dans l’entrepôt de données SQL. Toutefois, les données de salutation source doivent être dans le stockage Blob, et elle doit répondre aux critères supplémentaires. Lorsque vous chargez des données à partir d’une banque de données autre que le stockage Blob, vous pouvez activer la copie de données via un stockage Blob intermédiaire. Dans ce cas, la fabrique de données effectue tooensure de transformations de données hello requis qu’il répond aux exigences de hello de PolyBase. Il utilise ensuite les données tooload de PolyBase dans SQL Data Warehouse. Pour plus d’informations, consultez [PolyBase d’utilisation des données de tooload dans Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse). Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.
2. **Parfois, il faut un certain temps tooperform un mouvement de données hybride (autrement dit, toocopy entre une banque de données locale et un magasin de données cloud) via une connexion réseau lente**. tooimprove des performances, vous pouvez compresser hello en local afin que celui-ci utilise moins de temps toomove toohello mise en lots de données stocker dans le cloud de hello. Puis, vous pouvez décompresser les données de salutation Bonjour intermédiaire magasin avant de les charger dans le magasin de données de destination hello.
3. **Vous ne souhaitez pas tooopen ports autres que le port 80 et le port 443 dans votre pare-feu, en raison des stratégies informatiques d’entreprise**. Par exemple, lorsque vous copiez des données à partir d’un récepteur Azure SQL Database tooan de banque de données locale ou un récepteur de l’entrepôt de données SQL Azure, vous devez tooactivate les communications TCP sortantes sur le port 1433 pour le pare-feu Windows hello et de pare-feu de l’entreprise. Dans ce scénario, tirer parti de hello passerelle toofirst copie données tooa Blob intermédiaire instance de stockage via HTTP ou HTTPS sur le port 443. Ensuite, chargez les données de salutation dans la base de données SQL ou de l’entrepôt de données SQL à partir du transit de stockage Blob. Dans ce flux, vous n’avez pas besoin tooenable le port 1433.

### <a name="how-staged-copy-works"></a>Fonctionnement de la copie intermédiaire
Lorsque vous activez hello fonctionnalité de mise en lots, premières données hello sont copiées à partir de la banque de données de mise en lots de hello source données magasin toohello (apportez votre propre). Ensuite, les données de hello sont copiées de hello banque de données récepteur de données magasin toohello de mise en lots. Fabrique de données gère automatiquement les flux de deux étapes hello pour vous. Fabrique de données nettoie également les données temporaires à partir de hello mise en lots de stockage après le déplacement des données de hello sont terminé.

Dans le scénario de la copie cloud hello (source et le récepteur de données sont des magasins dans le cloud de hello), la passerelle n’est pas utilisée. Hello service Data Factory effectue les opérations de copie hello.

![Copie intermédiaire : scénario cloud](media/data-factory-copy-activity-performance/staged-copy-cloud-scenario.png)

Dans le scénario de copie hello hybride (source est locale et récepteur dans le cloud de hello), la passerelle de hello déplace tooa intermédiaire du magasin de données du magasin de données à partir de la source de données hello. Service de fabrique de données déplace le magasin de données récepteur toohello du magasin de données à partir de hello transit des données. Copie de données à partir d’un tooan de magasin de données cloud local banque de données via un intermédiaire également est pris en charge avec les flux hello inversée.

![Copie intermédiaire : scénario hybride](media/data-factory-copy-activity-performance/staged-copy-hybrid-scenario.png)

Lorsque vous activez le déplacement des données à l’aide d’un magasin intermédiaire, vous pouvez spécifier si vous souhaitez que hello toobe de données compressée avant le déplacement de données à partir de la source de hello magasin tooan temporaire ou la banque de données de mise en lots de données et puis décompressé avant le déplacement de données à partir d’un intervalle ou magasin de données récepteur toohello de magasin de données mise en lots.

Actuellement, vous ne pouvez pas copier de données entre deux banques de données locales à l’aide d’une banque intermédiaire. Nous pensons que cette option toobe disponible bientôt.

### <a name="configuration"></a>Configuration
Configurer hello **enableStaging** définition dans l’activité de copie toospecify si vous souhaitez hello toobe de données transférée dans le stockage Blob avant de les charger dans un magasin de données de destination. Lorsque vous définissez **enableStaging** tooTRUE, spécifier des propriétés supplémentaires hello répertoriées dans le tableau suivant de hello. Si vous n’en avez pas, vous devez également toocreate un stockage Azure ou le stockage partagé service lié à la signature d’accès pour l’environnement intermédiaire.

| Propriété | Description | Valeur par défaut | Requis |
| --- | --- | --- | --- |
| **enableStaging** |Spécifiez si vous souhaitez que les données toocopy via un intervalle de mise en lots de magasin. |False |Non |
| **linkedServiceName** |Spécifiez le nom hello d’un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) service, qui fait référence instance toohello de stockage que vous utilisez comme un magasin de mise en lots intermédiaire lié. <br/><br/> Vous ne pouvez pas utiliser le stockage comportant des données tooload signature d’accès partagé dans l’entrepôt de données SQL via PolyBase. Vous pouvez l’utiliser dans tous les autres scénarios. |N/A |Oui, lorsque **enableStaging** a la valeur tooTRUE |
| **path** |Spécifier le chemin de stockage d’objets Blob hello que les données de hello intermédiaire toocontain. Si vous ne fournissez pas un chemin d’accès, le service de hello crée une conteneur toostore les données de temporaire. <br/><br/> Spécifiez un chemin d’accès que si vous utilisez le stockage avec une signature d’accès partagé, ou vous avez besoin de toobe de données temporaires dans un emplacement spécifique. |N/A |Non |
| **enableCompression** |Spécifie si les données doivent être compressées avant qu’il soit copiée toohello destination. Ce paramètre réduit le volume hello de données transférées. |False |Non |

Voici un exemple de définition de l’activité de copie avec des propriétés de hello qui sont décrites dans le tableau précédent de hello :

```json
"activities":[  
{
    "name": "Sample copy activity",
    "type": "Copy",
    "inputs": [{ "name": "OnpremisesSQLServerInput" }],
    "outputs": [{ "name": "AzureSQLDBOutput" }],
    "typeProperties": {
        "source": {
            "type": "SqlSource",
        },
        "sink": {
            "type": "SqlSink"
        },
        "enableStaging": true,
        "stagingSettings": {
            "linkedServiceName": "MyStagingBlob",
            "path": "stagingcontainer/path",
            "enableCompression": true
        }
    }
}
]
```

### <a name="billing-impact"></a>Impact sur la facturation
Vous êtes facturé en fonction de deux étapes : la durée de la copie et le type de copie.

* Lorsque vous utilisez intermédiaire lors d’une copie de cloud (copie de données à partir d’un magasin de données du magasin tooanother cloud cloud données), vous êtes facturé hello [somme des durées de copie pour les étapes 1 et 2] x [prix unitaires de copie cloud].
* Lorsque vous utilisez intermédiaire lors d’une copie hybride (copie de données à partir d’une banque de données locale données magasin tooa cloud), vous êtes facturé pour [durée de la copie hybride] x [prix d’unitaire copie hybride] + [durée de la copie de cloud computing] x [prix unitaires de copie cloud].

## <a name="performance-tuning-steps"></a>Procédure de réglage des performances
Nous recommandons d’effectuer ces étapes tootune les performances de hello de votre service de fabrique de données avec l’activité de copie :

1. **Établir une ligne de base**. Pendant la phase de développement hello, testez votre pipeline à l’aide de l’activité de copie sur un échantillon représentatif de données. Vous pouvez utiliser hello Data Factory [découpage modèle](data-factory-scheduling-and-execution.md) durée hello toolimit vous travaillez avec des données.

   Collecter le temps d’exécution et les caractéristiques de performances à l’aide de hello **analyse et l’application de gestion**. Choisissez **Surveiller et gérer** sur votre page d’accueil Data Factory. Dans l’arborescence de hello, choisissez hello **jeu de données de sortie**. Bonjour **Windows de l’activité** , choisissez hello exécuter l’activité de copie. **Activité Windows** répertorie la durée de l’activité de copie hello et taille hello de données hello sont copiée. débit de Hello est répertorié dans **activité fenêtre Explorateur**. toolearn en savoir plus sur l’application hello, consultez [analyse et gérer des pipelines Azure Data Factory à l’aide de hello surveillance et l’application de gestion](data-factory-monitor-manage-app.md).

   ![Détails de l'exécution d'activité](./media/data-factory-copy-activity-performance/mmapp-activity-run-details.png)

   Plus loin dans l’article hello, vous pouvez comparer les performances de hello et la configuration de votre scénario tooCopy activité [référence des performances](#performance-reference) de nos tests.
2. **Diagnostiquer et optimiser les performances**. Si les performances hello que vous observez ne répondent pas à vos attentes, vous devez tooidentify les goulots d’étranglement. Ensuite, optimiser les performances tooremove ou réduire l’effet de hello des goulots d’étranglement. Une description complète des diagnostics de performances est abordée dans cet article hello, mais certaines considérations courantes sont :

   * Fonctionnalités de performances :
     * [Copie en parallèle](#parallel-copy)
     * [Unités de déplacement de données cloud](#cloud-data-movement-units)
     * [Copie intermédiaire](#staged-copy)
     * [Évolutivité de la passerelle de gestion des données](data-factory-data-management-gateway-high-availability-scalability.md)
   * [Passerelle de gestion de données](#considerations-for-data-management-gateway)
   * [Source](#considerations-for-the-source)
   * [Section sink](#considerations-for-the-sink)
   * [Sérialisation et désérialisation](#considerations-for-serialization-and-deserialization)
   * [Compression](#considerations-for-compression)
   * [Mappage de colonnes](#considerations-for-column-mapping)
   * [Autres points à considérer](#other-considerations)
3. **Développez le jeu de données entier hello configuration tooyour**. Lorsque vous êtes satisfait des performances et les résultats de l’exécution de hello, vous pouvez développer la définition de hello et pipeline toocover période active votre ensemble de données.

## <a name="considerations-for-data-management-gateway"></a>Considérations relatives à la passerelle de gestion des données
**Le programme d’installation de passerelle**: nous vous recommandons d’utiliser une passerelle de gestion des données de toohost ordinateur dédié. Voir [Considérations relatives à l’utilisation de la passerelle de gestion des données](data-factory-data-management-gateway.md#considerations-for-using-gateway).  

**Analyse de la passerelle et la montée en puissancehaut/**: une seule passerelle logique avec un ou plusieurs nœuds de passerelle peut traiter plusieurs activité de copie s’exécute sur hello même moment simultanément. Vous pouvez afficher l’instantané quasiment en temps réel de l’utilisation des ressources (processeur, mémoire, network(in/out), etc.) sur un ordinateur de passerelle, ainsi que le nombre de hello de travaux simultanés en cours d’exécution par rapport à la limite de hello portail Azure, consultez [passerelle moniteur dans le portail hello](data-factory-data-management-gateway.md#monitor-gateway-in-the-portal). Si vous avez besoin d’importante sur le déplacement des données hybride avec un grand nombre d’exécutions d’activité copie simultanée ou avec un gros volume de données toocopy, envisagez trop[montée en puissance ou la montée en puissance parallèle passerelle](data-factory-data-management-gateway-high-availability-scalability.md#scale-considerations) ainsi en toobetter utiliser votre ressource ou tooprovision plusieurs ressources tooempower copier. 

## <a name="considerations-for-hello-source"></a>Considérations relatives à la source de hello
### <a name="general"></a>Généralités
N’oubliez pas que hello sous-jacent du magasin de données ne soit pas submergé par les autres charges de travail qui sont exécutent sur ou s’y rapportant.

Pour les magasins de données de Microsoft, consultez [surveillance et de paramétrage des rubriques](#performance-reference) qui sont des magasins de toodata spécifique et vous aident à comprendre les caractéristiques de performances de magasin de données, réduire les temps de réponse et optimiser le débit.

Si vous copiez des données à partir de l’objet Blob stockage tooSQL l’entrepôt de données, envisagez d’utiliser **PolyBase** tooboost performances. Consultez [PolyBase d’utilisation des données de tooload dans Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) pour plus d’informations. Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.

### <a name="file-based-data-stores"></a>Magasins de données basés sur un fichier
*(Inclut le stockage des objets blob, Data Lake Store, Amazon S3, les systèmes de fichiers locaux et HDFS locaux)*

* **Taille moyenne de fichier et nombre de fichiers**: l’activité de copie transfère les données d’un fichier à la fois. Avec hello déplacée de la même quantité de données toobe, hello débit global est faible si les données de salutation est composée de nombreux petits fichiers plutôt que de quelques fichiers volumineux en raison de la phase d’amorçage toohello pour chaque fichier. Par conséquent, si possible, combiner plusieurs petits fichiers dans un plus grand débit plus élevé toogain de fichiers.
* **Fichier de format et compression**: pour davantage de performances tooimprove manières, consultez hello [considérations relatives à la sérialisation et la désérialisation](#considerations-for-serialization-and-deserialization) et [considérations pour la compression](#considerations-for-compression) sections.
* Pourquoi **système de fichiers local** scénario, dans lequel **passerelle de gestion des données** est obligatoire, voir hello [considérations relatives à la passerelle de gestion des données](#considerations-for-data-management-gateway) section.

### <a name="relational-data-stores"></a>Bases de données relationnelles
*(Inclut SQL Database, SQL Data Warehouse, Amazon Redshift, les bases de données SQL Server et les bases de données Oracle, MySQL, DB2, Teradata, Sybase et PostgreSQL, etc.)*

* **Modèle de données**: votre schéma de table a des répercussions sur le débit de copie. Une taille importante vous offre de meilleures performances à petite taille, toocopy hello même volume de données. Hello est que cette base de données hello peut extraire plus efficacement les lots de moins de données qui contiennent moins de lignes.
* **Requête ou procédure stockée**: optimiser la logique de requête de hello ou procédure stockée spécifiée dans les données de toofetch de source de l’activité de copie hello plus efficacement hello.
* Pour **local bases de données relationnelles**, tels que SQL Server et Oracle, qui nécessitent l’utilisation hello de **passerelle de gestion des données**, consultez hello [considérations relatives à la passerelle de gestion des données](#considerations-on-data-management-gateway) section.

## <a name="considerations-for-hello-sink"></a>Considérations pour le récepteur de hello
### <a name="general"></a>Généralités
N’oubliez pas que hello sous-jacent du magasin de données ne soit pas submergé par les autres charges de travail qui sont exécutent sur ou s’y rapportant.

Pour les magasins de données de Microsoft, consultez trop[surveillance et de paramétrage des rubriques](#performance-reference) qui sont des magasins de toodata spécifique. Ces rubriques peuvent vous aider à comprendre les caractéristiques de performances du magasin de données et la façon dont des temps de réponse de toominimize et accélère le débit.

Si vous copiez des données à partir de **stockage d’objets Blob** trop**SQL Data Warehouse**, envisagez d’utiliser **PolyBase** tooboost performances. Consultez [PolyBase d’utilisation des données de tooload dans Azure SQL Data Warehouse](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) pour plus d’informations. Consultez [Charger 1 To dans Azure SQL Data Warehouse en moins de 15 minutes avec Azure Data Factory](data-factory-load-sql-data-warehouse.md) pour obtenir une procédure pas à pas avec un cas d’utilisation.

### <a name="file-based-data-stores"></a>Magasins de données basés sur un fichier
*(Inclut le stockage des objets blob, Data Lake Store, Amazon S3, les systèmes de fichiers locaux et HDFS locaux)*

* **Copiez le comportement**: Si vous copiez des données d’un magasin de données de fichier différent, l’activité de copie a trois options via hello **copyBehavior** propriété. Elle conserve la hiérarchie, aplatit la hiérarchie ou fusionne les fichiers. Conserver ou de mise à plat de la hiérarchie a peu ou aucune surcharge de performances, mais entraîne la fusion de fichiers tooincrease surcharge de performances.
* **Fichier de format et compression**: voir hello [considérations relatives à la sérialisation et la désérialisation](#considerations-for-serialization-and-deserialization) et [considérations pour la compression](#considerations-for-compression) sections pour les performances de tooimprove plusieurs façons .
* **Stockage Blob**: actuellement, le stockage Blob ne prend en charge que les objets blob de blocs pour un transfert de données et un débit optimisés.
* Pour **systèmes de fichiers local** scénarios qui nécessitent l’utilisation de hello de **passerelle de gestion des données**, consultez hello [considérations relatives à la passerelle de gestion des données](#considerations-for-data-management-gateway) section.

### <a name="relational-data-stores"></a>Bases de données relationnelles
*(Inclut SQL Database, SQL Data Warehouse, les bases de données SQL Server et les bases de données Oracle)*

* **Copiez le comportement**: selon les propriétés de hello que vous avez définies pour **sqlSink**, l’activité de copie écrit la base de données de destination de données toohello de différentes façons.
  * Par défaut, hello données mouvement service utilise les données de tooinsert salutation API de copie en bloc en mode append, qui fournit des hello des performances optimales.
  * Si vous configurez une procédure stockée dans le récepteur de hello, base de données hello s’applique à une ligne de données hello a une heure au lieu d’un chargement en masse. Les performances chutent considérablement. Si votre jeu de données est importante, le cas échéant, envisagez de commutation toousing hello **sqlWriterCleanupScript** propriété.
  * Si vous configurez hello **sqlWriterCleanupScript** exécuter de propriété pour chaque activité de copie, déclencheurs de service hello hello script, puis vous utilisez les données de salutation tooinsert hello API de copie en bloc. Par exemple, toooverwrite hello toute table avec les données les plus récentes hello, vous pouvez spécifier un script toofirst supprimer tous les enregistrements avant de nouvelles données de chargement en masse hello à partir de la source de hello.
* **Modèle de données et taille de lot**:
  * Votre schéma de table a des répercussions sur le débit de copie. toocopy hello même volume de données, une taille importante vous donne meilleures performances à une petite taille, car la base de données hello peut valider plus efficacement les lots de moins de données.
  * L’activité de copie insère des données dans une série de lots. Vous pouvez définir le nombre de hello de lignes dans un lot à l’aide de hello **valeur writeBatchSize** propriété. Si vos données ont de petites lignes, vous pouvez définir hello **valeur writeBatchSize** propriété avec un toobenefit de valeur plus élevée à partir d’un traitement par lots et un débit plus élevé. Si la taille de ligne hello de vos données est importante, soyez prudent lorsque vous augmentez **valeur writeBatchSize**. Une valeur élevée peut provoquer l’échec de copie tooa dû à la surcharge de la base de données hello.
* Pour **local bases de données relationnelles** , tels que SQL Server et Oracle, qui nécessitent l’utilisation hello de **passerelle de gestion des données**, consultez hello [considérations relatives à la passerelle de gestion des données](#considerations-for-data-management-gateway) section.

### <a name="nosql-stores"></a>Magasins NoSQL
*(Inclut le Stockage Table et Azure Cosmos DB)*

* Pour le **Stockage Table**:
  * **Partition**: l’écriture des partitions de données toointerleaved considérablement dégrade les performances. Trier vos données sources par clé de partition afin que les données de salutation sont insérées efficacement une partition après l’autre, ou ajuster hello logique toowrite hello tooa unique partition de données.
* Pour **Azure Cosmos DB** :
  * **Taille du lot**: hello **valeur writeBatchSize** jeux de propriétés nombre hello de demandes parallèles documents toocreate de service de base de données Azure Cosmos toohello. Attendez-vous à améliorer les performances lorsque vous augmentez **valeur writeBatchSize** , car les demandes parallèles plus sont envoyés tooAzure Cosmos DB. Toutefois, observer la limitation lorsque vous écrivez tooAzure Cosmos DB (message d’erreur hello est « Requête taux est grand »). Divers facteurs peuvent entraîner la limitation, notamment la taille du document, nombre de hello de termes dans les documents hello et hello stratégie d’indexation de la collection cible. tooachieve copie débit, envisagez d’utiliser une collection mieux, par exemple, S3.

## <a name="considerations-for-serialization-and-deserialization"></a>Considérations relatives à la sérialisation et à la désérialisation
Une sérialisation et une désérialisation peuvent survenir quand le jeu de données d’entrée ou de sortie est un fichier. Consultez la page [Formats de fichier et de compression pris en charge](data-factory-supported-file-and-compression-formats.md) qui présente des détails sur les formats de fichier pris en charge par activité de copie.

**Comportement de copie**:

* Copie de fichiers entre banques de données basées sur fichier :
  * Lorsque les jeux de données d’entrée et de sortie qu'ont tous deux ne hello même ou les paramètres de format de fichier, le service de déplacement de données hello exécute une copie binaire sans sérialisation ou la désérialisation. Vous consultez un scénario de toohello le débit par rapport plus élevé, dans quel hello les paramètres de format de fichier source et le récepteur sont différents entre eux.
  * Lorsque l’entrée et les deux jeux de données sortie sont au format texte et l’encodage de hello uniquement type est différent, le service de déplacement de données hello ne conversion de codage. Il ne la sérialisation et la désérialisation, ce qui entraîne une surcharge de performances par rapport copie binaire de tooa.
  * Lorsque d’entrée et de sortie jeux de données à la fois avoir différents formats de fichiers ou des configurations différentes, telles que les délimiteurs, hello service de déplacement de données désérialise toostream de données source, transformer et puis de le sérialiser dans le format de sortie hello indiquée. Cette opération entraîne une baisse des performances beaucoup plus importante par rapport à des scénarios de tooother.
* Lorsque vous copiez des fichiers vers ou depuis un magasin de données qui n’est pas basé sur le fichier (par exemple, à partir d’un magasin relationnel tooa du magasin de fichiers), l’étape de sérialisation ou la désérialisation hello est requise. Cette étape génère une surcharge significative des performances.

**Format de fichier**: format de fichier hello que vous choisissez peut affecter les performances de copie. Par exemple, Avro est un format binaire compact qui stocke des métadonnées avec des données. Il a vaste prise en charge dans l’écosystème de Hadoop hello pour le traitement et l’interrogation. Toutefois, Avro est plus coûteuse pour la sérialisation et la désérialisation, ce qui aboutit à un débit plus faible par rapport à tootext format. Faites votre choix d’un format de fichier hello que guidage de flux de traitement. Démarrer avec les données de hello du formulaire sont stockées dans, la source des magasins de données ou toobe extraites de systèmes externes ; format de meilleures Hello pour le stockage, traitement analytique et l’interrogation ; et, dans le format des données de hello doivent être exportées dans les data warehouses pour les outils de visualisation et de création de rapports. Parfois, un format de fichier qui n’est pas optimal pour lire et écrire des performances peuvent être un bon choix lorsque vous considérez hello globale analytiques processus.

## <a name="considerations-for-compression"></a>Considérations relatives à la compression
Lorsque votre jeu de données d’entrée ou de sortie est un fichier, vous pouvez définir la compression de l’activité de copie tooperform ou la décompression lorsqu’il écrit la destination des données toohello. Lorsque vous choisissez la compression, vous trouvez un compromis entre les entrées/sorties (E/S) et le processeur. La compression des données de hello des coûts supplémentaires en ressources de calcul. Toutefois, en retour, elle réduit les E/S réseau et le stockage. En fonction de vos données, vous pouvez constater une augmentation du débit global de copie.

**Codec**: l’activité de copie prend en charge gzip, bzip2 et les types de compression Deflate. Azure HDInsight peut utiliser les trois types de traitement. Chaque codec de compression présente des avantages. Par exemple, bzip2 a débit hello plus bas, mais vous obtenez hello ruche de meilleurs résultats avec bzip2, car vous pouvez le fractionner pour le traitement. Gzip est l’option de hello plus équilibrée, et il est utilisé hello plus souvent. Choisissez le codec hello qui convient le mieux à votre scénario de bout en bout.

**Niveau**: vous avec le choix entre deux options pour chaque codec de compression, la compression la plus rapide et la compression optimale. Hello plus rapide compressée option compresse les données de salutation aussi rapidement que possible, même si le fichier résultant de hello n’est pas compressé de façon optimale. Hello option optimale compressée consacre plus de temps sur la compression et génère une quantité minimale de données. Vous pouvez tester les deux toosee options qui fournit de meilleures performances globales dans votre cas.

**Une considération**: toocopy une grande quantité de données entre une banque locale et le cloud de hello, envisagez d’utiliser de stockage d’objets blob temporaire avec la compression. L’utilisation du stockage temporaire est utile lorsque la bande passante hello de votre réseau d’entreprise et vos services Azure est le facteur de limitation hello, et que vous souhaitez hello d’entrée de jeu de données et les données de sortie défini à la fois toobe sous forme non compressée. Plus spécifiquement, vous pouvez scinder une activité de copie unique en deux activités de copie. copie de Hello première copie activité d’intérimaire de tooan source hello ou un objet blob de mise en lots sous forme compressée. activité de copie Hello deuxième copie des données de hello compressé à partir du transit et puis décompresse alors qu’il écrit toohello récepteur.

## <a name="considerations-for-column-mapping"></a>Considérations relatives au mappage de colonnes
Vous pouvez définir hello **columnMappings** propriété toomap de l’activité de copie tous les ou un sous-ensemble de hello d’entrée de colonnes de sortie toohello de colonnes. Une fois que le service de déplacement de données hello lit les données de hello à partir de la source de hello, il doit le mappage de colonnes tooperform sur les données de salutation avant l’écriture de récepteur de toohello données hello. Ce traitement supplémentaire réduit le débit de copie.

Si votre banque de données source ne peut être interrogée, par exemple, s’il s’agit d’un magasin relationnel comme base de données SQL ou SQL Server, ou s’il s’agit d’une banque NoSQL comme stockage de Table ou de la base de données Azure Cosmos, envisagez d’en exécutant un push de filtrage de colonne hello et la réorganisation des logique toohello **requête**  propriété au lieu d’utiliser le mappage de colonnes. De cette manière, projection de hello se produit pendant que le service de déplacement de données hello lit de stocker des données à partir de la source de données hello, où il est beaucoup plus efficace.

## <a name="other-considerations"></a>Autres points à considérer
Si hello la taille des données que vous souhaitez toocopy est grande, vous pouvez ajuster vos données hello entreprise logique toofurther partition à l’aide de hello découpage mécanisme dans la fabrique de données. Ensuite, planifiez toorun activité de copie plus fréquemment exécuter de la taille des données tooreduce hello pour chaque activité de copie.

Être prudent nombre hello de jeux de données et copie les activités nécessitant une fabrique de données tooconnector toohello mêmes magasin de données à hello même temps. Nombre de travaux simultanés copie peut limiter un magasin de données et entraîner des performances de toodegraded, copier les nouvelles tentatives internes de travail et dans certains cas, les erreurs d’exécution.

## <a name="sample-scenario-copy-from-an-on-premises-sql-server-tooblob-storage"></a>Exemple de scénario : copie à partir d’un stockage tooBlob de SQL Server locale
**Scénario**: un pipeline repose toocopy des données à partir d’un stockage de tooBlob de SQL Server local au format CSV. toomake hello plus rapide de travail de copie, les fichiers CSV hello doivent être compressées bzip2 format.

**Test et analyse**: débit hello de l’activité de copie est inférieure à 2 Mbits/s, qui est beaucoup plus lent que le test d’évaluation des performances hello.

**Analyse des performances et paramétrage**: tootroubleshoot hello problème de performances, nous allons voir comment les données de hello sont traitées et déplacées.

1. **Lire les données**: passerelle ouvre une tooSQL connexion serveur et envoie hello la requête. SQL Server répond en envoyant tooGateway de flux de données hello via l’intranet de hello.
2. **Sérialiser et compresser les données**: passerelle sérialise le format de tooCSV de flux de données hello et compresse hello des flux de données tooa bzip2.
3. **Écrire des données**: passerelle télécharge hello bzip2 flux tooBlob de stockage via hello Internet.

Comme vous pouvez le voir, les données de hello sont traités et déplacés de manière séquentielle diffusion en continu : SQL Server > réseau > passerelle > WAN > stockage d’objets Blob. **Hello performances globales sont contrôlé par un débit minimal de hello sur le pipeline de hello**.

![Flux de données](./media/data-factory-copy-activity-performance/case-study-pic-1.png)

Un ou plusieurs des hello suivant facteurs peuvent provoquer des hello goulot d’étranglement :

* **Source :**SQL Server offre lui-même un faible débit en raison des charges lourdes.
* **Passerelle de gestion des données**:
  * **LAN**: passerelle se trouve loin d’être l’ordinateur SQL Server hello et dispose d’une connexion à faible bande passante.
  * **Passerelle**: passerelle a atteint son hello tooperform de limitations charge opérations suivantes :
    * **Sérialisation**: sérialisation tooCSV de flux de données hello format a débit lent.
    * **Compression**: vous avez choisi un codec de compression lent (par exemple, bzip2, c’est-à-dire 2,8 Mbits/s avec Core i7).
  * **WAN**: la bande passante hello entre le réseau d’entreprise de hello et vos services Azure est faible (par exemple, T1 = 1,544 Kbits/s ; T2 = Kbits/s 6,312).
* **Récepteur**: le stockage Blob a un faible débit. (Ce scénario est peu probable car son contrat SLA garantit un minimum de 60 Mbits/s.)

Dans ce cas, la compression des données bzip2 peut être ralentir pipeline entier de hello. Commutation codec de compression gzip tooa peut faciliter ce goulot d’étranglement.

## <a name="sample-scenarios-use-parallel-copy"></a>Exemples de scénarios : utilisation de la copie en parallèle
**Scénario i :** copier 1 000 fichiers de 1 Mo à partir du stockage de tooBlob hello local fichier système.

**Analyse et réglage des performances**: pour obtenir un exemple, si vous avez installé la passerelle sur un ordinateur quadricœur, Data Factory utilise 16 copies parallèles toomove fichiers de stockage de tooBlob de système de fichiers hello simultanément. Cette exécution parallèle doit aboutir à un débit élevé. Vous pouvez également explicitement spécifier nombre de copies parallèles hello. Lorsque vous copiez plusieurs petits fichiers, les copies parallèles aident considérablement le débit en utilisant les ressources plus efficacement.

![Scénario 1](./media/data-factory-copy-activity-performance/scenario-1.png)

**Scénario II**: copier des objets BLOB de 20 de 500 Mo de tooData de stockage d’objets Blob Lake Store Analytique et puis régler les performances.

**Analyse et réglage des performances**: dans ce scénario, la fabrique de données copie les données de hello à partir du magasin d’objets Blob stockage tooData Lake à l’aide de copie unique (**parallelCopies** définir too1) et des unités de déplacement des données unique-cloud. Hello débit vous observez va être toothat fermer décrite dans hello [section de référence des performances](#performance-reference).   

![Scénario 2](./media/data-factory-copy-activity-performance/scenario-2.png)

**Scénario III**: la taille des fichiers individuels est supérieure à des dizaines de mégaoctets et le volume total est important.

**Analyse et l’activation de performances**: augmentation **parallelCopies** ne produit pas de meilleures performances de copie en raison des limitations de ressources hello d’un DMU unique-cloud. Au lieu de cela, vous devez spécifier plus cloud DMUs tooget plusieurs ressources tooperform hello le déplacement des données. Ne spécifiez pas une valeur pour hello **parallelCopies** propriété. Fabrique de données gère le parallélisme de hello pour vous. Dans ce cas, si vous définissez **cloudDataMovementUnits** too4, un débit d’environ quatre fois survient.

![Scénario 3](./media/data-factory-copy-activity-performance/scenario-3.png)

## <a name="reference"></a>Référence
Analyse des performances et réglage des références pour certaines des magasins de données hello pris en charge sont :

* Azure Storage (le Stockage Blob et le Stockage Table) : [Objectifs d’évolutivité d’Azure Storage](../storage/common/storage-scalability-targets.md) et [Liste de contrôle des performances et de l’évolutivité d’Azure Storage](../storage/common/storage-performance-checklist.md)
* Base de données SQL Azure : Vous pouvez [surveiller les performances de hello](../sql-database/sql-database-single-database-monitor.md) et vérifie le pourcentage de l’unité (DTU) de transaction de base de données hello
* Azure SQL Data Warehouse : sa capacité est mesurée en Data Warehouse Units (DWU) ; voir [Gestion de la puissance de calcul dans Azure SQL Data Warehouse (Vue d’ensemble)](../sql-data-warehouse/sql-data-warehouse-manage-compute-overview.md)
* Azure Cosmos DB : [Niveaux de performances d’Azure Cosmos DB](../documentdb/documentdb-performance-levels.md)
* SQL Server local : [Surveillance et réglage des performances](https://msdn.microsoft.com/library/ms189081.aspx)
* Serveur de fichiers local : [Réglage des performances des serveurs de fichiers](https://msdn.microsoft.com/library/dn567661.aspx)
