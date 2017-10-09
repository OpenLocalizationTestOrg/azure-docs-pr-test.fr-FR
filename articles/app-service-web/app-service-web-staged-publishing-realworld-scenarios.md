---
title: environnements de DevOps aaaUse efficacement pour votre application web | Documents Microsoft
description: "Découvrez comment toouse déploiement emplacements tooset d’et de gérer plusieurs environnements de développement de votre application"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 16a594dc-61f5-4984-b5ca-9d5abc39fb1e
ms.service: app-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 61a552e735a4ad9769b661d7c988744074ba2962
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-devops-environments-effectively-for-your-web-apps"></a>Utiliser efficacement les environnements DevOps pour vos applications web
Cet article vous montre comment tooset configurer et gérer les déploiements d’applications web lorsque plusieurs versions de votre application se trouvent dans différents environnements, tels que le développement, intermédiaire, l’assurance qualité (AQ) et de production. Chaque version de votre application peut être considérée comme un environnement de développement pour objectif spécifique de hello de votre processus de déploiement. Par exemple, les développeurs peuvent utiliser hello QA environnement tootest hello la qualité de l’application hello avant qu’ils push hello modifications tooproduction.
Plusieurs environnements de développement peuvent être un défi, car vous devez tootrack code, de gérer les ressources (calcul, l’application web, base de données, du cache, etc.) et de déployer le code dans des environnements.

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a>Configurer un environnement hors production (intermédiaire, développement, assurance qualité)
Une fois une application web de production est en cours d’exécution, étape suivante de hello est toocreate un environnement hors production. toouse les emplacements de déploiement, assurez-vous que vous êtes en mode de plan Standard ou Premium du Service d’applications Azure hello. Les emplacements de déploiement sont des applications web dynamiques qui ont leurs propres noms d’hôte. Éléments de configuration et de contenu Web application peuvent être échangés entre deux emplacements de déploiement, y compris l’emplacement de production hello. Lorsque vous déployez votre emplacement de déploiement d’application tooa, vous obtenez hello avantages suivants :

- Vous pouvez valider les modifications tooa web app dans un emplacement de déploiement intermédiaire avant d’échanger d’application hello avec l’emplacement de production hello.
- Lorsque vous déployez d’abord un emplacement tooa d’application web et il échangez en production, toutes les instances de l’emplacement de hello sont préparées avant d’être permutés en production. Ce processus élimine les temps d’arrêt lorsque vous déployez votre application web. redirection du trafic Hello est transparente, et aucune demande n’est supprimés en raison d’opérations de tooswap. tooautomate ce flux de travail entière, configurer [échange automatique](web-sites-staged-publishing.md#configure-auto-swap) lorsque la validation préalable d’échange n’est pas nécessaire.
- Après un échange, d’emplacement hello qui possède désormais les hello précédemment préparé l’application web a hello précédente application web de production. Si les modifications de hello permutées dans l’emplacement de production hello sont pas comme prévu, vous pouvez effectuer hello même échange immédiatement tooget votre « dernière bonne configuration connue » arrière d’application web.

tooset un emplacement de déploiement intermédiaire, consultez [configurer d’environnements intermédiaires pour applications web dans Azure App Service](web-sites-staged-publishing.md). Chaque environnement doit inclure son propre jeu de ressources. Par exemple, si votre application web utilise une base de données, les applications web intermédiaire et de production doivent utiliser différentes bases de données. Ajouter des ressources de l’environnement intermédiaire développement telles que la base de données, le stockage ou cache tooset votre environnement de développement intermédiaire.

## <a name="examples-of-using-multiple-development-environments"></a>Exemples d’utilisation de plusieurs environnements de développement
Un projet doit suivre la gestion du code source avec au moins deux environnements : développement et production. Si vous utilisez des systèmes de gestion de contenu (CMSs), les infrastructures d’applications, etc., application hello ne prenne pas en charge ce scénario sans personnalisation. Cette éventualité a la valeur true pour certaines des infrastructures hello connues qui sont décrites dans les sections suivantes de hello. Un grand nombre de questions proviennent toomind lorsque vous travaillez avec CMS/infrastructures, telles que :

- Comment vous décomposez le contenu hello dans différents environnements ?
- Quels fichiers pouvez-vous modifier sans affecter les mises à jour des versions d’infrastructure ?
- Comment gérez-vous les configurations par environnement ?
- Comment gérer les mises à jour de la version des modules, des plug-ins et infrastructure de base hello ?

Il existe de nombreuses façons tooset, plusieurs environnements pour votre projet. Hello exemples suivants illustrent une méthode pour chaque application respectif.

### <a name="wordpress"></a>WordPress
Dans cette section, vous allez apprendre comment tooset un workflow de déploiement à l’aide de connecteurs pour WordPress. WordPress, comme la plupart des solutions CMS, ne prend pas en charge l’utilisation de plusieurs environnements de développement sans personnalisation. fonctionnalité des applications Web Hello du Service d’application Azure a quelques fonctionnalités qui la rendent facile toostore des paramètres de configuration à l’extérieur de votre code.

1. Avant de créer un emplacement intermédiaire, configurer votre toosupport de code d’application plusieurs environnements. toosupport plusieurs environnements dans WordPress, vous devez tooedit `wp-config.php` sur votre développement local d’application web et ajouter hello suivant le code au début de hello du fichier de hello. Ce processus permettra toopick hello correct configuration de votre application en fonction de l’environnement sélectionné de hello.

    ```
    // Support multiple environments
    // set hello config file based on current environment
    if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) {
    // local development
     $config_file = 'config/wp-config.local.php';
    }
    elseif ((strpos(getenv('WP_ENV'),'stage') !== false) || (strpos(getenv('WP_ENV'),'prod' )!== false ))
    //single file for all azure development environments
     $config_file = 'config/wp-config.azure.php';
    }
    $path = dirname(__FILE__). '/';
    if (file_exists($path. $config_file)) {
    // include hello config file if it exists, otherwise WP is going toofail
    require_once $path. $config_file;
    ```

2. Créez un dossier sous la racine de l’application web appelée `config`et ajoutez hello `wp-config.azure.php` et `wp-config.local.php` les fichiers, qui représentent respectivement les votre environnement Azure et votre environnement local.

3. Copiez hello dans `wp-config.local.php`:

    ```
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', 'yourdatabasename');

    /** MySQL database username */
    define('DB_USER', 'yourdbuser');

    /** MySQL database password */
    define('DB_PASSWORD', 'yourpassword');

    /** MySQL hostname */
    define('DB_HOST', 'localhost');
    /**
     * For developers: WordPress debugging mode.
     * * Change this tootrue tooenable hello display of notices during development.
     * It is strongly recommended that plugin and theme developers use WP_DEBUG
     * in their development environments.
     */
    define('WP_DEBUG', true);

    //Security key settings
    define('AUTH_KEY', 'put your unique phrase here');
    define('SECURE_AUTH_KEY','put your unique phrase here');
    define('LOGGED_IN_KEY','put your unique phrase here');
    define('NONCE_KEY', 'put your unique phrase here');
    define('AUTH_SALT', 'put your unique phrase here');
    define('SECURE_AUTH_SALT', 'put your unique phrase here');
    define('LOGGED_IN_SALT', 'put your unique phrase here');
    define('NONCE_SALT', 'put your unique phrase here');

    /**
     * WordPress Database Table prefix.
     *
     * You can have multiple installations in one database if you give each a unique
     * prefix. Only numbers, letters, and underscores please!
     */
    $table_prefix = 'wp_';
    ```

    Hello sécurité clés comme illustré dans le code précédent hello peut aider à tooprevent votre application web à partir de piratée, donc utiliser les valeurs uniques. Si vous avez besoin de chaîne de hello toogenerate pour les clés de sécurité mentionnés dans le code hello, vous pouvez [générateur automatique de toohello accédez](https://api.wordpress.org/secret-key/1.1/salt) toocreate nouvelles paires clé/valeur.

4. Code copie hello suivant de `wp-config.azure.php`:

    ```    
    <?php
    // MySQL settings
    /** hello name of hello database for WordPress */

    define('DB_NAME', getenv('DB_NAME'));

    /** MySQL database username */
    define('DB_USER', getenv('DB_USER'));

    /** MySQL database password */
    define('DB_PASSWORD', getenv('DB_PASSWORD'));

    /** MySQL hostname */
    define('DB_HOST', getenv('DB_HOST'));

    /**
    * For developers: WordPress debugging mode.
    *
    * Change this tootrue tooenable hello display of notices during development.
    * It is strongly recommended that plugin and theme developers use WP_DEBUG
    * in their development environments.
    * Turn on debug logging tooinvestigate issues without displaying tooend user. For WP_DEBUG_LOG to
    * do anything, WP_DEBUG must be enabled (true). WP_DEBUG_DISPLAY should be used in conjunction
    * with WP_DEBUG_LOG so that errors are not displayed on hello page */

    */
    define('WP_DEBUG', getenv('WP_DEBUG'));
    define('WP_DEBUG_LOG', getenv('TURN_ON_DEBUG_LOG'));
    define('WP_DEBUG_DISPLAY',false);

    //Security key settings
    /** If you need toogenerate hello string for security keys mentioned above, you can go hello automatic generator toocreate new keys/values: https://api.wordpress.org/secret-key/1.1/salt **/
    define('AUTH_KEY',getenv('DB_AUTH_KEY'));
    define('SECURE_AUTH_KEY', getenv('DB_SECURE_AUTH_KEY'));
    define('LOGGED_IN_KEY', getenv('DB_LOGGED_IN_KEY'));
    define('NONCE_KEY', getenv('DB_NONCE_KEY'));
    define('AUTH_SALT', getenv('DB_AUTH_SALT'));
    define('SECURE_AUTH_SALT', getenv('DB_SECURE_AUTH_SALT'));
    define('LOGGED_IN_SALT',  getenv('DB_LOGGED_IN_SALT'));
    define('NONCE_SALT',  getenv('DB_NONCE_SALT'));

    /**
    * WordPress Database Table prefix.
    *
    * You can have multiple installations in one database if you give each a unique
    * prefix. Only numbers, letters, and underscores please!
    */
    $table_prefix = getenv('DB_PREFIX');
    ```

#### <a name="use-relative-paths"></a>Utiliser des chemins relatifs
Une dernière tooconfigure de chose dans l’application de WordPress hello est chemins d’accès relatifs. WordPress stocke les informations de l’URL de base de données hello. Ce stockage, le déplacement de contenu à partir d’un environnement tooanother plus difficile. Vous avez besoin de base de données tooupdate hello chaque fois que vous déplacez toostage local ou les environnements tooproduction étape. risque de hello tooreduce des problèmes qui peut être dû au déploiement d’une base de données chaque fois que vous déployez à partir d’un environnement tooanother, utilisez hello [relatif racine lie le plug-in](https://wordpress.org/plugins/root-relative-urls/), que vous pouvez installer à l’aide de l’administrateur de WordPress hello tableau de bord.

Ajouter hello suivant entrées tooyour `wp-config.php` fichier avant hello `That's all, stop editing!` commentaire :

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

Activer le plug-in hello via hello `Plugins` menu dans le tableau de bord administrateur WordPress. Enregistrez les paramètres permalink pour l’application WordPress.

#### <a name="hello-final-wp-configphp-file"></a>Hello final `wp-config.php` fichier
Les mises à jour de WordPress n’affecteront pas vos fichiers `wp-config.php`, `wp-config.azure.php` et `wp-config.local.php`. Voici une version finale de hello `wp-config.php` fichier :

```
<?php
/**
 * hello base configurations of hello WordPress.
 *
 * This file has hello following configurations: MySQL settings, Table Prefix,
 * Secret Keys, and ABSPATH. You can find more information by visiting
 *
 * Codex page. You can get hello MySQL settings from your web host.
 *
 * This file is used by hello wp-config.php creation script during the
 * installation. You don't have toouse hello web web app, you can just copy this file
 * too"wp-config.php" and fill in hello values.
 *
 * @package WordPress
 */

// Support multiple environments
// set hello config file based on current environment
if (strpos($_SERVER['HTTP_HOST'],'localhost') !== false) { // local development
  $config_file = 'config/wp-config.local.php';
}
elseif ((strpos(getenv('WP_ENV'),'stage') !== false) ||(strpos(getenv('WP_ENV'),'prod' )!== false )){
  $config_file = 'config/wp-config.azure.php';
}


$path = dirname(__FILE__). '/';
if (file_exists($path. $config_file)) {
  // include hello config file if it exists, otherwise WP is going toofail
  require_once $path. $config_file;
}

/** Database Charset toouse in creating database tables. */
define('DB_CHARSET', 'utf8');

/** hello Database Collate type. Don't change this if in doubt. */
define('DB_COLLATE', '');


/* That's all, stop editing! Happy blogging. */

define('WP_HOME', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_SITEURL', 'http://'. $_SERVER['HTTP_HOST']);
define('WP_CONTENT_URL', '/wp-content');
define('DOMAIN_CURRENT_SITE', $_SERVER['HTTP_HOST']);

/** Absolute path toohello WordPress directory. */
if ( !defined('ABSPATH') )
    define('ABSPATH', dirname(__FILE__). '/');

/** Sets up WordPress vars and included files. */
require_once(ABSPATH. 'wp-settings.php');
```

#### <a name="set-up-a-staging-environment"></a>Configuration d’un environnement intermédiaire
1. Si vous disposez déjà d’une application web de WordPress en cours d’exécution sur votre abonnement Azure, connectez-vous à toohello [portail Azure](http://portal.azure.com), puis ouvrez l’application web tooyour WordPress. Si vous n’avez pas une application web de WordPress, vous pouvez créer un à partir de hello Azure Marketplace. toolearn, voir [créer une application web de WordPress dans Azure App Service](web-sites-php-web-site-gallery.md).
Cliquez sur **paramètres** > **les emplacements de déploiement** > **ajouter** toocreate un emplacement de déploiement avec le nom de hello *étape*. Un emplacement de déploiement est une autre application web parts hello autant de ressources que l’application hello web principal que vous avez créé précédemment.

    ![Créer un emplacement de déploiement intermédiaire](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. Ajouter une autre base de données MySQL, par exemple `wordpress-stage-db`, groupe de ressources tooyour `wordpressapp-group`.

    ![Ajouter le groupe de tooresource de base de données MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. Mettre à jour les chaînes de connexion de hello pour votre scène déploiement emplacement toopoint toohello nouvelle base de données, `wordpress-stage-db`. Votre application web de production, `wordpressprodapp`et de l’application web, de mise en lots `wordpressprodapp-stage`, bases de données doit toodifferent de point.

#### <a name="configure-environment-specific-app-settings"></a>Configurer les paramètres d’application spécifiques à l’environnement
Les développeurs peuvent stocker des paires clé/valeur des chaînes dans Azure en tant que partie des informations de configuration hello, appelées **paramètres de l’application**, qui est associé à une application web. Lors de l’exécution, les applications web automatiquement récupérer ces valeurs et les rendre disponible toocode qui s’exécute dans votre application web. Du point de vue de la sécurité, c’est un avantage car les informations sensibles comme les chaînes de connexion à une base de données qui incluent des mots de passe, ne sont jamais affichées en clair dans un fichier tel que `wp-config.php`.

Ce processus, qui est expliqué dans hello après les paragraphes, est utile, car il inclut des modifications de fichiers et les modifications de base de données pour l’application de WordPress hello :

* Mise à jour de la version de WordPress
* Ajout, modification ou mise à jour de modules complémentaires
* Ajout, modification ou mise à jour des thèmes

Configuration des paramètres d’application pour :

* les informations de base de données
* l’activation/la désactivation de la journalisation WordPress
* Paramètres de sécurité WordPress

![Paramètres de l’application pour l’application web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

Assurez-vous que vous ajoutez hello suivant les paramètres de l’application pour votre web app et l’étape de l’emplacement de production. Notez que l’application web de production hello et l’application web intermédiaire utilisant différentes bases de données.

1. Désactivez hello **paramètre d’emplacement** case à cocher pour tous les paramètres de paramètres hello sauf WP_ENV. Ce processus échangera les configuration hello pour votre application web, le contenu du fichier et la base de données. Si **paramètre d’emplacement** est vérifié, paramètres de l’application et la configuration de chaîne de connexion de l’application hello web seront *pas* déplacer entre les environnements lors de l’exécution une **échanger** opération. Les modifications apportées à la base de données ne bloqueront pas votre application web de production.

2. Déployer hello développement local environnement web application toohello étape web d’applications et de la base de données à l’aide de WebMatrix ou les outils de votre choix, tels que FTP, Git ou PhpMyAdmin.

    ![Boîte de dialogue de publication de Matrix pour l’application web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. Parcourir et tester votre application web intermédiaire. Compte tenu d’un scénario dans lequel le thème de l’application web hello hello est toobe mis à jour, voici hello intermédiaires de l’application web.

    ![Parcourir l’application web intermédiaire avant d’échanger les emplacements](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. Si tout semble correct, cliquez sur hello **échanger** bouton sur votre zone de transit toomove d’application web de votre environnement de production toohello contenu. Dans ce cas, remplacez hello web app et la base de données hello dans des environnements pendant chaque **Swap** opération.

    ![Échanger les modifications de l’aperçu pour WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > Si votre scénario doit diffuser les fichiers tooonly (aucune mise à jour de base de données), puis vérifiez **paramètre d’emplacement** pour tous les hello liés à la base de données *paramètres de l’application* et *deparamètresdechaînesdeconnexion*Bonjour **paramètres de l’application Web** panneau dans hello portail Azure avant de procéder à hello **échanger**. Dans ce cas, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER et les paramètres de la chaîne de connexion par défaut ne s’affichent pas dans les modifications de présentation lors de l’**échange**. À ce stade, quand vous terminez hello **échanger** opération, hello WordPress l’application web sera ont hello met à jour uniquement les fichiers.
    >
    >

    Avant cela, une **échanger**, voici hello production WordPress web app.
    ![Application web de production avant l’échange d’emplacements](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)

    Après avoir hello **échanger** opération, le thème hello a été mis à jour sur votre application web de production.

    ![Application web de production après l’échange d’emplacements](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. Lorsque vous devez tooroll précédent, vous pouvez accéder à web de production toohello **paramètres de l’application**, puis cliquez sur hello **échanger** bouton tooswap hello web app et la base de données à partir de l’emplacement de production toostaging. N’oubliez pas que si les modifications de base de données sont incluses dans un **échanger** opération, puis hello prochaine fois que vous déployez tooyour intermédiaires de l’application web, vous devez toodeploy hello modifications toohello actuelle base de données pour votre application web intermédiaire. base de données actuelle Hello peut être la base de données de production précédent hello ou étape hello.

#### <a name="summary"></a>Résumé
Voici un processus générique pour une application qui possède une base de données :

1. Installer l’application hello sur votre environnement local.
2. Incluez les configurations propres à l’environnement (local et Azure Web Apps).
3. Configurez vos environnements intermédiaire et de production pour Web Apps.
4. Si vous avez une application de production en cours d’exécution sur Azure, synchroniser votre contenu (fichiers/code et la base de données) toolocal et mise en lots environnements de production.
5. Développez votre application sur votre environnement local.
6. Placez votre application web de production en maintenance ou en mode verrouillé et synchroniser le contenu de la base de données à partir d’environnements de production toostaging et de développement.
7. Déployer toohello environnement et test de mise en lots.
8. Déployer un environnement de tooproduction.
9. Répétez les étapes 4 à 6.

### <a name="umbraco"></a>Umbraco
Dans cette section, vous allez apprendre comment hello CMS Umbraco utilise un toodeploy module personnalisé dans plusieurs environnements de DevOps. Cet exemple fournit une approche différente de toomanaging plusieurs environnements de développement.

[Umbraco CMS](http://umbraco.com/) est une solution de CMS .NET prisée de nombreux développeurs. Il fournit hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy de module à partir d’environnements de développement toostaging tooproduction. Vous pouvez facilement créer un environnement de développement local pour une application web Umbraco CMS à l’aide de Visual Studio ou de WebMatrix.

- [Créer une application web Umbraco avec Visual Studio](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [Créer une application web Umbraco avec WebMatrix](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

N’oubliez pas tooremove hello `install` dossier sous votre application et ne jamais télécharger des applications web toostage ou de production. Ce didacticiel utilise WebMatrix.

#### <a name="set-up-a-staging-environment"></a>Configuration d’un environnement intermédiaire
1. Créer un emplacement de déploiement, comme mentionné précédemment pour hello Umbraco CMS web app, si que vous disposez déjà d’une application web de CMS Umbraco et en cours d’exécution. Si vous ne le faites pas, vous pouvez créer un à partir de hello Marketplace.
2. Mettre à jour la chaîne de connexion hello pour votre toohello de toopoint étape déploiement emplacement nouveau **umbraco-étape-db** base de données. Votre application web de production (umbraositecms-1) et l’application web intermédiaire (umbracositecms-1-étape) *doit* toodifferent de point de bases de données.

    ![Mettre à jour la chaîne de connexion pour l’application web intermédiaire vers une nouvelle base de données intermédiaire](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. Cliquez sur **obtenir publier les paramètres** pour l’emplacement de déploiement hello **étape**. Ce processus télécharge un fichier de paramètres de publication qui stocke toutes les informations de hello que Visual Studio ou WebMatrix, toopublish votre application à partir de l’application web Azure hello développement local web application toohello.

    ![Obtenir le paramètre de hello intermédiaires de l’application web de publication](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. Ouvrez votre application web de développement locale dans WebMatrix ou Visual Studio. Ce didacticiel utilise WebMatrix. Tout d’abord, vous devez tooimport hello publier le fichier de paramètres pour votre application web intermédiaire.

    ![Importer les paramètres de publication d’Umbraco à l’aide de Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. Passez en revue les modifications dans la boîte de dialogue hello et déployer votre application web locale application tooyour web Azure, *umbracositecms-1-étape*. Lorsque vous déployez des fichiers directement tooyour intermédiaire web app, vous serez omettre les fichiers Bonjour `~/app_data/TEMP/` dossier, car ces fichiers seront régénérés lors de l’application web hello étape a démarré. Vous devez également omettre hello `~/app_data/umbraco.config` fichier, qui sera également régénéré.

    ![Passer en revue les modifications de publication dans une matrice web](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. Après avoir publié correctement hello Umbraco local web application toohello intermédiaire web app, parcourir l’application web de la zone de transit tooyour et exécuter quelques tests toorule, tous les points.

#### <a name="set-up-hello-courier2-deployment-module"></a>Configurer le module de déploiement hello Courier2
Avec hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, vous pouvez simplement avec le bouton droit toopush contenu, les feuilles de style et les modules de développement à partir d’une site web application tooa application web de production. Ce processus réduit les risques de hello de rupture de votre application web de production lorsque vous déployez une mise à jour.
Acheter une licence pour Courier2 hello `*.azurewebsites.net` domaine et votre domaine personnalisé (par exemple http://abc.com). Après l’achat de licence de hello, place hello téléchargé licence (. Fichier LIC) Bonjour `bin` dossier.

![Placer un fichier de licence sous un dossier bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. [Télécharger le package de hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/). Signe dans tooyour étape web app, par exemple http://umbracocms-site-stage.azurewebsites.net/umbraco, cliquez sur hello **Developer** menu, puis sur **Packages** > **installer package local**.

    ![Programme d’installation de Umbraco Package](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. Télécharger le package de hello Courier2 à l’aide du programme d’installation hello.

    ![Téléchargement du package du module courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. package de hello tooconfigure, vous devez fichier courier.config tooupdate hello hello **Config** dossier de votre application web.

    ```xml
    <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="production web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1.azurewebsites.net</url>
          <user>0</user>
          <!--<login>user@email.com</login> -->
          <!-- <password>user_password</password>-->
          <!-- <passwordEncoding>Clear</passwordEncoding>-->
          </repository>
     </repositories>
     ```

4. Sous `<repositories>`, entrez hello production site URL et les informations utilisateur.
    Si vous utilisez le fournisseur d’appartenances Umbraco hello par défaut, puis ajouter des ID hello pour l’utilisateur d’Administration hello Bonjour &lt;utilisateur&gt; section.
    Si vous utilisez un fournisseur d’appartenances personnalisé Umbraco, utilisez `<login>`,`<password>` dans le site de production hello Courier2 module tooconnect toohello.
    Pour plus d’informations, [passez en revue la documentation hello pour le module de hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).

5. De même, installer le module de Courier2 hello sur votre site de production et configurer toopoint toohello étape web app dans son fichier courier.config respectifs, comme indiqué ici.

    ```xml
     <!-- Repository connection settings -->
     <!-- For each site, a custom repository must be configured, so Courier knows how tooconnect and authenticate-->
     <repositories>
        <!-- If a custom Umbraco Membership provider is used, specify login & password + set hello passwordEncoding tooclear: -->
        <repository name="Stage web app" alias="stage" type="CourierWebserviceRepositoryProvider" visible="true">
          <url>http://umbracositecms-1-stage.azurewebsites.net</url>
          <user>0</user>
          </repository>
     </repositories>
    ```

6. Cliquez sur hello **Courier2** onglet hello du tableau de bord Umbraco CMS web app, puis cliquez sur **emplacements**. Vous devez voir le nom de référentiel hello comme indiqué dans `courier.config`. Appliquez cette procédure à vos applications web de production et intermédiaire.

    ![Affichage du référentiel de l’application web](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. contenu toodeploy hello intermédiaire toohello production un site, accédez trop**contenu**et sélectionner une page existante ou créer une nouvelle page. Je vais sélectionner une page existante à partir de mon application web où titre hello de page de hello est **mise en route : nouvelles**, puis cliquez sur **enregistrer et publier**.

    ![Modification du titre de page et publication](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. Avec le bouton hello modifié tooview de page toutes les options de hello. Cliquez sur **Courier** tooopen hello **déploiement** boîte de dialogue. Cliquez sur **déployer** tooinitiate déploiement.

    ![Boîte de dialogue déploiement de module Courrier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. Passez en revue les modifications de hello, puis cliquez sur **continuer**.

    ![Passage en revue des modifications via la boîte de dialogue de déploiement du module Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    journal de déploiement Hello indique si le déploiement de hello a réussi.

     ![Affichage des journaux de déploiement du module Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. Parcourir vos toosee d’application de web production si les modifications de hello apparaissent.

     ![Accès à l’application web de production](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

toolearn plus en détail comment toouse expédition par courrier, révision hello documentation.

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a>Comment tooupgrade hello version de CMS Umbraco
Est de l’expédition par courrier aide pas de mise à niveau d’une version de CMS Umbraco tooanother. Lorsque vous mettez à niveau une version Umbraco CMS, vous devez vérifier les incompatibilités avec vos modules personnalisés ou des modules de partenaires et hello bibliothèques Umbraco principales. Voici les meilleures pratiques :

* Sauvegardez toujours votre application web et votre base de données avant de procéder une mise à niveau. Sur les applications web dans Azure, vous pouvez configurer des sauvegardes automatiques de vos sites Web à l’aide de la fonctionnalité de sauvegarde hello et restaurer votre site, si nécessaire à l’aide de la fonctionnalité de restauration hello. Pour plus d’informations, consultez [comment tooback votre application web](web-sites-backup.md) et [comment toorestore votre application web](web-sites-restore.md).
* Vérifiez si les packages à partir de partenaires sont compatibles avec la version hello vers que vous mettez à niveau. Page de téléchargement du package hello, passez en revue la compatibilité des projets avec la version de CMS Umbraco hello.

Pour plus d’informations sur la façon tooupgrade votre application web localement, [consultez les conseils de mise à niveau général hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).

Après la mise à niveau de votre site de développement local, publier hello toohello de modifications intermédiaires de l’application web. Testez votre application. Si tout semble correct, utilisez hello **échanger** bouton tooswap votre application de web site toohello production intermédiaire. Lorsque vous utilisez hello **échanger** opération, vous pouvez afficher les modifications de hello qui seront affectées dans la configuration de votre application web. Cela **échanger** opération échange hello des applications web et les bases de données. Après avoir hello **échanger**hello de base de données de production web application sera point toohello umbraco-étape-db et hello web application sera point tooumbraco-op-db base de données intermédiaire.

![Vue d’ensemble de l’échange pour le déploiement de CMS Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

Voici les avantages de l’échange hello web app et la base de données hello :

* Vous pouvez restaurer toohello la version précédente de votre application web avec un autre **échanger** s’il existe des problèmes d’application.
* Pour une mise à niveau, vous devez toodeploy fichiers et de bases de données à partir de hello web application toohello production d’applications web de mise en lots et de base de données. Beaucoup de choses peuvent aller de travers lorsque vous déployez des fichiers et des bases de données. À l’aide de hello **échanger** fonctionnalité d’emplacements, nous pouvons réduire les temps morts pendant une mise à niveau et réduire les risques de hello d’échecs qui peuvent se produire lorsque vous déployez des modifications.
* Vous pouvez effectuer **A / B test** à l’aide de hello [test en production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) fonctionnalité.

Cet exemple montre hello de souplesse de plate-forme hello vous permet de créer des modules personnalisés similaire tooUmbraco Courier toomanage du déploiement du module dans des environnements.

## <a name="references"></a>Références
[Développement logiciel agile avec Azure App Service](app-service-agile-software-development.md)

[Configurer des environnements intermédiaires pour les applications web dans Azure App Service](web-sites-staged-publishing.md)

[Comment accéder à des emplacements de déploiement en production toonon tooblock web](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
