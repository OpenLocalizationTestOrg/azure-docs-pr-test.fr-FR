---
title: "Démarrage rapide : création d’un serveur Azure Database pour MySQL à l’aide du portail Azure | Microsoft Docs"
description: "Cette procédure de l’article à l’aide hello tooquickly portail Azure créer un exemple de base de données Azure pour le serveur MySQL dans environ cinq minutes."
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.custom: mvc
ms.topic: hero-article
ms.date: 08/15/2017
ms.openlocfilehash: d5754fe7a6f0f0f4b3fa19d456c4e15e64ca396c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-mysql-server-using-azure-portal"></a>Création d’un serveur Azure Database pour MySQL à l’aide du portail Azure
Base de données Azure pour MySQL est un service géré qui vous permet de toorun, gérer et mettre à l’échelle des bases de données MySQL hautement disponibles dans le cloud de hello. Ce démarrage rapide vous montre comment toocreate Azure de base de données MySQL server à l’aide de hello portail Azure en cinq minutes environ. 

Si vous n’avez pas d’abonnement Azure, créez un compte [gratuit](https://azure.microsoft.com/free/) avant de commencer.

## <a name="log-in-tooazure"></a>Connectez-vous à tooAzure
Ouvrez votre navigateur web et accédez toohello [portail Microsoft Azure](https://portal.azure.com/). Entrez vos informations d’identification toosign dans toohello portal. affichage par défaut de Hello est votre tableau de bord de service.

## <a name="create-azure-database-for-mysql-server"></a>Créer un serveur de base de données Azure pour MySQL
Un serveur de base de données Azure pour MySQL est créé avec un ensemble défini de [ressources de calcul et de stockage](./concepts-compute-unit-and-storage.md). serveur de Hello est créé dans un [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md).

Suivez ces étapes de toocreate une base de données Azure pour le serveur MySQL :

1. Cliquez sur hello **nouveau** bouton (+) sur le coin supérieur gauche hello Hello portail Azure.

2. Sélectionnez **bases de données** de hello **nouveau** page, puis sélectionnez **base de données Azure pour MySQL** de hello **bases de données** page. Vous pouvez également taper **MySQL** Bonjour un service de hello de toofind de zone de recherche de page.
![Portail Azure - Nouveau - Base de données - MySQL](./media/quickstart-create-mysql-server-database-using-azure-portal/2_navigate-to-mysql.png)

3. Rempliront hello nouveau serveur détails avec hello suivant d’informations, comme indiqué dans le hello précédant l’image :

    **Paramètre** | **Valeur suggérée** | **Description du champ** 
    ---|---|---
    Nom du serveur | myserver4demo | Choisissez un nom unique qui identifie votre serveur de base de données Azure pour MySQL. nom de domaine Hello *mysql.database.azure.com* est ajouté toohello nom de serveur vous fournissez pour tooconnect d’applications pour. nom du serveur Hello peut contenir uniquement des lettres minuscules, des chiffres et des caractères de trait d’union (-) hello, et il doit contenir entre 3 et 63 caractères.
    Abonnement | Votre abonnement | Hello abonnement Azure que vous souhaitez toouse pour votre serveur. Si vous avez plusieurs abonnements, choisissez abonnement approprié de hello dans lequel les ressources hello sont facturé pour.
    Groupe de ressources | myResourceGroup | Vous pouvez définir un nouveau nom de groupe de ressources ou utiliser un nom de groupe existant dans votre abonnement.
    Connexion d’administrateur serveur | myadmin | Vérifiez votre propre toouse de compte de connexion lors de la connexion toohello server. nom de connexion Hello admin ne peut pas être 'azure_superuser', « admin », « administrateur », « root », « invité » ou « public ».
    Mot de passe | *Votre choix* | Créer un nouveau mot de passe pour le compte d’administrateur serveur hello. Doit contenir entre 8 caractères too128. Votre mot de passe doit contenir des caractères appartenant à trois des hello suivant catégories : majuscules des lettres, des lettres minuscules, des chiffres (0-9) et des caractères non alphanumériques ( !, $, #, %, etc..).
    Confirmer le mot de passe | *Votre choix*| Confirmer le mot de passe administrateur hello.
    Lieu | *utilisateurs tooyour le plus proche Hello région*| Choisissez un emplacement hello qui est le plus proche tooyour utilisateurs ou autres applications Azure.
    Version | *Choisissez la version la plus récente hello*| Choisissez la version la plus récente hello, sauf si vous avez des exigences spécifiques.
    Niveau de tarification | **De base**, **50 unités de calcul****50 Go** | Cliquez sur **niveau tarifaire** toospecify hello performances et la couche de niveau de service pour votre nouvelle base de données. Choisissez **le niveau de base** dans l’onglet hello haut hello. Cliquez sur le côté gauche de hello Hello **unités de calcul** curseur tooadjust hello valeur toohello moins le montant disponible pour ce démarrage rapide. Cliquez sur **Ok** hello toosave sélection de niveau de tarification. Consultez hello suivant capture d’écran.
    Code confidentiel toodashboard | Vérification | Vérifiez hello **toodashboard du code confidentiel** option tooallow simplifier le suivi de votre serveur sur la page de tableau de bord avant hello de votre portail Azure.

    > [!IMPORTANT]
    > connexion administrateur de serveur Hello et un mot de passe que vous spécifiez ici sont requis toolog dans toohello server et ses bases de données plus loin dans ce démarrage rapide. Retenez ou enregistrez ces informations pour une utilisation ultérieure.
    > 

    ![Portail Azure - créer MySQL en fournissant l’entrée du formulaire hello requis](./media/quickstart-create-mysql-server-database-using-azure-portal/3_create-server.png)

4.  Cliquez sur **créer** serveur hello de tooprovision. Configuration prend quelques minutes, des too20 minutes maximum.
   
5.  Dans la barre d’outils de hello, cliquez sur **Notifications** processus de déploiement de hello toomonitor (icône représentant une cloche).

## <a name="configure-a-server-level-firewall-rule"></a>Configurer une règle de pare-feu au niveau du serveur

Bonjour Azure de base de données pour le service MySQL crée un pare-feu au niveau serveur hello. Ce pare-feu empêche des applications externes et des outils de connexion toohello serveur et les bases de données sur le serveur de hello, sauf si une règle de pare-feu est créée le pare-feu tooopen hello pour des adresses IP spécifiques. 

1.  Localisez votre serveur une fois hello déploiement terminé. Si nécessaire, vous pouvez le rechercher. Par exemple, cliquez sur **toutes les ressources** de menu à gauche hello et tapez nom du serveur hello (exemple hello *myserver4demo*) toosearch pour votre serveur nouvellement créé. Cliquez sur le nom de votre serveur répertorié dans les résultats de recherche hello. Hello **vue d’ensemble** pour votre serveur s’ouvre et fournit des options pour poursuivre la configuration de la page.

2. Dans la page hello du serveur, sélectionnez **sécurité de connexion**.

3.  Sous hello **des règles de pare-feu** en-tête, cliquez dans la zone de texte vide hello Bonjour **nom de la règle** toobegin colonne création de règle de pare-feu hello. 

    Pour ce démarrage rapide, nous allons autoriser toutes les adresses IP dans le serveur de hello en remplissant la zone de texte hello dans chaque colonne avec hello valeurs suivantes :

    Nom de la règle | Adresse IP de début | Adresse IP de fin 
    ---|---|---
    AllowAllIps |  0.0.0.0 | 255.255.255.255

4. Sur la barre d’outils supérieure de hello Hello **sécurité de connexion** , cliquez sur **enregistrer**. Attendez quelques instants et message hello notification indiquant que la mise à jour de sécurité de connexion s’est correctement terminé avant de continuer.

    > [!NOTE]
    > TooAzure de connexions de base de données de MySQL communiquent via le port 3306. Si vous essayez de tooconnect à partir d’un réseau d’entreprise, le trafic sortant sur le port 3306 ne peut pas être autorisé par le pare-feu de votre réseau. Dans ce cas, vous ne serez pas en mesure de tooconnect tooyour serveur, sauf si votre service informatique ouvre le port 3306.
    > 

## <a name="get-hello-connection-information"></a>Obtenir des informations de connexion hello
serveur de base de données tooconnect tooyour, vous devez tooremember hello serveur complet administration et le nom d’identification. Il pouvez que vous avez noté ces valeurs plus haut dans l’article de démarrage rapide de hello. Dans le cas où vous n’avez pas, vous pouvez facilement trouver les serveur hello informations de nom et la connexion à partir du serveur de hello **vue d’ensemble** page ou hello **propriétés** page Bonjour portail Azure.

1. Ouvrez la page **Vue d’ensemble** de votre serveur. Prenez note de hello **nom du serveur** et **nom de connexion de serveur admin**. 
    Placez votre curseur dans chaque champ et icône de copie hello s’affiche à droite de toohello de texte hello. Cliquez sur icône de copie hello en tant que valeurs de hello toocopy nécessaires.

    Dans cet exemple, le nom du serveur hello est *myserver4demo.mysql.database.azure.com*, et de la connexion administrateur de serveur hello est  *myadmin@myserver4demo* .

## <a name="connect-toomysql-using-mysql-command-line-tool"></a>Se connecter à l’aide d’outil de ligne de commande mysql de tooMySQL
Il existe un certain nombre d’applications, vous pouvez utiliser tooconnect tooyour base de données Azure pour le serveur MySQL. Nous allons d’abord utiliser hello [mysql](https://dev.mysql.com/doc/refman/5.7/en/mysql.html) de ligne de commande outil tooillustrate comment tooconnect toohello server.  Vous pouvez utiliser un navigateur web et hello Azure Cloud Shell comme décrit ici sans hello doivent tooinstall des logiciels supplémentaires. Si vous avez hello mysql utilitaire est installé localement sur votre propre ordinateur, vous pouvez vous connecter à partir de là également.

1. Lancez hello Azure Cloud Shell via l’icône de terminal hello (> _) sur hello haut à droite de la page web du portail Azure de hello.

2. Bonjour Azure Cloud Shell s’ouvre dans votre navigateur, l’activation de commandes d’environnement tootype bash.

    ![Invite de commandes - Exemple de ligne de commande mysql](./media/quickstart-create-mysql-server-database-using-azure-portal/7_connect-to-server.png)

3. Invite hello Cloud, se connecter tooyour base de données Azure pour MySQL server en tapant la ligne de commande mysql hello invite hello vert.

    Hello, suivant le format est utilisé tooconnect tooan base de données Azure pour le serveur MySQL avec l’utilitaire de mysql hello :
    ```bash
    mysql --host <yourserver> --user <server admin login> --password
    ```

    Par exemple, hello commande suivante établit une connexion tooour exemple de serveur :
    ```azurecli-interactive
    mysql --host myserver4demo.mysql.database.azure.com --user myadmin@myserver4demo --password
    ```

    Paramètre mysql |Valeur suggérée|Description
    ---|---|---
    --host | *nom du serveur* | Spécifiez la valeur de nom de serveur hello utilisé lorsque vous avez créé précédemment des hello de base de données Azure pour MySQL. Le serveur que nous utilisons dans notre exemple est myserver4demo.mysql.database.azure.com. Utilisez le nom de domaine complet hello (\*. mysql.database.azure.com) comme indiqué dans l’exemple de hello. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom de votre serveur. 
    --user | *nom de connexion d’administrateur du serveur* |Tapez hello server connexion nom d’utilisateur administrateur fourni lorsque vous avez créé précédemment des hello de base de données Azure pour MySQL. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom d’utilisateur hello.  format de Hello est  *username@servername* .
    --password | *patienter jusqu’à être invité* | Vous serez invité trop « Entrez un mot de passe » après vous entrez la commande hello. Lorsque vous y êtes invité, tapez Bonjour même mot de passe que vous avez fourni lors de la création du serveur de hello.  Hello de note entré caractères ne figurent pas dans un interpréteur de commandes hello invite lorsque vous les tapez un mot de passe. Appuyez sur entrée une fois que vous avez tapé tous les tooauthenticate de caractères hello et vous connecter.

   Une fois connecté, utilitaire de mysql hello affiche un `mysql>` vous tootype commandes invite de commandes. 

    Exemple de sortie mysql :
    ```bash
    Welcome toohello MySQL monitor.  Commands end with ; or \g.
    Your MySQL connection id is 65505
    Server version: 5.6.26.0 MySQL Community Server (GPL)
    
    Copyright (c) 2000, 2017, Oracle and/or its affiliates. All rights reserved.
    
    Oracle is a registered trademark of Oracle Corporation and/or its
    affiliates. Other names may be trademarks of their respective
    owners.

    Type 'help;' or '\h' for help. Type '\c' tooclear hello current input statement.
    
    mysql>
    ```
    > [!TIP]
    > Si le pare-feu hello n’est pas configuré les adresse IP tooallow hello hello Azure Cloud Shell, hello erreur suivante se produit :
    >
    > ERREUR 2003 (28000) : Le Client avec l’adresse IP 123.456.789.0 n’est pas autorisé serveur hello de tooaccess.
    >
    > Erreur de hello tooresolve, vérifiez que hello server configuration correspondances hello étapes Bonjour *configurer une règle de pare-feu de niveau serveur* section de l’article de hello.

4. Vue serveur état tooensure hello connexion fonctionne. Type `status` à hello mysql > demander une fois qu’il est connecté.
    ```sql
    status
    ```

   > [!TIP]
   > Pour les autres commandes, consultez le [Manuel de référence de MySQL 5.7 - Chapitre 4.5.1](https://dev.mysql.com/doc/refman/5.7/en/mysql.html).

5.  Créer une base de données vide à hello mysql > invite de commandes en tapant hello de commande suivante :
    ```sql
    CREATE DATABASE quickstartdb;
    ```
    commande Hello peut prendre quelques instants toocomplete. 

    Dans un serveur Azure Database pour MySQL, vous pouvez créer une ou plusieurs bases de données. Vous pouvez choisir toocreate une base de données par serveur tooutilize toutes les ressources hello ou créer plusieurs bases de données tooshare les ressources hello. Il n’existe aucun toohello limiter le nombre de bases de données qui peuvent être créés, mais plusieurs bases de données partagent hello même ressources du serveur. 

6. Liste des bases de données hello hello mysql > invite de commandes en tapant hello de commande suivante :

    ```sql
    SHOW DATABASES;
    ```

7.  Type `\q` , puis appuyez sur outil de mysql entrée tooquit hello. Vous pouvez fermer hello Azure Cloud Shell une fois que vous avez terminé.

Vous avez maintenant connecté toohello base de données Azure pour MySQL et créé une base de données utilisateur vide. Continuer toohello suivant section toorepeat un toohello de tooconnect exercice similaire même serveur à l’aide d’un autre outil commun, le banc d’essai MySQL.

## <a name="connect-toohello-server-using-hello-mysql-workbench-gui-tool"></a>Connexion serveur toohello à l’aide d’outil d’interface utilisateur graphique de banc d’essai MySQL hello
tooconnect tooAzure MySQL server à l’aide de l’outil hello GUI banc d’essai MySQL :

1.  Lancez hello application banc d’essai MySQL sur votre ordinateur client. Vous pouvez télécharger et installer MySQL Workbench à partir [d’ici](https://dev.mysql.com/downloads/workbench/).

2.  Dans **le programme d’installation nouvelle connexion** boîte de dialogue, entrez hello suivant des informations sur la zone **paramètres** onglet :

    ![configurer une nouvelle connexion](./media/quickstart-create-mysql-server-database-using-azure-portal/setup-new-connection.png)

    | **Paramètre** | **Valeur suggérée** | **Description du champ** |
    |---|---|---|
    |   Nom de connexion | Connexion démo | Spécifiez une étiquette pour cette connexion. |
    | Méthode de connexion | Standard (TCP/IP) | Standard (TCP/IP) est suffisant. |
    | Nom d’hôte | *nom du serveur* | Spécifiez la valeur de nom de serveur hello utilisé lorsque vous avez créé précédemment des hello de base de données Azure pour MySQL. Le serveur que nous utilisons dans notre exemple est myserver4demo.mysql.database.azure.com. Utilisez le nom de domaine complet hello (\*. mysql.database.azure.com) comme indiqué dans l’exemple de hello. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom de votre serveur.  |
    | Port | 3306 | Utilisez toujours le port 3306 lors de la connexion de base de données de tooAzure pour MySQL. |
    | Nom d’utilisateur |  *nom de connexion d’administrateur du serveur* | Tapez hello server connexion nom d’utilisateur administrateur fourni lorsque vous avez créé précédemment des hello de base de données Azure pour MySQL. Le nom d’utilisateur dans notre exemple est myadmin@myserver4demo. Suivez les étapes de hello dans les informations de connexion du hello tooget de la section précédente hello si vous ne vous souvenez pas de nom d’utilisateur hello. format de Hello est  *username@servername* .
    | Mot de passe | votre mot de passe | Cliquez sur stocker dans le coffre de mot de passe de bouton toosave hello.... |

    Cliquez sur **tester la connexion** tootest si tous les paramètres sont configurés correctement. Cliquez sur OK toosave hello connexion. 

    > [!NOTE]
    > SSL est appliqué par défaut sur votre serveur et nécessite une configuration supplémentaire dans l’ordre tooconnect avec succès. Consultez [tooAzure base de données de connexion de connectivité configurez SSL dans votre application de toosecurely pour MySQL](./howto-configure-ssl.md).  Si vous souhaitez toodisable SSL pour ce démarrage rapide, visitez hello portail Azure et cliquez sur hello connexion sécurité page toodisable hello SSL d’appliquer la connexion bascule.

## <a name="clean-up-resources"></a>Supprimer des ressources
Nettoyer les ressources hello vous avez créé dans démarrage rapide de hello soit en supprimant hello [groupe de ressources Azure](../azure-resource-manager/resource-group-overview.md), qui inclut toutes les ressources hello dans le groupe de ressources hello ou en supprimant des ressources d’un serveur hello si vous souhaitez tookeep hello autres ressources intacts.

> [!TIP]
> Les autres démarrages rapides de cette collection reposent sur ce démarrage rapide. Si vous prévoyez toocontinue toowork avec ultérieures Démarrages rapides, effectuez pas nettoyer les hello ressources créées dans ce démarrage rapide. Si vous n’envisagez pas de toocontinue, utilisez hello suivant toodelete suit toutes les ressources créées par ce démarrage rapide Bonjour portail Azure.
>

groupe de ressource entier hello toodelete y compris les serveur hello nouvellement créé :
1.  Bonjour portail Azure, recherchez votre groupe de ressources. À partir du menu de gauche hello Bonjour portail Azure, cliquez sur **groupes de ressources** puis cliquez sur le nom de votre groupe de ressources, telles que notre exemple hello du **myresourcegroup**.
2.  Sur la page de votre groupe de ressources, cliquez sur **Supprimer**. Puis hello nom du type de votre groupe de ressources, telles que notre exemple **myresourcegroup**, en hello suppression de tooconfirm de zone de texte, puis cliquez sur **supprimer**.

Ou, au lieu de cela, toodelete hello créé récemment serveur :
1.  Localisez votre serveur Bonjour portail Azure, si vous ne pas les connaissez ouvrir. Hello menu de gauche dans le portail Azure, cliquez sur **toutes les ressources**, puis recherchez serveur hello vous avez créé.
2.  Sur hello **vue d’ensemble** , cliquez sur hello **supprimer** bouton dans le volet supérieur de hello.
![Base de données Azure pour MySQL : Supprimer le serveur](./media/quickstart-create-mysql-server-database-using-azure-portal/delete-server.png)
3.  Confirmez le nom du serveur hello souhaité toodelete, afficher hello bases de données dans cette section sont affectées. Tapez le nom de votre serveur dans la zone de texte hello, tels que notre exemple **myserver4demo**, puis cliquez sur **supprimer**.

## <a name="next-steps"></a>Étapes suivantes

> [!div class="nextstepaction"]
> [Concevoir votre première base de données Azure pour MySQL](./tutorial-design-database-using-portal.md)

