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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Connecter des machines virtuelles tooLog Analytique avec un agent Analytique de journal

Pour les ordinateurs Windows et Linux, hello méthode recommandée de collecte de journaux et la métrique est en installant l’agent de hello Analytique de journal.

Hello plus simple façon tooinstall hello Analytique de journal agent sur des machines virtuelles Azure est via hello Extension de machine virtuelle Analytique de journal.  À l’aide d’extension de hello simplifie le processus d’installation hello et configure automatiquement hello agent toosend données toohello Analytique de journal espace de travail que vous spécifiez. l’agent de Hello est également mis à niveau automatiquement, vous assurer que vous disposez des correctifs et des fonctionnalités les plus récentes hello.

Pour les machines virtuelles Windows, vous activez hello *Microsoft Monitoring Agent* extension de machine virtuelle.
Pour les ordinateurs virtuels Linux, vous activez hello *OMS Agent pour Linux* extension de machine virtuelle.

En savoir plus sur [extensions de machine virtuelle Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et hello [agent Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Lorsque vous utilisez basée sur l’agent de collection pour les données de journal, vous devez configurer [des sources de données dans le journal Analytique](log-analytics-data-sources.md) toospecify hello journaux et les mesures que vous souhaitez toocollect.

> [!IMPORTANT]
> Si vous configurez des données de journal de tooindex Analytique de journal à l’aide de [diagnostics Azure](log-analytics-azure-storage.md), et que vous configurez hello de toocollect agent hello même ouvre une session, puis hello journaux sont collectés à deux reprises. Vous êtes facturé pour les deux sources de données. Si vous avez installé d’agent hello, puis collecter des données de journal en utilisant uniquement l’agent hello - vous ne configurez pas les données du journal de toocollect Analytique de journal des diagnostics Azure.
>
>

Il existe trois méthodes simples pour extension de machine virtuelle tooenable hello Analytique de journal :

* À l’aide de hello portail Azure
* En utilisant Azure PowerShell
* En utilisant un modèle Azure Resource Manager

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Activer l’extension de machine virtuelle hello Bonjour portail Azure
Vous pouvez installer l’agent hello pour Analytique de journal et se connecter hello machine virtuelle Azure qui s’exécute sur à l’aide de hello [portail Azure](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall hello agent d’Analytique de journal et connecter l’espace de travail Analytique de journal hello machine virtuelle tooa
1. L’authentification à hello [portail Azure](http://portal.azure.com).
2. Sélectionnez **Parcourir** sur hello à gauche de hello portail, puis accédez trop**Analytique des journaux (OMS)** et sélectionnez-le.
3. Dans la liste d’espaces de travail Analytique des journaux, sélectionnez hello une que vous souhaitez toouse avec hello machine virtuelle Azure.  
   ![Espaces de travail OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. Sous **Gestion de Log Analytics**, sélectionnez **Machines virtuelles**.  
   ![Machines virtuelles](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. Dans la liste des hello **virtuels**, sélectionnez hello ordinateur virtuel sur lequel vous souhaitez que l’agent de hello de tooinstall. Hello **état de la connexion OMS** pour hello machine virtuelle indique qu’il est **non connecté**.  
   ![Machine virtuelle non connectée](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. Dans Détails hello pour votre machine virtuelle, sélectionnez **connexion**. l’agent de Hello est automatiquement installé et configuré pour votre espace de travail Analytique de journal. Ce processus prend quelques minutes, pendant cette période est hello état de la connexion d’OMS *connexion...*  
   ![Connecter une machine virtuelle](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. Après avoir installé et connecter l’agent de hello, hello **connexion OMS** état sera mis à jour tooshow **cet espace de travail**.  
   ![Connecté](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Activer l’extension de machine virtuelle hello à l’aide de PowerShell
Lorsque vous configurez votre machine virtuelle à l’aide de PowerShell, vous devez tooprovide hello **Id_espace_de_travail** et **workspaceKey**. les noms de propriété Hello dans votre configuration json sont **respectant la casse**.

Vous pouvez trouver hello Id et la clé sur hello **paramètres** page du portail OMS de hello, ou à l’aide de PowerShell comme indiqué dans le précédent exemple de hello.

![ID d’espace de travail et clé primaire](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Il existe différentes commandes pour les machines virtuelles Azure Classic et Azure Resource Manager. Vous trouverez ci-dessous des exemples pour les machines virtuelles Azure Classic et Azure Resource Manager.

Pour les machines virtuelles classiques, utilisez hello l’exemple PowerShell suivant :

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

Pour les ordinateurs virtuels Linux de gestionnaire de ressources à l’aide de hello suivant CLI
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Pour les ordinateurs virtuels de gestionnaire de ressources, utilisez hello l’exemple PowerShell suivant :

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


## <a name="deploy-hello-vm-extension-using-a-template"></a>Extension de machine virtuelle hello à l’aide d’un modèle de déploiement
À l’aide de Azure Resource Manager, vous pouvez créer un modèle (en format JSON) qui définit la configuration de votre application et de déploiement de hello. Ce modèle est appelé un modèle de gestionnaire de ressources et fournit un déploiement toodefine de façon déclarative. En utilisant un modèle, vous pouvez à plusieurs reprises déployer votre application tout au long du cycle de vie application hello et tout en étant certain que vos ressources sont déployées dans un état cohérent.

En incluant l’agent de hello Analytique de journal en tant que partie de votre modèle de gestionnaire de ressources, vous pouvez vous assurer que chaque machine virtuelle est préconfigurée de manière tooreport tooyour Analytique de journal espace de travail.

Pour plus d’informations sur les modèles Azure Resource Manager, voir [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Voici un exemple d’un modèle de gestionnaire de ressources qui est utilisé pour déployer un ordinateur virtuel qui exécute Windows hello extension Microsoft Monitoring Agent installée. Ce modèle est un modèle de type machine virtuelle, avec hello suivant ajouts :

* Paramètres workspaceId et workspaceName
* Section d’extension de ressources Microsoft.EnterpriseCloud.Monitoring
* Toolook sorties hello Id_espace_de_travail et workspaceSharedKey

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

Vous pouvez déployer un modèle à l’aide de hello suivant de commande PowerShell :

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Résolution des problèmes d’extension de machine virtuelle Analytique de journal hello
Vous recevez généralement un message émis par le portail Azure ou par Azure PowerShell en cas de problème.

1. L’authentification à hello [portail Azure](http://portal.azure.com).
2. Recherche hello machine virtuelle et ouvrez les détails de l’ordinateur virtuel.
3. Cliquez sur **Extensions** toocheck si l’extension d’OMS est activée ou non.

   ![Vue Extension de machine virtuelle](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Cliquez sur hello *MicrosoftMonitoringAgent*(Windows) ou *OmsAgentForLinux*(Linux) extension et consulter les détails. 

   ![Détails de l’extension de machine virtuelle](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Résolution des problèmes de machines virtuelles
Si hello *Microsoft Monitoring Agent* extension de l’agent de machine virtuelle n’est pas l’installation ou de création de rapports, vous pouvez effectuer hello suivant le problème de hello tootroubleshoot étapes.

1. Vérifiez si l’agent de machine virtuelle Azure hello est installé et les étapes de travail correctement à l’aide de hello [Ko 2965986](https://support.microsoft.com/kb/2965986#mt1).
   * Vous pouvez également consulter le fichier de journal de l’agent de machine virtuelle hello`C:\WindowsAzure\logs\WaAppAgent.log`
   * Si le journal de hello n’existe pas, l’agent de machine virtuelle hello n’est pas installé.
     * [Installer hello Agent de machine virtuelle Azure sur des machines virtuelles classiques](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Confirmer hello Microsoft Monitoring Agent tâche de pulsation d’extension est en cours d’exécution à l’aide de hello comme suit :
   * Ouvrez une session dans la machine virtuelle de toohello
   * Ouvrez le Planificateur de tâches et de recherche hello `update_azureoperationalinsight_agent_heartbeat` tâche
   * Confirmer la tâche hello est activé et qu’il s’exécute chaque minute
   * Vérifiez le fichier journal de pulsation de hello`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Passez en revue les fichiers de journaux Microsoft Monitoring Agent VM extension hello dans`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Vérifiez la machine virtuelle de hello peut exécuter des scripts PowerShell
5. Vérifiez que les autorisations sur C:\Windows\temp n’ont pas été modifiées.
6. Afficher l’état de hello Microsoft Monitoring Agent en tapant hello suivant de commande dans une fenêtre PowerShell avec élévation de privilèges sur l’ordinateur virtuel de hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Passez en revue les fichiers de journaux d’installation hello Microsoft Monitoring Agent dans`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Pour plus d’informations, consultez [Résolution des problèmes des extensions Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Résolution des problèmes des machines virtuelles Linux
Si hello *Agent OMS pour Linux* extension de l’agent de machine virtuelle n’est pas l’installation ou de création de rapports, vous pouvez effectuer hello suivant le problème de hello tootroubleshoot étapes.

1. Si l’état de l’extension hello est *inconnu* Vérifiez si l’agent de machine virtuelle Azure hello est installé et fonctionne correctement en consultant le fichier de journal de l’agent de machine virtuelle hello`/var/log/waagent.log`
   * Si le journal de hello n’existe pas, l’agent de machine virtuelle hello n’est pas installé.
   * [Installer hello Agent de machine virtuelle Azure sur les machines virtuelles Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Pour les autres États de fonctionnement anormales, révision hello Agent OMS pour extension Linux VM fichiers journaux `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` et`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Si le statut de l’extension hello est intègre, mais données ne sont pas en cours de téléchargement examiner hello Agent OMS pour Linux des fichiers journaux`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Étapes suivantes
* Configurer [des sources de données dans le journal Analytique](log-analytics-data-sources.md) toocollect des métriques et journaux hello toospecify.
* toogather des données à partir d’ordinateurs virtuels [solutions Analytique de journal ajouter à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md).
* Pour d’autres ressources s’exécutant dans Azure, [collectez des données à l’aide des diagnostics Azure](log-analytics-azure-storage.md).

Pour les ordinateurs qui ne sont pas dans Azure, vous pouvez installer l’agent de hello Analytique de journal à l’aide des méthodes hello décrits dans hello suivant des articles :

* [Se connecter à Windows ordinateurs tooLog Analytique](log-analytics-windows-agents.md)
* [Connecter des ordinateurs de Linux tooLog Analytique](log-analytics-linux-agents.md)
