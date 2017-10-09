---
title: "données aaaMove local HDFS | Documents Microsoft"
description: "Découvrez comment toomove des données à partir de local HDFS à l’aide d’Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 3215b82d-291a-46db-8478-eac1a3219614
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 96387e5dd089099fc2e983ab26d67c2044b973b0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-on-premises-hdfs-using-azure-data-factory"></a>Transfert de données à partir d’un HDFS local à l’aide d’Azure Data Factory
Cet article explique comment toouse hello activité de copie de données Azure Data Factory toomove un HDFS local. Il repose sur hello [les activités de déplacement des données](data-factory-data-movement-activities.md) article, qui présente une vue d’ensemble du déplacement des données avec l’activité de copie hello.

Vous pouvez copier des données à partir du magasin de données du récepteur HDFS tooany pris en charge. Pour une liste de données pris en charge des magasins récepteurs par l’activité de copie hello, consultez hello [prise en charge des magasins de données](data-factory-data-movement-activities.md#supported-data-stores-and-formats) table. Fabrique de données prend actuellement en charge le déplacement des données uniquement à partir d’un HDFS local tooother des magasins de données, mais ne pas pour le déplacement des données à partir d’autres données de magasins tooan local HDFS.

> [!NOTE]
> Activité de copie ne supprime pas le fichier de source de hello lorsqu’elle est correctement copié toohello destination. Si vous avez besoin de fichier de source de hello toodelete après la copie a réussi, créer un fichier de hello toodelete activité personnalisée et utiliser l’activité hello dans le pipeline de hello. 

## <a name="enabling-connectivity"></a>Activation de la connectivité
Service de fabrique de données prend en charge la connexion HDFS tooon local à l’aide de la passerelle de gestion des données de hello. Consultez [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) toolearn l’article sur la passerelle de gestion des données et des instructions détaillées sur la configuration de passerelle de hello. Utilisez hello passerelle tooconnect tooHDFS même s’il est hébergé dans une machine virtuelle IaaS de Azure.

> [!NOTE]
> Vérifiez que hello est passerelle de gestion des données peuvent accéder à trop**tous les** hello [serveur de noms de nœud] : [nom de port du nœud] et [serveurs de nœud de données] : [port de nœud de données] du cluster Hadoop de hello. Le [port du nœud de nom] par défaut est 50070 et le [port du nœud de données] par défaut est 50075.

Lorsque vous installez une passerelle sur hello même ordinateur ou local hello Azure VM comme hello HDFS, nous vous recommandons d’installer hello passerelle sur un ordinateur distinct/Azure IaaS machine virtuelle. Disposer d’une passerelle sur un ordinateur distinct réduit les conflits de ressources et améliore les performances. Lorsque vous installez la passerelle de hello sur un ordinateur distinct, machine de hello doit être machine hello tooaccess en mesure de hello HDFS.

## <a name="getting-started"></a>Prise en main
Vous pouvez créer un pipeline avec une activité de copie qui déplace les données d’une source HDFS à l’aide de différents outils/API.

toocreate de façon plus simple Hello un pipeline est toouse hello **Assistant copie de**. Consultez [didacticiel : créer un pipeline à l’aide d’Assistant copie de](data-factory-copy-data-wizard-tutorial.md) pour une procédure pas à pas rapides sur la création d’un pipeline à l’aide d’Assistant de données de copie hello.

Vous pouvez également utiliser hello suivant outils toocreate un pipeline : **portail Azure**, **Visual Studio**, **Azure PowerShell**, **modèle Azure Resource Manager** , **API .NET**, et **API REST**. Consultez [didacticiel d’activité de copie](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) pour obtenir des instructions toocreate un pipeline avec une activité de copie.

Si vous utilisez hello ou une API, vous effectuez hello suivant les étapes toocreate un pipeline qui déplace la banque de données récepteur tooa du magasin de données à partir des données d’une source :

1. Créer **services liés** fabrique de données tooyour toolink les données d’entrée et de sortie magasins.
2. Créer **datasets** toorepresent d’entrée et sortie l’opération de copie des données pour hello.
3. Création d’un **pipeline** avec une activité de copie qui utilise un jeu de données en tant qu’entrée et un jeu de données en tant que sortie.

Lorsque vous utilisez hello Assistant, les définitions de JSON pour ces entités de fabrique de données (services liés, des datasets et pipeline de hello) sont créées automatiquement pour vous. Lorsque vous utilisez/API des outils (à l’exception des API .NET), vous définissez ces entités de fabrique de données à l’aide du format JSON de hello.  Pour voir un exemple avec des définitions de JSON pour les entités de fabrique de données qui sont utilisées toocopy des données à partir d’un magasin de données HDFS, [exemple de JSON : copier des données locales HDFS tooAzure Blob](#json-example-copy-data-from-on-premises-hdfs-to-azure-blob) section de cet article.

Hello les sections suivantes fournit des détails sur les propriétés JSON qui sont utilisés toodefine Data Factory entités spécifiques tooHDFS :

## <a name="linked-service-properties"></a>Propriétés du service lié
Un service lié lie une fabrique de données de tooa de magasin de données. Vous créez un service lié de type **Hdfs** toolink une fabrique de données tooyour HDFS local. Hello tableau suivant fournit la description du service de tooHDFS spécifique lié éléments JSON.

| Propriété | Description | Requis |
| --- | --- | --- |
| type |propriété de type Hello doit indiquer : **Hdfs** |Oui |
| Url |URL toohello HDFS |Oui |
| authenticationType |Anonyme ou Windows. <br><br> toouse **l’authentification Kerberos** pour le connecteur HDFS, consultez trop[cette section](#use-kerberos-authentication-for-hdfs-connector) tooset votre environnement local en conséquence. |Oui |
| userName |Nom d’utilisateur de l’authentification Windows |Oui (pour l’authentification Windows) |
| password |Mot de passe de l’authentification Windows |Oui (pour l’authentification Windows) |
| gatewayName |Nom de passerelle hello hello service Data Factory doit utiliser tooconnect toohello HDFS. |Oui |
| Encryptedcredential |[Nouveau-AzureRMDataFactoryEncryptValue](https://msdn.microsoft.com/library/mt603802.aspx) sortie des informations d’identification de l’accès hello. |Non |

### <a name="using-anonymous-authentication"></a>Utilisation de l’authentification anonyme

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Anonymous",
            "userName": "hadoop",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

### <a name="using-windows-authentication"></a>Utilisation de l’authentification Windows

```JSON
{
    "name": "hdfs",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```
## <a name="dataset-properties"></a>Propriétés du jeu de données
Pour obtenir une liste complète des sections et les propriétés disponibles pour définir des jeux de données, consultez hello [création de datasets](data-factory-create-datasets.md) l’article. Les sections comme la structure, la disponibilité et la stratégie d'un jeu de données JSON sont similaires pour tous les types de jeux de données (SQL Azure, Azure Blob, Azure Table, etc.).

Hello **typeProperties** section est différente pour chaque type de jeu de données et fournit des informations sur l’emplacement de hello de données hello dans le magasin de données hello. jeu de données de type Hello typeProperties section **le partage de fichiers** (qui inclut les dataset HDFS) a hello propriétés suivantes

| Propriété | Description | Requis |
| --- | --- | --- |
| folderPath |Dossier toohello de chemin d’accès. Exemple : `myfolder`<br/><br/>Utilisez le caractère d’échappement ' \ ' pour les caractères spéciaux dans la chaîne de hello. Par exemple : pour dossier\sous-dossier, spécifiez dossier\\\\sous-dossier et pour d:\dossier d’exemple, spécifiez d:\\\\dossier d’exemple.<br/><br/>Vous pouvez combiner cette propriété avec **partitionBy** toohave chemins d’accès basés sur un secteur de début et date et l’heure de fin. |Oui |
| fileName |Spécifiez le nom hello du fichier de hello Bonjour **folderPath** si vous souhaitez hello table toorefer tooa fichier spécifique dans le dossier de hello. Si vous ne spécifiez pas de valeur pour cette propriété, la table de hello pointe tooall des fichiers dans le dossier de hello.<br/><br/>Lorsque le nom de fichier n’est pas spécifié pour un dataset de sortie, nom hello du fichier de hello généré serait Bonjour sous ce format : <br/><br/>Data<Guid>.txt (par exemple : Data.0a405f8a-93ff-4c6f-b3be-f69616f1df7a.txt) |Non |
| partitionedBy |partitionedBy peut être utilisé toospecify un folderPath dynamique, le nom de fichier de données de série chronologique. Exemple : folderPath peut être paramétré pour toutes les heures de données. |Non |
| format | Hello, les types de format suivants est pris en charge : **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Ensemble hello **type** propriété sous tooone de format de ces valeurs. Pour en savoir plus, consultez les sections relatives à [format Text](data-factory-supported-file-and-compression-formats.md#text-format), [format Json](data-factory-supported-file-and-compression-formats.md#json-format), [format Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [format Orc](data-factory-supported-file-and-compression-formats.md#orc-format) et [format Parquet](data-factory-supported-file-and-compression-formats.md#parquet-format). <br><br> Si vous souhaitez trop**copier les fichiers en tant que-est** entre des magasins basée sur le fichier (copie binaire), ignorer la section de format hello dans les deux définitions de jeu de données d’entrée et de sortie. |Non |
| compression | Spécifiez le type de hello et le niveau de compression pour les données de salutation. Les types pris en charge sont : **GZip**, **Deflate**, **BZip2** et **ZipDeflate**. Les niveaux pris en charge sont **Optimal** et **Fastest**. Pour plus d’informations, consultez [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support). |Non |

> [!NOTE]
> fileName et fileFilter ne peuvent pas être utilisés simultanément.

### <a name="using-partionedby-property"></a>Utilisation de la propriété partitionedBy
Comme indiqué dans la section précédente de hello, vous pouvez spécifier un folderPath dynamique et le nom de fichier de données de série chronologique par hello **partitionedBy** propriété, [fonctions de la fabrique de données et les variables système hello](data-factory-functions-variables.md).

toolearn en savoir plus sur les jeux de données de série temps, en planifiant et secteurs, consultez [création de Datasets](data-factory-create-datasets.md), [de planification et l’exécution de](data-factory-scheduling-and-execution.md), et [création de Pipelines](data-factory-create-pipelines.md) articles.

#### <a name="sample-1"></a>Exemple 1 :

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Slice}",
"partitionedBy":
[
    { "name": "Slice", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyyMMddHH" } },
],
```
Dans cet exemple {Slice} est remplacé par la valeur hello de fabrique de données variable système SliceStart au format (AAAAMMJJHH) de la hello spécifiée. Hello SliceStart fait référence à des temps de toostart de tranche de hello. Hello folderPath est différent pour chaque secteur. Par exemple : wikidatagateway/wikisampledataout/2014100103 ou wikidatagateway/wikisampledataout/2014100104.

#### <a name="sample-2"></a>Exemple 2 :

```JSON
"folderPath": "wikidatagateway/wikisampledataout/{Year}/{Month}/{Day}",
"fileName": "{Hour}.csv",
"partitionedBy":
 [
    { "name": "Year", "value": { "type": "DateTime", "date": "SliceStart", "format": "yyyy" } },
    { "name": "Month", "value": { "type": "DateTime", "date": "SliceStart", "format": "MM" } },
    { "name": "Day", "value": { "type": "DateTime", "date": "SliceStart", "format": "dd" } },
    { "name": "Hour", "value": { "type": "DateTime", "date": "SliceStart", "format": "hh" } }
],
```
Dans cet exemple, l'année, le mois, le jour et l'heure de SliceStart sont extraits dans des variables distinctes qui sont utilisées par les propriétés folderPath et fileName.

## <a name="copy-activity-properties"></a>Propriétés de l’activité de copie
Pour obtenir une liste complète des sections et les propriétés disponibles pour la définition d’activités, consultez hello [création de Pipelines](data-factory-create-pipelines.md) l’article. Les propriétés comme le nom, la description, les tables d'entrée et de sortie et les différentes stratégies sont disponibles pour tous les types d'activités.

Alors que les propriétés disponibles dans la section typeProperties hello activité hello varient selon chaque type d’activité. Pour l’activité de copie, ils varient selon les types de sources et récepteurs hello.

Pour l’activité de copie, lors de la source est de type **FileSystemSource** hello propriétés suivantes est disponible dans la section de typeProperties :

**FileSystemSource** prend en charge hello propriétés suivantes :

| Propriété | Description | Valeurs autorisées | Requis |
| --- | --- | --- | --- |
| recursive |Indique si les données de salutation sont lu de manière récursive à partir de dossiers de sub hello ou uniquement à partir de dossier spécifié de hello. |True, False (par défaut) |Non |

## <a name="supported-file-and-compression-formats"></a>Formats de fichier et de compression pris en charge
Pour plus d’informations, voir [Formats de fichiers et de compression pris en charge dans Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

## <a name="json-example-copy-data-from-on-premises-hdfs-tooazure-blob"></a>Exemple de JSON : copier des données locales HDFS tooAzure Blob
Cet exemple montre comment toocopy des données à partir d’un tooAzure HDFS local stockage d’objets Blob. Toutefois, les données peuvent être copiées **directement** tooany de récepteurs hello indiqué [ici](data-factory-data-movement-activities.md#supported-data-stores-and-formats) à l’aide de hello activité de copie dans Azure Data Factory.  

exemple Hello fournit les définitions de JSON pour hello suivant des entités de fabrique de données. Vous pouvez utiliser ces définitions de toocreate un pipeline toocopy des données d’HDFS tooAzure stockage d’objets Blob à l’aide de [portail Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).

1. Un service lié de type [OnPremisesHdfs](#linked-service-properties).
2. Un service lié de type [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Un [jeu de données](data-factory-create-datasets.md) d’entrée de type [FileShare](#dataset-properties).
4. Un [jeu de données](data-factory-create-datasets.md) de sortie de type [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Un [pipeline](data-factory-create-pipelines.md) avec activité de copie qui utilise [FileSystemSource](#copy-activity-properties) et [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemple Hello copie des données à partir d’un tooan HDFS local Azure blob toutes les heures. propriétés JSON Hello utilisées dans ces exemples sont décrits dans les sections suivantes des exemples de hello.

Dans un premier temps, configurer la passerelle de gestion des données hello. Hello instructions Bonjour [déplacement des données entre les emplacements locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) l’article.

**Service lié de HDFS :** cet exemple utilise hello l’authentification Windows. Consultez la section [Service lié HDFS](#linked-service-properties) pour connaître les différents types d’authentification que vous pouvez utiliser.

```JSON
{
    "name": "HDFSLinkedService",
    "properties":
    {
        "type": "Hdfs",
        "typeProperties":
        {
            "authenticationType": "Windows",
            "userName": "Administrator",
            "password": "password",
            "url" : "http://<machine>:50070/webhdfs/v1/",
            "gatewayName": "mygateway"
        }
    }
}
```

**Service lié Azure Storage :**

```JSON
{
  "name": "AzureStorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```

**HDFS d’entrée de jeu de données :** ce jeu de données fait référence le dossier HDFS toohello DataTransfer/UnitTest /. pipeline de Hello copie tous les fichiers de hello dans cette destination toohello de dossier.

Paramètre « external » : « true » informe service Data Factory de hello ce jeu de données hello est la fabrique de données externe toohello et n’est pas généré par une activité dans la fabrique de données hello.

```JSON
{
    "name": "InputDataset",
    "properties": {
        "type": "FileShare",
        "linkedServiceName": "HDFSLinkedService",
        "typeProperties": {
            "folderPath": "DataTransfer/UnitTest/"
        },
        "external": true,
        "availability": {
            "frequency": "Hour",
            "interval":  1
        }
    }
}
```

**Jeu de données de sortie Azure Blob :**

Les données sont écrites tooa nouvel objet blob toutes les heures (fréquence : heure, intervalle : 1). chemin d’accès du dossier Hello pour l’objet blob de hello est évaluée dynamiquement en fonction de l’heure de début hello de tranche hello qui est en cours de traitement. chemin d’accès du dossier Hello utilise l’année, mois, jours et heures des parties de l’heure de début hello.

```JSON
{
    "name": "OutputDataset",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/hdfs/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
            "partitionedBy": [
                {
                    "name": "Year",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "yyyy"
                    }
                },
                {
                    "name": "Month",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "MM"
                    }
                },
                {
                    "name": "Day",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "dd"
                    }
                },
                {
                    "name": "Hour",
                    "value": {
                        "type": "DateTime",
                        "date": "SliceStart",
                        "format": "HH"
                    }
                }
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

**Activité de copie dans un pipeline avec une source Système de fichiers et un récepteur blob :**

pipeline de Hello contient une activité de copie qui est configuré toouse ces jeux de données d’entrée et de sortie et est toorun planifiée toutes les heures. Dans la définition JSON du pipeline hello, hello **source** type est défini trop**FileSystemSource** et **récepteur** type est défini trop**BlobSink**. la requête SQL Hello spécifiée pour hello **requête** propriété sélectionne des données de hello Bonjour au-delà de toocopy d’heure.

```JSON
{
    "name": "pipeline",
    "properties":
    {
        "activities":
        [
            {
                "name": "HdfsToBlobCopy",
                "inputs": [ {"name": "InputDataset"} ],
                "outputs": [ {"name": "OutputDataset"} ],
                "type": "Copy",
                "typeProperties":
                {
                    "source":
                    {
                        "type": "FileSystemSource"
                    },
                    "sink":
                    {
                        "type": "BlobSink"
                    }
                },
                "policy":
                {
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1,
                    "timeout": "00:05:00"
                }
            }
        ],
        "start": "2014-06-01T18:00:00Z",
        "end": "2014-06-01T19:00:00Z"
    }
}
```

## <a name="use-kerberos-authentication-for-hdfs-connector"></a>Utilisation de l’authentification Kerberos pour le connecteur HDFS
Il existe deux tooset options d’environnement local de hello ainsi en toouse l’authentification Kerberos dans le connecteur HDFS. Vous pouvez choisir de hello une correspond mieux à votre cas.
* Option 1 : [Joindre l’ordinateur de la passerelle au domaine Kerberos](#kerberos-join-realm)
* Option 2 : [activer l’approbation mutuelle entre le domaine Windows et le domaine Kerberos](#kerberos-mutual-trust)

### <a name="kerberos-join-realm"></a>Option 1 : Joindre l’ordinateur de la passerelle au domaine Kerberos

#### <a name="requirement"></a>Condition :

* ordinateur de passerelle Hello a besoin de domaine Kerberos de hello toojoin et ne peut pas joindre un domaine Windows.

#### <a name="how-tooconfigure"></a>Comment tooconfigure :

**Sur l’ordinateur de la passerelle :**

1.  Exécutez hello **Ksetup** utilitaire tooconfigure hello serveur KDC Kerberos et le domaine.

    machine de Hello doit être configuré en tant que membre d’un groupe de travail, car un domaine Kerberos est différent d’un domaine Windows. Cela est possible en définissant de Kerberos hello et en ajoutant un serveur de contrôleur de domaine Kerberos comme suit. Remplacez *REALM.COM* par votre propre domaine respectif en fonction des besoins.

            C:> Ksetup /setdomain REALM.COM
            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>

    **Redémarrez** machine hello après l’exécution de ces 2 commandes.

2.  Vérifiez la configuration hello avec **Ksetup** commande. sortie de Hello doit être telles que :

            C:> Ksetup
            default realm = REALM.COM (external)
            REALM.com:
                kdc = <your_kdc_server_address>

**Dans Azure Data Factory :**

* Configurer l’utilisation du connecteur hello HDFS **l’authentification Windows** avec Kerberos principal nom et mot de passe tooconnect toohello HDFS source de données. Vérifiez les détails de configuration dans la section sur les [propriétés du service lié HDFS](#linked-service-properties).

### <a name="kerberos-mutual-trust"></a>Option 2 : activer l’approbation mutuelle entre le domaine Windows et le domaine Kerberos

#### <a name="requirement"></a>Condition :
*   ordinateur de passerelle Hello doit rejoindre un domaine Windows.
*   Vous avez besoin des paramètres d’autorisation tooupdate hello du contrôleur de domaine.

#### <a name="how-tooconfigure"></a>Comment tooconfigure :

> [!NOTE]
> Remplacez le domaine.com et AD.COM Bonjour suivant le didacticiel avec vos propres respectif domaine et contrôleur de domaine en fonction des besoins.

**Sur le serveur KDC :**

1.  Modifier la configuration KDC hello **krb5.conf** fichier toolet KDC approbation de domaine Windows toohello suivant le modèle de configuration de référence. Par défaut, configuration de hello se trouve dans **/etc/krb5.conf**.

            [logging]
             default = FILE:/var/log/krb5libs.log
             kdc = FILE:/var/log/krb5kdc.log
             admin_server = FILE:/var/log/kadmind.log

            [libdefaults]
             default_realm = REALM.COM
             dns_lookup_realm = false
             dns_lookup_kdc = false
             ticket_lifetime = 24h
             renew_lifetime = 7d
             forwardable = true

            [realms]
             REALM.COM = {
              kdc = node.REALM.COM
              admin_server = node.REALM.COM
             }
            AD.COM = {
             kdc = windc.ad.com
             admin_server = windc.ad.com
            }

            [domain_realm]
             .REALM.COM = REALM.COM
             REALM.COM = REALM.COM
             .ad.com = AD.COM
             ad.com = AD.COM

            [capaths]
             AD.COM = {
              REALM.COM = .
             }

  **Redémarrez** hello service KDC après la configuration.

2.  Préparer un principal nommé  **krbtgt/REALM.COM@AD.COM**  dans serveur KDC avec hello de commande suivante :

            Kadmin> addprinc krbtgt/REALM.COM@AD.COM

3.  Dans le fichier de configuration du service HDFS **hadoop.security.auth_to_local**, ajoutez `RULE:[1:$1@$0](.*@AD.COM)s/@.*//`.

**Sur le contrôleur de domaine :**

1.  Exécutez hello **Ksetup** commandes tooadd une entrée de domaine :

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

2.  Établir l’approbation de domaine Windows tooKerberos domaine. [] est hello mot de passe pour le principal de hello  **krbtgt/REALM.COM@AD.COM** .

            C:> netdom trust REALM.COM /Domain: AD.COM /add /realm /passwordt:[password]

3.  Sélectionnez l’algorithme de chiffrement utilisé dans Kerberos.

    1. Accédez tooServer Manager > Gestion des stratégies de groupe > domaine > objets de stratégie de groupe > par défaut ou stratégie de domaine Active et modifier.

    2. Bonjour **éditeur de gestion de stratégie de groupe** fenêtre contextuelle, accédez tooComputer Configuration > stratégies > Paramètres Windows > Paramètres de sécurité > Stratégies locales > Options de sécurité et configurer **réseau sécurité : configurer les types de chiffrement autorisés pour Kerberos**.

    3. Algorithme de chiffrement hello sélectionnez souhaité toouse lorsque connectez tooKDC. En règle générale, vous pouvez simplement sélectionner toutes les options de hello.

        ![Configuration des types de chiffrement pour Kerberos](media/data-factory-hdfs-connector/config-encryption-types-for-kerberos.png)

    4. Utilisez **Ksetup** algorithme de chiffrement du hello commande toospecify toobe utilisé sur hello domaine spécifique.

                C:> ksetup /SetEncTypeAttr REALM.COM DES-CBC-CRC DES-CBC-MD5 RC4-HMAC-MD5 AES128-CTS-HMAC-SHA1-96 AES256-CTS-HMAC-SHA1-96

4.  Créer un mappage de hello entre le compte de domaine hello et Kerberos principal, dans l’ordre toouse principal Kerberos dans un domaine Windows.

    1. Démarrer les outils d’administration hello > **Active Directory Users and Computers**.

    2. Pour configurer les fonctionnalités avancées, cliquez sur **Affichage** > **Fonctionnalités avancées**.

    3. Recherchez hello compte toowhich vous souhaitez les mappages toocreate, avec le bouton droit tooview **mappages nom** > cliquez sur **noms Kerberos** onglet.

    4. Ajouter un principal de domaine de hello.

        ![Mappage des identités de sécurité](media/data-factory-hdfs-connector/map-security-identity.png)

**Sur l’ordinateur de la passerelle :**

* Exécutez hello **Ksetup** commandes tooadd une entrée de domaine.

            C:> Ksetup /addkdc REALM.COM <your_kdc_server_address>
            C:> ksetup /addhosttorealmmap HDFS-service-FQDN REALM.COM

**Dans Azure Data Factory :**

* Configurer l’utilisation du connecteur hello HDFS **l’authentification Windows** avec votre compte de domaine ou une source de données Principal Kerberos tooconnect toohello HDFS. Vérifiez les détails de configuration dans la section sur les [propriétés du service lié HDFS](#linked-service-properties).

> [!NOTE]
> colonnes de toomap de toocolumns du jeu de données source à partir du jeu de données récepteur, consultez [mappage des colonnes de jeu de données dans Azure Data Factory](data-factory-map-columns.md).


## <a name="performance-and-tuning"></a>Performances et réglage
Consultez [copie activité optimiser les performances et Guide d’optimisation](data-factory-copy-activity-performance.md) toolearn sur la clé de facteurs d’affecter les performances de transfert de données (activité de copie) dans Azure Data Factory et de différentes façons toooptimize il.
