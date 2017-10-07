---
title: "aaaProvision de nouveaux clients dans une application mutualisée qui utilise la base de données SQL Azure | Documents Microsoft"
description: "Découvrez comment tooprovision et catalogue nouveaux locataires dans hello application Wingtip SaaS"
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
documentationcenter: 
author: stevestein
manager: craigg
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: sstein
ms.openlocfilehash: eb26f523305650c2124e36707d187dfcdad06fcc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-new-tenants-and-register-them-in-hello-catalog"></a>Configurer les nouveaux clients et les enregistrer dans le catalogue de hello

Dans ce didacticiel, vous en savoir plus sur la fourniture de hello et catalogue SaaS modèles, et comment ils sont implémentés dans hello application Wingtip SaaS. Vous créez et initialisez les nouvelles bases de données client et les enregistrez dans le catalogue de client de l’application hello. catalogue de Hello est une base de données qui maintient le mappage hello entre nombreux clients de l’application hello SaaS et de leurs données. catalogue de Hello joue un rôle d’important dirigeant application demandes toohello bonne base de données.  

Ce didacticiel vous montre comment effectuer les opérations suivantes :

> [!div class="checklist"]

> * Approvisionner un nouveau client unique et découvrir comment il est implémenté
> * Approvisionner un lot de locataires supplémentaires


toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

* Hello Wingtip SaaS application est déployée. toodeploy en moins de cinq minutes, consultez [déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)
* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="introduction-toohello-saas-catalog-pattern"></a>Introduction toohello modèle de catalogue de SaaS

Dans une application reposant sur la base de données de SaaS mutualisée, il est important tooknow où sont stockées les informations pour chaque client. Dans le modèle de catalogue hello SaaS, une base de données de catalogue est utilisé toohold hello et de mappage entre chaque client où leurs données sont stockées. Hello Wingtip SaaS application utilise un locataire unique par l’architecture de base de données, mais le modèle de base hello de stocker le mappage de locataire à base de données dans un catalogue s’applique si une base de données de l’architecture mutualisée ou locataire unique est utilisé.

Chaque client est attribué à une clé qui identifie les dans le catalogue de hello et qui est mappé à emplacement toohello de base de données appropriée hello. Dans l’application de Wingtip SaaS hello, clé de hello est formé à partir d’un hachage du nom du locataire hello. Cela permet de partie de nom de client hello de hello application URL toobe utilisés clé de hello tooconstruct. D’autres schémas de clé de client peuvent être utilisés.  

catalogue de Hello permet hello nom ou son emplacement hello toobe de base de données modifiée avec un impact minimal sur l’application hello.  Dans un modèle de base de données multiclient, il facilite également le « déplacement » d’un client entre les différentes bases de données.  catalogue de Hello peut également être utilisé tooindicate si un client ou la base de données est hors connexion pour maintenance ou d’autres actions. Cela est exploré Bonjour [restaurer le didacticiel d’un seul locataire](sql-database-saas-tutorial-restore-single-tenant.md).

En outre, catalogue hello, qui est en vigueur une base de données de gestion pour une application SaaS, peut stocker des métadonnées supplémentaires de client ou de la base de données, par exemple hello couche Édition ou une base de données, la version du schéma, le plan de service ou SLA offert tootenants et autres informations qui permet la gestion des applications, le support technique ou des processus de devops.  

Au-delà de hello application SaaS, catalogue de hello peut activer les outils de base de données.  Dans l’exemple de Wingtip SaaS hello, catalogue de hello est tooenable utilisé entre locataires requête exploré Bonjour [didacticiel d’analytique ad hoc](sql-database-saas-tutorial-adhoc-analytics.md). Gestion des travaux de bases de données croisées est explorée Bonjour [gestion du schéma](sql-database-saas-tutorial-schema-management.md) et [locataire analytique](sql-database-saas-tutorial-tenant-analytics.md) didacticiels. 

Dans l’application SaaS de Wingtip hello catalogue de hello est implémentée à l’aide des fonctionnalités de gestion de partition hello Hello [bibliothèque de Client élastique de base de données (EDCL)](sql-database-elastic-database-client-library.md). Hello EDCL permet à une application toocreate, gérer et utiliser une carte de partitions de base de données sauvegardée. Une carte de partitions contient une liste de partitions (bases de données) et de mappage hello entre les clés (clients) et les bases de données.  Les fonctions EDCL peuvent être utilisées par les applications ou scripts PowerShell pendant les entrées de hello toocreate dans la carte de partitions hello d’approvisionnement du client et à partir d’applications tooefficiently connecter toohello de base de données correct. EDCL met en cache connexion informations toominimize hello trafic toohello catalogue base de données et de la vitesse de l’application hello.  

> [!IMPORTANT]
> les données de mappage Hello sont accessibles dans la base de données du catalogue hello, mais *ne le modifiez pas*! Modifiez les données de mappage des API Elastic Database Client Library uniquement. Manipuler directement les données de mappage hello risques qui endommage hello catalogue et ne sont pas pris en charge.


## <a name="introduction-toohello-saas-provisioning-pattern"></a>Modèle de configuration de SaaS toohello introduction

Lors de l’intégration d’un nouveau client dans une application SaaS qui utilise un modèle de base de données à client unique, une nouvelle base de données client doit être approvisionnée.  Il doit être créé dans l’emplacement approprié de hello et niveau de service, initialisée avec les données de référence et le schéma approprié et puis enregistrée dans le catalogue de hello sous la clé de locataire approprié hello.  

Différentes approches peuvent être utilisée toodatabase mise en service, qui peut inclure l’exécution de scripts SQL, le déploiement d’un fichier bacpac ou copier une base de données de modèle 'or'.  

Hello approche que vous utilisez l’approvisionnement doit être comprise dans votre stratégie de gestion de schéma global, qui doit s’assurer que les nouvelles bases de données sont configurés avec le schéma le plus récent hello.  Cela est exploré Bonjour [didacticiel de gestion de schéma](sql-database-saas-tutorial-schema-management.md).  

Hello Wingtip SaaS application dispositions nouveaux clients en copiant une base de données finale nommé basetenantdb, déployé sur le serveur de catalogue hello.  L’approvisionnement peut être intégré dans l’application hello dans le cadre d’une expérience d’inscription, et/ou pris en charge en mode hors connexion à l’aide de scripts. Ce didacticiel décrit le processus d’approvisionnement à l’aide des scripts PowerShell. scripts de configuration Hello copier hello basetenantdb toocreate une base de données client dans un pool élastique, puis initialisent avec des informations spécifiques du client et l’inscrire dans la carte de partitions du catalogue hello.  Dans l’exemple d’application hello, bases de données reçoivent des noms basés sur le nom de client hello, mais cela n’est pas un élément essentiel du modèle de hello : hello catalogue de hello permet de toute base de données nom toobe affecté toohello. + 


## <a name="get-hello-wingtip-application-scripts"></a>Obtenir les scripts d’application hello Wingtip

Hello Wingtip SaaS scripts et code source d’applications sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. [Étapes de scripts de Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).


## <a name="provision-and-catalog-detailed-walkthrough"></a>Procédure pas à pas détaillée sur l’approvisionnement et l’inscription dans le catalogue

toounderstand comment hello Wingtip application met en œuvre d’approvisionnement du nouveau client, ajoutez un point d’arrêt et parcourir le flux de travail hello lors de la configuration d’un client :

1. Ouvrir... \\Modules d’apprentissage\\ProvisionAndCatalog\\_ProvisionAndCatalog.ps1 de démonstration_ et hello du jeu de paramètres suivants :
   * **$TenantName** = nom hello soit de nouveau hello (par exemple, *Bushwillow bleus*).
   * **$VenueType** = un des types de salle prédéfinis hello : *bleus*, classicalmusic, danse, jazz, judo, motorracing, polyvalent, opera, rockmusic, football.
   * **$DemoScenario** = **1**, définissez trop**1** trop*configurer un seul client*.

1. Ajouter un point d’arrêt en plaçant votre curseur n’importe où sur la ligne hello 48, ligne indiquant : *nouveau locataire '*, puis appuyez sur **F9**.

   ![point d’arrêt](media/sql-database-saas-tutorial-provision-and-catalog/breakpoint.png)

1. Appuyez sur la touche script hello toorun **F5**.

1. Une fois l’exécution du script hello s’arrête au point d’arrêt hello, appuyez sur **F11** toostep dans le code de hello.

   ![point d’arrêt](media/sql-database-saas-tutorial-provision-and-catalog/debug.png)



Tracer l’exécution du script hello en à l’aide de hello **déboguer** les options de menu - **F10** et **F11** toostep sur ou en hello appelées fonctions. Pour plus d’informations sur le débogage des scripts PowerShell, consultez [Conseils sur l’utilisation et le débogage de scripts PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise).


Hello Voici pas tooexplicitly suivre des étapes, mais une explication du flux de travail hello que parcourir lors du débogage de script de hello :

1. **Hello d’importation SubscriptionManagement.psm1** module qui contient les fonctions de signature dans tooAzure et en sélectionnant hello abonnement Azure que vous utilisez.
1. **Hello d’importation CatalogAndDatabaseManagement.psm1** module qui fournit un catalogue et l’abstraction de niveau de client sur hello [gestion de partition](sql-database-elastic-scale-shard-map-management.md) fonctions. Il s’agit d’un module important qui encapsule la majeure partie du modèle de catalogue hello et est mérite d’être exploré.
1. **Accédez aux détails de configuration**. Pas à pas détaillé Get-Configuration (F11) et voir comment la configuration de l’application hello est spécifiée. Noms de ressources et d’autres valeurs spécifiques à l’application sont définies ici, mais ne modifiez pas ces valeurs jusqu'à ce que vous êtes familiarisé avec les scripts hello.
1. **Obtenir l’objet catalogue hello**. Pas à pas détaillé Get-catalogue qui compose et retourne un objet de catalogue qui est utilisé dans le script de niveau supérieur hello.  Cette fonction utilise les fonctions de gestion de partitions qui sont importées à partir de **AzureShardManagement.psm1**. l’objet catalogue Hello est composée de suivant de hello :
   * $catalogServerFullyQualifiedName est construite à l’aide de stem standard de hello ainsi que votre nom d’utilisateur : _catalogue -\<utilisateur\>. database.windows.net_.
   * $catalogDatabaseName sont récupérées à partir de la configuration de hello : *tenantcatalog*.
   * $shardMapManager objet est initialisé à partir de la base de données de catalogue hello.
   * $shardMap objet est initialisé à partir de hello *tenantcatalog* carte de partitions dans la base de données de catalogue hello.
   Un objet de catalogue est composé retourné et utilisé dans le script de niveau supérieur hello.
1. **Calculer la nouvelle clé de locataire hello**. Une fonction de hachage est la clé de locataire hello toocreate utilisé à partir du nom de client hello.
1. **Vérifiez si clé de locataire hello existe déjà**. catalogue de Hello est vérifiée tooensure hello clé n’est disponible.
1. **base de données client Hello est doté de New-TenantDatabase.** Utilisez **F11** toostep dans et voir comment la base de données hello est configuré à l’aide un [modèle Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md).

nom de base de données Hello est construit à partir de hello client nom toomake il effacer quelle partition appartient toowhich client. (Autres stratégies d’affectation de noms de base de données peuvent être facilement utilisés.) + Un modèle de gestionnaire de ressources est utilisé toocreate une base de données client en copiant une base de données finale (baseTenantDB) sur le serveur de catalogue hello. Une autre approche pourrait être toocreate une base de données vide, puis initialisez-le en important un fichier bacpac ou tooexecute un script d’initialisation à partir d’un emplacement connu.  

modèle de gestionnaire de ressources Hello est dans le dossier de hello ...\Learning Modules\Common\ : *tenantdatabasecopytemplate.json*

Après la création de la base de données client hello, il est alors plu **initialisé avec le nom de la salle (locataire) hello et le type de lieu de hello**. Une autre initialisation peut également être accomplie ici.

Hello **base de données est inscrit dans le catalogue de hello** avec *Add-TenantDatabaseToCatalog* à l’aide de la clé de locataire hello. Utilisez **F11** toostep dans les détails de hello :

* base de données de catalogue Hello est ajouté carte de partitions toohello (liste hello des bases de données connus).
* Hello mappage de cette partition toohello de liens hello valeur de clé est créée.
* Métadonnées supplémentaires (nom de salle hello) sur le client de hello sont ajoutées table de clients toohello dans le catalogue de hello.  table de clients Hello ne fait pas partie du schéma de ShardManagement hello et n’est pas installé par hello EDCL.  Le tableau suivant illustre comment hello catalogue peuvent être étendues toosupport des données supplémentaires spécifiques à l’application.   


Après la configuration, l’exécution retourne toohello d’origine *ProvisionAndCatalog de démonstration* script, qui s’ouvre hello **événements** page pour le client dans le navigateur de hello hello :

   ![événements](media/sql-database-saas-tutorial-provision-and-catalog/new-tenant.png)


## <a name="provision-a-batch-of-tenants"></a>Approvisionner un lot de locataires

Cet exercice permet d’approvisionner un lot de 17 clients. Il est recommandé de que configurer de ce lot de locataires avant de démarrer d’autres didacticiels Wingtip SaaS, par conséquent, il est plus de quelques toowork de bases de données avec.

1. Ouvrir... \\Modules d’apprentissage\\ProvisionAndCatalog\\*ProvisionAndCatalog.ps1 de démonstration* Bonjour *PowerShell ISE* et modifiez hello *$ DemoScenario* too3 de paramètre :
   * **$DemoScenario** = **3**, également modifier**3** trop*approvisionner un lot de locataires*.
1. Appuyez sur **F5** et exécutez le script de hello.

script de Hello déploie un lot de clients supplémentaires. Il utilise un [modèle Azure Resource Manager](../azure-resource-manager/resource-manager-template-walkthrough.md) qui contrôle le traitement par lots hello et délègue ensuite la configuration de chaque modèle lié tooa de base de données. À l’aide des modèles de cette façon permet à Azure Resource Manager toobroker hello est le processus de votre script de déploiement. Configurer des modèles de bases de données en parallèle, où il peut et gère les nouvelles tentatives si nécessaire, optimisation des processus global de hello. script de Hello est idempotente par conséquent, si elle échoue ou s’arrête pour une raison quelconque, exécutez-le à nouveau.

### <a name="verify-hello-batch-of-tenants-successfully-deployed"></a>Vérifiez que le lot hello de clients déployés avec succès

* Ouvrez hello *tenants1* serveur en recherchant tooyour la liste des serveurs de hello [portail Azure](https://portal.azure.com), cliquez sur **bases de données SQL**et vérifiez que le lot de hello de 17 bases de données supplémentaires sont désormais dans la liste de hello :

   ![liste de base de données](media/sql-database-saas-tutorial-provision-and-catalog/database-list.png)



## <a name="other-provisioning-patterns"></a>Autres modèles d’approvisionnement

Voici les autres modèles d’approvisionnement non inclus dans ce tutoriel :

**Pré-approvisionnement des bases de données.** Hello prédéployant le modèle exploite le fait de hello que bases de données dans un pool élastique n’ajoutent pas de frais supplémentaires. Est de facturation pour le pool élastique de hello, ne Hello pas les bases de données et ne consomment des bases de données inactives aucune ressource. En pré-approvisionnant les bases de données d’un pool et en les allouant en cas de besoin, le délai d’intégration du client peut être considérablement réduit. plusieurs Hello pré-configurés des bases de données peut être sont ajustées tookeep nécessaire une mémoire tampon appropriée pour hello anticipées de taux de configuration.

**Approvisionnement automatique.** Dans le modèle de mise en service automatique hello, un service de mise en service dédié est utilisé tooprovision serveurs, les pools et les bases de données automatiquement en fonction des besoins, notamment les bases de données de configuration préalable dans les pools élastiques si vous le souhaitez. Et si la déduplication commandées et supprimés les bases de données, des écarts dans les pools élastiques peuvent être remplies par hello configuration service comme vous le souhaitez. Un tel service peut être simple ou complexe (par exemple, la gestion de l’approvisionnement sur plusieurs zones géographiques) et peut configurer la géoréplication automatiquement si cette stratégie est utilisée pour la récupération d’urgence. Avec le modèle de mise en service automatique hello, une application cliente ou un script soumet un approvisionnement toobe de file d’attente de tooa demande traité par hello service de configuration et interrogerait puis achèvement de toodetermine service hello. Si la configuration anticipée est utilisé, les demandes seraient gérés rapidement avec service hello la gestion de l’approvisionnement d’une base de données de remplacement en cours d’exécution en arrière-plan de hello.



## <a name="next-steps"></a>Étapes suivantes

Dans ce tutoriel, vous avez appris à effectuer les opérations suivantes :

> [!div class="checklist"]

> * Approvisionner un nouveau locataire unique
> * Approvisionner un lot de locataires supplémentaires
> * Pas à pas détaillé détails hello de configuration des clients et de les inscrire dans le catalogue de hello

Essayez de hello [didacticiel analyse des performances](sql-database-saas-tutorial-performance-monitoring.md).

## <a name="additional-resources"></a>Ressources supplémentaires

* Supplémentaires [didacticiels qui reposent sur hello application Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Bibliothèque cliente de base de données élastique](https://docs.microsoft.com/azure/sql-database/sql-database-elastic-database-client-library)
* [Comment tooDebug des Scripts dans Windows PowerShell ISE](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/how-to-debug-scripts-in-windows-powershell-ise)
