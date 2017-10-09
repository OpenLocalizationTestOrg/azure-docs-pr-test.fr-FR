---
title: "modèles d’aaaDevelop pour la pile de Azure | Documents Microsoft"
description: "Découvrir les meilleures pratiques en matière de modèles Azure Stack"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 8a5bc713-6f51-49c8-aeed-6ced0145e07b
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 01581abcb7a3616469dcd38a646734f68decd3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-considerations"></a>Considérations relatives au modèle Azure Resource Manager
Lorsque vous développez votre application, il est important tooensure la portabilité de modèle entre Azure et Azure pile.  Cette rubrique fournit des considérations de développement Azure Resource Manager [modèles](http://download.microsoft.com/download/E/A/4/EA4017B5-F2ED-449A-897E-BD92E42479CE/Getting_Started_With_Azure_Resource_Manager_white_paper_EN_US.pdf), pour vous permettre de prototype de votre déploiement d’application et de test dans Azure sans environnement de Azure pile tooan access.

## <a name="public-namespaces"></a>Espaces de noms publics
Parce que la pile de Azure est hébergé dans votre centre de données, il a des espaces de noms service autre point de terminaison à hello cloud public Azure. Par conséquent, codé en dur des points de terminaison publics dans les modèles de gestionnaire de ressources échouent lorsque vous essayez de toodeploy les tooAzure pile. Au lieu de cela, vous pouvez utiliser hello *référence* et *concaténer* fonction toodynamically générer le point de terminaison de service hello en fonction des valeurs extraites du fournisseur de ressources hello lors du déploiement. Par exemple, plutôt que de spécifier *blob.core.windows.net* dans votre modèle, récupérer hello [primaryEndpoints.blob](https://github.com/Azure/AzureStack-QuickStart-Templates/blob/master/101-simple-windows-vm/azuredeploy.json#L201) toodynamically définir hello *osDisk.URI* point de terminaison :

     "osDisk": {"name": "osdisk","vhd": {"uri": 
     "[concat(reference(concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName')), '2015-06-15').primaryEndpoints.blob, variables('vmStorageAccountContainerName'),
      '/',variables('OSDiskName'),'.vhd')]"}}

## <a name="api-versioning"></a>Contrôle de version d’API
Les versions de service Azure peuvent différer entre Azure et Azure Stack. Chaque ressource requiert l’attribut hello apiVersion, qui définit les fonctions hello. compatibilité des versions tooensure API dans la pile de Azure, hello suivant sont des versions d’API valides pour chaque fournisseur de ressources :

| Fournisseur de ressources | apiVersion |
| --- | --- |
| Calcul |`'2015-06-15'` |
| Réseau |`'2015-06-15'`, `'2015-05-01-preview'` |
| Storage |`'2016-01-01'`, `'2015-06-15'`, `'2015-05-01-preview'` |
| KeyVault | `'2015-06-01'` |
| App Service |`'2015-08-01'` |
| MySQL |`'2015-09-01'` |
| SQL |`'2014-04-01-preview'` |

## <a name="template-functions"></a>Fonctions des modèles de gestionnaire des ressources Azure
Le Gestionnaire de ressources [fonctions](../azure-resource-manager/resource-group-template-functions.md) fournissent des modèles dynamiques toobuild requis de fonctionnalités. Par exemple, vous pouvez utiliser des fonctions pour des tâches telles que :

* la concaténation ou la troncation des chaînes ; 
* le référencement de valeurs d’autres ressources ;
* Une itération sur les ressources toodeploy plusieurs instances 

Lorsque vous créez vos modèles, certaines fonctions ne sont pas disponibles dans le kit de développement Azure Stack et ne doivent pas être utilisées. Ces fonctions sont les suivantes :

* Skip
* Take

## <a name="resource-location"></a>Emplacement des ressources
Modèles du Gestionnaire de ressources utilisent un emplacement attribut tooplace des ressources pendant le déploiement. Dans Azure, emplacements renvoient tooa la région ouest des États-Unis ou en Amérique du Sud. Dans Azure Stack, les emplacements sont différents, car Azure Stack est situé dans votre centre de données.  tooensure modèles peuvent être transférées entre Azure et de la pile d’Azure, vous devez référencer emplacement du groupe de ressources hello lorsque vous déployez des ressources individuelles. Ce faire, vous pouvez utiliser `[resourceGroup().Location]` tooensure héritent de toutes les ressources hello emplacement du groupe de ressources.  Bonjour extrait de modèle de gestionnaire de ressources suivant est un exemple d’utilisation de cette fonction lors du déploiement d’un compte de stockage :

    "resources": [
    {
      "name": "[variables('storageAccountName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "[variables('apiVersionStorage')]",
      "location": "[resourceGroup().location]",
      "comments": "This storage account is used toostore hello VM disks",
      "properties": {
      "accountType": "Standard_GRS"
      }
    }
    ]


## <a name="next-steps"></a>Étapes suivantes
* [Déployer des modèles avec PowerShell](azure-stack-deploy-template-powershell.md)
* [Déployer des modèles avec l’interface de ligne de commande Azure](azure-stack-deploy-template-command-line.md)
* [Déployer des modèles avec Visual Studio](azure-stack-deploy-template-visual-studio.md)

