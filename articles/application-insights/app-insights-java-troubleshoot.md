---
title: "Résolution des problèmes d'Application Insights dans un projet web Java"
description: "Guide de dépannage : surveillance des applications Java en direct avec Application Insights."
services: application-insights
documentationcenter: java
author: mrbullwinkle
manager: carmonm
ms.assetid: ef602767-18f2-44d2-b7ef-42b404edd0e9
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: mbullwin
ms.openlocfilehash: 6b1cfa2b52e8e9e2b6a8ab87be6d4269cbe3f1cf
ms.sourcegitcommit: 295ec94e3332d3e0a8704c1b848913672f7467c8
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 11/06/2017
---
# <a name="troubleshooting-and-q-and-a-for-application-insights-for-java"></a>Guide de dépannage et questions-réponses concernant Application Insights pour Java
Vous avez des questions concernant [Azure Application Insights dans Java][java] ou vous rencontrez des problèmes ? Voici quelques conseils.

## <a name="build-errors"></a>Erreurs de build
**Dans Eclipse, quand j’ajoute le kit de développement logiciel (SDK) Application Insights via Maven ou Gradle, j’obtiens des erreurs de validation de build ou de somme de contrôle.**

* Si l’élément <version>de dépendance utilise un modèle avec des caractères génériques (par exemple, (Maven) `<version>[1.0,)</version>` or (Gradle) `version:'1.0.+'`), essayez de spécifier une version spécifique, comme par exemple  `1.0.2`. Consultez les [notes de publication](https://github.com/Microsoft/ApplicationInsights-Java#release-notes) relatives à la version la plus récente.

## <a name="no-data"></a>Absence de données
**J’ai ajouté Application Insights sans problème et exécuté mon application, mais je ne vois aucune donnée dans le portail.**

* Attendez une minute, puis cliquez sur Actualiser. Les graphiques s’actualisent à intervalles réguliers, mais vous pouvez également les actualiser manuellement. L’intervalle d’actualisation dépend de l’intervalle de temps sur lequel porte le graphique.
* Vérifiez que vous disposez d'une clé d'instrumentation définie dans le fichier ApplicationInsights.xml (situé dans le dossier de ressources de votre projet)
* Vérifiez qu’aucun nœud `<DisableTelemetry>true</DisableTelemetry>` ne se trouve dans le fichier .xml.
* Vous devrez ouvrir les ports TCP 80 et 443 de votre pare-feu pour le trafic sortant vers dc.services.visualstudio.com. Consultez la [liste complète des exceptions de pare-feu](app-insights-ip-addresses.md)
* Dans le panneau de démarrage Microsoft Azure, examinez la carte d'état du service. Si des alertes sont indiquées, attendez qu'elles soient corrigées (OK), puis fermez et rouvrez le volet de votre application Application Insights.
* Activez la journalisation dans la fenêtre de console IDE en ajoutant un élément `<SDKLogger />` sous le nœud racine dans le fichier ApplicationInsights.xml (situé dans le dossier de ressources de votre projet), puis vérifiez les entrées précédées du mot [Error].
* Assurez-vous que le fichier ApplicationInsights.xml approprié a été correctement chargé par le Kit de développement logiciel (SDK) Java, en vérifiant que le message de sortie de la console « Le fichier de configuration a été trouvé » s’affiche.
* Si le fichier de configuration est introuvable, vérifiez les messages de sortie pour voir où cette recherche a été effectuée et vous assurer que le fichier ApplicationInsights.xml se trouve dans l’un des emplacements de recherche. En règle générale, vous pouvez placer le fichier de configuration près du JAR du Kit de développement logiciel (SDK) Application Insights. Par exemple, il s’agit du dossier WEB-INF/lib dans Tomcat.

#### <a name="i-used-to-see-data-but-it-has-stopped"></a>Je pouvais voir les données, mais plus maintenant
* Vérifiez le [blog d'état](http://blogs.msdn.com/b/applicationinsights-status/).
* Vous souhaitez savoir si vous avez atteint votre quota mensuel de points de données ? Ouvrez Paramètres/Quota et tarification pour le savoir. Le cas échéant, vous pouvez mettre à niveau votre forfait ou payer pour disposer d’une capacité supplémentaire. Consultez le [mécanisme de tarification](https://azure.microsoft.com/pricing/details/application-insights/).

#### <a name="i-dont-see-all-the-data-im-expecting"></a>Je ne vois pas toutes les données que j’attends
* Ouvrez le panneau Quotas et tarification et vérifiez si l’ [échantillonnage](app-insights-sampling.md) est activé. (Une transmission de 100 % signifie que l’échantillonnage n’est pas activé). Le service Application Insights peut être défini pour n’accepter qu’une fraction des données de télémétrie provenant de votre application. Cela vous permet de respecter votre quota mensuel de télémétrie. 

## <a name="no-usage-data"></a>Absence de données d'utilisation
**Je vois des données concernant les requêtes et les temps de réponse, mais rien concernant les affichages de pages, le navigateur ou les données utilisateur.**

Assurez-vous d'avoir configuré correctement votre application de façon à envoyer la télémétrie depuis le serveur. L’étape suivante consiste à [configurer vos pages web pour l’envoi de la télémétrie depuis le navigateur web][usage].

Si votre client est une application d’un [téléphone ou d’un autre appareil][platforms], vous pouvez également envoyer la télémétrie à partir de ce dernier. 

Utilisez la même clé d'instrumentation pour configurer la télémétrie de votre client et de votre serveur. Les données apparaîtront dans la même ressource Application Insights, et vous pourrez mettre en corrélation les événements du serveur et du client.


## <a name="disabling-telemetry"></a>Désactivation de la télémétrie
**Comment puis-je désactiver la collecte télémétrique ?**

Dans le code :

```Java

    TelemetryConfiguration config = TelemetryConfiguration.getActive();
    config.setTrackingIsDisabled(true);
```

**Ou** 

Mettez à jour ApplicationInsights.xml (situé dans le dossier de ressources de votre projet). Ajoutez le code suivant sous le nœud racine :

```XML

    <DisableTelemetry>true</DisableTelemetry>
```

À l'aide de la méthode XML, vous devrez redémarrer l'application si vous modifiez la valeur.

## <a name="changing-the-target"></a>Modification de la cible
**Comment puis-je changer la ressource Azure à laquelle mon projet envoie des données ?**

* [Obtenez la clé d’instrumentation de la nouvelle ressource.][java]
* Si vous avez ajouté Application Insights à votre projet à l’aide du kit de ressources Azure pour Eclipse, cliquez avec le bouton droit sur votre projet web, sélectionnez **Azure**, **Configurer Application Insights**, puis modifiez la clé.
* Sinon, mettez à jour la clé du fichier ApplicationInsights.xml (situé dans le dossier de ressources de votre projet).

## <a name="debug-data-from-the-sdk"></a>Données de débogage du Kit de développement logiciel (SDK)

**Comment puis-je savoir ce que fait le Kit de développement logiciel (SDK) ?**

Pour obtenir plus d’informations sur ce qui se passe dans l’API, ajoutez `<SDKLogger/>` sous le nœud racine du fichier de configuration ApplicationInsights.xml.

Vous pouvez également demander à l’enregistreur d’événements une sortie vers un fichier :

```XML

    <SDKLogger type="FILE">
      <enabled>True</enabled>
      <UniquePrefix>JavaSDKLog</UniquePrefix>
    </SDKLogger>
```

Vous trouverez les fichiers sous `%temp%\javasdklogs` ou `java.io.tmpdir` si vous utilisez un serveur Tomcat.


## <a name="the-azure-start-screen"></a>L'écran d'accueil Azure
**J’ai ouvert [le portail Azure](https://portal.azure.com). Est-ce que la carte fournit des informations concernant mon application ?**

Non, elle montre l'intégrité des serveurs Azure dans le monde entier.

*Depuis le panneau de démarrage Azure (l’écran d’accueil), comment trouver les données relatives à mon application ?*

En supposant que vous ayez [configuré votre application pour Application Insights][java], cliquez sur Parcourir, sélectionnez Application Insights, puis sélectionnez la ressource d’application que vous avez créée pour votre application. Pour aller plus vite la prochaine fois, vous pouvez épingler votre application au panneau de démarrage.

## <a name="intranet-servers"></a>Serveurs intranet
**Puis-je surveiller un serveur sur mon intranet ?**

Oui, à condition que votre serveur puisse envoyer la télémétrie vers le portail Application Insights via l'Internet public. 

Vous devrez ouvrir les ports TCP 80 et 443 de votre pare-feu pour le trafic sortant vers dc.services.visualstudio.com et f5.services.visualstudio.com.

## <a name="data-retention"></a>Conservation des données
**Combien de temps les données sont-elles conservées dans le portail ? Sont-elles sécurisées ?**

Consultez [Rétention des données et confidentialité][data].

## <a name="debug-logging"></a>Enregistrement du débogage
Application Insights utilise `org.apache.http`. Cet élément a été déplacé au sein des principaux fichiers JAR d’Application Insights sous l’espace de noms `com.microsoft.applicationinsights.core.dependencies.http`. Cela permet à Application Insights de gérer les scénarios dans lesquels différentes versions du même élément `org.apache.http` existent dans une base de code. 

>[!NOTE]
>Si vous activez l’enregistrement au niveau du DÉBOGAGE pour tous les espaces de noms dans l’application, il est respecté par tous les modules en cours d’exécution, y compris `org.apache.http` renommé `com.microsoft.applicationinsights.core.dependencies.http`. Application Insights ne peut pas appliquer de filtrage pour ces appels, car l’appel de journal est effectué par la bibliothèque Apache. L’enregistrement au niveau du débogage produit une quantité considérable de données de journal et n’est pas recommandé pour les instances de production dynamiques.


## <a name="next-steps"></a>Étapes suivantes
**J’ai configuré Application Insights pour mon application serveur Java. Que puis-je faire d’autre ?**

* [Surveiller la disponibilité de vos pages web][availability]
* [Surveiller l’utilisation des pages web][usage]
* [Suivre l’utilisation de vos applications et diagnostiquer les problèmes des applications de vos appareils][platforms]
* [Écrire du code pour suivre l’utilisation de votre application][track]
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

