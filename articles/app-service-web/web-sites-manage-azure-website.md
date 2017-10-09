---
title: aaaManage une application web dans Azure App Service
description: "Tooresources de liens pour la gestion d’une application web dans Azure App Service."
services: app-service\web
documentationcenter: 
author: erikre
manager: erikre
editor: 
ms.assetid: d5e2887a-84f9-4747-a573-867635cb8b39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/24/2016
ms.author: rachelap
ms.openlocfilehash: daf69245e66068b0e97e3ae1c3fb5fce45605b91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-a-web-app-in-azure-app-service"></a>Gérer une application web dans Azure App Service
Cette rubrique contient des tooresources de liens pour la gestion d’une application web [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714). La gestion inclut toutes les tâches hello qui maintenir votre application web fonctionne correctement. 

Sur la durée de vie hello d’une application web, vous effectuerez des différentes tâches de gestion, que vous passez de l’opération toonormal de déploiement initial, la maintenance et les mises à jour.

Plusieurs tâches de gestion d’application web peuvent être effectuées dans hello portail Azure.

## <a name="before-you-deploy-your-web-app-tooproduction"></a>Avant de déployer votre tooproduction d’application web
### <a name="choose-a-tier"></a>Choisir un niveau
Azure App Service est disponibles en cinq niveaux : Gratuit, Partagé, De base, Standard et Premium. Pour plus d’informations sur les fonctions hello et pour chaque niveau de tarification, consultez [tarification](https://azure.microsoft.com/pricing/details/app-service/). 

* [Plans de Service d’applications](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) vous permet de regrouper plusieurs applications web sous hello même niveau.
* Vous avez toujours la possibilité de [changer de niveau](web-sites-scale.md) après avoir créé l’application web.

### <a name="configuration"></a>Configuration
Hello d’utilisation [Azure Portal](https://portal.azure.com/) tooset différentes options de configuration. Pour plus d’informations, consultez la page [Configurer des applications web dans Azure App Service](web-sites-configure.md). Voici une liste de vérification rapide :

* Sélectionnez **Versions exécutables** pour .NET, PHP, Java ou Python, si nécessaire.
* Activer **WebSockets** si votre application web utilise le protocole WebSocket de hello. (Ceci inclut les applications qui utilisent [ASP.NET SignalR](http://www.asp.net/signalr) ou [socket.io](web-sites-nodejs-chat-app-socketio.md).)
* Exécutez-vous des tâches Web continues ? Si tel est le cas, activez l'option **Toujours activé**.
* Ensemble hello **document par défaut**, tel que index.html.

Dans les paramètres de configuration de base de toothese de plus, vous souhaiterez suivant de hello tooconfigure :

* **SSL (Secure Socket Layer)** . toouse SSL avec un nom de domaine personnalisé, vous devez obtenir une connexion SSL de certificat et de configurer votre toouse d’application web il. Consultez la page [Activer le protocole HTTPS pour une application web dans Azure App Service](app-service-web-tutorial-custom-ssl.md).
* **Nom de domaine personnalisé.** Votre application web a automatiquement un sous-domaine sous azurewebsites.net. Vous pouvez lui associer un nom de domaine personnalisé, par exemple contoso.com. Consultez la page [Configurer un nom de domaine personnalisé dans Azure App Service](app-service-web-tutorial-custom-domain.md).

Configuration spécifique à la langue :

* **PHP**: [configurez PHP dans Azure App Service Web Apps](web-sites-php-configure.md).
* **Python**: [configurez Python dans Azure App Service Web Apps](web-sites-python-configure.md)

## <a name="while-your-web-app-is-running"></a>Pendant l’exécution de votre application web
Pendant l’exécution de votre application web, vous souhaitez toomake qu’il est disponible, et qu’il met à l’échelle toomeet le trafic des utilisateurs. Vous devez également les erreurs tootroubleshoot.

### <a name="monitoring"></a>Surveillance
* Via hello portail Azure, vous pouvez [ajouter des métriques de performances](web-sites-monitor.md) telles que l’utilisation du processeur et le nombre de demandes client.
* [Mettre à l’échelle votre application web](web-sites-scale.md) dans tootraffic de réponse. Selon votre niveau, vous pouvez adapter le nombre de hello d’ordinateurs virtuels et/ou de la taille de hello des instances de machine virtuelle hello. Dans hello Standard et les niveaux Premium, vous pouvez également configurer échelle, afin de votre application web s’adapte automatiquement, selon une planification fixe, soit dans tooload de réponse.  

### <a name="backups"></a>Sauvegardes
* Configurez les [sauvegardes automatiques](web-sites-backup.md) de votre application web. Pour en savoir plus sur les sauvegardes, regardez [cette vidéo](https://azure.microsoft.com/documentation/videos/azure-websites-automatic-and-easy-backup/).
* En savoir plus sur les options de hello pour [récupération de base de données](../sql-database/sql-database-business-continuity.md) dans la base de données SQL Azure.

### <a name="troubleshooting"></a>Résolution des problèmes
* Si une erreur survient, vous pouvez [dépanner dans Visual Studio](web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug), à l’aide des journaux de diagnostic et de débogage dans le cloud de hello. 
* En dehors de Visual Studio, il existe différentes façons toocollect des journaux de diagnostic. Consultez la page [Activer la journalisation des diagnostics pour les applications web dans Azure App Service](web-sites-enable-diagnostic-log.md).
* Pour les applications Node.js, consultez [comment toodebug un Node.js web application dans Azure App Service](web-sites-nodejs-debug.md).

### <a name="restoring-data"></a>Restauration de données
* [Restaurez](web-sites-restore.md) une application Web qui a été précédemment sauvegardée.

## <a name="when-you-update-your-web-app"></a>Lors de la mise à jour de votre application Web
Si vous n'avez pas activé les sauvegardes automatiques, vous pouvez créer une [sauvegarde manuelle](web-sites-backup.md).

Envisagez d'utiliser le [déploiement intermédiaire](web-sites-staged-publishing.md). Cette option vous permet de publier des mises à jour les tooa mise en lots de déploiement qui s’exécute côte à côte avec votre déploiement de production. 


<!-- Anchors. -->

[Before you deploy your site tooproduction]: #before-you-deploy-your-site-to-production
[While your website is running]: #while-your-website-is-running
[When you update your website]: #when-you-update-your-website


