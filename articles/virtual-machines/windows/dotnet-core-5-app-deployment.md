---
title: "aaaAutomating déploiement d’applications avec les Extensions de Machine virtuelle | Documents Microsoft"
description: Didacticiel sur DotNet Core pour les machines virtuelles Azure
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 79c91304-6c1b-4354-a185-fecc129b139d
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: nepeters
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6d52537fbd4e935f19d3864def11484f519f8598
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-deployment-with-azure-resource-manager-templates-for-windows-vms"></a><span data-ttu-id="e45e3-103">Déploiement d’applications avec des modèles Azure Resource Manager pour les machines virtuelles Windows</span><span class="sxs-lookup"><span data-stu-id="e45e3-103">Application deployment with Azure Resource Manager templates for Windows VMs</span></span>

<span data-ttu-id="e45e3-104">Une fois que toutes les exigences d’infrastructures Azure ont été identifiés et de traduire un modèle de déploiement, déploiement d’application réelle hello doit toobe adressé.</span><span class="sxs-lookup"><span data-stu-id="e45e3-104">Once all Azure infrastructural requirements have been identified and translated into a deployment template, hello actual application deployment needs toobe addressed.</span></span> <span data-ttu-id="e45e3-105">Déploiement d’application fait référence des fichiers binaires d’application réelle de hello tooinstalling sur les ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="e45e3-105">Application deployment here is referring tooinstalling hello actual application binaries onto Azure resources.</span></span> <span data-ttu-id="e45e3-106">Pour un exemple de magasin de musique hello, .net Core et IIS doivent toobe installé et configuré sur chaque ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e45e3-106">For hello Music Store sample, .Net Core and IIS need toobe installed and configured on each virtual machine.</span></span> <span data-ttu-id="e45e3-107">Bonjour magasin de musique binaires doivent toobe installé sur l’ordinateur virtuel de hello et hello de base de données du magasin de musique créé au préalable.</span><span class="sxs-lookup"><span data-stu-id="e45e3-107">hello Music Store binaries need toobe installed onto hello virtual machine, and hello Music Store database pre-created.</span></span>

<span data-ttu-id="e45e3-108">Ce document décrit en détail comment extensions de Machine virtuelle peuvent automatiser la configuration et déploiement tooAzure ordinateurs virtuels d’application.</span><span class="sxs-lookup"><span data-stu-id="e45e3-108">This document details how Virtual Machine extensions can automate application deployment and configuration tooAzure virtual machines.</span></span> <span data-ttu-id="e45e3-109">Toutes les dépendances et configurations uniques sont en surbrillance.</span><span class="sxs-lookup"><span data-stu-id="e45e3-109">All dependencies and unique configurations are highlighted.</span></span> <span data-ttu-id="e45e3-110">Pour une expérience optimale de hello, préalable déployer une instance de hello solution tooyour abonnement Azure et de travail en même temps que le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e45e3-110">For hello best experience, pre-deploy an instance of hello solution tooyour Azure subscription and work along with hello Azure Resource Manager template.</span></span> <span data-ttu-id="e45e3-111">modèle complète de Hello se trouve ici : [déploiement du magasin de musique sur Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span><span class="sxs-lookup"><span data-stu-id="e45e3-111">hello complete template can be found here – [Music Store Deployment on Windows](https://github.com/Microsoft/dotnet-core-sample-templates/tree/master/dotnet-core-music-windows).</span></span>

## <a name="configuration-script"></a><span data-ttu-id="e45e3-112">Script de configuration</span><span class="sxs-lookup"><span data-stu-id="e45e3-112">Configuration script</span></span>
<span data-ttu-id="e45e3-113">Extensions de Machine virtuelle sont des programmes spécialisés qui s’exécutent sur l’automatisation de machines virtuelles tooprovide configuration.</span><span class="sxs-lookup"><span data-stu-id="e45e3-113">Virtual Machine extensions are specialized programs that execute against virtual machines tooprovide configuration automation.</span></span> <span data-ttu-id="e45e3-114">Les extensions sont disponibles pour de nombreux objectifs spécifiques tels que la protection contre les virus, la configuration de la journalisation et la configuration de Docker.</span><span class="sxs-lookup"><span data-stu-id="e45e3-114">Extensions are available for many specific purposes such as anti-virus, logging configuration, and Docker configuration.</span></span> <span data-ttu-id="e45e3-115">Hello, extension de Script personnalisé peut être utilisé toorun un script sur un ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="e45e3-115">hello Custom Script extension can be used toorun any script against a virtual machine.</span></span> <span data-ttu-id="e45e3-116">Exemple de magasin de musique hello, il est les machines virtuelles de toohello script personnalisé extension tooconfigure hello Windows et installer l’application de magasin de musique hello.</span><span class="sxs-lookup"><span data-stu-id="e45e3-116">With hello Music Store sample, it is up toohello custom script extension tooconfigure hello Windows virtual machines and install hello Music Store application.</span></span>

<span data-ttu-id="e45e3-117">Avant indiquant comment les extensions de machine virtuelle sont déclarées dans un modèle Azure Resource Manager, examinez le script hello qui est exécuté.</span><span class="sxs-lookup"><span data-stu-id="e45e3-117">Before detailing how virtual machine extensions are declared in an Azure Resource Manager template, examine hello script that is run.</span></span> <span data-ttu-id="e45e3-118">Ce script configure la machine virtuelle toohost hello de hello Windows application de magasin de musique.</span><span class="sxs-lookup"><span data-stu-id="e45e3-118">This script configures hello Windows virtual machine toohost hello Music Store application.</span></span> <span data-ttu-id="e45e3-119">Lors de l’exécution, le script de hello installe les logiciels requis de tous les installer l’application de magasin de musique hello à partir du contrôle de code source et préparer hello de base de données.</span><span class="sxs-lookup"><span data-stu-id="e45e3-119">When run, hello script installs all needed software, install hello Music store application from source control, and prepare hello database.</span></span> 

> <span data-ttu-id="e45e3-120">Cet exemple ne sert qu’à des fins de démonstration.</span><span class="sxs-lookup"><span data-stu-id="e45e3-120">This sample is for demonstration purposes.</span></span>

```PowerShell
<#
    .SYNOPSIS
        Downloads and configures .Net Core Music Store application sample across IIS and Azure SQL DB.
#>

Param (
    [string]$user,
    [string]$password,
    [string]$sqlserver
)

# Firewall
netsh advfirewall firewall add rule name="http" dir=in action=allow protocol=TCP localport=80

# Folders
New-Item -ItemType Directory c:\temp
New-Item -ItemType Directory c:\music

# Install iis
Install-WindowsFeature web-server -IncludeManagementTools

# Install dot.net core sdk
Invoke-WebRequest http://go.microsoft.com/fwlink/?LinkID=615460 -outfile c:\temp\vc_redistx64.exe
Start-Process c:\temp\vc_redistx64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkID=809122 -outfile c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe
Start-Process c:\temp\DotNetCore.1.0.0-SDK.Preview2-x64.exe -ArgumentList '/quiet' -Wait
Invoke-WebRequest https://go.microsoft.com/fwlink/?LinkId=817246 -outfile c:\temp\DotNetCore.WindowsHosting.exe
Start-Process c:\temp\DotNetCore.WindowsHosting.exe -ArgumentList '/quiet' -Wait

# Download music app
Invoke-WebRequest  https://github.com/Microsoft/dotnet-core-sample-templates/raw/master/dotnet-core-music-windows/music-app/music-store-azure-demo-pub.zip -OutFile c:\temp\musicstore.zip
Expand-Archive C:\temp\musicstore.zip c:\music

# Azure SQL connection sting in environment variable
[Environment]::SetEnvironmentVariable("Data:DefaultConnection:ConnectionString", "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30",[EnvironmentVariableTarget]::Machine)

# Pre-create database
$env:Data:DefaultConnection:ConnectionString = "Server=$sqlserver;Database=MusicStore;Integrated Security=False;User Id=$user;Password=$password;MultipleActiveResultSets=True;Connect Timeout=30"
Start-Process 'C:\Program Files\dotnet\dotnet.exe' -ArgumentList 'c:\music\MusicStore.dll'

# Configure iis
Remove-WebSite -Name "Default Web Site"
Set-ItemProperty IIS:\AppPools\DefaultAppPool\ managedRuntimeVersion ""
New-Website -Name "MusicStore" -Port 80 -PhysicalPath C:\music\ -ApplicationPool DefaultAppPool
& iisreset
```

## <a name="vm-script-extension"></a><span data-ttu-id="e45e3-121">Extension de script de machine virtuelle</span><span class="sxs-lookup"><span data-stu-id="e45e3-121">VM Script Extension</span></span>
<span data-ttu-id="e45e3-122">Extensions de machine virtuelle peut être exécutées sur un ordinateur virtuel au moment de la génération en incluant la ressource d’extension hello dans le modèle de gestionnaire de ressources Azure hello.</span><span class="sxs-lookup"><span data-stu-id="e45e3-122">VM Extensions can be run against a virtual machine at build time by including hello extension resource in hello Azure Resource Manager template.</span></span> <span data-ttu-id="e45e3-123">extension de Hello peut être ajoutée avec l’Assistant de Visual Studio ajouter une ressource hello, ou en insérant un JSON valide dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="e45e3-123">hello extension can be added with hello Visual Studio Add Resource wizard, or by inserting valid JSON into hello template.</span></span> <span data-ttu-id="e45e3-124">Hello ressource d’Extension de Script est imbriquée dans hello ressource d’ordinateur virtuel ; Ceci peut être observé dans hello l’exemple suivant.</span><span class="sxs-lookup"><span data-stu-id="e45e3-124">hello Script Extension resource is nested inside hello Virtual Machine resource; this can be seen in hello following example.</span></span>

<span data-ttu-id="e45e3-125">Suivez ce lien toosee hello JSON exemple dans le modèle de gestionnaire de ressources hello – [Extension de Script de machine virtuelle](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span><span class="sxs-lookup"><span data-stu-id="e45e3-125">Follow this link toosee hello JSON sample within hello Resource Manager template – [VM Script Extension](https://github.com/Microsoft/dotnet-core-sample-templates/blob/master/dotnet-core-music-windows/azuredeploy.json#L339).</span></span> 

<span data-ttu-id="e45e3-126">Notez dans hello ci-dessous JSON qui hello script est stocké dans GitHub.</span><span class="sxs-lookup"><span data-stu-id="e45e3-126">Notice in hello below JSON that hello script is stored in GitHub.</span></span> <span data-ttu-id="e45e3-127">Ce script pourrait également être stocké dans Stockage Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e45e3-127">This script could also be stored in Azure Blob storage.</span></span> <span data-ttu-id="e45e3-128">Modèles Azure Resource Manager permettent également, hello script d’exécution chaîne toobe construit de telle sorte que les valeurs de paramètres de modèle peuvent être utilisées en tant que paramètres pour l’exécution du script.</span><span class="sxs-lookup"><span data-stu-id="e45e3-128">Also, Azure Resource Manager templates allow hello script execution string toobe constructed such that template parameters values can be used as parameters for script execution.</span></span> <span data-ttu-id="e45e3-129">Dans ce cas les données sont fournies lors du déploiement de modèles de hello, et ces valeurs peuvent ensuite être utilisées lors de l’exécution du script de hello.</span><span class="sxs-lookup"><span data-stu-id="e45e3-129">In this case data is provided when deploying hello templates, and these values can then be used when executing hello script.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.4",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://raw.githubusercontent.com/Microsoft/dotnet-core-sample-templates/master/dotnet-core-music-windows/scripts/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]"
    }
  }
}
```

<span data-ttu-id="e45e3-130">Comme indiqué ci-dessus, il est également de toostore possible vos scripts dans le stockage d’objets Blob Azure.</span><span class="sxs-lookup"><span data-stu-id="e45e3-130">As mentioned above, it is also possible toostore your custom scripts in Azure Blob storage.</span></span> <span data-ttu-id="e45e3-131">Il existe deux options pour stocker les ressources de script hello dans le stockage blob ; choix entre rendre hello public du conteneur/script et suivez hello même approche comme indiqué ci-dessus, ou il peut être conservée dans le stockage blob privé qui nécessite que vous tooprovide hello storageAccountName et storageAccountKey toohello CustomScriptExtension définition de ressource.</span><span class="sxs-lookup"><span data-stu-id="e45e3-131">There are two options for storing hello script resources in blob storage; either make hello container/script public and follow hello same approach as above, or it can also be kept in private blob storage which requires you tooprovide hello storageAccountName and storageAccountKey toohello CustomScriptExtension resource definition.</span></span>

<span data-ttu-id="e45e3-132">Dans l’exemple hello ci-dessous nous avons passé une étape supplémentaire.</span><span class="sxs-lookup"><span data-stu-id="e45e3-132">In hello example below we have gone a step further.</span></span> <span data-ttu-id="e45e3-133">Bien qu’il soit nom de compte de stockage possible tooprovide hello et la clé en tant que paramètre ou variable durant le déploiement, les modèles de gestionnaire de ressources fournissent hello `listKeys` fonction qui peut obtenir du compte de stockage hello par programmation la clé et de l’insérer dans toohello modèle au moment du déploiement.</span><span class="sxs-lookup"><span data-stu-id="e45e3-133">While it is possible tooprovide hello storage account name and key as a parameter or variable during deployment, Resource Manager templates provide hello `listKeys` function that can obtain hello storage account key programmatically and insert it in toohello template for you at deployment time.</span></span>

<span data-ttu-id="e45e3-134">Dans l’exemple hello CustomScriptExtension définition de ressource ci-dessous, notre script personnalisé a déjà été téléchargé tooan appelé compte de stockage Azure `mystorageaccount9999` qui existe dans un autre groupe de ressources appelé `mysa999rgname`.</span><span class="sxs-lookup"><span data-stu-id="e45e3-134">In hello example CustomScriptExtension resource definition below, our custom script has already been uploaded tooan Azure storage account called `mystorageaccount9999` which exists in another Resource Group called `mysa999rgname`.</span></span> <span data-ttu-id="e45e3-135">Lorsque nous déployez un modèle qui contient cette ressource, hello `listKeys` fonction obtient par programme hello de la clé de compte de stockage hello `mystorageaccount9999` dans le groupe de ressources de hello `mysa999rgname` et l’insère dans le modèle de toohello pour nous.</span><span class="sxs-lookup"><span data-stu-id="e45e3-135">When we deploy a template containing this resource, hello `listKeys` function programmatically obtains hello storage account key for hello storage account `mystorageaccount9999` in hello Resource Group `mysa999rgname` and inserts it in toohello template for us.</span></span>

```json
{
  "apiVersion": "2015-06-15",
  "type": "extensions",
  "name": "config-app",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'),copyindex())]",
    "[variables('musicstoresqlName')]"
  ],
  "tags": {
    "displayName": "config-app"
  },
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "https://mystorageaccount9999.blob.core.windows.net/container/configure-music-app.ps1"
      ]
    },
    "protectedSettings": {
      "commandToExecute": "[concat('powershell -ExecutionPolicy Unrestricted -File configure-music-app.ps1 -user ',parameters('adminUsername'),' -password ',parameters('adminPassword'),' -sqlserver ',variables('musicstoresqlName'),'.database.windows.net')]",
      "storageAccountName": "mystorageaccount9999",
      "storageAccountKey": "[listKeys(resourceId('mysa999rgname','Microsoft.Storage/storageAccounts', mystorageaccount9999), '2015-06-15').key1]"
    }
  }
}
```

<span data-ttu-id="e45e3-136">Hello le principal avantage de cette approche est qu’il ne nécessite pas toochange vous votre modèle ou les paramètres de déploiement dans l’événement de hello hello de modification de clé de compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="e45e3-136">hello main benefit of this approach is that it does not require you toochange your template or deployment parameters in hello event of hello storage account key changing.</span></span>

<span data-ttu-id="e45e3-137">Pour plus d’informations sur l’utilisation d’extension de script personnalisé hello, consultez [extensions de script personnalisé avec les modèles de gestionnaire de ressources](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e45e3-137">For more information on using hello custom script extension, see [Custom script extensions with Resource Manager templates](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="next-step"></a><span data-ttu-id="e45e3-138">Étape suivante</span><span class="sxs-lookup"><span data-stu-id="e45e3-138">Next Step</span></span>
<hr>

[<span data-ttu-id="e45e3-139">Découvrir d’autres modèles Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e45e3-139">Explore More Azure Resource Manager Templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

