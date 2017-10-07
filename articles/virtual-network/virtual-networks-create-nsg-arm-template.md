---
title: "aaaCreate réseau des groupes de sécurité - modèle de gestionnaire de ressources Azure | Documents Microsoft"
description: "Découvrez comment toocreate et déployer des groupes de sécurité réseau à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: f3e7385d-717c-44ff-be20-f9aa450aa99b
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3750168284fea7b41c8c0f908b0d31a9da5e38ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-network-security-groups-using-an-azure-resource-manager-template"></a>Créer des groupes de sécurité réseau à l’aide d’un modèle Azure Resource Manager

[!INCLUDE [virtual-networks-create-nsg-selectors-arm-include](../../includes/virtual-networks-create-nsg-selectors-arm-include.md)]

[!INCLUDE [virtual-networks-create-nsg-intro-include](../../includes/virtual-networks-create-nsg-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Cet article décrit le modèle de déploiement du Gestionnaire de ressources hello. Vous pouvez également [créer des groupes de sécurité réseau dans le modèle de déploiement classique hello](virtual-networks-create-nsg-classic-ps.md).

[!INCLUDE [virtual-networks-create-nsg-scenario-include](../../includes/virtual-networks-create-nsg-scenario-include.md)]

## <a name="nsg-resources-in-a-template-file"></a>Ressources NSG dans un fichier de modèle
Vous pouvez afficher et télécharger hello [exemple de modèle](https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/NSGs.json).

Hello section suivante présente définition hello Hello NSG frontal, selon le scénario de hello.

```json
"apiVersion": "2015-06-15",
"type": "Microsoft.Network/networkSecurityGroups",
"name": "[parameters('frontEndNSGName')]",
"location": "[resourceGroup().location]",
"tags": {
  "displayName": "NSG - Front End"
},
"properties": {
  "securityRules": [
    {
      "name": "rdp-rule",
      "properties": {
        "description": "Allow RDP",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "3389",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 100,
        "direction": "Inbound"
      }
    },
    {
      "name": "web-rule",
      "properties": {
        "description": "Allow WEB",
        "protocol": "Tcp",
        "sourcePortRange": "*",
        "destinationPortRange": "80",
        "sourceAddressPrefix": "Internet",
        "destinationAddressPrefix": "*",
        "access": "Allow",
        "priority": 101,
        "direction": "Inbound"
      }
    }
  ]
}
```
tooassociate hello NSG toohello sous-réseau frontal, vous disposez de définition de sous-réseau toochange hello dans le modèle de hello et utiliser l’id référence hello pour hello groupe de sécurité réseau.

```json
"subnets": [
  {
    "name": "[parameters('frontEndSubnetName')]",
    "properties": {
      "addressPrefix": "[parameters('frontEndSubnetPrefix')]",
      "networkSecurityGroup": {
      "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('frontEndNSGName'))]"
      }
    }
  }, 
```

Notez que même en cours d’exécution pour hello principal groupe de sécurité réseau et hello sous-réseau principal dans le modèle de hello hello.

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Déployer le modèle de hello ARM à l’aide de cliquez sur toodeploy
Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus. toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](http://github.com/telmosampaio/azure-templates/tree/master/201-IaaS-WebFrontEnd-SQLBackEnd-NSG), cliquez sur **déployer tooAzure**, remplacez les valeurs de paramètre par défaut hello si nécessaire et suivez les instructions de hello dans le portail de hello.

## <a name="deploy-hello-arm-template-by-using-powershell"></a>Déployer le modèle de hello ARM à l’aide de PowerShell
modèle d’ARM hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé Azure PowerShell, suivez les instructions de hello Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) tooinstall et le configurer.
2. Exécutez hello  **`New-AzureRmResourceGroup`**  toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.

    ```powershell
    New-AzureRmResourceGroup -Name TestRG -Location uswest `
    -TemplateFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' `
    -TemplateParameterFile 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Sortie attendue :

        ResourceGroupName : TestRG
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        Permissions       :
                            Actions  NotActions
                            =======  ==========
                            *                  
   
        Resources         :
                            Name                Type                                     Location
                            ==================  =======================================  ========
                            sqlAvSet            Microsoft.Compute/availabilitySets       westus  
                            webAvSet            Microsoft.Compute/availabilitySets       westus  
                            SQL1                Microsoft.Compute/virtualMachines        westus  
                            SQL2                Microsoft.Compute/virtualMachines        westus  
                            Web1                Microsoft.Compute/virtualMachines        westus  
                            Web2                Microsoft.Compute/virtualMachines        westus  
                            TestNICSQL1         Microsoft.Network/networkInterfaces      westus  
                            TestNICSQL2         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb1         Microsoft.Network/networkInterfaces      westus  
                            TestNICWeb2         Microsoft.Network/networkInterfaces      westus  
                            NSG-BackEnd         Microsoft.Network/networkSecurityGroups  westus  
                            NSG-FrontEnd        Microsoft.Network/networkSecurityGroups  westus  
                            TestPIPSQL1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPSQL2         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb1         Microsoft.Network/publicIPAddresses      westus  
                            TestPIPWeb2         Microsoft.Network/publicIPAddresses      westus  
                            TestVNet            Microsoft.Network/virtualNetworks        westus  
                            testvnetstorageprm  Microsoft.Storage/storageAccounts        westus  
                            testvnetstoragestd  Microsoft.Storage/storageAccounts        westus  
   
        ResourceId        : /subscriptions/[Subscription Id]/resourceGroups/TestRG

## <a name="deploy-hello-arm-template-by-using-hello-azure-cli"></a>Déployer le modèle de hello ARM à l’aide de hello CLI d’Azure
modèle ARM hello toodeploy à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello  **`azure config mode`**  mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.

    ```azurecli
    azure config mode arm
    ```

    Hello Voici la sortie hello attendu pour la commande hello :

        info:    New mode is arm

3. Exécutez hello  **`azure group deployment create`**  applet de commande toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.

    ```azurecli
    azure group create -n TestRG -l westus -f 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.json' -e 'https://raw.githubusercontent.com/telmosampaio/azure-templates/master/201-IaaS-WebFrontEnd-SQLBackEnd/azuredeploy.parameters.json'
    ```

    Sortie attendue :
   
        info:    Executing command group create
        info:    Getting resource group TestRG
        info:    Creating resource group TestRG
        info:    Created resource group TestRG
        info:    Initializing template configurations and parameters
        info:    Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/TestRG
        data:    Name:                TestRG
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:    
        info:    group create command OK
   
   * **-n (ou --name)**. Nom de toobe de groupe de ressources hello créé.
   * **-l (ou --location)**. Région Azure où le groupe de ressources hello sera créé.
   * **-f (ou --template-file)**. Fichier de modèle de chemin d’accès tooyour ARM.
   * **-e (ou --parameters-file)**. Fichier de paramètres de chemin d’accès tooyour ARM.

