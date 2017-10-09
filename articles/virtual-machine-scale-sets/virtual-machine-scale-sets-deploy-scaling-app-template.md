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
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="66eeb-103">Déploiement d’une application de mise à l’échelle à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="66eeb-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="66eeb-104">[Les modèles de gestionnaire de ressources Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) est un excellent moyen toodeploy groupes de ressources liées.</span><span class="sxs-lookup"><span data-stu-id="66eeb-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="66eeb-105">Ce didacticiel s’appuie [déployer un ensemble d’échelle simple](virtual-machine-scale-sets-mvss-start.md) et décrit le toodeploy une application simple d’échelle sur une échelle à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="66eeb-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="66eeb-106">Vous pouvez également configurer échelle à l’aide de PowerShell, CLI ou hello portail.</span><span class="sxs-lookup"><span data-stu-id="66eeb-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="66eeb-107">Pour plus d’informations, consultez [Vue d’ensemble de la mise à l’échelle automatique](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="66eeb-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="66eeb-108">Deux modèles de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="66eeb-108">Two quickstart templates</span></span>
<span data-ttu-id="66eeb-109">Lorsque vous déployez un jeu de mise à l’échelle, vous pouvez installer de nouveaux logiciels sur une image de plateforme à l’aide d’une [extension de machine virtuelle](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="66eeb-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="66eeb-110">Les extensions de machine virtuelle sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure, comme le déploiement d’une application.</span><span class="sxs-lookup"><span data-stu-id="66eeb-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="66eeb-111">Deux modèles différents sont fournis dans [Azure/azure-démarrage rapide-modèles](https://github.com/Azure/azure-quickstart-templates) qui indiquent comment une application de l’échelle automatique sur une échelle de toodeploy définie à l’aide des extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66eeb-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="66eeb-112">Serveur HTTP Python sur Linux</span><span class="sxs-lookup"><span data-stu-id="66eeb-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="66eeb-113">Hello [serveur HTTP de Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) exemple de modèle déploie une application simple échelle en cours d’exécution sur un ensemble d’échelle Linux.</span><span class="sxs-lookup"><span data-stu-id="66eeb-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="66eeb-114">[Bouteille](http://bottlepy.org/docs/dev/), une infrastructure web de Python et un serveur HTTP simple sont déployés sur chaque machine virtuelle dans l’échelle de hello définie à l’aide d’un script personnalisé, extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66eeb-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="66eeb-115">mise à l’échelle Hello définie échelles lors de l’utilisation moyenne du processeur sur tous les ordinateurs virtuels est supérieur à 60 % de mise à l’échelle lorsque hello utilisation moyenne du processeur est inférieure à 30 %.</span><span class="sxs-lookup"><span data-stu-id="66eeb-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="66eeb-116">En outre toohello ensemble d’échelle de ressource, hello *azuredeploy.json* exemple de modèle déclare également le réseau virtuel, adresse IP publique, équilibrage de charge et les ressources de paramètres de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="66eeb-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="66eeb-117">Pour plus d’informations sur la création de ces ressources dans un modèle, consultez la page [Jeu de mise à l’échelle Linux avec mise à l’échelle automatique](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="66eeb-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="66eeb-118">Bonjour *azuredeploy.json* modèle, hello `extensionProfile` propriété Hello `Microsoft.Compute/virtualMachineScaleSets` ressource spécifie une extension de script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="66eeb-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="66eeb-119">`fileUris`Spécifie l’emplacement des scripts hello.</span><span class="sxs-lookup"><span data-stu-id="66eeb-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="66eeb-120">Dans ce cas, deux fichiers : *workserver.py*, qui définit un serveur HTTP simple, et *installserver.sh*, qui est installé d’eau et démarre hello serveur HTTP.</span><span class="sxs-lookup"><span data-stu-id="66eeb-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="66eeb-121">`commandToExecute`Spécifie les hello commande toorun après avoir déployé un ensemble d’échelle hello.</span><span class="sxs-lookup"><span data-stu-id="66eeb-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="66eeb-122">Application ASP.NET MVC sur Windows</span><span class="sxs-lookup"><span data-stu-id="66eeb-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="66eeb-123">Hello [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) exemple de modèle déploie une application ASP.NET MVC simple s’exécutant dans IIS sur l’ensemble d’échelle de Windows.</span><span class="sxs-lookup"><span data-stu-id="66eeb-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="66eeb-124">IIS et hello application MVC sont déployés à l’aide de hello [PowerShell souhaité (DSC de) la configuration d’état](virtual-machine-scale-sets-dsc.md) extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="66eeb-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="66eeb-125">mise à l’échelle Hello configurer échelles (sur l’instance de la machine virtuelle à la fois) lorsque l’utilisation du processeur est supérieur à 50 % pendant 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="66eeb-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="66eeb-126">En outre toohello ensemble d’échelle de ressource, hello *azuredeploy.json* exemple de modèle déclare également le réseau virtuel, adresse IP publique, équilibrage de charge et les ressources de paramètres de mise à l’échelle.</span><span class="sxs-lookup"><span data-stu-id="66eeb-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="66eeb-127">Ce modèle illustre également la mise à niveau de l’application.</span><span class="sxs-lookup"><span data-stu-id="66eeb-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="66eeb-128">Pour plus d’informations sur la création de ces ressources dans un modèle, consultez la page [Jeu de mise à l’échelle Windows avec mise à l’échelle automatique](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="66eeb-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="66eeb-129">Bonjour *azuredeploy.json* modèle, hello `extensionProfile` propriété Hello `Microsoft.Compute/virtualMachineScaleSets` ressource spécifie un [configuration d’état souhaité (DSC)](virtual-machine-scale-sets-dsc.md) extension qui installe IIS et une valeur par défaut application Web à partir d’un package Web Deploy.</span><span class="sxs-lookup"><span data-stu-id="66eeb-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="66eeb-130">Hello *IISInstall.ps1* script installe IIS sur l’ordinateur virtuel de hello et se trouve dans hello *DSC* dossier.</span><span class="sxs-lookup"><span data-stu-id="66eeb-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="66eeb-131">application web MVC est Hello se trouve dans hello *WebDeploy* dossier.</span><span class="sxs-lookup"><span data-stu-id="66eeb-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="66eeb-132">script d’installation toohello Hello chemins d’accès et de l’application web hello sont définis dans hello `powershelldscZip` et `webDeployPackage` paramètres Bonjour *azuredeploy.parameters.json* fichier.</span><span class="sxs-lookup"><span data-stu-id="66eeb-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-hello-template"></a><span data-ttu-id="66eeb-133">Déployer le modèle de hello</span><span class="sxs-lookup"><span data-stu-id="66eeb-133">Deploy hello template</span></span>
<span data-ttu-id="66eeb-134">hello toodeploy façon la plus simple de Hello [serveur HTTP de Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modèle est toouse hello **déployer tooAzure** bouton trouvé Bonjour dans les fichiers Lisez-moi de hello dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="66eeb-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="66eeb-135">Vous pouvez également utiliser PowerShell ou CLI d’Azure toodeploy hello exemples de modèles.</span><span class="sxs-lookup"><span data-stu-id="66eeb-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="66eeb-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="66eeb-136">PowerShell</span></span>
<span data-ttu-id="66eeb-137">Hello de copie [serveur HTTP de Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) fichiers à partir du dossier de tooa hello GitHub dépôt sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="66eeb-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="66eeb-138">Ouvrez hello *azuredeploy.parameters.json* fichier et mise à jour des valeurs par défaut hello Hello `vmssName`, `adminUsername`, et `adminPassword` paramètres.</span><span class="sxs-lookup"><span data-stu-id="66eeb-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="66eeb-139">Enregistrer hello suite du script PowerShell trop*deploy.ps1* Bonjour même dossier que hello *azuredeploy.json* modèle.</span><span class="sxs-lookup"><span data-stu-id="66eeb-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="66eeb-140">toodeploy Bonjour exemple modèle exécuter Bonjour *deploy.ps1* script à partir d’une fenêtre de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="66eeb-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="66eeb-141">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="66eeb-141">Azure CLI</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="66eeb-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="66eeb-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
