---
title: "Utiliser un tunnel SSH pour accéder à Azure HDInsight | Microsoft Docs"
description: "Apprenez à utiliser un tunnel SSH pour accéder de façon sécurisée à des ressources Web hébergées sur vos nœuds HDInsight sous Linux."
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
ms.openlocfilehash: 4b606ea3797d685b9deacf72f1bd31e0ef007f98
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="use-ssh-tunneling-to-access-ambari-web-ui-jobhistory-namenode-oozie-and-other-web-uis"></a><span data-ttu-id="09f0d-103">Utilisation d’un tunnel SSH pour accéder à l’interface Web Ambari, JobHistory, NameNode, Oozie et d’autres interfaces Web</span><span class="sxs-lookup"><span data-stu-id="09f0d-103">Use SSH Tunneling to access Ambari web UI, JobHistory, NameNode, Oozie, and other web UIs</span></span>

<span data-ttu-id="09f0d-104">Les clusters HDInsight sous Linux donnent accès à l'interface utilisateur Web Ambari à Internet, mais pas pour certaines fonctionnalités de l'interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="09f0d-104">Linux-based HDInsight clusters provide access to Ambari web UI over the Internet, but some features of the UI are not.</span></span> <span data-ttu-id="09f0d-105">Par exemple, l'interface utilisateur Web pour d'autres services qui sont exposés via Ambari.</span><span class="sxs-lookup"><span data-stu-id="09f0d-105">For example, the web UI for other services that are surfaced through Ambari.</span></span> <span data-ttu-id="09f0d-106">Pour bénéficier de toutes les fonctionnalités de l'interface utilisateur Web Ambari, vous devez utiliser un tunnel SSH vers le principal cluster.</span><span class="sxs-lookup"><span data-stu-id="09f0d-106">For full functionality of the Ambari web UI, you must use an SSH tunnel to the cluster head.</span></span>

## <a name="why-use-an-ssh-tunnel"></a><span data-ttu-id="09f0d-107">Raisons pour lesquelles utiliser un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="09f0d-107">Why use an SSH tunnel</span></span>

<span data-ttu-id="09f0d-108">Plusieurs des menus d’Ambari fonctionnent uniquement via un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="09f0d-108">Several of the menus in Ambari only work through an SSH tunnel.</span></span> <span data-ttu-id="09f0d-109">Ces menus s’appuient sur des sites web et des services qui s’exécutent sur d’autres types de nœuds, tels que les nœuds Worker.</span><span class="sxs-lookup"><span data-stu-id="09f0d-109">These menus rely on web sites and services running on other node types, such as worker nodes.</span></span> <span data-ttu-id="09f0d-110">Souvent, ces sites Web ne sont pas sécurisés. Il est donc dangereux de les exposer directement sur Internet.</span><span class="sxs-lookup"><span data-stu-id="09f0d-110">Often, these web sites are not secured, so it is not safe to directly expose them on the internet.</span></span>

<span data-ttu-id="09f0d-111">Les interfaces utilisateur web suivantes nécessitent un tunnel SSH :</span><span class="sxs-lookup"><span data-stu-id="09f0d-111">The following Web UIs require an SSH tunnel:</span></span>

* <span data-ttu-id="09f0d-112">JobHistory</span><span class="sxs-lookup"><span data-stu-id="09f0d-112">JobHistory</span></span>
* <span data-ttu-id="09f0d-113">NameNode</span><span class="sxs-lookup"><span data-stu-id="09f0d-113">NameNode</span></span>
* <span data-ttu-id="09f0d-114">Thread Stacks</span><span class="sxs-lookup"><span data-stu-id="09f0d-114">Thread Stacks</span></span>
* <span data-ttu-id="09f0d-115">Interface utilisateur Web Oozie</span><span class="sxs-lookup"><span data-stu-id="09f0d-115">Oozie web UI</span></span>
* <span data-ttu-id="09f0d-116">Interface HBase Master et interface de journaux</span><span class="sxs-lookup"><span data-stu-id="09f0d-116">HBase Master and Logs UI</span></span>

<span data-ttu-id="09f0d-117">Si vous utilisez des actions de script pour personnaliser votre cluster, tous les services ou utilitaires que vous installez et qui exposent une interface utilisateur Web nécessitent un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="09f0d-117">If you use Script Actions to customize your cluster, any services or utilities that you install that expose a web UI require an SSH tunnel.</span></span> <span data-ttu-id="09f0d-118">Par exemple, si vous installez Hue à l'aide d'une action de script, vous devez utiliser un tunnel SSH pour accéder à l'interface utilisateur Web Hue.</span><span class="sxs-lookup"><span data-stu-id="09f0d-118">For example, if you install Hue using a Script Action, you must use an SSH tunnel to access the Hue web UI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09f0d-119">Si vous bénéficiez d’un accès direct à HDInsight via un réseau virtuel, il est inutile d’utiliser des tunnels SSH.</span><span class="sxs-lookup"><span data-stu-id="09f0d-119">If you have direct access to HDInsight through a virtual network, you do not need to use SSH tunnels.</span></span> <span data-ttu-id="09f0d-120">Pour avoir un exemple d’accès direct à HDInsight via un réseau virtuel, consultez le document [Connecter HDInsight à votre réseau local](connect-on-premises-network.md).</span><span class="sxs-lookup"><span data-stu-id="09f0d-120">For an example of directly accessing HDInsight through a virtual network, see the [Connect HDInsight to your on-premises network](connect-on-premises-network.md) document.</span></span>

## <a name="what-is-an-ssh-tunnel"></a><span data-ttu-id="09f0d-121">Définition d’un tunnel SSH</span><span class="sxs-lookup"><span data-stu-id="09f0d-121">What is an SSH tunnel</span></span>

<span data-ttu-id="09f0d-122">Le [tunnel Secure Shell (SSH)](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) achemine le trafic envoyé à un port sur votre station de travail locale.</span><span class="sxs-lookup"><span data-stu-id="09f0d-122">[Secure Shell (SSH) tunneling](https://en.wikipedia.org/wiki/Tunneling_protocol#Secure_Shell_tunneling) routes traffic sent to a port on your local workstation.</span></span> <span data-ttu-id="09f0d-123">Le trafic est acheminé via une connexion SSH vers le nœud principal de votre cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09f0d-123">The traffic is routed through an SSH connection to your HDInsight cluster head node.</span></span> <span data-ttu-id="09f0d-124">La requête est résolue comme si elle avait été créée sur le nœud principal.</span><span class="sxs-lookup"><span data-stu-id="09f0d-124">The request is resolved as if it originated on the head node.</span></span> <span data-ttu-id="09f0d-125">La réponse est alors acheminée via le tunnel sur votre station de travail.</span><span class="sxs-lookup"><span data-stu-id="09f0d-125">The response is then routed back through the tunnel to your workstation.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="09f0d-126">Composants requis</span><span class="sxs-lookup"><span data-stu-id="09f0d-126">Prerequisites</span></span>

* <span data-ttu-id="09f0d-127">Un client SSH.</span><span class="sxs-lookup"><span data-stu-id="09f0d-127">An SSH client.</span></span> <span data-ttu-id="09f0d-128">Pour en savoir plus, voir [Utilisation de SSH avec Hadoop Linux sur HDInsight depuis Linux, Unix ou OS X](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="09f0d-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="09f0d-129">Un navigateur web qui peut être configuré pour utiliser un proxy SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="09f0d-129">A web browser that can be configured to use a SOCKS5 proxy.</span></span>

    > [!WARNING]
    > <span data-ttu-id="09f0d-130">La prise en charge du proxy SOCKS intégrée à Windows ne prend pas en charge SOCKS5 et ne fonctionne pas dans le cadre des étapes décrites dans ce document.</span><span class="sxs-lookup"><span data-stu-id="09f0d-130">The SOCKS proxy support built into Windows does not support SOCKS5, and does not work with the steps in this document.</span></span> <span data-ttu-id="09f0d-131">Les navigateurs suivants s’appuient sur les paramètres de proxy Windows et ne fonctionnent pas dans le cadre des étapes décrites dans ce document :</span><span class="sxs-lookup"><span data-stu-id="09f0d-131">The following browsers rely on Windows proxy settings, and do not currently work with the steps in this document:</span></span>
    >
    > * <span data-ttu-id="09f0d-132">Microsoft Edge</span><span class="sxs-lookup"><span data-stu-id="09f0d-132">Microsoft Edge</span></span>
    > * <span data-ttu-id="09f0d-133">Microsoft Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="09f0d-133">Microsoft Internet Explorer</span></span>
    >
    > <span data-ttu-id="09f0d-134">Google Chrome repose également sur les paramètres de proxy Windows.</span><span class="sxs-lookup"><span data-stu-id="09f0d-134">Google Chrome also relies on the Windows proxy settings.</span></span> <span data-ttu-id="09f0d-135">Toutefois, vous pouvez installer des extensions qui prennent en charge SOCKS5.</span><span class="sxs-lookup"><span data-stu-id="09f0d-135">However, you can install extensions that support SOCKS5.</span></span> <span data-ttu-id="09f0d-136">Nous vous recommandons [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span><span class="sxs-lookup"><span data-stu-id="09f0d-136">We recommend [FoxyProxy Standard](https://chrome.google.com/webstore/detail/foxyproxy-standard/gcknhkkoolaabfmlnjonogaaifnjlfnp).</span></span>

## <span data-ttu-id="09f0d-137"><a name="usessh"></a>Création d’un tunnel à l'aide de la commande SSH</span><span class="sxs-lookup"><span data-stu-id="09f0d-137"><a name="usessh"></a>Create a tunnel using the SSH command</span></span>

<span data-ttu-id="09f0d-138">Utilisez la commande suivante pour créer un tunnel SSH à l'aide de la commande `ssh` .</span><span class="sxs-lookup"><span data-stu-id="09f0d-138">Use the following command to create an SSH tunnel using the `ssh` command.</span></span> <span data-ttu-id="09f0d-139">Remplacez **USERNAME** par un utilisateur SSH de votre cluster HDInsight et **CLUSTERNAME** par le nom de votre cluster HDInsight :</span><span class="sxs-lookup"><span data-stu-id="09f0d-139">Replace **USERNAME** with an SSH user for your HDInsight cluster, and replace **CLUSTERNAME** with the name of your HDInsight cluster:</span></span>

```bash
ssh -C2qTnNf -D 9876 USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
```

<span data-ttu-id="09f0d-140">Cette commande va permettre de créer une connexion qui achemine le trafic vers le port local 9876 du cluster via SSH.</span><span class="sxs-lookup"><span data-stu-id="09f0d-140">This command creates a connection that routes traffic to local port 9876 to the cluster over SSH.</span></span> <span data-ttu-id="09f0d-141">Les options sont :</span><span class="sxs-lookup"><span data-stu-id="09f0d-141">The options are:</span></span>

* <span data-ttu-id="09f0d-142">**D 9876** : port local qui achemine le trafic via le tunnel.</span><span class="sxs-lookup"><span data-stu-id="09f0d-142">**D 9876** - The local port that routes traffic through the tunnel.</span></span>
* <span data-ttu-id="09f0d-143">**C** : compresse toutes les données car le trafic web est principalement du texte</span><span class="sxs-lookup"><span data-stu-id="09f0d-143">**C** - Compress all data, because web traffic is mostly text.</span></span>
* <span data-ttu-id="09f0d-144">**2** : force le SSH à essayer le protocole version 2 uniquement</span><span class="sxs-lookup"><span data-stu-id="09f0d-144">**2** - Force SSH to try protocol version 2 only.</span></span>
* <span data-ttu-id="09f0d-145">**q** : mode silencieux</span><span class="sxs-lookup"><span data-stu-id="09f0d-145">**q** - Quiet mode.</span></span>
* <span data-ttu-id="09f0d-146">**T** : désactive l’allocation pseudo-tty puisque nous transférons simplement un port</span><span class="sxs-lookup"><span data-stu-id="09f0d-146">**T** - Disable pseudo-tty allocation, since we are just forwarding a port.</span></span>
* <span data-ttu-id="09f0d-147">**n** : empêche la lecture STDIN puisque nous transférons simplement un port</span><span class="sxs-lookup"><span data-stu-id="09f0d-147">**n** - Prevent reading of STDIN, since we are just forwarding a port.</span></span>
* <span data-ttu-id="09f0d-148">**N** : n’exécute pas une commande à distance puisque nous transférons simplement un port</span><span class="sxs-lookup"><span data-stu-id="09f0d-148">**N** - Do not execute a remote command, since we are just forwarding a port.</span></span>
* <span data-ttu-id="09f0d-149">**f** : s’exécute à l’arrière-plan</span><span class="sxs-lookup"><span data-stu-id="09f0d-149">**f** - Run in the background.</span></span>

<span data-ttu-id="09f0d-150">Une fois la commande terminée, le trafic envoyé au port 9876 sur l’ordinateur local est acheminé au nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="09f0d-150">Once the command finishes, traffic sent to port 9876 on the local computer is routed to the cluster head node.</span></span>

## <span data-ttu-id="09f0d-151"><a name="useputty"></a>Création d’un tunnel à l'aide de PuTTY</span><span class="sxs-lookup"><span data-stu-id="09f0d-151"><a name="useputty"></a>Create a tunnel using PuTTY</span></span>

<span data-ttu-id="09f0d-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) est un client SSH graphique pour Windows.</span><span class="sxs-lookup"><span data-stu-id="09f0d-152">[PuTTY](http://www.chiark.greenend.org.uk/~sgtatham/putty) is a graphical SSH client for Windows.</span></span> <span data-ttu-id="09f0d-153">Pour créer un tunnel SSH à l’aide de PuTTY, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="09f0d-153">Use the following steps to create an SSH tunnel using PuTTY:</span></span>

1. <span data-ttu-id="09f0d-154">Ouvrez PuTTY et saisissez vos informations de connexion.</span><span class="sxs-lookup"><span data-stu-id="09f0d-154">Open PuTTY, and enter your connection information.</span></span> <span data-ttu-id="09f0d-155">Si vous n’êtes pas familiarisé avec PuTTY, consultez la [documentation PuTTY (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span><span class="sxs-lookup"><span data-stu-id="09f0d-155">If you are not familiar with PuTTY, see the [PuTTY documentation (http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html)](http://www.chiark.greenend.org.uk/~sgtatham/putty/docs.html).</span></span>

2. <span data-ttu-id="09f0d-156">Dans la rubrique **Catégorie** située à gauche dans la boîte de dialogue, développez **Connexion** et **SSH**, puis sélectionnez **Tunnels**.</span><span class="sxs-lookup"><span data-stu-id="09f0d-156">In the **Category** section to the left of the dialog, expand **Connection**, expand **SSH**, and then select **Tunnels**.</span></span>

3. <span data-ttu-id="09f0d-157">Indiquez les informations suivantes dans le formulaire des **Options de contrôle de transfert du port SSH** .</span><span class="sxs-lookup"><span data-stu-id="09f0d-157">Provide the following information on the **Options controlling SSH port forwarding** form:</span></span>
   
   * <span data-ttu-id="09f0d-158">**Port source** : le port sur le client que vous souhaitez transférer.</span><span class="sxs-lookup"><span data-stu-id="09f0d-158">**Source port** - The port on the client that you wish to forward.</span></span> <span data-ttu-id="09f0d-159">Par exemple : **9876**.</span><span class="sxs-lookup"><span data-stu-id="09f0d-159">For example, **9876**.</span></span>

   * <span data-ttu-id="09f0d-160">**Destination** : l’adresse SSH pour le cluster HDInsight sous Linux.</span><span class="sxs-lookup"><span data-stu-id="09f0d-160">**Destination** - The SSH address for the Linux-based HDInsight cluster.</span></span> <span data-ttu-id="09f0d-161">Par exemple : **moncluster-ssh.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="09f0d-161">For example, **mycluster-ssh.azurehdinsight.net**.</span></span>

   * <span data-ttu-id="09f0d-162">**Dynamique** : active le routage dynamique du proxy SOCKS.</span><span class="sxs-lookup"><span data-stu-id="09f0d-162">**Dynamic** - Enables dynamic SOCKS proxy routing.</span></span>
     
     ![image des options de tunneling](./media/hdinsight-linux-ambari-ssh-tunnel/puttytunnel.png)

4. <span data-ttu-id="09f0d-164">Cliquez sur **Ajouter** pour ajouter les paramètres, puis cliquez sur **Ouvrir** pour ouvrir une connexion SSH.</span><span class="sxs-lookup"><span data-stu-id="09f0d-164">Click **Add** to add the settings, and then click **Open** to open an SSH connection.</span></span>

5. <span data-ttu-id="09f0d-165">Lorsque vous y êtes invité, connectez-vous au serveur.</span><span class="sxs-lookup"><span data-stu-id="09f0d-165">When prompted, log in to the server.</span></span>

## <a name="use-the-tunnel-from-your-browser"></a><span data-ttu-id="09f0d-166">Utilisation du tunnel à partir de votre navigateur</span><span class="sxs-lookup"><span data-stu-id="09f0d-166">Use the tunnel from your browser</span></span>

> [!IMPORTANT]
> <span data-ttu-id="09f0d-167">Les étapes décrites dans cette section utilisent le navigateur Mozilla FireFox, car il fournit les mêmes paramètres de proxy sur toutes les plateformes.</span><span class="sxs-lookup"><span data-stu-id="09f0d-167">The steps in this section use the Mozilla FireFox browser, as it provides the same proxy settings across all platforms.</span></span> <span data-ttu-id="09f0d-168">D’autres navigateurs modernes, tels que Google Chrome, peuvent nécessiter une extension du type FoxyProxy pour fonctionner avec le tunnel.</span><span class="sxs-lookup"><span data-stu-id="09f0d-168">Other modern browsers, such as Google Chrome, may require an extension such as FoxyProxy to work with the tunnel.</span></span>

1. <span data-ttu-id="09f0d-169">Configurez le navigateur pour qu’il utilise **localhost** et le port que vous avez utilisé lors de la création du tunnel en tant que proxy **SOCKS v5**.</span><span class="sxs-lookup"><span data-stu-id="09f0d-169">Configure the browser to use **localhost** and the port you used when creating the tunnel as a **SOCKS v5** proxy.</span></span> <span data-ttu-id="09f0d-170">Voici comment se présentent les paramètres Firefox :</span><span class="sxs-lookup"><span data-stu-id="09f0d-170">Here's what the Firefox settings look like.</span></span> <span data-ttu-id="09f0d-171">si vous avez utilisé un port autre que 9876, modifiez le port par celui que vous avez utilisé :</span><span class="sxs-lookup"><span data-stu-id="09f0d-171">If you used a different port than 9876, change the port to the one you used:</span></span>
   
    ![image des paramètres de Firefox](./media/hdinsight-linux-ambari-ssh-tunnel/firefoxproxy.png)
   
   > [!NOTE]
   > <span data-ttu-id="09f0d-173">La sélection de **DNS Distant** résout les requêtes DNS à l’aide du cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="09f0d-173">Selecting **Remote DNS** resolves Domain Name System (DNS) requests by using the HDInsight cluster.</span></span> <span data-ttu-id="09f0d-174">Ce paramètre résout les éléments DNS en utilisant le nœud principal du cluster.</span><span class="sxs-lookup"><span data-stu-id="09f0d-174">This setting resolves DNS using the head node of the cluster.</span></span>

2. <span data-ttu-id="09f0d-175">Vérifiez que le tunnel fonctionne en vous rendant sur un site tel que [http://www.whatismyip.com/](http://www.whatismyip.com/).</span><span class="sxs-lookup"><span data-stu-id="09f0d-175">Verify that the tunnel works by visiting a site such as [http://www.whatismyip.com/](http://www.whatismyip.com/).</span></span> <span data-ttu-id="09f0d-176">L’adresse IP renvoyée doit être celle utilisée par le centre de données Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="09f0d-176">The IP returned should be one used by the Microsoft Azure datacenter.</span></span>

## <a name="verify-with-ambari-web-ui"></a><span data-ttu-id="09f0d-177">Vérification avec l'interface utilisateur Web Ambari</span><span class="sxs-lookup"><span data-stu-id="09f0d-177">Verify with Ambari web UI</span></span>

<span data-ttu-id="09f0d-178">Une fois le cluster établi, suivez ces étapes pour vérifier que vous pouvez accéder à des interfaces utilisateur Web de service à partir du Web Ambari :</span><span class="sxs-lookup"><span data-stu-id="09f0d-178">Once the cluster has been established, use the following steps to verify that you can access service web UIs from the Ambari Web:</span></span>

1. <span data-ttu-id="09f0d-179">Dans votre navigateur, accédez à http://headnodehost:8080.</span><span class="sxs-lookup"><span data-stu-id="09f0d-179">In your browser, go to http://headnodehost:8080.</span></span> <span data-ttu-id="09f0d-180">L’adresse `headnodehost` est envoyée via le tunnel au cluster et renvoie le nœud principal sur lequel Ambari s’exécute.</span><span class="sxs-lookup"><span data-stu-id="09f0d-180">The `headnodehost` address is sent over the tunnel to the cluster and resolve to the headnode that Ambari is running on.</span></span> <span data-ttu-id="09f0d-181">Lorsque vous y êtes invité, saisissez le nom de l’utilisateur admin (admin) et le mot de passe correspondant à votre cluster.</span><span class="sxs-lookup"><span data-stu-id="09f0d-181">When prompted, enter the admin user name (admin) and password for your cluster.</span></span> <span data-ttu-id="09f0d-182">Vous pouvez y être invité une seconde fois par l'interface utilisateur Web Ambari.</span><span class="sxs-lookup"><span data-stu-id="09f0d-182">You may be prompted a second time by the Ambari web UI.</span></span> <span data-ttu-id="09f0d-183">Dans ce cas, saisissez de nouveau ces informations.</span><span class="sxs-lookup"><span data-stu-id="09f0d-183">If so, reenter the information.</span></span>

   > [!NOTE]
   > <span data-ttu-id="09f0d-184">Lorsque vous utilisez l’adresse http://headnodehost:8080 pour vous connecter au cluster, vous vous connectez via le tunnel.</span><span class="sxs-lookup"><span data-stu-id="09f0d-184">When using the http://headnodehost:8080 address to connect to the cluster, you are connecting through the tunnel.</span></span> <span data-ttu-id="09f0d-185">La communication est sécurisée grâce au tunnel SSH plutôt que via HTTPS.</span><span class="sxs-lookup"><span data-stu-id="09f0d-185">Communication is secured using the SSH tunnel instead of HTTPS.</span></span> <span data-ttu-id="09f0d-186">Pour vous connecter à Internet à l’aide de HTTPS, utilisez https://CLUSTERNAME.azurehdinsight.net, où **CLUSTERNAME** est le nom du cluster.</span><span class="sxs-lookup"><span data-stu-id="09f0d-186">To connect over the internet using HTTPS, use https://CLUSTERNAME.azurehdinsight.net, where **CLUSTERNAME** is the name of the cluster.</span></span>

2. <span data-ttu-id="09f0d-187">Dans l'interface utilisateur Web Ambari, sélectionnez HDFS dans la liste située sur la gauche de la page.</span><span class="sxs-lookup"><span data-stu-id="09f0d-187">From the Ambari Web UI, select HDFS from the list on the left of the page.</span></span>

    ![Image avec HDFS sélectionné](./media/hdinsight-linux-ambari-ssh-tunnel/hdfsservice.png)

3. <span data-ttu-id="09f0d-189">Lorsque les informations de service HDFS s’affichent, sélectionnez **Liens rapides**.</span><span class="sxs-lookup"><span data-stu-id="09f0d-189">When the HDFS service information is displayed, select **Quick Links**.</span></span> <span data-ttu-id="09f0d-190">Une liste des nœuds principaux du cluster s’affiche.</span><span class="sxs-lookup"><span data-stu-id="09f0d-190">A list of the cluster head nodes appears.</span></span> <span data-ttu-id="09f0d-191">Sélectionnez l’un des nœuds principaux, puis **Interface utilisateur NameNode**.</span><span class="sxs-lookup"><span data-stu-id="09f0d-191">Select one of the head nodes, and then select **NameNode UI**.</span></span>

    ![Image avec le menu Liens rapides développé](./media/hdinsight-linux-ambari-ssh-tunnel/namenodedropdown.png)

   > [!NOTE]
   > <span data-ttu-id="09f0d-193">Lorsque vous sélectionnez __Liens rapides__, un indicateur d’attente peut apparaître.</span><span class="sxs-lookup"><span data-stu-id="09f0d-193">When you select __Quick Links__, you may get a wait indicator.</span></span> <span data-ttu-id="09f0d-194">Cela peut se produire si votre connexion internet est lente.</span><span class="sxs-lookup"><span data-stu-id="09f0d-194">This condition can occur if you have a slow internet connection.</span></span> <span data-ttu-id="09f0d-195">Patientez une minute ou deux pour recevoir les données du serveur, puis réessayez.</span><span class="sxs-lookup"><span data-stu-id="09f0d-195">Wait a minute or two for the data to be received from the server, then try the list again.</span></span>
   >
   > <span data-ttu-id="09f0d-196">Certaines entrées du menu **Liens rapides** peuvent être tronquées par le côté droit de l’écran.</span><span class="sxs-lookup"><span data-stu-id="09f0d-196">Some entries in the **Quick Links** menu may be cut off by the right side of the screen.</span></span> <span data-ttu-id="09f0d-197">Dans ce cas, développez le menu à l’aide de la souris et utilisez la touche fléchée droite pour faire défiler l’écran vers la droite afin d’afficher le reste du menu.</span><span class="sxs-lookup"><span data-stu-id="09f0d-197">If so, expand the menu using your mouse and use the right arrow key to scroll the screen to the right to see the rest of the menu.</span></span>

4. <span data-ttu-id="09f0d-198">Une page similaire à celle ci-dessous s’affiche :</span><span class="sxs-lookup"><span data-stu-id="09f0d-198">A page similar to the following image is displayed:</span></span>

    ![Image de l’interface utilisateur NameNode](./media/hdinsight-linux-ambari-ssh-tunnel/namenode.png)

   > [!NOTE]
   > <span data-ttu-id="09f0d-200">Notez l’URL de cette page. Elle doit être semblable à **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span><span class="sxs-lookup"><span data-stu-id="09f0d-200">Notice the URL for this page; it should be similar to **http://hn1-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8088/cluster**.</span></span> <span data-ttu-id="09f0d-201">Cette URI utilise le nom de domaine complet (FQDN) interne du nœud et est uniquement accessible en cas d’utilisation d’un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="09f0d-201">This URI is using the internal fully qualified domain name (FQDN) of the node, and is only accessible when using an SSH tunnel.</span></span>

## <a name="next-steps"></a><span data-ttu-id="09f0d-202">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="09f0d-202">Next steps</span></span>

<span data-ttu-id="09f0d-203">Maintenant que vous avez appris à créer et utiliser un tunnel SSH, consultez le document suivant pour découvrir d’autres façons d’utiliser Ambari :</span><span class="sxs-lookup"><span data-stu-id="09f0d-203">Now that you have learned how to create and use an SSH tunnel, see the following document for other ways to use Ambari:</span></span>

* [<span data-ttu-id="09f0d-204">Gestion des clusters HDInsight à l'aide d’Ambari</span><span class="sxs-lookup"><span data-stu-id="09f0d-204">Manage HDInsight clusters by using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)

<span data-ttu-id="09f0d-205">Pour plus d’informations sur l’utilisation de SSH avec HDInsight, voir [Utilisation de SSH avec HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="09f0d-205">For more information on using SSH with HDInsight, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

