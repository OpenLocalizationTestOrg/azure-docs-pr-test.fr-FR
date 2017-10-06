---
title: "disponibilité d’aaaMonitor et la réactivité d’un site web | Documents Microsoft"
description: "Configurez des tests web dans Application Insights. Recevez des alertes si un site web devient indisponible ou répond lentement."
services: application-insights
documentationcenter: 
author: SoubhagyaDash
manager: carmonm
ms.assetid: 46dc13b4-eb2e-4142-a21c-94a156f760ee
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/25/2017
ms.author: bwren
ms.openlocfilehash: 4c5425c948770cc57a648ca50e217c75ac75fbd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-availability-and-responsiveness-of-any-web-site"></a>Analyse de la disponibilité et de la réactivité d'un site Web
Une fois que vous avez déployé votre application web ou un serveur de site web tooany, vous pouvez définir des tests toomonitor sa disponibilité et la réactivité. [Azure Application Insights](app-insights-overview.md) envoie des requêtes web tooyour application à intervalles réguliers à partir des points autour de Bonjour. et vous alerte si votre application réagit lentement ou pas du tout.

Vous pouvez définir des tests de disponibilité pour n’importe quel HTTP ou point de terminaison HTTPS est accessible à partir de hello internet public. Vous n’avez tooadd tout site web de toohello que vous testez. Il n’a même pas toobe votre site : vous pouvez tester un service de l’API REST sur lequel vous en avez besoin.

Il existe deux types de tests de disponibilité :

* [Test ping d’URL](#create): un simple test que vous pouvez créer dans hello portail Azure.
* [Test web de multi-step](#multi-step-web-tests): que vous créez dans Visual Studio Enterprise et téléchargement toohello portal.

Vous pouvez créer des tests de disponibilité too25 par la ressource d’application.

## <a name="create"></a>1. Ouvrir une ressource pour vos rapports de test de disponibilité

**Si vous avez déjà configuré Application Insights** pour votre application web, ouvrez sa ressource Application Insights Bonjour [portail Azure](https://portal.azure.com).

**Ou, si vous souhaitez toosee vos rapports dans une nouvelle ressource,** inscrire trop[Microsoft Azure](http://azure.com), accédez toohello [portail Azure](https://portal.azure.com)et créez une ressource Application Insights.

![New > Application Insights](./media/app-insights-monitor-web-app-availability/11-new-app.png)

Cliquez sur **toutes les ressources** Panneau de vue d’ensemble tooopen hello pour la ressource hello.

## <a name="setup"></a>2. Créer un test Ping d’URL
Ouvrez le panneau de disponibilité hello et ajouter un test.

![Remplissage hello au moins l’URL de votre site Web](./media/app-insights-monitor-web-app-availability/13-availability.png)

* **URL de Hello** peut être n’importe quelle page web souhaité tootest, mais il doit être visible à partir de hello internet public. URL de Hello peut inclure une chaîne de requête. Vous pouvez donc, par exemple, tester un peu votre base de données. Si les URL hello résout tooa redirection, nous le suivre des redirections de too10.
* **Analyser les requêtes dépendantes**: Si cette option est activée, les demandes de test de hello images, les scripts, les fichiers de style et les autres fichiers qui font partie de la page web de hello sous test. Hello enregistrées temps de réponse comprend hello durée tooget ces fichiers. test de Hello échoue si toutes ces ressources ne peut pas être téléchargés avec succès au sein de délai d’attente hello pour l’ensemble de l’essai hello. 

    Si l’option de hello n’est pas activée, les tests hello demande seulement fichier hello à l’URL de hello spécifiée.
* **Activer de nouvelles tentatives**: Si cette option est activée, en cas d’échec du test de hello, elle est relancée après un court intervalle. L’échec est signalé uniquement après trois tentatives infructueuses. Les tests suivants sont ensuite exécutées à la fréquence de test habituel hello. Nouvelle tentative est temporairement suspendue tant que réussite suivant de hello. Cette règle est appliquée indépendamment à chaque emplacement de test. Nous recommandons cette option. En moyenne, environ 80 % des échecs disparaissent lors de la nouvelle tentative.
* **Fréquence de test**: définit la fréquence à laquelle hello test est exécuté à partir de chaque emplacement de test. Avec une fréquence de 5 minutes et 5 emplacements de test, votre site sera testé en moyenne une fois par minute.
* **Emplacements de test** sont hello place où nos serveurs d’envoient des URL tooyour de demandes web. Choisissez-en plusieurs de façon à distinguer les problèmes de votre site web des problèmes de réseau. Vous pouvez sélectionner les emplacements de too16.
* **Critères de réussite**:

    **Délai d’expiration de test**: diminuer cette toobe valeur averti des réponses lentes. test de Hello est comptée comme un échec si les réponses hello à partir de votre site n’ont pas été reçus pendant cette période. Si vous avez sélectionné **analyser les requêtes dépendantes**, puis toutes les hello images, fichiers de style, scripts et autres ressources dépendantes doivent avoir été reçus pendant cette période.

    **Réponse HTTP**: hello a retourné le code d’état qui est considéré comme un succès. 200 est le code hello qui indique qu’une page web normale a été retournée.

    **Correspondance de contenu**: une chaîne telle que « Bienvenue ! Nous vérifions qu’une correspondance exacte respectant la casse est présente dans chaque réponse. Il doit s'agir d'une chaîne standard sans caractère générique. N’oubliez pas les modifications du contenu page avoir tooupdate que s’il.
* **Alertes** sont, par défaut, envoyés tooyou cas de défaillance dans trois emplacements plus de cinq minutes. Une défaillance dans un emplacement est toobe probablement un problème de réseau et pas un problème avec votre site. Mais vous pouvez modifier toobe du seuil hello plus ou moins sensibles et vous pouvez également modification qui hello des messages électroniques doit être envoyée.

    Vous pouvez configurer un [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) qui est appelé lorsqu’une alerte est déclenchée. (Mais notez qu’à l’heure actuelle, les paramètres de requête ne sont pas transmis en tant que propriétés.)

### <a name="test-more-urls"></a>Test d'autres URL
Ajoutez d’autres tests. Par exemple, dans Ajout tootesting votre page d’accueil, vous pouvez vous assurer que votre base de données est en cours d’exécution en testant URL hello pour une recherche.


## <a name="monitor"></a>3. Consulter les résultats des tests de disponibilité

Après quelques minutes, cliquez sur **Actualiser** toosee les résultats de test. 

![Synthèse des résultats sur le panneau d’édition familiale hello](./media/app-insights-monitor-web-app-availability/14-availSummary-3.png)

Hello scatterplot montre des résultats des tests qui ont des détails de l’étape de test de diagnostic dans les exemples de hello. moteur de test Hello stocke le détail de diagnostic pour les tests qui présentent des erreurs. Pour les tests réussis, informations de diagnostic sont stockées pour un sous-ensemble d’exécutions de hello. Placez le curseur sur n’importe quelle hello vert/rouge points toosee hello test timestamp, durée du test, l’emplacement et nom du test. Cliquez sur n’importe quel point dans hello ventilation tracer toosee hello les détails du résultat de test hello.  

Sélectionnez un test particulier, l’emplacement, ou réduire le temps de hello toosee période résultats supplémentaires autour hello période d’intérêt. Utilisez les résultats de toosee de l’Explorateur de recherche à partir de toutes les exécutions, ou des rapports personnalisés Analytique requêtes toorun sur ces données.

Dans les résultats bruts toohello de plus, il existe deux métriques de disponibilité dans Metrics Explorer : 

1. Disponibilité : Pourcentage de tests hello qui ont réussi, sur toutes les exécutions de tests. 
2. Durée du test : durée moyenne du test sur toutes les exécutions de test.

Vous pouvez appliquer des filtres sur le nom du test hello, les tendances de tooanalyze emplacement d’un test particulier et/ou d’emplacement.

## <a name="edit"></a>Examiner et modifier des tests

À partir de la page de résumé hello, sélectionnez un test spécifique. Ici, vous pouvez voir ses résultats spécifiques et le modifier ou le désactiver temporairement.

![Edit or disable a web test](./media/app-insights-monitor-web-app-availability/19-availEdit-3.png)

Vous pourriez toodisable les tests de disponibilité ou de l’alerte hello règles associées lorsque vous effectuez la maintenance de votre service. 

## <a name="failures"></a>Si vous constatez des erreurs
Cliquez sur un point rouge.

![Click a red dot](./media/app-insights-monitor-web-app-availability/open-instance-3.png)


À partir d’un résultat de test de disponibilité, vous pouvez :

* Vérifiez que hello réponse de votre serveur.
* Ouvrez la télémétrie hello envoyée par votre application serveur lors du traitement d’instance des demandes ayant échoué hello.
* Se connecter à un problème ou d’élément de travail de problème de hello tootrack Git ou VSTS. bogue de Hello contiendra un événement toothis de liaison.
* Ouvrez le résultat du test web hello dans Visual Studio.


*Le résultat semble correct, mais une erreur est signalée ?* Vérifiez toutes les images de hello, scripts, feuilles de style et tous les autres fichiers chargés par page de hello. Si un d'entre eux échoue, les tests hello sont signalée comme ayant échoué, même si la page html principal de hello charge OK.

*Aucun élément connexe ?* Si Application Insights est défini pour votre application côté serveur, cela peut être en raison d’un [échantillonnage](app-insights-sampling.md) en cours. 

## <a name="multi-step-web-tests"></a>Tests web à plusieurs étapes
Vous pouvez analyser un scénario qui implique une séquence d'URL. Par exemple, si vous analysez un site Web de ventes, vous pouvez tester que l’ajout d’éléments toohello panier d’achat fonctionne correctement.

> [!NOTE] 
> Les tests web à plusieurs étapes ont un coût. [Mécanisme de tarification](http://azure.microsoft.com/pricing/details/application-insights/).
> 

toocreate un test de plusieurs étape, vous enregistrez le scénario de hello à l’aide de Visual Studio Enterprise et téléchargez hello enregistrement tooApplication Insights. Application Insights relit le scénario de hello à intervalles et vérifie les réponses hello.

> [!NOTE]
> Vous ne pouvez pas utiliser de fonctions codées ni de boucles dans vos tests. test de Hello doit être entièrement contenue dans le script de .webtest hello. Toutefois, vous pouvez utiliser des plug-ins standard.
>

#### <a name="1-record-a-scenario"></a>1. Enregistrement d’un scénario
Utilisez Visual Studio Enterprise toorecord une session web.

1. Créez un projet de test de performance web.

    ![Dans Visual Studio Enterprise edition, créez un projet de modèle de performances de site Web et de Test de charge hello.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-create.png)

 * *Ne pas voir hello de performances de site Web et le modèle de Test de charge ?* - Fermez Visual Studio Enterprise. Ouvrez **le programme d’installation de Visual Studio** toomodify votre installation de Visual Studio Enterprise. Sous **Composants individuels**, sélectionnez **Web Performance and load testing tools** (Outils de test de performance Web et de charge).

2. Ouvrez le fichier de .webtest hello et commencer l’enregistrement.

    ![Ouvrir le fichier de .webtest hello et cliquez sur Enregistrer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-start.png)
3. Hello des actions de l’utilisateur vous souhaitez toosimulate dans votre test : ouvrir votre site Web, ajoutez un panier toohello de produit et ainsi de suite. Ensuite, arrêtez le test.

    ![exécutions de l’enregistreur de test de web de Hello dans Internet Explorer.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-record.png)

    Ne créez pas de scénario long. La limite est de 100 étapes et 2 minutes.
4. Modifiez hello du test :

   * Ajoutez des validations toocheck hello reçu texte et réponse codes.
   * supprimer les interactions superflues. Vous pouvez également supprimer les demandes dépendantes pour les images ou tooad ou le suivi des sites.

     Souvenez-vous que vous ne pouvez modifier un script de test hello - vous ne pouvez pas ajouter du code personnalisé ou appeler d’autres tests web. Ne pas insérer des boucles dans un test de hello. Vous pouvez utiliser des plug-ins de test web standard.
5. Exécuter les tests hello dans toomake Visual Studio qu’elle fonctionne.

    Hello outil web test runner s’ouvre un navigateur web et se répète hello actions enregistrées. Assurez-vous qu’il fonctionne comme prévu.

    ![Dans Visual Studio, ouvrez le fichier de .webtest hello et cliquez sur Exécuter.](./media/app-insights-monitor-web-app-availability/appinsights-71webtest-multi-vs-run.png)

#### <a name="2-upload-hello-web-test-tooapplication-insights"></a>2. Télécharger hello web test tooApplication Insights
1. Dans le portail Application Insights hello, créez un test web.

    ![Dans Panneau de tests web hello, cliquez sur Ajouter.](./media/app-insights-monitor-web-app-availability/16-another-test.png)
2. Sélectionnez le test de plusieurs étape et téléchargez le fichier .webtest de hello.

    ![Sélectionnez test web multi-étapes.](./media/app-insights-monitor-web-app-availability/appinsights-71webtestUpload.png)

    Emplacements de test hello ensemble, la fréquence et paramètres d’alerte Bonjour même façon que pour ping teste.

#### <a name="3-see-hello-results"></a>3. Consultez les résultats de hello

Afficher votre test de résultats et les erreurs dans hello les mêmes tests de façon que par url unique.

En outre, vous pouvez télécharger tooview de résultats de test hello dans Visual Studio.

#### <a name="too-many-failures"></a>Trop d’échecs ?

* Une raison courante de l’échec est que le test hello dure trop longtemps. Le test ne doit pas durer plus de deux minutes.

* N’oubliez pas que toutes les ressources hello d’une page doivent charger correctement pour hello test toosucceed, y compris les scripts, des feuilles de style, des images et ainsi de suite.

* Hello test web doit être entièrement contenu dans le script de .webtest hello : vous ne pouvez pas utiliser fonctions codées dans le test de hello.

### <a name="plugging-time-and-random-numbers-into-your-multi-step-test"></a>Ajout de plug-ins de temps et de nombres aléatoires à votre test à plusieurs étapes
Supposons que vous testiez un outil qui obtient des données temporelles, telles que des actions à partir d’un flux externe. Lorsque vous enregistrez votre test web, vous avez toouse des heures spécifiques, mais les définir comme paramètres de hello de test, StartTime et EndTime.

![Un test web avec des paramètres.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-parameters.png)

Lorsque vous exécutez hello test, vous aimeriez EndTime toobe hello présentent toujours une heure, et StartTime doit être de 15 minutes plus tôt.

Plug-ins de Test Web permettent hello toodo paramétrer fois.

1. Ajoutez un plug-in de test web pour chaque valeur de paramètre variable souhaitée. Dans la barre d’outils de test hello web, choisissez **ajouter un plug-in de Test Web**.

    ![Choisissez Ajouter un plug-in de test web et sélectionnez un type.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugins.png)

    Dans cet exemple, nous utilisons deux instances de hello Date heure un plug-in. Une instance est pour « il y a 15 minutes » et l’autre pour « maintenant ».
2. Ouvrez les propriétés de hello de chaque plug-in. Donnez-lui un nom et la définir toouse hello heure actuelle. Pour l'un d'eux, définissez Ajouter des minutes = -15.

    ![Définissez le nom, utilisez l’heure actuelle et ajouter des minutes.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-parameters.png)
3. Dans les paramètres de test web hello, utilisez {{nom du plug-in}} tooreference un nom de plug-in.

    ![Dans le paramètre de test hello, utilisez {{nom du plug-in}}.](./media/app-insights-monitor-web-app-availability/appinsights-72webtest-plugin-name.png)

À présent, téléchargez votre portail toohello de test. Il utilise les valeurs dynamiques hello sur chaque exécution du test de hello.

## <a name="dealing-with-sign-in"></a>Gestion de la connexion
Si vos utilisateurs se connectent tooyour application, vous disposez de différentes options pour la simulation de connexion afin que vous puissiez tester pages derrière hello connectez-vous. approche Hello que vous utilisez dépend du type hello de sécurité fournie par l’application hello.

Dans tous les cas, vous devez créer un compte dans votre application uniquement pour but de hello du test. Si possible, limitez les autorisations de hello de ce compte de test afin qu’il n’existe aucune possibilité d’affecter des utilisateurs réels des tests web hello.

### <a name="simple-username-and-password"></a>Nom d’utilisateur et mot de passe simples
Enregistrez un test web Bonjour normalement. Supprimez d’abord les cookies

### <a name="saml-authentication"></a>Authentication SAML
Utilisez le plug-in SAML hello n’est disponible pour les tests web.

### <a name="client-secret"></a>Clé secrète client
Si votre application présente un mode de connexion impliquant une clé secrète client, utilisez ce mode. Azure Active Directory (AAD) est un exemple de service fournissant une connexion avec clé secrète client. Dans AAD, question secrète du client hello est hello clé de l’application.

Voici un exemple de test web d’une application web Azure à l’aide d’une clé d’application :

![Exemple de clé secrète client](./media/app-insights-monitor-web-app-availability/110.png)

1. Récupérez le jeton d’ADD à l’aide de la clé secrète client (clé d’application).
2. Extrayez le jeton porteur de la réponse.
3. Appeler des API à l’aide du jeton de support dans l’en-tête d’autorisation hello.

Assurez-vous que test de hello web est un cas client réel, autrement dit, elle possède sa propre application dans AAD - et utiliser ses clientId + l’appkey. Votre service de test a également sa propre application dans AAD : hello appID URI de cette application est répercutée dans hello de tests web dans le champ « ressource » de hello.

### <a name="open-authentication"></a>Authentification ouverte
Comme exemple d’authentification ouverte, citons la connexion avec votre compte Microsoft ou Google. Nombre d’applications qu’utilisez OAuth fournit hello alternative secrète du client, votre première stratégie doit donc être tooinvestigate cette possibilité.

Si votre test doit se connecter à l’aide d’OAuth, l’approche générale de hello est :

* Utilisez un outil comme Fiddler tooexamine hello le trafic entre votre navigateur web, site d’authentification hello et votre application.
* Effectuer deux ou plusieurs connexions à l’aide de différents ordinateurs ou les navigateurs, ou à des intervalles de temps (tooexpire de jetons tooallow).
* En comparant les différentes sessions, identifier le jeton hello retransmis hello l’authentification de site, qui est ensuite transmis de serveur d’applications tooyour après la connexion.
* Enregistrez un test web à l’aide de Visual Studio.
* Paramétrer les jetons de hello, paramètre hello lorsque le jeton de hello est retourné à partir de l’authentificateur de hello et son utilisation dans le site de toohello requête hello.
  (Visual Studio tente de test de hello tooparameterize, mais ne paramétrez pas correctement les jetons hello).


## <a name="performance-tests"></a>Tests de performance
Vous pouvez effectuer un test de charge sur votre site web. Comme test de disponibilité hello, vous pouvez envoyer des demandes simples ou demandes de plusieurs étapes à partir de notre points monde hello. Contrairement à un test de disponibilité, de nombreuses demandes sont envoyées, afin de simuler la présence de plusieurs utilisateurs simultanés.

À partir du Panneau de vue d’ensemble de hello, ouvrez **paramètres**, **des Tests de performances**. Lorsque vous créez un test, vous êtes invité tooconnect tooor créer un compte Visual Studio Team Services.

Lorsque le test de hello est terminée, les temps de réponse et le taux de réussite sont affichés.


![Test de performance](./media/app-insights-monitor-web-app-availability/perf-test.png)

> [!TIP]
> effets de hello tooobserve de test de performances, utilisez [flux Live](app-insights-live-stream.md) et [Profiler](app-insights-profiler.md).
>

## <a name="automation"></a>Automatisation
* [Utilisez tooset de scripts PowerShell d’un test de disponibilité](app-insights-powershell.md#add-an-availability-test) automatiquement.
* Configurez un [webhook](../monitoring-and-diagnostics/insights-webhooks-alerts.md) qui est appelé lorsqu’une alerte est déclenchée.

## <a name="qna"></a>Des questions ? Des problèmes ?
* *Puis-je appeler du code à partir de mon test web ?*

    Non. les étapes de Hello du test de hello doivent être dans le fichier de .webtest hello. Et vous ne pouvez pas appeler d’autres tests web ou utiliser des boucles. En revanche, il existe un certain nombre de plug-ins qui peuvent s’avérer utiles.
* *Le protocole HTTPS est-il pris en charge ?*

    Nous prenons en charge TLS 1.1 et TLS 1.2.
* *Quelle est la différence entre les « tests Web » et les « tests de disponibilité » ?*

    Hello deux termes peut-être être référencée indifféremment. Tests de disponibilité est un terme plus générique ping d’URL unique hello teste également toohello des tests web de plusieurs étapes.
* *Je souhaite que les tests de disponibilité toouse sur notre serveur interne qui s’exécute derrière un pare-feu.*

    Il existe deux solutions possibles :
    
    * Configurer votre pare-feu toopermit les demandes entrantes à partir de hello [de notre site web, les adresses IP des agents de test](app-insights-ip-addresses.md).
    * Écrire votre propre code tooperiodically le test de votre serveur interne. Exécuter du code hello dans un processus en arrière-plan sur un serveur de test derrière votre pare-feu. Le processus de test peut envoyer ses résultats tooApplication Insights à l’aide de [TrackAvailability()](https://docs.microsoft.com/dotnet/api/microsoft.applicationinsights.telemetryclient.trackavailability) API dans le package SDK de noyaux hello. Cela nécessite votre test server toohave sortant accès toohello Application Insights ingestion point de terminaison, mais qui constitue un risque de sécurité beaucoup plus petit qu’alternative hello d’autoriser les demandes entrantes. résultats de Hello n’apparaissent pas dans les panneaux de tests web hello disponibilité, mais il apparaît sous la forme des résultats de disponibilité dans Analytique, la recherche et mesure de l’Explorateur.
* *Le chargement d’un test web multi-étapes échoue*

    La limite de taille est de 300 Ko.

    Les boucles ne sont pas prises en charge.

    Les tests web tooother références ne sont pas pris en charge.

    Les sources de données ne sont pas prises en charge.
* *Mon test à plusieurs étapes ne se termine pas.*

    Chaque test possède une limite de 100 demandes.

    test de Hello est arrêtée si elle s’exécute plu de deux minutes.
* *Comment puis-je exécuter un test avec des certificats clients ?*

    Désolé, ce n’est pas pris en charge.


## <a name="next"></a>Étapes suivantes
[Recherche des journaux de diagnostic][diagnostic]

[Résolution des problèmes][qna]

[Adresses IP d’agents de test web](app-insights-ip-addresses.md)

<!--Link references-->

[azure-availability]: ../insights-create-web-tests.md
[diagnostic]: app-insights-diagnostic-search.md
[qna]: app-insights-troubleshoot-faq.md
[start]: app-insights-overview.md
