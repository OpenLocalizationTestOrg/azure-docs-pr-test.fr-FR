---
title: "aaaRestore une base de données SQL Azure dans une application mutualisée | Documents Microsoft"
description: "Découvrez comment toorestore un seul locataires SQL la base de données après la suppression accidentelle de données"
keywords: "didacticiel sur les bases de données SQL"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/10/2017
ms.author: billgib;sstein
ms.openlocfilehash: 8507ecec2424c135f1859b88ebf2bb4e17538a58
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="restore-a-wingtip-saas-tenants-sql-database"></a>Restaurer une base de données SQL de clients SaaS Wingtip

application de Wingtip SaaS Hello est construite à l’aide d’un modèle de base de données pour chaque locataire, où chaque client a sa propre base de données. Un des avantages de hello de ce modèle est qu’il est facile toorestore les données d’un seul client de manière isolée sans affecter d’autres clients.

Dans ce didacticiel, vous allez découvrir deux modèles de récupération des données :

> [!div class="checklist"]

> * Restaurer une base de données dans une base de données parallèle (côte à côte)
> * Restaurer une base de données sur place


|||
|:--|:--|
| **Restaurer le locataire tooa antérieur dans le temps, dans une base de données parallèle** | Ce modèle peut être utilisé par le client hello pour révision, l’audit, la conformité, hello et etc.-base de données d’origine reste inchangée et en ligne. |
| **Restaurer un client sur place** | Ce modèle est généralement utilisé toorecover un locataire tooa état antérieur dans le temps, une fois un client supprime accidentellement des données. Hello de base de données d’origine est mis hors connexion et remplacé par la base de données restaurée hello. |
|||

toocomplete ce didacticiel, assurez-vous que hello est suivant des conditions préalables requises sont effectuées :

* Hello Wingtip SaaS application est déployée. toodeploy en moins de cinq minutes, consultez [déployer et Explorer hello Wingtip SaaS application](sql-database-saas-tutorial.md)
* Azure PowerShell est installé. Pour plus d’informations, consultez [Bien démarrer avec Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps).

## <a name="introduction-toohello-saas-tenant-restore-pattern"></a>Modèle de restauration locataire introduction toohello SaaS

Pour le client de hello rétablir le modèle, il existe deux modèles simples pour la restauration des données d’un locataire individuel. Étant donné que les bases de données des clients sont isolées les unes des autres, la restauration d’un client n’a aucun impact sur les données des autres clients.

Dans le premier modèle d’hello, les données sont restaurées dans une base de données. client de Hello reçoit ensuite base de données access toothis en même temps que leurs données de production. Ce modèle permet à un locataire des données de hello restaurée de tooreview admin et potentiellement l’utiliser tooselectively remplacer les valeurs de données actuelles. C’est toohello SaaS application concepteur toodetermine quel sophistiquée hello options à la récupération des données. Simplement tooreview en mesure des données dans l’état où qu'elle était à un moment donné dans le temps hello est tout ce qui est nécessaire dans certains scénarios. Si la base de données hello utilise [géo-réplication](sql-database-geo-replication-overview.md), nous vous recommandons de copier les données de hello requis à partir de la copie de hello restauré dans la base de données d’origine hello. Si vous remplacez la base de données d’origine hello avec base de données hello restaurée, vous devez tooreconfigure et resynchronisez les géo-réplication.

Dans hello second modèle, qui suppose que ce client hello a subi une perte ou l’altération de données, de la restauration de base de données de production du locataire hello tooa le point antérieur dans le temps. Restauration hello dans le modèle de la place, dans le locataire de hello est mis hors connexion pendant un bref instant pendant que la base de données hello est restauré et remis en ligne. Hello base de données d’origine est supprimé, mais peuvent toujours être restauré à partir si vous avez besoin tooan de retour toogo antérieur même point dans le temps. Une variante de ce modèle pourrait renommer des hello de base de données au lieu de sa suppression, bien que la base de données de changement de nom hello n’offre aucun avantage supplémentaire en termes de sécurité des données.

## <a name="get-hello-wingtip-application-scripts"></a>Obtenir les scripts d’application hello Wingtip

Hello Wingtip SaaS scripts et code source d’applications sont disponibles dans hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) référentiel github. [Étapes de scripts de Wingtip SaaS hello toodownload](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).

## <a name="simulate-a-tenant-accidentally-deleting-data"></a>Simuler la suppression accidentelle des données par le client

toodemonstrate ces scénarios de récupération, nous devons trop*accidentellement* supprimer certaines données de l’une des bases de données clientes hello. Pendant que vous pouvez supprimer n’importe quel enregistrement, hello prochaine étape configure hello démonstration toonot bloquées par des violations d’intégrité référentielle ! Il ajoute également des données d’achat de ticket que vous pouvez utiliser ultérieurement dans hello *les didacticiels Wingtip SaaS Analytique*.

Exécutez le script de génération de ticket hello et créer des données supplémentaires. Générateur de ticket Hello n’intentionnellement pas acheter les tickets pour chaque événement dernière locataires.

1. Ouvrir... \\Modules d’apprentissage\\utilitaires\\*TicketGenerator.ps1 de démonstration* Bonjour *PowerShell ISE*
1. Appuyez sur **F5** toorun hello script et générer des clients et les données de ventes de ticket.


### <a name="open-hello-events-app-tooreview-hello-current-events"></a>Ouvrez hello événements tooreview hello actuels événements de l’application

1. Ouvrez hello *concentrateur d’événements* (http://events.wtp.&lt; utilisateur&gt;. trafficmanager.net) et cliquez sur **salle de Concert Contoso**:

   ![events hub](media/sql-database-saas-tutorial-restore-single-tenant/events-hub.png)

1. Faites défiler la liste des événements hello et prenez note du dernier événement de hello dans la liste de hello :

   ![dernier événement](media/sql-database-saas-tutorial-restore-single-tenant/last-event.png)


### <a name="run-hello-demo-scenario-tooaccidentally-delete-hello-last-event"></a>Exécutez hello démonstration scénario tooaccidentally hello dernier événement delete

1. Ouvrir... \\Modules d’apprentissage\\continuité des activités et récupération d’urgence\\RestoreTenant\\*RestoreTenant.ps1 de démonstration* Bonjour *PowerShell ISE*, et ensemble hello de valeur suivante :
   * **$DemoScenario** = **1**, définissez trop**1** -supprimer des événements sans ventes de ticket.
1. Appuyez sur **F5** toorun hello script et supprimer le dernier événement de hello. Vous devez voir s’afficher une confirmation message similaire toohello :

   ```Console
   Deleting unsold events from Contoso Concert Hall ...
   Deleted event 'Seriously Strauss' from Contoso Concert Hall venue.
   ```

1. page événements de Contoso Hello s’ouvre. Faites défiler la liste et vérifiez les événements hello a disparu. Si l’événement de hello est toujours dans la liste de hello, cliquez sur Actualiser et vérifiez qu’il a disparu.

   ![dernier événement](media/sql-database-saas-tutorial-restore-single-tenant/last-event-deleted.png)


## <a name="restore-a-tenant-database-in-parallel-with-hello-production-database"></a>Restaurer une base de données client en parallèle avec la base de données de production hello

Cet exercice restaure le point de tooa de base de données de salle de Concert Contoso hello dans le temps avant l’événement de hello a été supprimé. Après la suppression des événements de hello dans les étapes précédentes hello, toorecover et de voir les données de salutation supprimée. Vous n’avez pas besoin toorestore votre base de données de production avec l’enregistrement de hello supprimé, mais vous devez toorecover hello ancienne base de données tooaccess hello anciennes données pour d’autres raisons de l’entreprise.

 Hello *restauration-TenantInParallel.ps1* script crée un parallèle client de base de données et une entrée de catalogue parallèle à la fois nommée *ContosoConcertHall\_ancien*. Ce modèle de restauration convient davantage dans le cas d’une récupération après une perte de données mineure ou dans des scénarios de récupération de conformité et d’audit. Il est également hello approche recommandée lorsque vous utilisez [géo-réplication](sql-database-geo-replication-overview.md).

1. Hello complète [simuler un utilisateur de supprimer accidentellement des données](#simulate-a-tenant-accidentally-deleting-data) section.
1. Ouvrir... \\Modules d’apprentissage\\continuité des activités et récupération d’urgence\\RestoreTenant\\_RestoreTenant.ps1 de démonstration_ Bonjour *PowerShell ISE*.
1. Définissez **$DemoScenario** = **2**, définissez cette propriété trop**2** trop*client de restauration en parallèle*.
1. Appuyez sur **F5** script de hello toorun.

script de Hello restaure hello client de base de données (base de données tooa parallèle) tooa point dans le temps avant la suppression des événements hello dans la section précédente de hello. Il crée une deuxième base de données, supprime toutes les métadonnées de catalogue existantes qui existe dans cette base de données et ajoute hello de base de données de catalogue toohello sous hello *ContosoConcertHall\_ancien* entrée.

script de démo Hello ouvre la page des événements hello dans votre navigateur. Note de l’URL de hello : ```http://events.wtp.&lt;user&gt;.trafficmanager.net/contosoconcerthall_old``` que cela est affichant les données de base de données restaurée de hello où *_old* est ajouté toohello nom.

Défilement hello événements répertoriés dans hello navigateur tooconfirm hello événements supprimés dans la section précédente de hello a été restaurée.

Notez ce client hello restauré exposition comme un client supplémentaire, avec ses propres tickets de toobrowse événements application, est peu probable toobe comment vous octroyez à qu'un locataire accéder aux toorestored données, mais sert tooeasily illustre le modèle de restauration hello.

En réalité, mieux vaudrait probablement conserver cette base de données restaurée pendant une période définie uniquement. Vous pouvez supprimer la saisie du locataire hello restaurée une fois que vous avez terminé en appelant hello *Remove-RestoredTenant.ps1* script.

1. Définissez **$DemoScenario** trop**4** tooselect hello *supprimer restauré locataire* scénario.
1. **Appuyez****sur****F5** pour exécuter le script.
1. Hello *ContosoConcertHall\_ancien* entrée est supprimée de catalogue de hello. Pour commencer, fermez la page des événements hello pour ce client dans votre navigateur.


## <a name="restore-a-tenant-in-place-replacing-hello-existing-tenant-database"></a>Restauration d’un client en place, en remplaçant la base de données de client existant hello

Cet exercice restaure point tooa de hello salle de Concert Contoso client dans le temps avant que l’événement de hello a été supprimé. Hello *TenantInPlace de restauration* script restaure hello actuel locataire tooa nouvelle base de données pointant tooa les point précédent dans le temps, et suppressions hello de base de données d’origine. Ce modèle de restauration est la mieux adapté pour la récupération à partir de grave corruption des données comme il peuvent y avoir des pertes de données importantes qui hello client aurait tooaccommodate.

1. Ouvrez le fichier **Demo-RestoreTenant.ps1** dans PowerShell ISE.
1. Définissez **$DemoScenario** trop**5** tooselect hello *restauration du client dans un scénario sur place*.
1. Appuyez sur **F5** pour exécuter le script.

script de Hello restaure point tooa de hello client de base de données de cinq minutes avant l’événement de hello a été supprimé. Pour cela d’abord prendre hello Contoso salle de client en mode hors connexion et présentent donc aucune autre met à jour de données de toohello. Ensuite, une base de données parallèle est créée par la restauration à partir du point de restauration hello et nommé avec un horodateur de nom de base de données tooensure hello n'est pas en conflit avec le nom de base de données client existantes hello. Ensuite, hello ancienne base de données est supprimé et base de données restaurée hello est le nom de base de données d’origine renommée toohello. Enfin, salle de Concert Contoso est remise à base de données en ligne tooallow hello application access toohello restaurée.

Vous avez restauré avec succès hello de base de données tooa point dans le temps avant l’événement de hello a été supprimé. Hello s’ouvre le page événements, par conséquent, vérifiez les événements dernière hello a été restaurée.


## <a name="next-steps"></a>Étapes suivantes

Dans ce didacticiel, vous avez appris à :

> [!div class="checklist"]

> * Restaurer une base de données dans une base de données parallèle (côte à côte)
> * Restaurer une base de données sur place

[Gérer le schéma de base de données client](sql-database-saas-tutorial-schema-management.md)

## <a name="additional-resources"></a>Ressources supplémentaires

* Supplémentaires [didacticiels qui reposent sur hello application Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)
* [Vue d’ensemble de la continuité de l’activité avec la base de données Azure SQL](sql-database-business-continuity.md)
* [En savoir plus sur les sauvegardes SQL Database](sql-database-automated-backups.md)
