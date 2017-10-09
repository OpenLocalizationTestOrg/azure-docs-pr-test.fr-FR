---
title: "la tolérance de panne aaaAdd dans l’activité de copie de fabrique de données Azure en ignorant les lignes incompatible | Documents Microsoft"
description: "Découvrez comment tooadd la tolérance de pannes dans l’activité de copie de fabrique de données Azure en ignorant les lignes incompatible pendant la copie"
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
ms.date: 07/19/2017
ms.author: jingwang
ms.openlocfilehash: e7cf6117655910844b292d340674d8d631450a81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-fault-tolerance-in-copy-activity-by-skipping-incompatible-rows"></a>Ajouter une tolérance de panne de l’activité de copie en ignorant les lignes incompatibles

Azure Data Factory [l’activité de copie](data-factory-data-movement-activities.md) offre des lignes de deux façons toohandle incompatibles lors de la copie des données entre les magasins de données source et le récepteur :

- Vous pouvez abandonner et Échec de copie de hello activité lorsque des données incompatibles sont rencontré (comportement par défaut).
- Vous pouvez continuer toocopy toutes les données hello en ajoutant une tolérance de panne et de lignes de données incompatibles ont été ignorées. En outre, vous pouvez consigner les lignes incompatible hello dans le stockage d’objets Blob Azure. Vous pouvez examiner hello journal toolearn hello cause de l’échec de hello, corriger les données de salutation sur la source de données hello, puis recommencez l’activité de copie hello.

## <a name="supported-scenarios"></a>Scénarios pris en charge
L’activité de copie offre la possibilité de détecter, d’ignorer et de journaliser les incompatibilités de données suivantes :

- **Incompatibilité entre le type de données source hello et un type natif hello récepteur**

    Par exemple : copier des données à partir d’un fichier CSV dans tooa de stockage d’objets Blob SQL de base de données avec une définition de schéma qui contient trois **INT** colonnes de type. Hello des lignes de fichier CSV qui contiennent des données numériques, tels que `123,456,789` sont copiés correctement magasin de récepteur toohello. Hello, toutefois, les lignes qui contiennent des valeurs non numériques, tels que `123,456,abc` sont détectés comme étant incompatibles et sont ignorés.

- **Incohérence entre le nombre de hello des colonnes de la source de hello et récepteur de hello**

    Par exemple : copier des données à partir d’un fichier CSV dans tooa de stockage d’objets Blob SQL de base de données avec une définition de schéma qui contient les six colonnes. Hello fichier CSV sont des lignes qui contiennent les six colonnes copiées magasin de récepteur toohello. lignes de fichier CSV Hello qui contiennent plus ou moins de six colonnes sont détectés comme étant incompatible et sont ignorés.

- **Violation de clé primaire lors de l’écriture de base de données relationnelle tooa**

    Par exemple : copier des données d’une base de données SQL server tooa SQL. Une clé primaire est définie dans la base de données SQL de récepteur hello, mais aucun ce type de clé primaire n’est définie dans SQL server de la source hello. lignes Hello dupliqué existent dans la source de hello ne peut pas être copié toohello récepteur. Activité de copie copie uniquement hello première ligne de source de données hello dans récepteur de hello. Hello source suivantes les lignes qui contiennent la valeur de clé primaire dupliquée de hello sont détectés comme étant incompatible et sont ignorés.

## <a name="configuration"></a>Configuration
Hello exemple suivant fournit une tooconfigure de définition JSON hello des lignes incompatible dans l’activité de copie ont été ignorées :

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

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| **enableSkipIncompatibleRow** | Activer ou non l’option d’ignorer les lignes incompatibles. | true<br/>False (valeur par défaut) | Non |
| **redirectIncompatibleRowSettings** | Un groupe de propriétés qui peuvent être spécifiées lorsque vous souhaitez que les lignes de toolog hello incompatible. | &nbsp; | Non |
| **linkedServiceName** | service Hello lié de stockage Azure toostore hello journal contenant les lignes hello ignorée. | nom Hello d’un [AzureStorage](data-factory-azure-blob-connector.md#azure-storage-linked-service) ou [AzureStorageSas](data-factory-azure-blob-connector.md#azure-storage-sas-linked-service) service, qui fait référence toohello instance de stockage que vous souhaitez le fichier journal de toouse toostore hello lié. | Non |
| **path** | chemin d’accès de Hello du fichier journal hello contenant hello ignorée lignes. | Spécifier le chemin de stockage d’objets Blob hello toouse toolog hello des données incompatibles. Si vous ne fournissez pas un chemin d’accès, le service de hello crée un conteneur pour vous. | Non |

## <a name="monitoring"></a>Surveillance
Après la fin de l’activité de copie de hello exécuter, vous pouvez voir le nombre hello des lignes ignorées Bonjour section analyse :

![Le système de surveillance a ignoré les lignes incompatibles](./media/data-factory-copy-activity-fault-tolerance/skip-incompatible-rows-monitoring.png)

Si vous configurez des lignes de toolog hello incompatibles, vous pouvez trouver le fichier de journal de hello à ce chemin d’accès : `https://[your-blob-account].blob.core.windows.net/[path-if-configured]/[copy-activity-run-id]/[auto-generated-GUID].csv` dans le fichier journal de hello, vous pouvez voir hello les lignes qui ont été ignorés et hello l’origine du problème d’incompatibilité de hello.

Les données d’origine hello et erreur correspondante de hello sont enregistrés dans le fichier de hello. Un exemple de contenu du fichier journal hello est comme suit :
```
data1, data2, data3, UserErrorInvalidDataValue,Column 'Prop_2' contains an invalid value 'data3'. Cannot convert 'data3' tootype 'DateTime'.,
data4, data5, data6, Violation of PRIMARY KEY constraint 'PK_tblintstrdatetimewithpk'. Cannot insert duplicate key in object 'dbo.tblintstrdatetimewithpk'. hello duplicate key value is (data4).
```

## <a name="next-steps"></a>Étapes suivantes
toolearn en savoir plus sur l’activité de copie de fabrique de données de Azure, consultez [déplacer des données à l’aide de l’activité de copie](data-factory-data-movement-activities.md).
