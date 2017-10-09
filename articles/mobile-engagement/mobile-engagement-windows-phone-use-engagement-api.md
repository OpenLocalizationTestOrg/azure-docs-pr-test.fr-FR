---
title: aaaHow tooUse hello API Engagement sur Windows Phone Silverlight
description: Comment tooUse hello API Engagement sur Windows Phone Silverlight
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: 
ms.assetid: ae2ba2e8-f75b-4dee-a164-a7dd65d35a23
ms.service: mobile-engagement
ms.workload: mobile
ms.tgt_pltfrm: mobile-windows-phone
ms.devlang: na
ms.topic: article
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 1e84be95cc910be7f1227b4ae60eb483a1939284
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-engagement-api-on-windows-phone-silverlight"></a>Comment tooUse hello API Engagement sur Windows Phone Silverlight
Ce document est un document toohello de module complémentaire [comment toointegrate Mobile Engagement dans votre application Windows Phone Silverlight](mobile-engagement-windows-phone-integrate-engagement.md). Elle fournit en profondeur plus d’informations sur comment toouse hello Engagement API tooreport vos statistiques de l’application.

Si vous souhaitez seulement Engagement tooreport sessions, activités, blocages et des informations techniques de votre application, puis hello la plus simple est de façon toomake tous les votre `PhoneApplicationPage` sous-classes héritent hello `EngagementPage` classe.

Si vous voulez toodo plus, par exemple, si vous avez besoin tooreport les événements d’application spécifique, les erreurs et les tâches, ou si vous avez tooreport activités de votre application d’une manière différente d’une implémentation dans hello hello `EngagementPage` des classes, vous devez toouse hello API d’engagement.

API d’Engagement Hello est fournie par hello `EngagementAgent` classe. Vous pouvez accéder à des méthodes toothose via `EngagementAgent.Instance`.

Même si le module de l’agent hello n’a pas été initialisée, chaque API de toohello d’appel est différée et sera exécutée à nouveau lorsque l’agent de hello n’est disponible.

## <a name="engagement-concepts"></a>Concepts liés à Engagement
Hello pièces suivantes affiner les Concepts d’Engagement Mobile hello pour la plateforme Windows Phone de hello.

### <a name="session-and-activity"></a>`Session` et `Activity`
Un *activité* est généralement associé à une page de l’application hello, qui est toosay hello *activité* démarre lorsque la page de hello et s’arrête lorsque la page de hello est fermé : il s’agit des cas hello si hello Engagement SDK est intégré à l’aide de hello `EngagementPage` classe.

Mais *activités* peut également être contrôlée manuellement à l’aide des API de l’Engagement de hello. Cela permet à une page donnée toosplit dans plusieurs tooget de parties sub plus de détails sur hello d’utilisation de cette page (par exemple tooknown la fréquence et la durée pendant laquelle les boîtes de dialogue sont utilisés à l’intérieur de cette page).

## <a name="reporting-activities"></a>Rapports d'activités
### <a name="user-starts-a-new-activity"></a>L'utilisateur démarre une nouvelle activité
#### <a name="reference"></a>Référence
            void StartActivity(string name, Dictionary<object, object> extras = null)

Vous devez toocall `StartActivity()` chaque activité utilisateur hello change. Hello premier appel toothis fonction démarre une nouvelle session de l’utilisateur.

> [!IMPORTANT]
> Hello SDK appelle automatiquement la méthode de EndActivity hello lors de la fermeture de l’application hello. Par conséquent, il est vivement recommandé toocall hello StartActivity (méthode) chaque fois que l’activité hello de modification d’utilisateur hello et appel de tooNEVER hello méthode EndActivity, depuis l’appel de cette méthode force hello session active toobe s’est terminée.
> 
> 

#### <a name="example"></a>Exemple
            EngagementAgent.Instance.StartActivity("main", new Dictionary<object, object>() {{"example", "data"}});

### <a name="user-ends-his-current-activity"></a>L'utilisateur met fin à l'activité en cours
#### <a name="reference"></a>Référence
            void EndActivity()

Vous devez toocall `EndActivity()` au moins une fois lorsque hello utilisateur a fini de sa dernière activité. Cela permet d’informer hello SDK Engagement qu’utilisateur de hello est actuellement inactive et que session d’utilisateur hello devez toobe fermés une fois hello expiration de la session expire (si vous appelez `StartActivity()` avant l’expiration du délai d’expiration de session hello, session de hello est simplement la suite).

#### <a name="example"></a>Exemple
            EngagementAgent.Instance.EndActivity();

## <a name="reporting-jobs"></a>Rapports de travaux
### <a name="start-a-job"></a>Démarrer un travail
#### <a name="reference"></a>Référence
            void StartJob(string name, Dictionary<object, object> extras = null)

Vous pouvez utiliser des tâches certains tootrack hello sur une période de temps.

#### <a name="example"></a>Exemple
            // An upload begins...

            // Set hello extras
            var extras = new Dictionary<object, object>();
            extras.Add("title", "avatar");
            extras.Add("type", "image");

            EngagementAgent.Instance.StartJob("uploadData", extras);

### <a name="end-a-job"></a>Mettre fin à un travail
#### <a name="reference"></a>Référence
            void EndJob(string name)

Dès qu’un objet d’un suivi par une tâche a été arrêtée, vous devez appeler la méthode de EndJob hello pour cette tâche, en fournissant le nom de la tâche hello.

#### <a name="example"></a>Exemple
            // In hello previous section, we started an upload tracking with a job
            // Then, hello upload ends

            EngagementAgent.Instance.EndJob("uploadData");

## <a name="reporting-events"></a>Rapports d'événements
Il existe trois types d'événements :

* Événements autonomes
* Événements de session
* Événements de travail

### <a name="standalone-events"></a>Événements autonomes
#### <a name="reference"></a>Référence
            void SendEvent(string name, Dictionary<object, object> extras = null)

Les événements autonome peuvent se produire en dehors du contexte hello d’une session.

#### <a name="example"></a>Exemple
            EngagementAgent.Instance.SendEvent("event", extra);

### <a name="session-events"></a>Événements de session
#### <a name="reference"></a>Référence
            void SendSessionEvent(string name, Dictionary<object, object> extras = null)

Événements de session sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors de sa session.

#### <a name="example"></a>Exemple
**Sans données :**

            EngagementAgent.Instance.SendSessionEvent("sessionEvent");

            // or

            EngagementAgent.Instance.SendSessionEvent("sessionEvent", null);

**Avec données :**

            Dictionary<object, object> extras = new Dictionary<object,object>();
            extras.Add("name", "data");
            EngagementAgent.Instance.SendSessionEvent("sessionEvent", extras);

### <a name="job-events"></a>Événements de travail
#### <a name="reference"></a>Référence
            void SendJobEvent(string eventName, string jobName, Dictionary<object, object> extras = null)

Événements de travail sont des actions de hello tooreport utilisés généralement effectuées par un utilisateur lors d’un travail.

#### <a name="example"></a>Exemple
            EngagementAgent.Instance.SendJobEvent("eventName", "jobName", extras);

## <a name="reporting-errors"></a>Rapports d'erreurs
Il existe trois types d'erreurs :

* Erreurs autonomes
* Erreurs de session
* Erreurs de travail

### <a name="standalone-errors"></a>Erreurs autonomes
#### <a name="reference"></a>Référence
            void SendError(string name, Dictionary<object, object> extras = null)

Erreurs de toosession contraires, autonome erreurs peuvent se produire en dehors du contexte hello d’une session.

#### <a name="example"></a>Exemple
            EngagementAgent.Instance.SendError("errorName", extras);

### <a name="session-errors"></a>Erreurs de session
#### <a name="reference"></a>Référence
            void SendSessionError(string name, Dictionary<object, object> extras = null)

Session erreurs sont généralement utilisés tooreport hello affecter l’utilisateur de hello lors de sa session.

#### <a name="example"></a>Exemple
            EngagementAgent.Instance.SendSessionError("errorName", extra);

### <a name="job-errors"></a>Erreurs de travail
#### <a name="reference"></a>Référence
            void SendJobError(string errorName, string jobName, Dictionary<object, object> extras = null)

Les erreurs peuvent être associée tooa travail au lieu d’être en cours d’exécution liées de session utilisateur en cours toohello.

#### <a name="example"></a>Exemple
            EngagementAgent.Instance.SendJobError("errorName", "jobname", extra);

## <a name="reporting-crashes"></a>Rapports d'incidents
l’agent de Hello fournit deux méthodes toodeal se bloque.

### <a name="send-an-exception"></a>Envoyer une exception
#### <a name="reference"></a>Référence
            void SendCrash(Exception e, bool terminateSession = false)

#### <a name="example"></a>Exemple
Vous pouvez envoyer une exception à tout moment en appelant :

            EngagementAgent.Instance.SendCrash(aCatchedException);

Vous pouvez également utiliser une session d’engagement paramètre facultatif tooterminate hello en hello même temps que l’envoi de panne de hello. Par conséquent, appelez le toodo :

            EngagementAgent.Instance.SendCrash(new Exception("example"), terminateSession: true);

Si vous procédez ainsi, les travaux et la session de hello va être fermée juste après l’envoi d’incident de hello.

### <a name="send-an-unhandled-exception"></a>Envoyer une exception non gérée
#### <a name="reference"></a>Référence
            void SendCrash(ApplicationUnhandledExceptionEventArgs e)

Engagement fournit également une méthode toosend non gérée exceptions. Ceci est particulièrement utile lorsqu’il est utilisé à l’intérieur du Gestionnaire d’événements UnhandledException hello silverlight.

Cette méthode sera **toujours** mettre fin à la session d’engagement hello et des travaux après avoir été appelé.

#### <a name="example"></a>Exemple
Vous pouvez l’utiliser tooimplement votre propre gestionnaire UnhandledException (surtout si vous avez désactivé hello automatique de rapport d’incident fonctionnalité d’Engagement). Par exemple, dans hello `Application_UnhandledException` méthode Hello `App.xaml.cs` fichier :

            // In your App.xaml.cs file

            // Code tooexecute on Unhandled Exceptions
            private void Application_UnhandledException(object sender, ApplicationUnhandledExceptionEventArgs e)
            {
              // your own code

              EngagementAgent.Instance.SendCrash(e);
            }

## <a name="onactivated"></a>OnActivated
### <a name="reference"></a>Référence
            void OnActivated(ActivatedEventArgs e)

Lorsqu’il hello utilisateur navigue vers l’avant, en dehors d’une application, une fois hello désactivé est déclenché, le système d’exploitation de hello tentera application hello de tooput à l’état dormant. Ensuite, application hello est tombstone. Dans ce processus, une application est arrêtée, mais certaines données sur l’état de hello de l’application hello et des pages individuelles hello au sein de l’application hello sont conservées.

Vous avez tooinsert `EngagementAgent.Instance.OnActivated(e)` Bonjour `Application_Activated` méthode Bonjour App.xaml.cs fichier tooreset Bonjour Engagement Agent lors de l’application hello a été désactivé.

### <a name="example"></a>Exemple
            // Inside your App.xaml.cs file

            // Code tooexecute when hello application is activated (brought tooforeground)
            // This code will not execute when hello application is first launched
            private void Application_Activated(object sender, ActivatedEventArgs e)
            {
              EngagementAgent.Instance.OnActivated(e);
            }

## <a name="device-id"></a>ID de périphérique
            String GetDeviceId()

Vous pouvez obtenir l’id d’appareil hello engagement en appelant cette méthode.

## <a name="extras-parameters"></a>Paramètres de suppléments
Données arbitraires peuvent être attachés tooan événement, une erreur, une activité ou une tâche. Ces données peuvent être structurées à l'aide d'un dictionnaire. Les clés et les valeurs peuvent être de n'importe quel type.

Les données de fonctionnalités supplémentaires sont sérialisées afin que si vous souhaitez tooinsert votre propre type de fonctionnalités supplémentaires vous ayez tooadd un contrat de données pour ce type.

### <a name="example"></a>Exemple
Nous créons une classe nommée « Person ».

            using System.Runtime.Serialization;

            namespace Engagement.Agent
            {
              [DataContract]
              public class Person
              {
                public Person(string name, int age)
                {
                  Age = age;
                  Name = name;
                }

                // Properties

                [DataMember]
                public int Age
                {
                  get;
                  set;
                }

                [DataMember]
                public string Name
                {
                  get;
                  set; 
                }
              }
            }

Ensuite, nous allons ajouter un `Person` tooan instance supplémentaire.

            Person person = new Person("Engagement Haddock", 51);
            var extras = new Dictionary<object, object>();
            extras.Add("people", person);

            EngagementAgent.Instance.SendEvent("Event", extras);

> [!WARNING]
> Si vous placez des autres types d’objets, assurez-vous que sa méthode ToString() est implémenté tooreturn une chaîne contrôlable de visu.
> 
> 

### <a name="limits"></a>limites
#### <a name="keys"></a>Clés
Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :

`^[a-zA-Z][a-zA-Z_0-9]*$`

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="size"></a>Taille
Fonctionnalités supplémentaires sont trop limitées**1024** caractères par l’appel.

## <a name="reporting-application-information"></a>Rapports d'informations sur l'application
### <a name="reference"></a>Référence
            void SendAppInfo(Dictionary<object, object> appInfos)

Vous pouvez manuellement signaler le suivi des informations (ou toutes les autres informations spécifiques aux applications à l’aide de la fonction de SendAppInfo() hello).

Notez que ces informations peuvent être envoyées de façon incrémentielle : uniquement hello valeur la plus récente d’une clé spécifique est conservé pour un périphérique donné. Comme l’événement extras, utiliser un dictionnaire\<objet, objet\> tooattach informations.

### <a name="example"></a>Exemple
            Dictionary<object, object> appInfo = new Dictionary<object, object>()
            {
               {"subscription", "2013-12-07"},
               {"premium", "true"}
            };

            EngagementAgent.Instance.SendAppInfo(appInfo);

### <a name="limits"></a>Limites
#### <a name="keys"></a>Clés
Chaque clé de l’objet de hello doit correspondre hello expression régulière suivante :

`^[a-zA-Z][a-zA-Z_0-9]*$`

Cela signifie que les clés doivent commencer par au moins une lettre, suivie de lettres, de chiffres ou de traits de soulignement (\_).

#### <a name="size"></a>Taille
Informations sur l’application sont trop limitées**1024** caractères par l’appel.

Bonjour exemple précédent, hello JSON envoyé toohello serveur est 44 caractères :

            {"subscription":"2013-12-07","premium":"true"}

## <a name="logging"></a>Journalisation
### <a name="enable-logging"></a>Activation de la journalisation
Hello SDK peut être configuré tooproduce des journaux de test dans la console hello IDE.
Ces journaux ne sont pas activés par défaut. toocustomize, propriété hello de mise à jour `EngagementAgent.Instance.TestLogEnabled` tooone de valeur hello disponible à partir de hello `EngagementTestLogLevel` énumération, par exemple :

            EngagementAgent.Instance.TestLogLevel = EngagementTestLogLevel.Verbose;
            EngagementAgent.Instance.Init();
