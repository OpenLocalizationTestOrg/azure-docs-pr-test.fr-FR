---
title: "aaaGet main de la détection des menaces de l’entrepôt de données SQL"
description: "Comment tooget démarrer avec la détection des menaces"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: c9073dd9-6c62-4735-8457-dfb9f859c900
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: dec0b734849e7f52434e099db0b38fbf0bf6ad53
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-threat-detection"></a>Prise en main de la détection de menaces
> [!div class="op_single_selector"]
> * [Audit](sql-data-warehouse-auditing-overview.md)
> * [Détection de menaces](sql-data-warehouse-security-threat-detection.md)
> 
> 

## <a name="overview"></a>Vue d'ensemble
La détection des menaces détecte des activités de base de données anormales indiquant de base de données des toohello des menaces de sécurité potentielles. Threat Detection est disponible en version préliminaire et est pris en charge pour SQL Data Warehouse.

La détection des menaces fournit une nouvelle couche de sécurité, ce qui permet aux clients toodetect et de répond toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales. Les utilisateurs peuvent Explorer à l’aide d’événements suspects hello [audit de l’entrepôt de données SQL Azure](sql-data-warehouse-auditing-overview.md) toodetermine s’ils résultent d’une tentative de tooaccess, violation ou exploiter les données dans l’entrepôt de données hello.
La détection des menaces rend les menaces potentielles tooaddress simple toohello données de l’entrepôt sans hello besoin toobe un expert en sécurité ou gérer des systèmes de surveillance de la sécurité avancée.

Par exemple, il détecte certaines activités de base de données anormales indiquant des tentatives d’injection SQL potentielles. Injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données. Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs de saisie d’application, de violation ou de modification des données dans la base de données hello.

## <a name="set-up-threat-detection-for-your-database"></a>Configurer Threat Detection pour votre base de données
1. Lancement hello portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com).
2. Accédez à panneau de configuration toohello Hello souhaité toomonitor SQL Data Warehouse. Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**.
   
    ![Volet de navigation][1]
3. Bonjour **audit et la détection des menaces** activer Panneau de configuration **ON** l’audit, qui affiche les paramètres de détection de menace hello.
   
    ![Volet de navigation][2]
4. **Activez** la détection des menaces.
5. Configurez la liste hello d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités de l’entrepôt de données anormales.
6. Cliquez sur **enregistrer** Bonjour **détection d’audit et de menaces** toosave Panneau de configuration hello nouvelle ou mis à jour stratégie de détection des menaces et de l’audit.
   
    ![Volet de navigation][3]

## <a name="explore-anomalous-data-warehouse-activities-upon-detection-of-a-suspicious-event"></a>Explorer les activités anormales sur l'entrepôt de données en cas de détection d'un événement suspect
1. Vous recevrez une notification par courrier électronique lorsque des activités anormales sont détectées au niveau de la base de données. <br/>
   messagerie de Hello fournit des informations sur les événements de sécurité anormaux hello, y compris la nature hello d’activités anormales de hello, nom de la base de données, heure de serveur hello et de nom de l’événement. En outre, il fournit des informations sur les causes possibles et recommandé actions tooinvestigate et atténuer la base de données du toohello de menaces potentielles hello.<br/>
   
    ![Volet de navigation][4]
2. Dans le message électronique de hello, cliquez sur hello **le journal d’audit Azure SQL** lien lance hello portail classique Azure et afficher les enregistrements de l’audit pertinentes hello en temps hello d’événement de suspectes hello.
   
    ![Volet de navigation][5]
3. Cliquez sur hello audit enregistrements tooview plus de détails sur les activités de base de données suspecte hello comme instruction SQL, IP raison et le client d’échec.
   
    ![Volet de navigation][6]
4. Dans le panneau des enregistrements d’audit hello, cliquez sur **ouvrir dans Excel** tooopen un préconfiguré excel tooimport de modèle et d’exécuter une analyse plus approfondie du journal d’audit de hello en temps hello d’événement de suspectes hello.<br/>
   **Remarque :** dans Excel 2010 ou version ultérieure, Power Query et hello **combinaison rapide** paramètre est requis
   
    ![Volet de navigation][7]
5. tooconfigure hello **combinaison rapide** le paramètre - Bonjour **POWER QUERY** onglet de ruban, sélectionnez **Options** boîte de dialogue Options toodisplay hello. Sélectionnez la section de confidentialité hello et choisissez hello deuxième option - « Ignorer les niveaux de confidentialité hello et potentiellement améliorer les performances » :
   
    ![Volet de navigation][8]
6. les journaux d’audit tooload SQL, assurez-vous que hello les paramètres dans l’onglet Paramètres de hello sont correctement définies et puis sélectionnez hello 'Data' ruban et cliquez sur le bouton Actualiser tout de hello.
   
    ![Volet de navigation][9]
7. résultats de Hello s’affichent dans hello **les journaux d’Audit SQL** feuille qui vous permet d’effectuer une analyse toorun des activités anormales de hello qui ont été détectés et d’atténuer l’impact hello d’événement de sécurité hello dans votre application.

<!--Image references-->
[1]: ./media/sql-data-warehouse-security-threat-detection/1_td_click_on_settings.png
[2]: ./media/sql-data-warehouse-security-threat-detection/2_td_turn_on_auditing.png
[3]: ./media/sql-data-warehouse-security-threat-detection/3_td_turn_on_threat_detection.png
[4]: ./media/sql-data-warehouse-security-threat-detection/4_td_email.png
[5]: ./media/sql-data-warehouse-security-threat-detection/5_td_audit_records.png
[6]: ./media/sql-data-warehouse-security-threat-detection/6_td_audit_record_details.png
[7]: ./media/sql-data-warehouse-security-threat-detection/7_td_audit_records_open_excel.png
[8]: ./media/sql-data-warehouse-security-threat-detection/8_td_excel_fast_combine.png
[9]: ./media/sql-data-warehouse-security-threat-detection/9_td_excel_parameters.png
