---
title: aaaCreate une ressource Azure Application Insights | Documents Microsoft
description: "Configurez manuellement la surveillance d’Application Insights pour une nouvelle application en direct."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 878b007e-161c-4e36-8ab2-3d7047d8a92d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: bwren
ms.openlocfilehash: 3aba7045e1f8fe43d473f0be01dd52106ab992a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-application-insights-resource"></a>Création d’une ressource Application Insights dans Azure
Azure Application Insights affiche les données relatives à votre application dans une *ressource* Microsoft Azure. Création d’une ressource est par conséquent partie de [configurer Application Insights toomonitor une nouvelle application][start]. Dans de nombreux cas, la création d’une ressource peut faire automatiquement hello IDE. Mais dans certains cas, vous créez manuellement une ressource, par exemple, les builds toohave des ressources distinctes pour le développement et de production de votre application.

Une fois que vous avez créé la ressource de hello, vous obtenez sa clé d’instrumentation et utilisez ce Kit de développement logiciel de hello tooconfigure dans l’application hello. liens vers les ressources clés Hello hello ressource toohello de télémétrie.

## <a name="sign-up-toomicrosoft-azure"></a>S’inscrire tooMicrosoft Azure
Si vous n’avez pas de [compte Microsoft, procurez-vous en un dès maintenant](http://live.com). (Si elle utilise des services comme Outlook.com, OneDrive, Windows Phone ou XBox Live, elle dispose d’un compte Microsoft.)

Vous devez également un abonnement trop[Microsoft Azure](http://azure.com). Si votre équipe ou organisation dispose d’un abonnement Azure, hello propriétaire peut ajouter vous tooit, à l’aide de votre identifiant Windows Live ID. Vous êtes facturé uniquement pour ce que vous utilisez. plan de base par défaut Hello autorise une certaine quantité d’utilisation expérimentale gratuitement.

Lorsque vous avez accès tooa abonnement, connectez-vous à Insights tooApplication à [http://portal.azure.com](https://portal.azure.com)et utiliser votre toologin Live ID.

## <a name="create-an-application-insights-resource"></a>Création d’une ressource Application Insights dans Azure
Bonjour [portal.azure.com](https://portal.azure.com), ajouter une ressource Application Insights :

![Cliquez sur Nouveau > Application Insights](./media/app-insights-create-new-resource/01-new.png)

* **Type d’application** affecte ce que vous voyez sur le panneau de vue d’ensemble de hello et propriétés hello disponibles dans [explorer métrique][metrics]. Si vous ne voyez pas votre type d’application, choisissez Général.
* **Abonnement** est votre compte de paiement dans Azure.
* **Groupe de ressources** facilite la gestion des propriétés telles que le contrôle d’accès. Si vous avez déjà créé des autres ressources Windows Azure, vous pouvez choisir tooput cette nouvelle ressource Bonjour même groupe.
* **Emplacement** correspond à l’endroit où nous conservons vos données.
* **Code confidentiel toodashboard** place une vignette d’accès rapide pour vos ressources sur votre page d’accueil Azure. Recommandé.

Une fois votre application créée, un nouveau panneau s’ouvre. Dans ce panneau, vous trouverez des données relatives à l’utilisation et aux performances de votre application. 

tooit de retour tooget prochaine ouverture de session dans tooAzure, recherchez la vignette de démarrage rapide de votre application sur hello démarrer carte (écran d’accueil). Ou cliquez sur Parcourir toofind il.

## <a name="copy-hello-instrumentation-key"></a>Copiez la clé d’instrumentation hello
clé d’instrumentation Hello identifie la ressource hello que vous avez créé. Vous en avez besoin toogive toohello Kit de développement logiciel.

![Cliquez sur Essentials, hello clé d’Instrumentation, CTRL + C](./media/app-insights-create-new-resource/02-props.png)

## <a name="install-hello-sdk-in-your-app"></a>Installer hello SDK dans votre application
Installer hello Application Insights SDK dans votre application. Cette étape dépend fortement de type hello de votre application. 

Utilisez tooconfigure de clé hello instrumentation [hello du Kit de développement logiciel que vous installez dans votre application][start].

Hello SDK inclut des modules standards qui envoient des données de télémétrie sans que vous ayez toowrite n’importe quel code. actions de l’utilisateur tootrack ou diagnostiquer les problèmes plus en détail, [utilisent les API hello] [ api] toosend vos propres données de télémétrie.

## <a name="monitor"></a>Reportez-vous aux données de télémétrie
Fermer hello rapide Démarrer Panneau des applications panneau tooreturn tooyour Bonjour portail Azure.

Cliquez sur hello recherche vignette toosee [recherche Diagnostic][diagnostic], où les événements de première hello apparaissent. 

Après quelques secondes, cliquez sur **Actualiser** pour obtenir des données supplémentaires.

## <a name="creating-a-resource-automatically"></a>Création automatique d’une ressource
Vous pouvez écrire un [script PowerShell](app-insights-powershell.md) toocreate une ressource automatiquement.

## <a name="next-steps"></a>Étapes suivantes
* [Création d’un tableau de bord](app-insights-dashboards.md)
* [Recherche de diagnostic](app-insights-diagnostic-search.md)
* [Exploration des mesures](app-insights-metrics-explorer.md)
* [Écriture de requêtes Analytics](app-insights-analytics.md)

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[diagnostic]: app-insights-diagnostic-search.md
[metrics]: app-insights-metrics-explorer.md
[start]: app-insights-overview.md

