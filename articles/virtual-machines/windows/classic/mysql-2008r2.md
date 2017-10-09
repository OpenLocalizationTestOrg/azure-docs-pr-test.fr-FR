---
title: "aaaCreate une machine virtuelle de Azure classique qui exécute MySQL | Documents Microsoft"
description: "Créer une machine virtuelle Azure exécutant Windows Server 2012 R2 et hello à l’aide du modèle de déploiement classique hello de la base de données MySQL."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 98fa06d2-9b92-4d05-ac16-3f8e9fd4feaa
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: cynthn
ms.openlocfilehash: 2c9564955c2bab197a8e494e939ce16c0b9bb605
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-mysql-on-a-virtual-machine-created-with-hello-classic-deployment-model-running-windows-server-2016"></a>Installer MySQL sur un ordinateur virtuel créé avec le modèle de déploiement classique hello exécutant Windows Server 2016
[MySQL](https://www.mysql.com) est une base de données SQL open source connue. Ce didacticiel vous montre comment hello tooinstall et exécutez **version community de MySQL 5.7.18** comme un serveur MySQL sur un ordinateur virtuel en cours d’exécution **Windows Server 2016**. Votre expérience peut être légèrement différente sur d’autres versions de MySQL ou Windows Server.

Pour obtenir des instructions sur l’installation de MySQL sur Linux, reportez-vous à : [comment tooinstall MySQL sur Azure](../../linux/mysql-install.md).

> [!IMPORTANT]
> Azure dispose de deux modèles de déploiement différents pour créer et utiliser des ressources : [le déploiement Resource Manager et le déploiement classique](../../../resource-manager-deployment-model.md). Cet article décrit à l’aide du modèle de déploiement classique hello. Microsoft recommande que la plupart des nouveaux déploiements de modèle du Gestionnaire de ressources hello.

## <a name="create-a-virtual-machine-running-windows-server-2016"></a>Création d’une machine virtuelle exécutant Windows Server 2016
Si vous n’avez pas déjà une machine virtuelle exécutant Windows Server 2016, vous pouvez utiliser cette [didacticiel](./tutorial.md) toocreate hello virtual machine.

## <a name="attach-a-data-disk"></a>Association d’un disque de données
Après la création de la machine virtuelle de hello, vous pouvez éventuellement attacher un disque de données. Ajout de qu'un disque de données est recommandé pour les charges de production et tooavoid manque d’espace sur hello le lecteur du système d’exploitation (c), qui inclut de système d’exploitation de hello.

Consultez [tooattach données de l’ordinateur virtuel Windows tooa disque](../attach-managed-disk-portal.md) et suivez les instructions de hello pour attacher un disque vide. Hello hôte cache paramètre défini trop**aucun** ou **en lecture seule**.

## <a name="log-on-toohello-virtual-machine"></a>Ouvrez une session sur l’ordinateur virtuel de toohello
Ensuite, vous allez [ouvrir une session sur l’ordinateur virtuel de toohello](./connect-logon.md) afin que vous pouvez installer MySQL.

## <a name="install-and-run-mysql-community-server-on-hello-virtual-machine"></a>Installer et exécuter le serveur MySQL de la Communauté sur l’ordinateur virtuel de hello
Suivez ces étapes tooinstall, configurer et exécuter la version de communauté hello de MySQL Server :

> [!NOTE]
> Lors du téléchargement des éléments à l’aide d’Internet Explorer, vous pouvez définir hello IE **Configuration de sécurité renforcée** tooOff et simplifier hello du processus de téléchargement. À partir du menu Démarrer de hello, cliquez sur le serveur/Local du Gestionnaire de serveur des outils d’administration, puis cliquez sur Internet Explorer **Configuration de sécurité renforcée** et définissez hello configuration tooOff).
>
>

1. Une fois que vous vous êtes connecté l’ordinateur virtuel de toohello à l’aide du Bureau à distance, cliquez sur **Internet Explorer** à partir de l’écran d’accueil hello.
2. Sélectionnez hello **outils** situé dans le coin supérieur droit de hello (icône de roue cogged hello), puis cliquez sur **Options Internet**. Cliquez sur hello **sécurité** , cliquez sur hello **Sites de confiance** icône, puis cliquez sur hello **Sites** bouton. Ajouter la liste de toohello http://*.mysql.com des sites de confiance. Cliquez sur **Fermer**, puis sur **OK**.
3. Dans hello barre d’adresse d’Internet Explorer, tapez https://dev.mysql.com/downloads/mysql/.
4. Utilisez hello MySQL site toolocate et télécharger la version la plus récente de hello MySQL Installer pour Windows hello. Lorsque vous choisissez hello MySQL Installer, téléchargez la version hello ayant hello terminer le jeu de fichiers (par exemple, hello mysql-programme d’installation-Communauté-5.7.18.0.msi avec une taille de fichier de 352.8 Mo) et enregistrer le programme d’installation hello.
5. Lorsque le programme d’installation hello a terminé le téléchargement, cliquez sur **exécuter** toolaunch le programme d’installation.
6. Sur hello **contrat de licence** page, acceptez le contrat de licence hello et cliquez sur **suivant**.
7. Sur hello **en choisissant un Type d’installation** , cliquez sur le type d’installation hello que vous souhaitez, puis cliquez sur **suivant**. Hello étapes suivantes supposent que la sélection de hello hello **serveur uniquement** type d’installation.
8. Si hello **vérifier les exigences** affiche, cliquez sur **Execute** le programme d’installation de toolet hello installe les composants manquants. Suivez les instructions qui affichent, tels que les runtime C++ Redistributable hello.
9. Sur hello **Installation** , cliquez sur **Execute**. Une fois l’installation terminée, cliquez sur **Suivant**.

10. Sur hello **Configuration du produit** , cliquez sur **suivant**.

11. Sur hello **mise en réseau et Type** page, spécifiez les options de connectivité et le type de configuration souhaitée, y compris le port TCP hello si nécessaire. Sélectionnez **Afficher les options avancées**, puis cliquez sur **Suivant**.
    ![](./media/mysql-2008r2/MySQL_TypeNetworking.png)

12. Sur hello **comptes et des rôles** , spécifiez un mot de passe fort MySQL racine. Ajoutez des comptes d’utilisateurs MySQL si nécessaire, puis cliquez sur **Suivant**.

    ![](./media/mysql-2008r2/MySQL_AccountsRoles_Filled.png)
13. Sur hello **Windows Service** page, spécifiez modifie les paramètres par défaut toohello pour l’exécution de hello MySQL Server comme un service Windows en fonction des besoins, puis cliquez sur **suivant**.

    ![](./media/mysql-2008r2/MySQL_WindowsService.png)
14. Hello choix sur hello **plug-ins et Extensions** page sont facultatifs. Cliquez sur **suivant** toocontinue.
15. Sur hello **Options avancées** page, spécifiez les options de toologging de modifications en fonction des besoins, puis cliquez sur **suivant**.

    ![](./media/mysql-2008r2/MySQL_AdvOptions.png)
16. Sur hello **appliquer la Configuration de serveur** , cliquez sur **Execute**. Lorsque les étapes de configuration hello sont terminées, cliquez sur **Terminer**.
17. Sur hello **Configuration du produit** , cliquez sur **suivant**.
18. Sur hello **Installation complète** , cliquez sur **tooClipboard de copier le journal** si vous souhaitez tooexamine ultérieurement, puis cliquez sur **Terminer**.
19. À partir de l’écran d’accueil hello, tapez **mysql**, puis cliquez sur **MySQL 5.7 de ligne de commande Client**.
20. Entrez le mot de passe hello racine que vous avez spécifié à l’étape 12, et vous voyez s’afficher une invite de commandes où vous pouvez émettre des commandes tooconfigure MySQL. Pour plus d’informations hello de commandes et la syntaxe, consultez [manuels de référence MySQL](https://dev.mysql.com/doc/refman/5.7/en/server-configuration.html).

    ![](./media/mysql-2008r2/MySQL_CommandPrompt.png)
21. Vous pouvez également configurer les paramètres par défaut configuration server, par exemple hello de base et les répertoires de données et les lecteurs. Pour plus d’informations, consultez la section [6.1.2 Paramètres par défaut de configuration du serveur](https://dev.mysql.com/doc/refman/5.7/en/server-configuration-defaults.html).

## <a name="configure-endpoints"></a>Configuration des points de terminaison

Pour les ordinateurs disponibles tooclient hello MySQL service toobe sur hello Internet, vous devez configurer un point de terminaison pour le port TCP de hello et créer une règle de pare-feu Windows. valeur de port par défaut Hello sur le serveur MySQL hello service écoute pour les clients de MySQL est 3306. Vous pouvez spécifier un autre port, tant que le port de hello est cohérent avec la valeur hello fourni sur hello **mise en réseau et Type** page (étape 11 de la procédure précédente de hello).

> [!NOTE]
> À des fins de production, envisagez de hello implications en matière de sécurité de fabrication de service des ordinateurs disponibles tooall hello serveur MySQL sur hello Internet. Vous pouvez définir l’hello d’adresses IP sources autorisées point de terminaison toouse hello avec une liste de contrôle d’accès (ACL). Pour plus d’informations, consultez [comment tooSet des points de terminaison tooa Machine virtuelle](setup-endpoints.md).
>
>

tooconfigure un point de terminaison pour hello service MySQL Server :

1. Bonjour portail Azure, cliquez sur **Machines virtuelles (classiques)**, cliquez sur nom hello de votre machine virtuelle de MySQL, puis cliquez sur **points de terminaison**.
2. Dans la barre de commandes hello, cliquez sur **ajouter**.
3. Sur hello **ajouter le point de terminaison** , tapez un nom unique pour **nom**.
4. Sélectionnez **TCP** en tant que protocole de hello.
5. Tapez le numéro de port hello, tel que **3306**, dans les deux **Port Public** et **Port privé**, puis cliquez sur **OK**.

## <a name="add-a-windows-firewall-rule-tooallow-mysql-traffic"></a>Ajouter un tooallow de règle de pare-feu Windows du trafic de MySQL
tooadd une règle de pare-feu Windows qui autorise le trafic MySQL hello Internet, exécutez hello suivant de commande à partir d’un _invite de commandes Windows PowerShell avec élévation de privilèges_ sur la machine virtuelle de hello MySQL server.

    New-NetFirewallRule -DisplayName "MySQL57" -Direction Inbound –Protocol TCP –LocalPort 3306 -Action Allow -Profile Public

## <a name="test-your-remote-connection"></a>Tester votre connexion à distance
service de tootest votre hello d’en cours d’exécution d’une connexion à distance toohello Azure VM MySQL Server, vous devez fournir le nom DNS de hello du service de cloud hello contenant hello VN.

1. Bonjour portail Azure, cliquez sur **Machines virtuelles (classiques)**, cliquez sur nom hello de votre machine virtuelle du serveur MySQL, puis cliquez sur **vue d’ensemble**.
2. Tableau de bord de machine virtuelle hello, notez hello **nom DNS** valeur. Voici un exemple :

   ![](media/mysql-2008r2/MySQL_DNSName.png)
3. À partir d’un ordinateur local exécutant MySQL ou hello MySQL client, exécutez hello suivant toolog de commande en tant qu’utilisateur MySQL.

     mysql -u <yourMysqlUsername> -p -h <yourDNSname>

   Par exemple, à l’aide de hello les nom d’utilisateur MySQL _dbadmin3_ et hello _testmysql.cloudapp.net_ de nom DNS pour l’ordinateur virtuel de hello, vous pouvez commencer à MySQL à l’aide de hello de commande suivante :

     mysql -u dbadmin3 -p -h testmysql.cloudapp.net

## <a name="next-steps"></a>Étapes suivantes
toolearn plus sur l’exécution de MySQL, consultez hello [Documentation MySQL](http://dev.mysql.com/doc/).
