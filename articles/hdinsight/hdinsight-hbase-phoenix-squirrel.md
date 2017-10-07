---
title: "aaaUse Apache Phoenix et non avec basé sur Windows Azure HDInsight | Documents Microsoft"
description: "Découvrez comment toouse Phoenix Apache dans HDInsight et comment tooinstall et configurer non sur votre cluster HBase de station de travail tooconnect tooan dans HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 1a756e98-75c1-44cd-a178-c5119683b7b7
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 147ac35fa882fd1bedbc5361ac804c36a4d56de1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a>Utiliser Apache Phoenix et SQuirreL avec les clusters HBase basés sur Windows dans HDInsight
Découvrez comment toouse [Apache Phoenix](http://phoenix.apache.org/) dans HDInsight et comment tooinstall et configurer non sur votre cluster HBase de station de travail tooconnect tooan dans HDInsight. Pour plus d'informations sur Phoenix, consultez [Phoenix en 15 minutes ou moins](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html). Pourquoi la grammaire de Phoenix, consultez [Phoenix grammaire](http://phoenix.apache.org/language/index.html).

> [!NOTE]
> Pourquoi les informations de version Phoenix dans HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?](hdinsight-component-versioning.md).
>

> [!IMPORTANT]
> les étapes dans ce document seul le travail clusters HDInsight de basés sur Windows Hello. HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4. Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure. Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Pour plus d’informations sur l’utilisation de Phoenix dans HDInsight sous Linux, consultez [Utilisation d’Apache Phoenix avec les clusters HBase basés sur Linux dans HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).
>



## <a name="use-sqlline"></a>Utiliser SQLLine
[SQLUltraLite](http://sqlline.sourceforge.net/) est un tooexecute utilitaire de ligne de commande SQL.

### <a name="prerequisites"></a>Composants requis
Avant de pouvoir utiliser SQLUltraLite, vous devez disposer de hello :

* **Un cluster HBase dans HDInsight**. Pour plus d’informations sur l’approvisionnement d’un cluster HBase, consultez [Prise en main d’Apache HBase dans HDInsight][hdinsight-hbase-get-started].
* **Connecter le cluster de HBase toohello via le protocole Bureau à distance de hello**. Pour obtenir des instructions, consultez [Hadoop de gérer des clusters dans HDInsight à l’aide de hello portail classique Azure][hdinsight-manage-portal].

**toofind nom d’hôte hello**

1. Ouvrez **ligne de commande Hadoop** à partir du bureau de hello.
2. Exécutez hello suivant le suffixe DNS de commande tooget hello :

        ipconfig

    Notez le **suffixe DNS propre à la connexion**. Par exemple, *myhbasecluster.f5.internal.cloudapp.net*. Lorsque vous vous connectez tooan HBase cluster, vous devez tooone tooconnect d’envieront hello à l’aide du nom de domaine complet. Chaque cluster HDInsight contient 3 Zookeepers : *zookeeper0*, *zookeeper1* et *zookeeper2*. Hello nom de domaine complet se présente comme *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.

**toouse SQLUltraLite**

1. Ouvrez **ligne de commande Hadoop** à partir du bureau de hello.
2. Exécutez hello suivant de commandes tooopen SQLUltraLite :

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    commandes Hello utilisées dans l’exemple hello :

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

Pour plus d’informations, consultez le [manuel SQLLine](http://sqlline.sourceforge.net/#manual) et la [grammaire Phoenix](http://phoenix.apache.org/language/index.html).

## <a name="use-squirrel"></a>Utiliser SQuirreL
[HIPPOCAMPIQUES SQL Client](http://squirrel-sql.sourceforge.net/) est un programme Java graphique qui vous permettent de structure de hello tooview d’une base de données compatible avec JDBC, parcourir les données hello dans les tables, émettre des commandes SQL etc.. Il peut être utilisé tooconnect tooApache Phoenix sur HDInsight.

Cette section vous montre comment tooinstall et configurer non sur votre station de travail tooconnect tooan cluster HBase dans HDInsight via VPN.

### <a name="prerequisites"></a>Composants requis
Avant de suivre les procédures de hello, vous devez disposer de hello :

* Un cluster HBase déployé tooan réseau virtuel Azure avec un ordinateur virtuel DNS.  Pour des instructions, consultez [Approvisionnement de clusters HBase sur Azure Virtual Network][hdinsight-hbase-provision-vnet].

* Obtenir le suffixe DNS spécifique à la connexion cluster hello HBase cluster. tooget il, RDP en cluster de hello, puis exécutez IPConfig.  suffixe DNS de Hello est similaire à :

        myhbase.b7.internal.cloudapp.net
* Téléchargez et installez [Microsoft Visual Studio Express pour Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) sur votre station de travail. Vous devez makecert hello package toocreate à partir de votre certificat.  
* Téléchargez et installez l' [environnement d'exécution Java](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) sur votre station de travail.  La version 3.0 ou supérieure du client SQL SQuirreL requiert la version 1.6 ou supérieure de JRE.  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a>Configurer un toohello de connexion VPN Point à Site réseau virtuel Azure
La configuration d'une connexion VPN de point à site comprend 3 étapes :

1. [Configurer un réseau virtuel et une passerelle de routage dynamique](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [Créer vos certificats](#Create-your-certificates)
3. [Configurer votre client VPN](#Configure-your-VPN-client)

Consultez [configurer un tooan de connexion VPN Point à Site réseau virtuel Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) pour plus d’informations.

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a>Configurer un réseau virtuel et une passerelle de routage dynamique
Assurer d’avoir configuré un cluster HBase dans un réseau virtuel Azure (voir la configuration requise de hello pour cette section). étape suivante de Hello est tooconfigure une connexion point à site.

**connectivité de point-to-site hello tooconfigure**

1. Connectez-vous à toohello [portail classique Azure][azure-portal].
2. Sur hello gauche, cliquez sur **réseaux**.
3. Cliquez sur hello de réseau virtuel que vous avez créé (voir [HBase de configurer des clusters sur un réseau virtuel Azure][hdinsight-hbase-provision-vnet]).
4. Cliquez sur **configurer** à partir du haut de hello.
5. Bonjour **connectivité de point-to-site** section, sélectionnez **configurer la connectivité de point-to-site**.
6. Configurer **adresse IP de départ** et **CIDR** plage d’adresses IP hello toospecify à partir de laquelle vos clients VPN recevront une adresse IP d’adresses lorsqu’il est connecté. Hello ne peuvent se chevaucher avec les hello plages situées sur votre site réseau et hello réseau virtuel Azure, à que vous vous connecterez. Par exemple, Si vous avez sélectionné 10.0.0.0/20 pour le réseau virtuel de hello, vous pouvez sélectionner 10.1.0.0/24 pour l’espace d’adressage client hello. Consultez hello [Point-To-Site connectivité] [ vnet-point-to-site-connectivity] page pour plus d’informations.
7. Dans la section des espaces d’adresse de réseau virtuel hello, cliquez sur **ajouter un sous-réseau de passerelle**.
8. Cliquez sur **enregistrer** bas hello de page de hello.
9. Cliquez sur **Oui** modification de hello tooconfirm. Attendez que le système de hello a terminé hello modifier avant de continuer de la procédure suivante de toohello.

**toocreate une passerelle avec routage dynamique**

1. À partir de hello portail classique Azure, cliquez sur **tableau de bord** de haut hello de page de hello.
2. Cliquez sur **créer une passerelle** bas hello de page de hello.
3. Cliquez sur **Oui** tooconfirm. Attendez que la passerelle de hello est créée.
4. Cliquez sur **tableau de bord** de haut de hello.  Vous verrez un schéma visuel de réseau virtuel de hello :

    ![Diagramme virtuel de point à site du réseau virtuel Azure][img-vnet-diagram]

    diagramme de Hello montre les connexions clientes, 0. Une fois que vous apportez à un réseau virtuel toohello de connexion, nombre de hello sera tooone mis à jour.

#### <a name="create-your-certificates"></a>Créer vos certificats
Une façon toocreate un certificat X.509 est à l’aide de hello outil de création de certificat (makecert.exe) qui est fourni avec [Microsoft Visual Studio Express pour Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).

**toocreate un certificat racine auto-signé**

1. Dans votre station de travail, ouvrez une fenêtre d'invite de commandes.
2. Accédez toohello dossier des outils Visual Studio.
3. Hello suivant de commande dans l’exemple hello ci-dessous crée et installer un certificat racine dans le magasin de certificats personnel hello sur votre station de travail et également créer un fichier .cer que vous téléchargerez plus tard toohello portail classique Azure.

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    Modifier le répertoire toohello que vous souhaitez hello toobe de fichier .cer situé dans, où HBaseVnetVPNRootCertificate est le nom hello que vous souhaitez toouse pour le certificat de hello.

    Ne fermez pas hello invite de commandes.  Vous en aurez besoin dans la procédure suivante de hello.

   > [!NOTE]
   > Étant donné que vous avez créé un certificat racine à partir duquel les certificats de client seront générées, vous pouvez souhaitez tooexport ce certificat avec sa clé privée et l’enregistrer tooa d’emplacement sûr où il peut être récupéré.
   >
   >

**toocreate un certificat client**

* À partir de hello même invite de commandes (il n’a toobe sur hello même ordinateur où vous avez créé le certificat racine de hello. certificat de client Hello doit être générée à partir du certificat racine de hello), exécution hello commande suivante :

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    HBaseVnetVPNRootCertificate est le nom du certificat racine hello.  Il a le nom du certificat racine toomatch hello.  

    Certificat racine de hello et certificat de client hello sont stockés dans votre magasin de certificats personnel sur votre ordinateur. Utilisez certmgr.msc tooverify.

    ![Certificat VPN de point à site du réseau virtuel Azure][img-certificate]

    Un certificat client doit être installé sur chaque ordinateur que vous souhaitez le réseau virtuel de tooconnect toohello. Nous vous recommandons de créer des certificats pour chaque ordinateur que vous souhaitez le réseau virtuel de tooconnect toohello client unique. les certificats clients tooexport hello, utilisez certmgr.msc.

**toohello de certificat racine tooupload hello portail classique Azure**

1. À partir de hello portail classique Azure, cliquez sur **réseau** sur hello gauche.
2. Cliquez sur le réseau virtuel hello où votre cluster HBase est déployée sur.
3. Cliquez sur **certificats** à partir du haut de hello.
4. Cliquez sur **télécharger** de hello bas, puis spécifiez le fichier de certificat racine hello que vous avez créé dans la procédure hello avant le dernier. Attendez que le certificat de hello a été importé.
5. Cliquez sur **tableau de bord** dessus hello.  diagramme de virtuel de Hello montre l’état de hello.

#### <a name="configure-your-vpn-client"></a>Configurer votre client VPN
**toodownload et installez hello le package VPN client**

1. À partir de la page du tableau de bord hello du réseau virtuel hello, dans la section Aperçu rapide de hello, cliquez sur **téléchargement hello 64 bits le Package VPN Client** ou **téléchargement hello 32 bits le Package VPN Client** en fonction de votre version de la station de travail du système d’exploitation.
2. Cliquez sur **exécuter** package de hello tooinstall.
3. À l’invite de sécurité hello, cliquez sur **plus d’informations**, puis cliquez sur **quand même exécuter**.
4. Cliquez sur **Oui** deux fois.

**tooconnect tooVPN**

1. Sur le bureau hello de votre station de travail, cliquez sur icône de réseaux hello sur la barre des tâches hello. Vous devez voir une connexion VPN avec le nom de votre réseau virtuel.
2. Cliquez sur le nom de la connexion VPN hello.
3. Cliquez sur **Connecter**.

**tootest hello résolution de noms de domaine et de la connexion VPN**

* À partir de la station de travail hello, ouvrez une invite de commandes et la commande ping de hello suivant les noms donnés suffixe DNS du cluster hello HBase est myhbase.b7.internal.cloudapp.net :

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a>Installation et configuration de SQuirreL sur votre poste de travail
**tooinstall non**

1. Téléchargez hello non SQL client jar fichier [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).
2. Fichier jar ouvrir/exécuter hello. Il requiert hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).
3. Cliquez sur **Suivant** deux fois.
4. Spécifiez un chemin d’accès où vous avez hello l’autorisation en écriture, puis cliquez sur **suivant**.

  > [!NOTE]
  > dossier d’installation par défaut Hello est dans le dossier C:\Program Files\squirrel-sql-3.6 de hello.  Dans chemin d’accès ordre toowrite toothis, programme d’installation hello doit disposer des privilèges d’administrateur hello. Vous pouvez ouvrir une invite de commandes en tant qu’administrateur, parcourir le dossier bin de tooJava, puis exécutez :
  >
  >     Java.exe-jar [chemin d’accès du fichier jar de non hello le hello]
5. Cliquez sur **OK** tooconfirm création du répertoire cible de hello.
6. Hello par défaut est tooinstall hello Base et packages Standard.  Cliquez sur **Suivant**.
7. Cliquez sur **Suivant** deux fois, puis sur **Terminé**.

**pilote de tooinstall hello Phoenix**

fichier jar de Hello phoenix pilote se trouve sur un cluster HBase de hello. chemin d’accès Hello est similaire toohello suivantes, en fonction des versions de hello :

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
Vous devez toocopy il tooyour de station de travail sous hello [dossier d’installation non] / lib de chemin d’accès.  Hello plus simple est tooRDP en cluster de hello, puis utilisez fichier copier/coller (CTRL + C et CTRL + V) toocopy il tooyour la station de travail.

**tooadd un tooSQuirreL de pilote Phoenix**

1. Ouvrez le client SQL SQuirreL dans votre poste de travail.
2. Cliquez sur hello **pilote** onglet hello gauche.
3. À partir de hello **pilotes** menu, cliquez sur **nouveau pilote**.
4. Entrez hello informations suivantes :

   * **Name**: Phoenix
   * **Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net
   * **Class Name**: org.apache.phoenix.jdbc.PhoenixDriver

     > [!WARNING]
     > Utilisateur toutes les minuscules Bonjour exemple d’URL. Vous pouvez utiliser le quorum complet zookeeper au cas où l’un d’eux est inactif.  noms d’hôtes Hello sont zookeeper0, zookeeper1 et zookeeper2.
     >
     >

     ![Pilote HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. Cliquez sur **OK**.

**toocreate un cluster HBase de toohello alias**

1. À partir de non, cliquez sur hello **alias** onglet hello gauche.
2. À partir de hello **alias** menu, cliquez sur **nouvel Alias**.
3. Entrez hello informations suivantes :

   * **Nom**: nom de hello du cluster de HBase hello ou n’importe quel nom que vous préférez.
   * **Driver**: Phoenix.  Cela doit correspondre au nom du pilote hello créé dans la procédure de dernière hello.
   * **URL**: hello URL est copié à partir de votre configuration du pilote. Assurez-vous que toouser toutes les minuscules.
   * **Nom d’utilisateur**: il s’agit de texte.  Étant donné que vous utilisez ici connectivité VPN, nom d’utilisateur hello n’est pas utilisée.
   * **Password**: il s’agit de texte.

     ![Pilote HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. Cliquez sur **Test**.
5. Cliquez sur **Connecter**. Lorsqu’elle s’effectue de connexion de hello, non l’aspect suivant :

    ![HBase Phoenix SQuirreL][img-squirrel]

**toorun un test**

1. Cliquez sur hello **SQL** onglet droite suivant toohello **objets** onglet.
2. Copiez et collez hello suivant de code :

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. Cliquez sur le bouton d’exécution hello.

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. Commutateur précédent toohello **objets** onglet.
5. Nom d’alias hello, puis **TABLE**.  Vous devez voir hello nouvelle table répertorié sous.

## <a name="next-steps"></a>Étapes suivantes
Dans cet article, vous avez appris comment toouse Phoenix Apache dans HDInsight.  toolearn, voir

* [Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.
* [Configurer des clusters HBase sur un réseau virtuel Azure][hdinsight-hbase-provision-vnet]: avec l’intégration de réseau virtuel, clusters HBase peuvent être déployé toohello même virtuel réseau en tant que vos applications, ainsi que les applications peuvent communiquer avec HBase directement.
* [Configurer la réplication de HBase de HDInsight](hdinsight-hbase-replication.md): Découvrez comment tooconfigure HBase la réplication entre deux centres de données Azure.
* [Analyse des sentiments Twitter avec HBase dans HDInsight][hbase-twitter-sentiment]: Découvrez comment toodo en temps réel [analyse des sentiments](http://en.wikipedia.org/wiki/Sentiment_analysis) de données à l’aide de HBase dans un cluster Hadoop dans HDInsight.

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-versions]: hdinsight-component-versioning.md
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
