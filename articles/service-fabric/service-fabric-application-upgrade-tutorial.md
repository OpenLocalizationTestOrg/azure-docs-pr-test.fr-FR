---
title: "didacticiel mise à niveau d’application Fabric aaaService | Documents Microsoft"
description: "Cet article explique les hello expérience de déploiement d’une application de Service Fabric, modifier le code de hello et déploiement d’une mise à niveau à l’aide de Visual Studio."
services: service-fabric
documentationcenter: .net
author: mani-ramaswamy
manager: timlt
editor: 
ms.assetid: a3181a7a-9ab1-4216-b07a-05b79bd826a4
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 8/9/2017
ms.author: subramar
ms.openlocfilehash: d069ff0b291018dbac846e65cddff1e9d73d156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-application-upgrade-tutorial-using-visual-studio"></a>Didacticiel sur la mise à niveau d'une application Service Fabric à l'aide de Visual Studio
> [!div class="op_single_selector"]
> * [PowerShell](service-fabric-application-upgrade-tutorial-powershell.md)
> * [Visual Studio](service-fabric-application-upgrade-tutorial.md)
> 
> 

<br/>

Azure Service Fabric simplifie hello la mise à niveau des applications cloud en veillant à ce que seuls les services modifiés sont mis à niveau, et que le contrôle d’intégrité de l’application est analysé tout au long du processus de mise à niveau hello. Elle annule également automatiquement version précédente de toohello application hello lorsqu’il rencontre des problèmes. Mises à niveau de service Fabric application *sans interruption de service*, car l’application hello peut être mis à niveau sans interruption de service. Ce didacticiel décrit comment toocomplete une mise à niveau propagée à partir de Visual Studio.

## <a name="step-1-build-and-publish-hello-visual-objects-sample"></a>Étape 1 : Créer et publier des exemples d’objets visuels hello
Commencez par télécharger hello [objets visuels](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Actors/VisualObjects) application à partir de GitHub. Ensuite, générer et publier l’application hello en cliquant sur le projet d’application hello, **VisualObjects**et en sélectionnant hello **publier** dans l’élément de menu hello Service Fabric.

![Menu contextuel pour une application Service Fabric][image1]

En sélectionnant **publier** affiche une fenêtre contextuelle, et vous pouvez définir hello **cibler profile** trop**PublishProfiles\Local.xml**. fenêtre Hello doit ressembler à hello suivant avant de cliquer sur **publier**.

![Publication d'une application Service Fabric][image2]

Vous pouvez maintenant cliquer sur **publier** dans la boîte de dialogue hello. Vous pouvez utiliser [Service Fabric Explorer tooview hello cluster et hello l’application](service-fabric-visualizing-your-cluster.md). Hello application d’objets visuels possède un service web que vous pouvez accéder en tapant les tooby [http://localhost :8081/visualobjects/](http://localhost:8081/visualobjects/) dans la barre d’adresses hello de votre navigateur.  Vous devez voir les 10 objets visual flottantes déplacer dans l’écran hello.

**Remarque :** si trop de déploiement`Cloud.xml` profil (Azure Service Fabric), application hello doit ensuite être disponible à l’adresse **http://{ServiceFabricName}. {} Region}.cloudapp.Azure.com:8081/visualobjects/**. Assurez-vous que vous n’avez `8081/TCP` configuré Bonjour équilibrage de charge (recherche hello équilibrage de charge Bonjour même groupe de ressources en tant qu’instance de Service Fabric hello).

## <a name="step-2-update-hello-visual-objects-sample"></a>Étape 2 : Mettre à jour des exemples d’objets visuels hello
Vous pouvez remarquer qu’avec la version de hello qui a été déployée à l’étape 1, les objets visuels hello ne pas faire pivoter. Nous allons mettre à niveau de ce tooone application où les objets visuels hello également faire pivoter.

Sélectionnez le projet VisualObjects.ActorService hello hello VisualObjects solution et ouvrez hello **VisualObjectActor.cs** fichier. Dans ce fichier, accédez à toohello méthode `MoveObject`, commentez `visualObject.Move(false)`et ne commentez pas `visualObject.Move(true)`. Cette modification de code fait pivoter les objets hello après la mise à niveau de service de hello.  **Vous pouvez désormais créer (pas la reconstruction) hello solution**, quelles sont les builds hello modifié des projets. Si vous sélectionnez *tout reconstruire*, vous disposez de versions de hello tooupdate pour tous les hello projets.

Nous devons également tooversion notre application. modification de la version de hello toomake une fois avec le bouton droit sur hello **VisualObjects** projet, vous pouvez utiliser Visual Studio de hello **modifier les Versions de manifeste** option. Cette option affiche la boîte de dialogue de hello pour les versions de l’édition comme suit :

![Boîte de dialogue Contrôle de version][image3]

Mise à jour des versions de hello pour hello modifié des projets et les packages de code, ainsi que de l’application de hello tooversion 2.0.0. Après les modifications de hello, manifeste de hello doit ressembler à hello suivant (parties en gras permet d’afficher les modifications hello) :

![Mise à jour des versions][image4]

outils de Visual Studio Hello faire cumuls automatique des versions lors de la sélection **mettre à jour automatiquement les applications et les versions de service**. Si vous utilisez [SemVer](http://www.semver.org), vous avez besoin de code de hello tooupdate et/ou configuration package version uniquement si cette option est sélectionnée.

Enregistrer les modifications de hello et recherchent hello **mise à niveau hello Application** boîte.

## <a name="step-3--upgrade-your-application"></a>Étape 3 : Mettre à niveau votre application
Familiarisez-vous avec hello [paramètres de mise à niveau l’application](service-fabric-application-upgrade-parameters.md) et hello [mise à niveau](service-fabric-application-upgrade.md) tooget une bonne compréhension de hello différentes mise à niveau des paramètres, les délais d’attente et d’intégrité critère qui peuvent être appliquées. Pour cette procédure pas à pas, critère d’évaluation de hello service d’intégrité a la valeur par défaut de toohello (mode non contrôlé). Vous pouvez configurer ces paramètres en sélectionnant **configurer les paramètres de mise à niveau** , puis en modifiant les paramètres de hello comme vous le souhaitez.

Est maintenant toutes les applications de hello toostart jeu de mise à niveau en sélectionnant **publier**. Cette option met à niveau votre tooversion application 2.0.0, dans laquelle faire pivoter les objets hello. Service Fabric met à niveau un domaine de mise à jour à la fois (certains objets sont mis à jour en premier lieu, suivi par d’autres) et service de hello reste accessible au cours de la mise à niveau hello. Service d’accès toohello peut être vérifié dans votre client (navigateur).  

À présent, comme hello continue mise à niveau d’application, vous pouvez le surveiller avec Service Fabric Explorer, à l’aide de hello **mises à niveau en cours d’exécution** onglet sous applications de hello.

Dans quelques minutes, tous les domaines de mise à jour doivent être mis à niveau (terminé), et fenêtre de sortie de Visual Studio hello doit également indiquer que la mise à niveau hello. Et vous devez constater que *tous les* rotation d’objets visuels de hello dans la fenêtre du navigateur sont maintenant !

Vous souhaitez tootry modification des versions de hello et le déplacement à partir de la version 2.0.0 tooversion 3.0.0 en guise d’exercice, ou même à partir de la version 2.0.0 sauvegarder tooversion 1.0.0. Manipuler les délais d’attente et toomake des stratégies de contrôle d’intégrité vous-même connaissent. Lorsque le déploiement tooan Azure cluster en tant qu’et non cluster local de tooa, paramètres hello utilisés peut-être toodiffer. Nous vous recommandons de définir les délais d’attente hello plus restrictives.

## <a name="next-steps"></a>Étapes suivantes
[mise à niveau de votre application à l’aide de PowerShell](service-fabric-application-upgrade-tutorial-powershell.md) vous guide à travers une mise à niveau de l’application à l’aide de PowerShell.

Contrôlez les mises à niveau de votre application à l’aide des [paramètres de mise à niveau](service-fabric-application-upgrade-parameters.md).

Rendre les mises à niveau de votre application compatible par learning comment toouse [sérialisation des données](service-fabric-application-upgrade-data-serialization.md).

Découvrez comment toouse des fonctionnalités avancées lors de la mise à niveau de votre application en vous reportant trop[rubriques avancées](service-fabric-application-upgrade-advanced.md).

Résoudre les problèmes courants dans les mises à niveau de l’application en faisant référence à des étapes de toohello de [résolution des problèmes de mises à niveau de l’application](service-fabric-application-upgrade-troubleshooting.md).

[image1]: media/service-fabric-application-upgrade-tutorial/upgrade7.png
[image2]: media/service-fabric-application-upgrade-tutorial/upgrade1.png
[image3]: media/service-fabric-application-upgrade-tutorial/upgrade5.png
[image4]: media/service-fabric-application-upgrade-tutorial/upgrade6.png
