---
title: aaaConfigure PHP dans Azure App Service Web Apps | Documents Microsoft
description: "Découvrez comment tooconfigure hello installation de PHP par défaut ou ajouter une installation de PHP personnalisée pour les applications Web dans Azure App Service."
services: app-service
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 95c4072b-8570-496b-9c48-ee21a223fb60
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 2e461e4a269a4ce5614f5f05560f38bc53066251
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-php-in-azure-app-service-web-apps"></a>Configurer PHP dans Azure App Service Web Apps
## <a name="introduction"></a>Introduction
Ce guide vous explique comment tooconfigure hello intégré runtime PHP pour les applications Web dans [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714), fournir un runtime PHP personnalisé et activer les extensions. toouse du Service d’applications, inscrivez-vous hello [version d’évaluation gratuite]. tooget hello plus à partir de ce guide, vous devez d’abord créer une application web PHP dans le Service d’applications.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="how-to-change-hello-built-in-php-version"></a>Comment : modifier hello intégrés PHP la version
Par défaut, PHP 5.5 est installé et immédiatement utilisable lorsque vous créez une application web App Service. Hello la meilleure façon toosee hello version disponible révision sa configuration par défaut, et extensions activées hello est toodeploy un script qui appelle hello [phpinfo()] (fonction).

Les versions PHP 5.6 et PHP 7.0 sont également disponibles, mais ne sont pas activées par défaut. tooupdate hello version de PHP, suivez une des méthodes suivantes :

### <a name="azure-portal"></a>Portail Azure
1. Parcourir l’application web tooyour hello [Azure Portal](https://portal.azure.com) , puis cliquez sur hello **paramètres** bouton.
   
    ![Paramètres d’application web][settings-button]
2. À partir de hello **paramètres** panneau sélectionner **paramètres de l’Application** et choisissez la nouvelle version PHP hello.
   
    ![Paramètres de l’application][application-settings]
3. Cliquez sur hello **enregistrer** bouton haut hello hello **paramètres de l’application Web** panneau.
   
    ![Enregistrer les paramètres de configuration][save-button]

### <a name="azure-powershell-windows"></a>Azure PowerShell (Windows)
1. Ouvrez Azure PowerShell et compte de connexion tooyour :
   
        PS C:\> Login-AzureRmAccount
2. Définir la version PHP hello pour l’application web de hello.
   
        PS C:\> Set-AzureWebsite -PhpVersion {5.5 | 5.6 | 7.0} -Name {app-name}
3. version de PHP Hello est maintenant définie. Vous pouvez confirmer les paramètres suivants :
   
        PS C:\> Get-AzureWebsite -Name {app-name} | findstr PhpVersion

### <a name="azure-command-line-interface-linux-mac-windows"></a>Interface en ligne de commande Azure (Linux, Mac et Windows)
toouse hello Interface de ligne de commande Azure, vous devez avoir **Node.js** installé sur votre ordinateur.

1. Ouvrez Terminal Server et compte de connexion tooyour.
   
        azure login
2. Définir la version PHP hello pour l’application web de hello.
   
        azure site set --php-version {5.5 | 5.6 | 7.0} {app-name}

3. version de PHP Hello est maintenant définie. Vous pouvez confirmer les paramètres suivants :
   
        azure site show {app-name}

> [!NOTE] 
> Hello [Azure CLI 2.0](https://github.com/Azure/azure-cli) commandes équivalente toohello ci-dessus sont :
>
>

    az login
    az appservice web config update --php-version {5.5 | 5.6 | 7.0} -g {resource-group-name} -n {app-name}
    az appservice web config show -g {resource-group-name} -n {app-name}

## <a name="how-to-change-hello-built-in-php-configurations"></a>Comment : modifier les configurations de PHP hello intégrées
Pour n’importe quel runtime PHP intégré, vous pouvez modifier les options de configuration hello en suivant les étapes de hello ci-dessous. (Pour plus d’informations sur les directives de php.ini, consultez la page [Liste des directives du php.ini].)

### <a name="changing-phpiniuser-phpiniperdir-phpiniall-configuration-settings"></a>Modification des paramètres de configuration PHP\_INI\_USER, PHP\_INI\_PERDIR et PHP\_INI\_ALL
1. Ajouter un [. user.ini] tooyour répertoire racine des fichiers.
2. Ajouter des toohello des paramètres de configuration `.user.ini` à l’aide du fichier hello la même syntaxe que vous utiliseriez dans un `php.ini` fichier. Par exemple, si vous souhaitiez tooturn hello `display_errors` paramètre et définissez `upload_max_filesize` définition too10M, votre `.user.ini` fichier contient ce texte :
   
        ; Example Settings
        display_errors=On
        upload_max_filesize=10M
   
        ; OPTIONAL: Turn this on toowrite errors tood:\home\LogFiles\php_errors.log
        ; log_errors=On
3. Déployez votre application web.
4. Redémarrage de l’application web de hello. (Le redémarrage est nécessaire, car la fréquence de hello avec quels PHP lit `.user.ini` fichiers est régie par hello `user_ini.cache_ttl` paramètre, qui est un paramètre de niveau système et 300 secondes (5 minutes) par défaut. Redémarrer l’application web hello force tooread hello nouveau les paramètres PHP dans hello `.user.ini` fichier.)

En tant qu’un autre toousing un `.user.ini` fichier, vous pouvez utiliser hello [ini_set()] fonction scripts tooset options de configuration qui ne sont pas les directives au niveau du système.

### <a name="changing-phpinisystem-configuration-settings"></a>Modification des paramètres de configuration PHP\_INI\_SYSTEM
1. Ajouter une application Web de tooyour paramètre d’application avec la clé de hello `PHP_INI_SCAN_DIR` et la valeur`d:\home\site\ini`
2. Créer un `settings.ini` de fichiers à l’aide de la Console de Kudu (http://&lt;-nom du site&gt;. scm.azurewebsite.net) Bonjour `d:\home\site\ini` active.
3. Ajouter des toohello des paramètres de configuration `settings.ini` à l’aide du fichier hello la même syntaxe que dans un fichier php.ini. Par exemple, si vous souhaitiez toopoint hello `curl.cainfo` définition tooa `*.crt` de fichiers et de définir 'wincache.maxfilesize' paramètre too512K, votre `settings.ini` fichier contient ce texte :
   
        ; Example Settings
        curl.cainfo="%ProgramFiles(x86)%\Git\bin\curl-ca-bundle.crt"
        wincache.maxfilesize=512
4. Redémarrez vos modifications de hello tooload application Web.

## <a name="how-to-enable-extensions-in-hello-default-php-runtime"></a>Comment : activer les extensions dans hello par défaut du runtime PHP
Comme indiqué dans la section précédente de hello, version PHP de hello meilleure manière toosee hello par défaut, sa configuration par défaut et hello activé extensions est toodeploy un script qui appelle [phpinfo()]. tooenable des extensions supplémentaires, suivez les étapes de hello ci-dessous :

### <a name="configure-via-ini-settings"></a>Configuration par des paramètres ini
1. Ajouter un `ext` Active toohello `d:\home\site` active.
2. Put `.dll` des fichiers d’extension Bonjour `ext` répertoire (par exemple, `php_xdebug.dll`). Assurez-vous que les extensions de hello sont compatibles avec la version par défaut de PHP et sont VC9 et est non thread-safe (nts) compatible.
3. Ajouter une application Web de tooyour paramètre d’application avec la clé de hello `PHP_INI_SCAN_DIR` et la valeur`d:\home\site\ini`
4. Dans `d:\home\site\ini`, créez un fichier `ini` appelé `extensions.ini`.
5. Ajouter des toohello des paramètres de configuration `extensions.ini` à l’aide du fichier hello la même syntaxe que dans un fichier php.ini. Par exemple, si vous souhaitiez tooenable hello MongoDB et XDebug les extensions, votre `extensions.ini` fichier contient ce texte :
   
        ; Enable Extensions
        extension=d:\home\site\ext\php_mongo.dll
        zend_extension=d:\home\site\ext\php_xdebug.dll
6. Redémarrez vos modifications de hello tooload application Web.

### <a name="configure-via-app-setting"></a>Configuration par un paramètre d’application
1. Ajouter un `bin` répertoire racine de toohello active.
2. Put `.dll` des fichiers d’extension Bonjour `bin` répertoire (par exemple, `php_xdebug.dll`). Assurez-vous que les extensions de hello sont compatibles avec la version par défaut de PHP et sont VC9 et est non thread-safe (nts) compatible.
3. Déployez votre application web.
4. Parcourir l’application web tooyour hello portail Azure, puis cliquez sur hello **paramètres** bouton.
   
    ![Paramètres d’application web][settings-button]
5. À partir de hello **paramètres** panneau sélectionner **paramètres de l’Application** et faites défiler toohello **paramètres de l’application** section.
6. Bonjour **paramètres de l’application** en créant un **PHP_EXTENSIONS** clé. valeur Hello pour cette clé serait une racine du chemin relatif toowebsite : **bin\your-ext-fichier**.
   
    ![Activer une extension dans les paramètres d'application][php-extensions]
7. Cliquez sur hello **enregistrer** bouton haut hello hello **paramètres de l’application Web** panneau.
   
    ![Enregistrer les paramètres de configuration][save-button]

Les extensions Zend sont également prises en charge à l’aide d’une clé **PHP_ZENDEXTENSIONS**. tooenable plusieurs extensions, inclure une liste séparée par des virgules de `.dll` fichiers pour la valeur du paramètre d’application hello.

## <a name="how-to-use-a-custom-php-runtime"></a>Utilisation d’un runtime PHP personnalisé
Au lieu de l’exécution PHP par défaut hello, application de Service Web Apps permet un runtime PHP, vous devez fournir tooexecute scripts PHP. Hello runtime que vous fournissez peut être configuré par un `php.ini` fichier que vous fournissez également. toouse un runtime PHP personnalisé avec des applications Web, suivez les étapes de hello ci-dessous.

1. Obtenez une version de PHP pour Windows, compatible avec NTS (Non-Thread-Safe), VC9 ou VC11. Les versions récentes de PHP pour Windows sont disponibles à l’adresse suivante : [http://windows.php.net/download/]. Les versions plus anciennes sont accessibles dans l’archive hello ici : [http://windows.php.net/downloads/releases/archives/].
2. Modifier hello `php.ini` fichier pour le runtime. Notez que tout paramètre de configuration correspondant à une directive de niveau système uniquement est ignoré par Web Apps. Pour plus d'informations sur les directives de niveau système uniquement, consultez la page [Liste des directives du php.ini].
3. Si vous le souhaitez, ajoutez des extensions tooyour PHP runtime et les activer dans hello `php.ini` fichier.
4. Ajouter un `bin` répertoire tooyour racine répertoire et put hello qui contient votre runtime PHP qu’il contient (par exemple, `bin\php`).
5. Déployez votre application web.
6. Parcourir l’application web tooyour hello portail Azure, puis cliquez sur hello **paramètres** bouton.
   
    ![Paramètres d’application web][settings-button]
7. À partir de hello **paramètres** panneau sélectionner **paramètres de l’Application** et faites défiler toohello **mappages de gestionnaires** section. Ajouter `*.php` toohello Extension de champ et ajouter hello chemin d’accès toohello `php-cgi.exe` exécutable. Si vous placez votre runtime PHP dans hello `bin` répertoire racine hello de votre application, chemin d’accès de hello sera `D:\home\site\wwwroot\bin\php\php-cgi.exe`.
   
    ![Indiquer le gestionnaire dans les mappages][handler-mappings]
8. Cliquez sur hello **enregistrer** bouton haut hello hello **paramètres de l’application Web** panneau.
   
    ![Enregistrer les paramètres de configuration][save-button]

<a name="composer" />

## <a name="how-to-enable-composer-automation-in-azure"></a>Activation de l’automatisation du Compositeur dans Azure
Par défaut, App Service ne fait rien avec composer.json, si vous en avez un dans votre projet PHP. Si vous utilisez [déploiement Git](app-service-deploy-local-git.md), vous pouvez activer composer.json du traitement au cours `git push` par activation de l’extension de Composer hello.

> [!NOTE]
> Vous pouvez [voter pour la prise en charge haut de gamme de Compositeur dans App Service ici](https://feedback.azure.com/forums/169385-web-apps-formerly-websites/suggestions/6477437-first-class-support-for-composer-and-pip)!
> 
> 

1. Dans votre PHP web lame l’application hello [portail Azure](https://portal.azure.com), cliquez sur **outils** > **Extensions**.
   
    ![Azure Portal Paramètres Panneau tooenable automation Composer dans Azure](./media/web-sites-php-configure/composer-extension-settings.png)
2. Cliquez sur **Ajouter** puis sur **Compositeur**.
   
    ![Ajouter l’automation de Composer Composer extension tooenable dans Azure](./media/web-sites-php-configure/composer-extension-add.png)
3. Cliquez sur **OK** tooaccept les conditions juridiques. Cliquez sur **OK** à nouveau les extension tooadd hello.
   
    Hello **extensions installées** panneau affiche désormais les extensions de Composer hello.  
    ![Accepter l’automation de Composer tooenable juridiques dans Azure](./media/web-sites-php-configure/composer-extension-view.png)
4. À présent, effectuer `git add`, `git commit`, et `git push` comme dans la section précédente de hello. Vous verrez alors que Compositeur installe des interdépendances définies dans composer.json.
   
    ![Déploiement Git avec automatisation du Compositeur dans Azure](./media/web-sites-php-configure/composer-extension-success.png)

## <a name="next-steps"></a>Étapes suivantes
Pour plus d’informations, consultez hello [centre de développement PHP](/develop/php/).

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

[version d’évaluation gratuite]: https://www.windowsazure.com/pricing/free-trial/
[phpinfo()]: http://php.net/manual/en/function.phpinfo.php
[select-php-version]: ./media/web-sites-php-configure/select-php-version.png
[Liste des directives du php.ini]: http://www.php.net/manual/en/ini.list.php
[. user.ini]: http://www.php.net/manual/en/configuration.file.per-user.php
[ini_set()]: http://www.php.net/manual/en/function.ini-set.php
[application-settings]: ./media/web-sites-php-configure/application-settings.png
[settings-button]: ./media/web-sites-php-configure/settings-button.png
[save-button]: ./media/web-sites-php-configure/save-button.png
[php-extensions]: ./media/web-sites-php-configure/php-extensions.png
[handler-mappings]: ./media/web-sites-php-configure/handler-mappings.png
[http://windows.php.net/download/]: http://windows.php.net/download/
[http://windows.php.net/downloads/releases/archives/]: http://windows.php.net/downloads/releases/archives/
[SETPHPVERCLI]: ./media/web-sites-php-configure/ChangePHPVersion-XPlatCLI.png
[GETPHPVERCLI]: ./media/web-sites-php-configure/ShowPHPVersion-XplatCLI.png
[SETPHPVERPS]: ./media/web-sites-php-configure/ChangePHPVersion-PS.png
[GETPHPVERPS]: ./media/web-sites-php-configure/ShowPHPVersion-PS.png

