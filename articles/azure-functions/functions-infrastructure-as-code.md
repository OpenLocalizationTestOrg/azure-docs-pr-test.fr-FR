---
title: "déploiement de ressources aaaAutomate pour une application de la fonction dans les fonctions de Azure | Documents Microsoft"
description: "Découvrez comment toobuild un modèle Azure Resource Manager qui déploie votre application de la fonction."
services: Functions
documtationcenter: na
author: lindydonna
manager: erikre
editor: 
tags: 
keywords: Azure Functions, fonctions, architecture sans serveur, infrastructure sous forme code, azure resource manager
ms.assetid: d20743e3-aab6-442c-a836-9bcea09bfd32
ms.server: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/25/2017
ms.author: glenga
ms.openlocfilehash: b0df0d4ef9fe93213f7b1cb1d1e6b4e14f8b3a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-resource-deployment-for-your-function-app-in-azure-functions"></a>Automatiser le déploiement de ressources pour votre application de fonction dans Azure Functions

Vous pouvez utiliser un toodeploy de modèle Azure Resource Manager une application de la fonction. Cet article présente les ressources de hello requis et les paramètres pour ce faire. Vous devrez peut-être toodeploy des ressources supplémentaires, en fonction de hello [les déclencheurs et les liaisons](functions-triggers-bindings.md) dans votre application de la fonction.

Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Pour des exemples de modèles, consultez :
- [Function app on Consumption plan] (Application de fonction dans le plan Consommation)
- [Function app on Azure App Service plan] (Application de fonction dans le plan Azure App Service)

## <a name="required-resources"></a>Ressources nécessaires

Une application de fonction nécessite les ressources suivantes :

* Un compte de [stockage Azure](../storage/index.md)
* Un plan d’hébergement (plan Consommation ou plan App Service)
* Une application de fonction 

### <a name="storage-account"></a>Compte de stockage

Un compte de stockage Azure est nécessaire pour une application de fonction. Vous avez besoin d’un compte à usage général qui prend en charge les objets blob, les tables, les files d’attente et les fichiers. Pour plus d’informations, consultez [Configuration requise du compte de stockage Azure Functions](functions-create-function-app-portal.md#storage-account-requirements).

```json
{
    "type": "Microsoft.Storage/storageAccounts",
    "name": "[variables('storageAccountName')]",
    "apiVersion": "2015-06-15",
    "location": "[resourceGroup().location]",
    "properties": {
        "accountType": "[parameters('storageAccountType')]"
    }
}
```

Hello en outre, les propriétés `AzureWebJobsStorage` et `AzureWebJobsDashboard` doivent être spécifiés comme paramètres d’application dans la configuration du site hello. exécution de fonctions d’Azure Hello utilise hello `AzureWebJobsStorage` toocreate les files d’attente interne de chaîne de connexion. Hello la chaîne de connexion `AzureWebJobsDashboard` est utilisé toolog tooAzure Table stockage et la puissance hello **moniteur** hello portail.

Ces propriétés sont spécifiées dans hello `appSettings` collection Bonjour `siteConfig` objet :

```json
"appSettings": [
    {
        "name": "AzureWebJobsStorage",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    },
    {
        "name": "AzureWebJobsDashboard",
        "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
    }
```    

### <a name="hosting-plan"></a>Plan d’hébergement

définition de Hello Hello plan d’hébergement varie selon que vous utilisez un plan de la consommation ou du Service d’applications. Consultez [déployer une application de fonction sur le plan de la consommation hello](#consumption) et [déployer une application de fonction sur hello plan App Service](#app-service-plan).

### <a name="function-app"></a>Conteneur de fonctions

ressources d’application Hello fonction est définie à l’aide d’une ressource de type **Microsoft.Web/Site** et type **functionapp**:

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ]
```

<a name="consumption"></a>

## <a name="deploy-a-function-app-on-hello-consumption-plan"></a>Déployer une application de fonction sur le plan de la consommation de hello

Vous pouvez exécuter une application de la fonction dans deux modes différents : hello du plan de la consommation et hello plan App Service. plan de la consommation Hello alloue automatiquement la puissance de calcul lorsque votre code est en cours d’exécution, peut évoluer en tant que charge de toohandle nécessaires, puis met à l’échelle vers le bas lorsque le code n’est pas en cours d’exécution. Par conséquent, vous n’avez pas toopay pour les machines virtuelles inactives, et vous n’avez pas la capacité de tooreserve à l’avance. toolearn en savoir plus sur l’hébergement des plans, consultez [plans de consommation de fonctions d’Azure et le Service application](functions-scale.md).

Pour un exemple de modèle Azure Resource Manager, consultez [Function app on Consumption plan] (Application de fonction dans le plan Consommation).

### <a name="create-a-consumption-plan"></a>Créer un plan Consommation

Un plan Consommation est un type spécial de ressource « serverfarm ». Vous la spécifiez à l’aide de hello `Dynamic` valeur hello `computeMode` et `sku` propriétés :

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "computeMode": "Dynamic",
        "sku": "Dynamic"
    }
}
```

### <a name="create-a-function-app"></a>Créer une Function App

En outre, un plan de la consommation nécessite deux paramètres supplémentaires dans la configuration du site hello : `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING` et `WEBSITE_CONTENTSHARE`. Ces propriétés configurer hello stockage compte et le fichier de chemin d’accès où le code d’application hello fonction et la configuration sont stockés.

```json
{
    "apiVersion": "2015-08-01",
    "type": "Microsoft.Web/sites",
    "name": "[variables('functionAppName')]",
    "location": "[resourceGroup().location]",
    "kind": "functionapp",            
    "dependsOn": [
        "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
    ],
    "properties": {
        "serverFarmId": "[resourceId('Microsoft.Web/serverfarms', variables('hostingPlanName'))]",
        "siteConfig": {
            "appSettings": [
                {
                    "name": "AzureWebJobsDashboard",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "AzureWebJobsStorage",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTAZUREFILECONNECTIONSTRING",
                    "value": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
                },
                {
                    "name": "WEBSITE_CONTENTSHARE",
                    "value": "[toLower(variables('functionAppName'))]"
                },
                {
                    "name": "FUNCTIONS_EXTENSION_VERSION",
                    "value": "~1"
                }
            ]
        }
    }
}
```                    

<a name="app-service-plan"></a> 

## <a name="deploy-a-function-app-on-hello-app-service-plan"></a>Déployer une application de fonction sur hello plan App Service

Bonjour plan App Service, votre application de la fonction s’exécute sur des machines virtuelles dédiées sur Basic, Standard et Premium SKU, les applications tooweb similaire. Pour plus d’informations sur le fonctionne de hello plan App Service, consultez hello [vue d’ensemble approfondie des plans de Service d’applications Azure](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md). 

Pour un exemple de modèle Azure Resource Manager, consultez [Function app on Azure App Service plan] (Application de fonction dans le plan Azure App Service).

### <a name="create-an-app-service-plan"></a>Créer un plan App Service

```json
{
    "type": "Microsoft.Web/serverfarms",
    "apiVersion": "2015-04-01",
    "name": "[variables('hostingPlanName')]",
    "location": "[resourceGroup().location]",
    "properties": {
        "name": "[variables('hostingPlanName')]",
        "sku": "[parameters('sku')]",
        "workerSize": "[parameters('workerSize')]",
        "hostingEnvironment": "",
        "numberOfWorkers": 1
    }
}
```

### <a name="create-a-function-app"></a>Créer une application de fonction 

Une fois que vous avez sélectionné une option de mise à l’échelle, créez une application de fonction. application Hello est un conteneur hello qui contient toutes vos fonctions.

Une application de fonction dispose de nombreuses ressources enfant que vous pouvez utiliser dans votre développement, notamment les paramètres de l’application et les options de contrôle de code source. Vous pouvez également choisir tooremove hello **sourcecontrols** ressource enfant et utilisez une autre [l’option de déploiement](functions-continuous-deployment.md) à la place.

> [!IMPORTANT]
> toosuccessfully déployer votre application à l’aide du Gestionnaire de ressources Azure, il est important toounderstand comment les ressources sont déployées dans Azure. Bonjour l’exemple suivant, les configurations de niveau supérieur sont appliquées à l’aide de **configuration**. Il est important tooset ces configurations à un haut niveau, car ils fournissent des informations toohello fonctions runtime et le déploiement du moteur. Informations de niveau supérieur sont requis avant les enfants hello **sourcecontrols/web** ressource est appliquée. Bien qu’il soit possible de tooconfigure ces paramètres dans hello niveau enfant **configuration/appSettings** ressource, dans certains cas, votre application de la fonction doit être déployée *avant* **configuration/appSettings**  est appliqué. Par exemple, quand vous utilisez des fonctions avec [Logic Apps](../logic-apps/index.md), vos fonctions sont une dépendance d’une autre ressource.

```json
{
  "apiVersion": "2015-08-01",
  "name": "[parameters('appName')]",
  "type": "Microsoft.Web/sites",
  "kind": "functionapp",
  "location": "[parameters('location')]",
  "dependsOn": [
    "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]",
    "[resourceId('Microsoft.Web/serverfarms', parameters('appName'))]"
  ],
  "properties": {
     "serverFarmId": "[variables('appServicePlanName')]",
     "siteConfig": {
        "alwaysOn": true,
        "appSettings": [
            { "name": "FUNCTIONS_EXTENSION_VERSION", "value": "~1" },
            { "name": "Project", "value": "src" }
        ]
     }
  },
  "resources": [
     {
        "apiVersion": "2015-08-01",
        "name": "appsettings",
        "type": "config",
        "dependsOn": [
          "[resourceId('Microsoft.Web/Sites', parameters('appName'))]",
          "[resourceId('Microsoft.Web/Sites/sourcecontrols', parameters('appName'), 'web')]",
          "[resourceId('Microsoft.Storage/storageAccounts', variables('storageAccountName'))]"
        ],
        "properties": {
          "AzureWebJobsStorage": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]",
          "AzureWebJobsDashboard": "[concat('DefaultEndpointsProtocol=https;AccountName=', variables('storageAccountName'), ';AccountKey=', listKeys(variables('storageAccountid'),'2015-05-01-preview').key1)]"
        }
     },
     {
          "apiVersion": "2015-08-01",
          "name": "web",
          "type": "sourcecontrols",
          "dependsOn": [
            "[resourceId('Microsoft.Web/sites/', parameters('appName'))]"
          ],
          "properties": {
            "RepoUrl": "[parameters('sourceCodeRepositoryURL')]",
            "branch": "[parameters('sourceCodeBranch')]",
            "IsManualIntegration": "[parameters('sourceCodeManualIntegration')]"
          }
     }
  ]
}
```
> [!TIP]
> Ce modèle utilise hello [projet](https://github.com/projectkudu/kudu/wiki/Customizing-deployments#using-app-settings-instead-of-a-deployment-file) valeur de paramètres d’application qui définit le répertoire de base hello dans le hello moteur de déploiement de fonctions (Kudu) recherche de code pouvant être déployée. Dans notre référentiel, nos fonctions se trouvent dans un sous-dossier de hello **src** dossier. Par conséquent, dans hello précédent exemple, nous avons défini valeur de paramètres d’application hello trop`src`. Si vos fonctions se trouvent dans votre référentiel racine hello, ou si vous ne déployez pas de contrôle de code source, vous pouvez supprimer cette valeur de paramètres d’application.

## <a name="deploy-your-template"></a>Déployer votre modèle

Vous pouvez utiliser les Hello suivant façons toodeploy votre modèle :

* [PowerShell](../azure-resource-manager/resource-group-template-deploy.md)
* [Interface de ligne de commande Azure](../azure-resource-manager/resource-group-template-deploy-cli.md)
* [Portail Azure](../azure-resource-manager/resource-group-template-deploy-portal.md)
* [API REST](../azure-resource-manager/resource-group-template-deploy-rest.md)

### <a name="deploy-tooazure-button"></a>TooAzure bouton déployer

Remplacez ```<url-encoded-path-to-azuredeploy-json>``` avec un [encodé en URL](https://www.bing.com/search?q=url+encode) version du chemin d’accès brutes de hello de votre `azuredeploy.json` fichier dans GitHub.

Voici un exemple qui utilise markdown :

```markdown
[![Deploy tooAzure](http://azuredeploy.net/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>)
```

Voici un exemple qui utilise HTML :

```html
<a href="https://portal.azure.com/#create/Microsoft.Template/uri/<url-encoded-path-to-azuredeploy-json>" target="_blank"><img src="http://azuredeploy.net/deploybutton.png"></a>
```

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur la façon de toodevelop et configurer les fonctions d’Azure.

* [Référence du développeur Azure Functions](functions-reference.md)
* [Fonctionnement des paramètres de l’application tooconfigure Azure](functions-how-to-use-azure-function-app-settings.md)
* [Créer votre première fonction Azure](functions-create-first-azure-function.md)

<!-- LINKS -->

[Function app on Consumption plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dynamic/azuredeploy.json (Application de fonction dans le plan Consommation)
[Function app on Azure App Service plan]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-function-app-create-dedicated/azuredeploy.json (Application de fonction dans le plan Azure App Service)
