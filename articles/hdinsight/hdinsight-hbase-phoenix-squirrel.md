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
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="179bf-103">Utiliser Apache Phoenix et SQuirreL avec les clusters HBase basés sur Windows dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="179bf-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="179bf-104">Découvrez comment toouse [Apache Phoenix](http://phoenix.apache.org/) dans HDInsight et comment tooinstall et configurer non sur votre cluster HBase de station de travail tooconnect tooan dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179bf-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight.</span></span> <span data-ttu-id="179bf-105">Pour plus d'informations sur Phoenix, consultez [Phoenix en 15 minutes ou moins](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="179bf-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="179bf-106">Pourquoi la grammaire de Phoenix, consultez [Phoenix grammaire](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="179bf-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="179bf-107">Pourquoi les informations de version Phoenix dans HDInsight, consultez [quelles sont les nouveautés dans les versions de cluster Hadoop hello fournies par HDInsight ?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="179bf-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="179bf-108">les étapes dans ce document seul le travail clusters HDInsight de basés sur Windows Hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-108">hello steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="179bf-109">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="179bf-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="179bf-110">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="179bf-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="179bf-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="179bf-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="179bf-112">Pour plus d’informations sur l’utilisation de Phoenix dans HDInsight sous Linux, consultez [Utilisation d’Apache Phoenix avec les clusters HBase basés sur Linux dans HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="179bf-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="179bf-113">Utiliser SQLLine</span><span class="sxs-lookup"><span data-stu-id="179bf-113">Use SQLLine</span></span>
<span data-ttu-id="179bf-114">[SQLUltraLite](http://sqlline.sourceforge.net/) est un tooexecute utilitaire de ligne de commande SQL.</span><span class="sxs-lookup"><span data-stu-id="179bf-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="179bf-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="179bf-115">Prerequisites</span></span>
<span data-ttu-id="179bf-116">Avant de pouvoir utiliser SQLUltraLite, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="179bf-116">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="179bf-117">**Un cluster HBase dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="179bf-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="179bf-118">Pour plus d’informations sur l’approvisionnement d’un cluster HBase, consultez [Prise en main d’Apache HBase dans HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="179bf-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="179bf-119">**Connecter le cluster de HBase toohello via le protocole Bureau à distance de hello**.</span><span class="sxs-lookup"><span data-stu-id="179bf-119">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="179bf-120">Pour obtenir des instructions, consultez [Hadoop de gérer des clusters dans HDInsight à l’aide de hello portail classique Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="179bf-120">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="179bf-121">**toofind nom d’hôte hello**</span><span class="sxs-lookup"><span data-stu-id="179bf-121">**toofind out hello host name**</span></span>

1. <span data-ttu-id="179bf-122">Ouvrez **ligne de commande Hadoop** à partir du bureau de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-122">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="179bf-123">Exécutez hello suivant le suffixe DNS de commande tooget hello :</span><span class="sxs-lookup"><span data-stu-id="179bf-123">Run hello following command tooget hello DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="179bf-124">Notez le **suffixe DNS propre à la connexion**.</span><span class="sxs-lookup"><span data-stu-id="179bf-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="179bf-125">Par exemple, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="179bf-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="179bf-126">Lorsque vous vous connectez tooan HBase cluster, vous devez tooone tooconnect d’envieront hello à l’aide du nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="179bf-126">When you connect tooan HBase cluster, you will need tooconnect tooone of hello Zookeepers using FQDN.</span></span> <span data-ttu-id="179bf-127">Chaque cluster HDInsight contient 3 Zookeepers :</span><span class="sxs-lookup"><span data-stu-id="179bf-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="179bf-128">*zookeeper0*, *zookeeper1* et *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="179bf-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="179bf-129">Hello nom de domaine complet se présente comme *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="179bf-129">hello FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="179bf-130">**toouse SQLUltraLite**</span><span class="sxs-lookup"><span data-stu-id="179bf-130">**toouse SQLLine**</span></span>

1. <span data-ttu-id="179bf-131">Ouvrez **ligne de commande Hadoop** à partir du bureau de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-131">Open **Hadoop Command Line** from hello desktop.</span></span>
2. <span data-ttu-id="179bf-132">Exécutez hello suivant de commandes tooopen SQLUltraLite :</span><span class="sxs-lookup"><span data-stu-id="179bf-132">Run hello following commands tooopen SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [hello FQDN of one of hello Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="179bf-134">commandes Hello utilisées dans l’exemple hello :</span><span class="sxs-lookup"><span data-stu-id="179bf-134">hello commands used in hello sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="179bf-135">Pour plus d’informations, consultez le [manuel SQLLine](http://sqlline.sourceforge.net/#manual) et la [grammaire Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="179bf-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="179bf-136">Utiliser SQuirreL</span><span class="sxs-lookup"><span data-stu-id="179bf-136">Use SQuirreL</span></span>
<span data-ttu-id="179bf-137">[HIPPOCAMPIQUES SQL Client](http://squirrel-sql.sourceforge.net/) est un programme Java graphique qui vous permettent de structure de hello tooview d’une base de données compatible avec JDBC, parcourir les données hello dans les tables, émettre des commandes SQL etc.. Il peut être utilisé tooconnect tooApache Phoenix sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179bf-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you tooview hello structure of a JDBC compliant database, browse hello data in tables, issue SQL commands etc. It can be used tooconnect tooApache Phoenix on HDInsight.</span></span>

<span data-ttu-id="179bf-138">Cette section vous montre comment tooinstall et configurer non sur votre station de travail tooconnect tooan cluster HBase dans HDInsight via VPN.</span><span class="sxs-lookup"><span data-stu-id="179bf-138">This section shows you how tooinstall and configure SQuirreL on your workstation tooconnect tooan HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="179bf-139">Composants requis</span><span class="sxs-lookup"><span data-stu-id="179bf-139">Prerequisites</span></span>
<span data-ttu-id="179bf-140">Avant de suivre les procédures de hello, vous devez disposer de hello :</span><span class="sxs-lookup"><span data-stu-id="179bf-140">Before following hello procedures, you must have hello following:</span></span>

* <span data-ttu-id="179bf-141">Un cluster HBase déployé tooan réseau virtuel Azure avec un ordinateur virtuel DNS.</span><span class="sxs-lookup"><span data-stu-id="179bf-141">An HBase cluster deployed tooan Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="179bf-142">Pour des instructions, consultez [Approvisionnement de clusters HBase sur Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="179bf-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="179bf-143">Obtenir le suffixe DNS spécifique à la connexion cluster hello HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="179bf-143">Get hello HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="179bf-144">tooget il, RDP en cluster de hello, puis exécutez IPConfig.</span><span class="sxs-lookup"><span data-stu-id="179bf-144">tooget it, RDP into hello cluster, and then run IPConfig.</span></span>  <span data-ttu-id="179bf-145">suffixe DNS de Hello est similaire à :</span><span class="sxs-lookup"><span data-stu-id="179bf-145">hello DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="179bf-146">Téléchargez et installez [Microsoft Visual Studio Express pour Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="179bf-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="179bf-147">Vous devez makecert hello package toocreate à partir de votre certificat.</span><span class="sxs-lookup"><span data-stu-id="179bf-147">You will need makecert from hello package toocreate your certificate.</span></span>  
* <span data-ttu-id="179bf-148">Téléchargez et installez l' [environnement d'exécution Java](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="179bf-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="179bf-149">La version 3.0 ou supérieure du client SQL SQuirreL requiert la version 1.6 ou supérieure de JRE.</span><span class="sxs-lookup"><span data-stu-id="179bf-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-toohello-azure-virtual-network"></a><span data-ttu-id="179bf-150">Configurer un toohello de connexion VPN Point à Site réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="179bf-150">Configure a Point-to-Site VPN connection toohello Azure virtual network</span></span>
<span data-ttu-id="179bf-151">La configuration d'une connexion VPN de point à site comprend 3 étapes :</span><span class="sxs-lookup"><span data-stu-id="179bf-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="179bf-152">Configurer un réseau virtuel et une passerelle de routage dynamique</span><span class="sxs-lookup"><span data-stu-id="179bf-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="179bf-153">Créer vos certificats</span><span class="sxs-lookup"><span data-stu-id="179bf-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="179bf-154">Configurer votre client VPN</span><span class="sxs-lookup"><span data-stu-id="179bf-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="179bf-155">Consultez [configurer un tooan de connexion VPN Point à Site réseau virtuel Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="179bf-155">See [Configure a Point-to-Site VPN connection tooan Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="179bf-156">Configurer un réseau virtuel et une passerelle de routage dynamique</span><span class="sxs-lookup"><span data-stu-id="179bf-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="179bf-157">Assurer d’avoir configuré un cluster HBase dans un réseau virtuel Azure (voir la configuration requise de hello pour cette section).</span><span class="sxs-lookup"><span data-stu-id="179bf-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see hello prerequisites for this section).</span></span> <span data-ttu-id="179bf-158">étape suivante de Hello est tooconfigure une connexion point à site.</span><span class="sxs-lookup"><span data-stu-id="179bf-158">hello next step is tooconfigure a point-to-site connection.</span></span>

<span data-ttu-id="179bf-159">**connectivité de point-to-site hello tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="179bf-159">**tooconfigure hello point-to-site connectivity**</span></span>

1. <span data-ttu-id="179bf-160">Connectez-vous à toohello [portail classique Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="179bf-160">Sign in toohello [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="179bf-161">Sur hello gauche, cliquez sur **réseaux**.</span><span class="sxs-lookup"><span data-stu-id="179bf-161">On hello left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="179bf-162">Cliquez sur hello de réseau virtuel que vous avez créé (voir [HBase de configurer des clusters sur un réseau virtuel Azure][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="179bf-162">Click hello virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="179bf-163">Cliquez sur **configurer** à partir du haut de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-163">Click **CONFIGURE** from hello top.</span></span>
5. <span data-ttu-id="179bf-164">Bonjour **connectivité de point-to-site** section, sélectionnez **configurer la connectivité de point-to-site**.</span><span class="sxs-lookup"><span data-stu-id="179bf-164">In hello **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="179bf-165">Configurer **adresse IP de départ** et **CIDR** plage d’adresses IP hello toospecify à partir de laquelle vos clients VPN recevront une adresse IP d’adresses lorsqu’il est connecté.</span><span class="sxs-lookup"><span data-stu-id="179bf-165">Configure **STARTING IP** and **CIDR** toospecify hello IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="179bf-166">Hello ne peuvent se chevaucher avec les hello plages situées sur votre site réseau et hello réseau virtuel Azure, à que vous vous connecterez.</span><span class="sxs-lookup"><span data-stu-id="179bf-166">hello range cannot overlap with any of hello ranges located on your on-premises network and hello Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="179bf-167">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="179bf-167">For example.</span></span> <span data-ttu-id="179bf-168">Si vous avez sélectionné 10.0.0.0/20 pour le réseau virtuel de hello, vous pouvez sélectionner 10.1.0.0/24 pour l’espace d’adressage client hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-168">if you selected 10.0.0.0/20 for hello virtual network, you can select 10.1.0.0/24 for hello client address space.</span></span> <span data-ttu-id="179bf-169">Consultez hello [Point-To-Site connectivité] [ vnet-point-to-site-connectivity] page pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="179bf-169">See hello [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="179bf-170">Dans la section des espaces d’adresse de réseau virtuel hello, cliquez sur **ajouter un sous-réseau de passerelle**.</span><span class="sxs-lookup"><span data-stu-id="179bf-170">In hello virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="179bf-171">Cliquez sur **enregistrer** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-171">Click **SAVE** on hello bottom of hello page.</span></span>
9. <span data-ttu-id="179bf-172">Cliquez sur **Oui** modification de hello tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="179bf-172">Click **YES** tooconfirm hello change.</span></span> <span data-ttu-id="179bf-173">Attendez que le système de hello a terminé hello modifier avant de continuer de la procédure suivante de toohello.</span><span class="sxs-lookup"><span data-stu-id="179bf-173">Wait until hello system has finished making hello change before you proceed toohello next procedure.</span></span>

<span data-ttu-id="179bf-174">**toocreate une passerelle avec routage dynamique**</span><span class="sxs-lookup"><span data-stu-id="179bf-174">**toocreate a dynamic routing gateway**</span></span>

1. <span data-ttu-id="179bf-175">À partir de hello portail classique Azure, cliquez sur **tableau de bord** de haut hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-175">From hello Azure Classic Portal, click **DASHBOARD** from hello top of hello page.</span></span>
2. <span data-ttu-id="179bf-176">Cliquez sur **créer une passerelle** bas hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-176">Click **CREATE GATEWAY** from hello bottom of hello page.</span></span>
3. <span data-ttu-id="179bf-177">Cliquez sur **Oui** tooconfirm.</span><span class="sxs-lookup"><span data-stu-id="179bf-177">Click **YES** tooconfirm.</span></span> <span data-ttu-id="179bf-178">Attendez que la passerelle de hello est créée.</span><span class="sxs-lookup"><span data-stu-id="179bf-178">Wait until hello gateway is created.</span></span>
4. <span data-ttu-id="179bf-179">Cliquez sur **tableau de bord** de haut de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-179">Click **DASHBOARD** from hello top.</span></span>  <span data-ttu-id="179bf-180">Vous verrez un schéma visuel de réseau virtuel de hello :</span><span class="sxs-lookup"><span data-stu-id="179bf-180">You will see a visual diagram of hello virtual network:</span></span>

    ![Diagramme virtuel de point à site du réseau virtuel Azure][img-vnet-diagram]

    <span data-ttu-id="179bf-182">diagramme de Hello montre les connexions clientes, 0.</span><span class="sxs-lookup"><span data-stu-id="179bf-182">hello diagram shows 0 client connections.</span></span> <span data-ttu-id="179bf-183">Une fois que vous apportez à un réseau virtuel toohello de connexion, nombre de hello sera tooone mis à jour.</span><span class="sxs-lookup"><span data-stu-id="179bf-183">After you make a connection toohello virtual network, hello number will be updated tooone.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="179bf-184">Créer vos certificats</span><span class="sxs-lookup"><span data-stu-id="179bf-184">Create your certificates</span></span>
<span data-ttu-id="179bf-185">Une façon toocreate un certificat X.509 est à l’aide de hello outil de création de certificat (makecert.exe) qui est fourni avec [Microsoft Visual Studio Express pour Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="179bf-185">One way toocreate an X.509 certificate is by using hello Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="179bf-186">**toocreate un certificat racine auto-signé**</span><span class="sxs-lookup"><span data-stu-id="179bf-186">**toocreate a self-signed root certificate**</span></span>

1. <span data-ttu-id="179bf-187">Dans votre station de travail, ouvrez une fenêtre d'invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="179bf-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="179bf-188">Accédez toohello dossier des outils Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="179bf-188">Navigate toohello Visual Studio tools folder.</span></span>
3. <span data-ttu-id="179bf-189">Hello suivant de commande dans l’exemple hello ci-dessous crée et installer un certificat racine dans le magasin de certificats personnel hello sur votre station de travail et également créer un fichier .cer que vous téléchargerez plus tard toohello portail classique Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-189">hello following command in hello example below will create and install a root certificate in hello Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload toohello Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="179bf-190">Modifier le répertoire toohello que vous souhaitez hello toobe de fichier .cer situé dans, où HBaseVnetVPNRootCertificate est le nom hello que vous souhaitez toouse pour le certificat de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-190">Change toohello directory that you want hello .cer file toobe located in, where HBaseVnetVPNRootCertificate is hello name that you want toouse for hello certificate.</span></span>

    <span data-ttu-id="179bf-191">Ne fermez pas hello invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="179bf-191">Don't close hello command prompt.</span></span>  <span data-ttu-id="179bf-192">Vous en aurez besoin dans la procédure suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-192">You will need it in hello next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="179bf-193">Étant donné que vous avez créé un certificat racine à partir duquel les certificats de client seront générées, vous pouvez souhaitez tooexport ce certificat avec sa clé privée et l’enregistrer tooa d’emplacement sûr où il peut être récupéré.</span><span class="sxs-lookup"><span data-stu-id="179bf-193">Because you have created a root certificate from which client certificates will be generated, you may want tooexport this certificate along with its private key and save it tooa safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="179bf-194">**toocreate un certificat client**</span><span class="sxs-lookup"><span data-stu-id="179bf-194">**toocreate a client certificate**</span></span>

* <span data-ttu-id="179bf-195">À partir de hello même invite de commandes (il n’a toobe sur hello même ordinateur où vous avez créé le certificat racine de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-195">From hello same command prompt (It has toobe on hello same computer where you created hello root certificate.</span></span> <span data-ttu-id="179bf-196">certificat de client Hello doit être générée à partir du certificat racine de hello), exécution hello commande suivante :</span><span class="sxs-lookup"><span data-stu-id="179bf-196">hello client certificate must be generated from hello root certificate), run hello following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="179bf-197">HBaseVnetVPNRootCertificate est le nom du certificat racine hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-197">HBaseVnetVPNRootCertificate is hello root certificate name.</span></span>  <span data-ttu-id="179bf-198">Il a le nom du certificat racine toomatch hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-198">It has toomatch hello root certificate name.</span></span>  

    <span data-ttu-id="179bf-199">Certificat racine de hello et certificat de client hello sont stockés dans votre magasin de certificats personnel sur votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="179bf-199">Both hello root certificate and hello client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="179bf-200">Utilisez certmgr.msc tooverify.</span><span class="sxs-lookup"><span data-stu-id="179bf-200">Use certmgr.msc tooverify.</span></span>

    ![Certificat VPN de point à site du réseau virtuel Azure][img-certificate]

    <span data-ttu-id="179bf-202">Un certificat client doit être installé sur chaque ordinateur que vous souhaitez le réseau virtuel de tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="179bf-202">A client certificate must be installed on each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="179bf-203">Nous vous recommandons de créer des certificats pour chaque ordinateur que vous souhaitez le réseau virtuel de tooconnect toohello client unique.</span><span class="sxs-lookup"><span data-stu-id="179bf-203">We recommend that you create unique client certificates for each computer that you want tooconnect toohello virtual network.</span></span> <span data-ttu-id="179bf-204">les certificats clients tooexport hello, utilisez certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="179bf-204">tooexport hello client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="179bf-205">**toohello de certificat racine tooupload hello portail classique Azure**</span><span class="sxs-lookup"><span data-stu-id="179bf-205">**tooupload hello root certificate toohello Azure Classic Portal**</span></span>

1. <span data-ttu-id="179bf-206">À partir de hello portail classique Azure, cliquez sur **réseau** sur hello gauche.</span><span class="sxs-lookup"><span data-stu-id="179bf-206">From hello Azure Classic Portal, click **NETWORK** on hello left.</span></span>
2. <span data-ttu-id="179bf-207">Cliquez sur le réseau virtuel hello où votre cluster HBase est déployée sur.</span><span class="sxs-lookup"><span data-stu-id="179bf-207">Click hello virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="179bf-208">Cliquez sur **certificats** à partir du haut de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-208">Click **CERTIFICATES** from hello top.</span></span>
4. <span data-ttu-id="179bf-209">Cliquez sur **télécharger** de hello bas, puis spécifiez le fichier de certificat racine hello que vous avez créé dans la procédure hello avant le dernier.</span><span class="sxs-lookup"><span data-stu-id="179bf-209">Click **UPLOAD** from hello bottom, and specify hello root certificate file you have created in hello procedure before last.</span></span> <span data-ttu-id="179bf-210">Attendez que le certificat de hello a été importé.</span><span class="sxs-lookup"><span data-stu-id="179bf-210">Wait until hello certificate got imported.</span></span>
5. <span data-ttu-id="179bf-211">Cliquez sur **tableau de bord** dessus hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-211">Click **DASHBOARD** on hello top.</span></span>  <span data-ttu-id="179bf-212">diagramme de virtuel de Hello montre l’état de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-212">hello virtual diagram shows hello status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="179bf-213">Configurer votre client VPN</span><span class="sxs-lookup"><span data-stu-id="179bf-213">Configure your VPN client</span></span>
<span data-ttu-id="179bf-214">**toodownload et installez hello le package VPN client**</span><span class="sxs-lookup"><span data-stu-id="179bf-214">**toodownload and install hello client VPN package**</span></span>

1. <span data-ttu-id="179bf-215">À partir de la page du tableau de bord hello du réseau virtuel hello, dans la section Aperçu rapide de hello, cliquez sur **téléchargement hello 64 bits le Package VPN Client** ou **téléchargement hello 32 bits le Package VPN Client** en fonction de votre version de la station de travail du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="179bf-215">From hello DASHBOARD page of hello virtual network, in hello quick glance section, click either **Download hello 64-bit Client VPN Package** or **Download hello 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="179bf-216">Cliquez sur **exécuter** package de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="179bf-216">Click **Run** tooinstall hello package.</span></span>
3. <span data-ttu-id="179bf-217">À l’invite de sécurité hello, cliquez sur **plus d’informations**, puis cliquez sur **quand même exécuter**.</span><span class="sxs-lookup"><span data-stu-id="179bf-217">At hello security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="179bf-218">Cliquez sur **Oui** deux fois.</span><span class="sxs-lookup"><span data-stu-id="179bf-218">Click **Yes** twice.</span></span>

<span data-ttu-id="179bf-219">**tooconnect tooVPN**</span><span class="sxs-lookup"><span data-stu-id="179bf-219">**tooconnect tooVPN**</span></span>

1. <span data-ttu-id="179bf-220">Sur le bureau hello de votre station de travail, cliquez sur icône de réseaux hello sur la barre des tâches hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-220">On hello desktop of your workstation, click hello Networks icon on hello Task bar.</span></span> <span data-ttu-id="179bf-221">Vous devez voir une connexion VPN avec le nom de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="179bf-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="179bf-222">Cliquez sur le nom de la connexion VPN hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-222">Click hello VPN connection name.</span></span>
3. <span data-ttu-id="179bf-223">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="179bf-223">Click **Connect**.</span></span>

<span data-ttu-id="179bf-224">**tootest hello résolution de noms de domaine et de la connexion VPN**</span><span class="sxs-lookup"><span data-stu-id="179bf-224">**tootest hello VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="179bf-225">À partir de la station de travail hello, ouvrez une invite de commandes et la commande ping de hello suivant les noms donnés suffixe DNS du cluster hello HBase est myhbase.b7.internal.cloudapp.net :</span><span class="sxs-lookup"><span data-stu-id="179bf-225">From hello workstation, open a command prompt and ping one of hello following names given hello HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="179bf-226">Installation et configuration de SQuirreL sur votre poste de travail</span><span class="sxs-lookup"><span data-stu-id="179bf-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="179bf-227">**tooinstall non**</span><span class="sxs-lookup"><span data-stu-id="179bf-227">**tooinstall SQuirreL**</span></span>

1. <span data-ttu-id="179bf-228">Téléchargez hello non SQL client jar fichier [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="179bf-228">Download hello SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="179bf-229">Fichier jar ouvrir/exécuter hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-229">Open/run hello jar file.</span></span> <span data-ttu-id="179bf-230">Il requiert hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="179bf-230">It requires hello [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="179bf-231">Cliquez sur **Suivant** deux fois.</span><span class="sxs-lookup"><span data-stu-id="179bf-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="179bf-232">Spécifiez un chemin d’accès où vous avez hello l’autorisation en écriture, puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="179bf-232">Specify a path where you have hello write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="179bf-233">dossier d’installation par défaut Hello est dans le dossier C:\Program Files\squirrel-sql-3.6 de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-233">hello default installation folder is in hello C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="179bf-234">Dans chemin d’accès ordre toowrite toothis, programme d’installation hello doit disposer des privilèges d’administrateur hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-234">In order toowrite toothis path, hello installer must be granted hello administrator privilege.</span></span> <span data-ttu-id="179bf-235">Vous pouvez ouvrir une invite de commandes en tant qu’administrateur, parcourir le dossier bin de tooJava, puis exécutez :</span><span class="sxs-lookup"><span data-stu-id="179bf-235">You can open a command prompt as administrator, navigate tooJava's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="179bf-236">Java.exe-jar [chemin d’accès du fichier jar de non hello le hello]</span><span class="sxs-lookup"><span data-stu-id="179bf-236">java.exe -jar [hello path of hello SQuirreL jar file]</span></span>
5. <span data-ttu-id="179bf-237">Cliquez sur **OK** tooconfirm création du répertoire cible de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-237">Click **OK** tooconfirm creating hello target directory.</span></span>
6. <span data-ttu-id="179bf-238">Hello par défaut est tooinstall hello Base et packages Standard.</span><span class="sxs-lookup"><span data-stu-id="179bf-238">hello default setting is tooinstall hello Base and Standard packages.</span></span>  <span data-ttu-id="179bf-239">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="179bf-239">Click **Next**.</span></span>
7. <span data-ttu-id="179bf-240">Cliquez sur **Suivant** deux fois, puis sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="179bf-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="179bf-241">**pilote de tooinstall hello Phoenix**</span><span class="sxs-lookup"><span data-stu-id="179bf-241">**tooinstall hello Phoenix driver**</span></span>

<span data-ttu-id="179bf-242">fichier jar de Hello phoenix pilote se trouve sur un cluster HBase de hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-242">hello phoenix driver jar file is located on hello HBase cluster.</span></span> <span data-ttu-id="179bf-243">chemin d’accès Hello est similaire toohello suivantes, en fonction des versions de hello :</span><span class="sxs-lookup"><span data-stu-id="179bf-243">hello path is similar toohello following based on hello versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="179bf-244">Vous devez toocopy il tooyour de station de travail sous hello [dossier d’installation non] / lib de chemin d’accès.</span><span class="sxs-lookup"><span data-stu-id="179bf-244">You need toocopy it tooyour workstation under hello [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="179bf-245">Hello plus simple est tooRDP en cluster de hello, puis utilisez fichier copier/coller (CTRL + C et CTRL + V) toocopy il tooyour la station de travail.</span><span class="sxs-lookup"><span data-stu-id="179bf-245">hello easiest way is tooRDP into hello cluster, and then use file copy/paste (CTRL+C and CTRL+V) toocopy it tooyour workstation.</span></span>

<span data-ttu-id="179bf-246">**tooadd un tooSQuirreL de pilote Phoenix**</span><span class="sxs-lookup"><span data-stu-id="179bf-246">**tooadd a Phoenix driver tooSQuirreL**</span></span>

1. <span data-ttu-id="179bf-247">Ouvrez le client SQL SQuirreL dans votre poste de travail.</span><span class="sxs-lookup"><span data-stu-id="179bf-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="179bf-248">Cliquez sur hello **pilote** onglet hello gauche.</span><span class="sxs-lookup"><span data-stu-id="179bf-248">Click hello **Driver** tab on hello left.</span></span>
3. <span data-ttu-id="179bf-249">À partir de hello **pilotes** menu, cliquez sur **nouveau pilote**.</span><span class="sxs-lookup"><span data-stu-id="179bf-249">From hello **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="179bf-250">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="179bf-250">Enter hello following information:</span></span>

   * <span data-ttu-id="179bf-251">**Name**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="179bf-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="179bf-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="179bf-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="179bf-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="179bf-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="179bf-254">Utilisateur toutes les minuscules Bonjour exemple d’URL.</span><span class="sxs-lookup"><span data-stu-id="179bf-254">User all lower case in hello Example URL.</span></span> <span data-ttu-id="179bf-255">Vous pouvez utiliser le quorum complet zookeeper au cas où l’un d’eux est inactif.</span><span class="sxs-lookup"><span data-stu-id="179bf-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="179bf-256">noms d’hôtes Hello sont zookeeper0, zookeeper1 et zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="179bf-256">hello hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Pilote HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. <span data-ttu-id="179bf-258">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="179bf-258">Click **OK**.</span></span>

<span data-ttu-id="179bf-259">**toocreate un cluster HBase de toohello alias**</span><span class="sxs-lookup"><span data-stu-id="179bf-259">**toocreate an alias toohello HBase cluster**</span></span>

1. <span data-ttu-id="179bf-260">À partir de non, cliquez sur hello **alias** onglet hello gauche.</span><span class="sxs-lookup"><span data-stu-id="179bf-260">From SQuirreL, Click hello **Aliases** tab on hello left.</span></span>
2. <span data-ttu-id="179bf-261">À partir de hello **alias** menu, cliquez sur **nouvel Alias**.</span><span class="sxs-lookup"><span data-stu-id="179bf-261">From hello **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="179bf-262">Entrez hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="179bf-262">Enter hello following information:</span></span>

   * <span data-ttu-id="179bf-263">**Nom**: nom de hello du cluster de HBase hello ou n’importe quel nom que vous préférez.</span><span class="sxs-lookup"><span data-stu-id="179bf-263">**Name**: hello name of hello HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="179bf-264">**Driver**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="179bf-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="179bf-265">Cela doit correspondre au nom du pilote hello créé dans la procédure de dernière hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-265">This must match hello driver name you created in hello last procedure.</span></span>
   * <span data-ttu-id="179bf-266">**URL**: hello URL est copié à partir de votre configuration du pilote.</span><span class="sxs-lookup"><span data-stu-id="179bf-266">**URL**: hello URL is copied from your driver configuration.</span></span> <span data-ttu-id="179bf-267">Assurez-vous que toouser toutes les minuscules.</span><span class="sxs-lookup"><span data-stu-id="179bf-267">Make sure toouser all lower case.</span></span>
   * <span data-ttu-id="179bf-268">**Nom d’utilisateur**: il s’agit de texte.</span><span class="sxs-lookup"><span data-stu-id="179bf-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="179bf-269">Étant donné que vous utilisez ici connectivité VPN, nom d’utilisateur hello n’est pas utilisée.</span><span class="sxs-lookup"><span data-stu-id="179bf-269">Because you use VPN connectivity here, hello user name is not used at all.</span></span>
   * <span data-ttu-id="179bf-270">**Password**: il s’agit de texte.</span><span class="sxs-lookup"><span data-stu-id="179bf-270">**Password**: It can be any text.</span></span>

     ![Pilote HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. <span data-ttu-id="179bf-272">Cliquez sur **Test**.</span><span class="sxs-lookup"><span data-stu-id="179bf-272">Click **Test**.</span></span>
5. <span data-ttu-id="179bf-273">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="179bf-273">Click **Connect**.</span></span> <span data-ttu-id="179bf-274">Lorsqu’elle s’effectue de connexion de hello, non l’aspect suivant :</span><span class="sxs-lookup"><span data-stu-id="179bf-274">When it makes hello connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="179bf-276">**toorun un test**</span><span class="sxs-lookup"><span data-stu-id="179bf-276">**toorun a test**</span></span>

1. <span data-ttu-id="179bf-277">Cliquez sur hello **SQL** onglet droite suivant toohello **objets** onglet.</span><span class="sxs-lookup"><span data-stu-id="179bf-277">Click hello **SQL** tab right next toohello **Objects** tab.</span></span>
2. <span data-ttu-id="179bf-278">Copiez et collez hello suivant de code :</span><span class="sxs-lookup"><span data-stu-id="179bf-278">Copy and paste hello following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="179bf-279">Cliquez sur le bouton d’exécution hello.</span><span class="sxs-lookup"><span data-stu-id="179bf-279">Click hello run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="179bf-281">Commutateur précédent toohello **objets** onglet.</span><span class="sxs-lookup"><span data-stu-id="179bf-281">Switch back toohello **Objects** tab.</span></span>
5. <span data-ttu-id="179bf-282">Nom d’alias hello, puis **TABLE**.</span><span class="sxs-lookup"><span data-stu-id="179bf-282">Expand hello alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="179bf-283">Vous devez voir hello nouvelle table répertorié sous.</span><span class="sxs-lookup"><span data-stu-id="179bf-283">You shall see hello new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="179bf-284">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="179bf-284">Next steps</span></span>
<span data-ttu-id="179bf-285">Dans cet article, vous avez appris comment toouse Phoenix Apache dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179bf-285">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="179bf-286">toolearn, voir</span><span class="sxs-lookup"><span data-stu-id="179bf-286">toolearn more, see</span></span>

* <span data-ttu-id="179bf-287">[Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.</span><span class="sxs-lookup"><span data-stu-id="179bf-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="179bf-288">[Configurer des clusters HBase sur un réseau virtuel Azure][hdinsight-hbase-provision-vnet]: avec l’intégration de réseau virtuel, clusters HBase peuvent être déployé toohello même virtuel réseau en tant que vos applications, ainsi que les applications peuvent communiquer avec HBase directement.</span><span class="sxs-lookup"><span data-stu-id="179bf-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="179bf-289">[Configurer la réplication de HBase de HDInsight](hdinsight-hbase-replication.md): Découvrez comment tooconfigure HBase la réplication entre deux centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="179bf-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="179bf-290">[Analyse des sentiments Twitter avec HBase dans HDInsight][hbase-twitter-sentiment]: Découvrez comment toodo en temps réel [analyse des sentiments](http://en.wikipedia.org/wiki/Sentiment_analysis) de données à l’aide de HBase dans un cluster Hadoop dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="179bf-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
