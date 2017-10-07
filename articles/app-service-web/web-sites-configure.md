---
title: aaaConfigure les applications web dans Azure App Service
description: "Comment tooconfigure une application web dans les Services d’application Azure"
services: app-service\web
documentationcenter: 
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 9af8a367-7d39-4399-9941-b80cbc5f39a0
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 8697ab6f21cfeb470e11f0d82c68692d43142fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-web-apps-in-azure-app-service"></a>Configurer des applications web dans Azure App Service
Cette rubrique explique comment une application web à l’aide de tooconfigure hello [Azure Portal].

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="application-settings"></a>Paramètres de l’application
1. Bonjour [Azure Portal], ouvrez Panneau hello pour l’application web de hello.
2. Cliquez sur **Tous les paramètres**.
3. Cliquez sur **Paramètres de l’application**.

![Paramètres de l’application][configure01]

Hello **paramètres de l’Application** panneau a regroupées sous plusieurs catégories de paramètres.

### <a name="general-settings"></a>Paramètres généraux :
**Versions d'infrastructure**. Définissez ces options si votre application utilise l'une de ces infrastructures : 

* **.NET framework**: version du .NET framework ensemble hello. 
* **PHP**: définir la version PHP hello, ou **OFF** toodisable PHP. 
* **Java**: une version Java hello Select ou **OFF** toodisable Java. Hello d’utilisation **Web conteneur** toochoose option entre les versions de Tomcat et Jetty.
* **Python**: version de Python hello Select, ou **OFF** toodisable Python.

Pour des raisons techniques, l’activation de Java pour votre application désactive les options .NET, PHP et Python hello.

<a name="platform"></a>
**Plateforme**. Indique si votre application web s’exécute dans un environnement 32 bits ou 64 bits. environnement de Hello 64 bits requiert le mode de base ou Standard. Les modes Gratuit et Partagé s'exécutent uniquement dans un environnement 32 bits.

**Web Sockets**. Définissez **ON** tooenable hello protocole WebSocket ; par exemple, si votre application web utilise [ASP.NET SignalR] ou [socket.io].

<a name="alwayson"></a>
**Toujours actif**. Par défaut, les applications web sont déchargées si elles sont inactives pendant un certain temps. Cela permet de préserver les ressources système de hello. En mode de base ou Standard, vous pouvez activer **Always On** tookeep hello application chargée de tout temps hello. Si votre application exécute des tâches Web continues ou s’exécute les tâches Web déclenchées à l’aide d’une expression CRON, vous devez activer **Always On**, ou les tâches web de hello peut ne pas fonctionner de manière fiable.

**Version de pipeline gérée**. Jeux de hello IIS [mode pipeline]. Laissez ce paramètre défini tooIntegrated (valeur par défaut de hello) sauf si vous avez une application héritée qui requiert une version antérieure de IIS.

**Basculement automatique**. Si vous activez l’échange automatique pour un emplacement de déploiement, du Service d’applications échangera automatiquement l’application hello web en production lorsque vous appuyez sur un emplacement de toothat de mise à jour. Pour plus d’informations, consultez [déployer toostaging les emplacements pour les applications web dans Azure App Service](web-sites-staged-publishing.md).

### <a name="debugging"></a>Débogage
**Débogage à distance**. Active le débogage distant. Lorsque activé, vous pouvez utiliser le débogueur distant de hello dans Visual Studio tooconnect directement tooyour web app. Le débogage à distance reste activé pendant 48 heures. 

### <a name="app-settings"></a>Paramètres de l'application
Cette section contient des paires nom/valeur qui seront chargées par votre application web au démarrage. 

* Dans le cas des applications .NET, ces paramètres sont inclus dans les `AppSettings` de votre configuration .NET au moment de l’exécution, en remplacement des paramètres existants. 
* Les applications PHP, Python, Java et Node peuvent accéder à ces paramètres sous forme de variables d'environnement au moment de l'exécution. Pour chaque paramètre d’application, les deux variables d’environnement sont créés ; un nom hello spécifié par l’entrée de paramètre d’application hello et l’autre avec un préfixe de APPSETTING_. Tous les deux contenir hello même valeur.

### <a name="connection-strings"></a>Chaînes de connexion
Chaînes de connexion des ressources liées. 

Pour les applications .NET, ces chaînes de connexion sont injectées dans votre configuration .NET `connectionStrings` paramètres lors de l’exécution, qui remplaceront les entrées existantes dont la clé de hello est hello nom de la base de données liée. 

Pour les applications PHP, Python, Java et de nœud, ces paramètres seront disponibles en tant que variables d’environnement lors de l’exécution, le préfixe avec le type de connexion hello. préfixes Hello de variable d’environnement sont les suivantes : 

* SQL Server : `SQLCONNSTR_`
* MySQL : `MYSQLCONNSTR_`
* Base de données SQL : `SQLAZURECONNSTR_`
* Personnalisé : `CUSTOMCONNSTR_`

Par exemple, si une chaîne de connexion MySql ont été nommée `connectionstring1`, il est accessible via la variable d’environnement hello `MYSQLCONNSTR_connectionString1`.

### <a name="default-documents"></a>Documents par défaut
document par défaut de Hello est hello web page qui s’affiche à l’URL racine de hello pour un site Web.  premier fichier correspondant Hello dans la liste de hello est utilisé. 

Les applications web peuvent utiliser des modules qui effectuent un routage en fonction de l’URL, au lieu de proposer du contenu statique. Dans ce cas, il n’existe pas de document par défaut.    

### <a name="handler-mappings"></a>Mappages de gestionnaires
Utiliser cette toohandle des processeurs zone tooadd script personnalisé requêtes pour les extensions de fichier spécifiques. 

* **Extension**. Hello fichier extension toobe géré, telles que *.php ou handler.fcgi. 
* **Chemin d'accès du processeur de script**. Hello chemin d’accès du processeur de script hello. Toofiles de demandes qui correspondent à extension de fichier hello sera traité par le processeur de script hello. Utiliser un chemin hello `D:\home\site\wwwroot` répertoire racine de l’application toorefer tooyour.
* **Arguments supplémentaires**. Arguments de ligne de commande facultatifs pour le processeur de script hello 

### <a name="virtual-applications-and-directories"></a>Applications et répertoires virtuels
tooconfigure des applications virtuelles et les répertoires, spécifiez chaque répertoire virtuel et sa racine du site Web relatif toohello chemin d’accès physique correspondant. Si vous le souhaitez, vous pouvez sélectionner hello **Application** case à cocher toomark un répertoire virtuel en tant qu’application.

## <a name="enabling-diagnostic-logs"></a>Activation des journaux de diagnostic
journaux de diagnostic tooenable :

1. Dans le panneau de hello pour votre application web, cliquez sur **tous les paramètres**.
2. Cliquez sur **Journaux de diagnostic**. 

Options liées à l'écriture des journaux de diagnostic à partir d'une application web qui prend en charge la journalisation : 

* **Journalisation des applications**. Écrit des journaux des applications système de fichiers toohello. La journalisation s’étend sur une période de 12 heures. 

**Niveau**. Lorsque la journalisation de l’application est activée, cette option spécifie la quantité de hello d’informations qui seront enregistrées (erreur, avertissement, Information ou Verbose).

**Journalisation du serveur Web**. Les journaux sont enregistrés au format de fichier journal étendu hello W3C. 

**Messages d’erreur détaillés**. Enregistre des messages d’erreur détaillés dans des fichiers .htm. fichiers de Hello sont enregistrés sous /LogFiles/DetailedErrors. 

**Suivi des demandes ayant échoué**. Échec de la demandes tooXML fichiers journaux. fichiers Hello sont enregistrés sous LogFiles/W3SVC*xxx*, où xxx est un identificateur unique. Ce dossier contient un fichier XSL et un ou plusieurs fichiers XML. Vérifiez que hello toodownload fichier XSL, car il fournit des fonctionnalités de mise en forme et de filtrer le contenu hello des fichiers XML de hello.

fichiers de journaux tooview hello, vous devez créer les informations d’identification de FTP, comme suit :

1. Dans le panneau de hello pour votre application web, cliquez sur **tous les paramètres**.
2. Cliquez sur **Informations d’identification du déploiement**.
3. Entrez un nom d'utilisateur et un mot de passe.
4. Cliquez sur **Save**.

![Définir les informations d’identification de déploiement][configure03]

nom d’utilisateur FTP Hello complet est « app\username » où *application* est le nom hello de votre application web. Hello nom d’utilisateur est répertorié dans le panneau de l’application hello web, sous **Essentials**.  

![Informations d’identification de déploiement FTP][configure02]

## <a name="other-configuration-tasks"></a>Autres tâches de configuration
### <a name="ssl"></a>SSL
En mode De base ou Standard, vous pouvez télécharger des certificats SSL pour un domaine personnalisé. Pour plus d’informations, consultez [Activer le protocole HTTPS pour une application web]. 

Cliquez sur vos certificats téléchargés, tooview **tous les paramètres** > **les domaines personnalisés et SSL**.

### <a name="domain-names"></a>Noms de domaine
Ajouter des noms de domaine personnalisés pour votre application web. Pour plus d’informations, consultez [Configurer un nom de domaine personnalisé pour une application web dans Azure App Service].

Cliquez sur les noms de votre domaine, tooview **tous les paramètres** > **les domaines personnalisés et SSL**.

### <a name="deployments"></a>Déploiements
* Configurer un déploiement continu Consultez [à l’aide de Git toodeploy Web Apps dans Azure App Service](web-sites-deploy.md).
* Emplacements de déploiement Consultez [déployer des environnements de tooStaging pour les applications Web dans Azure App Service].

Cliquez sur les emplacements de votre déploiement, tooview **tous les paramètres** > **les emplacements de déploiement**.

### <a name="monitoring"></a>Surveillance
En mode de base ou Standard, vous pouvez tester la disponibilité hello de points de terminaison HTTP ou HTTPS, à partir des emplacements de géo-distribué toothree. Un test de surveillance échoue si hello code de réponse HTTP est une erreur (4xx ou 5xx) ou de réponse de hello prend plus de 30 secondes. Un point de terminaison est considéré comme étant disponible si les tests d’analyse hello réussissent tous hello indiqué des emplacements. 

Pour plus d’informations, consultez [Surveillance de l’état d’un point de terminaison Web].

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications], où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="next-steps"></a>Étapes suivantes
* [Configuration d’un nom de domaine personnalisé dans Azure App Service]
* [Activer le protocole HTTPS pour une application dans Azure App Service]
* [Faire évoluer une application Web dans Azure App Service]
* [Surveiller les applications Web dans Azure App Service]

<!-- URL List -->

[ASP.NET SignalR]: http://www.asp.net/signalr
[Azure Portal]: https://portal.azure.com/
[Configuration d’un nom de domaine personnalisé dans Azure App Service]: ./app-service-web-tutorial-custom-domain.md
[déployer des environnements de tooStaging pour les applications Web dans Azure App Service]: ./web-sites-staged-publishing.md
[Activer le protocole HTTPS pour une application dans Azure App Service]: ./app-service-web-tutorial-custom-ssl.md
[Surveillance de l’état d’un point de terminaison Web]: http://go.microsoft.com/fwLink/?LinkID=279906
[Surveiller les applications Web dans Azure App Service]: ./web-sites-monitor.md
[mode pipeline]: http://www.iis.net/learn/get-started/introduction-to-iis/introduction-to-iis-architecture#Application
[Faire évoluer une application Web dans Azure App Service]: ./web-sites-scale.md
[socket.io]: ./web-sites-nodejs-chat-app-socketio.md
[essayez du Service d’applications]: https://azure.microsoft.com/try/app-service/

<!-- IMG List -->

[configure01]: ./media/web-sites-configure/configure01.png
[configure02]: ./media/web-sites-configure/configure02.png
[configure03]: ./media/web-sites-configure/configure03.png
