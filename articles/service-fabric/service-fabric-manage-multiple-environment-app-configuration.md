---
title: aaaManage plusieurs environnements dans le Service Fabric | Documents Microsoft
description: "Applications de service Fabric peuvent être exécutées sur des clusters dont la taille à partir d’un ordinateur toothousands, des ordinateurs. Dans certains cas, vous devez tooconfigure votre application différemment pour les différents environnements. Cet article décrit comment toodefine les paramètres d’application par l’environnement."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: f406eac9-7271-4c37-a0d3-0a2957b60537
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/18/2017
ms.author: mikkelhegn
ms.openlocfilehash: 2b3327e0e1a3bbd35a50835e720619f308b1b501
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-application-parameters-for-multiple-environments"></a>Gestion des paramètres d’application pour plusieurs environnements
Vous pouvez créer des clusters d’Azure Service Fabric à l’aide de n’importe où à partir d’un seul réduire des milliers d’ordinateurs. Alors que les fichiers binaires d’application peuvent s’exécuter sans modification sur ce large éventail d’environnements, il est souvent nécessaire application hello de tooconfigure différemment, en fonction du nombre de hello d’ordinateurs que vous déployez.

À titre d’exemple, envisagez d’utiliser `InstanceCount` pour un service sans état. Quand vous exécutez des applications dans Azure, vous devez généralement tooset ce paramètre toohello valeur spéciale « -1 ». Cette configuration garantit que votre service s’exécute sur chaque nœud de cluster de hello (ou tous les nœuds de type de nœud hello si vous avez défini une contrainte de placement). Toutefois, cette configuration n’est pas appropriée pour un seul ordinateur cluster, car vous ne peut pas avoir plusieurs processus à l’écoute sur hello même point de terminaison sur un seul ordinateur. Au lieu de cela, vous définissez généralement `InstanceCount` trop « 1 ».

## <a name="specifying-environment-specific-parameters"></a>Spécification des paramètres spécifiques à l’environnement
problème de configuration toothis Hello solution est un ensemble de services paramétrable par défaut et les fichiers de paramètres d’application qui remplissent ces valeurs de paramètre pour un environnement donné. Services par défaut et les paramètres de l’application sont configurés dans l’application hello et manifestes de service. Hello définition de schéma pour les fichiers ServiceManifest.xml et ApplicationManifest.xml hello est installée avec hello SDK de l’infrastructure de Service et les outils trop*C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

### <a name="default-services"></a>Services par défaut
Les applications Service Fabric sont constituées d’une collection d’instances de service. Il est possible que vous toocreate une application vide et ensuite créer dynamiquement toutes les instances de service, la plupart des applications dispose un ensemble de services principaux qui doit toujours être créé lors de l’application hello est instanciée. Il s’agit tooas référencé « services par défaut ». Ils sont spécifiés dans le manifeste de l’application hello, avec des espaces réservés pour la configuration per-environnement inclus entre crochets :

```xml
  <DefaultServices>
      <Service Name="Stateful1">
          <StatefulService
              ServiceTypeName="Stateful1Type"
              TargetReplicaSetSize="[Stateful1_TargetReplicaSetSize]"
              MinReplicaSetSize="[Stateful1_MinReplicaSetSize]">

              <UniformInt64Partition
                  PartitionCount="[Stateful1_PartitionCount]"
                  LowKey="-9223372036854775808"
                  HighKey="9223372036854775807"
              />
        </StatefulService>
    </Service>
  </DefaultServices>
```

Chacun des paramètres nommé de hello doit être défini dans l’élément des paramètres hello hello du manifeste d’application :

```xml
    <Parameters>
        <Parameter Name="Stateful1_MinReplicaSetSize" DefaultValue="3" />
        <Parameter Name="Stateful1_PartitionCount" DefaultValue="1" />
        <Parameter Name="Stateful1_TargetReplicaSetSize" DefaultValue="3" />
    </Parameters>
```

attribut de DefaultValue Hello spécifie hello toobe de valeur utilisé dans l’absence de hello d’un paramètre plus spécifique pour un environnement donné.

> [!NOTE]
> Tous les paramètres d’instance de service conviennent à la configuration par environnement. Dans l’exemple hello ci-dessus, hello LowKey et HighKey valeurs pour le schéma de partitionnement du service hello sont explicitement définies pour toutes les instances de service de hello, car la plage de partition hello est une fonction de domaine de données hello, pas l’environnement hello.
> 
> 

### <a name="per-environment-service-configuration-settings"></a>Paramètres de configuration de service par environnement
Hello [modèle d’application Service Fabric](service-fabric-application-model.md) tooinclude les packages de configuration qui contiennent des paires clé-valeur personnalisées qui peuvent être lus au moment de l’exécution des services Active. valeurs Hello de ces paramètres peuvent également être différenciées par l’environnement en spécifiant un `ConfigOverride` dans le manifeste de l’application hello.

Supposons que vous ayez hello suivant paramètre dans le fichier de Config\Settings.xml hello pour hello `Stateful1` service :

```xml
  <Section Name="MyConfigSection">
     <Parameter Name="MaxQueueSize" Value="25" />
  </Section>
```
Création de cette valeur pour une paire d’application/environnement spécifique, toooverride un `ConfigOverride` lorsque vous importez le manifeste de service hello dans le manifeste de l’application hello.

```xml
  <ConfigOverrides>
     <ConfigOverride Name="Config">
        <Settings>
           <Section Name="MyConfigSection">
              <Parameter Name="MaxQueueSize" Value="[Stateful1_MaxQueueSize]" />
           </Section>
        </Settings>
     </ConfigOverride>
  </ConfigOverrides>
```
Ce paramètre peut ensuite être configuré par environnement, comme indiqué ci-dessus. Vous pouvez le faire en déclarant dans la section Paramètres de hello hello du manifeste d’application et en spécifiant des valeurs spécifiques à l’environnement dans les fichiers de paramètres d’application hello.

> [!NOTE]
> Dans les cas de hello des paramètres de configuration de service, il existe trois emplacements où hello d’une clé peut avoir la valeur : package de configuration du service hello, manifeste de l’application hello et fichier de paramètres d’application hello. L’infrastructure de service seront toujours choisir à partir du fichier de paramètres d’application hello tout d’abord (si spécifié), hello du manifeste d’application, puis enfin hello package de configuration.
> 
> 

### <a name="setting-and-using-environment-variables"></a>Définition et utilisation des variables d’environnement 
Vous pouvez spécifier et définir des variables d’environnement dans le fichier ServiceManifest.xml de hello et ensuite substituer ces éléments dans le fichier ApplicationManifest.xml de hello sur chaque instance.
exemple Hello ci-dessous montre les deux variables d’environnement, une avec une valeur définie et hello autres est remplacé. Vous pouvez utiliser les paramètres de valeurs de variables d’environnement tooset Bonjour même façon que ces ont été utilisés pour les remplacements de configuration d’application.

```xml
<?xml version="1.0" encoding="utf-8" ?>
<ServiceManifest Name="MyServiceManifest" Version="SvcManifestVersion1" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
  <Description>An example service manifest</Description>
  <ServiceTypes>
    <StatelessServiceType ServiceTypeName="MyServiceType" />
  </ServiceTypes>
  <CodePackage Name="MyCode" Version="CodeVersion1">
    <SetupEntryPoint>
      <ExeHost>
        <Program>MySetup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    <EntryPoint>
      <ExeHost>
        <Program>MyServiceHost.exe</Program>
      </ExeHost>
    </EntryPoint>
    <EnvironmentVariables>
      <EnvironmentVariable Name="MyEnvVariable" Value=""/>
      <EnvironmentVariable Name="HttpGatewayPort" Value="19080"/>
    </EnvironmentVariables>
  </CodePackage>
  <ConfigPackage Name="MyConfig" Version="ConfigVersion1" />
  <DataPackage Name="MyData" Version="DataVersion1" />
</ServiceManifest>
```
variables d’environnement toooverride hello Bonjour ApplicationManifest.xml, package de code hello référence Bonjour ServiceManifest avec hello `EnvironmentOverrides` élément.

```xml
  <ServiceManifestImport>
    <ServiceManifestRef ServiceManifestName="FrontEndServicePkg" ServiceManifestVersion="1.0.0" />
    <EnvironmentOverrides CodePackageRef="MyCode">
      <EnvironmentVariable Name="MyEnvVariable" Value="mydata"/>
    </EnvironmentOverrides>
  </ServiceManifestImport>
 ``` 
 Une fois hello nommé l’instance de service est créé, vous pouvez accéder variables d’environnement hello à partir du code. par exemple, en c# vous pouvez effectuer suivant de hello

```csharp
    string EnvVariable = Environment.GetEnvironmentVariable("MyEnvVariable");
```

### <a name="service-fabric-environment-variables"></a>Variables d’environnement de Service Fabric
Des variables d’environnement définies pour chaque instance de service sont intégrées à Service Fabric. Hello la liste complète des variables d’environnement est ci-dessous, où hello celles en gras sont hello ceux que vous utiliserez dans votre service, hello autre étant utilisé par le runtime Service Fabric. 

* Fabric_ApplicationHostId
* Fabric_ApplicationHostType
* Fabric_ApplicationId
* **Fabric_ApplicationName**
* Fabric_CodePackageInstanceId
* **Fabric_CodePackageName**
* **Fabric_Endpoint_[YourServiceName]TypeEndpoint**
* **Fabric_Folder_App_Log**
* **Fabric_Folder_App_Temp**
* **Fabric_Folder_App_Work**
* **Fabric_Folder_Application**
* Fabric_NodeId
* **Fabric_NodeIPOrFQDN**
* **Fabric_NodeName**
* Fabric_RuntimeConnectionAddress
* Fabric_ServicePackageInstanceId
* Fabric_ServicePackageName
* Fabric_ServicePackageVersionInstance
* FabricPackageFileName

Hello code belows montre comment toolist hello variables d’environnement Service Fabric
 ```csharp
    foreach (DictionaryEntry de in Environment.GetEnvironmentVariables())
    {
        if (de.Key.ToString().StartsWith("Fabric"))
        {
            Console.WriteLine(" Environment variable {0} = {1}", de.Key, de.Value);
        }
    }
```
Hello ci-dessous des exemples de variables d’environnement pour un type d’application appelé `GuestExe.Application` avec un type de service appelé `FrontEndService` sur votre ordinateur de développement local.

* **Fabric_ApplicationName = fabric:/GuestExe.Application**
* **Fabric_CodePackageName = Code**
* **Fabric_Endpoint_FrontEndServiceTypeEndpoint = 80**
* **Fabric_NodeIPOrFQDN = localhost**
* **Fabric_NodeName = _Node_2**

### <a name="application-parameter-files"></a>Fichiers de paramètre d’application
projet d’application Service Fabric Hello peut inclure un ou plusieurs fichiers de paramètres d’application. Chacun d’eux définit des valeurs spécifiques hello pour les paramètres hello qui sont définis dans le manifeste de l’application hello :

```xml
    <!-- ApplicationParameters\Local.xml -->

    <Application Name="fabric:/Application1" xmlns="http://schemas.microsoft.com/2011/01/fabric">
        <Parameters>
            <Parameter Name ="Stateful1_MinReplicaSetSize" Value="3" />
            <Parameter Name="Stateful1_PartitionCount" Value="1" />
            <Parameter Name="Stateful1_TargetReplicaSetSize" Value="3" />
        </Parameters>
    </Application>
```
Par défaut, une nouvelle application contient trois fichiers de paramètres, nommés Local.1Node.xml, Local.5Node.xml et Cloud.xml :

![Fichiers de paramètres d’application dans l’Explorateur de solutions][app-parameters-solution-explorer]

toocreate un fichier de paramètres, simplement copier et coller un et lui donner un nouveau nom.

## <a name="identifying-environment-specific-parameters-during-deployment"></a>Identification des paramètres spécifiques à l’environnement au cours du déploiement
Au moment du déploiement, vous devez tooapply de fichier toochoose hello paramètre approprié à votre application. Vous pouvez le faire via la boîte de dialogue Publier hello dans Visual Studio ou PowerShell.

### <a name="deploy-from-visual-studio"></a>Déploiement depuis Visual Studio
Lorsque vous publiez votre application dans Visual Studio, vous pouvez choisir à partir de la liste de hello des fichiers de paramètres disponibles.

![Choisissez un fichier de paramètres dans la boîte de dialogue Publier hello][publishdialog]

### <a name="deploy-from-powershell"></a>Déploiement depuis PowerShell
Hello `Deploy-FabricApplication.ps1` script PowerShell inclus dans le modèle de projet application hello accepte un profil de publication en tant que paramètre et hello PublishProfile contient un fichier de paramètres de référence toohello application.

  ```PowerShell
    ./Deploy-FabricApplication -ApplicationPackagePath <app_package_path> -PublishProfileFile <publishprofile_path>
  ```

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur certains concepts fondamentaux hello qui sont décrites dans cette rubrique, consultez hello [vue d’ensemble technique du Service Fabric](service-fabric-technical-overview.md). Pour plus d’informations sur les autres fonctionnalités de gestion d’application disponibles dans Visual Studio, consultez la section [Gestion de vos applications de Service Fabric dans Visual Studio](service-fabric-manage-application-in-visual-studio.md).

<!-- Image references -->

[publishdialog]: ./media/service-fabric-manage-multiple-environment-app-configuration/publish-dialog-choose-app-config.png
[app-parameters-solution-explorer]:./media/service-fabric-manage-multiple-environment-app-configuration/app-parameters-in-solution-explorer.png
