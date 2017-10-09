---
title: "aaaDeploy un tooAzure exécutable existant Service Fabric | Documents Microsoft"
description: "Procédure pas à pas sur comment toopackage une application existante en tant qu’invité exécutable, il peut être déployé cluster Service Fabric de tooa"
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: d799c1c6-75eb-4b8a-9f94-bf4f3dadf4c3
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 07/02/2017
ms.author: mfussell;mikhegn
ms.openlocfilehash: 5599802bdb6bda2407a138d77e12148ccb64f437
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-guest-executable-tooservice-fabric"></a>Déployer une infrastructure de tooService exécutable invité
Vous pouvez exécuter n’importe quel type de code, comme Node.js, Java ou C++ dans Azure Service Fabric en tant que service. Service Fabric fait référence à des types de toothese de services en tant qu’invité exécutables.

Les invités exécutables sont traités par le Service Fabric comme des services sans état. En conséquence, ils sont placés dans des nœuds dans un cluster, sur la base de la disponibilité et d’autres mesures. Cet article décrit comment toopackage et déployer un cluster Service Fabric de tooa exécutable invité, à l’aide de Visual Studio ou un utilitaire de ligne de commande.

Dans cet article, nous couvrir hello étapes toopackage exécutable invité et déployez-le tooService l’ensemble fibre optique.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Avantages de l'exécution d'un exécutable invité dans Service Fabric
Il existe plusieurs avantages toorunning invité exécutable dans un cluster Service Fabric :

* Haute disponibilité : Les applications qui sont exécutées dans Service Fabric sont hautement disponibles. Service Fabric s’assure que les instances d’une application sont en cours d’exécution.
* Analyse du fonctionnement. La fonction d’analyse du fonctionnement de Service Fabric détecte si une application est en cours d’exécution et fournit des informations de diagnostic en cas d’échec.   
* Gestion du cycle de vie des applications. Outre les mises à niveau sans interruption de service, Service Fabric fournit la version précédente de la restauration automatique toohello s’il existe un événement fonctionnent-elles signalé pendant une mise à niveau.    
* Densité. Vous pouvez exécuter plusieurs applications dans un cluster, ce qui évite de hello pour chaque toorun application sur son propre matériel.
* Découverte : À l’aide de REST vous pouvez appeler hello Service Fabric Naming service toofind autres services dans un cluster de hello. 

## <a name="samples"></a>Exemples
* [Exemple pour empaqueter et déployer un fichier exécutable invité](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Vue d’ensemble des fichiers du manifeste de service et d’application
Dans le cadre du déploiement d’un exécutable invité, il est modèle de déploiement et d’empaquetage de Service Fabric hello toounderstand utile comme décrit dans [modèle d’application](service-fabric-application-model.md). le modèle de packaging Hello Service Fabric s’appuie sur deux fichiers XML : hello manifestes d’application et des services. Hello définition de schéma pour les fichiers ApplicationManifest.xml et ServiceManifest.xml hello est installé avec hello SDK de l’infrastructure de Service en *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Manifeste d’application** manifeste de l’application hello est utilisé toodescribe hello application. Il répertorie les services hello qui le composent et autres paramètres qui sont utilisé toodefine comment un ou plusieurs services doivent être déployés, telles que nombre hello d’instances.

  Dans Service Fabric, une application est une unité de déploiement et de mise à niveau. Une application peut être mise à niveau en tant qu’unité simple, dans laquelle les défaillances (et restaurations) potentielles sont gérées. L’infrastructure de service garantit que le processus de mise à niveau hello est soit réussi, sinon, si la mise à niveau hello échoue, ne laissez pas application hello dans un état inconnu ou instable.
* **Manifeste de service** manifeste de service hello décrit les composants de hello d’un service. Il inclut des données, telles que le nom de hello et le type de service et son code et la configuration. Hello manifeste de service inclut également des paramètres supplémentaires qui peuvent être utilisées de service de hello tooconfigure une fois qu’il est déployé.

## <a name="application-package-file-structure"></a>Structure de fichier d'un package d'application
toodeploy un tooService d’application Fabric, l’application hello doit suivre une structure de répertoire prédéfini. Hello Voici un exemple de cette structure.

```
|-- ApplicationPackageRoot
    |-- GuestService1Pkg
        |-- Code
            |-- existingapp.exe
        |-- Config
            |-- Settings.xml
        |-- Data
        |-- ServiceManifest.xml
    |-- ApplicationManifest.xml
```

Hello ApplicationPackageRoot contient le fichier ApplicationManifest.xml hello qui définit l’application hello. Un sous-répertoire pour chaque service inclus dans l’application hello est utilisé toocontain tous hello artefacts hello service requiert. Ces sous-répertoires sont hello ServiceManifest.xml et, en règle générale, hello suivant :

* *Code*. Ce répertoire contient un code de service hello.
* *Config*. Ce répertoire contient un fichier Settings.xml (et autres fichiers si nécessaire) que les service de hello peut accéder à des paramètres de configuration spécifiques tooretrieve runtime.
* *Data*. Il s’agit d’une annuaire supplémentaire toostore local des données supplémentaires qui hello service peut avoir besoin. Données doivent être les données uniquement éphémère toostore utilisé. L’infrastructure de service effectue pas de copie ou de la réplication du répertoire de données modifications toohello si le service de hello doit toobe déplacée (par exemple, pendant le basculement).

> [!NOTE]
> Vous n’avez pas toocreate hello `config` et `data` si vous n’en avez pas besoin de répertoires.
>
>

## <a name="package-an-existing-executable"></a>Empaqueter un exécutable existant
Lors de l’empaquetage d’un exécutable invité, vous pouvez choisir soit toouse un modèle de projet Visual Studio ou trop[créer le package d’application hello manuellement](#manually). À l’aide de Visual Studio, hello structure de package d’application et les fichiers manifeste sont créés par le nouveau modèle de projet hello pour vous.

> [!TIP]
> toopackage de façon plus simple Hello un exécutable dans un service de Windows existant est toouse Visual Studio et sur Linux toouse Yeoman
>

## <a name="use-visual-studio-toopackage-and-deploy-an-existing-executable"></a>Utilisez Visual Studio toopackage et déployer un fichier exécutable existant
Visual Studio fournit une infrastructure de Service toohelp de modèle de service vous déployez un cluster Service Fabric de tooa exécutable invité.

1. Sélectionnez **Fichier** > **Nouveau projet** pour créer une application Service Fabric.
2. Choisissez **exécutable invité** comme modèle de service hello.
3. Cliquez sur **Parcourir** dossier de hello tooselect avec votre fichier exécutable et le remplissage reste hello du service de hello paramètres toocreate hello.
   * *Comportement du package de code*. Peut être ensemble toocopy tout le contenu de votre projet de Visual Studio, de toohello dossier hello qui est utile si hello exécutable ne change pas. Si vous prévoyez toochange d’exécutable hello et que vous souhaitez toopick de capacité hello des nouvelles builds dynamiquement, vous pouvez choisir toolink toohello dossier à la place. Vous pouvez utiliser des dossiers liés lors de la création du projet d’application hello dans Visual Studio. Cette opération lie toohello source emplacement au sein du projet hello, donnant aux invités hello tooupdate exécutable dans la destination de la source. Ces mises à jour font partie du package d’application hello lors de la build.
   * *Programme* spécifie hello exécutable qui doit être exécutée de service de hello toostart.
   * *Arguments* spécifie les arguments hello qui doivent être passés toohello exécutable. Il peut s’agir d’une liste de paramètres avec des arguments.
   * *WorkingFolder* Spécifie le répertoire de travail hello pour les processus hello qui sont en train de toobe a démarré. Vous pouvez spécifier trois valeurs :
     * `CodeBase`Spécifie le répertoire de travail que hello est en train de toobe définir le répertoire de code toohello dans le package d’application hello (`Code` répertoire Bonjour précédant la structure de fichiers).
     * `CodePackage`Spécifie le répertoire de travail que hello est en train de toobe définir racine toohello du package d’application hello (`GuestService1Pkg` illustré hello précédant la structure de fichiers).
     * `Work`Spécifie que les fichiers de hello sont placés dans un sous-répertoire appelé travail.
4. Donnez un nom à votre service et cliquez sur **OK**.
5. Si votre service a besoin d’un point de terminaison pour la communication, vous pouvez maintenant ajouter hello protocole, port et fichier de type toohello ServiceManifest.xml. Par exemple : `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Vous pouvez maintenant utiliser hello package et action de publication sur votre cluster local en déboguant solution hello dans Visual Studio. Lorsque vous êtes prêt, vous pouvez publier le cluster de l’application hello tooa à distance ou archiver hello solution toosource contrôle.
7. Aller à la fin de toohello de toosee de cet article comment tooview votre service exécutable invité en cours d’exécution dans le Service Fabric Explorer.

## <a name="use-yoeman-toopackage-and-deploy-an-existing-executable-on-linux"></a>Utilisez Yoeman toopackage et déployer un exécutable existant sur Linux

procédure de Hello pour créer et déployer un invité exécutable sur Linux est hello même que le déploiement d’une application csharp ou java.

1. Saisissez `yo azuresfguest` dans un terminal.
2. Donnez un nom à votre application.
3. Nom de votre service et fournissent des détails de hello, y compris le chemin d’accès du fichier exécutable de hello et elle doit être appelée avec des paramètres de hello.

Yeoman crée un package d’application avec l’application appropriée hello et les fichiers manifeste avec installer et désinstaller des scripts.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Empaqueter et déployer manuellement d’un exécutable existant
processus Hello de l’empaquetage d’un exécutable invité manuellement est basée sur hello général comme suit :

1. Créer la structure de répertoire du package hello.
2. Ajouter des fichiers de code et la configuration de l’application hello.
3. Modifiez le fichier de manifeste de service hello.
4. Modifier le fichier manifeste d’application hello.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you toocreate hello ApplicationPackage automatically. hello tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-hello-package-directory-structure"></a>Créer la structure de répertoire du package hello
Commencez par créer la structure de répertoire hello, comme décrit dans hello précédant la section, « Structure de fichier de package Application ».

### <a name="add-hello-applications-code-and-configuration-files"></a>Ajouter des fichiers de code et la configuration de l’application hello
Une fois que vous avez créé la structure de répertoire hello, vous pouvez ajouter des fichiers de code et la configuration de l’application hello sous les répertoires de code et de configuration hello. Vous pouvez également créer des répertoires supplémentaires ou des sous-répertoires dans les répertoires de code ou la configuration hello.

Service Fabric est un `xcopy` de contenu hello hello répertoire racine d’application, il n’existe aucun toouse structure prédéfinie autre que la création de deux répertoires supérieur, les codes et les paramètres. (Vous pouvez choisir des noms différents si vous le souhaitez. Plus de détails sont dans la section suivante de hello.)

> [!NOTE]
> Assurez-vous que vous incluez tous les fichiers de hello et les dépendances qui hello les besoins de l’application. Service Fabric copie hello contenu du package d’application hello sur tous les nœuds de cluster hello où les services de l’application hello sont toobe continu déployé. package de Hello doit contenir tout code hello qu’application hello doit toorun. Ne supposez pas que les dépendances de hello sont déjà installés.
>
>

### <a name="edit-hello-service-manifest-file"></a>Modifier le fichier manifeste de service hello
étape suivante de Hello est hello tooedit hello service fichier manifeste tooinclude informations suivantes :

* nom Hello hello du type de service. Il s’agit d’un ID que le Service Fabric utilise tooidentify un service.
* commande toouse toolaunch hello application Hello (ExeHost).
* N’importe quel script qui doit tooset toobe exécuter l’application hello (SetupEntrypoint).

Hello Voici un exemple d’un `ServiceManifest.xml` fichier :

```xml
<?xml version="1.0" encoding="utf-8"?>
<ServiceManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" Name="NodeApp" Version="1.0.0.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceTypes>
      <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true"/>
   </ServiceTypes>
   <CodePackage Name="code" Version="1.0.0.0">
      <SetupEntryPoint>
         <ExeHost>
             <Program>scripts\launchConfig.cmd</Program>
         </ExeHost>
      </SetupEntryPoint>
      <EntryPoint>
         <ExeHost>
            <Program>node.exe</Program>
            <Arguments>bin/www</Arguments>
            <WorkingFolder>CodePackage</WorkingFolder>
         </ExeHost>
      </EntryPoint>
   </CodePackage>
   <Resources>
      <Endpoints>
         <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
      </Endpoints>
   </Resources>
</ServiceManifest>
```

Hello les sections suivantes accédez hello différentes parties du fichier hello que vous avez besoin de tooupdate.

#### <a name="update-servicetypes"></a>Mettre à jour ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* Vous pouvez choisir n’importe quel nom pour `ServiceTypeName`. valeur de Hello est utilisée dans hello `ApplicationManifest.xml` tooidentify hello service de fichiers.
* Spécifiez `UseImplicitHost="true"`. Cet attribut indique à Service Fabric que service de hello est basé sur une application autonome, par conséquent, tous les Service Fabric doit toodo est toolaunch sous la forme d’un processus et d’analyser son intégrité.

#### <a name="update-codepackage"></a>Mettre à jour CodePackage
Hello CodePackage élément indique les emplacement hello (version) de hello du code.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

Hello `Name` élément désigne toospecify utilisé hello du répertoire hello dans le package d’application hello qui contient le code du service hello. `CodePackage`a également hello `version` attribut. Cela peut être utilisé toospecify hello version de hello code et peut également être utilisé tooupgrade hello du code à l’aide d’infrastructure de gestion du cycle de vie hello application Service fabric.

#### <a name="optional-update-setupentrypoint"></a>Facultatif : mettre à jour SetupEntrypoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
élément de SetupEntryPoint Hello est toospecify utilisée n’importe quel fichier exécutable ou un lot qui doit être exécutée avant de lancer hello du code. Il est une étape facultative, donc il n’a pas besoin de toobe incluse si aucune initialisation n’est nécessaire. Hello SetupEntryPoint est exécutée chaque fois que le service de hello est redémarré.

Il est SetupEntryPoint qu’un seul, donc pas besoin de scripts d’installation toobe regroupé dans un fichier de commandes même si le programme d’installation de l’application hello requiert plusieurs scripts. Hello SetupEntryPoint peut exécuter n’importe quel type de fichier : fichiers exécutables, les fichiers de commandes et les applets de commande PowerShell. Pour en savoir plus, consultez la rubrique relative à la [configuration de l’élément SetupEntryPoint](service-fabric-application-runas-security.md).

Bonjour précédent exemple, hello SetupEntryPoint exécute un fichier de commandes appelé `LaunchConfig.cmd` qui est situé dans hello `scripts` sous-répertoire du répertoire de code hello (en supposant que hello WorkingFolder a la valeur tooCodeBase).

#### <a name="update-entrypoint"></a>Mettre à jour EntryPoint
```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
  </ExeHost>
</EntryPoint>
```

Hello `EntryPoint` élément dans le fichier manifeste de service hello est utilisé toospecify comment service hello de toolaunch. Hello `ExeHost` élément spécifie hello exécutable (et arguments) qui doit être utilisé toolaunch hello service.

* `Program`Spécifie le nom hello du fichier exécutable hello qui doit démarrer hello service.
* `Arguments`Spécifie les arguments hello qui doivent être passés toohello exécutable. Il peut s’agir d’une liste de paramètres avec des arguments.
* `WorkingFolder`Spécifie le répertoire de travail hello pour les processus hello qui sont en train de toobe a démarré. Vous pouvez spécifier trois valeurs :
  * `CodeBase`Spécifie le répertoire de travail que hello est en train de toobe définir le répertoire de code toohello dans le package d’application hello (`Code` répertoire hello précédant la structure de fichiers).
  * `CodePackage`Spécifie le répertoire de travail que hello est en train de toobe définir racine toohello du package d’application hello (`GuestService1Pkg` Bonjour précédant la structure de fichiers).
    * `Work`Spécifie que les fichiers de hello sont placés dans un sous-répertoire appelé travail.

Hello WorkingFolder est le répertoire de travail correct tooset utile hello afin que les chemins d’accès relatifs peuvent être utilisés par l’application ou l’initialisation des scripts hello.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Mettre à jour des points de terminaison et les inscrire auprès du service d’affectation de noms à des fins de communication
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
Bonjour précédent exemple, hello `Endpoint` élément spécifie les points de terminaison hello application hello peut écouter. Dans cet exemple, hello application Node.js écoute http sur le port 3000.

Vous pouvez en outre demander à Service Fabric toopublish cette toohello de point de terminaison d’affectation de noms Service pour d’autres services puissent détecter le service de toothis d’adresse de point de terminaison hello. Cela vous permet de toocommunicate en mesure de toobe entre les services qui sont des exécutables de l’invité.
Bonjour adresse de point de terminaison publié est sous forme de hello `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme` et `PathSuffix` sont des attributs facultatifs. `IPAddressOrFQDN`est hello adresse IP ou nom de domaine complet du nœud hello cet exécutable est placé sur, et elle est calculée pour vous.

Hello exemple suivant, une fois les services hello est déployé, dans l’Explorateur de l’infrastructure de Service vous voyez un point de terminaison similaire trop`http://10.1.4.92:3000/myapp/` publiée pour l’instance de service hello. S’il s’agit d’un ordinateur local, vous verrez`http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Vous pouvez utiliser ces adresses avec [proxy inverse](service-fabric-reverseproxy.md) toocommunicate entre les services.

### <a name="edit-hello-application-manifest-file"></a>Modifier le fichier manifeste d’application hello
Une fois que vous avez configuré hello `Servicemanifest.xml` fichier, vous devez toomake toohello de certaines modifications `ApplicationManifest.xml` fichier tooensure hello correct de type de service et le nom sont utilisés.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
Bonjour `ServiceManifestImport` élément, vous pouvez spécifier un ou plusieurs services que vous souhaitez tooinclude dans l’application hello. Les services sont référencés avec `ServiceManifestName`, qui spécifie le nom hello du répertoire de hello où hello `ServiceManifest.xml` fichier se trouve.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Configurez la journalisation
Pour les exécutables de l’invité, il est utile toobe toosee en mesure de console journaux toofind out si les scripts de configuration et application hello affichent toutes les erreurs.
Redirection de la console peut être configuré dans hello `ServiceManifest.xml` fichier à l’aide de hello `ConsoleRedirection` élément.

> [!WARNING]
> N’utilisez jamais de stratégie de redirection de console hello dans une application est déployée en production, car cela peut affecter le basculement d’application hello. N’utilisez cette stratégie *que* pour le développement local et à des fins de débogage.  
>
>

```xml
<EntryPoint>
  <ExeHost>
    <Program>node.exe</Program>
    <Arguments>bin/www</Arguments>
    <WorkingFolder>CodeBase</WorkingFolder>
    <ConsoleRedirection FileRetentionCount="5" FileMaxSizeInKb="2048"/>
  </ExeHost>
</EntryPoint>
```

`ConsoleRedirection`répertoire de travail tooa tooredirect utilisé console sortie (stdout et stderr) est possible. Cela fournit hello capacité tooverify qu’il n’y a aucune erreur durant l’installation de hello ou de l’exécution de l’application hello dans le cluster Service Fabric de hello.

`FileRetentionCount`Détermine le nombre de fichiers est enregistré dans le répertoire de travail hello. Une valeur de 5, par exemple, signifie que les fichiers de journaux hello pour les exécutions de cinq hello précédente sont stockés dans le répertoire de travail hello.

`FileMaxSizeInKb`Spécifie la taille maximale de hello des fichiers journaux de hello.

Fichiers journaux sont enregistrés dans un des répertoires de travail du service hello. toodetermine où se trouvent les fichiers hello, utilisez Service Fabric Explorer toodetermine service hello nœud est en cours d’exécution et le répertoire de travail est utilisé. Cette procédure est décrite ultérieurement dans cet article.

## <a name="deployment"></a>Déploiement
dernière étape de Hello est trop[déployer votre application](service-fabric-deploy-remove-applications.md). Hello suivant montre de script PowerShell comment toodeploy votre cluster de développement local toohello application et démarrer un nouveau service Service Fabric.

```PowerShell

Connect-ServiceFabricCluster localhost:19000

Write-Host 'Copying application package...'
Copy-ServiceFabricApplicationPackage -ApplicationPackagePath 'C:\Dev\MultipleApplications' -ImageStoreConnectionString 'file:C:\SfDevCluster\Data\ImageStoreShare' -ApplicationPackagePathInImageStore 'nodeapp'

Write-Host 'Registering application type...'
Register-ServiceFabricApplicationType -ApplicationPathInImageStore 'nodeapp'

New-ServiceFabricApplication -ApplicationName 'fabric:/nodeapp' -ApplicationTypeName 'NodeAppType' -ApplicationTypeVersion 1.0

New-ServiceFabricService -ApplicationName 'fabric:/nodeapp' -ServiceName 'fabric:/nodeapp/nodeappservice' -ServiceTypeName 'NodeApp' -Stateless -PartitionSchemeSingleton -InstanceCount 1

```

>[!TIP]
> [Compresser le package de hello](service-fabric-package-apps.md#compress-a-package) avant de copier le magasin d’images toohello si le package de hello est trop grande ou a de nombreux fichiers. En savoir plus [ici](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Plusieurs configurations différentes peuvent être utilisées pour déployer un service Service Fabric. Par exemple, il peut être déployé en tant qu’une ou plusieurs instances, ou il peut être déployé de manière à ce qu’il existe une instance du service hello sur chaque nœud du cluster Service Fabric de hello.

Hello `InstanceCount` paramètre Hello `New-ServiceFabricService` applet de commande est utilisée toospecify combien d’instances de service de hello doit être lancée dans le cluster Service Fabric de hello. Vous pouvez définir hello `InstanceCount` valeur, en fonction de type hello d’application que vous déployez. les scénarios les plus courants Hello deux sont :

* `InstanceCount = "1"`. Dans ce cas, seule une instance de service de hello est déployée dans un cluster de hello. Le planificateur du service Fabric détermine quel service hello de nœud est en train de toobe déployé sur.
* `InstanceCount ="-1"`. Dans ce cas, une instance du service de hello est déployée sur chaque nœud de cluster du Service Fabric hello. résultat de Hello a un seul (et unique) instance du service hello pour chaque nœud de cluster de hello.

Il s’agit d’une configuration utile pour des applications frontales (par exemple, un point de terminaison REST), étant donné que les applications clientes doivent trop « se connecter » tooany de nœuds hello dans le point de terminaison hello cluster toouse hello. Cette configuration peut également être utilisée lorsque, par exemple, tous les nœuds du cluster Service Fabric de hello sont équilibrage de charge tooa connecté. Le trafic des clients peut ensuite être distribué sur service hello qui s’exécute sur tous les nœuds de cluster de hello.

## <a name="check-your-running-application"></a>Vérification de votre application en cours d'exécution
Dans l’Explorateur de l’infrastructure de Service, identifiez le nœud hello où hello service s’exécute. Dans cet exemple, il s’exécute sur le nœud 1 :

![Nœud sur lequel le service est en cours d’exécution](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Si vous accédez toohello nœud et parcourir toohello application, vous consultez informations de nœud essentielles hello, y compris son emplacement sur le disque.

![Emplacement sur le disque](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Si vous y accédez toohello active à l’aide de l’Explorateur de serveurs, vous trouverez répertoire de travail hello et le dossier du journal du service hello, comme indiqué dans hello suivant capture d’écran : 

![Emplacement du journal](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toopackage un exécutable invité et déployez-le tooService l’ensemble fibre optique. Consultez hello suivant des articles pour les tâches et les informations connexes.

* [Exemple pour empaqueter et déployer un exécutable invité](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), y compris une version préliminaire toohello de lien de l’outil d’empaquetage hello
* [Exemple de l’invité deux exécutables (c# et nodejs) communique via le service d’affectation de noms de hello à l’aide de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)
* [Déploiement de plusieurs exécutables invités](service-fabric-deploy-multiple-apps.md)
* [Créez votre première application Service Fabric avec Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
