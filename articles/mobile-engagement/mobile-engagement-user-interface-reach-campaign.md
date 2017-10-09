---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - atteindre la campagne"
description: "Laern comment toocreate et gérer des campagnes de notification push à l’aide d’Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 2fe124a2-a86f-4136-81ba-a9d298ec798a
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 825e550ace63a34d1a90b10fa976a61eb15a6d04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-and-manage-push-notification-campaigns"></a>Comment toocreate et gérer des campagnes de notification push
Vous pouvez utiliser hello section portée de l’interface utilisateur de hello toocreate une nouvelle campagne de Push avec une formule complexe en fournissant toutes les informations de hello vous devez toosend une notification push. Hello options d’une campagne de Push varient légèrement en fonction des types de campagne hello quatre : annonces, sondages, exécute un push de données et des vignettes (Windows Phone uniquement).

### <a name="option-applies-to"></a>L'option s'applique à :
* Langues : toutes (Annonces, Sondages, Push de données et Vignettes)
* Campagne : toutes (Annonces, Sondages, Push de données et Vignettes)
* Notification : Annonces et Sondages
* Contenu : unique pour chaque type de campagne
* Audience : toutes (Annonces, Sondages, Push de données et Vignettes)
* Délai d’exécution : Annonces, Sondages et Vignettes
* Test : toutes (Annonces, Sondages, Push de données et Vignettes)

![Reach-Campaign1][20]

## <a name="languages"></a>Langues
Vous pouvez utiliser hello déroulante langues menu toosend une version différente de votre toodevices par émission de données qui sont définies toouse différentes langues. Par défaut, tous les appareils recevront hello même Push quelle que soit la langue qu’ils sont toouse. Utilisateurs avec leur appareils ensemble tooa autre langue reçoivent une version de langue par défaut hello Hello par émission de données. La plupart des options de campagne push hello permettent toospecify un contenu de remplacement pour chacune des langues supplémentaires hello que vous sélectionnez. 

![Reach-Campaign2][21]

### <a name="language-differences-apply-to"></a>Les différences linguistiques s'appliquent à :
* Langues : Langues Unique peuvent être sélectionnés dans la langue par défaut de toohello Ajout
* Campagne : identique pour toutes les langues
* Notification : Uniques pour chaque langue en outre toohello langue par défaut
* Contenu : Uniques pour chaque langue en outre toohello langue par défaut
* Audience : peut être filtrée par un critère de langue distinct
* Délai d’exécution : identique pour toutes les langues
* Test : Tooeach langue à la fois peuvent être envoyés

### <a name="supported-languages"></a>Langues prises en charge :
* Arabe (ar) 
* Bulgare (bg) 
* Catalan (ca) 
* Chinois (zh) 
* Croate (hr) 
* Tchèque (cs) 
* Danois (da) 
* Néerlandais (nl) 
* Anglais (en) 
* Finnois (fi) 
* Français (fr) 
* Allemand (de) 
* Grec (el) 
* Hébreu (he) 
* Hindi (hi) 
* Hongrois (hu) 
* Indonésien (id) 
* Italien (it) 
* Japonais (ja) 
* Coréen (ko) 
* Letton (lv) 
* Lituanien (lt) 
* Malais (macro-langue) (ms) 
* Norvégien Bokmål (nb) 
* Polonais (pl) 
* Portugais (pt) 
* Roumain (ro) 
* Russe (ru) 
* Serbe (sr) 
* Slovaque (sk) 
* Slovène (sl) 
* Espagnol (es) 
* Suédois (sv) 
* Tagalog (tl) 
* Thaï (th) 
* Turc (tr) 
* Ukrainien (uk) 
* Vietnamien (vi) 

## <a name="campaign"></a>Campagne
Vous pouvez utiliser hello campagne section tooset hello nom et la catégorie de votre campagne ainsi que si vous envisagez de section d’audience hello tooignore d’une campagne de Push et que vous envoyez à la place de cette campagne via hello API couverture (et certains éléments de niveau de faible hello API de Push). Catégories peuvent être utilisées avec une notification personnalisée modèle toocontrol dans l’application des notifications en fonction des paramètres prédéfinis. Vous pouvez obtenir une liste de vos « catégories » via l’API couverture de hello.

> [!WARNING]
> Si vous utilisez option de « Ignorer Audience, push seront envoyés toousers via hello API » hello de section de « De la campagne » hello d’une couverture campagne, campagne de hello n’envoie pas automatiquement, vous devez toosend manuellement via l’API couverture de hello.

![Reach-Campaign3][22]

### <a name="option-applies-to"></a>L'option s'applique à :
* Nom : toutes
* Catégorie : Annonces et Sondages
* Ignorer l’Audience push seront envoyés toousers via hello API : tous les

## <a name="notification"></a>Notification
Vous pouvez utiliser les paramètres de base hello Notification section tooset pour votre commande, notamment : hello titre Hello Push, le message de type hello, une image dans l’application, ou si elle est révocables. De nombreux paramètres de notification sont toohello spécifique à la plateforme de votre appareil. Vous pouvez choisir d'envoyer votre notification Push depuis l'application ou en dehors de l'application, ou les deux. (N’oubliez pas que les utilisateurs peuvent « opt-in » ou « annuler » de « hors de l’application » transmet au système d’exploitation de hello niveau sur leurs appareils, Azure Mobile Engagement à ne pas être en mesure de toooverride ce paramètre. Également n’oubliez pas que gère les API de portée hello « dans l’application » exécute un push de « hors de l’application ». Hello API de Push peut être utilisé toohandle « du délai d’attente d’application » exécute un push de trop.) Push peut être personnalisée avec des images ou du contenu HTML, y compris des liens ciblés pour la liaison en dehors de votre application ou tooanother l’emplacement dans votre application (Kit de développement logiciel Android 2.1.0 ou ultérieure catégories intentionnels requis). Vous pouvez modifier le badge d’icône ou iOS hello et envoyer le contenu de texte ou web (un popup avec html, URL lien tooanother emplacement du contenu à l’intérieur ou en dehors de l’application hello). Vous pouvez également faire sonner des appareils Android ou faire vibrer avec hello par émission de données. (N’oubliez pas que vous serez peut-être hello correcte des autorisations dans votre Android SDK tooring du fichier de manifeste ou faire vibrer un appareil). Il n'y a actuellement aucune norme industrielle pour les tailles « Grand format » puisque la taille des écrans est différente pour chaque appareil. Toutefois, les images 400 x 100 fonctionnent sur presque toutes les tailles d'écran.

### <a name="delivery-types"></a>Types d'envoi :
* Hors de l’application uniquement : hello notification arrive lorsque l’utilisateur de hello n’utilise pas l’application hello.
* Hello hors de notification uniquement de l’application requiert un certificat à partir d’Apple ou Google (certificat APN ou GCM).
* Dans l’application uniquement : notification de hello s’affiche uniquement lorsque l’application hello s’exécute.
* notification de Hello utilise hello Capptain remise système tooreach hello utilisateur. Vous pouvez entièrement personnaliser hello disposition/affichage visuel de votre publication.
* À tout moment : Cette option permet de s’assurer que vous envoyez une notification de que l’application hello est en cours d’exécution ou non.

![Reach-Campaign4][23]

### <a name="option-applies-to"></a>L'option s'applique à :
* Notification : Annonces et Sondages

## <a name="content"></a>Contenu
Vous pouvez utiliser le contenu de hello toomodify hello section de contenu des annonces, sondages, exécute un push de données et des vignettes (Windows Phone uniquement). le paramètre de contenu Hello de campagnes Push est type toohello spécifique de campagne. 

### <a name="see-also"></a>Voir aussi
* [Documentation de l’interface utilisateur - Reach - Contenu Push][Link 29]

![Reach-Campaign5][24]

## <a name="audience"></a>Public ciblé
Vous pouvez utiliser hello Audience section toodefine une liste standard des éléments toolimit votre campagne ou les limites de votre campagne en fonction de critères personnalisés. Hello standard d’options tooLimit votre Audience vous permet d’utilisateurs de nouveau ou ancien de tooeither toopush ou push natif uniquement. Vous pouvez également définir un nombre de hello toolimit quota des utilisateurs qui reçoivent les push hello. Vous pouvez modifier manuellement l’expression hello pour comment votre campagne est filtré tooinclude un ou plusieurs utilisateurs tootarget de critère. Vous pouvez taper manuellement une expression d'audience. Une telle expression doit définir explicitement la relation hello entre les critères. Un critère est décrit par un identificateur qui doit commencer par une majuscule et ne peut pas contenir d'espace. relation Hello entre les critères de hello peut être décrite à l’aide de 'and', 'or', 'not' opérateurs ainsi que '(',')'. Exemple : « Critère1 ou (Critère1 sans Critère2) ».

> [!NOTE]
> Avec un grand public inclus dans les campagnes, SSI hello ciblage d’analyse peut être lent, surtout si vous essayez de toostart plusieurs campagnes à hello même temps.

* Si possible, ne démarrez qu'une campagne à la fois.
* À hello plus uniquement démarrer quatre campagnes à la fois.
* Transmettre uniquement les utilisateurs actifs tooyour (case à cocher « retenir uniquement les utilisateurs qui peuvent être atteints à l’aide de Push natif » et « Retenir uniquement les utilisateurs actifs ») afin que seuls vos utilisateurs ayant toujours application hello installée et l’utiliser doivent toobe analysé.
  Une fois que votre audience est défini, vous pouvez utiliser hello simuler toofind bouton out combien d’utilisateurs recevront cette opération Push. Il calcule le nombre hello d’utilisateurs connus potentiellement ciblé par cette audience (Ceci est une estimation basée sur un échantillon aléatoire d’utilisateurs). N’oubliez pas que les utilisateurs qui ont désinstallé l’application hello font également partie de cette audience, mais qu’il ne peut pas être atteint.

### <a name="see-also"></a>Voir aussi
* [Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]

![Reach-Campaign6][25]

### <a name="edit-expression"></a>Modifier l'expression
![Reach-Campaign7][26]

### <a name="limit-your-audience-option-applies-to"></a>L'option de limitation de votre audience s'applique à :
* Solliciter uniquement un sous-ensemble d’utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)
* Solliciter uniquement d’anciens utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)
* Solliciter uniquement de nouveaux utilisateurs : toutes (Annonces, Sondages, Push de données et Vignettes)
* Solliciter uniquement des utilisateurs inactifs : Annonces, Sondages et Vignettes
* Solliciter uniquement des utilisateurs actifs : toutes (Annonces, Sondages, Push de données et Vignettes)
* Solliciter uniquement des utilisateurs qui peuvent être contactés via un Push natif : Annonces et Sondages

## <a name="time-frame"></a>Délai d'exécution
Vous pouvez utiliser hello laps de temps section tooset lorsque hello push seront envoyés, ou vous pouvez laisser immédiatement campagne de hello toostart vide hello laps de temps. N’oubliez pas qu’à l’aide du fuseau horaire d’utilisateurs finaux hello peut démarrer hello campagne un jour plus tôt que prévu pour vos utilisateurs finaux en Asie et envoyer des lots de petite taille de push à la fois jusqu'à ce que tous les fuseaux horaires dans le laps de temps hello hello world correspondance définie pour votre campagne. À l’aide du fuseau horaire de hello utilisateurs peut également entraîner des retards dans les campagnes, car elle comprend le temps de hello toorequest à partir de téléphone de hello avant de push de hello.

> [!NOTE]
> Les campagnes qui n'ont pas de date de fin peuvent mettre en cache des notifications Push localement et continuer de les afficher une fois que vous avez terminé manuellement ces campagnes. tooavoid ce comportement, le spécifique à une heure de fin pour les campagnes.

### <a name="see-also"></a>Voir aussi
* [Reach - Procédures - Planification][Link 3] 

![Reach-Campaign8][27]

### <a name="settings-apply-to"></a>Les paramètres s'appliquent à :
* Délai d’exécution : Annonces, Sondages et Vignettes

## <a name="test"></a>Test
Vous pouvez utiliser hello Test section toosend cet appareil de test propre tooyour par émission de données avant d’enregistrer la campagne de hello. Si vous avez configuré des langues personnalisées pour cette campagne, vous pouvez tester hello push dans chaque langue. Vous pouvez configurer un appareil de test depuis « Mon compte ».

> [!NOTE]
> Exécute un push d’aucun côté serveur données sont enregistrées lorsque vous utilisez le bouton de hello trop « ne test », les données sont enregistrées uniquement pour les campagnes push réel.

### <a name="see-also"></a>Voir aussi
* [Documentation sur l’interface utilisateur - Mon compte][Link 14]

![Reach-Campaign9][28]

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
[Link 27]: mobile-engagement-user-interface-reach-campaign.md
[Link 28]: mobile-engagement-user-interface-reach-criterion.md
[Link 29]: mobile-engagement-user-interface-reach-content.md

