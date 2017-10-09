---
title: "aaaAzure Mobile Engagement Troubleshooting Guide - Push/portée"
description: "Résolution des problèmes des interactions et des notifications utilisateur dans Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: 
author: piyushjo
manager: erikre
editor: 
ms.assetid: 3f1886b7-1fdd-47f4-b6b0-d79f158d5ef3
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 4ee0b34b9b753a98ccf24863acb28a5dc76bfb95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-push-and-reach-issues"></a>Guide de dépannage pour les problèmes liés à Push et Reach
Hello Voici les problèmes possibles, que vous pouvez rencontrer avec comment Azure Mobile Engagement renvoie les informations que les utilisateurs tooyour.

## <a name="push-failures"></a>Échecs Push
### <a name="issue"></a>Problème
* Push ne fonctionne pas (dans l'application, hors de l'application, ou les deux).

### <a name="causes"></a>Causes
* Autant de fois un échec de push est une indication que Azure Mobile Engagement, portée ou une autre fonctionnalité avancée d’Azure Mobile Engagement n’est pas correctement intégrée ou qu’une mise à niveau est requise dans hello SDK toofix un problème connu avec une nouvelle plateforme de système d’exploitation ou l’appareil.
* Si un élément est un problème dans l’application ou de test simplement un push dans l’application et simplement un toodetermine de push hors de l’application.
* Tester à partir de l’interface utilisateur de hello et hello API comme un toosee étape de dépannage les informations d’erreur supplémentaire sont disponibles aux deux emplacements.
* Hors de l’application push ne fonctionne pas si Azure Mobile Engagement et portée sont intégrés dans le Kit de développement logiciel de hello.
* Les transmissions de type push ne fonctionneront pas si les certificats ne sont pas valides, ou s’ils utilisent PROD DEV correctement (iOS uniquement). (**Remarque :** « hors de l’application » des notifications push peuvent ne pas être remises tooiOS, si les deux développement hello (DEV) et les versions de production (production) de votre application sont installés sur hello même appareil depuis le jeton de sécurité hello associé avec votre certificat peut être invalidée par Apple. tooresolve ce problème, désinstallez hello développement et les versions de production de votre application et réinstaller le programme uniquement hello une version sur votre appareil.)
* Hors de l’application des nombres de push sont gérées différemment dans les différentes plateformes (iOS affiche moins d’informations que Android si push natif est désactivées sur un appareil, hello API peut fournir plus d’informations que l’interface utilisateur de hello des statistiques de push de).
* Les push en dehors de l'application peuvent être bloqués par les clients au niveau du système d'exploitation (iOS et Android).
* Hors de l’application push s’affichera comme étant désactivés Bonjour Azure Mobile Engagement UI s’ils ne sont pas intégrés correctement, mais risque d’échouer en mode silencieux à partir de l’API de hello.
* Dans l’application push ne fonctionne pas si Azure Mobile Engagement et portée sont intégrés dans le Kit de développement logiciel de hello.
* Push GCM et ADM ne fonctionne pas si Azure Mobile Engagement et serveur spécifique de hello sont intégrés dans hello SDK (Android uniquement).
* En application et hors de l’application push doit-elle être testés séparément toodetermine s’il s’agit d’un problème de Push ou de portée.
* Dans l’application push nécessitent cette application hello ouvrir toobe reçu.
* Dans l’application push est souvent toobe le programme d’installation filtré par une balise d’informations sur application opt-in ou de refus.
* Si vous utilisez une catégorie personnalisée dans les notifications de portée toodisplay dans l’application, vous devez toofollow hello correct cycle de vie de la notification de hello, sans quoi les notification hello ne peut pas être effacée lorsque les utilisateur hello faire disparaître.
* Si vous démarrez une campagne avec aucune date de fin et un appareil reçoit hello dans la notification de l’application, mais elle n’apparaît pas encore, hello utilisateur toujours recevra hello de notification hello leur prochaine que connexion dans l’application hello, même si vous arrêtez manuellement les campagnes hello.
* Pour les problèmes avec les API de Push de hello, confirmez que vraiment et vous souhaitez toouse hello API de Push au lieu de l’API couverture de hello (étant donné que hello API couverture est utilisée plus souvent) que vous n’êtes pas à confusion hello « charge utile » et les paramètres de « notifiant ».
* Tester votre campagne push avec à la fois un appareil connecté via le Wi-Fi et 3G tooeliminate hello connexion réseau comme une source possible de problèmes.

## <a name="push-testing"></a>Test push
### <a name="issue"></a>Problème
* Push peut être envoyé tooa de périphérique spécifique basé sur un ID de périphérique.

### <a name="causes"></a>Causes
* Appareils de test sont configurés différemment pour chaque plateforme, mais à l’origine d’un événement dans votre application sur un appareil de test et recherchez l’ID de votre appareil dans le portail de hello doivent fonctionner toofind ID de votre appareil pour toutes les plateformes.
* Les périphériques de test fonctionnent différemment avec IDFA et IDFV (iOS uniquement).

## <a name="push-customization"></a>Personnalisation push
### <a name="issue"></a>Problème
* L'élément de contenu push avancé ne fonctionne pas (badge, sonnerie, vibration, image, etc.).
* Des liens à partir de push ne fonctionnent pas (hors de l’application, dans l’application, du site Web tooa, emplacement tooa dans l’application).
* Afficher des statistiques par émission de données que de push n’a pas envoyé à tooas de nombreuses personnes comme prévu (trop ou pas assez).
* Push dupliqués et reçus en double.
* Impossible d'inscrire le dispositif de test pour les push Azure Mobile Engagement (avec votre propre application de production ou développement).

### <a name="causes"></a>Causes
* toolink tooa emplacement spécifique dans l’application requiert « catégories » (Android uniquement).
* Approfondie liaison schémas tooredirect utilisateurs tooan un autre emplacement après avoir cliqué sur une notification push devez toobe créé dans et géré par votre appareil hello d’application et de système d’exploitation non par Mobile Engagement directement. (**Remarque :** hors de l’application notifications ne peut pas lier directement des emplacements d’application tooin avec iOS comme pour Android.)
* Serveurs de l’image externe doivent toouse en mesure de toobe HTTP « GET » et « HEAD » pour l’image volumineuse exécute un push toowork (Android uniquement).
* Dans votre code, vous pouvez désactiver l’agent d’Azure Mobile Engagement hello lorsque les clavier hello sont ouvert et que votre code de réactiver l’agent d’Azure Mobile Engagement hello une fois que le clavier de hello est fermée afin que hello clavier n’affecte pas apparence hello de votre notification (iOS uniquement).
* Certains éléments ne fonctionnent pas dans les simulations de test, mais uniquement les campagnes réelles (badge, sonnerie, vibration, image, etc.).
* Aucun côté serveur données sont enregistrées lorsque vous utilisez le bouton de hello trop « test » exécute un push. Les données sont enregistrées uniquement pour les campagnes push réelles.
* toohelp isoler le problème, résoudre les problèmes avec : test, de simuler et une campagne réelle dans la mesure où ils fonctionnent différemment.
* Hello durée que de « application » et les campagnes « tout temps » sont planifiée toorun peut affecter des numéros de remise dans la mesure où une campagne est adressée uniquement toousers qui sont « dans l’application » pendant l’exécution de la campagne de hello (et les utilisateurs qui disposent de leurs paramètres de périphérique définir tooreceive notifications « hors de l’application »).
* différences de comment handle Android et iOS en dehors des notifications de l’application le rend difficile toodirectly Hello comparer les statistiques de push entre hello Android et iOS une version de votre application. Android fournit plus d’informations de notification au niveau du système d’exploitation qu’iOS. Android signale quand une notification native est reçue, un clic sur ou supprimée dans le centre de notifications hello, mais iOS ne signale pas ces informations, sauf si les notifications hello sont cliquée. 
* Hello principale raison pour laquelle les nombres « poussées » sont différentes de celles de l’autre que « remis » des numéros pour atteint des campagnes est que « dans l’application » et « hors de l’application » notifications sont comptées différemment. « Dans l’application » notifications sont gérées par Mobile Engagement, mais « hors de l’application » notifications sont gérées par le centre de notifications hello Bonjour du système d’exploitation de votre appareil.

## <a name="push-targeting"></a>Ciblage push
### <a name="issue"></a>Problème
* La ciblage intégré ne fonctionne pas comme prévu.
* Le ciblage de balise d'informations d'application ne fonctionne pas comme prévu.
* Le ciblage par géolocalisation ne fonctionne pas comme prévu.
* Les options de langue ne fonctionnent pas comme prévu.

### <a name="causes"></a>Causes
* Assurez-vous que vous avez téléchargé les balises d’informations application via hello Azure Mobile Engagement UI ou des API.
* Limitation hello vitesse ou push quota push au niveau de l’application hello ou limitation audience hello au niveau de campagne hello peut empêcher une personne de recevoir une notification push spécifique même si elles répondent à vos critères de ciblage. 
* La définition d'une « langue » est différente du ciblage en fonction du pays ou des paramètres régionaux, qui lui-même est différent du ciblage en fonction de l'emplacement géographique basé sur l'emplacement téléphonique ou du GPS.
* message de type Hello Bonjour « langue par défaut » est envoyé client tooany ne disposant pas leur appareil définir tooone de langue de remplacement hello que vous spécifiez.

## <a name="push-scheduling"></a>Planification push
### <a name="issue"></a>Problème
* La planification push ne fonctionne pas comme prévu (envoi trop précoce ou retardé).

### <a name="causes"></a>Causes
* Fuseaux horaires peuvent problèmes grâce à la planification, surtout lorsque vous utilisez le fuseau horaire de hello les utilisateurs finaux.
* Les fonctionnalités push avancées peuvent retarder les push.
* Ciblage basé sur le téléphone paramètres (au lieu d’application Info balises) susceptibles de retarder la pousse car Azure Mobile Engagement peuvent avoir des données en temps réel hello phone toorequest avant d’envoyer une notification push.
* Les campagnes créées sans une date de fin stockent hello push localement sur l’appareil de hello et les affichent hello prochaine application hello est ouvert, même si la campagne de hello terminée manuellement.
* À partir de plusieurs campagnes à hello même temps peut prendre un tooscan plu de temps votre base d’utilisateurs (essayez tooonly démarrer une campagne à l’aide d’un maximum de quatre, également cibler uniquement les utilisateurs actifs tooyour afin que les anciens utilisateurs n’aient pas toobe analysé).
* Si vous utilisez option de « Ignorer Audience, push seront envoyés toousers via hello API » hello de section de « De la campagne » hello d’une couverture campagne, campagne de hello n’envoie pas automatiquement, vous devez toosend manuellement via l’API couverture de hello.
* Si vous utilisez une catégorie personnalisée dans les notifications de portée toodisplay dans l’application, vous devez toofollow hello correct cycle de vie d’une notification, ou bien les notifications hello ne peuvent pas être effacée lorsque les utilisateur hello faire disparaître.

