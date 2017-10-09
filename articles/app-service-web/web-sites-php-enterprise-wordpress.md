---
title: WordPress aaaEnterprise-classe sur Azure | Documents Microsoft
description: "Découvrez comment toohost un WordPress entreprise de site sur Azure App Service"
services: app-service\web
documentationcenter: 
author: sunbuild
manager: yochayk
editor: 
ms.assetid: 22d68588-2511-4600-8527-c518fede8978
ms.service: app-service-web
ms.devlang: php
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 10/24/2016
ms.author: sumuth
ms.openlocfilehash: 4347eddb31d622d1189dc5db4d81b0f3745d6e69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enterprise-class-wordpress-on-azure"></a>WordPress en version entreprise sur Azure
Azure App Service fournit un environnement modulable, sécurisé et facile à utiliser pour les sites [WordPress][wordpress] stratégiques et à grande échelle. Microsoft lui-même exécute des sites d’entreprise telles que hello [Office] [ officeblog] et [Bing] [ bingblog] blogs. Cet article vous explique comment toouse hello la fonctionnalité d’applications Web de Microsoft Azure App Service tooestablish et mettre à jour d’une entreprise, le site WordPress sur le cloud qui peut gérer un grand nombre de visiteurs.

## <a name="architecture-and-planning"></a>Architecture et planification
Il y a seulement deux conditions requises pour l’installation WordPress de base :

* **Base de données MySQL**: cette spécification est disponible via [ClearDB Bonjour Azure Marketplace][cdbnstore]. Comme alternative, vous pouvez gérer votre propre installation MySQL sur des machines virtuelles Azure, en utilisant [Windows][mysqlwindows] ou [Linux][mysqllinux].

  > [!NOTE]
  > ClearDB fournit plusieurs configurations MySQL. Chaque configuration présente des caractéristiques de performances différentes. Consultez hello [Azure Store] [ cdbnstore] pour plus d’informations sur les offres sont fournies via le magasin de Windows Azure hello ou directement, comme indiqué sur hello [site Web ClearDB](http://www.cleardb.com/pricing.view).
  >
  >
* **PHP 5.2.4 ou version ultérieure** : Azure App Service fournit actuellement [PHP 5.4, 5.5 et 5.6][phpwebsite].

  > [!NOTE]
  > Nous recommandons que vous hello s’exécutent toujours la dernière version de PHP afin que les derniers correctifs de sécurité hello.
  >
  >

### <a name="basic-deployment"></a>Déploiement basique
Si vous utilisez simplement les exigences de base hello, vous pouvez créer une solution de base d’une région Azure.

![Une application web Azure et une base de données MySQL hébergées dans une seule région Azure][basic-diagram]

Bien que cela vous permettrait de créer plusieurs instances d’applications Web de tooscale de site hello votre application, tous les éléments sont hébergé dans des centres de données hello dans une région géographique spécifique. Les visiteurs en dehors de cette région peuvent voir les temps de réponse lente lorsqu’ils utilisent le site de hello. Si des centres de données hello dans cette région sont défaillants, par conséquent, ne votre application.

### <a name="multi-region-deployment"></a>Déploiement multi-régions
À l’aide d’Azure [Traffic Manager][trafficmanager], vous pouvez faire évoluer votre site WordPress dans plusieurs régions géographiques et fournir hello même URL pour tous les visiteurs. Tous les visiteurs arrive via Traffic Manager et sont ensuite région tooa routé basé sur hello configuration d’équilibrage de charge.

![Une application web Azure, hébergée dans plusieurs régions, à l’aide de la haute disponibilité de CDBR routeur tooroute tooMySQL entre les régions][multi-region-diagram]

Dans chaque région, site de WordPress hello serait toujours être répartie sur plusieurs instances d’applications Web, mais cette mise à l’échelle est la région tooa spécifique. Les régions à fort trafic peuvent être mises à l’échelle différemment de celles qui présentent un trafic moins important.

tooreplicate et route le trafic toomultiple bases de données MySQL, vous pouvez utiliser [ClearDB routeurs de haute disponibilité (CDBRs)] [ cleardbscale] (illustré gauche) ou [MySQL Cluster transporteur Grade Edition (CGE)] [cge].

### <a name="multi-region-deployment-with-media-storage-and-caching"></a>Déploiement multi-régions avec stockage multimédia et mise en cache
Si le site de hello accepte les téléchargements ou les fichiers de support d’hôtes, utilisez le stockage Blob Azure. Si vous avez besoin de la mise en cache, [cache Redis][rediscache], [Memcache Cloud](http://azure.microsoft.com/gallery/store/garantiadata/memcached/), [MemCachier](http://azure.microsoft.com/gallery/store/memcachier/memcachier/), ou l’un des hello autres offres de mise en cache Bonjour [Azure Store](http://azure.microsoft.com/gallery/store/).

![Une application web Azure, hébergée dans de nombreuses régions, utilisant un routeur CDBR haute disponibilité pour MySQL, avec le service de cache géré, le Stockage Blob et le réseau de distribution de contenu][performance-diagram]

Stockage d’objets BLOB est réparti entre les régions par défaut, donc vous n’avez pas tooworry sur la réplication de fichiers sur tous les sites. Vous pouvez également activer hello Azure [Content Delivery Network] [ cdn] pour le stockage d’objets Blob, qui distribue les nœuds de tooend de fichiers qui sont plus proches tooyour visiteurs.

### <a name="planning"></a>Planification
#### <a name="additional-requirements"></a>Conditions supplémentaires
| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Téléchargement ou stockage de fichiers volumineux** |[Plug-in WordPress pour l’utilisation du Stockage Blob][storageplugin] |
| **Envoi d’e-mail** |[SendGrid] [ storesendgrid] et hello [plug-in WordPress pour l’utilisation de SendGrid][sendgridplugin] |
| **Noms de domaines personnalisés** |[Configuration d’un nom de domaine personnalisé dans Azure App Service][customdomain] |
| **HTTPS** |[Activation du protocole HTTPS pour une application web dans Azure App Service][httpscustomdomain] |
| **Validation de pré-production** |[Configurer des environnements intermédiaires pour les applications web dans Azure App Service][staging] <p>Lorsque vous déplacez une application web de mise en lots tooproduction, vous déplacer également la configuration de WordPress hello. Assurez-vous que tous les paramètres sont les exigences toohello mis à jour pour votre application de production avant de déplacer tooproduction d’application hello intermédiaire.</p> |
| **Surveillance et résolution de problèmes** |[Activation de la journalisation des diagnostics pour les applications web dans Azure App Service][log] et [Surveillance des applications web dans Azure App Service][monitor] |
| **Déploiement de votre site** |[Déployer une application web dans Azure App Service][deploy] |

#### <a name="availability-and-disaster-recovery"></a>Disponibilité et récupération d’urgence
| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Sites d’équilibrage de charge** ou **sites de géo-distribution** |[Router le trafic avec Azure Traffic Manager][trafficmanager] |
| **Sauvegarder et restaurer** |[Sauvegarde d’une application web dans Azure App Service][backup] et [Restauration d’une application web dans Azure App Service][restore] |

#### <a name="performance"></a>Performances
Les performances dans le cloud de hello sont obtenue principalement par le biais de la mise en cache et la montée en puissance parallèle. Toutefois, mémoire de hello, la bande passante et d’autres attributs d’héberger des applications Web doivent être considéré comme.

| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Compréhension des capacités des instances App Service** |[Détails des prix, notamment les capacités des niveaux App Service][websitepricing] |
| **Ressources de cache** |[Cache redis][rediscache], [Memcache Cloud](/gallery/store/garantiadata/memcached/), [MemCachier](/gallery/store/memcachier/memcachier/), ou l’un des hello autres offres de mise en cache dans hello [Azure Store](/gallery/store/) |
| **Mise en échelle de votre application** |[Mise à l’échelle d’une application web dans Azure App Service][websitescale] et [Routage haute disponibilité ClearDB][cleardbscale] Si vous choisissez toohost et que vous gérez votre propre installation MySQL, vous devez envisager [MySQL Cluster CGE] [ cge] pour la montée en puissance parallèle. |

#### <a name="migration"></a>Migration
Il existe deux méthodes toomigrate un tooAzure de site WordPress existant du Service d’applications :

* **[Exportation de WordPress][export]**: cette méthode exporte le contenu de votre blog hello. Vous pouvez ensuite importer hello tooa contenu nouveau WordPress site sur Azure App Service à l’aide de hello [plug-in WordPress importateur][import].

  > [!NOTE]
  > Ce processus vous permet de migrer votre contenu, mais non vos plug-ins, thèmes ou autres personnalisations. Vous devez installer ces composants à nouveau, manuellement.
  >
  >
* **Une migration manuelle**: [sauvegarder votre site] [ wordpressbackup] et [base de données][wordpressdbbackup]et restaurer manuellement il tooa application web Azure Service d’applications et la base de données MySQL associée. Cette méthode est utile toomigrate personnalisée sites car elle évite le fastidieuses hello de l’installation manuelle des plug-ins, les thèmes et les autres personnalisations.

## <a name="step-by-step-instructions"></a>Instructions pas à pas
### <a name="create-a-wordpress-site"></a>Créer un site WordPress
1. Hello d’utilisation [Azure Marketplace] [ cdbnstore] toocreate une base de données MySQL de taille hello que vous avez identifiés dans hello [Architecture et planification](#planning) section dans hello ou les régions où vous devez héberger votre site.
2. Suivez les étapes de hello dans [créer une application web de WordPress dans Azure App Service] [ createwordpress] toocreate une application web de WordPress. Lorsque vous créez l’application hello web, sélectionnez **utiliser une base de données MySQL existante**, puis sélectionnez la base de données hello que vous avez créé à l’étape 1.

Si vous migrez un site WordPress existant, consultez [migrer un tooAzure de site WordPress existant](#Migrate-an-existing-WordPress-site-to-Azure) après avoir créé une application web.

### <a name="migrate-an-existing-wordpress-site-tooazure"></a>Migrer un tooAzure de site WordPress existant
Comme mentionné dans hello [Architecture et planification](#planning) section, il existe deux façons toomigrate un site WordPress :

* **Utilisez l’exportation et d’importation** pour les sites qui n’ont pas de personnalisation ou où vous souhaitez simplement le contenu toomove hello.
* **Utiliser la sauvegarde et restauration** pour les sites qui ont de nombreuses personnalisations où vous souhaitez toomove tous les éléments.

Utilisez une des hello suivant toomigrate des sections de votre site.

#### <a name="hello-export-and-import-method"></a>Hello export et import, méthode
1. Utilisez [WordPress exporter] [ export] tooexport de votre site.
2. Créer une application web à l’aide des étapes de hello Bonjour [créer un site WordPress](#Create-a-new-WordPress-site) section.
3. Connectez-vous au site WordPress tooyour hello [portail Azure][mgmtportal], puis cliquez sur **plug-ins** > **nouveau**. Recherchez et installez hello **WordPress importateur** plug-in.
4. Après avoir installé le plug-in WordPress importateur de hello, cliquez sur **outils** > **importation**, puis cliquez sur **WordPress** toouse hello plug-in WordPress importateur.
5. Sur hello **importation WordPress** , cliquez sur **choisir un fichier**. Trouver le fichier WXR hello qui a été exporté à partir de votre site WordPress existant, puis cliquez sur **fichier de téléchargement et importation**.
6. Cliquez sur **Envoyer**. Vous êtes invité que hello importation a réussi.
7. Après avoir effectué toutes ces étapes, redémarrez votre site à partir de son **des Services d’application** panneau Bonjour [portail Azure][mgmtportal].

Après avoir importé le site de hello, vous devrez peut-être hello tooperform suivant les paramètres de tooenable étapes qui ne sont pas dans le fichier d’importation hello.

| Si vous utilisiez ceci... | Procédez comme suit... |
| --- | --- |
| **Permaliens** |Tableau de bord de WordPress hello du nouveau site de hello, cliquez sur **paramètres** > **permanents**, puis mettez à jour de la structure de permanents hello. |
| **image/liens média** |tooupdate lie toohello un nouvel emplacement, utilisez hello [plug-in de l’URL de mise à jour bleus velours][velvet], de recherche et remplacement outil, ou mettre à jour manuellement les liens hello dans votre base de données. |
| **Thèmes** |Accédez trop**apparence** > **thème**, puis mettez à jour le thème du site hello en fonction des besoins. |
| **Menus** |Si votre thème prend en charge les menus, page d’accueil des liens tooyour ait sous-répertoire ancien de hello incorporée dans les. Accédez trop**apparence** > **Menus**, puis les mises à jour. |

#### <a name="hello-backup-and-restore-method"></a>Hello backup et restore, méthode
1. Sauvegardez votre WordPress existant de site à l’aide des informations de hello au [WordPress sauvegardes][wordpressbackup].
2. Sauvegardez votre base de données existante à l’aide des informations de hello au [sauvegarder votre base de données][wordpressdbbackup].
3. Créer une base de données et de restauration de sauvegarde de hello.

   1. Achetez une nouvelle base de données à partir de hello [Azure Marketplace][cdbnstore], ou configurez une base de données MySQL sur un [Windows] [ mysqlwindows] ou [Linux ] [ mysqllinux] machine virtuelle.
   2. Utiliser un client MySQL comme [banc d’essai MySQL] [ workbench] toohello tooconnect nouvelle base de données et importer votre base de données WordPress.
   3. Mise à jour hello de base de données toochange hello entrées tooyour nouveau Azure App Service domaine, par exemple, mywordpress.azurewebsites.net. Hello d’utilisation [recherche et remplacement de Script de bases de données WordPress] [ searchandreplace] toosafely modifier toutes les instances.
4. Créer une application web Bonjour portail Azure et publier la sauvegarde de WordPress hello.

   1. toocreate une application web qui a une base de données, Bonjour [portail Azure][mgmtportal], cliquez sur **nouveau** > **Web + Mobile**  >  **Azure Marketplace** > **les applications Web** > **Web application + SQL** (ou **Web application + MySQL**) > **Créer**. Configurez tous les hello requis de paramètres toocreate une application web vide.
   2. Dans votre sauvegarde WordPress, recherchez hello **wp-config.PHP** de fichier, puis ouvrez-le dans un éditeur. Remplacez hello suivant entrées avec des informations de hello pour votre nouvelle base de données MySQL :

      * **Db_name**: nom d’utilisateur hello de base de données hello.
      * **DB_USER**: hello utilisateur nom utilisé tooaccess hello de base de données.
      * **DB_PASSWORD**: mot de passe utilisateur hello.

        Après avoir modifié ces entrées, enregistrez et fermez hello **wp-config.PHP** fichier.
   3. Hello d’utilisation [déployer une application web dans Azure App Service] [ deploy] méthode de déploiement de hello tooenable informations que vous souhaitez toouse et ensuite déployez votre application de web WordPress tooyour sauvegarde dans Azure App Service.
5. Après avoir déployé le site de WordPress hello, vous devez être nouveau site de tooaccess en mesure de hello (comme une application web du Service d’applications) à l’aide de hello *. azurewebsite.net des URL pour le site de hello.

### <a name="configure-your-site"></a>Configuration de votre site
Une fois le site de WordPress hello a été créé ou migré, utilisez hello suivant des performances de tooimprove informations ou activer des fonctionnalités supplémentaires.

| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Définition du mode de plan d’App Service, la taille et activation de la mise à l'échelle** |[Faire évoluer une application web dans Azure App Service][websitescale] |
| **Activation des connexions permanentes de base de données** |Par défaut, WordPress n’utilise pas les connexions de base de données persistante, ce qui risque de provoquer votre toobecome de base de données toohello connexion limitée après plusieurs connexions. tooenable des connexions persistantes, installez hello [plug-in de la carte des connexions persistantes](https://wordpress.org/plugins/persistent-database-connection-updater/installation/). |
| **Amélioration des performances** |<ul><li><p><a href="https://azure.microsoft.com/en-us/blog/disabling-arrs-instance-affinity-in-windows-azure-web-sites/">Désactiver le cookie d’ARR hello</a>, ce qui peut améliorer les performances lorsque WordPress s’exécute sur plusieurs instances d’applications Web.</p></li><li><p>Activation de la mise en cache. Vous pouvez utiliser <a href="http://msdn.microsoft.com/library/azure/dn690470.aspx">cache Redis</a> (aperçu) avec hello <a href="https://wordpress.org/plugins/redis-object-cache/">Redis le plug-in WordPress objet cache</a>, ou vous pouvez utiliser une des hello autres offres de mise en cache à partir de hello <a href="/gallery/store/">Azure Store</a>.</p></li><li><p>[Accélération de WordPress avec Wincache](https://wordpress.org/plugins/w3-total-cache/). Wincache est activé par défaut pour les applications Web Apps. Lors de l’utilisation conjointe de WinCache et dynamique du Cache, désactiver le cache de fichiers de WinCache, mais laissez l’utilisateur de hello et cache de session activée. tooturn désactiver le cache des fichiers, dans un fichier .ini de niveau système, définissez hello valeur suivante :<br/><code>wincache.fcenabled = 0</code></p></li><li><p>[Mise à l’échelle d’une application dans Azure App Service][websitescale] et <a href="http://www.cleardb.com/developers/cdbr/introduction">Routage haute disponibilité ClearDB</a> ou <a href="http://www.mysql.com/products/cluster/">Cluster CGE MySQL</a>.</p></li></ul> |
| **Utilisation d’objets blob pour le stockage** |<ol><li><p>[Création d’un compte de stockage Azure](../storage/common/storage-create-storage-account.md).</p></li><li><p>Découvrez comment trop[hello d’utilisation réseau de Distribution de contenu](../cdn/cdn-create-new-endpoint.md) toogeo-distribuer les données stockées dans des objets BLOB.</p></li><li><p>Installer et configurer hello <a href="https://wordpress.org/plugins/windows-azure-storage/">le stockage Azure pour le plug-in WordPress</a>.</p><p>Pour le programme d’installation détaillée et des informations de configuration du plug-in hello, consultez hello <a href="http://plugins.svn.wordpress.org/windows-azure-storage/trunk/UserGuide.docx">guide de l’utilisateur</a>.</p> </li></ol> |
| **Activation d’e-mail** |Activer <a href="https://azure.microsoft.com/en-us/marketplace/partners/sendgrid/sendgrid-azure/">SendGrid</a> à l’aide du magasin de Windows Azure hello. Installer hello <a href="http://wordpress.org/plugins/sendgrid-email-delivery-simplified">plug-in de SendGrid</a> pour WordPress. |
| **Configurer un nom de domaine personnalisé** |[Configurer un nom de domaine personnalisé dans Azure App Service][customdomain] |
| **Activation du protocole HTTPS pour un nom de domaine personnalisé** |[Activer le protocole HTTPS pour une application web dans Azure App Service][httpscustomdomain] |
| **Équilibrage de charge ou géo-distribution de votre site** |[Router le trafic avec Azure Traffic Manager][trafficmanager]. Si vous utilisez un domaine personnalisé, consultez [configurer un nom de domaine personnalisé dans Azure App Service] [ customdomain] pour plus d’informations sur la façon toouse Traffic Manager avec des noms de domaine personnalisé. |
| **Activation des sauvegardes automatisées** |[Sauvegarde d’une application web dans Azur  App Service][backup] |
| **Activer la journalisation des diagnostics** |[Activer la journalisation des diagnostics pour les applications web dans Azure App Service][log] |

## <a name="next-steps"></a>Étapes suivantes
* [Optimisation de WordPress](http://codex.wordpress.org/WordPress_Optimization)
* [Convertir toomultisite WordPress dans Azure App Service](web-sites-php-convert-wordpress-multisite.md)
* [Assistant de mise à niveau ClearDB pour Azure](http://www.cleardb.com/store/azure/upgrade)
* [Hébergement de WordPress dans un sous-dossier de votre application web dans Azure App Service](http://blogs.msdn.com/b/webapps/archive/2013/02/13/hosting-wordpress-in-a-subfolder-of-your-windows-azure-web-site.aspx)
* [Pas à pas : création d’un site WordPress avec Azure](http://blogs.technet.com/b/blainbar/archive/2013/08/07/article-create-a-wordpress-site-using-windows-azure-read-on.aspx)
* [Hébergement de votre blog WordPress existant sur Azure](http://blogs.msdn.com/b/msgulfcommunity/archive/2013/08/26/migrating-a-self-hosted-wordpress-blog-to-windows-azure.aspx)
* [Activation de permaliens conviviaux dans WordPress](http://www.iis.net/learn/extensions/url-rewrite-module/enabling-pretty-permalinks-in-wordpress)
* [Comment toomigrate et exécuter votre blog WordPress sur Azure App Service](http://www.kefalidis.me/2012/06/how-to-migrate-and-run-your-wordpress-blog-on-windows-azure-websites/)
* [Comment libérer de WordPress sur Azure App Service pour toorun](http://architects.dzone.com/articles/how-run-wordpress-azure)
* [WordPress sur Azure en moins de 2 minutes](http://www.sitepoint.com/wordpress-windows-azure-2-minutes-less/)
* [Déplacement d’un tooAzure de blog WordPress - partie 1 : création d’un blog WordPress sur Azure](http://www.davebost.com/2013/07/10/moving-a-wordpress-blog-to-windows-azure-part-1)
* [Déplacement d’un tooAzure de blog WordPress - partie 2 : transfert de votre contenu.](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-transferring-your-content)
* [Déplacement d’un tooAzure de blog WordPress - partie 3 : configuration de votre domaine personnalisé](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-3-setting-up-your-custom-domain)
* [Déplacement d’un tooAzure de blog WordPress - partie 4 : plutôt permanents et les règles de réécriture d’URL](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-4-pretty-permalinks-and-url-rewrite-rules)
* [Déplacement d’un tooAzure de blog WordPress - partie 5 : déplacement d’une racine de toohello sous-dossier](http://www.davebost.com/2013/07/11/moving-a-wordpress-blog-to-windows-azure-part-5-moving-from-a-subfolder-to-the-root)
* [Comment tooset d’un WordPress web app dans votre compte Azure](http://www.itexperience.net/2014/01/20/how-to-set-up-a-wordpress-website-in-your-windows-azure-account/)
* [Soutien de WordPress sur Azure](http://www.johnpapa.net/wordpress-on-azure/)
* [Astuces pour WordPress sur Azure](http://www.johnpapa.net/azurecleardbmysql/)

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de vous inscrivez pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est nécessaire ; vous ne prenez aucun engagement.
>
>

## <a name="whats-changed"></a>Changements apportés
Pour une modification de toohello guide à partir de sites Web tooApp Service, consultez [Azure App Service et son impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714).

<!-- URL List -->

[performance-diagram]: ./media/web-sites-php-enterprise-wordpress/performance-diagram.png
[basic-diagram]: ./media/web-sites-php-enterprise-wordpress/basic-diagram.png
[multi-region-diagram]: ./media/web-sites-php-enterprise-wordpress/multi-region-diagram.png
[wordpress]: http://www.microsoft.com/web/wordpress
[officeblog]: http://blogs.office.com/
[bingblog]: http://blogs.bing.com/
[cdbnstore]: http://www.cleardb.com/store/azure
[storageplugin]: https://wordpress.org/plugins/windows-azure-storage/
[sendgridplugin]: http://wordpress.org/plugins/sendgrid-email-delivery-simplified/
[phpwebsite]: web-sites-php-configure.md
[customdomain]: app-service-web-tutorial-custom-domain.md
[trafficmanager]: ../traffic-manager/traffic-manager-overview.md
[backup]: web-sites-backup.md
[restore]: web-sites-restore.md
[rediscache]: https://azure.microsoft.com/documentation/services/redis-cache/
[managedcache]: http://msdn.microsoft.com/library/azure/dn386122.aspx
[websitescale]: web-sites-scale.md
[managedcachescale]: http://msdn.microsoft.com/library/azure/dn386113.aspx
[cleardbscale]: http://www.cleardb.com/developers/cdbr/introduction
[staging]: web-sites-staged-publishing.md
[monitor]: web-sites-monitor.md
[log]: web-sites-enable-diagnostic-log.md
[httpscustomdomain]: app-service-web-tutorial-custom-ssl.md
[mysqlwindows]:../virtual-machines/windows/classic/mysql-2008r2.md
[mysqllinux]:../virtual-machines/linux/classic/mysql-on-opensuse.md
[cge]: http://www.mysql.com/products/cluster/
[websitepricing]: /pricing/details/app-service/
[export]: http://en.support.wordpress.com/export/
[import]: http://wordpress.org/plugins/wordpress-importer/
[wordpressbackup]: http://wordpress.org/plugins/wordpress-importer/
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[createwordpress]: web-sites-php-web-site-gallery.md
[velvet]: https://wordpress.org/plugins/velvet-blues-update-urls/
[mgmtportal]: https://portal.azure.com/
[wordpressbackup]: http://codex.wordpress.org/WordPress_Backups
[wordpressdbbackup]: http://codex.wordpress.org/Backing_Up_Your_Database
[workbench]: http://www.mysql.com/products/workbench/
[searchandreplace]: http://interconnectit.com/124/search-and-replace-for-wordpress-databases/
[deploy]: web-sites-deploy.md
[posh]: /powershell/azureps-cmdlets-docs
[Azure CLI]:../cli-install-nodejs.md
[storesendgrid]: https://azure.microsoft.com/marketplace/partners/sendgrid/sendgrid-azure/
[cdn]: ../cdn/cdn-overview.md
