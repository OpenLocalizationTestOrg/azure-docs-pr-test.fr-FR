---
title: "aaaApplication télémétrie Insights dans Visual Studio CodeLens | Documents Microsoft"
description: "Accédez rapidement à vos données de télémétrie des requêtes et des exceptions Application Insights à l’aide de CodeLens dans Visual Studio."
services: application-insights
documentationcenter: .net
author: numberbycolors
manager: carmonm
ms.assetid: 93559e44-23cb-4b9d-8425-60f7f0d0a82c
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: bwren
ms.openlocfilehash: e812aa48f2a67eea860e7ecde341855763bb8a8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-telemetry-in-visual-studio-codelens"></a>Données de télémétrie Application Insights dans Visual Studio CodeLens
Méthodes de code hello de votre application web peuvent être annotés avec des données de télémétrie sur les exceptions d’exécution et temps de réponse de demande. Si vous installez [Azure Application Insights](app-insights-overview.md) dans votre application, les données de télémétrie hello s’affiche dans Visual Studio [CodeLens](https://msdn.microsoft.com/library/dn269218.aspx) -hello notes haut hello de chaque fonction dans laquelle vous êtes habitué tooseeing utile des informations telles que nombre hello de fonction hello de décimales sont référencées ou hello dernière personne qui a modifié.

![CodeLens](./media/app-insights-visual-studio-codelens/codelens-overview.png)

> [!NOTE]
> Application Insights dans CodeLens est disponible dans Visual Studio 2015 Update 3 et version ultérieure ou avec la version la plus récente de hello [extension des outils de développement Analytique](https://visualstudiogallery.msdn.microsoft.com/82367b81-3f97-4de1-bbf1-eaf52ddc635a). CodeLens est disponible dans hello éditions Enterprise et Professional de Visual Studio.
> 
> 

## <a name="where-toofind-application-insights-data"></a>Où toofind données d’Application Insights
Recherchez les données de télémétrie Application Insights dans les indicateurs CodeLens de hello des méthodes de demande publique hello de votre application web. Les indicateurs CodeLens sont affichés au-dessus des déclarations de méthode et des autres déclarations en C# et Visual Basic. Si des données Application Insights sont disponibles pour une méthode, des indicateurs s’affichent pour les requêtes et les exceptions, par exemple « 100 requêtes, 1 % en échec » ou « 10 exceptions ». Cliquez sur un indicateur CodeLens pour en savoir plus. 

> [!TIP]
> Demande d’application Insights et les indicateurs d’exception peuvent prendre quelques secondes supplémentaires tooload après les autres indicateurs CodeLens s’affichent.
> 
> 

## <a name="exceptions-in-codelens"></a>Exceptions dans CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-exceptions.png)

indicateur de CodeLens exception Hello montre le nombre hello d’exceptions qui se sont produites dans hello dernières 24 heures de hello 15 la plupart des exceptions qui se produisent souvent dans votre application pendant cette période, lors du traitement de demande de hello pris en charge par la méthode hello.

toosee plus d’informations, cliquez sur indicateur de CodeLens hello exceptions :

* changement de pourcentage de Hello dans le nombre d’exceptions à partir de hello dernières 24 heures relatif toohello préalable des dernières 24 heures
* Choisissez **accédez toocode** code de source toonavigate toohello pour la fonction hello lever exception de hello
* Choisissez **recherche** tooquery toutes les instances de cette exception qui se sont produites dans hello des dernières 24 heures
* Choisissez **tendance** tooview une visualisation de tendance pour les occurrences de cette exception Bonjour dernières 24 heures
* Choisissez **afficher toutes les exceptions dans cette application** tooquery toutes les exceptions qui se sont produites dans hello des dernières 24 heures
* Choisissez **Explorer les tendances d’exception** tooview une visualisation de tendance pour toutes les exceptions qui se sont produites dans hello dernières 24 heures. 

> [!TIP]
> Si vous voyez « 0 exceptions » dans CodeLens mais que vous savez il doit y avoir des exceptions, vérifiez toomake que les ressources Application Insights droite hello sont sélectionné dans CodeLens. tooselect une autre ressource, avec le bouton droit sur votre projet dans l’Explorateur de solutions de hello et choisissez **Application Insights > choisir la Source de données de télémétrie**. CodeLens apparaît uniquement pour hello 15 la plupart des exceptions qui se produisent souvent dans votre application hello dernières 24 heures, par conséquent, si une exception est hello 16 plus fréquemment ou moins, vous verrez « exceptions 0 ». Exceptions à partir des vues ASP.NET ne peuvent pas apparaître sur les méthodes de contrôleur hello qui les vues générées.
> 
> [!TIP]
> Si le message « ? des exceptions » dans CodeLens, vous devez tooassociate que votre compte Azure avec Visual Studio ou de vos informations d’identification de compte Azure a expiré. Dans ce cas, cliquez sur « ? des exceptions » et choisissez **ajouter un compte...**  tooenter vos informations d’identification.
> 
> 

## <a name="requests-in-codelens"></a>Requêtes dans CodeLens
![TBD](./media/app-insights-visual-studio-codelens/codelens-requests.png)

Hello demande indique CodeLens hello nombre HTTP des demandes qui été traitée par une méthode Bonjour au-delà de 24 heures, ainsi que de pourcentage hello de ces demandes ayant échoué.

Cliquez sur plus de détails, toosee hello demande CodeLens indicateur :

* Hello absolue et le pourcentage des modifications dans le nombre de demandes, les demandes ayant échoué et les temps de réponse sur hello au-delà de toohello 24 heures par rapport préalable des dernières 24 heures
* fiabilité Hello de méthode hello, calculée en tant que pourcentage de hello de demandes qui n’a pas échoué Bonjour dernières 24 heures
* Choisissez **recherche** pour des demandes ou tooquery des demandes ayant échoué tous hello demandes (échecs) qui s’est produite dans hello des dernières 24 heures
* Choisissez **tendance** tooview une visualisation de tendance pour les demandes, les demandes ayant échoué ou moyen de réponse arrive dans hello dernières 24 heures.
* Choisissez nom hello Hello ressource Application Insights dans hello coin supérieur gauche de hello CodeLens détails de l’affichage toochange quelle ressource est source de hello pour les données de CodeLens.

## <a name="next"></a>Étapes suivantes
|  |  |
| --- | --- |
| **[Utilisation d’Application Insights dans Visual Studio](app-insights-visual-studio.md)**<br/>Rechercher les données de télémétrie, voir les données dans CodeLens et configurer Application Insights. le tout dans Visual Studio. |![Droit hello projet, puis choisissez Application Insights, recherche](./media/app-insights-visual-studio-codelens/34.png) |
| **[Ajouter des données](app-insights-asp-net-more.md)**<br/>Analysez l’utilisation, la disponibilité, les dépendances et les exceptions. Intégrer des traces à partir des frameworks de journalisation. Écrire des données de télémétrie personnalisées. |![Visual Studio](./media/app-insights-visual-studio-codelens/64.png) |
| **[Utilisation de portail d’Application Insights hello](app-insights-dashboards.md)**<br/>Tableaux de bord, puissants outils de diagnostic et d’analyse, alertes, mappage direct des dépendances de votre application et exportation des données de télémétrie. |![Visual Studio](./media/app-insights-visual-studio-codelens/62.png) |

