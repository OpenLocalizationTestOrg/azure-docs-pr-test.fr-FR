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
# <a name="specifying-volume-plugins-and-logging-drivers-for-your-container"></a>Spécification de plug-ins de volume et de pilotes de journalisation pour votre conteneur

Service Fabric prend en charge la spécification de [plug-ins de volume Docker](https://docs.docker.com/engine/extend/plugins_volume/) et de [pilotes de journalisation de Docker](https://docs.docker.com/engine/admin/logging/overview/) pour votre service de conteneur. plug-ins Hello sont spécifiés dans le manifeste de l’application hello comme indiqué dans hello suivant manifeste :


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

Bonjour précédent exemple, hello `Source` balise pour hello `Volume` fait référence le dossier source du toohello. dossier source de Hello peut être un dossier Bonjour machine virtuelle qui héberge les conteneurs hello ou un magasin persistant de distant. Hello `Destination` balise est l’emplacement de hello hello `Source` toowithin mappé hello exécute conteneur. 

Lorsque vous spécifiez un plug-in de volume, Service Fabric crée automatiquement le volume hello à l’aide de paramètres hello spécifiés. Hello `Source` balise est nom hello du volume de hello et hello `Driver` balise spécifie le plug-in de pilote de volume hello. Options peuvent être spécifiées à l’aide de hello `DriverOption` comme indiqué dans hello suivant extrait de la balise :

```xml
<Volume Source="myvolume1" Destination="c:\testmountlocation4" Driver="azurefile" IsReadOnly="true">
           <DriverOption Name="share" Value="models"/>
</Volume>
```

Si un pilote de journal Docker est spécifié, il est nécessaire toodeploy hello de toohandle agents (ou conteneurs) consigne dans le cluster de hello.  Hello `DriverOption` balise peut être des options de pilote journal toospecify utilisé ainsi.

Consultez toohello suivant le cluster Service Fabric tooa articles toodeploy conteneurs :


[Déployer un conteneur sur Service Fabric](service-fabric-deploy-container.md)

