---
title: aaaExporting des groupes de ressources Azure qui contiennent des extensions de machine virtuelle | Documents Microsoft
description: "Exportez des modèles Resource Manager qui incluent des extensions de machine virtuelle."
services: virtual-machines-windows
documentationcenter: 
author: neilpeterson
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 7f4e2ca6-f1c7-4f59-a2cc-8f63132de279
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 12/05/2016
ms.author: nepeters
ms.openlocfilehash: cdbc2030988a19fe68429e8733dc60536c264abf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="exporting-resource-groups-that-contain-vm-extensions"></a>Exportation de groupes de ressources contenant des extensions de machine virtuelle

Des groupes de ressources Azure peuvent être exportés dans un nouveau modèle Resource Manager qui peut alors être redéployé. Hello processus d’exportation interprète les ressources existantes et crée un modèle de gestionnaire de ressources que lors du déploiement des résultats dans un groupe de ressources similaires. Lorsque vous utilisez l’option d’exportation hello groupe de ressources par rapport à un groupe de ressources contenant les extensions de Machine virtuelle, toobe de besoin de plusieurs éléments considérées comme telles que de la compatibilité d’extension et protégés de paramètres.

Ce document décrit en détail le fonctionnement de hello processus d’exportation de groupe de ressources en ce qui concerne les extensions de machine virtuelle, notamment une liste de prise en charge les extensions, et plus d’informations sur la gestion des données sécurisées.

## <a name="supported-virtual-machine-extensions"></a>Extensions de machine virtuelle prises en charge

De nombreuses extensions de machine virtuelle sont disponibles. Toutes les extensions ne peuvent être exportées dans un modèle de gestionnaire de ressources à l’aide de la fonctionnalité de « Script d’automatisation » hello. Si une extension de machine virtuelle n’est pas pris en charge, il doit toobe manuellement replacée dans les modèles exportés hello.

Hello extensions suivantes peuvent être exportées avec la fonctionnalité de script d’automation hello.

| Extension ||||
|---|---|---|---|
| Sauvegarde Acronis | Agent Datadog Windows | Application de correctifs au système d’exploitation pour Linux | Instantané de machine virtuelle Linux
| Sauvegarde Acronis Linux | Extension Docker | Agent Puppet |
| Infos Bg | Extension DSC | Aperçu Apm 24 x 7 de site |
| Agent BMC CTM Linux | Dynatrace Linux | Serveur Linux 24 x 7 de site |
| Agent BMC CTM Windows | Dynatrace Windows | Windows Server 24 x 7 de site |
| Client Chef | Application de sécurité HPE Defender | Trend Micro DSA |
| Script personnalisé | Logiciel anti-programme malveillant IaaS | Trend Micro DSA Linux |
| Extension de script personnalisé | Diagnostics IaaS | Accès aux machines virtuelles pour Linux |
| Script personnalisé pour Linux | Client Chef Linux | Accès aux machines virtuelles pour Linux |
| Agent Datadog Linux | Diagnostic Linux | Instantané de machine virtuelle |

## <a name="export-hello-resource-group"></a>Exportation hello groupe de ressources

tooexport un groupe de ressources dans un modèle réutilisable, hello complète comme suit :

1. Se connecter toohello portail Azure
2. Sur hello Menu Hub, cliquez sur groupes de ressources
3. Sélectionnez le groupe de ressources cible hello à partir de la liste de hello
4. Dans le panneau de groupe de ressources hello, cliquez sur le Script d’automatisation

![Exportation de modèle](./media/extensions-export-templates/template-export.png)

Hello script automatisations de Azure Resource Manager génère un modèle de gestionnaire de ressources, un fichier de paramètres et plusieurs exemples de scripts de déploiement tels que PowerShell et CLI d’Azure. À ce stade, les modèles exportés hello peuvent être téléchargé à l’aide du bouton de téléchargement hello, ajouté en tant que nouveau modèle toohello modèle bibliothèque ou déployé à l’aide de hello bouton déployer.

## <a name="configure-protected-settings"></a>Configurer les paramètres protégés

Plusieurs extensions de machine virtuelle Azure incluent une configuration de paramètres protégés, qui chiffre les données sensibles telles que les informations d’identification et les chaînes de configuration. Les paramètres protégés ne sont pas exportés avec script d’automatisation hello. Si les paramètres nécessaires, protégés doivent toobe réinséré hello exportée basé sur un modèle.

### <a name="step-1---remove-template-parameter"></a>Étape 1 : Supprimer un paramètre de modèle

Lorsque hello que groupe de ressources sont exporté, un paramètre de modèle unique est créé tooprovide un toohello valeur exporté les paramètres protégés. Ce paramètre peut être supprimé. tooremove hello, examinez la liste de paramètres hello et supprimer le paramètre hello qui recherche d’exemple JSON toothis similaire.

```json
"extensions_extensionname_protectedSettings": {
    "defaultValue": null,
    "type": "SecureObject"
}
```

### <a name="step-2---get-protected-settings-properties"></a>Étape 2 : Obtenir les propriétés des paramètres protégés

Étant donné que chaque paramètre protégé a un jeu de propriétés requis, une liste de ces propriétés doivent toobe collectée. Vous trouverez chaque paramètre de configuration des paramètres protégés hello Bonjour [schéma Azure Resource Manager sur GitHub](https://raw.githubusercontent.com/Azure/azure-resource-manager-schemas/master/schemas/2015-08-01/Microsoft.Compute.json). Ce schéma inclut uniquement les jeux de paramètres hello pour les extensions hello répertoriées dans la section vue d’ensemble de hello de ce document. 

Dans le référentiel de schéma hello, de rechercher les extension hello que vous le souhaitez, pour cet exemple `IaaSDiagnostics`. Une fois hello extensions `protectedSettings` objet a été trouvé, prenez note de chaque paramètre. Dans l’exemple hello Hello `IaasDiagnostic` extension, hello requièrent les paramètres sont `storageAccountName`, `storageAccountKey`, et `storageAccountEndPoint`.

```json
"protectedSettings": {
    "type": "object",
    "properties": {
        "storageAccountName": {
            "type": "string"
        },
        "storageAccountKey": {
            "type": "string"
        },
        "storageAccountEndPoint": {
            "type": "string"
        }
    },
    "required": [
        "storageAccountName",
        "storageAccountKey",
        "storageAccountEndPoint"
    ]
}
```

### <a name="step-3---re-create-hello-protected-configuration"></a>Étape 3 - créer de nouveau la configuration de hello protégé

On hello modèle exporté, recherchez `protectedSettings` et remplacer hello exportée protégé définition de l’objet avec une autre qui inclut des paramètres d’extension hello requis et une valeur pour chacun d’eux.

Dans l’exemple hello Hello `IaasDiagnostic` extension, nouvelle configuration de paramètre protégé hello ressemblerait hello l’exemple suivant :

```json
"protectedSettings": {
    "storageAccountName": "[parameters('storageAccountName')]",
    "storageAccountKey": "[parameters('storageAccountKey')]",
    "storageAccountEndPoint": "https://core.windows.net"
}
```

ressource d’extension finale Hello ressemble toohello comme exemple de JSON suivant :

```json
{
    "name": "Microsoft.Insights.VMDiagnosticsSettings",
    "type": "extensions",
    "location": "[resourceGroup().location]",
    "apiVersion": "[variables('apiVersion')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
    ],
    "tags": {
        "displayName": "AzureDiagnostics"
    },
    "properties": {
        "publisher": "Microsoft.Azure.Diagnostics",
        "type": "IaaSDiagnostics",
        "typeHandlerVersion": "1.5",
        "autoUpgradeMinorVersion": true,
        "settings": {
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), variables('wadmetricsresourceid'), variables('vmName'), variables('wadcfgxend')))]",
            "storageAccount": "[parameters('existingdiagnosticsStorageAccountName')]"
        },
        "protectedSettings": {
            "storageAccountName": "[parameters('storageAccountName')]",
            "storageAccountKey": "[parameters('storageAccountKey')]",
            "storageAccountEndPoint": "https://core.windows.net"
        }
    }
}
```

Si vous utilisez des valeurs de propriété tooprovide modèle paramètres, ceux-ci doivent toobe créé. Lorsque vous créez des paramètres de modèle pour les valeurs de paramètre de protection par, assurez-vous que toouse hello `SecureString` le type de paramètre, afin que les valeurs sensibles sont sécurisés. Pour en savoir plus sur l’utilisation des paramètres, consultez [Création de modèles Azure Resource Manager](../../resource-group-authoring-templates.md).

Dans l’exemple hello Hello `IaasDiagnostic` extension, hello paramètres suivants est créé dans la section des paramètres de modèle de gestionnaire de ressources hello hello.

```json
"storageAccountName": {
    "defaultValue": null,
    "type": "SecureString"
},
"storageAccountKey": {
    "defaultValue": null,
    "type": "SecureString"
}
```

À ce stade, le modèle de hello peut être déployé à l’aide de n’importe quelle méthode de déploiement de modèle.
