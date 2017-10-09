---
title: aaaHow toocreate un ticket de support pour SQL Data Warehouse | Documents Microsoft
description: Comment toocreate une prise en charge de ticket dans Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: a91d1f53-03cb-464b-9d5b-4a9c1a194ed3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: 72f7eac82112fb7f1bfb05abca4ce40aeb3c828c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-support-ticket-for-sql-data-warehouse"></a>Comment toocreate une prise en charge de ticket pour SQL Data Warehouse
Si vous rencontrez des problèmes avec SQL Data Warehouse, créez un ticket de support pour que notre équipe d’ingénierie puisse vous aider.

> [!NOTE] 
> À compter de 20/12/2016, intégrité de ressource hello Bonjour portail Azure n’est pas précise. Nous essayons de toofix ce problème. 


## <a name="create-a-support-ticket"></a>Création d’un ticket de support
1. Ouvrez hello [portail Azure][Azure portal].
2. Sur l’écran d’accueil hello, cliquez sur hello **aide + support** vignette.
   
    ![Aide + Support](./media/sql-data-warehouse-get-started-create-support-ticket/help-support.png)
3. Hello aide + Support panneau, cliquez sur **demande de prise en charge de création**.
   
    ![Nouvelle demande de support](./media/sql-data-warehouse-get-started-create-support-ticket/create-support-request.png)
   
    <a name="request-quota-change"></a> 
4. Sélectionnez hello **le Type de demande**.
   
    ![Type de demande](./media/sql-data-warehouse-get-started-create-support-ticket/request-type.png)
   
   > [!NOTE]
   > Par défaut, le **Quota de DTU** de chaque serveur SQL (par exemple, myserver.database.windows.net) est de 45 000. Ce quota constitue simplement une limite de sécurité. Vous pouvez augmenter votre quota en créant un ticket de support en sélectionnant *Quota* en tant que type de demande hello. toocalculate votre DTU a besoin, multipliez hello 7.5 par hello total [DWU] [ DWU] si nécessaire. Par exemple, vous aimeriez toohost deux DW6000s sur un serveur SQL server, puis vous devez demander un quota UDBD 90 000.  Vous pouvez afficher votre consommation DTU actuelle à partir du panneau hello SQL server dans le portail de hello. Interruption et reprises des bases de données s’inscrivent du quota UDBD hello. 
   > 
   > 
5. Sélectionnez hello **abonnement** que les ordinateurs hôtes hello de base de données avec le problème hello vous signalez.
   
    ![Abonnement](./media/sql-data-warehouse-get-started-create-support-ticket/subscription.png)
6. Sélectionnez **SQL Data Warehouse** comme hello des ressources.
   
    ![Ressource](./media/sql-data-warehouse-get-started-create-support-ticket/resource.png)
7. Sélectionnez votre [plan de support Azure][Azure support plan].
   
   * **gestion de la facturation, des abonnements et des quotas** sont pris en charge à tous les niveaux de support.
   * Les problèmes **couverts par la garantie de réparation et d’assistance** sont pris en charge dans les plans de support suivants : [Developer][Developer], [Standard][Standard], [Professional Direct][Professional Direct] ou [Premier][Premier]. Problèmes de réparation sont les problèmes rencontrés par les clients lors de l’utilisation d’Azure dans lequel il existe une attente raisonnable ce problème de hello Microsoft dû.
   * **Développeur encadrement** et **les services de conseil** sont disponibles à hello [Direct Professionnel] [ Professional Direct] et [Premier] [ Premier] les niveaux de prise en charge. 
     
     Si vous avez un Premier plan de prise en charge, vous pouvez également signaler SQL Data Warehouse problèmes sur hello [portail en ligne de Microsoft Premier][Microsoft Premier online portal].  Consultez [les plans de support Azure] [ Azure support plan] toolearn plus hello prend en charge les différents plans, notamment la portée, le temps de réponse, la tarification, etc..  Pour accéder aux questions fréquemment posées sur le support Azure, consultez la page [FAQ du support Azure][Azure support FAQs].  
     
     ![Plan de support](./media/sql-data-warehouse-get-started-create-support-ticket/support-plan.png)
8. Sélectionnez hello **Type de problème** et **catégorie**. Dans cet exemple, nous avons choisi « Outils » en tant que type de problème de hello et « Outils de Client » comme catégorie de hello. 
   
    ![Catégorie de type de problème](./media/sql-data-warehouse-get-started-create-support-ticket/problem-type-category.png)
9. Décrire le problème de hello et choisissez niveau hello d’impact sur l’activité.
   
    ![Description du problème](./media/sql-data-warehouse-get-started-create-support-ticket/problem-description.png)
10. Vos **informations de contact** pour ce ticket de support seront pré-remplies. Mettez-les à jour si nécessaire.
    
    ![Informations de contact](./media/sql-data-warehouse-get-started-create-support-ticket/contact-info.png)
11. Cliquez sur **créer** toosubmit hello prise en charge de demande.

## <a name="monitor-a-support-ticket"></a>Surveiller un ticket de support
Une fois que vous avez envoyé la demande de support hello, équipe de support Azure hello vous contacter. toocheck votre état de la demande et les détails, cliquez sur **gérer les demandes de support** sur le tableau de bord hello.

![Vérification du statut](./media/sql-data-warehouse-get-started-create-support-ticket/check-status.png)

## <a name="other-resources"></a>Autres ressources
En outre, vous pouvez vous connecter avec hello Communauté de SQL Data Warehouse sur [Stack Overflow] [ Stack Overflow] ou sur hello [forum MSDN de l’entrepôt de données de SQL Azure] [ Azure SQL Data Warehouse MSDN forum].

<!--Image references--> 

<!--Article references--> 
[DWU]: ./sql-data-warehouse-overview-what-is.md

<!--MSDN references--> 

<!--Other web references--> 
[Azure portal]: https://portal.azure.com/
[Azure support plan]: https://azure.microsoft.com/support/plans/?WT.mc_id=Support_Plan_510979/  
[Developer]: https://azure.microsoft.com/support/plans/developer/  
[Standard]: https://azure.microsoft.com/support/plans/standard/  
[Professional Direct]: https://azure.microsoft.com/support/plans/prodirect/  
[Premier]: https://azure.microsoft.com/support/plans/premier/  
[Azure support FAQs]: https://azure.microsoft.com/support/faq/
[Microsoft Premier online portal]: https://premier.microsoft.com/
[Stack Overflow]: https://stackoverflow.com/questions/tagged/azure-sqldw/
[Azure SQL Data Warehouse MSDN forum]: https://social.msdn.microsoft.com/Forums/home?forum=AzureSQLDataWarehouse/

