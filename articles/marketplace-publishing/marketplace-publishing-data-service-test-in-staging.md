---
title: "aaaTesting votre Service de données de la plateforme pour hello Marketplace | Documents Microsoft"
description: "Comprendre comment tootest votre Service de données de la plateforme pour hello Azure Marketplace."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e861bd11-f74d-4d77-b4b5-23fb463644ad
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/26/2016
ms.author: hascipio; avikova
ms.openlocfilehash: 1b9c7027d8e0818b9bdee5cfca971bab25dd1959
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-your-data-service-offer-in-staging"></a>Tester votre offre de service de données dans l'emplacement intermédiaire
> [!IMPORTANT]
> **À ce stade, nous n’intégrons plus de nouveaux éditeurs de services de données. Le listing de nouveaux services de données ne sera pas approuvé.** Si vous avez une application SaaS vous aimeriez toopublish sur AppSource, vous trouverez plus d’informations [ici](https://appsource.microsoft.com/partners). Si vous avez des applications IaaS ou développeur de service vous serait comme toopublish sur Azure Marketplace, vous trouverez plus d’informations [ici](https://azure.microsoft.com/marketplace/programs/certified/).
> 
> 

Après avoir effectué les deux premières étapes de hello de [création de votre compte Microsoft Developer](marketplace-publishing-accounts-creation-registration.md) et [création de votre offre de Service de données dans le portail de publication](marketplace-publishing-data-service-creation.md) vous êtes prêt pour la disposition de votre offre Bonjour Azure Marketplace. Cette rubrique vous guident tout hello tout d’abord, intermédiaires, étape appelée « étape intermédiaire »

Désigne un déploiement de votre offre un « bac à sable » où vous pouvez tester et vérifier son fonctionnement avant d’en exécutant un push tooproduction privé de mise en lots. offre de Hello s’affiche dans la mise en lots comme il le ferait client tooa qui a déployé.

## <a name="step-1-pushing-your-offer-toostaging"></a>Étape 1. En exécutant un push de votre offre toostaging
En exécutant un push de votre toostaging offre vous permet d’offre de hello tootest avant de devenir disponible toofuture abonnés.  Vous pouvez voir comment votre offre apparaît et la fonction pour ceux qui s’abonnent tooyour données.  

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.1.png)

1. La connexion en hello [portail de publication](https://publish.windowsazure.com)
2. Sélectionnez **Data Services** dans la fenêtre de navigation gauche hello
3. Sélectionnez votre offre que vous souhaitez toopush toostaging. Vous verrez hello au-dessus d’écran.
4. Cliquez sur **Push tooStaging** bouton.  
5. Si des problèmes avec hello offre qui nécessaire toobe terminée préalable toopushing toostaging, vous verrez la liste affichée.  Corriger ces éléments en cliquant sur chaque élément de liste de hello. Lorsque toutes les corrections effectuées, cliquez sur **Push tooStaging** bouton Nouveau.

S’il n’y a aucun problème avec votre offre, vous verrez fenêtre hello ci-dessous.  

Si vous n’êtes pas planification/non approuvées toosurface votre offre dans le portail Azure (actuellement a une capacité limitée), puis la fenêtre contextuelle de hello simplement fermer.

tootest vos données de Service dans le portail Azure (dans le portail de DataMarket toohello ajout), vous aurez besoin d’un tootest ID d’abonnement Azure avec.  Cet ID d’abonnement identifiera compte hello qui sera autorisée tootest votre offre.  

Coupez et collez votre ID d’abonnement et cliquez sur hello coche toocontinue.

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.2.png)

> [!NOTE]
> Ces ID abonnements Azure est uniquement requises pour le test et de mise en lots Bonjour [portail de gestion Azure](https://manage.windowsazure.com). Ils ne sont pas requis tootest dans Azure Marketplace.
> 
> 

Hello écran suivant montre que la publication se déroule en affichant hello « en cours » icône mise en surbrillance jaune ci-dessous. En exécutant un push toostaging prend 10 minutes de too15.  Si l’opération prend plus de temps, actualisez d’abord votre navigateur (appuyez sur F5 dans Internet Explorer).  Bonjour rares cas où votre offre est toujours en exécutant un push toostaging après une heure, cliquez sur lien toolet nous savoir qu’il existe un problème de contact hello.

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-1.3.png)

Hello Push tooStaging issue hello « en cours » icône cesse de déplacement et l’état de hello sera mise à jour trop « intermédiaire ».  Vous est désormais prêt tootest votre offre.  

## <a name="step-2-test-your-staged-offer-in-datamarket"></a>Étape 2. Tester votre offre intermédiaire dans DataMarket
Cliquez sur le lien hello suivant texte hello **« consultez votre service proposer à... »** écran hello toodisplay hello abonné s’affiche lorsque votre offre est tooproduction et apparaîtra dans DataMarket.

  ![dessin](media/marketplace-publishing-data-service-test-in-staging/step-2.2.png)

Tester ou vérifiez chacun des éléments de 12 hello marqué ci-dessus tooensure tous les logos, prix/transactions, texte, images, documentation et les liens sont corrects et fonctionnent correctement.  Il s’agit d’un tooensure temps toutes les valeurs de test que vous avez entré lors de la création de votre offre ont été remplacés par des valeurs réelles.

1. Logo de l'offre
2. Nom de l’offre
3. Site Web de la société de tooyour/lien du nom du serveur de publication
4. Parcourir les catégories de votre offre
5. Abonnés tooassist du lien de prise en charge de votre offre
6. Description contextuelle de votre offre
7. Plan de l’offre précisant les détails de la facturation
8. Code de tooimplementation de lien
9. Exemples d'images illustrant l’utilisation des données de l'offre
10. Métadonnées d’entrée/sortie pour chaque service au sein de l’offre de hello
11. Conditions d'utilisation de l’offre
12. Aperçu des données de l’offre de hello

Enfin, recherchez le service de hello fonctionnera via hello Datamarket en cliquant sur le lien hello « Explorer ce jeu de données ».  Une nouvelle fenêtre s’ouvre dans l’outil de hello, nous appelons « Explorateur de Service » afin de vous pouvez afficher un aperçu des résultats hello d’une requête par rapport à votre service.  Dans cette fenêtre, vous pouvez entrer hello paramètres nécessitent et afficher les résultats de hello affichés à partir d’une requête sur votre service.   En outre, sont affichées hello URL pour votre requête.  

> [!NOTE]
> Être vraiment tooreview hello description textuelle du service hello affiché en haut de hello.  Et si votre offre se compose de plusieurs services appelant et cliquez sur les onglets de hello en hello bas tooswitch toohello suivant service tooreview de test.
> 
> 

## <a name="next-step"></a>Étape suivante
Si vous rencontrez des problèmes et avez besoin d'aide pour les résoudre, veuillez contacter l’ [assistance pour éditeurs Azure](http://go.microsoft.com/fwlink/?LinkId=272975).

Si vous êtes satisfait et prêt toopublish votre offre Lisez hello [tooProduction tooPush de demander une approbation](marketplace-publishing-push-to-production.md) documentation.

## <a name="see-also"></a>Voir aussi
* [Mise en route : Comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)

