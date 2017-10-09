---
title: aaaConvert toomicroservices des applications de Services de cloud computing Azure | Documents Microsoft
description: "Ce guide compare Web des Services de Cloud et rôles de travail et l’infrastructure de Service sans état services toohelp migrent à partir des Services de cloud computing tooService l’ensemble fibre optique."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: 5880ebb3-8b54-4be8-af4b-95a1bc082603
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: c43b11623b2ba7f6069782a8b7e030c82572a6e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="guide-tooconverting-web-and-worker-roles-tooservice-fabric-stateless-services"></a>Guide tooconverting rôles Web et Worker tooService sans état services de Fabric
Cet article décrit comment toomigrate votre Web des Services de Cloud et les rôles de travail tooService sans état services de Fabric. Il s’agit de hello la plus simple de migration à partir des Services de cloud computing tooService l’infrastructure pour les applications dont l’architecture globale est en train de toostay à peu près hello identiques.

## <a name="cloud-service-project-tooservice-fabric-application-project"></a>Projet d’application de Service project tooService l’infrastructure de cloud computing
 Un projet de Service Cloud et un projet d’Application de l’infrastructure de Service ont une structure similaire et les deux unités de déploiement représentent hello pour votre application : autrement dit, elles définissent complète hello est toorun déployé votre application. Un projet de service cloud contient un ou plusieurs rôles web ou de travail. De la même façon, un projet d’application Service Fabric regroupe un ou plusieurs services. 

Hello différence est que couples de projet de Service Cloud hello hello du déploiement d’applications avec un déploiement de machine virtuelle et contient donc les paramètres de configuration de machine virtuelle, tandis que le projet d’Application Service Fabric hello définit seulement une application qui sera déployée tooa l’ensemble des machines virtuelles existantes dans un cluster Service Fabric. cluster Service Fabric de Hello lui-même est uniquement déployé une fois, via un modèle de gestionnaire de ressources ou via hello portail Azure et plusieurs Service Fabric, les applications peuvent être déploiement tooit.

![Comparaison de projet entre Service Fabric et les services cloud][3]

## <a name="worker-role-toostateless-service"></a>Service de toostateless de rôle de travail
Point de vue conceptuel, un rôle de travail représente une charge de travail sans état, ce qui signifie que chaque instance de la charge de travail hello est identique et de requêtes peuvent être routé tooany instance à tout moment. Chaque instance n’est pas demande précédente de hello tooremember attendu. État de cette charge de travail hello opère sur est géré par un magasin d’état externe, telles que le stockage Azure Table ou de la base de données de Document Azure. Dans Service Fabric, ce type de charge de travail est représenté par un service sans état. Hello toomigrating d’approche la plus simple un tooService de rôle de travail Fabric est possible en convertissant le rôle de travail code tooa Service sans état.

![Rôle de travail tooStateless Service][4]

## <a name="web-role-toostateless-service"></a>Rôle toostateless service Web
TooWorker similaire rôle, un rôle Web représente également une charge de travail sans état, et donc conceptuellement il peut aussi être mappé tooa service sans état du Service Fabric. Toutefois, contrairement aux rôles web, Service Fabric ne prend pas en charge les IIS. toomigrate une application web à partir d’un service sans état tooa de rôle Web nécessite la première infrastructure web tooa mobile qui permettre être auto-hébergés et ne dépend pas d’IIS ou System.Web, telles que ASP.NET Core 1.

| **Application** | **Pris en charge** | **Chemin de migration** |
| --- | --- | --- |
| Formulaires web ASP.NET |Non |Convertir tooASP.NET 1 MVC de base |
| ASP.NET MVC |Avec migration |TooASP.NET mise à niveau de base 1 MVC |
| API Web ASP.NET |Avec migration |Utiliser un serveur auto-hébergé ou ASP.NET Core 1 |
| ASP.NET Core 1 |Oui |N/A |

## <a name="entry-point-api-and-lifecycle"></a>API de point d’entrée et cycle de vie
Les points d’entrée des API de rôle de travail et de Service Fabric sont semblables : 

| **Point d’entrée** | **Instances de** | **Service Service Fabric** |
| --- | --- | --- |
| Traitement en cours |`Run()` |`RunAsync()` |
| Démarrer la machine virtuelle |`OnStart()` |N/A |
| Arrêter la machine virtuelle |`OnStop()` |N/A |
| Ouvrir l’écouteur pour les requêtes du client |N/A |<ul><li> Sans état : `CreateServiceInstanceListener()`</li><li>Avec état : `CreateServiceReplicaListener()`</li></ul> |

### <a name="worker-role"></a>Instances de
```C#

using Microsoft.WindowsAzure.ServiceRuntime;

namespace WorkerRole1
{
    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
        }

        public override bool OnStart()
        {
        }

        public override void OnStop()
        {
        }
    }
}

```

### <a name="service-fabric-stateless-service"></a>Services sans état Service Fabric
```C#

using System.Collections.Generic;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Communication.Runtime;
using Microsoft.ServiceFabric.Services.Runtime;

namespace Stateless1
{
    public class Stateless1 : StatelessService
    {
        protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
        {
        }

        protected override Task RunAsync(CancellationToken cancelServiceInstance)
        {
        }
    }
}

```

Dans lequel la transformation toobegin ont un remplacement principal « exécuter ». Les services Service Fabric associent `Run`, `Start` et `Stop` en un point d’entrée unique, `RunAsync`. Votre service doit commencer à travailler lorsque `RunAsync` démarre et doit cesser de fonctionner lorsque hello `RunAsync` CancellationToken de la méthode est signalé. 

Il existe plusieurs différences importantes entre hello du cycle de vie et la durée de vie des services de rôles de travail et l’infrastructure de Service :

* **Cycle de vie :** plus grande différence de hello est qu’un rôle de travail est un ordinateur virtuel et par conséquent, leur cycle de vie est liée toohello machine virtuelle, qui inclut les événements de lorsque hello machine virtuelle démarre et arrête. Un service Service Fabric a un cycle de vie qui est distinct de cycle de vie de machine virtuelle hello, donc il n’inclut pas les événements pour lorsque hello hôte des ordinateurs virtuels ou de démarrage de la machine et de fin, car elles ne sont pas liées.
* **Durée de vie :** une instance de rôle de travail sera recyclé si hello `Run` issues de la méthode. Hello `RunAsync` méthode dans un service Service Fabric toutefois peut s’exécuter toocompletion et reste de l’instance de service hello. 

Service Fabric fournit un point d’entrée de configuration de la communication en option pour les services qui écoutent les requêtes des clients. Hello RunAsync et point d’entrée de communication sont des remplacements facultatif dans les services de l’infrastructure de Service - votre service peut choisir des demandes d’écoute tooclient tooonly, ou uniquement exécuter une boucle de traitement, ou les deux - c’est pourquoi hello RunAsync méthode est autorisée tooexit sans redémarrer l’instance de service de hello, car il peut continuer toolisten pour les demandes du client.

## <a name="application-api-and-environment"></a>API d’application et environnement
environnement de Services de cloud computing Hello API fournit des informations et des fonctionnalités d’instance de machine virtuelle en cours hello, ainsi que des informations sur les autres instances de rôle de machine virtuelle. L’infrastructure de service fournit des informations connexes tooits runtime et des informations sur le nœud hello un service sont en cours d’exécution. 

| **Tâche d’environnement** | **Cloud Services** | **Service Fabric** |
| --- | --- | --- |
| Paramètres de configuration et notification de modification |`RoleEnvironment` |`CodePackageActivationContext` |
| Stockage local |`RoleEnvironment` |`CodePackageActivationContext` |
| Informations sur le point de terminaison |`RoleInstance` <ul><li>Instance actuelle : `RoleEnvironment.CurrentRoleInstance`</li><li>Autres rôles et instances : `RoleEnvironment.Roles`</li> |<ul><li>`NodeContext` pour l’adresse du nœud actuel</li><li>`FabricClient` et `ServicePartitionResolver` pour la découverte de point de terminaison de service</li> |
| Émulation de l’environnement |`RoleEnvironment.IsEmulated` |N/A |
| Événement de modification simultanée |`RoleEnvironment` |N/A |

## <a name="configuration-settings"></a>Paramètres de configuration
Paramètres de configuration dans les Services de cloud computing sont définies pour un rôle d’ordinateur virtuel et appliquent tooall des instances de ce rôle de machine virtuelle. Ces paramètres correspondent à des paires clé-valeur définies dans les fichiers ServiceConfiguration.*.cscfg. Ils sont accessibles directement via RoleEnvironment. Dans l’infrastructure de Service, paramètres s’appliquent individuellement tooeach service et application de tooeach, plutôt que tooa machine virtuelle, car une machine virtuelle peut héberger plusieurs services et applications. Un service se compose de trois packages :

* **Code :** contient les exécutables du service hello, les fichiers binaires, les DLL et tous les autres fichiers toorun a besoin d’un service.
* **Config :** tous les fichiers de configuration et les paramètres d’un service.
* **Données :** les fichiers de données statiques associés hello service.

Chacun de ces packages peut être individuellement mis à niveau et faire l’objet d’un contrôle de version indépendant. Services tooCloud similaires, un package de configuration sont accessibles par programme via une API et les événements sont des services de hello toonotify disponibles d’une modification de package de configuration. Un fichier Settings.xml peut être utilisé pour la configuration de la clé-valeur et de l’accès par programme toohello application paramètres section similaire d’un fichier App.config. Toutefois, contrairement aux services cloud, les packages de configuration Service Fabric peuvent contenir des fichiers de configuration à n’importe quel format : XML, JSON, YAML ou tout format binaire personnalisé. 

### <a name="accessing-configuration"></a>Accès à la configuration
#### <a name="cloud-services"></a>Cloud Services
Les paramètres de configuration de ServiceConfiguration.*.cscfg sont accessibles par le biais de `RoleEnvironment`. Ces paramètres sont des instances de rôle tooall globalement disponible Bonjour même déploiement de Service Cloud.

```C#

string value = RoleEnvironment.GetConfigurationSettingValue("Key");

```

#### <a name="service-fabric"></a>Service Fabric
Chaque service dispose de son propre package de configuration individuel. Il n’existe aucun mécanisme intégré permettant à toutes les applications d’un cluster d’accéder à l’ensemble des paramètres de configuration. Lorsque vous utilisez le fichier de configuration de Settings.xml spéciaux de l’infrastructure de Service au sein d’un package de configuration, les valeurs dans Settings.xml peuvent être remplacés au niveau d’application hello, ce qui rend les paramètres de configuration de niveau application possible.

Paramètres de configuration sont accède au sein de chaque instance de service par le biais du service hello `CodePackageActivationContext`.

```C#

ConfigurationPackage configPackage = this.Context.CodePackageActivationContext.GetConfigurationPackageObject("Config");

// Access Settings.xml
KeyedCollection<string, ConfigurationProperty> parameters = configPackage.Settings.Sections["MyConfigSection"].Parameters;

string value = parameters["Key"]?.Value;

// Access custom configuration file:
using (StreamReader reader = new StreamReader(Path.Combine(configPackage.Path, "CustomConfig.json")))
{
    MySettings settings = JsonConvert.DeserializeObject<MySettings>(reader.ReadToEnd());
}

```

### <a name="configuration-update-events"></a>Événements de mise à jour de la configuration
#### <a name="cloud-services"></a>Services cloud
Hello `RoleEnvironment.Changed` événement est utilisé toonotify toutes les instances de rôle lorsqu’une modification se produit dans l’environnement de hello, tels qu’un changement de configuration. Il s’agit de mises à jour de la configuration tooconsume utilisé sans le recyclage des instances de rôle ou le redémarrage d’un processus de travail.

```C#

RoleEnvironment.Changed += RoleEnvironmentChanged;

private void RoleEnvironmentChanged(object sender, RoleEnvironmentChangedEventArgs e)
{
   // Get hello list of configuration changes
   var settingChanges = e.Changes.OfType<RoleEnvironmentConfigurationSettingChange>();
foreach (var settingChange in settingChanges) 
   {
      Trace.WriteLine("Setting: " + settingChange.ConfigurationSettingName, "Information");
   }
}

```

#### <a name="service-fabric"></a>Service Fabric
Chacun des trois types de package hello dans un service de Code, configuration et données - possèdent des événements qui notifier une instance de service lorsqu’un package est mis à jour, ajouté ou supprimé. Un service peut contenir plusieurs packages de chaque type. Par exemple, un service peut avoir plusieurs packages de configuration, chacun pouvant être géré et mis à niveau individuellement. 

Ces événements sont des modifications tooconsume disponible dans les packages de service sans avoir à redémarrer l’instance de service hello.

```C#

this.Context.CodePackageActivationContext.ConfigurationPackageModifiedEvent +=
                    this.CodePackageActivationContext_ConfigurationPackageModifiedEvent;

private void CodePackageActivationContext_ConfigurationPackageModifiedEvent(object sender, PackageModifiedEventArgs<ConfigurationPackage> e)
{
    this.UpdateCustomConfig(e.NewPackage.Path);
    this.UpdateSettings(e.NewPackage.Settings);
}

```

## <a name="startup-tasks"></a>Tâches de démarrage
Les tâches de démarrage sont des actions effectuées avant le démarrage d’une application. Une tâche de démarrage est généralement utilisées toorun les scripts de configuration avec des privilèges élevés. Les services cloud et Service Fabric prennent tous deux en charge les tâches de démarrage. Hello principale différence est que dans Services de cloud computing, une tâche de démarrage est liée tooa machine virtuelle, car il fait partie d’une instance de rôle, alors que le Service fabric une tâche de démarrage est service tooa liée, ce qui n’est pas liée tooany machine virtuelle particulière.

| Services cloud | Service Fabric |
| --- | --- | --- |
| Emplacement de la configuration |ServiceDefinition.csdef |
| Privilèges |« limités » ou « élevés » |
| Séquencement |« simple », « en arrière-plan », « au premier plan » |

### <a name="cloud-services"></a>Services cloud
Dans les services cloud, un point d’entrée de démarrage est configuré pour chaque rôle dans le fichier ServiceDefinition.csdef. 

```xml

<ServiceDefinition>
    <Startup>
        <Task commandLine="Startup.cmd" executionContext="limited" taskType="simple" >
            <Environment>
                <Variable name="MyVersionNumber" value="1.0.0.0" />
            </Environment>
        </Task>
    </Startup>
    ...
</ServiceDefinition>

```

### <a name="service-fabric"></a>Service Fabric
Dans Service Fabric, un point d’entrée de démarrage est configuré pour chaque service dans le fichier ServiceManifest.xml :

```xml

<ServiceManifest>
  <CodePackage Name="Code" Version="1.0.0">
    <SetupEntryPoint>
      <ExeHost>
        <Program>Startup.bat</Program>
      </ExeHost>
    </SetupEntryPoint>
    ...
</ServiceManifest>

``` 

## <a name="a-note-about-development-environment"></a>Remarque sur l’environnement de développement
Services Cloud et le Service Fabric sont intégrés à Visual Studio avec des modèles de projet et la prise en charge pour le débogage, la configuration et le déployer à la fois localement et tooAzure. Les services cloud et Service Fabric fournissent également tous deux un environnement local d’exécution de développement. Hello différence est que pendant que le Service de cloud computing développement runtime émule hello hello environnement Azure sur lequel il s’exécute, Service Fabric n’utilise pas un émulateur - elle utilise le runtime Service Fabric complète de hello. Hello Service Fabric est de l’environnement que vous exécutez sur votre ordinateur de développement local hello même environnement qui s’exécute en production.

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur le Service de l’infrastructure des Services fiables et hello différences fondamentales existant entre les Services de Cloud et le Service Fabric application architecture toounderstand définition parti tootake Hello complète des fonctionnalités de l’infrastructure de Service.

* [Découvrir les services fiables Service Fabric](service-fabric-reliable-services-quick-start.md)
* [Différences de toohello guide conceptuelle entre les Services de cloud computing et le Service Fabric](service-fabric-cloud-services-migration-differences.md)

<!--Image references-->
[3]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/service-fabric-cloud-service-projects.png
[4]: ./media/service-fabric-cloud-services-migration-worker-role-stateless-service/worker-role-to-stateless-service.png
