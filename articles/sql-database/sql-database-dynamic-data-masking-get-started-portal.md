---
title: "Portail Azure : masquage de données dynamiques de base de données SQL | Microsoft Docs"
description: "Comment tooget démarrer avec la base de données SQL masquage dynamique des données Bonjour portail Azure"
services: sql-database
documentationcenter: 
author: ronitr
manager: jhubbard
editor: 
ms.assetid: "2"
ms.service: sql-database
ms.custom: security
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.date: 11/22/2016
ms.author: ronitr; ronmat
ms.openlocfilehash: 5c5f74682a15d42eceb78c3ca0705401e1ac0ae7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-sql-database-dynamic-data-masking-with-hello-azure-portal"></a>Prise en main de la base de données SQL masquage dynamique des données avec hello portail Azure

Cette rubrique vous montre comment tooimplement [masquage dynamique des données](sql-database-dynamic-data-masking-get-started.md) avec hello portail Azure. Vous pouvez également implémenter à l’aide du masquage dynamique des données [applets de commande de base de données SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).


## <a name="set-up-dynamic-data-masking-for-your-database-using-hello-azure-portal"></a>Configurer le masquage dynamique des données pour votre base de données à l’aide de hello portail Azure
1. Lancement hello portail Azure à l’adresse [https://portal.azure.com](https://portal.azure.com).
2. Accédez à panneau des paramètres de base de données hello qui inclut des données sensibles hello souhaité toomask toohello.
3. Cliquez sur hello **masquage dynamique des données** vignette qui lance hello **masquage dynamique des données** Panneau de configuration.
   
   * Ou bien, vous pouvez faire défiler toohello **Operations** et cliquez sur **masquage dynamique des données**.
     
     ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/4_ddm_settings_tile.png)<br/><br/>
4. Bonjour **masquage dynamique des données** Panneau de configuration que vous pouvez voir certaines colonnes de la base de données, ce moteur de recommandations hello a signalé de masquage. Dans commande tooaccept recommandations de hello, cliquez simplement sur **ajouter un masque** pour une ou plusieurs colonnes et un masque seront créés selon le type de valeur par défaut hello pour cette colonne. Vous pouvez modifier la fonction de masquage en cliquant sur la règle de masquage hello et en modifiant les hello champ format tooa autre format de votre choix de masquage de hello. Être vraiment tooclick **enregistrer** toosave vos paramètres.
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/5_ddm_recommendations.png)<br/><br/>
5. tooadd un masque pour n’importe quelle colonne dans votre base de données, en haut de hello Hello **masquage dynamique des données** cliquez sur Panneau de configuration **ajouter un masque** tooopen hello **ajouter une règle de masquage** Panneau de configuration
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/6_ddm_add_mask.png)<br/><br/>
6. Sélectionnez hello **schéma**, **Table** et **colonne** hello toodefine désigné du champ qui sera masqué.
7. Choisissez un **de masquage de Format de champ** à partir de la liste de hello des catégories de masquage des données sensibles.
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/7_ddm_mask_field_format.png)<br/><br/>        
8. Cliquez sur **enregistrer** dans les données de salutation règle panneau tooupdate hello ensemble de règles dans hello masquage dynamique des données stratégie de masquage de masques.
9. Les utilisateurs SQL de type hello ou identités AAD qui doivent être exclues du masquage et ont accès aux données sensibles de toohello non masquée. La liste d'utilisateurs doit être délimitée par des points-virgules. Notez que les utilisateurs disposant des privilèges d’administrateur ont toujours toohello accéder aux données non masquées d’origine.
   
    ![Volet de navigation](./media/sql-database-dynamic-data-masking-get-started/8_ddm_excluded_users.png)
   
   > [!TIP]
   > toomake il hello par conséquent, la couche d’application peut afficher des données sensibles pour les utilisateurs de l’application privilégiée, hello utilisateur SQL ou l’application de hello identité AAD utilise la base de données tooquery hello. Il est vivement recommandé que cette liste contient un nombre minimal de l’exposition aux utilisateurs privilégiés toominimize des données sensibles hello.
   > 
   > 
10. Cliquez sur **enregistrer** dans la stratégie de masquage de nouveau ou mis à jour de configuration panneau toosave hello de masquage des données hello.


## <a name="next-steps"></a>Étapes suivantes

* Pour une vue d’ensemble du masquage des données dynamiques, consultez [Masquage des données dynamiques](sql-database-dynamic-data-masking-get-started.md).
* Vous pouvez également implémenter à l’aide du masquage dynamique des données [applets de commande de base de données SQL Azure](https://msdn.microsoft.com/library/azure/mt574084.aspx) ou hello [API REST](https://msdn.microsoft.com/library/dn505719.aspx).
