---
title: "une application web à partir de hello Azure Marketplace d’aaaCreate | Documents Microsoft"
description: "Découvrez comment toocreate une application web à partir de hello Azure Marketplace à l’aide de WordPress hello portail Azure."
services: app-service\web
documentationcenter: 
author: sunbuild
manager: erikre
editor: 
ms.service: app-service-web
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: sunbuild
ms.custom: mvc
ms.openlocfilehash: 5ad1ca2f3f7831d857c3e9b02738b6b34acf3649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-web-app-from-hello-azure-marketplace"></a>Créer une application web à partir de hello Azure Marketplace
<!-- Note: This article replaces web-sites-php-web-site-gallery.md -->

[!INCLUDE [tabs](../../includes/app-service-web-get-started-nav-tabs.md)]

Bonjour Azure Marketplace fournit une large gamme d’applications web populaires développé par les Communautés de logiciels open source, par exemple WordPress et Umbraco CMS. Dans ce didacticiel, vous apprendrez comment toocreate WordPress application Azure marketplace.
qui crée une application web Azure et une base de données MySQL. 

![Exemple de tableau de bord d’application web WordPress](./media/app-service-web-create-web-app-from-marketplace/wpdashboard2.png)

## <a name="before-you-begin"></a>Avant de commencer 

Si vous n’avez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) avant de commencer.

## <a name="deploy-from-azure-marketplace"></a>Déployer à partir d’Azure Marketplace
Suivez les étapes de hello ci-dessous toodeploy WordPress à partir d’Azure Marketplace.

### <a name="sign-in-tooazure"></a>Connectez-vous à tooAzure
Connectez-vous à toohello [portail Azure](https://portal.azure.com).

### <a name="deploy-wordpress-template"></a>Déployer un modèle WordPress
Bonjour Azure Marketplace fournit des modèles pour la configuration des ressources, hello du programme d’installation [WordPress](https://portal.azure.com/#create/WordPress.WordPress) tooget de modèle a démarré.
   
Entrez hello suivante informations toodeploy hello WordPress application et ses ressources.

  ![Flux de création WordPress](./media/app-service-web-create-web-app-from-marketplace/wordpress-portal-create.png)


| Champ         | Valeur suggérée           | Description  |
| ------------- |-------------------------|-------------|
| Nom de l'application      | mywordpressapp          | Entrez un nom d’application unique pour votre **nom d’application Web**. Ce nom est utilisé en tant que partie du nom DNS hello par défaut pour votre application `<app_name>.azurewebsites.net`, par conséquent, il doit toobe unique entre toutes les applications dans Azure. Vous pouvez mapper plus tard d’une application de tooyour de nom de domaine personnalisé avant de vous exposez tooyour utilisateurs |
| Abonnement  | Pay-As-You-Go             | Sélectionnez un **Abonnement**. Si vous avez plusieurs abonnements, choisissez l’abonnement approprié de hello. |
| Groupe de ressources| mywordpressappgroup                 |    Entrez un **groupe de ressources**. Un groupe de ressources est un conteneur logique dans lequel les ressources Azure comme les applications web, les bases de données, sont déployées et gérées. Vous pouvez créer un groupe de ressources ou utiliser un groupe existant |
| Plan App Service | myappplan          | Plans de Service d’application représentent collection hello de ressources physiques utilisées toohost vos applications. Sélectionnez hello **emplacement** et hello **niveau tarifaire**. Pour plus d’informations sur la tarification, consultez [Niveau de tarification d’App Service](https://azure.microsoft.com/pricing/details/app-service/) |
| Base de données      | mywordpressapp          | Sélectionnez le fournisseur de base de données appropriée de hello pour MySQL. Web Apps prend en charge **ClearDB**, **Base de données Azure pour MySQL** et **MySQL dans l’application**. Pour plus d’informations, consultez la section [Configuration de la base de données](#database-config) ci-dessous. |
| Application Insights | ON ou OFF          | Cette étape est facultative. [Application Insights](https://azure.microsoft.com/en-us/services/application-insights/) fournit des services de surveillance de votre application web en cliquant sur **ON**.|

<a name="database-config"></a>

### <a name="database-configuration"></a>Configuration de la base de données
Suivez les étapes hello ci-dessous en fonction de votre choix de fournisseur de base de données MySQL.  Il est recommandé de cette base de données d’application Web et MySQL soit Bonjour même emplacement.

#### <a name="cleardb"></a>ClearDB 
[ClearDB](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SuccessBricksInc.ClearDBMySQLDatabase?tab=Overview) est une solution tierce pour un service MySQL entièrement intégré dans Azure. Dans les bases de données ClearDB de toouse commande, vous devez tooassociate une carte de crédit de tooyour [compte Azure](http://account.windowsazure.com/subscriptions). Si vous avez sélectionné le fournisseur de base de données ClearDB, vous pouvez afficher la liste des toochoose de bases de données existant à partir d’ou sur **nouvel** bouton toocreate une base de données.

![Création de ClearDB](./media/app-service-web-create-web-app-from-marketplace/mysqldbcreate.png)

#### <a name="azure-database-for-mysql-preview"></a>Base de données Azure pour MySQL (Version préliminaire)
[Base de données Azure pour MySQL](https://azure.microsoft.com/en-us/services/mysql) fournit un service de base de données managés pour le développement d’applications et de déploiement qui vous permet de toostand une base de données MySQL en minutes et la montée en puissance sur hello rendiez sur cloud hello plus fiable. Avec les modèles de tarification inclus, vous obtenez toutes les fonctions hello souhaité à haute disponibilité, de sécurité et de récupération – intégrées, sans coût supplémentaire. Cliquez sur **niveau tarifaire** toochoose une autre [tarification](https://azure.microsoft.com/pricing/details/mysql). toouse existant de base de données ou existante de MySQL server, utilisez un groupe de ressources dans le hello serveur réside. 

![Configurer les paramètres de base de données hello pour l’application web de hello](./media/app-service-web-create-web-app-from-marketplace/wordpress-azure-database.PNG)

> [!NOTE]
>  Base de données Azure pour MySQL (Version préliminaire) et l’application Web sur Linux (Version préliminaire) ne sont pas disponibles dans toutes les régions. toolearn plus [base de données Azure pour MySQL (version préliminaire)](https://docs.microsoft.com/en-us/azure/mysql) et [l’application Web sur Linux](./app-service-linux-intro.md) limitations. 

#### <a name="mysql-in-app"></a>MySQL dans l’application
[Dans l’application MySQL](https://blogs.msdn.microsoft.com/appserviceteam/2017/03/06/announcing-general-availability-for-mysql-in-app) est une fonctionnalité de Service d’application qui permet d’exécuter MySql en mode natif sur la plateforme de hello. fonctionnalités principales du Hello pris en charge avec la version de hello de fonctionnalité de hello :

- Serveur MySQL en cours d’exécution sur hello même instance côte à côte avec votre serveur web qui héberge le site de hello. Les performances de votre application sont améliorées.
- Le stockage est partagé vos fichiers MySQL et d’application web. Remarque avec les plans gratuit et partagé, vous pouvez atteindre ses limites de quota lors de l’utilisation hello site basée sur les actions de hello vous effectuer. Consultez les [limitations de quota](https://azure.microsoft.com/en-us/pricing/details/app-service/plans/) des plans Gratuit et Partagé.
- Vous pouvez activer la journalisation des requêtes lentes et la journalisation générale pour MySQL. Notez que cela peut affecter les performances de site hello et ne doit pas toujours être activée. fonctionnalité de journalisation Hello permet d’examiner les problèmes d’application. 

Pour plus de détails, consultez cet [article](https://blogs.msdn.microsoft.com/appserviceteam/2016/08/18/announcing-mysql-in-app-preview-for-web-apps/ )

![Gestion de MySQL dans l’application](./media/app-service-web-create-web-app-from-marketplace/mysqlinappmanage.PNG)

Vous pouvez surveiller la progression de hello en cliquant sur icône de cloche hello haut hello de page du portail hello lors hello WordPress application est déployée.    
![Indicateur de progression](./media/app-service-web-create-web-app-from-marketplace/deploy-success.png)

## <a name="manage-your-new-azure-web-app"></a>Gérer votre nouvelle application web Azure

Accédez à toohello tootake portail Azure examiner hello vous venez de créer l’application web.

toodo, connectez-vous trop[https://portal.azure.com](https://portal.azure.com).

Dans le menu de gauche hello, cliquez sur **des Services d’application**, puis cliquez sur nom hello de votre application web Azure.

![Application de navigation du portail tooAzure web](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-list.png)


Vous accédez au _panneau_ de votre application web (une page du portail qui s’ouvre horizontalement).

Par défaut, les lames de votre application web montre hello **vue d’ensemble** page. Cette page propose un aperçu de votre application. Ici, vous pouvez également effectuer des tâches de gestion de base (parcourir, arrêter, démarrer, redémarrer et supprimer des éléments, par exemple). onglets Hello sur le côté gauche de hello du Panneau de hello affiche les pages de configuration différents de hello que vous pouvez ouvrir.

![Panneau App Service sur le portail Azure](./media/app-service-web-create-web-app-from-marketplace/nodejs-docs-hello-world-app-service-detail.png)

Ces onglets dans le panneau de hello affichent hello de nombreuses fonctionnalités, vous pouvez ajouter l’application web tooyour. Hello suivant liste vous donne quelques possibilités de hello :

* Mapper un nom DNS personnalisé
* Lier un certificat SSL personnalisé
* Configurer le déploiement continu
* Montée en puissance et augmentation de la taille des instances
* Ajouter une authentification utilisateur

Terminer toohave hello 5 minutes WordPress installation Assistant Application WordPress hausse et en cours d’exécution. Extraire [Wordpress documentation](https://codex.WordPress.org/) toodevelop votre application web.

![Assistant d’installation de WordPress](./media/app-service-web-create-web-app-from-marketplace/wplanguage.png)

## <a name="configuring-your-app"></a>Configuration de votre application 
Plusieurs étapes sont impliquées dans la gestion de votre application WordPress avant qu’elle soit prête à être utilisée en production. Suivez ces étapes tooconfigure et gérer votre application WordPress :

| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Téléchargement ou stockage de fichiers volumineux** |[Plug-in WordPress pour l’utilisation du Stockage Blob](https://wordpress.org/plugins/windows-azure-storage/)|
| **Envoi d’e-mail** |Achat [SendGrid](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/SendGrid.SendGrid?tab=Overview) service de messagerie et d’utiliser hello [plug-in WordPress pour l’utilisation de SendGrid](https://wordpress.org/plugins/sendgrid-email-delivery-simplified/) tooconfigure il|
| **Noms de domaines personnalisés** |[Configuration d’un nom de domaine personnalisé dans Azure App Service](app-service-web-tutorial-custom-domain.md) |
| **HTTPS** |[Activation du protocole HTTPS pour une application web dans Azure App Service](app-service-web-tutorial-custom-ssl.md) |
| **Validation de pré-production** |[Configuration des environnements intermédiaires et de développement pour les applications web dans Azure App Service](web-sites-staged-publishing.md)|
| **Surveillance et résolution de problèmes** |[Activation de la journalisation des diagnostics pour les applications web dans Azure App Service](web-sites-enable-diagnostic-log.md) et [Surveillance des applications web dans Azure App Service](app-service-web-tutorial-monitoring.md) |
| **Déploiement de votre site** |[Déploiement d’une application web dans Azure App Service](app-service-deploy-local-git.md) |


## <a name="secure-your-app"></a>Sécuriser votre application 
Plusieurs étapes sont impliquées dans la gestion de votre application WordPress avant qu’elle soit prête à être utilisée en production. Suivez ces étapes tooconfigure et gérer votre application WordPress :

| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Nom d’utilisateur et mot de passe forts**|  Modifiez le mot de passe fréquemment. N’utilisez pas de noms d’utilisateur couramment utilisés comme *admin* ou *wordpress*, etc. Forcer tous les WordPress utilisateurs toouse unique nom d’utilisateur et mots de passe forts. |
| **Rester à jour** | Conservez votre WordPress core, les thèmes, les plug-ins de toodate. Utiliser le runtime PHP hello plus récente disponible dans Azure App service |
| **Mettre à jour les clés de sécurité WordPress** | Mise à jour [clé de sécurité WordPress](https://codex.wordpress.org/Editing_wp-config.php#Security_Keys) chiffrement tooimprove stocké dans des cookies|

## <a name="improve-performance"></a>Améliorer les performances
Les performances dans le cloud de hello sont obtenue principalement par le biais de la mise en cache et la montée en puissance parallèle. Toutefois, mémoire de hello, la bande passante et d’autres attributs d’héberger des applications Web doivent être considéré comme.

| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Compréhension des capacités des instances App Service** |[Détails sur la tarification, y compris les capacités des niveaux App Service](https://azure.microsoft.com/en-us/pricing/details/app-service/)|
| **Ressources de cache** |Utilisez [cache Azure Redis](https://azure.microsoft.com/en-us/services/cache/), ou l’un des hello autres offres de mise en cache dans hello [Azure Store](https://azuremarketplace.microsoft.com) |
| **Mise en échelle de votre application** |Vous devez tooscale [application web de hello dans Azure App Service](web-sites-scale.md) et/ou la base de données MySQL. MySQL dans l’application ne prend pas en charge la montée en puissance parallèle, choisissez donc ClearDB ou Base de données Azure pour MySQL (Version préliminaire). [L’échelle de la base de données Azure pour MySQL (version préliminaire)](https://azure.microsoft.com/en-us/pricing/details/mysql/) ou si vous utilisez [ClearDB haute disponibilité routage](http://w2.cleardb.net/faqs/) tooscale votre base de données |

## <a name="availability-and-disaster-recovery"></a>Disponibilité et récupération d’urgence
Haute disponibilité comprend un aspect de hello de continuité toomaintain de récupération d’urgence. La planification des défaillances et des incidents dans hello cloud vous oblige les échecs de hello toorecognize rapidement. Ces solutions aident à implémenter une stratégie pour la haute disponibilité.

| toodo cela... | Élément à utiliser... |
| --- | --- |
| **Sites d’équilibrage de charge** ou **sites de géo-distribution** |[Router le trafic avec Azure Traffic Manager](https://azure.microsoft.com/en-us/services/traffic-manager/) |
| **Sauvegarder et restaurer** |[Sauvegarde d’une application web dans Azure App Service](web-sites-backup.md) et [Restauration d’une application web dans Azure App Service](web-sites-restore.md) |

## <a name="next-steps"></a>Étapes suivantes
En savoir plus sur les différentes fonctionnalités de [toodevelop de Service d’applications et de l’échelle](/app-service-web/).
