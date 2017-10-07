---
title: aaaSet une machine virtuelle de SQL Server comme serveur notebooks bloc-notes | Documents Microsoft
description: "Configurez une machine virtuelle pour la science des données avec SQL Server et un serveur IPython."
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 1fd6014a-d180-4558-b4eb-d9b5a331a99f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: xibingao;bradsev
ms.openlocfilehash: ee83d1d5de671d9817c1bc1abd6b4f9c256dde8f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-an-azure-sql-server-virtual-machine-as-an-ipython-notebook-server-for-advanced-analytics"></a>Configurer une machine virtuelle Azure SQL Server comme serveur IPython Notebook pour des analyses avancées
Cette rubrique montre comment tooprovision et configurer un toobe de machine virtuelle SQL Server utilisée dans le cadre d’un environnement de science des données basées sur le cloud. l’ordinateur virtuel Windows Hello est configuré avec la prise en charge des outils tels que des notebooks portable, l’Explorateur de stockage Azure et AzCopy, ainsi que d’autres utilitaires qui sont utiles pour les projets scientifiques de données. Azure Storage Explorer et AzCopy, par exemple, fournissent des moyens pratiques stockage d’objets blob tooAzure tooupload données à partir de votre ordinateur local ou un toodownload il tooyour la machine locale à partir du stockage d’objets blob.

Galerie de machine virtuelle Azure Hello inclut plusieurs images qui contiennent Microsoft SQL Server. Sélectionnez une image de machine virtuelle SQL Server adaptée à vos besoins en matière de données. Les images recommandées sont les suivantes :

* SQL Server 2012 SP2 Enterprise toomedium petites tailles de données
* SQL Server 2012 SP2 Enterprise optimisé pour les charges de travail DataWarehousing grand toovery grandes tailles de données
  
  > [!NOTE]
  > L’image SQL Server 2012 SP2 Enterprise **n’inclut aucun disque de données**. Vous serez peut-être tooadd ou joindre un ou plusieurs toostore de disques durs virtuels de vos données. Lorsque vous créez une machine virtuelle Azure, il possède un disque pour le lecteur de toohello C de système d’exploitation mappé hello et un lecteur de toohello D de disque temporaire mappé. N’utilisez pas de données toostore hello D. Hello nom l’indique, il fournit un stockage temporaire uniquement. Il n'offre aucune possibilité de redondance ou de sauvegarde, car il ne réside pas dans le stockage Azure.
  > 
  > 

## <a name="Provision"></a>Se connecter toohello portail classique Azure et configurer une machine virtuelle SQL Server
1. Connectez-vous à toohello [portail Azure Classic](http://manage.windowsazure.com/) à l’aide de votre compte.
   Si vous n'avez pas de compte Azure, visitez la page [Version d'évaluation gratuite d'Azure](https://azure.microsoft.com/pricing/free-trial/).
2. Dans le portail Azure Classic hello à hello bas à gauche de hello web page, cliquez sur **+ nouveau**, cliquez sur **de calcul**, cliquez sur **virtuels**, puis cliquez sur **FROM La galerie**.
3. Sur hello **créer une Machine virtuelle** page, sélectionnez une image de machine virtuelle contenant SQL Server en fonction de vos besoins, puis cliquez sur la flèche suivant de hello en bas à droite de la page de hello. Pour les informations les plus récentes sur hello hello pris en charge les images de SQL Server sur Azure, consultez [prise en main de SQL Server dans Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294720) rubrique Bonjour [SQL Server dans Azure Virtual Machines](http://go.microsoft.com/fwlink/p/?LinkId=294719) ensemble de documentation.
   
   ![Sélection de la machine virtuelle Serveur SQL][1]
4. Sur hello première **Configuration d’ordinateur virtuel** , fournissez les informations suivantes :
   
   * Entrez un **nom de machine virtuelle**.
   * Bonjour **nouveau nom d’utilisateur** boîte, nom d’utilisateur unique de type pour hello compte administrateur local d’ordinateur virtuel.
   * Bonjour **nouveau mot de passe** , tapez un mot de passe fort. Pour plus d’informations, consultez la page [Mots de passe forts](http://msdn.microsoft.com/library/ms161962.aspx).
   * Bonjour **confirmer le mot de passe** zone, tapez à nouveau le mot de passe hello.
   * Sélectionnez hello approprié **taille** de hello liste déroulante.
     
     > [!NOTE]
     > taille de Hello de machine virtuelle de hello est spécifiée lors de la configuration : A2 est hello plus petite taille recommandée pour les charges de production. La taille minimale recommandée pour une machine virtuelle utilisant SQL Server Édition Entreprise est A3. Sélectionnez A3 ou plus lorsque vous utilisez SQL Server Enterprise Edition. Sélectionnez A4 lorsque vous utilisez des images SQL Server 2012 ou 2014 Enterprise optimisées pour les charges de travail transactionnelles.
     > Sélectionnez A7 lorsque vous utilisez des images SQL Server 2012 ou 2014 Enterprise optimisées pour les charges de travail pour l’entreposage de données. taille de Hello sélectionnée limite le nombre de disques de données que vous pouvez configurer. Pour obtenir des informations plus récentes sur les tailles de machine virtuelle disponibles et nombre hello de disques de données que vous pouvez joindre la machine virtuelle de tooa, consultez [tailles de Machine virtuelle pour Azure](http://msdn.microsoft.com/library/azure/dn197896.aspx). Pour connaître les informations de tarification, consultez la page [Machines virtuelles Tarification](https://azure.microsoft.com/pricing/details/virtual-machines/).
     > 
     > 
   
   Cliquez sur hello suivant sur flèche toocontinue de hello en bas à droite.
   
   ![Configuration de machine virtuelle][2]
5. Sur hello deuxième **configuration d’ordinateur virtuel** page, configurez les ressources de mise en réseau, de stockage et de disponibilité :
   
   * Bonjour **Service Cloud** , choisissez **créer un service cloud**.
   * Bonjour **nom DNS du Service Cloud** zone, fournissez hello de première partie d’un nom DNS de votre choix, afin qu’elle complète un nom au format **TESTNAME.cloudapp.net**
   * Bonjour **régions ou d’affinités groupe/réseau virtuel** , sélectionnez une région où cette image virtuelle sera hébergée.
   * Bonjour **compte de stockage**, sélectionnez un compte de stockage existant ou un nom généré automatiquement.
   * Bonjour **à haute disponibilité** boîte, sélectionnez **(aucun)**.
   * Lisez et acceptez les informations de tarification de hello.
6. Bonjour **points de terminaison** , cliquez sur dans la liste déroulante vide de hello sous **nom**, puis sélectionnez **MSSQL** puis tapez le numéro de port hello de l’instance de moteur de base de données (dehello**1433** hello instance par défaut).
7. Votre machine virtuelle SQL Server peut également faire office de serveur Notebook IPython, que nous configurerons ultérieurement.
   Ajouter un toouse de port hello du nouveau point de terminaison toospecify pour votre serveur notebooks bloc-notes. Entrez un nom dans hello **nom** colonne, sélectionnez un numéro de port de votre choix pour le port public de hello et 9999 pour un port privé hello.
   
   Cliquez sur hello suivant sur flèche toocontinue de hello en bas à droite.
   
   ![Sélection des ports MSSQL et IPython][3]
8. Accepter la valeur par défaut hello **agent de machine virtuelle d’installer** option activée et cliquez sur la case à cocher hello hello en hello en bas à droite de hello de toocomplete Assistant hello les processus de configuration de machine virtuelle.
   
   `![Dernières Options de machine virtuelle][4]
9. Patientez pendant qu'Azure prépare votre machine virtuelle. Attendez tooproceed d’état de machine virtuelle hello via :
   
   * Démarrage (configuration)
   * Arrêté
   * Démarrage (configuration)
   * Exécution (configuration)
   * Exécution

## <a name="RemoteDesktop"></a>Machine virtuelle de hello ouverte à l’aide du Bureau à distance et terminer l’installation
1. Lors de la mise en service terminée, cliquez sur le nom hello de votre page de tableau de bord de machine virtuelle toogo toohello. Au bas de hello de page de hello, cliquez sur **connexion**.
2. Choisissez tooopen hello rpd fichier à l’aide du programme de bureau à distance Windows hello (`%windir%\system32\mstsc.exe`).
3. À hello **sécurité Windows** boîte de dialogue zone, fournissez le mot de passe de hello pour le compte d’administrateur local que vous avez spécifié dans une étape antérieure.
   (Vous pouvez être invité informations d’identification de hello tooverify de machine virtuelle de hello.)
4. Hello première fois que vous ouvrez une session sur l’ordinateur virtuel de toothis, plusieurs processus devront peut-être toocomplete, y compris le programme d’installation de votre bureau, mises à jour Windows et l’achèvement des tâches de configuration initiales de Windows hello (sysprep). Une fois Windows sysprep terminé, les tâches de configuration de SQL Server sont terminées. L’exécution de ces tâches peut prendre quelques minutes. `SELECT @@SERVERNAME`peut retourner pas le nom correct de hello jusqu'à ce que le programme d’installation de SQL Server se termine, et SQL Server Management Studio ne peut pas être visible sur la page de démarrage hello.

Une fois l’ordinateur virtuel de toohello connecté avec le Bureau à distance de Windows, hello machine virtuelle fonctionne comme beaucoup n’importe quel autre ordinateur. Connecter l’instance par défaut de toohello de SQL Server avec SQL Server Management Studio (en cours d’exécution sur l’ordinateur virtuel de hello) Bonjour normalement.

## <a name="InstallIPython"></a>Installer Notebook IPython et les autres outils connexes
tooconfigure votre nouvelle tooserve de machine virtuelle SQL Server comme un serveur de notebooks bloc-notes et prise en charge supplémentaire de l’installation des outils tels AzCopy, Explorateur de stockage Azure, des packages Python de science des données utiles et d’autres, un script de personnalisation spéciale est fourni tooyou. tooinstall :

1. Avec le bouton hello **Démarrer de Windows** icône et cliquez sur **l’invite de commandes (Admin)**
2. Hello suivant les commandes de copier et coller à l’invite de commandes hello.
  
        set script='https://raw.githubusercontent.com/Azure/Azure-MachineLearning-DataScience/master/Misc/MachineSetup/Azure_VM_Setup_Windows.ps1'
        @powershell -NoProfile -ExecutionPolicy unrestricted -Command "iex ((new-object net.webclient).DownloadString(%script%))"
3. Lorsque vous y êtes invité, entrez un mot de passe de votre choix pour hello serveur des notebooks bloc-notes.
4. script de personnalisation Hello automatise plusieurs procédures après l’installation, notamment :
    * Installation et configuration du serveur Notebook IPython
    * Ouverture des ports TCP dans le pare-feu Windows hello pour les points de terminaison hello créé précédemment :
    * pour la connectivité à distance de SQL Server ;
    * pour la connectivité à distance du serveur Notebook IPython.
    * Extraction des exemples de notebooks IPython et de scripts SQL
    * Téléchargement et installation des packages de science des données Python utiles
    * Téléchargement et installation d’outils Azure tels qu’AzCopy et Azure Storage Explorer   
    <br>
5. Vous pouvez accéder et exécuter des notebooks bloc-notes à partir de n’importe quel navigateur local ou distant à l’aide d’une URL sous forme de hello `https://<virtual_machine_DNS_name>:<port>`, où le port est sélectionné lors de la configuration d’ordinateur virtuel de hello du port public notebooks hello.
6. Serveur de notebooks bloc-notes s’exécute comme un service en arrière-plan et sera redémarré automatiquement lorsque vous redémarrez l’ordinateur virtuel de hello.

## <a name="Optional"></a>Attacher des disques de données selon vos besoins
Si votre image de machine virtuelle n’inclut pas de disques de données, par exemple, les disques que le lecteur C (disque du système d’exploitation) et D (disque temporaire), vous devez tooadd une, ou d’autres données disques toostore vos données. image de machine virtuelle Hello pour SQL Server 2012 SP2 Enterprise optimisé pour les charges de travail DataWarehousing est préconfigurée avec des disques supplémentaires pour les fichiers journaux et de données SQL Server.

> [!NOTE]
> N’utilisez pas de données toostore hello D. Hello nom l’indique, il fournit un stockage temporaire uniquement. Il n'offre aucune possibilité de redondance ou de sauvegarde, car il ne réside pas dans le stockage Azure.
> 
> 

tooattach autres disques de données, suivez les étapes de hello décrites dans [comment tooAttach un tooa de disque de données Machine virtuelle Windows](../virtual-machines/windows/classic/attach-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json), ce qui vous aidera à :

1. Attachement de disques vides toohello virtuels configurés dans les premières étapes
2. Initialisation de hello nouveaux disques de machine virtuelle de hello

## <a name="SSMS"></a>Se connecter tooSQL Server Management Studio et activer l’authentification en mode mixte
Hello du moteur de base de données SQL Server ne peut pas utiliser l’authentification Windows sans environnement de domaine. tooconnect toohello du moteur de base de données à partir d’un autre ordinateur, configurez SQL Server pour l’authentification en mode mixte. qui permet l'authentification SQL Server et l'authentification Windows Mode d’authentification SQL est requise dans les données tooingest des commandes directement à partir de vos bases de données de machine virtuelle SQL Server dans le [Azure Machine Learning Studio](https://studio.azureml.net) à l’aide du module d’importation de données hello.

1. Lors de la machine virtuelle de toohello connecté à l’aide du Bureau à distance, utilisez hello Windows **recherche** volet et le type **SQL Server Management Studio** (SMSS). Cliquez sur toostart hello SQL Server Management Studio (SSMS). Vous souhaiterez tooadd un tooSSMS raccourci sur votre bureau pour une utilisation ultérieure.
   
   ![Démarrer SSMS][5]
   
   Hello la première fois que vous ouvrez Management Studio, il doit créer des environnement de Management Studio utilisateurs hello. Cette opération peut prendre du temps.
2. Lorsque vous ouvrez, Management Studio présente hello **connecter tooServer** boîte de dialogue. Bonjour **nom du serveur** zone, entrez un nom hello de hello machine virtuelle tooconnect toohello du moteur de base de données avec l’Explorateur d’objets de hello.
   (Au lieu du nom d’ordinateur virtuel hello vous pouvez également utiliser **(local)** ou un point unique comme hello **nom du serveur**. Sélectionnez **l’authentification Windows**et laisser  ***votre\_VM\_nom*\\votre\_local\_administrateur**  Bonjour **nom d’utilisateur** boîte. Cliquez sur **Connecter**.
   
   ![Se connecter tooServer][6]
   
   <br>
   
   > [!TIP]
   > Vous pouvez modifier le mode d’authentification SQL Server hello à l’aide d’un changement de clé de Registre Windows ou hello SQL Server Management Studio. mode d’authentification toochange à l’aide de changement de clé du Registre hello, démarrer un **nouvelle requête** et exécutez hello script suivant :
   > 
   > 
   
       USE master
       go
   
       EXEC xp_instance_regwrite N'HKEY_LOCAL_MACHINE', N'Software\Microsoft\MSSQLServer\MSSQLServer', N'LoginMode', REG_DWORD, 2
       go

    mode d’authentification hello toochange à l’aide de SQL Server management Studio :

1. Dans **Explorateur d’objets SQL Server Management Studio**, cliquez sur le nom d’instance hello de SQL Server (nom de machine virtuelle hello), puis cliquez sur **propriétés**.
   
   ![Propriétés de serveur][7]
2. Sur hello **sécurité** sous **l’authentification du serveur**, sélectionnez **mode d’authentification SQL Server et Windows**, puis cliquez sur **OK** .
   
   ![Sélectionner le mode d'authentification][8]
3. Bonjour **SQL Server Management Studio** boîte de dialogue, cliquez sur **OK** pour accuser réception de hello exigence toorestart SQL Server.
4. Dans l’**Explorateur d’objets**, cliquez avec le bouton droit sur votre serveur, puis cliquez sur **Redémarrer**. (si SQL Server Agent est exécuté, il doit également être redémarré).
   
   ![Redémarrer][9]
5. Bonjour **SQL Server Management Studio** boîte de dialogue, cliquez sur **Oui** d’accord que vous souhaitez toorestart SQL Server.

## <a name="Logins"></a>Créer des connexions d’authentification SQL Server
tooconnect toohello du moteur de base de données à partir d’un autre ordinateur, vous devez créer au moins une connexion d’authentification SQL Server.  

Vous pouvez créer des connexions SQL Server par programme ou à l’aide de hello SQL Server Management Studio. toocreate un nouvel utilisateur d’administrateur système avec l’authentification SQL par programme, démarrer un **nouvelle requête** et exécutez hello script suivant. Remplacez les variables <nouveau nom d’utilisateur\> et <nouveau mot de passe\> par le *nom d’utilisateur* et le *mot de passe* de votre choix. 

    USE master
    go

    CREATE LOGIN <new user name> WITH PASSWORD = N'<new password>',
        CHECK_POLICY = OFF,
        CHECK_EXPIRATION = OFF;

    EXEC sp_addsrvrolemember @loginame = N'<new user name>', @rolename = N'sysadmin';


Ajuster la stratégie de mot de passe hello en fonction des besoins (exemple de code hello désactive d’expiration du mot de passe et de la vérification de la stratégie). Pour plus d'informations sur les connexions SQL Server, consultez la page [Créer un compte de connexion](http://msdn.microsoft.com/library/aa337562.aspx).  

toocreate des connexions SQL Server à l’aide de hello SQL Server Management Studio :

1. Dans **Explorateur d’objets SQL Server Management Studio**, développez le dossier hello d’instance de serveur hello dans lequel vous souhaitez toocreate hello nouveau compte de connexion.
2. Avec le bouton hello **sécurité** dossier, pointez trop**nouveau**, puis sélectionnez **connexion...** .
   
   ![Nouvelle connexion][10]
3. Bonjour **nouvelle connexion** la boîte de dialogue hello **général** , entrez le nom hello du nouvel utilisateur de hello Bonjour **nom de connexion** boîte.
4. Sélectionnez **Authentification SQL Server**.
5. Bonjour **mot de passe** , entrez un mot de passe pour le nouvel utilisateur de hello. Entrez de nouveau ce mot de passe dans hello **confirmer le mot de passe** boîte.
6. Sélectionnez des options de stratégie de mot de passe tooenforce pour la complexité et de mise en œuvre, **appliquer la stratégie de mot de passe** (recommandé). Il s'agit d'une option par défaut lorsque l'authentification SQL Server est sélectionnée.
7. Sélectionnez des options de stratégie de mot de passe tooenforce pour l’expiration, **appliquer l’expiration du mot de passe** (recommandé). Appliquer la stratégie de mot de passe doit être sélectionné tooenable cette case à cocher. Il s'agit d'une option par défaut lorsque l'authentification SQL Server est sélectionnée.
8. tooforce hello utilisateur toocreate un nouveau mot de passe après hello pour la première fois la connexion est utilisée, sélectionnez **utilisateur doit changer de mot de passe à la prochaine connexion** (recommandé si cette connexion est pour quelqu'un d’autre toouse. Si la connexion de hello est pour votre propre usage, ne sélectionnez pas cette option.) Appliquer l’expiration du mot de passe doit être sélectionné tooenable cette case à cocher. Il s'agit d'une option par défaut lorsque l'authentification SQL Server est sélectionnée.
9. À partir de hello **base de données par défaut** , sélectionnez une base de données par défaut pour la connexion de hello. **maître** est par défaut de hello pour cette option. Si vous n’avez pas encore créé une base de données utilisateur, laissez ce paramètre défini trop**master**.
10. Bonjour **langue par défaut** liste, laissez **par défaut** en tant que valeur de hello.
    
    ![Propriétés de connexion][11]
11. S’il s’agit de hello première connexion que vous créez, vous souhaiterez afficher cette connexion en tant qu’un administrateur SQL Server. Si tel est le cas, sur la page **Rôles du serveur**, activez la case à cocher **administrateur système**.
    
    > [!IMPORTANT]
    > Les membres du rôle serveur fixe sysadmin de hello disposent du contrôle total hello du moteur de base de données. Pour des raisons de sécurité, vous devez limiter soigneusement l'appartenance à ce rôle.
    > 
    > 
    
    ![administrateur système][12]
12. Cliquez sur OK.

## <a name="DNS"></a>Déterminer le nom DNS de hello de machine virtuelle de hello
tooconnect toohello du moteur de base de données SQL Server à partir d’un autre ordinateur, vous devez connaître hello système DNS (Domain Name) nom de l’ordinateur virtuel de hello.

(Il s’agit d’ordinateur virtuel des hello tooidentify utilise hello nom hello internet. Vous pouvez utiliser des adresses IP de hello, mais l’adresse hello peut-être changer lorsque Azure déplace des ressources pour la redondance ou la maintenance. nom DNS de Hello sera stable, car elle peut être redirigé la nouvelle adresse IP de tooa.)

1. Bonjour portail classique Azure (ou à partir de l’étape précédente de hello), sélectionnez **virtuels**.
2. Sur hello **INSTANCES DE MACHINE virtuelle** page hello **nom DNS** colonne, recherchez et copiez nom DNS de hello pour la machine virtuelle de hello qui s’affiche précédé **http://**. (l’interface utilisateur hello ne peut pas afficher complet hello, mais vous pouvez avec le bouton droit dessus et sélectionnez Copier.)

## <a name="cde"></a>Se connecter toohello du moteur de base de données à partir d’un autre ordinateur
1. Sur un ordinateur connecté toohello internet, ouvrez SQL Server Management Studio.
2. Bonjour **connecter tooServer** ou **connecter tooDatabase moteur** la boîte de dialogue hello **nom du serveur** , entrez le nom DNS de hello de l’ordinateur virtuel (déterminée Bonjour la tâche précédente) et un numéro de port de point de terminaison public au format hello de *NomDNS, numéro_port* comme **tutorialtestVM.cloudapp.net,57500**.
3. Bonjour **authentification** boîte, sélectionnez **l’authentification SQL Server**.
4. Bonjour **connexion** zone, entrez un nom hello d’une connexion que vous avez créé dans une tâche précédente.
5. Bonjour **mot de passe** boîte, un mot de passe hello type de connexion hello que vous créez dans une tâche précédente.
6. Cliquez sur **Connecter**.

## <a name="amlconnect"></a>Se connecter toohello du moteur de base de données à partir d’Azure Machine Learning
Dans les étapes ultérieures de hello équipe données science des processus, vous allez utiliser hello [Azure Machine Learning Studio](https://studio.azureml.net) toobuild et déployer des modèles d’apprentissage automatique. tooingest des données à partir de vos bases de données de machine virtuelle SQL Server directement dans Azure Machine Learning pour l’apprentissage ou de calcul de score, utilisez hello **importer des données** module dans une nouvelle [Azure Machine Learning Studio](https://studio.azureml.net) faire des essais. Cette rubrique est abordée dans plus de détails via hello liens du guide de processus de science des données de Team. Pour découvrir une introduction, consultez la page [Azure Machine Learning Studio - De quoi s’agit-il ?](machine-learning-what-is-ml-studio.md).

1. Bonjour **propriétés** volet Hello [module d’importer des données](https://msdn.microsoft.com/library/azure/dn905997.aspx), sélectionnez **base de données SQL Azure** de hello **Source de données** liste déroulante.
2. Bonjour **nom du serveur de base de données** texte, entrez`tcp:<DNS name of your virtual machine>,1433`
3. Entrez le nom d’utilisateur SQL hello Bonjour **le nom de compte d’utilisateur serveur** zone de texte.
4. Entrez le mot de passe de l’utilisateur hello sql Bonjour **mot de passe utilisateur Server** zone de texte.
   
   ![Importation de données Azure Machine Learning][13]

## <a name="shutdown"></a>Arrêter et libérer une machine virtuelle inutilisée
Le service Azure Virtual Machines est facturé au tarif du **paiement à l’utilisation**. tooensure qui vous ne sont pas facturées lorsque vous n’utilisez ne pas votre machine virtuelle, il a toobe Bonjour **arrêté (désalloué)** état.

> [!NOTE]
> Arrêt de la machine virtuelle de hello depuis à l’intérieur de (à l’aide des options d’alimentation de Windows), hello machine virtuelle est arrêtée, mais reste allouée. tooensure vous n'êtes pas facturé, toujours s’arrêter les machines virtuelles à partir de hello [portail classique Azure](http://manage.windowsazure.com/). Vous pouvez également arrêter hello machine virtuelle via Powershell en appelant ShutdownRoleOperation avec « PostShutdownAction » égal trop « StoppedDeallocated ».
> 
> 

tooshutdown et désallouer une machine virtuelle hello :

1. Connectez-vous à toohello [portail classique Azure](http://manage.windowsazure.com/) à l’aide de votre compte.  
2. Sélectionnez **virtuels** à partir de la barre de navigation gauche hello.
3. Dans la liste hello des machines virtuelles, cliquez sur nom hello de votre machine virtuelle, puis accédez toohello **tableau de bord** page.
4. Au bas de hello de page de hello, cliquez sur **arrêt**.

![Arrêt de la machine virtuelle][15]

machine virtuelle de Hello sera libérée mais pas supprimé. Vous pouvez redémarrer votre machine virtuelle à tout moment à partir de hello portail classique Azure.

## <a name="your-azure-sql-server-vm-is-ready-toouse-whats-next"></a>Votre machine virtuelle Azure SQL Server est prêt toouse : quelle est la suite ?
Votre ordinateur virtuel est maintenant prêt toouse dans vos exercices de science des données. machine virtuelle de Hello est également prêt à être utilisé comme un serveur notebooks bloc-notes de hello et le traitement des données et d’autres tâches conjointement avec Azure Machine Learning et hello processus de science des données équipe (TDSP).

les étapes suivantes dans le processus de science des données hello Hello sont mappées dans hello [processus de science des données équipe](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/) et peuvent inclure des étapes de déplacement des données dans HDInsight, processus et les exemples de celui-ci en préparation pour l’apprentissage à partir des données de hello avec Azure Machine L’apprentissage.

[1]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/selectsqlvmimg.png
[2]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/4vm-config.png
[3]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/sqlvmports.png
[4]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmpostopts.png
[5]:./media/machine-learning-data-science-setup-sql-server-virtual-machine/searchssms.png
[6]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/19connect-to-server.png
[7]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/20server-properties.png
[8]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/21mixed-mode.png
[9]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/22restart2.png
[10]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/23new-login.png
[11]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/24test-login.png
[12]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/25sysadmin.png
[13]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/amlreader.png
[15]: ./media/machine-learning-data-science-setup-sql-server-virtual-machine/vmshutdown.png

