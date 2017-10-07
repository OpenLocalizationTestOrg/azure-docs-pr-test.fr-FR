---
title: "livraison d’aaaContinuous avec Visual Studio Team Services dans Azure | Documents Microsoft"
description: "Découvrez comment tooconfigure votre Visual Studio Team Services projets d’équipe tooautomatically générer et déployer des fonctionnalités de l’application Web toohello dans Azure App Service ou cloud services."
services: cloud-services
documentationcenter: .net
author: mlearned
manager: douge
editor: 
ms.assetid: 797f67ad-e4d4-4063-ae91-41cbdf154191
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/06/2016
ms.author: mlearned
ms.openlocfilehash: eae75729e1c1a55f9bc3375604a8192f329d0042
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="continuous-delivery-tooazure-using-visual-studio-team-services"></a>TooAzure de livraison continue à l’aide de Visual Studio Team Services
Vous pouvez configurer votre build tooautomatically Visual Studio Team Services les projets d’équipe et déployer des applications web tooAzure ou services de cloud computing.  (Pour plus d’informations sur comment tooset une build en continu et la déployer à l’aide du système une *local* Team Foundation Server, consultez [livraison continue pour les Services de Cloud dans Azure](cloud-services-dotnet-continuous-delivery.md).)

Ce didacticiel suppose que vous avez Visual Studio 2013 et hello Azure SDK est installé. Si vous ne disposez pas de Visual Studio 2013, téléchargez-le en choisissant hello **commencez gratuitement** lien [www.visualstudio.com](http://www.visualstudio.com). Installation Bonjour Azure SDK depuis [ici](http://go.microsoft.com/fwlink/?LinkId=239540).

> [!NOTE]
> Vous avez besoin une toocomplete de compte Visual Studio Team Services pour ce didacticiel : vous pouvez [ouvrir un compte Visual Studio Team Services gratuit](http://go.microsoft.com/fwlink/p/?LinkId=512979).
> 
> 

tooset d’un tooautomatically de service cloud générer et déployer tooAzure à l’aide de Visual Studio Team Services, procédez comme suit.

## <a name="1-create-a-team-project"></a>1 : Création d'un projet d'équipe
Suivez les instructions de hello [ici](http://go.microsoft.com/fwlink/?LinkId=512980) toocreate votre équipe de projet et le lier tooVisual Studio. Cette procédure pas à pas part du principe que vous utilisez TFVC (Team Foundation Version Control) en tant que solution de contrôle de code source. Si vous souhaitez toouse Git pour le contrôle de version, consultez [version de Git hello de cette procédure pas à pas](http://go.microsoft.com/fwlink/p/?LinkId=397358).

## <a name="2-check-in-a-project-toosource-control"></a>2 : vérifier dans un contrôle toosource de projet
1. Dans Visual Studio, ouvrez solution hello vous souhaitez toodeploy ou créez un.
   Vous pouvez déployer une application web ou un service cloud (Application Azure) par hello suivant les étapes dans cette procédure pas à pas.
   Si vous souhaitez toocreate une nouvelle solution, créez un nouveau projet de Service Cloud Azure, ou un nouveau projet ASP.NET MVC. Assurez-vous que hello projet cible .NET Framework 4 ou 4.5 et si vous créez un projet de service cloud, ajoutez un rôle web d’ASP.NET MVC et un rôle de travail et choisissez l’application Internet pour un rôle web de hello. Lorsque vous y êtes invité, choisissez **Application Internet**.
   Si vous souhaitez toocreate une application web, choisissez le modèle de projet d’Application Web ASP.NET hello, puis MVC. Consultez la rubrique [Création d’une application Web ASP.NET dans Azure App Service](../app-service-web/app-service-web-get-started-dotnet.md).
   
   > [!NOTE]
   > Actuellement, Visual Studio Team Services ne prend en charge que les déploiements CI des applications web Visual Studio. Les projets de site web n’entrent pas dans ce cadre.
   > 
   > 
2. Ouvrez le menu contextuel de hello pour la solution de hello, puis choisissez **tooSource d’ajouter la Solution contrôle**.
   
    ![][5]
3. Accepter ou modifier les valeurs par défaut hello et choisissez hello **OK** bouton. Une fois que la fin du processus de hello, les icônes de contrôle de code source s’affichent dans **l’Explorateur de solutions**.
   
    ![][6]
4. Ouvrez le menu contextuel de hello pour la solution de hello, puis choisissez **archiver**.
   
    ![][7]
5. Bonjour **modifications en attente** zone de **Team Explorer**, tapez un commentaire d’archivage hello et choisissez hello **archiver** bouton.
   
    ![][8]
   
    Notez hello options tooinclude ou exclure lorsque vous archivez des modifications spécifiques. Si vous le souhaitez modifications sont exclues, choisissez hello **tout inclure** lien.
   
    ![][9]

## <a name="3-connect-hello-project-tooazure"></a>3 : connecter hello projet tooAzure
1. Maintenant que vous avez un projet d’équipe Visual Studio Team Services avec du code source qu’il contient, vous êtes prêt tooconnect votre projet d’équipe tooAzure.  Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), sélectionnez votre cloud service ou une application web ou créez-en un en choisissant hello  **+**  icône située en bas à gauche hello et en choisissant **leServiceCloud** ou **application Web** , puis **création rapide**. Choisissez hello **configurer la publication avec Visual Studio Team Services** lien.
   
    ![][10]
2. Dans l’Assistant de hello, tapez le nom hello de votre compte Visual Studio Team Services dans la zone de texte hello et cliquez sur hello **autoriser maintenant** lien. Vous pouvez être invité à toosign dans.
   
    ![][11]
3. Bonjour **demande de connexion** boîte de dialogue contextuelle, choisissez hello **accepter** bouton tooauthorize tooconfigure Azure votre projet d’équipe dans Visual Studio Team Services.
   
    ![][12]
4. Si le processus d'autorisation aboutit, une zone déroulante affiche une liste de vos projets Visual Studio Team Services. Choisissez le nom de hello du projet d’équipe que vous avez créé dans les étapes précédentes hello, puis coche hello de l’Assistant.
   
    ![][13]
5. Une fois que votre projet est lié, vous verrez des instructions relatives à la vérification dans le projet d’équipe de modifications tooyour Visual Studio Team Services.  Sur votre prochain archivage, Visual Studio Team Services générera et déploiera votre tooAzure du projet.  Essayez cette maintenant en cliquant sur hello **archiver à partir de Visual Studio** lier, puis hello **lancer Visual Studio** lien (ou équivalent de hello **Visual Studio** bouton bas hello écran portail Hello).
   
    ![][14]

## <a name="4-trigger-a-rebuild-and-redeploy-your-project"></a>4 : Déclenchement d'une régénération et redéploiement de votre projet
1. Dans Visual Studio **Team Explorer**, choisissez hello **Explorateur du contrôle de code Source** lien.
   
    ![][15]
2. Parcourir le fichier de solution tooyour et ouvrez-le.
   
    ![][16]
3. Dans l' **Explorateur de solutions**, ouvrez un fichier et modifiez-le. Par exemple, modifiez le fichier de hello `_Layout.cshtml` sous hello affichages\\dossier partagé dans un rôle de web MVC.
   
    ![][17]
4. Modifier le logo hello pour le site de hello, puis choisissez **Ctrl + S** fichier hello de toosave.
   
    ![][18]
5. Dans **Team Explorer**, choisissez hello **modifications en attente** lien.
   
    ![][19]
6. Entrez un commentaire, puis choisissez hello **archiver** bouton.
   
    ![][20]
7. Choisissez hello **domestique** bouton tooreturn toohello **Team Explorer** page d’accueil.
   
    ![][21]
8. Choisissez hello **génère** hello tooview de lien les builds en cours.
   
    ![][22]
   
    **Team Explorer** indique qu’une build est disponible pour archivage.
   
    ![][23]
9. Double-cliquez sur nom hello de build hello dans progression tooview un journal détaillé fur hello et build.
   
    ![][24]
10. Lors de la génération de hello est en cours d’exécution, examiner une définition de build hello qui a été créée lorsque vous avez lié tooAzure TFS à l’aide d’Assistant de hello.  Ouvrez le menu contextuel de hello pour la définition de build hello et choisissez **modifier la définition de Build**.
    
     ![][25]
    
     Bonjour **déclencheur** onglet, vous verrez que définition de build hello a la valeur toobuild sur chaque archivage par défaut.
    
     ![][26]
    
     Bonjour **processus** onglet, vous pouvez voir d’un environnement de déploiement hello est défini nom toohello de votre application web ou de service de cloud. Si vous travaillez avec des applications web, propriétés hello que vous voyez sera différentes de celles présentées ici.
    
     ![][27]
11. Spécifier des valeurs pour les propriétés de hello si vous souhaitez que les valeurs différentes de celles des valeurs par défaut hello. Hello propriétés pour la publication de Azure sont Bonjour **déploiement** section.
    
     Hello tableau suivant répertorie les propriétés disponibles hello dans hello **déploiement** section :
    
    | Propriété | Valeur par défaut |
    | --- | --- |
    | Autoriser les certificats non approuvés |Si cette propriété a la valeur false, des certificats SSL doivent être signés par une autorité racine. |
    | Autoriser la mise à niveau |Permet à un déploiement existant au lieu de créer un nouveau hello déploiement tooupdate. Conserve l’adresse IP de hello. |
    | Ne pas supprimer |Si cette propriété a la valeur true, ne remplacez pas un déploiement sans rapport (la mise à niveau est autorisée). |
    | Chemin d’accès tooDeployment paramètres |fichier de .pubxml tooyour Hello chemin d’accès pour une application web, dossier racine de toohello relatif de dépôt de hello. Ignorée pour les services cloud. |
    | Environnement de déploiement SharePoint |Bonjour même en tant que nom de service hello. |
    | Environnement de déploiement Azure |Hello cloud ou application nom du service web. |
12. Si vous utilisez plusieurs configurations de service (fichiers .cscfg), vous pouvez spécifier la configuration de service désiré hello Bonjour **arguments de Build, Avancé, MSBuild** paramètre. Par exemple, toouse ServiceConfiguration.Test.cscfg, définissez les arguments MSBuild option de ligne de `/p:TargetProfile=Test`.
    
     ![][38]
    
     À ce stade, la création de la build doit être terminée.
    
     ![][28]
13. Si vous double-cliquez sur le nom de la build hello, Visual Studio affiche un **résumé de la Build**, y compris les résultats des tests à partir d’associées des projets de test unitaire.
    
     ![][29]
14. Bonjour [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885), vous pouvez afficher le déploiement de hello associé sur hello **déploiements** onglet lorsque hello environnement intermédiaire est sélectionnée.
    
     ![][30]
15. Parcourir les URL du site tooyour. Pour une application web, cliquez sur hello **Parcourir** bouton de barre de commandes hello. Pour un service cloud, choisissez hello URL Bonjour **aperçu rapide** section Hello **tableau de bord** page qui affiche l’environnement intermédiaire de hello pour un service cloud. Les déploiements à partir de l’intégration continue pour les services cloud sont environnement intermédiaire de toohello publié par défaut. Vous pouvez le modifier en définissant les hello **autre environnement de Service Cloud** propriété trop**Production**. Cette capture d’écran montre où hello QU'URL du site se trouve sur la page du tableau de bord du service de cloud hello.
    
    ![][31]
    
    Un nouvel onglet de navigateur s’ouvre tooreveal votre site en cours d’exécution.
    
    ![][32]
    
    Services de cloud computing, si vous apportez d’autres projets tooyour de modifications, vous déclencheur génère plus et vous vont s’accumuler plusieurs déploiements. Hello version la plus récente marquée comme Active.
    
    ![][33]

## <a name="5-redeploy-an-earlier-build"></a>5 : Redéploiement d'une build antérieure
Cette étape s’applique toocloud services et est facultative. Dans hello portail Azure classic, choisissez un précédent déploiement, puis hello **redéployer** bouton toorewind votre tooan site précédemment archivage.  Notez que cela déclenche une nouvelle génération dans TFS et crée une entrée dans l’historique de votre déploiement.

![][34]

## <a name="6-change-hello-production-deployment"></a>6 : modifier le déploiement de Production hello
Cette étape s’applique uniquement les services toocloud, pas les applications web. Lorsque vous êtes prêt, vous pouvez promouvoir hello intermédiaire toohello environnement de production en choisissant hello **échanger** bouton Bonjour portail Azure classic. environnement d’intermédiaire Hello nouvellement déployé est promue tooProduction et environnement de Production précédent hello, le cas échéant, devient un environnement intermédiaire. Hello déploiement actif peut être différente pour hello Production et les environnements de préproduction, mais l’historique de déploiement hello des builds récentes est hello même indépendamment de l’environnement.

![][35]

## <a name="7-run-unit-tests"></a>7 : Exécution de tests unitaires
Cette étape s’applique uniquement les applications tooweb, pas les services de cloud computing. tooput une porte de la qualité de votre déploiement, vous pouvez exécuter des tests unitaires et si elles échouent, vous pouvez arrêter le déploiement de hello.

1. Dans Visual Studio, ajoutez un projet de test unitaire.
   
   ![][39]
2. Ajoutez le projet références toohello projet tootest.
   
   ![][40]
3. Ajoutez quelques tests unitaires. tooget démarré, essayez un test factice qui passera toujours.
   
       ```
       using System;
       using Microsoft.VisualStudio.TestTools.UnitTesting;
   
       namespace UnitTestProject1
       {
           [TestClass]
           public class UnitTest1
           {
               [TestMethod]
               [ExpectedException(typeof(NotImplementedException))]
               public void TestMethod1()
               {
                   throw new NotImplementedException();
               }
           }
       }
       ```
4. Modifier la définition de build hello, choisissez hello **processus** onglet et développez hello **Test** nœud.
5. Ensemble hello **faire échouer la build en cas d’échec du test** tooTrue. Cela signifie que le déploiement de hello n’aura pas lieu, sauf si les tests hello.
   
   ![][41]
6. Placez une nouvelle build dans la file d'attente.
   
   ![][42]
   
   ![][43]
7. Lors de la génération de hello se poursuit, vérifier sa progression.
   
    ![][44]
   
    ![][45]
8. Lors de la génération de hello est terminée, vérifiez les résultats des tests hello.
   
    ![][46]
   
    ![][47]
9. Essayez de créer un nouveau test qui échouera. Ajouter un nouveau test en copiant hello premier, renommez-la et commentez la ligne hello de code qui déclare que NotImplementedException est une exception attendue.
   
       ```
       [TestMethod]
       //[ExpectedException(typeof(NotImplementedException))]
       public void TestMethod2()
       {
           throw new NotImplementedException();
       }
       ```
10. Hello modification tooqueue archivez une nouvelle build.
    
     ![][48]
11. Vue hello toosee détails des résultats sur les échecs de hello.
    
     ![][49]
    
     ![][50]

## <a name="next-steps"></a>Étapes suivantes
Pour en savoir plus sur le test unitaire dans Visual Studio Team Services, consultez [Exécuter des tests unitaires dans votre build](http://go.microsoft.com/fwlink/p/?LinkId=510474). Si vous utilisez Git, consultez [partager votre code dans Git](http://www.visualstudio.com/get-started/share-your-code-in-git-vs.aspx) et [tooAzure de déploiement continu du Service d’applications](../app-service-web/app-service-continuous-deployment.md).  Pour en savoir plus sur Visual Studio Team Services, consultez [Visual Studio Team Services](http://go.microsoft.com/fwlink/?LinkId=253861).

[0]: ./media/cloud-services-continuous-delivery-use-vso/tfs0.PNG
[1]: ./media/cloud-services-continuous-delivery-use-vso/tfs1.png
[2]: ./media/cloud-services-continuous-delivery-use-vso/tfs2.png

[5]: ./media/cloud-services-continuous-delivery-use-vso/tfs5.png
[6]: ./media/cloud-services-continuous-delivery-use-vso/tfs6.png
[7]: ./media/cloud-services-continuous-delivery-use-vso/tfs7.png
[8]: ./media/cloud-services-continuous-delivery-use-vso/tfs8.png
[9]: ./media/cloud-services-continuous-delivery-use-vso/tfs9.png
[10]: ./media/cloud-services-continuous-delivery-use-vso/tfs10.png
[11]: ./media/cloud-services-continuous-delivery-use-vso/tfs11.png
[12]: ./media/cloud-services-continuous-delivery-use-vso/tfs12.png
[13]: ./media/cloud-services-continuous-delivery-use-vso/tfs13.png
[14]: ./media/cloud-services-continuous-delivery-use-vso/tfs14.png
[15]: ./media/cloud-services-continuous-delivery-use-vso/tfs15.png
[16]: ./media/cloud-services-continuous-delivery-use-vso/tfs16.png
[17]: ./media/cloud-services-continuous-delivery-use-vso/tfs17.png
[18]: ./media/cloud-services-continuous-delivery-use-vso/tfs18.png
[19]: ./media/cloud-services-continuous-delivery-use-vso/tfs19.png
[20]: ./media/cloud-services-continuous-delivery-use-vso/tfs20.png
[21]: ./media/cloud-services-continuous-delivery-use-vso/tfs21.png
[22]: ./media/cloud-services-continuous-delivery-use-vso/tfs22.png
[23]: ./media/cloud-services-continuous-delivery-use-vso/tfs23.png
[24]: ./media/cloud-services-continuous-delivery-use-vso/tfs24.png
[25]: ./media/cloud-services-continuous-delivery-use-vso/tfs25.png
[26]: ./media/cloud-services-continuous-delivery-use-vso/tfs26.png
[27]: ./media/cloud-services-continuous-delivery-use-vso/tfs27.png
[28]: ./media/cloud-services-continuous-delivery-use-vso/tfs28.png
[29]: ./media/cloud-services-continuous-delivery-use-vso/tfs29.png
[30]: ./media/cloud-services-continuous-delivery-use-vso/tfs30.png
[31]: ./media/cloud-services-continuous-delivery-use-vso/tfs31.png
[32]: ./media/cloud-services-continuous-delivery-use-vso/tfs32.png
[33]: ./media/cloud-services-continuous-delivery-use-vso/tfs33.png
[34]: ./media/cloud-services-continuous-delivery-use-vso/tfs34.png
[35]: ./media/cloud-services-continuous-delivery-use-vso/tfs35.png
[36]: ./media/cloud-services-continuous-delivery-use-vso/tfs36.PNG
[37]: ./media/cloud-services-continuous-delivery-use-vso/tfs37.PNG
[38]: ./media/cloud-services-continuous-delivery-use-vso/AdvancedMSBuildSettings.PNG
[39]: ./media/cloud-services-continuous-delivery-use-vso/AddUnitTestProject.PNG
[40]: ./media/cloud-services-continuous-delivery-use-vso/AddProjectReferences.PNG
[41]: ./media/cloud-services-continuous-delivery-use-vso/EditBuildDefinitionForTest.PNG
[42]: ./media/cloud-services-continuous-delivery-use-vso/QueueNewBuild.PNG
[43]: ./media/cloud-services-continuous-delivery-use-vso/QueueBuildDialog.PNG
[44]: ./media/cloud-services-continuous-delivery-use-vso/BuildInTeamExplorer.PNG
[45]: ./media/cloud-services-continuous-delivery-use-vso/BuildRequestInfo.PNG
[46]: ./media/cloud-services-continuous-delivery-use-vso/BuildSucceeded.PNG
[47]: ./media/cloud-services-continuous-delivery-use-vso/TestResultsPassed.PNG
[48]: ./media/cloud-services-continuous-delivery-use-vso/CheckInChangeToMakeTestsFail.PNG
[49]: ./media/cloud-services-continuous-delivery-use-vso/TestsFailed.PNG
[50]: ./media/cloud-services-continuous-delivery-use-vso/TestsResultsFailed.PNG
