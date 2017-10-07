---
title: "aaaTroubleshooting aucune donnée - Application Insights pour .NET"
description: "Vous ne voyez pas de données dans Azure Application Insights ? Essayez ici."
services: application-insights
documentationcenter: .net
author: CFreemanwa
manager: carmonm
ms.assetid: e231569f-1b38-48f8-a744-6329f41d91d3
ms.service: application-insights
ms.workload: mobile
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: bwren
ms.openlocfilehash: 261c25c89884c46e41bbc305474ac854360221ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-no-data---application-insights-for-net"></a>Guide de dépannage : Application Insights pour .NET
## <a name="some-of-my-telemetry-is-missing"></a>Certaines de mes données télémétriques manquent
*Dans Application Insights, je vois uniquement une fraction d’événements hello qui sont générés par mon application.*

* Si vous rencontrez régulièrement hello même fraction, tooadaptive probablement en raison de sa [échantillonnage](app-insights-sampling.md). tooconfirm, ouvrir la recherche (depuis le panneau de vue d’ensemble de hello) et que vous examinez une instance d’une demande ou d’autres événements. En bas de hello de la section des propriétés hello cliquez sur «... » tooget complète de la propriété. Si le nombre de requêtes est supérieur à 1, l’échantillonnage est en cours. 
* Dans le cas contraire, il est possible que vous rencontriez une [limite de débit](app-insights-pricing.md#limits-summary) pour votre plan tarifaire. Ces limites sont appliquées par minute.

## <a name="no-data-from-my-server"></a>Aucune donnée de mon serveur
*J’ai installé l’application sur mon serveur web et maintenant je ne vois pas les données de télémétrie à partir de celui-ci. Cela a fonctionné correctement sur mon ordinateur de développement.*

* Probablement un problème de pare-feu. [Définir des exceptions de pare-feu pour les données d’Application Insights toosend](app-insights-ip-addresses.md).

*Je [installé Status Monitor](app-insights-monitor-performance-live-website-now.md) sur mon toomonitor serveur web pour les applications existantes. Aucun résultat ne s’affiche.*

* Consultez [Résolution des problèmes liés à Status Monitor](app-insights-monitor-performance-live-website-now.md#troubleshooting-runtime-configuration-of-application-insights). 

## <a name="q01"></a>Aucune option « Ajouter Application Insights » dans Visual Studio
*Lorsque j’effectue un clic droit sur le projet existant dans l’Explorateur de solutions, je ne vois aucune option Application Insights.*

* Pas de tous les types de projet .NET sont pris en charge par les outils de hello. Les projets Web et WCF sont pris en charge. Pour les autres types de projet, telles que les applications de bureau ou de service, vous pouvez toujours [ajouter un projet d’Application Insights SDK tooyour manuellement](app-insights-windows-desktop.md).
* Vérifiez que vous disposez de [Visual Studio 2013 Update 3 ou version ultérieure](http://go.microsoft.com/fwlink/?LinkId=397827). Il est fourni avec les outils de développement Analytique, qui fournissent des hello Application Insights SDK préinstallé.
* Sélectionnez **Outils**, **Extensions et mises à jour**, puis vérifiez l’installation et l’activation des outils **Analyse développeur**. Dans ce cas, cliquez sur **mises à jour** toosee si une mise à jour est disponible.
* Ouvrez la boîte de dialogue Nouveau projet hello et choisissez l’application Web ASP.NET. Si vous voyez hello option d’Application Insights, puis hello outils sont installés. Si ce n’est pas le cas, essayez de désinstaller puis réinstaller les outils hello Application Insights.

## <a name="q02"></a>Échec de l’ajout d’Application Insights
*Lorsque vous essayez d’un projet existant tooadd Application Insights tooan, je vois un message d’erreur.*

Causes probables :

* Échec de la communication avec le portail Application Insights de hello ; ou
* votre compte Azure présente un problème ;
* Il vous suffit [accès en lecture toohello abonnement ou un groupe dans lequel vous essayez de ressource hello toocreate](app-insights-resources-roles-access-control.md).

Correctif :

* Vérifiez que vous avez fourni les informations d’identification de connexion pour le droit hello compte Azure. 
* Dans votre navigateur, vérifiez que vous avez accès toohello [portail Azure](https://portal.azure.com). Ouvrez Paramètres et vérifiez s’il existe des restrictions.
* [Un projet existant ajouter Application Insights tooyour](app-insights-asp-net.md): dans l’Explorateur de solutions, cliquez avec le bouton droit sur votre projet et choisissez « Ajouter Application Insights. »
* Si elle ne fonctionne toujours pas, suivez hello [procédure manuelle](app-insights-windows-services.md) tooadd une ressource dans le portail de hello, puis ajoutez le projet de tooyour hello SDK. 

## <a name="emptykey"></a>J’obtiens une erreur « La clé d’instrumentation ne peut pas être vide ».
Il semble qu'une erreur est survenue durant l'installation d'Application Insights ou d'un enregistreur de données.

Dans l’explorateur de solutions, cliquez avec le bouton droit sur votre projet, puis sélectionnez **Application Insights > Configurer Application Insights**. Vous obtenez une boîte de dialogue qui vous invite toosign dans tooAzure et créez une ressource Application Insights, ou réutiliser un existant.

## <a name="NuGetBuild"></a> « Packages NuGet manquants » sur mon serveur de builds
*Tous les éléments génère OK lorsque je suis le débogage sur mon ordinateur de développement, mais j’obtiens une erreur de NuGet sur le serveur de builds hello.*

Consultez les sections relatives à la [restauration des packages NuGet](http://docs.nuget.org/Consume/Package-Restore) et à la [restauration automatique des packages](http://docs.nuget.org/Consume/package-restore/migrating-to-automatic-package-restore).

## <a name="missing-menu-command-tooopen-application-insights-from-visual-studio"></a>Manquant tooopen de commande de menu Application Insights à partir de Visual Studio
*Lorsque j’effectue un clic droit sur mon projet Explorateur de solutions, je ne vois pas toutes les commandes Application Insights, ou je ne vois pas de commande Ouvrir Application Insights.*

Causes probables :

* Si vous avez créé des ressources d’Application Insights hello manuellement, ou si le projet de hello est d’un type qui n’est pas pris en charge par les outils Application Insights hello.
* outils de développement Analytique Hello sont désactivées dans votre Visual Studio. 
* Votre version de Visual Studio est antérieure à 2013 Mise à jour 3.

Correctif :

* assurez-vous que votre version de Visual Studio est bien 2013 Mise à jour 3 ou une version ultérieure.
* Sélectionnez **Outils**, **Extensions et mises à jour**, puis vérifiez l’installation et l’activation des outils **Analyse développeur**. Dans ce cas, cliquez sur **mises à jour** toosee si une mise à jour est disponible.
* Cliquez avec le bouton droit sur l’Explorateur de solutions. Si vous voyez la commande hello **Application Insights > configurer Application Insights**, utilisez-le tooconnect votre ressource de toohello projet Bonjour service Application Insights.

Dans le cas contraire, votre type de projet n’est pas directement pris en charge par les outils Application Insights hello. toosee votre télémétrie, connectez-vous toohello [portail Azure](https://portal.azure.com), choisissez Application Insights sur la barre de navigation gauche hello, sélectionnez votre application.

## <a name="access-denied-on-opening-application-insights-from-visual-studio"></a>« Accès refusé » lors de l’ouverture d’Application Insights dans Visual Studio
*Hello commande de menu « Ouvrir Application Insights » me prend toohello portail Azure, mais j’obtiens une erreur « accès refusé ».*

![](./media/app-insights-asp-net-troubleshoot-no-data/access-denied.png)

Hello Microsoft connectez-vous que vous avez utilisé dans votre navigateur par défaut n’a pas accès trop[hello ressource créé lors de l’Application Insights a été ajouté toothis application](app-insights-asp-net.md). Il existe deux raisons possibles : 

* Vous avez plusieurs comptes Microsoft - peut-être un travail et un compte Microsoft personnel ? Hello sign-in que vous avez utilisé dans votre navigateur par défaut a été associée à un autre compte que hello qui dispose d’un accès trop[ajouter Application Insights toohello projet](app-insights-asp-net.md). 
  
  * Correctif : Cliquez sur votre nom en haut à droite de la fenêtre de navigateur hello et se déconnecter. Connectez-vous ensuite à compte hello qui a accès. Sur la barre de navigation gauche hello, cliquez sur Application Insights puis sélectionnez votre application.
* Quelqu'un d’autre ajouté le projet d’Application Insights toohello, et ils l’ont oublié toogive vous [groupe de ressources accès toohello](app-insights-resources-roles-access-control.md) dans lequel elle a été créée. 
  
  * Correctif : Si elles utilisé un compte professionnel, ils peuvent ajouter vous toohello équipe ; ou ils peuvent accorder vous accès individuels toohello groupe de ressources.

## <a name="asset-not-found-on-opening-application-insights-from-visual-studio"></a>« Actif introuvable » lors de l’ouverture d’Application Insights dans Visual Studio
*Hello commande de menu « Ouvrir Application Insights » me prend toohello portail Azure, mais j’obtiens une erreur « ressource introuvable ».*

Causes probables :

* Hello ressource Application Insights pour votre application a été supprimé ; ou
* clé d’instrumentation Hello a été défini ou modifié dans ApplicationInsights.config en le modifiant directement, sans mettre à jour le fichier de projet hello. 

clé d’instrumentation Hello dans les contrôles ApplicationInsights.config où les données de télémétrie hello sont envoyée. Une ligne dans le fichier de projet hello détermine quelle ressource est ouvert lorsque vous utilisez la commande hello dans Visual Studio. 

Correctif :

* Dans l’Explorateur de solutions, cliquez sur le projet de hello et choisissez Application Insights, configurer Application Insights. Dans la boîte de dialogue hello, vous pouvez sélectionnez télémétrie toosend tooan une ressource existante ou créez-en un. Ou :
* Ressource hello ouvrir directement. Connectez-vous trop[hello portail Azure](https://portal.azure.com)et cliquez sur Application Insights sur la barre de navigation gauche hello, puis sélectionnez votre application.

## <a name="where-do-i-find-my-telemetry"></a>Où puis-je trouver mes données de télémétrie ?
*J’ai connecté toohello [portail Microsoft Azure](https://portal.azure.com), et je regarde hello tableau de bord de base Azure. Alors, où puis-je trouver mes données Application Insights ?*

* Sur la barre de navigation gauche hello, cliquez sur Application Insights, puis le nom de votre application. Si vous n’avez pas il tous les projets, vous devez trop[ajouter ou configurer Application Insights dans votre projet web](app-insights-asp-net.md).
  
    Vous allez voir certains graphiques récapitulatifs. Vous pouvez cliquer sur les toosee décrit plus en détail.
* Dans Visual Studio, pendant que vous déboguez votre application, cliquez sur hello Application Insights.

## <a name="q03"></a> Aucune donnée sur serveur (ou aucune donnée)
*J’ai exécuté mon application et puis ouvert le service d’Application Insights hello dans Microsoft Azure, mais tous les hello graphiques s’affichent « en savoir comment toocollect... » ou « Non configuré ».* Ou *Mode page et données utilisateur uniquement, mais aucune donnée de serveur.*

* Exécutez votre application en mode Débogage dans Visual Studio (F5). Utilisez application hello donc comme toogenerate certaines données de télémétrie. Vérifiez que vous pouvez voir les événements consignés dans la fenêtre de sortie de Visual Studio hello. 
  
    ![](./media/app-insights-asp-net-troubleshoot-no-data/output-window.png)
* Dans le portail Application Insights hello, ouvrez [recherche Diagnostic](app-insights-diagnostic-search.md). En général, les données s’affichent d’abord ici.
* Cliquez sur le bouton d’actualisation hello. Panneau de Hello s’actualise régulièrement, mais vous pouvez le faire aussi manuellement. intervalle d’actualisation Hello est plus long pour les plages de temps supérieure.
* Vérifiez que hello instrumentation clés correspondent. Sur le panneau principal de hello pour votre application dans le portail Application Insights hello, Bonjour **Essentials** liste déroulante, regardez **clé d’Instrumentation**. Ensuite, dans votre projet dans Visual Studio, ouvrez ApplicationInsights.config et recherche hello `<instrumentationkey>`. Vérifiez que hello deux clés sont égales. Si ce n’est pas le cas :
  
  * Dans le portail hello, cliquez sur Application Insights et recherchez les ressources d’application hello touche hello ; ou
  * Dans l’Explorateur de solutions Visual Studio, cliquez sur le projet de hello et choisissez Application Insights, configurer. Réinitialiser hello toosend télémétrie toohello droite la ressource application.
  * Si vous ne trouvez pas hello clés correspondantes, vérifiez que vous utilisez hello mêmes informations de connexion dans Visual Studio comme dans toohello portal.
    
    ![](./media/app-insights-asp-net-troubleshoot-no-data/ikey-check.png)
* Bonjour [tableau de bord accueil Microsoft Azure](https://portal.azure.com), examinez le mappage de contrôle d’intégrité du Service hello. S’il existe certaines indications d’alerte, patientez jusqu'à ce qu’ils ont retourné tooOK puis fermez et rouvrez le panneau des applications Application Insights.
* Vérifiez également [notre blog d'état](http://blogs.msdn.com/b/applicationinsights-status/).
* Avez-vous écrit tout code hello [côté serveur SDK](app-insights-api-custom-events-metrics.md) qui peuvent changer la clé d’instrumentation hello `TelemetryClient` instances ou dans `TelemetryContext`? Ou avez-vous rédigé une [configuration de filtre ou d’échantillonnage](app-insights-api-filtering-sampling.md) trop exclusive ?
* Si vous avez modifié ApplicationInsights.config, vérifiez attentivement configuration hello de [TelemetryInitializers et TelemetryProcessors](app-insights-api-filtering-sampling.md). Un paramètre ou nommé de manière incorrecte le type ne peut provoquer hello SDK toosend aucune données.

## <a name="q04"></a>Aucune donnée sur l’affichage des pages, les navigateurs et l’utilisation
*Voir les données dans le temps de réponse de serveur et les graphiques de demandes de serveur, mais aucune donnée dans le temps de chargement de la Page vue ou dans hello navigateur ou des panneaux de l’utilisation.*

les données de salutation est fourni à partir de scripts dans des pages web hello. 

* Si vous avez ajouté tooan Application Insights existante du projet web, [vous avez des scripts de hello tooadd manuellement](app-insights-javascript.md).
* Assurez-vous que Microsoft Internet Explorer n'affiche pas votre site en mode de compatibilité.
* Utilisez la fonctionnalité de débogage de navigateur hello (F12 dans certains navigateurs, puis choisissez réseau) tooverify que des données sont envoyées trop`dc.services.visualstudio.com`.

## <a name="no-dependency-or-exception-data"></a>Aucune donnée de dépendance ou d’exception
Voir [télémétrie des dépendances](app-insights-asp-net-dependencies.md) et [télémétrie d’exception](app-insights-asp-net-exceptions.md).

## <a name="no-performance-data"></a>Aucune donnée de performances
Les données de performances (UC, taux d’E/S, etc.) sont disponibles pour les [services web Java](app-insights-java-collectd.md), les [applications de bureau Windows](app-insights-windows-desktop.md), les [services et applications web IIS si vous installez le moniteur d’état (Status monitor)](app-insights-monitor-performance-live-website-now.md) et [Azure Cloud Services](app-insights-azure.md). Ces données figurent sous Paramètres, Serveurs.

Ces données ne sont pas disponibles pour les sites web Azure.

## <a name="no-server-data-since-i-published-hello-app-toomy-server"></a>Aucune donnée (serveur), car le serveur application toomy hello publié
* Vérifiez que vous avez copié réellement hello tous les Microsoft. DLL de ApplicationInsights toohello serveur, ainsi que de Microsoft.Diagnostics.Instrumentation.Extensions.Intercept.dll
* Dans votre pare-feu, vous pouvez avoir trop[ouvrir certains ports TCP](app-insights-ip-addresses.md#data-access-api).
* Si vous disposez d’un proxy toosend toouse hors de votre réseau d’entreprise, définissez [defaultProxy](https://msdn.microsoft.com/library/aa903360.aspx) dans le fichier Web.config
* Windows Server 2008 : Vérifiez que vous avez installé hello après les mises à jour : [KB2468871](https://support.microsoft.com/kb/2468871), [KB2533523](https://support.microsoft.com/kb/2533523), [KB2600217](https://support.microsoft.com/kb/2600217).

## <a name="i-used-toosee-data-but-it-has-stopped"></a>J’ai utilisé toosee données, mais il s’est arrêté.
* Vérifiez hello [blog de l’état](http://blogs.msdn.com/b/applicationinsights-status/).
* Vous souhaitez savoir si vous avez atteint votre quota mensuel de points de données ? Ouvrez hello paramètres/Quota et toofind tarification out. Le cas échéant, vous pouvez mettre à niveau votre forfait ou payer pour disposer d’une capacité supplémentaire. Consultez hello [tarification schéma](https://azure.microsoft.com/pricing/details/application-insights/).

## <a name="i-dont-see-all-hello-data-im-expecting"></a>Je ne vois pas toutes les données hello que je suis attendu
Si votre application envoie une grande quantité de données et que vous utilisez hello Application Insights SDK pour ASP.NET version 2.0.0-beta3 ou une version ultérieure, hello [échantillonnage adaptive](app-insights-sampling.md) fonctionnalité peut fonctionner et envoyer seulement un pourcentage de votre télémétrie. 

Vous pouvez le désactiver, mais cela n’est pas recommandé. L’échantillonnage est conçu pour que la télémétrie associée soit correctement transmise pour faciliter le diagnostic. 

## <a name="wrong-geographical-data-in-user-telemetry"></a>Données géographiques erronées dans la télémétrie de l’utilisateur
dimensions de pays, région et ville de Hello proviennent des adresses IP et ne sont pas toujours exactes.

## <a name="exception-method-not-found-on-running-in-azure-cloud-services"></a>Exception « méthode introuvable » lors de l’exécution dans Services cloud Azure
Avez-vous effectué une génération pour .NET 4.6 ? 4.6 n’est pas automatiquement pris en charge dans les rôles Azure Cloud Services. [Installez la version 4.6 sur chaque rôle](../cloud-services/cloud-services-dotnet-install-dotnet.md) avant d’exécuter votre application.

## <a name="still-not-working"></a>Ne fonctionne toujours pas...
* [Forum Application Insights](https://social.msdn.microsoft.com/Forums/vstudio/en-US/home?forum=ApplicationInsights)

