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
# <a name="use-devops-environments-effectively-for-your-web-apps"></a><span data-ttu-id="a077e-103">Utiliser efficacement les environnements DevOps pour vos applications web</span><span class="sxs-lookup"><span data-stu-id="a077e-103">Use DevOps environments effectively for your web apps</span></span>
<span data-ttu-id="a077e-104">Cet article vous montre comment tooset configurer et gérer les déploiements d’applications web lorsque plusieurs versions de votre application se trouvent dans différents environnements, tels que le développement, intermédiaire, l’assurance qualité (AQ) et de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-104">This article shows you how tooset up and manage web application deployments when multiple versions of your application are in various environments, such as development, staging, quality assurance (QA), and production.</span></span> <span data-ttu-id="a077e-105">Chaque version de votre application peut être considérée comme un environnement de développement pour objectif spécifique de hello de votre processus de déploiement.</span><span class="sxs-lookup"><span data-stu-id="a077e-105">Each version of your application can be considered as a development environment for hello specific purpose of your deployment process.</span></span> <span data-ttu-id="a077e-106">Par exemple, les développeurs peuvent utiliser hello QA environnement tootest hello la qualité de l’application hello avant qu’ils push hello modifications tooproduction.</span><span class="sxs-lookup"><span data-stu-id="a077e-106">For example, developers can use hello QA environment tootest hello quality of hello application before they push hello changes tooproduction.</span></span>
<span data-ttu-id="a077e-107">Plusieurs environnements de développement peuvent être un défi, car vous devez tootrack code, de gérer les ressources (calcul, l’application web, base de données, du cache, etc.) et de déployer le code dans des environnements.</span><span class="sxs-lookup"><span data-stu-id="a077e-107">Multiple development environments can be a challenge because you need tootrack code, manage resources (compute, web app, database, cache, etc.), and deploy code across environments.</span></span>

## <a name="set-up-a-non-production-environment-stage-dev-qa"></a><span data-ttu-id="a077e-108">Configurer un environnement hors production (intermédiaire, développement, assurance qualité)</span><span class="sxs-lookup"><span data-stu-id="a077e-108">Set up a non-production environment (stage, dev, QA)</span></span>
<span data-ttu-id="a077e-109">Une fois une application web de production est en cours d’exécution, étape suivante de hello est toocreate un environnement hors production.</span><span class="sxs-lookup"><span data-stu-id="a077e-109">After a production web app is up and running, hello next step is toocreate a non-production environment.</span></span> <span data-ttu-id="a077e-110">toouse les emplacements de déploiement, assurez-vous que vous êtes en mode de plan Standard ou Premium du Service d’applications Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-110">toouse deployment slots, make sure that you are running in hello Standard or Premium Azure App Service plan mode.</span></span> <span data-ttu-id="a077e-111">Les emplacements de déploiement sont des applications web dynamiques qui ont leurs propres noms d’hôte.</span><span class="sxs-lookup"><span data-stu-id="a077e-111">Deployment slots are live web apps that have their own host names.</span></span> <span data-ttu-id="a077e-112">Éléments de configuration et de contenu Web application peuvent être échangés entre deux emplacements de déploiement, y compris l’emplacement de production hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-112">Web app content and configuration elements can be swapped between two deployment slots, including hello production slot.</span></span> <span data-ttu-id="a077e-113">Lorsque vous déployez votre emplacement de déploiement d’application tooa, vous obtenez hello avantages suivants :</span><span class="sxs-lookup"><span data-stu-id="a077e-113">When you deploy your application tooa deployment slot, you get hello following benefits:</span></span>

- <span data-ttu-id="a077e-114">Vous pouvez valider les modifications tooa web app dans un emplacement de déploiement intermédiaire avant d’échanger d’application hello avec l’emplacement de production hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-114">You can validate changes tooa web app in a staging deployment slot before you swap hello app with hello production slot.</span></span>
- <span data-ttu-id="a077e-115">Lorsque vous déployez d’abord un emplacement tooa d’application web et il échangez en production, toutes les instances de l’emplacement de hello sont préparées avant d’être permutés en production.</span><span class="sxs-lookup"><span data-stu-id="a077e-115">When you deploy a web app tooa slot first and swap it into production, all instances of hello slot are warmed up before being swapped into production.</span></span> <span data-ttu-id="a077e-116">Ce processus élimine les temps d’arrêt lorsque vous déployez votre application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-116">This process eliminates downtime when you deploy your web app.</span></span> <span data-ttu-id="a077e-117">redirection du trafic Hello est transparente, et aucune demande n’est supprimés en raison d’opérations de tooswap.</span><span class="sxs-lookup"><span data-stu-id="a077e-117">hello traffic redirection is seamless, and no requests are dropped due tooswap operations.</span></span> <span data-ttu-id="a077e-118">tooautomate ce flux de travail entière, configurer [échange automatique](web-sites-staged-publishing.md#configure-auto-swap) lorsque la validation préalable d’échange n’est pas nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-118">tooautomate this entire workflow, configure [Auto Swap](web-sites-staged-publishing.md#configure-auto-swap) when pre-swap validation is not needed.</span></span>
- <span data-ttu-id="a077e-119">Après un échange, d’emplacement hello qui possède désormais les hello précédemment préparé l’application web a hello précédente application web de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-119">After a swap, hello slot that has hello previously staged web app now has hello previous production web app.</span></span> <span data-ttu-id="a077e-120">Si les modifications de hello permutées dans l’emplacement de production hello sont pas comme prévu, vous pouvez effectuer hello même échange immédiatement tooget votre « dernière bonne configuration connue » arrière d’application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-120">If hello changes swapped into hello production slot are not as you expected, you can perform hello same swap immediately tooget your "last known good" web app back.</span></span>

<span data-ttu-id="a077e-121">tooset un emplacement de déploiement intermédiaire, consultez [configurer d’environnements intermédiaires pour applications web dans Azure App Service](web-sites-staged-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="a077e-121">tooset up a staging deployment slot, see [Set up staging environments for web apps in Azure App Service](web-sites-staged-publishing.md).</span></span> <span data-ttu-id="a077e-122">Chaque environnement doit inclure son propre jeu de ressources.</span><span class="sxs-lookup"><span data-stu-id="a077e-122">Every environment should include its own set of resources.</span></span> <span data-ttu-id="a077e-123">Par exemple, si votre application web utilise une base de données, les applications web intermédiaire et de production doivent utiliser différentes bases de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-123">For example, if your web app uses a database, then both production and staging web apps should use different databases.</span></span> <span data-ttu-id="a077e-124">Ajouter des ressources de l’environnement intermédiaire développement telles que la base de données, le stockage ou cache tooset votre environnement de développement intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-124">Add staging development environment resources such as database, storage, or cache tooset your staging development environment.</span></span>

## <a name="examples-of-using-multiple-development-environments"></a><span data-ttu-id="a077e-125">Exemples d’utilisation de plusieurs environnements de développement</span><span class="sxs-lookup"><span data-stu-id="a077e-125">Examples of using multiple development environments</span></span>
<span data-ttu-id="a077e-126">Un projet doit suivre la gestion du code source avec au moins deux environnements : développement et production.</span><span class="sxs-lookup"><span data-stu-id="a077e-126">Any project should follow source code management with at least two environments: development and production.</span></span> <span data-ttu-id="a077e-127">Si vous utilisez des systèmes de gestion de contenu (CMSs), les infrastructures d’applications, etc., application hello ne prenne pas en charge ce scénario sans personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a077e-127">If you use content management systems (CMSs), application frameworks, etc., hello application might not support this scenario without customization.</span></span> <span data-ttu-id="a077e-128">Cette éventualité a la valeur true pour certaines des infrastructures hello connues qui sont décrites dans les sections suivantes de hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-128">This eventuality is true for some of hello popular frameworks that are discussed in hello following sections.</span></span> <span data-ttu-id="a077e-129">Un grand nombre de questions proviennent toomind lorsque vous travaillez avec CMS/infrastructures, telles que :</span><span class="sxs-lookup"><span data-stu-id="a077e-129">Lots of questions come toomind when you work with CMS/frameworks, such as:</span></span>

- <span data-ttu-id="a077e-130">Comment vous décomposez le contenu hello dans différents environnements ?</span><span class="sxs-lookup"><span data-stu-id="a077e-130">How do you break hello content out into different environments?</span></span>
- <span data-ttu-id="a077e-131">Quels fichiers pouvez-vous modifier sans affecter les mises à jour des versions d’infrastructure ?</span><span class="sxs-lookup"><span data-stu-id="a077e-131">What files can you change without affecting framework version updates?</span></span>
- <span data-ttu-id="a077e-132">Comment gérez-vous les configurations par environnement ?</span><span class="sxs-lookup"><span data-stu-id="a077e-132">How do you manage configurations per environment?</span></span>
- <span data-ttu-id="a077e-133">Comment gérer les mises à jour de la version des modules, des plug-ins et infrastructure de base hello ?</span><span class="sxs-lookup"><span data-stu-id="a077e-133">How do you manage version updates for modules, plugins, and hello core framework?</span></span>

<span data-ttu-id="a077e-134">Il existe de nombreuses façons tooset, plusieurs environnements pour votre projet.</span><span class="sxs-lookup"><span data-stu-id="a077e-134">There are many ways tooset up multiple environments for your project.</span></span> <span data-ttu-id="a077e-135">Hello exemples suivants illustrent une méthode pour chaque application respectif.</span><span class="sxs-lookup"><span data-stu-id="a077e-135">hello following examples show one method for each respective application.</span></span>

### <a name="wordpress"></a><span data-ttu-id="a077e-136">WordPress</span><span class="sxs-lookup"><span data-stu-id="a077e-136">WordPress</span></span>
<span data-ttu-id="a077e-137">Dans cette section, vous allez apprendre comment tooset un workflow de déploiement à l’aide de connecteurs pour WordPress.</span><span class="sxs-lookup"><span data-stu-id="a077e-137">In this section, you will learn how tooset up a deployment workflow by using slots for WordPress.</span></span> <span data-ttu-id="a077e-138">WordPress, comme la plupart des solutions CMS, ne prend pas en charge l’utilisation de plusieurs environnements de développement sans personnalisation.</span><span class="sxs-lookup"><span data-stu-id="a077e-138">WordPress, like most CMS solutions, does not support multiple development environments without customization.</span></span> <span data-ttu-id="a077e-139">fonctionnalité des applications Web Hello du Service d’application Azure a quelques fonctionnalités qui la rendent facile toostore des paramètres de configuration à l’extérieur de votre code.</span><span class="sxs-lookup"><span data-stu-id="a077e-139">hello Web Apps feature of Azure App Service has a few features that make it easy toostore configuration settings outside your code.</span></span>

1. <span data-ttu-id="a077e-140">Avant de créer un emplacement intermédiaire, configurer votre toosupport de code d’application plusieurs environnements.</span><span class="sxs-lookup"><span data-stu-id="a077e-140">Before you create a staging slot, set up your application code toosupport multiple environments.</span></span> <span data-ttu-id="a077e-141">toosupport plusieurs environnements dans WordPress, vous devez tooedit `wp-config.php` sur votre développement local d’application web et ajouter hello suivant le code au début de hello du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-141">toosupport multiple environments in WordPress, you need tooedit `wp-config.php` on your local development web app and add hello following code at hello beginning of hello file.</span></span> <span data-ttu-id="a077e-142">Ce processus permettra toopick hello correct configuration de votre application en fonction de l’environnement sélectionné de hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-142">This process will enable your application toopick hello correct configuration based on hello selected environment.</span></span>

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

2. <span data-ttu-id="a077e-143">Créez un dossier sous la racine de l’application web appelée `config`et ajoutez hello `wp-config.azure.php` et `wp-config.local.php` les fichiers, qui représentent respectivement les votre environnement Azure et votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="a077e-143">Create a folder under web app root called `config`, and add hello `wp-config.azure.php` and `wp-config.local.php` files, which represent your Azure environment and local environment respectively.</span></span>

3. <span data-ttu-id="a077e-144">Copiez hello dans `wp-config.local.php`:</span><span class="sxs-lookup"><span data-stu-id="a077e-144">Copy hello following in `wp-config.local.php`:</span></span>

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

    <span data-ttu-id="a077e-145">Hello sécurité clés comme illustré dans le code précédent hello peut aider à tooprevent votre application web à partir de piratée, donc utiliser les valeurs uniques.</span><span class="sxs-lookup"><span data-stu-id="a077e-145">Setting hello security keys as illustrated in hello previous code can help tooprevent your web app from being hacked, so use unique values.</span></span> <span data-ttu-id="a077e-146">Si vous avez besoin de chaîne de hello toogenerate pour les clés de sécurité mentionnés dans le code hello, vous pouvez [générateur automatique de toohello accédez](https://api.wordpress.org/secret-key/1.1/salt) toocreate nouvelles paires clé/valeur.</span><span class="sxs-lookup"><span data-stu-id="a077e-146">If you need toogenerate hello string for security keys mentioned in hello code, you can [go toohello automatic generator](https://api.wordpress.org/secret-key/1.1/salt) toocreate new key/value pairs.</span></span>

4. <span data-ttu-id="a077e-147">Code copie hello suivant de `wp-config.azure.php`:</span><span class="sxs-lookup"><span data-stu-id="a077e-147">Copy hello following code in `wp-config.azure.php`:</span></span>

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

#### <a name="use-relative-paths"></a><span data-ttu-id="a077e-148">Utiliser des chemins relatifs</span><span class="sxs-lookup"><span data-stu-id="a077e-148">Use relative paths</span></span>
<span data-ttu-id="a077e-149">Une dernière tooconfigure de chose dans l’application de WordPress hello est chemins d’accès relatifs.</span><span class="sxs-lookup"><span data-stu-id="a077e-149">One last thing tooconfigure in hello WordPress app is relative paths.</span></span> <span data-ttu-id="a077e-150">WordPress stocke les informations de l’URL de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-150">WordPress stores URL information in hello database.</span></span> <span data-ttu-id="a077e-151">Ce stockage, le déplacement de contenu à partir d’un environnement tooanother plus difficile.</span><span class="sxs-lookup"><span data-stu-id="a077e-151">This storage makes moving content from one environment tooanother more difficult.</span></span> <span data-ttu-id="a077e-152">Vous avez besoin de base de données tooupdate hello chaque fois que vous déplacez toostage local ou les environnements tooproduction étape.</span><span class="sxs-lookup"><span data-stu-id="a077e-152">You need tooupdate hello database every time you move from local toostage or stage tooproduction environments.</span></span> <span data-ttu-id="a077e-153">risque de hello tooreduce des problèmes qui peut être dû au déploiement d’une base de données chaque fois que vous déployez à partir d’un environnement tooanother, utilisez hello [relatif racine lie le plug-in](https://wordpress.org/plugins/root-relative-urls/), que vous pouvez installer à l’aide de l’administrateur de WordPress hello tableau de bord.</span><span class="sxs-lookup"><span data-stu-id="a077e-153">tooreduce hello risk of issues that can be caused with deploying a database every time you deploy from one environment tooanother, use hello [Relative Root links plugin](https://wordpress.org/plugins/root-relative-urls/), which you can install by using hello WordPress administrator dashboard.</span></span>

<span data-ttu-id="a077e-154">Ajouter hello suivant entrées tooyour `wp-config.php` fichier avant hello `That's all, stop editing!` commentaire :</span><span class="sxs-lookup"><span data-stu-id="a077e-154">Add hello following entries tooyour `wp-config.php` file before hello `That's all, stop editing!` comment:</span></span>

```

  define('WP_HOME', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_SITEURL', 'http://'. filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
    define('WP_CONTENT_URL', '/wp-content');
    define('DOMAIN_CURRENT_SITE', filter_input(INPUT_SERVER, 'HTTP_HOST', FILTER_SANITIZE_STRING));
```

<span data-ttu-id="a077e-155">Activer le plug-in hello via hello `Plugins` menu dans le tableau de bord administrateur WordPress.</span><span class="sxs-lookup"><span data-stu-id="a077e-155">Activate hello plugin through hello `Plugins` menu in WordPress administrator dashboard.</span></span> <span data-ttu-id="a077e-156">Enregistrez les paramètres permalink pour l’application WordPress.</span><span class="sxs-lookup"><span data-stu-id="a077e-156">Save your permalink settings for WordPress app.</span></span>

#### <a name="hello-final-wp-configphp-file"></a><span data-ttu-id="a077e-157">Hello final `wp-config.php` fichier</span><span class="sxs-lookup"><span data-stu-id="a077e-157">hello final `wp-config.php` file</span></span>
<span data-ttu-id="a077e-158">Les mises à jour de WordPress n’affecteront pas vos fichiers `wp-config.php`, `wp-config.azure.php` et `wp-config.local.php`.</span><span class="sxs-lookup"><span data-stu-id="a077e-158">Any WordPress core updates will not affect your `wp-config.php`, `wp-config.azure.php`, and `wp-config.local.php` files.</span></span> <span data-ttu-id="a077e-159">Voici une version finale de hello `wp-config.php` fichier :</span><span class="sxs-lookup"><span data-stu-id="a077e-159">Here's a final version of hello `wp-config.php` file:</span></span>

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

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="a077e-160">Configuration d’un environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="a077e-160">Set up a staging environment</span></span>
1. <span data-ttu-id="a077e-161">Si vous disposez déjà d’une application web de WordPress en cours d’exécution sur votre abonnement Azure, connectez-vous à toohello [portail Azure](http://portal.azure.com), puis ouvrez l’application web tooyour WordPress.</span><span class="sxs-lookup"><span data-stu-id="a077e-161">If you already have a WordPress web app running on your Azure subscription, sign in toohello [Azure portal](http://portal.azure.com), and then go tooyour WordPress web app.</span></span> <span data-ttu-id="a077e-162">Si vous n’avez pas une application web de WordPress, vous pouvez créer un à partir de hello Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a077e-162">If you don't have a WordPress web app, you can create one from hello Azure Marketplace.</span></span> <span data-ttu-id="a077e-163">toolearn, voir [créer une application web de WordPress dans Azure App Service](web-sites-php-web-site-gallery.md).</span><span class="sxs-lookup"><span data-stu-id="a077e-163">toolearn more, see [Create a WordPress web app in Azure App Service](web-sites-php-web-site-gallery.md).</span></span>
<span data-ttu-id="a077e-164">Cliquez sur **paramètres** > **les emplacements de déploiement** > **ajouter** toocreate un emplacement de déploiement avec le nom de hello *étape*.</span><span class="sxs-lookup"><span data-stu-id="a077e-164">Click **Settings** > **Deployment slots** > **Add** toocreate a deployment slot with hello name *stage*.</span></span> <span data-ttu-id="a077e-165">Un emplacement de déploiement est une autre application web parts hello autant de ressources que l’application hello web principal que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="a077e-165">A deployment slot is another web application that shares hello same resources as hello primary web app that you created previously.</span></span>

    ![Créer un emplacement de déploiement intermédiaire](./media/app-service-web-staged-publishing-realworld-scenarios/1setupstage.png)

2. <span data-ttu-id="a077e-167">Ajouter une autre base de données MySQL, par exemple `wordpress-stage-db`, groupe de ressources tooyour `wordpressapp-group`.</span><span class="sxs-lookup"><span data-stu-id="a077e-167">Add another MySQL database, say `wordpress-stage-db`, tooyour resource group, `wordpressapp-group`.</span></span>

    ![Ajouter le groupe de tooresource de base de données MySQL](./media/app-service-web-staged-publishing-realworld-scenarios/2addmysql.png)

3. <span data-ttu-id="a077e-169">Mettre à jour les chaînes de connexion de hello pour votre scène déploiement emplacement toopoint toohello nouvelle base de données, `wordpress-stage-db`.</span><span class="sxs-lookup"><span data-stu-id="a077e-169">Update hello connection strings for your stage deployment slot toopoint toohello new database, `wordpress-stage-db`.</span></span> <span data-ttu-id="a077e-170">Votre application web de production, `wordpressprodapp`et de l’application web, de mise en lots `wordpressprodapp-stage`, bases de données doit toodifferent de point.</span><span class="sxs-lookup"><span data-stu-id="a077e-170">Your production web app, `wordpressprodapp`, and staging web app, `wordpressprodapp-stage`, must point toodifferent databases.</span></span>

#### <a name="configure-environment-specific-app-settings"></a><span data-ttu-id="a077e-171">Configurer les paramètres d’application spécifiques à l’environnement</span><span class="sxs-lookup"><span data-stu-id="a077e-171">Configure environment-specific app settings</span></span>
<span data-ttu-id="a077e-172">Les développeurs peuvent stocker des paires clé/valeur des chaînes dans Azure en tant que partie des informations de configuration hello, appelées **paramètres de l’application**, qui est associé à une application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-172">Developers can store key/value string pairs in Azure as part of hello configuration information, called **App Settings**, that's associated with a web app.</span></span> <span data-ttu-id="a077e-173">Lors de l’exécution, les applications web automatiquement récupérer ces valeurs et les rendre disponible toocode qui s’exécute dans votre application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-173">At runtime, web apps automatically retrieve these values and make them available toocode that's running in your web app.</span></span> <span data-ttu-id="a077e-174">Du point de vue de la sécurité, c’est un avantage car les informations sensibles comme les chaînes de connexion à une base de données qui incluent des mots de passe, ne sont jamais affichées en clair dans un fichier tel que `wp-config.php`.</span><span class="sxs-lookup"><span data-stu-id="a077e-174">From a security perspective, that is a nice side benefit because sensitive information, such as database connection strings that include passwords, never show up as clear text in a file such as `wp-config.php`.</span></span>

<span data-ttu-id="a077e-175">Ce processus, qui est expliqué dans hello après les paragraphes, est utile, car il inclut des modifications de fichiers et les modifications de base de données pour l’application de WordPress hello :</span><span class="sxs-lookup"><span data-stu-id="a077e-175">This process, which is explained in hello following paragraphs, is useful because it includes both file changes and database changes for hello WordPress app:</span></span>

* <span data-ttu-id="a077e-176">Mise à jour de la version de WordPress</span><span class="sxs-lookup"><span data-stu-id="a077e-176">WordPress version upgrade</span></span>
* <span data-ttu-id="a077e-177">Ajout, modification ou mise à jour de modules complémentaires</span><span class="sxs-lookup"><span data-stu-id="a077e-177">Add new or edit or upgrade plugins</span></span>
* <span data-ttu-id="a077e-178">Ajout, modification ou mise à jour des thèmes</span><span class="sxs-lookup"><span data-stu-id="a077e-178">Add new or edit or upgrade themes</span></span>

<span data-ttu-id="a077e-179">Configuration des paramètres d’application pour :</span><span class="sxs-lookup"><span data-stu-id="a077e-179">Configure app settings for:</span></span>

* <span data-ttu-id="a077e-180">les informations de base de données</span><span class="sxs-lookup"><span data-stu-id="a077e-180">Database information</span></span>
* <span data-ttu-id="a077e-181">l’activation/la désactivation de la journalisation WordPress</span><span class="sxs-lookup"><span data-stu-id="a077e-181">Turning on/off WordPress logging</span></span>
* <span data-ttu-id="a077e-182">Paramètres de sécurité WordPress</span><span class="sxs-lookup"><span data-stu-id="a077e-182">WordPress security settings</span></span>

![Paramètres de l’application pour l’application web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/3configure.png)

<span data-ttu-id="a077e-184">Assurez-vous que vous ajoutez hello suivant les paramètres de l’application pour votre web app et l’étape de l’emplacement de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-184">Make sure that you add hello following app settings for your production web app and stage slot.</span></span> <span data-ttu-id="a077e-185">Notez que l’application web de production hello et l’application web intermédiaire utilisant différentes bases de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-185">Note that hello production web app and staging web app use different databases.</span></span>

1. <span data-ttu-id="a077e-186">Désactivez hello **paramètre d’emplacement** case à cocher pour tous les paramètres de paramètres hello sauf WP_ENV.</span><span class="sxs-lookup"><span data-stu-id="a077e-186">Clear hello **Slot Setting** checkbox for all hello settings parameters except WP_ENV.</span></span> <span data-ttu-id="a077e-187">Ce processus échangera les configuration hello pour votre application web, le contenu du fichier et la base de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-187">This process will swap hello configuration for your web app, file content, and database.</span></span> <span data-ttu-id="a077e-188">Si **paramètre d’emplacement** est vérifié, paramètres de l’application et la configuration de chaîne de connexion de l’application hello web seront *pas* déplacer entre les environnements lors de l’exécution une **échanger** opération.</span><span class="sxs-lookup"><span data-stu-id="a077e-188">If **Slot Setting** is checked, hello web app’s app settings and connection string configuration will *not* move across environments when doing a **Swap** operation.</span></span> <span data-ttu-id="a077e-189">Les modifications apportées à la base de données ne bloqueront pas votre application web de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-189">Any database changes that are present will not break your production web app.</span></span>

2. <span data-ttu-id="a077e-190">Déployer hello développement local environnement web application toohello étape web d’applications et de la base de données à l’aide de WebMatrix ou les outils de votre choix, tels que FTP, Git ou PhpMyAdmin.</span><span class="sxs-lookup"><span data-stu-id="a077e-190">Deploy hello local development environment web app toohello stage web app and database by using WebMatrix or tools of your choice, such as FTP, Git, or PhpMyAdmin.</span></span>

    ![Boîte de dialogue de publication de Matrix pour l’application web WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/4wmpublish.png)

3. <span data-ttu-id="a077e-192">Parcourir et tester votre application web intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-192">Browse and test your staging web app.</span></span> <span data-ttu-id="a077e-193">Compte tenu d’un scénario dans lequel le thème de l’application web hello hello est toobe mis à jour, voici hello intermédiaires de l’application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-193">Considering a scenario where hello theme of hello web app is toobe updated, here is hello staging web app.</span></span>

    ![Parcourir l’application web intermédiaire avant d’échanger les emplacements](./media/app-service-web-staged-publishing-realworld-scenarios/5wpstage.png)

4. <span data-ttu-id="a077e-195">Si tout semble correct, cliquez sur hello **échanger** bouton sur votre zone de transit toomove d’application web de votre environnement de production toohello contenu.</span><span class="sxs-lookup"><span data-stu-id="a077e-195">If all looks good, click hello **Swap** button on your staging web app toomove your content toohello production environment.</span></span> <span data-ttu-id="a077e-196">Dans ce cas, remplacez hello web app et la base de données hello dans des environnements pendant chaque **Swap** opération.</span><span class="sxs-lookup"><span data-stu-id="a077e-196">In this case, you swap hello web app and hello database across environments during every **Swap** operation.</span></span>

    ![Échanger les modifications de l’aperçu pour WordPress](./media/app-service-web-staged-publishing-realworld-scenarios/6swaps1.png)

    > [!NOTE]
    > <span data-ttu-id="a077e-198">Si votre scénario doit diffuser les fichiers tooonly (aucune mise à jour de base de données), puis vérifiez **paramètre d’emplacement** pour tous les hello liés à la base de données *paramètres de l’application* et *deparamètresdechaînesdeconnexion*Bonjour **paramètres de l’application Web** panneau dans hello portail Azure avant de procéder à hello **échanger**.</span><span class="sxs-lookup"><span data-stu-id="a077e-198">If your scenario needs tooonly push files (no database updates), then check **Slot Setting** for all hello database-related *app settings* and *connection strings settings* in hello **Web App Settings** blade within hello Azure portal before doing hello **Swap**.</span></span> <span data-ttu-id="a077e-199">Dans ce cas, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER et les paramètres de la chaîne de connexion par défaut ne s’affichent pas dans les modifications de présentation lors de l’**échange**.</span><span class="sxs-lookup"><span data-stu-id="a077e-199">In this case, DB_NAME, DB_HOST, DB_PASSWORD, DB_USER, and default connection string settings should not show up in preview changes when you do a **Swap**.</span></span> <span data-ttu-id="a077e-200">À ce stade, quand vous terminez hello **échanger** opération, hello WordPress l’application web sera ont hello met à jour uniquement les fichiers.</span><span class="sxs-lookup"><span data-stu-id="a077e-200">At this time, when you complete hello **Swap** operation, hello WordPress web app will have hello updates files only.</span></span>
    >
    >

    <span data-ttu-id="a077e-201">Avant cela, une **échanger**, voici hello production WordPress web app.</span><span class="sxs-lookup"><span data-stu-id="a077e-201">Before doing a **Swap**, here is hello production WordPress web app.</span></span>
    <span data-ttu-id="a077e-202">![Application web de production avant l’échange d’emplacements](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span><span class="sxs-lookup"><span data-stu-id="a077e-202">![Production web app before swapping slots](./media/app-service-web-staged-publishing-realworld-scenarios/7bfswap.png)</span></span>

    <span data-ttu-id="a077e-203">Après avoir hello **échanger** opération, le thème hello a été mis à jour sur votre application web de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-203">After hello **Swap** operation, hello theme has been updated on your production web app.</span></span>

    ![Application web de production après l’échange d’emplacements](./media/app-service-web-staged-publishing-realworld-scenarios/8afswap.png)

5. <span data-ttu-id="a077e-205">Lorsque vous devez tooroll précédent, vous pouvez accéder à web de production toohello **paramètres de l’application**, puis cliquez sur hello **échanger** bouton tooswap hello web app et la base de données à partir de l’emplacement de production toostaging.</span><span class="sxs-lookup"><span data-stu-id="a077e-205">When you need tooroll back, you can go toohello production web **App Settings**, and click hello **Swap** button tooswap hello web app and database from production toostaging slot.</span></span> <span data-ttu-id="a077e-206">N’oubliez pas que si les modifications de base de données sont incluses dans un **échanger** opération, puis hello prochaine fois que vous déployez tooyour intermédiaires de l’application web, vous devez toodeploy hello modifications toohello actuelle base de données pour votre application web intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-206">Remember that if database changes are included with a **Swap** operation, then hello next time you deploy tooyour staging web app, you need toodeploy hello database changes toohello current database for your staging web app.</span></span> <span data-ttu-id="a077e-207">base de données actuelle Hello peut être la base de données de production précédent hello ou étape hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-207">hello current database might be hello previous production database or hello stage database.</span></span>

#### <a name="summary"></a><span data-ttu-id="a077e-208">Résumé</span><span class="sxs-lookup"><span data-stu-id="a077e-208">Summary</span></span>
<span data-ttu-id="a077e-209">Voici un processus générique pour une application qui possède une base de données :</span><span class="sxs-lookup"><span data-stu-id="a077e-209">Following is a generalized process for any application that has a database:</span></span>

1. <span data-ttu-id="a077e-210">Installer l’application hello sur votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="a077e-210">Install hello application on your local environment.</span></span>
2. <span data-ttu-id="a077e-211">Incluez les configurations propres à l’environnement (local et Azure Web Apps).</span><span class="sxs-lookup"><span data-stu-id="a077e-211">Include environment-specific configurations (local and Azure Web Apps).</span></span>
3. <span data-ttu-id="a077e-212">Configurez vos environnements intermédiaire et de production pour Web Apps.</span><span class="sxs-lookup"><span data-stu-id="a077e-212">Set up your staging and production environments for Web Apps.</span></span>
4. <span data-ttu-id="a077e-213">Si vous avez une application de production en cours d’exécution sur Azure, synchroniser votre contenu (fichiers/code et la base de données) toolocal et mise en lots environnements de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-213">If you have a production application already running on Azure, sync your production content (files/code and database) toolocal and staging environments.</span></span>
5. <span data-ttu-id="a077e-214">Développez votre application sur votre environnement local.</span><span class="sxs-lookup"><span data-stu-id="a077e-214">Develop your application on your local environment.</span></span>
6. <span data-ttu-id="a077e-215">Placez votre application web de production en maintenance ou en mode verrouillé et synchroniser le contenu de la base de données à partir d’environnements de production toostaging et de développement.</span><span class="sxs-lookup"><span data-stu-id="a077e-215">Place your production web app under maintenance or locked mode, and sync database content from production toostaging and dev environments.</span></span>
7. <span data-ttu-id="a077e-216">Déployer toohello environnement et test de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="a077e-216">Deploy toohello staging environment and test.</span></span>
8. <span data-ttu-id="a077e-217">Déployer un environnement de tooproduction.</span><span class="sxs-lookup"><span data-stu-id="a077e-217">Deploy tooproduction environment.</span></span>
9. <span data-ttu-id="a077e-218">Répétez les étapes 4 à 6.</span><span class="sxs-lookup"><span data-stu-id="a077e-218">Repeat steps 4 through 6.</span></span>

### <a name="umbraco"></a><span data-ttu-id="a077e-219">Umbraco</span><span class="sxs-lookup"><span data-stu-id="a077e-219">Umbraco</span></span>
<span data-ttu-id="a077e-220">Dans cette section, vous allez apprendre comment hello CMS Umbraco utilise un toodeploy module personnalisé dans plusieurs environnements de DevOps.</span><span class="sxs-lookup"><span data-stu-id="a077e-220">In this section, you will learn how hello Umbraco CMS uses a custom module toodeploy across multiple DevOps environments.</span></span> <span data-ttu-id="a077e-221">Cet exemple fournit une approche différente de toomanaging plusieurs environnements de développement.</span><span class="sxs-lookup"><span data-stu-id="a077e-221">This example provides a different approach toomanaging multiple development environments.</span></span>

<span data-ttu-id="a077e-222">[Umbraco CMS](http://umbraco.com/) est une solution de CMS .NET prisée de nombreux développeurs.</span><span class="sxs-lookup"><span data-stu-id="a077e-222">[Umbraco CMS](http://umbraco.com/) is a popular .NET CMS solution that's used by many developers.</span></span> <span data-ttu-id="a077e-223">Il fournit hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) toodeploy de module à partir d’environnements de développement toostaging tooproduction.</span><span class="sxs-lookup"><span data-stu-id="a077e-223">It provides hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module toodeploy from development toostaging tooproduction environments.</span></span> <span data-ttu-id="a077e-224">Vous pouvez facilement créer un environnement de développement local pour une application web Umbraco CMS à l’aide de Visual Studio ou de WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a077e-224">You can easily create a local development environment for an Umbraco CMS web app by using Visual Studio or WebMatrix.</span></span>

- [<span data-ttu-id="a077e-225">Créer une application web Umbraco avec Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a077e-225">Create an Umbraco web app with Visual Studio</span></span>](https://our.umbraco.org/documentation/Installation/install-umbraco-with-nuget)
- [<span data-ttu-id="a077e-226">Créer une application web Umbraco avec WebMatrix</span><span class="sxs-lookup"><span data-stu-id="a077e-226">Create an Umbraco web app with WebMatrix</span></span>](http://umbraco.tv/videos/umbraco-v7/implementor/fundamentals/installation/creating-umbraco-site-from-webmatrix-web-gallery/)

<span data-ttu-id="a077e-227">N’oubliez pas tooremove hello `install` dossier sous votre application et ne jamais télécharger des applications web toostage ou de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-227">Always remember tooremove hello `install` folder under your application, and never upload it toostage or production web apps.</span></span> <span data-ttu-id="a077e-228">Ce didacticiel utilise WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a077e-228">This tutorial uses WebMatrix.</span></span>

#### <a name="set-up-a-staging-environment"></a><span data-ttu-id="a077e-229">Configuration d’un environnement intermédiaire</span><span class="sxs-lookup"><span data-stu-id="a077e-229">Set up a staging environment</span></span>
1. <span data-ttu-id="a077e-230">Créer un emplacement de déploiement, comme mentionné précédemment pour hello Umbraco CMS web app, si que vous disposez déjà d’une application web de CMS Umbraco et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a077e-230">Create a deployment slot as mentioned previously for hello Umbraco CMS web app, assuming you already have an Umbraco CMS web app up and running.</span></span> <span data-ttu-id="a077e-231">Si vous ne le faites pas, vous pouvez créer un à partir de hello Marketplace.</span><span class="sxs-lookup"><span data-stu-id="a077e-231">If you do not, you can create one from hello Marketplace.</span></span>
2. <span data-ttu-id="a077e-232">Mettre à jour la chaîne de connexion hello pour votre toohello de toopoint étape déploiement emplacement nouveau **umbraco-étape-db** base de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-232">Update hello connection string for your stage deployment slot toopoint toohello new **umbraco-stage-db** database.</span></span> <span data-ttu-id="a077e-233">Votre application web de production (umbraositecms-1) et l’application web intermédiaire (umbracositecms-1-étape) *doit* toodifferent de point de bases de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-233">Your production web app (umbraositecms-1) and staging web app (umbracositecms-1-stage) *must* point toodifferent databases.</span></span>

    ![Mettre à jour la chaîne de connexion pour l’application web intermédiaire vers une nouvelle base de données intermédiaire](./media/app-service-web-staged-publishing-realworld-scenarios/9umbconnstr.png)

3. <span data-ttu-id="a077e-235">Cliquez sur **obtenir publier les paramètres** pour l’emplacement de déploiement hello **étape**.</span><span class="sxs-lookup"><span data-stu-id="a077e-235">Click **Get Publish settings** for hello deployment slot **stage**.</span></span> <span data-ttu-id="a077e-236">Ce processus télécharge un fichier de paramètres de publication qui stocke toutes les informations de hello que Visual Studio ou WebMatrix, toopublish votre application à partir de l’application web Azure hello développement local web application toohello.</span><span class="sxs-lookup"><span data-stu-id="a077e-236">This process will download a publish settings file that stores all hello information that Visual Studio or WebMatrix requires toopublish your application from hello local development web app toohello Azure web app.</span></span>

    ![Obtenir le paramètre de hello intermédiaires de l’application web de publication](./media/app-service-web-staged-publishing-realworld-scenarios/10getpsetting.png)
4. <span data-ttu-id="a077e-238">Ouvrez votre application web de développement locale dans WebMatrix ou Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a077e-238">Open your local development web app in WebMatrix or Visual Studio.</span></span> <span data-ttu-id="a077e-239">Ce didacticiel utilise WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="a077e-239">This tutorial uses WebMatrix.</span></span> <span data-ttu-id="a077e-240">Tout d’abord, vous devez tooimport hello publier le fichier de paramètres pour votre application web intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-240">First, you need tooimport hello publish settings file for your staging web app.</span></span>

    ![Importer les paramètres de publication d’Umbraco à l’aide de Web Matrix](./media/app-service-web-staged-publishing-realworld-scenarios/11import.png)

5. <span data-ttu-id="a077e-242">Passez en revue les modifications dans la boîte de dialogue hello et déployer votre application web locale application tooyour web Azure, *umbracositecms-1-étape*.</span><span class="sxs-lookup"><span data-stu-id="a077e-242">Review changes in hello dialog box, and deploy your local web app tooyour Azure web app, *umbracositecms-1-stage*.</span></span> <span data-ttu-id="a077e-243">Lorsque vous déployez des fichiers directement tooyour intermédiaire web app, vous serez omettre les fichiers Bonjour `~/app_data/TEMP/` dossier, car ces fichiers seront régénérés lors de l’application web hello étape a démarré.</span><span class="sxs-lookup"><span data-stu-id="a077e-243">When you deploy files directly tooyour staging web app, you will omit files in hello `~/app_data/TEMP/` folder because these files will be regenerated when hello stage web app is first started.</span></span> <span data-ttu-id="a077e-244">Vous devez également omettre hello `~/app_data/umbraco.config` fichier, qui sera également régénéré.</span><span class="sxs-lookup"><span data-stu-id="a077e-244">You should also omit hello `~/app_data/umbraco.config` file, which will also be regenerated.</span></span>

    ![Passer en revue les modifications de publication dans une matrice web](./media/app-service-web-staged-publishing-realworld-scenarios/12umbpublish.png)

6. <span data-ttu-id="a077e-246">Après avoir publié correctement hello Umbraco local web application toohello intermédiaire web app, parcourir l’application web de la zone de transit tooyour et exécuter quelques tests toorule, tous les points.</span><span class="sxs-lookup"><span data-stu-id="a077e-246">After you successfully publish hello Umbraco local web app toohello staging web app, browse tooyour staging web app, and run a few tests toorule out any issues.</span></span>

#### <a name="set-up-hello-courier2-deployment-module"></a><span data-ttu-id="a077e-247">Configurer le module de déploiement hello Courier2</span><span class="sxs-lookup"><span data-stu-id="a077e-247">Set up hello Courier2 deployment module</span></span>
<span data-ttu-id="a077e-248">Avec hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, vous pouvez simplement avec le bouton droit toopush contenu, les feuilles de style et les modules de développement à partir d’une site web application tooa application web de production.</span><span class="sxs-lookup"><span data-stu-id="a077e-248">With hello [Courier2](http://umbraco.com/products/more-add-ons/courier-2) module, you can simply right-click toopush content, style sheets, and development modules from a staging web app tooa production web app.</span></span> <span data-ttu-id="a077e-249">Ce processus réduit les risques de hello de rupture de votre application web de production lorsque vous déployez une mise à jour.</span><span class="sxs-lookup"><span data-stu-id="a077e-249">This process reduces hello risk of breaking your production web app when you deploy an update.</span></span>
<span data-ttu-id="a077e-250">Acheter une licence pour Courier2 hello `*.azurewebsites.net` domaine et votre domaine personnalisé (par exemple http://abc.com).</span><span class="sxs-lookup"><span data-stu-id="a077e-250">Purchase a license for Courier2 for hello `*.azurewebsites.net` domain and your custom domain (say http://abc.com).</span></span> <span data-ttu-id="a077e-251">Après l’achat de licence de hello, place hello téléchargé licence (. Fichier LIC) Bonjour `bin` dossier.</span><span class="sxs-lookup"><span data-stu-id="a077e-251">After you purchase hello license, place hello downloaded license (.LIC file) in hello `bin` folder.</span></span>

![Placer un fichier de licence sous un dossier bin](./media/app-service-web-staged-publishing-realworld-scenarios/13droplic.png)

1. <span data-ttu-id="a077e-253">[Télécharger le package de hello Courier2](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span><span class="sxs-lookup"><span data-stu-id="a077e-253">[Download hello Courier2 package](https://our.umbraco.org/projects/umbraco-pro/umbraco-courier-2/).</span></span> <span data-ttu-id="a077e-254">Signe dans tooyour étape web app, par exemple http://umbracocms-site-stage.azurewebsites.net/umbraco, cliquez sur hello **Developer** menu, puis sur **Packages** > **installer package local**.</span><span class="sxs-lookup"><span data-stu-id="a077e-254">Sign in tooyour stage web app, say http://umbracocms-site-stage.azurewebsites.net/umbraco, click hello **Developer** menu, and then click **Packages** > **Install local package**.</span></span>

    ![Programme d’installation de Umbraco Package](./media/app-service-web-staged-publishing-realworld-scenarios/14umbpkg.png)

2. <span data-ttu-id="a077e-256">Télécharger le package de hello Courier2 à l’aide du programme d’installation hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-256">Upload hello Courier2 package by using hello installer.</span></span>

    ![Téléchargement du package du module courier](./media/app-service-web-staged-publishing-realworld-scenarios/15umbloadpkg.png)

3. <span data-ttu-id="a077e-258">package de hello tooconfigure, vous devez fichier courier.config tooupdate hello hello **Config** dossier de votre application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-258">tooconfigure hello package, you need tooupdate hello courier.config file under hello **Config** folder of your web app.</span></span>

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

4. <span data-ttu-id="a077e-259">Sous `<repositories>`, entrez hello production site URL et les informations utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a077e-259">Under `<repositories>`, enter hello production site URL and user information.</span></span>
    <span data-ttu-id="a077e-260">Si vous utilisez le fournisseur d’appartenances Umbraco hello par défaut, puis ajouter des ID hello pour l’utilisateur d’Administration hello Bonjour &lt;utilisateur&gt; section.</span><span class="sxs-lookup"><span data-stu-id="a077e-260">If you are using hello default Umbraco membership provider, then add hello ID for hello Administration user in hello &lt;user&gt; section.</span></span>
    <span data-ttu-id="a077e-261">Si vous utilisez un fournisseur d’appartenances personnalisé Umbraco, utilisez `<login>`,`<password>` dans le site de production hello Courier2 module tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="a077e-261">If you are using a custom Umbraco membership provider, use `<login>`,`<password>` in hello Courier2 module tooconnect toohello production site.</span></span>
    <span data-ttu-id="a077e-262">Pour plus d’informations, [passez en revue la documentation hello pour le module de hello Courier2](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span><span class="sxs-lookup"><span data-stu-id="a077e-262">For more details, [review hello documentation for hello Courier2 module](http://umbraco.com/help-and-support/customer-area/courier-2-support-and-download/developer-documentation).</span></span>

5. <span data-ttu-id="a077e-263">De même, installer le module de Courier2 hello sur votre site de production et configurer toopoint toohello étape web app dans son fichier courier.config respectifs, comme indiqué ici.</span><span class="sxs-lookup"><span data-stu-id="a077e-263">Similarly, install hello Courier2 module on your production site, and configure it toopoint toohello stage web app in its respective courier.config file as shown here.</span></span>

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

6. <span data-ttu-id="a077e-264">Cliquez sur hello **Courier2** onglet hello du tableau de bord Umbraco CMS web app, puis cliquez sur **emplacements**.</span><span class="sxs-lookup"><span data-stu-id="a077e-264">Click hello **Courier2** tab in hello Umbraco CMS web app dashboard, and then click **Locations**.</span></span> <span data-ttu-id="a077e-265">Vous devez voir le nom de référentiel hello comme indiqué dans `courier.config`.</span><span class="sxs-lookup"><span data-stu-id="a077e-265">You should see hello repository name as mentioned in `courier.config`.</span></span> <span data-ttu-id="a077e-266">Appliquez cette procédure à vos applications web de production et intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-266">Do this process on both your production and staging web apps.</span></span>

    ![Affichage du référentiel de l’application web](./media/app-service-web-staged-publishing-realworld-scenarios/16courierloc.png)

7. <span data-ttu-id="a077e-268">contenu toodeploy hello intermédiaire toohello production un site, accédez trop**contenu**et sélectionner une page existante ou créer une nouvelle page.</span><span class="sxs-lookup"><span data-stu-id="a077e-268">toodeploy content from hello staging site toohello production site, go too**Content**, and select an existing page or create a new page.</span></span> <span data-ttu-id="a077e-269">Je vais sélectionner une page existante à partir de mon application web où titre hello de page de hello est **mise en route : nouvelles**, puis cliquez sur **enregistrer et publier**.</span><span class="sxs-lookup"><span data-stu-id="a077e-269">I will select an existing page from my web app where hello title of hello page is **Getting Started – new**, and then click **Save and Publish**.</span></span>

    ![Modification du titre de page et publication](./media/app-service-web-staged-publishing-realworld-scenarios/17changepg.png)

8. <span data-ttu-id="a077e-271">Avec le bouton hello modifié tooview de page toutes les options de hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-271">Right-click hello modified page tooview all hello options.</span></span> <span data-ttu-id="a077e-272">Cliquez sur **Courier** tooopen hello **déploiement** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="a077e-272">Click **Courier** tooopen hello **Deployment** dialog box.</span></span> <span data-ttu-id="a077e-273">Cliquez sur **déployer** tooinitiate déploiement.</span><span class="sxs-lookup"><span data-stu-id="a077e-273">Click **Deploy** tooinitiate deployment.</span></span>

    ![Boîte de dialogue déploiement de module Courrier](./media/app-service-web-staged-publishing-realworld-scenarios/18dialog1.png)

9. <span data-ttu-id="a077e-275">Passez en revue les modifications de hello, puis cliquez sur **continuer**.</span><span class="sxs-lookup"><span data-stu-id="a077e-275">Review hello changes, and then click **Continue**.</span></span>

    ![Passage en revue des modifications via la boîte de dialogue de déploiement du module Courier](./media/app-service-web-staged-publishing-realworld-scenarios/19dialog2.png)

    <span data-ttu-id="a077e-277">journal de déploiement Hello indique si le déploiement de hello a réussi.</span><span class="sxs-lookup"><span data-stu-id="a077e-277">hello deployment log shows if hello deployment was successful.</span></span>

     ![Affichage des journaux de déploiement du module Courier](./media/app-service-web-staged-publishing-realworld-scenarios/20successdlg.png)

10. <span data-ttu-id="a077e-279">Parcourir vos toosee d’application de web production si les modifications de hello apparaissent.</span><span class="sxs-lookup"><span data-stu-id="a077e-279">Browse your production web app toosee if hello changes are reflected.</span></span>

     ![Accès à l’application web de production](./media/app-service-web-staged-publishing-realworld-scenarios/21umbpg.png)

<span data-ttu-id="a077e-281">toolearn plus en détail comment toouse expédition par courrier, révision hello documentation.</span><span class="sxs-lookup"><span data-stu-id="a077e-281">toolearn more about how toouse Courier, review hello documentation.</span></span>

#### <a name="how-tooupgrade-hello-umbraco-cms-version"></a><span data-ttu-id="a077e-282">Comment tooupgrade hello version de CMS Umbraco</span><span class="sxs-lookup"><span data-stu-id="a077e-282">How tooupgrade hello Umbraco CMS version</span></span>
<span data-ttu-id="a077e-283">Est de l’expédition par courrier aide pas de mise à niveau d’une version de CMS Umbraco tooanother.</span><span class="sxs-lookup"><span data-stu-id="a077e-283">Courier will not help you upgrade from one version of Umbraco CMS tooanother.</span></span> <span data-ttu-id="a077e-284">Lorsque vous mettez à niveau une version Umbraco CMS, vous devez vérifier les incompatibilités avec vos modules personnalisés ou des modules de partenaires et hello bibliothèques Umbraco principales.</span><span class="sxs-lookup"><span data-stu-id="a077e-284">When you upgrade an Umbraco CMS version, you must check for incompatibilities with your custom modules or modules from partners and hello Umbraco Core libraries.</span></span> <span data-ttu-id="a077e-285">Voici les meilleures pratiques :</span><span class="sxs-lookup"><span data-stu-id="a077e-285">Here are best practices:</span></span>

* <span data-ttu-id="a077e-286">Sauvegardez toujours votre application web et votre base de données avant de procéder une mise à niveau.</span><span class="sxs-lookup"><span data-stu-id="a077e-286">Always back up your web app and database before you upgrade.</span></span> <span data-ttu-id="a077e-287">Sur les applications web dans Azure, vous pouvez configurer des sauvegardes automatiques de vos sites Web à l’aide de la fonctionnalité de sauvegarde hello et restaurer votre site, si nécessaire à l’aide de la fonctionnalité de restauration hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-287">On web apps in Azure, you can set up automatic backups for your websites by using hello backup feature and restore your site if needed by using hello restore feature.</span></span> <span data-ttu-id="a077e-288">Pour plus d’informations, consultez [comment tooback votre application web](web-sites-backup.md) et [comment toorestore votre application web](web-sites-restore.md).</span><span class="sxs-lookup"><span data-stu-id="a077e-288">For more details, see [How tooback up your web app](web-sites-backup.md) and [How toorestore your web app](web-sites-restore.md).</span></span>
* <span data-ttu-id="a077e-289">Vérifiez si les packages à partir de partenaires sont compatibles avec la version hello vers que vous mettez à niveau.</span><span class="sxs-lookup"><span data-stu-id="a077e-289">Check if packages from partners are compatible with hello version you're upgrading to.</span></span> <span data-ttu-id="a077e-290">Page de téléchargement du package hello, passez en revue la compatibilité des projets avec la version de CMS Umbraco hello.</span><span class="sxs-lookup"><span data-stu-id="a077e-290">On hello package's download page, review hello project compatibility with Umbraco CMS version.</span></span>

<span data-ttu-id="a077e-291">Pour plus d’informations sur la façon tooupgrade votre application web localement, [consultez les conseils de mise à niveau général hello](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span><span class="sxs-lookup"><span data-stu-id="a077e-291">For more details about how tooupgrade your web app locally, [see hello general upgrade guidance](https://our.umbraco.org/documentation/getting-started/setup/upgrading/general).</span></span>

<span data-ttu-id="a077e-292">Après la mise à niveau de votre site de développement local, publier hello toohello de modifications intermédiaires de l’application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-292">After your local development site is upgraded, publish hello changes toohello staging web app.</span></span> <span data-ttu-id="a077e-293">Testez votre application.</span><span class="sxs-lookup"><span data-stu-id="a077e-293">Test your application.</span></span> <span data-ttu-id="a077e-294">Si tout semble correct, utilisez hello **échanger** bouton tooswap votre application de web site toohello production intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-294">If all looks good, use hello **Swap** button tooswap your staging site toohello production web app.</span></span> <span data-ttu-id="a077e-295">Lorsque vous utilisez hello **échanger** opération, vous pouvez afficher les modifications de hello qui seront affectées dans la configuration de votre application web.</span><span class="sxs-lookup"><span data-stu-id="a077e-295">When you use hello **Swap** operation, you can view hello changes that will be affected in your web app's configuration.</span></span> <span data-ttu-id="a077e-296">Cela **échanger** opération échange hello des applications web et les bases de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-296">This **Swap** operation swaps hello web apps and databases.</span></span> <span data-ttu-id="a077e-297">Après avoir hello **échanger**hello de base de données de production web application sera point toohello umbraco-étape-db et hello web application sera point tooumbraco-op-db base de données intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="a077e-297">After hello **Swap**, hello production web app will point toohello umbraco-stage-db database, and hello staging web app will point tooumbraco-prod-db database.</span></span>

![Vue d’ensemble de l’échange pour le déploiement de CMS Umbraco](./media/app-service-web-staged-publishing-realworld-scenarios/22umbswap.png)

<span data-ttu-id="a077e-299">Voici les avantages de l’échange hello web app et la base de données hello :</span><span class="sxs-lookup"><span data-stu-id="a077e-299">Here are advantages of swapping both hello web app and hello database:</span></span>

* <span data-ttu-id="a077e-300">Vous pouvez restaurer toohello la version précédente de votre application web avec un autre **échanger** s’il existe des problèmes d’application.</span><span class="sxs-lookup"><span data-stu-id="a077e-300">You can roll back toohello previous version of your web app with another **Swap** if there are any application issues.</span></span>
* <span data-ttu-id="a077e-301">Pour une mise à niveau, vous devez toodeploy fichiers et de bases de données à partir de hello web application toohello production d’applications web de mise en lots et de base de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-301">For an upgrade, you need toodeploy files and databases from hello staging web app toohello production web app and database.</span></span> <span data-ttu-id="a077e-302">Beaucoup de choses peuvent aller de travers lorsque vous déployez des fichiers et des bases de données.</span><span class="sxs-lookup"><span data-stu-id="a077e-302">Many things can go wrong when you deploy files and databases.</span></span> <span data-ttu-id="a077e-303">À l’aide de hello **échanger** fonctionnalité d’emplacements, nous pouvons réduire les temps morts pendant une mise à niveau et réduire les risques de hello d’échecs qui peuvent se produire lorsque vous déployez des modifications.</span><span class="sxs-lookup"><span data-stu-id="a077e-303">By using hello **Swap** feature of slots, we can reduce downtime during an upgrade and reduce hello risk of failures that can occur when you deploy changes.</span></span>
* <span data-ttu-id="a077e-304">Vous pouvez effectuer **A / B test** à l’aide de hello [test en production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) fonctionnalité.</span><span class="sxs-lookup"><span data-stu-id="a077e-304">You can do **A/B testing** by using hello [Testing in production](https://azure.microsoft.com/documentation/videos/introduction-to-azure-websites-testing-in-production-with-galin-iliev/) feature.</span></span>

<span data-ttu-id="a077e-305">Cet exemple montre hello de souplesse de plate-forme hello vous permet de créer des modules personnalisés similaire tooUmbraco Courier toomanage du déploiement du module dans des environnements.</span><span class="sxs-lookup"><span data-stu-id="a077e-305">This example shows you hello flexibility of hello platform where you can build custom modules similar tooUmbraco Courier module toomanage deployment across environments.</span></span>

## <a name="references"></a><span data-ttu-id="a077e-306">Références</span><span class="sxs-lookup"><span data-stu-id="a077e-306">References</span></span>
[<span data-ttu-id="a077e-307">Développement logiciel agile avec Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a077e-307">Agile software development with Azure App Service</span></span>](app-service-agile-software-development.md)

[<span data-ttu-id="a077e-308">Configurer des environnements intermédiaires pour les applications web dans Azure App Service</span><span class="sxs-lookup"><span data-stu-id="a077e-308">Set up staging environments for web apps in Azure App Service</span></span>](web-sites-staged-publishing.md)

[<span data-ttu-id="a077e-309">Comment accéder à des emplacements de déploiement en production toonon tooblock web</span><span class="sxs-lookup"><span data-stu-id="a077e-309">How tooblock web access toonon-production deployment slots</span></span>](http://ruslany.net/2014/04/azure-web-sites-block-web-access-to-non-production-deployment-slots/)
