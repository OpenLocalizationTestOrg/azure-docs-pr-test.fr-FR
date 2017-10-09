---
title: "aaaDeploy une application sur un ensemble d’échelle de machine virtuelle Azure | Documents Microsoft"
description: "En savoir plus toodeploy une application simple d’échelle sur une échelle de machine virtuelle à l’aide d’un modèle Azure Resource Manager."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Déploiement d’une application de mise à l’échelle à l’aide d’un modèle

[Les modèles de gestionnaire de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) est un excellent moyen toodeploy groupes de ressources liées. Ce didacticiel s’appuie [déployer un ensemble d’échelle simple](virtual-machine-scale-sets-mvss-start.md) et décrit le toodeploy une application simple d’échelle sur une échelle à l’aide d’un modèle Azure Resource Manager.  Vous pouvez également configurer échelle à l’aide de PowerShell, CLI ou hello portail. Pour plus d’informations, consultez [Vue d’ensemble de la mise à l’échelle automatique](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>Deux modèles de démarrage rapide
Lorsque vous déployez un jeu de mise à l’échelle, vous pouvez installer de nouveaux logiciels sur une image de plateforme à l’aide d’une [extension de machine virtuelle](../virtual-machines/virtual-machines-windows-extensions-features.md). Les extensions de machine virtuelle sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure, comme le déploiement d’une application. Deux modèles différents sont fournis dans [Azure/azure-démarrage rapide-modèles](https://github.com/Azure/azure-quickstart-templates) qui indiquent comment une application de l’échelle automatique sur une échelle de toodeploy définie à l’aide des extensions de machine virtuelle.

### <a name="python-http-server-on-linux"></a>Serveur HTTP Python sur Linux
Hello [serveur HTTP de Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) exemple de modèle déploie une application simple échelle en cours d’exécution sur un ensemble d’échelle Linux.  [Bouteille](http://bottlepy.org/docs/dev/), une infrastructure web de Python et un serveur HTTP simple sont déployés sur chaque machine virtuelle dans l’échelle de hello définie à l’aide d’un script personnalisé, extension de machine virtuelle. mise à l’échelle Hello définie échelles lors de l’utilisation moyenne du processeur sur tous les ordinateurs virtuels est supérieur à 60 % de mise à l’échelle lorsque hello utilisation moyenne du processeur est inférieure à 30 %.

En outre toohello ensemble d’échelle de ressource, hello *azuredeploy.json* exemple de modèle déclare également le réseau virtuel, adresse IP publique, équilibrage de charge et les ressources de paramètres de mise à l’échelle.  Pour plus d’informations sur la création de ces ressources dans un modèle, consultez la page [Jeu de mise à l’échelle Linux avec mise à l’échelle automatique](virtual-machine-scale-sets-linux-autoscale.md).

Bonjour *azuredeploy.json* modèle, hello `extensionProfile` propriété Hello `Microsoft.Compute/virtualMachineScaleSets` ressource spécifie une extension de script personnalisé. `fileUris`Spécifie l’emplacement des scripts hello. Dans ce cas, deux fichiers : *workserver.py*, qui définit un serveur HTTP simple, et *installserver.sh*, qui est installé d’eau et démarre hello serveur HTTP. `commandToExecute`Spécifie les hello commande toorun après avoir déployé un ensemble d’échelle hello.

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a>Application ASP.NET MVC sur Windows
Hello [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) exemple de modèle déploie une application ASP.NET MVC simple s’exécutant dans IIS sur l’ensemble d’échelle de Windows.  IIS et hello application MVC sont déployés à l’aide de hello [PowerShell souhaité (DSC de) la configuration d’état](virtual-machine-scale-sets-dsc.md) extension de machine virtuelle.  mise à l’échelle Hello configurer échelles (sur l’instance de la machine virtuelle à la fois) lorsque l’utilisation du processeur est supérieur à 50 % pendant 5 minutes. 

En outre toohello ensemble d’échelle de ressource, hello *azuredeploy.json* exemple de modèle déclare également le réseau virtuel, adresse IP publique, équilibrage de charge et les ressources de paramètres de mise à l’échelle. Ce modèle illustre également la mise à niveau de l’application.  Pour plus d’informations sur la création de ces ressources dans un modèle, consultez la page [Jeu de mise à l’échelle Windows avec mise à l’échelle automatique](virtual-machine-scale-sets-windows-autoscale.md).

Bonjour *azuredeploy.json* modèle, hello `extensionProfile` propriété Hello `Microsoft.Compute/virtualMachineScaleSets` ressource spécifie un [configuration d’état souhaité (DSC)](virtual-machine-scale-sets-dsc.md) extension qui installe IIS et une valeur par défaut application Web à partir d’un package Web Deploy.  Hello *IISInstall.ps1* script installe IIS sur l’ordinateur virtuel de hello et se trouve dans hello *DSC* dossier.  application web MVC est Hello se trouve dans hello *WebDeploy* dossier.  script d’installation toohello Hello chemins d’accès et de l’application web hello sont définis dans hello `powershelldscZip` et `webDeployPackage` paramètres Bonjour *azuredeploy.parameters.json* fichier. 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a>Déployer le modèle de hello
hello toodeploy façon la plus simple de Hello [serveur HTTP de Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modèle est toouse hello **déployer tooAzure** bouton trouvé Bonjour dans les fichiers Lisez-moi de hello dans GitHub.  Vous pouvez également utiliser PowerShell ou CLI d’Azure toodeploy hello exemples de modèles.

### <a name="powershell"></a>PowerShell
Hello de copie [serveur HTTP de Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) fichiers à partir du dossier de tooa hello GitHub dépôt sur votre ordinateur local.  Ouvrez hello *azuredeploy.parameters.json* fichier et mise à jour des valeurs par défaut hello Hello `vmssName`, `adminUsername`, et `adminPassword` paramètres. Enregistrer hello suite du script PowerShell trop*deploy.ps1* Bonjour même dossier que hello *azuredeploy.json* modèle. toodeploy Bonjour exemple modèle exécuter Bonjour *deploy.ps1* script à partir d’une fenêtre de commande PowerShell.

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a>Interface de ligne de commande Azure
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a>Étapes suivantes

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
