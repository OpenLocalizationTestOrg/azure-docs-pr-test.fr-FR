---
title: "ordinateurs aaaVirtual dans un modèle Azure Resource Manager | Microsoft Azure"
description: "En savoir plus sur la ressource d’ordinateur virtuel hello est défini dans un modèle Azure Resource Manager."
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f63ab5cc-45b8-43aa-a4e7-69dc42adbb99
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: davidmu
ms.openlocfilehash: 94adcbe5bf44be72ffc1b920461aed15c4fc025f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="virtual-machines-in-an-azure-resource-manager-template"></a><span data-ttu-id="08746-103">Machines virtuelles dans un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="08746-103">Virtual machines in an Azure Resource Manager template</span></span>

<span data-ttu-id="08746-104">Cet article décrit les aspects d’un modèle Azure Resource Manager s’applique toovirtual machines.</span><span class="sxs-lookup"><span data-stu-id="08746-104">This article describes aspects of an Azure Resource Manager template that apply toovirtual machines.</span></span> <span data-ttu-id="08746-105">Cet article ne décrit pas un modèle complet pour la création d’une machine virtuelle ; pour cela, vous avez besoin de définitions de ressource pour des comptes de stockage, d'interfaces réseau, d'adresses IP publiques et de réseaux virtuels.</span><span class="sxs-lookup"><span data-stu-id="08746-105">This article doesn’t describe a complete template for creating a virtual machine; for that you need resource definitions for storage accounts, network interfaces, public IP addresses, and virtual networks.</span></span> <span data-ttu-id="08746-106">Pour plus d’informations sur la façon dont ces ressources peuvent être définis, consultez hello [procédure pas à pas de gestionnaire de ressources du modèle](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="08746-106">For more information about how these resources can be defined together, see hello [Resource Manager template walkthrough](../../azure-resource-manager/resource-manager-template-walkthrough.md).</span></span>

<span data-ttu-id="08746-107">Il existe de nombreux [modèles dans la galerie de hello](https://azure.microsoft.com/documentation/templates/?term=VM) qui incluent des ressources de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="08746-107">There are many [templates in hello gallery](https://azure.microsoft.com/documentation/templates/?term=VM) that include hello VM resource.</span></span> <span data-ttu-id="08746-108">Les éléments qui peuvent être inclus dans un modèle ne sont tous décrits ici.</span><span class="sxs-lookup"><span data-stu-id="08746-108">Not all elements that can be included in a template are described here.</span></span>

<span data-ttu-id="08746-109">Cet exemple montre une section de ressources standard d’un modèle pour la création d’un nombre spécifié de machines virtuelles :</span><span class="sxs-lookup"><span data-stu-id="08746-109">This example shows a typical resource section of a template for creating a specified number of VMs:</span></span>

```json
"resources": [
  { 
    "apiVersion": "2016-04-30-preview", 
    "type": "Microsoft.Compute/virtualMachines", 
    "name": "[concat('myVM', copyindex())]", 
    "location": "[resourceGroup().location]",
    "copy": {
      "name": "virtualMachineLoop", 
      "count": "[parameters('numberOfInstances')]"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/myNIC', copyindex())]" 
    ], 
    "properties": { 
      "hardwareProfile": { 
        "vmSize": "Standard_DS1" 
      }, 
      "osProfile": { 
        "computername": "[concat('myVM', copyindex())]", 
        "adminUsername": "[parameters('adminUsername')]", 
        "adminPassword": "[parameters('adminPassword')]" 
      }, 
      "storageProfile": { 
        "imageReference": { 
          "publisher": "MicrosoftWindowsServer", 
          "offer": "WindowsServer", 
          "sku": "2012-R2-Datacenter", 
          "version": "latest" 
        }, 
        "osDisk": { 
          "name": "[concat('myOSDisk', copyindex())]",
          "caching": "ReadWrite", 
          "createOption": "FromImage" 
        },
        "dataDisks": [
          {
            "name": "[concat('myDataDisk', copyindex())]",
            "diskSizeGB": "100",
            "lun": 0,
            "createOption": "Empty"
          }
        ] 
      }, 
      "networkProfile": { 
        "networkInterfaces": [ 
          { 
            "id": "[resourceId('Microsoft.Network/networkInterfaces',
              concat('myNIC', copyindex()))]" 
          } 
        ] 
      },
      "diagnosticsProfile": {
        "bootDiagnostics": {
          "enabled": "true",
          "storageUri": "[concat('https://', variables('storageName'), '.blob.core.windows.net')]"
        }
      } 
    },
    "resources": [ 
      { 
        "name": "Microsoft.Insights.VMDiagnosticsSettings", 
        "type": "extensions", 
        "location": "[resourceGroup().location]", 
        "apiVersion": "2016-03-30", 
        "dependsOn": [ 
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
        ], 
        "properties": { 
          "publisher": "Microsoft.Azure.Diagnostics", 
          "type": "IaaSDiagnostics", 
          "typeHandlerVersion": "1.5", 
          "autoUpgradeMinorVersion": true, 
          "settings": { 
            "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
            variables('wadmetricsresourceid'), 
            concat('myVM', copyindex()),
            variables('wadcfgxend')))]", 
            "storageAccount": "[variables('storageName')]" 
          }, 
          "protectedSettings": { 
            "storageAccountName": "[variables('storageName')]", 
            "storageAccountKey": "[listkeys(variables('accountid'), 
              '2015-06-15').key1]", 
            "storageAccountEndPoint": "https://core.windows.net" 
          } 
        } 
      },
      {
        "name": "MyCustomScriptExtension",
        "type": "extensions",
        "apiVersion": "2016-03-30",
        "location": "[resourceGroup().location]",
        "dependsOn": [
          "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
        ],
        "properties": {
          "publisher": "Microsoft.Compute",
          "type": "CustomScriptExtension",
          "typeHandlerVersion": "1.7",
          "autoUpgradeMinorVersion": true,
          "settings": {
            "fileUris": [
              "[concat('https://', variables('storageName'),
                '.blob.core.windows.net/customscripts/start.ps1')]" 
            ],
            "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
          }
        }
      } 
    ]
  } 
]
``` 

> [!NOTE] 
><span data-ttu-id="08746-110">Cet exemple repose sur un compte de stockage créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="08746-110">This example relies on a storage account that was previously created.</span></span> <span data-ttu-id="08746-111">Vous pouvez créer le compte de stockage hello en la déployant à partir du modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-111">You could create hello storage account by deploying it from hello template.</span></span> <span data-ttu-id="08746-112">exemple de Hello s’appuie également sur une interface réseau et ses ressources dépendantes qui sont définies dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-112">hello example also relies on a network interface and its dependent resources that would be defined in hello template.</span></span> <span data-ttu-id="08746-113">Ces ressources ne sont pas affichés dans l’exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-113">These resources are not shown in hello example.</span></span>
>
>

## <a name="api-version"></a><span data-ttu-id="08746-114">Version de l'API</span><span class="sxs-lookup"><span data-stu-id="08746-114">API Version</span></span>

<span data-ttu-id="08746-115">Lorsque vous déployez des ressources à l’aide d’un modèle, vous avez toospecify une version de hello API toouse.</span><span class="sxs-lookup"><span data-stu-id="08746-115">When you deploy resources using a template, you have toospecify a version of hello API toouse.</span></span> <span data-ttu-id="08746-116">Hello montre une ressource d’ordinateur virtuel hello à l’aide de cet élément apiVersion :</span><span class="sxs-lookup"><span data-stu-id="08746-116">hello example shows hello virtual machine resource using this apiVersion element:</span></span>

```
"apiVersion": "2016-04-30-preview",
```

<span data-ttu-id="08746-117">version de Hello de hello API que vous spécifiez dans votre modèle affecte les propriétés que vous pouvez définir dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-117">hello version of hello API you specify in your template affects which properties you can define in hello template.</span></span> <span data-ttu-id="08746-118">En règle générale, vous devez sélectionner la version plus récente de l’API hello lors de la création de modèles.</span><span class="sxs-lookup"><span data-stu-id="08746-118">In general, you should select hello most recent API version when creating templates.</span></span> <span data-ttu-id="08746-119">Pour les modèles existants, vous pouvez décider si vous souhaitez toocontinue à l’aide d’une version antérieure de l’API ou mettre à jour votre modèle pour hello dernière version tootake un avantage des nouvelles fonctionnalités.</span><span class="sxs-lookup"><span data-stu-id="08746-119">For existing templates, you can decide whether you want toocontinue using an earlier API version, or update your template for hello latest version tootake advantage of new features.</span></span>

<span data-ttu-id="08746-120">Utilisez ces possibilités d’obtention de versions plus récentes de l’API hello :</span><span class="sxs-lookup"><span data-stu-id="08746-120">Use these opportunities for getting hello latest API versions:</span></span>

- <span data-ttu-id="08746-121">API REST - [Répertorier tous les fournisseurs de ressources](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span><span class="sxs-lookup"><span data-stu-id="08746-121">REST API - [List all resource providers](https://docs.microsoft.com/rest/api/resources/providers#Providers_List)</span></span>
- <span data-ttu-id="08746-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span><span class="sxs-lookup"><span data-stu-id="08746-122">PowerShell - [Get-AzureRmResourceProvider](/powershell/module/azurerm.resources/get-azurermresourceprovider)</span></span>
- <span data-ttu-id="08746-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span><span class="sxs-lookup"><span data-stu-id="08746-123">Azure CLI 2.0 - [az provider show](https://docs.microsoft.com/cli/azure/provider#show)</span></span>

## <a name="parameters-and-variables"></a><span data-ttu-id="08746-124">Paramètres et variables</span><span class="sxs-lookup"><span data-stu-id="08746-124">Parameters and variables</span></span>

<span data-ttu-id="08746-125">[Paramètres](../../resource-group-authoring-templates.md) facilitent vous toospecify des valeurs pour le modèle de hello lorsque vous l’exécutez.</span><span class="sxs-lookup"><span data-stu-id="08746-125">[Parameters](../../resource-group-authoring-templates.md) make it easy for you toospecify values for hello template when you run it.</span></span> <span data-ttu-id="08746-126">Cette section de paramètres est utilisée dans l’exemple de hello :</span><span class="sxs-lookup"><span data-stu-id="08746-126">This parameters section is used in hello example:</span></span>

```        
"parameters": {
  "adminUsername": { "type": "string" },
  "adminPassword": { "type": "securestring" },
  "numberOfInstances": { "type": "int" }
},
```

<span data-ttu-id="08746-127">Lorsque vous déployez le modèle d’exemple hello, vous entrez des valeurs pour le nom de hello et le mot de passe du compte d’administrateur hello sur chaque machine virtuelle et hello le numéro de toocreate de machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="08746-127">When you deploy hello example template, you enter values for hello name and password of hello administrator account on each VM and hello number of VMs toocreate.</span></span> <span data-ttu-id="08746-128">Vous pouvez hello spécifiant des valeurs de paramètre dans un fichier distinct qui est géré par le modèle de hello, ou en fournissant des valeurs lorsque vous y êtes invité.</span><span class="sxs-lookup"><span data-stu-id="08746-128">You have hello option of specifying parameter values in a separate file that's managed with hello template, or providing values when prompted.</span></span>

<span data-ttu-id="08746-129">[Variables](../../resource-group-authoring-templates.md) simplifient vous tooset des valeurs dans un modèle hello qui sont utilisés à plusieurs reprises tout au long ou qui peut changer au fil du temps.</span><span class="sxs-lookup"><span data-stu-id="08746-129">[Variables](../../resource-group-authoring-templates.md) make it easy for you tooset up values in hello template that are used repeatedly throughout it or that can change over time.</span></span> <span data-ttu-id="08746-130">Cette section de variables est utilisée dans l’exemple de hello :</span><span class="sxs-lookup"><span data-stu-id="08746-130">This variables section is used in hello example:</span></span>

```
"variables": { 
  "storageName": "mystore1",
  "accountid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name,
  '/providers/','Microsoft.Storage/storageAccounts/', variables('storageName'))]", 
  "wadlogs": "<WadCfg> 
    <DiagnosticMonitorConfiguration overallQuotaInMB=\"4096\" xmlns=\"http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration\"> 
      <DiagnosticInfrastructureLogs scheduledTransferLogLevelFilter=\"Error\"/> 
      <WindowsEventLog scheduledTransferPeriod=\"PT1M\" > 
        <DataSource name=\"Application!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"Security!*[System[(Level = 1 or Level = 2)]]\" /> 
        <DataSource name=\"System!*[System[(Level = 1 or Level = 2)]]\" />
      </WindowsEventLog>", 
  "wadperfcounters": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\">
      <PerformanceCounterConfiguration counterSpecifier=\"\\Process(_Total)\\Thread Count\" sampleRate=\"PT15S\" unit=\"Count\">
        <annotation displayName=\"Threads\" locale=\"en-us\"/>
      </PerformanceCounterConfiguration>
    </PerformanceCounters>", 
  "wadcfgxstart": "[concat(variables('wadlogs'), variables('wadperfcounters'), 
    '<Metrics resourceId=\"')]", 
  "wadmetricsresourceid": "[concat('/subscriptions/', subscription().subscriptionId, 
    '/resourceGroups/', resourceGroup().name , 
    '/providers/', 'Microsoft.Compute/virtualMachines/')]", 
  "wadcfgxend": "\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/>
    <MetricAggregation scheduledTransferPeriod=\"PT1M\"/>
    </Metrics></DiagnosticMonitorConfiguration>
    </WadCfg>"
}, 
```

<span data-ttu-id="08746-131">Lorsque vous déployez le modèle d’exemple hello, valeurs des variables sont utilisées pour le nom de hello et l’identificateur de compte de stockage hello créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="08746-131">When you deploy hello example template, variable values are used for hello name and identifier of hello previously created storage account.</span></span> <span data-ttu-id="08746-132">Variables sont également des paramètres de hello tooprovide utilisé pour l’extension de diagnostic hello.</span><span class="sxs-lookup"><span data-stu-id="08746-132">Variables are also used tooprovide hello settings for hello diagnostic extension.</span></span> <span data-ttu-id="08746-133">Hello d’utilisation [meilleures pratiques pour la création de modèles Azure Resource Manager](../../resource-manager-template-best-practices.md) toohelp vous décidez comment toostructure hello paramètres et les variables dans votre modèle.</span><span class="sxs-lookup"><span data-stu-id="08746-133">Use hello [best practices for creating Azure Resource Manager templates](../../resource-manager-template-best-practices.md) toohelp you decide how you want toostructure hello parameters and variables in your template.</span></span>

## <a name="resource-loops"></a><span data-ttu-id="08746-134">boucles de ressources</span><span class="sxs-lookup"><span data-stu-id="08746-134">Resource loops</span></span>

<span data-ttu-id="08746-135">Lorsque vous avez besoin de plusieurs machines virtuelles pour votre application, vous pouvez utiliser un élément copy dans un modèle.</span><span class="sxs-lookup"><span data-stu-id="08746-135">When you need more than one virtual machine for your application, you can use a copy element in a template.</span></span> <span data-ttu-id="08746-136">Cet élément facultatif effectue une itération sur la création de nombre de hello d’ordinateurs virtuels que vous avez spécifié en tant que paramètre :</span><span class="sxs-lookup"><span data-stu-id="08746-136">This optional element loops through creating hello number of VMs that you specified as a parameter:</span></span>

```
"copy": {
  "name": "virtualMachineLoop", 
  "count": "[parameters('numberOfInstances')]"
},
```

<span data-ttu-id="08746-137">En outre, notez dans l’exemple hello hello index de boucle est utilisé lorsque certaines hello spécifiant des valeurs pour la ressource de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-137">Also, notice in hello example that hello loop index is used when specifying some of hello values for hello resource.</span></span> <span data-ttu-id="08746-138">Par exemple, si vous avez entré un nombre d’instances de trois, noms hello de disques de système d’exploitation hello sont myOSDisk1, myOSDisk2 et myOSDisk3 :</span><span class="sxs-lookup"><span data-stu-id="08746-138">For example, if you entered an instance count of three, hello names of hello operating system disks are myOSDisk1, myOSDisk2, and myOSDisk3:</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
}
```

> [!NOTE] 
><span data-ttu-id="08746-139">Cet exemple utilise des disques gérés pour les ordinateurs virtuels de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-139">This example uses managed disks for hello virtual machines.</span></span>
>
>

<span data-ttu-id="08746-140">Gardez à l’esprit nécessitant la création d’une boucle pour une ressource dans le modèle de hello vous toouse hello boucle lors de la création ou de l’accès à d’autres ressources.</span><span class="sxs-lookup"><span data-stu-id="08746-140">Keep in mind that creating a loop for one resource in hello template may require you toouse hello loop when creating or accessing other resources.</span></span> <span data-ttu-id="08746-141">Par exemple, plusieurs machines virtuelles ne peut pas utiliser hello même interface réseau, donc si votre modèle effectue une itération sur la création de trois machines virtuelles, il doit également faire une boucle dans la création de trois interfaces réseau.</span><span class="sxs-lookup"><span data-stu-id="08746-141">For example, multiple VMs can’t use hello same network interface, so if your template loops through creating three VMs it must also loop through creating three network interfaces.</span></span> <span data-ttu-id="08746-142">Lorsque vous affectez un tooa d’interface réseau virtuelle, les index de boucle hello est tooidentify utilisé il :</span><span class="sxs-lookup"><span data-stu-id="08746-142">When assigning a network interface tooa VM, hello loop index is used tooidentify it:</span></span>

```
"networkInterfaces": [ { 
  "id": "[resourceId('Microsoft.Network/networkInterfaces',
    concat('myNIC', copyindex()))]" 
} ]
```

## <a name="dependencies"></a><span data-ttu-id="08746-143">Dépendances</span><span class="sxs-lookup"><span data-stu-id="08746-143">Dependencies</span></span>

<span data-ttu-id="08746-144">La plupart des ressources en dépendent autres toowork ressources correctement.</span><span class="sxs-lookup"><span data-stu-id="08746-144">Most resources depend on other resources toowork correctly.</span></span> <span data-ttu-id="08746-145">Machines virtuelles doit être associés à un réseau virtuel et un toodo qu’il nécessite une interface réseau.</span><span class="sxs-lookup"><span data-stu-id="08746-145">Virtual machines must be associated with a virtual network and toodo that it needs a network interface.</span></span> <span data-ttu-id="08746-146">Hello [dependsOn](../../resource-group-define-dependencies.md) élément est utilisé toomake que cette interface de réseau hello est prêt toobe utilisé avant la création des machines virtuelles de hello :</span><span class="sxs-lookup"><span data-stu-id="08746-146">hello [dependsOn](../../resource-group-define-dependencies.md) element is used toomake sure that hello network interface is ready toobe used before hello VMs are created:</span></span>

```
"dependsOn": [
  "[concat('Microsoft.Network/networkInterfaces/', 'myNIC', copyindex())]" 
],
```

<span data-ttu-id="08746-147">Resource Manager déploie en parallèle les ressources qui ne dépendent pas d'une autre ressource en cours de déploiement.</span><span class="sxs-lookup"><span data-stu-id="08746-147">Resource Manager deploys in parallel any resources that are not dependent on another resource being deployed.</span></span> <span data-ttu-id="08746-148">Soyez prudent lors de la définition des dépendances car vous pouvez accidentellement ralentir votre déploiement en spécifiant des dépendances inutiles.</span><span class="sxs-lookup"><span data-stu-id="08746-148">Be careful when setting dependencies because you can inadvertently slow your deployment by specifying unnecessary dependencies.</span></span> <span data-ttu-id="08746-149">Les dépendances peuvent couvrir plusieurs ressources.</span><span class="sxs-lookup"><span data-stu-id="08746-149">Dependencies can chain through multiple resources.</span></span> <span data-ttu-id="08746-150">Par exemple, interface de réseau hello dépend adresse IP publique de hello et ressources du réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="08746-150">For example, hello network interface depends on hello public IP address and virtual network resources.</span></span>

<span data-ttu-id="08746-151">Comment savoir si une dépendance est nécessaire ?</span><span class="sxs-lookup"><span data-stu-id="08746-151">How do you know if a dependency is required?</span></span> <span data-ttu-id="08746-152">Examinez les valeurs hello que vous définissez dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-152">Look at hello values you set in hello template.</span></span> <span data-ttu-id="08746-153">Si un élément dans la définition de ressource d’ordinateur virtuel hello pointe tooanother ressource déployée dans hello même modèle, vous avez besoin d’une dépendance.</span><span class="sxs-lookup"><span data-stu-id="08746-153">If an element in hello virtual machine resource definition points tooanother resource that is deployed in hello same template, you need a dependency.</span></span> <span data-ttu-id="08746-154">Par exemple, votre exemple de machine virtuelle définit un profil de réseau :</span><span class="sxs-lookup"><span data-stu-id="08746-154">For example, your example virtual machine defines a network profile:</span></span>

```
"networkProfile": { 
  "networkInterfaces": [ { 
    "id": "[resourceId('Microsoft.Network/networkInterfaces',
      concat('myNIC', copyindex())]" 
  } ] 
},
```

<span data-ttu-id="08746-155">tooset cette propriété, l’interface de réseau hello doit exister.</span><span class="sxs-lookup"><span data-stu-id="08746-155">tooset this property, hello network interface must exist.</span></span> <span data-ttu-id="08746-156">Vous avez donc besoin d’une dépendance.</span><span class="sxs-lookup"><span data-stu-id="08746-156">Therefore, you need a dependency.</span></span> <span data-ttu-id="08746-157">Vous devez également tooset une dépendance lorsqu’une ressource (enfant) est définie dans une autre ressource (parent).</span><span class="sxs-lookup"><span data-stu-id="08746-157">You also need tooset a dependency when one resource (a child) is defined within another resource (a parent).</span></span> <span data-ttu-id="08746-158">Par exemple, les paramètres de diagnostic hello et extensions de script personnalisé sont définies en tant que ressources enfants de l’ordinateur virtuel de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-158">For example, hello diagnostic settings and custom script extensions are both defined as child resources of hello virtual machine.</span></span> <span data-ttu-id="08746-159">Ils ne peuvent pas être créés jusqu'à ce que l’ordinateur virtuel de hello existe.</span><span class="sxs-lookup"><span data-stu-id="08746-159">They cannot be created until hello virtual machine exists.</span></span> <span data-ttu-id="08746-160">Par conséquent, les deux ressources sont marqués comme dépendant de la machine virtuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-160">Therefore, both resources are marked as dependent on hello virtual machine.</span></span>

## <a name="profiles"></a><span data-ttu-id="08746-161">Profils</span><span class="sxs-lookup"><span data-stu-id="08746-161">Profiles</span></span>

<span data-ttu-id="08746-162">Plusieurs éléments de profil sont utilisés lors de la définition d’une ressource de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08746-162">Several profile elements are used when defining a virtual machine resource.</span></span> <span data-ttu-id="08746-163">Certains sont obligatoires, et d’autres facultatifs.</span><span class="sxs-lookup"><span data-stu-id="08746-163">Some are required and some are optional.</span></span> <span data-ttu-id="08746-164">Par exemple, les éléments hardwareProfile, osProfile, storageProfile et VM hello sont obligatoires, mais hello diagnosticsProfile est facultatif.</span><span class="sxs-lookup"><span data-stu-id="08746-164">For example, hello hardwareProfile, osProfile, storageProfile, and networkProfile elements are required, but hello diagnosticsProfile is optional.</span></span> <span data-ttu-id="08746-165">Ces profils définissent des paramètres tels que :</span><span class="sxs-lookup"><span data-stu-id="08746-165">These profiles define settings such as:</span></span>
   
- [<span data-ttu-id="08746-166">taille</span><span class="sxs-lookup"><span data-stu-id="08746-166">size</span></span>](sizes.md)
- <span data-ttu-id="08746-167">[nom](/architecture/best-practices/naming-conventions) et informations d’identification</span><span class="sxs-lookup"><span data-stu-id="08746-167">[name](/architecture/best-practices/naming-conventions) and credentials</span></span>
- <span data-ttu-id="08746-168">disque et [paramètres du système d’exploitation](cli-ps-findimage.md)</span><span class="sxs-lookup"><span data-stu-id="08746-168">disk and [operating system settings](cli-ps-findimage.md)</span></span>
- [<span data-ttu-id="08746-169">interface réseau</span><span class="sxs-lookup"><span data-stu-id="08746-169">network interface</span></span>](../../virtual-network/virtual-networks-multiple-nics.md) 
- <span data-ttu-id="08746-170">diagnostics de démarrage</span><span class="sxs-lookup"><span data-stu-id="08746-170">boot diagnostics</span></span>

## <a name="disks-and-images"></a><span data-ttu-id="08746-171">Disques et images</span><span class="sxs-lookup"><span data-stu-id="08746-171">Disks and images</span></span>
   
<span data-ttu-id="08746-172">Dans Azure, les fichiers de disque dur virtuel peuvent représenter [des disques ou des images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08746-172">In Azure, vhd files can represent [disks or images](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="08746-173">Lorsque le système d’exploitation de hello dans un fichier de disque dur virtuel est spécialisé toobe un ordinateur virtuel spécifique, il est référencé tooas un disque.</span><span class="sxs-lookup"><span data-stu-id="08746-173">When hello operating system in a vhd file is specialized toobe a specific VM, it is referred tooas a disk.</span></span> <span data-ttu-id="08746-174">Lorsque le système d’exploitation de hello dans un fichier de disque dur virtuel est généralisée toobe utilisé toocreate de machines virtuelles, il est référencé tooas une image.</span><span class="sxs-lookup"><span data-stu-id="08746-174">When hello operating system in a vhd file is generalized toobe used toocreate many VMs, it is referred tooas an image.</span></span>   
    
### <a name="create-new-virtual-machines-and-new-disks-from-a-platform-image"></a><span data-ttu-id="08746-175">Créer des machines virtuelles et des disques à partir d’une image de plateforme</span><span class="sxs-lookup"><span data-stu-id="08746-175">Create new virtual machines and new disks from a platform image</span></span>

<span data-ttu-id="08746-176">Lorsque vous créez une machine virtuelle, vous devez décider quels toouse du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="08746-176">When you create a VM, you must decide what operating system toouse.</span></span> <span data-ttu-id="08746-177">élément d’imageReference Hello est système de d’exploitation hello toodefine utilisé d’une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="08746-177">hello imageReference element is used toodefine hello operating system of a new VM.</span></span> <span data-ttu-id="08746-178">Hello montre une définition pour un système d’exploitation Windows :</span><span class="sxs-lookup"><span data-stu-id="08746-178">hello example shows a definition for a Windows Server operating system:</span></span>

```
"imageReference": { 
  "publisher": "MicrosoftWindowsServer", 
  "offer": "WindowsServer", 
  "sku": "2012-R2-Datacenter", 
  "version": "latest" 
},
```

<span data-ttu-id="08746-179">Si vous souhaitez toocreate à un système d’exploitation Linux, vous pouvez utiliser cette définition :</span><span class="sxs-lookup"><span data-stu-id="08746-179">If you want toocreate a Linux operating system, you might use this definition:</span></span>

```
"imageReference": {
  "publisher": "Canonical",
  "offer": "UbuntuServer",
  "sku": "14.04.2-LTS",
  "version": "latest"
},
```

<span data-ttu-id="08746-180">Paramètres de configuration de disque de système d’exploitation hello assignés avec un élément d’osDisk hello.</span><span class="sxs-lookup"><span data-stu-id="08746-180">Configuration settings for hello operating system disk are assigned with hello osDisk element.</span></span> <span data-ttu-id="08746-181">Hello exemple définit un nouveau disque géré par hello jeu en mode de mise en cache trop**ReadWrite** et qu’un disque hello est créé à partir d’un [image de plateforme](cli-ps-findimage.md):</span><span class="sxs-lookup"><span data-stu-id="08746-181">hello example defines a new managed disk with hello caching mode set too**ReadWrite** and that hello disk is being created from a [platform image](cli-ps-findimage.md):</span></span>

```
"osDisk": { 
  "name": "[concat('myOSDisk', copyindex())]",
  "caching": "ReadWrite", 
  "createOption": "FromImage" 
},
```

### <a name="create-new-virtual-machines-from-existing-managed-disks"></a><span data-ttu-id="08746-182">Créer de nouvelles machines virtuelles à partir de disques gérés existants</span><span class="sxs-lookup"><span data-stu-id="08746-182">Create new virtual machines from existing managed disks</span></span>

<span data-ttu-id="08746-183">Si vous souhaitez que les ordinateurs virtuels de toocreate à partir de disques existants, supprimez hello imageReference et éléments d’osProfile hello et définir ces paramètres de disque :</span><span class="sxs-lookup"><span data-stu-id="08746-183">If you want toocreate virtual machines from existing disks, remove hello imageReference and hello osProfile elements and define these disk settings:</span></span>

```
"osDisk": { 
  "osType": "Windows",
  "managedDisk": { 
    "id": "[resourceId('Microsoft.Compute/disks', [concat('myOSDisk', copyindex())])]" 
  }, 
  "caching": "ReadWrite",
  "createOption": "Attach" 
},
```

### <a name="create-new-virtual-machines-from-a-managed-image"></a><span data-ttu-id="08746-184">Créer de nouvelles machines virtuelles à partir d'une image gérée</span><span class="sxs-lookup"><span data-stu-id="08746-184">Create new virtual machines from a managed image</span></span>

<span data-ttu-id="08746-185">Si vous voulez toocreate un ordinateur virtuel à partir d’une image managée, modifier l’élément imageReference hello et définir ces paramètres de disque :</span><span class="sxs-lookup"><span data-stu-id="08746-185">If you want toocreate a virtual machine from a managed image, change hello imageReference element and define these disk settings:</span></span>

```
"storageProfile": { 
  "imageReference": {
    "id": "[resourceId('Microsoft.Compute/images', 'myImage')]"
  },
  "osDisk": { 
    "name": "[concat('myOSDisk', copyindex())]",
    "osType": "Windows",
    "caching": "ReadWrite", 
    "createOption": "FromImage" 
  }
},
```

### <a name="attach-data-disks"></a><span data-ttu-id="08746-186">Connecter des disques de données</span><span class="sxs-lookup"><span data-stu-id="08746-186">Attach data disks</span></span>

<span data-ttu-id="08746-187">Vous pouvez éventuellement ajouter des disques de données toohello machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="08746-187">You can optionally add data disks toohello VMs.</span></span> <span data-ttu-id="08746-188">Hello [nombre de disques](sizes.md) dépend de taille hello du disque de système d’exploitation que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="08746-188">hello [number of disks](sizes.md) depends on hello size of operating system disk that you use.</span></span> <span data-ttu-id="08746-189">Avec hello taille des machines virtuelles de hello défini tooStandard_DS1_v2, nombre maximal de hello de disques de données qui pourraient être ajoutées toohello les est deux.</span><span class="sxs-lookup"><span data-stu-id="08746-189">With hello size of hello VMs set tooStandard_DS1_v2, hello maximum number of data disks that could be added toohello them is two.</span></span> <span data-ttu-id="08746-190">Dans l’exemple de hello, un disque de données managé est ajouté tooeach machine virtuelle :</span><span class="sxs-lookup"><span data-stu-id="08746-190">In hello example, one managed data disk is being added tooeach VM:</span></span>

```
"dataDisks": [
  {
    "name": "[concat('myDataDisk', copyindex())]",
    "diskSizeGB": "100",
    "lun": 0, 
    "caching": "ReadWrite",
    "createOption": "Empty"
  }
],
```

## <a name="extensions"></a><span data-ttu-id="08746-191">Extensions</span><span class="sxs-lookup"><span data-stu-id="08746-191">Extensions</span></span>

<span data-ttu-id="08746-192">Bien que [extensions](extensions-features.md) sont une ressource distincte, ils sont étroitement liés tooVMs.</span><span class="sxs-lookup"><span data-stu-id="08746-192">Although [extensions](extensions-features.md) are a separate resource, they are closely tied tooVMs.</span></span> <span data-ttu-id="08746-193">Extensions peuvent être ajoutées en tant qu’une ressource enfant de hello machine virtuelle ou comme une ressource distincte.</span><span class="sxs-lookup"><span data-stu-id="08746-193">Extensions can be added as a child resource of hello VM or as a separate resource.</span></span> <span data-ttu-id="08746-194">Il montre Hello hello [Extension Diagnostics](extensions-diagnostics-template.md) ajouté toohello VM :</span><span class="sxs-lookup"><span data-stu-id="08746-194">hello example shows hello [Diagnostics Extension](extensions-diagnostics-template.md) being added toohello VMs:</span></span>

```
{ 
  "name": "Microsoft.Insights.VMDiagnosticsSettings", 
  "type": "extensions", 
  "location": "[resourceGroup().location]", 
  "apiVersion": "2016-03-30", 
  "dependsOn": [ 
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]" 
  ], 
  "properties": { 
    "publisher": "Microsoft.Azure.Diagnostics", 
    "type": "IaaSDiagnostics", 
    "typeHandlerVersion": "1.5", 
    "autoUpgradeMinorVersion": true, 
    "settings": { 
      "xmlCfg": "[base64(concat(variables('wadcfgxstart'), 
      variables('wadmetricsresourceid'), 
      concat('myVM', copyindex()),
      variables('wadcfgxend')))]", 
      "storageAccount": "[variables('storageName')]" 
    }, 
    "protectedSettings": { 
      "storageAccountName": "[variables('storageName')]", 
      "storageAccountKey": "[listkeys(variables('accountid'), 
        '2015-06-15').key1]", 
      "storageAccountEndPoint": "https://core.windows.net" 
    } 
  } 
},
```

<span data-ttu-id="08746-195">Cette ressource d’extension utilise la variable de storageName hello et les valeurs de tooprovide de variables de diagnostic hello.</span><span class="sxs-lookup"><span data-stu-id="08746-195">This extension resource uses hello storageName variable and hello diagnostic variables tooprovide values.</span></span> <span data-ttu-id="08746-196">Si vous souhaitez que les données de salutation toochange collectées par cette extension, vous pouvez ajouter plus variable wadperfcounters de performances des compteurs toohello.</span><span class="sxs-lookup"><span data-stu-id="08746-196">If you want toochange hello data that is collected by this extension, you can add more performance counters toohello wadperfcounters variable.</span></span> <span data-ttu-id="08746-197">Vous pouvez également choisir les données de diagnostic tooput hello dans un autre compte de stockage que le stockage des disques de machine virtuelle hello.</span><span class="sxs-lookup"><span data-stu-id="08746-197">You could also choose tooput hello diagnostics data into a different storage account than where hello VM disks are stored.</span></span>

<span data-ttu-id="08746-198">Il existe de nombreuses extensions que vous pouvez installer sur un ordinateur virtuel, mais hello plus utile est probablement hello [Extension de Script personnalisé](extensions-customscript.md).</span><span class="sxs-lookup"><span data-stu-id="08746-198">There are many extensions that you can install on a VM, but hello most useful is probably hello [Custom Script Extension](extensions-customscript.md).</span></span> <span data-ttu-id="08746-199">Dans l’exemple de hello, un script PowerShell nommé start.ps1 s’exécute sur chaque ordinateur virtuel lors du premier démarrage :</span><span class="sxs-lookup"><span data-stu-id="08746-199">In hello example, a PowerShell script named start.ps1 runs on each VM when it first starts:</span></span>

```
{
  "name": "MyCustomScriptExtension",
  "type": "extensions",
  "apiVersion": "2016-03-30",
  "location": "[resourceGroup().location]",
  "dependsOn": [
    "[concat('Microsoft.Compute/virtualMachines/myVM', copyindex())]"
  ],
  "properties": {
    "publisher": "Microsoft.Compute",
    "type": "CustomScriptExtension",
    "typeHandlerVersion": "1.7",
    "autoUpgradeMinorVersion": true,
    "settings": {
      "fileUris": [
        "[concat('https://', variables('storageName'),
          '.blob.core.windows.net/customscripts/start.ps1')]" 
      ],
      "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted -File start.ps1"
    }
  }
}
```

<span data-ttu-id="08746-200">script de start.ps1 Hello permettre effectuer de nombreuses tâches de configuration.</span><span class="sxs-lookup"><span data-stu-id="08746-200">hello start.ps1 script can accomplish many configuration tasks.</span></span> <span data-ttu-id="08746-201">Par exemple, les disques de données hello ajoutés dans l’exemple de hello toohello machines virtuelles ne sont pas initialisés ; Vous pouvez utiliser un script personnalisé de tooinitialize les.</span><span class="sxs-lookup"><span data-stu-id="08746-201">For example, hello data disks that are added toohello VMs in hello example are not initialized; you can use a custom script tooinitialize them.</span></span> <span data-ttu-id="08746-202">Si vous avez plusieurs toodo de tâches de démarrage, vous pouvez utiliser des autres scripts PowerShell hello start.ps1 fichier toocall dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="08746-202">If you have multiple startup tasks toodo, you can use hello start.ps1 file toocall other PowerShell scripts in Azure storage.</span></span> <span data-ttu-id="08746-203">exemple de Hello utilise PowerShell, mais vous pouvez utiliser toute méthode de script qui est disponible sur le système d’exploitation hello que vous utilisez.</span><span class="sxs-lookup"><span data-stu-id="08746-203">hello example uses PowerShell, but you can use any scripting method that is available on hello operating system that you are using.</span></span>

<span data-ttu-id="08746-204">Vous pouvez voir l’état hello d’extensions hello installé à partir des paramètres d’Extensions hello dans le portail de hello :</span><span class="sxs-lookup"><span data-stu-id="08746-204">You can see hello status of hello installed extensions from hello Extensions settings in hello portal:</span></span>

![Obtenir l’état de l’extension](./media/template-description/virtual-machines-show-extensions.png)

<span data-ttu-id="08746-206">Vous pouvez également obtenir des informations sur l’extension à l’aide de hello **Get-AzureRmVMExtension** PowerShell commande hello **get d’extension de machine virtuelle** commande Azure CLI 2.0 ou hello **obtenir des informations d’extension**  API REST.</span><span class="sxs-lookup"><span data-stu-id="08746-206">You can also get extension information by using hello **Get-AzureRmVMExtension** PowerShell command, hello **vm extension get** Azure CLI 2.0 command, or hello **Get extension information** REST API.</span></span>

## <a name="deployments"></a><span data-ttu-id="08746-207">Déploiements</span><span class="sxs-lookup"><span data-stu-id="08746-207">Deployments</span></span>

<span data-ttu-id="08746-208">Lorsque vous déployez un modèle, les ressources de hello pistes Azure que vous avez déployé en tant que groupe et automatiquement assigne un nom de groupe toothis déployé.</span><span class="sxs-lookup"><span data-stu-id="08746-208">When you deploy a template, Azure tracks hello resources that you deployed as a group and automatically assigns a name toothis deployed group.</span></span> <span data-ttu-id="08746-209">nom de Hello du déploiement de hello est hello identique au nom du modèle de hello hello.</span><span class="sxs-lookup"><span data-stu-id="08746-209">hello name of hello deployment is hello same as hello name of hello template.</span></span>

<span data-ttu-id="08746-210">Si vous êtes obtenir des informations sur l’état de hello des ressources de déploiement de hello, vous pouvez utiliser le panneau de groupe de ressources hello Bonjour portail Azure :</span><span class="sxs-lookup"><span data-stu-id="08746-210">If you are curious about hello status of resources in hello deployment, you can use hello Resource Group blade in hello Azure portal:</span></span>

![Obtenir les informations de déploiement](./media/template-description/virtual-machines-deployment-info.png)
    
<span data-ttu-id="08746-212">Il n’est pas un problème toouse hello des mêmes ressources toocreate de modèle ou tooupdate des ressources existantes.</span><span class="sxs-lookup"><span data-stu-id="08746-212">It’s not a problem toouse hello same template toocreate resources or tooupdate existing resources.</span></span> <span data-ttu-id="08746-213">Lorsque vous utilisez des modèles de toodeploy de commandes, vous avez hello opportunité toosay qui [mode](../../resource-group-template-deploy.md) vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="08746-213">When you use commands toodeploy templates, you have hello opportunity toosay which [mode](../../resource-group-template-deploy.md) you want toouse.</span></span> <span data-ttu-id="08746-214">Hello peut être défini tooeither **Complete** ou **incrémentiel**.</span><span class="sxs-lookup"><span data-stu-id="08746-214">hello mode can be set tooeither **Complete** or **Incremental**.</span></span> <span data-ttu-id="08746-215">valeur par défaut Hello est toodo les mises à jour incrémentielles.</span><span class="sxs-lookup"><span data-stu-id="08746-215">hello default is toodo incremental updates.</span></span> <span data-ttu-id="08746-216">Soyez prudent lorsque vous utilisez hello **Complete** mode, car vous pouvez supprimer accidentellement des ressources.</span><span class="sxs-lookup"><span data-stu-id="08746-216">Be careful when using hello **Complete** mode because you may accidentally delete resources.</span></span> <span data-ttu-id="08746-217">Lorsque vous définissez le mode hello trop**Complete**, Gestionnaire de ressources supprime toutes les ressources dans le groupe de ressources hello qui ne sont pas dans le modèle de hello.</span><span class="sxs-lookup"><span data-stu-id="08746-217">When you set hello mode too**Complete**, Resource Manager deletes any resources in hello resource group that are not in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="08746-218">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="08746-218">Next Steps</span></span>

- <span data-ttu-id="08746-219">Créez votre propre modèle à l’aide de la rubrique [Création de modèles Azure Resource Manager](../../resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="08746-219">Create your own template using [Authoring Azure Resource Manager templates](../../resource-group-authoring-templates.md).</span></span>
- <span data-ttu-id="08746-220">Déployer le modèle hello que vous avez créé à l’aide de [créer une machine virtuelle Windows avec un modèle de gestionnaire de ressources](ps-template.md).</span><span class="sxs-lookup"><span data-stu-id="08746-220">Deploy hello template that you created using [Create a Windows virtual machine with a Resource Manager template](ps-template.md).</span></span>
- <span data-ttu-id="08746-221">Découvrez comment toomanage hello machines virtuelles que vous avez créée en examinant [créer et gérer des machines virtuelles Windows avec module d’Azure PowerShell hello](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="08746-221">Learn how toomanage hello VMs that you created by reviewing [Create and manage Windows VMs with hello Azure PowerShell module](tutorial-manage-vm.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
