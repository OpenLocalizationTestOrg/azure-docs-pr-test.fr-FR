---
title: aaaTroubleshoot Application Insights dans un projet de web Java
description: "Guide de dépannage : surveillance des applications Java en direct avec Application Insights."
services: application-insights
documentationcenter: java
author: CFreemanwa
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: bwren
ms.openlocfilehash: c274c01b1992971fae194c3e510512ca06ab76b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Guide de dépannage et questions-réponses concernant Application Insights pour Java
Vous avez des questions concernant [Azure Application Insights dans Java][java] ou vous rencontrez des problèmes ? Voici quelques conseils.

## <a name="build-errors"></a>Erreurs de build
**Dans Eclipse, lors de l’ajout de hello Application Insights SDK via Maven ou Gradle, j’obtiens build ou la somme de contrôle des erreurs de validation.**

* Si hello dépendance <version> élément utilise un modèle avec des caractères génériques (par exemple, (Maven) `<version>[1.0,)</version>` ou (Gradle) `version:'1.0.+'`), essayez de spécifier une version spécifique à la place comme `1.0.2`. Consultez hello [notes de publication](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) pour la version la plus récente hello.

## <a name="no-data"></a>Absence de données
**J’ai ajouté Application Insights avec succès et que vous avez exécuté mon application, mais j’ai constaté jamais de données dans le portail de hello.**

* Attendez une minute, puis cliquez sur Actualiser. graphiques de Hello eux-mêmes actualiser régulièrement, mais vous pouvez également actualiser manuellement. intervalle d’actualisation Hello dépend de la plage de temps hello du graphique de hello.
* Vérifiez que vous disposez d’une clé d’instrumentation définie dans le fichier de ApplicationInsights.xml hello (dans le dossier de ressources hello dans votre projet)
* Vérifiez qu’il y a aucune `<DisableTelemetry>true</DisableTelemetry>` nœud hello du fichier xml.
* Dans votre pare-feu, vous pouvez avoir tooopen les ports TCP 80 et 443 pour toodc.services.visualstudio.com de trafic sortant. Consultez hello [la liste complète des exceptions de pare-feu](app-insights-ip-addresses.md)
* Bonjour Microsoft Azure démarrer du tableau, examinez le mappage d’état service hello. S’il existe certaines indications d’alerte, patientez jusqu'à ce qu’ils ont retourné tooOK puis fermez et rouvrez le panneau des applications Application Insights.
* Activer la journalisation de fenêtre de console toohello IDE, en ajoutant un `<SDKLogger />` élément sous le nœud racine de hello dans le fichier de ApplicationInsights.xml hello (dans le dossier de ressources hello dans votre projet) et pour les entrées précédés [erreur].
* Vérifiez que hello correct ApplicationInsights.xml fichier a été chargé avec succès par hello Kit de développement logiciel Java, en examinant les messages de sortie de la console hello pour une instruction « fichier de Configuration a été trouvé ».
* Si le fichier de configuration hello est introuvable, vérifiez toosee de messages de sortie hello où le fichier de configuration hello est recherché et assurez-vous que hello Qu'applicationinsights.XML se trouve dans un de ces emplacements de recherche. En règle générale, vous pouvez placer le fichier de configuration hello près de fichiers JAR les SDK Insights de l’Application hello. Par exemple : dans Tomcat, cela signifie que le dossier WEB-INF/lib de hello.

#### <a name="i-used-toosee-data-but-it-has-stopped"></a>J’ai utilisé toosee données, mais il s’est arrêté.
* Vérifiez hello [blog de l’état](http://blogs.msdn.com/b/applicationinsights-status/).
* Vous souhaitez savoir si vous avez atteint votre quota mensuel de points de données ? Ouvrez Paramètres/Quota et toofind tarification out. Le cas échéant, vous pouvez mettre à niveau votre forfait ou payer pour disposer d’une capacité supplémentaire. Consultez hello [tarification schéma](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-hello-data-im-expecting"></a>Je ne vois pas toutes les données hello que je suis attendu
* Ouvrez hello Quotas et la tarification de lames et vérifiez si [échantillonnage](app-insights-sampling.md) est dans l’opération. (transmission de 100 % signifie que l’échantillonnage n’est pas dans l’opération). Hello service Application Insights peut être ensemble tooaccept qu’une fraction des données de télémétrie hello qui arrive à partir de votre application. Cela vous permet de respecter votre quota mensuel de télémétrie. 

## <a name="no-usage-data"></a>Absence de données d'utilisation
**Je vois des données concernant les requêtes et les temps de réponse, mais rien concernant les affichages de pages, le navigateur ou les données utilisateur.**

Vous définissez correctement vos données de télémétrie application toosend à partir du serveur de hello. À présent, votre prochaine étape trop[configurer votre télémétrie toosend de pages web à partir du navigateur web de hello][usage].

Si votre client est une application d’un [téléphone ou d’un autre appareil][platforms], vous pouvez également envoyer la télémétrie à partir de ce dernier. 

Utilisez hello même tooset clé d’instrumentation de télémétrie de votre client et le serveur. les données de salutation apparaîtront dans hello même ressource Application Insights, et vous pourrez événements toocorrelate en mesure de client et le serveur.


## <a name="disabling-telemetry"></a>Désactivation de la télémétrie
**Comment puis-je désactiver la collecte télémétrique ?**

Dans le code :

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Ou** 

Mettre à jour ApplicationInsights.xml (dans le dossier de ressources hello dans votre projet). Ajoutez les éléments suivants de hello sous le nœud racine de hello :

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

À l’aide de la méthode de hello XML, vous avez application hello de toorestart lorsque vous modifiez la valeur de hello.

## <a name="changing-hello-target"></a>Modification de la cible de hello
**Comment puis-je changer la ressource Azure à laquelle mon projet envoie des données ?**

* [Obtenir la clé d’instrumentation hello de ressource hello.][java]
* Si vous avez ajouté Application Insights tooyour projet hello boîte à outils Azure pour Eclipse, cliquez avec le bouton droit sur votre projet web, sélectionnez **Azure**, **configurer Application Insights**et modifier la clé de hello.
* Sinon, mettre à jour de clé hello dans ApplicationInsights.xml dans le dossier de ressources hello dans votre projet.

## <a name="debug-data-from-hello-sdk"></a>Déboguer des données à partir de hello SDK

**Comment puis-je savoir quel hello effectue un kit de développement logiciel ?**

Ajout de plus d’informations sur ce qui se passe dans hello API, tooget `<SDKLogger/>` sous le nœud racine de hello hello ApplicationInsights.xml du fichier de configuration.

Vous pouvez également demander à fichier de tooa toooutput hello enregistreur d’événements :

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Vous trouverez les fichiers Hello sous `%temp%\javasdklogs` ou `java.io.tmpdir` en cas de serveur Tomcat.


## <a name="hello-azure-start-screen"></a>écran de démarrage Azure Hello
**Je regarde [hello Azure portal](https://portal.azure.com). Mappage de hello indique quelque chose sur mon application ?**

Non, il affiche la santé des serveurs Windows Azure hello monde hello.

*À partir du tableau de démarrage Azure hello (écran d’accueil), comment rechercher données relatives à mon application ?*

En supposant que vous [configurer votre application pour Application Insights][java], cliquez sur Parcourir, sélectionnez Application Insights et sélectionnez les ressources d’application hello vous avez créé pour votre application. tooget il plus rapidement à l’avenir, vous pouvez épingler votre application toohello démarrer votre tableau.

## <a name="intranet-servers"></a>Serveurs intranet
**Puis-je surveiller un serveur sur mon intranet ?**

Oui, la condition de votre serveur peut envoyer le portail d’Application Insights toohello télémétrie via hello internet public. 

Dans votre pare-feu, vous pouvez avoir tooopen les ports TCP 80 et 443 pour toodc.services.visualstudio.com de trafic sortant et f5.services.visualstudio.com.

## <a name="data-retention"></a>Conservation des données
**La durée pendant laquelle les données sont conservées dans le portail de hello ? Sont-elles sécurisées ?**

Consultez [Rétention des données et confidentialité][data].

## <a name="next-steps"></a>Étapes suivantes
**J’ai configuré Application Insights pour mon application serveur Java. Que puis-je faire d’autre ?**

* [Surveiller la disponibilité de vos pages web][availability]
* [Surveiller l’utilisation des pages web][usage]
* [Suivre l’utilisation de vos applications et diagnostiquer les problèmes des applications de vos appareils][platforms]
* [Écrire l’utilisation tootrack du code de votre application][track]
* [Capturer les journaux de diagnostic][javalogs]

## <a name="get-help"></a>Obtenir de l'aide
* [Dépassement de capacité de la pile](http://stackoverflow.com/questions/tagged/ms-application-insights)

<!--Link references-->

[availability]: app-insights-monitor-web-app-availability.md
[data]: app-insights-data-retention-privacy.md
[java]: app-insights-java-get-started.md
[javalogs]: app-insights-java-trace-logs.md
[platforms]: app-insights-platforms.md
[track]: app-insights-api-custom-events-metrics.md
[usage]: app-insights-javascript.md

