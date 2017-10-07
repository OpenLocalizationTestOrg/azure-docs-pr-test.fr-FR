---
title: "aaaCreate votre première application Azure microservices sur Linux à l’aide de C# | Documents Microsoft"
description: "Créer et déployer une application Service Fabric à l’aide de C#"
services: service-fabric
documentationcenter: csharp
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: 5a96d21d-fa4a-4dc2-abe8-a830a3482fb1
ms.service: service-fabric
ms.devlang: csharp
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/21/2017
ms.author: subramar
ms.openlocfilehash: 68d685e130be338ebcdb2f1af24b66d1e14f580a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-azure-service-fabric-application"></a>Créer votre première application Azure Service Fabric
> [!div class="op_single_selector"]
> * [C# - Windows](service-fabric-create-your-first-application-in-visual-studio.md)
> * [Java - Linux](service-fabric-create-your-first-linux-application-with-java.md)
> * [C# - Linux](service-fabric-create-your-first-linux-application-with-csharp.md)
>
>

Service Fabric fournit des Kits de développement logiciel (SDK) pour générer des services Linux dans .NET Core et Java. Dans ce didacticiel, nous abordons la façon dont une application pour Linux et génération d’un service à l’aide de c# (.NET Core) de toocreate.

## <a name="prerequisites"></a>Composants requis
Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement Linux](service-fabric-get-started-linux.md). Si vous utilisez Mac OS X, vous pouvez [configurer un environnement Linux à boîtier unique sur une machine virtuelle à l’aide de Vagrant](service-fabric-get-started-mac.md).

Vous pouvez également tooinstall hello [CLI de l’infrastructure de Service](service-fabric-cli.md)

### <a name="install-and-set-up-hello-generators-for-csharp"></a>Installer et configurer des générateurs de hello pour CSharp
Service Fabric fournit des outils de génération de modèles automatique qui vous aideront à créer une application Service Fabric CSharp à partir du terminal à l’aide du générateur de modèles Yeoman. Veuillez suivre les étapes de hello ci-dessous tooensure que vous avez Générateur de modèle yeoman hello Service Fabric pour CSharp vous travaillez sur votre ordinateur.
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
  sudo npm install -g generator-azuresfcsharp
  ```

## <a name="create-hello-application"></a>Créer l’application hello
Une application de Service Fabric peut contenir un ou plusieurs services, chacun avec un rôle spécifique dans la fonctionnalité de l’application hello de remise. Hello Service Fabric [Yeoman](http://yeoman.io/) toocreate facile rend générateur pour CSharp, que vous avez installés dans la dernière étape, votre premier service et tooadd plus ultérieurement. Nous allons utiliser Yeoman toocreate une application avec un seul service.

1. Dans un terminal, tapez Bonjour suivant toostart commande Création de la structure de hello :`yo azuresfcsharp`
2. Donnez un nom à votre application.
3. Choisissez le type hello de votre premier service et nommez-le. Pour des raisons de hello de ce didacticiel, nous choisissons un Service d’acteur fiable.

   ![Générateur Yeoman Service Fabric pour C#][sf-yeoman]

> [!NOTE]
> Pour plus d’informations sur les options de hello, consultez [Service Fabric, vue d’ensemble du modèle de programmation](service-fabric-choose-framework.md).
>
>

## <a name="build-hello-application"></a>Générez l’application hello
modèles de Service Fabric Yeoman Hello incluent un script de génération que vous pouvez utiliser l’application hello toobuild hello terminal (après la navigation dans le dossier d’application toohello).

  ```sh
 cd myapp
 ./build.sh
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

Une fois que l’application hello a été déployée, ouvrez un navigateur et accédez à [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) à [http://localhost:19080/Explorer](http://localhost:19080/Explorer). Développez ensuite hello **Applications** nœud et notez qu’il existe désormais une entrée pour votre type d’application et un autre pour la première instance de ce type de hello.

## <a name="start-hello-test-client-and-perform-a-failover"></a>Démarrer le client test hello et effectuer un basculement
Les projets d’acteur n’effectuent aucune opération automatiquement. Ils ont besoin d’un autre toosend de service ou le client les messages. modèle d’acteur Hello inclut un script de test simple que vous pouvez utiliser toointeract avec le service d’acteur hello.

1. Exécutez le script hello à l’aide de la sortie de hello hello espion utilitaire toosee du service d’acteur hello.

    ```bash
    cd myactorsvcTestClient
    watch -n 1 ./testclient.sh
    ```
2. Dans l’Explorateur de l’infrastructure de Service, recherchez le nœud qui héberge le réplica principal de hello pour le service d’acteur hello. Dans la capture d’écran de hello ci-dessous, il est nœud 3.

    ![Réplica principal de recherche hello dans Service Fabric Explorer][sfx-primary]
3. Cliquez sur le nœud hello vous trouvé à l’étape précédente de hello, puis sélectionnez **désactiver (Redémarrer)** à partir du menu d’Actions hello. Cette action redémarre un seul nœud dans votre application forcée d’un réplica secondaire de basculement tooa, en cours d’exécution sur un autre nœud de cluster local. Quand vous effectuez cette action, payer sortie de toohello une attention particulière à partir de client de test hello et notez que ce compteur hello continue tooincrement malgré hello basculement.

## <a name="adding-more-services-tooan-existing-application"></a>Ajout d’application existante de plusieurs services tooan

tooadd une autre application de tooan service déjà créé à l’aide de `yo`, effectuer hello comme suit :
1. Modifier la racine toohello du répertoire d’application existant hello.  Par exemple, `cd ~/YeomanSamples/MyApplication`si `MyApplication` est l’application hello créée par Yeoman.
2. Exécutez `yo azuresfcsharp:AddService`.

## <a name="migrating-from-projectjson-toocsproj"></a>Migration à partir de project.json too.csproj
1. Vous pouvez migrer les format hello project.json toocsproj 'dotnet migrate' dans le répertoire racine du projet en cours d’exécution.
2. Mise à jour hello projet référence en conséquence les fichiers toocsproj dans les fichiers projet.
3. Mettre à jour hello fichier noms toocsproj fichiers projet dans build.sh.

## <a name="next-steps"></a>Étapes suivantes

* [Présentation des Acteurs fiables Service Fabric](service-fabric-reliable-actors-introduction.md)
* [Interaction avec les clusters de l’infrastructure de Service à l’aide de hello CLI de l’infrastructure de Service](service-fabric-cli.md)
* En savoir plus sur les [options de prise en charge de Service Fabric](service-fabric-support.md)
* [Prise en main de l’interface de ligne de commande Service Fabric](service-fabric-cli.md)

<!-- Images -->
[sf-yeoman]: ./media/service-fabric-create-your-first-linux-application-with-csharp/yeoman-csharp.png
[sfx-primary]: ./media/service-fabric-create-your-first-linux-application-with-csharp/sfx-primary.png
