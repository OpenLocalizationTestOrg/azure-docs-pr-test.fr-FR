---
title: "aaaNetworking pour les jeux de mise à l’échelle de machine virtuelle Azure | Documents Microsoft"
description: "Propriétés de mise en réseau de configuration pour des groupes de machines virtuelles identiques Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: guybo
ms.openlocfilehash: ef3f0cfe648d2195c051a73987e654f0e15d13bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="networking-for-azure-virtual-machine-scale-sets"></a>Mise en réseau pour des groupes de machines virtuelles identiques Azure

Lorsque vous déployez une échelle de machine virtuelle Azure définie via le portail de hello, certaines propriétés de réseau sont par défaut, par exemple un équilibrage de charge Azure avec des règles de trafic entrant NAT. Cet article décrit comment toouse certaines hello des fonctionnalités réseau que vous pouvez configurer avec une échelle plus avancées définit.

Vous pouvez configurer toutes les fonctionnalités de hello abordées dans cet article à l’aide de modèles Azure Resource Manager. Des exemples d’interfaces de ligne de commande Azure et Powershell sont également inclus pour les fonctionnalités sélectionnées. Utilisez CLI 2.10 et PowerShell 4.2.0 ou version ultérieure.

## <a name="accelerated-networking"></a>Mise en réseau accélérée
Azure [Accelerated réseau](../virtual-network/virtual-network-create-vm-accelerated-networking.md) améliore les performances du réseau en e/s de racine unique (SR-IOV) de la virtualisation tooa virtual machine. toouse accelerated mise en réseau avec des jeux de mise à l’échelle, définissez enableAcceleratedNetworking trop**true** dans les paramètres des configurations de votre jeu de mise à l’échelle. Par exemple :
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
      "name": "niconfig1",
      "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
          ...
        ]
      }
    }
   ]
}
```

## <a name="create-a-scale-set-that-references-an-existing-azure-load-balancer"></a>Créer un groupe identique qui fait référence à un équilibrage de charge Azure existant
Lorsqu’un ensemble d’échelle est créé à l’aide de hello portail Azure, un nouvel équilibrage de charge est créé pour la plupart des options de configuration. Si vous créez un ensemble d’échelle, qui doit tooreference un équilibrage de charge existante, procéder à l’aide de CLI. Hello, exemple de script suivant crée un équilibreur de charge, puis crée un ensemble d’échelle, ce qui fait référence :
```bash
az network lb create -g lbtest -n mylb --vnet-name myvnet --subnet mysubnet --public-ip-address-allocation Static --backend-pool-name mybackendpool

az vmss create -g lbtest -n myvmss --image Canonical:UbuntuServer:16.04-LTS:latest --admin-username negat --ssh-key-value /home/myuser/.ssh/id_rsa.pub --upgrade-policy-mode Automatic --instance-count 3 --vnet-name myvnet --subnet mysubnet --lb mylb --backend-pool-name mybackendpool

```

## <a name="configurable-dns-settings"></a>Paramètres DNS configurables
Par défaut, les groupes identiques de prennent les paramètres DNS spécifiques hello hello réseau virtuel et sous-réseau qu’ils ont été créés dans. Toutefois, vous pouvez configurer les paramètres DNS de hello pour une échelle définie directement.
~
### <a name="creating-a-scale-set-with-configurable-dns-servers"></a>Création d’un groupe identique avec les serveurs DNS configurables
toocreate une échelle définie avec une configuration DNS personnalisée à l’aide de la version 2.0 CLI, ajoutez hello **serveurs dns--** argument toohello **mise créer** commande, suivi par un espace séparées par des adresses ip de serveur. Par exemple :
```bash
--dns-servers 10.0.0.6 10.0.0.5
```
tooconfigure des serveurs DNS personnalisés dans un modèle Azure, ajouter la section des configurations du jeu d’une échelle de toohello de propriété de paramètres DNS. Par exemple :
```json
"dnsSettings":{
    "dnsServers":["10.0.0.6", "10.0.0.5"]
}
```

### <a name="creating-a-scale-set-with-configurable-virtual-machine-domain-names"></a>Création d’un groupe identique avec des noms de domaine de machines virtuelles configurables
toocreate une échelle définie avec un nom DNS personnalisé pour les ordinateurs virtuels à l’aide de la version 2.0 CLI, ajoutez hello **vm--nom de domaine** argument toohello **mise créer** commande, suivi d’une chaîne représentant le nom de domaine hello.

nom de domaine tooset hello dans un modèle Azure, ajoutez un **dnsSettings** ensemble d’échelle de propriété toohello **configurations** section. Par exemple :

```json
"networkProfile": {
  "networkInterfaceConfigurations": [
    {
    "name": "nic1",
    "properties": {
      "primary": "true",
      "ipConfigurations": [
      {
        "name": "ip1",
        "properties": {
          "subnet": {
            "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
          },
          "publicIPAddressconfiguration": {
            "name": "publicip",
            "properties": {
            "idleTimeoutInMinutes": 10,
              "dnsSettings": {
                "domainNameLabel": "[parameters('vmssDnsName')]"
              }
            }
          }
        }
      }
    ]
    }
}
```

sortie Hello, d’un nom dns de chaque machine virtuelle serait Bonjour suivant du formulaire : 
```
<vm><vmindex>.<specifiedVmssDomainNameLabel>
```

## <a name="public-ipv4-per-virtual-machine"></a>IPv4 publique par machine virtuelle
En règle générale, les machines virtuelles des groupes identiques Azure ne nécessitent pas leurs propres adresses IP publiques. La plupart des scénarios, il est plus économique et plus sûre tooassociate un public IP adresse tooa charge équilibrage tooan individuel ordinateur virtuel ou (également appelé jumpbox), qui achemine ensuite entrant connexions tooscale ensemble les ordinateurs virtuels en fonction des besoins (par exemple, via règles NAT entrantes).

Toutefois, certains scénarios nécessitent ensemble d’échelle de machines virtuelles toohave leur propre adresse IP publique adresses. Un exemple de jeu, où une console doit toomake une connexion directe tooa cloud machine, qui effectue le traitement du jeu physique. Un autre exemple est où les ordinateurs virtuels doivent toomake connexions externes tooone autre régions dans une base de données distribuée.

### <a name="creating-a-scale-set-with-public-ip-per-virtual-machine"></a>Création d’un groupe identique avec IP public par machine virtuelle
toocreate un ensemble d’échelle qui affecte un ordinateur virtuel des tooeach d’adresse publique IP CLI 2.0, ajouter hello **--public-ip-par-vm** paramètre toohello **mise créer** commande. 

toocreate une échelle définie à l’aide d’un modèle Azure, vérifiez que hello API version de hello Microsoft.Compute/virtualMachineScaleSets ressource est au moins **2017-03-30**et ajoutez un **publicIpAddressConfiguration**Toohello l’échelle de la propriété JSON définie la section de configurations IP. Par exemple :

```json
"publicIpAddressConfiguration": {
    "name": "pub1",
    "properties": {
      "idleTimeoutInMinutes": 15
    }
}
```
Exemple de modèle : [201-vmss-public-ip-linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-public-ip-linux)

### <a name="querying-hello-public-ip-addresses-of-hello-virtual-machines-in-a-scale-set"></a>Adresse IP publique hello l’interrogation du jeu d’ordinateurs virtuels hello dans une échelle des adresses
des adresses IP publiques toolist hello affecté tooscale virtuels ensemble à l’aide de la version 2.0 CLI, utilisez hello **az mise liste-instance-public-IP** commande.

mise à l’échelle toolist définie les adresses IP publiques à l’aide de PowerShell, utilisez les hello _Get-AzureRmPublicIpAddress_ commande. Par exemple :
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -VirtualMachineScaleSetName myvmss
```

Vous pouvez également des adresses IP publiques requête hello en référençant directement les id de ressource de hello de configuration d’adresse IP publique hello. Par exemple :
```PowerShell
PS C:\> Get-AzureRmPublicIpAddress -ResourceGroupName myrg -Name myvmsspip
```

attribuer des adresses IP publiques de tooquery hello tooscale virtuels ensemble à l’aide de hello [Explorateur de ressources Azure](https://resources.azure.com), ou hello API REST Azure avec la version **2017-03-30** ou une version ultérieure.

tooview des adresses IP publiques pour une échelle définie à l’aide de l’Explorateur de ressources, de hello examiner hello **publicipaddresses** section sous votre ensemble d’échelle. Par exemple : https://resources.azure.com/subscriptions/_your_sub_id_/resourceGroups/_your_rg_/providers/Microsoft.Compute/virtualMachineScaleSets/_your_vmss_/publicipaddresses

```
GET https://management.azure.com/subscriptions/{your sub ID}/resourceGroups/{RG name}/providers/Microsoft.Compute/virtualMachineScaleSets/{scale set name}/publicipaddresses?api-version=2017-03-30
```

Exemple de sortie :
```json
{
  "value": [
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/pipvmss/virtualMachines/0/networkInterfaces/pipvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"a64060d5-4dea-4379-a11d-b23cd49a3c8d\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "ee8cb20f-af8e-4cd6-892f-441ae2bf701f",
        "ipAddress": "13.84.190.11",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/0/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    },
    {
      "name": "pub1",
      "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig/publicIPAddresses/pub1",
      "etag": "W/\"5f6ff30c-a24c-4818-883c-61ebd5f9eee8\"",
      "properties": {
        "provisioningState": "Succeeded",
        "resourceGuid": "036ce266-403f-41bd-8578-d446d7397c2f",
        "ipAddress": "13.84.159.176",
        "publicIPAddressVersion": "IPv4",
        "publicIPAllocationMethod": "Dynamic",
        "idleTimeoutInMinutes": 15,
        "ipConfiguration": {
          "id": "/subscriptions/your-subscription-id/resourceGroups/your-rg/providers/Microsoft.Compute/virtualMachineScaleSets/yourvmss/virtualMachines/3/networkInterfaces/yourvmssnic/ipConfigurations/yourvmssipconfig"
        }
      }
    }
```

## <a name="multiple-ip-addresses-per-nic"></a>Plusieurs adresses IP par carte réseau
Chaque carte réseau attachée tooa que machine virtuelle dans un ensemble d’échelle peut avoir une ou plusieurs configurations IP associées. Une adresse IP privée est affectée à chaque configuration. Une ressource d’adresse IP publique peut également être associée à chaque configuration. toounderstand le nombre d’adresses IP peut être affectée tooa carte réseau, et le nombre d’adresses IP publique que vous pouvez utiliser dans un abonnement Azure, consultez trop[limite Azure](../azure-subscription-service-limits.md?toc=%2fazure%2fvirtual-network%2ftoc.json#azure-resource-manager-virtual-networking-limits).

## <a name="multiple-nics-per-virtual-machine"></a>Plusieurs cartes réseau par machine virtuelle
Vous pouvez avoir des cartes réseau de too8 par machine virtuelle, en fonction de la taille de l’ordinateur. Hello de nombre maximal de cartes réseau par machine est disponible dans hello [article de taille de machine virtuelle](../virtual-machines/windows/sizes.md). Hello exemple suivant est qu'une échelle de définie le profil réseau affichant plusieurs entrées de la carte réseau et plusieurs adresses IP publiques par machine virtuelle :
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
        "name": "nic1",
        "properties": {
            "primary": "true",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        },
        {
        "name": "nic2",
        "properties": {
            "primary": "false",
            "ipConfigurations": [
            {
                "name": "ip1",
                "properties": {
                "subnet": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                },
                "publicipaddressconfiguration": {
                    "name": "pub1",
                    "properties": {
                    "idleTimeoutInMinutes": 15
                    }
                },
                "loadBalancerInboundNatPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                    }
                ],
                "loadBalancerBackendAddressPools": [
                    {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                    }
                ]
                }
            }
            ]
        }
        }
    ]
}
```

## <a name="nsg-per-scale-set"></a>Groupes de sécurité réseau par groupe identique
Groupes de sécurité réseau peuvent être appliqués directement tooa un ensemble d’échelle, en ajoutant une section de configuration de référence toohello network interface de montée en puissance hello définie des propriétés de la machine virtuelle.

Par exemple : 
```
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations sur les réseaux virtuels Azure, consultez trop[cette documentation](../virtual-network/virtual-networks-overview.md).
