---
title: "Déployez une application sur un groupe de machines virtuelles identiques Azure | Microsoft Docs"
description: "Apprenez à déployer une application de mise à l’échelle automatique simple sur un jeu de mise à l’échelle de machines virtuelles identiques à l’aide d’un modèle Azure Resource Manager."
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
ms.openlocfilehash: 07883a33382cc660b043c99872312a9e77228253
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="e0595-103">Déploiement d’une application de mise à l’échelle à l’aide d’un modèle</span><span class="sxs-lookup"><span data-stu-id="e0595-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="e0595-104">Les [modèles Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) constituent un excellent moyen de déployer des groupes de ressources liées.</span><span class="sxs-lookup"><span data-stu-id="e0595-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="e0595-105">Ce didacticiel se base sur [Déploiement d’un jeu de mise à l’échelle simple](virtual-machine-scale-sets-mvss-start.md) et décrit comment déployer une application de mise à l’échelle automatique simple sur un jeu de mise à l’échelle à l’aide d’un modèle Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e0595-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how to deploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="e0595-106">Vous pouvez également configurer la mise à l’échelle automatique en utilisant PowerShell, CLI ou le portail.</span><span class="sxs-lookup"><span data-stu-id="e0595-106">You can also set up autoscaling using PowerShell, CLI, or the portal.</span></span> <span data-ttu-id="e0595-107">Pour plus d’informations, consultez [Vue d’ensemble de la mise à l’échelle automatique](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0595-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="e0595-108">Deux modèles de démarrage rapide</span><span class="sxs-lookup"><span data-stu-id="e0595-108">Two quickstart templates</span></span>
<span data-ttu-id="e0595-109">Lorsque vous déployez un jeu de mise à l’échelle, vous pouvez installer de nouveaux logiciels sur une image de plateforme à l’aide d’une [extension de machine virtuelle](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="e0595-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="e0595-110">Les extensions de machine virtuelle sont de petites applications permettant d’exécuter des tâches de configuration et d’automatisation post-déploiement sur des machines virtuelles Azure, comme le déploiement d’une application.</span><span class="sxs-lookup"><span data-stu-id="e0595-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="e0595-111">Deux modèles différents sont fournis dans [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) et montrent comment déployer une application de mise à l’échelle automatique sur un jeu de mise à l’échelle à l’aide des extensions de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e0595-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how to deploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="e0595-112">Serveur HTTP Python sur Linux</span><span class="sxs-lookup"><span data-stu-id="e0595-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="e0595-113">Le modèle [serveur HTTP Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) déploie une application simple de mise à l’échelle automatique simple sur un jeu de mise à l’échelle Linux.</span><span class="sxs-lookup"><span data-stu-id="e0595-113">The [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="e0595-114">[Bottle](http://bottlepy.org/docs/dev/), un framework web de Python et un serveur HTTP simple sont déployés sur chaque machine virtuelle dans le jeu de mise à l’échelle à l’aide d’une extension de machine virtuelle à script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e0595-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in the scale set using a custom script VM extension.</span></span> <span data-ttu-id="e0595-115">Le jeu de mise à l’échelle monte en puissance lorsque l’utilisation moyenne de l’UC entre toutes les machines virtuelles est supérieure à 60 % et descend en puissance lorsque l’utilisation moyenne est inférieure à 30 %.</span><span class="sxs-lookup"><span data-stu-id="e0595-115">The scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when the average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="e0595-116">En plus de la ressource de jeu de mise à l’échelle, l’exemple de modèle *azuredeploy.json* déclare également le réseau virtuel, l’adresse IP publique, l’équilibrage de charge et les paramètres de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="e0595-116">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="e0595-117">Pour plus d’informations sur la création de ces ressources dans un modèle, consultez la page [Jeu de mise à l’échelle Linux avec mise à l’échelle automatique](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="e0595-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="e0595-118">Dans le modèle *azuredeploy.json*, la propriété `extensionProfile` de la ressource `Microsoft.Compute/virtualMachineScaleSets` spécifie une extension à script personnalisé.</span><span class="sxs-lookup"><span data-stu-id="e0595-118">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="e0595-119">`fileUris` spécifie l’emplacement du ou des scripts.</span><span class="sxs-lookup"><span data-stu-id="e0595-119">`fileUris` specifies the script(s) location.</span></span> <span data-ttu-id="e0595-120">Dans ce cas, nous avons deux fichiers : *workserver.py*, qui définit un serveur HTTP simple, et *installserver.sh*, qui installe Bottle et démarre le serveur HTTP.</span><span class="sxs-lookup"><span data-stu-id="e0595-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts the HTTP server.</span></span> <span data-ttu-id="e0595-121">`commandToExecute` spécifie la commande à exécuter une fois le jeu de mise à l’échelle déployé.</span><span class="sxs-lookup"><span data-stu-id="e0595-121">`commandToExecute` specifies the command to run after the scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="e0595-122">Application ASP.NET MVC sur Windows</span><span class="sxs-lookup"><span data-stu-id="e0595-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="e0595-123">L’exemple de modèle [Application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) déploie une application ASP.NET MVC simple dans IIS sur un jeu de mise à l’échelle Windows.</span><span class="sxs-lookup"><span data-stu-id="e0595-123">The [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="e0595-124">IIS et l’application MVC sont déployés à l’aide de l’extension de machine virtuelle [Configuration d’état souhaité (DSC) PowerShell](virtual-machine-scale-sets-dsc.md).</span><span class="sxs-lookup"><span data-stu-id="e0595-124">IIS and the MVC app are deployed using the [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="e0595-125">Le jeu de mise à l’échelle monte en puissance (sur une instance de machine virtuelle à la fois) lorsque l’utilisation de l’UC dépasse 50 % pendant 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="e0595-125">The scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="e0595-126">En plus de la ressource de jeu de mise à l’échelle, l’exemple de modèle *azuredeploy.json* déclare également le réseau virtuel, l’adresse IP publique, l’équilibrage de charge et les paramètres de mise à l’échelle automatique.</span><span class="sxs-lookup"><span data-stu-id="e0595-126">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="e0595-127">Ce modèle illustre également la mise à niveau de l’application.</span><span class="sxs-lookup"><span data-stu-id="e0595-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="e0595-128">Pour plus d’informations sur la création de ces ressources dans un modèle, consultez la page [Jeu de mise à l’échelle Windows avec mise à l’échelle automatique](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="e0595-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="e0595-129">Dans le modèle *azuredeploy.json*, la propriété `extensionProfile` de la ressource `Microsoft.Compute/virtualMachineScaleSets` spécifie une extension [Configuration d’état souhaité (DSC)](virtual-machine-scale-sets-dsc.md) qui installe IIS et une application par défaut à partir d’un package WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="e0595-129">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="e0595-130">Le script *IISInstall.ps1* installe IIS sur la machine virtuelle et se trouve dans le dossier *DSC*.</span><span class="sxs-lookup"><span data-stu-id="e0595-130">The *IISInstall.ps1* script installs IIS on the virtual machine and is found in the *DSC* folder.</span></span>  <span data-ttu-id="e0595-131">L’application web MVC se trouve dans le dossier *WebDeploy*.</span><span class="sxs-lookup"><span data-stu-id="e0595-131">The MVC web app is found in the *WebDeploy* folder.</span></span>  <span data-ttu-id="e0595-132">Les chemins d’accès pour le script d’installation et de l’application web sont définis dans les paramètres `powershelldscZip` et `webDeployPackage` dans le fichier *azuredeploy.parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="e0595-132">The paths to the install script and the web app are defined in the `powershelldscZip` and `webDeployPackage` parameters in the *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="e0595-133">Déployer le modèle</span><span class="sxs-lookup"><span data-stu-id="e0595-133">Deploy the template</span></span>
<span data-ttu-id="e0595-134">Le moyen le plus simple pour déployer le modèle [serveur HTTP Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) consiste à utiliser le bouton **Déployer dans Azure** qui se trouve dans les fichiers Lisez-moi dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="e0595-134">The simplest way to deploy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is to use the **Deploy to Azure** button found in the in the readme files in GitHub.</span></span>  <span data-ttu-id="e0595-135">Vous pouvez également utiliser PowerShell ou l’interface Azure CLI pour déployer les exemples de modèles.</span><span class="sxs-lookup"><span data-stu-id="e0595-135">You can also use PowerShell or Azure CLI to deploy the sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="e0595-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="e0595-136">PowerShell</span></span>
<span data-ttu-id="e0595-137">Copiez les fichiers de [serveur HTTP Python sur Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [application ASP.NET MVC sur Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) du référentiel GitHub dans un dossier sur votre ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="e0595-137">Copy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from the GitHub repo to a folder on your local computer.</span></span>  <span data-ttu-id="e0595-138">Ouvrez le fichier *azuredeploy.parameters.json* et de mettez à jour les valeurs par défaut des paramètres `vmssName`, `adminUsername` et `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="e0595-138">Open the *azuredeploy.parameters.json* file and update the default values of the `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="e0595-139">Enregistrez le script PowerShell suivant dans *deploy.ps1* dans le même dossier que le modèle *azuredeploy.json*.</span><span class="sxs-lookup"><span data-stu-id="e0595-139">Save the following PowerShell script to *deploy.ps1* in the same folder as the *azuredeploy.json* template.</span></span> <span data-ttu-id="e0595-140">Pour déployer l’exemple de modèle, exécutez le script *deploy.ps1* à partir d’une fenêtre de commande PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e0595-140">To deploy the sample template run the *deploy.ps1* script from a PowerShell command window.</span></span>

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
    Write-Host "Resource group '$resourceGroupName' does not exist. To create a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start the deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="e0595-141">Interface de ligne de commande Azure</span><span class="sxs-lookup"><span data-stu-id="e0595-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
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

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
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

## <a name="next-steps"></a><span data-ttu-id="e0595-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e0595-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
