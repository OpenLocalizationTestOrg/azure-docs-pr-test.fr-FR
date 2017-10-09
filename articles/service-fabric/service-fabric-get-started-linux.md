---
title: "aaaSet de votre environnement de développement sur Linux | Documents Microsoft"
description: "Installer le runtime de hello et Kit de développement logiciel et créez un cluster de développement local sur Linux. Après avoir terminé cette installation, vous serez prêt toobuild applications."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: d552c8cd-67d1-45e8-91dc-871853f44fc6
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/23/2017
ms.author: subramar
ms.openlocfilehash: 9d82c2015f9e2c6fb55f2052c7cdb1e906c5deeb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="prepare-your-development-environment-on-linux"></a>Préparer votre environnement de développement sur Linux
> [!div class="op_single_selector"]
> * [Windows](service-fabric-get-started.md)
> * [Linux](service-fabric-get-started-linux.md)
> * [OSX](service-fabric-get-started-mac.md)
>
>  

toodeploy et exécutez [les applications Azure Service Fabric](service-fabric-application-model.md) sur votre ordinateur de développement Linux, installer hello runtime et le Kit de développement logiciel courants. Vous pouvez également installer les Kits de développement logiciel (SDK) facultatifs pour Java et .NET Core.

## <a name="prerequisites"></a>Composants requis

Hello versions de système d’exploitation suivantes est prises en charge pour le développement :

* Ubuntu 16.04 (`Xenial Xerus`)

## <a name="update-your-apt-sources"></a>Mise à jour des sources APT
tooinstall hello SDK et hello runtime associé package via l’outil de ligne de commande get-apt hello, vous devez tout d’abord mettre à jour vos sources de l’outil de mise en package avancées (APT).

1. Ouvrez un terminal.
2. Ajouter la liste de sources de hello Service Fabric référentiel tooyour.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] http://apt-mo.trafficmanager.net/repos/servicefabric/ xenial main" > /etc/apt/sources.list.d/servicefabric.list'
    ```

3. Ajouter hello `dotnet` liste des sources de référentiel tooyour.

    ```bash
    sudo sh -c 'echo "deb [arch=amd64] https://apt-mo.trafficmanager.net/repos/dotnet-release/ xenial main" > /etc/apt/sources.list.d/dotnetdev.list'
    ```

4. Ajouter hello nouvelle garde de confidentialité Gnu (GnuPG ou GPG) clé tooyour APT trousseau de clés.

    ```bash
    sudo apt-key adv --keyserver apt-mo.trafficmanager.net --recv-keys 417A0893
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys 417A0893
    ```

5. Ajoutez hello officiel Docker GPG tooyour clé APT porte-clé.

    ```bash
    sudo apt-get install curl
    sudo curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    ```

6. Configurer le référentiel de Docker hello.

    ```bash
    sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
    ```

7. Actualiser votre package listes selon hello nouvellement ajouté référentiels.

    ```bash
    sudo apt-get update
    ```

## <a name="install-and-set-up-hello-sdk-for-local-cluster-setup"></a>Installer et configurer hello Kit de développement logiciel pour le programme d’installation de cluster local

Une fois que vous avez mis à jour vos sources, vous pouvez installer hello SDK. Installer le package de Service Fabric SDK hello, vérifier l’installation de hello et acceptez le contrat de licence toohello.

```bash
sudo apt-get install servicefabricsdkcommon
```

>   [!TIP]
>   Hello commandes suivantes automatisent acceptant licence hello pour les packages de Service Fabric :
>   ```bash
>   echo "servicefabric servicefabric/accepted-eula-v1 select true" | sudo debconf-set-selections
>   echo "servicefabricsdkcommon servicefabricsdkcommon/accepted-eula-v1 select true" | sudo debconf-set-selections
>   ```

## <a name="set-up-a-local-cluster"></a>Configurer un cluster local
  Si l’installation de hello est réussie, vous devez être en mesure de toostart un cluster local.

  1. Exécutez le script d’installation de cluster hello.

      ```bash
      sudo /opt/microsoft/sdk/servicefabric/common/clustersetup/devclustersetup.sh
      ```

  2. Ouvrez un navigateur web et accédez trop[Service Fabric Explorer](http://localhost:19080/Explorer). Si le cluster de hello a démarré, vous devez voir le tableau de bord de Service Fabric Explorer hello.

      ![Service Fabric Explorer sur Linux][sfx-linux]

  À ce stade, vous pouvez déployer des packages d’application Service Fabric préconfigurés ou de nouveaux packages basés sur des conteneurs invités ou des exécutables invités. toobuild de nouveaux services à l’aide de Java de hello ou les kits de développement logiciel de .NET Core, les étapes hello facultatives d’installation qui sont fournies dans les sections suivantes.


  > [!NOTE]
  > Les clusters autonomes ne sont pas pris en charge sous Linux. prend en charge l’aperçu Hello uniquement une case et Azure Linux des clusters comportant plusieurs ordinateurs.
  >

## <a name="set-up-hello-service-fabric-cli"></a>Configurer hello CLI de l’infrastructure de Service

Hello [Service Fabric CLI](service-fabric-cli.md) dispose des commandes pour interagir avec les entités de Service Fabric, y compris des clusters et des applications. Il est basé sur python, soyez sûr toohave python et pip installé avant de poursuivre hello de commande suivante :

```bash
pip install sfctl
```

## <a name="install-and-set-up-hello-generators-for-containers-and-guest-executables"></a>Installer et configurer des générateurs de hello pour les conteneurs et les fichiers exécutables de l’invité
Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Service Fabric depuis le terminal à l’aide du générateur de modèle Yeoman. Veuillez suivre les étapes de hello ci-dessous tooensure que vous possédez Générateur de modèle yeoman hello Service Fabric pour travailler sur votre ordinateur.

1. Installer nodejs et NPM sur votre machine

  ```bash
  sudo apt-get install npm
  sudo apt install nodejs-legacy
  ```
2. Installer le générateur de modèles [Yeoman](http://yeoman.io/) sur votre machine à partir de NPM

  ```bash
  sudo npm install -g yo
  ```
3. Installer le Générateur de conteneur de Service Fabric yo hello et Générateur d’execuatble invité à partir de NPM

  ```bash
  sudo npm install -g generator-azuresfcontainer  # for Service Fabric container application
  sudo npm install -g generator-azuresfguest      # for Service Fabric guest executable application
  ```

Après avoir installé hello au-dessus des générateurs, vous devez être en mesure de toocreate des applications avec les services d’invité exécutable ou un conteneur en exécutant `yo azuresfguest` ou `yo azuresfcontainer` respectivement.

## <a name="install-hello-necessary-java-artifacts-optional-if-you-want-toouse-hello-java-programming-models"></a>Installer les artefacts Java hello nécessaires (facultatifs, si vous souhaitez que toouse hello Java de modèles de programmation)

les services de Service Fabric toobuild à l’aide de Java, vous assurer 1.8 JDK installé avec Gradle qui est utilisé pour exécuter des tâches de génération. Hello suivant extrait installe Open JDK 1.8, ainsi que de Gradle. bibliothèques de Service Fabric Java Hello sont extraites à partir de Maven.

  ```bash
  sudo apt-get install openjdk-8-jdk-headless
  sudo apt-get install gradle
  ```

## <a name="install-hello-eclipse-neon-plug-in-optional"></a>Installer hello Neon Eclipse plug-in (facultatif)

Vous pouvez installer hello Eclipse plug-in pour l’infrastructure de Service à partir de hello **IDE Eclipse pour développeurs Java**. Vous pouvez utiliser les applications exécutables d’Eclipse toocreate Service Fabric invité et les applications de conteneur dans les applications de l’infrastructure Java tooService Ajout.

1. Dans Eclipse, assurez-vous qu’avoir dernière Eclipse Neon hello version la plus récente Buildship (1.0.17 ou version ultérieure) installé. Vous pouvez vérifier les versions des composants installés hello en sélectionnant **aide** > **détails de l’Installation**. Vous pouvez mettre à jour Buildship à l’aide d’instructions hello à [Eclipse Buildship : Eclipse Plug-ins pour Gradle][buildship-update].

2. tooinstall hello sélectionnez de plug-in, Service Fabric **aide** > **installer le nouveau logiciel**.

3. Bonjour **travailler avec** , tapez **http://dl.microsoft.com/eclipse**.

4. Cliquez sur **Add**.

    ![page de logiciels disponibles Hello][sf-eclipse-plugin]

5. Sélectionnez hello **ServiceFabric** plug-in, puis cliquez sur **suivant**.

6. Complétez les étapes d’installation hello et puis acceptez le contrat de licence utilisateur final hello.

Si vous avez déjà hello Eclipse de l’infrastructure du Service plug-in installé, assurez-vous que vous avez la version la plus récente hello. Vous pouvez vérifier en sélectionnant **aide** > **détails de l’Installation** et puis en recherchant l’infrastructure de Service dans la liste hello des plug-ins installés. Si une version plus récente est disponible, sélectionnez **Mettre à jour**.

Pour plus d’informations, consultez la section [Plug-in Service Fabric pour le développement d’applications Java sous Eclipse](service-fabric-get-started-eclipse.md).


## <a name="install-hello-net-core-sdk-optional-if-you-want-toouse-hello-net-core-programming-models"></a>Installer hello .NET Core Kit de développement logiciel (facultatif, si vous souhaitez que les modèles de programmation .NET Core hello toouse)
Hello .NET Core SDK fournit des bibliothèques de hello et modèles qui sont des services de Service Fabric toobuild requis avec le .NET Core. Installer de kit de développement .NET Core hello par les éléments suivants de hello en cours d’exécution :

   ```bash
   sudo apt-get install servicefabricsdkcsharp
   ```

## <a name="update-hello-sdk-and-runtime"></a>Hello de mise à jour SDK et d’exécution

version la plus récente toohello tooupdate de hello SDK et d’exécution, exécutez hello suivant les commandes (désélectionnez les kits de développement logiciel hello que vous ne souhaitez pas) :

```bash
sudo apt-get update
sudo apt-get install servicefabric servicefabricsdkcommon servicefabricsdkcsharp
```
tooupdate hello Kit de développement logiciel Java fichiers binaires à partir de Maven, vous devez tooupdate détails sur la version hello du binaire correspondant de hello Bonjour ``build.gradle`` version plus récente du fichier toopoint toohello. tooknow là où vous avez besoin tooupdate version de hello, vous pouvez faire référence tooany ``build.gradle`` fichier dans les exemples de prise en main de Service Fabric [ici](https://github.com/Azure-Samples/service-fabric-java-getting-started).

> [!NOTE]
> Mise à jour les packages hello risque de votre toostop de cluster de développement local en cours d’exécution. Redémarrez votre cluster local après une mise à niveau en suivant les instructions de hello sur cette page.

## <a name="next-steps"></a>Étapes suivantes

* [Créer et déployer votre première application Java Service Fabric sous Linux à l’aide de Yeoman](service-fabric-create-your-first-linux-application-with-java.md)
* [Créer et déployer votre première application Java Service Fabric sous Linux à l’aide du plug-in Service Fabric pour Eclipse](service-fabric-get-started-eclipse.md)
* [Create your first Java application on Linux (Créer votre première application Java sur Linux)](service-fabric-create-your-first-linux-application-with-csharp.md)
* [Prepare your development environment on OSX (Préparer votre environnement de développement sur OSX)](service-fabric-get-started-mac.md)
* [Utiliser hello Service Fabric CLI toomanage vos applications](service-fabric-application-lifecycle-sfctl.md)
* [Différences entre Service Fabric Windows/Linux](service-fabric-linux-windows-differences.md)
* [Prise en main de l’interface de ligne de commande Service Fabric](service-fabric-cli.md)

<!-- Links -->

[azure-xplat-cli-github]: https://github.com/Azure/azure-xplat-cli
[install-node]: https://nodejs.org/en/download/package-manager/#installing-node-js-via-package-manager
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship

<!--Images -->

[sf-eclipse-plugin]: ./media/service-fabric-get-started-linux/service-fabric-eclipse-plugin.png
[sfx-linux]: ./media/service-fabric-get-started-linux/sfx-linux.png
