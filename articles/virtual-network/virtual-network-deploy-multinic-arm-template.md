---
title: "aaaCreate une machine virtuelle avec plusieurs cartes réseau - modèle Azure Resource Manager | Documents Microsoft"
description: "Créez une machine virtuelle avec plusieurs cartes réseau à l’aide d’un modèle Azure Resource Manager."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 486f7dd5-cf2f-434c-85d1-b3e85c427def
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/02/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f5d9ffcbd40c72dc18ae6de38e739eb5e45bf669
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-multiple-nics-using-a-template"></a>Créer une machine virtuelle avec plusieurs cartes réseau à l’aide d’un modèle
[!INCLUDE [virtual-network-deploy-multinic-arm-selectors-include.md](../../includes/virtual-network-deploy-multinic-arm-selectors-include.md)]

[!INCLUDE [virtual-network-deploy-multinic-intro-include.md](../../includes/virtual-network-deploy-multinic-intro-include.md)]

> [!NOTE]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [Resource Manager et classique](../resource-manager-deployment-model.md).  Cet article couvre l’utilisation de modèle de déploiement Resource Manager hello, qui recommandées par Microsoft pour la plupart des déploiements de nouveau au lieu de hello [modèle de déploiement classique](virtual-network-deploy-multinic-classic-ps.md).
> 

[!INCLUDE [virtual-network-deploy-multinic-scenario-include.md](../../includes/virtual-network-deploy-multinic-scenario-include.md)]

étapes suivantes Hello utilisent un groupe de ressources nommé *IaaSStory* pour les serveurs WEB hello et un groupe de ressources nommé *IaaSStory-principal* pour les serveurs de base de données de hello.

## <a name="prerequisites"></a>Composants requis
Avant de pouvoir créer hello des serveurs de base de données, vous devez toocreate hello *IaaSStory* groupe de ressources avec toutes les ressources nécessaires hello pour ce scénario. fin de ces ressources, toocreate hello comme suit :

1. Accédez trop[page de modèle hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Dans la page de modèle hello, toohello à droite de **groupe de ressources Parent**, cliquez sur **déployer tooAzure**.
3. Si nécessaire, modifiez les valeurs de paramètre hello, puis suivez les étapes de hello hello Azure en version préliminaire toodeploy portail hello groupe de ressources.

> [!IMPORTANT]
> Assurez-vous que vos noms de compte de stockage sont uniques. Vous ne pouvez pas avoir des noms de compte de stockage en double dans Azure.
> 

## <a name="understand-hello-deployment-template"></a>Comprendre le modèle de déploiement hello
Avant de déployer les modèles hello fournis dans cette documentation, assurez-vous que vous comprenez ce qu’il fait. Hello suit fournit une bonne vue d’ensemble du modèle de hello :

1. Accédez trop[page de modèle hello](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC).
2. Cliquez sur **azuredeploy.json** fichier de modèle tooopen hello.
3. Hello d’avis *osType* paramètre répertoriée ci-dessous. Ce paramètre est utilisé tooselect le toouse d’image de machine virtuelle pour le serveur de base de données hello, ainsi que plusieurs systèmes d’exploitation les paramètres associés.

    ```json
    "osType": {
      "type": "string",
      "defaultValue": "Windows",
      "allowedValues": [
        "Windows",
        "Ubuntu"
      ],
      "metadata": {
      "description": "Type of OS toouse for VMs: Windows or Ubuntu."
      }
    },
    ```

4. Faites défiler la liste des variables toohello et vérifiez la définition de hello pour hello **dbVMSetting** variables, répertoriés ci-dessous. Il reçoit l’un des éléments de tableau hello contenues dans hello **dbVMSettings** variable. Si vous êtes familiarisé avec la terminologie de développement logiciel, vous pouvez afficher hello **dbVMSettings** variable comme une table de hachage ou un dictionnaire.

    ```json
    "dbVMSetting": "[variables('dbVMSettings')[parameters('osType')]]"
    ```

5. Supposons que vous décidez de toodeploy les machines virtuelles Windows en cours d’exécution SQL dans hello back-end. Puis hello valeur pour **osType** serait *Windows*et hello **dbVMSetting** variable contient l’élément hello répertoriée ci-dessous, qui représente la première valeur de hello Bonjour **dbVMSettings** variable.

    ```json
    "Windows": {
      "vmSize": "Standard_DS3",
      "publisher": "MicrosoftSQLServer",
      "offer": "SQL2014SP1-WS2012R2",
      "sku": "Standard",
      "version": "latest",
      "vmName": "DB",
      "osdisk": "osdiskdb",
      "datadisk": "datadiskdb",
      "nicName": "NICDB",
      "ipAddress": "192.168.2.",
      "extensionDeployment": "",
      "avsetName": "ASDB",
      "remotePort": 3389,
      "dbPort": 1433
    },
    ```

6. Hello d’avis **vmSize** contient la valeur de hello *Standard_DS3*. Utilisez hello de plusieurs cartes réseau autorisent uniquement certaines tailles de machine virtuelle. Vous pouvez vérifier les tailles de machine virtuelle prend en charge plusieurs cartes réseau en lisant hello [tailles de machine virtuelle Windows](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) et [tailles de Linux VM](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) articles.

7. Faites défiler la liste trop**ressources** et avis hello premier élément. Il décrit un compte de stockage. Ce compte de stockage sera utilisés par chaque ordinateur virtuel de la base de données des disques de données utilisé toomaintain hello. Dans ce scénario, chaque machine virtuelle de base de données possède un disque de système d’exploitation stocké dans le stockage standard et deux disques de données stockés dans le stockage SSD (Premium).

    ```json
    {
      "apiVersion": "2015-05-01-preview",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[parameters('prmStorageName')]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "Storage Account - Premium"
      },
      "properties": {
      "accountType": "[parameters('prmStorageType')]"
      }
    },
    ```

8. Faites défiler toohello de ressource suivant, comme indiqué ci-dessous. Cette ressource représente hello que carte réseau utilisée pour l’accès de base de données dans chaque base de données de machine virtuelle. Utilisation de hello avis de hello **copie** fonction de cette ressource. Hello modèle vous permet de toodeploy comme de nombreux ordinateurs virtuels que vous le souhaitez, en fonction de hello **dbCount** paramètre. Par conséquent, vous devez toocreate hello du même montant de cartes réseau pour l’accès de base de données, un pour chaque machine virtuelle.

    ```json
    {
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Network/networkInterfaces",
    "name": "[concat(variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
    "location": "[variables('location')]",
    "tags": {
      "displayName": "NetworkInterfaces - DB DA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "privateIPAllocationMethod": "Static",
            "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(4))]",
            "subnet": {
              "id": "[variables('backEndSubnetRef')]"
            }
          }
         }
       ] 
     }
    },
    ```

9. Faites défiler toohello de ressource suivant, comme indiqué ci-dessous. Cette ressource représente hello que carte réseau utilisée pour la gestion de chaque machine virtuelle de la base de données. Une fois encore, vous devez avoir une carte réseau pour chaque machine virtuelle de base de données. Hello d’avis **sécurité réseau** élément, liaison d’un groupe de sécurité réseau qui permet l’accès tooRDP/SSH toothis carte réseau uniquement.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[concat(variables('dbVMSetting').nicName, '-RA-',copyindex(1))]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "NetworkInterfaces - DB RA"
    },
    "copy": {
      "name": "dbniccount",
      "count": "[parameters('dbCount')]"
    },
    "properties": {
      "ipConfigurations": [
        {
          "name": "ipconfig1",
          "properties": {
            "networkSecurityGroup": {
             "id": "[resourceId('Microsoft.Network/networkSecurityGroups', parameters('remoteAccessNSGName'))]"
             },
             "privateIPAllocationMethod": "Static",
             "privateIPAddress": "[concat(variables('dbVMSetting').ipAddress,copyindex(54))]",
             "subnet": {
              "id": "[variables('backEndSubnetRef')]"
             }
           }
          }
        ]
      }
    },
```

10. Faites défiler toohello de ressource suivant, comme indiqué ci-dessous. Cette ressource représente un toobe de jeu de disponibilité partagé par tous les ordinateurs virtuels de base de données. De cette façon, vous assurer qu’il y aura toujours une machine virtuelle Bonjour configuré pour s’exécuter lors de la maintenance.

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/availabilitySets",
      "name": "[variables('dbVMSetting').avsetName]",
      "location": "[variables('location')]",
      "tags": {
        "displayName": "AvailabilitySet - DB"
      }
    },
    ```

11. Faites défiler les ressources suivant toohello. Cette ressource représente la base de données de hello machines virtuelles, comme dans hello tout d’abord quelques lignes répertoriées ci-dessous. Utilisation de hello avis de hello **copie** fonctionne à nouveau, de s’assurer que plusieurs ordinateurs virtuels sont créés en fonction hello **dbCount** paramètre. Notez également hello **dependsOn** collection. Il répertorie les deux cartes réseau qui est nécessaire toobe créé avant hello qu'ordinateur virtuel est déployé, ainsi que le groupe à haute disponibilité hello et compte de stockage hello.

    ```json
    "apiVersion": "2015-06-15",
    "type": "Microsoft.Compute/virtualMachines",
    "name": "[concat(variables('dbVMSetting').vmName,copyindex(1))]",
    "location": "[variables('location')]",
    "dependsOn": [
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-DA-', copyindex(1))]",
      "[concat('Microsoft.Network/networkInterfaces/', variables('dbVMSetting').nicName,'-RA-', copyindex(1))]",
      "[concat('Microsoft.Compute/availabilitySets/', variables('dbVMSetting').avsetName)]",
      "[concat('Microsoft.Storage/storageAccounts/', parameters('prmStorageName'))]"
    ],
    "tags": {
      "displayName": "VMs - DB"
    },
    "copy": {
      "name": "dbvmcount",
      "count": "[parameters('dbCount')]"
    },
    ```

12. Faites défiler toohello de ressource de machine virtuelle hello **VM** élément, comme indiqué ci-dessous. Notez que deux cartes réseau sont référencées pour chaque machine virtuelle. Lorsque vous créez plusieurs cartes réseau pour un ordinateur virtuel, vous devez définir hello **principal** propriété de l’une des cartes réseau de hello trop*true*, et hello reste trop*false*.

    ```json
    "networkProfile": {
      "networkInterfaces": [
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-DA-',copyindex(1)))]",
          "properties": { "primary": true }
        },
        {
          "id": "[resourceId('Microsoft.Network/networkInterfaces', concat(variables('dbVMSetting').nicName,'-RA-',copyindex(1)))]",
          "properties": { "primary": false }
        }
      ]
    }
    ```

## <a name="deploy-hello-arm-template-by-using-click-toodeploy"></a>Déployer le modèle de hello ARM à l’aide de cliquez sur toodeploy

> [!IMPORTANT]
> Assurez-vous que vous suivez hello [préalables](#Pre-requisites) étapes avant de suivre les instructions hello ci-dessous.
> 

Hello exemple de modèle disponible dans le référentiel de public hello utilise un fichier de paramètre contenant le scénario hello hello par défaut les valeurs utilisées toogenerate décrit ci-dessus. toodeploy ce modèle à l’aide de cliquez toodeploy, suivez [ce lien](https://github.com/Azure/azure-quickstart-templates/tree/master/IaaS-Story/11-MultiNIC), toohello à droite de **groupe de ressources du serveur principal (consultez la documentation)** cliquez sur **déployer tooAzure**, remplacer Hello des valeurs de paramètre par défaut si nécessaire et suivez les instructions de hello dans le portail de hello.

Hello figure ci-dessous contenu hello du nouveau groupe de ressources hello, après le déploiement.

![Groupe de ressources du back end](./media/virtual-network-deploy-multinic-arm-template/Figure2.png)

## <a name="deploy-hello-template-by-using-powershell"></a>Déployer le modèle de hello à l’aide de PowerShell
modèle de hello toodeploy vous avez téléchargé à l’aide de PowerShell, installer et configurer des PowerShell en effectuant les étapes hello Bonjour [installer et configurer PowerShell](/powershell/azure/overview) de l’article, puis terminez hello comme suit :

Exécutez hello  **`New-AzureRmResourceGroup`**  toocreate d’applet de commande un groupe de ressources à l’aide de hello modèle.

```powershell
New-AzureRmResourceGroup -Name IaaSStory-Backend -Location uswest `
TemplateFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json' `
-TemplateParameterFile 'https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json'
```

Sortie attendue :

    ResourceGroupName : IaaSStory-Backend
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    Permissions       :
                        Actions  NotActions
                        =======  ==========
                        *
        Resources         :
                        Name                 Type                                 Location
                        ===================  ===================================  ========
                        ASDB                 Microsoft.Compute/availabilitySets   westus  
                        DB1                  Microsoft.Compute/virtualMachines    westus  
                        DB2                  Microsoft.Compute/virtualMachines    westus  
                        NICDB-DA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-DA-2           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-1           Microsoft.Network/networkInterfaces  westus  
                        NICDB-RA-2           Microsoft.Network/networkInterfaces  westus  
                        wtestvnetstorageprm  Microsoft.Storage/storageAccounts    westus  
    ResourceId        : /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend

## <a name="deploy-hello-template-by-using-hello-azure-cli"></a>Déployer le modèle de hello à l’aide de hello CLI d’Azure
modèle de hello toodeploy à l’aide de hello CLI d’Azure, suivez les étapes de hello ci-dessous.

1. Si vous n’avez jamais utilisé CLI d’Azure, consultez [installer et configurer hello CLI d’Azure](../cli-install-nodejs.md) et suivez les instructions de hello point toohello où vous sélectionnez votre compte Azure et votre abonnement.
2. Exécutez hello  **`azure config mode`**  mode Manager tooResource commande tooswitch, comme indiqué ci-dessous.

    ```azurecli
    azure config mode arm
    ```

    Hello attendu sortie suivante :

        info:    New mode is arm

3. Ouvrez hello [fichier de paramètres](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.parameters.json), sélectionnez son contenu et enregistrez-le tooa fichier sur votre ordinateur. Pour cet exemple, nous avons enregistré des fichiers de paramètres hello trop*parameters.json*.
4. Exécutez hello  **`azure group deployment create`**  applet de commande toodeploy hello nouveau réseau virtuel à l’aide des paramètres et modèle de hello fichiers téléchargés et de modifier les propriétés. liste de Hello affiché après la sortie de hello explique paramètres hello utilisés.

    ```azurecli
    azure group create -n IaaSStory-Backend -l westus --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/IaaS-Story/11-MultiNIC/azuredeploy.json -e parameters.json
    ```

    Sortie attendue :
   
        info:    Executing command group create
        + Getting resource group IaaSStory-Backend
        + Creating resource group IaaSStory-Backend
        info:    Created resource group IaaSStory-Backend
        + Initializing template configurations and parameters
        + Creating a deployment
        info:    Created template deployment "azuredeploy"
        data:    Id:                  /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/IaaSStory-Backend
        data:    Name:                IaaSStory-Backend
        data:    Location:            westus
        data:    Provisioning State:  Succeeded
        data:    Tags: null
        data:
        info:    group create command OK

