---
title: aaaMicrosoft Dynamics CRM et Azure Application Insights | Documents Microsoft
description: "Obtenez des données de télémétrie à partir de Microsoft Dynamics CRM Online à l’aide d’Application Insights. Procédure pas à pas de configuration, obtention de données, visualisation et exportation."
services: application-insights
documentationcenter: 
author: mazharmicrosoft
manager: carmonm
ms.assetid: 04c66338-687e-49e5-9975-be935f98f156
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/16/2017
ms.author: bwren
ms.openlocfilehash: a39398060d6553fb18a26c101f085b7d87443636
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="walkthrough-enabling-telemetry-for-microsoft-dynamics-crm-online-using-application-insights"></a>Procédure pas à pas : activation de télémétrie pour Microsoft Dynamics CRM Online à l’aide d’Application Insights
Cet article vous montre comment les données de télémétrie tooget de [Microsoft Dynamics CRM Online](https://www.dynamics.com/) à l’aide de [Azure Application Insights](https://azure.microsoft.com/services/application-insights/). Nous examinerons hello ensemble du processus de l’ajout d’Application Insights script tooyour application, la capture des données et visualisation des données.

> [!NOTE]
> [Parcourir l’exemple de solution hello](https://dynamicsandappinsights.codeplex.com/).
> 
> 

## <a name="add-application-insights-toonew-or-existing-crm-online-instance"></a>Ajouter Application Insights toonew ou l’instance existante de CRM Online
toomonitor votre application, vous ajoutez une application de tooyour Application Insights SDK. Hello SDK envoie télémétrie toohello [portail Application Insights](https://portal.azure.com), où vous pouvez utiliser nos puissantes analyses et les outils de diagnostic, ou exporter hello données toostorage.

### <a name="create-an-application-insights-resource-in-azure"></a>Créer une ressource Application Insights dans Azure
1. Obtenez un [compte dans Microsoft Azure](http://azure.com/pricing). 
2. L’authentification à hello [portail Azure](https://portal.azure.com) et ajouter une nouvelle ressource Application Insights. C’est là où vos données seront traitées et affichées.
   
    ![Cliquez sur +, Services de développement, Application Insights.](./media/app-insights-sample-mscrm/01.png)
   
    Choisissez ASP.NET en tant que type de l’application hello.
3. Ouvrez la page de prise en main de hello « analyse et de diagnostiquer côté client ».
   
    ![Extrait de code pour l’insertion dans votre page web](./media/app-insights-sample-mscrm/03.png)

**Maintenir la page de codes hello** pendant que vous hello étape suivante dans une autre fenêtre de navigateur. Vous devez les code hello bientôt. 

### <a name="create-a-javascript-web-resource-in-microsoft-dynamics-crm"></a>Créer une ressource web JavaScript dans Microsoft Dynamics CRM
1. Ouvrez votre instance de CRM Online et connectez-vous avec des privilèges d’administrateur.
2. Ouvrez Microsoft Dynamics CRM paramètres, des personnalisations, personnaliser hello système
   
    ![Paramètres Microsoft Dynamics CRM](./media/app-insights-sample-mscrm/04.png)
   
    ![Paramètres > Personnalisations](./media/app-insights-sample-mscrm/05.png)

    ![Personnaliser l’option de système de hello](./media/app-insights-sample-mscrm/06.png)

1. Créez une ressource JavaScript.
   
    ![Nouvelle boîte de dialogue ressource web](./media/app-insights-sample-mscrm/07.png)
   
    Donnez-lui un nom, sélectionnez **Script (JScript)** et éditeur de texte hello ouvert.
   
    ![Éditeur de texte hello ouvert](./media/app-insights-sample-mscrm/08.png)
2. Copiez le code de hello d’Application Insights. Lors de la copie que les balises de script que tooignore. Reportez-vous à la capture d’écran ci-dessous :
   
    ![Définissez votre clé d’instrumentation](./media/app-insights-sample-mscrm/09.png)
   
    code de Hello inclut la clé d’instrumentation hello qui identifie votre ressource Application insights.
3. Enregistrez et publiez.
   
    ![Enregistrez et publiez](./media/app-insights-sample-mscrm/10.png)

### <a name="instrument-forms"></a>Instrumenter les formulaires
1. Dans Microsoft CRM Online, ouvrez le formulaire de compte hello
   
    ![Formulaire de compte](./media/app-insights-sample-mscrm/11.png)
2. Ouvrez l’écran hello propriétés
   
    ![Propriétés de formulaire](./media/app-insights-sample-mscrm/12.png)
3. Ajouter hello ressource web JavaScript que vous avez créé
   
    ![Ajoutez un menu](./media/app-insights-sample-mscrm/13.png)
   
    ![Ajouter une ressource web de hello](./media/app-insights-sample-mscrm/14.png)
4. Enregistrez et publiez vos personnalisations de formulaire.

## <a name="metrics-captured"></a>Mesures capturées
Vous avez maintenant configuré la capture de données de télémétrie pour écran de hello. Chaque fois qu’il est utilisé, les données sont envoyées ressource d’Application Insights tooyour.

Voici les exemples de données hello qui s’affiche.

#### <a name="application-health"></a>Intégrité d’application
![Exemple de temps de chargement de la page](./media/app-insights-sample-mscrm/15.png)

![Exemple de graphique des affichages de pages](./media/app-insights-sample-mscrm/16.png)

Exceptions du navigateur :

![Graphique des exceptions du navigateur](./media/app-insights-sample-mscrm/17.png)

Cliquez sur hello graphique tooget plus en détail :

![Liste des exceptions](./media/app-insights-sample-mscrm/18.png)

#### <a name="usage"></a>Usage
![Utilisateurs, sessions et affichages de page](./media/app-insights-sample-mscrm/19.png)

![Graphiques de session](./media/app-insights-sample-mscrm/20.png)

![Versions de navigateur](./media/app-insights-sample-mscrm/21.png)

#### <a name="browsers"></a>Navigateurs
![Répartition du temps de chargement de la page](./media/app-insights-sample-mscrm/22.png)

![Nombre de sessions par version de navigateur](./media/app-insights-sample-mscrm/23.png)

#### <a name="geolocation"></a>Géolocalisation
![Nombre de sessions par pays](./media/app-insights-sample-mscrm/24.png)

![Sessions et utilisateurs par pays](./media/app-insights-sample-mscrm/25.png)

#### <a name="inside-page-view-request"></a>Demande d’affichage de page
![Résumé d’affichage de la page](./media/app-insights-sample-mscrm/26.png)

![Recherche sur les événements d’affichage de page](./media/app-insights-sample-mscrm/27.png)

![Affichages de page similaires](./media/app-insights-sample-mscrm/28.png)

![Propriétés d'affichage de la page](./media/app-insights-sample-mscrm/29.png)

![Pages par session](./media/app-insights-sample-mscrm/30.png)

## <a name="sample-code"></a>Exemple de code
[Parcourir le code d’exemple hello](https://dynamicsandappinsights.codeplex.com/).

## <a name="power-bi"></a>Power BI
Vous pouvez faire de même effectuer une analyse si vous [exporter les données de hello tooMicrosoft Power BI](app-insights-export-power-bi.md).

## <a name="sample-microsoft-dynamics-crm-solution"></a>Exemple de solution Microsoft Dynamics CRM
[Voici les solutions d’exemple hello implémentée dans Microsoft Dynamics CRM](https://dynamicsandappinsights.codeplex.com/).

## <a name="learn-more"></a>En savoir plus
* [Présentation d’Application Insights](app-insights-overview.md)
* [Application Insights pour les pages web](app-insights-javascript.md)
* [Plus d'exemples et de procédures pas à pas](app-insights-code-samples.md)
