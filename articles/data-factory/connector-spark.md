---
title: "Copier des données de Spark avec Azure Data Factory | Microsoft Docs"
description: "Découvrez comment utiliser l’activité de copie pour copier des données de Spark vers des magasins de données récepteurs pris en charge dans le cadre d’un pipeline Azure Data Factory."
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
ms.openlocfilehash: 0107c0e02e7158ad73671ae8e4599e1e998f20fc
ms.sourcegitcommit: be9a42d7b321304d9a33786ed8e2b9b972a5977e
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/19/2018
---
# <a name="copy-data-from-spark-using-azure-data-factory"></a>Copier des données de Spark avec Azure Data Factory 

Cet article explique comment utiliser l’activité de copie dans Azure Data Factory pour copier des données de Spark. Il s’appuie sur l’article [Vue d’ensemble de l’activité de copie](copy-activity-overview.md).

> [!NOTE]
> Cet article s’applique à la version 2 de Data Factory, actuellement en préversion. Si vous utilisez la version 1 du service Data Factory, qui est en disponibilité générale, voir [Activité de copie dans V1](v1/data-factory-data-movement-activities.md).


## <a name="supported-capabilities"></a>Fonctionnalités prises en charge

Vous pouvez copier des données de Spark vers n’importe quel magasin de données récepteur pris en charge. Pour obtenir la liste des banques de données prises en charge en tant que sources ou récepteurs par l’activité de copie, consultez le tableau [Banques de données prises en charge](copy-activity-overview.md#supported-data-stores-and-formats).

Azure Data Factory fournit un pilote intégré qui permet la connexion. Vous n’avez donc pas besoin d’installer manuellement un pilote à l’aide de ce connecteur.

## <a name="getting-started"></a>Prise en main

[!INCLUDE [data-factory-v2-connector-get-started-2](../../includes/data-factory-v2-connector-get-started-2.md)]

Les sections suivantes donnent des précisions sur les propriétés utilisées pour définir des entités Data Factory propres au connecteur Spark.

## <a name="linked-service-properties"></a>Propriétés du service lié

Les propriétés suivantes sont prises en charge pour le service lié Spark :

| Propriété | DESCRIPTION | Obligatoire |
|:--- |:--- |:--- |
| Type | La propriété type doit être définie sur **Spark**. | OUI |
| host | Adresse IP ou nom d’hôte du serveur Spark.  | OUI |
| port | Port TCP utilisé par le serveur Spark pour écouter les connexions clientes.  | OUI |
| serverType | Type de serveur Spark. <br/>Valeurs autorisées : **SharkServer**, **SharkServer2**, **SparkThriftServer**. | Non  |
| thriftTransportProtocol | Protocole de transport à utiliser dans la couche Thrift. <br/>Valeurs autorisées : **Binary**, **SASL**, **HTTP ** | Non  |
| authenticationType | Méthode d’authentification utilisée pour accéder au serveur Spark. <br/>Valeurs autorisées : **Anonymous**, **Username**, **UsernameAndPassword**, **WindowsAzureHDInsightService** | OUI |
| username | Nom d’utilisateur utilisé pour accéder au serveur Spark.  | Non  |
| password | Mot de passe correspondant au nom d’utilisateur indiqué dans le champ username. Vous pouvez choisir de marquer ce champ comme SecureString pour le stocker en toute sécurité dans le fichier de définition d’application, ou stocker le mot de passe dans Azure Key Vault et laisser l’activité de copie en tirer (pull) les données durant la copie. Pour plus d’informations, consultez [Stocker des informations d’identification dans Key Vault](store-credentials-in-key-vault.md). | Non  |
| httpPath | URL partielle correspondant au serveur Spark.  | Non  |
| enableSsl | Indique si les connexions au serveur sont chiffrées suivant le protocole SSL. La valeur par défaut est false.  | Non  |
| trustedCertPath | Chemin d’accès complet du fichier .pem contenant les certificats d’autorité de certification approuvés permettant de vérifier le serveur en cas de connexion via SSL. Cette propriété n’est disponible que si le protocole SSL est utilisé sur un runtime d’intégration auto-hébergé. Valeur par défaut : le fichier cacerts.pem installé avec le runtime d’intégration.  | Non  |
| useSystemTrustStore | Indique s’il faut utiliser un certificat d’autorité de certification provenant du magasin de confiance du système ou d’un fichier PEM spécifié. La valeur par défaut est false.  | Non  |
| allowHostNameCNMismatch | Indique si le nom du certificat SSL émis par l’autorité de certification doit correspondre au nom d’hôte du serveur en cas de connexion SSL. La valeur par défaut est false.  | Non  |
| allowSelfSignedServerCert | Indique si les certificats auto-signés provenant du serveur sont autorisés ou non. La valeur par défaut est false.  | Non  |
| connectVia | [Runtime d’intégration](concepts-integration-runtime.md) à utiliser pour la connexion à la banque de données. Vous pouvez utiliser un runtime d’intégration auto-hébergé ou un runtime d’intégration Azure (si votre banque de données est accessible publiquement). À défaut de spécification, le runtime d’intégration Azure par défaut est utilisé. |Non  |

**Exemple :**

```json
{
    "name": "SparkLinkedService",
    "properties": {
        "type": "Spark",
        "typeProperties": {
            "host" : "<cluster>.azurehdinsight.net",
            "port" : "<port>",
            "authenticationType" : "WindowsAzureHDInsightService",
            "username" : "<username>",
            "password": {
                 "type": "SecureString",
                 "value": "<password>"
            },
            "httpPath" : "gateway/sandbox/spark"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriétés du jeu de données

Pour obtenir la liste complète des sections et propriétés disponibles pour la définition de jeux de données, consultez l’article sur les [jeux de données](concepts-datasets-linked-services.md). Cette section donne la liste des propriétés prises en charge par le jeu de données Spark.

Pour copier des données de Spark, affectez la valeur **SparkObject** à la propriété type du jeu de données. Il n’y a aucune autre propriété propre au type dans cette sorte de jeu de données.

**Exemple**

```json
{
    "name": "SparkDataset",
    "properties": {
        "type": "SparkObject",
        "linkedServiceName": {
            "referenceName": "<Spark linked service name>",
            "type": "LinkedServiceReference"
        }
    }
}
```

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie

Pour obtenir la liste complète des sections et des propriétés disponibles pour la définition des activités, consultez l’article [Pipelines](concepts-pipelines-activities.md). Cette section donne la liste des propriétés prises en charge par la source Spark.

### <a name="sparksource-as-source"></a>SparkSource comme source

Pour copier des données de Spark, affectez la valeur **SparkSource** au type source de l’activité de copie. Les propriétés prises en charge dans la section **source** de l’activité de copie sont les suivantes :

| Propriété | DESCRIPTION | Obligatoire |
|:--- |:--- |:--- |
| Type | La propriété type de la source de l’activité de copie doit être définie sur **SparkSource**. | OUI |
| query | Utiliser la requête SQL personnalisée pour lire les données. Par exemple : `"SELECT * FROM MyTable"`. | OUI |

**Exemple :**

```json
"activities":[
    {
        "name": "CopyFromSpark",
        "type": "Copy",
        "inputs": [
            {
                "referenceName": "<Spark input dataset name>",
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
                "type": "SparkSource",
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
