---
title: aaaAzure Service Fabric Docker composer Preview | Documents Microsoft
description: "Azure Service Fabric accepte toomake de format Docker Compose il conteneurs d’exsiting tooorchestrate plus faciles à l’aide de l’infrastructure de Service. Cette prise en charge est actuellement en mode préliminaire."
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
ms.openlocfilehash: 824044fd698f0ed94c4212722bc82187905315dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a><span data-ttu-id="9e5f2-104">Spécification de plug-ins de volume et de pilotes de journalisation pour votre conteneur</span><span class="sxs-lookup"><span data-stu-id="9e5f2-104">Specifying volume plugins and logging drivers for your container</span></span>

<span data-ttu-id="9e5f2-105">Service Fabric prend en charge la spécification de [plug-ins de volume Docker](https://docs.docker.com/engine/extend/plugins_volume/) et de [pilotes de journalisation de Docker](https://docs.docker.com/engine/admin/logging/overview/) pour votre service de conteneur.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-105">Service Fabric supports specifying [Docker volume plugins](https://docs.docker.com/engine/extend/plugins_volume/) and [Docker logging drivers](https://docs.docker.com/engine/admin/logging/overview/) for your container service.</span></span> <span data-ttu-id="9e5f2-106">plug-ins Hello sont spécifiés dans le manifeste de l’application hello comme indiqué dans hello suivant manifeste :</span><span class="sxs-lookup"><span data-stu-id="9e5f2-106">hello plugins are specified in hello application manifest as shown in hello following manifest:</span></span>


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

<span data-ttu-id="9e5f2-107">Bonjour précédent exemple, hello `Source` balise pour hello `Volume` fait référence le dossier source du toohello.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-107">In hello preceding example, hello `Source` tag for hello `Volume` refers toohello source folder.</span></span> <span data-ttu-id="9e5f2-108">dossier source de Hello peut être un dossier Bonjour machine virtuelle qui héberge les conteneurs hello ou un magasin persistant de distant.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-108">hello source folder could be a folder in hello VM that hosts hello containers or a persistent remote store.</span></span> <span data-ttu-id="9e5f2-109">Hello `Destination` balise est l’emplacement de hello hello `Source` toowithin mappé hello exécute conteneur.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-109">hello `Destination` tag is hello location that hello `Source` is mapped toowithin hello running container.</span></span> 

<span data-ttu-id="9e5f2-110">Lorsque vous spécifiez un plug-in de volume, Service Fabric crée automatiquement le volume hello à l’aide de paramètres hello spécifiés.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-110">When specifying a volume plugin, Service Fabric automatically creates hello volume using hello parameters specified.</span></span> <span data-ttu-id="9e5f2-111">Hello `Source` balise est nom hello du volume de hello et hello `Driver` balise spécifie le plug-in de pilote de volume hello.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-111">hello `Source` tag is hello name of hello volume, and hello `Driver` tag specifies hello volume driver plugin.</span></span> <span data-ttu-id="9e5f2-112">Options peuvent être spécifiées à l’aide de hello `DriverOption` comme indiqué dans hello suivant extrait de la balise :</span><span class="sxs-lookup"><span data-stu-id="9e5f2-112">Options can be specified using hello `DriverOption` tag as shown in hello following snippet:</span></span>

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

<span data-ttu-id="9e5f2-113">Si un pilote de journal Docker est spécifié, il est nécessaire toodeploy hello de toohandle agents (ou conteneurs) consigne dans le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-113">If a Docker log driver is specified, it is necessary toodeploy agents (or containers) toohandle hello logs in hello cluster.</span></span>  <span data-ttu-id="9e5f2-114">Hello `DriverOption` balise peut être des options de pilote journal toospecify utilisé ainsi.</span><span class="sxs-lookup"><span data-stu-id="9e5f2-114">hello `DriverOption` tag can be used toospecify log driver options as well.</span></span>

<span data-ttu-id="9e5f2-115">Consultez toohello suivant le cluster Service Fabric tooa articles toodeploy conteneurs :</span><span class="sxs-lookup"><span data-stu-id="9e5f2-115">Refer toohello following articles toodeploy containers tooa Service Fabric cluster:</span></span>


[<span data-ttu-id="9e5f2-116">Déployer un conteneur sur Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9e5f2-116">Deploy a container on Service Fabric</span></span>](service-fabric-deploy-container.md)

