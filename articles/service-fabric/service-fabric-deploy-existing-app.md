---
title: "Déploiement d’un exécutable existant dans Azure Service Fabric | Microsoft Docs"
description: "Procédure pas à pas pour empaqueter une application existante en tant que fichier exécutable invité afin de la déployer sur un cluster Service Fabric"
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
ms.openlocfilehash: c851e1f756957d58d5f7372098620e4b7129b089
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2017
---
# <a name="deploy-a-guest-executable-to-service-fabric"></a>Déploiement d'un exécutable invité dans Service Fabric
Vous pouvez exécuter n’importe quel type de code, comme Node.js, Java ou C++ dans Azure Service Fabric en tant que service. Dans la terminologie Service Fabric, ces types de service sont appelés des exécutables invités.

Les invités exécutables sont traités par le Service Fabric comme des services sans état. En conséquence, ils sont placés dans des nœuds dans un cluster, sur la base de la disponibilité et d’autres mesures. Cet article explique comment empaqueter et déployer un exécutable invité dans un cluster Service Fabric, en utilisant Visual Studio ou un utilitaire en ligne de commande.

Dans cet article, nous abordons les étapes pour empaqueter un exécutable invité et le déployer dans Service Fabric.  

## <a name="benefits-of-running-a-guest-executable-in-service-fabric"></a>Avantages de l'exécution d'un exécutable invité dans Service Fabric
L’exécution d’un exécutable invité dans un cluster Service Fabric présente plusieurs avantages :

* Haute disponibilité : Les applications qui sont exécutées dans Service Fabric sont hautement disponibles. Service Fabric s’assure que les instances d’une application sont en cours d’exécution.
* Analyse du fonctionnement. La fonction d’analyse du fonctionnement de Service Fabric détecte si une application est en cours d’exécution et fournit des informations de diagnostic en cas d’échec.   
* Gestion du cycle de vie des applications. Outre les mises à niveau sans temps d’arrêt, Service Fabric assure la restauration automatique de la version précédente en cas d’événement signalant un problème d’intégrité lors d’une mise à niveau.    
* Densité. Vous pouvez exécuter plusieurs applications dans un cluster, ce qui élimine le besoin d’exécuter chaque application sur son propre matériel.
* Détectabilité : À l’aide de REST, vous pouvez appeler le service d’attribution de noms Service Fabric pour trouver d’autres services dans le cluster. 

## <a name="samples"></a>Exemples
* [Exemple pour empaqueter et déployer un fichier exécutable invité](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started)
* [Exemple de deux exécutables invités (C# et nodejs) communiquant via le service d’attribution de noms à l’aide de REST](https://github.com/Azure-Samples/service-fabric-dotnet-containers)

## <a name="overview-of-application-and-service-manifest-files"></a>Vue d’ensemble des fichiers du manifeste de service et d’application
Dans le cadre du déploiement d’un exécutable invité, il est utile de comprendre le modèle d’empaquetage et de déploiement Service Fabric tel que décrit dans [Modèle d’application](service-fabric-application-model.md). Le modèle d’empaquetage Service Fabric repose sur deux fichiers XML : les manifestes d’application et de service. La définition de schéma pour les fichiers ApplicationManifest.xml et ServiceManifest.xml est installée avec le Kit de développement logiciel (SDK) Service Fabric sous *C:\Program Files\Microsoft SDKs\Service Fabric\schemas\ServiceFabricServiceModel.xsd*.

* **Manifeste d’application** : le manifeste d’application permet de décrire l’application. Il répertorie les services qui la composent, ainsi que d’autres paramètres utilisés pour définir la manière dont les services doivent être déployés (comme le nombre d’instances).

  Dans Service Fabric, une application est une unité de déploiement et de mise à niveau. Une application peut être mise à niveau en tant qu’unité simple, dans laquelle les défaillances (et restaurations) potentielles sont gérées. Service Fabric garantit la réussite de la mise à niveau. En cas d’échec, elle fait en sorte que l’application ne reste pas dans un état inconnu ou instable.
* **Manifeste de service** : le manifeste de service décrit les composants d’un service. Il inclut des données telles que le nom et le type du service, ainsi que son code et sa configuration. Le manifeste de service inclut également des paramètres supplémentaires qui peuvent être utilisés pour configurer le service après son déploiement.

## <a name="application-package-file-structure"></a>Structure de fichier d'un package d'application
Pour que vous puissiez la déployer sur Service Fabric, votre application doit respecter une structure de répertoire prédéfinie. Voici un exemple de structure de ce type.

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

Le paramètre ApplicationPackageRoot contient le fichier ApplicationManifest.xml, qui définit l’application. Un sous-répertoire pour chaque service inclus dans l’application est utilisé pour contenir tous les artefacts nécessaires au service. Ces sous-répertoires correspondent au fichier ServiceManifest.xml et généralement aux éléments suivants :

* *Code*. Ce répertoire contient le code du service.
* *Config*. Ce répertoire contient un fichier Settings.xml (et d’autres fichiers si nécessaire) auquel le service peut accéder lors de l’exécution pour récupérer des paramètres de configuration spécifiques.
* *Data*. Il s’agit d’un répertoire supplémentaire pour stocker des données locales supplémentaires dont le service peut avoir besoin. Le répertoire Data doit être utilisé uniquement pour stocker des données éphémères. Service Fabric ne copie et ne réplique pas les modifications dans le répertoire des données si le service doit être déplacé, par exemple, pendant le basculement.

> [!NOTE]
> Il est inutile de créer les répertoires `config` et `data` si vous n’en avez pas besoin.
>
>

## <a name="package-an-existing-executable"></a>Empaqueter un exécutable existant
Lors de l’empaquetage d’un exécutable invité, vous pouvez choisir d’utiliser un modèle de projet Visual Studio ou de [créer le package d’application manuellement](#manually). À l’aide de Visual Studio, la structure de package d’application et les fichiers manifeste sont créés pour vous par le modèle de nouveau projet.

> [!TIP]
> Pour empaqueter un exécutable Windows existant dans un service, le plus simple consiste à utiliser Visual Studio, ou Yeoman si vous êtes sur Linux.
>

## <a name="use-visual-studio-to-package-and-deploy-an-existing-executable"></a>Utiliser Visual Studio pour empaqueter et déployer un exécutable existant
Visual Studio fournit un modèle de service Service Fabric pour vous aider à déployer un fichier exécutable invité sur un cluster Service Fabric.

1. Sélectionnez **Fichier** > **Nouveau projet** pour créer une application Service Fabric.
2. Choisissez **Exécutable invité** comme modèle de service.
3. Cliquez sur **Parcourir** pour sélectionner le dossier avec votre exécutable et renseignez le reste des paramètres pour créer le service.
   * *Comportement du package de code*. Peut être défini pour copier tout le contenu de votre dossier dans le projet Visual Studio, ce qui est utile si l’exécutable ne change pas. Si vous vous attendez à ce que le fichier exécutable soit modifié et souhaitez avoir la possibilité de choisir les nouvelles versions de façon dynamique, vous pouvez choisir de créer un lien vers le dossier à la place. Vous pouvez utiliser les dossiers liés lors de la création du projet d’application dans Visual Studio. Cela permet de créer un lien vers l’emplacement source à partir du projet, ce qui ouvre la possibilité de mettre à jour l’exécutable invité dans la destination de la source correspondante. Ces mises à jour sont incluses dans le package d’application au moment de la création de la build.
   * *Program* : spécifie l’exécutable qui doit être exécuté pour démarrer le service.
   * *Arguments* : spécifie les arguments qui doivent être passés à l’exécutable. Il peut s’agir d’une liste de paramètres avec des arguments.
   * *WorkingFolder* : spécifie le répertoire de travail pour le processus qui va démarrer. Vous pouvez spécifier trois valeurs :
     * `CodeBase` indique que le répertoire de travail doit être défini sur le répertoire du code dans le package d’application (répertoire `Code` dans la structure de fichiers indiquée précédemment).
     * `CodePackage` indique que le répertoire de travail doit être défini sur la racine du package d’application (`GuestService1Pkg` dans la structure de fichiers indiquée précédemment).
     * `Work` spécifie que les fichiers sont placés dans un sous-répertoire appelé « work ».
4. Donnez un nom à votre service et cliquez sur **OK**.
5. Si votre service a besoin d’un point de terminaison pour les communications, vous pouvez désormais ajouter le protocole, le port et le type dans le fichier ServiceManifest.xml. Par exemple : `<Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" UriScheme="http" PathSuffix="myapp/" Type="Input" />`.
6. Vous pouvez maintenant utiliser le package et exécuter l’action de publication sur votre cluster local, en effectuant le débogage de la solution dans Visual Studio. Vous pouvez, quand vous le souhaitez, publier l’application sur un cluster à distance ou archiver la solution pour contrôler le code source.
7. Accédez à la fin de cet article pour découvrir comment afficher le service d’exécutable invité lancé dans Service Fabric Explorer.

## <a name="use-yeoman-to-package-and-deploy-an-existing-executable-on-linux"></a>Utiliser Yeoman pour empaqueter et déployer un exécutable existant sous Linux

La procédure de création et de déploiement d'un exécutable invité sur Linux est identique au déploiement d’une application csharp ou java.

1. Saisissez `yo azuresfguest` dans un terminal.
2. Donnez un nom à votre application.
3. Nommez votre service et fournissez les détails, y compris le chemin d’accès de l’exécutable et les paramètres avec lesquels il doit être appelé.

Yeoman crée un package d’application avec l’application et les fichiers manifeste appropriés ainsi que les scripts d'installation et de désinstallation.

<a id="manually"></a>

## <a name="manually-package-and-deploy-an-existing-executable"></a>Empaqueter et déployer manuellement d’un exécutable existant
Le processus d’empaquetage manuel d’un exécutable invité est basé sur les étapes générales suivantes :

1. Créez la structure de répertoires du package.
2. Ajoutez des fichiers de code et de configuration de l’application.
3. Modifiez le fichier de manifeste de service.
4. Modifiez le fichier de manifeste d’application.

<!--
>[AZURE.NOTE] We do provide a packaging tool that allows you to create the ApplicationPackage automatically. The tool is currently in preview. You can download it from [here](http://aka.ms/servicefabricpacktool).
-->

### <a name="create-the-package-directory-structure"></a>Création de la structure de répertoires du package
Commencez par créer la structure de répertoires, comme décrit dans la section précédente, « Structure de fichier d’un package d’application ».

### <a name="add-the-applications-code-and-configuration-files"></a>Ajout des fichiers de code et de configuration de l’application
Après avoir créé la structure de répertoires, vous pouvez ajouter les fichiers de code et de configuration de l’application dans les répertoires code et config. Vous pouvez également créer d’autres répertoires ou sous-répertoires dans les répertoires code ou config.

Service Fabric crée une `xcopy` du contenu du répertoire racine de l’application. Par conséquent, il n’existe aucune structure prédéfinie à utiliser, autre que la création des deux principaux répertoires code et paramètres. (Vous pouvez choisir des noms différents si vous le souhaitez. Pour plus d’informations, consultez la section suivante.)

> [!NOTE]
> Veillez à bien inclure la totalité des fichiers et dépendances nécessaires à l’application. Service Fabric copie le contenu du package d’application sur tous les nœuds du cluster dans lequel les services de l’application seront déployés. Le package doit contenir l’ensemble du code nécessaire à l’exécution de l’application. Ne supposez pas que les dépendances sont déjà installées.
>
>

### <a name="edit-the-service-manifest-file"></a>Modification du fichier de manifeste de service
L’étape suivante consiste à modifier le fichier de manifeste de service afin d’inclure les informations suivantes :

* Le nom du type de service. Il s’agit d’un ID que Service Fabric utilise pour identifier un service.
* La commande à utiliser pour lancer l’application (ExeHost).
* Tout script devant être exécuté pour installer ou configurer l’application (SetupEntrypoint).

Voici un exemple de fichier `ServiceManifest.xml` :

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

Examinons les différentes parties du fichier que vous devez mettre à jour :

#### <a name="update-servicetypes"></a>Mettre à jour ServiceTypes
```xml
<ServiceTypes>
  <StatelessServiceType ServiceTypeName="NodeApp" UseImplicitHost="true" />
</ServiceTypes>
```

* Vous pouvez choisir n’importe quel nom pour `ServiceTypeName`. La valeur est utilisée dans le fichier `ApplicationManifest.xml` pour identifier le service.
* Spécifiez `UseImplicitHost="true"`. Cet attribut indique à Service Fabric que le service est basé sur une application autonome et que la seule opération nécessaire consiste à la lancer en tant que processus et à surveiller son intégrité.

#### <a name="update-codepackage"></a>Mettre à jour CodePackage
L’élément CodePackage spécifie l’emplacement (et la version) du code du service.

```xml
<CodePackage Name="Code" Version="1.0.0.0">
```

L’élément `Name` est utilisé pour spécifier le nom du répertoire dans le package d’application qui contient le code du service. `CodePackage` a également l’attribut `version`. Cela peut être utilisé pour spécifier la version du code et peut également permettre de mettre à niveau le code de service en utilisant l’infrastructure de gestion du cycle de vie d’application dans Service Fabric.

#### <a name="optional-update-setupentrypoint"></a>Facultatif : mettre à jour SetupEntrypoint
```xml
<SetupEntryPoint>
   <ExeHost>
       <Program>scripts\launchConfig.cmd</Program>
   </ExeHost>
</SetupEntryPoint>
```
L’élément SetupEntryPoint sert à spécifier un fichier exécutable ou de commandes qui doit être exécuté avant le lancement du code du service. Cette étape est facultative. Il n’est pas nécessaire de l’inclure si aucune procédure d’initialisation n’est requise. SetupEntrypoint est exécuté chaque fois que le service est redémarré.

Comme il n’existe qu’un seul paramètre SetupEntrypoint, les scripts d’installation doivent être regroupés dans un même fichier de commandes si l’installation de l’application nécessite plusieurs scripts. L’élément SetupEntrypoint peut exécuter n’importe quel type de fichier : exécutable, fichier de commandes, applet de commande PowerShell, etc. Pour en savoir plus, consultez la rubrique relative à la [configuration de l’élément SetupEntryPoint](service-fabric-application-runas-security.md).

Dans l’exemple ci-dessus, l’élément SetupEntryPoint exécute un fichier de commandes appelé `LaunchConfig.cmd`, qui se trouve dans le sous-répertoire `scripts` du répertoire du code (si l’on suppose que l’élément WorkingFolder est défini sur CodeBase).

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

L’élément `EntryPoint` dans le fichier de manifeste de service sert à spécifier comment lancer le service. L’élément `ExeHost` spécifie le fichier exécutable (et les arguments) à utiliser pour lancer le service.

* `Program` spécifie le nom de l’exécutable qui doit démarrer le service.
* `Arguments` spécifie les arguments qui doivent être passés au fichier exécutable. Il peut s’agir d’une liste de paramètres avec des arguments.
* `WorkingFolder` spécifie le répertoire de travail pour le processus qui va être démarré. Vous pouvez spécifier trois valeurs :
  * `CodeBase` indique que le répertoire de travail doit être défini sur le répertoire du code dans le package d’application (répertoire `Code` dans la structure de fichiers indiquée précédemment).
  * `CodePackage` indique que le répertoire de travail doit être défini sur la racine du package d’application (`GuestService1Pkg` dans la structure de fichiers indiquée précédemment).
    * `Work` spécifie que les fichiers sont placés dans un sous-répertoire appelé « work ».

L’élément WorkingFolder est utile pour définir le répertoire de travail correct, afin que des chemins d’accès relatifs puissent être utilisés par l’application ou des scripts d’initialisation.

#### <a name="update-endpoints-and-register-with-naming-service-for-communication"></a>Mettre à jour des points de terminaison et les inscrire auprès du service d’affectation de noms à des fins de communication
```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000" Type="Input" />
</Endpoints>

```
Dans l’exemple fourni précédemment, l’élément `Endpoint` spécifie les points de terminaison que l’application peut écouter. Dans cet exemple, l’application Node.js écoute sur le port HTTP 3000.

En outre, vous pouvez demander à Service Fabric de publier ce point de terminaison auprès du service d’affectation de noms, afin que les autres services puissent découvrir l’adresse du point de terminaison de ce service. Ainsi, vous être en mesure d’assurer la communication entre les services qui sont des exécutables invités.
L’adresse du point de terminaison publié prend la forme `UriScheme://IPAddressOrFQDN:Port/PathSuffix`. `UriScheme` et `PathSuffix` sont des attributs facultatifs. `IPAddressOrFQDN` correspond à l’adresse IP ou au nom de domaine complet du nœud sur lequel est placé cet exécutable. Ce paramètre est calculé pour vous.

Dans l’exemple suivant, une fois que le service est déployé dans Service Fabric Explorer, vous pouvez voir un point de terminaison similaire à `http://10.1.4.92:3000/myapp/` publié pour l’instance de service. S’il s’agit d’un ordinateur local, vous verrez`http://localhost:3000/myapp/`.

```xml
<Endpoints>
   <Endpoint Name="NodeAppTypeEndpoint" Protocol="http" Port="3000"  UriScheme="http" PathSuffix="myapp/" Type="Input" />
</Endpoints>
```
Vous pouvez utiliser ces adresses avec le [proxy inverse](service-fabric-reverseproxy.md) pour la communication entre les services.

### <a name="edit-the-application-manifest-file"></a>Modifiez le fichier de manifeste d’application
Après avoir configuré le fichier `Servicemanifest.xml`, vous devez apporter des modifications au fichier `ApplicationManifest.xml` afin de garantir que le type et le nom du service utilisés sont corrects.

```xml
<?xml version="1.0" encoding="utf-8"?>
<ApplicationManifest xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" ApplicationTypeName="NodeAppType" ApplicationTypeVersion="1.0" xmlns="http://schemas.microsoft.com/2011/01/fabric">
   <ServiceManifestImport>
      <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
   </ServiceManifestImport>
</ApplicationManifest>
```

#### <a name="servicemanifestimport"></a>ServiceManifestImport
Dans l’élément `ServiceManifestImport` , vous pouvez spécifier un ou plusieurs services à inclure dans l’application. Les services sont référencés avec `ServiceManifestName`, qui spécifie le nom du répertoire dans lequel se trouve le fichier `ServiceManifest.xml`.

```xml
<ServiceManifestImport>
  <ServiceManifestRef ServiceManifestName="NodeApp" ServiceManifestVersion="1.0.0.0" />
</ServiceManifestImport>
```

## <a name="set-up-logging"></a>Configurez la journalisation
Pour les exécutables invités, il est utile de pouvoir consulter les journaux de la console afin de déterminer si les scripts de l’application et de configuration affichent une erreur.
La redirection de la console peut être configurée dans le fichier `ServiceManifest.xml` à l’aide de l’élément `ConsoleRedirection`.

> [!WARNING]
> N’utilisez jamais la stratégie de redirection de console dans une application déployée dans un environnement de production, car cela peut affecter le basculement de l’application. N’utilisez cette stratégie *que* pour le développement local et à des fins de débogage.  
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

`ConsoleRedirection` peut être utilisé pour rediriger la sortie de la console (stdout et stderr) vers un répertoire de travail. Cela permet de vérifier qu’aucune erreur ne s’est produite au cours de l’installation ou de l’exécution de l’application dans le cluster Service Fabric.

`FileRetentionCount` détermine le nombre de fichiers enregistrés dans le répertoire de travail. La valeur 5, par exemple, signifie que les fichiers journaux des cinq précédentes exécutions sont stockés dans le répertoire de travail.

`FileMaxSizeInKb` spécifie la taille maximale des fichiers journaux.

Les fichiers journaux sont enregistrés dans un des répertoires de travail du service. Pour déterminer l’emplacement des fichiers, utilisez Service Fabric Explorer afin d’identifier le nœud que le service exécute et le répertoire de travail utilisé. Cette procédure est décrite ultérieurement dans cet article.

## <a name="deployment"></a>Déploiement
La dernière étape consiste à [déployer votre application](service-fabric-deploy-remove-applications.md). Le script PowerShell ci-dessous indique comment déployer votre application dans le cluster de développement local et comment démarrer un nouveau service Service Fabric.

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
> [Compressez le package](service-fabric-package-apps.md#compress-a-package) avant de le copier dans le magasin d’images s’il est volumineux ou s’il contient de nombreux fichiers. En savoir plus [ici](service-fabric-deploy-remove-applications.md#upload-the-application-package).
>

Plusieurs configurations différentes peuvent être utilisées pour déployer un service Service Fabric. Par exemple, il peut être déployé sous la forme d’une ou de plusieurs instances, ou de manière à ce qu’il existe une seule instance du service sur chaque nœud du cluster Service Fabric.

Le paramètre `InstanceCount` de l’applet de commande `New-ServiceFabricService` permet de spécifier le nombre d’instances du service qui doivent être lancées dans le cluster Service Fabric. Vous pouvez définir la valeur `InstanceCount` selon le type d’application que vous déployez. Les deux scénarios les plus courants sont :

* `InstanceCount = "1"`. Dans ce cas, une seule instance du service est déployée sur le cluster. Le planificateur de Service Fabric détermine le nœud sur lequel le service sera déployé.
* `InstanceCount ="-1"`. Dans ce cas, une seule instance du service est déployée sur chaque nœud du cluster Service Fabric. Nous obtenons une seule (et unique) instance du service pour chaque nœud du cluster.

Cette configuration est utile pour les applications frontales (par exemple, un point de terminaison REST), car les applications clientes doivent simplement « se connecter » à l’un des nœuds du cluster afin d’utiliser le point de terminaison. Cette configuration peut également être utilisée lorsque, par exemple, tous les nœuds du cluster Service Fabric sont connectés à un équilibrage de charge. Le trafic client peut ensuite être distribué au sein du service qui s’exécute sur tous les nœuds du cluster.

## <a name="check-your-running-application"></a>Vérification de votre application en cours d'exécution
Dans l'Explorateur Service Fabric, identifiez le nœud sur lequel le service s'exécute. Dans cet exemple, il s’exécute sur le nœud 1 :

![Nœud sur lequel le service est en cours d’exécution](./media/service-fabric-deploy-existing-app/nodeappinsfx.png)

Si vous accédez au nœud, puis à l’application, vous voyez apparaître des informations essentielles sur le nœud, notamment son emplacement sur le disque.

![Emplacement sur le disque](./media/service-fabric-deploy-existing-app/locationondisk2.png)

Si vous accédez au répertoire à l’aide de l’Explorateur de serveurs, vous trouverez le répertoire de travail et le dossier des journaux du service, comme indiqué dans la capture d’écran suivante : 

![Emplacement du journal](./media/service-fabric-deploy-existing-app/loglocation.png)

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris à empaqueter un exécutable invité et à le déployer dans Service Fabric. Consultez les articles suivants pour obtenir des informations supplémentaires et connaître les tâches connexes.

* [Exemple pour empaqueter et déployer un exécutable invité](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started), avec un lien vers la version préliminaire de l’outil d’empaquetage
* [Exemple de deux exécutables invités (C# et nodejs) communiquant via le service d’attribution de noms à l’aide de REST](https://github.com/Azure-Samples/service-fabric-containers)
* [Déploiement de plusieurs exécutables invités](service-fabric-deploy-multiple-apps.md)
* [Créez votre première application Service Fabric avec Visual Studio](service-fabric-create-your-first-application-in-visual-studio.md)
