---
title: "Créer des clusters Hadoop avec Azure REST API - Azure | Documents Microsoft"
description: "Découvrez comment créer des clusters HDInsight en soumettant des modèles Azure Resource Manager à l’API REST Azure."
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
ms.openlocfilehash: a36a41c231472ceeeb46d02ddb65549b1c79728a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="create-hadoop-clusters-using-the-azure-rest-api"></a><span data-ttu-id="f682b-103">Créer des clusters Hadoop à l’aide de l’API REST Azure</span><span class="sxs-lookup"><span data-stu-id="f682b-103">Create Hadoop clusters using the Azure REST API</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="f682b-104">Découvrez comment créer des clusters HDInsight l’aide d’un modèle Azure Resource Manager et de l’API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="f682b-104">Learn how to create an HDInsight cluster using an Azure Resource Manager template and the Azure REST API.</span></span>

<span data-ttu-id="f682b-105">L’API REST Azure vous permet d’effectuer des opérations de gestion sur les services hébergés sur la plateforme Azure, y compris la création de nouvelles ressources, telles que des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f682b-105">The Azure REST API allows you to perform management operations on services hosted in the Azure platform, including the creation of new resources such as HDInsight clusters.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f682b-106">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="f682b-106">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f682b-107">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f682b-107">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!NOTE]
> <span data-ttu-id="f682b-108">Les étapes décrites dans ce document se servent de l’utilitaire [curl (https://curl.haxx.se/)](https://curl.haxx.se/) pour communiquer avec l’API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="f682b-108">The steps in this document use the [curl (https://curl.haxx.se/)](https://curl.haxx.se/) utility to communicate with the Azure REST API.</span></span>

## <a name="create-a-template"></a><span data-ttu-id="f682b-109">Créer un modèle</span><span class="sxs-lookup"><span data-stu-id="f682b-109">Create a template</span></span>

<span data-ttu-id="f682b-110">Les modèles Azure Resource Manager sont des documents JSON qui décrivent un **groupe de ressources** et toutes les ressources qu’il contient (par exemple, HDInsight). Cette approche à base de modèles vous permet de définir les ressources dont vous avez besoin pour HDInsight dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="f682b-110">Azure Resource Manager templates are JSON documents that describe a **resource group** and all resources in it (such as HDInsight.) This template-based approach allows you to define the resources that you need for HDInsight in one template.</span></span>

<span data-ttu-id="f682b-111">Le document JSON suivant résulte d’une fusion des fichiers de modèle et de paramètres disponibles sur [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password). Ce code crée un cluster Linux qui utilise un mot de passe pour sécuriser le compte d’utilisateur SSH.</span><span class="sxs-lookup"><span data-stu-id="f682b-111">The following JSON document is a merger of the template and parameters files from [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), which creates a Linux-based cluster using a password to secure the SSH user account.</span></span>

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
                           "description": "The type of the HDInsight cluster to create."
                       }
                   },
                   "clusterName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the HDInsight cluster to create."
                       }
                   },
                   "clusterLoginUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to submit jobs to the cluster and to log into cluster dashboards."
                       }
                   },
                   "clusterLoginPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "sshUserName": {
                       "type": "string",
                       "metadata": {
                           "description": "These credentials can be used to remotely access the cluster."
                       }
                   },
                   "sshPassword": {
                       "type": "securestring",
                       "metadata": {
                           "description": "The password must be at least 10 characters in length and must contain at least one digit, one non-alphanumeric character, and one upper or lower case letter."
                       }
                   },
                   "clusterStorageAccountName": {
                       "type": "string",
                       "metadata": {
                           "description": "The name of the storage account to be created and be used as the cluster's storage."
                       }
                   },
                   "clusterWorkerNodeCount": {
                       "type": "int",
                       "defaultValue": 4,
                       "metadata": {
                           "description": "The number of nodes in the HDInsight cluster."
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

<span data-ttu-id="f682b-112">Cet exemple est utilisé dans les étapes de ce document.</span><span class="sxs-lookup"><span data-stu-id="f682b-112">This example is used in the steps in this document.</span></span> <span data-ttu-id="f682b-113">Remplacez les *valeurs* de l’exemple dans la section **Paramètres** par les valeurs de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="f682b-113">Replace the example *values* in the **Parameters** section with the values for your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f682b-114">Le modèle utilise le nombre par défaut de nœuds worker (4) pour un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f682b-114">The template uses the default number of worker nodes (4) for an HDInsight cluster.</span></span> <span data-ttu-id="f682b-115">Si vous envisagez d’utiliser plus de 32 nœuds worker, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.</span><span class="sxs-lookup"><span data-stu-id="f682b-115">If you plan on more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14 GB ram.</span></span>
>
> <span data-ttu-id="f682b-116">Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f682b-116">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="f682b-117">Connexion à votre abonnement Azure</span><span class="sxs-lookup"><span data-stu-id="f682b-117">Log in to your Azure subscription</span></span>

<span data-ttu-id="f682b-118">Suivez la procédure décrite dans la [prise en main d’Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) et connectez-vous à votre abonnement en utilisant la commande `az login`.</span><span class="sxs-lookup"><span data-stu-id="f682b-118">Follow the steps documented in [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) and connect to your subscription using the `az login` command.</span></span>

## <a name="create-a-service-principal"></a><span data-ttu-id="f682b-119">Créer un principal du service</span><span class="sxs-lookup"><span data-stu-id="f682b-119">Create a service principal</span></span>

> [!NOTE]
> <span data-ttu-id="f682b-120">Ces étapes sont une version abrégée de la section *Créer un principal du service avec un mot de passe - Azure CLI* dans le document [Créer un principal du service pour accéder aux ressources à l’aide de l’interface de ligne de commande (CLI) Azure](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) .</span><span class="sxs-lookup"><span data-stu-id="f682b-120">These steps are an abridged version of the *Create service principal with password* section of the [Use Azure CLI to create a service principal to access resources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document.</span></span> <span data-ttu-id="f682b-121">Les étapes suivantes créent un principal de service qui est utilisé pour s’authentifier sur l’API REST Azure.</span><span class="sxs-lookup"><span data-stu-id="f682b-121">These steps create a service principal that is used to authenticate to the Azure REST API.</span></span>

1. <span data-ttu-id="f682b-122">À partir d’une ligne de commande, utilisez la commande suivante pour répertorier vos abonnements Azure.</span><span class="sxs-lookup"><span data-stu-id="f682b-122">From a command line, use the following command to list your Azure subscriptions.</span></span>

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    <span data-ttu-id="f682b-123">Dans la liste, sélectionnez l’abonnement que vous souhaitez utiliser et notez les colonnes **Subscription_ID** et __Tenant_ID__.</span><span class="sxs-lookup"><span data-stu-id="f682b-123">In the list, select the subscription that you want to use and note the **Subscription_ID** and __Tenant_ID__ columns.</span></span> <span data-ttu-id="f682b-124">Enregistrez ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="f682b-124">Save these values.</span></span>

2. <span data-ttu-id="f682b-125">Utilisez les commandes suivantes pour créer une application dans Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f682b-125">Use the following command to create an application in Azure Active Directory.</span></span>

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    <span data-ttu-id="f682b-126">Remplacez les valeurs de `--display-name`, `--homepage` et `--identifier-uris` par vos propres valeurs.</span><span class="sxs-lookup"><span data-stu-id="f682b-126">Replace the values for the `--display-name`, `--homepage`, and `--identifier-uris` with your own values.</span></span> <span data-ttu-id="f682b-127">Fournissez un mot de passe pour la nouvelle entrée Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f682b-127">Provide a password for the new Active Directory entry.</span></span>

   > [!NOTE]
   > <span data-ttu-id="f682b-128">Les valeurs `--home-page` et `--identifier-uris` n’ont pas à faire référence à une page web réelle hébergée sur Internet.</span><span class="sxs-lookup"><span data-stu-id="f682b-128">The `--home-page` and `--identifier-uris` values don't need to reference an actual web page hosted on the internet.</span></span> <span data-ttu-id="f682b-129">Les URI doivent être uniques.</span><span class="sxs-lookup"><span data-stu-id="f682b-129">They must be unique URIs.</span></span>

   <span data-ttu-id="f682b-130">La valeur retournée par cette commande est __l’ID de l’application__ pour la nouvelle application.</span><span class="sxs-lookup"><span data-stu-id="f682b-130">The value returned from this command is the __App ID__ for the new application.</span></span> <span data-ttu-id="f682b-131">Enregistrez cette valeur.</span><span class="sxs-lookup"><span data-stu-id="f682b-131">Save this value.</span></span>

3. <span data-ttu-id="f682b-132">Utilisez la commande suivante pour créer un principal du service à l’aide de **l’ID de l’application**.</span><span class="sxs-lookup"><span data-stu-id="f682b-132">Use the following command to create a service principal using the **App ID**.</span></span>

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     <span data-ttu-id="f682b-133">La valeur retournée par cette commande est __l’ID d’objet__.</span><span class="sxs-lookup"><span data-stu-id="f682b-133">The value returned from this command is the __Object ID__.</span></span> <span data-ttu-id="f682b-134">Enregistrez cette valeur.</span><span class="sxs-lookup"><span data-stu-id="f682b-134">Save this value.</span></span>

4. <span data-ttu-id="f682b-135">Affectez le rôle **Owner** (Propriétaire) au principal du service à l’aide de la valeur **Object ID** (ID d’objet).</span><span class="sxs-lookup"><span data-stu-id="f682b-135">Assign the **Owner** role to the service principal using the **Object ID** value.</span></span> <span data-ttu-id="f682b-136">Utilisez **l’ID d’abonnement** obtenu précédemment.</span><span class="sxs-lookup"><span data-stu-id="f682b-136">Use the **subscription ID** you obtained earlier.</span></span>

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a><span data-ttu-id="f682b-137">Obtenir un jeton d’authentification</span><span class="sxs-lookup"><span data-stu-id="f682b-137">Get an authentication token</span></span>

<span data-ttu-id="f682b-138">Utilisez la commande suivante pour récupérer un jeton d’authentification :</span><span class="sxs-lookup"><span data-stu-id="f682b-138">Use the following command to retrieve an authentication token:</span></span>

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

<span data-ttu-id="f682b-139">Définissez `$TENANTID`, `$APPID` et `$PASSWORD` sur des valeurs obtenues ou utilisées précédemment.</span><span class="sxs-lookup"><span data-stu-id="f682b-139">Set `$TENANTID`, `$APPID`, and `$PASSWORD` to the values obtained or used previously.</span></span>

<span data-ttu-id="f682b-140">Si cette demande aboutit, vous recevez une réponse de type 200 dont le corps contient un document JSON.</span><span class="sxs-lookup"><span data-stu-id="f682b-140">If this request is successful, you receive a 200 series response and the response body contains a JSON document.</span></span>

<span data-ttu-id="f682b-141">Le document JSON retourné par cette demande contient un élément nommé **access_token**.</span><span class="sxs-lookup"><span data-stu-id="f682b-141">The JSON document returned by this request contains an element named **access_token**.</span></span> <span data-ttu-id="f682b-142">La valeur de l’élément **access_token** est utilisée pour les demandes d’authentification adressées à l’API REST.</span><span class="sxs-lookup"><span data-stu-id="f682b-142">The value of **access_token** is used to authentication requests to the REST API.</span></span>

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a><span data-ttu-id="f682b-143">Créer un groupe de ressources</span><span class="sxs-lookup"><span data-stu-id="f682b-143">Create a resource group</span></span>

<span data-ttu-id="f682b-144">Procédez comme suit pour créer un groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f682b-144">Use the following to create a resource group.</span></span>

* <span data-ttu-id="f682b-145">Définissez `$SUBSCRIPTIONID` sur l’ID d’abonnement reçu lors de la création du principal du service.</span><span class="sxs-lookup"><span data-stu-id="f682b-145">Set `$SUBSCRIPTIONID` to the subscription ID received while creating the service principal.</span></span>
* <span data-ttu-id="f682b-146">Définissez `$ACCESSTOKEN` sur le jeton d’accès reçu à l’étape précédente.</span><span class="sxs-lookup"><span data-stu-id="f682b-146">Set `$ACCESSTOKEN` to the access token received in the previous step.</span></span>
* <span data-ttu-id="f682b-147">Remplacez `DATACENTERLOCATION` par le centre de données dans lequel vous voulez créer le groupe de ressources et les ressources.</span><span class="sxs-lookup"><span data-stu-id="f682b-147">Replace `DATACENTERLOCATION` with the data center you wish to create the resource group, and resources, in.</span></span> <span data-ttu-id="f682b-148">Par exemple, « South Central US ».</span><span class="sxs-lookup"><span data-stu-id="f682b-148">For example, 'South Central US'.</span></span>
* <span data-ttu-id="f682b-149">Définissez `$RESOURCEGROUPNAME` sur le nom que vous souhaitez utiliser pour ce groupe :</span><span class="sxs-lookup"><span data-stu-id="f682b-149">Set `$RESOURCEGROUPNAME` to the name you wish to use for this group:</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

<span data-ttu-id="f682b-150">Si cette demande est acceptée, vous recevez une réponse 200 qui contient un document JSON renfermant des informations sur le groupe.</span><span class="sxs-lookup"><span data-stu-id="f682b-150">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the group.</span></span> <span data-ttu-id="f682b-151">L’élément `"provisioningState"` contient la valeur `"Succeeded"`.</span><span class="sxs-lookup"><span data-stu-id="f682b-151">The `"provisioningState"` element contains a value of `"Succeeded"`.</span></span>

## <a name="create-a-deployment"></a><span data-ttu-id="f682b-152">Créer un déploiement</span><span class="sxs-lookup"><span data-stu-id="f682b-152">Create a deployment</span></span>

<span data-ttu-id="f682b-153">Utilisez la commande suivante pour déployer le modèle sur le groupe de ressources.</span><span class="sxs-lookup"><span data-stu-id="f682b-153">Use the following command to deploy the template to the resource group.</span></span>

* <span data-ttu-id="f682b-154">Définissez `$DEPLOYMENTNAME` sur le nom que vous souhaitez utiliser pour ce déploiement.</span><span class="sxs-lookup"><span data-stu-id="f682b-154">Set `$DEPLOYMENTNAME` to the name you wish to use for this deployment.</span></span>

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string to the template and parameters}"
```

> [!NOTE]
> <span data-ttu-id="f682b-155">Si vous avez enregistré le modèle dans un fichier, vous pouvez utiliser la commande suivante à la place de `-d "{ template and parameters}"`:</span><span class="sxs-lookup"><span data-stu-id="f682b-155">If you saved the template to a file, you can use the following command instead of `-d "{ template and parameters}"`:</span></span>
>
> `--data-binary "@/path/to/file.json"`

<span data-ttu-id="f682b-156">Si cette demande est acceptée, vous recevez une réponse 200 qui contient un document JSON renfermant des informations sur le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f682b-156">If this request is successful, you receive a 200 series response and the response body contains a JSON document containing information about the deployment operation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f682b-157">Le déploiement a été soumis, mais n’est pas terminé.</span><span class="sxs-lookup"><span data-stu-id="f682b-157">The deployment has been submitted, but has not completed.</span></span> <span data-ttu-id="f682b-158">Le processus de déploiement prend généralement 15 minutes environ.</span><span class="sxs-lookup"><span data-stu-id="f682b-158">It can take several minutes, usually around 15, for the deployment to complete.</span></span>

## <a name="check-the-status-of-a-deployment"></a><span data-ttu-id="f682b-159">Vérifier l’état d’un déploiement</span><span class="sxs-lookup"><span data-stu-id="f682b-159">Check the status of a deployment</span></span>

<span data-ttu-id="f682b-160">Pour vérifier le statut du déploiement, utilisez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="f682b-160">To check the status of the deployment, use the following command:</span></span>

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

<span data-ttu-id="f682b-161">Cette commande renvoie un document JSON renfermant des informations sur le déploiement.</span><span class="sxs-lookup"><span data-stu-id="f682b-161">This command returns a JSON document containing information about the deployment operation.</span></span> <span data-ttu-id="f682b-162">L’élément `"provisioningState"` contient l’état du déploiement.</span><span class="sxs-lookup"><span data-stu-id="f682b-162">The `"provisioningState"` element contains the status of the deployment.</span></span> <span data-ttu-id="f682b-163">Si cet élément contient la valeur `"Succeeded"`, cela indique que le déploiement a été correctement effectué.</span><span class="sxs-lookup"><span data-stu-id="f682b-163">If this element contains a value of `"Succeeded"`, then the deployment has completed successfully.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="f682b-164">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="f682b-164">Troubleshoot</span></span>

<span data-ttu-id="f682b-165">Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="f682b-165">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f682b-166">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f682b-166">Next steps</span></span>

<span data-ttu-id="f682b-167">Vous avez créé un cluster HDInsight. Pour apprendre à l’utiliser, consultez les rubriques ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="f682b-167">Now that you have successfully created an HDInsight cluster, use the following to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="f682b-168">Clusters Hadoop</span><span class="sxs-lookup"><span data-stu-id="f682b-168">Hadoop clusters</span></span>

* [<span data-ttu-id="f682b-169">Utilisation de Hive avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-169">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f682b-170">Utilisation de Pig avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-170">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f682b-171">Utilisation de MapReduce avec HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-171">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="f682b-172">Clusters HBase</span><span class="sxs-lookup"><span data-stu-id="f682b-172">HBase clusters</span></span>

* [<span data-ttu-id="f682b-173">Prise en main de HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-173">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="f682b-174">Développement d’applications Java pour HBase sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-174">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="f682b-175">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="f682b-175">Storm clusters</span></span>

* [<span data-ttu-id="f682b-176">Développement de topologies Java pour Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-176">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="f682b-177">Utilisation de composants Python dans Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-177">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="f682b-178">Déploiement et analyse des topologies avec Storm sur HDInsight</span><span class="sxs-lookup"><span data-stu-id="f682b-178">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
