---
title: "aaaConnect un tooRedis d’application web du Service d’applications via le protocole Memcache - Azure de hello | Documents Microsoft"
description: "Se connecter à une application web dans Azure App service tooRedis Cache à l’aide du protocole de Memcache hello"
services: app-service\web
documentationcenter: php
author: SyntaxC4
manager: erikre
editor: riande
ms.assetid: 0fcdf9fa-2995-4839-ba4d-cfa389c4ba06
ms.service: app-service-web
ms.devlang: php
ms.topic: get-started-article
ms.tgt_pltfrm: windows
ms.workload: na
ms.date: 02/29/2016
ms.author: cfowler
ms.openlocfilehash: 48036d60fbbced59eb1e37584f507fffffff753d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# Se connecter à une application web dans Azure App Service tooRedis Cache via hello protocole Memcache
Dans cet article, vous allez apprendre comment tooconnect un WordPress web app dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) trop[Cache Redis Azure] [ 12] à l’aide de hello [Memcache] [ 13] protocole. Si vous avez une application web existante qui utilise un serveur memcache pour la mise en cache en mémoire, vous pouvez le migrer tooAzure du Service d’applications et utilisez hello tiers de la première mise en cache la solution dans Microsoft Azure avec peu ou aucune modification tooyour code de l’application. En outre, vous pouvez utiliser votre Memcache expertise toocreate distribuées et évolutives, les applications existantes dans Azure App Service avec le Cache Redis Azure pour la mise en cache en mémoire, lors de l’utilisation des infrastructures d’applications répandues telles que .NET, PHP, Node.js, Java et Python.  

Service d’applications Web Apps permet ce scénario d’application avec le shim Memcache d’applications Web de hello, qui est un serveur local en memcache qui agit comme un proxy Memcache pour la mise en cache des appels tooAzure Cache Redis. Cela permet de n’importe quelle application qui communique à l’aide des données de toocache du protocole Memcache hello avec le Cache Redis. Ce shim Memcache fonctionnant au niveau du protocole hello, il peut être utilisé par une application ou d’une infrastructure d’application tant qu’il communique à l’aide du protocole de Memcache hello.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## Composants requis
shim Memcache d’applications Web de Hello utilisable avec n’importe quelle application autant qu’il communique à l’aide du protocole de Memcache hello. Pour cet exemple particulier, application de référence hello est un site WordPress évolutive qui peut être configuré à partir de hello Azure Marketplace.

Suivez les étapes de hello décrites dans les articles suivants :

* [Configurer une instance du Service de Cache Redis Azure de hello][0]
* [Déployer un site WordPress évolutif dans Azure][1]

Après avoir site WordPress évolutive de hello déployé et une instance de Cache Redis configuré, vous serez prêt tooproceed avec l’activation du shim Memcache hello dans Azure App Service Web Apps.

## Activer le shim Memcache d’applications Web de hello
Dans l’ordre tooconfigure Memcache du shim, vous devez créer trois paramètres de l’application. Cela est possible à l’aide de diverses méthodes notamment hello [Azure Portal](http://go.microsoft.com/fwlink/?LinkId=529715), hello [portail classique][3], hello [applets de commande PowerShell Azure] [ 5] ou hello [Interface de ligne de commande Azure][5]. Pour des raisons de hello de cette publication, je vais toouse hello [Azure Portal] [ 4] tooset paramètres de l’application hello. Hello valeurs suivantes peuvent être récupérés de **paramètres** Panneau de votre instance de Cache Redis.

![Panneau Paramètres de Cache Redis Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/1-azure-redis-cache-settings.png)

### Ajouter le paramètre d’application REDIS_HOST
premier paramètre d’application vous avez besoin de Hello toocreate est hello **REDIS\_hôte** paramètre d’application. Ce paramètre définit les informations de cache hello hello shim transfère hello destination toowhich. Hello valeur requise pour le paramètre d’application hello REDIS_HOST peut être récupérée à partir de hello **propriétés** Panneau de votre instance de Cache Redis.

![Nom d’hôte du Cache Redis Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/2-azure-redis-cache-hostname.png)

Clé d’ensemble hello d’aussi un paramètre application hello**REDIS\_hôte** et la valeur hello de toohello de paramètre d’application hello **nom d’hôte** de l’instance de Cache Redis hello.

![Paramètre d’application Web App REDIS_HOST](./media/web-sites-connect-to-redis-using-memcache-protocol/3-azure-website-appsettings-redis-host.png)

### Ajouter un paramètre d’application REDIS_KEY
Hello du deuxième paramètre d’application vous devez toocreate est hello **REDIS\_clé** paramètre d’application. Ce paramètre fournit l’instance de Cache Redis hello authentication toosecurely requis jeton accès hello. Vous pouvez récupérer la valeur hello requis pour le paramètre d’application hello REDIS_KEY de hello **clés d’accès** Panneau de l’instance de Cache Redis hello.

![Clé primaire du Cache Redis Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/4-azure-redis-cache-primarykey.png)

Clé d’ensemble hello d’aussi un paramètre application hello**REDIS\_clé** et la valeur hello de toohello de paramètre d’application hello **clé primaire** de l’instance de Cache Redis hello.

![Paramètre d’application de site Web Azure REDIS_KEY](./media/web-sites-connect-to-redis-using-memcache-protocol/5-azure-website-appsettings-redis-primarykey.png)

### Ajouter un paramètre d’application MEMCACHESHIM_REDIS_ENABLE
paramètre d’application dernière Hello est utilisé tooenable hello Memcache Shim dans les applications Web, qui utilise hello REDIS_HOST et REDIS_KEY tooconnect toohello Cache Redis Azure et appels de cache hello vers l’avant. Clé d’ensemble hello d’aussi un paramètre application hello**MEMCACHESHIM\_REDIS\_activer** et hello valeur trop**true**.

![Paramètre d’application Web App MEMCACHESHIM_REDIS_ENABLE](./media/web-sites-connect-to-redis-using-memcache-protocol/6-azure-website-appsettings-enable-shim.png)

Une fois que vous avez terminé les paramètres de l’application Ajout hello trois (3), cliquez sur **enregistrer**.

## Activer l’extension Memcache pour PHP
Dans l’ordre pour hello de toospeak application hello protocole Memcache, il est nécessaire tooinstall hello Memcache extension tooPHP--l’infrastructure de langage hello pour votre site WordPress.

### Télécharger hello php_memcache Extension
Parcourir trop[PECL][6]. Sous hello mise en cache de la catégorie, cliquez sur [memcache][7]. Sous les téléchargements hello colonne, cliquez sur lien DLL hello.

![Site web PECL PHP](./media/web-sites-connect-to-redis-using-memcache-protocol/7-php-pecl-website.png)

Télécharger la version hello de PHP activé dans les applications Web sur le lien Non Thread-Safe (NTS) x86 hello. (PHP 5.4 par défaut)

![Package Memcache de site web PECL PHP](./media/web-sites-connect-to-redis-using-memcache-protocol/8-php-pecl-memcache-package.png)

### Activer l’extension de php_memcache hello
Après avoir téléchargé le fichier de hello, décompressez et télécharger hello **php\_memcache.dll** dans hello **d:\\domestique\\site\\wwwroot\\bin\\ext\\**  active. Une fois téléchargé hello php_memcache.dll dans l’application hello web, vous devez tooenable hello extension toohello Runtime PHP. tooenable hello extension Memcache Bonjour portail Azure, ouvrez hello **paramètres de l’Application** panneau pour l’application web de hello, puis ajoutez un nouveau paramètre d’application avec clé hello de **PHP\_EXTENSIONS** et hello valeur **bin\\ext\\php_memcache.dll**.

> [!NOTE]
> Si l’application web hello doit tooload plusieurs extensions PHP, valeur hello PHP_EXTENSIONS doit être une liste délimitée par des virgules des fichiers tooDLL de chemins d’accès relatifs.
> 
> 

![Paramètre d’application Web App PHP_EXTENSIONS](./media/web-sites-connect-to-redis-using-memcache-protocol/9-azure-website-appsettings-php-extensions.png)

Une fois que vous avez terminé, cliquez sur **Enregistrer**.

## Installer le plug-in Memcache WordPress
> [!NOTE]
> Vous pouvez également télécharger hello [le plug-in Cache memcache objet](https://wordpress.org/plugins/memcached/) à partir de WordPress.org.
> 
> 

Dans la page de plug-ins hello WordPress, cliquez sur **nouveau**.

![Page du plug-in WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/10-wordpress-plugin.png)

Dans la zone de recherche de hello, tapez **memcached** et appuyez sur **entrée**.

![Plug-in Ajouter nouveau de WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/11-wordpress-add-new-plugin.png)

Rechercher **Cache d’objets en memcache** dans la liste hello, puis cliquez sur **installer maintenant**.

![Plug-in Installer Memcache de WordPress](./media/web-sites-connect-to-redis-using-memcache-protocol/12-wordpress-install-memcache-plugin.png)

### Activer hello plug-in WordPress de Memcache
> [!NOTE]
> Suivez les instructions de hello dans ce billet de blog [comment tooenable une Extension de Site dans les applications Web] [ 8] tooinstall Visual Studio Team Services.
> 
> 

Bonjour `wp-config.php` , ajoutez hello suivant le code de commentaire de modification stop hello près de fin hello du fichier de hello ci-dessus.

```php
$memcached_servers = array(
    'default' => array('localhost:' . getenv("MEMCACHESHIM_PORT"))
);
```

Une fois que ce code a été collé, monaco enregistrera automatiquement les documents de hello.

étape suivante de Hello est un plug-in de cache d’objets tooenable hello. Il suffit de glisser -déplacer **cache.php de l’objet** de **wp-contenu/plug-ins/memcache** dossier toohello **wp-content** dossier tooenable hello Memcache objet Fonctionnalités de cache.

![Recherchez le plug-in de hello memcache cache.php de l’objet](./media/web-sites-connect-to-redis-using-memcache-protocol/13-locate-memcache-object-cache-plugin.png)

Maintenant que hello **objet-cache.php** fichier est Bonjour **wp-content** dossier, hello memcache objet est maintenant activé.

![Activer le plug-in de hello memcache cache.php de l’objet](./media/web-sites-connect-to-redis-using-memcache-protocol/14-enable-memcache-object-cache-plugin.png)

## Vérifiez que hello Memcache fonctionne plug-in du Cache d’objets
Tous les hello étapes tooenable hello Web applications Memcache shim sont désormais terminées. reste Hello est tooverify que les données de salutation le remplissage de votre instance de Cache Redis.

### Activer la prise en charge du port non-SSL hello dans le Cache Redis Azure
> [!NOTE]
> Au moment de l’écriture de cet article de hello, hello Redis de CLI ne prend pas en charge la connectivité SSL, donc hello étapes suivantes sont nécessaires.
> 
> 

Bonjour Azure Portal, parcourir l’instance de Cache Redis toohello que vous avez créé pour cette application web. Une fois les lames du cache hello sont ouvert, cliquez sur hello **paramètres** icône.

![Bouton Paramètres de Cache Redis Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/15-azure-redis-cache-settings-button.png)

Sélectionnez **Ports d’accès** à partir de la liste de hello.

![Port d’accès de Cache Redis Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/16-azure-redis-cache-access-port.png)

Cliquez sur **Non** sous l’option **Permettre l’accès uniquement via SSL**.

![Port d’accès SSL uniquement de Cache Redis Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/17-azure-redis-cache-access-port-ssl-only.png)

Vous verrez que le port NON-SSL hello est maintenant défini. Cliquez sur **Enregistrer**.

![Portail d’accès Redis non SSL de Cache Redis Azure](./media/web-sites-connect-to-redis-using-memcache-protocol/18-azure-redis-cache-access-port-non-ssl.png)

### Se connecter tooAzure Cache Redis redis-CLI
> [!NOTE]
> Cette étape suppose que Redis est installé localement sur votre ordinateur de développement. [Installez Redis localement en suivant ces instructions][9].
> 
> 

Ouvrez la console de ligne de commande de hello choix et le type de commande suivante :

```shell
redis-cli –h <hostname-for-redis-cache> –a <primary-key-for-redis-cache> –p 6379
```

Remplacez hello  **&lt;nom d’hôte de cache redis&gt;**  avec le nom d’hôte de hello xxxxx.redis.cache.windows.net réel et hello  **&lt;primaire-clé-de--cache redis&gt;**  avec la clé d’accès hello pour le cache de hello, puis appuyez sur **entrée**. Une fois hello CLI a connecté instance de Cache Redis toohello, émettez les commandes redis. Dans la capture d’écran de hello ci-dessous, j’ai choisi toolist clés de hello.

![Se connecter tooAzure Cache Redis CLI de Redis dans Terminal Server](./media/web-sites-connect-to-redis-using-memcache-protocol/19-redis-cli-terminal.png)

clés de hello toolist Hello appel doivent retourner une valeur. Si ce n’est pas, essayez de naviguer toohello l’application web, puis réessayez.

## Conclusion
Félicitations ! application de WordPress Hello a maintenant un tooaid centralisée en mémoire cache dans augmente le débit. N’oubliez pas, hello Web applications Memcache Shim peut être utilisé avec n’importe quel client Memcache, quelle que soit la langue ou une application framework de programmation. tooprovide des commentaires ou tooask questions shim Memcache d’applications Web de hello, validez trop[Forums MSDN] [ 10] ou [Stackoverflow][11].

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

[0]: ../redis-cache/cache-dotnet-how-to-use-azure-redis-cache.md#create-a-cache
[1]: http://bit.ly/1t0KxBQ
[2]: http://manage.windowsazure.com
[3]: http://portal.azure.com
[4]: /powershell/azureps-cmdlets-docs
[5]: /downloads
[6]: http://pecl.php.net
[7]: http://pecl.php.net/package/memcache
[8]: http://blog.syntaxc4.net/post/2015/02/05/how-to-enable-a-site-extension-in-azure-websites.aspx
[9]: http://redis.io/download#installation
[10]: https://social.msdn.microsoft.com/Forums/home?forum=windowsazurewebsitespreview
[11]: http://stackoverflow.com/questions/tagged/azure-web-sites
[12]: /services/cache/
[13]: http://memcached.org
