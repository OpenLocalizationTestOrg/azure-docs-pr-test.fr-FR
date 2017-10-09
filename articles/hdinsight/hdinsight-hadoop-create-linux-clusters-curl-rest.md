---
title: "aaaCreate Hadoop clusters à l’aide des API REST de Azure - Azure | Documents Microsoft"
description: "Découvrez comment toocreate HDInsight clusters en soumettant toohello de modèles Azure Resource Manager API REST Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 98be5893-2c6f-4dfa-95ec-d4d8b5b7dcb5
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/10/2017
ms.author: larryfr
ms.openlocfilehash: 87b585e5084eccdc3d7c57483deabb4ad6e32597
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a><span data-ttu-id="5de33-103">Créer des clusters Hadoop à l’aide de hello API REST Azure</span><span class="sxs-lookup"><span data-stu-id="5de33-103">Create Hadoop clusters using hello Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="5de33-104">Découvrez comment toocreate un HDInsight de cluster à l’aide d’un modèle Azure Resource Manager et hello API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="5de33-104">Learn how toocreate an HDInsight cluster using an Azure Resource Manager template and hello Azure REST API.</span></span>

<span data-ttu-id="5de33-105">Hello API REST Azure vous permet de tooperform les opérations de gestion sur les services hébergés dans hello plateforme Azure, y compris la création de nouvelles ressources telles que des clusters HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-105">hello Azure REST API allows you tooperform management operations on services hosted in hello Azure platform, including hello creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5de33-106">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="5de33-106">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5de33-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5de33-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="5de33-108">Hello les étapes dans cette hello d’utilisation de document [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilitaire avec hello API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="5de33-108">hello steps in this document use hello [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility toocommunicate with hello Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="5de33-109">Créer un modèle</span><span class="sxs-lookup"><span data-stu-id="5de33-109">Create a template</span></span>

<span data-ttu-id="5de33-110">Les modèles Azure Resource Manager sont des documents JSON qui décrivent un **groupe de ressources** et toutes les ressources qu’il contient (par exemple, HDInsight). Cette approche basée sur un modèle vous permet de ressources hello toodefine dont vous avez besoin pour HDInsight dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="5de33-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you toodefine hello resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="5de33-111">Bonjour document JSON suivant est une fusion de hello les fichiers de modèle et les paramètres à partir de [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), ce qui crée une base de Linux cluster à l’aide d’un Bonjour toosecure de mot de passe SSH compte d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5de33-111">hello following JSON document is a merger of hello template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password toosecure hello SSH user account.</span></span>

   ```json
   {
       "properties": {
           "template": {
               "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
               "contentVersion": "1.0.0.0",
               "parameters": {
                   "clusterType": {
                       "type": "string",
                       "allowedValues": ["hadoop",
                       "hbase",
                       "storm",
                       "spark"],
                       "metadata": {
                           "description": "hello type of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello HDInsight cluster toocreate."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used toosubmit jobs toohello cluster and toolog into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used tooremotely access hello cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "hello password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "hello name of hello storage account toobe created and be used as hello cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "hello number of nodes in hello HDInsight cluster."
                       }
                   }
               },
               "variables": {
                   "defaultApiVersion": "2015-05-01-preview",
                   "clusterApiVersion": "2015-03-01-preview"
               },
               "resources": [{
                   "name": "[parameters('clusterStorageAccountName')]",
                   "type": "Microsoft.Storage/storageAccounts",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('defaultApiVersion')]",
                   "dependsOn": [],
                   "tags": {

                   },
                   "properties": {
                       "accountType": "Standard_LRS"
                   }
               },
               {
                   "name": "[parameters('clusterName')]",
                   "type": "Microsoft.HDInsight/clusters",
                   "location": "[resourceGroup().location]",
                   "apiVersion": "[variables('clusterApiVersion')]",
                   "dependsOn": ["[concat('Microsoft.Storage/storageAccounts/',parameters('clusterStorageAccountName'))]"],
                   "tags": {

                   },
                   "properties": {
                       "clusterVersion": "3.5",
                       "osType": "Linux",
                       "clusterDefinition": {
                           "kind": "[parameters('clusterType')]",
                           "configurations": {
                               "gateway": {
                                   "restAuthCredential.isEnabled": true,
                                   "restAuthCredential.username": "[parameters('clusterLoginUserName')]",
                                   "restAuthCredential.password": "[parameters('clusterLoginPassword')]"
                               }
                           }
                       },
                       "storageProfile": {
                           "storageaccounts": [{
                               "name": "[concat(parameters('clusterStorageAccountName'),'.blob.core.windows.net')]",
                               "isDefault": true,
                               "container": "[parameters('clusterName')]",
                               "key": "[listKeys(resourceId('Microsoft.Storage/storageAccounts', parameters('clusterStorageAccountName')), variables('defaultApiVersion')).key1]"
                           }]
                       },
                       "computeProfile": {
                           "roles": [{
                               "name": "headnode",
                               "targetInstanceCount": "2",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           },
                           {
                               "name": "workernode",
                               "targetInstanceCount": "[parameters('clusterWorkerNodeCount')]",
                               "hardwareProfile": {
                                   "vmSize": "Standard_D3"
                               },
                               "osProfile": {
                                   "linuxOperatingSystemProfile": {
                                       "username": "[parameters('sshUserName')]",
                                       "password": "[parameters('sshPassword')]"
                                   }
                               }
                           }]
                       }
                   }
               }],
               "outputs": {
                   "cluster": {
                       "type": "object",
                       "value": "[reference(resourceId('Microsoft.HDInsight/clusters',parameters('clusterName')))]"
                   }
               }
           },
           "mode": "incremental",
           "Parameters": {
               "clusterName": {
                   "value": "newclustername"
               },
               "clusterType": {
                   "value": "hadoop"
               },
               "clusterStorageAccountName": {
                   "value": "newstoragename"
               },
               "clusterLoginUserName": {
                   "value": "admin"
               },
               "clusterLoginPassword": {
                   "value": "changeme"
               },
               "sshUserName": {
                   "value": "sshuser"
               },
               "sshPassword": {
                   "value": "changeme"
               }
           }
       }
   }
   ```

<span data-ttu-id="5de33-112">Cet exemple est utilisé dans les étapes de hello dans ce document.</span><span class="sxs-lookup"><span data-stu-id="5de33-112">This example is used in hello steps in this document.</span></span> <span data-ttu-id="5de33-113">Remplacez l’exemple de hello *valeurs* Bonjour **paramètres** section avec des valeurs hello pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="5de33-113">Replace hello example *values* in hello **Parameters** section with hello values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5de33-114">modèle de Hello utilise le nombre de nœuds de travail (4) par défaut de hello pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5de33-114">hello template uses hello default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="5de33-115">Si vous envisagez d’utiliser plus de 32 nœuds worker, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="5de33-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="5de33-116">Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="5de33-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="5de33-117">Ouvrez une session dans tooyour abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="5de33-117">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="5de33-118">Suivez les étapes de hello documentées dans [prise en main Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) et connecter abonnement tooyour à l’aide de hello `az login` commande.</span><span class="sxs-lookup"><span data-stu-id="5de33-118">Follow hello steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect tooyour subscription using hello `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="5de33-119">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="5de33-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="5de33-120">Ces étapes sont une version abrégée de hello *créer le service principal avec un mot de passe* section Hello [CLI d’Azure utilisation toocreate un principal de service tooaccess ressources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span><span class="sxs-lookup"><span data-stu-id="5de33-120">These steps are an abridged version of hello *Create service principal with password* section of hello [Use Azure CLI toocreate a service principal tooaccess resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="5de33-121">Les étapes suivantes créent un principal de service qui est utilisé tooauthenticate toohello API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="5de33-121">These steps create a service principal that is used tooauthenticate toohello Azure REST API.</span></span>

1. <span data-ttu-id="5de33-122">À partir d’une ligne de commande, utilisez hello suivant toolist de commande vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="5de33-122">From a command line, use hello following command toolist your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="5de33-123">Dans la liste hello, sélectionnez l’abonnement hello que vous le souhaitez toouse et notez hello **ID_ABONNEMENT** et __Tenant_ID__ colonnes.</span><span class="sxs-lookup"><span data-stu-id="5de33-123">In hello list, select hello subscription that you want toouse and note hello **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="5de33-124">Enregistrez ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="5de33-124">Save these values.</span></span>

2. <span data-ttu-id="5de33-125">Utilisez hello suivant commande toocreate une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="5de33-125">Use hello following command toocreate an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="5de33-126">Remplacez les valeurs hello pour hello `--display-name`, `--homepage`, et `--identifier-uris` avec vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="5de33-126">Replace hello values for hello `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="5de33-127">Fournir un mot de passe pour la nouvelle entrée de Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-127">Provide a password for hello new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="5de33-128">Hello `--home-page` et `--identifier-uris` les valeurs ne doivent tooreference une page web réel hébergé sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="5de33-128">hello `--home-page` and `--identifier-uris` values don't need tooreference an actual web page hosted on hello internet.</span></span> <span data-ttu-id="5de33-129">Les URI doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="5de33-129">They must be unique URIs.</span></span>

   <span data-ttu-id="5de33-130">valeur retournée à partir de cette commande Hello est hello __ID d’application__ pour application hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-130">hello value returned from this command is hello __App ID__ for hello new application.</span></span> <span data-ttu-id="5de33-131">Enregistrez cette valeur.</span><span class="sxs-lookup"><span data-stu-id="5de33-131">Save this value.</span></span>

3. <span data-ttu-id="5de33-132">Toocreate de commande suivant de hello utilisez un principal de service à l’aide de hello **ID d’application**.</span><span class="sxs-lookup"><span data-stu-id="5de33-132">Use hello following command toocreate a service principal using hello **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="5de33-133">valeur retournée à partir de cette commande Hello est hello __ID d’objet__.</span><span class="sxs-lookup"><span data-stu-id="5de33-133">hello value returned from this command is hello __Object ID__.</span></span> <span data-ttu-id="5de33-134">Enregistrez cette valeur.</span><span class="sxs-lookup"><span data-stu-id="5de33-134">Save this value.</span></span>

4. <span data-ttu-id="5de33-135">Affecter hello **propriétaire** rôle toohello principal de service à l’aide de hello **ID d’objet** valeur.</span><span class="sxs-lookup"><span data-stu-id="5de33-135">Assign hello **Owner** role toohello service principal using hello **Object ID** value.</span></span> <span data-ttu-id="5de33-136">Hello d’utilisation **ID d’abonnement** obtenues précédemment.</span><span class="sxs-lookup"><span data-stu-id="5de33-136">Use hello **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="5de33-137">Obtenir un jeton d’authentification</span><span class="sxs-lookup"><span data-stu-id="5de33-137">Get an authentication token</span></span>

<span data-ttu-id="5de33-138">Utilisez hello suivant commande tooretrieve un jeton d’authentification :</span><span class="sxs-lookup"><span data-stu-id="5de33-138">Use hello following command tooretrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="5de33-139">Définissez `$TENANTID`, `$APPID`, et `$PASSWORD` toohello valeurs obtenues ou précédemment utilisé.</span><span class="sxs-lookup"><span data-stu-id="5de33-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` toohello values obtained or used previously.</span></span>

<span data-ttu-id="5de33-140">Si cette demande réussit, vous recevez une réponse 200 de série et les corps de réponse hello contient un document JSON.</span><span class="sxs-lookup"><span data-stu-id="5de33-140">If this request is successful, you receive a 200 series response and hello response body contains a JSON document.</span></span>

<span data-ttu-id="5de33-141">Hello document JSON retourné par la demande contient un élément nommé **access_token**.</span><span class="sxs-lookup"><span data-stu-id="5de33-141">hello JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="5de33-142">Hello valeur **access_token** est utilisé tooauthentication demandes toohello API REST.</span><span class="sxs-lookup"><span data-stu-id="5de33-142">hello value of **access_token** is used tooauthentication requests toohello REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="5de33-143">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="5de33-143">Create a resource group</span></span>

<span data-ttu-id="5de33-144">Utilisez hello suivant toocreate un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="5de33-144">Use hello following toocreate a resource group.</span></span>

* <span data-ttu-id="5de33-145">Définissez `$SUBSCRIPTIONID` toohello ID d’abonnement reçues lors de la création de hello principal du service.</span><span class="sxs-lookup"><span data-stu-id="5de33-145">Set `$SUBSCRIPTIONID` toohello subscription ID received while creating hello service principal.</span></span>
* <span data-ttu-id="5de33-146">Définissez `$ACCESSTOKEN` toohello obtenu à l’étape précédente de hello du jeton d’accès.</span><span class="sxs-lookup"><span data-stu-id="5de33-146">Set `$ACCESSTOKEN` toohello access token received in hello previous step.</span></span>
* <span data-ttu-id="5de33-147">Remplacez `DATACENTERLOCATION` avec le centre de données hello vous souhaitez le groupe de ressources toocreate hello et ressources, dans.</span><span class="sxs-lookup"><span data-stu-id="5de33-147">Replace `DATACENTERLOCATION` with hello data center you wish toocreate hello resource group, and resources, in.</span></span> <span data-ttu-id="5de33-148">Par exemple, « South Central US ».</span><span class="sxs-lookup"><span data-stu-id="5de33-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="5de33-149">Définissez `$RESOURCEGROUPNAME` toohello nom du toouse pour ce groupe :</span><span class="sxs-lookup"><span data-stu-id="5de33-149">Set `$RESOURCEGROUPNAME` toohello name you wish toouse for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="5de33-150">Si cette demande réussit, vous recevez une réponse 200 de série et les corps de réponse hello contient un document JSON contenant des informations sur le groupe de hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-150">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello group.</span></span> <span data-ttu-id="5de33-151">Hello `"provisioningState"` élément contient une valeur de `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="5de33-151">hello `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="5de33-152">Créer un déploiement</span><span class="sxs-lookup"><span data-stu-id="5de33-152">Create a deployment</span></span>

<span data-ttu-id="5de33-153">Utilisez hello suivant du groupe de ressources toohello de modèle de commande toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-153">Use hello following command toodeploy hello template toohello resource group.</span></span>

* <span data-ttu-id="5de33-154">Définissez `$DEPLOYMENTNAME` toohello nom du toouse pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="5de33-154">Set `$DEPLOYMENTNAME` toohello name you wish toouse for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="5de33-155">Si vous avez enregistré le fichier de tooa hello modèle, vous pouvez utiliser hello suivant de commande au lieu de `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="5de33-155">If you saved hello template tooa file, you can use hello following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="5de33-156">Si cette demande réussit, vous recevez une réponse 200 de série et les corps de réponse hello contient un document JSON contenant des informations sur l’opération de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-156">If this request is successful, you receive a 200 series response and hello response body contains a JSON document containing information about hello deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5de33-157">déploiement de Hello a été envoyée, mais n’est pas terminée.</span><span class="sxs-lookup"><span data-stu-id="5de33-157">hello deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="5de33-158">Il peut prendre plusieurs minutes, en règle générale environ 15, hello déploiement toocomplete.</span><span class="sxs-lookup"><span data-stu-id="5de33-158">It can take several minutes, usually around 15, for hello deployment toocomplete.</span></span>

## <a name="check-hello-status-of-a-deployment"></a><span data-ttu-id="5de33-159">Vérifiez l’état d’un déploiement hello</span><span class="sxs-lookup"><span data-stu-id="5de33-159">Check hello status of a deployment</span></span>

<span data-ttu-id="5de33-160">état de hello toocheck de déploiement hello, hello utilisez commande suivante :</span><span class="sxs-lookup"><span data-stu-id="5de33-160">toocheck hello status of hello deployment, use hello following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="5de33-161">Cette commande retourne un document JSON contenant des informations sur l’opération de déploiement hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-161">This command returns a JSON document containing information about hello deployment operation.</span></span> <span data-ttu-id="5de33-162">Hello `"provisioningState"` élément contient l’état hello du déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="5de33-162">hello `"provisioningState"` element contains hello status of hello deployment.</span></span> <span data-ttu-id="5de33-163">Si cet élément contient une valeur de `"Succeeded"`, puis déploiement de hello est bien terminée.</span><span class="sxs-lookup"><span data-stu-id="5de33-163">If this element contains a value of `"Succeeded"`, then hello deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="5de33-164">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="5de33-164">Troubleshoot</span></span>

<span data-ttu-id="5de33-165">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="5de33-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5de33-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5de33-166">Next steps</span></span>

<span data-ttu-id="5de33-167">Maintenant que vous avez créé un cluster HDInsight, utilisez hello suivant toolearn comment toowork avec votre cluster.</span><span class="sxs-lookup"><span data-stu-id="5de33-167">Now that you have successfully created an HDInsight cluster, use hello following toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="5de33-168">Clusters Hadoop</span><span class="sxs-lookup"><span data-stu-id="5de33-168">Hadoop clusters</span></span>

* [<span data-ttu-id="5de33-169">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="5de33-170">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="5de33-171">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="5de33-172">Clusters HBase</span><span class="sxs-lookup"><span data-stu-id="5de33-172">HBase clusters</span></span>

* [<span data-ttu-id="5de33-173">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="5de33-174">Développement d’applications Java pour HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="5de33-175">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="5de33-175">Storm clusters</span></span>

* [<span data-ttu-id="5de33-176">Développement de topologies Java pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="5de33-177">Utilisation de composants Python dans Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="5de33-178">Déploiement et analyse des topologies avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="5de33-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
