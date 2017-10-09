---
title: "Artificial utiliser Services mobiles, quel est l’application de Service ?"
description: "Découvrez quels sont les avantages du Service d’applications apporte tooyour les projets de Services mobiles existants."
services: app-service\mobile
documentationcenter: ios
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 26b68a11-8352-4f78-acd2-e4e0ec177781
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: na
ms.topic: get-started-article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 315cc6eedcdca6c3f9f9bb9fd5ec7baf655b7e20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started"></a>J'utilise Mobile Services. Comment App Service peut-il m'aider ?
## <a name="overview"></a>Vue d'ensemble
Votre service Mobile Service existant est sécurisé et restera pris en charge. Toutefois de hello d’avantages *Azure App Service* plateforme fournit pour votre application mobile qui ne sont pas disponibles aujourd'hui avec les Services mobiles :

* Offre plus simple, plus facile et plus économique pour les applications qui incluent à la fois des clients web et mobiles
* Nouvelles fonctionnalités d'hôte, y compris les tâches web, les enregistrements CName personnalisés et une meilleure analyse
* Intégration clé en main avec Traffic Manager
* Connectivité tooyour des ressources locales et des réseaux dans Ajout tooHybrid connexions VPN
* Surveillance, alertes et dépannage de votre application à l’aide de NewRelic ou d’AppInsights
* Plus riche éventail de ressources de calcul sous-jacent hello et la tarification
* Fonctionnalités intégrées de mise à l'échelle automatique, d'équilibrage de la charge et d'analyse des performances
* Fonctionnalités intégrées intermédiaires, de sauvegarde, de restauration et de test en production

## <a name="new-hosting-features"></a>Nouvelles fonctionnalités d'hébergement
Dans *Azure App Service* hello *l’application Mobile* principal code est exécuté dans hello même conteneur en tant qu’application Web et application API. Par conséquent, vous pouvez tirer parti de toutes les fonctionnalités de hello dans ce conteneur, y compris ceux qui ne sont pas présents dans les Services mobiles :

* Ajoutez une logique de backend qui s’exécute en permanence via les tâches web.
* Assurez-vous que votre code de backend est toujours en cours d’exécution.
* Utilisez personnalisé tooprovide CNAME convivial et stable noms tooyour points de terminaison de service principal mobile
* Dimensionnez géographiquement votre application avec Traffic Manager.
* Incluez les bibliothèques et les packages que vous souhaitez.
* (Pour .NET) Tirez parti des fonctionnalités d’ASP.NET, y compris MVC.
* (Pour Node.js) Tirer parti de n’importe quelle bibliothèque JavaScript pure de l’écosystème du nœud hello, notamment les bibliothèques MVC communes.

## <a name="access-on-premises-data-using-vnet"></a>Accédez aux données locales à l'aide de VNet
Avec Mobile Services vous pouvez déjà utiliser des connexions hybrides tooaccess ressources locales. Toutefois, dans certaines situations, une solution VPN est préférée. Avec *Azure App Service* , vous pouvez utiliser Azure VNet pour votre code de backend d'application mobile.

## <a name="use-your-favorite-backend-language"></a>Utilisez votre langage de backend favori
*Azure App Service* offres plus larges et plus riche prise en charge pour les plateformes ASP.NET et Node.js, y compris accéder toohello les runtimes plus récente.

## <a name="set-up-automatic-scale"></a>Configurez la mise à l'échelle automatique
Avec Mobile Services, toutes les instances de votre code de backend s'exécutaient sur de petites machines virtuelles. *Azure App Service* vous permet de taille de hello tooselect des machines virtuelles à partir d’un ensemble d’options beaucoup plus riche. Vous pouvez également adapter rapidement de façon horizontale toohandle ou toute charge de client entrantes, en fonction de diverses mesures de performances.

## <a name="be-in-hello-know"></a>Être Bonjour « savoir »
Réagir tooissues dans en temps réel avec des alertes et surveillance tooautomatically informe vous et votre équipe. Intégrer une application avancée analytique et les fonctionnalités d’analyse à partir de New Relic et AppInsights tooget encore plus riche idée de performances de votre application Mobile. Avec *Azure App Service* vous pouvez désormais configurer des alertes basées sur les diverses mesures de performance, par programmation et via hello portail Azure.

## <a name="keep-your-assets-safe"></a>Protégez vos actifs
Sauvegardez automatiquement votre backend et votre base de données. Votre code et les données est sécurisé à partir d’urgence et facilement restaurées, ce qui vous permet de toorun votre entreprise en toute confiance.

## <a name="ready-stage-go"></a>À vos marques, prêt, partez !
*Azure App Service* vous permet désormais de créer plusieurs environnements intermédiaires et de test privés pour vos applications mobiles. Utilisez les tooperform test avant de déployer. Remplacez tooproduction sans interruption. Les applications Web sont déjà chargées, garantissant la meilleure expérience aux utilisateurs hello.

Vous pouvez commencer à tirer parti d’ *App Service* pour votre application Mobile Service existante en suivant ce [didacticiel](app-service-mobile-migrating-from-mobile-services.md).
