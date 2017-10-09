---
title: "aaaUsing Elasticsearch comme un magasin de suivi d’application Service Fabric | Documents Microsoft"
description: "Explique comment les applications de l’infrastructure de Service peuvent utiliser toostore Elasticsearch et Kibana, index et recherche dans les traces d’application (journaux)"
services: service-fabric
documentationcenter: .net
author: karolz-ms
manager: adegeo
editor: 
ms.assetid: e59b0c39-e468-4d9e-b453-d5f2a8ad20d8
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/07/2017
ms.author: karolz@microsoft.com
redirect_url: /azure/service-fabric/service-fabric-diagnostics-event-aggregation-eventflow
ms.openlocfilehash: b5977c54e69319e3caa376e44a02f971b66a3254
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-elasticsearch-as-a-service-fabric-application-trace-store"></a>Utiliser Elasticsearch en tant que magasin de trace d’applications Service Fabric
## <a name="introduction"></a>Introduction
Cet article décrit comment les applications [Azure Service Fabric](https://azure.microsoft.com/documentation/services/service-fabric/) peuvent utiliser **Elasticsearch** et **Kibana** pour le stockage, l’indexation et la recherche de traces d’applications. [Elasticsearch](https://www.elastic.co/guide/index.html) est un moteur de recherche et d’analyse en temps réel open source, distribué et évolutif, qui convient parfaitement à cette tâche. Il peut être installé sur des machines virtuelles Windows ou Linux exécutées dans Microsoft Azure. Elasticsearch peut traiter efficacement les traces *structurées* produites à l’aide de technologies telles que **Event Tracing for Windows (ETW)**.

ETW est utilisé par l’infrastructure de Service runtime toosource des informations de diagnostic (suivi). Il s’agit de hello méthode recommandée pour le Service Fabric applications toosource leurs informations de diagnostic, trop. À l’aide de hello même mécanisme permettant de corrélation entre les suivis fourni par le runtime et fourni par l’application et en fait, résolution des problèmes. Modèles de projet de service Fabric dans Visual Studio incluent une API de journalisation (en fonction de hello .NET **EventSource** classe) qui émet des suivis ETW par défaut. Pour obtenir une vue d’ensemble du traçage d’applications Service Fabric à l’aide d’ETW, consultez [Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md).

Pour les traces hello tooshow dans Elasticsearch, ils ont besoin de toobe capturées au niveau de nœuds de cluster Service Fabric hello en temps réel (pendant l’exécution application hello) et envoyé le point de terminaison tooan Elasticsearch. Il existe deux options principales pour la capture de traces :

* **Capture de traces dans le processus**  
  application Hello, ou plus précisément, les processus de service, est responsable de l’envoi de magasin de trace toohello hello des données de diagnostic (Elasticsearch).
* **Capture de traces hors processus**  
  Un agent séparé est capturer une trace à partir de service hello ou les processus et les envoyer de magasin de trace toohello.

Nous décrivons ci-dessous comment tooset des Elasticsearch sur Azure, traitent les professionnels de l’hello et les inconvénients des deux options de capture et expliquent comment tooconfigure une infrastructure de Service service toosend données tooElasticsearch.

## <a name="set-up-elasticsearch-on-azure"></a>Configurer Elasticsearch sur Azure
Hello tooset de façon plus simple de service de Elasticsearch hello sur Azure s’effectue via [ **modèles Azure Resource Manager**](../azure-resource-manager/resource-group-overview.md). Un [modèle Azure Resource Manager de démarrage rapide pour Elasticsearch](https://github.com/Azure/azure-quickstart-templates/tree/master/elasticsearch) est disponible à partir du référentiel de modèles de démarrage rapide Azure. Ce modèle utilise des comptes de stockage distincts pour les unités d’échelle (groupes de nœuds). Il peut également approvisionner des nœuds client et serveur distincts avec des configurations différentes et divers nombres de disques de données associés.

Ici, nous utilisons un autre modèle, appelé **ES-multiposte** de hello [référentiel des outils de diagnostic Azure](https://github.com/Azure/azure-diagnostics-tools). Ce modèle est toouse plus facile, et il crée un cluster Elasticsearch protégé par l’authentification de base HTTP. Avant de continuer, vous pouvez télécharger hello du référentiel à partir de GitHub tooyour machine (par le clonage du référentiel de hello ou téléchargement d’un fichier zip). modèle de Hello ES-multiposte se trouve dans le dossier hello avec hello même nom.

### <a name="prepare-a-machine-toorun-elasticsearch-installation-scripts"></a>Préparer un ordinateur toorun Elasticsearch des scripts d’installation
Hello plus simple façon toouse hello ES-multiposte modèle est via un script Azure PowerShell fourni appelé `CreateElasticSearchCluster`. toouse ce script, vous devez les modules PowerShell tooinstall et un outil appelé **openssl**. Hello ce dernier est nécessaire pour la création d’une clé SSH qui peut être utilisé tooadminister votre cluster Elasticsearch à distance.

`CreateElasticSearchCluster`script est conçu pour simplifier l’utilisation avec le modèle hello ES-multiposte depuis un ordinateur Windows. Il s’agit de modèle de hello toouse possible sur un ordinateur non-Windows, mais ce scénario est abordée dans cet article hello.

1. Si vous ne l’avez pas déjà fait, installez les [**modules Azure PowerShell**](http://aka.ms/webpi-azps). À l’invite, cliquez sur **Exécuter**, puis sur **Installer**. PowerShell Azure 1.3 (ou une version ultérieure) est requis.
2. Hello **openssl** tool est inclus dans la distribution hello de [ **Git pour Windows**](http://www.git-scm.com/downloads). Si vous ne l’avez pas déjà fait, installez [Git pour Windows](http://www.git-scm.com/downloads) maintenant. (les options d’installation par défaut hello sont OK).
3. En supposant que Git a été installé mais non inclus dans le chemin d’accès de système de hello, ouvrez une fenêtre de Microsoft Azure PowerShell et exécutez hello suivant de commandes :
   
    ```powershell
    $ENV:PATH += ";<Git installation folder>\usr\bin"
    $ENV:OPENSSL_CONF = "<Git installation folder>\usr\ssl\openssl.cnf"
    ```
   
    Remplacez hello `<Git installation folder>` emplacement Git de hello sur votre ordinateur ; valeur par défaut hello est **« C:\Program Files\Git »**. Notez le point-virgule hello au début de hello du chemin d’accès de la première hello.
4. Vérifiez que vous êtes connecté tooAzure (via [ `Add-AzureRmAccount` ](https://msdn.microsoft.com/library/mt619267.aspx) applet de commande) et que vous avez sélectionné les abonnement hello qui doivent être utilisé toocreate votre cluster recherche élastique. Vous pouvez vérifier que l’abonnement sélectionné est correct à l’aide des applets de commande `Get-AzureRmContext` et `Get-AzureRmSubscription`.
5. Si vous n’avez pas déjà fait, accédez hello Active toohello ES-multiposte.

### <a name="run-hello-createelasticsearchcluster-script"></a>Exécutez le script de CreateElasticSearchCluster hello
Avant d’exécuter les script hello, ouvrez hello `azuredeploy-parameters.json` de fichiers et de vérifier ou de fournir des valeurs pour les paramètres du script hello. Hello paramètres suivants est fourni :

| Nom du paramètre | Description |
| --- | --- |
| dnsNameForLoadBalancerIP |nom Hello toocreate utilisé hello visible publiquement nom DNS de cluster de recherche élastique hello (en ajoutant le nom de toohello fourni domaine hello région Azure). Par exemple, si la valeur de ce paramètre est « myBigCluster » et la région Azure hello choisi est ouest des États-Unis, hello résultant nom DNS de cluster de hello est myBigCluster.westus.cloudapp.azure.com. <br /><br />Ce nom sert également de nombreux artefacts associé hello recherche élastique cluster, tels que les noms de nœud de données, un nom de racine. |
| adminUsername |nom Hello du compte d’administrateur hello pour la gestion de cluster de recherche élastique hello (clés SSH correspondantes sont générées automatiquement). |
| dataNodeCount |nombre de Hello de nœuds de cluster de recherche élastique hello. version actuelle de Hello du script de hello ne distingue pas entre les nœuds de données et des requêtes ; tous les nœuds de lire les deux rôles. Nœuds de too3 de valeurs par défaut. |
| dataDiskSize |taille de Hello de disques de données (en Go) qui est allouée à chaque nœud de données. Chaque nœud reçoit 4 disques de données, exclusivement dédié tooElastic service de recherche. |
| region |nom de Hello de région Azure où le cluster de recherche élastique hello doit être situé. |
| esUserName |Hello nom d’utilisateur de l’utilisateur de hello est configuré du cluster de tooES toohave accès (sujet tooHTTP l’authentification de base). Hello et mot de passe ne fait pas partie du fichier de paramètres doit être fourni lorsque `CreateElasticSearchCluster` script est appelé. |
| vmSizeDataNodes |Hello taille de machine virtuelle Azure pour les nœuds de cluster recherche élastique. TooStandard_D2 de valeurs par défaut. |

Vous êtes le script de hello toorun prêt. Exécutez hello de commande suivante :

```powershell
CreateElasticSearchCluster -ResourceGroupName <es-group-name> -Region <azure-region> -EsPassword <es-password>
```

où 

| Nom du paramètre de script | Description |
| --- | --- |
| `<es-group-name>` |nom Hello hello Azure du groupe de ressources qui contient toutes les ressources de cluster recherche élastique. |
| `<azure-region>` |nom Hello Hello région Azure où le cluster de recherche élastique hello doit être créé. |
| `<es-password>` |mot de passe Hello pour hello élastique rechercher un utilisateur. |

> [!NOTE]
> Si vous obtenez une exception NullReferenceException à partir de l’applet de commande Test-AzureResourceGroup de hello, vous avez oublié toolog sur tooAzure (`Add-AzureRmAccount`).
> 
> 

Si vous obtenez une erreur de script de hello en cours d’exécution et que vous déterminez que l’erreur de hello a été provoqué par une valeur de paramètre de modèle incorrect, corrigez le fichier de paramètres hello et réexécutez le script de hello avec un nom de groupe de ressources différent. Vous pouvez également réutiliser hello du même nom de groupe de ressources et script hello hello ancien de nettoyage en ajoutant hello `-RemoveExistingResourceGroup` invocation du script toohello paramètre.

### <a name="result-of-running-hello-createelasticsearchcluster-script"></a>Résultat de l’exécution du script de CreateElasticSearchCluster hello
Une fois que vous exécutez hello `CreateElasticSearchCluster` script, hello suivant artefacts principales sera créé. Pour cet exemple, nous supposons que vous avez utilisé « myBigCluster » en tant que valeur hello Hello `dnsNameForLoadBalancerIP` paramètre et cette région de hello où vous avez créé le cluster de hello est ouest des États-Unis.

| Artefact | Nom, emplacement et remarques |
| --- | --- |
| Clé SSH d’administration à distance |fichier myBigCluster.key (dans le répertoire hello à partir de quels hello CreateElasticSearchCluster a été exécuté). <br /><br />Ce fichier de clé peut être utilisé tooconnect toohello admin nœud et (via le nœud Administration de hello) toodata des nœuds de cluster de hello. |
| Nœud admin |myBigCluster-admin.westus.cloudapp.azure.com  <br /><br />Un ordinateur virtuel dédié pour l’administration à distance du cluster de Elasticsearch--hello uniquement un type qui autorise les connexions SSH externes. Il s’exécute sur hello est du même réseau virtuel que tous les nœuds de cluster Elasticsearch hello, mais ne pas exécuter les services Elasticsearch. |
| Nœuds de données |myBigCluster1... myBigCluster*N* <br /><br />Nœuds de données qui exécutent les services Elasticsearch et Kibana. Vous pouvez vous connecter via SSH tooeach nœud, mais uniquement via le nœud Administration de hello. |
| Cluster Elasticsearch |http://myBigCluster.westus.cloudapp.azure.com/es/ <br /><br />point de terminaison principal Hello pour cluster de Elasticsearch hello (suffixe de /es Remarque hello). Il est protégé par l’authentification HTTP de base (informations d’identification hello étaient hello spécifié esUserName/esPassword des paramètres de modèle de hello multiposte-ES). Hello cluster possède également hello head plug-in installé (http://myBigCluster.westus.cloudapp.azure.com/es/_plugin/head) pour l’administration du cluster de base. |
| Service Kibana |http://myBigCluster.westus.cloudapp.azure.com <br /><br />Hello Kibana service tooshow données est définie à partir de hello créé Elasticsearch cluster. Il est protégé par hello mêmes informations d’identification de l’authentification en tant que hello du cluster lui-même. |

## <a name="in-process-versus-out-of-process-trace-capturing"></a>Comparaison de la collecte de traces dans le processus et hors processus
Dans l’introduction de hello, nous l’avons mentionné deux méthodes fondamentales de la collecte de données de diagnostic : intra-processus et out-of-process. Chacune de ces méthodes présente ses propres avantages et inconvénients.

Avantages de hello **capture de trace dans le processus** incluent :

1. *Simplicité de configuration et de déploiement*
   
   * configuration de Hello de collecte de données de diagnostic est simplement dans le cadre de la configuration de l’application hello. Il s’agit de conserver facilement tooalways « synchronisé » avec hello il le reste de l’application hello.
   * Vous pouvez facilement réaliser une configuration par application ou par service.
   * Out-of-process trace capture nécessite généralement un déploiement séparé et la configuration de l’agent de diagnostic hello, qui est une tâche administrative supplémentaire et une source potentielle d’erreurs. technologie d’agent particulier Hello permet souvent qu’une seule instance de l’agent de hello par l’ordinateur virtuel (nœud). Cela signifie que la configuration de la collection hello de configuration de diagnostic hello est partagée entre toutes les applications et services qui s’exécutent sur ce nœud.
2. *Flexibilité*
   
   * application Hello peut envoyer des données de hello qu’elle puisse toogo, tant qu’il existe une bibliothèque de client qui prend en charge le système de stockage de données hello ciblé. Vous pouvez ajouter de nouveaux récepteurs si vous le souhaitez.
   * Vous pouvez également implémenter des règles de capture, de filtrage et d’agrégation de données complexes.
   * Capture d’une trace d’out-of-process est souvent limitée par les récepteurs de données hello hello prend en charge de l’agent. Certains agents sont extensibles.
3. *Contexte et des données d’application toointernal accès*
   
   * sous-système de diagnostic Hello en cours d’exécution à l’intérieur du processus de service ou application hello peut accroître facilement les traces hello avec des informations contextuelles.
   * Dans l’approche d’out-of-process hello, hello données doivent être envoyées agent tooan via un mécanisme de communication entre processus, tels que le suivi d’événements pour Windows. Ce mécanisme peut imposer des limites supplémentaires.

Avantages de hello **out-of-process trace capture** incluent :

1. *Hello capacité toomonitor hello application et collecter les vidages sur incident*
   
   * Dans le processus trace capture peut être échoue si l’application hello échoue toostart ou tombe en panne. Un agent indépendant a beaucoup plus de chance de capturer des informations de dépannage cruciales.<br /><br />
2. *Maturité, fiabilité et performances éprouvées*
   
   * Un agent développé par un fournisseur de plate-forme (par exemple, un agent Microsoft Azure Diagnostics) a été toorigorous sujet renforcement de nom et de test.
   * Avec la trace dans le processus capture, il convient tooensure qu’activité hello d’envoi de données de diagnostic à partir d’un processus d’application ne pas interférer avec les tâches principales de l’application hello ou introduire des problèmes de synchronisation ou de performances. Un agent de manière indépendante en cours d’exécution est moins susceptible d’engendrer des problèmes de toothese et spécifiquement conçue toolimit son impact sur le système de hello.

Il est possible de toocombine et tirent parti de ces deux approches. En effet, il peut être la meilleure solution hello pour de nombreuses applications.

Ici, nous utilisons hello **Microsoft.Diagnostic.Listeners bibliothèque** et hello intra-processus trace de la capture de données toosend à partir d’un cluster de Service Fabric application tooan Elasticsearch.

## <a name="use-hello-listeners-library-toosend-diagnostic-data-tooelasticsearch"></a>Utilisez tooElasticsearch de données de diagnostic toosend hello écouteurs de la bibliothèque
bibliothèque de Microsoft.Diagnostic.Listeners Hello fait partie de l’exemple d’application de Service Fabric PartyCluster. toouse il :

1. Télécharger [hello PartyCluster exemple](https://github.com/Azure-Samples/service-fabric-dotnet-management-party-cluster) à partir de GitHub.
2. Copier projets hello Microsoft.Diagnostics.Listeners et Microsoft.Diagnostics.Listeners.Fabric (dossiers entières) hello PartyCluster Active toohello solution dossier d’exemples d’application hello supposée toosend hello données tooElasticsearch .
3. Ouvrez la solution de cible de hello, cliquez sur le nœud de la solution dans l’Explorateur de solutions de hello hello et choisissez **ajouter un projet existant**. Ajoutez le projet toohello solution hello Microsoft.Diagnostics.Listeners. Répétez même hello pour le projet de Microsoft.Diagnostics.Listeners.Fabric hello.
4. Ajouter une référence de projet à partir de vos projets toohello deux ajouté projets de service. (Chaque service qui est supposé toosend données tooElasticsearch doit référencer Microsoft.Diagnostics.EventListeners et Microsoft.Diagnostics.EventListeners.Fabric).
   
    ![TooMicrosoft.Diagnostics.EventListeners de références de projet et les bibliothèques Microsoft.Diagnostics.EventListeners.Fabric][1]

### <a name="service-fabric-general-availability-release-and-microsoftdiagnosticstracing-nuget-package"></a>Disponibilité générale de la version de Service Fabric et package NuGet Microsoft.Diagnostics.Tracing
Les applications créées avec version à disponibilité générale de Service Fabric (2.0.135, publiée le 31 mars 2016) ciblent **.NET Framework 4.5.2**. Cette version est la version la plus récente de hello Hello .NET Framework pris en charge par Azure lors de mise en production hello GA hello. Malheureusement, cette version de framework de hello ne dispose pas de certaines APIs EventListener que hello Microsoft.Diagnostics.Listeners a besoin de bibliothèque. Étant donné que EventSource (composant hello base hello de journalisation de l’API dans les applications de l’infrastructure) et EventListener sont étroitement liés, chaque projet qui utilise la bibliothèque de Microsoft.Diagnostics.Listeners hello doit utiliser une autre implémentation de EventSource. Cette implémentation est fournie par hello **package Nuget de Microsoft.Diagnostics.Tracing**, créés par Microsoft. package de Hello est entièrement compatible avec la source d’événement inclus dans le cadre de hello, aucune modification de code ne doit donc être nécessaire que les modifications de l’espace de noms référencé.

toostart à l’aide de la mise en œuvre de Microsoft.Diagnostics.Tracing hello de classe EventSource de hello, procédez comme suit pour chaque projet de service qui doit toosend données tooElasticsearch :

1. Avec le bouton droit sur le projet de service hello et choisissez **gérer les Packages Nuget**.
2. Basculer la source du package toohello nuget.org (si ce n’est pas déjà fait) et recherchez «**Microsoft.Diagnostics.Tracing**».
3. Installer hello `Microsoft.Diagnostics.Tracing.EventSource` package (et ses dépendances).
4. Ouvrez hello **ServiceEventSource.cs** ou **ActorEventSource.cs** dans votre projet de service et remplacez hello `using System.Diagnostics.Tracing` directive sur fichier hello avec hello `using Microsoft.Diagnostics.Tracing` directive.

Ces étapes ne sera pas nécessaires qu’une seule fois hello **.NET Framework 4.6** est pris en charge par Microsoft Azure.

### <a name="elasticsearch-listener-instantiation-and-configuration"></a>Instanciation et configuration de l’écouteur Elasticsearch
Hello dernière étape pour l’envoi de données de diagnostic tooElasticsearch est toocreate une instance de `ElasticSearchListener` et configurez-le avec les données de connexion Elasticsearch. écouteur de Hello capture automatiquement tous les événements déclenchés via les classes EventSource définies dans le projet de service hello. Il nécessitant toobe actif pendant la durée de vie hello du service de hello, hello meilleures placer toocreate il se trouve dans le code d’initialisation service hello. Voici comment le code d’initialisation hello pour un service sans état pourrait ressembler après les modifications nécessaires hello (ajouts décrites dans les commentaires commençant par `****`) :

```csharp
using System;
using System.Diagnostics;
using System.Fabric;
using System.Threading;
using System.Threading.Tasks;
using Microsoft.ServiceFabric.Services.Runtime;

// **** Add hello following directives
using Microsoft.Diagnostics.EventListeners;
using Microsoft.Diagnostics.EventListeners.Fabric;

namespace Stateless1
{
    internal static class Program
    {
        /// <summary>
        /// This is hello entry point of hello service host process.
        /// </summary>        
        private static void Main()
        {
            try
            {
                // **** Instantiate ElasticSearchListener
                var configProvider = new FabricConfigurationProvider("ElasticSearchEventListener");
                ElasticSearchListener esListener = null;
                if (configProvider.HasConfiguration)
                {
                    esListener = new ElasticSearchListener(configProvider, new FabricHealthReporter("ElasticSearchEventListener"));
                }

                // hello ServiceManifest.XML file defines one or more service type names.
                // Registering a service maps a service type name tooa .NET type.
                // When Service Fabric creates an instance of this service type,
                // an instance of hello class is created in this host process.

                ServiceRuntime.RegisterServiceAsync("Stateless1Type", 
                    context => new Stateless1(context)).GetAwaiter().GetResult();

                ServiceEventSource.Current.ServiceTypeRegistered(Process.GetCurrentProcess().Id, typeof(Stateless1).Name);

                // Prevents this host process from terminating so services keep running.
                Thread.Sleep(Timeout.Infinite);

                // **** Ensure that hello ElasticSearchListner instance is not garbage-collected prematurely
                GC.KeepAlive(esListener);
            }
            catch (Exception e)
            {
                ServiceEventSource.Current.ServiceHostInitializationFailed(e);
                throw;
            }
        }
    }
}
```

Les données de connexion Elasticsearch doivent être placées dans une section distincte dans le fichier de configuration de service hello (**PackageRoot\Config\Settings.xml**). nom Hello de section de hello doit correspondre à valeur toohello passé toohello `FabricConfigurationProvider` constructeur, par exemple :

```xml
<Section Name="ElasticSearchEventListener">
  <Parameter Name="serviceUri" Value="http://myBigCluster.westus.cloudapp.azure.com/es/" />
  <Parameter Name="userName" Value="(ES user name)" />
  <Parameter Name="password" Value="(ES user password)" />
  <Parameter Name="indexNamePrefix" Value="myapp" />
</Section>
```
Hello des valeurs de `serviceUri`, `userName` et `password` paramètres correspondent adresse de point de terminaison du cluster toohello Elasticsearch Elasticsearch nom d’utilisateur et mot de passe, respectivement. `indexNamePrefix`est le préfixe hello pour les index de Elasticsearch ; bibliothèque de Microsoft.Diagnostics.Listeners Hello crée un nouvel index pour ses données tous les jours.

### <a name="verification"></a>Vérification
Et voilà ! Maintenant, chaque fois que le service de hello est exécuté, il commence à envoyer des traces toohello Elasticsearch de service spécifié dans la configuration de hello. Vous pouvez le vérifier en hello ouverture que kibana UI associé avec l’instance de Elasticsearch hello cible. Dans notre exemple, adresse de la page hello est http://myBigCluster.westus.cloudapp.azure.com/. Vérifiez que les index avec le préfixe de nom hello choisi pour hello `ElasticSearchListener` instance effectivement ont été créés et remplis avec des données.

![Kibana affichant des événements d’application du cluster Party][2]

## <a name="next-steps"></a>Étapes suivantes
* [En savoir plus sur le diagnostic et la surveillance d’un service Fabric Service](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

<!--Image references-->
[1]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/listener-lib-references.png
[2]: ./media/service-fabric-diagnostics-how-to-use-elasticsearch/kibana.png
