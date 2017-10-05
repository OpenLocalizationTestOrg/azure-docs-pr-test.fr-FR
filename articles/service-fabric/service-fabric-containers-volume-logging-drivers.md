---
title: "Version préliminaire de Docker Compose dans Azure Service Fabric | Microsoft Docs"
description: "Azure Service Fabric accepte le format Docker Compose pour vous permettre d’orchestrer facilement des conteneurs existants à l’aide de Service Fabric. Cette prise en charge est actuellement en mode préliminaire."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: ab49c4b9-74a8-4907-b75b-8d2ee84c6d90
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: b12ef95add6347621f7d4865fac46568f91a1e12
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="2ed33-104">Spécification de plug-ins de volume et de pilotes de journalisation pour votre conteneur</span><span class="sxs-lookup"><span data-stu-id="2ed33-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="2ed33-105">Service Fabric prend en charge la spécification de [plug-ins de volume Docker](https://docs.docker.com/engine/extend/plugins_volume/) et de [pilotes de journalisation de Docker](https://docs.docker.com/engine/admin/logging/overview/) pour votre service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="2ed33-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="2ed33-106">Les plug-ins sont spécifiés dans le manifeste de l’application, comme indiqué dans le manifeste suivant :</span><span class="sxs-lookup"><span data-stu-id="2ed33-106">The plugins are specified in the application manifest as shown in the following manifest:</span></span>


```xml
?xml version="1.0" encoding="UTF-8"?>
<ApplicationManifest ApplicationTypeName="WinNodeJsApp" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
    <Description>Calculator Application</Description>
    <Parameters>
        <Parameter Name="ServiceInstanceCount" DefaultValue="3"></Parameter>
      <Parameter Name="MyCpuShares" DefaultValue="3"></Parameter>
    </Parameters>
    <ServiceManifestImport>
        <ServiceManifestRef ServiceManifestName="NodeServicePackage" ServiceManifestVersion="1.0"/>
     <Policies>
       <ContainerHostPolicies CodePackageRef="NodeService.Code" Isolation="hyperv"> 
        <PortBinding ContainerPort="8905" EndpointRef="Endpoint1"/>
        <RepositoryCredentials PasswordEncrypted="false" Password="****" AccountName="test"/>
        <LogConfig Driver="etwlogs" >
          <DriverOption Name="test" Value="vale"/>
        </LogConfig>
        <Volume Source="c:\workspace" Destination="c:\testmountlocation1" IsReadOnly="false"></Volume>
        <Volume Source="d:\myfolder" Destination="c:\testmountlocation2" IsReadOnly="true"> </Volume>
        <Volume Source="myexternalvolume" Destination="c:\testmountlocation3" Driver="sf" IsReadOnly="true"></Volume>
       </ContainerHostPolicies>
   </Policies>
    </ServiceManifestImport>
    <ServiceTemplates>
        <StatelessService ServiceTypeName="StatelessNodeService" InstanceCount="5">
            <SingletonPartition></SingletonPartition>
        </StatelessService>
    </ServiceTemplates>
</ApplicationManifest>
```

<span data-ttu-id="2ed33-107">Dans l’exemple précédent, l’étiquette `Source` pour le `Volume` fait référence au dossier source.</span><span class="sxs-lookup"><span data-stu-id="2ed33-107">In the preceding example, the `Source` tag for the `Volume` refers to the source folder.</span></span> <span data-ttu-id="2ed33-108">Le dossier source peut être un dossier de la machine virtuelle qui héberge les conteneurs ou un magasin distant persistant.</span><span class="sxs-lookup"><span data-stu-id="2ed33-108">The source folder could be a folder in the VM that hosts the containers or a persistent remote store.</span></span> <span data-ttu-id="2ed33-109">L’étiquette `Destination` correspond à l’emplacement auquel est mappé l’élément `Source` dans le conteneur en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="2ed33-109">The `Destination` tag is the location that the `Source` is mapped to within the running container.</span></span> 

<span data-ttu-id="2ed33-110">Lorsque vous spécifiez un plug-in de volume, Service Fabric crée automatiquement le volume à l’aide des paramètres spécifiés.</span><span class="sxs-lookup"><span data-stu-id="2ed33-110">When specifying a volume plugin, Service Fabric automatically creates the volume using the parameters specified.</span></span> <span data-ttu-id="2ed33-111">La balise `Source` est le nom du volume, et la balise `Driver` spécifie le plug-in de pilote de volume.</span><span class="sxs-lookup"><span data-stu-id="2ed33-111">The `Source` tag is the name of the volume, and the `Driver` tag specifies the volume driver plugin.</span></span> <span data-ttu-id="2ed33-112">Des options peuvent être spécifiées à l’aide de la balise `DriverOption`, comme indiqué dans l’extrait de code suivant :</span><span class="sxs-lookup"><span data-stu-id="2ed33-112">Options can be specified using the `DriverOption` tag as shown in the following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="2ed33-113">Si un pilote de journalisation Docker est spécifié, il est nécessaire de déployer des agents (ou conteneurs) pour gérer les journaux dans le cluster.</span><span class="sxs-lookup"><span data-stu-id="2ed33-113">If a Docker log driver is specified, it is necessary to deploy agents (or containers) to handle the logs in the cluster.</span></span>  <span data-ttu-id="2ed33-114">La balise `DriverOption` peut également être utilisée pour spécifier les options de pilote de journal.</span><span class="sxs-lookup"><span data-stu-id="2ed33-114">The `DriverOption` tag can be used to specify log driver options as well.</span></span>

<span data-ttu-id="2ed33-115">Consultez les articles suivants pour déployer des conteneurs dans un cluster Service Fabric :</span><span class="sxs-lookup"><span data-stu-id="2ed33-115">Refer to the following articles to deploy containers to a Service Fabric cluster:</span></span>


[<span data-ttu-id="2ed33-116">Déployer un conteneur sur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="2ed33-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

