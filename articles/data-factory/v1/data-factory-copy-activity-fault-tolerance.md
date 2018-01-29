---
title: "Ajouter une tolérance de panne de l’activité de copie dans Azure Data Factory en ignorant les lignes incompatibles | Microsoft Docs"
description: "Découvrez comment ajouter une tolérance de panne de l’activité de copie dans Azure Data Factory en ignorant les lignes incompatibles durant la copie"
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/05/2018
ms.author: jingwang
robots: noindex
ms.openlocfilehash: 6e7923e2e0a23f22f7dff8c316050a1757310456
ms.sourcegitcommit: 9a8b9a24d67ba7b779fa34e67d7f2b45c941785e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/08/2018
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Ajouter une tolérance de panne de l’activité de copie en ignorant les lignes incompatibles
> [!NOTE]
> Cet article s’applique à la version 1 de Data factory, qui est généralement disponible (GA). Si vous utilisez la version 2 du service Data Factory, qui est en préversion, consultez [fault tolerance in copy activity of Data Factory version 2](../copy-activity-fault-tolerance.md) (Tolérance de panne de l’activité de copie dans Data Factory version 2).

Avec l’[activité de copie](data-factory-data-movement-activities.md) dans Azure Data Factory, vous avez deux moyens de traiter les lignes incompatibles lors de la copie de données entre les magasins de données source et récepteur :

- Vous pouvez abandonner et laisser en échec l’activité de copie en cas de détection de données incompatibles (comportement par défaut).
- Vous pouvez continuer à copier toutes les données en ajoutant une tolérance de panne et en ignorant les lignes de données incompatibles. Vous avez également la possibilité de journaliser les lignes incompatibles dans le stockage Blob Azure afin de pouvoir examiner la cause de l’échec dans le journal, corriger les données sur la source de données, puis effectuer une nouvelle tentative de copie.

## <a name="supported-scenarios"></a>Scénarios pris en charge
L’activité de copie offre la possibilité de détecter, d’ignorer et de journaliser les incompatibilités de données suivantes :

- **Incompatibilité entre le type de données sources et le type natif récepteur**

    Exemple : copie de données d’un fichier CSV du stockage Blob Azure dans une base de données SQL avec une définition de schéma contenant trois colonnes de type **INT**. Les lignes du fichier CSV qui contiennent des données numériques, telles que `123,456,789`, sont correctement copiées dans le magasin récepteur. En revanche, les lignes qui contiennent des valeurs non numériques, telles que `123,456,abc`, sont considérées comme incompatibles et ignorées.

- **Incompatibilité du nombre de colonnes entre la source et le récepteur**

    Exemple : copie de données d’un fichier CSV du stockage Blob Azure dans une base de données SQL avec une définition de schéma contenant six colonnes. Les lignes du fichier CSV qui contiennent six colonnes sont correctement copiées dans le magasin récepteur. Les lignes du fichier CSV qui contiennent plus ou moins de six colonnes sont considérées comme incompatibles et ignorées.

- **Violation de clé primaire lors de l’écriture dans une base de données relationnelle**

    Exemple : copie de données depuis un serveur SQL dans une base de données SQL. Il existe une clé primaire définie dans la base de données SQL réceptrice, mais aucune clé primaire correspondante n’est définie dans le serveur SQL source. Les lignes en double qui peuvent exister dans la source ne sont pas copiées dans le récepteur. L’activité de copie ne copie que la première ligne des données sources dans le récepteur. Toutes les lignes sources suivantes contenant une valeur de clé primaire en double sont considérées comme incompatibles et ignorées.

>[!NOTE]
>Cette fonctionnalité ne s’applique pas quand l’activité de copie est configurée pour appeler un mécanisme de chargement de données externes, comme [Azure SQL Data Warehouse PolyBase](data-factory-azure-sql-data-warehouse-connector.md#use-polybase-to-load-data-into-azure-sql-data-warehouse) ou [Amazon Redshift Unload](data-factory-amazon-redshift-connector.md#use-unload-to-copy-data-from-amazon-redshift). Pour charger des données dans SQL Data Warehouse avec PolyBase, utilisez la prise en charge native de la tolérance de panne de PolyBase en spécifiant « [polyBaseSettings](data-factory-azure-sql-data-warehouse-connector.md#sqldwsink) » dans l’activité de copie.

## <a name="configuration"></a>Configuration
L’exemple suivant fournit une définition JSON pour configurer la manière d’ignorer les lignes incompatibles dans le cadre de l’activité de copie :

```json
"typeProperties": {
    "source": {
        "type": "BlobSource"
    },
    "sink": {
        "type": "SqlSink",
    },         
    "enableSkipIncompatibleRow": true,           
    "redirectIncompatibleRowSettings": {
        "linkedServiceName": "BlobStorage",
        "path": "redirectcontainer/erroroutput"
    }
}
```

| Propriété | DESCRIPTION | Valeurs autorisées | Obligatoire |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Activer ou non l’option d’ignorer les lignes incompatibles. | True<br/>False (valeur par défaut) | Non  |
| **redirectIncompatibleRowSettings** | Groupe de propriétés qui peuvent être spécifiées lorsque vous souhaitez journaliser les lignes incompatibles. | &nbsp; | Non  |
| **linkedServiceName** | Service lié de Stockage Azure pour stocker le journal contenant les lignes ignorées. | Nom d’un service lié [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) faisant référence à l’instance de stockage que vous souhaitez utiliser pour stocker le fichier journal. | Non  |
| **path** | Chemin d’accès du fichier journal contenant les lignes ignorées. | Spécifiez le chemin d’accès sur Stockage Blob que vous souhaitez utiliser pour journaliser les données incompatibles. Si vous ne spécifiez pas le chemin d’accès, le service crée un conteneur à votre place. | Non  |

## <a name="monitoring"></a>Surveillance
Une fois l’exécution de l’activité de copie terminée, vous pouvez voir le nombre de lignes ignorées dans la section Surveillance :

![Le système de surveillance a ignoré les lignes incompatibles](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Si vous configurez la journalisation des lignes incompatibles, le chemin d’accès du fichier journal est le suivant : `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv`. Vous pourrez y vérifier les lignes qui ont été ignorées et la cause racine de l’incompatibilité.

Les données d’origine et l’erreur correspondante sont consignées dans le fichier journal. Voici un exemple de contenu de fichier journal :
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' to type 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. The duplicate key value is (data4).
```

## <a name="next-steps"></a>étapes suivantes
Pour en savoir plus sur l’activité de copie dans Azure Data Factory, voir [Déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md).
