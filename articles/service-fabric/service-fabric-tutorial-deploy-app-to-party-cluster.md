---
title: "aaaDeploy un tooa d’application Azure Service Fabric tiers Cluster | Documents Microsoft"
description: "Découvrez comment toodeploy un tooa application partie du Cluster."
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
ms.openlocfilehash: db16b6418fa2533ed915c8b6e612b7a8e7311bed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-party-cluster-in-azure"></a>Déployer une application de tooa Cluster tiers dans Azure
Ce didacticiel fait partie de deux d’une série et vous montre comment toodeploy un tooa d’application Azure Service Fabric Cluster tiers dans Azure.

Dans la deuxième partie de la série de didacticiels hello, vous apprenez comment :
> [!div class="checklist"]
> * Déployer un cluster à distance tooa d’application à l’aide de Visual Studio
> * Supprimer une application d’un cluster à l’aide de Service Fabric Explorer

Cette série de didacticiels vous montre comment effectuer les opérations suivantes :
> [!div class="checklist"]
> * [Créer une application .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * Déployer le cluster de l’application hello tooa à distance
> * [Configurer l’intégration et le déploiement continus à l’aide de Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel :
- Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Installer Visual Studio 2017](https://www.visualstudio.com/) et installer hello **le développement Azure** et **développement web ASP.NET et** les charges de travail.
- [Installer hello SDK de l’infrastructure de Service](service-fabric-get-started.md)

## <a name="download-hello-voting-sample-application"></a>Télécharger l’application d’exemple hello vote
Si vous n’avez pas généré application d’exemple hello vote [première partie de cette série de didacticiels](service-fabric-tutorial-create-dotnet-app.md), vous pouvez le télécharger. Dans une fenêtre de commande, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="set-up-a-party-cluster"></a>Configurer un cluster tiers
Clusters tiers sont des clusters Service Fabric gratuites et limitée dans le temps hébergé sur Azure et exécuté par l’équipe de Service Fabric hello où tout le monde peut déployer des applications et en savoir plus sur la plateforme de hello. gratuitement.

tooget accès tooa tiers Cluster, parcourir toothis site : http://aka.ms/tryservicefabric et suivez hello instructions tooget tooa cluster d’accès. Vous avez besoin d’un Facebook ou GitHub compte tooget accès tooa tiers Cluster.

> [!NOTE]
> Clusters de tiers ne sont pas sécurisés, vos applications et toutes les données que vous placez dans les peuvent être tooothers visible. Ne déploie pas tout ce que vous ne souhaitez pas que d’autres toosee. Être tooread que sur les conditions d’utilisation pour tous les détails de hello.

## <a name="configure-hello-listening-port"></a>Configurer le port d’écoute hello
Lors de la création de hello VotingWeb le service frontal, Visual Studio sélectionne de manière aléatoire un port pour hello service toolisten sur.  Hello VotingWeb service joue le rôle hello frontal pour cette application et qu’il accepte le trafic externe, nous allons donc lier ce tooa service fixée et bien en connaître le port. Dans l’Explorateur de solutions, ouvrez *VotingWeb/PackageRoot/ServiceManifest.xml*.  Recherche hello **point de terminaison** ressource Bonjour **ressources** section et modifier hello **Port** too80 de valeur.

```xml
<Resources>
    <Endpoints>
      <!-- This endpoint is used by hello communication listener tooobtain hello port on which too
           listen. Please note that if your service is partitioned, this port is shared with 
           replicas of different partitions that are placed in your code. -->
      <Endpoint Protocol="http" Name="ServiceEndpoint" Type="Input" Port="80" />
    </Endpoints>
  </Resources>
```

Mettre à jour également valeur de la propriété URL de l’Application hello dans le projet de vote hello sorte un navigateur web s’ouvre toohello bon port lorsque vous déboguez à l’aide de « F5 ».  Dans l’Explorateur de solutions, sélectionnez hello **vote** mise à jour et projet hello **URL de l’Application** propriété.

![URL de l’application](./media/service-fabric-tutorial-deploy-app-to-party-cluster/application-url.png)

## <a name="deploy-hello-app-toohello-azure"></a>Déployer hello application toohello Azure
Maintenant que l’application hello est prête, vous pouvez la déployer toohello Cluster tiers directement à partir de Visual Studio.

1. Avec le bouton droit **vote** dans hello l’Explorateur de solutions et choisissez **publier**.

    ![Boîte de dialogue Publier](./media/service-fabric-tutorial-deploy-app-to-party-cluster/publish-app.png)

2. Type Bonjour point de terminaison de connexion de hello tiers Cluster Bonjour **connexion de point de terminaison** champ et cliquez sur **publier**.

    Une fois la publication de hello a terminé, vous devez être en mesure de toosend une application de toohello demande via un navigateur.

3. Ouvrez préféré navigateur et tapez dans l’adresse du cluster hello (hello connexion point de terminaison sans informations de port hello - par exemple, win1kw5649s.westus.cloudapp.azure.com).

    Vous devez maintenant voir hello même résultat que vous avez vu lors de l’exécution application hello localement.

    ![Réponse de l’API à partir du cluster](./media/service-fabric-tutorial-deploy-app-to-party-cluster/response-from-cluster.png)

## <a name="remove-hello-application-from-a-cluster-using-service-fabric-explorer"></a>Supprimer l’application hello à partir d’un cluster à l’aide du Service Fabric Explorer
Service Fabric Explorer est un tooexplore d’interface utilisateur graphique et gérer des applications dans un cluster Service Fabric.

application hello tooremove hello tiers Cluster :

1. Parcourir toohello Service Fabric Explorer, à l’aide du lien hello fournie par la page d’inscription de tiers Cluster hello. Par exemple, http://win1kw5649s.westus.cloudapp.azure.com:19080/Explorer/index.html.

2. Dans l’Explorateur de l’infrastructure de Service, accédez à toohello **fabric://Voting** nœud de treeview hello sur le côté gauche de hello.

3. Cliquez sur hello **Action** bouton Bonjour droite **Essentials** volet, choisissez **supprimer l’Application**. Confirmer la suppression hello instance de l’application, ce qui supprime l’instance de notre application s’exécutant dans un cluster de hello hello.

![Supprimer l’application dans Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/delete-application.png)

## <a name="remove-hello-application-type-from-a-cluster-using-service-fabric-explorer"></a>Supprimer le type d’application hello à partir d’un cluster à l’aide du Service Fabric Explorer
Les applications sont déployées en tant que types d’applications dans un cluster Service Fabric, ce qui permet de vous toohave plusieurs instances et les versions de l’application hello en cours d’exécution dans un cluster de hello. Après l’avoir supprimé hello qui exécute l’instance de notre application, nous pouvons également supprimer de type hello, nettoyage de hello toocomplete du déploiement de hello.

Pour plus d’informations sur le modèle d’application hello dans l’infrastructure de Service, consultez [une application dans l’infrastructure de Service de modèle](service-fabric-application-model.md).

1. Accédez toohello **VotingType** nœud hello treeview.

2. Cliquez sur hello **Action** bouton Bonjour droite **Essentials** volet, choisissez **la mise hors service Type**. Vérifiez le type d’application hello annulation du déploiement.

![Annuler la mise en service du type d’application dans Service Fabric Explorer](./media/service-fabric-tutorial-deploy-app-to-party-cluster/unprovision-type.png)

Ceci conclut le didacticiel de hello.

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Déployer un cluster à distance tooa d’application à l’aide de Visual Studio
> * Supprimer une application d’un cluster à l’aide de Service Fabric Explorer

Avance toohello étape suivante du didacticiel :
> [!div class="nextstepaction"]
> [Configurer l’intégration continue avec Visual Studio Team Services](service-fabric-tutorial-deploy-app-with-cicd-vsts.md)