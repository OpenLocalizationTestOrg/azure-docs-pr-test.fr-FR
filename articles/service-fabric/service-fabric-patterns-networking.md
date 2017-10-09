---
title: "modèles d’aaaNetworking pour Azure Service Fabric | Documents Microsoft"
description: "Décrit les modèles de mise en réseau courants pour l’infrastructure de Service et comment toocreate un cluster à l’aide des fonctionnalités de mise en réseau Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/16/2017
ms.author: ryanwi
ms.openlocfilehash: 5973e3f9917076c6a36e71443ec256e0f414ff87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-networking-patterns"></a>Modèles de mise en réseau de Service Fabric
Vous pouvez intégrer votre cluster Azure Service Fabric avec d’autres fonctionnalités de mise en réseau Azure. Dans cet article, nous vous indiquons comment toocreate clusters que hello utilisation suivant de fonctionnalités :

- [Réseau virtuel ou sous-réseau existant](#existingvnet)
- [Adresse IP publique statique](#staticpublicip)
- [Équilibreur de charge interne uniquement](#internallb)
- [Équilibreur de charge interne et externe](#internalexternallb)

Service Fabric s’exécute dans un groupe de machines virtuelles identiques standard. Toutes les fonctionnalités que vous pouvez utiliser dans un groupe de machines virtuelles identiques sont utilisables avec un cluster Service Fabric. sections de mise en réseau Hello de modèles Azure Resource Manager de hello pour les machines virtuelles identiques et l’infrastructure de Service sont identiques. Après avoir déployé tooan réseau virtuel existant, il est facile tooincorporate autres fonctionnalités, comme Azure ExpressRoute, passerelle VPN à Azure, un groupe de sécurité réseau et réseau virtuel d’homologation de mise en réseau.

Service Fabric se distingue d’autres fonctionnalités de mise en réseau sur un aspect. Hello [portail Azure](https://portal.azure.com) en interne utilise hello Service Fabric ressource fournisseur toocall tooa cluster tooget plus d’informations sur les nœuds et les applications. fournisseur de ressources de Service Fabric Hello requiert port de passerelle accès entrant accessible publiquement toohello HTTP (port 19080, par défaut) sur le point de terminaison de gestion hello. [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) utilise hello toomanage de point de terminaison de gestion de votre cluster. fournisseur de ressources de Service Fabric Hello utilise également ces informations de tooquery de port sur votre cluster, toodisplay Bonjour portail Azure. 

Si le port 19080 n’est pas accessible à partir du fournisseur de ressources de Service Fabric hello, un message comme *nœuds introuvable* apparaît dans le portail de hello, et votre liste de nœud et l’application est vide. Si vous souhaitez toosee votre cluster Bonjour portail Azure, votre équilibreur de charge doit exposer une adresse IP publique, et votre groupe de sécurité réseau doit autoriser le trafic entrant du port 19080. Si votre programme d’installation ne remplit pas ces exigences, hello portail Azure n’affiche pas d’état hello de votre cluster.

## <a name="templates"></a>Modèles

Tous les modèles Service Fabric se trouvent dans [un même fichier de téléchargement](https://msdnshared.blob.core.windows.net/media/2016/10/SF_Networking_Templates.zip). Vous devez être en mesure de toodeploy modèles hello en tant que-est à l’aide de hello suivant de commandes PowerShell. Si vous déployez hello modèle de réseau virtuel Azure existant ou hello modèle IP publique statique, lisez d’abord hello [Initial setup](#initialsetup) section de cet article.

<a id="initialsetup"></a>
## <a name="initial-setup"></a>Configuration initiale

### <a name="existing-virtual-network"></a>Réseau virtuel existant

Bonjour l’exemple suivant, nous allons commencer avec un réseau virtuel existant nommé ExistingRG-réseau virtuel, Bonjour **ExistingRG** groupe de ressources. sous-réseau de Hello est nommée par défaut. Ces ressources par défaut sont créés lorsque vous utilisez hello toocreate portail Azure une machine virtuelle standard (VM). Vous pouvez créer des réseaux hello et sous-réseau sans créer de hello machine virtuelle, mais hello principal objectif d’ajout d’un réseau virtuel existant cluster tooan est tooother de connectivité réseau tooprovide machines virtuelles. Création hello VM constitue un bon exemple d’utilisation de réseau virtuel existant en général. Si votre cluster Service Fabric utilise uniquement un équilibreur de charge interne, sans une adresse IP publique, vous pouvez utiliser hello de machine virtuelle et son adresse IP publique sécurisé *accéder boîte*.

### <a name="static-public-ip-address"></a>Adresse IP publique statique

En général, une adresse IP publique statique est une ressource dédiée qui est gérée indépendamment de hello ou plusieurs machines virtuelles auquel elle est assignée. Il est configuré dans un groupe de ressources de mise en réseau dédié (en opposition tooin hello Service Fabric groupe de ressources cluster lui-même). Créer une adresse IP publique statique nommée staticIP1 Bonjour même groupe de ressources ExistingRG, Bonjour portail Azure ou à l’aide de PowerShell :

```powershell
PS C:\Users\user> New-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG -Location westus -AllocationMethod Static -DomainNameLabel sfnetworking

Name                     : staticIP1
ResourceGroupName        : ExistingRG
Location                 : westus
Id                       : /subscriptions/1237f4d2-3dce-1236-ad95-123f764e7123/resourceGroups/ExistingRG/providers/Microsoft.Network/publicIPAddresses/staticIP1
Etag                     : W/"fc8b0c77-1f84-455d-9930-0404ebba1b64"
ResourceGuid             : 77c26c06-c0ae-496c-9231-b1a114e08824
ProvisioningState        : Succeeded
Tags                     :
PublicIpAllocationMethod : Static
IpAddress                : 40.83.182.110
PublicIpAddressVersion   : IPv4
IdleTimeoutInMinutes     : 4
IpConfiguration          : null
DnsSettings              : {
                             "DomainNameLabel": "sfnetworking",
                             "Fqdn": "sfnetworking.westus.cloudapp.azure.com"
                           }
```

### <a name="service-fabric-template"></a>Modèle Service Fabric

Dans les exemples hello dans cet article, nous utilisons hello Service Fabric template.json. Vous pouvez utiliser hello standard portail toodownload hello modèle d’Assistant à partir du portail de hello avant de créer un cluster. Vous pouvez également utiliser un des modèles de hello Bonjour [galerie de modèles](https://azure.microsoft.com/en-us/documentation/templates/?term=service+fabric), comme hello [cluster Service Fabric de cinq nœuds](https://azure.microsoft.com/en-us/documentation/templates/service-fabric-unsecure-cluster-5-node-1-nodetype/).

<a id="existingvnet"></a>
## <a name="existing-virtual-network-or-subnet"></a>Réseau virtuel ou sous-réseau existant

1. Renommez hello sous-réseau paramètre toohello du sous-réseau existant de hello et ajoutez deux nouveaux paramètres tooreference hello réseau virtuel existant :

    ```
        "subnet0Name": {
                "type": "string",
                "defaultValue": "default"
            },
            "existingVNetRGName": {
                "type": "string",
                "defaultValue": "ExistingRG"
            },

            "existingVNetName": {
                "type": "string",
                "defaultValue": "ExistingRG-vnet"
            },
            /*
            "subnet0Name": {
                "type": "string",
                "defaultValue": "Subnet-0"
            },
            "subnet0Prefix": {
                "type": "string",
                "defaultValue": "10.0.0.0/24"
            },*/
    ```


2. Hello de modification `vnetID` variable toopoint toohello le réseau virtuel existant :

    ```
            /*old "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',parameters('virtualNetworkName'))]",*/
            "vnetID": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingVNetRGName'), '/providers/Microsoft.Network/virtualNetworks/', parameters('existingVNetName'))]",
    ```

3. Supprimez `Microsoft.Network/virtualNetworks` de vos ressources, afin qu’Azure ne crée pas de nouveau réseau virtuel :

    ```
    /*{
    "apiVersion": "[variables('vNetApiVersion')]",
    "type": "Microsoft.Network/virtualNetworks",
    "name": "[parameters('virtualNetworkName')]",
    "location": "[parameters('computeLocation')]",
    "properities": {
        "addressSpace": {
            "addressPrefixes": [
                "[parameters('addressPrefix')]"
            ]
        },
        "subnets": [
            {
                "name": "[parameters('subnet0Name')]",
                "properties": {
                    "addressPrefix": "[parameters('subnet0Prefix')]"
                }
            }
        ]
    },
    "tags": {
        "resourceType": "Service Fabric",
        "clusterName": "[parameters('clusterName')]"
    }
    },*/
    ```

4. Commentez de réseau virtuel de hello de hello `dependsOn` attribut de `Microsoft.Compute/virtualMachineScaleSets`, de sorte que vous ne dépendez pas Création d’un nouveau réseau virtuel :

    ```
    "apiVersion": "[variables('vmssApiVersion')]",
    "type": "Microsoft.Computer/virtualMachineScaleSets",
    "name": "[parameters('vmNodeType0Name')]",
    "location": "[parameters('computeLocation')]",
    "dependsOn": [
        /*"[concat('Microsoft.Network/virtualNetworks/', parameters('virtualNetworkName'))]",
        */
        "[Concat('Microsoft.Storage/storageAccounts/', variables('uniqueStringArray0')[0])]",

    ```

5. Déployer le modèle de hello :

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingexistingvnet -Location westus
    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingexistingvnet -TemplateFile C:\SFSamples\Final\template\_existingvnet.json
    ```

    Après le déploiement, votre réseau virtuel doit inclure ensemble d’échelle de nouveau hello de machines virtuelles. type de nœud de jeu Hello machine virtuelle mise à l’échelle doit afficher sous-réseau et réseau virtuel hello. Vous pouvez également utiliser protocole RDP (Remote Desktop) tooaccess hello machine virtuelle qui a été déjà dans le réseau virtuel de hello et ensemble d’échelle de nouveau tooping hello de machines virtuelles :

    ```
    C:>\Users\users>ping 10.0.0.5 -n 1
    C:>\Users\users>ping NOde1000000 -n 1
    ```

Pour un autre exemple, consultez [qui n’est pas spécifique tooService Fabric](https://github.com/gbowerman/azure-myriad/tree/master/existing-vnet).


<a id="staticpublicip"></a>
## <a name="static-public-ip-address"></a>Adresse IP publique statique

1. Ajouter des paramètres pour le nom hello Hello existants du groupe de ressources IP statique, nom et le nom de domaine complet (FQDN) :

    ```
    "existingStaticIPResourceGroup": {
                "type": "string"
            },
            "existingStaticIPName": {
                "type": "string"
            },
            "existingStaticIPDnsFQDN": {
                "type": "string"
    }
    ```

2. Supprimer hello `dnsName` paramètre. (l’adresse IP hello a déjà un.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

3. Ajoutez une variable tooreference hello adresse IP statique existante :

    ```
    "existingStaticIP": "[concat('/subscriptions/', subscription().subscriptionId, '/resourceGroups/', parameters('existingStaticIPResourceGroup'), '/providers/Microsoft.Network/publicIPAddresses/', parameters('existingStaticIPName'))]",
    ```

4. Supprimez `Microsoft.Network/publicIPAddresses` de vos ressources, afin qu’Azure ne crée pas de nouvelle adresse IP :

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

5. Commentez adresse IP hello hello `dependsOn` attribut de `Microsoft.Network/loadBalancers`, de sorte que vous ne dépendez pas la création d’une nouvelle adresse IP :

    ```
    "apiVersion": "[variables('lbIPApiVersion')]",
    "type": "Microsoft.Network/loadBalancers",
    "name": "[concat('LB', '-', parameters('clusterName'), '-', parameters('vmNodeType0Name'))]",
    "location": "[parameters('computeLocation')]",
    /*
    "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', concat(parameters('lbIPName'), '-', '0'))]"
    ], */
    "properties": {
    ```

6. Bonjour `Microsoft.Network/loadBalancers` ressources, modification hello `publicIPAddress` élément de `frontendIPConfigurations` tooreference hello une adresse IP statique existante au lieu d’une nouvellement créée :

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                "publicIPAddress": {
                                    /*"id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"*/
                                    "id": "[variables('existingStaticIP')]"
                                }
                            }
                        }
                    ],
    ```

7. Bonjour `Microsoft.ServiceFabric/clusters` ressources, modification `managementEndpoint` toohello DNS FQDN de l’adresse IP hello. Si vous utilisez un cluster sécurisé, assurez-vous de modifier *http://* trop*https://*. (Notez que cette étape s’applique uniquement les clusters tooService l’ensemble fibre optique. Si vous utilisez un groupe de machines virtuelles identiques, ignorez cette étape.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',parameters('existingStaticIPDnsFQDN'),':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

8. Déployer le modèle de hello :

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkingstaticip -Location westus

    $staticip = Get-AzureRmPublicIpAddress -Name staticIP1 -ResourceGroupName ExistingRG

    $staticip

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkingstaticip -TemplateFile C:\SFSamples\Final\template\_staticip.json -existingStaticIPResourceGroup $staticip.ResourceGroupName -existingStaticIPName $staticip.Name -existingStaticIPDnsFQDN $staticip.DnsSettings.Fqdn
    ```

Après le déploiement, vous pouvez voir que votre équilibreur de charge est lié toohello publique adresse IP statique à partir de hello autre groupe de ressources. Hello du point de terminaison de connexion de l’infrastructure de Service client et [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) toohello de point de terminaison DNS FQDN de l’adresse IP hello.

<a id="internallb"></a>
## <a name="internal-only-load-balancer"></a>Équilibreur de charge interne uniquement

Ce scénario remplace l’équilibrage de charge externe hello dans le modèle de Service Fabric hello par défaut avec un équilibrage de charge interne uniquement. Pour les implications pour hello portail Azure et pour le fournisseur de ressources de Service Fabric hello, consultez hello précédant la section.

1. Supprimer hello `dnsName` paramètre. (Il n’est pas nécessaire.)

    ```
    /*
    "dnsName": {
        "type": "string"
    },
    */
    ```

2. Si vous utilisez une méthode d’allocation statique, vous pouvez éventuellement ajouter un paramètre d’adresse IP statique. Si vous utilisez une méthode d’allocation dynamique, il est inutile toodo cette étape.

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

3. Supprimez `Microsoft.Network/publicIPAddresses` de vos ressources, afin qu’Azure ne crée pas de nouvelle adresse IP :

    ```
    /*
    {
        "apiVersion": "[variables('publicIPApiVersion')]",
        "type": "Microsoft.Network/publicIPAddresses",
        "name": "[concat(parameters('lbIPName'),)'-', '0')]",
        "location": "[parameters('computeLocation')]",
        "properties": {
            "dnsSettings": {
                "domainNameLabel": "[parameters('dnsName')]"
            },
            "publicIPAllocationMethod": "Dynamic"        
        },
        "tags": {
            "resourceType": "Service Fabric",
            "clusterName": "[parameters('clusterName')]"
        }
    }, */
    ```

4. Supprimez l’adresse IP de hello `dependsOn` attribut de `Microsoft.Network/loadBalancers`, de sorte que vous ne dépendez pas la création d’une nouvelle adresse IP. Ajouter un réseau virtuel de hello `dependsOn` attribut parce qu’équilibrage de charge hello dépend désormais de sous-réseau hello à partir du réseau virtuel de hello :

    ```
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'))]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /*"[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"*/
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
    ```

5. Modifier l’équilibreur de charge hello `frontendIPConfigurations` définition à partir de l’aide un `publicIPAddress`, toousing un sous-réseau et `privateIPAddress`. `privateIPAddress` utilise une adresse IP interne statique prédéfinie. toouse une adresse IP dynamique, supprimez hello `privateIPAddress` élément et modifiez `privateIPAllocationMethod` trop**dynamique**.

    ```
                "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /*
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                } */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
    ```

6. Bonjour `Microsoft.ServiceFabric/clusters` ressources, modification `managementEndpoint` adresse d’équilibrage de charge interne toopoint toohello. Si vous utilisez un cluster sécurisé, assurez-vous de modifier *http://* trop*https://*. (Notez que cette étape s’applique uniquement les clusters tooService l’ensemble fibre optique. Si vous utilisez un groupe de machines virtuelles identiques, ignorez cette étape.)

    ```
                    "fabricSettings": [],
                    /*"managementEndpoint": "[concat('http://',reference(concat(parameters('lbIPName'),'-','0')).dnsSettings.fqdn,':',parameters('nt0fabricHttpGatewayPort'))]",*/
                    "managementEndpoint": "[concat('http://',reference(variables('lbID0')).frontEndIPConfigurations[0].properties.privateIPAddress,':',parameters('nt0fabricHttpGatewayPort'))]",
    ```

7. Déployer le modèle de hello :

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternallb -TemplateFile C:\SFSamples\Final\template\_internalonlyLB.json
    ```

Après le déploiement, votre équilibreur de charge utilise adresse hello 10.0.0.250 statique privé. Si vous avez un autre ordinateur dans le même réseau virtuel, vous pouvez accéder toohello interne [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) point de terminaison. Notez qu’il connecte tooone de nœuds hello derrière un équilibreur de charge hello.

<a id="internalexternallb"></a>
## <a name="internal-and-external-load-balancer"></a>Équilibreur de charge interne et externe

Dans ce scénario, vous démarrez avec équilibrage de charge externe à nœud unique type hello existant et ajouter un équilibreur de charge interne pour hello même type de nœud. Équilibreur de charge unique tooa uniquement peut être affecté à un pool d’adresses de serveur principal de tooa port back-end attaché. Choisissez quel équilibreur de charge doit avoir vos ports d’application et lequel doit avoir vos points de terminaison de gestion (ports 19000 et 19080). Si vous placez des points de terminaison de gestion hello sur l’équilibreur de charge interne hello, conserver Bonjour d’esprit ressource de Service Fabric restrictions fournisseur décrites plus haut dans l’article de hello. Dans l’exemple hello, que nous utilisons, les points de terminaison de gestion hello restent sur l’équilibrage de charge externe hello. Vous également ajoutez un port d’application 80 de port et les placez sur l’équilibreur de charge interne hello.

Dans un cluster de deux de type de nœud, un type de nœud est sur l’équilibrage de charge externe hello. Bonjour autre type de nœud est sur l’équilibreur de charge interne hello. toouse un cluster de deux de type de nœud, dans hello portail créé deux de type de nœud modèle (qui est fourni avec deux programmes d’équilibrage de charge), basculez l’équilibreur de charge interne du tooan équilibrage de la charge deuxième hello. Pour plus d’informations, consultez hello [équilibreur de charge interne uniquement](#internallb) section.

1. Ajouter le paramètre d’adresse IP équilibrage hello de charge interne statique. (Pour les notes associée toousing une adresse IP dynamique, consultez les sections précédentes de cet article.)

    ```
            "internalLBAddress": {
                "type": "string",
                "defaultValue": "10.0.0.250"
            }
    ```

2. Ajoutez un paramètre port d’application 80.

3. les versions internes tooadd hello existante mise en réseau des variables, copier et les coller et ajouter des «-Int » toohello nom :

    ```
    /* Add internal load balancer networking variables */
            "lbID0-Int": "[resourceId('Microsoft.Network/loadBalancers', concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal'))]",
            "lbIPConfig0-Int": "[concat(variables('lbID0-Int'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
            "lbPoolID0-Int": "[concat(variables('lbID0-Int'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
            "lbProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricGatewayProbe')]",
            "lbHttpProbeID0-Int": "[concat(variables('lbID0-Int'),'/probes/FabricHttpGatewayProbe')]",
            "lbNatPoolID0-Int": "[concat(variables('lbID0-Int'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]",
            /* Internal load balancer networking variables end */
    ```

4. Si vous démarrez avec un modèle généré par le portail hello qui utilise le port 80 de l’application, le modèle de portail par défaut hello ajoute AppPort1 (port 80) sur l’équilibrage de charge externe hello. Dans ce cas, supprimez AppPort1 à partir de l’équilibrage de charge externe hello `loadBalancingRules` et sondes, vous pouvez l’ajouter équilibreur de charge interne toohello :

    ```
    "loadBalancingRules": [
        {
            "name": "LBHttpRule",
            "properties":{
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('nt0fabricHttpGatewayPort')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[variables('lbHttpProbeID0')]"
                },
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortLBRule1",
            "properties": {
                "backendAddressPool": {
                    "id": "[variables('lbPoolID0')]"
                },
                "backendPort": "[parameters('loadBalancedAppPort1')]",
                "enableFloatingIP": "false",
                "frontendIPConfiguration": {
                    "id": "[variables('lbIPConfig0')]"            
                },
                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                "idleTimeoutInMinutes": "5",
                "probe": {
                    "id": "[concate(variables('lbID0'), '/probes/AppPortProbe1')]"
                },
                "protocol": "tcp"
            }
        }*/

    ],
    "probes": [
        {
            "name": "FabricGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricTcpGatewayPort')]",
                "protocol": "tcp"
            }
        },
        {
            "name": "FabricHttpGatewayProbe",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('nt0fabricHttpGatewayPort')]",
                "protocol": "tcp"
            }
        } /* Remove AppPort1 from hello external load balancer.
        {
            "name": "AppPortProbe1",
            "properties": {
                "intervalInSeconds": 5,
                "numberOfProbes": 2,
                "port": "[parameters('loadBalancedAppPort1')]",
                "protocol": "tcp"
            }
        } */

    ],
    "inboundNatPools": [
    ```

5. Ajoutez une deuxième ressource `Microsoft.Network/loadBalancers`. Il semble similaire équilibreur de charge interne toohello créé Bonjour [équilibreur de charge interne uniquement](#internallb) section, mais il utilise hello »-Int » charge les variables de programme d’équilibrage et implémente uniquement hello application port 80. Cela supprime également `inboundNatPools`, points de terminaison tookeep RDP sur l’équilibreur de charge public hello. Si vous voulez RDP sur l’équilibreur de charge interne hello, déplacez `inboundNatPools` toothis de programme d’équilibrage de charge externe hello interne à partir de l’équilibrage de charge :

    ```
            /* Add a second load balancer, configured with a static privateIPAddress and hello "-Int" load balancer variables. */
            {
                "apiVersion": "[variables('lbApiVersion')]",
                "type": "Microsoft.Network/loadBalancers",
                /* Add "-Internal" toohello name. */
                "name": "[concat('LB','-', parameters('clusterName'),'-',parameters('vmNodeType0Name'), '-Internal')]",
                "location": "[parameters('computeLocation')]",
                "dependsOn": [
                    /* Remove public IP dependsOn, add vnet dependsOn
                    "[concat('Microsoft.Network/publicIPAddresses/',concat(parameters('lbIPName'),'-','0'))]"
                    */
                    "[concat('Microsoft.Network/virtualNetworks/',parameters('virtualNetworkName'))]"
                ],
                "properties": {
                    "frontendIPConfigurations": [
                        {
                            "name": "LoadBalancerIPConfig",
                            "properties": {
                                /* Switch from Public tooPrivate IP address
                                */
                                "publicIPAddress": {
                                    "id": "[resourceId('Microsoft.Network/publicIPAddresses',concat(parameters('lbIPName'),'-','0'))]"
                                }
                                */
                                "subnet" :{
                                    "id": "[variables('subnet0Ref')]"
                                },
                                "privateIPAddress": "[parameters('internalLBAddress')]",
                                "privateIPAllocationMethod": "Static"
                            }
                        }
                    ],
                    "backendAddressPools": [
                        {
                            "name": "LoadBalancerBEAddressPool",
                            "properties": {}
                        }
                    ],
                    "loadBalancingRules": [
                        /* Add hello AppPort rule. Be sure tooreference hello "-Int" versions of backendAddressPool, frontendIPConfiguration, and hello probe variables. */
                        {
                            "name": "AppPortLBRule1",
                            "properties": {
                                "backendAddressPool": {
                                    "id": "[variables('lbPoolID0-Int')]"
                                },
                                "backendPort": "[parameters('loadBalancedAppPort1')]",
                                "enableFloatingIP": "false",
                                "frontendIPConfiguration": {
                                    "id": "[variables('lbIPConfig0-Int')]"
                                },
                                "frontendPort": "[parameters('loadBalancedAppPort1')]",
                                "idleTimeoutInMinutes": "5",
                                "probe": {
                                    "id": "[concat(variables('lbID0-Int'),'/probes/AppPortProbe1')]"
                                },
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "probes": [
                    /* Add hello probe for hello app port. */
                    {
                            "name": "AppPortProbe1",
                            "properties": {
                                "intervalInSeconds": 5,
                                "numberOfProbes": 2,
                                "port": "[parameters('loadBalancedAppPort1')]",
                                "protocol": "tcp"
                            }
                        }
                    ],
                    "inboundNatPools": [
                    ]
                },
                "tags": {
                    "resourceType": "Service Fabric",
                    "clusterName": "[parameters('clusterName')]"
                }
            },
    ```

6. Dans `networkProfile` pour hello `Microsoft.Compute/virtualMachineScaleSets` ressource, ajoutez un pool d’adresses de serveur principal interne hello :

    ```
    "loadBalancerBackendAddressPools": [
                                                        {
                                                            "id": "[variables('lbPoolID0')]"
                                                        },
                                                        {
                                                            /* Add internal BE pool */
                                                            "id": "[variables('lbPoolID0-Int')]"
                                                        }
    ],
    ```

7. Déployer le modèle de hello :

    ```powershell
    New-AzureRmResourceGroup -Name sfnetworkinginternalexternallb -Location westus

    New-AzureRmResourceGroupDeployment -Name deployment -ResourceGroupName sfnetworkinginternalexternallb -TemplateFile C:\SFSamples\Final\template\_internalexternalLB.json
    ```

Après le déploiement, vous pouvez voir deux équilibreurs de charge dans le groupe de ressources hello. Si vous y accédez équilibreurs de charge hello, vous pouvez voir l’adresse IP publique de hello et l’adresse IP publique de gestion des points de terminaison (ports 19000 et 19080) affectés toohello. Vous pouvez également voir hello statique interne IP adresse et application de point de terminaison (port 80) attribué toohello interne l’équilibrage de charge. Les deux utiliser des équilibreurs de charge back-end pool définie hello même échelle de machines virtuelles.

## <a name="next-steps"></a>Étapes suivantes
[Créer un cluster](service-fabric-cluster-creation-via-arm.md)
