---
title: "aaaThreat détection - base de données SQL Azure | Documents Microsoft"
description: "La détection des menaces détecte des activités de base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles."
services: sql-database
documentationcenter: 
author: rmatchoro
manager: jhubbard
editor: v-romcal
ms.assetid: b50d232a-4225-46ed-91e7-75288f55ee84
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 06/19/2017
ms.author: ronmat; ronitr
ms.openlocfilehash: 0879d20eff515a4e69358b5a98ceccf57fbd0ea2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sql-database-threat-detection"></a>Détection de menaces pour les bases de données SQL

Détection des menaces SQL détecte des activités anormales indiquant les bases de données tooaccess ou exploiter tentatives inhabituel et potentiellement dangereux.

## <a name="overview"></a>Vue d'ensemble

Détection des menaces SQL fournit une nouvelle couche de sécurité, ce qui permet aux clients toodetect et de répond toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales.  Les utilisateurs reçoivent une alerte en cas d’activités de base de données suspectes, de vulnérabilités potentielles, d’attaques par injection de code SQL et de modèles d’accès anormaux à la base de données. Alertes de détection des menaces SQL fournissent des détails d’activité suspecte et recommandent la mesure sur la façon de tooinvestigate et d’atténuer les menaces de hello. Les utilisateurs peuvent Explorer à l’aide d’événements suspects hello [l’audit de base de données SQL](sql-database-auditing.md) toodetermine s’ils résultent d’une tentative de tooaccess, violation, ou exploiter les données dans la base de données hello. La détection des menaces rend tooaddress simple potentiels menaces toohello base de données sans nécessité de hello toobe un expert en sécurité ou gérer des systèmes de surveillance de la sécurité avancée.

Par exemple, injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données. Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs d’entrée application, violation ou modification des données dans la base de données hello.

Détection des menaces SQL intègre les alertes avec [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/), et chaque serveur de base de données SQL protégé sera facturée selon hello même prix en tant que couche Azure Security Center Standard, à 15 $/ nœud/mois, où chaque protégé SQL Serveur de base de données est comptabilisée comme un seul nœud. Nous vous invitons tootry son évolution horizontale pendant 60 jours pour le libérer. 

## <a name="set-up-threat-detection-for-your-database-in-hello-azure-portal"></a>Configurer la détection des menaces pour votre base de données Bonjour portail Azure
1. Lancez hello Azure portail à [https://portal.azure.com](https://portal.azure.com).
2. Accédez à panneau de configuration de toohello de base de données SQL toomonitor de hello. Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**. 
    ![Volet de navigation][1]
3. Bonjour **audit et la détection des menaces** activer Panneau de configuration **ON** l’audit, qui affiche les paramètres de détection de menace hello.
  
    ![Volet de navigation][2]
4. **Activez** la détection des menaces.
5. Configurez la liste hello d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités anormales base de données.
6. Cliquez sur **enregistrer** Bonjour **détection d’audit et de menaces** panneau toosave hello nouveaux ou mis à jour l’audit et paramètres de la détection.
       
    ![Volet de navigation][3]

## <a name="set-up-threat-detection-using-powershell"></a>Configurer la détection des menaces avec PowerShell

Pour obtenir un exemple de script, consultez [Configurer l’audit et la détection des menaces avec PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).

## <a name="explore-anomalous-database-activities-upon-detection-of-a-suspicious-event"></a>Explorer les activités anormales sur la base de données en cas de détection d’un événement suspect
1. Vous recevrez une notification par courrier électronique lorsque des activités anormales sont détectées au niveau de la base de données. <br/>
   messagerie de Hello fournit des informations sur les événements de sécurité anormaux hello, y compris la nature hello d’activités anormales de hello, nom de la base de données, nom du serveur, nom de l’application et heure de l’événement hello. En outre, par courrier électronique hello fournit des informations sur les causes possibles et recommandé actions tooinvestigate et atténuer la base de données du toohello de menaces potentielles hello.<br/>
     
    ![Volet de navigation][4]
2. alerte par courrier électronique de Hello comprend un journal d’Audit SQL de toohello lien direct. En cliquant sur cette hello lance de lien Azure portal et ouvre hello SQL les enregistrements d’Audit en temps hello d’événement de suspectes hello. Cliquez sur un tooview d’enregistrement d’audit plus de détails sur les activités de base de données suspecte hello, rend plus faciles instructions SQL toofind hello qui ont été exécutées (nom de l’utilisateur, qu’ils a et à quel moment) et déterminer si les événements hello était légitime ou malveillant (par exemple, application injection de tooSQL une vulnérabilité a été exploitée, un utilisateur une violation des données sensibles, etc.).<br/>
   ![Volet de navigation][5]


## <a name="explore-threat-detection-alerts-for-your-database-in-hello-azure-portal"></a>Explorer les alertes de détection des menaces pour votre base de données Bonjour portail Azure

SQL Database Threat Detection intègre ses alertes avec [Azure Security Center](https://azure.microsoft.com/en-us/services/security-center/). Une vignette de sécurité SQL dynamique dans le panneau de base de données hello dans l’état de hello assure le suivi du portail Azure hello de menaces actives. 

   ![Volet de navigation][6]
   
1. En cliquant sur la vignette de sécurité SQL hello lance le panneau des alertes Azure Security Center hello et fournit une vue d’ensemble de menaces SQL actives détecté sur la base de données hello. 

  ![Volet de navigation][7]

2. En cliquant sur une alerte spécifique, vous obtenez des détails supplémentaires et des actions permettant d’examiner cette menace et d’atténuer les menaces futures.

  ![Volet de navigation][8]


## <a name="next-steps"></a>Étapes suivantes

* En savoir plus sur la détection des menaces, visitez hello [blog Azure](https://azure.microsoft.com/en-us/blog/azure-sql-database-threat-detection-general-availability-in-spring-2017/) 
* En savoir plus sur [Audit Azure SQL Database](sql-database-auditing.md)
* En savoir plus sur [Azure Security Center](https://docs.microsoft.com/en-us/azure/security-center/security-center-intro)
* Pour plus d’informations sur la tarification, consultez hello [page de tarification de base de données SQL](https://azure.microsoft.com/en-us/pricing/details/sql-database/)  
* Pour obtenir un exemple de script PowerShell, consultez [Configurer l’audit et la détection des menaces avec PowerShell](scripts/sql-database-auditing-and-threat-detection-powershell.md).



<!--Image references-->
[1]: ./media/sql-database-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-database-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-database-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-database-threat-detection/4_td_email.png
[5]: ./media/sql-database-threat-detection/5_td_audit_record_details.png
[6]: ./media/sql-database-threat-detection/6_td_security_tile_view_alerts.png
[7]: ./media/sql-database-threat-detection/7_td_SQL_security_alerts_list.png
[8]: ./media/sql-database-threat-detection/8_td_SQL_security_alert_details.png


