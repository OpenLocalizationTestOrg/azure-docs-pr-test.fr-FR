---
title: "aaaAzure API Kit de développement logiciel de Mobile Engagement Web | Documents Microsoft"
description: "Hello les dernières mises à jour et les procédures à suivre pour hello Web SDK pour Azure Mobile Engagement"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 8a87d5ac-d8b7-4a0d-bdee-414dbcc561b2
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: web
ms.devlang: js
ms.topic: article
ms.date: 06/07/2016
ms.author: piyushjo
ms.openlocfilehash: ec1261d6ad573b8c3ad6d5f616ab7bbe560d6fe2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-mobile-engagement-api-in-a-web-application"></a>Utilisez hello Azure Mobile Engagement API dans une application web
Ce document est un document de toohello d’addition qui vous indique comment trop[intégrer Mobile Engagement dans une application web](mobile-engagement-web-integrate-engagement.md). Il fournit des informations détaillées à propos de la façon dont toouse hello Azure Mobile Engagement API tooreport vos statistiques de l’application.

API d’Engagement Mobile Hello est fournie par hello `engagement.agent` objet. Hello par défaut de kit de développement Web Azure Mobile Engagement d’alias est `engagement`. Vous pouvez redéfinir l’alias à partir de la configuration du Kit de développement logiciel hello.

## <a name="mobile-engagement-concepts"></a>Concepts de Mobile Engagement
Hello parties suivantes affiner commun [concepts de Mobile Engagement](mobile-engagement-concepts.md) pour la plateforme web de hello.

### <a name="session-and-activity"></a>`Session` et `Activity`
Si l’utilisateur de hello reste inactif pendant plus de quelques secondes entre deux activités, hello séquence de l’utilisateur des activités est fractionné en deux sessions distinctes. Délai d’expiration de session hello sont appelés des ces quelques secondes.

Si votre application web ne déclare pas fin hello d’activités des utilisateurs par lui-même (en appelant hello `engagement.agent.endActivity` fonction), serveur de Mobile Engagement hello expire automatiquement hello session utilisateur dans les trois minutes après la fermeture de la page de l’application hello. Il s’agit de délai d’expiration de session de serveur hello.

### `Crash`
Les rapports automatisés d’exceptions JavaScript non interceptées ne sont pas créés par défaut. Toutefois, vous pouvez signaler les pannes manuellement à l’aide de hello `sendCrash` (voir la section de hello sur les rapports d’incidents).

## <a name="reporting-activities"></a>Rapports d’activités
Création de rapports sur l’activité des utilisateurs inclut lorsqu’un utilisateur démarre une nouvelle activité et lorsque l’utilisateur de hello met fin à l’activité en cours hello.

### <a name="user-starts-a-new-activity"></a>L’utilisateur démarre une nouvelle activité
    engagement.agent.startActivity("MyUserActivity");

Vous devez toocall `startActivity()` chaque activité utilisateur change. Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.

### <a name="user-ends-hello-current-activity"></a>Utilisateur met fin à l’activité en cours hello
    engagement.agent.endActivity();

Vous devez toocall `endActivity()` au moins une fois lorsque hello utilisateur a fini de leur dernière activité. Cela permet d’informer hello Kit de développement Web Mobile Engagement qu’utilisateur de hello est actuellement inactif et que la session d’utilisateur hello a besoin toobe fermés après l’expiration du délai d’expiration de session hello. Si vous appelez `startActivity()` avant l’expiration du délai d’expiration de session hello, hello simplement la reprise de session.

Étant donné qu’aucun appel fiable pour la fermeture de la fenêtre de navigateur hello, il est souvent de fin de hello toocatch impossible ou difficile d’activités des utilisateurs à l’intérieur d’un environnement web. Qui est hello pourquoi Mobile Engagement serveur expire automatiquement session d’utilisateur hello dans les trois minutes après la fermeture de la page de l’application hello.

## <a name="reporting-events"></a>Rapports d’événements
Les rapports d’événements couvrent les événements de session et les événements autonomes.

### <a name="session-events"></a>Événements de session
Événements de session sont généralement des actions de hello tooreport utilisé effectuées par un utilisateur au cours de la session de l’utilisateur hello.

**Exemple sans données supplémentaires :**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login');
      // [...]
    }

**Exemple avec des données supplémentaires :**

    loginButton.onclick = function() {
      engagement.agent.sendSessionEvent('login', {user: 'alice'});
      // [...]
    }

### <a name="standalone-events"></a>Événements autonomes
Contrairement aux événements de session, les événements autonome peuvent se produire en dehors du contexte hello d’une session.

Pour cela, utilisez ``engagement.agent.sendEvent`` au lieu de ``engagement.agent.sendSessionEvent``.

## <a name="reporting-errors"></a>Rapports d’erreurs
Les rapports d’erreurs couvrent les erreurs de session et les erreurs autonomes.

### <a name="session-errors"></a>Erreurs de session
Erreurs de session sont généralement des erreurs hello tooreport utilisé qui ont un impact sur l’utilisateur de hello pendant la session de l’utilisateur hello.

**Exemple sans données supplémentaires :**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short');
      }
      // [...]
    }

**Exemple avec des données supplémentaires :**

    var validateForm = function() {
      // [...]
      if (password.length < 6) {
        engagement.agent.sendSessionError('password_too_short', {length: 4});
      }
      // [...]
    }

### <a name="standalone-errors"></a>Erreurs autonomes
Contrairement aux erreurs de session, les erreurs autonome peuvent se produire en dehors du contexte hello d’une session.

Pour cela, utilisez `engagement.agent.sendError` au lieu de `engagement.agent.sendSessionError`.

## <a name="reporting-jobs"></a>Rapports de travaux
Les rapports de travaux couvrent les erreurs et les événements qui se produisent lors d’un travail, ainsi que les rapports d’incidents.

**Exemple :**

Si vous souhaitez toomonitor une requête AJAX, vous utiliseriez suivant de hello :

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
      // [...]
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-errors-during-a-job"></a>Signaler les erreurs lors d’un travail
Erreurs peuvent être associée tooa travail au lieu de la session utilisateur en cours toohello en cours d’exécution.

**Exemple :**

Si vous souhaitez tooreport une erreur si une requête AJAX échoue :

    // [...]
    xhr.onreadystatechange = function() {
      if (xhr.readyState == 4) {
        // [...]
        if (xhr.status == 0 || xhr.status >= 400) {
          engagement.agent.sendJobError('publish_xhr', 'publish', {status: xhr.status, statusText: xhr.statusText});
        }
        engagement.agent.endJob('publish');
      }
    }
    engagement.agent.startJob('publish');
    xhr.send();
    // [...]

### <a name="reporting-events-during-a-job"></a>Rapports d’événements pendant un travail
Les événements peuvent être associée tooa exécution de travail au lieu de la session utilisateur en cours toohello, grâce toohello `engagement.agent.sendJobEvent` (fonction).

Cette fonction fonctionne exactement comme `engagement.agent.sendJobError`.

### <a name="reporting-crashes"></a>Rapports d’incidents
Hello d’utilisation `sendCrash` fonction tooreport tombe en panne manuellement.

Hello `crashid` argument est une chaîne qui identifie le type hello d’incident.
Hello `crash` argument est généralement la trace de la pile hello d’incident hello sous forme de chaîne.

    engagement.agent.sendCrash(crashid, crash);

## <a name="extra-parameters"></a>Paramètres supplémentaires
Vous pouvez attacher des événements de tooan de données arbitraires, erreur, activité ou la tâche.

les données de salutation peuvent être n’importe quel objet JSON (mais pas un tableau ou type primitif).

**Exemple :**

    var extras = {"video_id": 123, "ref_click": "http://foobar.com/blog"};
    engagement.agent.sendEvent("video_clicked", extras);

### <a name="limits"></a>limites
Les limites qui s’appliquent les paramètres tooextra sont dans des domaines de hello des expressions régulières pour les clés, les types valeur et taille.

#### <a name="keys"></a>Clés
Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :

    ^[a-zA-Z][a-zA-Z_0-9]*

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="values"></a>Valeurs
Les valeurs sont limitée toostring, nombre et types booléens.

#### <a name="size"></a>Taille
Fonctionnalités supplémentaires sont limitées too1, 024 caractères par appel (après que hello Kit de développement Web Mobile Engagement qu’elle l’encode au format JSON).

## <a name="reporting-application-information"></a>Rapports d’informations sur l’application
Vous pouvez signaler manuellement le suivi des informations (ou toutes autres informations spécifiques à l’application) à l’aide de hello `sendAppInfo()` (fonction).

Notez que ces informations peuvent être envoyées de façon incrémentielle. Uniquement hello valeur la plus récente pour une clé spécifique est conservé pour un périphérique spécifique.

Comme événement extras, vous pouvez utiliser les informations de l’application de JSON objet tooabstract. Notez que les tableaux ou les sous-objets sont traités comme des chaînes plates (à l’aide de la sérialisation JSON).

**Exemple :**

Voici un exemple de code pour le sexe de l’utilisateur expéditeur hello et date de naissance :

    var appInfos = {"birthdate":"1983-12-07","gender":"female"};
    engagement.agent.sendAppInfo(appInfos);

### <a name="limits"></a>limites
Les limites qui s’appliquent les informations de tooapplication sont dans des zones de hello des expressions régulières pour les clés et la taille.

#### <a name="keys"></a>Clés
Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :

    ^[a-zA-Z][a-zA-Z_0-9]*

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="size"></a>Taille
Informations de l’application sont limitée too1, 024 caractères par appel (après que hello Kit de développement Web Mobile Engagement qu’elle l’encode au format JSON).

Bonjour précédent exemple, hello JSON envoyé toohello server est 44 caractères :

    {"birthdate":"1983-12-07","gender":"female"}
