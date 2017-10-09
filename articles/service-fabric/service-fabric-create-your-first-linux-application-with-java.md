---
title: aaaCreate une application de Java Azure Service Fabric acteurs fiable sur Linux | Documents Microsoft
description: "Découvrez comment toocreate et déployer une application d’acteurs fiable Java Service Fabric dans cinq minutes."
services: service-fabric
documentationcenter: java
author: rwike77
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: ryanwi
ms.openlocfilehash: 11496b767811c89969c65d1682d843448eb6a922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-java-service-fabric-reliable-actors-application-on-linux"></a>Création de votre première application Java Service Fabric Reliable Actors
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Ce guide de démarrage rapide vous aide à créer votre première application Azure Service Fabric Java dans un environnement de développement Linux en quelques minutes.  Lorsque vous avez terminé, vous avez une application de service unique simple Java en cours d’exécution sur le cluster de développement local hello.  

## <a name="prerequisites"></a>Composants requis
Avant de commencer, installez hello Service Fabric SDK hello Service Fabric CLI et le programme d’installation d’un cluster de développement dans votre [environnement de développement Linux](service-fabric-get-started-linux.md). Si vous utilisez Mac OS X, vous pouvez [configurer un environnement de développement Linux sur une machine virtuelle à l’aide de Vagrant](service-fabric-get-started-mac.md).

Vous pouvez également tooinstall hello [Service Fabric CLI](service-fabric-cli.md).

### <a name="install-and-set-up-hello-generators-for-java"></a>Installer et configurer des générateurs de hello pour Java
Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Java Service Fabric à partir d’un terminal à l’aide du générateur de modèle Yeoman. Veuillez suivre les étapes de hello ci-dessous tooensure que vous avez Générateur de modèle yeoman hello Service Fabric pour Java vous travaillez sur votre ordinateur.
1. Installer nodejs et NPM sur votre machine

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM

  ```bash
  sudo npm install -g yo
  ```
3. Installer le Générateur d’applications hello Service Fabric yo Java à partir de NPM

  ```bash
  sudo npm install -g generator-azuresfjava
  ```

## <a name="create-hello-application"></a>Créer l’application hello
Une application de Service Fabric contient un ou plusieurs services, chacun avec un rôle spécifique dans la fonctionnalité de l’application hello de remise. Générateur Hello vous avez installé dans la dernière section de hello, rend facile toocreate votre premier service et tooadd plus ultérieurement.  Vous pouvez également créer, générer et déployer des applications Java Service Fabric à l’aide d’un plug-in d’Eclipse. Consultez les instructions de [création et déploiement de votre première application Java à l’aide d’Eclipse](service-fabric-get-started-eclipse.md). Pour ce guide de démarrage rapide, utilisez Yeoman toocreate une application avec un service unique qui stocke et obtient une valeur de compteur.

1. Saisissez ``yo azuresfjava`` dans un terminal.
2. Donnez un nom à votre application.
3. Choisissez le type hello de votre premier service et nommez-le. Pour ce didacticiel, choisissez un service Reliable Actors. Pour plus d’informations sur hello autres types de services, consultez [Service Fabric, vue d’ensemble du modèle de programmation](service-fabric-choose-framework.md).
   ![Générateur Yeoman Service Fabric pour Java][sf-yeoman]

## <a name="build-hello-application"></a>Générez l’application hello
modèles de Service Fabric Yeoman Hello incluent un script de génération pour [Gradle](https://gradle.org/), vous pouvez utiliser application hello toobuild hello Terminal Server.
Les dépendances Java Service Fabric ont été extraites de Maven. toobuild et utiliser des applications de Service Fabric Java hello, vous devez tooensure que JDK et Gradle sont installés. Si non encore installé, vous pouvez exécuter hello suivant tooinstall JDK(openjdk-8-jdk) et Gradle -

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

toobuild et package d’application hello, exécutez hello suivante :

  ```bash
  cd myapp
  gradle
  ```

## <a name="deploy-hello-application"></a>Déployer l’application hello
Une fois que l’application hello est générée, vous pouvez le déployer de cluster local de toohello.

1. Connectez le cluster Service Fabric local de toohello.

    ```bash
    sfctl cluster select --endpoint http://localhost:19080
    ```

2. Exécuter le script d’installation hello fournies dans hello modèle toocopy application hello magasin d’images du cluster toohello du package, inscrire le type d’application hello et créer une instance de l’application hello.

    ```bash
    ./install.sh
    ```

L’application hello généré déploiement est même hello comme toute autre application de Service Fabric. Consultez la documentation de hello sur [gérer une application Service Fabric avec hello Service Fabric CLI](service-fabric-application-lifecycle-sfctl.md) pour obtenir des instructions détaillées.

Commandes de toothese de paramètres sont accessibles dans les manifestes hello généré à l’intérieur du package d’application hello.

Une fois que l’application hello a été déployée, ouvrez un navigateur et accédez à [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) à [http://localhost:19080/Explorer](http://localhost:19080/Explorer).
Développez ensuite hello **Applications** nœud et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Démarrer le client test hello et effectuer un basculement
Acteurs ne font rien sur leurs propres, ils ont besoin d’un autre toosend de service ou le client les messages. modèle d’acteur Hello inclut un script de test simple que vous pouvez utiliser toointeract avec le service d’acteur hello.

1. Exécutez le script hello à l’aide de la sortie de hello hello espion utilitaire toosee du service d’acteur hello.  script de test Hello appelle hello `setCountAsync()` hello des appels de méthode sur hello acteur tooincrement un compteur, `getCountAsync()` méthode hello acteur tooget hello nouvelle valeur du compteur, et affiche cette valeur toohello console.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```

2. Dans l’Explorateur de l’infrastructure de Service, recherchez hello nœud hébergement hello réplica principal pour le service d’acteur hello. Dans la capture d’écran de hello ci-dessous, il est nœud 3. handles de réplica principal de service Hello lire et écrire des opérations.  Modifications d’état de service sont ensuite répliquées toohello réplicas secondaires, en cours d’exécution sur les nœuds 0 et 1 dans hello capture d’écran ci-dessous.

    ![Réplica principal de recherche hello dans Service Fabric Explorer][sfx-primary]

3. Dans **nœuds**, cliquez sur le nœud hello vous trouvé à l’étape précédente de hello, puis sélectionnez **désactiver (Redémarrer)** à partir du menu d’Actions hello. Cette action redémarre le nœud hello réplica du service principal hello en cours d’exécution et force un tooone de basculement des réplicas secondaires de hello en cours d’exécution sur un autre nœud.  Ce réplica secondaire est promue tooprimary, un autre réplica secondaire est créé sur un autre nœud et réplica principal de hello commence des opérations de lecture/écriture de tootake. Lors du redémarrage de nœud de hello, regardez la sortie hello de client de test hello et notez que ce compteur hello continue tooincrement malgré hello basculement.

## <a name="remove-hello-application"></a>Supprimer l’application hello
Utiliser le script de désinstallation hello fournie dans l’instance de l’application hello modèle toodelete hello, annulez l’inscription du package d’application hello et supprimer le package d’application hello à partir du magasin d’images du cluster hello.

```bash
./uninstall.sh
```

Dans l’Explorateur de l’infrastructure de Service, vous voyez qu’application hello et le type d’application n’apparaissent plus dans hello **Applications** nœud.

## <a name="service-fabric-java-libraries-on-maven"></a>Bibliothèques Java Service Fabric sur Maven
Les bibliothèques Java Service Fabric ont été hébergées dans Maven. Vous pouvez ajouter des dépendances de hello Bonjour ``pom.xml`` ou ``build.gradle`` de vos bibliothèques de Service Fabric Java toouse projets à partir de **mavenCentral**.

### <a name="actors"></a>Acteurs

Assistance Reliable Actor de Service Fabric pour votre application.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-actors-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-actors-preview:0.10.0'
  }
  ```

### <a name="services"></a>Services

Assistance des services sans état de Service Fabric pour votre application.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-services-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-services-preview:0.10.0'
  }
  ```

### <a name="others"></a>Autres
#### <a name="transport"></a>Transport

Assistance de la couche transport pour application Java Service Fabric. Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service, sauf si vous effectuez la programmation au niveau de la couche de transport hello.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-transport-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-transport-preview:0.10.0'
  }
  ```

#### <a name="fabric-support"></a>Assista,ce Fabric

Support de niveau système pour l’infrastructure de Service qui communique avec le runtime du Service Fabric toonative. Vous n’avez pas besoin tooexplicitly ajouter cette dépendance tooyour Reliable Actor ou les applications de Service. Il obtient extraites automatiquement à partir de Maven, lorsque vous incluez hello autres dépendances ci-dessus.

  ```XML
  <dependency>
      <groupId>com.microsoft.servicefabric</groupId>
      <artifactId>sf-preview</artifactId>
      <version>0.10.0</version>
  </dependency>
  ```

  ```gradle
  repositories {
      mavenCentral()
  }
  dependencies {
      compile 'com.microsoft.servicefabric:sf-preview:0.10.0'
  }
  ```

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Migration d’ancien toobe d’applications Java de l’infrastructure de Service utilisé avec Maven
Nous avons déplacé récemment bibliothèques Service Fabric Java à partir du référentiel de tooMaven Service Fabric Java SDK. Alors que hello nouvelles applications vous générez à l’aide de Yeoman ou Eclipse, générera une dernière version des projets mis à jour (qui seront en mesure de toowork avec Maven), vous pouvez mettre à jour votre Service Fabric existant sans état ou les applications Java acteur, qui utilisaient l’hello Service L’infrastructure du SDK Java précédemment, dépendances de Service Fabric Java hello toouse à partir de Maven. Suivez les étapes de hello mentionnés [ici](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure votre ancienne application fonctionne avec Maven.

## <a name="next-steps"></a>Étapes suivantes

* [Création de votre première application Java Service Fabric sur Linux à l’aide d’Eclipse](service-fabric-get-started-eclipse.md)
* [Présentation des Acteurs fiables Service Fabric](service-fabric-reliable-actors-introduction.md)
* [Interagir avec des clusters Service Fabric à l’aide de hello CLI de l’infrastructure de Service](service-fabric-cli.md)
* En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)
* [Prise en main de l’interface de ligne de commande Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-yeoman.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-java/sfx-primary.png
[sf-eclipse-templates]: ./media/service-fabric-create-your-first-linux-application-with-java/sf-eclipse-templates.png
