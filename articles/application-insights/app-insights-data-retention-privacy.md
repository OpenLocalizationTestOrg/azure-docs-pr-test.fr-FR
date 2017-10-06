---
title: "aaaData rétention et stockage dans Azure Application Insights | Documents Microsoft"
description: Retention and privacy policy statement
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: a6268811-c8df-42b5-8b1b-1d5a7e94cbca
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: bwren
ms.openlocfilehash: 7823431d03a57db5268d2724a0604e40666009f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="data-collection-retention-and-storage-in-application-insights"></a>Collecte, rétention et stockage des données dans Application Insights


Lorsque vous installez [Azure Application Insights] [ start] SDK dans votre application, il envoie la télémétrie sur votre toohello application Cloud. Naturellement, les développeurs responsables veulent tooknow exactement quelles données sont envoyées, que passe-t-il toohello données et comment ils peuvent conserver le contrôle de celui-ci. Ils souhaitent savoir, plus particulièrement, si les données sensibles peuvent être envoyées, où elles sont stockées et à quel point elles sont sécurisées ? 

Tout d’abord, hello bref :

* les modules de télémétrie standard Hello manquer de « zone de hello » sont service de toohello toosend peu probable que des données sensibles. les données de télémétrie Hello sont concernée par la charge, les métriques de performances et l’utilisation, les rapports d’exception et autres données de diagnostic. données d’utilisateur principal Hello visibles dans les rapports de diagnostic hello sont des URL ; mais votre application ne doit pas placer dans tous les cas les données sensibles en texte brut dans une URL.
* Vous pouvez écrire du code qui envoie les données de télémétrie personnalisées supplémentaires toohelp des diagnostics et de surveiller l’utilisation. (Cette extensibilité est une fonctionnalité intéressante de Application Insights.) Il serait possible, par erreur, toowrite ce code afin qu’il inclue personnel et autres données sensibles. Si votre application fonctionne avec ces données, vous devez appliquer un code attentive processus tooall hello que vous écrivez.
* Lors du développement et test de votre application, il est facile tooinspect qu’envoyé par hello SDK. les données de Hello apparaissent dans les fenêtres du navigateur et hello IDE de sortie de débogage de hello. 
* les données de salutation sont maintenues dans [Microsoft Azure](http://azure.com) serveurs hello États-Unis ou en Europe. (Mais votre application peut s’exécuter n’importe où.) Azure dispose de [processus de sécurité renforcés, il est conforme à une large gamme de normes de conformité](https://azure.microsoft.com/support/trust-center/). Seuls vous et votre équipe ont accès aux données de tooyour. Personnel de Microsoft peut avoir restreint tooit accès uniquement dans certaines circonstances limitées avec votre base de connaissances. Il est chiffré en transit, mais pas dans les serveurs hello.

reste Hello de cet article présente plus en détail ces réponses. Elle a conçu toobe autonome, afin que vous pouvez l’afficher toocolleagues qui ne font pas partie de votre équipe.

## <a name="what-is-application-insights"></a>Présentation d’Application Insights
[Azure Application Insights] [ start] est un service fourni par Microsoft qui vous aident à améliorer les performances de hello et de facilité d’utilisation de votre application en temps réel. Il analyse votre application tout temps hello qu’il est en cours d’exécution, pendant le test et une fois que vous avez publié ou déployé. Application Insights crée des graphiques et des tableaux qui vous montre, par exemple, les heures de la journée, vous obtenez la plupart des utilisateurs, comment est de l’application hello réactive, et des services et qu'il est pris en charge par n’importe quel externe qui il dépend. S’il existe des incidents, les échecs ou les problèmes de performances, vous pouvez rechercher dans les données de télémétrie hello dans la cause de détail toodiagnose hello. Et le service de hello vous enverra des messages électroniques si des modifications sont effectuées dans la disponibilité de hello et les performances de votre application.

Dans commande tooget cette fonctionnalité, vous installez une Application Insights SDK dans votre application, qui devient partie intégrante de son code. Lorsque votre application s’exécute, hello SDK surveille son fonctionnement et envoie le service de télémétrie toohello Application Insights. Il s’agit d’un service cloud hébergé par [Microsoft Azure](http://azure.com). (Mais Application Insights fonctionne pour toutes les applications, pas uniquement celles qui sont hébergées dans Azure.)

![Hello SDK dans votre application envoie la télémétrie toohello service Application Insights.](./media/app-insights-data-retention-privacy/01-scheme.png)

Hello service Application Insights stocke et analyse les données de télémétrie hello. analyse de hello toosee ou parcourez hello stockées télémétrie, vous vous connectez tooyour compte Azure et les ressources d’Application Insights hello ouvert pour votre application. Vous pouvez également partager des données toohello accès avec d’autres membres de votre équipe, ou avec les abonnés Azure spécifiés.

Vous pouvez avoir des données exportées à partir de hello service Application Insights, par exemple les outils de tooa tooexternal ou de la base de données. Vous fournissez une touche spéciale que vous obtenez à partir du service de hello chaque outil. clé de Hello peut être révoqué, si nécessaire. 

Application Insights SDK sont disponibles pour une gamme de types d’applications : les services web hébergés dans vos propres serveurs J2EE ou ASP.NET, ou dans Azure ; clients Web - autrement dit, le code hello en cours d’exécution dans une page web ; applications de bureau et des services ; APPAREIL des applications telles que Windows Phone, iOS et Android. Tous les envoient la télémétrie toohello même service.

## <a name="what-data-does-it-collect"></a>Quelles données collecte-t-il ?
### <a name="how-is-hello-data-is-collected"></a>Comment les données de salutation est collectées ?
Il existe trois sources de données :

* Hello SDK, qui vous intégrez votre application soit [dans le développement](app-insights-asp-net.md) ou [au moment de l’exécution](app-insights-monitor-performance-live-website-now.md). Il existe différents Kits SDK pour différents types d’applications. Il existe également un [Kit de développement logiciel pour les pages web](app-insights-javascript.md), qui charge dans le navigateur hello-l’utilisateur final, ainsi que la page de hello.
  
  * Chaque SDK comporte un certain nombre de [modules](app-insights-configuration-with-applicationinsights-config.md), qui utilisent différentes techniques toocollect différents types de données de télémétrie.
  * Si vous installez hello SDK dans le développement, vous pouvez utiliser ses toosend API vos propres données de télémétrie, dans des modules standards plus toohello. Ces données de télémétrie personnalisée peuvent inclure toutes les données toosend.
* Sur certains serveurs web, il existe également des agents qui s’exécutent en même temps que l’application hello et envoyer la télémétrie sur l’UC, la mémoire et son niveau d’occupation réseau. Par exemple, les machines virtuelles Azure, les hôtes Docker, et [les serveurs J2EE](app-insights-java-agent.md) peuvent disposer de ces agents.
* [Tests de disponibilité](app-insights-monitor-web-app-availability.md) processus exécutés par Microsoft qui envoient des demandes tooyour web app à intervalles réguliers. résultats de Hello sont envoyés de service d’Application Insights toohello.

### <a name="what-kinds-of-data-are-collected"></a>Quel genre de données est collecté ?
les catégories principales Hello sont :

* [La télémétrie du serveur web](app-insights-asp-net.md) : requêtes HTTP.  URI, demande de durée tooprocess hello, le code de réponse, adresse IP du client. L’Id de session.
* [Les pages web](app-insights-javascript.md) : page, utilisateur et décomptes de sessions. Le temps de chargement de page. Les exceptions. Appels Ajax.
* Les performances des compteurs : mémoire, UC, E/S, occupation du réseau.
* Le contexte du client et du serveur : système d’exploitation, paramètres régionaux, type d’appareil, navigateur, résolution d’écran.
* [Les exceptions](app-insights-asp-net-exceptions.md) et les incidents : **vidages de pile**, génération d’id, type d’UC. 
* [Dépendances](app-insights-asp-net-dependencies.md) -appelle tooexternal des services tels que REST, SQL, AJAX. L’URI ou la chaîne de connexion, la durée, la réussite, la commande.
* [Les tests de disponibilité](app-insights-monitor-web-app-availability.md) : durée et étapes du test, réponses.
* [Les journaux de suivi](app-insights-asp-net-trace-logs.md) et [la télémétrie personnalisée](app-insights-api-custom-events-metrics.md) - **tout ce que vous codez dans vos journaux ou télémétrie**.

[Plus de détails](#data-sent-by-application-insights).

## <a name="how-can-i-verify-whats-being-collected"></a>Comment puis-je vérifier ce qui a été collecté ?
Si vous développez une application hello à l’aide de Visual Studio, exécutez l’application hello en mode de débogage (F5). les données de télémétrie Hello s’affiche dans la fenêtre de sortie hello. À partir de là, vous pouvez les copier et les mettre au format JSON pour une inspection facile. 

![](./media/app-insights-data-retention-privacy/06-vs.png)

Il existe également une vue plus lisible dans la fenêtre de Diagnostics hello.

Pour les pages web, ouvrez la fenêtre de débogage de votre navigateur.

![Appuyez sur F12 et ouvrez l’onglet réseau hello.](./media/app-insights-data-retention-privacy/08-browser.png)

### <a name="can-i-write-code-toofilter-hello-telemetry-before-it-is-sent"></a>Puis-je écrire des données de télémétrie code toofilter hello avant d’être envoyée ?
Cela est possible en écrivant un [plug-in de processeur de télémétrie](app-insights-api-filtering-sampling.md).

## <a name="how-long-is-hello-data-kept"></a>Combien de temps donnée hello conservés ?
Points de données brutes (autrement dit, les éléments que vous pouvez interroger dans Analytique et inspecter dans la recherche) sont conservés pour too90 jours. Si vous avez besoin des données tookeep plues, vous pouvez utiliser [exportation continue](app-insights-export-telemetry.md) toocopy il compte de stockage tooa.

Les données agrégées (autrement dit, les nombres, moyennes et autres données statistiques que vous voyez dans Metrics Explorer) sont conservées avec une granularité de 1 minute pendant 90 jours.

## <a name="who-can-access-hello-data"></a>Qui peut accéder à des données de salutation ?
les données de salutation sont visible tooyou et, si vous avez un compte d’organisation, les membres de votre équipe. 

Il peut être exporté par vous et les membres de votre équipe et peut être copié tooother emplacements et passé sur tooother personnes.

#### <a name="what-does-microsoft-do-with-hello-information-my-app-sends-tooapplication-insights"></a>Ce que fait Microsoft faire avec les informations de hello mon application envoie tooApplication Insights ?
Microsoft utilise les données de hello uniquement dans l’ordre tooprovide hello service tooyou.

## <a name="where-is-hello-data-held"></a>Les données de salutation lieu ?
* Dans les États-Unis de hello ou Europe. Vous pouvez sélectionner les emplacement hello lorsque vous créez une nouvelle ressource Application Insights. 


#### <a name="does-that-mean-my-app-has-toobe-hosted-in-hello-usa-or-europe"></a>Cela signifie-t-il que mon application a toobe hébergé Bonjour USA ou Europe ?
* Non. Votre application peut s’exécuter n’importe où, dans votre propre hôtes locaux ou Bonjour Cloud.

## <a name="how-secure-is-my-data"></a>Mes données sont-elles sécurisées ?
Application Insights est un service Azure. Stratégies de sécurité sont décrites dans hello [livre blanc Azure sécurité, confidentialité et la conformité](http://go.microsoft.com/fwlink/?linkid=392408).

les données de salutation sont stockées dans les serveurs Microsoft Azure. Pour les comptes Bonjour portail Azure, les restrictions de compte sont décrites dans hello [document Azure sécurité, confidentialité et la conformité](http://go.microsoft.com/fwlink/?linkid=392408).

Accéder aux données de tooyour par le personnel de Microsoft est limitée. Nous avons accès à vos données uniquement avec l’autorisation et, si nécessaire toosupport votre utilisation des Application Insights. 

Les données en bloc entre les applications tous nos clients (par exemple, des débits de données et la taille moyenne des traces) sont utilisé tooimprove Application Insights.

#### <a name="could-someone-elses-telemetry-interfere-with-my-application-insights-data"></a>Les données de télémétrie d’une autre personne peuvent-elles interférer avec mes données d’Application Insights ?
Ils pourrait envoyer compte tooyour de télémétrie supplémentaires à l’aide de clé d’instrumentation hello, qui se trouve dans le code hello de vos pages web. Avec suffisamment de données supplémentaires, vos mesures ne représentent pas correctement les performances et l’utilisation de votre application.

Si vous partagez le code avec d’autres projets, n’oubliez pas tooremove votre clé d’instrumentation.

## <a name="is-hello-data-encrypted"></a>Les données de salutation sont chiffrées ?
Pas à l’intérieur des serveurs hello à l’heure actuelle.

Toutes les données sont chiffrées lors de leurs déplacements entre les centres de données.

#### <a name="is-hello-data-encrypted-in-transit-from-my-application-tooapplication-insights-servers"></a>Les données de salutation sont chiffrées en transit à partir de serveurs de Insights tooApplication de mon application ?
Oui, nous utilisons le portail de toohello toosend données https à partir de presque tous les kits de développement logiciel, y compris les serveurs web, les appareils et des pages web HTTPS. Hello seule exception concerne les données envoyées à partir des pages web HTTP brut. 

## <a name="personally-identifiable-information"></a>Informations d’identification personnelle
#### <a name="could-personally-identifiable-information-pii-be-sent-tooapplication-insights"></a>Impossible d’informations personnellement identifiables (PII) envoyées tooApplication Insights ?
Oui, c’est possible. 

En règle générale :

* La plupart des données de télémétrie standard (à savoir toute télémétrie envoyée sans que n’ayez écrit de code) ne comprennent pas d’informations explicites. Toutefois, il peut être individuals tooidentify possibles par inférence à partir d’une collection d’événements.
* Les messages d’exception et les messages de suivi peuvent contenir des informations personnelles
* Télémétrie personnalisée - autrement dit, les appels tels que TrackEvent que vous écrivez dans le code à l’aide de hello API ou journal des traces - peut contenir les données que vous choisissez.

table Hello à fin hello de ce document contient des descriptions plus détaillées des données hello collectées.

#### <a name="am-i-responsible-for-complying-with-laws-and-regulations-in-regard-toopii"></a>Suis-je responsable pour se conformer aux lois et réglementations en tenir compte tooPII ?
Oui. Il s’agit de votre tooensure de responsabilité qui collecte de hello et utilisation des données de salutation est conforme aux lois et réglementations et avec les conditions de hello Microsoft Online Services.

Vous devez informer vos clients correctement votre application collecte les données de salutation et utilisation des données de hello.

#### <a name="can-my-users-turn-off-application-insights"></a>Mes utilisateurs peuvent-ils désactiver Application Insights ?
Pas directement. Nous ne fournissent pas un commutateur que vos utilisateurs peuvent fonctionner tooturn off Application Insights.

Toutefois, vous pouvez implémenter cette fonctionnalité dans votre application. Hello tous les kits de développement incluent un paramètre de l’API qui désactive la collecte de données de télémétrie. 

#### <a name="my-application-is-unintentionally-collecting-sensitive-information-can-application-insights-scrub-this-data-so-it-isnt-retained"></a>Mon application collecte involontairement des informations sensibles. Est-ce qu’Application Insights peut nettoyer ces données afin qu’elles ne soient pas conservées ?
Application Insights ne filtre pas les données et ne les supprime pas non plus. Vous devez gérer les données de salutation appropriée et éviter d’envoyer ce tooApplication données Insights.

## <a name="data-sent-by-application-insights"></a>Données envoyées par Application Insights
Kits de développement logiciel Hello varient entre les plateformes et il existe plusieurs composants que vous pouvez installer. (Consultez trop[Application Insights - vue d’ensemble][start].) Chaque composant envoie des données différentes.

#### <a name="classes-of-data-sent-in-different-scenarios"></a>Classes de données envoyées dans différents scénarios
| Votre action | Classes de données collectées (voir tableau suivant) |
| --- | --- |
| [Ajouter un projet de web Application Insights SDK tooa .NET][greenbrown] |ServerContext<br/>Inferred<br/>Perf counters<br/>Requêtes<br/>**Exceptions**<br/>Session<br/>users |
| [Installer Status Monitor sur IIS][redfield] |Dépendances<br/>ServerContext<br/>Inferred<br/>Perf counters |
| [Ajouter Application Insights SDK d’application web Java tooa][java] |ServerContext<br/>Inferred<br/>Requête<br/>Session<br/>users |
| [Ajouter une page de tooweb SDK JavaScript][client] |ClientContext  <br/>Inferred<br/>Page<br/>ClientPerf<br/>Ajax |
| [Définir les propriétés par défaut][apiproperties] |**Propriétés** sur tous les événements standard et personnalisés |
| [Appeler TrackMetric][api] |Valeurs numériques<br/>**Propriétés** |
| [Appeler Track*][api] |Nom de l'événement<br/>**Propriétés** |
| [Appeler TrackException][api] |**Exceptions**<br/>Vidage de pile<br/>**Propriétés** |
| Le Kit SDK ne peut pas collecter les données. Par exemple : <br/> - impossible d’accéder aux compteurs de performances<br/> - exception dans l’initialiseur de télémétrie |SDK diagnostics |

Pour les [Kits de développement logiciel (SDK) des autres plateformes][platforms], consultez les documents correspondants.

#### <a name="hello-classes-of-collected-data"></a>classes de Hello des données collectées
| Classe des données collectées | Comprend (liste non exhaustive) |
| --- | --- |
| **Propriétés** |**Toutes les données - en fonction de votre code** |
| DeviceContext |ID, adresse IP, paramètres régionaux, modèle d’appareil, réseau, type de réseau, nom OEM, résolution d’écran, instance de rôle, nom du rôle, type d’appareil |
| ClientContext  |Système d’exploitation, paramètres régionaux, langue, réseau, résolution de la fenêtre |
| Session |ID de session |
| ServerContext |Nom de l’ordinateur, paramètres régionaux, système d’exploitation, appareil, session utilisateur, contexte utilisateur, opération |
| Inferred |Emplacement géographique à partir de l’adresse IP, horodatage, système d’exploitation, navigateur |
| Mesures |Valeur et nom de la mesure |
| Événements |Valeur et nom de l’événement |
| PageViews |URL et nom de la page ou de l’écran |
| Client perf |URL/nom de la page, temps de chargement du navigateur |
| Ajax |Appels HTTP à partir de la page web tooserver |
| Requests |URL, durée, code de réponse |
| Les dépendances |Type (SQL, HTTP, ...), chaîne de connexion ou URI, synchronisation/désynchronisation, durée, réussite, instruction SQL (avec Status Monitor) |
| **Exceptions** |Type, **message**, piles d’appels, fichier source et numéro ligne, ID du thread |
| Crashes |ID de processus, ID de processus parent, ID de thread d’incident ; correctif de l’application, ID, version ; type d’exception, adresse, motif ; symboles et enregistrements masqués, adresses binaires de début et de fin, nom et chemin du fichier binaire, type de processeur |
| Trace |**Message** et niveau de gravité |
| Perf counters |Temps processeur, mémoire disponible, taux de demande, taux d’exception, octets privés du processus, taux d’E/S, durée de la demande, longueur de file d’attente de la demande |
| Availability |Code de réponse de test web, durée de chaque étape de test, nom de test, horodatage, réussite, temps de réponse, emplacement de test |
| SDK diagnostics |Message de suivi ou exception |

Vous pouvez [désactiver certaines données de hello en modifiant ApplicationInsights.config][config]

## <a name="credits"></a>Crédits
Ce produit contient des données GeoLite2 créées par MaxMind, disponible sur [http://www.maxmind.com](http://www.maxmind.com).



<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[apiproperties]: app-insights-api-custom-events-metrics.md#properties
[client]: app-insights-javascript.md
[config]: app-insights-configuration-with-applicationinsights-config.md
[greenbrown]: app-insights-asp-net.md
[java]: app-insights-java-get-started.md
[platforms]: app-insights-platforms.md
[pricing]: http://azure.microsoft.com/pricing/details/application-insights/
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md

