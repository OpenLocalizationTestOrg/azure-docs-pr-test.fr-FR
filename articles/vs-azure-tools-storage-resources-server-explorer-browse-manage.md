---
title: "aaaBrowsing et la gestion des ressources de stockage avec l’Explorateur de serveurs | Documents Microsoft"
description: "Consultation et gestion des ressources de stockage avec l’Explorateur de serveurs"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>Consultation et gestion des ressources de stockage avec l’Explorateur de serveurs
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>Vue d'ensemble
Si vous avez installé hello Windows Azure Tools pour Microsoft Visual Studio, vous pouvez afficher des objets blob, file d’attente et des données de table à partir de vos comptes de stockage pour Azure. nœud de stockage Azure Hello dans l’Explorateur de serveurs affiche les données qui se trouve dans votre compte d’émulateur de stockage local et vos autres comptes de stockage Azure.

tooview l’Explorateur de serveurs dans Visual Studio, hello barre de menus, choisissez **vue**, **l’Explorateur de serveurs**. nœud de stockage Hello affiche tous les comptes de stockage hello qui existent sous chaque abonnement Azure/certificat qu'auquel vous êtes connecté. Si votre compte de stockage n’apparaît pas, vous pouvez l’ajouter en suivant les instructions hello [plus loin dans cette rubrique](#add-storage-accounts-by-using-server-explorer).

À partir de Azure SDK 2.7, vous pouvez également utiliser hello nouveau Cloud Explorer tooview et gérer vos ressources Azure. Pour plus d’informations, consultez [Gestion des ressources Azure avec Cloud Explorer](vs-azure-tools-resources-managing-with-cloud-explorer.md) .

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>Afficher et gérer les ressources de stockage dans Visual Studio
L’Explorateur de serveurs affiche automatiquement la liste des objets blob, des files d’attente et des tables de votre compte d’émulateur de stockage. compte d’émulateur de stockage Hello est répertorié dans l’Explorateur de serveurs sous le nœud de stockage hello comme hello **développement** nœud.

ressources de toosee hello émulateur du compte de stockage, développez hello **développement** nœud. Si l’émulateur de stockage hello n’a pas été démarré lorsque vous développez hello **développement** nœud, il démarre automatiquement. Le démarrage peut prendre plusieurs secondes. Vous pouvez continuer toowork dans d’autres zones de Visual Studio pendant le démarrage de l’émulateur de stockage hello.

tooview des ressources dans un compte de stockage, développez le nœud du compte de stockage hello dans l’Explorateur de serveurs. Hello suivant sous-nœuds s’affichent :

* Objets blob
* Files d’attente
* Tables

## <a name="work-with-blob-resources"></a>Utilisation des ressources d’objets blob
nœud d’objets BLOB Hello affiche une liste de conteneurs pour le compte de stockage hello sélectionné. Les conteneurs d’objets blob contiennent des fichiers d’objets blob, que vous pouvez ranger dans des dossiers et des sous-dossiers. Consultez [comment toouse stockage d’objets Blob à partir de .NET](storage/blobs/storage-dotnet-how-to-use-blobs.md) pour plus d’informations.

### <a name="toocreate-a-blob-container"></a>toocreate un conteneur d’objets blob
1. Menu contextuel Ouvrir hello hello **BLOB** nœud, puis choisissez **créer un conteneur d’objets Blob**.
2. Bonjour **créer un conteneur d’objets Blob** boîte de dialogue, entrez le nom hello de conteneur hello.  
3. Appuyez sur **entrée** sur votre clavier ou vous pouvez cliquer sur ou cliquez en dehors du conteneur d’objets blob hello nom champ toosave hello.
   
   > [!NOTE]
   > nom de conteneur Hello doit commencer par une lettre minuscule (a-z) ou un chiffre (0-9).
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete un conteneur d’objets blob
* Conteneur d’objets blob hello tooremove puis puis cliquez sur le menu contextuel Ouvrir hello **supprimer**.

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>toodisplay une liste d’éléments de hello contenus dans un conteneur d’objets blob
* Ouvrez le menu contextuel de hello pour un nom de conteneur dans la liste de hello, puis choisissez **ouvrir**.
  
    Lorsque vous affichez le contenu de hello d’un conteneur d’objets blob, il apparaît dans un onglet appelé hello vue du conteneur d’objets blob.
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    Vous pouvez effectuer hello suivant des opérations sur les objets BLOB à l’aide des boutons de hello dans hello en haut à droite de la vue du conteneur d’objets blob hello :
  
  * Entrer une valeur de filtre et l’appliquer
  * Actualiser la liste hello d’objets BLOB dans le conteneur de hello
  * Charger un fichier
  * Supprimer un objet blob
    
    > [!NOTE]
    > Suppression d’un fichier à partir d’un conteneur d’objets blob ne supprime pas les fichiers sous-jacents hello ; Il supprime uniquement de conteneur d’objets blob hello.
    > 
    > 
  * Ouvrir un objet blob
  * Enregistrer un ordinateur local de blob toohello

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate un dossier ou un sous-dossier dans un conteneur d’objets blob
1. Choisissez le conteneur d’objets blob hello dans Cloud Explorer. Dans la fenêtre du conteneur hello, choisissez hello **télécharger un objet Blob** bouton.
   
    ![Chargement d’un fichier dans un dossier d’objets blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. Bonjour **télécharger un nouveau fichier** boîte de dialogue, choisissez hello **Parcourir** bouton toospecify hello fichier souhaité tooupload, puis entrez un nom de dossier Bonjour **dossier (facultatif)** boîte .
   
    Vous pouvez ajouter des dossiers de conteneur en suivant les sous-dossiers hello même procédure. Si vous ne spécifiez pas un nom de dossier, fichier de hello sera téléchargé toohello de niveau supérieur du conteneur d’objets blob hello. fichier de Hello s’affiche dans le dossier spécifié de hello dans le conteneur de hello.
   
    ![Dossier ajouté tooa conteneur d’objets blob](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. Double-cliquez sur le dossier de hello ou appuyez sur entrée contenu de hello toosee du dossier de hello. Lorsque vous êtes dans le dossier du conteneur hello, vous pouvez naviguer racine toohello arrière du conteneur de hello en choisissant hello **ouvrir le répertoire Parent** (flèche haut) bouton.

### <a name="toodelete-a-container-folder"></a>toodelete un dossier conteneur
* Supprimer tous les fichiers hello dans le dossier de hello
  
  > [!NOTE]
  > Étant donné que les dossiers dans les conteneurs d’objets blob sont des dossiers virtuels, vous ne pouvez pas créer un dossier vide, ni supprimer un dossier toodelete son contenu du fichier. Vous avez toodelete hello tout contenu d’un dossier de hello toodelete.
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>BLOB toofilter dans un conteneur
Vous pouvez filtrer les objets BLOB hello qui sont affichés en spécifiant un préfixe commun.

Par exemple, si vous entrez le préfixe de hello `hello` dans hello de zone de texte de filtre, puis cliquez sur hello **Execute** (**!**) bouton, seuls les objets BLOB qui commencent par « hello » s’affichent.

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> champ de filtre Hello respecte la casse et ne prend en charge le filtrage avec des caractères génériques. Les objets blob ne peuvent être filtrés que par préfixe. préfixe de Hello peut-être inclure un délimiteur si vous utilisez un BLOB tooorganize de délimiteur dans une hiérarchie virtuelle. Par exemple, le filtrage sur hello préfixe HelloFabric / retourne tous les objets BLOB à partir de cette chaîne.
> 
> 

### <a name="toodownload-blob-data"></a>données d’objet blob toodownload
* Dans **Cloud Explorer**, ouvrir le menu contextuel de hello pour un ou plusieurs objets BLOB, puis sélectionnez **ouvrir**, ou choisissez le nom d’objet blob hello, puis hello **ouvrir** bouton ou double-cliquez sur nom d’objet blob Hello.
  
    Hello la progression du téléchargement d’un objet blob apparaît dans hello **journal des activités Azure** fenêtre.
  
    objet blob de Hello s’ouvre dans l’éditeur par défaut de hello pour ce type de fichier. Si le système d’exploitation de hello reconnaît le type de fichier hello, fichier de hello s’ouvre dans une application installée localement ; dans le cas contraire, vous êtes invité à entrer toochoose une application qui est appropriée pour le type de fichier hello d’objet blob de hello. fichier Hello local qui est créé lorsque vous téléchargez un objet blob est marqué comme étant en lecture seule.
  
    Données d’objet BLOB sont mis en cache localement et vérifiées hello pour heure de dernière modification l’objet blob Bonjour service Blob. Si l’objet blob de hello a été mis à jour depuis son dernier téléchargement, il sera de nouveau téléchargé ; Sinon, les objets blob de hello est chargée à partir du disque local de hello. Par défaut, un objet blob est le répertoire temporaire de tooa téléchargé. toodownload BLOB tooa spécifique directory hello sélectionné sur le menu contextuel hello ouvrir les noms d’objets blob et choisissez **Enregistrer sous**. Lorsque vous enregistrez un objet blob de cette manière, fichier d’objet blob hello n’est pas ouvert et les fichiers locaux hello sont créé avec les attributs en lecture-écriture.

### <a name="tooupload-blobs"></a>objets BLOB de tooupload
* Choisissez hello **télécharger un objet Blob** bouton lorsqu’un conteneur de hello est ouvert pour l’affichage dans la vue du conteneur d’objets blob hello.
  
    Vous pouvez choisir l’une ou plusieurs tooupload de fichiers et que vous pouvez télécharger des fichiers de n’importe quel type. Hello **journal des activités Azure** affiche hello la progression du téléchargement de hello. Pour plus d’informations sur la façon toowork avec les données blob, consultez [comment toouse hello Service de stockage d’objets Blob Azure dans .NET](http://go.microsoft.com/fwlink/p/?LinkId=267911).

### <a name="tooview-logs-transferred-tooblobs"></a>tooview journaux transférés tooblobs
* Si vous utilisez des données toolog de Diagnostics Windows Azure à partir de votre application Windows Azure et que vous avez transféré le compte de stockage de journaux tooyour, vous verrez des conteneurs qui ont été créés par Azure pour ces journaux. Affichant ces journaux dans l’Explorateur de serveurs d’est un problèmes de tooidentify facilement avec votre application, surtout si elle a été déployée tooAzure. Pour plus d’informations sur les diagnostics Azure, consultez [Collecte des données de journalisation avec les diagnostics Azure](https://msdn.microsoft.com/library/azure/gg433048.aspx).

### <a name="tooget-hello-url-for-a-blob"></a>URL de hello tooget pour un objet blob
* Ouvrez le menu contextuel de l’objet blob de hello, puis choisissez **copier l’URL**.

### <a name="tooedit-a-blob"></a>tooedit un objet blob
* Sélectionnez les objets blob de hello, puis choisissez hello **ouvrir l’objet Blob** bouton.
  
    fichier de Hello est téléchargés tooa un emplacement temporaire et ouvert sur l’ordinateur local de hello. Vous devez télécharger les blob hello à nouveau une fois que vous apportez des modifications.

## <a name="work-with-queue-resources"></a>Utiliser des ressources de file d’attente
Files d’attente de services de stockage sont hébergées dans un compte de stockage Azure et vous pouvez les utiliser tooallow votre toocommunicate de rôles de service cloud entre eux et avec d’autres services par un mécanisme de transmission de message. Vous pouvez accéder par programme à file d’attente hello via un service cloud et sur un service web pour les clients externes. Vous pouvez également accéder à la file d’attente de hello directement à l’aide de l’Explorateur de serveurs dans Visual Studio.

Lorsque vous développez un service cloud qui utilise des files d’attente, vous pouvez souhaitez que les files d’attente de toouse Visual Studio toocreate et fonctionner avec elles interactivement lorsque vous développez et testez votre code.

Dans l’Explorateur de serveurs, vous pouvez afficher les files d’attente hello dans un compte de stockage, créer et supprimer des files d’attente, ouvrir une file d’attente tooview ses messages et ajouter file d’attente de messages tooa. Lorsque vous ouvrez une file d’attente pour l’affichage, vous pouvez afficher les messages individuels hello, et vous pouvez effectuer hello suivant des actions de la file d’attente hello à l’aide des boutons de hello dans l’angle supérieur gauche de hello :

* Actualiser la vue hello de file d’attente hello
* Ajouter une file d’attente de messages toohello
* Retrait du message de salutation au premier plan
* Toute file d’attente de hello clair

Hello suivant image montre une file d’attente qui contient deux messages.

![Affichage d’une file d’attente](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

Pour plus d’informations sur le stockage des files d’attente de services, consultez [Comment : hello d’utilisation Service de stockage de file d’attente](http://go.microsoft.com/fwlink/?LinkID=264702). Pour plus d’informations sur le service web de hello pour les files d’attente des services de stockage, consultez [Concepts du Service de file d’attente](http://go.microsoft.com/fwlink/?LinkId=264788). Pour plus d’informations sur la façon dont toosend messages tooa des services de stockage file d’attente à l’aide de Visual Studio, consultez [tooa de l’envoi de Messages file d’attente de Services de stockage](https://msdn.microsoft.com/library/azure/jj649344.aspx).

> [!NOTE]
> Les files d’attente de services de stockage sont différentes des files d’attente Service Bus. Pour plus d’informations sur les files d’attente Service Bus, consultez « Files d’attente, rubriques et abonnements Service Bus ».
> 
> 

## <a name="work-with-table-resources"></a>Utiliser des ressources de table
Hello service de stockage de Table Azure stocke de grandes quantités de données structurées. service de Hello est une banque de données NoSQL qui accepte authentifié d’appels à partir de l’intérieur et extérieur hello cloud Azure. Les tables Azure sont idéales pour le stockage des données structurées non relationnelles.

### <a name="toocreate-a-table"></a>toocreate une table
1. Dans le Cloud Explorer, sélectionnez hello **Tables** nœud de stockage de hello compte, puis choisissez **Create Table**.
2. Bonjour **Create Table** boîte de dialogue, entrez un nom pour la table de hello.

### <a name="tooview-table-data"></a>données de la table tooview
1. Dans le Cloud Explorer, ouvrez hello **Azure** nœud, puis ouvrez hello **stockage** nœud.
2. Nœud du compte de stockage ouvert hello que vous êtes intéressé et ouvrez hello **Tables** nœud toosee une liste de tables pour le compte de stockage hello.
3. Ouvrez le menu contextuel de hello pour une table, puis choisissez **vue Table**.
   
    ![Table Azure dans l’Explorateur de solutions](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

table de Hello est organisée par entités (affichées dans les lignes) et des propriétés (affichées dans les colonnes). Par exemple, hello après l’illustration montre les entités répertoriées dans hello **Concepteur de tables**:

### <a name="tooedit-table-data"></a>données de la table tooedit
1. Bonjour **Concepteur de tables**, ouvrez le menu contextuel de hello pour une entité (une seule ligne) ou une propriété (une seule cellule), puis sélectionnez **modifier**.
   
    ![Ajouter ou modifier une entité de table](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    Les entités dans une table unique ne sont pas hello toohave requis même jeu de propriétés (colonnes). Conservez Bonjour esprit suivant des restrictions sur l’affichage et la modification des données de la table.
   
   * Vous ne pouvez pas afficher ni modifier des données binaires (type octet[]), mais vous pouvez les stocker dans une table.
   * Vous ne pouvez pas modifier hello **PartitionKey** ou **RowKey** des valeurs, car le stockage de table dans Azure ne prend pas en charge cette opération.
   * Vous ne pouvez pas créer de propriété appelée Timestamp, car les services Azure Storage utilisent une propriété portant ce nom.
   * Si vous entrez une valeur DateTime, vous devez suivre un format toohello approprié des paramètres linguistiques et régionaux de votre ordinateur (par exemple, MM/jj/aaaa hh [AM | PM] pour les États-Unis ).

### <a name="tooadd-entities"></a>entités tooadd
1. Bonjour **Concepteur de tables**, choisissez hello **ajouter une entité** bouton.
   
    ![Ajouter une entité](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. Bonjour **ajouter une entité** boîte de dialogue, entrez les valeurs hello Hello **PartitionKey** et **RowKey** propriétés.
   
    ![Boîte de dialogue Ajouter une entité](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    Entrez des valeurs de hello avec soin, car vous ne pouvez pas les modifier après avoir fermé la boîte de dialogue hello, sauf si vous supprimez hello entité et ajoutez de nouveau.

### <a name="toofilter-entities"></a>entités toofilter
Vous pouvez personnaliser l’ensemble de hello d’entités qui apparaissent dans une table si vous utilisez le Générateur de requêtes hello.

1. Générateur de requêtes tooopen hello, ouvrez une table pour l’affichage.
2. Choisissez le bouton Générateur de requêtes de hello sur la barre d’outils de la vue de table hello.
   
    Hello **Générateur de requêtes** boîte de dialogue s’affiche. Hello l’illustration suivante montre une requête en cours de construction dans le Générateur de requête hello.
   
    ![Générateur de requêtes](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. Lorsque vous avez terminé création hello requête, fermez boîte de dialogue hello. Hello résultant texte de requête de hello apparaît dans une zone de texte comme un filtre de Services de données WCF.
4. toorun hello de requête, choisissez l’icône de triangle vert hello.
   
    Vous pouvez également filtrer les données d’entité qui s’affiche dans hello **Concepteur de tables** si vous entrez une chaîne de filtre de Services de données WCF directement dans le champ de filtre hello. Ce type de chaîne est similaire tooa clause SQL WHERE, mais est envoyé toohello serveur comme une requête HTTP. Pour plus d’informations sur la façon dont les chaînes de filtrage de tooconstruct, consultez [construire des chaînes de filtrage pour hello Concepteur de tables](https://msdn.microsoft.com/library/azure/ff683669.aspx).
   
    Hello l’illustration suivante montre un exemple de chaîne de filtrage valide :
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>Actualiser les données de stockage
Lorsque l’Explorateur de serveurs se connecte tooor Obtient des données à partir d’un compte de stockage, elle peut prendre tooa minute hello opération toocomplete. S’il ne peut pas se connecter, opération de hello peut expirer. Pendant l’extraction des données, vous pouvez continuer toowork dans d’autres parties de Visual Studio. opération de hello toocancel si elle est trop longue, choisissez hello **arrêter l’actualisation** bouton de barre d’outils de l’Explorateur de serveurs hello.

#### <a name="toorefresh-blob-container-data"></a>données de conteneur d’objets blob toorefresh
* Sélectionnez hello **BLOB** nœud sous **stockage** et choisissez hello **Actualiser** bouton de barre d’outils de l’Explorateur de serveurs hello.
* liste hello toorefresh d’objets BLOB qui s’affiche, choisissez hello **Execute** bouton.

#### <a name="toorefresh-table-data"></a>données de la table toorefresh
* Sélectionnez hello **Tables** nœud sous **stockage** et choisissez hello **Actualiser** bouton.
* liste de hello toorefresh des entités qui s’affiche dans hello **Concepteur de tables**, choisissez hello **Execute** bouton sur hello **Concepteur de tables**.

#### <a name="toorefresh-queue-data"></a>données de file d’attente toorefresh
* Sélectionnez hello **les files d’attente** nœud, puis choisissez hello **Actualiser** bouton.

#### <a name="toorefresh-all-items-in-a-storage-account"></a>toorefresh tous les éléments dans un compte de stockage
* Choisissez le nom du compte hello, puis hello **Actualiser** bouton de barre d’outils hello pour l’Explorateur de serveurs.

### <a name="add-storage-accounts-by-using-server-explorer"></a>Ajouter des comptes de stockage à l’aide de l’Explorateur de serveurs
Il existe deux façons tooadd les comptes de stockage à l’aide de l’Explorateur de serveurs. Vous pouvez créer un compte de stockage dans votre abonnement Azure, ou vous pouvez attacher un compte de stockage existant.

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>toocreate un compte de stockage à l’aide de l’Explorateur de serveurs
1. Dans l’Explorateur de serveurs, ouvrez le menu contextuel de hello pour le nœud de stockage hello, puis choisissez Créer un compte de stockage.
   
    ![Créer un compte de stockage Azure](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. Sélectionnez ou entrez hello suivant les informations de compte de stockage hello Bonjour **créer un compte de stockage** boîte de dialogue.
   
   * Bonjour toowhich abonnement Azure vous souhaitez que le compte de stockage tooadd hello.
   * Hello nom toouse hello nouveau compte de stockage.
   * région de Hello ou un groupe d’affinités (par exemple, ouest des États-Unis ou Asie orientale).
   * Hello du type de réplication que vous souhaitez toouse hello compte de stockage, telles que géo-redondant.
3. Cliquez sur **Créer**.
   
    nouveau compte de stockage Hello s’affiche dans hello **stockage** liste dans l’Explorateur de solutions.

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>tooattach un compte de stockage existant à l’aide de l’Explorateur de serveurs
1. Dans l’Explorateur de serveurs, ouvrez le menu contextuel de hello pour le nœud de stockage Azure hello, puis choisissez **attacher un stockage externe**.
   
    ![Ajout d’un compte de stockage existant](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. Sélectionnez ou entrez hello suivant les informations de compte de stockage hello Bonjour **créer un compte de stockage** boîte de dialogue.
   
   * nom Hello hello existant du compte de stockage souhaité tooattach. Vous pouvez entrer un nom ou sélectionnez-le dans la liste de hello.
   * clé Hello pour hello sélectionné un compte de stockage. Cette valeur est généralement fournie quand vous sélectionnez un compte de stockage. Si vous souhaitez que Visual Studio tooremember hello clé du compte, sélectionnez case clé du compte mémoriser hello.
   * Hello protocole toouse tooconnect toohello compte de stockage, tels que HTTP, HTTPS ou un point de terminaison personnalisé. Consultez [comment les chaînes de connexion tooConfigure](https://msdn.microsoft.com/library/azure/ee758697.aspx) pour plus d’informations sur les points de terminaison personnalisés.

### <a name="tooview-hello-secondary-endpoints"></a>points de terminaison secondaires tooview hello
* Si vous avez créé un compte de stockage à l’aide de hello **redondante avec accès en lecture** option de réplication, vous pouvez afficher ses points de terminaison secondaire. Ouvrir le menu contextuel de hello pour le nom de compte hello, puis choisissez **propriétés**.
  
    ![Points de terminaison de stockage secondaires](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>tooremove un compte de stockage à partir de l’Explorateur de serveurs
* Dans l’Explorateur de serveurs, ouvrir le menu contextuel de hello pour le nom de compte hello, puis choisissez **supprimer**. Si vous supprimez un compte de stockage, toutes les informations de clé enregistrées pour ce compte seront également supprimées.
  
  > [!NOTE]
  > Si vous supprimez un compte de stockage à partir de l’Explorateur de serveurs, il n’affecte pas votre compte de stockage ou les données qu’il contient ; Il supprime simplement hello référence l’Explorateur de serveurs. toopermanently supprimer un compte de stockage, utilisez hello [portail Azure classic](http://go.microsoft.com/fwlink/?LinkID=213885).
  > 
  > 

## <a name="next-steps"></a>Étapes suivantes
toolearn savoir plus sur l’utilisation de services de stockage Azure, voir [l’accès aux Services de stockage Azure hello](https://msdn.microsoft.com/library/azure/ee405490.aspx).

