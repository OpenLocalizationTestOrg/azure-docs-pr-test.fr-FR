---
title: aaaUse SSH tooaccess tunneling Azure HDInsight | Documents Microsoft
description: "Découvrez comment toouse un toosecurely de tunnel SSH parcourir les ressources web hébergées sur vos nœuds HDInsight de basés sur Linux."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 879834a4-52d0-499c-a3ae-8d28863abf65
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: larryfr
ms.openlocfilehash: 8a315c53751bbe6950a182674f4108c67c2f2f8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="use-ssh-tunneling-tooaccess-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="45af7-103">Utiliser le Tunneling SSH tooaccess Ambari web UI, JobHistory, NameNode, Oozie et autres interfaces utilisateur web</span><span class="sxs-lookup"><span data-stu-id="45af7-103">Use SSH Tunneling tooaccess Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="45af7-104">Les clusters HDInsight basés sur Linux fournissent l’interface utilisateur de web de tooAmbari accès via Internet de hello, mais certaines fonctionnalités de l’interface utilisateur de hello ne sont pas.</span><span class="sxs-lookup"><span data-stu-id="45af7-104">Linux-based HDInsight clusters provide access tooAmbari web UI over hello Internet, but some features of hello UI are not.</span></span> <span data-ttu-id="45af7-105">Par exemple, hello interface utilisateur web pour d’autres services qui sont exposés via Ambari.</span><span class="sxs-lookup"><span data-stu-id="45af7-105">For example, hello web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="45af7-106">Pour toutes les fonctionnalités de l’interface utilisateur web de Ambari hello, vous devez utiliser une tête de cluster de toohello tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-106">For full functionality of hello Ambari web UI, you must use an SSH tunnel toohello cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="45af7-107">Raisons pour lesquelles utiliser un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="45af7-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="45af7-108">Plusieurs menus hello dans Ambari fonctionnent uniquement via un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-108">Several of hello menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="45af7-109">Ces menus s’appuient sur des sites web et des services qui s’exécutent sur d’autres types de nœuds, tels que les nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="45af7-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="45af7-110">Souvent, ces sites web ne sont pas sécurisés, donc il n’est pas sécurisé toodirectly exposent les sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="45af7-110">Often, these web sites are not secured, so it is not safe toodirectly expose them on hello internet.</span></span>

<span data-ttu-id="45af7-111">Hello suivant des interfaces utilisateur Web nécessite un tunnel SSH :</span><span class="sxs-lookup"><span data-stu-id="45af7-111">hello following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="45af7-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="45af7-112">JobHistory</span></span>
* <span data-ttu-id="45af7-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="45af7-113">NameNode</span></span>
* <span data-ttu-id="45af7-114">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="45af7-114">Thread Stacks</span></span>
* <span data-ttu-id="45af7-115">Interface utilisateur Web Oozie</span><span class="sxs-lookup"><span data-stu-id="45af7-115">Oozie web UI</span></span>
* <span data-ttu-id="45af7-116">Interface HBase Master et interface de journaux</span><span class="sxs-lookup"><span data-stu-id="45af7-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="45af7-117">Si vous utilisez des Actions de Script toocustomize votre cluster, tous les services ou les utilitaires que vous installez qui exposent une interface utilisateur web nécessitent un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-117">If you use Script Actions toocustomize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="45af7-118">Par exemple, si vous installez la teinte à l’aide d’une Action de Script, vous devez utiliser un SSH tunnel tooaccess hello teinte interface utilisateur web.</span><span class="sxs-lookup"><span data-stu-id="45af7-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel tooaccess hello Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45af7-119">Si vous avez tooHDInsight un accès direct via un réseau virtuel, il est inutile des tunnels toouse SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-119">If you have direct access tooHDInsight through a virtual network, you do not need toouse SSH tunnels.</span></span> <span data-ttu-id="45af7-120">Pour obtenir un exemple d’accéder directement à HDInsight via un réseau virtuel, consultez hello [réseau de se connecter de HDInsight tooyour local](connect-on-premises-network.md) document.</span><span class="sxs-lookup"><span data-stu-id="45af7-120">For an example of directly accessing HDInsight through a virtual network, see hello [Connect HDInsight tooyour on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="45af7-121">Définition d’un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="45af7-121">What is an SSH tunnel</span></span>

<span data-ttu-id="45af7-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) achemine le trafic envoyé tooa port sur votre station de travail locale.</span><span class="sxs-lookup"><span data-stu-id="45af7-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent tooa port on your local workstation.</span></span> <span data-ttu-id="45af7-123">le trafic de Hello est acheminé via un SSH connexion tooyour HDInsight nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="45af7-123">hello traffic is routed through an SSH connection tooyour HDInsight cluster head node.</span></span> <span data-ttu-id="45af7-124">demande de Hello est résolu comme si elle a été créée sur le nœud principal de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-124">hello request is resolved as if it originated on hello head node.</span></span> <span data-ttu-id="45af7-125">réponse de Hello est alors acheminé par le biais de station de travail tooyour hello tunnel.</span><span class="sxs-lookup"><span data-stu-id="45af7-125">hello response is then routed back through hello tunnel tooyour workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="45af7-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="45af7-126">Prerequisites</span></span>

* <span data-ttu-id="45af7-127">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-127">An SSH client.</span></span> <span data-ttu-id="45af7-128">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="45af7-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="45af7-129">Un navigateur web qui peut être configuré toouse un proxy SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="45af7-129">A web browser that can be configured toouse a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="45af7-130">prise en charge du proxy Hello SOCKS intégrée de Windows ne prend pas en charge SOCKS5 et ne fonctionne pas avec les étapes hello dans ce document.</span><span class="sxs-lookup"><span data-stu-id="45af7-130">hello SOCKS proxy support built into Windows does not support SOCKS5, and does not work with hello steps in this document.</span></span> <span data-ttu-id="45af7-131">Hello navigateurs suivants s’appuient sur les paramètres de proxy de Windows et ne le faites pas actuellement utiliser des étapes hello dans ce document :</span><span class="sxs-lookup"><span data-stu-id="45af7-131">hello following browsers rely on Windows proxy settings, and do not currently work with hello steps in this document:</span></span>
    >
    > * <span data-ttu-id="45af7-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="45af7-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="45af7-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="45af7-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="45af7-134">Google Chrome s’appuie également sur les paramètres du proxy Windows hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-134">Google Chrome also relies on hello Windows proxy settings.</span></span> <span data-ttu-id="45af7-135">Toutefois, vous pouvez installer des extensions qui prennent en charge SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="45af7-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="45af7-136">Nous vous recommandons [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="45af7-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="45af7-137"><a name="usessh"></a>Créer un tunnel à l’aide de la commande SSH de hello</span><span class="sxs-lookup"><span data-stu-id="45af7-137"><a name="usessh"></a>Create a tunnel using hello SSH command</span></span>

<span data-ttu-id="45af7-138">Suivant de hello utilisez commande toocreate un tunnel SSH à l’aide de hello `ssh` commande.</span><span class="sxs-lookup"><span data-stu-id="45af7-138">Use hello following command toocreate an SSH tunnel using hello `ssh` command.</span></span> <span data-ttu-id="45af7-139">Remplacez **nom d’utilisateur** à un utilisateur SSH pour votre cluster HDInsight, puis remplacez **CLUSTERNAME** avec nom hello de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="45af7-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with hello name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="45af7-140">Cette commande crée une connexion qui achemine le cluster toohello 9876 trafic toolocal port via SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-140">This command creates a connection that routes traffic toolocal port 9876 toohello cluster over SSH.</span></span> <span data-ttu-id="45af7-141">options de Hello sont :</span><span class="sxs-lookup"><span data-stu-id="45af7-141">hello options are:</span></span>

* <span data-ttu-id="45af7-142">**D 9876** -hello port local qui achemine le trafic via un tunnel de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-142">**D 9876** - hello local port that routes traffic through hello tunnel.</span></span>
* <span data-ttu-id="45af7-143">**C** : compresse toutes les données car le trafic web est principalement du texte</span><span class="sxs-lookup"><span data-stu-id="45af7-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="45af7-144">**2** -force SSH tootry protocol version 2 uniquement.</span><span class="sxs-lookup"><span data-stu-id="45af7-144">**2** - Force SSH tootry protocol version 2 only.</span></span>
* <span data-ttu-id="45af7-145">**q** : mode silencieux</span><span class="sxs-lookup"><span data-stu-id="45af7-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="45af7-146">**T** : désactive l’allocation pseudo-tty puisque nous transférons simplement un port</span><span class="sxs-lookup"><span data-stu-id="45af7-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="45af7-147">**n** : empêche la lecture STDIN puisque nous transférons simplement un port</span><span class="sxs-lookup"><span data-stu-id="45af7-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="45af7-148">**N** : n’exécute pas une commande à distance puisque nous transférons simplement un port</span><span class="sxs-lookup"><span data-stu-id="45af7-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="45af7-149">**f** -s’exécutent en arrière-plan de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-149">**f** - Run in hello background.</span></span>

<span data-ttu-id="45af7-150">Une fois la commande hello se termine, le trafic envoyé tooport 9876 sur l’ordinateur local de hello est routé toohello nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="45af7-150">Once hello command finishes, traffic sent tooport 9876 on hello local computer is routed toohello cluster head node.</span></span>

## <span data-ttu-id="45af7-151"><a name="useputty"></a>Création d’un tunnel à l'aide de PuTTY</span><span class="sxs-lookup"><span data-stu-id="45af7-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="45af7-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) est un client SSH graphique pour Windows.</span><span class="sxs-lookup"><span data-stu-id="45af7-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="45af7-153">Utilisez hello suivant les étapes toocreate un tunnel SSH à l’aide de PuTTY :</span><span class="sxs-lookup"><span data-stu-id="45af7-153">Use hello following steps toocreate an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="45af7-154">Ouvrez PuTTY et saisissez vos informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="45af7-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="45af7-155">Si vous n’êtes pas familiarisé avec PuTTY, consultez hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="45af7-155">If you are not familiar with PuTTY, see hello [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="45af7-156">Bonjour **catégorie** toohello de la section gauche de la boîte de dialogue hello, développez **connexion**, développez **SSH**, puis sélectionnez **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="45af7-156">In hello **Category** section toohello left of hello dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="45af7-157">Fournir hello suivant les informations de hello **réacheminement de port Options contrôlant SSH** formulaire :</span><span class="sxs-lookup"><span data-stu-id="45af7-157">Provide hello following information on hello **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="45af7-158">**Port source** -hello port client hello que vous souhaitez tooforward.</span><span class="sxs-lookup"><span data-stu-id="45af7-158">**Source port** - hello port on hello client that you wish tooforward.</span></span> <span data-ttu-id="45af7-159">Par exemple : **9876**.</span><span class="sxs-lookup"><span data-stu-id="45af7-159">For example, **9876**.</span></span>

   * <span data-ttu-id="45af7-160">**Destination** -hello adresse SSH pour le cluster HDInsight de basés sur Linux de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-160">**Destination** - hello SSH address for hello Linux-based HDInsight cluster.</span></span> <span data-ttu-id="45af7-161">Par exemple : **moncluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="45af7-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="45af7-162">**Dynamique** : active le routage dynamique du proxy SOCKS.</span><span class="sxs-lookup"><span data-stu-id="45af7-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![image des options de tunneling](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="45af7-164">Cliquez sur **ajouter** tooadd hello paramètres, puis cliquez sur **ouvrir** tooopen une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-164">Click **Add** tooadd hello settings, and then click **Open** tooopen an SSH connection.</span></span>

5. <span data-ttu-id="45af7-165">Lorsque vous y êtes invité, connectez-vous toohello server.</span><span class="sxs-lookup"><span data-stu-id="45af7-165">When prompted, log in toohello server.</span></span>

## <a name="use-hello-tunnel-from-your-browser"></a><span data-ttu-id="45af7-166">Utiliser le tunnel hello depuis votre navigateur</span><span class="sxs-lookup"><span data-stu-id="45af7-166">Use hello tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="45af7-167">Hello étapes cette hello d’utilisation de section navigateur Mozilla FireFox, car elle fournit hello mêmes paramètres de proxy sur toutes les plateformes.</span><span class="sxs-lookup"><span data-stu-id="45af7-167">hello steps in this section use hello Mozilla FireFox browser, as it provides hello same proxy settings across all platforms.</span></span> <span data-ttu-id="45af7-168">Autres navigateurs modernes, tels que Google Chrome, peuvent nécessiter une extension du type toowork FoxyProxy avec le tunnel hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy toowork with hello tunnel.</span></span>

1. <span data-ttu-id="45af7-169">Configurer hello navigateur toouse **localhost** et la création de port hello vous avez utilisé lorsque tunnel hello comme un **SOCKS v5** proxy.</span><span class="sxs-lookup"><span data-stu-id="45af7-169">Configure hello browser toouse **localhost** and hello port you used when creating hello tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="45af7-170">Voici ce que les paramètres de Firefox hello similaire.</span><span class="sxs-lookup"><span data-stu-id="45af7-170">Here's what hello Firefox settings look like.</span></span> <span data-ttu-id="45af7-171">Si vous avez utilisé un port autre que 9876, modifiez hello port toohello est que celle que vous avez utilisé :</span><span class="sxs-lookup"><span data-stu-id="45af7-171">If you used a different port than 9876, change hello port toohello one you used:</span></span>
   
    ![image des paramètres de Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="45af7-173">En sélectionnant **DNS distant** résout les demandes de système DNS (Domain Name) à l’aide du cluster HDInsight de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using hello HDInsight cluster.</span></span> <span data-ttu-id="45af7-174">Ce paramètre est résolu DNS à l’aide du nœud principal de hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-174">This setting resolves DNS using hello head node of hello cluster.</span></span>

2. <span data-ttu-id="45af7-175">Vérifiez ce tunnel hello fonctionne en visitant un site tel que [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="45af7-175">Verify that hello tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="45af7-176">Hello IP retourné doit être une utilisée par le centre de données de Microsoft Azure hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-176">hello IP returned should be one used by hello Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="45af7-177">Vérification avec l'interface utilisateur Web Ambari</span><span class="sxs-lookup"><span data-stu-id="45af7-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="45af7-178">Une fois que le cluster de hello a été établie, utilisez hello suivant tooverify étapes que vous pouvez accéder à des interfaces utilisateur web du service à partir de hello Ambari Web :</span><span class="sxs-lookup"><span data-stu-id="45af7-178">Once hello cluster has been established, use hello following steps tooverify that you can access service web UIs from hello Ambari Web:</span></span>

1. <span data-ttu-id="45af7-179">Dans votre navigateur, accédez à toohttp://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="45af7-179">In your browser, go toohttp://headnodehost:8080.</span></span> <span data-ttu-id="45af7-180">Hello `headnodehost` adresse est envoyé sur le cluster de toohello tunnel hello et résoudre le nœud principal toohello qui Ambari est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="45af7-180">hello `headnodehost` address is sent over hello tunnel toohello cluster and resolve toohello headnode that Ambari is running on.</span></span> <span data-ttu-id="45af7-181">Lorsque vous y êtes invité, entrez le nom d’utilisateur admin hello (admin) et le mot de passe pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="45af7-181">When prompted, enter hello admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="45af7-182">Vous pouvez être invité à une seconde fois par l’interface utilisateur web de Ambari hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-182">You may be prompted a second time by hello Ambari web UI.</span></span> <span data-ttu-id="45af7-183">Dans ce cas, entrez à nouveau les informations de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-183">If so, reenter hello information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="45af7-184">Lorsque vous utilisez le cluster toohello tooconnect hello http://headnodehost:8080 adresse, vous vous connectez via un tunnel de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-184">When using hello http://headnodehost:8080 address tooconnect toohello cluster, you are connecting through hello tunnel.</span></span> <span data-ttu-id="45af7-185">Communication est sécurisée à l’aide de tunnel SSH de hello au lieu de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="45af7-185">Communication is secured using hello SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="45af7-186">tooconnect plus hello internet à l’aide de HTTPS, utilisez https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom hello du cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-186">tooconnect over hello internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is hello name of hello cluster.</span></span>

2. <span data-ttu-id="45af7-187">À partir de l’interface utilisateur de Ambari Web de hello, sélectionnez HDFS dans liste hello gauche hello de page de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-187">From hello Ambari Web UI, select HDFS from hello list on hello left of hello page.</span></span>

    ![Image avec HDFS sélectionné](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="45af7-189">Lorsque hello informations du service HDFS s’affiche, sélectionnez **liens rapides**.</span><span class="sxs-lookup"><span data-stu-id="45af7-189">When hello HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="45af7-190">Une liste de nœuds principaux d’un cluster hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="45af7-190">A list of hello cluster head nodes appears.</span></span> <span data-ttu-id="45af7-191">Sélectionnez un des nœuds de tête hello, puis **NameNode UI**.</span><span class="sxs-lookup"><span data-stu-id="45af7-191">Select one of hello head nodes, and then select **NameNode UI**.</span></span>

    ![Image avec un menu de liens rapides hello développé](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="45af7-193">Lorsque vous sélectionnez __Liens rapides__, un indicateur d’attente peut apparaître.</span><span class="sxs-lookup"><span data-stu-id="45af7-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="45af7-194">Cela peut se produire si votre connexion internet est lente.</span><span class="sxs-lookup"><span data-stu-id="45af7-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="45af7-195">Patienter une minute ou deux pour hello toobe de données provenant du serveur de hello, puis réessayez la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-195">Wait a minute or two for hello data toobe received from hello server, then try hello list again.</span></span>
   >
   > <span data-ttu-id="45af7-196">Certaines entrées de hello **liens rapides** menu peut être tronqué à droite hello d’écran hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-196">Some entries in hello **Quick Links** menu may be cut off by hello right side of hello screen.</span></span> <span data-ttu-id="45af7-197">Dans ce cas, développez le menu hello à l’aide de la souris et utilisez hello flèche droite tooscroll clé hello écran toohello toosee droite hello reste du menu de hello.</span><span class="sxs-lookup"><span data-stu-id="45af7-197">If so, expand hello menu using your mouse and use hello right arrow key tooscroll hello screen toohello right toosee hello rest of hello menu.</span></span>

4. <span data-ttu-id="45af7-198">Un toohello similaire de page suivant l’image s’affiche :</span><span class="sxs-lookup"><span data-stu-id="45af7-198">A page similar toohello following image is displayed:</span></span>

    ![Image de hello NameNode UI](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="45af7-200">Notez l’URL de hello pour cette page ; Il doit être similaire trop**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="45af7-200">Notice hello URL for this page; it should be similar too**http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="45af7-201">Cet URI utilise le nom de domaine complet interne hello (FQDN) du nœud de hello et est accessible uniquement lors de l’utilisation d’un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="45af7-201">This URI is using hello internal fully qualified domain name (FQDN) of hello node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="45af7-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="45af7-202">Next steps</span></span>

<span data-ttu-id="45af7-203">Maintenant que vous avez appris comment toocreate et utilisez un tunnel SSH, consultez hello suivant du document pour les autres façons de toouse Ambari :</span><span class="sxs-lookup"><span data-stu-id="45af7-203">Now that you have learned how toocreate and use an SSH tunnel, see hello following document for other ways toouse Ambari:</span></span>

* [<span data-ttu-id="45af7-204">Gestion des clusters HDInsight à l'aide d’Ambari</span><span class="sxs-lookup"><span data-stu-id="45af7-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="45af7-205">Pour plus d’informations sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="45af7-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

