---
title: "Copier des données de MariaDB avec Azure Data Factory | Microsoft Docs"
description: "Découvrez comment utiliser l’activité de copie pour copier des données de MariaDB vers des magasins de données récepteurs pris en charge dans le cadre d’un pipeline Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/30/2017
ms.author: jingwang
ms.openlocfilehash: 34942a079d4ae132535806a11db4476bf28aa55c
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-mariadb-using-azure-data-factory"></a>Copier des données de MariaDB avec Azure Data Factory 

Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour copier des données de MariaDB. Il s’appuie sur l’article [Vue d’ensemble de l’activité de copie](copy-activity-overview.md).

> [!NOTE]
> Cet article s’applique à la version 2 de Data Factory, actuellement en préversion. Si vous utilisez la version 1 du service Data Factory, qui est en disponibilité générale, voir [Activité de copie dans V1](v1/data-factory-data-movement-activities.md).

## <a name="supported-capabilities"></a>Fonctionnalités prises en charge

Vous pouvez copier des données de MariaDB vers n’importe quel magasin de données récepteur pris en charge. Pour obtenir la liste des banques de données prises en charge en tant que sources ou récepteurs par l’activité de copie, consultez le tableau [Banques de données prises en charge](copy-activity-overview.md#supported-data-stores-and-formats).

Azure Data Factory fournit un pilote intégré qui permet la connexion. Vous n’avez donc pas besoin d’installer manuellement un pilote à l’aide de ce connecteur.

Ce connecteur prend actuellement en charge les versions de MariaDB antérieures à 10.2.

## <a name="getting-started"></a>Prise en main

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

Les sections suivantes donnent des précisions sur les propriétés utilisées pour définir des entités Data Factory propres au connecteur MariaDB.

## <a name="linked-service-properties"></a>Propriétés du service lié

Les propriétés suivantes sont prises en charge pour le service lié MariaDB :

| Propriété | DESCRIPTION | Obligatoire |
|:--- |:--- |:--- |
| Type | La propriété type doit être définie sur **MariaDB**. | OUI |
| connectionString | Chaîne de connexion ODBC permettant de se connecter à MariaDB. Vous pouvez choisir de marquer ce champ comme SecureString pour le stocker en toute sécurité dans le fichier de définition d’application, ou stocker le mot de passe dans Azure Key Vault et laisser l’activité de copie en tirer (pull) les données lors de la copie. Pour plus d’informations, consultez la page [Stocker des informations d’identification dans Key Vault](store-credentials-in-key-vault.md). | OUI |
| connectVia | [Runtime d’intégration](concepts-integration-runtime.md) à utiliser pour la connexion à la banque de données. Vous pouvez utiliser un runtime d’intégration auto-hébergé ou un runtime d’intégration Azure (si votre banque de données est accessible publiquement). À défaut de spécification, le runtime d’intégration Azure par défaut est utilisé. |Non  |

**Exemple :**

```json
{
    "name": "MariaDBLinkedService",
    "properties": {
        "type": "MariaDB",
        "typeProperties": {
            "connectionString": {
                 "type": "SecureString",
                 "value": "Server=<host>;Port=<port>;Database=<database>;UID=<user name>;PWD=<password>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données

Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article sur les [jeux de données](concepts-datasets-linked-services.md). Cette section donne la liste des propriétés prises en charge par le jeu de données MariaDB.

Pour copier des données de MariaDB, affectez la valeur **MariaDBTable** à la propriété type du jeu de données. Il n’y a aucune autre propriété propre au type dans cette sorte de jeu de données.

**Exemple**

```json
{
    "name": "MariaDBDataset",
    "properties": {
        "type": "MariaDBTable",
        "linkedServiceName": {
            "referenceName": "<MariaDB linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie

Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Pipelines](concepts-pipelines-activities.md). Cette section donne la liste des propriétés prises en charge par la source MariaDB.

### <a name="mariadbsource-as-source"></a>MariaDBSource comme source

Pour copier des données de MariaDB, affectez la valeur **MariaDBSource** au type source de l’activité de copie. Les propriétés prises en charge dans la section **source** de l’activité de copie sont les suivantes :

| Propriété | DESCRIPTION | Obligatoire |
|:--- |:--- |:--- |
| Type | La propriété type de la source de l’activité de copie doit être définie sur **MariaDBSource**. | OUI |
| query | Utiliser la requête SQL personnalisée pour lire les données. Par exemple : `"SELECT * FROM MyTable"`. | OUI |

**Exemple :**

```json
"activities":[
    {
        "name": "CopyFromMariaDB",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<MariaDB input dataset name>",
                "type": "DatasetReference"
            }
        ],
        "outputs": [
            {
                "referenceName": "<output dataset name>",
                "type": "DatasetReference"
            }
        ],
        "typeProperties": {
            "source": {
                "type": "MariaDBSource",
                "query": "SELECT * FROM MyTable"
            },
            "sink": {
                "type": "<sink type>"
            }
        }
    }
]
```

## <a name="next-steps"></a>étapes suivantes
Pour obtenir la liste des banques de données prises en charge en tant que sources et récepteurs par l’activité de copie dans Azure Data Factory, consultez le tableau [banques de données prises en charge](copy-activity-overview.md#supported-data-stores-and-formats).
