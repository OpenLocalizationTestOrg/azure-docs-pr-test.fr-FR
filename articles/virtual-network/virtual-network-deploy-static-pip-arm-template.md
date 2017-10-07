---
title: "aaaCreate une machine virtuelle avec une adresse IP publique statique - modèle Azure Resource Manager | Documents Microsoft"
description: "Découvrez comment toocreate une machine virtuelle avec une adresse IP publique statique d’adresses à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: d551085a-c7ed-4ec6-b4c3-e9e1cebb774c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/27/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 6a8640ed4fad06b0e09820e6114fd6789db73847
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-an-azure-resource-manager-template"></a>Créer une machine virtuelle avec une adresse IP publique statique à l’aide d’un modèle Azure Resource Manager

> [!div class="op_single_selector"]
> * [portail Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Interface de ligne de commande Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Modèle](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (classique)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu du modèle de déploiement classique hello.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="public-ip-address-resources-in-a-template-file"></a>Ressources d’adresses IP publiques dans un fichier de modèle
Vous pouvez afficher et télécharger hello [exemple de modèle](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json).

Hello section suivante montre définition hello de ressource IP publique hello, selon le scénario hello ci-dessus :

```json
{
  "apiVersion": "2015-06-15",
  "type": "Microsoft.Network/publicIPAddresses",
  "name": "[variables('webVMSetting').pipName]",
  "location": "[variables('location')]",
  "properties": {
    "publicIPAllocationMethod": "Static"
  },
  "tags": {
    "displayName": "PublicIPAddress - Web"
  }
},
```

Hello d’avis **publicIPAllocationMethod** propriété, qui est définie trop*statique*. Cette propriété peut avoir la valeur *Dynamic* (par défaut) ou *Static*. Définir les garanties toostatic qui adresse IP publique hello attribuée ne change pas.

Hello section suivante montre association hello d’adresse IP publique de hello avec une interface réseau :

```json
  {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[variables('webVMSetting').nicName]",
    "location": "[variables('location')]",
    "tags": {
    "displayName": "NetworkInterface - Web"
    },
    "dependsOn": [
      "[concat('Microsoft.Network/publicIPAddresses/', variables('webVMSetting').pipName)]",
      "[concat('Microsoft.Network/virtualNetworks/', parameters('vnetName'))]"
    ],
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
          "privateIPAllocationMethod": "Static",
          "privateIPAddress": "[variables('webVMSetting').ipAddress]",
          "publicIPAddress": {
          "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('webVMSetting').pipName)]"
          },
          "subnet": {
            "id": "[variables('frontEndSubnetRef')]"
          }
        }
      }
    ]
  }
},
```

Hello d’avis **publicIPAddress** propriété pointant toohello **Id** d’une ressource nommée **variables('webVMSetting').pipName**. Qui est le nom hello de ressource IP publique hello indiquée ci-dessus.

Enfin, interface de réseau hello ci-dessus est répertorié dans hello **VM** propriété Hello machine virtuelle en cours de création.

```json
      "networkProfile": {
        "networkInterfaces": [
          {
            "id": "[resourceId('Microsoft.Network/networkInterfaces', variables('webVMSetting').nicName)]"
          }
        ]
      }
```

## <a name="deploy-hello-template-by-using-click-toodeploy"></a>Déployer le modèle de hello à l’aide de cliquez sur toodeploy

Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus. toodeploy ce modèle à l’aide cliquez sur toodeploy, cliquez sur **déployer tooAzure** dans le fichier Readme.md hello hello [machine virtuelle avec PIP statique](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/03-Static-public-IP) modèle. Remplacez les valeurs de paramètre par défaut hello si vous le souhaitez et entrez des valeurs pour les paramètres vide hello.  Suivez les instructions de hello de toocreate de portail hello une machine virtuelle avec une adresse IP publique statique.

## <a name="deploy-hello-template-by-using-powershell"></a>Déployer le modèle de hello à l’aide de PowerShell

modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé Azure PowerShell, hello terminé les étapes Bonjour [comment tooInstall et configurer Azure PowerShell](/powershell/azure/overview) l’article.
2. Dans une console PowerShell, exécutez hello `New-AzureRmResourceGroup` toocreate de l’applet de commande Nouveau groupe de ressources, si nécessaire. Si vous avez déjà créé un groupe de ressources, accédez à toostep 3.

    ```powershell
    New-AzureRmResourceGroup -Name PIPTEST -Location westus
    ```

    Sortie attendue :
   
        ResourceGroupName : PIPTEST
        Location          : westus
        ProvisioningState : Succeeded
        Tags              :
        ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/StaticPublicIP

3. Dans une console PowerShell, exécutez hello `New-AzureRmResourceGroupDeployment` modèle de hello toodeploy applet de commande.

    ```powershell
    New-AzureRmResourceGroupDeployment -Name DeployVM -ResourceGroupName PIPTEST `
        -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json `
        -TemplateParameterUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json
    ```

    Sortie attendue :
   
        DeploymentName    : DeployVM
        ResourceGroupName : PIPTEST
        ProvisioningState : Succeeded
        Timestamp         : [Date and time]
        Mode              : Incremental
        TemplateLink      :
                            Uri            : https://raw.githubusercontent.com/Azure/azure-quickstart-templates/mas
                            ter/IaaS-Story/03-Static-public-IP/azuredeploy.json
                            ContentVersion : 1.0.0.0
   
        Parameters        :
                            Name                      Type                       Value     
                            ========================  =========================  ==========
                            vnetName                  String                     WTestVNet
                            vnetPrefix                String                     192.168.0.0/16
                            frontEndSubnetName        String                     FrontEnd  
                            frontEndSubnetPrefix      String                     192.168.1.0/24
                            storageAccountNamePrefix  String                     iaasestd  
                            stdStorageType            String                     Standard_LRS
                            osType                    String                     Windows   
                            adminUsername             String                     adminUser
                            adminPassword             SecureString                         
   
        Outputs           :

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Déployer le modèle de hello à l’aide de hello CLI d’Azure
modèle de hello toodeploy à l’aide de hello CLI d’Azure, hello complète comme suit :

1. Si vous n’avez jamais utilisé CLI d’Azure, suivez les étapes de hello Bonjour [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) tooinstall de l’article et le configurer.
2. Exécutez hello `azure config mode` mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.

    ```azurecli
    azure config mode arm
    ```

    Hello attendu la sortie de commande hello ci-dessus :

        info:    New mode is arm

3. Ouvrez hello [fichier de paramètres](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.parameters.json), sélectionnez son contenu et enregistrez-le tooa fichier sur votre ordinateur. Pour cet exemple, les paramètres de hello sont enregistrés les fichiers tooa nommé *parameters.json*. Modifier les valeurs de paramètre hello dans fichier hello si vous le souhaitez, mais au minimum, il est recommandé de modifier la valeur hello pour hello adminPassword paramètre tooa unique mot de passe complexe.
4. Exécutez hello `azure group deployment create` cmd toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés. Dans la commande de hello ci-dessous, remplacez <path> avec le chemin d’accès hello vous avez enregistré le fichier hello. 

    ```azurecli
    azure group create -n PIPTEST2 -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/03-Static-public-IP/azuredeploy.json -e <path>\parameters.json
    ```

    Sortie attendue (répertorie les valeurs de paramètre utilisées) :

        info:    Executing command group create
        + Getting resource group PIPTEST2
        + Creating resource group PIPTEST2
        info:    Created resource group PIPTEST2
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/[Subscription ID]/resourceGroups/PIPTEST2
        data:    Name:                PIPTEST2
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

