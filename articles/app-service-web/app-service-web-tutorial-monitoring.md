---
title: "une application Web d’aaaMonitor | Documents Microsoft"
description: "Découvrez comment tooset d’analyse sur votre application Web"
services: App-Service
keywords: 
author: btardif
ms.author: byvinyal
ms.date: 04/04/2017
ms.topic: article
ms.service: app-service-web
ms.openlocfilehash: c2f5e9842c732a804f1caee5d67e53dad24e190a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-app-service"></a>Surveiller App Service
Ce didacticiel vous guide et à surveiller votre application à l’aide de hello plateforme intégrées outils toosolve des problèmes lorsqu’ils se produisent.

Chaque section de ce document traite d’une fonctionnalité spécifique. L’utilisation conjointe de fonctionnalités de hello vous permettre de :
- Identifier un problème dans votre application.
- Détermination de lorsque le problème de hello est provoquée par la plateforme de votre code ou hello.
- Limiter les source hello problème de hello dans votre code.
- Déboguer et résoudre les problème de hello.

## <a name="before-you-begin"></a>Avant de commencer
- Vous avez besoin d’un toomonitor d’application Web et que vous suivez hello décrites comme suit.
    - Vous pouvez créer une application hello comme suit décrit dans hello [créer une application ASP.NET dans Azure avec la base de données SQL](app-service-web-tutorial-dotnet-sqldatabase.md) didacticiel.

- Si vous souhaitez tootry out **débogage distant** de votre application, vous avez besoin de Visual Studio.
    - Si vous n’avez pas encore Visual Studio 2017 installé, vous pouvez télécharger et utiliser hello libre [2017 de Visual Studio Community Edition](https://www.visualstudio.com/downloads/).
    - Assurez-vous que vous activez **le développement Azure** pendant l’installation de Visual Studio hello.

## <a name="metrics"></a> Étape 1 : Afficher les mesures
**Mesures** sont toounderstand utile :
- Intégrité d’application
- Performances de l’application
- Consommation des ressources

Lorsque vous recherchez un problème d’application, examen des métriques est un bon point toostart. Portail Azure a un moyen rapide de toovisually inspecter les métriques de votre application à l’aide de hello **Azure analyse**.

Les mesures offrent un historique de différentes agrégations clés pour votre application. Pour n’importe quelle application hébergée dans le service d’applications, vous devez surveiller hello Web App et hello plan App Service.

> [!NOTE]
> Un plan App Service représente collection hello de ressources physiques utilisées toohost vos applications. Toutes les applications tooan du Service d’applications plan partage hello les ressources affectées qu’elle vous permettant de coût de toosave lorsque plusieurs applications d’hébergement.
>
> Les plans App Service définissent :
> * Région : Europe du Nord, États-Unis de l’Est, Sud-Est asiatique, etc.
> * Taille d’instance : Petit, Moyen, Grand, etc.
> * Comptage : une, deux ou trois instances, etc.
> * Référence (SKU) : Gratuit, Partagé, De base, Standard, Premium, etc.

métriques de tooreview pour votre application Web, accédez toohello **vue d’ensemble** Panneau de l’application hello souhaité toomonitor. Un graphique des mesures de votre application est disponible sous forme de **vignette de surveillance**. Cliquez sur hello vignette tooedit et configurer le métriques tooview et hello toodisplay de plage de temps.

Par le panneau des ressources par défaut hello fournit une vue pour hello les demandes d’Application et les erreurs pour hello dernière heure.
![Application Monitor](media/app-service-web-tutorial-monitoring/app-service-monitor.png)

Comme vous pouvez le voir dans l’exemple de hello, nous disposons d’une application qui génère plusieurs **erreurs du serveur HTTP**. volume élevé de Hello d’erreurs est hello première indication nous devons tooinvestigate cette application.

> [!TIP]
> Plus d’informations sur Azure moniteur avec hello suivant liens :
> - [Prise en main d’Azure Monitor](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Mesures Azure](..\monitoring-and-diagnostics\monitoring-overview-metrics.md)
> - [Mesures prises en charge avec Azure Monitor](..\monitoring-and-diagnostics\monitoring-supported-metrics.md)
> - [Tableaux de bord Azure](..\azure-portal\azure-portal-dashboards.md)

## <a name="alerts"></a> Étape 2 : Configurer des alertes
**Alertes** peut être configuré tootrigger sur des conditions spécifiques de votre application.

Dans [étape 1 - des métriques de vue](#metrics), nous avons vu qu’application hello avait un grand nombre d’erreurs.

Permet de configurer une alerte tooautomatically soyez averti en cas d’erreur. Dans ce cas, nous souhaitez toosend d’alerte hello et envoyer par courrier électronique chaque fois que quantité, hello pour les erreurs HTTP 50 X dépasse un certain seuil.

toocreate une alerte, accédez trop**analyse** > **alertes** et cliquez sur **[+] ajouter une alerte**.

![Alertes](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts.png)

Fournir des valeurs pour la configuration d’alerte hello :
- **Ressource :** hello toomonitor de site avec l’alerte de hello.
- **Nom :** nom de votre alerte, ici : *Grand nombre d’erreurs HTTP 50X*.
- **Description :** explication textuelle de ce que l’alerte doit surveiller.
- **Alerte sur :** les alertes peuvent surveiller les mesures ou les événements, ici nous observons les mesures.
- **Métrique :** le métrique toomonitor, dans ce cas : *erreurs du serveur HTTP*.
- **Condition :** lorsque tooalert, dans ce cas, sélectionnez hello *supérieur* option.
- **Seuil :** What toolook de valeur, dans ce cas : *400*.
- **Période :** alertes s’exécutent sur la valeur moyenne de hello d’une métrique. Les périodes plus courtes génèrent des alertes plus sensibles. Dans notre exemple, nous choisissons *5 minutes*.
- **Envoyer un courrier électronique aux propriétaires et aux contributeurs :** ici : *Activé*.

Maintenant que hello alerte est créée un message électronique est envoyée chaque fois que hello application dépasse le seuil de hello configuré. Alertes actives peuvent être consultées dans hello portail Azure.

![Alertes déclenchées](media/app-service-web-tutorial-monitoring/app-service-monitor-alerts-triggered.png)


> [!TIP]
> Plus d’informations sur les alertes Azure avec hello suivant liens :
> - [Que sont les alertes dans Microsoft Azure](..\monitoring-and-diagnostics\monitoring-overview-alerts.md)
> - [Effectuer une opération sur les mesures](..\monitoring-and-diagnostics\monitoring-overview.md)
> - [Créer des alertes de mesures](..\monitoring-and-diagnostics\insights-alerts-portal.md)

## <a name="companion"></a> Étape 3 : Compagnon App Service
**Le Guide du Service d’applications** offre un moyen pratique de toomonitor votre application avec une expérience native sur votre appareil mobile (iOS ou Android).

Utilisez le compagnon App Service pour :
- consulter les mesures d’application,
- consulter et agir sur les alertes d’application et les recommandations,
- Effectuer le dépannage de base (Parcourir, Démarrer, arrêter, redémarrer hello application)
- Obtenez des notifications push pour les événements critiques.

![Compagnon App Service](media/app-service-web-tutorial-monitoring/app-service-companion.png)

[![Compagnon App Service - App Store](media/app-service-web-tutorial-monitoring/app-service-companion-appStore.png)](https://itunes.apple.com/app/azure-app-service-companion/id1146659260)
[![Compagnon App Service - Google Play](media/app-service-web-tutorial-monitoring/app-service-companion-googlePlay.png)](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

Vous pouvez installer le Guide du Service d’applications à partir de hello [App Store](https://itunes.apple.com/app/azure-app-service-companion/id1146659260) ou [Google Play](https://play.google.com/store/apps/details?id=azureApps.AzureApps)

## <a name="diagnose"></a> Étape 4 : Diagnostiquer et résoudre les problèmes
**Diagnostiquer et résoudre les problèmes** permet de distinguer les problèmes d’application des problèmes de plateforme. Il peut également suggérer des tooget de limiter les risques votre toohealthy précédent de l’application Web.

![Diagnostiquer et résoudre les problèmes](media/app-service-web-tutorial-monitoring/app-service-monitor-diagnosis.png)

Continuer avec les étapes précédentes du formulaire exemple hello, nous pouvons voir qu’application hello a été difficultés marquée. En revanche, la disponibilité de plateforme hello n’a pas déplacé de 100 %.

Lorsque application hello pose problème et hello reste plateforme haut, il est montre clairement que nous avons affaire à un problème d’application.

## <a name="logging"></a> Étape 5 - Journalisation
Maintenant que nous avons cerner le problème d’application hello échecs tooan, nous pouvons examiner tooget de journaux des applications et le serveur hello plus d’informations.

Journalisation permet de toocollect les deux **Application Diagnostics** et **Diagnostics du serveur Web** journaux pour votre application Web.

### <a name="application-diagnostics"></a>Diagnostics d’application
Application diagnostics permet de traces toocapture vous produites par l’application hello lors de l’exécution.

Ajout de traçage tooyour application améliore considérablement votre capacité toodebug et les problèmes liés au point de code confidentiel.

Dans ASP.NET, vous pouvez vous connecter à l’aide de traces d’application [classe System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx) toogenerate les événements capturés par l’infrastructure de journal hello. Vous pouvez également spécifier la gravité hello de trace hello pour le filtrage plus facile.

```csharp
public ActionResult Delete(Guid? id)
{
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id);
    if (id == null)
    {
        System.Diagnostics.Trace.TraceError("/Todos/Delete/ failed, ID is null");
        return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
    }
    Todo todo = db.Todoes.Find(id);
    if (todo == null)
    {
        System.Diagnostics.Trace.TraceWarning("/Todos/Delete/ failed, ID: " + id + " could not be found");
        return HttpNotFound();
    }
    System.Diagnostics.Trace.TraceInformation("GET /Todos/Delete/" + id + "completed successfully");
    return View(todo);
}
```
journal des applications tooenable accédez trop**analyse** > **journaux de Diagnostic** et activer l’Application enregistre à l’aide de hello bascule.

![Surveiller l’application](media/app-service-web-tutorial-monitoring/app-service-monitor-applogs.png)

Journaux des applications peuvent être de système de fichiers de l’application Web de tooyour stockée ou poussé tooblob stockage. Pour les scénarios de production, il est recommandé toouse stockage d’objets blob.

> [!IMPORTANT]
> L’activation de la journalisation a une incidence sur les performances de votre application et sur l’utilisation des ressources. Pour les scénarios de production, les journaux d’erreurs sont recommandés. Activez une journalisation plus détaillée uniquement en cas de problème.

 ### <a name="web-server-diagnostics"></a>Diagnostics de serveur web
Les journaux des serveurs web sont générés même si votre application n’est pas instrumentée. App Service peut collecter trois types de journaux de serveur :

- **Journalisation du serveur web**
    - Informations sur les transactions HTTP à l’aide de hello [format de fichier journal étendu W3C](https://msdn.microsoft.com/library/windows/desktop/aa814385.aspx).
    - Utile lors de la détermination des métriques d’un site global comme nombre hello de demandes traitées ou le nombre de requêtes qui proviennent d’une adresse IP spécifique.
- **Messages d’erreurs détaillés**
    - Informations d’erreur détaillées pour les codes d’état HTTP qui indiquent un échec (code d’état 400 ou supérieur).
    - [En savoir plus sur la journalisation d’erreurs détaillée](https://www.iis.net/learn/troubleshoot/diagnosing-http-errors/how-to-use-http-detailed-errors-in-iis)
- **Suivi des demandes ayant échoué**
    - Des informations détaillées sur les demandes ayant échoué, y compris une trace des composants d’IIS hello utilisé tooprocess hello demande et hello temps dans chaque composant.
    - Les journaux de demandes ayant échoué sont utiles lors de la tentative de tooisolate ce qui provoque une erreur HTTP spécifique.
    - [En savoir plus sur le suivi des demandes ayant échoué](https://www.iis.net/learn/troubleshoot/using-failed-request-tracing/troubleshooting-failed-requests-using-tracing-in-iis)

journalisation du serveur tooenable :
- Accédez trop**analyse** > **journaux de Diagnostic**.
- Activer hello différents types de Diagnostics du serveur Web à l’aide de hello bascule.

![Surveiller l’application](media/app-service-web-tutorial-monitoring/app-service-monitor-serverlogs.png)

> [!IMPORTANT]
> L’activation de la journalisation a une incidence sur les performances de votre application et sur l’utilisation des ressources. Pour les scénarios de production, les journaux d’erreurs sont recommandés. Activez une journalisation plus détaillée uniquement en cas de problème.

### <a name="accessing-logs"></a>Accès aux journaux
Les journaux enregistrés dans le stockage d’objets blob sont accessibles à l’aide de l’Explorateur de stockage Microsoft Azure. Journaux stockés dans le système de fichiers de l’application hello Web sont accessibles via FTP sous hello suivant des chemins d’accès :

- **Journaux d’application** - `%HOME%/LogFiles/Application/`
    - Ce dossier contient un ou plusieurs fichiers texte contenant des informations générées dans le cadre de la journalisation des applications.
- **Suivi des demandes ayant échoué** - `%HOME%/LogFiles/W3SVC#########/`
    - Ce dossier contient un fichier XSL et un ou plusieurs fichiers XML.
- **Journaux d’erreurs détaillés** - `%HOME%/LogFiles/DetailedErrors/`
    - Ce dossier contient un ou plusieurs fichiers .htm incluant des informations détaillées sur les erreurs HTTP générées par votre application.
- **Journaux des serveurs web** - `%HOME%/LogFiles/http/RawLogs`
    - Ce dossier contient un ou plusieurs fichiers de texte formatés à l’aide du format de fichier journal étendu hello W3C.

## <a name="streaming"></a> Étape 6 - Diffusion de journaux
Journaux de diffusion en continu sont pratiques lorsque vous déboguez une application, car elle enregistre le temps par rapport trop[l’accès aux journaux de hello](#Accessing-Logs) via FTP.

App Service peut diffuser les **journaux d’application** et les **journaux de serveur web** lorsqu’ils sont générés.

> [!TIP]
> Avant d’essayer de journaux de toostream, assurez-vous que vous avez activé la collecte des journaux comme décrit dans hello [journalisation](#logging) section.

journaux de toostream, accédez trop**analyse**> **flux du journal**. Sélectionnez **Journaux d’application** ou **Journaux des serveurs web** en fonction des informations que vous recherchez. À ce stade, vous pouvez aussi suspendre, redémarrer et vider le tampon de hello.

![Journaux en continu](media/app-service-web-tutorial-monitoring/app-service-monitor-logstream.png)

> [!TIP]
> Les journaux sont générés uniquement lorsque l’application hello est le trafic, vous pouvez également augmenter détail hello de tooget de journaux des événements ou des informations plus.

## <a name="remote"></a> Étape 7 - Débogage à distance
Une fois que vous avez source hello de branches de code confidentiel des problèmes d’applications hello, utilisez **débogage distant** toowalk via le code de hello.

Permet de débogage distant vous attacher un débogueur de tooyour application Web en cours d’exécution dans le cloud de hello. Vous pouvez définir des points d’arrêt, manipuler directement de mémoire, parcourir le code et même modifier le chemin d’accès du code hello exactement comme vous le feriez pour une application en cours d’exécution localement.

tooattach hello débogueur tooyour l’application en cours d’exécution dans le cloud de hello :

- À l’aide de Visual Studio 2017, solution hello ouvert pour l’application hello souhaité toodebug
- Définissez des points d’arrêt comme vous le feriez pour un développement en local.
- Ouvrez **l’explorateur de cloud** (ctr + /, ctrl + x).
- Connectez-vous avec vos informations d’identification Azure.
- Rechercher hello application toodebug
- Sélectionnez **attacher le débogueur** hello du formulaire **Actions** volet.

![Débogage à distance](media/app-service-web-tutorial-monitoring/app-service-monitor-vsdebug.png)

Visual Studio configure votre application pour le débogage distant et lance une fenêtre de navigateur qui navigue tooyour application. Parcourir votre application tootrigger des points d’arrêt et de parcourir le code de hello.

> [!WARNING]
> Nous vous déconseillons d'exécuter le mode débogage en production. Si votre application de production n’est pas mis à l’échelle des instances de serveur toomultiple, débogage empêcher serveur hello web répond tooother demandes. Pour résoudre des problèmes de production, votre meilleure ressource est trop[configurer la journalisation](#logging) et [Application Insights](#insights).



## <a name="explorer"></a> Étape 8 : Process Explorer
Lorsque votre application est remontée toomore plusieurs instances, **Explorateur de processus** peut vous aider à identifier des problèmes spécifiques d’instance.

Utilisez **Process Explorer** pour :

- Énumérer tous les processus hello entre différentes instances de votre plan App Service.
- Extraire et afficher les poignées de hello et modules associés à chaque processus.
- Nombre d’UC de la vue, le jeu de travail et le Thread à hello traiter au niveau toohelp vous identifier les processus d’échappement
- rechercher des descripteurs de fichiers ouverts, voire arrêter une instance de processus spécifique.

Process Explorer se trouve sous **Surveillance** > **Process Explorer**.

![Process Explorer](media/app-service-web-tutorial-monitoring/app-service-monitor-processexplorer.png)


## <a name="insights"></a> Étape 9 - Application Insights
**Application Insights** fournit des fonctionnalités avancées de profilage et de surveillance de votre application.

Utilisez Application Insights toodetect et diagnostiquer les problèmes de performances dans votre application Web et les exceptions.

Vous pouvez activer Application Insights pour votre application web sous **Surveillance** > **Application Insights**.

> [!NOTE]
> Application Insights peuvent vous inviter tooinstall hello Application Insights site extension toostart collecte de données. Installation de l’extension de site hello entraîne un redémarrage de l’application.

![Application Insights](media/app-service-web-tutorial-monitoring/app-service-monitor-appinsights.png)

Application Insights a un grand nombre de fonctionnalités défini, toolearn, suivez les liens de hello inclus dans hello [étapes](#next) section.

## <a name="next"></a> Étapes suivantes

 - [Présentation d’Application Insights](..\application-insights\app-insights-overview.md)
 - [Surveiller les performances de l’application web Azure avec Application Insights](..\application-insights\app-insights-azure-web-apps.md)
 - [Analyse de la disponibilité et de la réactivité d’un site web avec Application Insights](..\application-insights\app-insights-monitor-web-app-availability.md)
