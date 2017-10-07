---
title: aaaUsing recherche dans Azure Application Insights | Documents Microsoft
description: "Recherchez et filtrez la télémétrie brute envoyée par votre application web."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 2a437555-8043-45ec-937a-225c9bf0066b
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: df2b0eb017ad48bcdc6ef57d8dff207d120143b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-search-in-application-insights"></a>Utilisation de la recherche dans Application Insights
La recherche est une fonctionnalité de [Application Insights](app-insights-overview.md) que vous utilisez toofind et Explorer des éléments de télémétrie individuels, tels que les vues de page, des exceptions ou requêtes web. Vous pouvez également afficher le suivi et les événements de journal que vous avez codés.

(Pour les requêtes plus complexes sur vos données, utilisez [Analytics](app-insights-analytics-tour.md).)

## <a name="where-do-you-see-search"></a>Où voyez-vous Recherche ?
### <a name="in-hello-azure-portal"></a>Bonjour portail Azure
Vous pouvez ouvrir la recherche de diagnostic explicitement à partir du Panneau de vue d’ensemble de Application Insights hello de votre application :

![Open diagnostic search](./media/app-insights-diagnostic-search/01-open-Diagnostic.png)

Il s’affiche également lorsque vous parcourez certains graphiques et éléments de la grille. Dans ce cas, les filtres sont prédéfinis toofocus sur le type hello de l’élément sélectionné. 

Par exemple, dans Panneau de vue d’ensemble de hello, est un graphique à barres des demandes classés par temps de réponse. Cliquez sur via un toosee de plage de performances une liste des requêtes individuelles dans cette plage de temps de réponse :

![Cliquer sur les performances des demandes](./media/app-insights-diagnostic-search/07-open-from-filters.png)

corps de Hello de Diagnostic de recherche est une liste d’éléments de télémétrie - demandes de serveur, de page vues, les événements personnalisés que vous avez codé et ainsi de suite. En haut de la liste de hello hello est un graphique de synthèse indiquant le nombre d’événements au fil du temps.

Cliquez sur Actualiser tooget nouveaux événements.

### <a name="in-visual-studio"></a>Dans Visual Studio

Dans Visual Studio, il existe également une fenêtre de recherche Application Insights. Il est très utile pour l’affichage des événements de télémétrie générés par l’application hello que vous déboguez. Mais il peut également afficher les événements hello collectés à partir de votre application publiée à hello portail Azure.

Ouvrez la fenêtre de recherche hello dans Visual Studio :

![Recherche Application Insights dans Visual Studio](./media/app-insights-diagnostic-search/32.png)

fenêtre de recherche Hello possède un portail web toohello similaire de fonctionnalités :

![Fenêtre de recherche Visual Studio Application Insights](./media/app-insights-diagnostic-search/34.png)

onglet d’opération de suivi Hello est disponible lorsque vous ouvrez une requête ou un affichage de page. Une « opération » est une séquence d’événements qui est associée à tooa une seule vue de demande ou de la page. Par exemple, les appels de dépendance, les exceptions, les journaux de suivi et les événements personnalisés peuvent faire partie d’une opération unique. onglet de l’opération de suivi Hello affiche hello graphiquement échéance et la durée de ces événements dans l’affichage de demande ou de la page de toohello de relation. 

## <a name="inspect-individual-items"></a>Inspecter les éléments un par un
Sélectionnez les champs clés toosee d’élément de données de télémétrie et les éléments associés. Si vous souhaitez toosee hello ensemble de champs, cliquez sur «... ». 

![Cliquez sur le nouvel élément de travail, modifier des champs de hello, puis cliquez sur OK.](./media/app-insights-diagnostic-search/10-detail.png)

## <a name="filter-event-types"></a>Filtrer les types d’événement
Ouvrez le panneau de filtre hello et sélectionner les types d’événements de hello vous souhaitez toosee. (Si, ultérieurement, vous souhaitez que les filtres de hello toorestore avec lequel vous avez ouvert le panneau de hello, cliquez sur Réinitialiser).

![Choisissez le filtre et sélectionnez les types de télémétrie](./media/app-insights-diagnostic-search/02-filter-req.png)

types d’événements Hello sont :

* **Suivi** - [Les journaux de diagnostic](app-insights-asp-net-trace-logs.md) comprennent les appels TrackTrace, log4Net, NLog et System.Diagnostic.Trace.
* **Demandes** : demandes HTTP reçues par votre serveur d’applications, dont les pages, les scripts, les images, les fichiers de style et les données. Ces événements sont utilisés toocreate hello demande et réponse vue d’ensemble des graphiques.
* **Affichage de page** - [télémétrie envoyé par le client web de hello](app-insights-javascript.md), utilisé toocreate page Afficher les rapports. 
* **Événement personnalisé** : Si vous avez inséré trop d’appels tooTrackEvent() dans l’ordre[surveiller l’utilisation de](app-insights-api-custom-events-metrics.md), vous pouvez les rechercher ici.
* **Exception** - non interceptée [exceptions dans le serveur de hello](app-insights-asp-net-exceptions.md)et celles que vous vous connectez à l’aide de TrackException().
* **Dépendance** - [appels à partir de votre application serveur](app-insights-asp-net-dependencies.md) tooother services tels que les API REST ou des bases de données et des appels AJAX à partir de votre [code client](app-insights-javascript.md).
* **Disponibilité** : résultats des [tests de disponibilité](app-insights-monitor-web-app-availability.md).

## <a name="filter-on-property-values"></a>Filtrer des valeurs de propriétés
Vous pouvez filtrer les événements sur les valeurs hello de leurs propriétés. les propriétés disponibles Hello dépendent des types d’événements hello que vous avez sélectionné. 

Par exemple, les demandes avec un code de réponse spécifique. 

![Développez une propriété et choisissez une valeur](./media/app-insights-diagnostic-search/03-response500.png)

Le choix d’aucune valeur d’une propriété particulière a hello même effet que le choix de toutes les valeurs. Cela désactive le filtrage sur cette propriété.

### <a name="narrow-your-search"></a>Affiner votre recherche
Notez que hello compte toohello à droite des valeurs de filtre de hello indiquer le nombre d’occurrences il dans ensemble filtré de hello en cours. 

Dans cet exemple, il est clair que demande ' Rpt/Employees' hello des résultats dans la plupart des erreurs de hello '500' :

![Développez une propriété et choisissez une valeur](./media/app-insights-diagnostic-search/04-failingReq.png)




## <a name="find-events-with-hello-same-property"></a>Rechercher des événements par hello même propriété
Rechercher tous les hello les éléments hello même valeur de propriété :

![Cliquez avec le bouton droit sur une propriété](./media/app-insights-diagnostic-search/12-samevalue.png)


## <a name="search-hello-data"></a>Rechercher les données hello

> [!NOTE]
> toowrite des requêtes plus complexes, ouvrez [ **Analytique** ](app-insights-analytics-tour.md) de haut hello du Panneau de recherche hello.
> 

Vous pouvez rechercher des termes du contrat d’une des valeurs de propriété hello. Cela est particulièrement utile si vous avez écrit des [événements personnalisés](app-insights-api-custom-events-metrics.md) avec des valeurs de propriété. 

Vous souhaiterez peut-être tooset une plage de temps que les recherches sur une plage plus courte sont plus rapides. 

![Open diagnostic search](./media/app-insights-diagnostic-search/appinsights-311search.png)

Recherchez des mots entiers, pas des sous-chaînes. Utilisez des guillemets tooenclose des caractères spéciaux.

| string | n’est *pas* trouvé par | mais ceux-ci la trouvent |
| --- | --- | --- |
| HomeController.About |home<br/>contrôleur<br/>out | homecontroller<br/>about<br/>« homecontroller.about »|
|États-Unis|Uni<br/>ted|états<br/>unis<br/>états ET unis<br/>« états-unis »

Vous pouvez utiliser des expressions de recherche hello sont :

| Exemple de requête | Résultat |
| --- | --- |
| `apple` |Rechercher tous les événements dans la plage de temps hello dont les champs incluent le mot hello « apple » |
| `apple AND banana` |Trouve les événements qui contiennent les deux mots. Utilisez « AND » en lettres majuscules (et non « and » en lettres minuscules). |
| `apple OR banana`<br/>`apple banana` |Trouve les événements qui contiennent un des deux mots. Utilisez « OR » en lettres capitales (et non « or » en lettres minuscules).<br/>Forme abrégée. |
| `apple NOT banana` |Rechercher des événements qui contiennent un mot, mais pas hello autres. |



## <a name="sampling"></a>échantillonnage
Si votre application génère un grand nombre de télémétrie (et que vous utilisez hello ASP.NET SDK version 2.0.0-beta3 ou version ultérieure), module d’échantillonnage adaptive hello réduit automatiquement le volume hello envoyé toohello portail en envoyant qu’une fraction représentative d’événements. Toutefois, les événements qui sont associée toohello même demande sont sélectionnées ou désélectionnées en tant que groupe, afin que vous pouvez naviguer entre les événements connexes. 

[En savoir plus sur l'échantillonnage](app-insights-sampling.md).



## <a name="create-work-item"></a>Création d’un élément de travail
Vous pouvez créer un bogue dans GitHub ou Visual Studio Team Services avec les détails de hello à partir de n’importe quel élément de données de télémétrie. 

![Cliquez sur le nouvel élément de travail, modifier des champs de hello, puis cliquez sur OK.](./media/app-insights-diagnostic-search/42.png)

Bonjour première fois que vous procédez ainsi, vous êtes invité à tooconfigure un tooyour lien Team Services compte et de projet.

![Remplir les URL hello de votre serveur Team Services et le nom du projet hello et cliquez sur Autoriser](./media/app-insights-diagnostic-search/41.png)

(Vous pouvez également configurer hello lien sur le panneau d’éléments de travail hello).

## <a name="save-your-search"></a>Enregistrer votre recherche
Lorsque vous avez défini tous les filtres hello que vous le souhaitez, vous pouvez enregistrer hello recherche en tant que favori. Si vous travaillez dans un compte de société, vous pouvez choisir si tooshare avec d’autres membres de l’équipe.

![Favori, hello nom du jeu, puis cliquez sur Enregistrer](./media/app-insights-diagnostic-search/08-favorite-save.png)

recherche de hello toosee, **Panneau de vue d’ensemble toohello accédez** et ouvrir Favoris :

![Vignette des favoris](./media/app-insights-diagnostic-search/09-favorite-get.png)

Si vous avez enregistré avec l’intervalle de temps relatif, panneau de rouvrir hello possède les données les plus récentes hello. Si vous avez enregistré avec l’intervalle de temps absolu, vous voyez hello mêmes données chaque fois. (Si 'Relative' n’est pas disponible lorsque vous souhaitez toosave favoris, cliquez sur la plage de temps dans l’en-tête de hello et définir une plage de temps qui n’est pas une plage personnalisée).

## <a name="send-more-telemetry-tooapplication-insights"></a>Envoyer la télémétrie plus tooApplication Insights
En outre toohello out of box données de télémétrie envoyée par l’Application Insights SDK, vous pouvez :

* Capturer le suivi du journal dans votre infrastructure de journalisation favorite dans [.NET](app-insights-asp-net-trace-logs.md) ou [Java](app-insights-java-trace-logs.md). Cela signifie que vous pouvez effectuer des recherches dans le suivi du journal et les mettre en corrélation avec les pages vues, les exceptions et autres événements. 
* [Écrire du code](app-insights-api-custom-events-metrics.md) toosend événements personnalisés, des vues de page et des exceptions. 

[Découvrez comment toosend se connecte et télémétrie personnalisée tooApplication Insights](app-insights-asp-net-trace-logs.md).

## <a name="questions"></a>Questions et réponses
### <a name="limits"></a>Quelle est la quantité de données conservée ?

Consultez hello [résumé des limites](app-insights-pricing.md#limits-summary).

### <a name="how-can-i-see-post-data-in-my-server-requests"></a>Comment puis-je consulter les données POST dans mes demandes serveur ?
Nous n’enregistre pas automatiquement les données de publication hello, mais vous pouvez utiliser [TrackTrace ou journal des appels](app-insights-asp-net-trace-logs.md). Placez les données de publication hello dans le paramètre de message hello. Vous ne pouvez pas filtrer sur le message de type hello Bonjour même façon, vous pouvez filtrer sur les propriétés, mais limite de taille hello est plus long.

## <a name="video"></a>Vidéo

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="add"></a>Étapes suivantes
* [Écrire des requêtes complexes dans Analytics](app-insights-analytics-tour.md)
* [Envoyer les journaux et les données de télémétrie personnalisées tooApplication Insights](app-insights-asp-net-trace-logs.md)
* [Configuration des tests de disponibilité et de réactivité](app-insights-monitor-web-app-availability.md)
* [Dépannage](app-insights-troubleshoot-faq.md)
