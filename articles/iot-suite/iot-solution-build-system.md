---
title: "Exemple Azure IoT MyDriving : création d’une application | Microsoft Docs"
description: "Créer une application qui est une démonstration complète de la tooarchitect un système IoT à l’aide de Microsoft Azure, notamment les flux Analytique, Machine Learning et concentrateurs d’événements."
services: 
documentationcenter: .net
suite: 
author: harikmenon
manager: douge
ms.assetid: c2fcd6ee-3bbe-43d1-a066-dce52cc3a53d
ms.service: multiple
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: dotnet
ms.topic: article
ms.date: 06/30/2017
ms.author: harikm
ms.openlocfilehash: e78571225697f745fe011c722e57c8600704c392
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="build-and-deploy-hello-mydriving-solution-tooyour-environment"></a>Générez et déployez hello MyDriving solution tooyour environnement
MyDriving est une solution Internet des objets (IoT, Internet of Things) qui recueille les données de votre voiture, les traite à l’aide de services Machine Learning et les affiche sur votre téléphone mobile. Hello se compose d’une variété de services fournis par Microsoft Azure. les clients de Hello peuvent être des téléphones Android, iOS ou Windows 10.

Nous avons créé hello MyDriving solution toogive vous indiqués dans la création de votre propre système IoT. À partir de hello [référentiel MyDriving sur GitHub](https://github.com/Azure-Samples/MyDriving), vous pouvez obtenir les scripts Azure Resource Manager architecture de back-end toodeploy hello dans votre propre compte Azure. À partir de là, vous pouvez reconfigurer les différents services de hello, modifier hello requêtes toosuit vos propres données et ainsi de suite. Vous pouvez trouver ces scripts, ainsi que du code pour l’application mobile hello, projet d’API de Service d’application Azure hello et plus--dans le référentiel de MyDriving hello.

Si vous n’avez pas encore essayé application hello, examinez hello [guide pas à pas de Get](iot-solution-get-started.md).

Il existe un compte détaillé de l’architecture de hello Bonjour [Guide de référence MyDriving](http://aka.ms/mydrivingdocs). En résumé, il existe plusieurs éléments que nous configurons toocreate un projet similaire :

* Une **application cliente** s’exécute sur des téléphones Android, iOS et Windows 10. Nous utilisons hello Xamarin plateforme tooshare proportion de code hello, qui est stocké sur GitHub sous `src/MobileApp`. application Hello effectue deux fonctions distinctes :
  * Il relaie les données de télémétrie à partir de l’appareil de diagnostic embarqués (OBD) hello et de cloud back-end de son propre emplacement toohello système de service.
  * Il s’agit d’une interface utilisateur qui permet aux utilisateurs d’effectuer des interrogations concernant leurs trajets routiers enregistrés.
* A **service de cloud computing** reçoit les données de voyage hello en temps réel et le traite. Hello principal de la création de ce service sont toochoose, paramétrer et rattachez une variété de services Azure. Certaines parties de hello nécessitent des données entrantes hello scripts toofilter et processus. Nous utilisons un tooconfigure de modèle Azure Resource Manager toutes les parties hello.
* A **application de service mobile** est service web de hello derrière la partie d’interface utilisateur hello d’application pour appareil hello. Sa tâche principale est tooquery hello des données stockées et traitées. Le code correspondant se trouve sur GitHub sous `src/MobileAppService`.
* **Visual Studio avec Xamarin** est notre environnement de développement. Sert de Xamarin, ce qui existe à la fois en tant que composant de Visual Studio et un environnement autonome de développement intégré (IDE), code d’inter-plateformes appareil toobuild hello. code de toobuild hello iOS, il est nécessaire toohave une instance de Xamarin s’exécutant sur un ordinateur du système d’exploitation X. Si nécessaire, elle peut être exécutée en tant qu’agent, géré à partir de Visual Studio.
* **Tests unitaires** du périphérique de hello applications est effectuée dans Xamarin Test Cloud.
* **GitHub** est référentiel hello où nous permet de stocker tous les modèles, scripts et les code hello.
* **Visual Studio Team Services** est un service cloud qui a utilisé toomanage build en continu hello et test d’applications de service et le périphérique hello web.
* **HockeyApp** est toodistribute utilisé les versions de code de périphérique hello. Il collecte également les rapports d’incident et d’utilisation, ainsi que les commentaires des utilisateurs.
* **Visual Studio Application Insights** moniteurs hello service web mobile.

Voyons comment nous configurons tout cela. 

> [!NOTE] 
> La plupart des hello suivant les étapes sont facultatives.
>
>

## <a name="sign-up-for-accounts"></a>S’inscrire pour obtenir un compte
* [Visual Studio Dev Essentials](https://www.visualstudio.com/products/visual-studio-dev-essentials-vs.aspx). Ce programme gratuit fournit des outils de développement de réduire un accès facile et services, notamment Visual Studio, Visual Studio Team Services et Azure. Il vous offre un crédit de 25 $ par mois sur Azure pendant douze mois. Il inclut également la formation de tooPluralsight d’abonnements et de l’université Xamarin. Vous pouvez aussi vous inscrire séparément pour bénéficier des niveaux gratuits d’[Azure](https://azure.com) et de [Visual Studio Team Services](https://www.visualstudio.com/products/visual-studio-team-services-vs.aspx). Sachez cependant que ceux-ci n’offrent pas de crédits Azure.
* [HockeyApp](https://rink.hockeyapp.net/) (facultatif) pour gérer la distribution de test des applications mobiles et collecter les données de télémétrie.
* [Xamarin](https://xamarin.com/) (obligatoire), pour créer une application mobile hello et en cours d’exécution s’exécute le débogage et les tests sur [Xamarin Test Cloud](https://xamarin.com/test-cloud).
* [GitHub](https://github.com/Azure-Samples/MyDriving/) (facultatif), référentiels publics libre toocreate pour votre propre code (de dépôts privés sont payés). Vous pouvez également utiliser plan de base hello dans Visual Studio Team Services pour les référentiels privés.
* [Power BI](https://powerbi.microsoft.com/) (facultatif), visualisation enrichie toocreate des données au sein de l’ensemble du système hello.

> [!NOTE]
> Vous n’avez pas besoin d’un compte tooaccess hello code MyDriving de GitHub [hello GitHub MyDriving référentiel](https://github.com/Azure-Samples/MyDriving).
> 
> 

## <a name="install-development-tools"></a>Installer les outils de développement
Bonjour le programme d’installation suivant est pour le développement de solution complète de hello : un iOS, Android et Windows 10 Mobile application multiplateforme, avec un Azure back-end.

En guise d’alternative, vous pouvez utiliser Xamarin Studio sur Mac ou Windows toodevelop hello des applications mobiles si vous ne travaillez pas sur hello Azure précédent se terminer.

Une [description plus complète de cette configuration](https://msdn.microsoft.com/library/mt613162.aspx)est à votre disposition.

### <a name="windows-development-machine"></a>Ordinateur de développement Windows
outil de central Hello sur Windows est Visual Studio, pour utiliser hello MyDriving app pour Android et Windows, projet d’API du Service application hello et extensions de microservice.

Visual Studio intègre d’autres composants utiles, tels que Xamarin, Git et des émulateurs.

Installer :

* [Visual Studio avec Xamarin](https://www.visualstudio.com/products/visual-studio-community-vs) (toutes éditions - l’édition Community est gratuite).
* [SQLite pour plateforme Windows universelle](https://visualstudiogallery.msdn.microsoft.com/4913e7d5-96c9-4dde-a1a1-69820d615936). Obligatoire de code de Windows 10 Mobile toobuild hello.
* [Kit de développement logiciel (SDK) Azure pour Visual Studio](https://www.visualstudio.com/vs/azure-tools/). Permet de vous hello SDK pour exécuter des applications dans Azure, ainsi que des outils de ligne de commande de gestion Azure.
* [Kit de développement logiciel (SDK) Azure Service Fabric](http://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MicrosoftAzure-ServiceFabric). Toobuild requis hello [microservice](../service-fabric/service-fabric-get-started.md) extension.

Assurez-vous que les extensions Visual Studio droite hello. Sous **Outils**, vous pouvez voir **Android, iOS, Xamarin, etc**. Dans le cas contraire, ouvrez Visual Studio, recherchez Xamarin, suivez hello invites tooinstall il. Vérifiez également que **Git pour Windows** est installé. Si non, dans Visual Studio, rechercher et suivez les hello invites tooinstall il. 

### <a name="mac-development-machine"></a>Ordinateur de développement Mac
Hello Mac (Yosemite ou version ultérieure) est requis si vous souhaitez toodevelop pour iOS. Bien que nous utiliser Visual Studio avec Xamarin sur Windows toodevelop et gérer tout code hello, Xamarin utilise un agent installé sur un Mac dans l’ordre toobuild et signe hello code iOS.

![Développez sur Windows et générez sur Mac](./media/iot-solution-build-system/image1.png)

(En guise d’alternative, vous pouvez utiliser Xamarin Studio directement sur hello Mac toodevelop des applications multiplateformes).

Vous n’avez pas besoin hello Mac si vous ne souhaitez pas iOS tooinclude comme plateforme cible.

Installer :

* [Xamarin Studio pour iOS](https://developer.xamarin.com/guides/ios/getting_started/installation/mac/). Vous pouvez également configurer Visual Studio et Xamarin sur un Mac exécutant une machine virtuelle Windows. Consultez la page [Configuration, installation et vérifications pour les utilisateurs Mac](https://msdn.microsoft.com/library/mt488770.aspx) sur MSDN.
* [Outils de développement Azure](https://azure.microsoft.com/downloads/) (facultatif).

Activer la connexion à distance sur hello Mac. Ouvrez **Préférences système** > **Partage**, puis sélectionnez **Connexion à distance**.

Lorsque vous ouvrez un projet iOS dans Visual Studio sous Windows, hello Xamarin plug-in vous demandera ID hello Hello Mac.

## <a name="fetch-hello-github-repository"></a>Extraction du référentiel GitHub de hello
Extraire une copie locale de [hello référentiel de GitHub MyDriving](https://github.com/Azure-Samples/MyDriving) à l’aide de hello **ZIP de téléchargement** bouton dans GitHub, Visual Studio ou un autre client Git.

Décompressez le dossier tooa hello portant un nom de chemin d’accès court, par exemple c\\code.

Vous pouvez également, si vous souhaitez tookeep les toodate avec ou contribuez du code de tooour, cloner référentiel de hello comme suit :

**git clone https://github.com/Azure-Samples/MyDriving.git**

## <a name="get-a-bing-maps-api-key"></a>Obtenir une clé d’API Bing Cartes
[Inscrivez-vous pour obtenir une clé d’API Bing Cartes](https://msdn.microsoft.com/library/ff428642.aspx).

Vous devez tooreplace cette ligne dans 22 dans `src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs`.

## <a name="build-hello-demo-app"></a>Générez l’application de démonstration hello
Ouvrez ces solutions dans Visual Studio :

* src\MobileApps\MyDriving.sln
* src\MobileAppService\MyDrivingService.sln
* src\Extensions\ServiceFabric\VINLookUpApplication\VINLookUpApplication.sln

Vous obtiendrez des invites pour :

* approuver des projets potentiellement non fiables ; Choisissez tooopen les si vous souhaitez toogo avance.
* définir le mode développeur si vous travaillez sur un nouvel ordinateur Windows 10 ;
* entrer vos informations d’identification Xamarin ;
* Se connecter toohello Xamarin Mac. Si vous n’avez pas un Mac, avec le bouton hello iOS de projet dans Visual Studio, puis **décharger le projet**.

Régénérez la solution de hello.

Si vous avez la construction du problème, essayez de hello solutions tooquirks que nous avons trouvé :

* *VINLookupApplication projet n’est pas chargé*: Assurez-vous que vous avez installé hello [Azure SDK pour Visual Studio](https://www.visualstudio.com/vs/azure-tools/).
* *Projet de service Fabric ne générer*: générer des projets d’interface hello tout d’abord et assurez-vous que vous avez installé hello SDK de l’infrastructure de Service.
* *L’application Android n’est pas générée*:
  
  * Ouvrez **Outils** > **Android** > **Android SDK Manager** et vérifiez qu’Android 6 (API 23)/plateforme du Kit SDK est installé.
  * Supprimez ce répertoire, puis régénérez :<br/>
    `%LocalAppData%\Xamarin\zips`

## <a name="get-tooknow-hello-code"></a>Obtenir le code de hello tooknow
Dans la solution de hello, vous trouverez :

* Extensions Azure : Service Fabric.
* Azure HDInsight : scripts pour le traitement des données de trajet dans Azure.
* Mobile d’applications : applications pour appareil hello.
* MobileAppsService/MyDrivingService : web hello précédent se terminer.
* Power BI : définition de rapport hello.
* Scripts :
  
  * Le Gestionnaire de ressources : modèles toobuild hello ressources Azure.
  * PowerShell : Modèles de gestionnaire de ressources Scripts toorun hello.
  * Azure SQL Database : débogage des bases de données.
* SQL Database : CreateTables : définitions de schéma.
* Analytique de flux de données Azure : Interroge ce flux de données entrant de transformation hello.

## <a name="run-hello-apps-in-development-mode"></a>Exécuter des applications de hello en mode de développement
Prenez action toorun applications hello, en fonction de l’appareil hello que vous utilisez :

* Serveur principal : MyDrivingService ensemble en tant que projet de démarrage hello et appuyez sur service de F5 toorun hello web principal. Il s’ouvre une vue du navigateur de liste de hello API.
* Les clients mobiles : hello [des applications mobiles sont développées dans Xamarin](https://developer.xamarin.com/guides/cross-platform/deployment,_testing,_and_metrics/debugging_with_xamarin/).
  
  * Android : pour plus d’informations, consultez [Debugging Android in Xamarin](http://developer.xamarin.com/guides/android/deployment,_testing,_and_metrics/debugging_with_xamarin_android/)(Débogage d’Android dans Xamarin).
  * iOS : pour plus d’informations, consultez [Debugging in iOS](http://developer.xamarin.com/guides/ios/deployment,_testing,_and_metrics/debugging_in_xamarin_ios/)(Débogage dans iOS).
  * Windows Phone : pour plus d’informations, consultez [Xamarin + Windows Phone](https://developer.xamarin.com/guides/cross-platform/windows/phone/).

## <a name="upload-hello-mobile-app-toohockeyapp"></a>Télécharger hello application mobile tooHockeyApp
HockeyApp gère distribution hello de vos utilisateurs Android, iOS ou Windows application tootest, notification des utilisateurs de nouvelles versions. Il collecte également des rapports d’incidents utiles, les commentaires des utilisateurs avec captures d’écran et des mesures sur l’utilisation.

[Commencez par charger](http://support.hockeyapp.net/kb/app-management-2/how-to-create-a-new-app) votre application générée. Ensuite, connectez-vous trop[HockeyApp](https://rink.hockeyapp.net) à partir de votre ordinateur de développement. Dans le tableau de bord du développeur hello, cliquez sur **nouvelle application**, puis faites glisser les fichiers hello généré dans la fenêtre hello. (Une version ultérieure, vous pouvez automatiser votre toodo de service de build cela.)

Vous accédez maintenant au tableau de bord de votre application.

![Onglet vue d’ensemble sur le tableau de bord application hello](./media/iot-solution-build-system/image2.png)

Répétez le processus de hello pour chaque plateforme que votre application s’exécute sur. Ensuite, vous pouvez effectuer les suivant hello :

* Hello d’utilisation [ID de l’application](http://support.hockeyapp.net/kb/app-management-2/how-to-find-the-app-id) à partir des données de panne toosend hello du tableau de bord et des commentaires à partir de votre application. MyDriving, mettre à jour ID hello dans src/MobileApps/MyDriving/MyDriving.Utils/Logger.cs.
* [Invitez les utilisateurs de test](http://support.hockeyapp.net/kb/app-management-2/how-to-invite-beta-testers). Vous obtenez un toorecruit URL aux utilisateurs de testeurs. Ils être en mesure de toosign pour votre équipe, téléchargez l’application hello et vous envoyer des commentaires.
* Si vous préférez une version bêta plus ouvrir, définissez hello distribution toopublic. Cliquez sur **Gérer l’application** > **Distribution** > **Télécharger = Public**. Désormais, tout le monde peut télécharger votre application et vous envoyer des commentaires. De même, tous les utilisateurs recevront une notification lorsque vous publierez une nouvelle version. Vous pouvez également leur fournir des rapports d’incident.
  
   ![Équipes sur le tableau de bord hello](./media/iot-solution-build-system/image3.png)
* [Panne de liaison signale tooVisual Studio Team Services](http://support.hockeyapp.net/kb/third-party-bug-trackers-services-and-webhooks/how-to-use-hockeyapp-with-visual-studio-team-services-vsts-or-team-foundation-server-tfs). Cliquez sur **Gérer l’application** > **Visual Studio Team Services**. HockeyApp peut créer automatiquement des éléments de travail dans Team Services quand des rapports d’incident sont disponibles ou à la réception des commentaires.

Lecture plus à hello [HockeyApp site](https://hockeyapp.net).

## <a name="test-hello-mobile-app-on-xamarin-test-cloud"></a>Tester l’application mobile hello sur Xamarin Test Cloud
[Xamarin Test Cloud](https://developer.xamarin.com/guides/testcloud/introduction-to-test-cloud/) automatise les tests d’interface utilisateur sur les appareils réels dans le cloud de hello. À l’aide de framework NUnit de hello, vous écrivez des tests qui exécutent votre application via l’interface utilisateur hello.

toouse Xamarin, vous incorporez hello [Xamarin.UITests](https://developer.xamarin.com/guides/testcloud/uitest/intro-to-uitest/) SDK dans votre application, qui est fourni comme package NuGet. Vous trouverez dans l’application de démonstration hello, et il n’est fourni lorsque vous créez des projets de test avec hello modèles Xamarin.

![Où toofind hello SDK inter-plateformes sur l’interface de hello](./media/iot-solution-build-system/image4.png)

Un exemple de projet de test est inclus avec l’application hello dans le référentiel de hello. Dans [MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService), regardez sous [src](https://github.com/Azure-Samples/MyDriving/tree/master/src)/MobileApps/[MyDriving](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileApps/MyDriving)/MyDriving.UITests/.

Si vous utilisez une version de Visual Studio Team Services, il est facile toowrite unité de Xamarin UI teste et les exécuter dans le cadre de votre build.

## <a name="deploy-azure-services"></a>Déployer des services Azure
tooperform un déploiement automatique de services Azure et les services de build Team Services, consultez toohello des instructions dans **scripts/README.md**.

Microsoft Azure fournit une multitude de services différents que vous pouvez utiliser des applications de cloud toobuild. Bien que la plupart peuvent être utilisées individuellement (tels que les applications de Service/Web application), elles sont à leur quand ils sont interconnectés tooform un système intégré que nous utilisons dans MyDriving.

Il est possible de toocreate et interconnexion manuellement les services Azure, mais il est beaucoup plus rapides et plus fiables toouse les modèles Azure Resource Manager. [Le Gestionnaire de ressources](../azure-resource-manager/resource-group-overview.md) automatise le déploiement hello des ressources d’une solution et rendre les interconnexions hello entre eux.

Vous trouverez les modèle hello pour système de MyDriving hello dans le référentiel GitHub de hello sous [scripts/ARM](https://github.com/Azure-Samples/MyDriving/tree/master/scripts/ARM). Il fournit une vue complète et concise de la façon dont les différents services de hello dans notre architecture sont interconnectés. Nous vous expliquons tous ces éléments en détail dans hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs), mais vous pouvez apprendre beaucoup simplement en lisant les hello du modèle.

> [!NOTE]
> Services Azure plus ont associé un coût, en fonction du niveau tarifaire de hello. Si vous êtes tooAzure nouveau, vous pouvez [essayer gratuitement](https://azure.microsoft.com/free/). Toutefois, si vous ne prévoyez pas certains composants Bonjour MyDriving système toouse, être tooremove que les coûts de souscrivant tooavoid. Hello « Estimation les coûts d’exploitation » section plus loin dans cet article fournit un résumé des frais de service par défaut.
> 
> 

### <a name="edit-hello-template"></a>Modifier un modèle de hello
toocustomize votre déploiement, peut-être tooremove les composants ou tooadd d’autres utilisateurs, tout d’abord effectuer une copie de scénario\_complete.params.json et scénario\_complete.json dans lequel les modifications toomake.

Vous pouvez utiliser le scénario de hello\_complete.params.json toooverride de fichier différentes valeurs par défaut, par exemple hello service référence (SKU) ou hello réplication type de stockage, comme décrit dans hello tableau suivant. valeurs par défaut de Hello sélectionnez les options de coût le plus bas hello.

| **Paramètre** | **Description** | **Valeur par défaut** |
| --- | --- | --- |
| Référence IoT Hub |Niveau pour le service Azure IoT Hub |F1 |
| Type de compte de stockage |Type de réplication de stockage |LRS standard |
| Objectif de service SQL |Consommation des emplacements de concurrence |DW100 |
| Référence du plan d’hébergement |Plan de service pour App Service |F1 |

Dans scenario\_complete.json :

* Recherchez « baseName » et le modifier nom tooa que vous préférez.
* Recherchez « Create ». Chacune de ces sections crée une ressource.
* Valeur sqlServerAdminLogin et sqlServerAdminPassword toosuitable.
* Avant de supprimer une section qui crée une ressource, vérifiez s’il a des dépendances en recherchant son nom ailleurs dans le fichier de hello. Notez que chaque section qui crée un service inclut une section *dependsOn* répertoriant ses dépendances.

Voici le modèle hello configure. Détails sont disponibles dans hello [Guide de référence](http://aka.ms/mydrivingdocs).

| **Service** | **Description et détails** |
| --- | --- |
| Comptes de stockage |modèle de Hello crée trois comptes : |
| -Base de données SQL qui reçoit la télémétrie agrégée à partir de flux de données Analytique et sert de magasin de stockage hello pour les tables Azure App Service qui exposent ces données via les points de terminaison API. | |
| -Stockage objet blob qui accumule les données d’historique à partir d’une autre tâche de flux de données Analytique, toobe traité par HDInsight. | |
| -   Une base de données SQL qui reçoit les résultats traités par HDInsight pour une utilisation avec Power BI. | |
| Azure IoT Hub |Établit un appareil connecté tooeach de connexion bidirectionnel. Bonjour MyDriving solution, application mobile hello joue un tooAzure de données toosend champ passerelle IoT Hub. IoT Hub Azure sert alors une entrée tooStream Analytique. |
| Hubs d'événements Azure |Une sortie d’une tâche de flux de données Analytique hello en file d’attente de sortie tooextensions créés avec Azure Service Fabric. |
| Azure SQL Data Warehouse | |
| Tâches Stream Analytics |Connecter des entrées et sorties avec une requête, qui est utilisé tooaggregate des données en temps réel et historiques pour hello API de Service d’application, Azure Machine Learning, extensions et Power BI. |
| Espace de travail Machine Learning |Inclut des expériences, le code R et le service API. |
| Azure Data Factory |Reformation Machine Learning planifiée. |
| Plan d’hébergement Service Fabric |Pour les extensions. |
| App Service (« Application mobile ») |Hôtes hello Mobile Apps projet d’API qui fournit des points de terminaison pour l’application mobile hello. Hello code de l’API doit être déployé tooApp Service depuis Visual Studio. |
| Règles d'alerte |Envoie de que vous envoyer par courrier électronique si indiquent des échecs de réponses d’application hello. |
| Application Insights |Pour analyser les performances de hello API dans le Service d’applications. Vous avez la connexion de hello tooconfigure dans Visual Studio. |
| coffre de clés Azure |Pour l’enregistrement de certificat de cluster du service web hello. |

### <a name="run-hello-template"></a>Exécuter le modèle de hello
Dans **scripts/README.md**, il existe des instructions détaillées pour le modèle de hello en cours d’exécution.

tooprovision tous ces services dans votre propre compte Azure à l’aide du script de hello, effectuez l’une des hello suivant :

* Utilisez PowerShell :
  
  ```
  
  cd scripts/PowerShell;
  deploy.ps1 *location* *resourceGroupName*
  ```
  
  * *emplacement* est hello [emplacement Azure](https://azure.microsoft.com/regions/), tel que `North Europe` ou `West US`. Utilisez `Get-AzureLocation` toofind une liste des emplacements disponibles.
  * *resourceGroupName* est hello nom de groupe toohello toogive qui appartiennent à toutes les ressources hello. Lorsque vous avez terminé avec des ressources hello, vous pouvez les supprimer tous les éléments en supprimant ce groupe.
* Exécutez DeploymentScripts/Bash/deploy.sh avec Bash.
* Ouvrir et générer des solutions de Visual Studio hello DeploymentScripts/VS/DeployARM.sln.

Notez que chaque modèle de temps de hello est exécuté, il crée un ensemble de ressources avec les nouveaux noms. des ressources toodelete hello, accédez toohello portal et supprimer le groupe de ressources hello.

Si le script de hello échoue pour une raison quelconque, vous pouvez réexécuter il.

permet de script Hello hello de l’option de configuration de l’intégration continue dans Visual Studio Team Services. Si vous avez configuré un projet Team Services, vous avez une URL : https://yourAccountName.visualstudio.com. Entrez l’URL complète de hello lorsque vous êtes invité. Vous pouvez lui donner un nouveau nom ou le nom existant d’un projet Team Services.

## <a name="set-up-build-and-test-definitions-in-visual-studio-team-services"></a>Configurer des définitions de build et de test dans Visual Studio Team Services
Nous utiliser Team Services sur ce projet, principalement pour ses fonctionnalités de génération et de test. Cependant, il offre également une excellente prise en charge de la collaboration : gestion des tâches avec les tableaux Kanban, révision du code intégrée aux tâches et au contrôle de code source et builds contrôlées. Il s’intègre efficacement à d’autres outils tels que GitHub, Xamarin, HockeyApp et, bien sûr, Visual Studio. Vous pouvez y accéder via l’interface web hello ou Visual Studio, selon ce qui est plus pratique à tout moment.

Hello étapes de build de hello et définitions de version utilisent divers services de plug-in qui sont disponibles dans les Services d’équipe hello [Marketplace](https://marketplace.visualstudio.com/VSTS). Dans les lignes de commande Ajout toobasic utilitaires toorun ou copier les fichiers, il sont des services qui appeler builds par Xamarin, Android et d’autres fournisseurs, et qui connectent tooHockeyApp.

![Options de génération dans Team Services](./media/iot-solution-build-system/image5.png)

### <a name="build-definitions"></a>Définitions de build
Nous avons des définitions de build pour chacune des principales cibles de hello. ainsi que de variantes pour les tests de fonctionnalités et de régression. Cela nous donne :

* MyDriving.Services (application hello web principal pour l’application mobile hello)
* MyDriving.Xamarin.Android
  
  * MyDriving.Xamarin.Android-Feature
  * MyDriving.Xamarin.Android-Regression
* MyDriving.Xamarin.iOS
  
  * MyDriving.Xamarin.iOS-Feature
  * MyDriving.Xamarin.iOS-Regression
* MyDriving.Xamarin.UWP
  
  * MyDriving.Xamarin.UWP-Feature
  * MyDriving.Xamarin.UWP-Regression

Si vous souhaitez toosee hello tous les détails de notre configuration, consultez la section 4.7 Hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs), « Génération et Configuration de la mise en production. » Elles suivent hello même modèle général. script de Hello :

1. Restaure le package NuGet de hello. Nous ne pas conserver le code compilé dans le référentiel de hello, hello premier de chaque build existe toorestore hello requis les packages NuGet.
2. Active la licence de hello. génération de Hello est effectuée dans le cloud de hello, où nous avons besoin d’une licence, en particulier, pour hello Xamarin build service--nous doivent tooactivate notre licence sur l’ordinateur de build actuel hello. Ensuite, nous désactiver immédiatement après, tooallow il toobe utilisé sur un autre ordinateur.
3. Les builds à l’aide du service approprié de hello. Nous utilisons des builds de Xamarin pour des applications mobiles hello, et Visual Studio génère pour le service web principal de hello.
4. Génère des tests.
5. Exécute les tests. Nous exécuter des tests d’application mobile hello dans Xamarin Test Cloud.
6. Publie un emplacement de dépôt toohello hello build résultat.

déclencheur Hello pour les builds principal hello a la valeur toocontinuous integration. Autrement dit, génération de hello est exécutée chaque fois que code est activé dans la branche principale du toohello.

![Interface où le déclencheur de hello est ensemble toocontinuous integration](./media/iot-solution-build-system/image6.png)

### <a name="release-definitions"></a>Définitions de mise en production
Définitions de version sont définies dans quantité hello même façon.

Pour le service web de hello, nous configurons déploiement sous la forme d’une application web Azure :

![Interface pour configurer le déploiement sous la forme d’une application web Azure](./media/iot-solution-build-system/image7.png)

Et nous avons défini le déploiement toocontinuous déclencheur hello. Autrement dit, chaque archivage suivi par une build réussie des résultats dans une application web de toohello mise à jour.

![Interface pour la configuration de déploiement hello toocontinuous déclencheur](./media/iot-solution-build-system/image8.png)

Pour les applications mobiles, nous déployer tooHockeyApp :

![Interface pour le déploiement d’une application mobile de tooHockeyApp](./media/iot-solution-build-system/image9.png)

## <a name="explore-telemetry-by-using-application-insights"></a>Explorer les données de télémétrie à l’aide d’Application Insights
[Application Insights](../application-insights/app-insights-overview.md) collecte une télémétrie sur les performances de hello et d’utilisation de vos services web. Hello Application Insights SDK envoie des données de télémétrie de hello service toohello ressource Application Insights dans Azure.

Accédez à toohello ressource Application Insights ce modèle hello configuré. Là, vous pouvez explorer les graphiques des performances hello de votre [projet de Service d’application Mobile](https://github.com/Azure-Samples/MyDriving/tree/master/src/MobileAppService). Ils indiquent les demandes et temps de réponse du serveur, les échecs et le nombre d’exceptions. Il existe également des graphiques de dépendance de temps de réponse : autrement dit, base de données appelle toohello et tooREST API comme Machine Learning. S’il existe des problèmes de performances, vous serez en mesure de toosee quel élément de votre système est à l’origine les.

![Exemple de graphique de performances](./media/iot-solution-build-system/image11.png)

Si vous avez un service web que vous configurez manuellement, il tooget facile hello mêmes graphiques. Dans le panneau de service web hello, cliquez sur **outils** > **Extensions** > **ajouter**. Sélectionnez **Application Insights**.

![Interface de sélection de graphiques de hello tooget Application Insights](./media/iot-solution-build-system/image12.png)

fonctionnalité de Hello fonctionne en instrumentant votre application avec hello Application Insights SDK.

Vous pouvez ajouter des données de télémétrie personnalisée (ou instrumenter une application qui est en cours d’exécution quelque part en dehors d’Azure) en [Ajout hello Application Insights SDK](../application-insights/app-insights-asp-net.md) au moment du développement. Il s’agit de mesures toolog utiles qui varient selon l’application hello, telles que la longueur moyenne de voyage utilisateurs ou de la consommation totale. Dans Visual Studio, cliquez sur le projet de hello et sélectionnez **ajouter Application Insights**.

![Interface de sélection des données de télémétrie personnalisées ajouter Application Insights tooadd](./media/iot-solution-build-system/image10.png)

Application Insights envoie des alertes par e-mail s’il détecte un nombre inhabituel de réponses d’échec. Vous pouvez également configurer vos propres alertes pour différentes métriques, telles que les temps de réponse.

Toobe simplement assurer que votre service web est toujours opérationnel et en cours d’exécution, vous pouvez configurer [les tests de disponibilité](../application-insights/app-insights-monitor-web-app-availability.md). Ces tests ping sur votre site à partir de différents emplacements monde hello toutes les 15 minutes. Là encore, vous obtenez un message électronique s’il semble toobe un problème.

## <a name="estimate-operational-costs"></a>Estimer les coûts d’exploitation
Il est extrêmement économique toorun une application telle que celle-ci à petite échelle. Plusieurs services de hello ont des niveaux d’entrée de gamme libres, afin que le développement et l’opération à petite échelle coûtent très peu. Et bien sûr, vos propres applications n’ont pas toouse toutes les fonctionnalités de hello illustrées dans MyDriving.

Voici une estimation approximative de nos coûts lors de la définition de la configuration de développement hello pour MyDriving. Nous indiquons également des alternatives que nous n’avons *pas* utilisées. Ces informations peuvent être utiles quand vous estimez vos propres coûts.

Nous partons de l’hypothèse suivante :

* Une équipe de cinq personnes maximum (et des parties prenantes pour observation).
* En fonctionnement depuis un mois environ.
* 100 utilisateurs avec quatre trajets par jour.

> [!NOTE]
> Si vous êtes tooAzure nouveau, il existe un [libre compte](https://azure.microsoft.com/free/).
> 
> 

| **Service/composant** | **Remarques** | **Coût par mois** |
| --- | --- | --- |
| [Visual Studio 2015 Community](https://www.visualstudio.com/products/visual-studio-community-vs) avec [Xamarin](https://visualstudiogallery.msdn.microsoft.com/dcd5b7bd-48f0-4245-80b6-002d22ea6eee) <br/>Environnement de développement multiplateforme |Visual Studio Community. (Peut-être [Visual Studio Professional](https://www.visualstudio.com/vs-2015-product-editions) pour [Xamarin.Forms](https://xamarin.com/forms), toodesign inter-plateformes à partir d’une base de code unique.) |0 $ |
| [Azure IoT Hub](https://azure.microsoft.com/pricing/details/iot-hub/) <br/>Toodevices de connexion de données bidirectionnelle |8 000 messages + 0,5 Ko/message gratuit. |0 $ |
| [Stream Analytics](https://azure.microsoft.com/pricing/details/stream-analytics/)  <br/>    Traitement des données de flux à volume élevé |Facturation de 0,031 $ par unité de diffusion en continu par heure pendant l’activation. Vous choisissez nombre hello d’unités de diffusion en continu que vous le souhaitez. tooscale plus haut. |23 $ |
| [Machine Learning](https://azure.microsoft.com/documentation/services/machine-learning/)<br/>  Réponses adaptatives. |10 $/siège/mois. <br/>                                                                                                                                                                                 + 3 heures d’expérience \* $1 / heure d’expérience. <br/>                                                                                                                                                           + 3,5 heures UC d’API \* $2 / heure UC de production. <br/>                                                                                                                                                           Le temps processeur de l’API est basé sur une reformation de 5 min/jour, une augmentation pouvant se produire avec un volume supérieur de données d’entrée.                   <br/>                                                                                                                                                                     + min 2 jours score tooprocess 400 allers-retours/jour. |20 $ |
| [App Service](https://azure.microsoft.com/pricing/details/app-service/)  <br/>  pour l’hébergement des applications mobiles principales |Niveau B1 : applications web de production. |56 $ |
| [Visual Studio Team Services ](https://azure.microsoft.com/pricing/details/visual-studio-team-services/)  <br/>  Gestion des builds, des tests unitaires et de la mise en production ; gestion des tâches |Agents privés, cinq utilisateurs. |0 $ |
| [Application Insights](https://azure.microsoft.com/pricing/details/application-insights/) <br/>Surveillance des performances et de l’utilisation des sites et services web. |Niveau Gratuit. |0 $ |
| [HockeyApp](http://hockeyapp.net/pricing/) <br/>  Distribution d’applications en version bêta, et collecte de commentaires et de données d’utilisation et d’incident |Deux applications gratuites pour les nouveaux utilisateurs.<br/>  30 $ par mois par la suite. |0 $ |
| [Xamarin](https://store.xamarin.com/)<br/>  Code sur une plateforme unifiée pour plusieurs appareils |Essai gratuit. <br/>25 $ par mois par la suite. |0 $ |
| [SQL Database](https://azure.microsoft.com/pricing/details/sql-database/) pour Azure App Service |Niveau de base ; modèle de base de données unique. |5 $ |
| [Service Fabric](https://azure.microsoft.com/pricing/details/service-fabric/) (facultatif) |Exécution d’un cluster local. |0 $ |
| [Power BI](https://powerbi.microsoft.com/pricing/)<br/>  Affichage polyvalent et analyse des données par flux et statiques |Gratuit : 1 Go, 10 000 lignes/heure, actualisation quotidienne. <br/> 10 $/utilisateur/mois pour [limites supérieures](https://powerbi.microsoft.com/documentation/powerbi-power-bi-pro-content-what-is-it/), plus d’options de connexion, collaboration. |0 $ |
| [Stockage](https://azure.microsoft.com/pricing/details/storage/) |L (localement redondant) &lt; 100 Go 0,024 $/Go. |3 $ |
| [Data Factory](https://azure.microsoft.com/pricing/details/data-factory/) |0,60 $ par activité \* (8 - 5 FOC). |2 $ |
| [HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/) <br/>   Cluster à la demande pour reformation quotidienne |Trois nœuds A3 à 0,32 $/heure pour 1 heure par jour * 31 jours. |30 $ |
| [Hubs d'événements](https://azure.microsoft.com/pricing/details/event-hubs/) |De base avec unité de débit 11 $/mois + entrée 0,028 $. |11 $ |
| Dongle OBD | |12 $ |
| **Total** | |**157 $** |

Pour plus d'informations, consultez les pages suivantes :

* Récapitulatif des [limites et quotas de service Azure](../azure-subscription-service-limits.md#iot-hub-limits)
* [Calculatrice de prix](https://azure.microsoft.com/pricing/calculator/)

## <a name="send-us-your-feedback"></a>Envoyez-nous vos commentaires
Car nous avons créé des systèmes de votre propre IoT MyDriving toohelp jumpstart, nous voulons certainement toohear part sur le bon fonctionnement. Faites-nous savoir si :

* Vous rencontrez des difficultés ou des problèmes.
* Il existe un point d’extension qui peut la rendre plus adapté tooyour scénario.
* Vous trouverez un tooaccomplish de manière plus efficace de certains besoins.
* Vous avez des suggestions pour améliorer MyDriving ou cette documentation.

commentaires de toogive, [problème sur GitHub] du fichier ou de laisser un commentaire ci-dessous (en-us edition).

Nous attendons toohearing de votre part.

## <a name="next-steps"></a>Étapes suivantes
Nous vous recommandons de hello [Guide de référence MyDriving](http://aka.ms/mydrivingdocs), qui est une description complète de la conception de hello de hello système et ses composants.

