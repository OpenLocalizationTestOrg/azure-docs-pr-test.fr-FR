---
title: "livraison d’aaaContinuous avec Git et Visual Studio Team Services dans Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure votre Visual Studio Team Services projets d’équipe toouse Git tooautomatically générer et déployer des fonctionnalités de l’application Web toohello dans Azure App Service ou cloud services."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 4b3297ef-0de6-4d5f-925c-fcdacc3085ac
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: 936c42194f45be55597a77f9a3a6deb4480ed94b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services-and-git"></a>TooAzure de livraison continue avec Visual Studio Team Services et Git
Vous pouvez utiliser toohost de projets d’équipe Visual Studio Team Services un référentiel Git de votre code source et automatiquement générer et déployer des applications web tooAzure ou services de cloud computing, chaque fois que vous effectuez un push un référentiel de toohello de validation.

Vous aurez besoin de Visual Studio 2013 et hello Azure SDK est installé. Si vous ne disposez pas de Visual Studio 2013, téléchargez-le en choisissant hello **commencez gratuitement** lien [www.visualstudio.com](http://www.visualstudio.com). Installation Bonjour Azure SDK depuis [ici](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Vous avez besoin une toocomplete de compte Visual Studio Team Services pour ce didacticiel : vous pouvez [ouvrir un compte Visual Studio Team Services gratuit](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset d’un tooautomatically de service cloud générer et déployer tooAzure à l’aide de Visual Studio Team Services, procédez comme suit.

## <a name="1-create-a-git-repository"></a>1 : Création d'un référentiel Git
1. Si vous ne disposez pas de compte Visual Studio Team Services, vous pouvez en obtenir un [ici](http://go.microsoft.com/fwlink/?LinkId=397665). Lorsque vous créez un projet d'équipe, choisissez Git comme système de contrôle de code source. Suivez le projet d’équipe tooyour hello instructions tooconnect Visual Studio.
2. Dans **Team Explorer**, choisissez hello **cloner ce référentiel** lien.
   
    ![][3]
3. Spécifier l’emplacement de hello de copie locale de hello, puis choisissez hello **Clone** bouton.

## <a name="2-create-a-project-and-commit-it-toohello-repository"></a>2 : créer un projet et validez-la toohello référentiel
1. Dans **Team Explorer**, Bonjour **Solutions** , choisissez hello **nouveau** lien toocreate un nouveau projet dans le référentiel local de hello.
   
    ![][4]
2. Vous pouvez déployer une application web ou un service cloud (Application Azure) par hello suivant les étapes dans cette procédure pas à pas. Créez un projet de service cloud Azure ou un projet MVC ASP.NET. Assurez-vous que les cibles du projet hello hello .NET Framework 4 ou version ultérieure. Si vous créez un projet de service cloud, ajoutez un rôle web ASP.NET MVC et un rôle de travail.
   Si vous souhaitez toocreate une application web, choisissez hello **Application Web ASP.NET** modèle de projet, puis choisissez **MVC**. Pour plus d’informations, consultez la rubrique [Création d’une application web ASP.NET dans Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md) .
3. Ouvrez le menu contextuel de hello pour la solution de hello, puis choisissez **valider**.
   
    ![][7]
4. S’il s’agit hello première fois que vous utilisez Git dans Visual Studio Team Services, vous devez tooprovide tooidentify de certaines informations vous-même dans Git. Bonjour **modifications en attente** zone de **Team Explorer**, entrez votre nom d’utilisateur et votre adresse de messagerie. Entrez un commentaire pour la validation de hello, puis choisissez hello **validation** bouton.
   
    ![][8]
5. Notez hello options tooinclude ou exclure lorsque vous archivez des modifications spécifiques. Si hello modifications que vous souhaitez sont exclus, choisissez **tout inclure**.
6. Vous avez maintenant hello validée change dans votre copie locale du référentiel de hello. Ensuite, de synchroniser ces modifications avec le serveur de hello en choisissant hello **synchronisation** lien.

## <a name="3-connect-hello-project-tooazure"></a>3 : connecter hello projet tooAzure
1. Maintenant que vous avez un référentiel Git dans Visual Studio Team Services avec du code source qu’il contient, vous êtes prêt tooconnect votre tooAzure de référentiel git.  Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), sélectionnez votre cloud service ou une application web ou créez-en un en choisissant Bonjour + l’icône située en bas à gauche hello et en choisissant **Service Cloud** ou **Web App**, puis **création rapide**.
   
    ![][9]
2. Pour les services de cloud, choisissez hello **configurer la publication avec Visual Studio Team Services** lien. Pour les applications web, choisissez hello **configurer le déploiement à partir du contrôle de code source** lien.
   
    ![][10]
3. Dans l’Assistant de hello, tapez le nom hello de votre compte Visual Studio Team Services dans la zone de texte hello et choisissez hello **autoriser maintenant** lien. Vous pouvez être invité à toosign dans.
   
    ![][11]
4. Bonjour **demande de connexion** boîte de dialogue contextuelle, choisissez **accepter** tooauthorize tooconfigure Azure votre projet d’équipe dans Visual Studio Team Services.
   
    ![][12]
5. Si la procédure d’autorisation réussit, une zone déroulante affiche la liste de vos projets d’équipe Visual Studio Team Services.  Sélectionnez Nom hello du projet d’équipe que vous avez créé dans les étapes précédentes hello et choisissez le bouton hello de l’Assistant.
   
    ![][13]
   
    Hello prochaine fois que vous effectuez un push un référentiel de tooyour de validation, Visual Studio Team Services générera et déploiera votre tooAzure du projet.

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4 : Déclenchement d'une régénération et redéploiement de votre projet
1. Dans Visual Studio, ouvrez un fichier et modifiez-le. Par exemple, modifiez le fichier de hello `_Layout.cshtml` sous hello affichages\\dossier partagé dans un rôle de web MVC.
   
    ![][17]
2. Modifier le texte de pied de page hello pour le site de hello et enregistrez le fichier de hello.
   
    ![][18]
3. Dans **l’Explorateur de solutions**, ouvrez le menu contextuel de hello hello nœud de la solution, le nœud de projet, hello fichier ou vous avez modifié, puis choisissez **valider**.
4. Tapez un commentaire et sélectionnez **Valider**.
   
    ![][20]
5. Choisissez hello **synchronisation** lien.
   
    ![][38]
6. Choisissez hello **Push** lien toopush votre référentiel toohello de validation dans Visual Studio Team Services. (Vous pouvez également utiliser hello **synchronisation** bouton toocopy votre référentiel toohello de validations. Hello différence est que **synchronisation** également extrait hello modifications les plus récentes à partir du référentiel de hello.)
   
    ![][39]
7. Choisissez hello **domestique** bouton tooreturn toohello **Team Explorer** page d’accueil.
   
    ![][21]
8. Choisissez **génère** tooview hello les builds en cours.
   
    ![][22]
   
    **Team Explorer** indique qu’une build est disponible pour archivage.
   
    ![][23]
9. tooview un journal détaillé que hello génération progresse, double-cliquez sur nom hello build hello en cours d’exécution.
10. Lors de la génération de hello est en cours d’exécution, examiner une définition de build hello qui a été créée lorsque vous avez utilisé hello Assistant toolink tooAzure.  Ouvrez le menu contextuel de hello pour la définition de build hello et choisissez **modifier la définition de Build**.
    
    ![][25]
11. Bonjour **déclencheur** onglet, vous verrez que définition de build hello a la valeur toobuild sur chaque archivage, par défaut. (Pour un service cloud, Visual Studio Team Services génère et déploie toohello de branche principale hello environnement intermédiaire automatiquement. Vous avez toujours toodo un site en direct toohello toodeploy étape manuelle. Pour une application web qui n’a pas environnement intermédiaire, il déploie branche principale de hello directement toohello live site.
    
    ![][26]
12. Bonjour **processus** onglet, vous pouvez voir d’un environnement de déploiement hello est défini nom toohello de votre application web ou de service de cloud.
    
     ![][27]
13. Spécifier des valeurs pour les propriétés de hello si vous souhaitez que les valeurs différentes de celles des valeurs par défaut hello. Hello propriétés pour la publication de Azure sont Bonjour **déploiement** section et vous devrez peut-être également tooset MSBuild paramètres. Par exemple, dans un projet de service cloud, toospecify une configuration de service autre que « Cloud », définissez hello MSbuild paramètres trop`/p:TargetProfile=[YourProfile]` où *[YourProfile]* correspond à un fichier de configuration de service avec un nom tel que ServiceConfiguration. *YourProfile*.cscfg.
    
     Hello tableau suivant répertorie les propriétés disponibles hello dans hello **déploiement** section :
    
    | Propriété | Valeur par défaut |
    | --- | --- |
    | Autoriser les certificats non approuvés |Si cette propriété a la valeur false, des certificats SSL doivent être signés par une autorité racine. |
    | Autoriser la mise à niveau |Permet à un déploiement existant au lieu de créer un nouveau hello déploiement tooupdate. Conserve l’adresse IP de hello. |
    | Ne pas supprimer |Si cette propriété a la valeur true, ne remplacez pas un déploiement sans rapport (la mise à niveau est autorisée). |
    | Chemin d’accès tooDeployment paramètres |fichier de .pubxml tooyour Hello chemin d’accès pour une application web, dossier racine de toohello relatif de dépôt de hello. Ignorée pour les services cloud. |
    | Environnement de déploiement SharePoint |Bonjour même en tant que nom de service hello. |
    | Environnement de déploiement Azure |Hello cloud ou application nom du service web. |
14. À ce stade, la création de la build doit être terminée.
    
     ![][28]
15. Si vous double-cliquez sur le nom de la build hello, Visual Studio affiche un **résumé de la Build**, y compris les résultats des tests à partir d’associées des projets de test unitaire.
    
     ![][29]
16. Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), vous pouvez afficher le déploiement de hello associé sur hello **déploiements** onglet lorsque hello environnement intermédiaire est sélectionnée.
    
     ![][30]
17. Parcourir les URL du site tooyour. Pour une application web, choisissez simplement hello **Parcourir** bouton dans le portail de hello. Pour un service cloud, choisissez hello URL Bonjour **aperçu rapide** section Hello **tableau de bord** page qui affiche l’environnement intermédiaire de hello.
    
    Les déploiements à partir de l’intégration continue pour les services cloud sont environnement intermédiaire de toohello publié par défaut. Vous pouvez le modifier en définissant les hello **autre environnement de Service Cloud** propriété trop**Production**. Voici où les URL du site hello est sur la page du tableau de bord du service de cloud hello.
    
    ![][31]
    
    Un nouvel onglet de navigateur s’ouvre tooreveal votre site en cours d’exécution.
    
    ![][32]
18. Si vous apportez des autres modifications tooyour projet vous déclencheur génère plus et vous vont s’accumuler plusieurs déploiements. Hello dernière une est marquée comme Active.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5 : Redéploiement d'une build antérieure
Cette étape est facultative. Hello portail Azure classic, choisissez un précédent déploiement et choisissez **redéployer** toorewind votre tooan site précédemment archivage. Notez que cela déclenche une nouvelle génération dans TFS et crée une entrée dans l’historique de votre déploiement.

![][34]

## <a name="6-change-hello-production-deployment"></a>6 : modifier le déploiement de Production hello
Lorsque vous êtes prêt, vous pouvez promouvoir hello intermédiaire toohello environnement de Production en choisissant **échanger** Bonjour portail Azure classic. environnement d’intermédiaire Hello nouvellement déployé est promue tooProduction et environnement de Production précédent hello, le cas échéant, devient un environnement intermédiaire. Hello déploiement actif peut être différente pour hello Production et les environnements de préproduction, mais l’historique de déploiement hello des builds récentes est hello même indépendamment de l’environnement.

![][35]

## <a name="7-deploy-from-a-working-branch"></a>7 : Déploiement à partir d’une branche en cours d’utilisation
Lorsque vous utilisez Git, vous généralement apportez des modifications dans une branche de travail et s’intégrer dans la branche principale de hello lorsque votre développement atteint un état terminé. Pendant la phase de développement hello d’un projet, vous souhaitez toobuild et déployer tooAzure de branche de travail hello.

1. Dans **Team Explorer**, choisissez hello **accueil** bouton, puis choisissez hello **Branches** bouton.
   
    ![][40]
2. Choisissez hello **nouvelle branche** lien.
   
    ![][41]
3. Entrez le nom hello de branche hello, tels que « working », puis choisissez **créer une branche**. pour créer une branche locale.
   
    ![][42]
4. Publier la branche de hello. Choisissez le nom de la branche hello dans **Unpublished branches**, puis choisissez **publier**.
   
    ![][44]
5. Par défaut, modifie uniquement le déclencheur de branche principale toohello une build en continu. tooset de build en continu pour une branche de travail, choisissez hello **génère** page **Team Explorer**, puis choisissez **modifier la définition de Build**.
6. Ouvrez hello **paramètres Source** onglet. Sous **analysé les branches pour l’intégration continue et build**, choisissez **cliquez ici tooadd une nouvelle ligne**.
   
    ![][47]
7. Spécifiez la branche hello créé, tels que refs/têtes/travail.
   
    ![][48]
8. Apportez une modification dans le code hello, fichier hello modifié sur le menu contextuel hello ouvrir, puis choisissez **valider**.
   
    ![][43]
9. Choisissez hello **validations non synchronisées** la liaison et choisissez hello **synchronisation** bouton ou hello **Push** hello toocopy de lien change copie toohello de branche de travail hello dans Visual Studio Team Services.
   
   ![][45]
10. Accédez toohello **génère** afficher et rechercher build hello déclenchant simplement obtenu pour la branche de travail hello.

## <a name="next-steps"></a>Étapes suivantes
consultez d’autres conseils sur l’utilisation de Git avec Visual Studio Team Services, toolearn [développer et partager votre code dans Git, à l’aide de Visual Studio](https://www.visualstudio.com/en-us/docs/git/share-your-code-in-git-vs-2017) et pour plus d’informations sur l’utilisation d’un référentiel Git qui n’est pas géré par toopublish de Visual Studio Team Services tooAzure, consultez [tooAzure de déploiement continu du Service d’applications](../app-service-web/app-service-continuous-deployment.md). Pour en savoir plus sur Visual Studio Team Services, consultez [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateTeamProjectInGit.PNG
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png
[3]: ./media/cloud-services-continuous-delivery-use-vso-git/CloneThisRepository.PNG
[4]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateNewSolutionInClonedRepo.PNG
[7]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitMenuItem.PNG
[8]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[9]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateCloudService.PNG
[10]: ./media/cloud-services-continuous-delivery-use-vso-git/SetUpPublishingWithVSO.PNG
[11]: ./media/cloud-services-continuous-delivery-use-vso-git/AuthorizeConnection.PNG
[12]: ./media/cloud-services-continuous-delivery-use-vso-git/ConnectionRequest.PNG
[13]: ./media/cloud-services-continuous-delivery-use-vso-git/ChooseARepo3.PNG
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso-git/MakeACodeChange.PNG
[20]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[21]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerHome.png
[22]: ./media/cloud-services-continuous-delivery-use-vso-git/TeamExplorerBuilds.PNG
[23]: ./media/cloud-services-continuous-delivery-use-vso-git/BuildInQueue.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso-git/ProcessTab.PNG
[28]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso-git/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateANewAccount.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso-git/PushCurrentBranch.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso-git/BranchesInTeamExplorer.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso-git/NewBranch.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso-git/CreateBranch.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso-git/CommitAChange2.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso-git/PublishBranch.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso-git/SyncChanges2.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso-git/SourceSettingsPage.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso-git/IncludeWorkingBranch.PNG
