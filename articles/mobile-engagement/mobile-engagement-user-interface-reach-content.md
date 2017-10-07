---
title: "aaaAzure l’Interface utilisateur Mobile Engagement - atteindre le contenu"
description: "Découvrez comment toomanage un contenu unique hello hello différents types de notifications push campagnes dans Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: add64f06-43c9-475c-8722-51cd00bb844b
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: de389eb4368d986ef00135036c26e26a2464663e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-hello-unique-content-of-hello-different-types-of-push-notification-campaigns"></a>Comment toomanage hello contenu unique de hello différents types de campagnes de notification push
Vous pouvez utiliser la section de contenu hello d’un nouveau couvertures campagne toomodify hello de contenu des annonces, sondages, exécute un push de données et des vignettes (Windows Phone uniquement). le paramètre de contenu Hello de campagnes Push est type toohello spécifique de campagne. 

### <a name="content-types"></a>Types de contenu :
* Annonces
* Sondages
* Push de données
* Vignettes (Windows Phone uniquement)

## <a name="content-of-announcements"></a>Contenu des annonces
 ![Reach-Content1][30] 

### <a name="choose-hello-type-of-your-announcement"></a>Choisissez le type hello de l’annonce :
* Notification uniquement : il s’agit d’une simple notification standard. Ce qui signifie que si un utilisateur clique dessus, aucun affichage supplémentaire ne s’affiche, mais seulement l’action hello associée tooit se produira.
* Annonce de texte : il est une notification qui engage hello utilisateur toohave examiner une vue de texte.
* Annonce de Web : il est une notification qui engage hello utilisateur toohave examiner un affichage web.

### <a name="see-also"></a>Voir aussi
* [Reach - Procédures - Annonces][Link 3] 

### <a name="about-web-view-announcements"></a>À propos des annonces d'affichage Web :
Occurrences de modèle hello « {deviceid} » dans le code de hello HTML ou le code JavaScript que vous fournissez ici seront automatiquement remplacées par identificateur hello du périphérique hello affichant l’annonce de type hello. Il s’agit d’un identificateurs d’appareil Azure Mobile Engagement tooretrieve facilement dans un externe de votre arrière-guichet de service web.
Si vous voulez toocreate un plein écran affichage web (sans hello Action et quitter boutons que nous fournissons) vous pouvez utiliser hello suivant des fonctions à partir du code JavaScript de l’annonce de votre vue de web : 

* effectuer l’action d’annonce hello : ReachContent.actionContent()
* sortie de l’annonce de type hello : ReachContent.exitContent()

### <a name="choose-your-action"></a>Choisissez votre action :
### <a name="about-action-urls"></a>À propos des URL d'action :
Toute URL qui peut être interprétée par le système d'exploitation d'un appareil cible peut être utilisée comme une URL d'action.
Toute URL dédiée par votre application peut prise en charge (par exemple, les utilisateurs toomake raccourcis tooa écran en particulier) peut également servir comme une URL d’action.
Chaque occurrence de hello {deviceid} pattern est automatiquement remplacé par identificateur hello du périphérique hello action de hello. Cela peut être des identificateurs d’appareil Azure Mobile Engagement tooeasily utilisé récupérer via un service web externe de votre arrière-guichet.

* **Actions Android et iOS**
  * Ouvrir une page Web
  * http://\[domaine-site-web\] 
  * Exemple : http://www.azure.com
  * Envoyer un courrier électronique
  * mailto:\[destinataire-e-mail\]?subject=\[objet\]&body=\[message\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!
  * Envoyer un SMS
  * sms:\[numéro-téléphone\] 
  * Exemple :sms:2125551212
  * Composer un numéro de téléphone
  * tel:\[numéro-téléphone\] 
  * Exemple :tel:2125551212
* **Actions Android uniquement**
  * Télécharger une application sur hello Play Store
  * market://details?id=\[package d’application\] 
  * Exemple :market://details?id=com.microsoft.office.word
  * Démarrer une recherche géolocalisée
  * geo:0,0?q=\[requête de recherche\] 
  * Exemple :geo:0,0?q=starbucks,paris
* **Actions iOS uniquement**
  * Télécharger une application sur hello App Store
  * http://itunes.apple.com/[pays]/app/[nom de l’application]/id[ID de l’application]?mt=8 
  * Exemple: http://itunes.apple.com/fr/app/briquet-virtuel/id430154748?mt=8
  * Actions Windows
  * Ouvrir une page Web
  * http://\[domaine-site-web\] 
  * Exemple : http://www.azure.com
  * Envoyer un courrier électronique
  * mailto:\[destinataire-e-mail\]?subject=\[objet\]&body=\[message\] 
  * Example:mailto:foo@example.com?subject=Greetings%20from%20Azure%20Mobile%20Engagement!&amp;body=Good%20stuff!
  * Envoyer un SMS (application Skype du Store requise)
  * sms:\[numéro-téléphone\] 
  * Exemple :sms:2125551212
  * Composer un numéro de téléphone (application Skype du Store requise)
  * tel:\[numéro-téléphone\] 
  * Exemple :tel:2125551212
  * Télécharger une application sur hello Play Store
  * ms-windows-store:PDP?PFN=\[ID de package d’application\] 
  * Exemple :ms-windows-store:PDP?PFN=4d91298a-07cb-40fb-aecc-4cb5615d53c1
  * Démarrer une recherche Bing Cartes
  * bingmaps:?q=\[requête de recherche\] 
  * Exemple :bingmaps:?q=starbucks,paris
  * Utiliser un modèle personnalisé
  * \[schéma personnalisé\]://\[paramètres du schéma personnalisé\] 
  * Exemple :myCustomProtocol://myCustomParams
  * Utiliser un package de données (application du Store pour la lecture d'extension requise)
  * \[dossier\]\[données\].\[extension\] 
  * Exemple :myfolderdata.txt

### <a name="build-a-tracking-url"></a>Génération d'une URL de suivi :
* Consultez hello la section « Paramètres » de hello <UI Documentation> pour obtenir des instructions sur la création d’une URL de suivi qui permettront de toodownload des utilisateurs de vos autres applications.

### <a name="define-hello-texts-of-your-announcement"></a>Définir les textes hello de l’annonce
Renseignez le titre de hello, le contenu et les textes de bouton de l’annonce. Vous pouvez cibler un public d’une campagne de futures en fonction des commentaires de la portée de la façon dont les utilisateurs ont répondu toothis campagne hello. Ciblage de l’audience peut être basé sur les commentaires hello d’indique si cette campagne a été simplement envoyée, réponse, actionnés ou quittés.

### <a name="see-also"></a>Voir aussi
* [Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]

## <a name="content-of-polls"></a>Contenu des sondages
![Reach-Content2][31] 

Renseignez hello titre, description et les textes de bouton de l’annonce. Ajoutez ensuite des questions et choix pour les questions de tooyour réponses hello.
Vous pouvez cibler un public d’une campagne de futures en fonction des commentaires de la portée de la façon dont les utilisateurs ont répondu toothis campagne hello. Le ciblage de l'audience est déterminé selon que la campagne est issue d'une transmission de type push, qu'elle a obtenu une réponse, qu'elle a été activée ou quittée. Ciblage de l’audience peut également être basé sur les commentaires de réponse au sondage, où les choix de questions et réponses hello sont utilisés comme critères.

### <a name="see-also"></a>Voir aussi
* [Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]

## <a name="content-of-data-pushes"></a>Contenu des Push de données
![Reach-Content3][32] 

### <a name="choose-hello-type-of-your-data"></a>Choisissez le type hello de vos données :
* Texte
* Données binaires
* Données Base64

### <a name="define-hello-content-of-your-data"></a>Définir le contenu de hello de vos données
* Si vous avez sélectionné des données de texte toopush, copiez et collez le texte hello dans la zone « contenu » de hello.
* Si vous avez sélectionné toopush données binaire ou en base 64, utilisez tooupload de bouton « Télécharger votre fichier » hello votre fichier.
* Vous pouvez cibler un public d’une campagne de futures en fonction des commentaires de la portée de la façon dont les utilisateurs ont répondu toothis campagne hello. Le ciblage de l'audience est déterminé selon que la campagne est issue d'une transmission de type push, qu'elle a obtenu une réponse, qu'elle a été activée ou quittée.

### <a name="see-also"></a>Voir aussi
* [Documentation sur l’interface utilisateur - Reach - Nouveau critère Push][Link 28]

## <a name="content-of-tiles-windows-phone-only"></a>Contenu des vignettes (Windows Phone uniquement)
![Reach-Content4][33]

### <a name="define-hello-content-of-your-tile"></a>Définir le contenu de votre vignette hello
charge utile de vignette Hello est hello toobe de texte affichée dans la mosaïque hello de votre application sur les appareils Windows Phone.
Un push de la vignette est version du Service de Notification Push Microsoft (MPNS) hello d’un push natif pour Windows Phone. Hello vignette push type est hello uniquement par émission de données qui n’a pas de réponse et donc audience hello de futures campagnes ne peut pas être généré sur les résultats d’une campagne de push de vignette hello. 

### <a name="see-also"></a>Voir aussi
* [Documentation sur les API - API Reach - Push natif][Link 4]

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

