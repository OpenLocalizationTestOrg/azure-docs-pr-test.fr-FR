---
title: "Déployer une application Azure Service Fabric sur un cluster tiers | Microsoft Docs"
description: "Découvrez comment déployer une application sur un cluster tiers."
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: msfussell
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: mikhegn
ms.openlocfilehash: 6624d683edb548a65d07ab4012c599faaf940ed0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/18/2017
---
# <a name="deploy-an-application-to-a-party-cluster-in-azure"></a>Déployer une application sur un cluster tiers dans Azure
Deuxième d’une série, ce didacticiel vous montre comment déployer une application Azure Service Fabric sur un cluster tiers dans Azure.

Dans ce deuxième volet, vous apprenez à :
> [!div class="checklist"]
> * Déployer une application sur un cluster distant à l’aide de Visual Studio
> * Supprimer une application d’un cluster à l’aide de Service Fabric Explorer

Cette série de didacticiels vous montre comment effectuer les opérations suivantes :
> [!div class="checklist"]
> * [Créer une application .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * Déployer l’application sur un cluster distant
> * [Configurer l’intégration et le déploiement continus à l’aide de Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel :
- Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Installez Visual Studio 2017](https://www.visualstudio.com/) et les charges de travail **Développement Azure** et **Développement web et ASP.NET**.
- [Installez le Kit de développement logiciel (SDK) Service Fabric](service-fabric-get-started.md).

## <a name="download-the-voting-sample-application"></a>Télécharger l’exemple d’application de vote
Si vous n’avez pas généré l’exemple d’application de vote lors de la [première partie de cette série de didacticiels](service-fabric-tutorial-create-dotnet-app.md), vous pouvez le télécharger. Dans une fenêtre Commande, exécutez la commande suivante pour cloner le référentiel de l’exemple d’application sur votre ordinateur local.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>Configurer un cluster tiers
Les clusters tiers sont des clusters Service Fabric gratuits et limités dans le temps. Ils sont hébergés sur Azure et exécutés par l’équipe Service Fabric, dont tous les membres peuvent déployer des applications et en savoir plus sur la plateforme gratuitement.

Pour accéder à un cluster tiers, rendez-vous sur le site http://aka.ms/tryservicefabric et suivez les instructions. Vous avez besoin d’un compte Facebook ou GitHub pour accéder à un cluster tiers.

> [!NOTE]
> Les clusters tiers ne sont pas sécurisés. Vos applications et toutes les données que vous y placez sont donc visibles par d’autres personnes. Ne déployez aucun élément que vous souhaitez cacher aux autres utilisateurs. Veillez à lire les conditions d’utilisation pour plus d’informations.

## <a name="configure-the-listening-port"></a>Configurer le port d’écoute
Lorsque le service frontal VotingWeb est créé, Visual Studio sélectionne de manière aléatoire le port d’écoute du service.  Le service VotingWeb joue le rôle de serveur frontal de cette application et accepte le trafic externe. Associez ce service à un port fixe et connu. Dans l’Explorateur de solutions, ouvrez *VotingWeb/PackageRoot/ServiceManifest.xml*.  Recherchez la ressource **Endpoint** dans la section **Resources**, puis remplacez la valeur du **port** par 80.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by the communication listener to obtain the port on which to 
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

Mettez également à jour la valeur de la propriété d’URL d’application dans le projet Voting, afin qu’un navigateur web s’ouvre sur le port adéquat lorsque vous effectuez le débogage en appuyant sur F5.  Dans l’Explorateur de solutions, sélectionnez le projet **Voting** et mettez à jour la propriété **URL de l’application**.

![URL de l’application](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-the-app-to-the-azure"></a>Déployer l’application dans Azure
Maintenant que l’application est prête, vous pouvez la déployer sur le cluster tiers directement à partir de Visual Studio.

1. Dans l’Explorateur de solutions, cliquez avec le bouton droit sur **Voting**, puis choisissez **Publier**.

    ![Boîte de dialogue Publier](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. Saisissez le point de terminaison de connexion du cluster tiers dans le champ **Point de terminaison de connexion** et cliquez sur **Publier**.

    Une fois la publication terminée, vous devez être en mesure d’envoyer une demande à l’application via un navigateur.

3. Ouvrez le navigateur de votre choix et saisissez l’adresse du cluster (le point de terminaison de connexion sans les informations de port ; par exemple, win1kw5649s.westus.cloudapp.azure.com).

    Vous devez maintenant obtenir le même résultat que lors de l’exécution de l’application en local.

    ![Réponse de l’API à partir du cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-the-application-from-a-cluster-using-service-fabric-explorer"></a>Supprimer l’application d’un cluster à l’aide de Service Fabric Explorer
Service Fabric Explorer est une interface utilisateur graphique qui permet d’explorer et de gérer des applications dans un cluster Service Fabric.

Pour supprimer l’application du cluster tiers :

1. Accédez à Service Fabric Explorer à l’aide du lien fourni sur la page d’inscription du cluster tiers. Par exemple, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.

2. Dans Service Fabric Explorer, accédez au nœud **fabric://Voting**, dans l’arborescence figurant sur le côté gauche.

3. Cliquez sur le bouton **Action** dans le volet **Essentials** à droite, puis choisissez **Supprimer l’application**. Confirmez la suppression de l’instance d’application, ce qui supprime l’instance de notre application en cours d’exécution dans le cluster.

![Supprimer l’application dans Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-the-application-type-from-a-cluster-using-service-fabric-explorer"></a>Supprimer le type d’application d’un cluster à l’aide de Service Fabric Explorer
Les applications sont déployées en tant que types d’applications dans un cluster Service Fabric, ce qui vous permet d’avoir plusieurs instances et versions de l’application en cours d’exécution au sein du cluster. Après avoir supprimé l’instance en cours d’exécution de notre application, nous pouvons également supprimer le type pour nettoyer le déploiement.

Pour plus d’informations sur le modèle d’application dans Service Fabric, consultez [Modéliser une application dans Service Fabric](service-fabric-application-model.md).

1. Accédez au nœud **VotingType** dans l’arborescence.

2. Cliquez sur le bouton **Action** dans le volet **Essentials** à droite, puis choisissez **Unprovision Type** (Annuler la mise en service du type). Confirmez l’annulation de la mise en service du type d’application.

![Annuler la mise en service du type d’application dans Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

Cela conclut le didacticiel.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Déployer une application sur un cluster distant à l’aide de Visual Studio
> * Supprimer une application d’un cluster à l’aide de Service Fabric Explorer

Passez au didacticiel suivant :
> [!div class="nextstepaction"]
> [Configurer l’intégration continue avec Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)