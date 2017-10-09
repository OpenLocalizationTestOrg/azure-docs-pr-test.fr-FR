---
title: "mise à niveau de l’application de l’ensemble fibre optique aaaService à l’aide de PowerShell | Documents Microsoft"
description: "Cet article explique les hello expérience de déploiement d’une application de Service Fabric, modifier le code de hello et déploiement d’une mise à niveau à l’aide de PowerShell."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 9bc75748-96b0-49ca-8d8a-41fe08398f25
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: f31212264de45c3b257a0efafb75c10c279b989f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-using-powershell"></a>Mise à niveau d’applications Service Fabric à l’aide de PowerShell
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Hello plus fréquemment utilisés et mise à niveau recommandé est mise à niveau propagée de hello analysé.  Azure Service Fabric analyse hello selon l’intégrité de l’application hello mis à niveau sur un ensemble de stratégies d’intégrité. Une fois qu’un domaine de mise à jour (ID) est mis à niveau, Service Fabric évalue l’intégrité des applications hello et passe de domaine de mise à jour suivant toohello ou Échec de mise à niveau hello en fonction des stratégies de contrôle d’intégrité hello.

Une mise à niveau de l’application analysée peut être effectuée à l’aide de hello gérés ou des API natives, PowerShell ou REST. Pour obtenir des instructions sur l’exécution d’une mise à niveau à l’aide de Visual Studio, consultez [Mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md).

Avec les mises à niveau propagées du Service Fabric est analysé, administrateur de l’application hello peut configurer stratégie d’évaluation d’intégrité hello que Service Fabric utilise toodetermine si l’application hello est saine. En outre, administrateur de hello peut configurer toobe d’action hello prise lors de l’évaluation d’intégrité de hello échoue (par exemple, effectuer une restauration automatique.) Cette section décrit une mise à niveau analysé pour un des exemples du kit SDK hello qui utilise PowerShell. Hello vidéo Microsoft Virtual Academy suivante vous guide également dans une mise à niveau de l’application :<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=OrHJH66yC_6406218965">
<img src="./media/service-fabric-application-upgrade-tutorial-powershell/AppLifecycleVid.png" WIDTH="360" HEIGHT="244">
</a></center>

## <a name="step-1-build-and-deploy-hello-visual-objects-sample"></a>Étape 1 : Créer et déployer l’exemple d’objets visuels hello
Générer et publier l’application hello en cliquant sur le projet d’application hello, **VisualObjectsApplication,** et en sélectionnant hello **publier** commande.  Pour plus d’informations, consultez le [didacticiel sur la mise à niveau d’une application Service Fabric](service-fabric-application-upgrade-tutorial.md).  Vous pouvez également utiliser PowerShell toodeploy votre application.

> [!NOTE]
> Avant d’une des commandes de Service Fabric hello peut être utilisée dans PowerShell, vous devez tout d’abord tooconnect toohello cluster à l’aide de hello `Connect-ServiceFabricCluster` applet de commande. De même, il est supposé que hello que cluster a déjà été configuré sur votre ordinateur local. Consultez l’article hello sur [configuration de votre environnement de développement Service Fabric](service-fabric-get-started.md).
> 
> 

Après la génération de projet hello dans Visual Studio, vous pouvez utiliser la commande PowerShell de hello [ServiceFabricApplicationPackage de copie](/powershell/servicefabric/vlatest/copy-servicefabricapplicationpackage) toocopy hello application package toohello images. Si vous souhaitez que le package d’application hello tooverify localement, utilisez hello [ServiceFabricApplicationPackage-Test](/powershell/servicefabric/vlatest/test-servicefabricapplicationpackage) applet de commande. étape suivante Hello est tooregister hello toohello Service Fabric exécution de l’application à l’aide de hello [Register-ServiceFabricApplicationPackage](/powershell/servicefabric/vlatest/register-servicefabricapplicationtype) applet de commande. Bonjour étape finale est toostart une instance de l’application hello à l’aide de hello [New-ServiceFabricApplication](/powershell/module/servicefabric/new-servicefabricapplication?view=azureservicefabricps) applet de commande.  Ces trois étapes sont analogues toousing hello **déployer** élément de menu dans Visual Studio.

Vous pouvez maintenant utiliser [Service Fabric Explorer tooview hello cluster et hello l’application](service-fabric-visualizing-your-cluster.md). application Hello possède un service web qui peut être navigué tooin Internet Explorer en tapant [http://localhost : 8081/visualobjects](http://localhost:8081/visualobjects) dans la barre d’adresses hello.  Vous devez voir certains objets visuels flottantes déplacement dans l’écran hello.  En outre, vous pouvez utiliser [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps) toocheck état de l’application hello.

## <a name="step-2-update-hello-visual-objects-sample"></a>Étape 2 : Mettre à jour des exemples d’objets visuels hello
Vous pouvez remarquer qu’avec la version de hello qui a été déployée à l’étape 1, les objets visuels hello ne pas faire pivoter. Nous allons mettre à niveau de ce tooone application où les objets visuels hello également faire pivoter.

Sélectionnez le projet VisualObjects.ActorService hello hello VisualObjects solution et ouvrir le fichier de StatefulVisualObjectActor.cs hello. Dans ce fichier, accédez à toohello méthode `MoveObject`, commentez `this.State.Move()`et ne commentez pas `this.State.Move(true)`. Cette modification fait pivoter les objets hello après la mise à niveau de service de hello.

Nous devons également tooupdate hello *ServiceManifest.xml* fichier (sous PackageRoot) du projet de hello **VisualObjects.ActorService**. Hello de mise à jour *CodePackage* hello service version too2.0 et hello lignes correspondantes de hello *ServiceManifest.xml* fichier.
Vous pouvez utiliser Visual Studio de hello *modifier les fichiers manifeste* option une fois avec le bouton droit sur les modifications du fichier manifeste hello solution toomake hello.

Après les modifications de hello, manifeste de hello doit ressembler à hello suivantes (en surbrillance des parties permet d’afficher les modifications hello) :

```xml
<ServiceManifestName="VisualObjects.ActorService" Version="2.0" xmlns="http://schemas.microsoft.com/2011/01/fabric" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">

<CodePackageName="Code" Version="2.0">
```

Maintenant hello *ApplicationManifest.xml* fichier (situés sous hello **VisualObjects** projet sous hello **VisualObjects** solution) est mis à jour tooversion 2.0 Hello  **VisualObjects.ActorService** projet. En outre, la version de l’Application hello est mis à jour too2.0.0.0 de 1.0.0.0. Hello *ApplicationManifest.xml* doit ressemble hello suivant extrait de code :

```xml
<ApplicationManifestxmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="VisualObjects" ApplicationTypeVersion="2.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">

 <ServiceManifestRefServiceManifestName="VisualObjects.ActorService" ServiceManifestVersion="2.0" />
```


À présent, générer le projet de hello en sélectionnant simplement hello **ActorService** projet, puis cliquant et en sélectionnant hello **générer** option dans Visual Studio. Si vous sélectionnez **tout reconstruire**, vous devez mettre à jour versions hello pour tous les projets, étant donné que le code de hello aurait été modifié. Ensuite, nous allons hello du package mis à jour des applications en cliquant sur ***VisualObjectsApplication***, en sélectionnant hello Menu de l’infrastructure de Service et en choisissant **Package**. Cette action crée un package d’application qui peut être déployé.  Votre application de mises à jour est toobe prêt déployée.

## <a name="step-3--decide-on-health-policies-and-upgrade-parameters"></a>Étape 3 : Décider des stratégies de contrôle d’intégrité et des paramètres de mise à niveau
Familiarisez-vous avec hello [paramètres de mise à niveau l’application](service-fabric-application-upgrade-parameters.md) et hello [mise à niveau](service-fabric-application-upgrade.md) tooget une bonne compréhension de hello différentes mise à niveau des paramètres, les délais d’attente et d’intégrité critère appliqué . Pour cette procédure pas à pas, critère d’évaluation de hello service d’intégrité est défini par défaut de toohello (et recommandé) valeurs, ce qui signifie que tous les services et les instances doivent être *intègre* après mise à niveau hello.  

Cependant, nous allons l’augmenter hello *HealthCheckStableDuration* too60 secondes (de sorte que les services de hello sont sains pour le domaine de la prochaine mise à jour au moins 20 secondes avant la mise à niveau hello passe toohello).  Nous allons également définir hello *UpgradeDomainTimeout* toobe 1200 secondes et hello *UpgradeTimeout* toobe 3 000 secondes.

Enfin, nous allons également définir hello *UpgradeFailureAction* toorollback. Cette option nécessite le Service Fabric tooroll hello arrière toohello précédente version de l’application si elle rencontre des problèmes pendant la mise à niveau hello. Par conséquent, lorsque vous démarrez la mise à niveau hello (à l’étape 4), hello paramètres suivants sont spécifiés :

FailureAction = Rollback

HealthCheckStableDurationSec = 60

UpgradeDomainTimeoutSec = 1200

UpgradeTimeout = 3000

## <a name="step-4-prepare-application-for-upgrade"></a>Étape 4 : Préparer l'application pour la mise à niveau
Maintenant l’application hello est générée et prêt toobe mis à niveau. Si vous ouvrez une fenêtre PowerShell en tant qu’administrateur et tapez [Get-ServiceFabricApplication](/powershell/module/servicefabric/get-servicefabricapplication?view=azureservicefabricps), la commande doit vous informer que le type d’application 1.0.0.0 de **VisualObjects** est en cours de déploiement.  

package d’application Hello est stocké sous suivant de hello chemin d’accès relatif dans lequel vous avez décompressé hello Service Fabric SDK - *Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug*. Vous devez trouver un dossier « Package » dans ce répertoire, où le package d’application hello est stocké. Vérifiez tooensure d’horodatages hello qu’il s’agit de build la plus récente hello (vous devrez peut-être toomodify hello chemins en conséquence).

Maintenant nous allons hello de la copie mise à jour toohello de package d’application images de l’infrastructure de Service (où les packages d’application hello sont enregistrées par l’infrastructure de Service). Hello paramètre *ApplicationPackagePathInImageStore* informe l’infrastructure de Service dans lequel il peut trouver le package d’application hello. Nous avons mis l’application hello mis à jour « VisualObjects\_V2 » avec hello suivant de commandes (vous devrez peut-être des chemins d’accès toomodify à nouveau de façon appropriée).

```powershell
Copy-ServiceFabricApplicationPackage  -ApplicationPackagePath .\Samples\Services\Stateful\VisualObjects\VisualObjects\obj\x64\Debug\Package
-ImageStoreConnectionString fabric:ImageStore   -ApplicationPackagePathInImageStore "VisualObjects\_V2"
```

étape suivante de Hello est tooregister cette application avec l’infrastructure de Service, qui peut être effectuée à l’aide de hello [Register-ServiceFabricApplicationType](/powershell/module/servicefabric/register-servicefabricapplicationtype?view=azureservicefabricps) commande :

```powershell
Register-ServiceFabricApplicationType -ApplicationPathInImageStore "VisualObjects\_V2"
```

Si hello commande précédente ne réussit pas, il est probable que vous avez besoin d’une reconstruction de tous les services. Comme indiqué dans l’étape 2, vous avez peut-être tooupdate ainsi votre version de service Web.

## <a name="step-5-start-hello-application-upgrade"></a>Étape 5 : Démarrer la mise à niveau des applications hello
Maintenant, nous sommes tous ensemble toostart hello application mise à niveau à l’aide de hello [Start-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/start-servicefabricapplicationupgrade?view=azureservicefabricps) commande :

```powershell
Start-ServiceFabricApplicationUpgrade -ApplicationName fabric:/VisualObjects -ApplicationTypeVersion 2.0.0.0 -HealthCheckStableDurationSec 60 -UpgradeDomainTimeoutSec 1200 -UpgradeTimeout 3000   -FailureAction Rollback -Monitored
```


Hello nom de l’application est hello même qu’il a été décrit dans hello *ApplicationManifest.xml* fichier. L’infrastructure de service utilise cette tooidentify nom quelle application est mise à niveau. Si vous définissez hello toobe de délais d’attente trop court, vous pouvez rencontrer un message d’échec de que les États hello problème. Consultez toohello section de dépannage ou augmenter les délais d’expiration hello.

À présent, comme hello continue mise à niveau d’application, vous pouvez l’analyser à l’aide du Service Fabric Explorer, ou à l’aide de hello [Get-ServiceFabricApplicationUpgrade](/powershell/module/servicefabric/get-servicefabricapplicationupgrade?view=azureservicefabricps) commande PowerShell : 

```powershell
Get-ServiceFabricApplicationUpgrade fabric:/VisualObjects
```

Dans quelques minutes, état hello que vous avez obtenu à l’aide de hello précédant la commande PowerShell, doivent indiquer que tous les domaines de mise à jour ont été mis à niveau (terminé). Et vous devez rechercher que les objets visuels de hello dans la fenêtre du navigateur ont démarré rotation !

Vous pouvez essayer de la mise à niveau à partir de la version 2 tooversion 3 ou version 2 tooversion 1 en guise d’exercice. Déplacement à partir de la version 2 tooversion 1 est également considérée comme une mise à niveau. Manipuler les délais d’attente et toomake des stratégies de contrôle d’intégrité vous-même connaissent. Lorsque vous déployez tooan cluster Azure, ensemble de paramètres besoin toobe hello en conséquence. Il s’agit habituellement les délais d’attente de bonne tooset hello.

## <a name="next-steps"></a>Étapes suivantes
[Mise à niveau de votre application à l’aide de Visual Studio](service-fabric-application-upgrade-tutorial.md) vous guide à travers une mise à niveau de l’application à l’aide de Visual Studio.

Contrôlez les mises à niveau de votre application à l’aide des [paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).

Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).

Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).

Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau de l’application](service-fabric-application-upgrade-troubleshooting.md).

