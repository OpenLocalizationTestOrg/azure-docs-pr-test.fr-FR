---
title: aaaHow tooUse hello Engagement API sur iOS
description: "Dernière iOS SDK - comment tooUse hello Engagement API sur iOS"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 1fb4509e-3804-46c1-949f-1cf727f91f9f
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-ios
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 7fb9b95ad319cf3b1e2de81b5d6aee5b30266069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-ios"></a>Comment tooUse hello Engagement API sur iOS
Ce document est un module complémentaire toohello comment tooIntegrate Engagement sur iOS : il fournit obtenir plus de détails sur comment toouse hello Engagement API tooreport vos statistiques de l’application.

Gardez à l’esprit que si vous ne souhaitez qu’Engagement tooreport sessions, activités, blocages et des informations techniques, de votre application puis hello la plus simple façon est toomake toutes vos personnalisé `UIViewController` objets héritent de hello correspondant `EngagementViewController` classe .

Si vous voulez toodo plus, par exemple, si vous avez besoin tooreport les événements d’application spécifique, les erreurs et les tâches, ou si vous avez tooreport activités de votre application d’une manière différente d’une implémentation dans hello hello `EngagementViewController` des classes, vous devez toouse hello API d’engagement.

API d’Engagement Hello est fournie par hello `EngagementAgent` classe. Une instance de cette classe peut être récupérée en appelant hello `[EngagementAgent shared]` méthode statique (Notez que hello `EngagementAgent` objet retourné est un singleton).

Avant que les appels d’API, hello `EngagementAgent` objet doit être initialisé en appelant la méthode hello`[EngagementAgent init:@"Endpoint={YOUR_APP_COLLECTION.DOMAIN};SdkKey={YOUR_SDK_KEY};AppId={YOUR_APPID}"];`

## <a name="engagement-concepts"></a>Concepts liés à Engagement
parties suivantes Hello affiner hello commun [Concepts d’Engagement Mobile](mobile-engagement-concepts.md) pour la plateforme iOS de hello.

### <a name="session-and-activity"></a>`Session` et `Activity`
Un *activité* est généralement associé à un écran de l’application hello, qui est toosay hello *activité* démarre lorsque l’écran hello s’affiche et s’arrête lors de la fermeture de l’écran hello : il s’agit de hello cas, lorsque Kit de développement logiciel Engagement Hello est intégré à l’aide de hello `EngagementViewController` classes.

Mais *activités* peut également être contrôlée manuellement à l’aide des API de l’Engagement de hello. Cela permet à un écran toosplit dans plusieurs tooget de parties sub plus de détails sur hello d’utilisation de l’écran (par exemple tooknown la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisés à l’intérieur de cet écran).

## <a name="reporting-activities"></a>Rapports d'activités
### <a name="user-starts-a-new-activity"></a>L'utilisateur démarre une nouvelle activité
            [[EngagementAgent shared] startActivity:@"MyUserActivity" extras:nil];

Vous devez toocall `startActivity()` chaque activité utilisateur hello change. Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.

### <a name="user-ends-his-current-activity"></a>L'utilisateur met fin à l'activité en cours
            [[EngagementAgent shared] endActivity];

> [!WARNING]
> Vous devez **jamais** appeler cette fonction par vous-même, sauf si vous souhaitez toosplit une utilisation de votre application dans plusieurs sessions : un appel de fonction de toothis se terminer hello session active immédiatement, par conséquent, un appel ultérieur trop`startActivity()`démarre une nouvelle session. Cette fonction est appelée automatiquement par le Kit de développement logiciel de hello lorsque votre application est fermée.
> 
> 

## <a name="reporting-events"></a>Rapports d'événements
### <a name="session-events"></a>Événements de session
Événements de session sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors de sa session.

**Exemple sans données supplémentaires :**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:nil];
            ...
       }
       [...]
    }

**Exemple avec des données supplémentaires :**

    @implementation MyViewController {
       [...]
       - (void)willRotateToInterfaceOrientation:(UIInterfaceOrientation)toInterfaceOrientation duration:(NSTimeInterval)duration
       {
        [super willRotateToInterfaceOrientation:toInterfaceOrientation duration:duration];
            ...
        NSMutableDictionary* extras = [NSMutableDictionary dictionary];
        [extras setObject:[NSNumber numberWithInt:toInterfaceOrientation] forKey:@"to_orientation_id"];
        [extras setObject:[NSNumber numberWithDouble:duration] forKey:@"duration"];
        [[EngagementAgent shared] sendSessionEvent:@"will_rotate" extras:extras];
            ...
       }
       [...]
    }

### <a name="standalone-events"></a>Événements autonomes
Événements de toosession contraires, autonome événements peuvent être utilisés en dehors du contexte hello d’une session.

**Exemple :**

    [[EngagementAgent shared] sendEvent:@"received_notification" extras:nil];

## <a name="reporting-errors"></a>Rapports d'erreurs
### <a name="session-errors"></a>Erreurs de session
Session erreurs sont généralement utilisés tooreport hello affecter l’utilisateur de hello lors de sa session.

**Exemple :**

    /** hello user has entered invalid data in a form */
    @implementation MyViewController {
      [...]
      -(void)onMyFormSubmitted:(MyForm*)form {
        [...]
        /* hello user has entered an invalid email address */
        [[EngagementAgent shared] sendSessionError:@"sign_up_email" extras:nil]
        [...]
      }
      [...]
    }

### <a name="standalone-errors"></a>Erreurs autonomes
Erreurs toosession contraires, autonome peuvent être utilisés en dehors du contexte hello d’une session.

**Exemple :**

    [[EngagementAgent shared] sendError:@"something_failed" extras:nil];

## <a name="reporting-jobs"></a>Rapports de travaux
**Exemple :**

Supposons que vous voulez tooreport hello la durée de votre processus de connexion :

    [...]
    -(void)signIn
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      [... sign in ...]

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    }
    [...]

### <a name="report-errors-during-a-job"></a>Signaler les erreurs lors d'un travail
Les erreurs peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.

**Exemple :**

Supposons que vous souhaitez tooreport une erreur pendant le processus de connexion :

    [...]
    -(void)signin
    {
      /* Start job */
      [[EngagementAgent shared] startJob:@"sign_in" extras:nil];

      BOOL success = NO;
      while (!success) {
        /* Try toosign in */
        NSError* error = nil;
        [self trySigin:&error];
        success = error == nil;

        /* If an error occured report it */
        if(!success)
        {
          [[EngagementAgent shared] sendJobError:@"sign_in_error"
                         jobName:@"sign_in"
                          extras:[NSDictionary dictionaryWithObject:[error localizedDescription] forKey:@"error"]];

          /* Retry after a moment */
          [NSThread sleepForTimeInterval:20];
        }
      }

      /* End job */
      [[EngagementAgent shared] endJob:@"sign_in"];
    };
    [...]

### <a name="events-during-a-job"></a>Événements lors d'un travail
Les événements peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.

**Exemple :**

Supposons que nous disposons d’un réseau social, nous utilisons un temps total hello tooreport travail pendant le hello utilisateur est connecté toohello server. Hello peuvent recevoir des messages de ses amis, il s’agit d’un événement de tâche.

    [...]
    - (void) signin
    {
      [...Sign in code...]
      [[EngagementAgent shared] startJob:@"connection" extras:nil];
    }
    [...]
    - (void) signout
    {
      [...Sign out code...]
      [[EngagementAgent shared] endJob:@"connection"];
    }
    [...]
    - (void) onMessageReceived
    {
      [...Notify user...]
      [[EngagementAgent shared] sendJobEvent:@"connection" jobName:@"message_received" extras:nil];
    }
    [...]

## <a name="extra-parameters"></a>Paramètres supplémentaires
Données arbitraires peuvent être attachés tooevents, les erreurs, les activités et les tâches.

Ces données peuvent être structurées, elles utilisent la classe NSDictionary d'iOS.

Notez que les données supplémentaires peuvent contenir des `arrays(NSArray, NSMutableArray)`, `numbers(NSNumber class)`, `strings(NSString, NSMutableString)`, `urls(NSURL)`, `data(NSData, NSMutableData)` ou d'autres instances `NSDictionary`.

> [!NOTE]
> Hello paramètre supplémentaire est sérialisé au format JSON. Si vous souhaitez toopass différents objets que hello ceux décrits précédemment, vous devez implémenter hello suivant de méthode dans votre classe :
> 
> -(NSString*)JSONRepresentation;
> 
> méthode Hello doit retourner une représentation JSON de votre objet.
> 
> 

### <a name="example"></a>Exemple
    NSMutableDictionary* extras = [NSMutableDictionary dictionaryWithCapacity:2];
    [extras setObject:[NSNumber numberWithInt:123] forKey:@"video_id"];
    [extras setObject:@"http://foobar.com/blog" forKey:@"ref_click"];
    [[EngagementAgent shared] sendEvent:@"video_clicked" extras:extras];

### <a name="limits"></a>Limites
#### <a name="keys"></a>Clés
Chaque clé Bonjour `NSDictionary` doit correspondre à hello expression régulière suivante :

`^[a-zA-Z][a-zA-Z_0-9]*`

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="size"></a>Taille
Fonctionnalités supplémentaires sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par agent d’Engagement hello).

Bonjour exemple précédent, hello JSON envoyé toohello serveur est 58 caractères :

    {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Rapports d'informations sur l'application
Vous pouvez signaler manuellement le suivi des informations (ou toutes les autres informations spécifiques aux applications) à l’aide de hello `sendAppInfo:` (fonction).

Notez que ces informations peuvent être envoyées de façon incrémentielle : uniquement hello valeur la plus récente d’une clé spécifique est conservé pour un périphérique donné.

Comme les autres fonctionnalités d’événement, hello `NSDictionary` classe informations tooabstract utilisés de l’application, notez que les tableaux ou les dictionnaires secondaire seront traités en tant que chaînes plats (à l’aide de la sérialisation JSON).

**Exemple :**

    NSMutableDictionary* appInfo = [NSMutableDictionary dictionaryWithCapacity:2];
    [appInfo setObject:@"female" forKey:@"gender"];
    [appInfo setObject:@"1983-12-07" forKey:@"birthdate"]; // December 7th 1983
    [[EngagementAgent shared] sendAppInfo:appInfo];

### <a name="limits"></a>Limites
#### <a name="keys"></a>Clés
Chaque clé Bonjour `NSDictionary` doit correspondre à hello expression régulière suivante :

`^[a-zA-Z][a-zA-Z_0-9]*`

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="size"></a>Taille
Informations sur l’application sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par agent d’Engagement hello).

Bonjour exemple précédent, hello JSON envoyé toohello serveur est 44 caractères :

    {"birthdate":"1983-12-07","gender":"female"}
