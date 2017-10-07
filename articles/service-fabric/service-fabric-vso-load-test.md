---
title: "aaaLoad tester votre application à l’aide de Visual Studio Team Services | Documents Microsoft"
description: "Découvrez comment toostress tester vos applications Azure Service Fabric à l’aide de Visual Studio Team Services."
services: service-fabric
documentationcenter: na
author: cawams
manager: timlt
editor: 
ms.assetid: fc743585-0d1b-483f-981d-493f4552ac07
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: cawa
ms.openlocfilehash: 663cf8db5e8f0a4d0d7f27b585645d7f776392f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="load-test-your-application-by-using-visual-studio-team-services"></a>Effectuez un test de charge de votre application avec Visual Studio Team Services
Cet article explique comment toouse Microsoft Visual Studio load test fonctionnalités toostress tester une application. Il utilise un serveur principal de service avec état Azure Service Fabric et un serveur frontal web de service sans état. Bonjour application exemple utilisée ici est un simulateur d’emplacement avion. Vous indiquez l’ID de l’avion, l’heure de départ et la destination. Hello back-end de l’application traite les demandes de hello et frontal hello affiche un avion hello carte qui correspond aux critères de hello.

Hello diagramme suivant illustre les applications de Service Fabric hello que vous allez tester.

![Diagramme de l’application d’emplacement hello exemple avion][0]

## <a name="prerequisites"></a>Composants requis
Avant de commencer, vous toodo hello éléments suivants sont nécessaires :

* Obtenir un compte Visual Studio Team Services. Vous pouvez en obtenir un gratuitement sur [Visual Studio Team Services](https://www.visualstudio.com).
* Obtenir et installer Visual Studio 2013 ou Visual Studio 2015. Cet article utilise Visual Studio 2015 Enterprise, mais Visual Studio 2013 et autres éditions fonctionnent de la même façon.
* Déployer votre tooa application environnement intermédiaire. Consultez [comment tooa des applications toodeploy à distance de cluster à l’aide de Visual Studio](service-fabric-publish-app-remote-cluster.md) pour plus d’informations à ce sujet.
* Comprendre le modèle d’utilisation de votre application. Cette information est un modèle de charge hello toosimulate utilisé.
* Comprendre l’objectif de hello pour votre test de charge. Cela vous permet d’interpréter et d’analyser les résultats de test de charge hello.

## <a name="create-and-run-hello-web-performance-and-load-test-project"></a>Créer et exécuter le projet de Test de charge et de performances de site Web hello
### <a name="create-a-web-performance-and-load-test-project"></a>Créer un projet de test de performance web et de charge
1. Ouvrez Visual Studio 2015. Choisissez **fichier** > **nouveau** > **projet** menu hello barre tooopen hello **nouveau projet** boîte de dialogue.
2. Développez hello **Visual C#** nœud et choisissez **Test** > **projet de Test de charge et de performances de site Web**. Donnez un nom hello projet, puis choisissez hello **OK** bouton.

    ![Capture d’écran de la boîte de dialogue Nouveau projet hello][1]

    Vous devriez voir un nouveau projet de test de performance web et de charge dans l’Explorateur de solutions.

    ![Capture d’écran de l’Explorateur de solutions affichant le projet hello][2]

### <a name="record-a-web-performance-test"></a>Enregistrer un test de performances web
1. Projet de .webtest hello ouvert.
2. Choisissez hello **Ajouter enregistrement** icône toostart une session d’enregistrement dans votre navigateur.

    ![Capture d’écran de l’icône Ajouter un enregistrement de hello dans un navigateur][3]

    ![Capture d’écran du bouton d’enregistrement hello dans un navigateur][4]
3. Parcourir l’application de Service Fabric toohello. Panneau de configuration de l’enregistrement Hello doit afficher les demandes web hello.

    ![Capture d’écran de requêtes web dans hello d’enregistrement du Panneau de configuration][5]
4. Effectuer une séquence d’actions que vous attendez hello utilisateurs tooperform. Ces actions sont utilisées en tant que modèle toogenerate hello charge.
5. Lorsque vous avez terminé, choisissez hello **arrêter** enregistrement toostop de bouton.

    ![Capture d’écran du bouton d’arrêt hello][6]

    projet de .webtest Hello dans Visual Studio doit avoir capturé une série de demandes. Les paramètres dynamiques sont automatiquement remplacés. À ce stade, vous pouvez supprimer toutes les demandes de dépendance supplémentaires et répétées qui ne font pas partie de votre scénario de test.
6. Enregistrer le projet de hello, puis choisissez hello **exécuter le Test** tester localement de performances de site web de commande toorun hello et assurez-vous que tout fonctionne correctement.

    ![Capture d’écran de hello commande d’exécuter le Test][7]

### <a name="parameterize-hello-web-performance-test"></a>Paramétrer le test de performances web hello
Vous pouvez paramétrer le test de performances web hello en convertissant un test de performances web codé de tooa, puis en modifiant les code hello. En guise d’alternative, vous pouvez lier la liste données tooa des test de performances hello web afin que hello test effectue une itération dans les données de salutation. Consultez [générer et exécuter un test de performances web codé](https://msdn.microsoft.com/library/ms182552.aspx) pour plus d’informations sur la façon dont tooconvert hello web performance test tooa test codé de le. Consultez [ajouter un test de performances web de données source tooa](https://msdn.microsoft.com/library/ms243142.aspx) pour plus d’informations sur la façon dont les performances de site web toobind données tooa de test.

Pour cet exemple, nous allons convertir test tooa codé du test de performances hello web afin de pouvoir remplacer hello avion ID avec un GUID généré et ajouter d’autres demandes toosend vols toodifferent emplacements.

### <a name="create-a-load-test-project"></a>Créer un projet de test de charge
Un projet de test de charge se compose d’un ou plusieurs scénarios décrits par le test de performances web hello et de test unitaire, ainsi que les paramètres de test de charge spécifié supplémentaire. Hello suit montrent comment toocreate une charge de projet de test :

1. Dans le menu contextuel de hello de votre projet de Test de charge et de performances de site Web, choisissez **ajouter** > **Test de charge**. Bonjour **du Test de charge** Assistant, choisissez hello **suivant** bouton Paramètres de test tooconfigure hello.
2. Bonjour **modèle de charge** , choisissez si vous souhaitez une charge utilisateur constante ou une charge par étape, qui commence par un nombre limité d’utilisateurs, et augmente hello utilisateurs au fil du temps.

    Si vous avez une bonne estimation de hello charge utilisateur et que vous souhaitez toosee fonctionnement d’un système en cours de hello, choisissez **charge constante**. Si votre objectif est toolearn si hello système effectue régulièrement sous différentes charges, choisissez **charge par étape**.
3. Bonjour **la combinaison de tests** , choisissez hello **ajouter** bouton, puis sélectionnez hello de test que vous souhaitez tooinclude hello test de charge. Vous pouvez utiliser hello **Distribution** pourcentage de hello colonne toospecify du nombre total de tests exécutés pour chaque test.
4. Bonjour **paramètres d’exécution** section, spécifiez la durée du test de charge hello.

   > [!NOTE]
   > Hello **d’itérations de Test** option est disponible uniquement lorsque vous exécutez un test de charge localement à l’aide de Visual Studio.
   >
   >
5. Bonjour **emplacement** section de **paramètres d’exécution**, spécifier l’emplacement de hello où les requêtes de tests de charge sont générés. Assistant de Hello peut vous demander toolog dans tooyour compte Team Services. Connectez-vous, puis choisissez un emplacement géographique. Lorsque vous avez terminé, choisissez hello **Terminer** bouton.
6. Une fois le test de charge hello est créé, ouvrez hello .loadtest projet et choisissez actuel hello comme paramètre, d’exécution **paramètres d’exécution** > **exécution1 [actifs]**. Paramètres de hello exécuter s’ouvre dans hello **propriétés** fenêtre.
7. Bonjour **résultats** section Hello **paramètres d’exécution** fenêtre Propriétés, hello **Timing Details Storage** paramètre doit avoir **aucun** en tant que sa valeur par défaut. Modifiez cette valeur trop**tous les détails individuels** tooget plus d’informations sur les résultats de test de charge hello. Consultez [tests de charge](https://www.visualstudio.com/load-testing.aspx) pour plus d’informations sur comment tooconnect tooVisual Studio Team Services et exécuter une charge de test.

### <a name="run-hello-load-test-by-using-visual-studio-team-services"></a>Exécuter un test de charge hello à l’aide de Visual Studio Team Services
Choisissez hello **exécuter le Test de charge** commande toostart hello série.

![Capture d’écran de hello commande d’exécuter un Test de charge][8]

## <a name="view-and-analyze-hello-load-test-results"></a>Afficher et analyser les résultats de test de charge hello
En tant que hello charger test progresse, les informations de performances hello représentée dans le graphique. Vous devez voir quelque chose de similaire toohello suivant du graphique.

![Capture d’écran du graphique de performances pour les résultats des tests de charge][9]

1. Choisissez hello **télécharger rapport** lien vers haut hello de page de hello. Après le téléchargement de rapports de hello, choisissez hello **afficher le rapport** bouton.

    Sur hello **graphique** onglet, vous pouvez voir des graphiques pour différents compteurs de performance. Sur hello **Résumé** sous l’onglet hello globale des résultats de test s’affichent. Hello **Tables** onglet affiche le nombre total de hello des tests de charge de réussites et les échecs.
2. Choisissez les liens de numéro hello sur hello **Test** > **n’a pas pu** et hello **erreurs** > **nombre** colonnes Détails de l’erreur toosee.

    Hello **détail** onglet affiche des informations scénario virtuelles utilisateur et de test pour les demandes ayant échouées. Ces données peuvent être utiles si le test de charge hello inclut plusieurs scénarios.

Consultez [analyse charger des résultats des Test Bonjour vue graphiques de l’Analyseur de Test de charge de hello](https://www.visualstudio.com/load-testing.aspx) pour plus d’informations sur l’affichage de chargement des résultats de tests.

## <a name="automate-your-load-test"></a>Automatiser votre test de charge
Test de charge de Visual Studio Team Services fournit les API toohelp gérer des tests de charge et d’analyser les résultats dans un compte Team Services. Consultez la page [API Rest de test de charge Cloud](http://blogs.msdn.com/b/visualstudioalm/archive/2014/11/03/cloud-load-testing-rest-apis-are-here.aspx) pour plus d’informations.

## <a name="next-steps"></a>Étapes suivantes
* [Surveillance et diagnostic des services dans une configuration de développement d’ordinateur local](service-fabric-diagnostics-how-to-monitor-and-diagnose-services-locally.md)

[0]: ./media/service-fabric-vso-load-test/OverviewDiagram.png
[1]: ./media/service-fabric-vso-load-test/NewProjectDialog.png
[2]: ./media/service-fabric-vso-load-test/Project.png
[3]: ./media/service-fabric-vso-load-test/AddRecording.png
[4]: ./media/service-fabric-vso-load-test/AddRecording2.png
[5]: ./media/service-fabric-vso-load-test/ActionSequence.png
[6]: ./media/service-fabric-vso-load-test/StopRecording.png
[7]: ./media/service-fabric-vso-load-test/RunTest.png
[8]: ./media/service-fabric-vso-load-test/RunTest2.png
[9]: ./media/service-fabric-vso-load-test/Graph.png
