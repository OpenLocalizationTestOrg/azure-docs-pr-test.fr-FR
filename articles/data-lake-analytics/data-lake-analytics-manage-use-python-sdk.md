---
title: "aaaManage Analytique de LAC de données Azure à l’aide de Python | Documents Microsoft"
description: "Découvrez comment toouse Python toocreate un lac de données de la banque de compte et envoyer des travaux. "
services: data-lake-analytics
documentationcenter: 
author: matt1883
manager: jhubbard
editor: cgronlun
ms.assetid: d4213a19-4d0f-49c9-871c-9cd6ed7cf731
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: saveenr
ms.openlocfilehash: 3c0fff155db7c4fd4e84c2562816995eb156be16
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-data-lake-analytics-using-python"></a>Gérer Azure Data Lake Analytics à l’aide de Python

## <a name="python-versions"></a>Versions de Python

* Utilisez la version 64 bits de Python.
* Vous pouvez utiliser la distribution Python standard hello à  **[Python.org télécharge](https://www.python.org/downloads/)**. 
* De nombreux développeurs trouvent pratique toouse hello  **[distribution de Python de Anaconda](https://www.continuum.io/downloads)**.  
* Cet article a été écrit à l’aide de la version 3.6 à partir de la distribution de Python standard hello de Python

## <a name="install-azure-python-sdk"></a>Installer le Kit de développement logiciel (SDK) Python

Installez hello suivant des modules :

* Hello **azure-mgmt-ressource** module inclut d’autres modules Azure pour Active Directory, etc..
* Hello **magasin azure-mgmt-datalake** module inclut les opérations de gestion de compte Azure Data Lake Store hello.
* Hello **magasin azure-datalake** module inclut les opérations de système de fichiers de hello Azure Data Lake Store. 
* Hello **azure-datalake-analytique** module inclut les opérations d’Analytique de LAC de données Azure hello. 

Tout d’abord, assurez-vous d’avoir hello dernières `pip` en exécutant hello de commande suivante :

```
python -m pip install --upgrade pip
```

Ce document a été écrit à l’aide de `pip version 9.0.1`.

Utilisez hello suit `pip` commandes des modules de hello tooinstall à partir de la ligne de commande hello :

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a>Créer un script Python

Collez hello après le code dans le script de hello :

```python
## Use this only for Azure AD service-to-service authentication
#from azure.common.credentials import ServicePrincipalCredentials

## Use this only for Azure AD end-user authentication
#from azure.common.credentials import UserPassCredentials

## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

## Required for Azure Data Lake Analytics catalog management
from azure.mgmt.datalake.analytics.catalog import DataLakeAnalyticsCatalogManagementClient

## Use these as needed for your application
import logging, getpass, pprint, uuid, time
```

Exécutez cette tooverify de script qui hello modules peuvent être importés.

## <a name="authentication"></a>Authentification

### <a name="interactive-user-authentication-with-a-pop-up"></a>Authentification utilisateur interactif avec une fenêtre contextuelle

Cette méthode n’est pas prise en charge.

### <a name="interactive-user-authentication-with-a-device-code"></a>Authentification utilisateur interactif avec un code d’appareil

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a>Authentification non interactive avec SPI et un secret

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a>Authentification non interactive avec API et un certificat

Cette méthode n’est pas prise en charge.

## <a name="common-script-variables"></a>Variables de script courantes

Ces variables sont utilisées dans les exemples de hello.

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a>Créer des clients de hello

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a>Créer un groupe de ressources Azure

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a>Créer un compte Analytique Data Lake

Commencez par créer un compte Store.

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```
Puis créez un compte ADLA qui utilise ce Store.

```python
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()
```

## <a name="submit-a-job"></a>Soumettre un travail

```python
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

## <a name="wait-for-a-job-tooend"></a>Attendre un tooend de travail

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a>Lister les pipelines et les récurrences
Si des métadonnées de pipeline ou de récurrence sont jointes à vos travaux, vous pouvez lister les pipelines et les récurrences.

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a>Gérer les stratégies de calcul

objet de DataLakeAnalyticsAccountManagementClient Hello fournit des méthodes pour la gestion hello de calcul des stratégies pour un compte Analytique lac de données.

### <a name="list-compute-policies"></a>Lister les stratégies de calcul

Hello suivant code récupère une liste de stratégies de calcul pour un compte Analytique lac de données.

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a>Créer une nouvelle stratégie de calcul

Hello suivante de code crée une nouvelle stratégie de calcul pour un compte Analytique lac de données, paramètre hello maximale AUs disponible toohello spécifié utilisateur too50 et too250 de priorité hello minimal de tâche.

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a>Étapes suivantes

- toosee hello même didacticiel à l’aide d’autres outils, cliquez sur les sélecteurs d’onglet hello haut hello de page de hello.
- toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).
- Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).

