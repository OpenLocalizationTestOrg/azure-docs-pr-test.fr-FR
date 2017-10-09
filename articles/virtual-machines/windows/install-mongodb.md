---
title: aaaInstall MongoDB sur un ordinateur virtuel Windows Azure | Documents Microsoft
description: "Découvrez comment tooinstall MongoDB sur une machine virtuelle de Azure exécutant Windows Server 2012 R2 est créé avec le modèle de déploiement du Gestionnaire de ressources hello."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: 53faf630-8da5-4955-8d0b-6e829bf30cba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: becd2c607d098e2bc806139e03f2c42f1f01f6f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-configure-mongodb-on-a-windows-vm-in-azure"></a>Installation et configuration de MongoDB sur une machine virtuelle Windows dans Azure
[MongoDB](http://www.mongodb.org) est une base de données NoSQL open-source qui offre des performances élevées. Cet article vous guide lors de l’installation et de la configuration de MongoDB sur une machine virtuelle Windows Server 2012 R2 (VM) dans Azure. Vous pouvez également [installer MongoDB sur une machine virtuelle Linux dans Azure](../linux/install-mongodb.md).

## <a name="prerequisites"></a>Composants requis
Avant d’installer et configurer MongoDB, vous devez toocreate une machine virtuelle et, dans l’idéal, ajoutez un tooit de disque de données. Consultez hello suivant articles toocreate une machine virtuelle et ajoutez un disque de données :

* Créer une machine virtuelle Windows Server à l’aide de [hello portail Azure](quick-create-portal.md) ou [Azure PowerShell](quick-create-powershell.md).
* Joindre des données disque tooa machine virtuelle Windows Server avec [hello portail Azure](attach-managed-disk-portal.md) ou [Azure PowerShell](attach-disk-ps.md).

toobegin installation et configuration MongoDB, [session tooyour machine virtuelle Windows Server](connect-logon.md) à l’aide du Bureau à distance.

## <a name="install-mongodb"></a>Installation de MongoDB
> [!IMPORTANT]
> Les fonctionnalités de sécurité MongoDB, comme l’authentification et la liaison d’adresse IP, ne sont pas activées par défaut. Les fonctionnalités de sécurité doivent être activées avant de déployer l’environnement de production tooa MongoDB. Pour en savoir plus, consultez la page [Sécurité et authentification pour MongoDB](http://www.mongodb.org/display/DOCS/Security+and+Authentication).


1. Une fois que vous avez connecté tooyour machine virtuelle en utilisant Bureau à distance, ouvrez Internet Explorer à partir de hello **Démarrer** menu hello machine virtuelle.
2. Sélectionnez **Utiliser les paramètres de sécurité, de confidentialité et de compatibilité recommandés** lorsque s’ouvre pour la première fois, puis cliquez sur **OK**.
3. La configuration de la sécurité renforcée d’Internet Explorer est activée par défaut. Ajoutez hello MongoDB site Web toohello liste des sites autorisés :
   
   * Sélectionnez hello **outils** icône dans le coin supérieur droit de hello.
   * Dans **Options Internet**, sélectionnez hello **sécurité** onglet et sélectionnez hello **Sites de confiance** icône.
   * Cliquez sur hello **Sites** bouton. Ajouter *https://\*. mongodb.org* toohello liste des sites de confiance, boîte de dialogue Fermer puis hello.
     
     ![Configuration des paramètres de sécurité Internet Explorer](./media/install-mongodb/configure-internet-explorer-security.png)
4. Parcourir toohello [MongoDB - téléchargements](http://www.mongodb.org/downloads) page (http://www.mongodb.org/downloads).
5. Si nécessaire, sélectionnez hello **serveur de la Communauté** edition et hello puis sélectionnez dernière stable version actuelle de Windows Server 2008 R2 64 bits et les versions ultérieures. toodownload hello du programme d’installation, cliquez sur **téléchargement (msi)**.
   
    ![Téléchargez le programme d’installation de MongoDB](./media/install-mongodb/download-mongodb.png)
   
    Exécuter le programme d’installation hello après que hello téléchargement est terminé.
6. Lisez et acceptez le contrat de licence hello. Lorsqu’une invite s’affiche, sélectionnez **Terminer** le programme d’installation.
7. Dans l’écran final de hello, cliquez sur **installer**.

## <a name="configure-hello-vm-and-mongodb"></a>Configurer hello VM et MongoDB
1. variables de chemin d’accès Hello ne sont pas mis à jour par le programme d’installation de hello MongoDB. Sans hello MongoDB `bin` emplacement dans votre variable de chemin d’accès, vous devez chemin d’accès complet de toospecify hello chaque fois que vous utilisez un fichier exécutable MongoDB. variable de chemin d’accès tooyour tooadd hello emplacement :
   
   * Avec le bouton hello **Démarrer** , puis sélectionnez **système**.
   * Cliquez sur **Paramètres système avancés**, puis cliquez sur **Variables d’environnement**.
   * Sous **Variables système**, sélectionnez **Chemin d’accès**, puis cliquez sur **Modifier**.
     
     ![Configurez les variables PATH](./media/install-mongodb/configure-path-variables.png)
     
     Ajouter le chemin d’accès de hello tooyour MongoDB `bin` dossier. MongoDB est généralement installé sur *C:\Program Files\MongoDB*. Vérifiez le chemin d’installation de hello sur votre machine virtuelle. exemple Hello ajoute hello par défaut MongoDB installation emplacement toohello `PATH` variable :
     
     ```
     ;C:\Program Files\MongoDB\Server\3.2\bin
     ```
     
     > [!NOTE]
     > Être vraiment tooadd hello début point-virgule (`;`) tooindicate que vous ajoutez un emplacement tooyour `PATH` variable.

2. Créez les répertoires de journaux et de données MongoDB sur votre disque dur. À partir de hello **Démarrer** menu, sélectionnez **invite de commandes**. Hello exemple suivant créer les répertoires hello sur le lecteur F:
   
    ```
    mkdir F:\MongoData
    mkdir F:\MongoLogs
    ```
3. Démarrer une instance de MongoDB avec hello commande suivante, l’ajustement des données de tooyour hello chemin d’accès et des journaux en conséquence :
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log
    ```
   
    Il peut prendre plusieurs minutes MongoDB tooallocate les fichiers de journal hello et commence à écouter les connexions. Tous les messages du journal sont suggéré toohello *F:\MongoLogs\mongolog.log* de fichiers `mongod.exe` serveur démarre et alloue des fichiers journaux.
   
   > [!NOTE]
   > invite de commandes Hello reste se concentrent sur cette tâche pendant l’exécution de votre instance de MongoDB. Laissez ouverte toocontinue hello invite de commandes fenêtre MongoDB en cours d’exécution. Ou bien, installez MongoDB en tant que service, comme indiqué dans l’étape suivante de hello.

4. Pour une expérience MongoDB plus robuste, installez hello `mongod.exe` en tant que service. Création d’un service signifie que vous n’avez pas besoin tooleave une invite de commandes en cours d’exécution chaque fois que vous toouse MongoDB. Créez le service de hello comme suit, ajustement hello données tooyour de chemin d’accès et des journaux en conséquence :
   
    ```
    mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log `
        --logappend  --install
    ```
   
    Hello commande précédente crée un service nommé MongoDB, avec une description de « Mongodb ». Hello paramètres suivants est également spécifiée :
   
   * Hello `--dbpath` option spécifie l’emplacement de hello hello du répertoire de données.
   * Hello `--logpath` option doit être toospecify utilisé un fichier journal, car le service en cours d’exécution de hello n’a pas une sortie toodisplay de la fenêtre commande.
   * Hello `--logappend` option spécifie qu’un redémarrage du service de hello, le fichier journal existant de sortie tooappend toohello.
   
   service de MongoDB hello toostart, exécutez hello de commande suivante :
   
    ```
    net start MongoDB
    ```
   
    Pour plus d’informations sur la création du service de MongoDB hello, consultez [configurer un Service Windows pour MongoDB](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-windows/#mongodb-as-a-windows-service).

## <a name="test-hello-mongodb-instance"></a>Instance de test hello MongoDB
Avec MongoDB lancé en tant qu’instance unique ou installé en tant que service, vous pouvez maintenant commencer la création et l’utilisation de vos bases de données. toostart hello MongoDB interpréteur de commandes d’administration, ouvrez une autre fenêtre d’invite de commandes à partir de hello **Démarrer** menu, puis entrez hello de commande suivante :

```
mongo  
```

Vous pouvez répertorier les bases de données hello hello `db` commande. Insérez des données comme suit :

```
db.foo.insert( { a : 1 } )
```

Recherchez des données comme suit :

```
db.foo.find()
```

Hello la sortie est similaire toohello l’exemple suivant :

```
{ "_id" : "ObjectId("57f6a86cee873a6232d74842"), "a" : 1 }
```

Hello de sortie `mongo` console comme suit :

```
exit
```

## <a name="configure-firewall-and-network-security-group-rules"></a>Configuration des règles de pare-feu et de groupe de sécurité réseau
Maintenant que MongoDB est installé et en cours d’exécution, ouvrir un port dans le pare-feu Windows pour vous connecter à distance tooMongoDB. toocreate un nouvelle règle de trafic entrant tooallow le port TCP 27017, ouvrez une invite PowerShell d’administration, puis entrez hello de commande suivante :

```powerahell
New-NetFirewallRule `
    -DisplayName "Allow MongoDB" `
    -Direction Inbound `
    -Protocol TCP `
    -LocalPort 27017 `
    -Action Allow
```

Vous pouvez également créer des règles de hello à l’aide de hello **pare-feu Windows avec fonctions avancées de sécurité** outil de gestion graphique. Créer un nouvelle règle de trafic entrant tooallow le port TCP 27017.

Si nécessaire, créez un groupe de sécurité réseau règle tooallow accès tooMongoDB d’en dehors du sous-réseau de réseau virtuel Azure existant hello. Vous pouvez créer des règles du groupe de sécurité réseau de hello à l’aide de hello [portail Azure](nsg-quickstart-portal.md) ou [Azure PowerShell](nsg-quickstart-powershell.md). Comme avec les règles de pare-feu Windows hello, autoriser l’interface de réseau virtuel TCP port 27017 toohello de votre VM MongoDB.

> [!NOTE]
> Le port TCP 27017 est le port par défaut de hello utilisé par MongoDB. Vous pouvez modifier ce port à l’aide de hello `--port` lors du démarrage de paramètre `mongod.exe` manuellement ou à partir d’un service. Si vous modifiez le port de hello, rendre que tooupdate hello pare-feu Windows et le groupe de sécurité réseau règles Bonjour étapes précédentes.


## <a name="next-steps"></a>Étapes suivantes
Dans ce didacticiel, vous avez appris comment tooinstall et configurer MongoDB sur votre machine virtuelle Windows. Vous pouvez désormais accéder aux MongoDB sur votre machine virtuelle Windows, en suivant hello rubriques Bonjour avancées [documentation MongoDB](https://docs.mongodb.com/manual/).

