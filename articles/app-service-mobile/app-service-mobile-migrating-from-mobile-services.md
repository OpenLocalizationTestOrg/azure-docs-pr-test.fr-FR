---
title: "aaaMigrate à partir des Services mobiles tooan application de Service d’applications mobiles"
description: "Découvrez comment tooeasily migrer votre tooan d’application Mobile Services application de Service d’applications mobiles"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 07507ea2-690f-4f79-8776-3375e2adeb9e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile
ms.devlang: na
ms.topic: article
ms.date: 10/03/2016
ms.author: glenga
ms.openlocfilehash: cd2e8d98595703389300b79da9bf51cdcefe7b40
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="article-top"></a>Migrer votre tooAzure de Service Mobile Azure App Service existant
Avec hello [disponibilité générale du Service d’applications Azure], Azure Mobile Services, sites peuvent facilement être migrés avantage monolithiques tootake de toutes les fonctionnalités de hello du Service d’applications Azure.  Ce document explique le tooexpect lors de la migration de votre site à partir d’Azure Mobile Services tooAzure du Service d’applications.

## <a name="what-does-migration-do"></a>Quelle est la migration ? site de tooyour
Migration de votre Service Mobile Azure devient votre Service Mobile dans un [Azure App Service] application sans affecter le code de hello.  Elle ne modifie en rien vos Notification Hubs, connexion de données SQL, paramètres d’authentification, travaux planifiés et nom de domaine.  Les clients mobiles à l’aide de votre Service Mobile Azure continuent toooperate normalement.  Migration redémarre votre service une fois qu’il est tooAzure transférée du Service d’applications.

[!INCLUDE [app-service-mobile-migrate-vs-upgrade](../../includes/app-service-mobile-migrate-vs-upgrade.md)]

## <a name="why-migrate"></a>Pourquoi migrer votre site
Microsoft recommande que vous migrez votre avantage de tootake Service Mobile Azure des fonctionnalités hello d’Azure App Service, y compris :

* nouvelles fonctionnalités d’hôte, dont [Tâches web] et [noms de domaine personnalisés] ;
* Connectivité tooyour ressources locales à l’aide de [VNet] en outre trop[connexions hybrides].
* surveillance et dépannage à l’aide de New Relic ou d’ [Application Insights];
* outils DevOps intégrés, dont [mise en lots des emplacements], restauration et tests en production ;
* [mise à l’échelle automatique], équilibrage de charge et [analyse des performances].

Pour plus d’informations sur les avantages de hello de Service d’applications Azure, consultez hello [vs de Services mobiles. App Service].

## <a name="before-you-begin"></a>Avant de commencer
Avant de commencer tout travail majeur sur votre site, vous devez sauvegarder les scripts et la base de données SQL de service mobile.

## <a name="migrating-site"></a>Migration de vos sites
processus de migration Hello migre tous les sites dans une région Azure unique.

toomigrate votre site :

1. Connectez-vous à toohello [portail classique Azure].
2. Sélectionnez un Service Mobile dans la région de hello vous souhaitez toomigrate.
3. Cliquez sur hello **migrer tooApp Service** bouton.

   ![Bouton de la migration de Hello][0]
4. Boîte de dialogue Service hello migration tooApp de lecture.
5. Entrez le nom hello de votre Service Mobile dans zone de hello.  Par exemple, si votre nom de domaine est contoso.azure-mobile.net, puis entrez *contoso* dans la zone hello fournie.
6. Cliquez sur le bouton de graduation hello.

Surveiller l’état de hello de migration hello hello moniteur d’activité. Votre site est répertorié en tant que *migration* Bonjour portail classique Azure.

  ![Moniteur d’activité de migration][1]

Chaque migration peut prendre de 3 minutes too15 par le service mobile en cours de migration.  Votre site reste disponible pendant la migration de hello.
Votre site est redémarré à la fin de hello hello du processus de migration.  site de Hello n’est pas disponible pendant le processus de redémarrage hello, qui peuvent durer quelques secondes.

## <a name="finalizing-migration"></a>Hello Finalisation de la Migration
Plan tootest votre site à partir d’un client mobile à fin hello hello du processus de migration.  Vérifiez que vous pouvez effectuer toutes les actions client courantes sans modifications toohello client mobile.  

### <a name="update-app-service-tier"></a>Sélectionner un niveau tarifaire App Service approprié
Vous avez plus de souplesse dans la tarification après avoir migré tooAzure du Service d’applications.

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Panneau de paramètres Hello s’ouvre par défaut.
4. Cliquez sur **du Plan App Service** dans le menu Paramètres de hello.
5. Cliquez sur hello **niveau tarifaire** vignette.
6. Configuration requise de hello vignette tooyour approprié, puis cliquez sur **sélectionnez**.  Vous devrez peut-être tooClick **afficher toutes les** hello toosee disponible niveaux tarifaires.

Comme point de départ, nous vous recommandons de hello suivant niveaux :

| Niveau tarifaire du service mobile | Niveau tarifaire d’App Service |
|:--- |:--- |
| Gratuit |F1 Gratuit |
| De base |B1 De base |
| Standard |S1 Standard |

Il est une flexibilité considérable en choisissant hello droite niveau tarifaire pour votre application.  Consultez trop[tarification de Service application] pour plus d’informations sur la tarification de hello de votre nouveau Service d’application.

> [!TIP]
> Hello niveau App Service Standard contient des fonctionnalités de réduire l’accès que vous pourriez vouloir toouse, y compris [mise en lots des emplacements], les sauvegardes automatiques et la mise à l’échelle automatique.  Découvrez les nouvelles fonctionnalités de hello lorsque vous y.
>
>

### <a name="review-migration-scheduler-jobs"></a>Consultez hello migré Planificateur de travaux
Les tâches du planificateur ne sont visibles pendant environ 30 minutes après une migration.  Les tâches planifiées continuent toorun en arrière-plan de hello.
tooview vos tâches planifiées, une fois qu’ils sont visibles :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **Parcourir >**, entrez **planification** Bonjour *filtre* zone, puis sélectionnez **Collections planificateur**.

Il existe un nombre limité de tâches de planificateur gratuites disponibles après la migration.  Examinez votre utilisation et hello [Plans de planificateur Azure].

### <a name="configure-cors"></a>Configurer CORS si nécessaire
Partage des ressources cross-origin est une technique de tooallow un site Web de tooaccess une API Web dans un domaine différent.  Si vous utilisez Azure Mobile Services avec un site Web associé, vous devez tooconfigure CORS dans le cadre de la migration de hello.  Si vous accédez à Azure Mobile Services exclusivement à partir de périphériques mobiles, CORS ne doivent pas toobe configurée, sauf dans de rares cas.

Vos paramètres CORS migrés sont disponibles sous forme de hello **MS_CrossDomainWhitelist** paramètre d’application.  toomigrate votre installation de l’application Service CORS de toohello site :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Panneau de paramètres Hello s’ouvre par défaut.
4. Cliquez sur **CORS** dans le menu de hello API.
5. Entrez les origines autorisées dans hello zone, appuyez sur ENTRÉE après chacune d’elles.
6. Une fois votre liste d’origines d’autorisé est correct, cliquez sur bouton Enregistrer de hello.

> [!TIP]
> Un des avantages de hello d’à l’aide d’un Service d’application Azure est que vous pouvez exécuter votre site web et le service mobile sur hello même site.  Pour plus d’informations, consultez hello [étapes](#next-steps) section.
>
>

### <a name="download-publish-profile"></a>Télécharger un nouveau profil de publication
profil de publication Hello de votre site est modifié lors de la migration tooAzure du Service d’applications.  Si vous avez l’intention toopublish votre site à partir de Visual Studio, vous avez besoin d’un nouveau profil de publication.  toodownload hello nouveau profil de publication :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Cliquez sur **Obtenir le profil de publication**.

fichier de paramètres de publication Hello est téléchargés tooyour ordinateur.  Normalement, il est appelé *sitename*.PublishSettings.  Hello d’importation de paramètres dans votre projet existant de publication :

1. Ouvrez Visual Studio et votre projet Service mobile Azure.
2. Avec le bouton droit de votre projet dans hello **l’Explorateur de solutions** et sélectionnez **publier...**
3. Cliquez sur **Importer**.
4. Cliquez sur **Parcourir** et sélectionnez le fichier de paramètres de publication que vous avez téléchargé.  Cliquez sur **OK**
5. Cliquez sur **valider la connexion** tooensure hello publiez le travail de paramètres.
6. Cliquez sur **publier** toopublish votre site.

## <a name="working-with-your-site"></a>Utilisation de votre site après migration
Commencer à travailler avec votre nouveau Service d’application Bonjour [portail Azure] après la migration.  Hello Voici quelques remarques sur les opérations spécifiques que vous avez utilisé tooperform Bonjour [portail classique Azure], avec leurs équivalents de Service d’applications.

### <a name="publishing-your-site"></a>Téléchargement et publication de votre site migré
Votre site est disponible via git ou ftp, et peut être publié à nouveau à l’aide de différents mécanismes, dont WebDeploy, TFS, Mercurial, GitHub et FTP.  informations d’identification de déploiement Hello sont migrées avec rest hello de votre site.  Si vous n’avez pas défini vos informations d’identification de déploiement ou ne vous en souvenez pas, vous pouvez les réinitialiser :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Panneau de paramètres Hello s’ouvre par défaut.
4. Cliquez sur **informations d’identification de déploiement** Bonjour menu de publication.
5. Entrez les informations d’identification de déploiement nouveau hello dans les zones de hello proposées, puis cliquez sur Enregistrer hello.

Vous pouvez utiliser ces sites de hello tooclone informations d’identification avec git ou configurer des déploiements automatisés à partir de GitHub, TFS ou Mercurial.  Pour plus d’informations, consultez hello [documentation sur le déploiement du Service d’applications Azure].

### <a name="appsettings"></a>Paramètres de l’application
La plupart des paramètres pour un service mobile migré sont disponibles via les Paramètres de l’application.  Vous pouvez obtenir la liste de paramètres de l’application hello du hello [portail Azure].
tooview ou modifier vos paramètres d’application :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Panneau de paramètres Hello s’ouvre par défaut.
4. Cliquez sur **paramètres de l’Application** menu général de hello.
5. Faites défiler la section de paramètres d’application toohello et trouver vos paramètres d’application.
6. Cliquez sur valeur hello de valeur hello tooedit du paramètre d’application hello.  Cliquez sur **enregistrer** valeur hello de toosave.

Vous pouvez mettre à jour plusieurs paramètres de l’application à hello même temps.

> [!TIP]
> Il existe deux paramètres d’Application avec hello même valeur.  Par exemple, vous pouvez voir *ApplicationKey* et *MS\_ApplicationKey*.  Mettre à jour les deux paramètres d’application à hello même temps.
>
>

### <a name="authentication"></a>Authentification
Tous les paramètres d’authentification sont disponibles en tant que Paramètres de l’application dans le site migré.  tooupdate vos paramètres d’authentification, vous devez modifier les paramètres de l’application appropriée.  Hello tableau suivant montre les paramètres d’application appropriée hello pour votre fournisseur d’authentification :

| Fournisseur | ID client | Clé secrète client | Autres paramètres |
|:--- |:--- |:--- |:--- |
| Compte Microsoft |**MS\_MicrosoftClientID** |**MS\_MicrosoftClientSecret** |**MS\_MicrosoftPackageSID** |
| Facebook |**MS\_FacebookAppID** |**MS\_FacebookAppSecret** | |
| Twitter |**MS\_TwitterConsumerKey** |**MS\_TwitterConsumerSecret** | |
| Google |**MS\_GoogleClientID** |**MS\_GoogleClientSecret** | |
| Azure AD |**MS\_AadClientID** | |**MS\_AadTenants** |

Remarque : **MS\_AadTenants** est stocké sous forme de liste séparée par des virgules de domaines du locataire (champs hello « Clients autorisés » dans le portail de Services mobiles hello).

> [!WARNING]
> **N’utilisez pas de mécanismes d’authentification hello dans le menu Paramètres de hello**
>
> Azure App Service fournit un système de l’authentification et l’autorisation de « pas de code » distinct sous hello *l’authentification / autorisation* menu Paramètres et hello (déconseillée) *Mobile authentification* option de menu des paramètres hello.  Ces options sont incompatibles avec un service mobile Azure migré.  Vous pouvez [mettre à niveau votre site](app-service-mobile-net-upgrading-from-mobile-services.md) parti tootake d’authentification du Service d’applications Azure hello.
>
>

### <a name="easytables"></a>Données
Hello *données* onglet dans les Services mobiles a été remplacé par *Tables facile* dans hello portail Azure.  tooaccess Tables simple :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Panneau de paramètres Hello s’ouvre par défaut.
4. Cliquez sur **tables facile** dans le menu MOBILE hello.

Vous pouvez ajouter une table en cliquant sur hello **ajouter** bouton ou accéder à vos tables existantes en cliquant sur un nom de table.  À partir de ce panneau, vous pouvez effectuer diverses opérations, notamment :

* modifier les autorisations de table ;
* Modification des scripts opérationnels hello
* Gestion d’un schéma de table hello
* Suppression de table hello
* Effacer le contenu de la table hello
* Suppression des lignes spécifiques de la table de hello

### <a name="easyapis"></a>API
Hello *API* onglet dans les Services mobiles a été remplacé par *API facile* dans hello portail Azure.  tooaccess API simple :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Panneau de paramètres Hello s’ouvre par défaut.
4. Cliquez sur **API facile** dans le menu MOBILE hello.

Votre API migrés figurent déjà dans le panneau de hello.  Vous pouvez également ajouter une API à partir de ce panneau.  toomanage une API spécifique, cliquez sur les API hello.
À partir du Panneau de nouveau hello, vous pouvez ajuster les autorisations de hello et modifier des scripts de hello pour hello API.

### <a name="on-demand-jobs"></a>Tâches du planificateur
Toutes les tâches du planificateur sont disponibles via hello section Collections de travaux du planificateur.  tooaccess vos travaux du planificateur :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **Parcourir >**, entrez **planification** Bonjour *filtre* zone, puis sélectionnez **Collections planificateur**.
3. Sélectionnez hello Collection de tâches pour votre site.  Elle sera nommée *sitename*-Jobs.
4. Cliquez sur **Paramètres**.
5. Cliquez sur **Tâches du planificateur** sous MANAGE.

Les tâches planifiées sont répertoriés avec une fréquence hello que vous avez spécifié avant la migration.  Les tâches à la demande sont désactivées.  toorun un travail à la demande :

1. Sélectionnez la tâche hello toorun vous le souhaitez.
2. Si nécessaire, cliquez sur **activer** tâche hello de tooenable.
3. Cliquez sur **Paramètres**, puis sur **Planification**.
4. Sélectionnez **Une fois** comme Périodicité, puis cliquez sur **Enregistrer**

Vos tâches à la demande se trouvent dans `App_Data/config/scripts/scheduler post-migration`.  Nous vous conseillons de convertir toutes les tâches à la demande trop[Tâches web] ou [fonctions].  Vous devez écrire de nouvelles tâches du planificateur en tant que [Tâches web] ou [fonctions].

### <a name="notification-hubs"></a>Notification Hubs
Mobile Services utilise Notification Hubs pour les notifications push.  Hello, suivant les paramètres de l’application est utilisés toolink hello tooyour du Hub de Notification Service Mobile après la migration :

| Paramètre de l’application | Description |
|:--- |:--- |
| **MS\_PushEntityNamespace** |Hello Namespace de concentrateur de Notification |
| **MS\_NotificationHubName** |Hello nom du concentrateur de Notification |
| **MS\_NotificationHubConnectionString** |Chaîne de connexion de concentrateur de Notification de Hello |
| **MS\_NamespaceName** |Alias pour MS_PushEntityNamespace |

Votre concentrateur de Notification est gérée via hello [portail Azure].  Notez le nom de Hub de Notification hello (vous le trouverez à l’aide des paramètres de l’application hello) :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **Parcourir**>, puis **Notification Hubs**
3. Cliquez sur nom de Hub de Notification hello associé au service mobile de hello.

> [!NOTE]
> Si votre concentrateur de notification est de type « Mixte », il n’est pas visible.  Les concentrateurs de notification de type « Mixte » utilisent Notification Hubs et des fonctionnalités de Service Bus héritées.  [Convertissez vos espaces de noms mixte] avant de continuer.  Une fois la conversion de hello est terminée, votre concentrateur de notification s’affiche dans hello [portail Azure].
>
>

Pour plus d’informations, consultez hello [concentrateurs de Notification] documentation.

> [!TIP]
> Fonctionnalités de gestion de concentrateurs de notification Bonjour [portail Azure] sont toujours en version préliminaire.  Hello [portail classique Azure] reste disponible pour la gestion de vos Hubs de Notification.
>
>

### <a name="legacy-push"></a>Paramètres Push hérités
Si vous avez configuré un Push sur votre service mobile avant l’introduction de hello sur Notification Hubs, vous utilisez *push héritée*.  Si vous utilisez des notifications Push et ne voyez aucun concentrateur de notification répertorié dans votre configuration, il est probable que vous utilisiez des paramètres *push hérités*.  Cette fonctionnalité est migrée avec toutes les autres fonctionnalités.  Toutefois, nous vous recommandons de mettre à niveau les concentrateurs tooNotification peu après que la migration hello est terminée.

Bonjour intermédiaires, tous les paramètres de push héritée hello (avec une exception notable de hello du certificat APNS de hello) sont disponibles dans les paramètres de l’application.  Mettre à jour le certificat APNS de hello en remplaçant hello le fichier approprié sur le système de fichiers hello.

### <a name="app-settings"></a>Autres paramètres d’application
Hello, suivant les paramètres de l’application supplémentaires est migrés à partir de votre Service Mobile et disponibles sous *paramètres* > *paramètres de l’application*:

| Paramètre de l’application | Description |
|:--- |:--- |
| **MS\_MobileServiceName** |nom Hello de votre application |
| **MS\_MobileServiceDomainSuffix** |préfixe du domaine Hello. Par exemple, azure-mobile.net. |
| **MS\_ApplicationKey** |Clé de votre application. |
| **MS\_MasterKey** |Clé principale de votre application |

clé de l’application Hello et la clé principale sont identiques toohello clés d’Application à partir de votre Service Mobile d’origine.  En particulier, hello clé d’Application est envoyée par des clients mobiles toovalidate leur utilisation de l’API de mobile hello.

### <a name="cliequivalents"></a>Équivalents de ligne de commande
Vous pouvez utiliser plus de hello *azure mobile* commande toomanage votre site Azure Mobile Services.  Au lieu de cela, de nombreuses fonctions ont été remplacées par hello *site azure* commande.  Utilisez hello suivant équivalents toofind de table pour des commandes communes :

| Commande *Azure Mobile* | Commande *Azure Site* équivalente |
|:--- |:--- |
| mobile locations |site location list |
| mobile list |site list |
| mobile show *nom* |site show *nom* |
| mobile restart *nom* |site restart *nom* |
| mobile redeploy *nom* |site deployment redeploy *commitId* *nom* |
| mobile key set *nom* *type* *valeur* |site appsetting delete *clé* *nom* <br/> site appsetting add *clé*=*valeur* *nom* |
| mobile config list *nom* |site appsetting list *nom* |
| mobile config get *nom* *clé* |site appsetting show *clé* *nom* |
| mobile config set *nom* *clé* |site appsetting delete *clé* *nom* <br/> site appsetting add *clé*=*valeur* *nom* |
| mobile domain list *nom* |site domain list *nom* |
| mobile domain add *nom* *domaine* |site domain add *domaine* *nom* |
| mobile domain delete *nom* |site domain delete *domaine* *nom* |
| mobile scale show *nom* |site show *nom* |
| mobile scale change *nom* |site scale mode *mode* *nom* <br /> site scale instances *instances* *nom* |
| mobile appsetting list *nom* |site appsetting list *nom* |
| mobile appsetting add *nom* *clé* *valeur* |site appsetting add *clé*=*valeur* *nom* |
| mobile appsetting delete *nom* *clé* |site appsetting delete *clé* *nom* |
| mobile appsetting show *nom* *clé* |site appsetting delete *clé* *nom* |

Mettre à jour des paramètres en mettant à jour hello paramètre appropriée de l’Application d’authentification ou les notifications.
Modifiez des fichiers et publiez votre site via ftp ou git.

### <a name="diagnostics"></a>Diagnostics et journalisation
Les journalisation des diagnostics est normalement désactivée dans un Azure App Service.  journalisation des diagnostics tooenable :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Panneau de paramètres Hello s’ouvre par défaut.
4. Sélectionnez **journaux de Diagnostic** sous le menu des fonctionnalités hello.
5. Cliquez sur **ON** pour hello suivant journaux : **journalisation des applications (système de fichiers)**, **messages d’erreur détaillés**, et **n’a pas pu le suivi des demandes**
6. Cliquez sur **Système de fichiers** pour la journalisation du serveur web.
7. Cliquez sur **Enregistrer**.

tooview hello journaux :

1. Connectez-vous à toohello [portail Azure].
2. Sélectionnez **toutes les ressources** ou **des Services d’application** puis cliquez sur nom hello de votre Service Mobile migrés.
3. Cliquez sur hello **outils** bouton
4. Sélectionnez **flux du journal** sous le menu d’observer hello.

Les journaux sont affichés dans la fenêtre hello comme ils sont générés.  Vous pouvez également télécharger les journaux hello pour une analyse ultérieure à l’aide de vos informations d’identification de déploiement. Pour plus d’informations, consultez hello [journalisation] documentation.

## <a name="known-issues"></a>Problèmes connus
### <a name="deleting-a-migrated-mobile-app-clone-causes-a-site-outage"></a>La suppression d’un clone d’application mobile migré entraîne un arrêt du site
Si vous clonez votre service mobile migré à l’aide d’Azure PowerShell, puis supprimer hello clone, hello entrée DNS pour votre service de production est supprimé.  Votre site est plus accessibles à partir de hello Internet.  

Solution : Si vous le souhaitez tooclone votre site, le faire via le portail de hello.

### <a name="changing-webconfig-does-not-work"></a>La modification du fichier web.config ne fonctionne pas
Si vous avez un site ASP.NET, change toohello `Web.config` fichier ne sont pas appliquées.  Bonjour Azure App Service génère adéquat `Web.config` fichier pendant l’exécution de Services mobiles de démarrage toosupport hello.  Vous pouvez remplacer certains paramètres (comme les en-têtes personnalisés) à l’aide d’un fichier de transformation XML.  Créer un fichier appelé dans `applicationHost.xdt` -ce fichier doit finir Bonjour `D:\home\site` répertoire hello Service Azure.  Chargez le fichier `applicationHost.xdt` via un script de déploiement personnalisé ou en utilisant directement Kudu.  Hello Voici un exemple de document :

```
<?xml version="1.0" encoding="utf-8"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
  <system.webServer>
    <httpProtocol>
      <customHeaders>
        <add name="X-Frame-Options" value="DENY" xdt:Transform="Replace" />
        <remove name="X-Powered-By" xdt:Transform="Insert" />
      </customHeaders>
    </httpProtocol>
    <security>
      <requestFiltering removeServerHeader="true" xdt:Transform="SetAttributes(removeServerHeader)" />
    </security>
  </system.webServer>
</configuration>
```

Pour plus d’informations, consultez hello [exemples de transformation XDT] documentation sur GitHub.

### <a name="migrated-mobile-services-cannot-be-added-tootraffic-manager"></a>Impossible d’ajouter des Services mobiles migrés tooTraffic Manager
Lorsque vous créez un profil Traffic Manager, vous ne pouvez sélectionner directement un profil de toohello migrés service mobile.  Utilisez un « point de terminaison externe ».  Le système d'extrémité externe peut uniquement être ajouté via PowerShell.  Pour plus d’informations, reportez-vous au [didacticiel de Traffic Manager](https://azure.microsoft.com/blog/azure-traffic-manager-external-endpoints-and-weighted-round-robin-via-powershell/).

## <a name="next-steps"></a>Étapes suivantes
Maintenant que votre application est migré tooApp Service, il existe d’autres fonctionnalités que vous pouvez utiliser :

* Déploiement [mise en lots des emplacements] permettent de site de tooyour toostage modifications et effectuer un B tests.
* [Tâches web] remplacent les tâches planifiées à la demande.
* Vous pouvez [en permanence déployer] votre site en liant votre site tooGitHub, TFS ou Mercurial.
* Vous pouvez utiliser [Application Insights] toomonitor votre site.
* Servir un site Web et une API Mobile à partir de hello même code.

### <a name="upgrading-your-site"></a>La mise à niveau votre tooAzure de site des Services mobiles SDK des applications mobiles
* Pour les projets de serveur Node.js, hello new [Mobile applications Node.js SDK] fournit plusieurs nouvelles fonctionnalités. Par exemple, vous pouvez maintenant faire du développement et du débogage localement, utiliser n’importe quelle version de Node.js à partir de 0.10 et utiliser n’importe quel middleware Express.js pour personnaliser.
* Pour. Les projets serveur NET, hello new [les packages NuGet de kit de développement d’applications Mobile](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) avec plus de souplesse sur les dépendances de NuGet.  Ces packages prennent en charge l’authentification du Service d’applications de nouvelle hello et composent avec n’importe quel projet ASP.NET. Pour plus d’informations sur la mise à niveau, consultez [mettre à niveau votre tooApp .NET de Service Mobile existant Service](app-service-mobile-net-upgrading-from-mobile-services.md).

<!-- Images -->
[0]: ./media/app-service-mobile-migrating-from-mobile-services/migrate-to-app-service-button.PNG
[1]: ./media/app-service-mobile-migrating-from-mobile-services/migration-activity-monitor.png
[2]: ./media/app-service-mobile-migrating-from-mobile-services/triggering-job-with-postman.png

<!-- Links -->
[Tarification d’App Service]: https://azure.microsoft.com/en-us/pricing/details/app-service/
[Application Insights]: ../application-insights/app-insights-overview.md
[mise à l’échelle automatique]: ../app-service-web/web-sites-scale.md
[Azure App Service]: ../app-service/app-service-value-prop-what-is.md
[documentation sur le déploiement du Service d’applications Azure]: ../app-service-web/web-sites-deploy.md
[portail classique Azure]: https://manage.windowsazure.com
[portail Azure]: https://portal.azure.com
[Azure Region]: https://azure.microsoft.com/en-us/regions/
[Plans de planificateur Azure]: ../scheduler/scheduler-plans-billing.md
[en permanence déployer]: ../app-service-web/app-service-continuous-deployment.md
[Convertissez vos espaces de noms mixte]: https://azure.microsoft.com/en-us/blog/updates-from-notification-hubs-independent-nuget-installation-model-pmt-and-more/
[curl]: http://curl.haxx.se/
[noms de domaine personnalisés]: ../app-service-web/web-sites-custom-domain-name.md
[Fiddler]: http://www.telerik.com/fiddler
[disponibilité générale du Service d’applications Azure]: https://azure.microsoft.com/blog/announcing-general-availability-of-app-service-mobile-apps/
[connexions hybrides]: ../app-service-web/web-sites-hybrid-connection-get-started.md
[journalisation]: ../app-service-web/web-sites-enable-diagnostic-log.md
[Mobile applications Node.js SDK]: https://github.com/azure/azure-mobile-apps-node
[vs de Services mobiles. App Service]: app-service-mobile-value-prop-migration-from-mobile-services.md
[concentrateurs de Notification]: ../notification-hubs/notification-hubs-push-notification-overview.md
[analyse des performances]: ../app-service-web/web-sites-monitor.md
[Postman]: http://www.getpostman.com/
[mise en lots des emplacements]: ../app-service-web/web-sites-staged-publishing.md
[VNet]: ../app-service-web/web-sites-integrate-with-vnet.md
[Tâches web]: ../app-service-web/websites-webjobs-resources.md
[exemples de transformation XDT]: https://github.com/projectkudu/kudu/wiki/Xdt-transform-samples
[fonctions]: ../azure-functions/functions-overview.md
