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
# <a name="manage-azure-data-lake-analytics-using-python"></a><span data-ttu-id="18015-103">Gérer Azure Data Lake Analytics à l’aide de Python</span><span class="sxs-lookup"><span data-stu-id="18015-103">Manage Azure Data Lake Analytics using Python</span></span>

## <a name="python-versions"></a><span data-ttu-id="18015-104">Versions de Python</span><span class="sxs-lookup"><span data-stu-id="18015-104">Python versions</span></span>

* <span data-ttu-id="18015-105">Utilisez la version 64 bits de Python.</span><span class="sxs-lookup"><span data-stu-id="18015-105">Use a 64-bit version of Python.</span></span>
* <span data-ttu-id="18015-106">Vous pouvez utiliser la distribution Python standard hello à  **[Python.org télécharge](https://www.python.org/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="18015-106">You can use hello standard Python distribution found at **[Python.org downloads](https://www.python.org/downloads/)**.</span></span> 
* <span data-ttu-id="18015-107">De nombreux développeurs trouvent pratique toouse hello  **[distribution de Python de Anaconda](https://www.continuum.io/downloads)**.</span><span class="sxs-lookup"><span data-stu-id="18015-107">Many developers find it convenient toouse hello **[Anaconda Python distribution](https://www.continuum.io/downloads)**.</span></span>  
* <span data-ttu-id="18015-108">Cet article a été écrit à l’aide de la version 3.6 à partir de la distribution de Python standard hello de Python</span><span class="sxs-lookup"><span data-stu-id="18015-108">This article was written using Python version 3.6 from hello standard Python distribution</span></span>

## <a name="install-azure-python-sdk"></a><span data-ttu-id="18015-109">Installer le Kit de développement logiciel (SDK) Python</span><span class="sxs-lookup"><span data-stu-id="18015-109">Install Azure Python SDK</span></span>

<span data-ttu-id="18015-110">Installez hello suivant des modules :</span><span class="sxs-lookup"><span data-stu-id="18015-110">Install hello following modules:</span></span>

* <span data-ttu-id="18015-111">Hello **azure-mgmt-ressource** module inclut d’autres modules Azure pour Active Directory, etc..</span><span class="sxs-lookup"><span data-stu-id="18015-111">hello **azure-mgmt-resource** module includes other Azure modules for Active Directory, etc.</span></span>
* <span data-ttu-id="18015-112">Hello **magasin azure-mgmt-datalake** module inclut les opérations de gestion de compte Azure Data Lake Store hello.</span><span class="sxs-lookup"><span data-stu-id="18015-112">hello **azure-mgmt-datalake-store** module includes hello Azure Data Lake Store account management operations.</span></span>
* <span data-ttu-id="18015-113">Hello **magasin azure-datalake** module inclut les opérations de système de fichiers de hello Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="18015-113">hello **azure-datalake-store** module includes hello Azure Data Lake Store filesystem operations.</span></span> 
* <span data-ttu-id="18015-114">Hello **azure-datalake-analytique** module inclut les opérations d’Analytique de LAC de données Azure hello.</span><span class="sxs-lookup"><span data-stu-id="18015-114">hello **azure-datalake-analytics** module includes hello Azure Data Lake Analytics operations.</span></span> 

<span data-ttu-id="18015-115">Tout d’abord, assurez-vous d’avoir hello dernières `pip` en exécutant hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="18015-115">First, ensure you have hello latest `pip` by running hello following command:</span></span>

```
python -m pip install --upgrade pip
```

<span data-ttu-id="18015-116">Ce document a été écrit à l’aide de `pip version 9.0.1`.</span><span class="sxs-lookup"><span data-stu-id="18015-116">This document was written using `pip version 9.0.1`.</span></span>

<span data-ttu-id="18015-117">Utilisez hello suit `pip` commandes des modules de hello tooinstall à partir de la ligne de commande hello :</span><span class="sxs-lookup"><span data-stu-id="18015-117">Use hello following `pip` commands tooinstall hello modules from hello commandline:</span></span>

```
pip install azure-mgmt-resource
pip install azure-datalake-store
pip install azure-mgmt-datalake-store
pip install azure-mgmt-datalake-analytics
```

## <a name="create-a-new-python-script"></a><span data-ttu-id="18015-118">Créer un script Python</span><span class="sxs-lookup"><span data-stu-id="18015-118">Create a new Python script</span></span>

<span data-ttu-id="18015-119">Collez hello après le code dans le script de hello :</span><span class="sxs-lookup"><span data-stu-id="18015-119">Paste hello following code into hello script:</span></span>

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

<span data-ttu-id="18015-120">Exécutez cette tooverify de script qui hello modules peuvent être importés.</span><span class="sxs-lookup"><span data-stu-id="18015-120">Run this script tooverify that hello modules can be imported.</span></span>

## <a name="authentication"></a><span data-ttu-id="18015-121">Authentification</span><span class="sxs-lookup"><span data-stu-id="18015-121">Authentication</span></span>

### <a name="interactive-user-authentication-with-a-pop-up"></a><span data-ttu-id="18015-122">Authentification utilisateur interactif avec une fenêtre contextuelle</span><span class="sxs-lookup"><span data-stu-id="18015-122">Interactive user authentication with a pop-up</span></span>

<span data-ttu-id="18015-123">Cette méthode n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="18015-123">This method is not supported.</span></span>

### <a name="interactive-user-authentication-with-a-device-code"></a><span data-ttu-id="18015-124">Authentification utilisateur interactif avec un code d’appareil</span><span class="sxs-lookup"><span data-stu-id="18015-124">Interactive user authentication with a device code</span></span>

```python
user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
password = getpass.getpass()
credentials = UserPassCredentials(user, password)
```

### <a name="noninteractive-authentication-with-spi-and-a-secret"></a><span data-ttu-id="18015-125">Authentification non interactive avec SPI et un secret</span><span class="sxs-lookup"><span data-stu-id="18015-125">Noninteractive authentication with SPI and a secret</span></span>

```python
credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')
```

### <a name="noninteractive-authentication-with-api-and-a-certificate"></a><span data-ttu-id="18015-126">Authentification non interactive avec API et un certificat</span><span class="sxs-lookup"><span data-stu-id="18015-126">Noninteractive authentication with API and a certificate</span></span>

<span data-ttu-id="18015-127">Cette méthode n’est pas prise en charge.</span><span class="sxs-lookup"><span data-stu-id="18015-127">This method is not supported.</span></span>

## <a name="common-script-variables"></a><span data-ttu-id="18015-128">Variables de script courantes</span><span class="sxs-lookup"><span data-stu-id="18015-128">Common script variables</span></span>

<span data-ttu-id="18015-129">Ces variables sont utilisées dans les exemples de hello.</span><span class="sxs-lookup"><span data-stu-id="18015-129">These variables are used in hello samples.</span></span>

```python
subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adla = '<Azure Data Lake Analytics Account Name>'
```

## <a name="create-hello-clients"></a><span data-ttu-id="18015-130">Créer des clients de hello</span><span class="sxs-lookup"><span data-stu-id="18015-130">Create hello clients</span></span>

```python
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')
```

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="18015-131">Créer un groupe de ressources Azure</span><span class="sxs-lookup"><span data-stu-id="18015-131">Create an Azure Resource Group</span></span>

```python
armGroupResult = resourceClient.resource_groups.create_or_update( rg, ResourceGroup( location=location ) )
```

## <a name="create-data-lake-analytics-account"></a><span data-ttu-id="18015-132">Créer un compte Analytique Data Lake</span><span class="sxs-lookup"><span data-stu-id="18015-132">Create Data Lake Analytics account</span></span>

<span data-ttu-id="18015-133">Commencez par créer un compte Store.</span><span class="sxs-lookup"><span data-stu-id="18015-133">First create a store account.</span></span>

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
<span data-ttu-id="18015-134">Puis créez un compte ADLA qui utilise ce Store.</span><span class="sxs-lookup"><span data-stu-id="18015-134">Then create an ADLA account that uses that store.</span></span>

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

## <a name="submit-a-job"></a><span data-ttu-id="18015-135">Soumettre un travail</span><span class="sxs-lookup"><span data-stu-id="18015-135">Submit a job</span></span>

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

## <a name="wait-for-a-job-tooend"></a><span data-ttu-id="18015-136">Attendre un tooend de travail</span><span class="sxs-lookup"><span data-stu-id="18015-136">Wait for a job tooend</span></span>

```python
jobResult = adlaJobClient.job.get(adla, jobId)
while(jobResult.state != JobState.ended):
    print('Job is not yet done, waiting for 3 seconds. Current state: ' + jobResult.state.value)
    time.sleep(3)
    jobResult = adlaJobClient.job.get(adla, jobId)

print ('Job finished with result: ' + jobResult.result.value)
```

## <a name="list-pipelines-and-recurrences"></a><span data-ttu-id="18015-137">Lister les pipelines et les récurrences</span><span class="sxs-lookup"><span data-stu-id="18015-137">List pipelines and recurrences</span></span>
<span data-ttu-id="18015-138">Si des métadonnées de pipeline ou de récurrence sont jointes à vos travaux, vous pouvez lister les pipelines et les récurrences.</span><span class="sxs-lookup"><span data-stu-id="18015-138">Depending whether your jobs have pipeline or recurrence metadata attached, you can list pipelines and recurrences.</span></span>

```python
pipelines = adlaJobClient.pipeline.list(adla)
for p in pipelines:
    print('Pipeline: ' + p.name + ' ' + p.pipelineId)

recurrences = adlaJobClient.recurrence.list(adla)
for r in recurrences:
    print('Recurrence: ' + r.name + ' ' + r.recurrenceId)
```

## <a name="manage-compute-policies"></a><span data-ttu-id="18015-139">Gérer les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="18015-139">Manage compute policies</span></span>

<span data-ttu-id="18015-140">objet de DataLakeAnalyticsAccountManagementClient Hello fournit des méthodes pour la gestion hello de calcul des stratégies pour un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="18015-140">hello DataLakeAnalyticsAccountManagementClient object provides methods for managing hello compute policies for a Data Lake Analytics account.</span></span>

### <a name="list-compute-policies"></a><span data-ttu-id="18015-141">Lister les stratégies de calcul</span><span class="sxs-lookup"><span data-stu-id="18015-141">List compute policies</span></span>

<span data-ttu-id="18015-142">Hello suivant code récupère une liste de stratégies de calcul pour un compte Analytique lac de données.</span><span class="sxs-lookup"><span data-stu-id="18015-142">hello following code retrieves a list of compute policies for a Data Lake Analytics account.</span></span>

```python
policies = adlaAccountClient.computePolicies.listByAccount(rg, adla)
for p in policies:
    print('Name: ' + p.name + 'Type: ' + p.objectType + 'Max AUs / job: ' + p.maxDegreeOfParallelismPerJob + 'Min priority / job: ' + p.minPriorityPerJob)
```

### <a name="create-a-new-compute-policy"></a><span data-ttu-id="18015-143">Créer une nouvelle stratégie de calcul</span><span class="sxs-lookup"><span data-stu-id="18015-143">Create a new compute policy</span></span>

<span data-ttu-id="18015-144">Hello suivante de code crée une nouvelle stratégie de calcul pour un compte Analytique lac de données, paramètre hello maximale AUs disponible toohello spécifié utilisateur too50 et too250 de priorité hello minimal de tâche.</span><span class="sxs-lookup"><span data-stu-id="18015-144">hello following code creates a new compute policy for a Data Lake Analytics account, setting hello maximum AUs available toohello specified user too50, and hello minimum job priority too250.</span></span>

```python
userAadObjectId = "3b097601-4912-4d41-b9d2-78672fc2acde"
newPolicyParams = ComputePolicyCreateOrUpdateParameters(userAadObjectId, "User", 50, 250)
adlaAccountClient.computePolicies.createOrUpdate(rg, adla, "GaryMcDaniel", newPolicyParams)
```

## <a name="next-steps"></a><span data-ttu-id="18015-145">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="18015-145">Next steps</span></span>

- <span data-ttu-id="18015-146">toosee hello même didacticiel à l’aide d’autres outils, cliquez sur les sélecteurs d’onglet hello haut hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="18015-146">toosee hello same tutorial using other tools, click hello tab selectors on hello top of hello page.</span></span>
- <span data-ttu-id="18015-147">toolearn U-SQL, consultez [prise en main langage lac de données Azure Analytique U-SQL](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="18015-147">toolearn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
- <span data-ttu-id="18015-148">Pour les tâches de gestion, consultez [Gestion d’Azure Data Lake Analytics à l’aide du portail Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="18015-148">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>

