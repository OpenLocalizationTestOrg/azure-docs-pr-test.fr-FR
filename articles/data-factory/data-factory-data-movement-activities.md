---
title: "aaaMove des données à l’aide de l’activité de copie | Documents Microsoft"
description: "Apprenez-en plus sur le déplacement des données dans les pipelines Data Factory : migration de données entre des magasins de cloud, entre des boutiques locales et cloud. Utiliser l’activité de copie."
keywords: "copier des données, déplacement des données, migration des données, transférer des données"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 67543a20-b7d5-4d19-8b5e-af4c1fd7bc75
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: 29b74154b9006795ead3b0ee9638a3dbf2c5d831
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-by-using-copy-activity"></a>Déplacer des données à l’aide de l’activité de copie
## <a name="overview"></a>Vue d'ensemble
Dans Azure Data Factory, vous pouvez utiliser les données de toocopy de l’activité de copie entre locaux et cloud banques de données. Après copie des données de hello, il peut être davantage transformée et analysée. Vous pouvez également utiliser la transformation toopublish de l’activité de copie et les résultats de l’analyse de décisionnel (BI) et la consommation de l’application.

![Rôle d’activité de copie](media/data-factory-data-movement-activities/copy-activity.png)

L’activité de copie est effectuée par un [service globalement disponible](#global)sécurisé, fiable et évolutif. Cet article fournit des détails sur le déplacement des données dans Data Factory et dans l’activité de copie.

Voyons d’abord comment la migration de données se produit entre deux banques de données cloud, et entre une banque de données locale et une banque de données cloud.

> [!NOTE]
> toolearn sur les activités en général, consultez [présentation des pipelines et activités](data-factory-create-pipelines.md).
>
>

### <a name="copy-data-between-two-cloud-data-stores"></a>Copie de données entre deux magasins de données cloud
Lorsque les magasins de données source et le récepteur sont dans le cloud de hello, l’activité de copie traverse hello suivant des données de toocopy d’étapes à partir de récepteur de toohello hello source. service Hello optimisant l’activité de copie :

1. Lit les données à partir du magasin de données source hello.
2. Effectue la sérialisation/désérialisation, la compression/décompression, le mappage de colonnes et la conversion de type sont effectués par la passerelle de gestion des données. Il effectue ces opérations en fonction des configurations hello du jeu de données d’entrée hello, dataset de sortie et l’activité de copie.
3. Écrit le magasin de données de destination toohello données.

service de Hello choisit automatiquement le déplacement des données hello région optimal tooperform hello. Cette zone est généralement hello un plus proche toohello récepteur magasin de données.

![Copie cloud-cloud](./media/data-factory-data-movement-activities/cloud-to-cloud.png)

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copie de données entre un magasin de données local et un magasin de données cloud
toosecurely déplacement des données entre une banque de données locale et un magasin de données cloud, installer la passerelle de gestion des données sur votre ordinateur local. La passerelle de gestion des données est un agent qui permet le traitement et le déplacement de données hybrides. Vous pouvez l’installer sur hello même ordinateur comme magasin de données de salutation lui-même ou sur un ordinateur distinct qui possède les accès toohello données à stocker.

Dans ce scénario, passerelle de gestion des données effectue hello sérialisation/désérialisation, la compression/décompression, mappage de colonne et de conversion de type. Données ne passent pas par le biais hello service Azure Data Factory. Au lieu de cela, passerelle de gestion des données écrit directement la banque de destination toohello hello données.

![Copie de type local vers cloud](./media/data-factory-data-movement-activities/onprem-to-cloud.png)

Consultez la page [Déplacement de données entre des sources locales et le cloud à l’aide de la passerelle de gestion des données](data-factory-move-data-between-onprem-and-cloud.md) pour une introduction et une procédure pas à pas. Pour obtenir des informations détaillées sur cet agent, consultez [Passerelle de gestion de données](data-factory-data-management-gateway.md) .

Vous pouvez également déplacer des données à partir de / stocke les données de toosupported qui sont hébergés sur Azure IaaS virtual machines virtuelles à l’aide de passerelle de gestion des données. Dans ce cas, vous pouvez installer la passerelle de gestion des données sur hello même machine virtuelle comme magasin de données de salutation lui-même ou sur une machine virtuelle distincte qui a accès toohello données à stocker.

## <a name="supported-data-stores-and-formats"></a>Banques de données et formats pris en charge
Activité de copie dans la fabrique de données copie des données à partir d’un magasin de données de source données magasin tooa récepteur. Fabrique de données prend en charge hello suivant des magasins de données. Données à partir de n’importe quelle source peuvent être écrites tooany récepteur. Cliquez sur un toolearn de magasin de données comment tooand de données toocopy de ce magasin.

> [!NOTE] 
> Si vous avez besoin de données toomove vers/depuis un magasin de données qui ne gère pas l’activité de copie, utilisez un **activité personnalisée** dans la fabrique de données avec votre propre logique pour la copie/déplacement de données. Pour plus d’informations sur la création et l’utilisation d’une activité personnalisée, consultez [Utilisation des activités personnalisées dans un pipeline Azure Data Factory](data-factory-use-custom-activities.md).

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

> [!NOTE]
> Stocke des données avec * peut être local ou sur Azure IaaS et vous obligent tooinstall [passerelle de gestion des données](data-factory-data-management-gateway.md) sur un ordinateur de IaaS Azure/le local.

### <a name="supported-file-formats"></a>Formats de fichiers pris en charge
Vous pouvez utiliser l’activité de copie trop**copier les fichiers en tant que-est** entre deux fichiers banques de données, vous pouvez ignorer hello [format section](data-factory-create-datasets.md) dans à la fois hello d’entrée et de sortie des définitions de jeu de données. les données de salutation sont copiées efficacement sans toute sérialisation/désérialisation.

Activité de copie également lit et écrit toofiles dans des formats spécifiés : **texte JSON, Avro, ORC et Parquet**et codec de compression **GZip, Deflate, BZip2 et ZipDeflate** sont pris en charge. Pour plus d’informations, consultez [Formats de fichier et de compression pris en charge](data-factory-supported-file-and-compression-formats.md).

Par exemple, vous pouvez ainsi copier des activités suivantes de hello :

* Copiez les données locale SQL Server et d’écriture tooAzure Data Lake Store dans un format ORC.
* Copiez les fichiers au format texte (CSV) du système de fichiers local et d’écriture tooAzure Blob dans le format Avro.
* Copier des fichiers à partir du système de fichiers local et décompresser puis terres tooAzure Data Lake Store.
* Copier des données au format de texte compressé (CSV) GZip d’objets Blob Azure et d’écriture tooAzure base de données SQL.

## <a name="global"></a>Déplacement des données disponible globalement
Azure Data Factory est disponible uniquement dans les régions Europe du Nord, est des États-Unis et ouest des États-Unis hello. Toutefois, le service hello optimisant l’activité de copie est disponible globalement dans hello suivant des régions et des zones géographiques différentes. topologie de globalement disponible Hello garantit le déplacement des données efficace qui généralement évite de sauts entre régions. Consultez la section [Services par région](https://azure.microsoft.com/regions/#services) pour connaître la disponibilité de Data Factory et du déplacement des données dans une région.

### <a name="copy-data-between-cloud-data-stores"></a>Copier des données entre des banques de données cloud
Lorsque les magasins de données source et le récepteur sont dans le cloud de hello, Data Factory utilise un déploiement de service dans la région de hello est le plus proche de récepteur toohello Bonjour mêmes données de hello toomove geography. Consultez toohello tableau pour le mappage suivant :

| Geography hello destination de banques de données | Région de la banque de données de destination hello | Région utilisée pour le déplacement des données |
|:--- |:--- |:--- |
| États-Unis | Est des États-Unis | Est des États-Unis |
| &nbsp; | Est des États-Unis 2 | Est des États-Unis 2 |
| &nbsp; | Centre des États-Unis | Centre des États-Unis |
| &nbsp; | États-Unis - partie centrale septentrionale | États-Unis - partie centrale septentrionale |
| &nbsp; | Centre-Sud des États-Unis | États-Unis - partie centrale méridionale |
| &nbsp; | Centre-Ouest des États-Unis | Centre-Ouest des États-Unis |
| &nbsp; | Ouest des États-Unis | Ouest des États-Unis |
| &nbsp; | Ouest des États-Unis 2 | Ouest des États-Unis |
| Canada | Est du Canada | Centre du Canada |
| &nbsp; | Centre du Canada | Centre du Canada |
| Brésil | Sud du Brésil | Sud du Brésil |
| Europe | Europe du Nord | Europe du Nord |
| &nbsp; | Europe de l'Ouest | Europe de l'Ouest |
| Royaume-Uni | Ouest du Royaume-Uni | Sud du Royaume-Uni |
| &nbsp; | Sud du Royaume-Uni | Sud du Royaume-Uni |
| Asie-Pacifique | Asie du Sud-Est | Asie du Sud-Est |
| &nbsp; | Est de l'Asie | Asie du Sud-Est |
| Australie | Est de l’Australie | Est de l’Australie |
| &nbsp; | Sud-est de l’Australie | Sud-Est de l’Australie |
| Japon | Est du Japon | Est du Japon |
| &nbsp; | Ouest du Japon | Est du Japon |
| Inde | Inde centrale | Inde centrale |
| &nbsp; | Inde occidentale | Inde centrale |
| &nbsp; | Inde du Sud | Inde centrale |

Ou bien, vous pouvez indiquer explicitement tooperform hello copie la zone de hello de toobe de service de fabrique de données utilisée en spécifiant `executionLocation` propriété sous l’activité de copie `typeProperties`. Les valeurs prises en charge pour cette propriété sont énumérées dans la colonne **Région utilisée pour le déplacement des données** ci-dessus. Notez que vos données parcourt cette région acheminement hello pendant la copie. Par exemple, toocopy entre Azure stocke en Corée, vous pouvez spécifier `"executionLocation": "Japan East"` tooroute via Japon (consultez [exemple JSON](#by-using-json-scripts) en tant que référence).

> [!NOTE]
> Si région hello hello destination du magasin de données n’est pas dans la liste précédente ou indétectables, par défaut l’activité de copie échoue, au lieu de passer par une autre région, sauf si `executionLocation` est spécifié. liste des régions Hello pris en charge est développée au fil du temps.
>

### <a name="copy-data-between-an-on-premises-data-store-and-a-cloud-data-store"></a>Copie de données entre un magasin de données local et un magasin de données cloud
Lorsque les données sont copiées entre l’instance locale (ou une machine virtuelle Azure/IaaS) et l’instance cloud, le déplacement des données est effectué par la [passerelle de gestion des données](data-factory-data-management-gateway.md) sur un ordinateur local ou une machine virtuelle IaaS Azure. les données de salutation ne transmet pas via service hello dans le cloud de hello, sauf si vous utilisez hello [intermédiaire copie](data-factory-copy-activity-performance.md#staged-copy) fonctionnalité. Dans ce cas, les données circulent dans hello mise en lots de stockage d’objets Blob Azure avant de les écrire dans le magasin de données récepteur hello.

## <a name="create-a-pipeline-with-copy-activity"></a>Créer un pipeline avec une activité de copie
Vous pouvez créer un pipeline avec une activité de copie de plusieurs façons :

### <a name="by-using-hello-copy-wizard"></a>À l’aide d’Assistant copie de hello
Hello Assistant copie de fabrique de données vous aide à toocreate un pipeline avec l’activité de copie. Ce pipeline vous permet de toocopy des données à partir des sources prises en charge toodestinations *sans écrire de JSON* définitions pour les services liés, les datasets et les pipelines. Consultez [Assistant copie de fabrique de données](data-factory-copy-wizard.md) pour plus d’informations sur l’Assistant de hello.  

### <a name="by-using-json-scripts"></a>Avec utilisation de scripts JSON
Vous pouvez utiliser éditeur Data Factory dans hello portail Azure, Visual Studio ou Azure PowerShell toocreate une définition JSON pour un pipeline (à l’aide de l’activité de copie). Ensuite, vous pouvez la déployer pipeline hello toocreate Data Factory. Consultez le [Didacticiel : Utilisation de l’activité de copie dans un pipeline Azure Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour connaître les instructions des procédures pas à pas.    

Les propriétés JSON (le nom, la description, les tables d'entrée et de sortie et les différentes stratégies) sont disponibles pour tous les types d'activités. Les propriétés qui sont disponibles dans hello `typeProperties` section d’activité hello varient selon chaque type d’activité.

Pour l’activité de copie, hello `typeProperties` section varie en fonction des types hello des sources et récepteurs. Cliquez sur un source/récepteur Bonjour [prise en charge des sources et récepteurs](#supported-data-stores-and-formats) toolearn section sur les propriétés de type activité de copie prend en charge pour ce magasin de données.

Voici un exemple de définition JSON :

```json
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from Azure blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "type": "Copy",
        "inputs": [
          {
            "name": "InputBlobTable"
          }
        ],
        "outputs": [
          {
            "name": "OutputSQLTable"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink"
          },
          "executionLocation": "Japan East"          
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2016-07-12T00:00:00Z",
    "end": "2016-07-13T00:00:00Z"
  }
}
```
planification de Hello est définie dans hello sortie dataset détermine quand l’activité hello s’exécute (par exemple : **quotidienne**, fréquence que **jour**et l’intervalle **1**). Hello activité de copie des données à partir d’un jeu de données d’entrée (**source**) jeu de données de sortie tooan (**récepteur**).

Vous pouvez spécifier plus d’un jeu de données d’entrée tooCopy activité. Ils sont utilisés tooverify hello dépendances avant l’exécution d’activité hello. Toutefois, uniquement les données de salutation hello le premier jeu de données sont copiée toohello destination dataset. Pour plus d’informations, consultez [Planification et exécution](data-factory-scheduling-and-execution.md).  

## <a name="performance-and-tuning"></a>Performances et réglage
Consultez hello [l’activité de copie guide des performances et paramétrage](data-factory-copy-activity-performance.md), qui décrit les principaux facteurs qui affectent les performances de hello de transfert de données (activité de copie) dans Azure Data Factory. Également, il répertorie hello observé les performances lors des tests internes et présente des performances de hello toooptimize manières d’activité de copie.

## <a name="fault-tolerance"></a>Tolérance de panne
Par défaut, l’activité de copie s’arrête la copie des données et retourner l’échec lorsque rencontrent des données incompatibles entre source et le récepteur ; Vous pouvez configurer explicitement tooskip et lignes incompatible de journal hello et copie uniquement ces la copie des données compatibles toomake hello a réussi. Consultez hello [la tolérance de panne de l’activité de copie](data-factory-copy-activity-fault-tolerance.md) sur plus de détails.

## <a name="security-considerations"></a>Considérations relatives à la sécurité
Consultez hello [considérations de sécurité](data-factory-data-movement-security-considerations.md), qui décrit l’infrastructure de sécurité que les services de déplacement des données dans Azure Data Factory utiliser toosecure vos données.

## <a name="scheduling-and-sequential-copy"></a>Planification et copie séquentielle
Consultez [Planification et exécution](data-factory-scheduling-and-execution.md) pour plus d’informations sur le fonctionnement de la planification et de l’exécution dans Data Factory. Il est possible de toorun plusieurs opérations de copie une après l’autre de manière séquentielle/classés. Consultez hello [copier de manière séquentielle](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline) section.

## <a name="type-conversions"></a>Conversions des types
Les magasins de données ont différents types de systèmes natifs. Activité de copie effectue des conversions de type automatique à partir de types de sources de toosink types avec hello suivant l’approche en deux étapes :

1. Convertir à partir du type de source native types tooa .NET.
2. Convertir à partir d’un type de récepteur native de tooa de type .NET.

mappage de Hello à partir d’un type .NET de type natif système tooa pour un magasin de données est dans un article de magasin de données respectifs hello. (Cliquez sur le lien spécifique de hello Bonjour [prise en charge des magasins de données](#supported-data-stores) table). Vous pouvez utiliser ces types appropriés de mappages toodetermine lors de la création de vos tables, afin que l’activité de copie effectue des conversions de droite hello.

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur hello activité de copie plus, consultez [copier les données d’objets Blob Azure storage tooAzure de base de données SQL](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
* toolearn sur le déplacement des données à partir d’une banque de données locale données magasin tooa cloud, consultez [déplacer des données à partir de banques de données locales toocloud](data-factory-move-data-between-onprem-and-cloud.md).
