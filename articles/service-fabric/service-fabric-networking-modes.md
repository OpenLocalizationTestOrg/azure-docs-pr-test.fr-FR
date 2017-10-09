---
title: "aaaConfigure mise en réseau des modes pour les services de conteneur Azure Service Fabric | Documents Microsoft"
description: "Découvrez comment modes de mise en réseau différents toosetup hello que Azure Service Fabric prend en charge."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: 5c5dd4c590c7698a947503cbe8ef66ff7d6b503a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-container-networking-modes"></a>Modes de mise en réseau du conteneur Service Fabric

Hello mode de mise en réseau par défaut proposé dans hello l’infrastructure de Service de cluster pour les services de conteneur est hello `nat` en mode de mise en réseau. Avec hello `nat` mise en réseau en mode, ayant plusieurs conteneurs service écoute toohello même port entraîne des erreurs de déploiement. Pour l’exécution de plusieurs services qui écoutent sur hello prend en charge le même port, le Service Fabric hello `open` en mode de mise en réseau (version 5.7 ou version ultérieure). Avec hello `open` en mode de mise en réseau, chaque service de conteneur obtient une adresse IP affectée dynamiquement en interne autorisant plusieurs toohello de toolisten services même port.   

Par conséquent, avec un seul type de service avec un point de terminaison statique défini dans le manifeste de service hello, nouveaux services peuvent être créées et supprimées sans erreurs de déploiement à l’aide de hello `open` en mode de mise en réseau. De même, un utilisateur peut employer hello même `docker-compose.yml` fichier avec les mappages de ports statiques pour la création de plusieurs services.

À l’aide de hello attribué dynamiquement des services de toodiscover IP n’est pas conseillé depuis les changements d’adresses IP hello lorsque le service de hello redémarre ou déplace le nœud de tooanother. Utilisez uniquement hello **Service Fabric Naming Service** ou hello **Service DNS** pour la découverte de service. 


> [!WARNING]
> Au total, seules 4 096 adresses IP sont autorisées par réseau virtuel dans Azure. Par conséquent, les somme hello de nombre hello de nœuds et de nombre hello conteneur d’instances de service (avec `open` mise en réseau) ne peut pas dépasser 4096 au sein d’un réseau virtuel. Pour de tels scénarios haute densités, hello `nat` est recommandé de mode de mise en réseau.
>

## <a name="setting-up-open-networking-mode"></a>Configuration du mode de mise en réseau ouvert

1. Installer le modèle de gestionnaire de ressources Azure hello en activant le Service DNS et hello fournisseur IP sous `fabricSettings`. 

    ```json
    "fabricSettings": [
                {
                    "name": "DnsService",
                    "parameters": [
                       {
                            "name": "IsEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name": "Hosting",
                    "parameters": [
                      { 
                            "name": "IPProviderEnabled",
                            "value": "true"
                      }
                    ]
                },
                {
                    "name":  "Trace/Etw", 
                    "parameters": [
                    {
                            "name": "Level",
                            "value": "5"
                    }
                    ]
                },
                {
                    "name": "Setup",
                    "parameters": [
                    {
                            "name": "ContainerNetworkSetup",
                            "value": "true"
                    }
                    ]
                }
            ],
    ```

2. Configurer hello réseau profil section tooallow toobe configuré sur chaque nœud du cluster de hello des adresses IP multiples. Hello exemple suivant définit les cinq adresses IP par nœud (par conséquent, vous pouvez avoir cinq instances de service à l’écoute du port toohello sur chaque nœud) pour un cluster du Service Windows Fabric.

    ```json
    "variables": {
        "nicName": "NIC",
        "vmName": "vm",
        "virtualNetworkName": "VNet",
        "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
        "vmNodeType0Name": "[toLower(concat('NT1', variables('vmName')))]",
        "subnet0Name": "Subnet-0",
        "subnet0Prefix": "10.0.0.0/24",
        "subnet0Ref": "[concat(variables('vnetID'),'/subnets/',variables('subnet0Name'))]",
        "lbID0": "[resourceId('Microsoft.Network/loadBalancers',concat('LB','-', parameters('clusterName'),'-',variables('vmNodeType0Name')))]",
        "lbIPConfig0": "[concat(variables('lbID0'),'/frontendIPConfigurations/LoadBalancerIPConfig')]",
        "lbPoolID0": "[concat(variables('lbID0'),'/backendAddressPools/LoadBalancerBEAddressPool')]",
        "lbProbeID0": "[concat(variables('lbID0'),'/probes/FabricGatewayProbe')]",
        "lbHttpProbeID0": "[concat(variables('lbID0'),'/probes/FabricHttpGatewayProbe')]",
        "lbNatPoolID0": "[concat(variables('lbID0'),'/inboundNatPools/LoadBalancerBEAddressNatPool')]"
    }
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

    Pour les clusters Linux, une configuration IP publique supplémentaire est ajoutée connectivité sortante de tooallow. Hello extrait de code suivant définit cinq adresses IP par nœud d’un cluster Linux :

    ```json
    "networkProfile": {
                "networkInterfaceConfigurations": [
                  {
                    "name": "[concat(parameters('nicName'), '-0')]",
                    "properties": {
                      "ipConfigurations": [
                        {
                          "name": "[concat(parameters('nicName'),'-',0)]",
                          "properties": {
                            "primary": "true",
                            "publicipaddressconfiguration": {
                              "name": "devpub",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "loadBalancerBackendAddressPools": [
                              {
                                "id": "[variables('lbPoolID0')]"
                              }
                            ],
                            "loadBalancerInboundNatPools": [
                              {
                                "id": "[variables('lbNatPoolID0')]"
                              }
                            ],
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 1)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 1)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 2)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 2)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 3)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 3)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 4)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 4)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        },
                        {
                          "name": "[concat(parameters('nicName'),'-', 5)]",
                          "properties": {
                            "primary": "false",
                            "publicipaddressconfiguration": {
                              "name": "[concat('devpub', 5)]",
                              "properties": {
                                "idleTimeoutInMinutes": 15
                              }
                            },
                            "subnet": {
                              "id": "[variables('subnet0Ref')]"
                            }
                          }
                        }
                      ],
                      "primary": true
                    }
                  }
                ]
              }
    ```

3. Pour les clusters ne, définir un groupe de sécurité réseau de Windows règle ouverture de port UDP/53 pour le réseau virtuel de hello avec hello valeurs suivantes :

   | Priorité |    Nom    |    Source      |  Destination   |   Service    | Action |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     2000 | Custom_Dns | VirtualNetwork | VirtualNetwork | DNS (UDP/53) | AUTORISER  |


4. Spécifiez le mode de mise en réseau hello dans le manifeste de l’application hello pour chaque service `<NetworkConfig NetworkType="open">`.  mode de Hello `open` entraîne service hello obtention d’une adresse IP dédiée. Si un mode n’est pas spécifié, la valeur par défaut toohello base `nat` mode. Par conséquent, dans hello exemple manifeste, `NodeContainerServicePackage1` et `NodeContainerServicePackage2` pouvez chaque toohello écoute même port (les deux services qui écoutent sur `Endpoint1`).

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <ApplicationManifest ApplicationTypeName="NodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
      <Description>Calculator Application</Description>
      <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
        <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
      </Parameters>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage1" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService1.Code" Isolation="hyperv">
           <NetworkConfig NetworkType="open"/>
           <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
      <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeContainerServicePackage2" ServiceManifestVersion="1.0"/>
        <Policies>
          <ContainerHostPolicies CodePackageRef="NodeContainerService2.Code" Isolation="default">
            <NetworkConfig NetworkType="open"/>
            <PortBinding ContainerPort="8910" EndpointRef="Endpoint1"/>
          </ContainerHostPolicies>
        </Policies>
      </ServiceManifestImport>
    </ApplicationManifest>
    ```
Vous pouvez combiner différents modes de mise en réseau entre les services au sein d’une application d’un cluster Windows. Par conséquent, vous pouvez avoir des services sur les modes de mise en réseau `open` et `nat`. Quand un service est configuré avec `nat`, port hello il s’agit d’écoute toomust être unique. La combinaison de modes de mise en réseau pour différents services n’est pas prise en charge sur les clusters Linux. 


## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez obtenu des informations sur les modes de mise en réseau offerts par Service Fabric.  

* [Modèle d'application Service Fabric](service-fabric-application-model.md)
* [Ressources du manifeste de Service Fabric](service-fabric-application-model.md)
* [Déployer un tooService de conteneur Windows Fabric sur Windows Server 2016](service-fabric-get-started-containers.md)
* [Déployer un tooService de conteneur Docker Fabric sur Linux](service-fabric-get-started-containers-linux.md)
