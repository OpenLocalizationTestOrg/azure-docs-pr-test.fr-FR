---
title: "aaaAutoscale groupes de mise à l’échelle de machines virtuelles Linux | Documents Microsoft"
description: "Mettre à l’échelle automatiquement un jeu de mise à l’échelle de machine virtuelle Linux avec l’interface de ligne de commande Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a>Mise à l’échelle automatique de machines Linux dans un jeu de mise à l’échelle de machine virtuelle
Machines virtuelles identiques facilitent vous toodeploy et gérer des machines virtuelles identiques en tant qu’ensemble. Les groupes à échelle identique fournissent une couche de calcul hautement évolutive et personnalisable pour les applications « hyperscale », et prennent en charge les images de plateforme Windows, les images de plateforme Linux, des images personnalisées et les extensions. toolearn, voir [vue d’ensemble des jeux de Machine virtuelle mise à l’échelle](virtual-machine-scale-sets-overview.md).

Ce didacticiel vous montre comment définie des toocreate une échelle d’ordinateurs virtuels Linux à l’aide de la version la plus récente d’Ubuntu Linux hello. didacticiel de Hello vous montre également comment tooautomatically échelle hello machines hello haute. Vous créez la montée en puissance hello définir et configurer la mise à l’échelle en créant un modèle Azure Resource Manager et de déploiement à l’aide de CLI d’Azure. Pour en savoir plus sur les modèles, consultez [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md). toolearn en savoir plus sur la mise à l’échelle automatique de jeux de mise à l’échelle, consultez [mise à l’échelle automatique et mise à l’échelle de Machine virtuelle définit](virtual-machine-scale-sets-autoscale-overview.md).

Dans ce didacticiel, vous déployez suivant de hello extensions et ressources :

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets
* Microsoft.Insights.VMDiagnosticsSettings
* Microsoft.Insights/autoscaleSettings

Pour plus d’informations sur les ressources Azure Manager, consultez [Déploiement Azure Resource Manager et déploiement classique](../azure-resource-manager/resource-manager-deployment-model.md).

Avant de commencer les étapes hello dans ce didacticiel, [installer hello CLI d’Azure](../cli-install-nodejs.md).

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a>Étape 1 : créer un groupe de ressources et un compte de stockage

1. **Connectez-vous à tooMicrosoft Azure**  
Dans l’interface de ligne de commande (interpréteur de commandes, Terminal Server, invite), mode de commutation tooResource Manager, puis [connectez-vous avec votre id Professionnel ou scolaire](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Suivez les invites hello pour une tooyour d’expérience de connexion interactive compte Azure.

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > Si vous avez un travail ou scolaire ID et vous ne pas disposer de l’authentification à deux facteurs est activée, utilisez `azure login -u` avec toolog d’ID hello dans sans une session interactive. Si vous ne disposez pas d’un ID professionnel ou scolaire, vous pouvez [créer un ID professionnel ou scolaire à partir de votre compte Microsoft personnel](../active-directory/active-directory-users-create-azure-portal.md).
    
2. **Créer un groupe de ressources**  
Toutes les ressources doivent être le groupe de ressources tooa déployé. Pour ce didacticiel, nommez le groupe de ressources hello **vmsstest1**.
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. **Déployer un compte de stockage dans le nouveau groupe de ressources hello**  
Ce compte de stockage est où se trouve le modèle de hello. Créez un compte de stockage nommé **vmsstestsa**.
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a>Étape 2 : Créer le modèle de hello
Un modèle Azure Resource Manager rend possible pour vous toodeploy et gérer des ressources Azure ensemble à l’aide d’une description JSON des ressources de hello et des paramètres de déploiement associés.

1. Dans votre éditeur favori, créer le fichier hello VMSSTemplate.json et ajouter hello initiales JSON structure toosupport hello du modèle.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Paramètres ne sont pas toujours nécessaires, mais ils fournissent un moyen tooinput valeurs lorsque le modèle de hello est déployé. Ajouter ces paramètres sous l’élément parent de hello paramètres que vous avez ajouté le modèle de toohello.

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * Un nom pour la machine virtuelle distincte hello constituant des machines de hello tooaccess utilisé dans l’ensemble d’échelle hello.
   * Nom de compte de stockage hello où se trouve le modèle de hello.
   * nombre de Hello d’instances de machines virtuelles tooinitially créer dans un ensemble d’échelle hello.
   * Un nom et un mot de passe du compte d’administrateur hello sur des machines virtuelles de hello.
   * Un préfixe de nom pour les ressources hello qui sont créés à l’échelle de hello toosupport définie.

3. Variables peuvent être utilisées dans un valeurs toospecify de modèle qui changent fréquemment ou les valeurs qui doivent toobe créées à partir d’une combinaison de valeurs de paramètre. Ajoutez ces variables sous l’élément parent de hello variables que vous avez ajouté le modèle de toohello.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * Noms DNS qui sont utilisés par les interfaces réseau hello.
   * les noms d’adresses IP Hello et préfixes pour le réseau virtuel de hello et sous-réseaux.
   * Hello noms et les identificateurs de réseau virtuel de hello, équilibreur de charge et les interfaces réseau.
   * Noms de compte de stockage pour les comptes de hello associés avec des machines hello dans un ensemble d’échelle hello.
   * Paramètres de hello extension de Diagnostics qui est installée sur les ordinateurs virtuels de hello. Pour plus d’informations sur l’extension des Diagnostics de hello, consultez [créer une machine virtuelle Windows avec l’analyse et de diagnostics à l’aide du modèle de gestionnaire de ressources Azure](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Ajouter une ressource de compte de stockage hello sous l’élément parent de hello ressources que vous avez ajouté le modèle de toohello. Ce modèle utilise un Bonjour toocreate de boucle recommandé cinq comptes de stockage où sont stockées les disques du système d’exploitation hello et les données de diagnostic. Cet ensemble de comptes peut prendre en charge les machines virtuelles de too100 dans un ensemble d’échelle, qui est la valeur maximale actuelle de hello. Chaque compte de stockage est nommé avec un indicateur de lettre qui a été défini dans les variables hello combinés avec le suffixe hello que vous fournissez dans les paramètres de hello pour le modèle de hello.
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. Ajouter une ressource de réseau virtuel hello. Pour plus d’informations, consultez [Fournisseurs de ressources réseau](../virtual-network/resource-groups-networking.md).

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Ajoutez hello publiques ressources d’adresse IP qui sont utilisés par hello équilibreur de charge et interface réseau.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Ajouter une ressource d’équilibrage de charge hello qui est utilisé par un ensemble d’échelle hello. Pour plus d’informations, consultez [Prise en charge d’un équilibreur de charge par Azure Resource Manager](../load-balancer/load-balancer-arm.md)

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. Ajouter la ressource d’interface réseau hello qui est utilisé par la machine virtuelle distincte de hello. Étant donné que les ordinateurs dans un ensemble d’échelle ne sont pas accessibles via une adresse IP publique, un ordinateur virtuel distinct est créé dans hello même virtuel réseau tooremotely accès hello machines.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Ajouter la machine virtuelle distincte de hello Bonjour même réseau que l’ensemble d’échelle hello.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
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
        }
      }
    },
    ```

10. Ajouter l’ensemble d’échelle de machine virtuelle hello de ressource et spécifiez l’extension diagnostics hello qui est installée sur tous les ordinateurs virtuels dans un ensemble d’échelle hello. La plupart des paramètres hello pour cette ressource sont similaires avec la ressource d’ordinateur virtuel hello. Hello principales différences sont les élément capacité hello qui spécifie le nombre de hello d’ordinateurs virtuels dans un ensemble d’échelle hello et upgradePolicy qui spécifie comment les mises à jour sont effectuées toovirtual machines. Hello ensemble d’échelle n’est pas créé tant que tous les comptes de stockage hello sont créés comme spécifié avec l’élément dependsOn de hello.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Ajouter une ressource autoscaleSettings hello qui définit comment l’ensemble d’échelle hello s’ajuste en fonction de l’utilisation du processeur sur les ordinateurs hello dans le jeu de hello.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    Pour ce didacticiel, les valeurs suivantes sont importantes :
    
    * **metricName**  
    Cette valeur est hello identique au compteur de performance hello que nous avons défini dans la variable de wadperfcounter hello. À l’aide de cette variable, hello extension Diagnostics collecte hello **Processor\PercentProcessorTime** compteur.
    
    * **metricResourceUri**  
    Cette valeur est l’identificateur de ressource de hello de hello machines virtuelles identiques.
    
    * **timeGrain**  
    Cette valeur est la granularité hello des métriques de hello sont collectés. Dans ce modèle, il a la valeur tooone minute.
    
    * **statistic**  
    Cette valeur détermine comment les métriques de hello sont hello tooaccommodate combinée automatique d’action de mise à l’échelle. Hello les valeurs possibles sont : moyenne, Min, Max. Dans ce modèle, hello total utilisation moyenne du processeur d’ordinateurs virtuels hello est collectée.

    * **timeWindow**  
    Cette valeur est la plage de hello de temps dans laquelle les données d’instance sont collectées. Elle doit être comprise entre 5 minutes et 12 heures.
    
    * **timeAggregation**  
    sa valeur détermine l’association de données hello collectées au fil du temps. valeur par défaut de Hello est moyenne. Hello les valeurs possibles sont : moyenne, Minimum, Maximum, dernier, Total, le nombre.
    
    * **operator**  
    Cette valeur est un opérateur hello toocompare utilisé hello métrique données et hello du seuil. Hello les valeurs possibles sont : Equals, NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.
    
    * **threshold**  
    Cette valeur déclenche l’action de mise à l’échelle de hello. Dans ce modèle, les ordinateurs sont ajoutés échelle toohello définie lors de l’utilisation moyenne du processeur hello entre les ordinateurs dans le jeu de hello est supérieure à 50 %.
    
    * **direction**  
    Cette valeur détermine l’action hello qui est effectuée lorsque la valeur de seuil hello est atteint. les valeurs possibles de Hello sont augmentent ou diminuent. Dans ce modèle, hello nombre d’ordinateurs virtuels dans un ensemble d’échelle hello est augmenté si le seuil de hello est supérieure à 50 % dans la fenêtre de temps hello défini.

    * **type**  
    Cette valeur est de type hello d’action qui doit se produire et doit avoir la valeur tooChangeCount.
    
    * **value**  
    Cette valeur est le nombre de hello d’ordinateurs virtuels qui sont ajoutés ou supprimés à partir d’un ensemble d’échelle hello. Cette valeur doit être définie sur 1 ou supérieur. Hello par défaut est 1. Dans ce modèle, nombre de hello d’ordinateurs dans l’échelle de hello jeu augmente de 1 lorsque hello seuil est atteint.

    * **cooldown**  
    Cette valeur est hello toowait de temps depuis la dernière action de mise à l’échelle hello avant l’action suivante de hello se produit. Elle doit être comprise entre une minute et une semaine.

12. Enregistrez le fichier de modèle hello.    

## <a name="step-3-upload-hello-template-toostorage"></a>Étape 3 : Téléchargez hello modèle toostorage
modèle de Hello peut être téléchargé en tant que vous connaissez le nom de hello et une clé primaire hello du compte de stockage que vous avez créé à l’étape 1.

1. Dans l’interface de ligne de commande (interpréteur de commandes, Terminal Server, invite), exécutez ces commandes variables d’environnement tooset hello nécessaire tooaccess hello compte de stockage :

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    Vous pouvez obtenir la clé de hello en cliquant sur icône de clé hello lors de l’affichage des ressources de compte de stockage hello Bonjour portail Azure. Quand vous utilisez une invite de commandes Windows, tapez **set** à la place d’export.

2. Créer un conteneur hello pour le stockage hello modèle.
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. Télécharger un nouveau conteneur hello modèle fichier toohello.
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a>Étape 4 : Déployer le modèle de hello
Maintenant que vous avez créé le modèle de hello, vous pouvez commencer à déployer des ressources de hello. Utilisez ce processus de hello toostart commande :

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

Lorsque vous appuyez sur, entrez, vous sont des valeurs de tooprovide demandées pour les variables hello que vous affectés. Remplacez les valeurs suivantes :

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

Il doit prendre environ 15 minutes pour tous les toosuccessfully de ressources hello être déployé.

> [!NOTE]
> Vous pouvez également utiliser les ressources de hello du portail hello capacité toodeploy. Utilisez ce lien : https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>


## <a name="step-5-monitor-resources"></a>Étape 5 : analyser les ressources
Vous pouvez obtenir des informations sur les jeux de mise à l’échelle de machine virtuelle à l’aide des méthodes suivantes :

* Hello portail Azure, vous pouvez obtenir actuellement une quantité limitée d’informations à l’aide du portail de hello.

* Hello [Explorateur de ressources Azure](https://resources.azure.com/) -cet outil est hello meilleur pour Explorer l’état actuel de hello de votre ensemble d’échelle. Suivez ce chemin d’accès, et vous devez voir vue d’instance hello de montée en puissance hello définie que vous avez créé :
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* CLI Azure - Utilisez cette tooget commande certaines informations :

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* Se connecter toohello jumpbox virtuels comme vous le feriez pour n’importe quel autre ordinateur et vous pouvez ensuite accéder à distance virtuels hello dans toomonitor hello échelle ensemble des processus individuels.

> [!NOTE]
> Vous trouverez une API REST complète permettant d’obtenir des informations sur les groupes à échelle identique dans [Groupes de machines virtuelles à échelle identique](https://msdn.microsoft.com/library/mt589023.aspx)

## <a name="step-6-remove-hello-resources"></a>Étape 6 : Supprimer des ressources de hello
Vous êtes facturé pour les ressources utilisées dans Azure, il est toujours ressource toodelete bonnes pratiques qui n’est plus nécessaires. Vous n’avez pas besoin toodelete chaque ressource séparément à partir d’un groupe de ressources. Vous pouvez supprimer le groupe de ressources hello et toutes ses ressources sont automatiquement supprimés.

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a>Étapes suivantes
* Découvrez des exemples de fonctionnalités de surveillance Azure Monitor dans les [exemples de démarrage rapide de l’interface CLI multiplateforme d’Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md)
* En savoir plus sur les fonctionnalités de notification de [utiliser échelle actions toosend par courrier électronique et webhook des notifications d’alerte dans le moniteur de Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Découvrez comment trop[toosend par courrier électronique et webhook des notifications d’alerte de les journaux d’audit d’utilisation dans le moniteur de Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)
* Extraire hello [application de démonstration de mise à l’échelle sur Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modèle qui définit un Bonjour de tooexercise Python/bottle application automatique de mise à l’échelle de la fonctionnalité de mise à l’échelle de Machine virtuelle définit.

