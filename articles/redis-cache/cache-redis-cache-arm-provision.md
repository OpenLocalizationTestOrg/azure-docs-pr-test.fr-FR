---
title: "aaaProvision un Cache Redis à l’aide du Gestionnaire de ressources Azure | Documents Microsoft"
description: "Utilisez le Gestionnaire de ressources Azure modèle toodeploy un cache Azure Redis Cache."
services: app-service
documentationcenter: 
author: steved0x
manager: douge
editor: 
ms.assetid: ce6f5372-7038-4655-b1c5-108f7c148282
ms.service: cache
ms.workload: web
ms.tgt_pltfrm: cache-redis
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: sdanie
ms.openlocfilehash: 46e7b3b2493ac51dbe6bab0b086304802afc5d48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-redis-cache-using-a-template"></a>Créer un cache Redis à l’aide d’un modèle
Dans cette rubrique, vous apprendrez comment toocreate un modèle Azure Resource Manager qui déploie un Azure Redis Cache. cache de Hello peut être utilisé avec un stockage compte tookeep diagnostic des données existantes. Vous apprendrez également comment toodefine les ressources qui sont déployés et comment les paramètres toodefine sont spécifiés lorsque le déploiement de hello est exécutée. Vous pouvez utiliser ce modèle pour vos propres déploiements, ou personnaliser toomeet vos besoins.

Actuellement, les paramètres de diagnostic sont partagés pour tous les caches Bonjour même région pour un abonnement. Mise à jour un cache dans la région de hello affecte tous les autres caches dans la région de hello.

Pour en savoir plus sur la création de modèles, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Pour le modèle complète de hello, consultez [modèle de Cache Redis](https://github.com/Azure/azure-quickstart-templates/blob/master/101-redis-cache/azuredeploy.json).

> [!NOTE]
> Modèles de gestionnaire de ressources pour hello nouvelle [niveau Premium](cache-premium-tier-intro.md) sont disponibles. 
> 
> * [Créer un cache Redis Premium avec le clustering](https://azure.microsoft.com/documentation/templates/201-redis-premium-cluster-diagnostics/)
> * [Créer un cache Redis Premium avec la persistance des données](https://azure.microsoft.com/documentation/templates/201-redis-premium-persistence/)
> * [Créer un cache Redis Premium avec un réseau virtuel et le clustering facultatif](https://azure.microsoft.com/documentation/templates/201-redis-premium-vnet-cluster-diagnostics/)
> 
> toocheck pour les derniers modèles de hello, consultez [modèles de démarrage rapide Azure](https://azure.microsoft.com/documentation/templates/) et recherchez `Redis Cache`.
> 
> 

## <a name="what-you-will-deploy"></a>Ce que vous allez déployer
Dans ce modèle, vous allez déployer un cache Redis Azure qui utilise un compte de stockage existant pour les données de diagnostic.

toorun hello déploiement automatiquement, cliquez sur hello suivant bouton :

[![Déployer tooAzure](./media/cache-redis-cache-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-redis-cache%2Fazuredeploy.json)

## <a name="parameters"></a>Paramètres
Avec Azure Resource Manager, vous définissez des paramètres pour les valeurs souhaitées toospecify lorsque le modèle de hello est déployé. modèle de Hello inclut une section appelée paramètres qui contient toutes les valeurs de paramètre hello.
Vous devez définir un paramètre pour les valeurs qui varient en fonction de projet que vous déployez hello ou dans l’environnement hello que vous effectuez le déploiement. Ne définissez pas de paramètres pour les valeurs qui doivent restent hello identiques. Chaque valeur de paramètre est utilisé dans hello modèle toodefine hello ressources qui sont déployés. 

[!INCLUDE [app-service-web-deploy-redis-parameters](../../includes/cache-deploy-parameters.md)]

### <a name="rediscachelocation"></a>redisCacheLocation
emplacement Hello Hello du Cache Redis. Pour de meilleures performances, utilisez hello même emplacement que hello toobe application utilisé avec le cache de hello.

    "redisCacheLocation": {
      "type": "string"
    }

### <a name="existingdiagnosticsstorageaccountname"></a>existingDiagnosticsStorageAccountName
nom de Hello de hello toouse du compte stockage existant pour les diagnostics. 

    "existingDiagnosticsStorageAccountName": {
      "type": "string"
    }

### <a name="enablenonsslport"></a>enableNonSslPort
Valeur booléenne qui indique si tooallow accéder via les ports non-SSL.

    "enableNonSslPort": {
      "type": "bool"
    }

### <a name="diagnosticsstatus"></a>diagnosticsStatus
Valeur qui indique si les diagnostics sont activés. Utilisez ON ou OFF.

    "diagnosticsStatus": {
      "type": "string",
      "defaultValue": "ON",
      "allowedValues": [
            "ON",
            "OFF"
        ]
    }

## <a name="resources-toodeploy"></a>Ressources toodeploy
### <a name="redis-cache"></a>Cache Redis
Crée hello du Cache Redis Azure.

    {
      "apiVersion": "2015-08-01",
      "name": "[parameters('redisCacheName')]",
      "type": "Microsoft.Cache/Redis",
      "location": "[parameters('redisCacheLocation')]",
      "properties": {
        "enableNonSslPort": "[parameters('enableNonSslPort')]",
        "sku": {
          "capacity": "[parameters('redisCacheCapacity')]",
          "family": "[parameters('redisCacheFamily')]",
          "name": "[parameters('redisCacheSKU')]"
        }
      },
      "resources": [
        {
          "apiVersion": "2015-07-01",
          "type": "Microsoft.Cache/redis/providers/diagnosticsettings",
          "name": "[concat(parameters('redisCacheName'), '/Microsoft.Insights/service')]",
          "location": "[parameters('redisCacheLocation')]",
          "dependsOn": [
            "[concat('Microsoft.Cache/Redis/', parameters('redisCacheName'))]"
          ],
          "properties": {
            "status": "[parameters('diagnosticsStatus')]",
            "storageAccountName": "[parameters('existingDiagnosticsStorageAccountName')]"
          }
        }
      ]
    }



## <a name="commands-toorun-deployment"></a>Déploiement de toorun de commandes
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -ResourceGroupName ExampleDeployGroup -redisCacheName ExampleCache

### <a name="azure-cli"></a>Interface de ligne de commande Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-redis-cache/azuredeploy.json -g ExampleDeployGroup


