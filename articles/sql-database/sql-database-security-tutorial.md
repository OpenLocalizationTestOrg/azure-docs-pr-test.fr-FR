---
title: "aaaSecure votre base de données SQL Azure | Documents Microsoft"
description: "En savoir plus sur les techniques et fonctionnalités toosecure votre base de données SQL Azure."
services: sql-database
documentationcenter: 
author: DRediske
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 06/28/2017
ms.author: daredis
ms.openlocfilehash: 1450d633d6f65faf1b8a2dc0dc7dfe996fb0719d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-azure-sql-database"></a>Sécuriser votre base de données SQL Azure

Base de données SQL protège vos données en limitant la base de données access tooyour à l’aide de règles de pare-feu, nécessitant des utilisateurs tooprove leur identité et autorisation toodata via les autorisations et les appartenances de rôle, ainsi que par le biais des mécanismes d’authentification sécurité de niveau ligne et masquage dynamique des données.

Vous pouvez améliorer la protection de hello de votre base de données contre les utilisateurs malveillants ou de tout accès non autorisé seulement quelques étapes simples. Ce didacticiel vous apprend à effectuer les opérations suivantes : 

> [!div class="checklist"]
> * Configurer des règles de pare-feu de niveau serveur pour votre serveur Bonjour portail Azure
> * Créer des règles de pare-feu pour votre base de données à l’aide de SSMS
> * Se connecter à l’aide d’une chaîne de connexion sécurisée de la base de données tooyour
> * Gérer l’accès des utilisateurs
> * Protéger vos données à l’aide du chiffrement
> * Activer l’audit Azure SQL Database
> * Activer la détection de menaces pour les bases de données SQL

Si vous ne disposez pas d’abonnement Azure, créez un [compte gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="prerequisites"></a>Composants requis

toocomplete ce didacticiel, assurez-vous que vous avez hello suivant :

- Version la plus récente installée hello de [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) (SSMS). 
- Microsoft Excel.
- Création d’un serveur SQL Azure et la base de données - voir [créer une base de données SQL Azure Bonjour Azure portal](sql-database-get-started-portal.md), [créer une seule base de données SQL Azure à l’aide de hello CLI d’Azure](sql-database-get-started-cli.md), et [Create a SQL Azure unique base de données à l’aide de PowerShell](sql-database-get-started-powershell.md). 

## <a name="log-in-toohello-azure-portal"></a>Ouvrez une session dans toohello portail Azure

Connectez-vous à toohello [portail Azure](https://portal.azure.com/).

## <a name="create-a-server-level-firewall-rule-in-hello-azure-portal"></a>Créer une règle de pare-feu de niveau serveur dans hello portail Azure

Les bases de données SQL sont protégées par un pare-feu dans Azure. Par défaut, toutes les connexions toohello serveur hello bases de données et à l’intérieur du serveur de hello sont rejetées à l’exception des connexions à partir d’autres services Azure. Pour plus d’informations, consultez [Règles de pare-feu au niveau du serveur et de la base de données d’Azure SQL Database](sql-database-firewall-configure.md).

une configuration plus sécurisée Hello est tooOFF de tooset « Autoriser l’accès tooAzure services ». Si vous devez tooconnect toohello base de données à partir d’un service cloud ou machine virtuelle Azure, vous devez créer un [adresse IP réservée](../virtual-network/virtual-networks-reserved-public-ip.md) et autoriser uniquement hello réservé accès par adresse IP via le pare-feu hello. 

Suivez ces étapes toocreate un [règle de pare-feu de niveau serveur de base de données SQL](sql-database-firewall-configure.md) pour vos connexions au serveur tooallow à partir d’une adresse IP spécifique. 

> [!NOTE]
> Si vous avez créé une base de données d’exemple dans Azure à l’aide d’un des didacticiels précédents de hello ou Démarrages rapides et sont effectuer ce didacticiel sur un ordinateur avec hello même adresse IP qu’il avait lorsque vous passé en revue ces didacticiels, vous pouvez ignorer cette étape car vous devrez déjà créé une règle de pare-feu de niveau serveur.
>

1. Cliquez sur **bases de données SQL** de hello gauche menu et cliquez sur hello base de données vous souhaitez que la règle de pare-feu hello tooconfigure pour sur hello **bases de données SQL** page. nom de serveur complet Hello page Vue d’ensemble de votre base de données ouvre, affichant vous hello entièrement (tel que **mynewserver-20170313.database.windows.net**) et fournit des options de configuration supplémentaire.

      ![règle de pare-feu de serveur](./media/sql-database-security-tutorial/server-firewall-rule.png) 

2. Cliquez sur **définir serveur pare-feu** barre d’outils hello comme indiqué dans l’image précédente de hello. Hello **des paramètres de pare-feu** page serveur de base de données SQL hello s’ouvre. 

3. Cliquez sur **ajouter l’adresse IP du client** hello barre d’outils tooadd hello adresse IP publique du portail de toohello connecté hello ordinateur avec ou entrer manuellement les règles de pare-feu hello, puis cliquez sur **enregistrer**.

      ![définir la règle de pare-feu de serveur](./media/sql-database-security-tutorial/server-firewall-rule-set.png) 

4. Cliquez sur **OK** puis cliquez sur hello **X** tooclose hello **des paramètres de pare-feu** page.

Vous pouvez maintenant vous connecter tooany de base de données de serveur de hello avec hello spécifié plage d’adresses IP ou adresse IP.

> [!NOTE]
> SQL Database communique par le biais du port 1433. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 1433 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, vous ne serez pas de serveur de base de données SQL Azure en mesure de tooconnect tooyour, sauf si votre service informatique s’ouvre le port 1433.
>

## <a name="create-a-database-level-firewall-rule-using-ssms"></a>Créer une règle de pare-feu au niveau de la base de données à l’aide de SSMS

Règles de pare-feu de niveau base de données vous activer les paramètres de pare-feu différent de toocreate pour différentes bases de données hello même pare-feu de serveur et toocreate logique les règles qui sont portables - c'est-à-dire qu’elles respectent les base de données hello pendant un [basculement ](sql-database-geo-replication-overview.md) plutôt que stockés sur le serveur SQL de hello. Règles de pare-feu de niveau base de données ne peuvent être configuré à l’aide d’instructions Transact-SQL et uniquement après avoir configuré la première règle de pare-feu de niveau serveur hello. Pour plus d’informations, consultez [Règles de pare-feu au niveau du serveur et de la base de données d’Azure SQL Database](sql-database-firewall-configure.md).

Suit ces toocreate suit une règle de pare-feu de base de données spécifique.

1. Se connecter à une base de données tooyour, par exemple à l’aide de [SQL Server Management Studio](./sql-database-connect-query-ssms.md).

2. Dans l’Explorateur d’objets, cliquez sur hello base de données tooadd un pare-feu pour la règle, puis cliquez sur **nouvelle requête**. Une fenêtre de requête vide s’ouvre tooyour connecté de base de données.

3. Dans la fenêtre de requête hello, modifiez des hello tooyour publique adresse IP, puis exécutez hello suivant la requête :

    ```sql
    EXECUTE sp_set_database_firewall_rule N'Example DB Rule','0.0.0.4','0.0.0.4';
    ```

4. Dans la barre d’outils de hello, cliquez sur **Execute** règle de pare-feu toocreate hello.

## <a name="view-how-tooconnect-an-application-tooyour-database-using-a-secure-connection-string"></a>Afficher comment tooconnect un tooyour de l’application de base de données à l’aide d’une chaîne de connexion sécurisée

tooensure une connexion sécurisée, chiffrée entre une application cliente et la base de données SQL, la chaîne de connexion hello a toobe configuré pour :

- demander une connexion chiffrée ;
- certificat de serveur hello toonot approbation. 

Cela établit une connexion à l’aide de la sécurité TLS (Transport Layer) et réduit les risques d’attaques de man-in-the-middle hello. Vous pouvez obtenir les chaînes de connexion correctement configuré pour votre base de données SQL pour les clients pris en charge à pilotes à partir de hello portail Azure comme pour ADO.net dans cette capture d’écran.

1. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page.

2. Sur hello **vue d’ensemble** pour votre base de données, cliquez sur **afficher les chaînes de connexion de base de données**.

3. Hello révision complète **ADO.NET** chaîne de connexion.

    ![Chaîne de connexion ADO.NET](./media/sql-database-security-tutorial/adonet-connection-string.png)

## <a name="creating-database-users"></a>Création d’utilisateurs de base de données

Avant de créer des utilisateurs, vous devez d’abord choisir l’un des deux types d’authentification pris en charge par Azure SQL Database : 

**L’authentification SQL**qui utilise le nom d’utilisateur et mot de passe pour les connexions et les utilisateurs qui ne sont valides uniquement dans hello le contexte d’une base de données spécifique au sein d’un serveur logique. 

**L’authentification Azure Active Directory**, qui utilise des identités gérées par Azure Active Directory. 

Si vous souhaitez toouse [Azure Active Directory](./sql-database-aad-authentication.md) tooauthenticate par rapport à la base de données SQL, un annuaire Azure Active Directory rempli doit exister avant de pouvoir continuer.

Suivez ces étapes toocreate un utilisateur à l’aide de l’authentification SQL :

1. Se connecter à une base de données tooyour, par exemple à l’aide de [SQL Server Management Studio](./sql-database-connect-query-ssms.md) à l’aide de vos informations d’identification administrateur de serveur.

2. Dans l’Explorateur d’objets, cliquez sur la base de données hello tooadd un nouvel utilisateur sur et cliquez sur **nouvelle requête**. Une fenêtre de requête vide s’ouvre toohello connecté de base de données sélectionnée.

3. Dans la fenêtre de requête hello, entrez hello suivant la requête :

    ```sql
    CREATE USER ApplicationUser WITH PASSWORD = 'YourStrongPassword1';
    ```

4. Dans la barre d’outils de hello, cliquez sur **Execute** utilisateur de hello toocreate.

5. Par défaut, utilisateur de hello peut se connecter toohello de base de données, mais ne comporte aucune donnée de tooread ou d’écriture des autorisations. toogrant toohello de ces autorisations utilisateur récemment créé, exécutez hello suivant les deux commandes dans une nouvelle fenêtre de requête

    ```sql
    ALTER ROLE db_datareader ADD MEMBER ApplicationUser;
    ALTER ROLE db_datawriter ADD MEMBER ApplicationUser;
    ```

Il s’agit des meilleures pratiques toocreate ces comptes non administrateurs à tooyour de niveau tooconnect hello de base de données de base de données, sauf si vous avez besoin de tooexecute les tâches d’administration telles que la création de nouveaux utilisateurs. Passez en revue hello [didacticiel d’Azure Active Directory](./sql-database-aad-authentication-configure.md) sur la façon de tooauthenticate à l’aide d’Azure Active Directory.


## <a name="protect-your-data-with-encryption"></a>Protéger vos données à l’aide du chiffrement

Chiffrement de données transparent de base de données SQL Azure (TDE) chiffre automatiquement vos données au repos, sans nécessiter des modifications toohello application l’accès aux hello base de données chiffrée. Pour les bases de données créées, TDE est activé par défaut. tooenable chiffrement transparent des données pour votre base de données ou un tooverify TDE est activé, procédez comme suit :

1. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 

2. Cliquez sur **chiffrement Transparent des données** tooopen page de configuration hello pour le chiffrement transparent des données.

    ![Chiffrement transparent des données](./media/sql-database-security-tutorial/transparent-data-encryption-enabled.png)

3. Si nécessaire, définissez **le chiffrement des données** tooON et cliquez sur **enregistrer**.

processus de chiffrement Hello démarre en arrière-plan de hello. Vous pouvez surveiller la progression hello à l’aide de base de données tooSQL connexion [SQL Server Management Studio](./sql-database-connect-query-ssms.md) en interrogeant la colonne encryption_state hello hello `sys.dm_database_encryption_keys` vue.

## <a name="enable-sql-database-auditing-if-necessary"></a>Activer l’audit Azure SQL Database, si nécessaire

Audit de base de données SQL Azure effectue le suivi des événements de base de données et les écrit le journal d’audit de tooan dans votre compte de stockage Azure. L’audit peut vous aider à respecter une conformité réglementaire, à comprendre l’activité de la base de données et à découvrir des discordances et anomalies susceptibles d’indiquer des violations potentielles de la sécurité. Suivez ces étapes de toocreate une stratégie d’audit par défaut pour votre base de données SQL :

1. Sélectionnez **bases de données SQL** hello menu de gauche, cliquez sur votre base de données sur hello **bases de données SQL** page. 

2. Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**. Notez que l’audit au niveau serveur est désactivée et qu’il existe un **afficher les paramètres du serveur** lien qui vous permet de tooview ou modifier les paramètres d’audit de serveur hello à partir de ce contexte.

    ![Panneau Audit](./media/sql-database-security-tutorial/auditing-get-started-settings.png)

3. Si vous préférez tooenable un type d’Audit (ou un emplacement ?) différent de hello celle spécifiée au niveau du serveur hello, activer **ON** l’audit, puis choisissez hello **Blob** du Type d’audit. Si l’audit des objets Blob de serveur est activé, audit de base de données configurée hello existe côte à côte avec l’audit du Blob serveur hello.

    ![Activer l’audit](./media/sql-database-security-tutorial/auditing-get-started-turn-on.png)

4. Sélectionnez **détails de stockage** tooopen hello Panneau de stockage des journaux d’Audit. Compte de stockage Azure hello sélectionnez où seront enregistrés les journaux et la période de rétention hello, après le hello anciens journaux seront supprimés, puis cliquez sur **OK** bas hello. 

   > [!TIP]
   > Utilisez hello même compte de stockage pour tous les hello tooget de bases de données audités meilleur parti de l’audit de hello des modèles de rapports.
   > 

5. Cliquez sur **Enregistrer**.

> [!IMPORTANT]
> Si vous souhaitez que les événements audité de hello toocustomize, cela via PowerShell ou l’API REST - consultez hello [Automation (PowerShell / de l’API REST)](sql-database-auditing.md#subheading-7) section pour plus d’informations.
>

## <a name="enable-sql-database-threat-detection"></a>Activer la détection de menaces pour les bases de données SQL

La détection des menaces fournit une nouvelle couche de sécurité, ce qui permet aux clients toodetect et de répond toopotential menaces qu’ils se produisent en fournissant des alertes de sécurité sur les activités anormales. Les utilisateurs peuvent Explorer à l’aide de l’audit de base de données SQL de toodetermine s’ils résultent d’une tooaccess de la tentative de violation ou exploitent les données dans la base de données hello d’événements suspects hello. La détection des menaces rend tooaddress simple potentiels menaces toohello base de données sans nécessité de hello toobe un expert en sécurité ou gérer des systèmes de surveillance de la sécurité avancée.
Par exemple, il détecte certaines activités de base de données anormales indiquant des tentatives d’injection SQL potentielles. Injection SQL est un des hello Web application problèmes de sécurité courants sur hello Internet, les applications utilisées tooattack piloté par les données. Les attaquants profiter d’application vulnérabilités tooinject des instructions SQL malveillantes dans les champs de saisie d’application, de violation ou de modification des données dans la base de données hello.

1. Accédez à panneau de configuration de toohello de base de données SQL toomonitor de hello. Dans le panneau des paramètres de hello, sélectionnez **audit et la détection des menaces**.

    ![Volet de navigation](./media/sql-database-security-tutorial/auditing-get-started-settings.png)
2. Bonjour **audit et la détection des menaces** activer Panneau de configuration **ON** l’audit, qui affiche les paramètres de détection de menace hello.

3. **Activez** la détection des menaces.

4. Configurez la liste hello d’adresses de messagerie qui recevront les alertes de sécurité lors de la détection des activités anormales base de données.

5. Cliquez sur **enregistrer** Bonjour **détection d’audit et de menaces** panneau toosave hello nouvelle ou mis à jour stratégie de détection des menaces et de l’audit.

    ![Volet de navigation](./media/sql-database-security-tutorial/td-turn-on-threat-detection.png)

    Si des activités de base de données anormales sont détectées, vous recevrez une notification par courrier électronique. messagerie de Hello fournit des informations sur les événements de sécurité anormaux hello, y compris la nature hello d’activités anormales de hello, nom de la base de données, heure de serveur hello et de nom de l’événement. En outre, il fournit des informations sur les causes possibles et recommandé actions tooinvestigate et atténuer la base de données du toohello de menaces potentielles hello. parcours étapes suivant de Hello vous guident dans le toodo devez vous recevez ce courrier électronique :

    ![Courrier électronique de détection de menaces](./media/sql-database-threat-detection-get-started/4_td_email.png)

6. Dans le message électronique de hello, cliquez sur hello **le journal d’audit Azure SQL** lien lance hello portail Azure et afficher les enregistrements d’audit pertinentes hello en temps hello d’événement de suspectes hello.

    ![Enregistrements d’audit](./media/sql-database-threat-detection-get-started/5_td_audit_records.png)

7. Cliquez sur hello audit enregistrements tooview plus de détails sur les activités de base de données suspecte hello comme instruction SQL, IP raison et le client d’échec.

    ![Détails des enregistrements](./media/sql-database-security-tutorial/6_td_audit_record_details.png)

8. Dans le panneau des enregistrements d’audit hello, cliquez sur **ouvrir dans Excel** tooopen un préconfiguré excel tooimport de modèle et d’exécuter une analyse plus approfondie du journal d’audit de hello en temps hello d’événement de suspectes hello.

    > [!NOTE]
    > Dans Excel 2010 ou version ultérieure, Power Query et hello **combinaison rapide** paramètre n’est requis.

    ![Ouvrir les enregistrements dans Excel](./media/sql-database-threat-detection-get-started/7_td_audit_records_open_excel.png)

9. tooconfigure hello **combinaison rapide** le paramètre - Bonjour **POWER QUERY** onglet de ruban, sélectionnez **Options** boîte de dialogue Options toodisplay hello. Sélectionnez la section de confidentialité hello et choisissez hello deuxième option - « Ignorer les niveaux de confidentialité hello et potentiellement améliorer les performances » :

    ![Combinaison rapide dans Excel](./media/sql-database-threat-detection-get-started/8_td_excel_fast_combine.png)

10. les journaux d’audit tooload SQL, assurez-vous que hello les paramètres dans l’onglet Paramètres de hello sont correctement définies et puis sélectionnez hello 'Data' ruban et cliquez sur le bouton Actualiser tout de hello.

    ![Paramètres Excel](./media/sql-database-threat-detection-get-started/9_td_excel_parameters.png)

11. résultats de Hello s’affichent dans hello **les journaux d’Audit SQL** feuille qui vous permet d’effectuer une analyse toorun des activités anormales de hello qui ont été détectés et d’atténuer l’impact hello d’événement de sécurité hello dans votre application.


## <a name="next-steps"></a>Étapes suivantes
Vous pouvez améliorer la protection de hello de votre base de données contre les utilisateurs malveillants ou de tout accès non autorisé seulement quelques étapes simples. Ce didacticiel vous apprend à effectuer les opérations suivantes : 

> [!div class="checklist"]
> * Définir des règles de pare-feu pour votre serveur et ou base de données
> * Se connecter à l’aide d’une chaîne de connexion sécurisée de la base de données tooyour
> * Gérer l’accès des utilisateurs
> * Protéger vos données à l’aide du chiffrement
> * Activer l’audit Azure SQL Database
> * Activer la détection de menaces pour les bases de données SQL

> [!div class="nextstepaction"]
>[Améliorer les performances des bases de données SQL](sql-database-performance-tutorial.md)

