---
title: "déploiement aaaFlighting (bêta) dans Azure App Service"
description: "Découvrez comment tooflight de nouvelles fonctionnalités dans votre application ou une version bêta tester vos mises à jour dans ce didacticiel de bout en bout. Il réunit les fonctionnalités App Service comme la publication continue, les emplacements, le routage du trafic et l’intégration d’Application Insights."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
ms.assetid: 17953c51-38f8-442d-bb0b-f69c1542f0e9
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/02/2016
ms.author: cephalin
ms.openlocfilehash: e83477b1fe46be09e5baa7bc2bd239b840b05cf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="flighting-deployment-beta-testing-in-azure-app-service"></a>Déploiement avec distribution d’une version d’évaluation (test bêta) dans Azure App Service
Ce didacticiel vous montre comment toodo *version d’évaluation des déploiements* en intégrant hello différentes fonctionnalités de [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) et [Azure Application Insights](/services/application-insights/).

La *distribution d’une version d’évaluation* est un processus de déploiement qui valide une nouvelle fonctionnalité ou une modification auprès d’un nombre limité de clients réels. Il s’agit d’un test majeur dans un scénario de production. Il s’agit d’analogues toobeta test et est parfois appelée « test contrôlé vol ». Beaucoup de grandes entreprises avec une présence web utilisent cette approche pour obtenir les premières validations de leurs mises à jour d’application dans leur pratique de [développement agile](https://en.wikipedia.org/wiki/Agile_software_development). Azure App Service vous permet de test toointegrate en production avec la publication continue et Application Insights tooimplement hello même scénario DevOps. Avantages de cette approche :

* **Obtenir des commentaires réel *avant* mises à jour sont publiée tooproduction** -hello uniquement mieux obtenir des commentaires dès que vous relâchez gagne commentaires avant de libérer. Vous pouvez tester les mises à jour avec le trafic des utilisateurs réels et les comportements dès que vous le souhaitez dans le cycle de vie du produit hello.
* **Améliorer [ le développement continu piloté par les tests](https://en.wikipedia.org/wiki/Continuous_test-driven_development)** : en intégrant des tests en production avec une intégration et une instrumentation continues dans Application Insights, la validation utilisateur se produit automatiquement et très tôt dans le cycle de vie du produit. Cela contribue à réduire les investissements en temps dans l’exécution de tests manuels.
* **Optimiser le flux de travail test** -grâce à l’automatisation de test en production avec l’instrumentation de surveillance continue, vous pouvez éventuellement atteindre les objectifs de hello différents types de tests dans un processus unique, tel que [intégration](https://en.wikipedia.org/wiki/Integration_testing), [régression](https://en.wikipedia.org/wiki/Regression_testing), [facilité d’utilisation](https://en.wikipedia.org/wiki/Usability_testing), accessibilité, la localisation, [performances](https://en.wikipedia.org/wiki/Software_performance_testing), [sécurité](https://en.wikipedia.org/wiki/Security_testing), et [ acceptation](https://en.wikipedia.org/wiki/Acceptance_testing).

Un déploiement avec distribution d’une version d’évaluation ne se limite pas au routage du trafic en direct. Dans un tel déploiement souhaitées toogain insight aussi rapidement que possible, qu’il s’agisse d’un bogue inattendu, une dégradation des performances, les problèmes d’expérience utilisateur. N’oubliez pas : vous êtes confronté à des clients réels. C’est le cas toodo il à droite, vous devez vous assurer que vous avez configuré votre version d’évaluation toogather de déploiement toutes les données hello vous devez pouvoir toomake une décision informée pour l’étape suivante. Ce didacticiel vous montre comment les données toocollect avec Application Insights, mais vous peuvent utiliser New Relic ou autres technologies qui correspond le mieux à votre scénario.

## <a name="what-you-will-do"></a>Procédure à suivre
Dans ce didacticiel, vous allez apprendre comment toobring hello suivant tootest ensemble de scénarios de votre application de Service de l’application en production :

* [Acheminer le trafic de production](app-service-web-test-in-production-get-start.md) tooyour bêta application
* [Instrumenter votre application](../application-insights/app-insights-web-track-usage.md) tooobtain des mesures utiles
* Déployer votre application bêta et suivre les mesures de l’application en direct en continu
* Métriques de comparaison entre application de production hello et hello bêta application toosee comment le code change traduire tooresults

## <a name="what-you-will-need"></a>Éléments requis
* Un compte Azure
* Un compte [GitHub](https://github.com/)
* Vous pouvez télécharger Visual Studio 2015 - hello [Community edition](https://www.visualstudio.com/en-us/products/visual-studio-express-vs.aspx).
* Interpréteur de commandes GIT (installé avec [GitHub pour Windows](https://windows.github.com/))-ainsi, vous toorun les deux commandes hello Git et PowerShell Bonjour même session
* Dernières informations [Azure PowerShell](https://github.com/Azure/azure-powershell/releases/download/v0.9.8-September2015/azure-powershell.0.9.8.msi)
* Présentation de la base des éléments suivants de hello :
  * Déploiement de modèles [Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) (voir [Déployer une application complexe de manière prévisible dans Microsoft Azure](app-service-deploy-complex-application-predictably.md))
  * [Git](http://git-scm.com/documentation)
  * [PowerShell](https://technet.microsoft.com/library/bb978526.aspx)

> [!NOTE]
> Vous avez besoin une toocomplete compte Azure ce didacticiel :
>
> * Vous pouvez [ouvrir un compte Azure gratuitement](https://azure.microsoft.com/pricing/free-trial/) -vous obtenez des crédits vous pouvez utiliser tootry à payer des services Azure et même après leur utilisation vous pouvez conserver le compte de hello et libérer de l’utilisation des services Azure, telles que les applications Web.
> * Vous pouvez [activer les avantages de votre abonnement Visual Studio](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) : votre abonnement Visual Studio vous donne droit chaque mois à des crédits dont vous pouvez vous servir pour les services Azure payants.
>
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
>
>

## <a name="set-up-your-production-web-app"></a>Configurer votre application web de production
> [!NOTE]
> script Hello utilisé dans ce didacticiel configure automatiquement la publication continue à partir de votre référentiel GitHub. Cela nécessite que vos informations d’identification GitHub sont déjà stockées dans Azure, sinon hello script va échouer lors de la tentative de paramètres de contrôle de code source tooconfigure pour les applications web hello.
>
> toostore informations d’identification de votre GitHub dans Azure, créez une application web Bonjour [Azure Portal](https://portal.azure.com/) et [configurer le déploiement de GitHub](app-service-continuous-deployment.md). Vous ne devez toodo ce qu’une seule fois.
>
>

Dans un scénario classique de DevOps, vous avez une application qui est en cours d’exécution en direct dans Azure, et vous souhaitez tooit de modifications toomake via la publication continue. Dans ce scénario, vous allez déployer tooproduction un modèle que vous avez développé et testé.

1. Créer votre propre branchement de hello [ToDoApp](https://github.com/azure-appservice-samples/ToDoApp) référentiel. Pour plus d’informations sur la création de votre branchement, consultez [Branchement dans un référentiel](https://help.github.com/articles/fork-a-repo/). Une fois votre branchement créé, il est visible dans votre navigateur.

   ![](./media/app-service-agile-software-development/production-1-private-repo.png)
2. Ouvrez une session Git Shell. Si vous n’avez pas encore Git Shell, installez [GitHub for Windows](https://windows.github.com/) .
3. Créer un clone local de votre branche en exécutant hello de commande suivante :

     git clone https://github.com/<your_fork>/ToDoApp.git
4. Une fois que vous avez votre clone local, accédez trop*&lt;repository_root >*\ARMTemplates et exécution hello deploy.ps1 script avec un suffixe unique, comme indiqué ci-dessous :

     .\deploy.ps1 –RepoUrl https://github.com/<your_fork>/todoapp.git -ResourceGroupSuffix <your_suffix>
5. Lorsque vous y êtes invité, tapez Bonjour voulue nom d’utilisateur et mot de passe pour l’accès de la base de données. N’oubliez pas d’informations d’identification de votre base de données car vous en aurez besoin toospecify les à nouveau lorsque la mise à jour hello groupe de ressources.

   Vous devez voir hello mise en service de la progression de plusieurs ressources d’Azure. Lorsque le déploiement terminé, script de hello lancer l’application hello dans le navigateur de hello et vous donne un signal sonore convivial.
   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.1-app-in-browser.png)
6. De retour dans votre session Git Shell, exécutez :

     .\swap –Name ToDoApp<your_suffix>

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.2-swap-to-production.png)
7. Une fois le script de hello, revenez adresse du frontale toobrowse toohello (http://ToDoApp*&lt;your_suffix >*.azurewebsites.net/) toosee hello applications exécutent en production.
8. Ouvrez une session sur hello [portail Azure](https://portal.azure.com/) et examiner ce qui est créé.

   Vous devez être en mesure de toosee deux les applications web Bonjour même groupe de ressources, avec hello `Api` suffixe de nom de hello. Si vous examinez l’affichage hello du groupe de ressources, vous verrez également hello de base de données SQL, server, hello plan App Service et emplacements intermédiaires de hello pour les applications web hello. Parcourir les différentes ressources hello et de les comparer avec  *&lt;repository_root >*toosee \ARMTemplates\ProdAndStage.json comment ils sont configurés dans le modèle de hello.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/00.3-resource-group-view.png)

Vous avez configuré l’application de production hello.  À présent, imaginons que vous avez reçu des commentaires que la facilité d’utilisation est faible pour l’application hello. Par conséquent, vous décidez de tooinvestigate. Vous allez tooinstrument toogive de votre application vous commentaires.

## <a name="investigate-instrument-your-client-app-for-monitoringmetrics"></a>Enquête : Instrumenter votre application cliente aux fins de surveillance/mesures
1. Ouvrez *&lt;racine_référentiel>*\src\MultiChannelToDo.sln dans Visual Studio.
2. Restaurez tous les packages Nuget en cliquant avec le bouton droit sur la solution > **Gérer les packages NuGet pour la solution** > **Restaurer**.
3. Avec le bouton droit **MultiChannelToDo.Web** > **ajouter de télémétrie Application Insights** > **configurer les paramètres** > modifier le groupe de ressources tooToDoApp*&lt;your_suffix >* > **ajouter Application Insights tooProject**.
4. Bonjour portail Azure, ouvrez le panneau de hello pour hello **MultiChannelToDo.Web** ressources d’Application Insight. Puis Bonjour **contrôle d’intégrité de l’Application** partie, cliquez sur **apprendre comment charger des données par page de navigateur toocollect** > Copier le code.
5. Ajouter hello copié le code d’instrumentation JS trop*&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, juste avant la fermeture de hello `<heading>` balise. Elle doit contenir la clé d’instrumentation unique hello de votre ressource Application Insight.

        <script type="text/javascript">
        var appInsights=window.appInsights||function(config){
            function s(config){t[config]=function(){var i=arguments;t.queue.push(function(){t[config].apply(t,i)})}}var t={config:config},r=document,f=window,e="script",o=r.createElement(e),i,u;for(o.src=config.url||"//az416426.vo.msecnd.net/scripts/a/ai.0.js",r.getElementsByTagName(e)[0].parentNode.appendChild(o),t.cookie=r.cookie,t.queue=[],i=["Event","Exception","Metric","PageView","Trace"];i.length;)s("track"+i.pop());return config.disableExceptionTracking||(i="onerror",s("_"+i),u=f[i],f[i]=function(config,r,f,e,o){var s=u&&u(config,r,f,e,o);return s!==!0&&t["_"+i](config,r,f,e,o),s}),t
        }({
            instrumentationKey:"<your_unique_instrumentation_key>"
        });

        window.appInsights=appInsights;
        appInsights.trackPageView();
        </script>
6. Envoyer des événements personnalisés Insights tooApplication clics de souris en ajoutant hello suivant en bas de toohello de code du corps :

       <script>
           $(document.body).find("*").click(function(event) {

               appInsights.trackEvent(event.target.tagName + ": " + event.target.className);
           });
       </script>

   Cet extrait de code JavaScript envoie à une événement personnalisé de tooApplication Insights chaque fois qu’un utilisateur clique sur n’importe où dans l’application web hello.
7. Dans l’interpréteur de commandes Git, validez et envoyez de votre branche tooyour de modifications dans GitHub. Puis, attendez que le navigateur toorefresh de clients.

       git add -A :/
       git commit -m "add AI configuration for client app"
       git push origin master
8. Échange tooproduction de modifications d’application hello déployé :

     .\swap –Name ToDoApp<your_suffix>
9. Parcourir la ressource Application Insights toohello que vous avez configuré. Cliquez sur Événements personnalisés.

   ![](./media/app-service-web-test-in-production-controlled-test-flight/01-custom-events.png)

   Si vous ne voyez pas les mesures pour les événements personnalisés, attendez quelques minutes et cliquez sur **Actualiser**.

Supposons que vous voyiez un graphique comme ci-dessous :

![](./media/app-service-web-test-in-production-controlled-test-flight/02-custom-events-chart-view.png)

Et la grille d’événement hello en dessous :

![](./media/app-service-web-test-in-production-controlled-test-flight/03-custom-event-grid-view.png)

Selon le code d’application tooyour ToDoApp, hello **bouton** événement correspond toohello bouton d’envoi et hello **entrée** événement correspond toohello la zone de texte. Jusqu’à présent, tout est logique. Toutefois, il semble y avoir une quantité importante de clics et très peu de clics sur les éléments d’action hello (hello **LI** événements).

Basé sur ce formulaire vous votre hypothèse certains utilisateurs sont confondu quelle partie de hello l’interface utilisateur est interactif et c’est parce que le curseur de hello le style pour la sélection de texte lorsqu’il se trouve sur les éléments de liste hello et leurs icônes.

![](./media/app-service-web-test-in-production-controlled-test-flight/04-to-do-list-item-ui.png)

Il peut s’agir d’un exemple fictif. Toutefois, vous êtes continu toomake une application de tooyour d’amélioration du produit, puis effectuez une commentaires de version d’évaluation déploiement tooget facilité d’utilisation à partir de clients en direct.

### <a name="instrument-your-server-app-for-monitoringmetrics"></a>Instrumenter votre application serveur aux fins de surveillance/mesures
Il s’agit d’une tangente étant donné que le scénario hello présenté dans ce didacticiel porte uniquement sur hello client application. Toutefois, par souci d’exhaustivité, vous allez définir hello de l’application côté serveur.

1. Avec le bouton droit **MultiChannelToDo** > **ajouter de télémétrie Application Insights** > **configurer les paramètres** > modifier le groupe de ressources tooToDoApp*&lt;your_suffix >* > **ajouter Application Insights tooProject**.
2. Dans l’interpréteur de commandes Git, validez et envoyez de votre branche tooyour de modifications dans GitHub. Puis, attendez que le navigateur toorefresh de clients.

       git add -A :/
       git commit -m "add AI configuration for server app"
       git push origin master
3. Échange tooproduction de modifications d’application hello déployé :

     .\swap –Name ToDoApp<your_suffix>

Et voilà !

## <a name="investigate-add-slot-specific-tags-tooyour-client-app-metrics"></a>Recherchez la cause : Ajouter des métriques de balises spécifiques à l’emplacement tooyour client application
Dans cette section, vous allez configurer hello déploiement différents emplacements toosend spécifiques à l’emplacement de télémétrie toohello même ressource Application Insights. De cette manière, vous pouvez comparer les données de télémétrie de données entre le trafic à partir de différents emplacements (environnements de déploiement) tooeasily consultez effet hello des modifications de votre application. AT hello même temps, vous pouvez séparer le trafic de production hello hello reste pour pouvoir continuer toomonitor votre application de production en fonction des besoins.

Étant donné que vous êtes collecte des données sur le comportement du client, vous allez [ajouter un tooyour d’initialiseur de télémétrie du code JavaScript](../application-insights/app-insights-api-filtering-sampling.md) dans index.cshtml. Si vous souhaitez que les performances de tootest côté serveur, par exemple, vous pouvez également faire de même dans votre code serveur (consultez [API Application Insights pour les événements personnalisés et les métriques](../application-insights/app-insights-api-custom-events-metrics.md).

1. Ajoutez d’abord hello 1re lettre des mots de code hello deux `//` commentaires ci-dessous dans le bloc de hello JavaScript que vous avez ajouté toohello `<heading>` balise précédemment.

        window.appInsights = appInsights;

        // Begin new code
        appInsights.queue.push(function () {
            appInsights.context.addTelemetryInitializer(function (envelope) {
                var telemetryItem = envelope.data.baseData;
                telemetryItem.properties = telemetryItem.properties || {};
                telemetryItem.properties["Environment"] = "@System.Configuration.ConfigurationManager.AppSettings["environment"]";
            });
        });
        // End new code

        appInsights.trackPageView();

    Ce code d’initialiseur, Bonjour `appInsights` objet tooadd hello une propriété personnalisée nommée `Environment` pièce tooevery de télémétrie qu’il envoie.
2. Ensuite, ajoutez cette propriété personnalisée en tant que [paramètre d’emplacement](web-sites-staged-publishing.md#AboutConfiguration) pour votre application web dans Azure. toodo, hello exécution suivant des commandes dans votre session d’interpréteur de commandes Git.

        $app = Get-AzureWebsite -Name todoapp<your_suffix> -Slot production
        $app.AppSettings.Add("environment", "Production")
        $app.SlotStickyAppSettingNames.Add("environment")
        $app | Set-AzureWebsite -Name todoapp<your_suffix> -Slot production

    Hello Web.config dans votre projet définit déjà hello `environment` paramètre d’application. Avec ce paramètre, lorsque vous testez l’application hello localement, vos métriques seront marqués avec `VS Debugger`. Toutefois, lorsque vous appuyez sur votre tooAzure de modifications, Azure sera trouver et utiliser hello `environment` paramètre dans la configuration de l’application hello web d’application et vos métriques seront marqués avec `Production`.
3. Valider push votre branche de tooyour de modifications de code sur GitHub et attendez que votre application nouveaux utilisateurs toouse hello (besoin toorefresh hello navigateur). Il prend environ 15 minutes pour hello nouvelle propriété tooshow dans votre Application Insights `MultiChannelToDo.Web` ressource.

        git add -A :/
        git commit -m "add environment property tooAI events for client app"
        git push origin master
4. Passez maintenant toohello **événements personnalisés** panneau à nouveau et filtrer des mesures hello sur `Environment=Production`. Vous devez maintenant être en mesure de toosee tous les événements personnalisés de hello en production de hello emplacement avec ce filtre.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/05-filter-on-production-environment.png)
5. Cliquez sur hello **favoris** telles que le bouton toosave hello actuel Metrics Explorer paramètres toosomething **événements personnalisés : Production**. Vous pourrez facilement basculer entre cette vue et une vue d’emplacement de déploiement ultérieurement.

   > [!TIP]
   > Pour une analyse encore plus puissante, envisagez d’ [intégrer votre ressource Application Insights avec Power BI](../application-insights/app-insights-export-power-bi.md).
   >
   >

### <a name="add-slot-specific-tags-tooyour-server-app-metrics"></a>Ajouter des balises spécifiques à l’emplacement tooyour server application métriques
Là encore, par souci d’exhaustivité, vous allez définir hello de l’application côté serveur. Contrairement aux application client hello instrumentée dans JavaScript, les balises spécifiques à l’emplacement pour l’application de serveur hello est instrumentée avec le code .NET.

1. Ouvrez *&lt;racine_référentiel >*\src\MultiChannelToDo\Global.asax.cs. Ajoutez le bloc de code hello ci-dessous, juste avant l’accolade de l’espace de noms de fermeture de hello.

        namespace MultiChannelToDo
        {
                ...

                // Begin new code
            public class ConfigInitializer
            : ITelemetryInitializer
            {
                void ITelemetryInitializer.Initialize(ITelemetry telemetry)
                {
                    telemetry.Context.Properties["Environment"] = System.Configuration.ConfigurationManager.AppSettings["environment"];
                }
            }
                // End new code
        }
2. Corriger les erreurs de résolution de nom hello en ajoutant hello `using` instructions ci-dessous toohello début du fichier de hello :

        using Microsoft.ApplicationInsights.Channel;
        using Microsoft.ApplicationInsights.Extensibility;
3. Ajoutez le code hello ci-dessous début toohello Hello `Application_Start()` méthode :

        TelemetryConfiguration.Active.TelemetryInitializers.Add(new ConfigInitializer());
4. Valider push votre branche de tooyour de modifications de code sur GitHub et attendez que votre application nouveaux utilisateurs toouse hello (besoin toorefresh hello navigateur). Il prend environ 15 minutes pour hello nouvelle propriété tooshow dans votre Application Insights `MultiChannelToDo` ressource.

        git add -A :/
        git commit -m "add environment property tooAI events for server app"
        git push origin master

## <a name="update-set-up-your-beta-branch"></a>Mise à jour : Configurer votre branche bêta
1. Ouvrez  *&lt;repository_root >*\ARMTemplates\ProdAndStagetest.json et trouver hello `appsettings` ressources (recherchez `"name": "appsettings"`). Elles sont au nombre de 4, une pour chaque emplacement.
2. Pour chaque `appsettings` ressource, ajoutez une `"environment": "[parameters('slotName')]"` application paramétrage toohello de la fin de hello `properties` tableau. N’oubliez pas ligne précédente de hello tooend par une virgule.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/06-arm-app-setting-with-slot-name.png)

    Vous venez d’ajouter hello `environment` application définissant des emplacements de hello tooall dans le modèle de hello.
3. Dans l’hello du même fichier, recherche hello `slotconfignames` ressources (recherchez `"name": "slotconfignames"`). Elles sont au nombre de 2, une pour chaque application.
4. Pour chaque `slotconfignames` ressource, ajoutez `"environment"` fin toohello Hello `appSettingNames` tableau. N’oubliez pas ligne précédente de hello tooend par une virgule.

    Vous venez d’apporter hello `environment` application paramètre tooits déploiement respectifs Stick pour les deux applications.  
5. Dans votre session d’interpréteur de commandes Git, hello exécution commandes suivantes avec hello même suffixe de groupe de ressources que vous utilisiez auparavant.

        git checkout -b beta
        git push origin beta
        .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch beta
6. Lorsque vous y êtes invité, spécifiez hello les mêmes informations d’identification de base de données SQL comme avant. Ensuite, lorsque le groupe de ressources tooupdate hello, type de demande `Y`, puis `ENTER`.

    Une fois que la fin du script hello, toutes vos ressources dans le groupe de ressources hello d’origine sont conservés, mais un nouvel emplacement nommé « bêta » est créé avec hello même configuration que hello emplacement « Intermédiaire » qui a été créé à partir de l’hello.

   > [!NOTE]
   > Cette méthode de création de différents environnements de déploiement est différente de la méthode hello dans [développement Agile avec Azure App Service](app-service-agile-software-development.md). Ici, vous créez des environnements de déploiement avec des emplacements de déploiement, alors qu’avec l’autre méthode, vous créez des environnements de déploiement avec des groupes de ressources. La gestion des environnements de déploiement avec les groupes de ressources vous permet de tookeep hello production environnement hors des limites toodevelopers, mais il n’est pas facile toodo test en production, vous pouvez ainsi faire facilement avec les emplacements.
   >
   >

Si vous le souhaitez, vous pouvez également créer une application alpha en exécutant la commande suivante :

    git checkout -b alpha
    git push origin alpha
    .\deploy.ps1 -RepoUrl https://github.com/<your_fork>/ToDoApp.git -ResourceGroupSuffix <your_suffix> -SlotName beta -Branch alpha

Pour ce didacticiel, vous continuerez simplement à utiliser votre application bêta.

## <a name="update-push-your-updates-toohello-beta-app"></a>Mise à jour : Distribuer votre application de bêta toohello mises à jour
Sauvegarder l’application tooyour que vous souhaitez tooimprove.

1. Vérifiez que vous êtes à présent dans votre branche bêta

        git checkout beta
2. Dans  *&lt;repository_root >*\src\MultiChannelToDo.Web\app\Index.cshtml, rechercher hello `<li>` de balise et ajouter hello `style="cursor:pointer"` d’attribut, comme illustré ci-dessous.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/07-change-cursor-style-on-li.png)
3. validez et envoyez tooAzure.
4. Vérifiez que hello modification est maintenant répercutée dans l’emplacement de bêta hello en naviguant toohttp://todoapp*&lt;your_suffix >*-beta.azurewebsites.net/. Si vous ne voyez pas hello modifier encore, actualisez votre navigateur tooget hello nouveau javascript code.

    ![](./media/app-service-web-test-in-production-controlled-test-flight/08-verify-change-in-beta-site.png)

Maintenant que vous avez votre modification en cours d’exécution dans l’emplacement de bêta hello, vous êtes prêt tooperform un version d’évaluation du déploiement.

## <a name="validate-route-traffic-toohello-beta-app"></a>Valider : Route le trafic toohello bêta application
Dans cette section, vous achemine le trafic toohello bêta application. Par souci de clarté, de démonstration, vous allez tooroute une partie significative de tooit de trafic utilisateur hello. En réalité, hello quantité de trafic que vous souhaitez tooroute dépend de votre situation spécifique. Par exemple, si votre site est à l’échelle de hello de microsoft.com, il vous faudra peut-être inférieur à un pour cent de votre total du trafic de données de commandes toogain utile.

1. Dans votre session d’interpréteur de commandes Git, exécutez hello suivant de commandes tooroute la moitié de l’emplacement de hello production trafic toohello bêta :

        $siteName = "ToDoApp<your suffix>"
        $rule = New-Object Microsoft.WindowsAzure.Commands.Utilities.Websites.Services.WebEntities.RampUpRule
        $rule.ActionHostName = "$siteName-beta.azurewebsites.net"
        $rule.ReroutePercentage = 50
        $rule.Name = "beta"
        Set-AzureWebsite $siteName -Slot Production -RoutingRules $rule

   Hello `ReroutePercentage=50` propriété spécifie que 50 % du trafic de production hello est URL de l’application toohello routé bêta (spécifié par hello `ActionHostName` propriété).
2. Maintenant accédez toohttp://ToDoApp*&lt;your_suffix >*. azurewebsites.net. 50 % du trafic de hello doit maintenant être emplacement bêta de toohello redirigé.
3. Dans votre ressource Application Insights, filtrer les métriques hello en environnement = « bêta ».

   > [!NOTE]
   > Si vous enregistrez cette vue filtrée en tant que favori d’un autre, vous pouvez facilement inverser hello explorer métrique entre les modes production et vues de la version bêta.
   >
   >

Supposons que dans Application Insights, vous voyez quelque chose de similaire toohello suivantes :

![](./media/app-service-web-test-in-production-controlled-test-flight/09-test-beta-site-in-production.png)

Non seulement cette affiche qu’il n’y a plus nombre de clics sur hello `<li>` balises, mais il semble toobe une hausse du nombre de clics sur `<li>` balises. Vous pouvez ensuite en conclure que les personnes ont découverts hello nouvelle `<li>` les étiquettes sont interactifs et effacez toutes leurs tâches précédemment s’est terminée dans l’application hello maintenant.

Des données hello du déploiement de votre version d’évaluation, vous décidez que votre nouvelle interface utilisateur est prête pour la production.

## <a name="go-live-move-your-new-code-into-production"></a>Mise en ligne : Mettre votre nouveau code en production
Vous êtes maintenant prêt toomove votre tooproduction de mise à jour. Ce qui est élevée qui est maintenant, vous savez que votre mise à jour a déjà été validée *avant* tooproduction push est exécuté. Vous pouvez donc la déployer en toute confiance. Étant donné que vous avez apportées à une application de client de mise à jour toohello AngularJS, vous validé uniquement le code côté client de hello. Si vous étiez toomake modifications toohello principal API Web app, vous pourriez valider vos modifications de la même façon et facilement.

1. Dans l’interpréteur de commandes Git, supprimer la règle de routage de trafic hello en exécutant hello de commande suivante :

        Set-AzureWebsite $siteName -Slot Production -RoutingRules @()
2. Exécutez les commandes de Git hello :

        git checkout master
        git pull origin master
        git merge beta
        git push origin master
3. Attendez quelques minutes pour hello nouveau code toohello toobe déployé staging emplacement, puis lancement http://ToDoApp*&lt;your_suffix >*-tooverify staging.azurewebsites.net qui hello nouvelle mise à jour est préparée intermédiaire de hello emplacement. Souvenez-vous que hello branche de principale de votre branche est lié toohello intermédiaire emplacement de votre application.
4. À présent, remplacez hello staging emplacement en production

        cd <ROOT>\ToDoApp\ARMTemplates
        .\swap.ps1 -Name todoapp<your_suffix>

## <a name="summary"></a>Résumé
Azure App Service facilite pour les entreprises de taille petite toomedium tootest leurs applications côté client en production, un problème qui a été fait habituellement dans les grandes entreprises. Nous espérons que ce didacticiel vous a donné hello connaissances nécessaires toobring ensemble App Service et Application Insights toomake version d’évaluation déploiement possible et même les autres scénarios de test de production, dans votre monde DevOps.

## <a name="more-resources"></a>Autres ressources
* [Développement logiciel agile avec Azure App Service](app-service-agile-software-development.md)
* [Configurer des environnements intermédiaires pour les applications web dans Azure App Service](web-sites-staged-publishing.md)
* [Déployer une application complexe de manière prévisible dans Microsoft Azure](app-service-deploy-complex-application-predictably.md)
* [Création de modèles Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md)
* [JSONLint - hello validateur JSON](http://jsonlint.com/)
* [Création de branches Git – Branchement et fusion basiques](http://www.git-scm.com/book/en/v2/Git-Branching-Basic-Branching-and-Merging)
* [Azure PowerShell](/powershell/azure/overview)
* [Projet Wiki Kudu](https://github.com/projectkudu/kudu/wiki)
