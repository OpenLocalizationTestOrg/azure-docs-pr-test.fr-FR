---
title: "aaaQuickly déployer un cluster de Azure Service Fabric application tooan existant"
description: Utilisez un toohost de cluster Azure Service Fabric une application Node.js existante avec Visual Studio.
services: service-fabric
documentationcenter: nodejs
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: hero-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/13/2017
ms.author: adegeo
ms.openlocfilehash: 20a3eb4a9206ba465acf96d0976ba241b07158bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="host-a-nodejs-application-on-azure-service-fabric"></a>Héberger une application Node.js sur Microsoft Azure Service Fabric

Ce démarrage rapide vous permet de déployer un cluster de l’infrastructure de Service de tooa (Node.js dans cet exemple) d’application existant en cours d’exécution sur Azure.

## <a name="prerequisites"></a>Composants requis

Avant de commencer, assurez-vous que vous avez bien [configuré votre environnement de développement](service-fabric-get-started.md). Qui inclut l’installation de type hello Service Fabric SDK et Visual Studio 2017 ou 2015.

Vous devez également toohave une application Node.js existante pour le déploiement. Ce démarrage rapide utilise un site web Node.js simple qui peut être téléchargé [ici][download-sample]. Extraire ce fichier tooyour `<path-to-project>\ApplicationPackageRoot\<package-name>\Code\` dossier après avoir créé un projet de hello dans l’étape suivante de hello.

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit][create-account].

## <a name="create-hello-service"></a>Créer le service de hello

Lancez Visual Studio en tant qu’**administrateur**.

Créer un projet avec `CTRL`+`SHIFT`+`N`

Bonjour **nouveau projet** boîte de dialogue, choisissez **Cloud > Application Service Fabric**.

Nommez l’application hello **MyGuestApp** et appuyez sur **OK**.

>[!IMPORTANT]
>Node.js peuvent facilement s’interrompre hello 260 caractères pour les tracés qui dispose de windows. Utilisez un chemin d’accès court pour le projet hello lui-même comme **c:\code\svc1**.
   
![Boîte de dialogue Nouveau projet dans Visual Studio][new-project]

Vous pouvez créer n’importe quel type de service Service Fabric à partir de la boîte de dialogue suivante hello. Pour ce démarrage rapide, choisissez **Exécutable invité**.

Nom de votre service de hello **MyGuestService** et définir les options de hello sur toohello de droite hello des valeurs suivantes :

| Paramètre                   | Valeur |
| ------------------------- | ------ |
| Dossier du package de code       | _&lt;dossier Hello avec votre application Node.js&gt;_ |
| Comportement du package de code     | Copiez le dossier contenu tooproject |
| Programme                   | node.exe |
| Arguments                 | server.js |
| Dossier de travail            | CodePackage |

Appuyez sur **OK**.

![Boîte de dialogue Nouveau service dans Visual Studio.][new-service]

Visual Studio crée le projet d’application hello et de projet de service d’acteur hello et les affiche dans l’Explorateur de solutions.

projet d’application Hello (**MyGuestApp**) ne contient pas de code directement. Au lieu de cela, il fait référence à un ensemble de projets de service. En outre, il contient trois autres types de contenu :

* **Profils de publication**  
Préférences d’outils pour différents environnements.

* **Scripts**  
Script PowerShell de déploiement/mise à niveau de votre application.

* **Définition d’application**  
Inclut le manifeste de l’application hello sous *ApplicationPackageRoot*. Fichiers de paramètres d’application associée sont sous *ApplicationParameters*, qui définissent l’application hello et vous tooconfigure spécifiquement pour un environnement donné.
    
Pour une vue d’ensemble du contenu hello hello du projet de service, consultez [prise en main des Services fiables](service-fabric-reliable-services-quick-start.md).

## <a name="set-up-networking"></a>Configurer la mise en réseau

exemple Hello application Node.js nous mettons déploiement utilise le port **80** et nous devons tootell Service Fabric dont nous avons besoin que le port exposé.

Ouvrez hello **ServiceManifest.xml** fichier de projet de hello. Bas hello du manifeste de hello, il existe un `<Resources> \ <Endpoints>` avec une entrée déjà définie. Modifier cette entrée tooadd `Port`, `Protocol`, et `Type`. 

```xml
  <Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Name="MyGuestAppServiceTypeEndpoint" Port="80" Protocol="http" Type="Input" />
    </Endpoints>
  </Resources>
```

## <a name="deploy-tooazure"></a>Déployer tooAzure

Si vous appuyez sur **F5** et exécutez hello projet, il est déployé toohello les cluster local. Toutefois, nous allons déployer tooAzure à la place.

Avec le bouton droit sur le projet de hello et choisissez **publier...**  qui ouvre un tooAzure toopublish de boîte de dialogue.

![Boîte de dialogue tooazure pour un service service fabric publier][publish]

Sélectionnez hello **PublishProfiles\Cloud.xml** cibler profile.

Si vous n’avez pas précédemment, choisissez un toodeploy compte Azure à. Si vous n’en avez pas, [obtenez-en un][create-account].

Sous **point de terminaison de connexion**, sélectionnez hello toodeploy du cluster Service Fabric pour. Si vous n’avez pas une option, sélectionnez  **&lt;créer un nouveau Cluster... &gt;**  qui ouvre toohello de fenêtre de navigateur web portail Azure. Pour plus d’informations, consultez [créer un cluster dans le portail de hello](service-fabric-cluster-creation-via-portal.md#create-cluster-in-the-azure-portal). 

Lorsque vous créez le cluster Service Fabric de hello, assurez-vous que tooset hello **les points de terminaison personnalisé** aussi un paramètre**80**.

![Configuration de type nœud Service Fabric avec le point de terminaison personnalisé][custom-endpoint]

Création d’un nouveau cluster Service Fabric prend quelques toocomplete de temps. Une fois qu’il a été créé, accédez toohello arrière boîte de dialogue Publier et sélectionnez  **&lt;Actualiser&gt;**. nouveau cluster de Hello est répertorié dans la zone de liste déroulante hello. Sélectionnez-la.

Appuyez sur **publier** et attendez hello déploiement toofinish.

Cela peut prendre quelques minutes. Après avoir terminé, il peut prendre quelques minutes pour toobe d’application hello entièrement disponible.

## <a name="test-hello-website"></a>Site Web de test hello

Une fois que votre service a été publié, testez-le dans un navigateur web. 

Tout d’abord, ouvrez hello portail Azure et trouver votre service Service Fabric.

Vérifiez le panneau de vue d’ensemble de hello d’adresse de service hello. Nom de domaine hello utilisation à partir de hello _point de terminaison de connexion Client_ propriété. Par exemple, `http://mysvcfab1.westus2.cloudapp.azure.com`.

![Panneau de vue d’ensemble de l’infrastructure de service sur hello portail Azure][overview]

Accédez adresse toothis où vous verrez hello `HELLO WORLD` réponse.

## <a name="delete-hello-cluster"></a>Supprimer le cluster de hello

N’oubliez pas de toodelete toutes les ressources hello que vous avez créé pour ce démarrage rapide, en tant que vous êtes facturés pour ces ressources.

## <a name="next-steps"></a>Étapes suivantes
Apprenez-en davantage sur les [exécutables invités](service-fabric-deploy-existing-app.md).

<!-- Image References -->

[new-project]: ./media/quickstart-guest-app/new-project.png
[new-service]: ./media/quickstart-guest-app/template.png
[solution-exp]: ./media/quickstart-guest-app/solution-explorer.png
[publish]: ./media/quickstart-guest-app/publish.png
[overview]: ./media/quickstart-guest-app/overview.png
[custom-endpoint]: ./media/quickstart-guest-app/custom-endpoint.png

[download-sample]: https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/service-fabric-node-website.zip
[create-account]: https://azure.microsoft.com/free/?WT.mc_id=A261C142F