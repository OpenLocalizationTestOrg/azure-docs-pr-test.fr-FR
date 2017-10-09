---
title: "performances aaaMonitor de nombreuses bases de données SQL Azure dans une application de SaaS mutualisée | Documents Microsoft"
description: "Surveiller et gérer les performances des bases de données et les pools d’application d’Azure SQL de base de données Wingtip SaaS hello"
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
ms.date: 07/26/2017
ms.author: sstein
ms.openlocfilehash: f0d7ba456c485b7de249a56abac3cf4be3857285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-performance-of-hello-wingtip-saas-application"></a>Surveiller les performances de hello application Wingtip SaaS

Ce didacticiel aborde plusieurs scénarios de gestion de performance clés utilisés dans les applications SaaS. À l’aide d’une activité toosimulate du Générateur de charge sur toutes les bases de données client, les fonctionnalités d’alerte de base de données SQL et les pools élastiques et de surveillance intégrée hello sont illustrées.

application de Wingtip SaaS Hello utilise un modèle de données de locataire unique, où chaque salle (client) a sa propre base de données. Comme de nombreuses applications SaaS, hello anticipées de modèle de charge de travail de client est imprévisible et sporadique. En d’autres termes, les ventes de tickets peuvent se produire à tout moment. tootake l’avantage de ce modèle d’utilisation typique de la base de données, bases de données sont déployées dans des pools de base de données élastique de client. Pools élastiques optimiser le coût hello d’une solution en partage de ressources entre plusieurs bases de données. Avec ce type de modèle, il est important de toomonitor de base de données et tooensure de l’utilisation de ressources pool qui charge sont raisonnablement équilibrée entre les pools. Vous devez également tooensure que les bases de données disposent des ressources adéquates et atteint pas de pools de leurs [eDTU](sql-database-what-is-a-dtu.md) limites. Ce didacticiel explore les méthodes toomonitor et gérer des bases de données et des pools et la manière dont une action corrective tootake dans toovariations de réponse dans la charge de travail.

Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]

> * Simuler l’utilisation de bases de données clientes hello en exécutant un générateur de charge fourni
> * Client de hello analyse des bases de données qu’ils répondent augmentation toohello charge
> * Montée en puissance hello pool élastique dans réponse toohello accrue de la base de données de charge
> * Configurer une deuxième activité de base de données du solde tooload pool élastique


toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

* Hello Wingtip SaaS application est déployée. toodeploy en moins de cinq minutes, consultez [déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)
* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="introduction-toosaas-performance-management-patterns"></a>Modèles de gestion des performances introduction tooSaaS

Gestion des performances de la base de données se compose de la compilation et analyse des données de performances puis réagir toothis données en ajustant les paramètres toomaintain un temps de réponse acceptable pour votre application. Lorsque vous hébergez plusieurs clients, pools de bases de données élastiques sont un tooprovide de manière économique et gérer les ressources d’un groupe de bases de données avec les charges de travail imprévisibles. Avec certains modèles de charge de travail, il peut être avantageux de gérer ne serait-ce que 2 bases de données S3 dans un pool.

![Médias](./media/sql-database-saas-tutorial-performance-monitoring/app-diagram.png)

Pools et hello de bases de données dans des pools, doit être analysé tooensure ils restent dans des limites acceptables de performances. Hello pool configuration toomeet hello besoins des charges de travail d’agrégation hello de toutes les bases de données, vous être assuré qu’Edtu de pool hello est appropriées pour hello de paramétrer la charge de travail global. Ajustez hello par base de données min et par base de données max eDTU valeurs tooappropriate valeurs pour les exigences de votre application spécifique.

### <a name="performance-management-strategies"></a>Stratégies de gestion des performances

* tooavoid avoir toomanually surveiller les performances, il est plus efficace**définir des alertes qui se déclenchent lorsque les bases de données ou les pools Comète hors des limites normales**.
* toorespond les fluctuations de tooshort à long terme dans le niveau de performances des agrégats hello d’un pool, hello **niveau eDTU de pool peut être monté en haut ou bas**. Si ce problème se produit sur une base régulière ou prévisible, **mise à l’échelle de pool de hello peut être planifiée toooccur automatiquement**. Par exemple, diminuez la taille du pool lorsque vous savez que votre charge de travail est faible, disons la nuit ou le week-end.
* fluctuations de toorespond toolonger à long terme, ou les modifications de plusieurs bases de données, de hello **des bases de données peuvent être déplacés dans les autres pools**.
* toorespond tooshort terme augmente dans *individuels* charge de la base de données **des bases de données peuvent être extraite d’un pool et affectés un niveau de performances individuels**. Une fois que la charge de hello est réduite, base de données hello peut ensuite être retournée toohello pool. Lorsque cela est connu d’avance, bases de données peuvent être déplacés préventivement base de données tooensure hello a toujours ressources hello que nécessaires et tooavoid impact sur les autres bases de données dans le pool de hello. Si cette exigence est prévisible, par exemple un lieu rencontre un appel de ventes de ticket pour un événement populaires, ce comportement de gestion peut être intégré dans l’application hello.

Hello [portail Azure](https://portal.azure.com) intégrés de surveillance et de génération d’alertes sur la plupart des ressources. Pour SQL Database, la surveillance et les alertes sont disponibles pour les bases de données et les pools. Cette intégrées d’analyse et d’alerte étant propres à la ressource, il est pratique toouse pour un petit nombre de ressources, mais n’est pas très utile lorsque vous travaillez avec nombreuses ressources.

Pour les scénarios de volume important où vous travaillez avec nombreuses ressources, [Log Analytics (OMS)](sql-database-saas-tutorial-log-analytics.md) peut être utilisé. Il s’agit d’un service Azure distinct offrant l’analytique des journaux de diagnostic et des données de télémétrie rassemblés dans un espace de travail Log Analytics. Analytique de journal peut collecter des données de télémétrie à partir de nombreux services et être tooquery utilisé et définir des alertes.

## <a name="get-hello-wingtip-application-source-code-and-scripts"></a>Obtenir les scripts et le code source des applications Wingtip hello

Hello Wingtip SaaS scripts et code source d’applications sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. [Étapes de scripts de Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="provision-additional-tenants"></a>Approvisionner des locataires supplémentaires

Les pools peuvent être économiques avec deux bases de données S3, hello plusieurs bases de données qui se trouvent dans hello de pool hello plus rentable hello moyenne effet devient. Pour une bonne compréhension du fonctionnement de la gestion et de la surveillance des performances à grande échelle, ce didacticiel requiert le déploiement d’au moins 20 bases de données.

Si vous déjà configuré un lot de clients dans un didacticiel précédent, ignorer toohello [simuler l’utilisation sur toutes les bases de données clientes](#simulate-usage-on-all-tenant-databases) section.

1. Ouvrir... \\Modules d’apprentissage\\l’analyse des performances et gestion\\*PerformanceMonitoringAndManagement.ps1 de démonstration* Bonjour *PowerShell ISE*. Gardez ce script ouvert, car vous exécuterez plusieurs scénarios au cours de ce didacticiel.
1. Définissez **$DemoScenario** = **1**, **Approvisionner un lot de locataires**
1. Appuyez sur **F5** script de hello toorun.

script de Hello déploiera 17 locataires en moins de cinq minutes.

Hello *New-TenantBatch* script utilise un ensemble d’imbriqués ou lié de [le Gestionnaire de ressources](../azure-resource-manager/index.md) les modèles qui créent un lot de clients, qui, par défaut, copie de base de données hello **basetenantdb** sur hello catalogue server toocreate hello nouvelles bases de données client, puis inscrit dans le catalogue de hello et enfin les initialise avec le type de nom et le lieu de locataire hello. Cela est cohérent avec la méthode hello application hello configure un nouveau client. Toutes les modifications apportées trop*basetenantdb* est appliqué tooany nouveaux locataires configurés par la suite. Consultez hello [didacticiel de la gestion des schémas](sql-database-saas-tutorial-schema-management.md) toosee comment toomake schéma change également*existant* locataire des bases de données (y compris hello *basetenantdb* base de données).

## <a name="simulate-usage-on-all-tenant-databases"></a>Simuler l’utilisation sur toutes les bases de données de locataire

Hello *PerformanceMonitoringAndManagement.ps1 de démonstration* script est fourni qui simule une charge de travail en cours d’exécution sur toutes les bases de données client. la charge de Hello est générée à l’aide d’un des scénarios de charge disponibles hello :

| Démonstration | Scénario |
|:--|:--|
| 2 | Générer une charge d’intensité normale (environ 40 DTU) |
| 3 | Générer une charge avec des pics plus longs et plus fréquents par base de données|
| 4 | Générer une charge avec des pics de DTU supérieurs par base de données (environ 80 DTU)|
| 5 | Générer une charge normale et une charge élevée sur un seul locataire (environ 95 DTU)|
| 6 | Générer une charge déséquilibrée entre plusieurs pools|

Générateur de charge Hello applique un *synthétique* base de données de chargement de l’UC uniquement tooevery client. Générateur de Hello démarre une tâche pour chaque base de données client qui appelle périodiquement une procédure stockée qui génère la charge de hello. intervalles, la durée et les niveaux de charge hello (dans Edtu) sont différentes entre toutes les bases de données, en simulant des activités de client imprévisible.

1. Ouvrir... \\Modules d’apprentissage\\l’analyse des performances et gestion\\*PerformanceMonitoringAndManagement.ps1 de démonstration* Bonjour *PowerShell ISE*. Gardez ce script ouvert, car vous exécuterez plusieurs scénarios au cours de ce didacticiel.
1. Définissez **$DemoScenario** = **2**, *Générer une charge d’intensité normale*.
1. Appuyez sur **F5** tooapply un tooall charge vos bases de données client.

Wingtip est une application SaaS, et charge du monde réel hello sur une application SaaS est généralement sporadique et imprévisibles. toosimulate cela, hello charge générateur génère une charge aléatoire distribuée sur tous les locataires. Plusieurs minutes sont nécessaires pour tooemerge de modèle de charge hello, exécutez le Générateur de charge hello de 3 à 5 minutes avant de tenter de charger de hello toomonitor Bonjour les sections suivantes.

> [!IMPORTANT]
> Générateur de charge Hello est en cours d’exécution comme une série de tâches dans votre session PowerShell locale. Conserver hello *PerformanceMonitoringAndManagement.ps1 de démonstration* onglet ouvert ! Si vous fermez l’onglet de hello ou suspendre votre ordinateur, le Générateur de charge hello s’arrête. Générateur de charge Hello reste dans un *appel de travail* état où il génère la charge sur les nouveaux clients sont mis en service après le démarrage du Générateur de hello. Utilisez *Ctrl-C* toostop appel de nouvelles tâches et sortie hello script. Générateur de charge Hello continue toorun, mais uniquement sur les clients existants.

## <a name="monitor-resource-usage-using-hello-azure-portal"></a>Surveiller l’utilisation des ressources à l’aide de hello portail Azure

utilisation des ressources toomonitor hello qui chargent des résultats à partir de hello appliqué, ouvrir le pool de toohello portail hello contenant des bases de données clientes hello :

1. Ouvrez hello [portail Azure](https://portal.azure.com) et parcourir toohello *tenants1 -&lt;utilisateur&gt;*  server.
1. Faites défiler vers le bas, recherchez les pools élastiques, puis cliquez sur **Pool1**. Ce pool contient toutes les bases de locataire hello créés jusqu'à présent.

Observez hello **analyse du pool élastique** et **analyse de la base de données élastique** graphiques.

Bonjour l’utilisation des ressources du pool est l’utilisation de base de données d’agrégation hello pour toutes les bases de données dans le pool de hello. graphique de base de données Hello montre hello cinq bases de données plus sensible :

![](./media/sql-database-saas-tutorial-performance-monitoring/pool1.png)

Étant donné que les bases de données supplémentaires dans le pool hello au-delà de hello les cinq premiers, l’utilisation du pool de hello affiche l’activité qui n’est pas reflétée dans le graphique de cinq bases de données supérieur hello. Pour plus de détails, cliquez sur **Utilisation des ressources de base de données** :

![](./media/sql-database-saas-tutorial-performance-monitoring/database-utilization.png)


## <a name="set-performance-alerts-on-hello-pool"></a>Définir des alertes de performances sur le pool de hello

Définir une alerte sur le pool hello qui se déclenche sur \>utilisation de 75 % comme suit :

1. Ouvrez *Pool1* (sur hello *tenants1 -\<utilisateur\>*  serveur) Bonjour [portail Azure](https://portal.azure.com).
1. Cliquez sur **Règles d’alerte**, puis sur **+ Ajouter une alerte**.

   ![ajouter une alerte](media/sql-database-saas-tutorial-performance-monitoring/add-alert.png)

1. Entrez un nom, par exemple **Nombre élevé de DTU**,
1. Hello du jeu de valeurs suivantes :
   * **Métrique = pourcentage eDTU**
   * **Condition = supérieur à**.
   * **Seuil = 75**.
   * **Période = 30 dernières minutes sur hello**.
1. Ajouter un toohello d’adresse de messagerie *administrateur supplémentaire email(s)* , puis cliquez sur **OK**.

   ![définir une alerte](media/sql-database-saas-tutorial-performance-monitoring/alert-rule.png)


## <a name="scale-up-a-busy-pool"></a>Augmenter la taille d’un pool occupé

Si au niveau de charge globale hello augmente sur un point de toohello pool qu’il maximise out pool de hello et atteint 100 % eDTU d’utilisation, puis les performances de base de données individuelle sont affecté, ralentir potentiellement des temps de réponse pour toutes les bases de données dans le pool de hello.

**À court terme**, mise à l’échelle des ressources supplémentaires de hello pool tooprovide ou supprimez les bases de données à partir du pool de hello (en les déplaçant tooother pools, ou en dehors du niveau de service autonome hello pool tooa).

**À long terme**, envisagez d’optimiser les requêtes ou les performances d’utilisation de base de données tooimprove d’index. En fonction de hello tooperformance de respect de l’application émet son tooscale pratique meilleures un pool d’avant d’atteindre 100 % eDTU d’utilisation. Utiliser une alerte toowarn vous à l’avance.

Vous pouvez simuler un pool occupé par la charge croissante du hello produite par le Générateur de hello. À l’origine tooburst de bases de données hello plus fréquemment et pour la charge d’agrégation hello plus long, croissant sur le pool de hello sans l’évolution des besoins de bases de données individuelles hello hello. Mise à l’échelle d’un pool de hello est facilement effectué dans le portail de hello ou à partir de PowerShell. Cet exercice utilise un portail de hello.

1. Définissez *$DemoScenario* = **3**, _charge générer rafales plus long et plus fréquente par base de données_ intensité hello tooincrease charge hello d’agrégation pool Hello sans modifier les pics de charge hello requis par chaque base de données.
1. Appuyez sur **F5** tooapply un tooall charge vos bases de données client.

1. Accédez trop**Pool1** Bonjour portail Azure.

Hello d’analyse augmente l’utilisation du pool eDTU sur le graphique du haut hello. Prend quelques minutes pour hello nouvelle tookick charge plus élevée, mais vous devez voir rapidement les pool hello démarrer l’utilisation de max toohit et comme charge de hello steadies dans le nouveau modèle de hello, elle surcharge rapidement le pool de hello.

1. tooscale pool de hello, cliquez sur **configurer pool** haut hello hello **Pool1** page.
1. Ajuster hello **eDTU du Pool** aussi un paramètre**100**. Modification des eDTU du pool hello ne modifie pas les paramètres de base de données hello (qui est toujours 50 eDTU par base de données). Vous pouvez voir les paramètres de base de données hello sur le côté droit de hello Hello **configurer pool** page.
1. Cliquez sur **enregistrer** le pool hello tooscale toosubmit hello demande.

Revenir en arrière trop**Pool1** > **vue d’ensemble** hello tooview graphiques de surveillance. Analyser l’effet hello d’offrant davantage de ressources de pool de hello (bien qu’avec les bases de données et une charge aléatoire qu’il n’est pas toujours facile toosee ait jusqu'à ce que vous exécutez pendant un certain temps). Lorsque vous examinez hello graphiques portent à l’esprit que 100 % sur hello supérieur maintenant le graphique représente 100 Edtu, sur hello graphique 100 % inférieure est toujours 50 Edtu comme hello par base de données max est toujours 50 Edtu.

Bases de données restent en ligne et entièrement disponibles tout au long du processus de hello. À hello dernier moment que chaque base de données est prêt toobe activé avec le nouveau eDTU du pool hello, toutes les connexions actives sont interrompues. Code d’application doit toujours être écrits tooretry supprimé les connexions et donc se reconnectera toohello de base de données dans le pool d’échelle hello.

## <a name="load-balance-between-pools"></a>Équilibrage de charge entre pools

Comme un autre tooscaling pool de hello, créez un pool deuxième et placer les bases de données toobalance hello charger entre hello deux pools. toodo ce nouveau pool d’hello doit être créé sur hello même serveur que hello tout d’abord.

1. Bonjour [portail Azure](https://portal.azure.com), ouvrez hello **tenants1 -&lt;utilisateur&gt;**  server.
1. Cliquez sur **+ nouveau pool** toocreate un pool sur le serveur en cours de hello.
1. Sur hello **pool élastique** modèle :

    1. Définissez **nom** trop*Pool2*.
    1. Laissez hello tarification comme **Pool Standard**.
    1. Cliquez sur **Configurer le pool**.
    1. Définissez **eDTU du Pool** trop*eDTU 50*.
    1. Cliquez sur **ajouter des bases de données** toosee une liste des bases de données serveur hello qui peuvent être ajoutées trop*Pool2*.
    1. Sélectionnez n’importe quel toomove 10 bases de données de ces toohello nouveau pool, puis cliquez sur **sélectionnez**. Si vous avez déjà exécuté Générateur de charge hello, service de hello sait déjà que votre profil de performance requiert un plus grand pool que taille de 50 eDTU hello par défaut et vous conseille de commencer avec un paramètre eDTU 100.

    ![Recommandation](media/sql-database-saas-tutorial-performance-monitoring/configure-pool.png)

    1. Pour ce didacticiel, conservez par défaut de hello 50 Edtu, puis cliquez sur **sélectionnez** à nouveau.
    1. Sélectionnez **OK** toocreate Bonjour nouveau pool et toomove Bonjour des bases de données sélectionnées dans celui-ci.

Création du pool de hello et le déplacement de bases de données hello prend quelques minutes. Comme les bases de données sont déplacées qu’ils restent en ligne et entièrement accessibles tant que hello très dernier moment, à partir de laquelle toutes les connexions ouvertes sont fermées. Tant que vous disposez d’une logique de nouvelle tentative, les clients se connecteront puis toohello de base de données dans un nouveau pool de hello.

Parcourir trop**Pool2** (sur hello *tenants1* server) tooopen hello pool et surveiller ses performances. Si vous ne le voyez pas, attendez que l’approvisionnement de hello nouveau pool toocomplete.

Vous voyez à présent que l’utilisation des ressources sur le *Pool1* a chuté et que le *Pool2* est chargé dans la même mesure.

## <a name="manage-performance-of-a-single-database"></a>Gérer les performances d’une base de données

Si une base de données dans un pool est confronté à une charge élevée prolongée, selon la configuration de pool hello, il peut généralement des ressources de hello toodominate dans le pool de hello et avoir un impact sur d’autres bases de données. Si l’activité hello est probablement toocontinue pendant un certain temps, base de données hello peut être temporairement déplacé en dehors du pool de hello. Ainsi, Bonjour Bonjour de toohave de base de données des ressources supplémentaires, il a besoin et elle isole de hello autres bases de données.

Cet exercice simule l’effet de hello de salle de Concert Contoso subissent une charge élevée lorsque les tickets accédez de vente pour un concert populaires.

1. Ouvrez hello... \\ *PerformanceMonitoringAndManagement.ps1 de démonstration* script.
1. Définissez **$DemoScenario = 5, Générer une charge normale et une charge élevée sur un seul locataire (environ 95 DTU).**
1. Définissez **$SingleTenantDatabaseName = contosoconcerthall**
1. Exécuter à l’aide du script hello **F5**.


1. Bonjour [portail Azure](https://portal.azure.com) ouvrir **Pool1**.
1. Inspecter hello **analyse du pool élastique** du graphique et recherchez l’utilisation du pool eDTU hello augmenté. Après une ou deux minutes, une charge plus élevée hello doit démarrer tookick dans, et vous devez voir rapidement que le pool de hello atteint 100 % d’utilisation.
1. Inspecter hello **analyse de la base de données élastique** complet qui montre les bases de données plus sensible hello Bonjour dernière heure. Hello *contosoconcerthall* base de données doit s’afficher dès qu’une des bases de données plus sensible hello cinq.
1. **Cliquez sur l’analyse de base de données élastique hello** **graphique** et qu’il ouvre hello **l’utilisation des ressources de base de données** page où vous pouvez surveiller des bases de données hello. Cela vous permet d’isoler l’affichage de hello pour hello *contosoconcerthall* base de données.
1. Dans la liste hello des bases de données, cliquez sur **contosoconcerthall**.
1. Cliquez sur **niveau tarifaire (échelle dtu)** tooopen hello **configuration des performances** page dans laquelle vous pouvez définir un niveau de performance autonome pour la base de données hello.
1. Cliquez sur hello **Standard** onglet options d’échelle hello tooopen niveau Standard de hello.
1. Faites glisser hello **curseur DTU** tooright tooselect **100** dtu. Notez que cela correspond à toohello objectif de service, **S3**.
1. Cliquez sur **appliquer** toomove hello de base de données en dehors du pool de hello et faites-en un *Standard S3* base de données.
1. Une fois la mise à l’échelle est terminée, effet de hello analyse sur la base de données contosoconcerthall hello et Pool1 sur des panneaux de base de données et le pool élastique hello.

Une fois qu’une charge élevée sur la base de données contosoconcerthall hello hello disparaisse vous devez retourner rapidement, toohello pool tooreduce son coût. S’il est difficile de savoir qui produira lorsque vous pouvez définir une alerte sur la base de données hello déclenchera lorsque son utilisation DTU inférieur hello par base de données max sur le pool de hello. Le déplacement d’une base de données dans un pool est décrite dans l’exercice 5.

## <a name="other-performance-management-patterns"></a>Autres modèles de gestion des performances

**Mise à l’échelle préemptives** dans l’exercice hello ci-dessus dans lequel vous exploré comment tooscale une base de données isolé, vous connaissez le toolook de la base de données pour. Si Gestion hello de salle de Concert Contoso avait informé Wingtips de vente de ticket imminente hello, base de données hello Impossible ont été déplacé en dehors du pool de hello préalablement. Dans le cas contraire, il aurait probablement requis une alerte sur le pool de hello ou toospot de base de données hello que s’est-il passé. Vous ne voudriez toolearn à ce sujet de hello autres locataires dans hello pool signale que des problèmes de performances. Et si le client de hello capable de prédire la durée pendant laquelle ils devront des ressources supplémentaires, vous pouvez définir un Azure Automation runbook toomove hello de base de données en dehors du pool de hello et puis replacer selon une planification définie.

**Client libre-service mise à l’échelle** , car la mise à l’échelle est une tâche appelée facilement via l’API de gestion hello, vous pouvez facilement créer des bases de données clientes tooscale de possibilité de hello dans votre application côté client et il offre une fonctionnalité de votre service SaaS. Par exemple, permettent aux clients administrer l’évolutivité, sans doute lié directement tootheir facturation !

**Mise à l’échelle un pool de haut et bas sur des modèles d’utilisation toomatch planification**

Lorsque l’utilisation d’agrégation clients suit les modèles d’utilisation prévisible, vous pouvez utiliser Azure Automation tooscale un pool de haut et bas selon une planification. Par exemple, diminuez la taille d’un pool après 18 h et avant 6 h en semaine lorsque vous savez que les besoins en ressources baissent.



## <a name="next-steps"></a>Étapes suivantes

Ce didacticiel vous explique comment effectuer les opérations suivantes :

> [!div class="checklist"]
> * Simuler l’utilisation de bases de données clientes hello en exécutant un générateur de charge fourni
> * Client de hello analyse des bases de données qu’ils répondent augmentation toohello charge
> * Montée en puissance hello pool élastique dans réponse toohello accrue de la base de données de charge
> * Configurer une deuxième activité de base de données d’hello de solde de tooload pool élastique

[Didacticiel Restaurer une base de données à locataire unique](sql-database-saas-tutorial-restore-single-tenant.md)


## <a name="additional-resources"></a>Ressources supplémentaires

* Supplémentaires [didacticiels qui reposent sur hello déploiement d’application Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Pools élastiques SQL](sql-database-elastic-pool.md)
* [Azure Automation](../automation/automation-intro.md)
* [Log Analytics](sql-database-saas-tutorial-log-analytics.md) - Didacticiel Configuration et utilisation de Log Analytics
