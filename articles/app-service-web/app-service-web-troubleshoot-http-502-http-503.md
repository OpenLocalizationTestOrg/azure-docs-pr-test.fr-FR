---
title: "passerelle incorrecte d’aaaFix 502, 503 service non disponibles erreurs | Documents Microsoft"
description: "Corriger les erreurs « 502 Passerelle incorrecte » et « 503 Service indisponible » dans votre application web hébergée dans Azure App Service."
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: top-support-issue
keywords: 502 Passerelle incorrecte, 503 Service indisponible, erreur 503, erreur 502
ms.assetid: 51cd331a-a3fa-438f-90ef-385e755e50d5
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2016
ms.author: cephalin
ms.openlocfilehash: d9d8dcddaac930967a2e8d2bfd8cad09e6824c17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-http-errors-of-502-bad-gateway-and-503-service-unavailable-in-your-azure-web-apps"></a>Résoudre les erreurs HTTP de type « 502 Passerelle incorrecte » et « 503 Service indisponible » dans vos applications web Azure
« 502 Passerelle incorrecte » et « 503 Service indisponible » sont des erreurs courantes dans votre application web hébergée dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). Cet article vous permet de résoudre ces erreurs.

Si vous avez besoin d’aide à tout moment dans cet article, vous pouvez contacter hello experts Azure sur [hello MSDN Azure et hello forums de débordement de pile](https://azure.microsoft.com/support/forums/). Vous pouvez également signaler un incident au support Azure. Accédez toohello [site de Support technique Azure](https://azure.microsoft.com/support/options/) , puis cliquez sur **Get Support**.

## <a name="symptom"></a>Symptôme
Lorsque vous accédez à l’application web toohello, elle retourne un HTTP Erreur de « 502 Passerelle incorrecte » ou un HTTP erreur « 503 Service non disponible ».

## <a name="cause"></a>Cause :
Ce problème est souvent dû à des problèmes au niveau de l’application, tels que :

* demandes exigeant beaucoup de temps ;
* un taux d’utilisation élevé de la mémoire/UC par l’application ;
* panne en raison de l’exception de tooan d’application.

## <a name="troubleshooting-steps-toosolve-502-bad-gateway-and-503-service-unavailable-errors"></a>Dépannage des étapes toosolve « 502 Passerelle incorrecte » et les erreurs « 503 service non disponible »
Le dépannage peut être divisé en trois tâches distinctes, dans un ordre séquentiel :

1. [Observer et contrôler le comportement de l’application](#observe)
2. [Collecter les données](#collect)
3. [Limiter le problème de hello](#mitigate)

[App Service Web Apps](/services/app-service/web/) vous offre différentes options à chaque étape.

<a name="observe" />

### <a name="1-observe-and-monitor-application-behavior"></a>1. Observer et contrôler le comportement de l'application
#### <a name="track-service-health"></a>Suivi de l’état du service
Microsoft Azure publie chaque interruption du service et chaque dégradation des performances. Vous pouvez suivre la santé hello du service de hello sur hello [Azure Portal](https://portal.azure.com/). Pour plus d’informations, consultez la rubrique [Suivi de l’état du service](../monitoring-and-diagnostics/insights-service-health.md).

#### <a name="monitor-your-web-app"></a>Contrôle de votre application web
Cette option permet de vous toofind out si votre application rencontre des problèmes. Dans le panneau de votre application web, cliquez sur hello **demandes et les erreurs** vignette. Hello **métrique** panneau affiche toutes les métriques hello que vous pouvez ajouter.

Parmi les métriques hello que vous pouvez vouloir toomonitor pour votre application web

* Plage de travail moyenne de la mémoire
* Temps de réponse moyen
* Temps processeur
* Plage de travail de la mémoire
* Demandes

![surveiller l’application web pour résoudre les erreurs HTTP de type « 502 Passerelle incorrecte » et « 503 Service indisponible »](./media/app-service-web-troubleshoot-HTTP-502-503/1-monitor-metrics.png)

Pour plus d’informations, consultez :

* [Surveiller les applications web dans Microsoft Azure App Service](web-sites-monitor.md)
* [Réception de notifications d'alerte](../monitoring-and-diagnostics/insights-receive-alert-notifications.md)

<a name="collect" />

### <a name="2-collect-data"></a>2. Collecter les données
#### <a name="use-hello-azure-app-service-support-portal"></a>Utilisez hello portail de Support Azure App Service
Web Apps fournit hello capacité tootroubleshoot problèmes connexes tooyour web application en examinant HTTP journaux, les journaux des événements, les vidages de processus et bien plus encore. Vous pouvez accéder à toutes ces informations à l’aide de notre portail de support à l’adresse **http://&lt;your app name>.scm.azurewebsites.net/Support**

portail de Support technique Azure App Service Hello fournit trois onglets distincts toosupport hello trois étapes d’un scénario de dépannage courantes :

1. Observer le comportement actuel
2. Analyser à la collecte des informations de diagnostic et en cours d’exécution hello analyseurs intégrés
3. Résoudre

Si le problème de hello se produit dès maintenant, cliquez sur **analyser** > **Diagnostics** > **diagnostiquer maintenant** toocreate une session de diagnostic pour vous, qui collectera HTTP connecte, Observateur d’événements, mémoire dumps, les journaux d’erreurs PHP et PHP traitent le rapport.

Une fois la collecte des données de hello, il sera également exécuter une analyse sur les données de salutation et vous fournir un rapport HTML.

Dans le cas des données toodownload hello, par défaut, il est stocké dans le dossier de D:\home\data\DaaS hello.

Pour plus d’informations sur le portail de Support technique Azure App Service hello, consultez [tooSupport de nouvelles mises à jour Extension de Site des sites Web Azure](https://azure.microsoft.com/blog/new-updates-to-support-site-extension-for-azure-websites).

#### <a name="use-hello-kudu-debug-console"></a>Utilisez hello Kudu la Console de débogage
Web Apps est fourni avec une console de débogage que vous pouvez utiliser pour le débogage, l’exploration, le téléchargement de fichiers, ainsi que les points de terminaison JSON pour obtenir des informations relatives à votre environnement. Il s’agit de hello *Kudu Console* ou hello *tableau de bord SCM* pour votre application web.

Vous pouvez accéder à ce tableau de bord en accédant le lien toohello **https://&lt;votre nom de l’application >.scm.azurewebsites.net/**.

Certains des éléments de hello Kudu offre sont :

* paramètres d’environnement pour votre application ;
* flux de journal ;
* vidage de diagnostic ;
* console de débogage dans laquelle vous pouvez exécuter les applets de commande Powershell et les commandes DOS de base.

Une autre fonctionnalité utile de Kudu est que, dans le cas où votre application lève des exceptions de première chance, vous pouvez utiliser Kudu et images hello SysInternals outil Procdump toocreate mémoire. Ces images mémoire sont des instantanés des processus de hello et peuvent vous aider à résoudre les problèmes plus complexes avec votre application web.

Pour plus d'informations sur les fonctionnalités disponibles dans Kudu, consultez [Outils en ligne de Sites Web Azure que vous devez connaître](https://azure.microsoft.com/blog/windows-azure-websites-online-tools-you-should-know-about/).

<a name="mitigate" />

### <a name="3-mitigate-hello-issue"></a>3. Limiter le problème de hello
#### <a name="scale-hello-web-app"></a>Échelle hello web app
Dans Azure App Service, pour améliorer les performances et le débit, vous pouvez ajuster échelle hello à partir duquel vous exécutez votre application. Mise à l’échelle d’une application web implique deux actions connexes : la modification de votre tooa de plan App Service supérieur tarification et configurer certains paramètres après avoir basculé toohello niveau de tarification supérieur.

Pour plus d'informations sur la mise à l'échelle, consultez [Mise à l'échelle d'une application web dans Microsoft Azure App Service](web-sites-scale.md).

En outre, vous pouvez choisir toorun votre application sur plusieurs instances. Non seulement cela vous offre plus de capacité de traitement, mais également un certain niveau de tolérance aux pannes. Si hello processus tombe en panne sur une instance, hello autre instance toujours continue à servir les demandes.

Vous pouvez définir hello mise à l’échelle toobe manuel ou automatique.

#### <a name="use-autoheal"></a>Utilisation de la correction automatique (AutoHeal)
AutoHeal recycle le processus de travail hello pour votre application en fonction des paramètres que vous choisissez (par exemple, les modifications de configuration, les demandes, les limites de mémoire ou une durée de hello nécessaire tooexecute une demande). La plupart du temps de hello, recycler le processus de hello est hello toorecover de façon plus rapide d’un problème. Bien que vous pouvez toujours redémarrer hello web de l’application directement dans hello portail Azure, AutoHeal fera automatiquement pour vous. Vous devez toodo est ajoutent des déclencheurs dans le fichier web.config racine de hello pour votre application web. Notez que ces paramètres fonctionnerait Bonjour même façon, même si votre application n’est pas un .net.

Pour plus d'informations, consultez [Correction automatique de Sites Web Azure](https://azure.microsoft.com/blog/auto-healing-windows-azure-web-sites/).

#### <a name="restart-hello-web-app"></a>Redémarrage de l’application web de hello
Il s’agit souvent hello toorecover de façon la plus simple des problèmes à usage unique. Sur hello [Azure Portal](https://portal.azure.com/), dans Panneau de votre application web, vous avez hello options toostop ou redémarrer votre application.

 ![Redémarrez l’application toosolve HTTP erreurs 502 Passerelle incorrecte et 503 service non disponible](./media/app-service-web-troubleshoot-HTTP-502-503/2-restart.png)

Vous pouvez également gérer votre application web à l’aide d’Azure PowerShell. Pour plus d'informations, consultez [Utilisation d'Azure PowerShell avec le Gestionnaire de ressources Azure](../powershell-azure-resource-manager.md).

