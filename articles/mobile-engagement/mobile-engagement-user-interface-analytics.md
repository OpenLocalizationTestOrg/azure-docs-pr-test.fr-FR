---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - Analytique"
description: "Découvrez comment tooanalyze les données historiques relatives à votre application à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 6b2533ac-b8ec-4e35-872c-d563895bdc0c
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4a9df11226fed6710cfb1337ae84ece7596d482f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooanalyze-historical-data-about-your-application"></a>Comment tooanalyze les données historiques relatives à votre application
Cet article décrit hello **ANALYTICS** onglet Hello **Mobile Engagement** portal. Vous utilisez hello **Mobile Engagement** toomonitor portail et gérer vos applications mobiles. Notez que toostart à l’aide du portail hello vous devez tout d’abord toocreate un **Azure Mobile Engagement** compte.

Hello section Analytique de hello l’interface utilisateur fournit des informations agrégées sur votre application basée sur des données historiques mis à jour toutes les 24 heures. informations de Hello s’affichent sur les différents tableaux de bord composé de cartes, grilles et les graphiques de barres/ligne/secteur. les données de salutation peuvent aussi être téléchargées en tant que fichiers .csv. La plupart de ces informations est disponible en temps réel en hello section Moniteur de hello l’interface utilisateur, et il est également accessibles à partir de hello Analytique API.

> [!NOTE]
> De nombreuses sections de hello **Mobile Engagement** interface utilisateur du portail contient hello **afficher l’aide** bouton. Appuyez sur ce bouton tooget informations contextuelles supplémentaires sur une section.

## <a name="standard-and-custom-analytics"></a>Analyses standard et personnalisées :
Azure Mobile Engagement fournit un ensemble de basique, standards des informations analytiques sur vos applications qui peuvent représentés graphiquement dès que vous intégrez votre application à hello SDK. Azure Mobile Engagement fournit également des hello capacité toogather analytique personnalisés supplémentaires informations que vous voulez sur le comportement de vos utilisateurs finals. Pour ce faire, créez un plan de balises des « Tags (app info) » personnalisées, réalisées à partir des **Paramètres** de manière à ce qu'Azure Mobile Engagement puisse collecter ces données supplémentaires pour vous.

## <a name="analytics"></a>Analyse
* Tableau de bord : affiche des informations générales sur vos utilisateurs nouveaux et actifs et leurs tendances.
* Utilisateurs : les utilisateurs sont identifiés par l'identifiant de leur appareil. Cet identifiant est unique pour chaque appareil (un nouvel utilisateur représente en réalité un nouvel appareil). Un utilisateur est considéré comme nouveau sur une période donnée s'il a effectué sa première session durant cette période. Un utilisateur est considéré comme retenu s’il a ouvert au moins une session pendant hello ces 7 derniers jours. Les utilisateurs actifs sont ceux qui ont effectué au moins une session durant une période donnée. Vous pouvez les trier par mois, par semaine, par jour ou par heure. Tous les graphiques hello ressemblent mais vous toofilter par différentes fonctionnalités, telles que la version de hello de votre application, puis toosort par une période de temps. Hello standards informations collectées en intégrant hello SDK comprennent hello : les utilisateurs actifs, nouvel utilisateur, le nombre de sessions, la longueur de chaque session, les informations techniques dans les pays hello variables locales, emplacement, langue, appareils, opérateur microprogramme, réseau (Wi-Fi), les versions de l’application hello et Kit de développement logiciel, utilisé par les clients. Ces informations peuvent être affichées en temps réel à partir de la section de moniteur hello.

> [!NOTE]
> Hello laps de temps est basée sur date hello à partir des paramètres de périphérique hello utilisateurs, pour un utilisateur dont le téléphone a date de hello mal définie pourrait s’afficher dans hello incorrect laps de temps.

* Rétention : un utilisateur est considéré comme retenu sur une période donnée s'il a effectué sa première session durant cette période. Vous pouvez modifier les intervalles de temps hello pendant lesquels les utilisateurs retenus (et les nouveaux utilisateurs) sont comptabilisés toohours, jours, semaines ou mois. analytique de rétention utilisateur Hello s’appuie sur les cohortes. Une cohorte est ensemble hello de tous les utilisateurs de nouveau hello détecté pendant une période donnée (par exemple, l’ensemble hello d’utilisateurs effectuant leur première session durant ce laps de temps). Nous utilisons des cohortes d'un jour, de deux jours, de quatre jours, de sept jours et d'un mois. Un ensemble cohorte, chaque jour 1, 2 jours, 4 jours, 7 jours ou 1 mois, Azure Mobile Engagement calcule hello de tous les utilisateurs qui appartiennent toohello cohorte et sont toujours actif (par exemple, l’ensemble hello d’utilisateurs qui ont effectué au moins une session pendant la période de hello). Cet ensemble d'utilisateurs est appelé une version de cohorte. (Azure Mobile Engagement peut vous indiquer le nombre de vos utilisateurs est toujours à l’aide de votre application, mais seul magasin spécifique de la plate-forme hello peut vous indiquer le nombre de vos utilisateurs désinstallé votre iTunes app - par exemple, GooglePlay, Windows Store, etc..).
* Sessions : Une utilisation de l’application hello par un utilisateur. Les sessions sont générées à partir de la séquence de hello d’activités effectuées par les utilisateurs (une activité est l’utilisation de toohello généralement associé d’un écran de l’application hello, mais cela peut varier en fonction de hello de façon hello SDK a été intégré dans l’application hello). Un utilisateur peut effectuer uniquement une activité à la fois : une session démarre dès que l’utilisateur de hello démarre sa première activité et s’arrête lorsqu’il termine sa dernière activité. Lorsqu'un utilisateur n'effectue aucune activité durant quelques secondes, sa séquence d'activités est divisée en deux sessions distinctes.
* Activités : les noms de chaque écran dans votre application hello et longueur hello de temps que les utilisateurs passent sur chaque écran. Les activités sont une option analytique personnalisée qui correspondre toohello les balises « info application » que vous avez configuré pour votre propre application :
* Chemin d’accès de l’utilisateur : vous indique comment vos utilisateurs naviguent à travers les différentes activités de votre application (écrans). Vous pouvez déplacer le niveau de hello hello curseur tooadjust de détails. Les nœuds bleus représentent les activités de votre application. Leur taille est proportionnelle toohello temps que les utilisateurs. Les nœuds blancs représentent le début et la fin de la session. Les nœuds rouges représentent les incidents. Les liens représentent les transitions existantes entre les différentes activités de votre application (ou entre les activités et les incidents). Cliquez sur un nœud ou un lien de toodisplay une info-bulle avec plus d’informations sur vos données : hello durée sur un écran en particulier, nombre de hello de transitions et le pourcentage de hello de transitions à partir de l’activité de destination hello toohello de l’activité source. (Un---60 %---> B signifie que les utilisateurs vont de l’activité A tombe en tooactivity B 60 % de temps de hello.) Vous pouvez réorganiser le graphique de hello que vous le souhaitez tooclarify ; sa position est enregistrée chaque fois que vous apportez une modification. Vous pouvez afficher ou masquer hello pannes toolighten hello graphique.
* Événements : Des actions spécifiques effectuées par un utilisateur dans l’application hello. distribution Hello d’événements est indiquée en tant que nombre hello d’événements par l’utilisateur et par session. Un événement représente une action instantanée, par exemple, un clic sur un bouton ou hello le réception d’une notification. (signification hello des événements dépend comment hello SDK a été intégré dans l’application hello.) Un événement peut survenir durant une session ou bien une tâche,ou peut être autonome.
* Travaux : Tooevents similaire à ceci près qu’ils se concentrent sur la longueur de l’action de hello hello. Par exemple, travaux peuvent indiquer des informations techniques sur la durée de tooload contenu ou un service d’appel de tooweb. Il peut également afficher la durée d’un toofill utilisateur d’un formulaire, créer un compte ou effectuer un achat. Une tâche représente la durée hello d’une tâche, exemple, durée hello d’une tâche de téléchargement ou d’hello temps une bannière est affichée sur l’écran hello. (sens hello de travaux dépend comment hello SDK a été intégré dans l’application hello.) Travaux sont généralement associés à des tâches en arrière-plan qui sont effectuées en dehors de l’étendue de hello d’une session (c'est-à-dire sans activité utilisateur).
* Technicals : Des informations techniques sur les périphériques de hello d’utilisateurs hello de votre application, vous pouvez effectuer le suivi, tels que hello taille paramètres régionaux, transporteur, réseau, périphériques, microprogramme et écran des appareils des utilisateurs hello et hello Version de votre application et hello version du Kit de développement logiciel utilisée dans votre application.
* Erreurs : Informations sur les erreurs techniques au sein de l’application hello qui ne provoquent pas hello toocrash de l’application. Une erreur représente un problème instantané, par exemple, une défaillance réseau ou une mauvaise manipulation. (signification hello des événements dépend comment hello SDK a été intégré dans l’application hello.) Une erreur peut survenir durant une session ou bien une tâche, ou peut être autonome.
* Pannes : Plus d’informations sur les erreurs qui provoquent toocrash de votre application. Un incident est une condition inattendue où application hello cesse d’exécuter ses fonctions attendues et doit être arrêtée. Un incident est généralement en raison du bogue tooa dans l’application hello.

![Analyse 2][11]

## <a name="accessing-hello-retention-overview"></a>L’accès à la vue d’ensemble de la rétention de hello
![Analyse 3][12]

vue d’ensemble de la rétention Hello est divisée dans le milieu hello dans plusieurs cartes, chaque vue d’ensemble de hello montrant pendant une certaine période de rétention. période de rétention de 2 jours Hello est visible dans l’exemple de hello. Bonjour autres cartes afficher hello 4 jours et les périodes de rétention de 7 jours.

## <a name="understanding-hello-retention-overview-cards"></a>Présentation des cartes de vue d’ensemble de la rétention hello
![Analyse 4][13]

### <a name="each-card-is-composed-of-3-main-parts"></a>Chaque carte est composée de trois éléments principaux :
1. 1 : les cohortes hello et période de hello considérés comme
2. 2-4 : hello rétention pour hello période actuelle
3. 5 : un graphique Sparkline de l’historique de hello

### <a name="here-is-detailed-information-about-each-element"></a>Voici des informations détaillées sur chaque élément :
1. Cohorte et période : ce titre donne de type hello de cohorte. « Période de 2 jours » signifie que nous examinerons hello comportement des utilisateurs plus de 2 jours, les utilisateurs qui sont arrivés sur une période de 2 jours et si qu’ils se connectent Bonjour suivant des blocs de 2 jours. exemple Hello ci-dessus considère que l’activité hello d’utilisateurs entre hello 21 et 22 novembre.
2. Cela donne le taux de rétention hello sur hello 21 et 22 novembre pour les utilisateurs de hello arrivant 19 et 20 novembre. Ici nous avons eu 1 utilisateur active entre hello 21 et 22, sur hello 3 qui ont été nouveaux utilisateurs entre hello 19 et 20.
3. Cette offre d’indicateur visuel hello mêmes informations que ci-dessus représentées graphiquement. (hello troisième hello cercle est à partir du nombre de 33 % hello.) couleur de Hello donne des informations supplémentaires : vert indique que ce nombre augmente de calcul précédent de hello. La couleur jaune signifie qu'il est identique et la couleur rouge, qu'il est plus faible.
4. Cela indique les valeurs hello utilisés pour le calcul de hello.
5. Il s’agit d’un graphique Sparkline d’historique de hello des valeurs de rétention hello. Il vous permet des valeurs hello toosee dans hello au-delà de toohave une vue générale de la façon dont elle a évolué.

## <a name="see-also"></a>Voir aussi
* [Concepts][Link 6]
* [Service de guide de résolution des problèmes][Link 24]

<!--Image references-->
[1]: ./media/mobile-engagement-user-interface-navigation/navigation1.png
[2]: ./media/mobile-engagement-user-interface-home/home1.png
[3]: ./media/mobile-engagement-user-interface-home/home2.png
[4]: ./media/mobile-engagement-user-interface-home/home3.png
[5]: ./media/mobile-engagement-user-interface-home/home4.png
[6]: ./media/mobile-engagement-user-interface-home/home5.png
[7]: ./media/mobile-engagement-user-interface-my-account/myaccount1.png
[8]: ./media/mobile-engagement-user-interface-my-account/myaccount2.png
[9]: ./media/mobile-engagement-user-interface-my-account/myaccount3.png
[10]: ./media/mobile-engagement-user-interface-analytics/analytics1.png
[11]: ./media/mobile-engagement-user-interface-analytics/analytics2.png
[12]: ./media/mobile-engagement-user-interface-analytics/analytics3.png
[13]: ./media/mobile-engagement-user-interface-analytics/analytics4.png
[14]: ./media/mobile-engagement-user-interface-monitor/monitor1.png
[15]: ./media/mobile-engagement-user-interface-monitor/monitor2.png
[16]: ./media/mobile-engagement-user-interface-monitor/monitor3.png
[17]: ./media/mobile-engagement-user-interface-monitor/monitor4.png
[18]: ./media/mobile-engagement-user-interface-reach/reach1.png
[19]: ./media/mobile-engagement-user-interface-reach/reach2.png
[20]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign1.png
[21]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign2.png
[22]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign3.png
[23]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign4.png
[24]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign5.png
[25]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign6.png
[26]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign7.png
[27]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign8.png
[28]: ./media/mobile-engagement-user-interface-reach-campaign/Reach-Campaign9.png
[29]: ./media/mobile-engagement-user-interface-reach-criterion/Reach-Criterion1.png
[30]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content1.png
[31]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content2.png
[32]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content3.png
[33]: ./media/mobile-engagement-user-interface-reach-content/Reach-Content4.png
[34]: ./media/mobile-engagement-user-interface-dashboard/dashboard1.png
[35]: ./media/mobile-engagement-user-interface-segments/segments1.png
[36]: ./media/mobile-engagement-user-interface-segments/segments2.png
[37]: ./media/mobile-engagement-user-interface-segments/segments3.png
[38]: ./media/mobile-engagement-user-interface-segments/segments4.png
[39]: ./media/mobile-engagement-user-interface-segments/segments5.png
[40]: ./media/mobile-engagement-user-interface-segments/segments6.png
[41]: ./media/mobile-engagement-user-interface-segments/segments7.png
[42]: ./media/mobile-engagement-user-interface-segments/segments8.png
[43]: ./media/mobile-engagement-user-interface-segments/segments9.png
[44]: ./media/mobile-engagement-user-interface-segments/segments10.png
[45]: ./media/mobile-engagement-user-interface-segments/segments11.png
[46]: ./media/mobile-engagement-user-interface-settings/settings1.png
[47]: ./media/mobile-engagement-user-interface-settings/settings2.png
[48]: ./media/mobile-engagement-user-interface-settings/settings3.png
[49]: ./media/mobile-engagement-user-interface-settings/settings4.png
[50]: ./media/mobile-engagement-user-interface-settings/settings5.png
[51]: ./media/mobile-engagement-user-interface-settings/settings6.png
[52]: ./media/mobile-engagement-user-interface-settings/settings7.png
[53]: ./media/mobile-engagement-user-interface-settings/settings8.png
[54]: ./media/mobile-engagement-user-interface-settings/settings9.png
[55]: ./media/mobile-engagement-user-interface-settings/settings10.png
[56]: ./media/mobile-engagement-user-interface-settings/settings11.png
[57]: ./media/mobile-engagement-user-interface-settings/settings12.png
[58]: ./media/mobile-engagement-user-interface-settings/settings13.png

<!--Link references-->
[Link 1]: mobile-engagement-user-interface.md
[Link 2]: mobile-engagement-troubleshooting-guide.md
[Link 3]: mobile-engagement-how-tos.md
[Link 4]: http://go.microsoft.com/fwlink/?LinkID=525553
[Link 5]: http://go.microsoft.com/fwlink/?LinkID=525554
[Link 6]: http://go.microsoft.com/fwlink/?LinkId=525555
[Link 7]: https://account.windowsazure.com/PreviewFeatures
[Link 8]: https://social.msdn.microsoft.com/Forums/azure/home?forum=azuremobileengagement
[Link 9]: http://azure.microsoft.com/services/mobile-engagement/
[Link 10]: http://azure.microsoft.com/documentation/services/mobile-engagement/
[Link 11]: http://azure.microsoft.com/pricing/details/mobile-engagement/
[Link 12]: mobile-engagement-user-interface-navigation.md
[Link 13]: mobile-engagement-user-interface-home.md
[Link 14]: mobile-engagement-user-interface-my-account.md
[Link 15]: mobile-engagement-user-interface-analytics.md
[Link 16]: mobile-engagement-user-interface-monitor.md
[Link 17]: mobile-engagement-user-interface-reach.md
[Link 18]: mobile-engagement-user-interface-segments.md
[Link 19]: mobile-engagement-user-interface-dashboard.md
[Link 20]: mobile-engagement-user-interface-settings.md
[Link 21]: mobile-engagement-troubleshooting-guide-analytics.md
[Link 22]: mobile-engagement-troubleshooting-guide-apis.md
[Link 23]: mobile-engagement-troubleshooting-guide-push-reach.md
[Link 24]: mobile-engagement-troubleshooting-guide-service.md
[Link 25]: mobile-engagement-troubleshooting-guide-sdk.md
[Link 26]: mobile-engagement-troubleshooting-guide-sr-info.md
[Link 27]: ../mobile-engagement-how-tos-first-push.md
[Link 28]: ../mobile-engagement-how-tos-test-campaign.md
[Link 29]: ../mobile-engagement-how-tos-personalize-push.md
[Link 30]: ../mobile-engagement-how-tos-differentiate-push.md
[Link 31]: ../mobile-engagement-how-tos-schedule-campaign.md
[Link 32]: ../mobile-engagement-how-tos-text-view.md
[Link 33]: ../mobile-engagement-how-tos-web-view.md
