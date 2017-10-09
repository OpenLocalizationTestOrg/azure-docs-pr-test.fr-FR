---
title: "aaaOffline de synchronisation des données dans les applications mobiles Azure | Documents Microsoft"
description: "Référence conceptuel et vue d’ensemble de la fonctionnalité de synchronisation des données hors connexion hello pour les applications mobiles Azure"
documentationcenter: windows
author: ggailey777
manager: syntaxc4
editor: 
services: app-service\mobile
ms.assetid: 982fb683-8884-40da-96e6-77eeca2500e3
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/30/2016
ms.author: glenga
ms.openlocfilehash: 58673240ba433651faf1f619ca5da33dd6459d2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="offline-data-sync-in-azure-mobile-apps"></a>Synchronisation des données hors connexion dans Azure Mobile Apps
## <a name="what-is-offline-data-sync"></a>Qu’est-ce que la synchronisation des données hors connexion ?
Synchronisation des données hors connexion est un client et serveur de fonctionnalité SDK des applications mobiles Azure qui permet de facilement pour les applications toocreate les développeurs qui fonctionne sans connexion réseau.

Lorsque votre application est en mode hors connexion, vous pouvez toujours créer et modifier des données, qui sont enregistrées magasin local de tooa. Lors de l’application hello est remis en ligne, il peut synchroniser les modifications locales avec votre serveur principal de l’application Mobile Azure. fonctionnalité de Hello inclut également la prise en charge pour la détection des conflits lorsque hello même enregistrement est modifié sur les deux hello client et hello back-end. Conflits peuvent ensuite être traitées sur le serveur de hello ou client de hello.

La synchronisation hors connexion présente plusieurs avantages :

* Améliorer la réactivité de l’application en mettant en cache les données du serveur local sur le périphérique de hello
* Créer des applications robustes qui demeurent opérationnelles en cas de problèmes réseau
* Autoriser toocreate des utilisateurs finaux et de modifier les données même s’il n’existe pas d’accès réseau, prise en charge des scénarios avec peu ou pas de connectivité
* Synchroniser des données entre plusieurs appareils et de détecter les conflits hello même enregistrement est modifié par deux périphériques
* Limiter l’utilisation du réseau sur les réseaux à forte latence ou limités

Hello suivant didacticiels montrent tooadd hors connexion de la synchronisation des clients mobiles tooyour à l’aide des applications mobiles Azure :

* [Android : activer la synchronisation hors connexion]
* [Apache Cordova : activer la synchronisation hors connexion](app-service-mobile-cordova-get-started-offline-data.md)
* [iOS : activer la synchronisation hors connexion]
* [Xamarin iOS : activer la synchronisation hors connexion]
* [Xamarin Android : activer la synchronisation hors connexion]
* [Xamarin.Forms : activer la synchronisation hors connexion](app-service-mobile-xamarin-forms-get-started-offline-data.md)
* [Plateforme Windows universelle : activer la synchronisation hors connexion]

## <a name="what-is-a-sync-table"></a>Qu’est-ce qu’une table de synchronisation ?
tooaccess hello point de terminaison « / tables », hello Azure Mobile client SDK fournit des interfaces telles que `IMobileServiceTable` (Kit de développement logiciel du client .NET) ou `MSTable` (client d’iOS). Ces API vous connecter directement principal de l’application Mobile Azure toohello et échoue si l’appareil de hello client n’a pas d’une connexion réseau.

toosupport hors connexion, votre application doit plutôt utiliser hello *table de synchronisation* API, telles que `IMobileServiceSyncTable` (Kit de développement logiciel du client .NET) ou `MSSyncTable` (client d’iOS). Hello tous les mêmes opérations CRUD (création, lecture, mise à jour, suppression) fonctionnent avec la synchronisation des API de table, à la différence près qu’ils lisent ou d’écriture tooa *magasin local*. Avant de pouvoir effectuer toutes les opérations de table de synchronisation, le magasin local de hello doit être initialisé.

## <a name="what-is-a-local-store"></a>Qu’est-ce qu’un magasin local ?
Un magasin local est la couche de persistance des données hello sur hello client. client d’applications mobiles Azure Hello kits de développement logiciel fournissent une valeur par défaut local stocker l’implémentation. Dans Windows, Xamarin et Android, cette implémentation est basée sur SQLite. Sur iOS, la solution fonctionne sur les données de base.

toouse hello SQLite implémentation basée sur Windows Phone ou Windows Store 8.1, vous devez tooinstall une extension de SQLite. Pour plus d’informations, voir [Plateforme Windows universelle : activer la synchronisation hors connexion]. Android et iOS sont fournis avec une version de SQLite périphérique hello système d’exploitation lui-même, il n’est pas nécessaire tooreference votre propre version de SQLite.

Les développeurs peuvent également implémenter leur propre magasin local. Par exemple, si vous le souhaitez toostore données dans un format chiffré sur les clients mobiles hello, vous pouvez définir un magasin local qui utilise SQLCipher pour le chiffrement.

## <a name="what-is-a-sync-context"></a>Qu’est-ce qu’un contexte de synchronisation ?
Un *contexte de synchronisation* est associé à un objet client mobile (comme `IMobileServiceClient` ou `MSClient`) et effectue le suivi des modifications apportées avec les tables de synchronisation. contexte de synchronisation Hello conserve un *file d’attente de l’opération*, envoyer toohello serveur qui conserve une liste triée des opérations CUD (Create, Update, Delete) qui est plus récente.

Un magasin local est associé avec le contexte de synchronisation hello à l’aide d’une méthode d’initialisation comme `IMobileServicesSyncContext.InitializeAsync(localstore)` Bonjour [le client .NET SDK].

## <a name="how-sync-works"></a>Fonctionnement de la synchronisation hors connexion
Quand vous utilisez des tables de synchronisation, votre code client détermine à quel moment les modifications locales sont synchronisées avec une application principale Azure Mobile App. Rien n’est envoyé toohello principal jusqu'à ce qu’un appel trop*push* modifications locales. De même, magasin local de hello est remplie avec les nouvelles données uniquement s’il existe un appel trop*extraction* données.

* **Push**: par émission de données est une opération sur le contexte de synchronisation hello et envoie toutes les modifications CUD depuis le push de dernière hello. Notez qu’il est toosend n’est pas possible que des modifications d’une table individuelle, car sinon opérations a pu être envoyées de manière désordonnées. Par émission de données exécute une série de REST appels tooyour Azure Mobile service principal d’application, qui à son tour modifie votre base de données du serveur.
* **Extraire**: extraction est effectuée sur une base par table et peut être personnalisé avec un tooretrieve de requête uniquement un sous-ensemble de données du serveur hello. Hello client d’Azure Mobile kits de développement logiciel, puis insérez les données résultantes hello magasin local de hello.
* **Push implicite**: si une extraction est exécutée sur une table qui est en attente de mises à jour locales, par extraction de données hello exécute d’abord un `push()` sur le contexte de synchronisation hello. Cette commande permet de réduire les conflits entre les modifications qui sont déjà en file d’attente et de nouvelles données à partir du serveur de hello.
* **Synchronisation incrémentielle**: hello premier paramètre toohello par extraction de données n’est pas un *nom de la requête* qui est utilisé uniquement sur les clients hello. Si vous utilisez un nom de requête de non null, hello Kit de développement Azure Mobile effectue un *synchronisation incrémentielle*. Chaque fois qu’une opération d’extraction retourne un jeu de résultats, hello dernières `updatedAt` horodatage à partir de ce jeu de résultats est stocké dans les tables de hello Kit de développement logiciel système local. Les opérations d’extraction ultérieures n’extraient que les enregistrements postérieurs à cet horodatage.

  la synchronisation incrémentielle toouse votre serveur doit retourner explicite `updatedAt` les valeurs et doit également prendre en charge le tri par ce champ. Toutefois, étant donné que hello Kit de développement logiciel ajoute son propre tri sur le champ d’updatedAt hello, vous ne pouvez pas utiliser une requête de tirage possède son propre `orderBy` clause.

  nom de la requête Hello peut être toute chaîne que vous choisissez, mais il doit être unique pour chaque requête logique dans votre application.
  Sinon, les opérations d’extraction différents peuvent remplacer hello même horodatage de la synchronisation incrémentielle et de vos requêtes peuvent retourner des résultats incorrects.

  Si la requête de hello possède un paramètre, une façon toocreate un nom de requête unique est la valeur du paramètre tooincorporate hello.
  Par exemple, si vous filtrez sur le nom d’utilisateur, le nom de votre requête peut être le suivant (en C#) :

        await todoTable.PullAsync("todoItems" + userid,
            syncTable.Where(u => u.UserId == userid));

  Si vous souhaitez tooopt hors synchronisation incrémentielle, passez `null` comme hello ID de requête. Dans ce cas, tous les enregistrements sont récupérées à chaque appel trop`PullAsync`, qui est potentiellement inefficace.
* **Purge**: vous pouvez effacer le contenu de hello d’à l’aide du magasin local hello `IMobileServiceSyncTable.PurgeAsync`.
  Purge peut être nécessaire si vous avez des données obsolètes dans la base de données client hello, ou si vous le souhaitez toodiscard toutes les modifications en attente.

  Une purge efface une table à partir du magasin local de hello. S’il n’y en attente d’une synchronisation avec la base de données de serveur hello, lève une exception de purge hello une exception, sauf si des opérations hello *Forcer purge* paramètre est défini.

  Un exemple de données obsolètes sur le client de hello, supposons que dans l’exemple de « liste de tâches » hello, appareil1 extrait uniquement les éléments qui ne sont pas terminées. Un objet todoitem « Acheter du lait » est marquée effectué sur le serveur de hello par un autre périphérique. Toutefois, appareil1 a toujours hello todoitem de « Acheter du lait » dans le magasin local, car il collecte uniquement les éléments qui ne sont pas marquée comme terminée. Une purge efface cet élément obsolète.

## <a name="next-steps"></a>Étapes suivantes
* [iOS : activer la synchronisation hors connexion]
* [Xamarin iOS : activer la synchronisation hors connexion]
* [Xamarin Android : activer la synchronisation hors connexion]
* [Plateforme Windows universelle : activer la synchronisation hors connexion]

<!-- Links -->
[le client .NET SDK]: app-service-mobile-dotnet-how-to-use-client-library.md
[Android : activer la synchronisation hors connexion]: app-service-mobile-android-get-started-offline-data.md
[iOS : activer la synchronisation hors connexion]: app-service-mobile-ios-get-started-offline-data.md
[Xamarin iOS : activer la synchronisation hors connexion]: app-service-mobile-xamarin-ios-get-started-offline-data.md
[Xamarin Android : activer la synchronisation hors connexion]: app-service-mobile-xamarin-android-get-started-offline-data.md
[Plateforme Windows universelle : activer la synchronisation hors connexion]: app-service-mobile-windows-store-dotnet-get-started-offline-data.md
