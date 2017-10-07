---
title: "machines virtuelles d’aaaConnect tooLog Analytique | Documents Microsoft"
description: "Pour Windows et Linux machines virtuelles s’exécutant dans Azure, hello recommandé moyen de fichiers journaux collectés et métriques sont en installant l’extension de machine virtuelle Azure de journal Analytique hello. Vous pouvez utiliser hello portail Azure ou PowerShell tooinstall hello extension de machine virtuelle Analytique de journal sur les machines virtuelles Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="78169-104">Connecter des machines virtuelles tooLog Analytique avec un agent Analytique de journal</span><span class="sxs-lookup"><span data-stu-id="78169-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="78169-105">Pour les ordinateurs Windows et Linux, hello méthode recommandée de collecte de journaux et la métrique est en installant l’agent de hello Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="78169-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="78169-106">Hello plus simple façon tooinstall hello Analytique de journal agent sur des machines virtuelles Azure est via hello Extension de machine virtuelle Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="78169-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="78169-107">À l’aide d’extension de hello simplifie le processus d’installation hello et configure automatiquement hello agent toosend données toohello Analytique de journal espace de travail que vous spécifiez.</span><span class="sxs-lookup"><span data-stu-id="78169-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="78169-108">l’agent de Hello est également mis à niveau automatiquement, vous assurer que vous disposez des correctifs et des fonctionnalités les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="78169-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="78169-109">Pour les machines virtuelles Windows, vous activez hello *Microsoft Monitoring Agent* extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="78169-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="78169-110">Pour les ordinateurs virtuels Linux, vous activez hello *OMS Agent pour Linux* extension de machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="78169-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="78169-111">En savoir plus sur [extensions de machine virtuelle Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et hello [agent Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78169-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="78169-112">Lorsque vous utilisez basée sur l’agent de collection pour les données de journal, vous devez configurer [des sources de données dans le journal Analytique](log-analytics-data-sources.md) toospecify hello journaux et les mesures que vous souhaitez toocollect.</span><span class="sxs-lookup"><span data-stu-id="78169-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="78169-113">Si vous configurez des données de journal de tooindex Analytique de journal à l’aide de [diagnostics Azure](log-analytics-azure-storage.md), et que vous configurez hello de toocollect agent hello même ouvre une session, puis hello journaux sont collectés à deux reprises.</span><span class="sxs-lookup"><span data-stu-id="78169-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="78169-114">Vous êtes facturé pour les deux sources de données.</span><span class="sxs-lookup"><span data-stu-id="78169-114">You are charged for both data sources.</span></span> <span data-ttu-id="78169-115">Si vous avez installé d’agent hello, puis collecter des données de journal en utilisant uniquement l’agent hello - vous ne configurez pas les données du journal de toocollect Analytique de journal des diagnostics Azure.</span><span class="sxs-lookup"><span data-stu-id="78169-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="78169-116">Il existe trois méthodes simples pour extension de machine virtuelle tooenable hello Analytique de journal :</span><span class="sxs-lookup"><span data-stu-id="78169-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="78169-117">À l’aide de hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="78169-117">By using hello Azure portal</span></span>
* <span data-ttu-id="78169-118">En utilisant Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="78169-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="78169-119">En utilisant un modèle Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="78169-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="78169-120">Activer l’extension de machine virtuelle hello Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="78169-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="78169-121">Vous pouvez installer l’agent hello pour Analytique de journal et se connecter hello machine virtuelle Azure qui s’exécute sur à l’aide de hello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78169-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="78169-122">tooinstall hello agent d’Analytique de journal et connecter l’espace de travail Analytique de journal hello machine virtuelle tooa</span><span class="sxs-lookup"><span data-stu-id="78169-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="78169-123">L’authentification à hello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78169-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="78169-124">Sélectionnez **Parcourir** sur hello à gauche de hello portail, puis accédez trop**Analytique des journaux (OMS)** et sélectionnez-le.</span><span class="sxs-lookup"><span data-stu-id="78169-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="78169-125">Dans la liste d’espaces de travail Analytique des journaux, sélectionnez hello une que vous souhaitez toouse avec hello machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="78169-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![Espaces de travail OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="78169-127">Sous **Gestion de Log Analytics**, sélectionnez **Machines virtuelles**.</span><span class="sxs-lookup"><span data-stu-id="78169-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="78169-128">![Machines virtuelles](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="78169-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="78169-129">Dans la liste des hello **virtuels**, sélectionnez hello ordinateur virtuel sur lequel vous souhaitez que l’agent de hello de tooinstall.</span><span class="sxs-lookup"><span data-stu-id="78169-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="78169-130">Hello **état de la connexion OMS** pour hello machine virtuelle indique qu’il est **non connecté**.</span><span class="sxs-lookup"><span data-stu-id="78169-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="78169-131">![Machine virtuelle non connectée](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="78169-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="78169-132">Dans Détails hello pour votre machine virtuelle, sélectionnez **connexion**.</span><span class="sxs-lookup"><span data-stu-id="78169-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="78169-133">l’agent de Hello est automatiquement installé et configuré pour votre espace de travail Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="78169-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="78169-134">Ce processus prend quelques minutes, pendant cette période est hello état de la connexion d’OMS *connexion...*</span><span class="sxs-lookup"><span data-stu-id="78169-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="78169-135">![Connecter une machine virtuelle](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="78169-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="78169-136">Après avoir installé et connecter l’agent de hello, hello **connexion OMS** état sera mis à jour tooshow **cet espace de travail**.</span><span class="sxs-lookup"><span data-stu-id="78169-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="78169-137">![Connecté](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="78169-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="78169-138">Activer l’extension de machine virtuelle hello à l’aide de PowerShell</span><span class="sxs-lookup"><span data-stu-id="78169-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="78169-139">Lorsque vous configurez votre machine virtuelle à l’aide de PowerShell, vous devez tooprovide hello **Id_espace_de_travail** et **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="78169-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="78169-140">les noms de propriété Hello dans votre configuration json sont **respectant la casse**.</span><span class="sxs-lookup"><span data-stu-id="78169-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="78169-141">Vous pouvez trouver hello Id et la clé sur hello **paramètres** page du portail OMS de hello, ou à l’aide de PowerShell comme indiqué dans le précédent exemple de hello.</span><span class="sxs-lookup"><span data-stu-id="78169-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![ID d’espace de travail et clé primaire](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="78169-143">Il existe différentes commandes pour les machines virtuelles Azure Classic et Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="78169-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="78169-144">Vous trouverez ci-dessous des exemples pour les machines virtuelles Azure Classic et Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="78169-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="78169-145">Pour les machines virtuelles classiques, utilisez hello l’exemple PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="78169-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="78169-146">Pour les ordinateurs virtuels Linux de gestionnaire de ressources à l’aide de hello suivant CLI</span><span class="sxs-lookup"><span data-stu-id="78169-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="78169-147">Pour les ordinateurs virtuels de gestionnaire de ressources, utilisez hello l’exemple PowerShell suivant :</span><span class="sxs-lookup"><span data-stu-id="78169-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="78169-148">Extension de machine virtuelle hello à l’aide d’un modèle de déploiement</span><span class="sxs-lookup"><span data-stu-id="78169-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="78169-149">À l’aide de Azure Resource Manager, vous pouvez créer un modèle (en format JSON) qui définit la configuration de votre application et de déploiement de hello.</span><span class="sxs-lookup"><span data-stu-id="78169-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="78169-150">Ce modèle est appelé un modèle de gestionnaire de ressources et fournit un déploiement toodefine de façon déclarative.</span><span class="sxs-lookup"><span data-stu-id="78169-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="78169-151">En utilisant un modèle, vous pouvez à plusieurs reprises déployer votre application tout au long du cycle de vie application hello et tout en étant certain que vos ressources sont déployées dans un état cohérent.</span><span class="sxs-lookup"><span data-stu-id="78169-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="78169-152">En incluant l’agent de hello Analytique de journal en tant que partie de votre modèle de gestionnaire de ressources, vous pouvez vous assurer que chaque machine virtuelle est préconfigurée de manière tooreport tooyour Analytique de journal espace de travail.</span><span class="sxs-lookup"><span data-stu-id="78169-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="78169-153">Pour plus d’informations sur les modèles Azure Resource Manager, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="78169-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="78169-154">Voici un exemple d’un modèle de gestionnaire de ressources qui est utilisé pour déployer un ordinateur virtuel qui exécute Windows hello extension Microsoft Monitoring Agent installée.</span><span class="sxs-lookup"><span data-stu-id="78169-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="78169-155">Ce modèle est un modèle de type machine virtuelle, avec hello suivant ajouts :</span><span class="sxs-lookup"><span data-stu-id="78169-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="78169-156">Paramètres workspaceId et workspaceName</span><span class="sxs-lookup"><span data-stu-id="78169-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="78169-157">Section d’extension de ressources Microsoft.EnterpriseCloud.Monitoring</span><span class="sxs-lookup"><span data-stu-id="78169-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="78169-158">Toolook sorties hello Id_espace_de_travail et workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="78169-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="78169-159">Vous pouvez déployer un modèle à l’aide de hello suivant de commande PowerShell :</span><span class="sxs-lookup"><span data-stu-id="78169-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="78169-160">Résolution des problèmes d’extension de machine virtuelle Analytique de journal hello</span><span class="sxs-lookup"><span data-stu-id="78169-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="78169-161">Vous recevez généralement un message émis par le portail Azure ou par Azure PowerShell en cas de problème.</span><span class="sxs-lookup"><span data-stu-id="78169-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="78169-162">L’authentification à hello [portail Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="78169-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="78169-163">Recherche hello machine virtuelle et ouvrez les détails de l’ordinateur virtuel.</span><span class="sxs-lookup"><span data-stu-id="78169-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="78169-164">Cliquez sur **Extensions** toocheck si l’extension d’OMS est activée ou non.</span><span class="sxs-lookup"><span data-stu-id="78169-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![Vue Extension de machine virtuelle](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="78169-166">Cliquez sur hello *MicrosoftMonitoringAgent*(Windows) ou *OmsAgentForLinux*(Linux) extension et consulter les détails.</span><span class="sxs-lookup"><span data-stu-id="78169-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Détails de l’extension de machine virtuelle](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="78169-168">Résolution des problèmes de machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="78169-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="78169-169">Si hello *Microsoft Monitoring Agent* extension de l’agent de machine virtuelle n’est pas l’installation ou de création de rapports, vous pouvez effectuer hello suivant le problème de hello tootroubleshoot étapes.</span><span class="sxs-lookup"><span data-stu-id="78169-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="78169-170">Vérifiez si l’agent de machine virtuelle Azure hello est installé et les étapes de travail correctement à l’aide de hello [Ko 2965986](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="78169-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="78169-171">Vous pouvez également consulter le fichier de journal de l’agent de machine virtuelle hello`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="78169-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="78169-172">Si le journal de hello n’existe pas, l’agent de machine virtuelle hello n’est pas installé.</span><span class="sxs-lookup"><span data-stu-id="78169-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="78169-173">Installer hello Agent de machine virtuelle Azure sur des machines virtuelles classiques</span><span class="sxs-lookup"><span data-stu-id="78169-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="78169-174">Confirmer hello Microsoft Monitoring Agent tâche de pulsation d’extension est en cours d’exécution à l’aide de hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="78169-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="78169-175">Ouvrez une session dans la machine virtuelle de toohello</span><span class="sxs-lookup"><span data-stu-id="78169-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="78169-176">Ouvrez le Planificateur de tâches et de recherche hello `update_azureoperationalinsight_agent_heartbeat` tâche</span><span class="sxs-lookup"><span data-stu-id="78169-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="78169-177">Confirmer la tâche hello est activé et qu’il s’exécute chaque minute</span><span class="sxs-lookup"><span data-stu-id="78169-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="78169-178">Vérifiez le fichier journal de pulsation de hello`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="78169-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="78169-179">Passez en revue les fichiers de journaux Microsoft Monitoring Agent VM extension hello dans`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="78169-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="78169-180">Vérifiez la machine virtuelle de hello peut exécuter des scripts PowerShell</span><span class="sxs-lookup"><span data-stu-id="78169-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="78169-181">Vérifiez que les autorisations sur C:\Windows\temp n’ont pas été modifiées.</span><span class="sxs-lookup"><span data-stu-id="78169-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="78169-182">Afficher l’état de hello Microsoft Monitoring Agent en tapant hello suivant de commande dans une fenêtre PowerShell avec élévation de privilèges sur l’ordinateur virtuel de hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="78169-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="78169-183">Passez en revue les fichiers de journaux d’installation hello Microsoft Monitoring Agent dans`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="78169-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="78169-184">Pour plus d’informations, consultez [Résolution des problèmes des extensions Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="78169-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="78169-185">Résolution des problèmes des machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="78169-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="78169-186">Si hello *Agent OMS pour Linux* extension de l’agent de machine virtuelle n’est pas l’installation ou de création de rapports, vous pouvez effectuer hello suivant le problème de hello tootroubleshoot étapes.</span><span class="sxs-lookup"><span data-stu-id="78169-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="78169-187">Si l’état de l’extension hello est *inconnu* Vérifiez si l’agent de machine virtuelle Azure hello est installé et fonctionne correctement en consultant le fichier de journal de l’agent de machine virtuelle hello`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="78169-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="78169-188">Si le journal de hello n’existe pas, l’agent de machine virtuelle hello n’est pas installé.</span><span class="sxs-lookup"><span data-stu-id="78169-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="78169-189">Installer hello Agent de machine virtuelle Azure sur les machines virtuelles Linux</span><span class="sxs-lookup"><span data-stu-id="78169-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="78169-190">Pour les autres États de fonctionnement anormales, révision hello Agent OMS pour extension Linux VM fichiers journaux `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` et`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="78169-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="78169-191">Si le statut de l’extension hello est intègre, mais données ne sont pas en cours de téléchargement examiner hello Agent OMS pour Linux des fichiers journaux`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="78169-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="78169-192">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="78169-192">Next steps</span></span>
* <span data-ttu-id="78169-193">Configurer [des sources de données dans le journal Analytique](log-analytics-data-sources.md) toocollect des métriques et journaux hello toospecify.</span><span class="sxs-lookup"><span data-stu-id="78169-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="78169-194">toogather des données à partir d’ordinateurs virtuels [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="78169-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="78169-195">Pour d’autres ressources s’exécutant dans Azure, [collectez des données à l’aide des diagnostics Azure](log-analytics-azure-storage.md).</span><span class="sxs-lookup"><span data-stu-id="78169-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="78169-196">Pour les ordinateurs qui ne sont pas dans Azure, vous pouvez installer l’agent de hello Analytique de journal à l’aide des méthodes hello décrits dans hello suivant des articles :</span><span class="sxs-lookup"><span data-stu-id="78169-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="78169-197">Se connecter à Windows ordinateurs tooLog Analytique</span><span class="sxs-lookup"><span data-stu-id="78169-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="78169-198">Connecter des ordinateurs de Linux tooLog Analytique</span><span class="sxs-lookup"><span data-stu-id="78169-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
