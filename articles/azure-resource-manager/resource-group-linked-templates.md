---
title: "modèles d’aaaLink pour le déploiement d’Azure | Documents Microsoft"
description: "Décrit comment toouse lié modèles dans un toocreate de modèle Azure Resource Manager, une solution de modèle modulaire. Montre comment les valeurs de paramètres toopass, spécifier un fichier de paramètres et créés de façon dynamique les URL."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 27d8c4b2-1e24-45fe-88fd-8cf98a6bb2d2
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/31/2017
ms.author: tomfitz
ms.openlocfilehash: b935b1810db5ce894d009403cd4bb945cab34ba7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-linked-templates-when-deploying-azure-resources"></a>Utilisation de modèles liés lors du déploiement des ressources Azure
Dans un modèle Azure Resource Manager, vous pouvez lier de tooanother modèle, ce qui vous permet de toodecompose votre déploiement dans un ensemble de modèles ciblés, usage particulier. Tout comme la décomposition d’une application en plusieurs classes de codes, cette décomposition procure des avantages en matière de test, de réutilisation et de lisibilité.  

Vous pouvez passer des paramètres d’un modèle lié tooa de modèle principal, et ces paramètres capable de mapper directement tooparameters ou variables exposées par hello appelant le modèle. modèle lié de Hello peut également passer un modèle de source de toohello précédent variable de sortie, l’activation d’un échange de données bidirectionnelle entre les modèles.

## <a name="linking-tooa-template"></a>Liaison de modèle de tooa
Vous créez un lien entre les deux modèles en ajoutant une ressource de déploiement dans le modèle principal de hello points toohello modèle lié. Vous définissez hello **templateLink** toohello de propriété URI de modèle lié de hello. Vous pouvez fournir des valeurs de paramètre de modèle lié de hello directement dans votre modèle ou dans un fichier de paramètres. exemple Hello utilise hello **paramètres** propriété toospecify directement une valeur de paramètre.

```json
"resources": [ 
  { 
      "apiVersion": "2017-05-10", 
      "name": "linkedTemplate", 
      "type": "Microsoft.Resources/deployments", 
      "properties": { 
        "mode": "incremental", 
        "templateLink": {
          "uri": "https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion": "1.0.0.0"
        }, 
        "parameters": { 
          "StorageAccountName":{"value": "[parameters('StorageAccountName')]"} 
        } 
      } 
  } 
] 
```

Comme d’autres types de ressources, vous pouvez définir des dépendances entre les modèles liés hello et d’autres ressources. Par conséquent, lorsque les autres ressources requièrent une valeur de sortie de modèle lié de hello, faire en sorte modèle lié de hello est déployé avant eux. Ou, lorsque le modèle lié de hello s’appuie sur d’autres ressources, vous pouvez vous assurer qu'autres ressources sont déployées avant de modèle lié de hello. Vous pouvez récupérer une valeur à partir d’un modèle lié avec hello selon la syntaxe :

```json
"[reference('linkedTemplate').outputs.exampleProperty.value]"
```

Hello service Gestionnaire de ressources doit être un modèle lié de tooaccess en mesure de hello. Vous ne pouvez pas spécifier un fichier local ou un fichier qui est uniquement disponible sur votre réseau local pour le modèle lié de hello. Vous pouvez seulement fournir une valeur URI qui inclut soit **http** soit **https**. Une option consiste à tooplace votre modèle lié dans un compte de stockage et utilisez hello URI de cet élément, comme indiqué dans hello l’exemple suivant :

```json
"templateLink": {
    "uri": "http://mystorageaccount.blob.core.windows.net/templates/template.json",
    "contentVersion": "1.0.0.0",
}
```

Bien que le modèle lié de hello doit être disponible en externe, elle ne doit pas toobe toohello généralement disponible public. Vous pouvez ajouter votre compte de stockage privé tooa modèle qui est propriétaire du compte de stockage accessible tooonly hello. Ensuite, vous créez un accès partagé (SAS) de signature jeton tooenable d’accéder au cours du déploiement. Vous ajoutez ce toohello jeton SAS URI pour le modèle lié de hello. Pour connaître les étapes de configuration d’un modèle dans un compte de stockage et de génération d’un jeton SAP, consultez [Déployer des ressources avec des modèles Resource Manager et Azure PowerShell](resource-group-template-deploy.md) ou [Déployer des ressources avec des modèles Resource Manager et l’interface de ligne de commande Azure](resource-group-template-deploy-cli.md). 

Hello l’exemple suivant montre un modèle parent ce modèle tooanother de liens. modèle de lié Hello est accessible avec un jeton SAP qui est passé en tant que paramètre.

```json
"parameters": {
    "sasToken": { "type": "securestring" }
},
"resources": [
    {
        "apiVersion": "2017-05-10",
        "name": "linkedTemplate",
        "type": "Microsoft.Resources/deployments",
        "properties": {
          "mode": "incremental",
          "templateLink": {
            "uri": "[concat('https://storagecontosotemplates.blob.core.windows.net/templates/helloworld.json', parameters('sasToken'))]",
            "contentVersion": "1.0.0.0"
          }
        }
    }
],
```

Même si le jeton de hello est passé dans sous forme de chaîne sécurisée, hello URI de modèle lié hello, y compris le jeton SAS de hello, est enregistré dans les opérations de déploiement hello. exposition de toolimit, définir un délai d’expiration pour le jeton de hello.

Resource Manager gère chaque modèle lié comme un déploiement séparé. Dans l’historique de déploiement hello pour le groupe de ressources hello, vous voyez des déploiements distincts pour le parent de hello et les modèles imbriqués.

![historique des déploiements](./media/resource-group-linked-templates/linked-deployment-history.png)

## <a name="linking-tooa-parameter-file"></a>Fichier de paramètres de liaison tooa
Hello l’exemple suivant utilise hello **parametersLink** fichier de paramètres de propriété toolink tooa.

```json
"resources": [ 
  { 
     "apiVersion": "2017-05-10", 
     "name": "linkedTemplate", 
     "type": "Microsoft.Resources/deployments", 
     "properties": { 
       "mode": "incremental", 
       "templateLink": {
          "uri":"https://www.contoso.com/AzureTemplates/newStorageAccount.json",
          "contentVersion":"1.0.0.0"
       }, 
       "parametersLink": { 
          "uri":"https://www.contoso.com/AzureTemplates/parameters.json",
          "contentVersion":"1.0.0.0"
       } 
     } 
  } 
] 
```

Hello URI valeur pour le fichier de paramètres liés de hello ne peut pas être un fichier local et doit inclure **http** ou **https**. fichier de paramètres Hello peut également être limité tooaccess via un jeton SAP.

## <a name="using-variables-toolink-templates"></a>À l’aide de modèles de toolink de variables
Hello les exemples précédents ont montré les valeurs d’URL codées en dur pour les liens de modèle hello. Cette approche peut s’avérer efficace avec un modèle isolé, mais elle est incompatible avec le traitement d’un large ensemble des modèles modulaires. Au lieu de cela, vous pouvez créer une variable statique qui stocke une URL de base pour les modèles principal hello et créer dynamiquement des URL pour les modèles de hello lié à partir de cette URL de base. avantage Hello de cette approche est, vous pouvez facilement déplacer ou branchement de modèle de hello, car vous devez seulement variable statique de toochange hello dans les modèles principal hello. les modèles principal Hello passe hello correct Qu'uri dans l’ensemble de hello décomposé de modèle.

Hello suivant montre comment toouse un toocreate URL base lié deux URL pour les modèles (**sharedTemplateUrl** et **vmTemplate**). 

```json
"variables": {
    "templateBaseUrl": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/postgresql-on-ubuntu/",
    "sharedTemplateUrl": "[concat(variables('templateBaseUrl'), 'shared-resources.json')]",
    "vmTemplateUrl": "[concat(variables('templateBaseUrl'), 'database-2disk-resources.json')]"
}
```

Vous pouvez également utiliser [le déploiement()](resource-group-template-functions-deployment.md#deployment) tooget hello URL de base pour le modèle actuel de hello et utiliser cette URL de hello tooget des autres modèles dans hello même emplacement. Cette approche est utile si votre emplacement de modèle change (peut-être due tooversioning) ou que vous souhaitiez tooavoid dur codage URL dans le fichier de modèle hello. 

```json
"variables": {
    "sharedTemplateUrl": "[uri(deployment().properties.templateLink.uri, 'shared-resources.json')]"
}
```

## <a name="complete-example"></a>Exemple complet
Hello suivant des exemples de modèles affiche une disposition simplifiée des modèles liés tooillustrate de plusieurs des concepts de hello dans cet article. Il suppose que les modèles hello ont été ajoutées toohello même conteneur dans un compte de stockage avec un accès public désactivé. modèle lié de Hello transmet un modèle principal toohello arrière de valeur Bonjour **génère** section.

Hello **parent.json** se compose de :

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerSasToken": { "type": "string" }
  },
  "resources": [
    {
      "apiVersion": "2017-05-10",
      "name": "linkedTemplate",
      "type": "Microsoft.Resources/deployments",
      "properties": {
        "mode": "incremental",
        "templateLink": {
          "uri": "[concat(uri(deployment().properties.templateLink.uri, 'helloworld.json'), parameters('containerSasToken'))]",
          "contentVersion": "1.0.0.0"
        }
      }
    }
  ],
  "outputs": {
    "result": {
      "type": "string",
      "value": "[reference('linkedTemplate').outputs.result.value]"
    }
  }
}
```

Hello **helloworld.json** se compose de :

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "variables": {},
  "resources": [],
  "outputs": {
    "result": {
        "value": "Hello World",
        "type" : "string"
    }
  }
}
```

Dans PowerShell, vous obtenez un jeton pour le conteneur de hello et déployez des modèles de hello avec :

```powershell
Set-AzureRmCurrentStorageAccount -ResourceGroupName ManageGroup -Name storagecontosotemplates
$token = New-AzureStorageContainerSASToken -Name templates -Permission r -ExpiryTime (Get-Date).AddMinutes(30.0)
$url = (Get-AzureStorageBlob -Container templates -Blob parent.json).ICloudBlob.uri.AbsoluteUri
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup -TemplateUri ($url + $token) -containerSasToken $token
```

Dans Azure CLI 2.0, vous obtenez un jeton pour le conteneur de hello et déployez des modèles de hello avec hello suivant de code :

```azurecli
expiretime=$(date -u -d '30 minutes' +%Y-%m-%dT%H:%MZ)
connection=$(az storage account show-connection-string \
    --resource-group ManageGroup \
    --name storagecontosotemplates \
    --query connectionString)
token=$(az storage container generate-sas \
    --name templates \
    --expiry $expiretime \
    --permissions r \
    --output tsv \
    --connection-string $connection)
url=$(az storage blob url \
    --container-name templates \
    --name parent.json \
    --output tsv \
    --connection-string $connection)
parameter='{"containerSasToken":{"value":"?'$token'"}}'
az group deployment create --resource-group ExampleGroup --template-uri $url?$token --parameters $parameter
```

## <a name="next-steps"></a>Étapes suivantes
* toolearn sur hello définissant l’ordre de déploiement hello pour vos ressources, consultez [définition des dépendances dans les modèles Azure Resource Manager](resource-group-define-dependencies.md)
* toolearn toodefine qu’une seule ressource créer mais de nombreuses instances de celui-ci, voir [créer plusieurs instances de ressources dans le Gestionnaire de ressources Azure](resource-group-create-multiple.md)

