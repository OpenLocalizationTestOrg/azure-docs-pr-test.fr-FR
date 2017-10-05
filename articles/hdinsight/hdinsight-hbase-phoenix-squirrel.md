---
title: Utiliser Apache Phoenix et SQuirreL avec Azure HDInsight Windows | Microsoft Docs
description: "Découvrez comment utiliser Apache Phoenix dans HDInsight et comment installer et configurer SQuirreL sur votre poste de travail pour vous connecter à un cluster HBase dans HDInsight."
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
ms.openlocfilehash: 024b70df99fdefa1598225ebb1fbfee85ea375d0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="use-apache-phoenix-and-squirrel-with-windows-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="497b4-103">Utiliser Apache Phoenix et SQuirreL avec les clusters HBase basés sur Windows dans HDInsight</span><span class="sxs-lookup"><span data-stu-id="497b4-103">Use Apache Phoenix and SQuirreL with Windows-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="497b4-104">Découvrez comment utiliser [Apache Phoenix](http://phoenix.apache.org/) dans HDInsight et comment installer et configurer SQuirreL sur votre poste de travail pour vous connecter à un cluster HBase dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="497b4-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight.</span></span> <span data-ttu-id="497b4-105">Pour plus d'informations sur Phoenix, consultez [Phoenix en 15 minutes ou moins](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="497b4-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="497b4-106">Pour en savoir plus sur la grammaire Phoenix, consultez la page [Grammaire Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="497b4-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="497b4-107">Pour plus d’informations sur la version de Phoenix dans HDInsight, consultez [Nouveautés des versions de cluster Hadoop fournies par HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="497b4-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>

> [!IMPORTANT]
> <span data-ttu-id="497b4-108">Les étapes décrites dans ce document fonctionnent uniquement pour les clusters HDInsight Windows.</span><span class="sxs-lookup"><span data-stu-id="497b4-108">The steps in this document only work for Windows-based HDInsight clusters.</span></span> <span data-ttu-id="497b4-109">HDInsight est uniquement disponible sur Windows pour les versions antérieures à HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="497b4-109">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="497b4-110">Linux est le seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="497b4-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="497b4-111">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="497b4-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="497b4-112">Pour plus d’informations sur l’utilisation de Phoenix dans HDInsight sous Linux, consultez [Utilisation d’Apache Phoenix avec les clusters HBase basés sur Linux dans HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span><span class="sxs-lookup"><span data-stu-id="497b4-112">For information on using Phoenix on Linux-based HDInsight, see [Use Apache Phoenix with Linux-based HBase clusters in HDInsight](hdinsight-hbase-phoenix-squirrel-linux.md).</span></span>
>



## <a name="use-sqlline"></a><span data-ttu-id="497b4-113">Utiliser SQLLine</span><span class="sxs-lookup"><span data-stu-id="497b4-113">Use SQLLine</span></span>
<span data-ttu-id="497b4-114">[SQLLine](http://sqlline.sourceforge.net/) est un utilitaire de ligne de commande pour exécuter SQL.</span><span class="sxs-lookup"><span data-stu-id="497b4-114">[SQLLine](http://sqlline.sourceforge.net/) is a command line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="497b4-115">Composants requis</span><span class="sxs-lookup"><span data-stu-id="497b4-115">Prerequisites</span></span>
<span data-ttu-id="497b4-116">Avant de pouvoir utiliser SQLLine, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="497b4-116">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="497b4-117">**Un cluster HBase dans HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="497b4-117">**A HBase cluster in HDInsight**.</span></span> <span data-ttu-id="497b4-118">Pour plus d’informations sur l’approvisionnement d’un cluster HBase, consultez [Prise en main d’Apache HBase dans HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="497b4-118">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="497b4-119">**Une connexion au cluster HBase à l'aide du protocole RDP (Remote Desktop Protocol)**.</span><span class="sxs-lookup"><span data-stu-id="497b4-119">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="497b4-120">Pour obtenir des instructions, consultez [Gestion des clusters Hadoop dans HDInsight au moyen du portail Azure Classic][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="497b4-120">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure Classic Portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="497b4-121">**Pour déterminer le nom d'hôte**</span><span class="sxs-lookup"><span data-stu-id="497b4-121">**To find out the host name**</span></span>

1. <span data-ttu-id="497b4-122">Ouvrez la **ligne de commande Hadoop** à partir du Bureau.</span><span class="sxs-lookup"><span data-stu-id="497b4-122">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="497b4-123">Exécutez la commande suivante pour obtenir le suffixe DNS :</span><span class="sxs-lookup"><span data-stu-id="497b4-123">Run the following command to get the DNS suffix:</span></span>

        ipconfig

    <span data-ttu-id="497b4-124">Notez le **suffixe DNS propre à la connexion**.</span><span class="sxs-lookup"><span data-stu-id="497b4-124">Write down **Connection-specific DNS Suffix**.</span></span> <span data-ttu-id="497b4-125">Par exemple, *myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="497b4-125">For example, *myhbasecluster.f5.internal.cloudapp.net*.</span></span> <span data-ttu-id="497b4-126">Quand vous vous connectez à un cluster HBase, vous devez vous connecter à l'un des Zookeepers avec le nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="497b4-126">When you connect to an HBase cluster, you will need to connect to one of the Zookeepers using FQDN.</span></span> <span data-ttu-id="497b4-127">Chaque cluster HDInsight contient 3 Zookeepers :</span><span class="sxs-lookup"><span data-stu-id="497b4-127">Each HDInsight cluster has 3 Zookeepers.</span></span> <span data-ttu-id="497b4-128">*zookeeper0*, *zookeeper1* et *zookeeper2*.</span><span class="sxs-lookup"><span data-stu-id="497b4-128">They are *zookeeper0*, *zookeeper1*, and *zookeeper2*.</span></span> <span data-ttu-id="497b4-129">Le nom de domaine complet doit ressembler à *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="497b4-129">The FQDN will be something like *zookeeper2.myhbasecluster.f5.internal.cloudapp.net*.</span></span>

<span data-ttu-id="497b4-130">**Pour utiliser SQLLine**</span><span class="sxs-lookup"><span data-stu-id="497b4-130">**To use SQLLine**</span></span>

1. <span data-ttu-id="497b4-131">Ouvrez la **ligne de commande Hadoop** à partir du Bureau.</span><span class="sxs-lookup"><span data-stu-id="497b4-131">Open **Hadoop Command Line** from the desktop.</span></span>
2. <span data-ttu-id="497b4-132">Exécutez les commandes suivantes pour ouvrir SQLLine :</span><span class="sxs-lookup"><span data-stu-id="497b4-132">Run the following commands to open SQLLine:</span></span>

        cd %phoenix_home%\bin
        sqlline.py [The FQDN of one of the Zookeepers]

    ![HDInsight hbase phoenix sqlline][hdinsight-hbase-phoenix-sqlline]

    <span data-ttu-id="497b4-134">Commandes utilisées dans l’exemple :</span><span class="sxs-lookup"><span data-stu-id="497b4-134">The commands used in the sample:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

<span data-ttu-id="497b4-135">Pour plus d’informations, consultez le [manuel SQLLine](http://sqlline.sourceforge.net/#manual) et la [grammaire Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="497b4-135">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="use-squirrel"></a><span data-ttu-id="497b4-136">Utiliser SQuirreL</span><span class="sxs-lookup"><span data-stu-id="497b4-136">Use SQuirreL</span></span>
<span data-ttu-id="497b4-137">Le [client SQuirrel SQL](http://squirrel-sql.sourceforge.net/) est un programme Java graphique qui vous permet d’afficher la structure d’une base de données compatible JDBC, parcourir les données dans des tables, exécuter des commandes SQL, etc. SQuirreL peut être utilisé pour se connecter à Phoenix Apache sur HDInsight.</span><span class="sxs-lookup"><span data-stu-id="497b4-137">[SQuirreL SQL Client](http://squirrel-sql.sourceforge.net/) is a graphical Java program that will allow you to view the structure of a JDBC compliant database, browse the data in tables, issue SQL commands etc. It can be used to connect to Apache Phoenix on HDInsight.</span></span>

<span data-ttu-id="497b4-138">Cette section vous indique comment installer et configurer SQuirreL sur votre poste de travail pour vous connecter à un cluster HBase dans HDInsight via une connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="497b4-138">This section shows you how to install and configure SQuirreL on your workstation to connect to an HBase cluster in HDInsight via VPN.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="497b4-139">Composants requis</span><span class="sxs-lookup"><span data-stu-id="497b4-139">Prerequisites</span></span>
<span data-ttu-id="497b4-140">Avant de suivre les procédures, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="497b4-140">Before following the procedures, you must have the following:</span></span>

* <span data-ttu-id="497b4-141">Un cluster HBase déployé sur un réseau virtuel Azure avec une machine virtuelle DNS.</span><span class="sxs-lookup"><span data-stu-id="497b4-141">An HBase cluster deployed to an Azure virtual network with a DNS virtual machine.</span></span>  <span data-ttu-id="497b4-142">Pour des instructions, consultez [Approvisionnement de clusters HBase sur Azure Virtual Network][hdinsight-hbase-provision-vnet].</span><span class="sxs-lookup"><span data-stu-id="497b4-142">For instructions, see [Create HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet].</span></span>

* <span data-ttu-id="497b4-143">Obtenez le suffixe DNS propre à la connexion du cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="497b4-143">Get the HBase cluster cluster Connection-specific DNS suffix.</span></span> <span data-ttu-id="497b4-144">Pour l'obtenir, ouvrez une session RDP sur le cluster, puis exécutez IPConfig.</span><span class="sxs-lookup"><span data-stu-id="497b4-144">To get it, RDP into the cluster, and then run IPConfig.</span></span>  <span data-ttu-id="497b4-145">Le suffixe DNS doit ressembler à :</span><span class="sxs-lookup"><span data-stu-id="497b4-145">The DNS suffix is similar to:</span></span>

        myhbase.b7.internal.cloudapp.net
* <span data-ttu-id="497b4-146">Téléchargez et installez [Microsoft Visual Studio Express pour Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="497b4-146">Download and install [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx) on your workstation.</span></span> <span data-ttu-id="497b4-147">Vous utiliserez l'outil makecert du package pour créer votre certificat.</span><span class="sxs-lookup"><span data-stu-id="497b4-147">You will need makecert from the package to create your certificate.</span></span>  
* <span data-ttu-id="497b4-148">Téléchargez et installez l' [environnement d'exécution Java](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="497b4-148">Download and install [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html) on your workstation.</span></span>  <span data-ttu-id="497b4-149">La version 3.0 ou supérieure du client SQL SQuirreL requiert la version 1.6 ou supérieure de JRE.</span><span class="sxs-lookup"><span data-stu-id="497b4-149">SQuirreL SQL client version 3.0 and higher requires JRE version 1.6 or higher.</span></span>  

### <a name="configure-a-point-to-site-vpn-connection-to-the-azure-virtual-network"></a><span data-ttu-id="497b4-150">Configurer une connexion VPN de point à site au réseau virtuel Azure</span><span class="sxs-lookup"><span data-stu-id="497b4-150">Configure a Point-to-Site VPN connection to the Azure virtual network</span></span>
<span data-ttu-id="497b4-151">La configuration d'une connexion VPN de point à site comprend 3 étapes :</span><span class="sxs-lookup"><span data-stu-id="497b4-151">There are 3 steps involved configuring a point-to-site VPN connection:</span></span>

1. [<span data-ttu-id="497b4-152">Configurer un réseau virtuel et une passerelle de routage dynamique</span><span class="sxs-lookup"><span data-stu-id="497b4-152">Configure a virtual network and a dynamic routing gateway</span></span>](#Configure-a-virtual-network-and-a-dynamic-routing-gateway)
2. [<span data-ttu-id="497b4-153">Créer vos certificats</span><span class="sxs-lookup"><span data-stu-id="497b4-153">Create your certificates</span></span>](#Create-your-certificates)
3. [<span data-ttu-id="497b4-154">Configurer votre client VPN</span><span class="sxs-lookup"><span data-stu-id="497b4-154">Configure your VPN client</span></span>](#Configure-your-VPN-client)

<span data-ttu-id="497b4-155">Consultez [Configurer une connexion VPN de point à site à un réseau virtuel Azure](../vpn-gateway/vpn-gateway-point-to-site-create.md) pour plus d'informations</span><span class="sxs-lookup"><span data-stu-id="497b4-155">See [Configure a Point-to-Site VPN connection to an Azure Virtual Network](../vpn-gateway/vpn-gateway-point-to-site-create.md) for more information.</span></span>

#### <a name="configure-a-virtual-network-and-a-dynamic-routing-gateway"></a><span data-ttu-id="497b4-156">Configurer un réseau virtuel et une passerelle de routage dynamique</span><span class="sxs-lookup"><span data-stu-id="497b4-156">Configure a virtual network and a dynamic routing gateway</span></span>
<span data-ttu-id="497b4-157">Assurez-vous d'avoir approvisionné un cluster HBase dans un réseau virtuel Azure (voir la configuration requise pour cette section).</span><span class="sxs-lookup"><span data-stu-id="497b4-157">Assure you have provisioned an HBase cluster in an Azure virtual network (see the prerequisites for this section).</span></span> <span data-ttu-id="497b4-158">L'étape suivante consiste à configurer une connexion de point à site.</span><span class="sxs-lookup"><span data-stu-id="497b4-158">The next step is to configure a point-to-site connection.</span></span>

<span data-ttu-id="497b4-159">**Pour configurer la connexion de point à site**</span><span class="sxs-lookup"><span data-stu-id="497b4-159">**To configure the point-to-site connectivity**</span></span>

1. <span data-ttu-id="497b4-160">Connectez-vous au [portail Azure Classic][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="497b4-160">Sign in to the [Azure Classic Portal][azure-portal].</span></span>
2. <span data-ttu-id="497b4-161">Dans le volet gauche, cliquez sur **RÉSEAUX**.</span><span class="sxs-lookup"><span data-stu-id="497b4-161">On the left, click **NETWORKS**.</span></span>
3. <span data-ttu-id="497b4-162">Cliquez sur le réseau virtuel que vous avez créé (voir [Approvisionnement de clusters HBase sur Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span><span class="sxs-lookup"><span data-stu-id="497b4-162">Click the virtual network you have created (see [Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]).</span></span>
4. <span data-ttu-id="497b4-163">Cliquez sur **CONFIGURER** en haut.</span><span class="sxs-lookup"><span data-stu-id="497b4-163">Click **CONFIGURE** from the top.</span></span>
5. <span data-ttu-id="497b4-164">Dans la section **connectivité de point à site**, sélectionnez **Configurer la connectivité de point à site**.</span><span class="sxs-lookup"><span data-stu-id="497b4-164">In the **point-to-site connectivity** section, select **Configure point-to-site connectivity**.</span></span>
6. <span data-ttu-id="497b4-165">Configurez **IP DE DÉPART** et **CIDR** pour spécifier la plage d’adresses IP qui déterminera l’adresse IP de vos clients VPN au moment de la connexion.</span><span class="sxs-lookup"><span data-stu-id="497b4-165">Configure **STARTING IP** and **CIDR** to specify the IP address range from which your VPN clients will receive an IP address when connected.</span></span> <span data-ttu-id="497b4-166">La plage ne peut pas chevaucher les plages de votre réseau local et du réseau virtuel Azure auquel vous allez vous connecter.</span><span class="sxs-lookup"><span data-stu-id="497b4-166">The range cannot overlap with any of the ranges located on your on-premises network and the Azure virtual network you will be connecting to.</span></span> <span data-ttu-id="497b4-167">Par exemple,</span><span class="sxs-lookup"><span data-stu-id="497b4-167">For example.</span></span> <span data-ttu-id="497b4-168">si vous avez sélectionné 10.0.0.0/20 pour le réseau virtuel, vous pouvez sélectionner 10.1.0.0/24 pour l’espace d’adressage du client.</span><span class="sxs-lookup"><span data-stu-id="497b4-168">if you selected 10.0.0.0/20 for the virtual network, you can select 10.1.0.0/24 for the client address space.</span></span> <span data-ttu-id="497b4-169">Consultez la page [Connectivité de point à site][vnet-point-to-site-connectivity] pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="497b4-169">See the [Point-To-Site Connectivity][vnet-point-to-site-connectivity] page for more information.</span></span>
7. <span data-ttu-id="497b4-170">Dans la section des espaces d'adressage de réseau virtuel, cliquez sur **ajouter un sous-réseau de passerelle**.</span><span class="sxs-lookup"><span data-stu-id="497b4-170">In the virtual network address spaces section, click **add gateway subnet**.</span></span>
8. <span data-ttu-id="497b4-171">Cliquez sur **ENREGISTRER** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="497b4-171">Click **SAVE** on the bottom of the page.</span></span>
9. <span data-ttu-id="497b4-172">Cliquez sur **OUI** pour confirmer la modification.</span><span class="sxs-lookup"><span data-stu-id="497b4-172">Click **YES** to confirm the change.</span></span> <span data-ttu-id="497b4-173">Attendez que le système ait terminé d'appliquer la modification avant de passer à la procédure suivante.</span><span class="sxs-lookup"><span data-stu-id="497b4-173">Wait until the system has finished making the change before you proceed to the next procedure.</span></span>

<span data-ttu-id="497b4-174">**Pour créer une passerelle de routage dynamique**</span><span class="sxs-lookup"><span data-stu-id="497b4-174">**To create a dynamic routing gateway**</span></span>

1. <span data-ttu-id="497b4-175">Dans le portail Azure Classic, cliquez sur **TABLEAU DE BORD** en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="497b4-175">From the Azure Classic Portal, click **DASHBOARD** from the top of the page.</span></span>
2. <span data-ttu-id="497b4-176">Cliquez sur **CRÉER UNE PASSERELLE** en bas de la page.</span><span class="sxs-lookup"><span data-stu-id="497b4-176">Click **CREATE GATEWAY** from the bottom of the page.</span></span>
3. <span data-ttu-id="497b4-177">Cliquez sur **OUI** pour confirmer.</span><span class="sxs-lookup"><span data-stu-id="497b4-177">Click **YES** to confirm.</span></span> <span data-ttu-id="497b4-178">Attendez que la passerelle soit créée.</span><span class="sxs-lookup"><span data-stu-id="497b4-178">Wait until the gateway is created.</span></span>
4. <span data-ttu-id="497b4-179">Cliquez sur **TABLEAU DE BORD** en haut.</span><span class="sxs-lookup"><span data-stu-id="497b4-179">Click **DASHBOARD** from the top.</span></span>  <span data-ttu-id="497b4-180">Un schéma visuel du réseau virtuel est affiché :</span><span class="sxs-lookup"><span data-stu-id="497b4-180">You will see a visual diagram of the virtual network:</span></span>

    ![Diagramme virtuel de point à site du réseau virtuel Azure][img-vnet-diagram]

    <span data-ttu-id="497b4-182">Le diagramme indique 0 connexion du client.</span><span class="sxs-lookup"><span data-stu-id="497b4-182">The diagram shows 0 client connections.</span></span> <span data-ttu-id="497b4-183">Une fois établie la connexion au réseau virtuel, le nombre passe à un.</span><span class="sxs-lookup"><span data-stu-id="497b4-183">After you make a connection to the virtual network, the number will be updated to one.</span></span>

#### <a name="create-your-certificates"></a><span data-ttu-id="497b4-184">Créer vos certificats</span><span class="sxs-lookup"><span data-stu-id="497b4-184">Create your certificates</span></span>
<span data-ttu-id="497b4-185">L’une des méthodes pour créer un certificat X.509 consiste à utiliser l'outil de création de certificats (makecert.exe) fourni avec [Microsoft Visual Studio Express pour Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="497b4-185">One way to create an X.509 certificate is by using the Certificate Creation Tool (makecert.exe) that comes with [Microsoft Visual Studio Express for Windows Desktop](https://www.visualstudio.com/products/visual-studio-express-vs.aspx).</span></span>

<span data-ttu-id="497b4-186">**Pour créer un certificat racine auto-signé**</span><span class="sxs-lookup"><span data-stu-id="497b4-186">**To create a self-signed root certificate**</span></span>

1. <span data-ttu-id="497b4-187">Dans votre station de travail, ouvrez une fenêtre d'invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="497b4-187">From your workstation, open a command prompt window.</span></span>
2. <span data-ttu-id="497b4-188">Accédez au dossier des outils Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="497b4-188">Navigate to the Visual Studio tools folder.</span></span>
3. <span data-ttu-id="497b4-189">La commande suivante dans l'exemple ci-dessous crée et installe un certificat racine dans le magasin de certificats Personal sur votre station de travail, ainsi que le fichier .cer correspondant que vous téléchargerez plus tard dans le portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="497b4-189">The following command in the example below will create and install a root certificate in the Personal certificate store on your workstation and also create a corresponding .cer file that you’ll later upload to the Azure Classic Portal.</span></span>

        makecert -sky exchange -r -n "CN=HBaseVnetVPNRootCertificate" -pe -a sha1 -len 2048 -ss My "C:\Users\JohnDole\Desktop\HBaseVNetVPNRootCertificate.cer"

    <span data-ttu-id="497b4-190">Indiquez le répertoire de destination du fichier .cer, HBaseVnetVPNRootCertificate étant le nom que vous voulez utiliser pour le certificat.</span><span class="sxs-lookup"><span data-stu-id="497b4-190">Change to the directory that you want the .cer file to be located in, where HBaseVnetVPNRootCertificate is the name that you want to use for the certificate.</span></span>

    <span data-ttu-id="497b4-191">Ne fermez pas l'invite de commandes.</span><span class="sxs-lookup"><span data-stu-id="497b4-191">Don't close the command prompt.</span></span>  <span data-ttu-id="497b4-192">Vous en aurez besoin dans la prochaine procédure.</span><span class="sxs-lookup"><span data-stu-id="497b4-192">You will need it in the next procedure.</span></span>

   > [!NOTE]
   > <span data-ttu-id="497b4-193">Comme vous avez créé un certificat racine permettant de générer des certificats clients, il peut être utile d'exporter ce certificat avec sa clé privée et de l'enregistrer à un emplacement sûr à partir duquel il pourra être récupéré.</span><span class="sxs-lookup"><span data-stu-id="497b4-193">Because you have created a root certificate from which client certificates will be generated, you may want to export this certificate along with its private key and save it to a safe location where it may be recovered.</span></span>
   >
   >

<span data-ttu-id="497b4-194">**Pour créer un certificat client**</span><span class="sxs-lookup"><span data-stu-id="497b4-194">**To create a client certificate**</span></span>

* <span data-ttu-id="497b4-195">Dans la même invite de commandes (sur le même ordinateur que celui où vous avez créé le certificat racine,</span><span class="sxs-lookup"><span data-stu-id="497b4-195">From the same command prompt (It has to be on the same computer where you created the root certificate.</span></span> <span data-ttu-id="497b4-196">le certificat client doit être généré à partir du certificat racine), exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="497b4-196">The client certificate must be generated from the root certificate), run the following command:</span></span>

          makecert.exe -n "CN=HBaseVnetVPNClientCertificate" -pe -sky exchange -m 96 -ss My -in "HBaseVnetVPNRootCertificate" -is my -a sha1

    <span data-ttu-id="497b4-197">HBaseVnetVPNRootCertificate est le nom du certificat racine.</span><span class="sxs-lookup"><span data-stu-id="497b4-197">HBaseVnetVPNRootCertificate is the root certificate name.</span></span>  <span data-ttu-id="497b4-198">Il doit correspondre au nom du certificat racine.</span><span class="sxs-lookup"><span data-stu-id="497b4-198">It has to match the root certificate name.</span></span>  

    <span data-ttu-id="497b4-199">Le certificat racine et le certificat client sont stockés dans le magasin de certificats personnels de votre ordinateur.</span><span class="sxs-lookup"><span data-stu-id="497b4-199">Both the root certificate and the client certificate are stored in your Personal certificate store on your computer.</span></span> <span data-ttu-id="497b4-200">Utilisez certmgr.msc à des fins de vérification.</span><span class="sxs-lookup"><span data-stu-id="497b4-200">Use certmgr.msc to verify.</span></span>

    ![Certificat VPN de point à site du réseau virtuel Azure][img-certificate]

    <span data-ttu-id="497b4-202">Vous devez installer un certificat client sur chaque ordinateur que vous voulez connecter au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="497b4-202">A client certificate must be installed on each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="497b4-203">Nous vous recommandons de créer un certificat client unique pour chaque ordinateur que vous souhaitez connecter au réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="497b4-203">We recommend that you create unique client certificates for each computer that you want to connect to the virtual network.</span></span> <span data-ttu-id="497b4-204">Pour exporter les certificats clients, utilisez certmgr.msc.</span><span class="sxs-lookup"><span data-stu-id="497b4-204">To export the client certificates, use certmgr.msc.</span></span>

<span data-ttu-id="497b4-205">**Pour télécharger le certificat racine sur le portail Azure Classic**</span><span class="sxs-lookup"><span data-stu-id="497b4-205">**To upload the root certificate to the Azure Classic Portal**</span></span>

1. <span data-ttu-id="497b4-206">Dans le portail Azure Classic, cliquez sur **RÉSEAU** à gauche.</span><span class="sxs-lookup"><span data-stu-id="497b4-206">From the Azure Classic Portal, click **NETWORK** on the left.</span></span>
2. <span data-ttu-id="497b4-207">Cliquez sur le réseau virtuel sur lequel est déployé votre cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="497b4-207">Click the virtual network where your HBase cluster is deployed to.</span></span>
3. <span data-ttu-id="497b4-208">Cliquez sur **CERTIFICATS** en haut.</span><span class="sxs-lookup"><span data-stu-id="497b4-208">Click **CERTIFICATES** from the top.</span></span>
4. <span data-ttu-id="497b4-209">Cliquez sur **TÉLÉCHARGER** en bas et spécifiez le fichier de certificat racine que vous avez créé dans l'avant-dernière procédure.</span><span class="sxs-lookup"><span data-stu-id="497b4-209">Click **UPLOAD** from the bottom, and specify the root certificate file you have created in the procedure before last.</span></span> <span data-ttu-id="497b4-210">Attendez que le certificat soit importé.</span><span class="sxs-lookup"><span data-stu-id="497b4-210">Wait until the certificate got imported.</span></span>
5. <span data-ttu-id="497b4-211">Cliquez sur **TABLEAU DE BORD** en haut.</span><span class="sxs-lookup"><span data-stu-id="497b4-211">Click **DASHBOARD** on the top.</span></span>  <span data-ttu-id="497b4-212">Le diagramme virtuel affiche l'état.</span><span class="sxs-lookup"><span data-stu-id="497b4-212">The virtual diagram shows the status.</span></span>

#### <a name="configure-your-vpn-client"></a><span data-ttu-id="497b4-213">Configurer votre client VPN</span><span class="sxs-lookup"><span data-stu-id="497b4-213">Configure your VPN client</span></span>
<span data-ttu-id="497b4-214">**Pour télécharger et installer le package client VPN**</span><span class="sxs-lookup"><span data-stu-id="497b4-214">**To download and install the client VPN package**</span></span>

1. <span data-ttu-id="497b4-215">Dans la page TABLEAU DE BORD du réseau virtuel, dans la section aperçu rapide, cliquez sur **Télécharger le package client VPN 64 bits** ou **Télécharger le package client VPN 32 bits** selon la version du système d’exploitation de votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="497b4-215">From the DASHBOARD page of the virtual network, in the quick glance section, click either **Download the 64-bit Client VPN Package** or **Download the 32-bit Client VPN Package** based on your workstation OS version.</span></span>
2. <span data-ttu-id="497b4-216">Cliquez sur **Exécuter** pour installer le package.</span><span class="sxs-lookup"><span data-stu-id="497b4-216">Click **Run** to install the package.</span></span>
3. <span data-ttu-id="497b4-217">À l’invite de sécurité, cliquez sur **Plus d’informations**, puis sur **Exécuter quand même**.</span><span class="sxs-lookup"><span data-stu-id="497b4-217">At the security prompt, click **More info**, and then click **Run anyway**.</span></span>
4. <span data-ttu-id="497b4-218">Cliquez sur **Oui** deux fois.</span><span class="sxs-lookup"><span data-stu-id="497b4-218">Click **Yes** twice.</span></span>

<span data-ttu-id="497b4-219">**Pour se connecter au VPN**</span><span class="sxs-lookup"><span data-stu-id="497b4-219">**To connect to VPN**</span></span>

1. <span data-ttu-id="497b4-220">Sur le Bureau de votre poste de travail, cliquez sur l'icône Réseaux de la barre des tâches.</span><span class="sxs-lookup"><span data-stu-id="497b4-220">On the desktop of your workstation, click the Networks icon on the Task bar.</span></span> <span data-ttu-id="497b4-221">Vous devez voir une connexion VPN avec le nom de votre réseau virtuel.</span><span class="sxs-lookup"><span data-stu-id="497b4-221">You shall see a VPN connection with your virtual network name.</span></span>
2. <span data-ttu-id="497b4-222">Cliquez sur le nom de la connexion VPN.</span><span class="sxs-lookup"><span data-stu-id="497b4-222">Click the VPN connection name.</span></span>
3. <span data-ttu-id="497b4-223">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="497b4-223">Click **Connect**.</span></span>

<span data-ttu-id="497b4-224">**Pour tester la connexion VPN et la résolution de noms de domaine**</span><span class="sxs-lookup"><span data-stu-id="497b4-224">**To test the VPN connection and domain name resolution**</span></span>

* <span data-ttu-id="497b4-225">Dans la station de travail, ouvrez une invite de commandes et testez l'un des noms suivants, le suffixe DNS du cluster HBase étant myhbase.b7.internal.cloudapp.net :</span><span class="sxs-lookup"><span data-stu-id="497b4-225">From the workstation, open a command prompt and ping one of the following names given the HBase cluster's DNS suffix is myhbase.b7.internal.cloudapp.net:</span></span>

        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        zookeeper0.myhbase.b7.internal.cloudapp.net
        headnode0.myhbase.b7.internal.cloudapp.net
        headnode1.myhbase.b7.internal.cloudapp.net
        workernode0.myhbase.b7.internal.cloudapp.net

### <a name="install-and-configure-squirrel-on-your-workstation"></a><span data-ttu-id="497b4-226">Installation et configuration de SQuirreL sur votre poste de travail</span><span class="sxs-lookup"><span data-stu-id="497b4-226">Install and configure SQuirreL on your workstation</span></span>
<span data-ttu-id="497b4-227">**Pour installer SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="497b4-227">**To install SQuirreL**</span></span>

1. <span data-ttu-id="497b4-228">Téléchargez le fichier jar du client SQL SQuirreL à l’adresse [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span><span class="sxs-lookup"><span data-stu-id="497b4-228">Download the SQuirreL SQL client jar file from [http://squirrel-sql.sourceforge.net/#installation](http://squirrel-sql.sourceforge.net/#installation).</span></span>
2. <span data-ttu-id="497b4-229">Ouvrez/exécutez le fichier jar.</span><span class="sxs-lookup"><span data-stu-id="497b4-229">Open/run the jar file.</span></span> <span data-ttu-id="497b4-230">Pour cela, vous avez besoin de l' [environnement d'exécution Java](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span><span class="sxs-lookup"><span data-stu-id="497b4-230">It requires the [Java Runtime Environment](http://www.oracle.com/technetwork/java/javase/downloads/jre7-downloads-1880261.html).</span></span>
3. <span data-ttu-id="497b4-231">Cliquez sur **Suivant** deux fois.</span><span class="sxs-lookup"><span data-stu-id="497b4-231">Click **Next** twice.</span></span>
4. <span data-ttu-id="497b4-232">Spécifiez un chemin d'accès pour lequel vous disposez de l'autorisation d'écriture, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="497b4-232">Specify a path where you have the write permission, and then click **Next**.</span></span>

  > [!NOTE]
  > <span data-ttu-id="497b4-233">Le dossier d'installation par défaut se trouve dans le dossier C:\Program Files\squirrel-sql-3.6.</span><span class="sxs-lookup"><span data-stu-id="497b4-233">The default installation folder is in the C:\Program Files\squirrel-sql-3.6 folder.</span></span>  <span data-ttu-id="497b4-234">Pour pouvoir écrire dans ce chemin d'accès, le programme d'installation doit disposer des privilèges d'administrateur.</span><span class="sxs-lookup"><span data-stu-id="497b4-234">In order to write to this path, the installer must be granted the administrator privilege.</span></span> <span data-ttu-id="497b4-235">Vous pouvez ouvrir une invite de commandes en tant qu’administrateur, accéder au dossier bin de Java et exécuter :</span><span class="sxs-lookup"><span data-stu-id="497b4-235">You can open a command prompt as administrator, navigate to Java's bin folder, and then run:</span></span>
  >
  >     <span data-ttu-id="497b4-236">Java.exe-jar [chemin d’accès du fichier jar SQuirreL]</span><span class="sxs-lookup"><span data-stu-id="497b4-236">java.exe -jar [the path of the SQuirreL jar file]</span></span>
5. <span data-ttu-id="497b4-237">Cliquez sur **OK** pour confirmer la création du répertoire cible.</span><span class="sxs-lookup"><span data-stu-id="497b4-237">Click **OK** to confirm creating the target directory.</span></span>
6. <span data-ttu-id="497b4-238">La configuration par défaut installe les packages de base et standard.</span><span class="sxs-lookup"><span data-stu-id="497b4-238">The default setting is to install the Base and Standard packages.</span></span>  <span data-ttu-id="497b4-239">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="497b4-239">Click **Next**.</span></span>
7. <span data-ttu-id="497b4-240">Cliquez sur **Suivant** deux fois, puis sur **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="497b4-240">Click **Next** twice, and then click **Done**.</span></span>

<span data-ttu-id="497b4-241">**Pour installer le pilote Phoenix**</span><span class="sxs-lookup"><span data-stu-id="497b4-241">**To install the Phoenix driver**</span></span>

<span data-ttu-id="497b4-242">Le fichier jar du pilote phoenix se trouve dans le cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="497b4-242">The phoenix driver jar file is located on the HBase cluster.</span></span> <span data-ttu-id="497b4-243">Le chemin d'accès ressemble au suivant selon les versions :</span><span class="sxs-lookup"><span data-stu-id="497b4-243">The path is similar to the following based on the versions:</span></span>

    C:\apps\dist\phoenix-4.0.0.2.1.11.0-2316\phoenix-4.0.0.2.1.11.0-2316-client.jar
<span data-ttu-id="497b4-244">Vous devez le copier sur votre poste de travail sous [Dossier d’installation SQuirreL]/lib.</span><span class="sxs-lookup"><span data-stu-id="497b4-244">You need to copy it to your workstation under the [SQuirreL installation folder]/lib path.</span></span>  <span data-ttu-id="497b4-245">Le moyen le plus simple est d'ouvrir une session RDP sur le cluster, puis de copier et coller le fichier (CTRL+C et CTRL+V) pour le copier sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="497b4-245">The easiest way is to RDP into the cluster, and then use file copy/paste (CTRL+C and CTRL+V) to copy it to your workstation.</span></span>

<span data-ttu-id="497b4-246">**Pour ajouter un pilote Phoenix à SQuirreL**</span><span class="sxs-lookup"><span data-stu-id="497b4-246">**To add a Phoenix driver to SQuirreL**</span></span>

1. <span data-ttu-id="497b4-247">Ouvrez le client SQL SQuirreL dans votre poste de travail.</span><span class="sxs-lookup"><span data-stu-id="497b4-247">Open SQuirreL SQL Client from your workstation.</span></span>
2. <span data-ttu-id="497b4-248">Cliquez sur l'onglet **Driver** à gauche.</span><span class="sxs-lookup"><span data-stu-id="497b4-248">Click the **Driver** tab on the left.</span></span>
3. <span data-ttu-id="497b4-249">Dans le menu **Drivers** (Pilotes), cliquez sur **New Driver** (Nouveau pilote).</span><span class="sxs-lookup"><span data-stu-id="497b4-249">From the **Drivers** menu, click **New Driver**.</span></span>
4. <span data-ttu-id="497b4-250">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="497b4-250">Enter the following information:</span></span>

   * <span data-ttu-id="497b4-251">**Name**: Phoenix</span><span class="sxs-lookup"><span data-stu-id="497b4-251">**Name**: Phoenix</span></span>
   * <span data-ttu-id="497b4-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="497b4-252">**Example URL**: jdbc:phoenix:zookeeper2.contoso-hbase-eu.f5.internal.cloudapp.net</span></span>
   * <span data-ttu-id="497b4-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span><span class="sxs-lookup"><span data-stu-id="497b4-253">**Class Name**: org.apache.phoenix.jdbc.PhoenixDriver</span></span>

     > [!WARNING]
     > <span data-ttu-id="497b4-254">N'utilisez que des minuscules dans l'exemple d'URL.</span><span class="sxs-lookup"><span data-stu-id="497b4-254">User all lower case in the Example URL.</span></span> <span data-ttu-id="497b4-255">Vous pouvez utiliser le quorum complet zookeeper au cas où l’un d’eux est inactif.</span><span class="sxs-lookup"><span data-stu-id="497b4-255">You can use they full zookeeper quorum in case one of them is down.</span></span>  <span data-ttu-id="497b4-256">Les noms d’hôte sont zookeeper0, zookeeper1 et zookeeper2.</span><span class="sxs-lookup"><span data-stu-id="497b4-256">The hostnames are zookeeper0, zookeeper1, and zookeeper2.</span></span>
     >
     >

     ![Pilote HDInsight HBase Phoenix SQuirreL][img-squirrel-driver]
5. <span data-ttu-id="497b4-258">Cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="497b4-258">Click **OK**.</span></span>

<span data-ttu-id="497b4-259">**Pour créer un alias pour le cluster HBase**</span><span class="sxs-lookup"><span data-stu-id="497b4-259">**To create an alias to the HBase cluster**</span></span>

1. <span data-ttu-id="497b4-260">Dans SQuirreL, cliquez sur l’onglet **Aliases** à gauche.</span><span class="sxs-lookup"><span data-stu-id="497b4-260">From SQuirreL, Click the **Aliases** tab on the left.</span></span>
2. <span data-ttu-id="497b4-261">Dans le menu **Aliases** (Alias), cliquez sur **New Alias** (Nouvel alias).</span><span class="sxs-lookup"><span data-stu-id="497b4-261">From the **Aliases** menu, click **New Alias**.</span></span>
3. <span data-ttu-id="497b4-262">Entrez les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="497b4-262">Enter the following information:</span></span>

   * <span data-ttu-id="497b4-263">**Name**: nom du cluster HBase ou un nom de votre choix.</span><span class="sxs-lookup"><span data-stu-id="497b4-263">**Name**: The name of the HBase cluster or any name you prefer.</span></span>
   * <span data-ttu-id="497b4-264">**Driver**: Phoenix.</span><span class="sxs-lookup"><span data-stu-id="497b4-264">**Driver**: Phoenix.</span></span>  <span data-ttu-id="497b4-265">Le nom du pilote doit correspondre à celui que vous avez créé dans la dernière procédure.</span><span class="sxs-lookup"><span data-stu-id="497b4-265">This must match the driver name you created in the last procedure.</span></span>
   * <span data-ttu-id="497b4-266">**URL**: l'URL est copiée à partir de la configuration de votre pilote.</span><span class="sxs-lookup"><span data-stu-id="497b4-266">**URL**: The URL is copied from your driver configuration.</span></span> <span data-ttu-id="497b4-267">N'utilisez que des minuscules.</span><span class="sxs-lookup"><span data-stu-id="497b4-267">Make sure to user all lower case.</span></span>
   * <span data-ttu-id="497b4-268">**Nom d’utilisateur**: il s’agit de texte.</span><span class="sxs-lookup"><span data-stu-id="497b4-268">**User name**: It can be any text.</span></span>  <span data-ttu-id="497b4-269">Étant donné que vous utilisez une connectivité VPN ici, le nom d’utilisateur n’est pas du tout utilisé.</span><span class="sxs-lookup"><span data-stu-id="497b4-269">Because you use VPN connectivity here, the user name is not used at all.</span></span>
   * <span data-ttu-id="497b4-270">**Password**: il s’agit de texte.</span><span class="sxs-lookup"><span data-stu-id="497b4-270">**Password**: It can be any text.</span></span>

     ![Pilote HDInsight HBase Phoenix SQuirreL][img-squirrel-alias]
4. <span data-ttu-id="497b4-272">Cliquez sur **Test**.</span><span class="sxs-lookup"><span data-stu-id="497b4-272">Click **Test**.</span></span>
5. <span data-ttu-id="497b4-273">Cliquez sur **Connecter**.</span><span class="sxs-lookup"><span data-stu-id="497b4-273">Click **Connect**.</span></span> <span data-ttu-id="497b4-274">Quand la connexion est établie, SQuirreL ressemble à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="497b4-274">When it makes the connection, SQuirreL looks like:</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel]

<span data-ttu-id="497b4-276">**Pour exécuter un test**</span><span class="sxs-lookup"><span data-stu-id="497b4-276">**To run a test**</span></span>

1. <span data-ttu-id="497b4-277">Cliquez sur l’onglet **SQL** juste à côté de l’onglet **Objects** (Objets).</span><span class="sxs-lookup"><span data-stu-id="497b4-277">Click the **SQL** tab right next to the **Objects** tab.</span></span>
2. <span data-ttu-id="497b4-278">Copiez et collez le code suivant :</span><span class="sxs-lookup"><span data-stu-id="497b4-278">Copy and paste the following code:</span></span>

        CREATE TABLE IF NOT EXISTS us_population (state CHAR(2) NOT NULL, city VARCHAR NOT NULL, population BIGINT  CONSTRAINT my_pk PRIMARY KEY (state, city))
3. <span data-ttu-id="497b4-279">Cliquez sur le bouton d'exécution.</span><span class="sxs-lookup"><span data-stu-id="497b4-279">Click the run button.</span></span>

    ![HBase Phoenix SQuirreL][img-squirrel-sql]
4. <span data-ttu-id="497b4-281">Revenez à l'onglet **Objects** .</span><span class="sxs-lookup"><span data-stu-id="497b4-281">Switch back to the **Objects** tab.</span></span>
5. <span data-ttu-id="497b4-282">Développez le nom d'alias, puis **TABLE**.</span><span class="sxs-lookup"><span data-stu-id="497b4-282">Expand the alias name, and then expand **TABLE**.</span></span>  <span data-ttu-id="497b4-283">La nouvelle table doit être affichée.</span><span class="sxs-lookup"><span data-stu-id="497b4-283">You shall see the new table listed under.</span></span>

## <a name="next-steps"></a><span data-ttu-id="497b4-284">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="497b4-284">Next steps</span></span>
<span data-ttu-id="497b4-285">Dans cet article, vous avez appris comment utiliser Apache Phoenix dans HDInsight.</span><span class="sxs-lookup"><span data-stu-id="497b4-285">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="497b4-286">Pour plus d'informations, consultez les rubriques suivantes :</span><span class="sxs-lookup"><span data-stu-id="497b4-286">To learn more, see</span></span>

* <span data-ttu-id="497b4-287">[Vue d’ensemble de HDInsight HBase][hdinsight-hbase-overview] : HBase est une base de données NoSQL open source Apache basée sur Hadoop qui fournit un accès aléatoire et une forte cohérence pour de grandes quantités de données non structurées et semi-structurées.</span><span class="sxs-lookup"><span data-stu-id="497b4-287">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="497b4-288">[Approvisionnement de clusters HBase sur Azure Virtual Network][hdinsight-hbase-provision-vnet] : avec l’intégration du réseau virtuel, les clusters HBase peuvent être déployés sur le même réseau virtuel que vos applications pour permettre à celles-ci de communiquer directement avec HBase.</span><span class="sxs-lookup"><span data-stu-id="497b4-288">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="497b4-289">[Configurer la réplication HBase dans HDInsight](hdinsight-hbase-replication.md): découvrez comment configurer la réplication HBase entre deux centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="497b4-289">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="497b4-290">[Analyse de sentiments Twitter avec HBase dans HDInsight][hbase-twitter-sentiment] : découvrez comment effectuer une [analyse de sentiments](http://en.wikipedia.org/wiki/Sentiment_analysis) en temps réel des données volumineuses à l’aide de HBase dans un cluster Hadoop sous HDInsight.</span><span class="sxs-lookup"><span data-stu-id="497b4-290">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
