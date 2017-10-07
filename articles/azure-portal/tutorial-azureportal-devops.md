---
title: "Didacticiel : DevOps hello portail Azure | Documents Microsoft"
description: "En savoir plus hello différents flux de travail DevOps Bonjour portail Azure."
services: azure-portal
documentationcenter: 
author: mlearned
manager: douge
editor: mlearned
ms.assetid: 4f1c5bc1-c732-4d35-b5df-0fd68e547d38
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 06/05/2016
ms.author: mlearned
ms.openlocfilehash: 4c32dbbd4e4b1c3809ef4b01e1496e350183ebde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-devops-with-hello-azure-portal"></a>Didacticiel : DevOps hello portail Azure
Hello plateforme Azure est plein de flux de travail flexible DevOps. Dans ce didacticiel, vous découvrez comment tooleverage les fonctionnalités de hello de toodevelop du portail Azure hello, tester, déployer, résoudre les problèmes, surveiller et gérer des applications en cours d’exécution. Ce didacticiel se concentre sur les éléments suivants de hello :

1. Création d’une application web et possibilité de déploiement continu
2. Développement et test d’une application
3. Surveillance et dépannage d’une application
4. Tâches de gestion des applications générales

## <a name="creating-a-web-app-and-enabling-continuous-deployment"></a>Création d’une application web et possibilité de déploiement continu
Créer une application Web avec [Azure App Service](https://azure.microsoft.com/services/app-service/), que vous allez utiliser dans le reste de hello de ce didacticiel. Vous allez d’abord activer le déploiement continu à partir de votre référentiel de code source dans notre environnement Azure en cours d’exécution.

1. Connectez-vous à hello portail Azure
2. Choisissez **des Services d’application** &gt; **icône Ajouter** et entrez un nom, choisissez votre abonnement et créer un nouveau tooserve de groupe de ressources en tant que conteneur hello pour le service de hello.
   
   Les groupes de ressources permettent de toomanage différents aspects de la solution hello telles que la facturation, déploiements et de surveillance sous la forme d’un seul groupe via [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).
   
   ![image1][image1]
3. Après quelques instants, votre App Service est créé. Prendre des différentes options de menu pour le service de hello hello de tooexplore quelques minutes dans le portail de hello.
   
   ![image2][image2]    
4. Cliquez sur les URL hello. Notez les diverses options disponibles pour les outils et des référentiels hello. Vous pouvez également utiliser des langages de hello et infrastructures de votre choix, y compris .NET, Java et Ruby.
   
   ![image3][image3]    
5. Hello portail Azure permet un déploiement continu un processus simple qui implique quelques étapes simples. Bonjour portail Azure, choisissez les paramètres à partir de l’icône hello pour le service d’application hello que vous venez de créer.
   
   ![image4][image4]
   
   À partir du panneau hello qui s’ouvre sur hello droite, faites défiler toohello section de la publication.
   
   ![image5][image5]
6. Ensuite, configurez certains paramètres tooenable un déploiement continu pour l’application hello. Cliquez sur Source du déploiement, puis sur Choisir la source. Notez les diverses hello des options pour les sources de référentiel.
   
   ![image6][image6]
7. Pour cet exemple, sélectionnez GitHub. Éventuellement, choisissez hello le référentiel de votre choix et configurer les informations d’identification d’autorisation de hello.
   
   ![image7][image7]
8. Après le référentiel de tooyour d’autorisation, vous pouvez ensuite choisir un projet et la branche que vous souhaitez toodeploy. Plusieurs exemples fictifs sont répertoriés ci-dessous.
   
   ![image8][image8]
9. Une fois votre projet et votre branche choisis, cliquez sur OK. Vous devez commencer toosee des notifications d’un déploiement.
   
   ![image9][image9]
10. Accédez tooGitHub arrière toosee hello webhook qui a été créé le référentiel de contrôle de source de hello toointegrate avec Azure. Hello portail Azure permet l’intégration avec GitHub avec seulement quelques étapes simples.
    
    ![image10][image10]
11. toodemonstrate le déploiement continu, vous ajouter rapidement certains référentiel de contenu toohello. Pour obtenir un exemple simple, ajoutez un référentiel GitHub d’exemples texte fichier tooa. Vous êtes libre toouse .NET, Ruby, Python ou un autre type d’application à l’aide du Service d’applications. Pensez libre tooadd un fichier texte, référentiel de toohello application ASP.NET MVC, Java ou Ruby de votre choix.
    
    ![image11][image11]
12. Après avoir validé le référentiel de tooyour de modifications, vous voyez un nouveau déploiement lancer dans la zone de notification de portail de hello. Si vous ne voyez pas rapidement modifications après avoir validé tooyour référentiel, cliquez sur Synchroniser.
    
    ![image12][image12]
13. À ce stade, si vous essayez de chargez la page hello pour le service de l’application hello, vous pouvez recevoir une erreur 403. Dans cet exemple, il est, car il n’existe aucune configuration de document par défaut pour la page hello tel qu’un fichier comme index.htm ou default.html. Vous pouvez y remédier rapidement avec hello pour les outils Bonjour portail Azure.  Bonjour portail Azure, choisissez les paramètres &gt; paramètres de l’Application.
    
     ![image13][image13]
14. Un panneau regroupant les paramètres de l’application s’ouvre. Entrez le nom hello de page de hello « SamplePage.html » et cliquez sur Enregistrer. Prendre des autres paramètres hello de tooexplore quelques minutes.
    
    ![image14][image14]
15. Si vous le souhaitez actualiser votre tooensure URL de navigateur vous voyez les modifications hello attendu. Dans ce cas, il est de texte simple maintenant remplissage page de hello. Chaque référentiel toohello de modification supplémentaire se traduirait par un nouveau déploiement automatique.
    
    ![image15][image15]
    
    L’activation d’un déploiement continu avec hello portail Azure est une expérience simple. Vous pouvez également générer des pipelines de version plus complexes et utiliser de nombreuses autres techniques avec contrôle de code source existant et d’intégration continue systèmes toodeploy tooAzure, telles que tirant parti de génération automatisé et les systèmes de gestion de version.

## <a name="develop-and-test-an-app"></a>Développement et test d’une application
Ensuite, modifiez toohello code base et déployer rapidement ces modifications. Vous serez également configurer certains tests de performances pour l’application Web hello.

1. Bonjour Azure Portal choisir les Services d’application à partir du volet de navigation hello et recherchez votre application de Service.
   
   ![image16][image16]
2. Cliquez sur Outils
   
   ![image17][image17]
3. Notez que hello catégorie sous Outils de développement. Il existe plusieurs outils utiles ici qui nous permettent de toowork avec les applications sans quitter hello portail Azure. Cliquez sur Console.
   
   ![image18][image18]
4. Dans la fenêtre de console hello, vous pouvez émettre des commandes actives pour votre application. Commande de type hello dir et appuyez sur entrer. Notez que les commandes nécessitant des privilèges élevés ne fonctionnent pas.
   
   ![image19][image19]
5. Replacer toohello développer catégorie et choisissez Visual Studio Online. Remarque : Visual Studio Online devient Visual Studio Team Services.
   
   ![image20][image20]
6. Basculer sur l’expérience d’édition dans le navigateur hello pour votre application.
   
   ![image21][image21]
7. Une extension web pour votre application s’installe. Extensions rapidement et facilement ajoutent des fonctionnalités tooapps dans Azure. Notez que certaines des hello autres types d’extensions disponibles dans la capture d’écran hello ci-dessous.
   
   ![image22][image22]
8. Une fois que hello extension Visual Studio Online est installé, cliquez sur OK.
   
   ![image23][image23]
9. Un navigateur onglet s’ouvre dans lequel vous consultez un développement IDE directement dans le navigateur de hello. Avis hello ci-dessous bénéficie dans Chrome.
   
   ![image24][image24]
10. Vous pouvez effectuer plusieurs activités telles que les fichiers de la modifier, ajouter des fichiers et des dossiers et télécharger le contenu à partir du site en ligne hello. Créez un fichier de SamplePage.html toohello édition rapide.
    
    ![image25][image25]
11. Dans quelques instants, hello modifications sont automatiquement enregistrées. Si vous accédez toohello arrière page, vous pouvez voir les modifications de hello. Gardez à l’esprit que les modifications en direct ne sont généralement pas appropriées pour les environnements de production. Toutefois, les outils de hello rendent toomake très facile de rapides modifications pour le développement et les environnements de test.
    
    ![image26][image26]
    
    ![image27][image27]
12. Replacez le panneau d’outils toohello et sous la catégorie de développer hello, cliquez sur le Test de performances.
    
    ![image28][image28]
13. Vous devez tooset un compte de services d’équipe. Pour plus d’informations, consultez la page [Créer un compte Team Services](https://www.visualstudio.com/docs/setup-admin/team-services/sign-up-for-visual-studio-team-services)
14. Cliquez sur Nouveau toocreate un test de performances.
    
    ![image29][image29]
    
    Configurer hello différentes valeurs et cliquez sur Exécuter le Test bas hello hello boîte de dialogue tooinitiate un test de performances.
    
    ![image30][image30]
    
    ![image31][image31]
15. Une fois le test de hello démarre l’exécution, vous pouvez surveiller l’état de hello.
    
    ![image32][image32]
    
    Une fois le test de hello terminée, en cliquant sur le résultat de hello affiche plus de détails.
    
    ![image33][image33]
16. Dans cet exemple, vous avez créé une petite série de tests, donc il est tooanalyze de données limité, mais vous pouvez consultez diverses mesures ainsi que réexécutez votre test à partir de cette vue. Hello portail Azure facilite la création, l’exécution et analyse des tests de performances web un processus simple. Hello captures d’écran ci-dessous affichent les données de performances de hello.
    
    ![image34][image34]
    
    ![image35][image35]
    
    ![image36][image36]

## <a name="monitoring-and-troubleshooting-an-app"></a>Surveillance et dépannage d’une application
Azure fournit de nombreuses fonctionnalités de surveillance et de dépannage pour les applications en cours d’exécution.

1. Bonjour portail Azure pour notre application Web, sélectionnez Outils.
   
   ![image37][image37]
2. Sous catégorie de résolution des problèmes de hello, notez hello différentes options pour l’utilisation des problèmes potentiels d’outils tootroubleshoot avec une application en cours d’exécution. Vous pouvez par exemple analyser le trafic HTTP en direct, activer la réparation spontanée, afficher les journaux et bien plus encore.
   
   ![image38][image38]
3. Choisissez l’affichage de certains codes HTTP get tooquickly de métriques d’un Site.
   
   ![image39][image39]
4. Sélectionnez Diagnostics en tant que service. Choisissez votre type d’application, puis sélectionnez Exécuter.
   
   ![image40][image40]
   
   La collecte commence.
   
   ![image41][image41]
5. Vous pouvez choisir les problèmes potentiels de hello journal approprié toodiagnose. Vous devez toosee de journalisation tooenable toutes les données disponibles hello options telles que les journaux HTTP.
   
   ![image42][image42]
   
   En cliquant sur le fichier d’image mémoire hello vous pouvez télécharger et analyser un DebugDiag toohelp de rapports d’analyse recherche les problèmes potentiels.
   
   ![image43][image43]
6. tooview plus de données, vous devez tooenable la journalisation supplémentaire. Bonjour portail Azure, accédez toohello Web app et choisissez les paramètres.
   
   ![image44][image44]
7. Faites défiler la liste des catégories de fonctionnalités toohello et choisissez les journaux de Diagnostic.
   
      ![image45][image45]
8. Notez que hello diverses options pour la journalisation. Activez la journalisation du serveur web et cliquez sur Enregistrer.
   
   ![image46][image46]
9. Replacer la zone d’outils toohello pour l’application hello et choisissez Diagnostics en tant que service et cliquez sur Exécuter toorerun hello la collecte de données.
   
   ![image47][image47]
10. Avec le paramètre d’enregistrement hello HTTP activé, vous voyez maintenant les données collectées pour les journaux HTTP.
    
    ![image48][image48]
11. En cliquant sur le fichier journal de hello HTML, vous produire un rapport basé sur le navigateur rich pour un examen approfondi.
    
    ![image49][image49]
12. Replacer dans la section Outils toohello hello portail Azure pour l’application hello. Faites défiler la section des outils toohello et choisissez Explorateur de processus.
    
    ![image50][image50]
13. En choisissant Explorateur de processus, vous pouvez afficher plus d’informations sur les processus en cours d’exécution. Notez ci-dessous vous permettre Explorer le processus et même supprimer des processus à partir d’hello portail Azure.
    
    ![image51][image51]
    
    ![image52][image52]
14. Replacez le panneau des paramètres toohello sur hello gauche. Cliquez sur Nouvelle demande de support.
    
    ![image53][image53]
15. À partir du panneau hello sur hello droite, vous pouvez remplir des détails sur les problèmes de hello, entrez les informations de contact et même télécharger des données de diagnostic. Hello portail Azure permet de travailler avec prise en charge de Microsoft, une expérience transparente.
    
    ![image54][image54]
    
    ![image55][image55]
    
    Hello portail Azure permet de fournir performante et familière pour les outils expériences toohelp moniteur et résoudre les problèmes de nos applications en cours d’exécution. Vous êtes également en mesure de tootake action rapidement en effectuant des tâches telles que le recyclage des processus, l’activation et désactivation des différentes collections de données et l’intégration de même avec prise en charge du professionnel de Microsoft.

## <a name="general-application-management"></a>Gestion des applications générales
Lors de la gestion des applications, vous devez souvent tooperform un vaste éventail d’activités telles que la configuration des stratégies de sauvegarde, l’implémentation et la gestion des fournisseurs d’identité et configurer le contrôle d’accès en fonction du rôle. Comme avec hello autres expériences DevOps, hello plateforme Azure s’intègre à ces tâches directement dans le portail de hello.

1. tooensure vous conservez hello Web application protégée contre la perte de données, vous devez le tooconfigure sauvegardes. Accédez à zone de paramètres toohello pour votre application Web.
   
   ![image56][image56]
2. Dans le panneau hello sur hello droite, faites défiler catégorie de fonctions toohello.
   
    ![image57][image57]
3. Choisissez les sauvegardes ; un panneau s’ouvre sur la droite de hello.
   
   ![image58][image58]
4. Cliquez sur Configurer, choisissez un compte de stockage panneau hello sur hello droite.
   
   ![image59][image59]
5. Maintenant, créez et choisissez une toohold de conteneur de stockage de vos sauvegardes. Cliquez sur Créer en bas de hello du Panneau de hello. Puis sélectionnez le conteneur de hello.
   
   ![image60][image60]
6. Une fois que vous avez choisi le conteneur de hello, vous pouvez configurer des planifications, ainsi que les sauvegardes le programme d’installation pour vos bases de données. Pour ce scénario, cliquez sur hello icône d’enregistrement.
   
    ![image61][image61]
7. Après l’enregistrement, faites défiler panneau toohello arrière sur la gauche de hello pour les sauvegardes. Cliquez sur Sauvegarder maintenant les application hello tooback.
   
    ![image62][image62]
8. Dans quelques instants, vous verrez qu’une sauvegarde a été créée. Hello avis restaurer maintenant une option sur hello capture d’écran ci-dessous.
   
    ![image63][image63]
9. Cliquez sur Restaurer maintenant et examinez le panneau de toohello options hello sur hello droite. Vous pouvez choisir qu'une sauvegarde appropriée et facilement tooan de restauration précédemment d’état en fonction des besoins. Hello portail Azure nous a aidés à facilement activer une stratégie de récupération d’urgence simple pour l’application hello.
   
    ![image64][image64]
10. Déplacer Panneau de paramètres toohello sur hello gauche et sous fonctionnalités et choisissez l’authentification ou d’autorisation.
    
     ![image65][image65]
11. Dans le panneau hello sur hello droit, choisissez l’authentification du Service application. Notez que hello de diverses options que vous pouvez configurer avec les fournisseurs populaires.
    
     ![image66][image66]
12. Choisissez fournisseur hello de votre choix et notez les options hello pour l’étendue de hello. Vous pouvez fournir un ID d’application et le code Secret et rapidement activer l’authentification Facebook pour l’application hello. Hello portail Azure Active l’authentification en tant qu’une solution clé en main pour les applications.
    
     ![image67][image67]
13. Replacez le panneau des paramètres toohello et choisir des utilisateurs sous la catégorie de gestion des ressources hello.
    
     ![image68][image68]
14. Dans le panneau hello sur hello droite examiner hello diverses options pour l’ajout de rôles et les utilisateurs. Hello portail Azure vous permet de facilement contrôler RBAC (contrôle d’accès basé sur les rôles) pour une application hello.
    
     ![image69][image69]

## <a name="summary"></a>Résumé
Ce didacticiel présentés ici puissance hello avec hello plateforme Azure rapidement l’activation de déploiement continu pour une application web, développement différents et activités de test, analyse et résolution des problèmes d’une application en temps réel et enfin la gestion de clé stratégies telles que la récupération d’urgence, d’identité et contrôle d’accès en fonction du rôle. Hello plateforme Azure permet une expérience intégrée pour ces flux de travail DevOps et travailler efficacement, en restant dans le contexte pour la tâche hello en cours.

## <a name="next-steps"></a>Étapes suivantes
* Le Gestionnaire de ressources Azure est important pour l’activation de DevOps sur hello plateforme Azure.  toolearn plus visitez [vue d’ensemble du Gestionnaire de ressources Azure](../azure-resource-manager/resource-group-overview.md).
* toolearn plus sur le déploiement du Service d’applications Azure, visitez [déployer votre tooAzure d’application du Service d’applications](../app-service-web/web-sites-deploy.md)

[image1]: ./media/tutorial-azureportal-devops/image1.png
[image2]: ./media/tutorial-azureportal-devops/image2.png
[image3]: ./media/tutorial-azureportal-devops/image3.png
[image4]: ./media/tutorial-azureportal-devops/image4.png
[image5]: ./media/tutorial-azureportal-devops/image5.png
[image6]: ./media/tutorial-azureportal-devops/image6.png
[image7]: ./media/tutorial-azureportal-devops/image7.png
[image8]: ./media/tutorial-azureportal-devops/image8.png
[image9]: ./media/tutorial-azureportal-devops/image9.png
[image10]: ./media/tutorial-azureportal-devops/image10.png
[image11]: ./media/tutorial-azureportal-devops/image11.png
[image12]: ./media/tutorial-azureportal-devops/image12.png
[image13]: ./media/tutorial-azureportal-devops/image13.png
[image14]: ./media/tutorial-azureportal-devops/image14.png
[image15]: ./media/tutorial-azureportal-devops/image15.png
[image16]: ./media/tutorial-azureportal-devops/image16.png
[image17]: ./media/tutorial-azureportal-devops/image17.png
[image18]: ./media/tutorial-azureportal-devops/image18.png
[image19]: ./media/tutorial-azureportal-devops/image19.png
[image20]: ./media/tutorial-azureportal-devops/image20.png
[image21]: ./media/tutorial-azureportal-devops/image21.png
[image22]: ./media/tutorial-azureportal-devops/image22.png
[image23]: ./media/tutorial-azureportal-devops/image23.png
[image24]: ./media/tutorial-azureportal-devops/image24.png
[image25]: ./media/tutorial-azureportal-devops/image25.png
[image26]: ./media/tutorial-azureportal-devops/image26.png
[image27]: ./media/tutorial-azureportal-devops/image27.png
[image28]: ./media/tutorial-azureportal-devops/image28.png
[image29]: ./media/tutorial-azureportal-devops/image29.png
[image30]: ./media/tutorial-azureportal-devops/image30.png
[image31]: ./media/tutorial-azureportal-devops/image31.png
[image32]: ./media/tutorial-azureportal-devops/image32.png
[image33]: ./media/tutorial-azureportal-devops/image33.png
[image34]: ./media/tutorial-azureportal-devops/image34.png
[image35]: ./media/tutorial-azureportal-devops/image35.png
[image36]: ./media/tutorial-azureportal-devops/image36.png
[image37]: ./media/tutorial-azureportal-devops/image37.png
[image38]: ./media/tutorial-azureportal-devops/image38.png
[image39]: ./media/tutorial-azureportal-devops/image39.png
[image40]: ./media/tutorial-azureportal-devops/image40.png
[image41]: ./media/tutorial-azureportal-devops/image41.png
[image42]: ./media/tutorial-azureportal-devops/image42.png
[image43]: ./media/tutorial-azureportal-devops/image43.png
[image44]: ./media/tutorial-azureportal-devops/image44.png
[image45]: ./media/tutorial-azureportal-devops/image45.png
[image46]: ./media/tutorial-azureportal-devops/image46.png
[image47]: ./media/tutorial-azureportal-devops/image47.png
[image48]: ./media/tutorial-azureportal-devops/image48.png
[image49]: ./media/tutorial-azureportal-devops/image49.png
[image50]: ./media/tutorial-azureportal-devops/image50.png
[image51]: ./media/tutorial-azureportal-devops/image51.png
[image52]: ./media/tutorial-azureportal-devops/image52.png
[image53]: ./media/tutorial-azureportal-devops/image53.png
[image54]: ./media/tutorial-azureportal-devops/image54.png
[image55]: ./media/tutorial-azureportal-devops/image55.png
[image56]: ./media/tutorial-azureportal-devops/image56.png
[image57]: ./media/tutorial-azureportal-devops/image57.png
[image58]: ./media/tutorial-azureportal-devops/image58.png
[image59]: ./media/tutorial-azureportal-devops/image59.png
[image60]: ./media/tutorial-azureportal-devops/image60.png
[image61]: ./media/tutorial-azureportal-devops/image61.png
[image62]: ./media/tutorial-azureportal-devops/image62.png
[image63]: ./media/tutorial-azureportal-devops/image63.png
[image64]: ./media/tutorial-azureportal-devops/image64.png
[image65]: ./media/tutorial-azureportal-devops/image65.png
[image66]: ./media/tutorial-azureportal-devops/image66.png
[image67]: ./media/tutorial-azureportal-devops/image67.png
[image68]: ./media/tutorial-azureportal-devops/image68.png
[image69]: ./media/tutorial-azureportal-devops/image69.png
