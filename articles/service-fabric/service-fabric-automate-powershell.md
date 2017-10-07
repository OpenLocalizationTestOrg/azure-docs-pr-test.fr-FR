---
title: aaaAutomate gestion des applications Azure Service Fabric | Documents Microsoft
description: "Déployer, mettre à niveau, tester et supprimer des applications Service Fabric à l’aide de PowerShell."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: f03f4294-571d-4262-8a77-cc8b481b959d
ms.service: service-fabric
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 06/16/2017
ms.author: ryanwi
redirect_url: /azure/service-fabric/service-fabric-deploy-remove-applications
ms.openlocfilehash: a64a39dbee26be8ac15fee767a90fd06bfe4b896
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="automate-hello-application-lifecycle-using-powershell"></a>Automatiser le cycle de vie application hello à l’aide de PowerShell
Plusieurs aspects de hello [cycle de vie application Service Fabric](service-fabric-application-lifecycle.md) peut être automatisée.  Cet article présente des tâches de toouse PowerShell tooautomate commun pour le déploiement, la mise à niveau, supprimer et tester des applications d’Azure Service Fabric.  Des API gérées et HTTP pour la gestion de l’application sont également disponibles. Consultez la rubrique [Cycle de vie de l’application](service-fabric-application-lifecycle.md) pour plus d’informations.  

## <a name="prerequisites"></a>Composants requis
Avant de passer les tâches toohello dans l’article de hello, veillez à :

* Se familiariser avec les concepts de Service Fabric hello décrits dans [une vue d’ensemble technique du Service Fabric](service-fabric-technical-overview.md).
* [Installer le runtime de hello, Kit de développement logiciel et les outils](service-fabric-get-started.md), qui est également installé hello **ServiceFabric** module PowerShell.
* [Activer l'exécution du script PowerShell](service-fabric-get-started.md#enable-powershell-script-execution).
* Démarrer un cluster local.  Lancer une nouvelle fenêtre PowerShell en tant qu’administrateur, puis exécutez script d’installation de cluster hello à partir du dossier du Kit de développement logiciel hello :`& "$ENV:ProgramFiles\Microsoft SDKs\Service Fabric\ClusterSetup\DevClusterSetup.ps1"`
* Avant d’exécuter les commandes PowerShell dans cet article, connectez-vous d’abord cluster Service Fabric local de toohello à l’aide de [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps):`Connect-ServiceFabricCluster localhost:19000`
* Bonjour tâches suivantes nécessite une toodeploy de package d’application v1 et v2 d’un package d’application pour la mise à niveau. Télécharger hello [ **WordCount** exemple d’application](http://aka.ms/servicefabricsamples) (situé dans les exemples de prise en main de hello). Générer et empaqueter l’application hello dans Visual Studio (avec le bouton droit sur **WordCount** dans l’Explorateur de solutions, puis sélectionnez **Package**). Copier le package v1 hello dans `C:\ServiceFabricSamples\Services\WordCount\WordCount\pkg\Debug` trop`C:\Temp\WordCount`. Copie `C:\Temp\WordCount` trop`C:\Temp\WordCountV2`, création de package d’application hello v2 pour la mise à niveau. Ouvrez `C:\Temp\WordCountV2\ApplicationManifest.xml` dans un éditeur de texte. Bonjour **ApplicationManifest** élément, de modification hello **ApplicationTypeVersion** trop d’attributs à partir de « 1.0.0 » « 2.0.0 » numéro de version d’application tooupdate hello. Enregistrez le fichier de ApplicationManifest.xml de hello modifié.

## <a name="task-deploy-a-service-fabric-application"></a>Tâche : déployer une application Service Fabric
Après avoir généré et empaqueté application hello (ou téléchargé le package d’application hello), vous pouvez déployer l’application hello dans un cluster Service Fabric local. Le déploiement implique le téléchargement du package d’application hello, l’enregistrement du type d’application hello et création d’instance de l’application hello. Utilisez les instructions de hello dans cette section de toodeploy un nouveau cluster de tooa d’application.

### <a name="step-1-upload-hello-application-package"></a>Étape 1 : Télécharger le package d’application hello
Téléchargement toohello de package d’application hello magasin d’images place dans un emplacement accessible toointernal Service Fabric de composants.  package d’application Hello contient hello nécessaire manifeste d’application, les manifestes de service et le code, configuration et application de données ou les modules toocreate hello et instances de service. Si vous souhaitez que le package d’application hello tooverify localement, utilisez hello [ServiceFabricApplicationPackage-Test](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) applet de commande.  Hello [ServiceFabricApplicationPackage de copie](/powershell/module/servicefabric/copy-servicefabricapplicationpackage?view=azureservicefabricps) commande téléchargements hello package. Par exemple :

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCount\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

### <a name="step-2-register-hello-application-type"></a>Étape 2 : Inscrire le type d’application hello
Le package d’application hello inscription rend type d’application hello et version déclarées dans le manifeste de l’application hello disponible pour la. système de Hello lit package hello téléchargé à l’étape de hello 1, vérifiez le package de hello (équivalent toorunning [ServiceFabricApplicationPackage-Test](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) localement), traiter le contenu du package hello et copiez tooan du package hello traité emplacement du système interne.  Exécutez hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) applet de commande :

```powershell
Register-ServiceFabricApplicationType WordCount
```
toosee tous les types d’application hello inscrit dans le cluster hello, exécutez hello [Get-ServiceFabricApplicationType](/powershell/module/servicefabric/get-servicefabricapplicationtype?view=azureservicefabricps) applet de commande :

```powershell
Get-ServiceFabricApplicationType
```

### <a name="step-3-create-hello-application-instance"></a>Étape 3 : Créer l’instance de l’application hello
Une application peut être instanciée à l’aide de n’importe quelle version de type d’application qui a été inscrit avec succès à l’aide de hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) commande. nom Hello de chaque application est déclarée au niveau du déploiement et doit commencer par hello **fabric :** schéma et être unique pour chaque instance d’application. Hello type nom et la version de type d’application sont déclarées dans hello **ApplicationManifest.xml** fichier du package d’application hello. Si tous les services par défaut ont été définies dans le manifeste de l’application hello du type d’application cible hello, celles sont créés pour l’instant.

```powershell
New-ServiceFabricApplication fabric:/WordCount WordCount 1.0.0
```

Hello [Get-ServiceFabricApplication](/powershell/servicefabric/vlatest/get-servicefabricapplication) commande répertorie toutes les instances d’application qui ont été créés, ainsi que leur état global. Hello [Get-ServiceFabricService](/powershell/module/servicefabric/get-servicefabricservice?view=azureservicefabricps) commande répertorie toutes les instances de service hello qui ont été créés dans une instance d’une application donnée. Les services par défaut (le cas échéant) sont répertoriés.

```powershell
Get-ServiceFabricApplication

Get-ServiceFabricApplication | Get-ServiceFabricService
```

## <a name="task-upgrade-a-service-fabric-application"></a>Tâche : mettre à niveau une application Service Fabric
Vous pouvez mettre à niveau une application Service Fabric précédemment déployée avec un package d’application mis à jour. Cette tâche met à niveau l’application WordCount hello qui a été déployée dans « tâche : déployer une application de Service Fabric. » Consultez le [didacticiel sur la mise à niveau d'une application Service Fabric](service-fabric-application-upgrade.md) pour plus d’informations.

tookeep plus simple pour cet exemple, uniquement hello application numéro de version a été mis à jour dans le package d’application hello WordCountV2 créé dans les conditions préalables de hello. Un scénario plus réaliste impliquerait vos fichiers de code, de configuration ou de données du service de mise à jour puis la reconstruction et empaquetage d’application hello avec des numéros de version mise à jour.  

### <a name="step-1-upload-hello-updated-application-package"></a>Étape 1 : Télécharger le package de mise à jour d’application hello
Hello WordCount v1 application est prête toobe mis à niveau. Si vous ouvrez une fenêtre PowerShell en tant qu’administrateur et tapez [ **Get-ServiceFabricApplication**](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), vous voyez que la version 1.0.0 de hello WordCount type d’application est déployée.  

Maintenant, hello de la copie mise à jour application package toohello Service Fabric magasin d’images (où les packages d’application hello sont enregistrées par l’infrastructure de Service). Hello paramètre **ApplicationPackagePathInImageStore** informe l’infrastructure de Service dans lequel il peut trouver le package d’application hello. Hello commande copies hello package d’application trop suivante**WordCountV2** dans le magasin d’images hello :  

```powershell
Copy-ServiceFabricApplicationPackage C:\Temp\WordCountV2\ -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCountV2

```
### <a name="step-2-register-hello-updated-application-type"></a>Étape 2 : Inscrire hello mise à jour de type d’application
étape suivante Hello est tooregister hello nouvelle version de l’application hello avec Service Fabric, ce qui peut être effectuée à l’aide de hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) applet de commande :

```powershell
Register-ServiceFabricApplicationType WordCountV2
```

### <a name="step-3-start-hello-upgrade"></a>Étape 3 : Démarrer la mise à niveau hello
Différents paramètres de mise à niveau, les délais d’attente et critères d’intégrité peuvent être mises à niveau tooapplication appliqué. Lisez hello [paramètres de mise à niveau l’application](service-fabric-application-upgrade-parameters.md) et [mise à niveau](service-fabric-application-upgrade.md) toolearn plus de documents. Tous les services et les instances doivent être *intègre* après mise à niveau hello.  Ensemble hello **HealthCheckStableDuration** too60 secondes (de sorte que les services de hello sont sains au moins 20 secondes avant la mise à niveau hello passe toohello ensuite mettre à niveau de domaine).  Également ensemble hello **UpgradeDomainTimeout** too1200 secondes et hello **UpgradeTimeout** too3000 secondes. Enfin, définissez hello **UpgradeFailureAction** trop**restauration**, les demandes de Service Fabric restaure hello version précédente de l’application toohello si les échecs sont produisent pendant la mise à niveau.

Vous pouvez maintenant démarrer la mise à niveau de hello application à l’aide de hello [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) applet de commande :

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/WordCount -ApplicationTypeVersion 2.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000  -FailureAction Rollback -Monitored
```

Notez que ce nom de l’application hello hello est identique comme hello déployé précédemment v1.0.0 nom de l’application (fabric : / WordCount). L’infrastructure de service utilise cette tooidentify nom quelle application est mise à niveau. Si vous définissez hello toobe de délais d’attente trop court, vous pouvez rencontrer un message d’erreur de délai d’attente que les États hello problème. Consultez trop[résoudre les problèmes de mises à niveau de l’application](service-fabric-application-upgrade-troubleshooting.md), ou augmenter les délais d’expiration hello.

### <a name="step-4-check-upgrade-progress"></a>Étape 4 : vérification de la progression de la mise à niveau
Vous pouvez surveiller la progression de mise à niveau l’application à l’aide de [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md), ou à l’aide de hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) applet de commande :

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/WordCount
```

Dans quelques minutes, hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) applet de commande indique que tous les domaines de mise à niveau ont été mis à niveau (terminé).

## <a name="task-test-a-service-fabric-application"></a>Tâche : tester une application Service Fabric
toowrite des services de qualité, les développeurs doivent stabilité hello toobe tooinduce en mesure d’infrastructure non fiable erreurs tootest de leurs services. Service Fabric offre aux développeurs d’actions d’erreur hello capacité tooinduce et tester des services en présence de hello d’échecs à l’aide de hello chaos et le basculement de scénarios de test.  Lisez [Introduction toohello erreur Analysis Service](service-fabric-testability-overview.md) pour plus d’informations.

### <a name="step-1-run-hello-chaos-test-scenario"></a>Étape 1 : Exécuter le scénario de test de chaos hello
scénario de test de chaos Hello génère des erreurs sur l’intégralité du cluster Service Fabric hello. scénario de Hello compresse les erreurs s’affichés généralement sur un mois ou années tooa quelques heures. combinaison Hello de défauts entrelacées avec un taux élevé de pannes de recherche des cas qui passe inaperçues dans le cas contraire. Hello exemple ci-après exécute scénario de test de chaos hello pendant 60 minutes.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$concurrentFaults = 3
$waitTimeBetweenIterationsSec = 60

Invoke-ServiceFabricChaosTestScenario -TimeToRunMinute $timeToRun -MaxClusterStabilizationTimeoutSec $maxStabilizationTimeSecs -MaxConcurrentFaults $concurrentFaults -EnableMoveReplicaFaults -WaitTimeBetweenIterationsSec $waitTimeBetweenIterationsSec
```

### <a name="step-2-run-hello-failover-test-scenario"></a>Étape 2 : Exécuter le scénario de test de basculement hello
Hello basculement cibles du scénario de test une partition de service spécifique au lieu de l’ensemble du cluster hello et autres services laisse pas affectés. scénario de Hello effectue une itération dans une séquence d’erreurs simulés dans la validation de service pendant l’exécution de votre logique métier. Un échec de validation de service indique une erreur nécessitant un examen approfondi. test de basculement Hello n'induit qu’une seule erreur à la fois, comme le scénario de test toohello opposés chaos, qui est susceptible d’entraîner des erreurs multiples. Hello exemple ci-après exécute le test de basculement hello pendant 60 minutes par rapport à l’ensemble fibre optique hello : WordCount/WordCountService service.

```powershell
$timeToRun = 60
$maxStabilizationTimeSecs = 180
$waitTimeBetweenFaultsSec = 10
$serviceName = "fabric:/WordCount/WordCountService"

Invoke-ServiceFabricFailoverTestScenario -TimeToRunMinute $timeToRun -MaxServiceStabilizationTimeoutSec $maxStabilizationTimeSecs -WaitTimeBetweenFaultsSec $waitTimeBetweenFaultsSec -ServiceName $serviceName -PartitionKindUniformInt64 -PartitionKey 1
```

## <a name="task-remove-a-service-fabric-application"></a>Tâche : supprimer une application Service Fabric
Vous pouvez supprimer une instance d’une application déployée, supprimer type hello mis en service de l’application hello cluster et supprimer le package d’application hello de hello images.

### <a name="step-1-remove-an-application-instance"></a>Étape 1 : Suppression d’une instance d’application
Lorsqu’une instance d’application n’est plus nécessaire, vous pouvez le supprimer définitivement à l’aide de hello [Remove-ServiceFabricApplication](/powershell/module/servicefabric/remove-servicefabricapplication?view=azureservicefabricps) applet de commande. Cette opération supprime également automatiquement tous les services appartenant application toohello, suppression permanente de tous les États de service. Cette opération ne peut pas être annulée et l'état de l'application ne peut pas être récupéré.

```powershell
Remove-ServiceFabricApplication fabric:/WordCount
```

### <a name="step-2-unregister-hello-application-type"></a>Étape 2 : Annuler l’inscription de type de l’application hello
Lorsque vous n’avez plus besoin une version particulière d’un type d’application, annuler son inscription à l’aide de hello [Unregister-ServiceFabricApplicationType](/powershell/module/servicefabric/unregister-servicefabricapplicationtype?view=azureservicefabricps) applet de commande. Lors de la désinscription des types inutilisées versions d’espace de stockage utilisé par le package d’application hello dans le magasin d’images hello. L'enregistrement d'un type d'application peut être annulé s'il ne contient aucune instance d'application ou s'il n'est référencé par aucune mise à niveau d'application.

```powershell
Unregister-ServiceFabricApplicationType WordCount 1.0.0
```

### <a name="step-3-remove-hello-application-package"></a>Étape 3 : Supprimer le package d’application hello
Une fois que le type d’application hello est annulée, hello application peut être supprimé à partir du magasin d’images hello à l’aide de hello [Remove-ServiceFabricApplicationPackage](/powershell/module/servicefabric/remove-servicefabricapplicationpackage?view=azureservicefabricps) applet de commande.

```powershell
Remove-ServiceFabricApplicationPackage -ImageStoreConnectionString file:C:\SfDevCluster\Data\ImageStoreShare -ApplicationPackagePathInImageStore WordCount
```

## <a name="next-steps"></a>Étapes suivantes
[Cycle de vie des applications de la structure du service](service-fabric-application-lifecycle.md)

[Déployer une application](service-fabric-deploy-remove-applications.md)

[Mise à niveau de l’application](service-fabric-application-upgrade.md)

[Applets de commande Azure Service Fabric](/powershell/azure/overview?view=azureservicefabricps)

