---
title: "modèles de toocheck aaaUse validateur de modèle pour la pile de Azure | Documents Microsoft"
description: "Vérifier les modèles de déploiement tooAzure pile"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: d9e6aee1-4cba-4df5-b5a3-6f38da9627a3
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: helaw
ms.openlocfilehash: ee649f2ebf77486ca5036116dd73a45d66884704
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="check-your-templates-for-azure-stack-with-template-validator"></a>Vérifier vos modèles pour Azure Stack par le validateur de modèle
Vous pouvez utiliser toocheck d’outil de validation de modèle hello si votre gestionnaire de ressources Azure [modèles](azure-stack-arm-templates.md) sont prêts pour la pile de Azure. outil de validation de modèle Hello est disponible dans le cadre des outils de pile de Azure hello. Télécharger les outils de pile de Azure hello à l’aide de hello étapes de hello [télécharger les outils à partir de GitHub](azure-stack-powershell-download.md) l’article. 

les modèles toovalidate, vous utilisez hello suivant des modules PowerShell et hello JSON fichier situé dans **TemplateValidator** et **CloudCapabilities** dossiers : 

 - AzureRM.CloudCapabilities.psm1 crée un fichier JSON de fonctionnalités cloud représentant les services hello et les versions dans un cloud comme Azure pile.
 - AzureRM.TemplateValidator.psm1 utilise un modèles de tootest de fichiers JSON des capacités du cloud pour le déploiement dans la pile de Azure.
 - AzureStackCloudCapabilities_with_AddOns_20170627.json est un fichier des fonctionnalités du cloud par défaut.  Vous pouvez créer vos propres ou utiliser ce tooget fichier a démarré. 

Dans cette rubrique, vous aller exécuter une validation de vos modèles, et éventuellement générer un fichier des fonctionnalités du cloud.

## <a name="validate-templates"></a>Valider des modèles
Dans ces étapes, valider les modèles à l’aide du module PowerShell de AzureRM.TemplateValidator de hello. Vous pouvez utiliser vos propres modèles, ou valider hello [modèles de démarrage rapide de pile Azure](https://github.com/Azure/AzureStack-QuickStart-Templates).

1.  Module d’importation hello AzureRM.TemplateValidator.psm1 PowerShell :
    
    ```PowerShell
    cd "c:\AzureStack-Tools-master\TemplateValidator"
    Import-Module .\AzureRM.TemplateValidator.psm1
    ```

2.  Validateur de modèle hello, exécutez :

    ```PowerShell
    Test-AzureRMTemplate -TemplatePath <path tootemplate.json or template folder> `
    -CapabilitiesPath <path toocloudcapabilities.json> `
    -Verbose
    ```

Les avertissements de validation de modèle ou les erreurs sont journalisées toohello PowerShell console et sont également consignées tooan HTML fichier dans le répertoire source hello. Un exemple de sortie de rapport de validation hello ressemble à ceci :

![exemple de rapport de validation](./media/azure-stack-validate-templates/image1.png)

### <a name="parameters"></a>Paramètres

| Paramètre | Description | Requis |
| ----- | -----| ----- |
| TemplatePath | Spécifie toorecursively de chemin d’accès hello trouver des modèles de gestionnaire de ressources | Oui | 
| TemplatePattern | Spécifie le nom hello de toomatch des fichiers de modèle. | Non |
| CapabilitiesPath | Spécifie le fichier JSON fonctionnalités hello chemin d’accès toocloud | Oui | 
| IncludeComputeCapabilities | Inclut l’évaluation de ressources IaaS telles que des tailles de machine virtuelle et des extensions de machine virtuelle | Non |
| IncludeStorageCapabilities | Inclut l’évaluation de ressources de stockage comme des types de références (SKU) | Non |
| Rapport | Spécifie le nom de hello le rapport HTML généré | Non |
| Détaillé | Console de toohello de journaux des erreurs et avertissements | Non|


### <a name="examples"></a>Exemples
Cet exemple valide tous les hello [modèles de démarrage rapide de pile Azure](https://github.com/Azure/AzureStack-QuickStart-Templates) téléchargé localement et valide également les tailles de machine virtuelle hello et des extensions par rapport aux fonctionnalités du Kit de développement de pile Azure.

```PowerShell
test-AzureRMTemplate -TemplatePath C:\AzureStack-Quickstart-Templates `
-CapabilitiesPath .\TemplateValidator\AzureStackCloudCapabilities_with_AddOns_20170627.json.json `
-TemplatePattern MyStandardTemplateName.json`
-IncludeComputeCapabilities`
-Report TemplateReport.html
```

## <a name="build-cloud-capabilities-file"></a>Générer le fichier des fonctionnalités du cloud
les fichiers téléchargés Hello incluent une valeur par défaut *AzureStackCloudCapabilities_with_AddOns_20170627.json* fichier, qui décrit les versions de service hello disponibles dans le Kit de développement Azure pile avec les services PaaS.  Si vous installez des fournisseurs de ressources supplémentaires, vous pouvez utiliser un fichier JSON, y compris les nouveaux services de hello hello AzureRM.CloudCapabilities PowerShell module toobuild.  

1.  Assurez-vous que vous disposez de connectivité tooAzure pile.  Ces étapes peuvent être effectuées à partir de l’hôte de kit de développement de Azure pile hello, ou vous pouvez utiliser [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooconnect à partir de votre station de travail. 
2.  Importez hello module AzureRM.CloudCapabilities PowerShell :

    ```PowerShell
    Import-Module .\CloudCapabilities\AzureRM.CloudCapabilities.psm1
    ``` 

3.  Utilisez des versions de service de tooretrieve applet de commande Get-CloudCapabilities de hello et créer un fichier JSON de fonctionnalités cloud :

    ```PowerShell
    Get-AzureRMCloudCapabilities -Location 'local' -Verbose
    ```             


## <a name="next-steps"></a>Étapes suivantes
 - [Déployer des modèles tooAzure pile](azure-stack-arm-templates.md)
 - [Développer des modèles pour Azure Stack] (azure-stack-develop-templates.md)

