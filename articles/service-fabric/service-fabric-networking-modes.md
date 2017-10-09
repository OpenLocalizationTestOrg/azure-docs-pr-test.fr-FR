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
# <a name="service-fabric-container-networking-modes"></a><span data-ttu-id="d3124-103">Modes de mise en réseau du conteneur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d3124-103">Service Fabric container networking modes</span></span>

<span data-ttu-id="d3124-104">Hello mode de mise en réseau par défaut proposé dans hello l’infrastructure de Service de cluster pour les services de conteneur est hello `nat` en mode de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="d3124-104">hello default networking mode offered in hello Service Fabric cluster for container services is hello `nat` networking mode.</span></span> <span data-ttu-id="d3124-105">Avec hello `nat` mise en réseau en mode, ayant plusieurs conteneurs service écoute toohello même port entraîne des erreurs de déploiement.</span><span class="sxs-lookup"><span data-stu-id="d3124-105">With hello `nat` networking mode, having more than one containers service listening toohello same port results in deployment errors.</span></span> <span data-ttu-id="d3124-106">Pour l’exécution de plusieurs services qui écoutent sur hello prend en charge le même port, le Service Fabric hello `open` en mode de mise en réseau (version 5.7 ou version ultérieure).</span><span class="sxs-lookup"><span data-stu-id="d3124-106">For running several services that listen on hello same port, Service Fabric supports hello `open` networking mode (version 5.7 or higher).</span></span> <span data-ttu-id="d3124-107">Avec hello `open` en mode de mise en réseau, chaque service de conteneur obtient une adresse IP affectée dynamiquement en interne autorisant plusieurs toohello de toolisten services même port.</span><span class="sxs-lookup"><span data-stu-id="d3124-107">With hello `open` networking mode, each container service gets a dynamically assigned IP address internally allowing multiple services toolisten toohello same port.</span></span>   

<span data-ttu-id="d3124-108">Par conséquent, avec un seul type de service avec un point de terminaison statique défini dans le manifeste de service hello, nouveaux services peuvent être créées et supprimées sans erreurs de déploiement à l’aide de hello `open` en mode de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="d3124-108">Thus, with a single service type with a static endpoint defined in hello service manifest, new services may be created and deleted without deployment errors using hello `open` networking mode.</span></span> <span data-ttu-id="d3124-109">De même, un utilisateur peut employer hello même `docker-compose.yml` fichier avec les mappages de ports statiques pour la création de plusieurs services.</span><span class="sxs-lookup"><span data-stu-id="d3124-109">Similarly, one can use hello same `docker-compose.yml` file with static port mappings for creating multiple services.</span></span>

<span data-ttu-id="d3124-110">À l’aide de hello attribué dynamiquement des services de toodiscover IP n’est pas conseillé depuis les changements d’adresses IP hello lorsque le service de hello redémarre ou déplace le nœud de tooanother.</span><span class="sxs-lookup"><span data-stu-id="d3124-110">Using hello dynamically assigned IP toodiscover services is not advisable since hello IP address changes when hello service restarts or moves tooanother node.</span></span> <span data-ttu-id="d3124-111">Utilisez uniquement hello **Service Fabric Naming Service** ou hello **Service DNS** pour la découverte de service.</span><span class="sxs-lookup"><span data-stu-id="d3124-111">Only use hello **Service Fabric Naming Service**  or hello **DNS Service** for service discovery.</span></span> 


> [!WARNING]
> <span data-ttu-id="d3124-112">Au total, seules 4 096 adresses IP sont autorisées par réseau virtuel dans Azure.</span><span class="sxs-lookup"><span data-stu-id="d3124-112">Only a total of 4096 IPs are allowed per vNET in Azure.</span></span> <span data-ttu-id="d3124-113">Par conséquent, les somme hello de nombre hello de nœuds et de nombre hello conteneur d’instances de service (avec `open` mise en réseau) ne peut pas dépasser 4096 au sein d’un réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="d3124-113">Thus, hello sum of hello number of nodes and hello number of container service instances (with `open` networking) cannot exceed 4096 within a vNET.</span></span> <span data-ttu-id="d3124-114">Pour de tels scénarios haute densités, hello `nat` est recommandé de mode de mise en réseau.</span><span class="sxs-lookup"><span data-stu-id="d3124-114">For such high-density scenarios, hello `nat` networking mode is recommended.</span></span>
>

## <a name="setting-up-open-networking-mode"></a><span data-ttu-id="d3124-115">Configuration du mode de mise en réseau ouvert</span><span class="sxs-lookup"><span data-stu-id="d3124-115">Setting up open networking mode</span></span>

1. <span data-ttu-id="d3124-116">Installer le modèle de gestionnaire de ressources Azure hello en activant le Service DNS et hello fournisseur IP sous `fabricSettings`.</span><span class="sxs-lookup"><span data-stu-id="d3124-116">Set up hello Azure Resource Manager template by enabling DNS Service and hello IP Provider under `fabricSettings`.</span></span> 

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

2. <span data-ttu-id="d3124-117">Configurer hello réseau profil section tooallow toobe configuré sur chaque nœud du cluster de hello des adresses IP multiples.</span><span class="sxs-lookup"><span data-stu-id="d3124-117">Set up hello network profile section tooallow multiple IP addresses toobe configured on each node of hello cluster.</span></span> <span data-ttu-id="d3124-118">Hello exemple suivant définit les cinq adresses IP par nœud (par conséquent, vous pouvez avoir cinq instances de service à l’écoute du port toohello sur chaque nœud) pour un cluster du Service Windows Fabric.</span><span class="sxs-lookup"><span data-stu-id="d3124-118">hello following example sets up five IP addresses per node (thus you can have five service instances listening toohello port on each node) for a Windows Service Fabric cluster.</span></span>

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

    <span data-ttu-id="d3124-119">Pour les clusters Linux, une configuration IP publique supplémentaire est ajoutée connectivité sortante de tooallow.</span><span class="sxs-lookup"><span data-stu-id="d3124-119">For Linux clusters, an additional public IP configuration is added tooallow outbound connectivity.</span></span> <span data-ttu-id="d3124-120">Hello extrait de code suivant définit cinq adresses IP par nœud d’un cluster Linux :</span><span class="sxs-lookup"><span data-stu-id="d3124-120">hello following snippet sets up five IP addresses per node for a Linux cluster:</span></span>

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

3. <span data-ttu-id="d3124-121">Pour les clusters ne, définir un groupe de sécurité réseau de Windows règle ouverture de port UDP/53 pour le réseau virtuel de hello avec hello valeurs suivantes :</span><span class="sxs-lookup"><span data-stu-id="d3124-121">For Windows clusters only, set up an NSG rule opening up port UDP/53 for hello vNET with hello following values:</span></span>

   | <span data-ttu-id="d3124-122">Priorité</span><span class="sxs-lookup"><span data-stu-id="d3124-122">Priority</span></span> |    <span data-ttu-id="d3124-123">Nom</span><span class="sxs-lookup"><span data-stu-id="d3124-123">Name</span></span>    |    <span data-ttu-id="d3124-124">Source</span><span class="sxs-lookup"><span data-stu-id="d3124-124">Source</span></span>      |  <span data-ttu-id="d3124-125">Destination</span><span class="sxs-lookup"><span data-stu-id="d3124-125">Destination</span></span>   |   <span data-ttu-id="d3124-126">Service</span><span class="sxs-lookup"><span data-stu-id="d3124-126">Service</span></span>    | <span data-ttu-id="d3124-127">Action</span><span class="sxs-lookup"><span data-stu-id="d3124-127">Action</span></span> |
   |:--------:|:----------:|:--------------:|:--------------:|:------------:|:------:|
   |     <span data-ttu-id="d3124-128">2000</span><span class="sxs-lookup"><span data-stu-id="d3124-128">2000</span></span> | <span data-ttu-id="d3124-129">Custom_Dns</span><span class="sxs-lookup"><span data-stu-id="d3124-129">Custom_Dns</span></span> | <span data-ttu-id="d3124-130">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d3124-130">VirtualNetwork</span></span> | <span data-ttu-id="d3124-131">VirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="d3124-131">VirtualNetwork</span></span> | <span data-ttu-id="d3124-132">DNS (UDP/53)</span><span class="sxs-lookup"><span data-stu-id="d3124-132">DNS (UDP/53)</span></span> | <span data-ttu-id="d3124-133">AUTORISER</span><span class="sxs-lookup"><span data-stu-id="d3124-133">Allow</span></span>  |


4. <span data-ttu-id="d3124-134">Spécifiez le mode de mise en réseau hello dans le manifeste de l’application hello pour chaque service `<NetworkConfig NetworkType="open">`.</span><span class="sxs-lookup"><span data-stu-id="d3124-134">Specify hello networking mode in hello app manifest for each service `<NetworkConfig NetworkType="open">`.</span></span>  <span data-ttu-id="d3124-135">mode de Hello `open` entraîne service hello obtention d’une adresse IP dédiée.</span><span class="sxs-lookup"><span data-stu-id="d3124-135">hello mode `open` results in hello service getting a dedicated IP address.</span></span> <span data-ttu-id="d3124-136">Si un mode n’est pas spécifié, la valeur par défaut toohello base `nat` mode.</span><span class="sxs-lookup"><span data-stu-id="d3124-136">If a mode isn't specified, it defaults toohello basic `nat` mode.</span></span> <span data-ttu-id="d3124-137">Par conséquent, dans hello exemple manifeste, `NodeContainerServicePackage1` et `NodeContainerServicePackage2` pouvez chaque toohello écoute même port (les deux services qui écoutent sur `Endpoint1`).</span><span class="sxs-lookup"><span data-stu-id="d3124-137">Thus, in hello following manifest example, `NodeContainerServicePackage1` and `NodeContainerServicePackage2` can each listen toohello same port (both services are listening on `Endpoint1`).</span></span>

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
<span data-ttu-id="d3124-138">Vous pouvez combiner différents modes de mise en réseau entre les services au sein d’une application d’un cluster Windows.</span><span class="sxs-lookup"><span data-stu-id="d3124-138">You can mix and match different networking modes across services within an application for a Windows cluster.</span></span> <span data-ttu-id="d3124-139">Par conséquent, vous pouvez avoir des services sur les modes de mise en réseau `open` et `nat`.</span><span class="sxs-lookup"><span data-stu-id="d3124-139">Thus, you can have some services on `open` mode and some on `nat` networking mode.</span></span> <span data-ttu-id="d3124-140">Quand un service est configuré avec `nat`, port hello il s’agit d’écoute toomust être unique.</span><span class="sxs-lookup"><span data-stu-id="d3124-140">When a service is configured with `nat`, hello port it is listening toomust be unique.</span></span> <span data-ttu-id="d3124-141">La combinaison de modes de mise en réseau pour différents services n’est pas prise en charge sur les clusters Linux.</span><span class="sxs-lookup"><span data-stu-id="d3124-141">Mixing networking modes for different services isn't supported on Linux clusters.</span></span> 


## <a name="next-steps"></a><span data-ttu-id="d3124-142">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="d3124-142">Next steps</span></span>
<span data-ttu-id="d3124-143">Dans cet article, vous avez obtenu des informations sur les modes de mise en réseau offerts par Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="d3124-143">In this article, you learned about networking modes offered by Service Fabric.</span></span>  

* [<span data-ttu-id="d3124-144">Modèle d'application Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d3124-144">Service Fabric application model</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="d3124-145">Ressources du manifeste de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d3124-145">Service Fabric service manifest resources</span></span>](service-fabric-application-model.md)
* [<span data-ttu-id="d3124-146">Déployer un tooService de conteneur Windows Fabric sur Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d3124-146">Deploy a Windows container tooService Fabric on Windows Server 2016</span></span>](service-fabric-get-started-containers.md)
* [<span data-ttu-id="d3124-147">Déployer un tooService de conteneur Docker Fabric sur Linux</span><span class="sxs-lookup"><span data-stu-id="d3124-147">Deploy a Docker container tooService Fabric on Linux</span></span>](service-fabric-get-started-containers-linux.md)
