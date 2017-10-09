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
# <a name="create-hadoop-clusters-using-hello-azure-rest-api"></a>Créer des clusters Hadoop à l’aide de hello API REST Azure

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

Découvrez comment toocreate un HDInsight de cluster à l’aide d’un modèle Azure Resource Manager et hello API REST Azure.

Hello API REST Azure vous permet de tooperform les opérations de gestion sur les services hébergés dans hello plateforme Azure, y compris la création de nouvelles ressources telles que des clusters HDInsight hello.

> [!IMPORTANT]
> Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!NOTE]
> Hello les étapes dans cette hello d’utilisation de document [curl (https://curl.haxx.se/)](https://curl.haxx.se/) toocommunicate utilitaire avec hello API REST Azure.

## <a name="create-a-template"></a>Créer un modèle

Les modèles Azure Resource Manager sont des documents JSON qui décrivent un **groupe de ressources** et toutes les ressources qu’il contient (par exemple, HDInsight). Cette approche basée sur un modèle vous permet de ressources hello toodefine dont vous avez besoin pour HDInsight dans un modèle.

Bonjour document JSON suivant est une fusion de hello les fichiers de modèle et les paramètres à partir de [https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password](https://github.com/Azure/azure-quickstart-templates/tree/master/101-hdinsight-linux-ssh-password), ce qui crée une base de Linux cluster à l’aide d’un Bonjour toosecure de mot de passe SSH compte d’utilisateur.

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

Cet exemple est utilisé dans les étapes de hello dans ce document. Remplacez l’exemple de hello *valeurs* Bonjour **paramètres** section avec des valeurs hello pour votre cluster.

> [!IMPORTANT]
> modèle de Hello utilise le nombre de nœuds de travail (4) par défaut de hello pour un cluster HDInsight. Si vous envisagez d’utiliser plus de 32 nœuds worker, vous devez sélectionner une taille de nœud principal avec au moins 8 cœurs et 14 Go de RAM.
>
> Pour plus d’informations sur les tailles de nœud et les coûts associés, consultez [Tarification HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).

## <a name="log-in-tooyour-azure-subscription"></a>Ouvrez une session dans tooyour abonnement Azure

Suivez les étapes de hello documentées dans [prise en main Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) et connecter abonnement tooyour à l’aide de hello `az login` commande.

## <a name="create-a-service-principal"></a>Créer un principal du service

> [!NOTE]
> Ces étapes sont une version abrégée de hello *créer le service principal avec un mot de passe* section Hello [CLI d’Azure utilisation toocreate un principal de service tooaccess ressources](../azure-resource-manager/resource-group-authenticate-service-principal-cli.md#create-service-principal-with-password) document. Les étapes suivantes créent un principal de service qui est utilisé tooauthenticate toohello API REST Azure.

1. À partir d’une ligne de commande, utilisez hello suivant toolist de commande vos abonnements Azure.

   ```bash
   az account list --query '[].{Subscription_ID:id,Tenant_ID:tenantId,Name:name}'  --output table
   ```

    Dans la liste hello, sélectionnez l’abonnement hello que vous le souhaitez toouse et notez hello **ID_ABONNEMENT** et __Tenant_ID__ colonnes. Enregistrez ces valeurs.

2. Utilisez hello suivant commande toocreate une application dans Azure Active Directory.

   ```bash
   az ad app create --display-name "exampleapp" --homepage "https://www.contoso.org" --identifier-uris "https://www.contoso.org/example" --password <Your password> --query 'appId'
   ```

    Remplacez les valeurs hello pour hello `--display-name`, `--homepage`, et `--identifier-uris` avec vos propres valeurs. Fournir un mot de passe pour la nouvelle entrée de Active Directory hello.

   > [!NOTE]
   > Hello `--home-page` et `--identifier-uris` les valeurs ne doivent tooreference une page web réel hébergé sur hello internet. Les URI doivent être uniques.

   valeur retournée à partir de cette commande Hello est hello __ID d’application__ pour application hello. Enregistrez cette valeur.

3. Toocreate de commande suivant de hello utilisez un principal de service à l’aide de hello **ID d’application**.

   ```bash
   az ad sp create --id <App ID> --query 'objectId'
   ```

     valeur retournée à partir de cette commande Hello est hello __ID d’objet__. Enregistrez cette valeur.

4. Affecter hello **propriétaire** rôle toohello principal de service à l’aide de hello **ID d’objet** valeur. Hello d’utilisation **ID d’abonnement** obtenues précédemment.

   ```bash
   az role assignment create --assignee <Object ID> --role Owner --scope /subscriptions/<Subscription ID>/
   ```

## <a name="get-an-authentication-token"></a>Obtenir un jeton d’authentification

Utilisez hello suivant commande tooretrieve un jeton d’authentification :

```bash
curl -X "POST" "https://login.microsoftonline.com/$TENANTID/oauth2/token" \
-H "Cookie: flight-uxoptin=true; stsservicecookie=ests; x-ms-gateway-slice=productionb; stsservicecookie=ests" \
-H "Content-Type: application/x-www-form-urlencoded" \
--data-urlencode "client_id=$APPID" \
--data-urlencode "grant_type=client_credentials" \
--data-urlencode "client_secret=$PASSWORD" \
--data-urlencode "resource=https://management.azure.com/"
```

Définissez `$TENANTID`, `$APPID`, et `$PASSWORD` toohello valeurs obtenues ou précédemment utilisé.

Si cette demande réussit, vous recevez une réponse 200 de série et les corps de réponse hello contient un document JSON.

Hello document JSON retourné par la demande contient un élément nommé **access_token**. Hello valeur **access_token** est utilisé tooauthentication demandes toohello API REST.

```json
{
    "token_type":"Bearer",
    "expires_in":"3599",
    "expires_on":"1463409994",
    "not_before":"1463406094",
    "resource":"https://management.azure.com/","access_token":"eyJ0eXAiOiJKV1QiLCJhbGciOiJSUzI1NiIsIng1dCI6Ik1uQ19WWoNBVGZNNXBPWWlKSE1iYTlnb0VLWSIsImtpZCI6Ik1uQ19WWmNBVGZNNXBPWWlKSE1iYTlnb0VLWSJ9.eyJhdWQiOiJodHRwczovL21hbmFnZW1lbnQuYXp1cmUuY29tLyIsImlzcyI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI2Ny8iLCJpYXQiOjE0NjM0MDYwOTQsIm5iZiI6MTQ2MzQwNjA5NCwiZXhwIjoxNDYzNDA5OTk5LCJhcHBpZCI6IjBlYzcyMzM0LTZkMDMtNDhmYi04OWU1LTU2NTJiODBiZDliYiIsImFwcGlkYWNyIjoiMSIsImlkcCI6Imh0dHBzOi8vc3RzLndpbmRvd3MubmV0LzcyZjk4OGJmLTg2ZjEtNDFhZi05MWFiLTJkN2NkMDExZGI0Ny8iLCJvaWQiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJzdWIiOiJlNjgxZTZiMi1mZThkLTRkZGUtYjZiMS0xNjAyZDQyNWQzOWYiLCJ0aWQiOiI3MmY5ODhiZi04NmYxLTQxYWYtOTFhYi0yZDdjZDAxMWRiNDciLCJ2ZXIiOiIxLjAifQ.nJVERbeDHLGHn7ZsbVGBJyHOu2PYhG5dji6F63gu8XN2Cvol3J1HO1uB4H3nCSt9DTu_jMHqAur_NNyobgNM21GojbEZAvd0I9NY0UDumBEvDZfMKneqp7a_cgAU7IYRcTPneSxbD6wo-8gIgfN9KDql98b0uEzixIVIWra2Q1bUUYETYqyaJNdS4RUmlJKNNpENllAyHQLv7hXnap1IuzP-f5CNIbbj9UgXxLiOtW5JhUAwWLZ3-WMhNRpUO2SIB7W7tQ0AbjXw3aUYr7el066J51z5tC1AK9UC-mD_fO_HUP6ZmPzu5gLA6DxkIIYP3grPnRVoUDltHQvwgONDOw"
}
```

## <a name="create-a-resource-group"></a>Créer un groupe de ressources

Utilisez hello suivant toocreate un groupe de ressources.

* Définissez `$SUBSCRIPTIONID` toohello ID d’abonnement reçues lors de la création de hello principal du service.
* Définissez `$ACCESSTOKEN` toohello obtenu à l’étape précédente de hello du jeton d’accès.
* Remplacez `DATACENTERLOCATION` avec le centre de données hello vous souhaitez le groupe de ressources toocreate hello et ressources, dans. Par exemple, « South Central US ».
* Définissez `$RESOURCEGROUPNAME` toohello nom du toouse pour ce groupe :

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME?api-version=2015-01-01" \
    -H "Authorization: Bearer $ACCESSTOKEN" \
    -H "Content-Type: application/json" \
    -d $'{
"location": "DATACENTERLOCATION"
}'
```

Si cette demande réussit, vous recevez une réponse 200 de série et les corps de réponse hello contient un document JSON contenant des informations sur le groupe de hello. Hello `"provisioningState"` élément contient une valeur de `"Succeeded"`.

## <a name="create-a-deployment"></a>Créer un déploiement

Utilisez hello suivant du groupe de ressources toohello de modèle de commande toodeploy hello.

* Définissez `$DEPLOYMENTNAME` toohello nom du toouse pour ce déploiement.

```bash
curl -X "PUT" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json" \
-d "{set your body string toohello template and parameters}"
```

> [!NOTE]
> Si vous avez enregistré le fichier de tooa hello modèle, vous pouvez utiliser hello suivant de commande au lieu de `-d "{ template and parameters}"`:
>
> `--data-binary "@/path/to/file.json"`

Si cette demande réussit, vous recevez une réponse 200 de série et les corps de réponse hello contient un document JSON contenant des informations sur l’opération de déploiement hello.

> [!IMPORTANT]
> déploiement de Hello a été envoyée, mais n’est pas terminée. Il peut prendre plusieurs minutes, en règle générale environ 15, hello déploiement toocomplete.

## <a name="check-hello-status-of-a-deployment"></a>Vérifiez l’état d’un déploiement hello

état de hello toocheck de déploiement hello, hello utilisez commande suivante :

```bash
curl -X "GET" "https://management.azure.com/subscriptions/$SUBSCRIPTIONID/resourcegroups/$RESOURCEGROUPNAME/providers/microsoft.resources/deployments/$DEPLOYMENTNAME?api-version=2015-01-01" \
-H "Authorization: Bearer $ACCESSTOKEN" \
-H "Content-Type: application/json"
```

Cette commande retourne un document JSON contenant des informations sur l’opération de déploiement hello. Hello `"provisioningState"` élément contient l’état hello du déploiement de hello. Si cet élément contient une valeur de `"Succeeded"`, puis déploiement de hello est bien terminée.

## <a name="troubleshoot"></a>Résolution des problèmes

Si vous rencontrez des problèmes lors de la création de clusters HDInsight, reportez-vous aux [exigences de contrôle d’accès](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Étapes suivantes

Maintenant que vous avez créé un cluster HDInsight, utilisez hello suivant toolearn comment toowork avec votre cluster.

### <a name="hadoop-clusters"></a>Clusters Hadoop

* [Utilisation de Hive avec HDInsight](hdinsight-use-hive.md)
* [Utilisation de Pig avec HDInsight](hdinsight-use-pig.md)
* [Utilisation de MapReduce avec HDInsight](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a>Clusters HBase

* [Prise en main de HBase sur HDInsight](hdinsight-hbase-tutorial-get-started-linux.md)
* [Développement d’applications Java pour HBase sur HDInsight](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a>Clusters Storm

* [Développement de topologies Java pour Storm sur HDInsight](hdinsight-storm-develop-java-topology.md)
* [Utilisation de composants Python dans Storm sur HDInsight](hdinsight-storm-develop-python-topology.md)
* [Déploiement et analyse des topologies avec Storm sur HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)
