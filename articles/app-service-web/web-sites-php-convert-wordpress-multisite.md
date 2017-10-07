---
title: tooMultisite de WordPress aaaConvert dans Azure App Service
description: "Découvrez comment tootake une application web de WordPress existante créée via la galerie hello dans Azure et les convertir tooWordPress Multisite"
services: app-service\web
documentationcenter: php
author: rmcmurray
manager: erikre
editor: 
ms.assetid: fe52dbf4-179c-42f1-adf9-d6a9af920c39
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 1153f0a8043de875f081704cd0a124776758878c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="convert-wordpress-toomultisite-in-azure-app-service"></a>Convertir tooMultisite WordPress dans Azure App Service
## <a name="overview"></a>Vue d'ensemble
*Par [Ben Lobaugh][ben-lobaugh], [Microsoft Open Technologies Inc.][ms-open-tech]*

Dans ce didacticiel, vous allez apprendre comment tootake une application web de WordPress existante créée via la galerie de hello dans Azure et des convertir dans un déploiement Multisite WordPress installer. En outre, vous allez apprendre comment tooassign un tooeach de domaine personnalisé de hello sous-sites au sein de votre installation.

Ce didacticiel part du principe que vous disposez d'une installation existante de WordPress. Si vous ne le faites pas, suivez les instructions hello fournies dans [créer un site web de WordPress à partir de la galerie Azure hello][website-from-gallery].

Convertir un WordPress existant tooMultisite d’installation de site unique est généralement relativement simple, et de nombreuses étapes initiales de hello ici proviennent directement des hello [créer un réseau] [ wordpress-codex-create-a-network] page hello [WordPress code](http://codex.wordpress.org).

Allons-y.

## <a name="allow-multisite"></a>Autorisation du multisite
Vous devez tout d’abord tooenable Multisite via hello `wp-config.php` fichier avec hello **WP\_autoriser\_MULTISITE** constante. Il existe deux méthodes tooedit vos fichiers d’application web : hello est tout d’abord via FTP et hello seconde à partir de Git. Si vous n’êtes pas familiarisé avec la toosetup de ces méthodes, consultez toohello suivant didacticiels :

* [Site web PHP avec MySQL et FTP][website-w-mysql-and-ftp-ftp-setup]
* [Site web PHP avec MySQL et Git][website-w-mysql-and-git-git-setup]

Ouvrez hello `wp-config.php` fichier éditeur hello de votre choix, puis ajoutez suit hello ci-dessus hello `/* That's all, stop editing! Happy blogging. */` ligne.

    /* Multisite */

    define( 'WP_ALLOW_MULTISITE', true );

Être toosave que le fichier hello et téléchargez-le toohello précédent serveur !

## <a name="network-setup"></a>Configuration réseau
Connectez-vous à toohello *wp-admin* zone de votre application web et que vous devez voir un nouvel élément sous hello **outils** menu appelé **le programme d’installation réseau**. Cliquez sur **le programme d’installation réseau** et renseignez les détails de hello de votre réseau.

![Écran Configuration réseau][wordpress-network-setup]

Ce didacticiel utilise hello *sous-répertoires* schéma de site, car il doit toujours fonctionner, et nous en définissant des domaines personnalisés pour chaque sous-site plus loin dans le didacticiel de hello. Toutefois, il doit être possible toosetup un sous-domaine installer si vous mappez un domaine via hello [portail Azure](https://portal.azure.com) et le programme d’installation générique DNS correctement.

Pour plus d’informations sur le sous-domaine vs paramétrages du sous-répertoire voir hello [Types de réseau multisite] [ wordpress-codex-types-of-networks] article sur hello WordPress code.

## <a name="enable-hello-network"></a>Activer hello réseau
Hello réseau est maintenant configuré dans la base de données hello, mais il existe une fonctionnalité de réseau étape tooenable hello restants. Finaliser hello `wp-config.php` paramètres et assurez-vous que `web.config` correctement achemine chaque site.

Après avoir cliqué sur hello **installer** bouton sur hello *le programme d’installation réseau* tooupdate hello va tenter de page, WordPress `wp-config.php` et `web.config` fichiers. Toutefois, vous devez toujours vérifier hello fichiers tooensure hello mises à jour ont réussi. Si ce n’est pas le cas, cet écran vous présente avec les mises à jour nécessaires hello. Modifier et enregistrer des fichiers de hello.

Une fois ces mises à jour, vous devez toolog out et le journal de nouveau tableau de bord hello wp-admin.

Un menu supplémentaire doit maintenant être l’administrateur hello sur la barre intitulée **Mes Sites**. Ce menu vous permet de toocontrol votre nouveau réseau via hello **compte administrateur** tableau de bord.

## <a name="adding-custom-domains"></a>Ajout de domaines personnalisés
Hello [mappage du domaine WordPress MU] [ wordpress-plugin-wordpress-mu-domain-mapping] plug-in met un site de tooany est très simple tooadd des domaines personnalisés dans votre réseau. Hello plug-in toooperate correctement, vous devez toodo une installation supplémentaire sur hello portail et votre bureau d’enregistrement de domaine.

## <a name="enable-domain-mapping-toohello-web-app"></a>Activer l’application web de domaine mappage toohello
Hello **libre** [du Service d’applications](http://go.microsoft.com/fwlink/?LinkId=529714) plan ne prend pas en charge l’ajout de domaines personnalisés tooWeb applications. Vous devez tooswitch trop**Shared** ou **Standard** mode. toodo cela :

* Connectez-vous à toohello portail Azure et recherchez votre application web. 
* Cliquez sur hello **montée en puissance** onglet **paramètres**.
* Sous **Général**, sélectionnez *PARTAGÉ* ou *STANDARD*.
* Cliquez sur **Enregistrer**.

Vous pouvez recevoir un message vous demandant de modification de hello tooverify et accuser réception de votre application web peut maintenant faire un coût, en fonction de l’utilisation et hello autre configuration que vous définissez.

Il prend quelques secondes tooprocess hello les nouveaux paramètres, maintenant est un paramètre de toostart temps votre domaine.

## <a name="verify-your-domain"></a>Vérification de votre domaine
Avant que les applications Web Azure vous permettra de toomap un site toohello de domaine, vous devez d’abord tooverify que vous disposez de domaine de hello toomap hello d’autorisation. toodo par conséquent, vous devez ajouter une entrée DNS CNAME tooyour enregistrement.

* Ouvrez une session dans le Gestionnaire DNS du domaine tooyour
* Créez un enregistrement CNAME *awverify*
* Point *awverify* trop*awverify. YOUR_DOMAIN.azurewebsites.NET*

Elle peut prendre un certain temps pour hello DNS modifications toogo en effet, donc si hello suit ne fonctionne pas immédiatement, aller apporter une tasse de café, puis y revenir et recommencez l’opération.

## <a name="add-hello-domain-toohello-web-app"></a>Ajouter une application web de hello domaine toohello
L’application web tooyour retour via hello portail Azure, cliquez sur **paramètres**, puis cliquez sur **les domaines personnalisés et SSL**.

Hello lorsque *paramètres SSL* sont affichés, vous verrez des champs hello où vous allez entrer tous les domaines hello dont vous souhaitez tooassign tooyour web app. Si un domaine n’est pas répertorié ici, il ne sera pas disponible pour le mappage à l’intérieur de WordPress, quelle que soit la manière dont DNS du domaine hello est le programme d’installation.

![Boîte de dialogue Manage custom domains][wordpress-manage-domains]

Après avoir tapé votre domaine dans la zone de texte hello, Azure vérifie hello enregistrement CNAME que vous avez créé précédemment. Si hello DNS n’a pas été entièrement propagé, affiche un indicateur rouge. Si elle est terminée, vous voyez une coche verte. 

Prenez note de l’adresse IP répertoriée au bas de hello de boîte de dialogue hello de hello. Vous devez cette hello toosetup un enregistrement de votre domaine.

## <a name="setup-hello-domain-a-record"></a>Le programme d’installation d’enregistrement A de domaine hello
Si hello autres étapes ont réussi, vous pouvez maintenant affecter hello domaine tooyour Azure web application via un enregistrement A DNS. 

Il est important toonote ici que les applications web Azure acceptent CNAME et un enregistrement, toutefois vous *doit* utiliser un mappage de domaine approprié tooenable enregistrement A. Un enregistrement CNAME ne peut pas être transféré tooanother CNAME, qui est ce que Azure créé pour vous avec YOUR_DOMAIN.azurewebsites.net.

L’adresse IP de hello à partir de l’étape précédente de hello, retourner le Gestionnaire DNS tooyour et hello du programme d’installation une adresse IP toothat toopoint enregistrement.

## <a name="install-and-setup-hello-plugin"></a>Installer et configurer le plug-in hello
Actuellement, WordPress Multisite n’a pas une méthode intégrée toomap personnalisé des domaines. Toutefois, il n’est un plug-in appelé [mappage du domaine WordPress MU] [ wordpress-plugin-wordpress-mu-domain-mapping] qui ajoute des fonctionnalités de hello pour vous. Ouvrez une session dans la partie du compte administrateur toohello de votre site et installer hello **mappage du domaine WordPress MU** plug-in.

Une fois l’installation et l’activation du plug-in de hello, visitez **paramètres** > **mappage domaine** plug-in de tooconfigure hello. Dans la zone de texte premier hello, *adresse IP du serveur*, d’entrée hello adresse IP que vous avez utilisé toosetup hello un enregistrement pour le domaine de hello. Définissez les *domaine Options* souhaitée (valeurs par défaut hello conviennent souvent) et cliquez sur **enregistrer**.

## <a name="map-hello-domain"></a>Mapper un domaine de hello
Visitez hello **tableau de bord** pour le site de hello vous souhaitez toomap domaine hello. Cliquez sur **outils** > **mappage domaine** et de type hello nouveau domaine dans la zone de texte hello et cliquez sur **ajouter**.

Par défaut, hello nouveau domaine sera domaine du site toohello réécrite générées automatiquement. Si vous voulez toohave de tout le trafic envoyé toohello nouveau domaine, activez hello *domaine principal pour ce blog* avant l’enregistrement. Vous pouvez ajouter un nombre illimité de site tooa de domaines, mais une seule peut être principale.

## <a name="do-it-again"></a>Répétition de l'opération
Les applications Web Azure permettent de tooadd un nombre illimité de domaines tooa web app. tooadd un autre domaine, vous devez tooexecute hello **vérifier votre domaine** et **le programme d’installation d’enregistrement de domaine A hello** sections pour chaque domaine.    

> [!NOTE]
> Si vous souhaitez tooget démarré avec le Service d’application Azure avant de s’inscrire pour un compte Azure, accédez trop[essayez du Service d’applications](https://azure.microsoft.com/try/app-service/), où vous pouvez créer une application web de courte durée de démarrage immédiatement dans le Service d’applications. Aucune carte de crédit n’est requise ; vous ne prenez aucun engagement.
> 
> 

## <a name="whats-changed"></a>Changements apportés
* Pour un toohello guide voir changer à partir de sites Web tooApp Service : [Azure App Service et son Impact sur les Services Azure existants](http://go.microsoft.com/fwlink/?LinkId=529714)

[ben-lobaugh]: http://ben.lobaugh.net
[ms-open-tech]: http://msopentech.com
[website-from-gallery]: https://www.windowsazure.com/develop/php/tutorials/website-from-gallery/
[wordpress-codex-create-a-network]: http://codex.wordpress.org/Create_A_Network
[website-w-mysql-and-ftp-ftp-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-ftp/#header-0
[website-w-mysql-and-git-git-setup]: https://www.windowsazure.com/develop/php/tutorials/website-w-mysql-and-git/#header-1
[wordpress-network-setup]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-network-setup.png
[wordpress-codex-types-of-networks]: http://codex.wordpress.org/Before_You_Create_A_Network#Types_of_multisite_network
[wordpress-plugin-wordpress-mu-domain-mapping]: http://wordpress.org/extend/plugins/wordpress-mu-domain-mapping/

[wordpress-manage-domains]: ./media/web-sites-php-convert-wordpress-multisite/wordpress-manage-domains.png


