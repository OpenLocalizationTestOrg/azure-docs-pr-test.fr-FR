---
title: aaaTemplates
description: "Cette rubrique décrit les modèles pour les hubs de notification Azure."
services: notification-hubs
documentationcenter: .net
author: ysxu
manager: erikre
editor: 
ms.assetid: a41897bb-5b4b-48b2-bfd5-2e3c65edc37e
ms.service: notification-hubs
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: multiple
ms.topic: article
ms.date: 06/29/2016
ms.author: yuaxu
ms.openlocfilehash: 0149f0c7473e5a4b952905bc8217582b58db2a0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="templates"></a>Modèles
## <a name="overview"></a>Vue d'ensemble
Les modèles permettent à un client application toospecify hello format exact de notifications hello qu'il veut tooreceive. À l’aide de modèles, une application peut permettre de différents avantages, notamment hello suivantes :

* Un serveur principal non spécifique à une plateforme
* Des notifications personnalisées
* Indépendance vis-à-vis de la version du client
* Localisation facile

Cette section fournit deux exemples complets de comment toouse modèles toosend indépendant de la plateforme des notifications ciblant tous vos appareils plates-formes et toopersonalize diffusion tooeach de périphérique de notification.

## <a name="using-templates-cross-platform"></a>Utilisation des modèles entre plateformes
notifications de push toosend Hello moyen standard est toosend, pour chaque notification qui est toobe envoyée, une charge utile tooplatform notification les services (WNS, APNS). Par exemple, une alerte tooAPNS, de toosend charge utile de hello est un objet Json de hello suivant du formulaire :

    {"aps": {"alert" : "Hello!" }}

toosend un message toast similaire sur une application du Windows Store, charge XML hello est comme suit :

    <toast>
      <visual>
        <binding template=\"ToastText01\">
          <text id=\"1\">Hello!</text>
        </binding>
      </visual>
    </toast>

Vous pouvez créer des charges utiles similaires pour les plateformes MPNS (Windows Phone) et GCM (Android).

Cette exigence force hello application back-end tooproduce différentes charges utiles pour chaque plateforme et le rend hello principal responsable de la partie de la couche de présentation de hello d’application hello. Certaines préoccupations concernent les présentations graphiques et la localisation (en particulier pour les applications Windows Store qui incluent des notifications pour divers types de mosaïques).

fonctionnalité de modèle de Notification Hubs Hello permet à une application toocreate spécial inscriptions des clients, appelé inscriptions de modèle, y compris, en outre ensemble toohello de balises, un modèle. fonctionnalité de modèle de Notification Hubs Hello permet des périphériques client application tooassociate avec des modèles si vous travaillez avec des Installations (recommandées) ou les enregistrements. Étant donné hello précédant les exemples de la charge utile, hello uniquement les informations indépendant de la plateforme sont message d’alerte réel hello (Hello). Un modèle est un ensemble d’instructions pour hello Hub de Notification sur comment tooformat indépendant de la plateforme de message pour l’inscription de hello de cette application de client spécifique. Bonjour précédent exemple, message de salutation plateforme indépendant est une propriété unique : **message = Hello !**.

Hello illustration suivante décrit hello au-dessus de processus :

![](./media/notification-hubs-templates/notification-hubs-hello.png)

modèle Hello pour l’inscription d’une application cliente iOS hello est comme suit :

    {"aps": {"alert": "$(message)"}}

modèle de Hello correspondant pour l’application de client hello du Windows Store est la suivante :

    <toast>
        <visual>
            <binding template=\"ToastText01\">
                <text id=\"1\">$(message)</text>
            </binding>
        </visual>
    </toast>

Notez que hello réel du message est remplacé par hello expression $(message). Cette expression indique hello concentrateur de Notification, chaque fois qu’il envoie un message toothis enregistrement particulier, toobuild un message qui suit il et les commutateurs dans la valeur courante hello.

Si vous travaillez avec un modèle d’Installation, clé « modèles » de l’installation hello conserve un JSON de plusieurs modèles. Si vous travaillez avec un modèle d’inscription, hello application cliente peut créer plusieurs enregistrements dans l’ordre toouse plusieurs modèles ; par exemple, un modèle pour les messages d’alerte et un modèle pour les mises à jour de la vignette. Les applications clientes peuvent également combiner inscriptions natives (inscriptions sans modèle) et inscriptions avec modèle.

Hello Hub de Notification envoie une notification pour chaque modèle sans tenir compte si elles appartiennent toohello même application cliente. Ce comportement peut être utilisé tootranslate des notifications d’indépendant de la plateforme en plus des notifications. Par exemple, hello même toohello message indépendant de plateforme que Hub de Notification peut être traduit en toute transparence une alerte de toast et une mise à jour de la vignette, sans nécessiter de hello toobe principal prenant en charge de celui-ci. Notez que certaines plateformes (par exemple, iOS) peuvent réduire plusieurs notifications toohello appareil même si elles sont envoyées sur une courte période de temps.

## <a name="using-templates-for-personalization"></a>Utilisation des modèles à des fins de personnalisation
Modèles de toousing un autre avantage est hello capacité toouse personnalisation de l’inscription par tooperform concentrateurs de Notification des notifications. Par exemple, considérez une application Météo qui affiche une vignette avec les conditions météo hello à un emplacement spécifique. Un utilisateur peut choisir entre les degrés Celsius ou Fahrenheit, et une prévision à un jour ou sur les cinq prochains jours. À l’aide de modèles, chaque installation de l’application cliente peut inscrire pour format hello requis (1 jour Fahrenheit Celsius, 1 jour, 5 jours Celsius, 5 jours Fahrenheit), et avoir hello principal d’envoyer un message unique qui contient toutes les informations de hello requis toofill celles modèles (par exemple, une cinq jours prévision avec degrés Celsius et Fahrenheit).

modèle de Hello pour hello une journée prévision avec Celsius températures est comme suit :

    <tile>
      <visual>
        <binding template="TileWideSmallImageAndText04">
          <image id="1" src="$(day1_image)" alt="alt text"/>
          <text id="1">Seattle, WA</text>
          <text id="2">$(day1_tempC)</text>
        </binding>  
      </visual>
    </tile>

message envoyé de Hello toohello Hub de Notification contient hello toutes les propriétés suivantes :

<table border="1">

<tr><td>day1_image</td><td>day2_image</td><td>day3_image</td><td>day4_image</td><td>day5_image</td></tr>

<tr><td>day1_tempC</td><td>day2_tempC</td><td>day3_tempC</td><td>day4_tempC</td><td>day5_tempC</td></tr>

<tr><td>day1_tempF</td><td>day2_tempF</td><td>day3_tempF</td><td>day4_tempF</td><td>day5_tempF</td></tr>
</table><br/>

À l’aide de ce modèle, hello principal envoie uniquement un seul message sans avoir toostore les options de personnalisation spécifiques pour les utilisateurs d’application hello. Hello illustration suivante décrit ce scénario :

![](./media/notification-hubs-templates/notification-hubs-registration-specific.png)

## <a name="how-tooregister-templates"></a>Comment les modèles tooregister
tooregister avec des modèles à l’aide du modèle d’Installation hello (recommandé) ou hello modèle d’inscription, consultez [gestion de l’inscription](notification-hubs-push-notification-registration-management.md).

## <a name="template-expression-language"></a>Langage d’expression de modèle
Les modèles sont tooXML limité ou formats de documents JSON. Vous pouvez également placer des expressions à des endroits particuliers ; par exemple, des attributs de nœud ou des valeurs pour XML, des valeurs de propriété de chaîne pour JSON.

Hello tableau suivant affiche langage hello autorisée dans les modèles :

| Expression | Description |
| --- | --- |
| $(prop) |Propriété d’événement tooan référence avec le nom donné de hello. Les noms de propriétés ne respectent pas la casse. Cette expression est résolue en valeur de texte de la propriété hello ou dans une chaîne vide si la propriété de hello n’est pas présente. |
| $(prop, n) |Comme ci-dessus, mais hello texte est explicitement tronqué sur n caractères, par exemple $(titre, 20) découpe hello contenu de la propriété de titre hello à 20 caractères. |
| .(prop, n) |Comme ci-dessus, mais hello texte est suivi du suffixe avec trois points comme il est tronqué. taille totale de Hello Hello détouré chaîne et suffixe de hello ne dépasse pas n caractères. . (titre, 20) avec une propriété d’entrée de « This is ligne de titre hello » entraîne **ce titre de hello est en cours...** |
| %(prop) |Too$(name) similaire à l’exception de cette sortie hello est codée au format URI. |
| #(prop) |Utilisé dans les modèles JSON (par exemple, pour les modèles iOS et Android).<br><br>Cette fonction est effective même hello exactement comme $(prop) précédemment spécifié, sauf lorsque utilisés dans les modèles JSON (par exemple, les modèles d’Apple). Dans ce cas, si cette fonction n’est pas entourée par des « {', '} » (par exemple, 'myJsonProperty' : « #(nom) »), et il a la valeur nombre tooa au format Javascript, par exemple, regexp : (0 &#124; (&#91; 1-9 &#93; &#91; 0-9 & #93  ;*))(\. &#91; 0-9 &#93; +) ? ((e &#124; E) (+ &#124;-) ? &#91; 0-9 &#93; +) ?, puis hello de sortie JSON est un nombre.<br><br>Par exemple, 'badge : '#(name)' devient 'badge' : 40 (et non '40'). |
| ‘text’ ou « text » |Un littéral. Les littéraux contiennent du texte arbitraire placé entre guillemets simples ou doubles. |
| expr1 + expr2 |opérateur de concaténation Hello jointure de deux expressions en une seule chaîne. |

les expressions Hello peuvent être hello précédant les formulaires.

Lors de l’utilisation de la concaténation, ensemble de l’expression hello doit être entouré de {}. Par exemple, {$(prop) + ' - ' + $(prop2)}. |

Par exemple, suivant de hello n’est pas un modèle XML valide :

    <tile>
      <visual>
        <binding $(property)>
          <text id="1">Seattle, WA</text>
        </binding>  
      </visual>
    </tile>


Comme expliqué ci-dessus, lors de l’utilisation de la concaténation, les expressions doivent être placées entre accolades. Par exemple :

    <tile>
      <visual>
        <binding template="ToastText01">
          <text id="1">{'Hi, ' + $(name)}</text>
        </binding>  
      </visual>
    </tile>

