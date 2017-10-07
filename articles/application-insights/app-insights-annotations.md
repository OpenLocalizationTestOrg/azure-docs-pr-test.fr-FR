---
title: annotations aaaRelease pour Application Insights | Documents Microsoft
description: "Ajouter un déploiement ou générer des marqueurs graphiques de l’Explorateur de métriques tooyour dans Application Insights."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: 23173e33-d4f2-4528-a730-913a8fd5f02e
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: e802d22701cb69e96fd1a6b469ea67454195f77a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="annotations-on-metric-charts-in-application-insights"></a>Annotations sur les graphiques de métriques dans Application Insights
Des annotations sur les graphiques [Metrics Explorer](app-insights-metrics-explorer.md) montrent les endroits où vous avez déployé une nouvelle build ou tout autre événement majeur. Elles rendent facile toosee si vos modifications avaient aucun effet sur les performances de votre application. Ils peuvent être créés automatiquement par hello [système de génération Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/build/build-your-app-vs). Vous pouvez également créer annotations tooflag n’importe quel événement voulue en [leur création à partir de PowerShell](#create-annotations-from-powershell).

![Exemples d’annotations avec corrélation visible avec le délai de réponse de serveur](./media/app-insights-annotations/00.png)



## <a name="release-annotations-with-vsts-build"></a>Annotations de version avec Build VSTS

Les annotations de version sont une fonctionnalité de génération de nuage hello et version de service de Visual Studio Team Services. 

### <a name="install-hello-annotations-extension-one-time"></a>Installation de l’extension d’Annotations hello (une fois)
annotations de toobe toocreate en mesure de mise en production, vous devez tooinstall une Hello plusieurs extensions de Service d’équipe disponibles dans hello Visual Studio Marketplace.

1. Connectez-vous à tooyour [Visual Studio Team Services](https://www.visualstudio.com/en-us/get-started/setup/sign-up-for-visual-studio-online) projet.
2. Dans Visual Studio Marketplace, [obtenir hello version Annotations extension](https://marketplace.visualstudio.com/items/ms-appinsights.appinsightsreleaseannotations)et ajouter le compte de tooyour Team Services.

![En haut à droite de la page web de Team Services, ouvrez Marketplace. Sélectionnez Visual Team Services, puis, sous Build, choisissez Afficher plus.](./media/app-insights-annotations/10.png)

Vous ne devez toodo ce qu’une seule fois pour votre compte Visual Studio Team Services. Des annotations de version peuvent désormais être configurées pour n’importe quel projet de votre compte. 

### <a name="configure-release-annotations"></a>Configurer des annotations de version

Vous devez tooget une API distincte clé pour chaque modèle de version VSTS.

1. Connectez-vous à toohello [portail Microsoft Azure](https://portal.azure.com) et ouvrir la ressource Application Insights hello surveille votre application. (Ou [créez-en une maintenant](app-insights-overview.md)si vous ne l’avez pas encore fait.)
2. Ouvrez **Accès d’API**, **ID Application Insights**.
   
    ![Dans portal.azure.com, ouvrez votre ressource Application Insights, puis choisissez Paramètres. Ouvrir Accès API. Copiez hello ID d’Application](./media/app-insights-annotations/20.png)

4. Dans une fenêtre de navigateur distincte, ouvrez (ou créez) modèle de version hello qui gère vos déploiements à partir de Visual Studio Team Services. 
   
    Ajouter une tâche, puis sélectionnez les tâches d’Application Insights version Annotation hello à partir du menu de hello.
   
    Hello de coller **Id d’Application** que vous avez copié à partir de hello panneau d’accès de l’API.
   
    ![Dans Visual Studio Team Services, ouvrez Version, sélectionnez une définition de version, puis choisissez Modifier. Cliquez sur Ajouter une tâche, puis sélectionnez la tâche Annotation de version Application Insights. Collez hello ID Application Insights.](./media/app-insights-annotations/30.png)
4. Ensemble hello **APIKey** variable du champ de tooa `$(ApiKey)`.

5. Dans hello fenêtre Azure, créez une nouvelle clé d’API et création d’une copie de celle-ci.
   
    ![Bonjour panneau d’accès aux API Bonjour Azure fenêtre, cliquez sur Créer une clé API. Fournissez un commentaire, cochez Écrire des annotations, puis cliquez sur Générer une clé. Copie hello nouvelle clé.](./media/app-insights-annotations/40.png)

6. Ouvrez l’onglet de Configuration hello du modèle de mise en production hello.
   
    Créez une définition de variable pour `ApiKey`.
   
    Collez votre définition de la variable ApiKey de toohello clé API.
   
    ![Dans la fenêtre de hello Team Services, sélectionnez l’onglet de Configuration hello et cliquez sur Ajouter une Variable. Hello nom tooApiKey et dans la valeur de hello, coller clé hello que vient d’être générée, puis cliquez sur icône de verrou hello.](./media/app-insights-annotations/50.png)
7. Enfin, **enregistrer** hello de définition de la version.


## <a name="view-annotations"></a>Afficher les annotations
Maintenant, chaque fois que vous utilisez hello version modèle toodeploy une nouvelle version, une annotation sera envoyée tooApplication Insights. les annotations Hello seront affiche sur les graphiques dans Metrics Explorer.

Cliquez sur n’importe quel annotation marqueur tooopen plus d’informations sur version hello, y compris le demandeur, branche de contrôle de code source, la définition de mise en production, environnement et bien plus encore.

![Cliquez sur un marqueur d’annotation de version.](./media/app-insights-annotations/60.png)

## <a name="create-custom-annotations-from-powershell"></a>Créer des annotations personnalisées à partir de PowerShell
Vous pouvez également créer des annotations à partir du processus de votre choix (sans utiliser Visual Studio Team System). 


1. Effectuer une copie locale de hello [script Powershell à partir de GitHub](https://github.com/Microsoft/ApplicationInsights-Home/blob/master/API/CreateReleaseAnnotation.ps1).

2. Obtenir hello ID d’Application et créer une clé d’API à partir de hello panneau d’accès de l’API.

3. Appeler le script de hello comme suit :

```PS

     .\CreateReleaseAnnotation.ps1 `
      -applicationId "<applicationId>" `
      -apiKey "<apiKey>" `
      -releaseName "<myReleaseName>" `
      -releaseProperties @{
          "ReleaseDescription"="a description";
          "TriggerBy"="My Name" }
```

Il s’agit de script de hello toomodify facile, par exemple toocreate annotations pour hello passée.

## <a name="next-steps"></a>Étapes suivantes

* [Créer des éléments de travail](app-insights-diagnostic-search.md#create-work-item)
* [Automation avec PowerShell](app-insights-powershell.md)
