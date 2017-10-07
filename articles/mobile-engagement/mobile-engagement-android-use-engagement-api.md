---
title: aaaHow tooUse hello API Engagement sur Android
description: "Dernier Kit de développement logiciel Android - comment tooUse hello API Engagement sur Android"
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: 09b62659-82ae-4a55-8784-fca0b6b22eaf
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-android
ms.devlang: na
ms.topic: article
ms.date: 07/25/2016
ms.author: piyushjo;ricksal
ms.openlocfilehash: e0b2d484616c0c7874e77c5283d94c3063949ed2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-android"></a>Comment tooUse hello API Engagement sur Android
Ce document est un document toohello de module complémentaire [avancé Reporting des options pour le Kit de développement Android Mobile Engagement](mobile-engagement-android-advanced-reporting.md). Elle fournit en profondeur plus d’informations sur comment toouse hello Engagement API tooreport vos statistiques de l’application.

N’oubliez pas que si vous souhaitez uniquement Engagement tooreport sessions, activités, blocages et des informations techniques de votre application, puis hello plus simple consiste toomake tous vos `Activity` sous-classes héritent hello correspondant `EngagementActivity` classe.

Si vous voulez toodo plus, par exemple, si vous avez besoin tooreport les événements d’application spécifique, les erreurs et les tâches, ou si vous avez tooreport activités de votre application d’une manière différente d’une implémentation dans hello hello `EngagementActivity` des classes, vous devez toouse hello API d’engagement.

API d’Engagement Hello est fournie par hello `EngagementAgent` classe. Une instance de cette classe peut être récupérée en appelant hello `EngagementAgent.getInstance(Context)` méthode statique (Notez que hello `EngagementAgent` objet retourné est un singleton).

## <a name="engagement-concepts"></a>Concepts liés à Engagement
parties suivantes Hello affiner hello commun [Concepts d’Engagement Mobile](mobile-engagement-concepts.md), pour la plateforme de Android hello.

### <a name="session-and-activity"></a>`Session` et `Activity`
Si l’utilisateur de hello reste inactif entre deux de plus de quelques secondes *activités*, puis sa séquence de *activités* est fractionné en deux distinctes *sessions*. Ces quelques secondes sont appelés hello « session timeout ».

Un *activité* est généralement associé à un écran de l’application hello, qui est toosay hello *activité* démarre lorsque l’écran hello s’affiche et s’arrête lors de la fermeture de l’écran hello : il s’agit de hello cas, lorsque Kit de développement logiciel Engagement Hello est intégré à l’aide de hello `EngagementActivity` classes.

Mais *activités* peut également être contrôlée manuellement à l’aide des API de l’Engagement de hello. Cela permet à un écran toosplit dans plusieurs tooget de parties sub plus de détails sur hello d’utilisation de l’écran (par exemple tooknown la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisés à l’intérieur de cet écran).

## <a name="reporting-activities"></a>Rapports d'activités
> [!IMPORTANT]
> Vous ne devez pas tooreport des activités, telles que décrites dans cette section si vous utilisez hello `EngagementActivity` classe et ses variantes, comme expliqué comment Bonjour tooIntegrate Engagement sur document Android.
> 
> 

### <a name="user-starts-a-new-activity"></a>L'utilisateur démarre une nouvelle activité
            EngagementAgent.getInstance(this).startActivity(this, "MyUserActivity", null);
            // Passing hello current activity is required for Reach toodisplay in-app notifications, passing null will postpone such announcements and polls.

Vous devez toocall `startActivity()` chaque activité utilisateur hello change. Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.

Hello meilleures toocall place cette fonction se trouve sur chaque activité `onResume` rappel.

### <a name="user-ends-his-current-activity"></a>L'utilisateur met fin à l'activité en cours
            EngagementAgent.getInstance(this).endActivity();

Vous devez toocall `endActivity()` au moins une fois lorsque hello utilisateur a fini de sa dernière activité. Cela permet d’informer hello SDK Engagement qu’utilisateur de hello est actuellement inactive et que session d’utilisateur hello devez toobe fermés une fois hello expiration de la session expire (si vous appelez `startActivity()` avant l’expiration du délai d’expiration de session hello, hello simplement la reprise de session).

Hello meilleures toocall place cette fonction se trouve sur chaque activité `onPause` rappel.

## <a name="reporting-events"></a>Rapports d'événements
### <a name="session-events"></a>Événements de session
Événements de session sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors de sa session.

**Exemple sans données supplémentaires :**

            public MyActivity extends EngagementActivity {
               [...]
               @Override
               public boolean onPrepareOptionsMenu(Menu menu) {
                  getEngagementAgent().sendSessionEvent("menu_shown", null);
               }
               [...]
            }

**Exemple avec des données supplémentaires :**

            public MyActivity extends EngagementActivity {
              [...]
              @Override
              public boolean onMenuItemSelected(int featureId, MenuItem item) {
                Bundle extras = new Bundle();
                extras.putInt("id", item.getItemId());
                getEngagementAgent().sendSessionEvent("menu_selected", extras);
              }
              [...]
            }

### <a name="standalone-events"></a>Événements autonomes
Toosession contraires événements, les événements autonome peuvent se produire en dehors du contexte hello d’une session.

**Exemple :**

Supposons que vous souhaitez tooreport les événements qui se produit quand un récepteur de diffusion est déclenché :

            /** Triggered by Intent.ACTION_BATTERY_LOW */
            public BatteryLowReceiver extends BroadcastReceiver {
              [...]
              @Override
              public void onReceive(Context context, Intent intent) {
                EngagementAgent.getInstance(context).sendEvent("battery_low", null);
              }
              [...]
            }

## <a name="reporting-errors"></a>Rapports d'erreurs
### <a name="session-errors"></a>Erreurs de session
Session erreurs sont généralement utilisés tooreport hello affecter l’utilisateur de hello lors de sa session.

**Exemple :**

            /** hello user has entered invalid data in a form */
            public MyActivity extends EngagementActivity {
              [...]
              public void onMyFormSubmitted(MyForm form) {
                [...]
                /* hello user has entered an invalid email address */
                getEngagementAgent().sendSessionError("sign_up_email", null);
                [...]
              }
              [...]
            }

### <a name="standalone-errors"></a>Erreurs autonomes
Erreurs de toosession contraires, autonome erreurs peuvent se produire en dehors du contexte hello d’une session.

**Exemple :**

Hello suivant montre comment tooreport une erreur chaque fois que la mémoire de hello devient faible sur le téléphone hello lors de l’exécution de votre application est en cours d’exécution.

            public MyApplication extends EngagementApplication {

              @Override
              protected void onApplicationProcessLowMemory() {
                EngagementAgent.getInstance(this).sendError("low_memory", null);
              }
            }

## <a name="reporting-jobs"></a>Rapports de travaux
### <a name="example"></a>Exemple
Supposons que vous voulez tooreport hello la durée de votre processus de connexion :

            [...]
            public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has started */
              engagementAgent.startJob("sign_in", null);

              [... sign in ...]

              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="report-errors-during-a-job"></a>Signaler les erreurs lors d'un travail
Les erreurs peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.

**Exemple :**

Supposons que vous vouliez tooreport une erreur au cours de vous connecter processus :

[...] public void signIn(Context context, ...) {

              /* We need an Android context toocall hello Engagement API, if you are extending Activity, Service, you can pass "this" */
              EngagementAgent engagementAgent = EngagementAgent.getInstance(context);

              /* Report sign in job has been started */
              engagementAgent.startJob("sign_in", null);

              /* Try toosign in */
              while(true)
                try {
                  trySignin();
                  break;
                }
                catch(Exception e) {
                  /* Report hello error tooEngagement */
                  engagementAgent.sendJobError("sign_in_error", "sign_in", null);

                  /* Retry after a moment */
                  sleep(2000);
                }
              [...]
              /* Report sign in job is now ended */
              engagementAgent.endJob("sign_in");
            }
            [...]

### <a name="reporting-events-during-a-job"></a>Rapports d'événements pendant une tâche
Les événements peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.

**Exemple :**

Supposons que nous disposons d’un réseau social, nous utilisons un temps total hello tooreport travail pendant le hello utilisateur est connecté toohello server. utilisateur de Hello peut rester connecté en arrière-plan même quand il utilise une autre application ou lorsque le téléphone de hello est en veille, donc il n’existe aucune session.

Hello peuvent recevoir des messages de ses amis, il s’agit d’un événement de tâche.

            [...]
            public void signin(Context context, ...) {
              [...Sign in code...]
              EngagementAgent.getInstance(context).startJob("connection", null);
            }
            [...]
            public void signout(Context context) {
              [...Sign out code...]
              EngagementAgent.getInstance(context).endJob("connection");
            }
            [...]
            public void onMessageReceived(Context context) {
              [...Notify in status bar...]
              EngagementAgent.getInstance(context).sendJobEvent("message_received", "connection", null);
            }
            [...]

## <a name="extra-parameters"></a>Paramètres supplémentaires
Données arbitraires peuvent être attachés tooevents, les erreurs, les activités et les tâches.

Ces données peuvent être structurées, elles utilisent la classe Bundle d'Android (en fait, elles font office de paramètres extras dans les Intents Android). Notez qu'une classe Bundle peut contenir des tableaux ou d'autres instances de classe Bundle.

> [!IMPORTANT]
> Si vous placez dans les paramètres parcelable ou sérialisables, vérifiez que leurs `toString()` méthode est implémentée tooreturn une chaîne contrôlable de visu. Les classes sérialisables qui contiennent des champs non temporaires non sérialisables entraînent le blocage d'Android à l'appel de `bundle.putSerializable("key",value);`
> 
> [!WARNING]
> Les matrices creuses dans les paramètres extras ne sont pas prises en charge, autrement dit, elles ne sont pas sérialisées sous forme de tableau. Vous devez les convertir en tableaux standard avant de les utiliser dans les paramètres extras.
> 
> 

### <a name="example"></a>Exemple
            Bundle extras = new Bundle();
            extras.putString("video_id", 123);
            extras.putString("ref_click", "http://foobar.com/blog");
            EngagementAgent.getInstance(context).sendEvent("video_clicked", extras);

### <a name="limits"></a>Limites
#### <a name="keys"></a>Clés
Chaque clé Bonjour `Bundle` doit correspondre à hello expression régulière suivante :

`^[a-zA-Z][a-zA-Z_0-9]*`

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="size"></a>Taille
Fonctionnalités supplémentaires sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par le service d’Engagement hello).

Bonjour exemple précédent, hello JSON envoyé toohello serveur est 58 caractères :

            {"ref_click":"http:\/\/foobar.com\/blog","video_id":"123"}

## <a name="reporting-application-information"></a>Rapports d'informations sur l'application
Vous pouvez signaler manuellement le suivi des informations (ou toutes les autres informations spécifiques aux applications) à l’aide de hello `sendAppInfo()` (fonction).

Notez que ces informations peuvent être envoyées de façon incrémentielle : uniquement hello valeur la plus récente d’une clé spécifique est conservé pour un périphérique donné.

Comme événement extras, hello classe de regroupement est utilisée tooabstract informations de l’application, notez que les tableaux ou inférieur regroupe sera traité en tant que chaînes plats (à l’aide de la sérialisation JSON).

### <a name="example"></a>Exemple
Voici un sexe de l’utilisateur toosend exemple code et la date de naissance :

            Bundle appInfo = new Bundle();
            appInfo.putString("status", "premium");
            appInfo.putString("expiration", "2016-12-07"); // December 7th 2016
            EngagementAgent.getInstance(context).sendAppInfo(appInfo);

### <a name="limits"></a>limites
#### <a name="keys"></a>Clés
Chaque clé Bonjour `Bundle` doit correspondre à hello expression régulière suivante :

`^[a-zA-Z][a-zA-Z_0-9]*`

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="size"></a>Taille
Informations sur l’application sont trop limitées**1024** caractères par appel (une fois encodées au format JSON par le service d’Engagement hello).

Bonjour exemple précédent, hello JSON envoyé toohello serveur est 44 caractères :

            {"expiration":"2016-12-07","status":"premium"}
