---
title: "aaaDeploy une application Azure Service Fabric avec d’intégration continue (Team Services) | Documents Microsoft"
description: "Découvrez comment tooset d’intégration continue et de déploiement pour une application de Service Fabric à l’aide de Visual Studio Team Services.  Déployer un cluster de Service Fabric tooa application dans Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/09/2017
ms.author: ryanwi
ms.openlocfilehash: ba9a632b247b0f467e7b66fbe77b4ad54fb3d9ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-with-cicd-tooa-service-fabric-cluster"></a>Déployer une application avec le cluster de l’élément de configuration/CD tooa Service Fabric
Ce didacticiel est partie trois d’une série et décrit comment tooset d’intégration continue et de déploiement pour une application Azure Service Fabric à l’aide de Visual Studio Team Services.  Une application de Service Fabric existante est nécessaire, l’application hello créé dans [générer une application .NET](service-fabric-tutorial-create-dotnet-app.md) est utilisé comme un exemple.

Dans la troisième partie de la série de hello, vous apprenez comment :

> [!div class="checklist"]
> * Ajouter le projet de tooyour de contrôle de code source
> * Créer une définition de build dans Team Services
> * Créer une définition de mise en production dans Team Services
> * Déployer et mettre à niveau une application automatiquement

Cette série de didacticiels vous montre comment effectuer les opérations suivantes :
> [!div class="checklist"]
> * [Créer une application .NET Service Fabric](service-fabric-tutorial-create-dotnet-app.md)
> * [Déployer le cluster de l’application hello tooa à distance](service-fabric-tutorial-deploy-app-to-party-cluster.md)
> * Configurer l’intégration et le déploiement continus à l’aide de Visual Studio Team Services

## <a name="prerequisites"></a>Composants requis
Avant de commencer ce didacticiel :
- Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).
- [Installer Visual Studio 2017](https://www.visualstudio.com/) et installer hello **le développement Azure** et **développement web ASP.NET et** les charges de travail.
- [Installer hello SDK de l’infrastructure de Service](service-fabric-get-started.md)
- Créez une application Service Fabric, par exemple en suivant [ce didacticiel](service-fabric-tutorial-create-dotnet-app.md). 
- Créez un cluster Service Fabric Windows sur Azure, par exemple en suivant [ce didacticiel](service-fabric-tutorial-create-cluster-azure-ps.md).
- Créez un compte [Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services).

## <a name="download-hello-voting-sample-application"></a>Télécharger l’application d’exemple hello vote
Si vous n’avez pas généré application d’exemple hello vote [première partie de cette série de didacticiels](service-fabric-tutorial-create-dotnet-app.md), vous pouvez le télécharger. Dans une fenêtre de commande, exécutez hello suivant commande tooclone hello exemple application référentiel tooyour ordinateur local.

```
git clone https://github.com/Azure-Samples/service-fabric-dotnet-quickstart
```

## <a name="prepare-a-publish-profile"></a>Préparer un profil de publication
Maintenant que vous avez [créé une application](service-fabric-tutorial-create-dotnet-app.md) et [déployé hello application tooAzure](service-fabric-tutorial-deploy-app-to-party-cluster.md), vous êtes prêt tooset d’intégration continue.  Tout d’abord, préparez un profil de publication au sein de votre application pour une utilisation par les processus de déploiement hello qui s’exécute dans Team Services.  profil de publication Hello doit être cluster hello tootarget configurés que vous avez créé précédemment.  Démarrez Visual Studio et ouvrez un projet d’application Service Fabric existant.  Dans **l’Explorateur de solutions**, application hello d’avec le bouton droit et sélectionnez **publier...** .

Choisissez un profil cible au sein de votre toouse de projet d’application pour votre flux de travail d’intégration continue, par exemple le Cloud.  Spécifiez le point de terminaison de connexion hello cluster.  Vérifiez hello **mise à niveau hello Application** case à cocher afin que les mises à niveau de votre application pour chaque déploiement dans les Services d’équipe.  Cliquez sur hello **enregistrer** toohello de lien hypertexte toosave hello paramètres du profil de publication, puis cliquez sur **Annuler** boîte de dialogue tooclose hello.  

![Profil d’envoi (push)][publish-app-profile]

## <a name="share-your-visual-studio-solution-tooa-new-team-services-git-repo"></a>Partager votre référentiel Git de Services d’équipe Visual Studio solution tooa nouveau
Partager des fichiers source de votre application tooa projet d’équipe dans Team Services, vous pouvez générer les builds.  

Créer un nouveau dépôt Git local pour votre projet en sélectionnant **ajouter tooSource contrôle** -> **Git** sur la barre d’état hello dans hello coin inférieur droit de Visual Studio. 

Bonjour **Push** afficher dans **Team Explorer**, sélectionnez hello **publier le référentiel Git** sous **Push tooVisual Studio Team Services**.

![Envoi (push) du dépôt Git][push-git-repo]

Vérifiez votre adresse de messagerie et sélectionnez votre compte dans hello **Team Services domaine** liste déroulante. Entrez le nom de votre dépôt et sélectionnez **Publier le dépôt**.

![Envoi (push) du dépôt Git][publish-code]

Référentiel de hello de publication de crée un nouveau projet d’équipe dans votre compte avec hello comme référentiel local de hello du même nom. référentiel de hello toocreate dans un projet d’équipe existant, cliquez sur **avancé** suivant trop**référentiel** nom et sélectionnez un projet d’équipe. Vous pouvez afficher votre code sur le web de hello en sélectionnant **affichez-le sur le web de hello**.

## <a name="configure-continuous-delivery-with-vsts"></a>Configurer la livraison continue avec VSTS
Une définition de build Team Services décrit un flux de travail qui se compose d’un ensemble d’étapes de génération exécutées séquentiellement. Créer une définition de build qui produit un package d’application Service Fabric et autres artefacts, le cluster Service Fabric de tooa toodeploy. Vous trouverez plus d’informations sur les définitions de build Team Services [ici](https://www.visualstudio.com/docs/build/define/create). 

Une définition de mise en production Team Services décrit un flux de travail qui déploie un cluster de tooa package application. Utilisés conjointement, hello définition de build et définition de la version exécutez hello l’ensemble du workflow en commençant par tooending de fichiers de code source avec une application en cours d’exécution dans votre cluster. Plus d’informations sur les [définitions de version](https://www.visualstudio.com/docs/release/author-release-definition/more-release-definition)Team Services.

### <a name="create-a-build-definition"></a>Créer une définition de build
Ouvrez un navigateur web et accédez de nouveau projet d’équipe tooyour à : https://myaccount.visualstudio.com/Voting/Voting%20Team/_git/Voting. 

Sélectionnez hello **générer & version** sous l’onglet puis **génère**, puis **+ nouvelle définition**.  Dans **sélectionner un modèle**, sélectionnez hello **Application Azure Service Fabric** modèle et cliquez sur **appliquer**. 

![Choisir le modèle de build][select-build-template] 

Hello vote application contient un projet .NET Core, ajoutez une tâche qui restaure les dépendances hello. Bonjour **tâches** afficher, sélectionnez **+ ajouter une tâche** en bas à gauche hello. Effectuez une recherche sur la tâche de ligne de commande de « Ligne de commande » toofind hello, puis cliquez sur **ajouter**. 

![Ajouter une tâche][add-task] 

Dans la nouvelle tâche de hello, entrez « Exécuter dotnet.exe » dans **nom d’affichage**, « dotnet.exe » dans **outil**et « restore » dans **Arguments**. 

![Nouvelle tâche][new-task] 

Bonjour **déclencheurs** afficher, cliquez sur hello **activer ce déclencheur** commutateur sous **intégration continue**. 

Sélectionnez **enregistrer et de file d’attente** et entrez « Hébergé VS2017 » hello **file d’attente de l’Agent**. Sélectionnez **file d’attente** toomanually de démarrer une génération.  Les builds sont également déclenchées sur notification Push ou archivage.

toocheck votre progression de la génération, commutateur toohello **génère** onglet.  Une fois que vous avez vérifié que la génération de hello s’exécute avec succès, définir une définition de mise en production qui déploie votre cluster tooa d’application. 

### <a name="create-a-release-definition"></a>Création d’une définition de version  

Sélectionnez hello **générer & version** sous l’onglet puis **versions**, puis **+ nouvelle définition**.  Dans **définition de la version créer**, sélectionnez hello **Azure Service Fabric déploiement** modèle à partir de la liste de hello et cliquez sur **suivant**.  Sélectionnez hello **générer** source, vérifiez hello **déploiement continu** , puis cliquez sur **créer**. 

Bonjour **environnements** afficher, cliquez sur **ajouter** toohello à droite de **connexion Cluster**.  Spécifiez un nom de connexion de « mysftestcluster », un point de terminaison de cluster de « tcp://mysftestcluster.westus.cloudapp.azure.com:19000 » et hello Azure Active Directory ou informations d’identification de certificat pour le cluster de hello. Informations d’identification d’Azure Active Directory, définir les informations de hello souhaité toouse tooconnect toohello cluster Bonjour **nom d’utilisateur** et **mot de passe** champs. Pour l’authentification basée sur certificat, définissez hello Base64 encodage du fichier de certificat client hello hello **certificat Client** champ.  Consultez la fenêtre contextuelle de hello aide sur ce champ pour plus d’informations sur la façon de tooget cette valeur.  Si votre certificat est protégé par mot de passe, définir le mot de passe hello Bonjour **mot de passe** champ.  Cliquez sur **enregistrer** définition de la version toosave hello.

![Ajouter une connexion au cluster][add-cluster-connection] 

Cliquez sur **Exécuter sur l’agent**, puis sélectionnez **Hébergée VS2017** pour **File d’attente de déploiement**. Cliquez sur **enregistrer** définition de la version toosave hello.

![Exécuter sur l’agent][run-on-agent]

Sélectionnez **+ version** -> **créer version** -> **créer** toomanually créer une mise en production.  Vérifiez que hello déploiement a réussi et application hello est en cours d’exécution dans un cluster de hello.  Ouvrez un navigateur web et accédez trop[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Notez la version de l’application hello, dans cet exemple, « 1.0.0.20170616.3 ». 

## <a name="commit-and-push-changes-trigger-a-release"></a>Valider et envoyer les modifications, déclencher une mise en production
tooverify qui hello pipeline d’intégration continue fonctionne en vérifiant certaines modifications du code tooTeam Services.    

Lorsque vous écrivez votre code, vos modifications sont suivies automatiquement par Visual Studio. Valider les modifications tooyour référentiel Git en sélectionnant hello en attente (icône de modifications![Pending][pending]) à partir de la barre d’état hello dans bas hello à droite.

Sur hello **modifications** afficher dans Team Explorer, ajoutez un message qui décrit votre mise à jour et valider vos modifications.

![Valider tout][changes]

Icône de barre de statut de modifications non publiées hello Select (![Unpublished modifications][unpublished-changes]) ou de vue de synchronisation dans Team Explorer de bienvenue. Sélectionnez **Push** tooupdate votre code dans Team Services/TFS.

![Envoi (push) des modifications][push]

En exécutant un push hello modifications tooTeam Services automatiquement déclencheurs une build.  Lors de la définition de build hello terminée avec succès, une version est créée automatiquement et commence la mise à niveau d’application hello sur le cluster de hello.

toocheck votre progression de la génération, commutateur toohello **génère** onglet **Team Explorer** dans Visual Studio.  Une fois que vous avez vérifié que la génération de hello s’exécute avec succès, définir une définition de mise en production qui déploie votre cluster tooa d’application.

Vérifiez que hello déploiement a réussi et application hello est en cours d’exécution dans un cluster de hello.  Ouvrez un navigateur web et accédez trop[http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/](http://mysftestcluster.westus.cloudapp.azure.com:19080/Explorer/).  Notez la version de l’application hello, dans cet exemple, « 1.0.0.20170815.3 ».

![Service Fabric Explorer][sfx1]

## <a name="update-hello-application"></a>Mettre à jour d’application hello
Apporter des modifications de code dans l’application hello.  Enregistrer et valider les modifications de hello, suivant les étapes précédentes hello.

Une fois hello mise à niveau d’application hello commence, vous pouvez surveiller la progression de mise à niveau de hello dans Service Fabric Explorer :

![Service Fabric Explorer][sfx2]

mise à niveau des applications Hello peut prendre plusieurs minutes. Lors de la mise à niveau hello est terminée, application hello exécute version suivante de hello.  Dans cet exemple, 1.0.0.20170815.4.

![Service Fabric Explorer][sfx3]

## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]
> * Ajouter le projet de tooyour de contrôle de code source
> * Créer une définition de build
> * Création d’une définition de version
> * Déployer et mettre à niveau une application automatiquement

Maintenant que vous avez déployé une application et configuré l’intégration continue, essayez suivante de hello :
- [Mettre à niveau une application](service-fabric-application-upgrade.md)
- [Tester une application](service-fabric-testability-overview.md) 
- [Surveiller et diagnostiquer](service-fabric-diagnostics-overview.md)


<!-- Image References -->
[publish-app-profile]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishAppProfile.png
[push-git-repo]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishGitRepo.png
[publish-code]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/PublishCode.png
[select-build-template]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SelectBuildTemplate.png
[add-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddTask.png
[new-task]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewTask.png
[set-continuous-integration]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SetContinuousIntegration.png
[add-cluster-connection]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/AddClusterConnection.png
[sfx1]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX1.png
[sfx2]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX2.png
[sfx3]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/SFX3.png
[pending]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Pending.png
[changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Changes.png
[unpublished-changes]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/UnpublishedChanges.png
[push]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/Push.png
[continuous-delivery-with-VSTS]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/VSTS-Dialog.png
[new-service-endpoint]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpoint.png
[new-service-endpoint-dialog]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/NewServiceEndpointDialog.png
[run-on-agent]: ./media/service-fabric-tutorial-deploy-app-with-cicd-vsts/RunOnAgent.png