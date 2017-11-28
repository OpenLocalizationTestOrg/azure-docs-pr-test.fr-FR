---
title: "aaaMonitor et gérer Azure HDInsight à l’aide de l’interface utilisateur de Ambari Web | Documents Microsoft"
description: "Découvrez comment toouse Ambari toomonitor et gérer des clusters HDInsight de basés sur Linux. Dans ce document, vous découvrez comment les clusters toouse hello l’interface utilisateur Web de Ambari inclus avec HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a><span data-ttu-id="59a42-104">Gérer des clusters HDInsight à l’aide de hello Ambari Web UI</span><span class="sxs-lookup"><span data-stu-id="59a42-104">Manage HDInsight clusters by using hello Ambari Web UI</span></span>

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

<span data-ttu-id="59a42-105">Apache Ambari simplifie la gestion de hello et la surveillance d’un cluster Hadoop en fournissant un web toouse simple API REST et de l’interface utilisateur.</span><span class="sxs-lookup"><span data-stu-id="59a42-105">Apache Ambari simplifies hello management and monitoring of a Hadoop cluster by providing an easy toouse web UI and REST API.</span></span> <span data-ttu-id="59a42-106">Ambari est inclus sur les clusters HDInsight de basés sur Linux et est utilisé toomonitor hello cluster et apporter des modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="59a42-106">Ambari is included on Linux-based HDInsight clusters, and is used toomonitor hello cluster and make configuration changes.</span></span>

<span data-ttu-id="59a42-107">Dans ce document, vous découvrez comment toouse hello l’interface utilisateur de Ambari Web avec un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59a42-107">In this document, you learn how toouse hello Ambari Web UI with an HDInsight cluster.</span></span>

## <span data-ttu-id="59a42-108"><a id="whatis"></a>Présentation d'Ambari</span><span class="sxs-lookup"><span data-stu-id="59a42-108"><a id="whatis"></a>What is Ambari?</span></span>

<span data-ttu-id="59a42-109">[Apache Ambari](http://ambari.apache.org) simplifie la gestion d’Hadoop grâce à une interface utilisateur web facile à utiliser.</span><span class="sxs-lookup"><span data-stu-id="59a42-109">[Apache Ambari](http://ambari.apache.org) simplifies Hadoop management by providing an easy-to-use web UI.</span></span> <span data-ttu-id="59a42-110">Vous pouvez utiliser Ambari pour créer, gérer et surveiller les clusters Hadoop.</span><span class="sxs-lookup"><span data-stu-id="59a42-110">You can use Ambari create, manage, and monitor Hadoop clusters.</span></span> <span data-ttu-id="59a42-111">Les développeurs peuvent intégrer ces fonctionnalités dans leurs applications à l’aide de hello [API REST de Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span><span class="sxs-lookup"><span data-stu-id="59a42-111">Developers can integrate these capabilities into their applications by using hello [Ambari REST APIs](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).</span></span>

<span data-ttu-id="59a42-112">Hello l’interface utilisateur de Ambari Web est fourni par défaut avec les clusters HDInsight qui utilisent le système d’exploitation de Linux hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-112">hello Ambari Web UI is provided by default with HDInsight clusters that use hello Linux operating system.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59a42-113">Linux est hello seul système d’exploitation utilisé sur HDInsight version 3.4 ou supérieure.</span><span class="sxs-lookup"><span data-stu-id="59a42-113">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="59a42-114">Pour plus d’informations, consultez [Suppression de HDInsight sous Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="59a42-114">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> 

## <a name="connectivity"></a><span data-ttu-id="59a42-115">Connectivité</span><span class="sxs-lookup"><span data-stu-id="59a42-115">Connectivity</span></span>

<span data-ttu-id="59a42-116">Hello l’interface utilisateur de Ambari Web est disponible sur votre cluster HDInsight à HTTPS://CLUSTERNAME.azurehdidnsight.net, où **CLUSTERNAME** est le nom hello de votre cluster.</span><span class="sxs-lookup"><span data-stu-id="59a42-116">hello Ambari Web UI is available on your HDInsight cluster at HTTPS://CLUSTERNAME.azurehdidnsight.net, where **CLUSTERNAME** is hello name of your cluster.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="59a42-117">Connexion tooAmbari sur HDInsight nécessite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="59a42-117">Connecting tooAmbari on HDInsight requires HTTPS.</span></span> <span data-ttu-id="59a42-118">Lorsque vous y êtes invité pour l’authentification, utilisez le nom de compte d’administrateur hello et le mot de passe fourni lors de la création de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-118">When prompted for authentication, use hello admin account name and password you provided when hello cluster was created.</span></span>

## <a name="ssh-tunnel-proxy"></a><span data-ttu-id="59a42-119">Tunnel SSH (proxy)</span><span class="sxs-lookup"><span data-stu-id="59a42-119">SSH tunnel (proxy)</span></span>

<span data-ttu-id="59a42-120">Alors que Ambari pour votre cluster est accessible directement sur hello Internet, des liens à partir de hello l’interface utilisateur de Ambari Web (par exemple, toohello JobTracker) ne sont pas exposés sur hello internet.</span><span class="sxs-lookup"><span data-stu-id="59a42-120">While Ambari for your cluster is accessible directly over hello Internet, some links from hello Ambari Web UI (such as toohello JobTracker) are not exposed on hello internet.</span></span> <span data-ttu-id="59a42-121">tooaccess ces services, vous devez créer un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="59a42-121">tooaccess these services, you must create an SSH tunnel.</span></span> <span data-ttu-id="59a42-122">Pour plus d’informations, consultez [Utilisation du tunneling SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="59a42-122">For more information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span></span>

## <a name="ambari-web-ui"></a><span data-ttu-id="59a42-123">Interface utilisateur web d'Ambari</span><span class="sxs-lookup"><span data-stu-id="59a42-123">Ambari Web UI</span></span>

<span data-ttu-id="59a42-124">Lors de la connexion toohello l’interface utilisateur de Ambari Web, vous êtes invité à tooauthenticate toohello page.</span><span class="sxs-lookup"><span data-stu-id="59a42-124">When connecting toohello Ambari Web UI, you are prompted tooauthenticate toohello page.</span></span> <span data-ttu-id="59a42-125">Utilisateur d’administrateur de cluster de hello utilisation (par défaut, administrateur) et le mot de passe que vous avez utilisé lors de la création du cluster.</span><span class="sxs-lookup"><span data-stu-id="59a42-125">Use hello cluster admin user (default Admin) and password you used during cluster creation.</span></span>

<span data-ttu-id="59a42-126">Lors de la page de hello s’ouvre, notez barre hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-126">When hello page opens, note hello bar at hello top.</span></span> <span data-ttu-id="59a42-127">Cette barre contient des éléments suivants de hello plus d’informations et des contrôles :</span><span class="sxs-lookup"><span data-stu-id="59a42-127">This bar contains hello following information and controls:</span></span>

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* <span data-ttu-id="59a42-129">**Logo de Ambari** -tableau de bord de hello s’ouvre, ce qui peut être utilisé toomonitor hello cluster.</span><span class="sxs-lookup"><span data-stu-id="59a42-129">**Ambari logo** - Opens hello dashboard, which can be used toomonitor hello cluster.</span></span>

* <span data-ttu-id="59a42-130">**Ops # de nom de cluster** -affiche le nombre hello des opérations de Ambari en cours.</span><span class="sxs-lookup"><span data-stu-id="59a42-130">**Cluster name # ops** - Displays hello number of ongoing Ambari operations.</span></span> <span data-ttu-id="59a42-131">Nom de cluster en sélectionnant hello ou **ops de #** affiche une liste des opérations d’arrière-plan.</span><span class="sxs-lookup"><span data-stu-id="59a42-131">Selecting hello cluster name or **# ops** displays a list of background operations.</span></span>

* <span data-ttu-id="59a42-132">**alertes de #** -affiche les avertissements ou les alertes critiques, le cas échéant, pour un cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-132">**# alerts** - Displays warnings or critical alerts, if any, for hello cluster.</span></span>

* <span data-ttu-id="59a42-133">**Tableau de bord** -tableau de bord affiche hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-133">**Dashboard** - Displays hello dashboard.</span></span>

* <span data-ttu-id="59a42-134">**Services** -informations et la configuration des paramètres pour les services cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-134">**Services** - Information and configuration settings for hello services in hello cluster.</span></span>

* <span data-ttu-id="59a42-135">**Hôtes** -informations et la configuration des paramètres pour les nœuds dans le cluster de hello hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-135">**Hosts** - Information and configuration settings for hello nodes in hello cluster.</span></span>

* <span data-ttu-id="59a42-136">**Alertes** : journal contenant informations, avertissements et alertes critiques.</span><span class="sxs-lookup"><span data-stu-id="59a42-136">**Alerts** - A log of information, warnings, and critical alerts.</span></span>

* <span data-ttu-id="59a42-137">**Administrateur** -pile/services logiciels qui sont installés sur le cluster de hello, les informations de compte de service et la sécurité Kerberos.</span><span class="sxs-lookup"><span data-stu-id="59a42-137">**Admin** - Software stack/services that are installed on hello cluster, service account information, and Kerberos security.</span></span>

* <span data-ttu-id="59a42-138">**Bouton Administrateur** : gestion d'Ambari, paramètres utilisateur et déconnexion.</span><span class="sxs-lookup"><span data-stu-id="59a42-138">**Admin button** - Ambari management, user settings, and logout.</span></span>

## <a name="monitoring"></a><span data-ttu-id="59a42-139">Surveillance</span><span class="sxs-lookup"><span data-stu-id="59a42-139">Monitoring</span></span>

### <a name="alerts"></a><span data-ttu-id="59a42-140">Alertes</span><span class="sxs-lookup"><span data-stu-id="59a42-140">Alerts</span></span>

<span data-ttu-id="59a42-141">Hello liste suivante contient des États alerte courantes hello utilisés par Ambari :</span><span class="sxs-lookup"><span data-stu-id="59a42-141">hello following list contains hello common alert statuses used by Ambari:</span></span>

* <span data-ttu-id="59a42-142">**OK**</span><span class="sxs-lookup"><span data-stu-id="59a42-142">**OK**</span></span>
* <span data-ttu-id="59a42-143">**Avertissement**</span><span class="sxs-lookup"><span data-stu-id="59a42-143">**Warning**</span></span>
* <span data-ttu-id="59a42-144">**CRITIQUE**</span><span class="sxs-lookup"><span data-stu-id="59a42-144">**CRITICAL**</span></span>
* <span data-ttu-id="59a42-145">**INCONNU**</span><span class="sxs-lookup"><span data-stu-id="59a42-145">**UNKNOWN**</span></span>

<span data-ttu-id="59a42-146">Autres que des alertes **OK** provoquer hello **les alertes #** entrée haut hello hello numéro de page toodisplay hello d’alertes.</span><span class="sxs-lookup"><span data-stu-id="59a42-146">Alerts other than **OK** cause hello **# alerts** entry at hello top of hello page toodisplay hello number of alerts.</span></span> <span data-ttu-id="59a42-147">Cette entrée affiche les alertes hello et leur état.</span><span class="sxs-lookup"><span data-stu-id="59a42-147">Selecting this entry displays hello alerts and their status.</span></span>

<span data-ttu-id="59a42-148">Les alertes sont organisés en plusieurs groupes par défaut, qui peuvent être affichés à partir de hello **alertes** page.</span><span class="sxs-lookup"><span data-stu-id="59a42-148">Alerts are organized into several default groups, which can be viewed from hello **Alerts** page.</span></span>

![page d’alertes](./media/hdinsight-hadoop-manage-ambari/alerts.png)

<span data-ttu-id="59a42-150">Vous pouvez gérer les groupes de hello à l’aide de hello **Actions** menu et en sélectionnant **gérer les groupes d’alerte**.</span><span class="sxs-lookup"><span data-stu-id="59a42-150">You can manage hello groups by using hello **Actions** menu and selecting **Manage Alert Groups**.</span></span>

![gérer des groupes d'alertes, boîte de dialogue](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

<span data-ttu-id="59a42-152">Vous pouvez également gérer les méthodes d’alerte et créer des notifications d’alerte à partir de hello **Actions** menu en sélectionnant __gérer les Notifications d’alerte__.</span><span class="sxs-lookup"><span data-stu-id="59a42-152">You can also manage alerting methods, and create alert notifications from hello **Actions** menu by selecting __Manage Alert Notifications__.</span></span> <span data-ttu-id="59a42-153">Les notifications en cours sont affichées.</span><span class="sxs-lookup"><span data-stu-id="59a42-153">Any current notifications are displayed.</span></span> <span data-ttu-id="59a42-154">Vous pouvez également créer des notifications à partir d’ici.</span><span class="sxs-lookup"><span data-stu-id="59a42-154">You can also create notifications from here.</span></span> <span data-ttu-id="59a42-155">Les notifications peuvent être envoyées via **EMAIL** ou **SNMP** lorsque des combinaisons spécifiques alerte/gravité se produisent.</span><span class="sxs-lookup"><span data-stu-id="59a42-155">Notifications can be sent via **EMAIL** or **SNMP** when specific alert/severity combinations occur.</span></span> <span data-ttu-id="59a42-156">Par exemple, vous pouvez envoyer un message électronique lorsqu’un des alertes de hello Bonjour **fils par défaut** groupe est défini trop**critique**.</span><span class="sxs-lookup"><span data-stu-id="59a42-156">For example, you can send an email message when any of hello alerts in hello **YARN Default** group is set too**Critical**.</span></span>

![créer une alerte, boîte de dialogue](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

<span data-ttu-id="59a42-158">Enfin, en sélectionnant __gérer les paramètres d’alerte__ de hello __Actions__ menu vous permet de nombre de hello tooset d’occurrences d’une alerte avant une notification est envoyée.</span><span class="sxs-lookup"><span data-stu-id="59a42-158">Finally, selecting __Manage Alert Settings__ from hello __Actions__ menu allows you tooset hello number of times an alert must occur before a notification is sent.</span></span> <span data-ttu-id="59a42-159">Ce paramètre peut être utilisé tooprevent des notifications pour les erreurs temporaires.</span><span class="sxs-lookup"><span data-stu-id="59a42-159">This setting can be used tooprevent notifications for transient errors.</span></span>

### <a name="cluster"></a><span data-ttu-id="59a42-160">Cluster</span><span class="sxs-lookup"><span data-stu-id="59a42-160">Cluster</span></span>

<span data-ttu-id="59a42-161">Hello **métriques** du tableau de bord hello contient une série de widgets qui la rendent l’état de hello toomonitor facile de votre cluster en un coup de œil.</span><span class="sxs-lookup"><span data-stu-id="59a42-161">hello **Metrics** tab of hello dashboard contains a series of widgets that make it easy toomonitor hello status of your cluster at a glance.</span></span> <span data-ttu-id="59a42-162">Plusieurs widgets, tels que **Utilisation du processeur**, fournissent des informations supplémentaires lorsque vous cliquez dessus.</span><span class="sxs-lookup"><span data-stu-id="59a42-162">Several widgets, such as **CPU Usage**, provide additional information when clicked.</span></span>

![tableau de bord avec des mesures](./media/hdinsight-hadoop-manage-ambari/metrics.png)

<span data-ttu-id="59a42-164">Hello **Heatmaps** onglet affiche les métriques comme couleur heatmaps, allant de toored vert.</span><span class="sxs-lookup"><span data-stu-id="59a42-164">hello **Heatmaps** tab displays metrics as colored heatmaps, going from green toored.</span></span>

![tableau de bord avec des cartes thermiques](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

<span data-ttu-id="59a42-166">Pour plus d’informations sur les nœuds de hello au sein du cluster de hello, sélectionnez **hôtes**.</span><span class="sxs-lookup"><span data-stu-id="59a42-166">For more information on hello nodes within hello cluster, select **Hosts**.</span></span> <span data-ttu-id="59a42-167">Puis sélectionnez le nœud spécifique de hello que vous intéressez.</span><span class="sxs-lookup"><span data-stu-id="59a42-167">Then select hello specific node you are interested in.</span></span>

![détails de l'hôte](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a><span data-ttu-id="59a42-169">Services</span><span class="sxs-lookup"><span data-stu-id="59a42-169">Services</span></span>

<span data-ttu-id="59a42-170">Hello **Services** encadré sur le tableau de bord hello fournit un aperçu rapide des état hello de services hello en cours d’exécution sur le cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-170">hello **Services** sidebar on hello dashboard provides quick insight into hello status of hello services running on hello cluster.</span></span> <span data-ttu-id="59a42-171">Des icônes différentes sont utilisées tooindicate état ou les actions qui doivent être prises.</span><span class="sxs-lookup"><span data-stu-id="59a42-171">Various icons are used tooindicate status or actions that should be taken.</span></span> <span data-ttu-id="59a42-172">Par exemple, un symbole de recyclage jaune s’affiche si un service doit toobe de recyclage.</span><span class="sxs-lookup"><span data-stu-id="59a42-172">For example, a yellow recycle symbol is displayed if a service needs toobe recycled.</span></span>

![barre latérale des services](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> <span data-ttu-id="59a42-174">services Hello affichées varient entre les versions et les types de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59a42-174">hello services displayed differ between HDInsight cluster types and versions.</span></span> <span data-ttu-id="59a42-175">services Hello affichés ici peuvent être différentes de celle des services hello affichées pour votre cluster.</span><span class="sxs-lookup"><span data-stu-id="59a42-175">hello services displayed here may be different than hello services displayed for your cluster.</span></span>

<span data-ttu-id="59a42-176">Sélection d’un service affiche des informations plus détaillées sur le service de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-176">Selecting a service displays more detailed information on hello service.</span></span>

![informations de résumé du service](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a><span data-ttu-id="59a42-178">Liens rapides</span><span class="sxs-lookup"><span data-stu-id="59a42-178">Quick links</span></span>

<span data-ttu-id="59a42-179">Affichage de certains services une **liens rapides** lien en hello haut hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-179">Some services display a **Quick Links** link at hello top of hello page.</span></span> <span data-ttu-id="59a42-180">Cela peut être utilisé tooaccess web de spécifique au service interfaces utilisateur, tel que :</span><span class="sxs-lookup"><span data-stu-id="59a42-180">This can be used tooaccess service-specific web UIs, such as:</span></span>

* <span data-ttu-id="59a42-181">**Historique des travaux** : historique des travaux MapReduce.</span><span class="sxs-lookup"><span data-stu-id="59a42-181">**Job History** - MapReduce job history.</span></span>
* <span data-ttu-id="59a42-182">**Gestionnaire des ressources** : interface utilisateur du gestionnaire des ressources YARN.</span><span class="sxs-lookup"><span data-stu-id="59a42-182">**Resource Manager** - YARN ResourceManager UI.</span></span>
* <span data-ttu-id="59a42-183">**NameNode** : interface utilisateur NameNode HDFS.</span><span class="sxs-lookup"><span data-stu-id="59a42-183">**NameNode** - Hadoop Distributed File System (HDFS) NameNode UI.</span></span>
* <span data-ttu-id="59a42-184">**Interface utilisateur web Oozie** : interface utilisateur Oozie.</span><span class="sxs-lookup"><span data-stu-id="59a42-184">**Oozie Web UI** - Oozie UI.</span></span>

<span data-ttu-id="59a42-185">En sélectionnant une de ces liaisons, un nouvel onglet s’ouvre dans votre navigateur, qui affiche la page sélectionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-185">Selecting any of these links opens a new tab in your browser, which displays hello selected page.</span></span>

> [!NOTE]
> <span data-ttu-id="59a42-186">En sélectionnant hello **liens rapides** entrée pour un service peut retourner une erreur « serveur introuvable ».</span><span class="sxs-lookup"><span data-stu-id="59a42-186">Selecting hello **Quick Links** entry for a service may return a "server not found" error.</span></span> <span data-ttu-id="59a42-187">Si vous rencontrez cette erreur, vous devez utiliser un tunnel SSH lors de l’utilisation de hello **liens rapides** entrée pour ce service.</span><span class="sxs-lookup"><span data-stu-id="59a42-187">If you encounter this error, you must use an SSH tunnel when using hello **Quick Links** entry for this service.</span></span> <span data-ttu-id="59a42-188">Pour plus d’informations, consultez [Utilisation du tunneling SSH avec HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="59a42-188">For information, see [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)</span></span>

## <a name="management"></a><span data-ttu-id="59a42-189">Gestion</span><span class="sxs-lookup"><span data-stu-id="59a42-189">Management</span></span>

### <a name="ambari-users-groups-and-permissions"></a><span data-ttu-id="59a42-190">Utilisateurs d'Ambari, groupes et autorisations</span><span class="sxs-lookup"><span data-stu-id="59a42-190">Ambari users, groups, and permissions</span></span>

<span data-ttu-id="59a42-191">Il est possible de travailler avec des utilisateurs, des groupes et des autorisations lorsque vous utilisez un cluster HDInsight [joint au domaine](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59a42-191">Working with users, groups, and permissions are supported when using a [domain joined](hdinsight-domain-joined-introduction.md) HDInsight cluster.</span></span> <span data-ttu-id="59a42-192">Pour plus d’informations sur l’utilisation de hello Ambari interface utilisateur de gestion sur un cluster à un domaine, consultez [gérer appartenant au domaine des clusters HDInsight](hdinsight-domain-joined-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="59a42-192">For information on using hello Ambari Management UI on a domain-joined cluster, see [Manage domain-joined HDInsight clusters](hdinsight-domain-joined-introduction.md).</span></span>

> [!WARNING]
> <span data-ttu-id="59a42-193">Ne modifiez pas le mot de passe hello de surveillance de Ambari hello (hdinsightwatchdog) sur votre cluster HDInsight de basés sur Linux.</span><span class="sxs-lookup"><span data-stu-id="59a42-193">Do not change hello password of hello Ambari watchdog (hdinsightwatchdog) on your Linux-based HDInsight cluster.</span></span> <span data-ttu-id="59a42-194">Modification des sauts de mot de passe hello hello des actions de script toouse capacité ou effectuer des opérations de mise à l’échelle avec votre cluster.</span><span class="sxs-lookup"><span data-stu-id="59a42-194">Changing hello password breaks hello ability toouse script actions or perform scaling operations with your cluster.</span></span>

### <a name="hosts"></a><span data-ttu-id="59a42-195">Hôtes</span><span class="sxs-lookup"><span data-stu-id="59a42-195">Hosts</span></span>

<span data-ttu-id="59a42-196">Hello **hôtes** page répertorie tous les hôtes de cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-196">hello **Hosts** page lists all hosts in hello cluster.</span></span> <span data-ttu-id="59a42-197">toomanage hôtes, procédez comme suit.</span><span class="sxs-lookup"><span data-stu-id="59a42-197">toomanage hosts, follow these steps.</span></span>

![page d'hôtes](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> <span data-ttu-id="59a42-199">L’ajout, la désactivation et la remise en service d’un hôte ne doivent pas être utilisés avec des clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59a42-199">Adding, decommissioning, and recommissioning a host should not be used with HDInsight clusters.</span></span>

1. <span data-ttu-id="59a42-200">Sélectionnez l’hôte hello que vous souhaitez toomanage.</span><span class="sxs-lookup"><span data-stu-id="59a42-200">Select hello host that you wish toomanage.</span></span>

2. <span data-ttu-id="59a42-201">Hello d’utilisation **Actions** action de hello tooselect de menu que vous souhaitez tooperform :</span><span class="sxs-lookup"><span data-stu-id="59a42-201">Use hello **Actions** menu tooselect hello action that you wish tooperform:</span></span>

   * <span data-ttu-id="59a42-202">**Démarrer tous les composants** -démarrer tous les composants sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-202">**Start all components** - Start all components on hello host.</span></span>

   * <span data-ttu-id="59a42-203">**Arrêter tous les composants** -arrêter tous les composants sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-203">**Stop all components** - Stop all components on hello host.</span></span>

   * <span data-ttu-id="59a42-204">**Redémarrez tous les composants** - arrêter et démarrer tous les composants sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-204">**Restart all components** - Stop and start all components on hello host.</span></span>

   * <span data-ttu-id="59a42-205">**Activer le mode de maintenance** -supprime les alertes pour les hôtes hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-205">**Turn on maintenance mode** - Suppresses alerts for hello host.</span></span> <span data-ttu-id="59a42-206">Ce mode doit être activé si vous effectuez des actions qui génèrent des alertes.</span><span class="sxs-lookup"><span data-stu-id="59a42-206">This mode should be enabled if you are performing actions that generate alerts.</span></span> <span data-ttu-id="59a42-207">Par exemple, l’arrêt et le démarrage d’un service.</span><span class="sxs-lookup"><span data-stu-id="59a42-207">For example, stopping and starting a service.</span></span>

   * <span data-ttu-id="59a42-208">**Désactiver le mode de maintenance** -renvoie hello d’alerte de toonormal hôte.</span><span class="sxs-lookup"><span data-stu-id="59a42-208">**Turn off maintenance mode** - Returns hello host toonormal alerting.</span></span>

   * <span data-ttu-id="59a42-209">**Arrêter** -arrêt DataNode ou NodeManagers sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-209">**Stop** - Stops DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="59a42-210">**Démarrer** -démarre le DataNode ou NodeManagers sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-210">**Start** - Starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="59a42-211">**Redémarrez** -s’arrête et démarre DataNode ou NodeManagers sur l’ordinateur hôte de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-211">**Restart** - Stops and starts DataNode or NodeManagers on hello host.</span></span>

   * <span data-ttu-id="59a42-212">**Désaffecter** -supprime un ordinateur hôte en cluster de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-212">**Decommission** - Removes a host from hello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="59a42-213">N'utilisez pas cette action sur les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59a42-213">Do not use this action on HDInsight clusters.</span></span>

   * <span data-ttu-id="59a42-214">**Recommission** -ajoute un cluster de toohello hôte précédemment mis hors service.</span><span class="sxs-lookup"><span data-stu-id="59a42-214">**Recommission** - Adds a previously decommissioned host toohello cluster.</span></span>

     > [!NOTE]
     > <span data-ttu-id="59a42-215">N'utilisez pas cette action sur les clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="59a42-215">Do not use this action on HDInsight clusters.</span></span>

### <span data-ttu-id="59a42-216"><a id="service"></a>Services</span><span class="sxs-lookup"><span data-stu-id="59a42-216"><a id="service"></a>Services</span></span>

<span data-ttu-id="59a42-217">À partir de hello **tableau de bord** ou **Services** page, utilisez hello **Actions** situé en bas de hello de liste hello de services toostop et démarrer tous les services.</span><span class="sxs-lookup"><span data-stu-id="59a42-217">From hello **Dashboard** or **Services** page, use hello **Actions** button at hello bottom of hello list of services toostop and start all services.</span></span>

![Actions de service](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> <span data-ttu-id="59a42-219">Alors que **ajouter un Service** est répertorié dans ce menu ne doit pas être le cluster HDInsight de tooadd utilisé services toohello.</span><span class="sxs-lookup"><span data-stu-id="59a42-219">While **Add Service** is listed in this menu, it should not be used tooadd services toohello HDInsight cluster.</span></span> <span data-ttu-id="59a42-220">Les nouveaux services doivent être ajoutés à l'aide d'une action de script lors de l’approvisionnement du cluster.</span><span class="sxs-lookup"><span data-stu-id="59a42-220">New services should be added using a Script Action during cluster provisioning.</span></span> <span data-ttu-id="59a42-221">Pour plus d’informations sur l’utilisation des actions de script, consultez [Personnaliser des clusters HDInsight à l’aide d’actions de script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="59a42-221">For more information on using Script Actions, see [Customize HDInsight clusters using Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="59a42-222">Lors de hello **Actions** bouton peut redémarrer tous les services, la fréquence à laquelle vous souhaitez toostart, arrêter ou redémarrer un service spécifique.</span><span class="sxs-lookup"><span data-stu-id="59a42-222">While hello **Actions** button can restart all services, often you want toostart, stop, or restart a specific service.</span></span> <span data-ttu-id="59a42-223">Utilisez hello suivant des actions de tooperform étapes sur chaque service :</span><span class="sxs-lookup"><span data-stu-id="59a42-223">Use hello following steps tooperform actions on an individual service:</span></span>

1. <span data-ttu-id="59a42-224">À partir de hello **tableau de bord** ou **Services** , sélectionnez un service.</span><span class="sxs-lookup"><span data-stu-id="59a42-224">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="59a42-225">À partir du haut hello Hello **Résumé** utiliser hello, onglet **Actions Service** bouton et sélectionnez hello action tootake.</span><span class="sxs-lookup"><span data-stu-id="59a42-225">From hello top of hello **Summary** tab, use hello **Service Actions** button and select hello action tootake.</span></span> <span data-ttu-id="59a42-226">Cette action redémarre le service hello sur tous les nœuds.</span><span class="sxs-lookup"><span data-stu-id="59a42-226">This restarts hello service on all nodes.</span></span>

    ![action de service](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > <span data-ttu-id="59a42-228">Le redémarrage de certains services pendant l’exécution du cluster de hello peut générer des alertes.</span><span class="sxs-lookup"><span data-stu-id="59a42-228">Restarting some services while hello cluster is running may generate alerts.</span></span> <span data-ttu-id="59a42-229">tooavoid des alertes, vous pouvez utiliser hello **Actions Service** bouton tooenable **mode Maintenance** service hello avant d’effectuer le redémarrage de hello.</span><span class="sxs-lookup"><span data-stu-id="59a42-229">tooavoid alerts, you can use hello **Service Actions** button tooenable **Maintenance mode** for hello service before performing hello restart.</span></span>

3. <span data-ttu-id="59a42-230">Une fois qu’une action a été sélectionnée, hello **op de #** entrée haut hello tooshow par incréments de page hello qu’une opération d’arrière-plan est en cours.</span><span class="sxs-lookup"><span data-stu-id="59a42-230">Once an action has been selected, hello **# op** entry at hello top of hello page increments tooshow that a background operation is occurring.</span></span> <span data-ttu-id="59a42-231">Si configuré toodisplay, liste hello des opérations d’arrière-plan s’affiche.</span><span class="sxs-lookup"><span data-stu-id="59a42-231">If configured toodisplay, hello list of background operations is displayed.</span></span>

   > [!NOTE]
   > <span data-ttu-id="59a42-232">Si vous avez activé **mode Maintenance** pour le service de hello, n’oubliez pas de toodisable à l’aide de hello **Actions Service** bouton une fois l’opération de hello est terminée.</span><span class="sxs-lookup"><span data-stu-id="59a42-232">If you enabled **Maintenance mode** for hello service, remember toodisable it by using hello **Service Actions** button once hello operation has finished.</span></span>

<span data-ttu-id="59a42-233">tooconfigure un service, utilisez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="59a42-233">tooconfigure a service, use hello following steps:</span></span>

1. <span data-ttu-id="59a42-234">À partir de hello **tableau de bord** ou **Services** , sélectionnez un service.</span><span class="sxs-lookup"><span data-stu-id="59a42-234">From hello **Dashboard** or **Services** page, select a service.</span></span>

2. <span data-ttu-id="59a42-235">Sélectionnez hello **configurations** configuration actuelle de hello onglet s’affiche.</span><span class="sxs-lookup"><span data-stu-id="59a42-235">Select hello **Configs** tab. hello current configuration is displayed.</span></span> <span data-ttu-id="59a42-236">Une liste des configurations précédentes est également affichée.</span><span class="sxs-lookup"><span data-stu-id="59a42-236">A list of previous configurations is also displayed.</span></span>

    ![configurations](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. <span data-ttu-id="59a42-238">Utilisez hello champs affichés toomodify hello configuration, puis sélectionnez **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="59a42-238">Use hello fields displayed toomodify hello configuration, and then select **Save**.</span></span> <span data-ttu-id="59a42-239">Ou sélectionnez une configuration précédente, puis **rendre actuel** tooroll sauvegarder toohello les paramètres précédents.</span><span class="sxs-lookup"><span data-stu-id="59a42-239">Or select a previous configuration and then select **Make current** tooroll back toohello previous settings.</span></span>

## <a name="ambari-views"></a><span data-ttu-id="59a42-240">Affichages Ambari</span><span class="sxs-lookup"><span data-stu-id="59a42-240">Ambari views</span></span>

<span data-ttu-id="59a42-241">Ambari vues permettent aux développeurs les éléments d’interface utilisateur tooplug dans hello l’interface utilisateur de Ambari Web à l’aide de hello [Ambari vues Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span><span class="sxs-lookup"><span data-stu-id="59a42-241">Ambari Views allow developers tooplug UI elements into hello Ambari Web UI using hello [Ambari Views Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views).</span></span> <span data-ttu-id="59a42-242">HDInsight fournit hello suivant vues avec les types de cluster Hadoop :</span><span class="sxs-lookup"><span data-stu-id="59a42-242">HDInsight provides hello following views with Hadoop cluster types:</span></span>

* <span data-ttu-id="59a42-243">Gestionnaire de file d’attente de fils : Gestionnaire de file d’attente hello fournit une interface utilisateur simple pour afficher et modifier des files d’attente des fils.</span><span class="sxs-lookup"><span data-stu-id="59a42-243">Yarn Queue Manager: hello queue manager provides a simple UI for viewing and modifying YARN queues.</span></span>

* <span data-ttu-id="59a42-244">Ruche vue : hello la ruche de vue vous permet de toorun les requêtes Hive directement à partir de votre navigateur web.</span><span class="sxs-lookup"><span data-stu-id="59a42-244">Hive View: hello Hive View allows you toorun Hive queries directly from your web browser.</span></span> <span data-ttu-id="59a42-245">Vous pouvez enregistrer des requêtes, afficher les résultats, enregistrer les résultats de stockage de cluster toohello ou télécharger le système local tooyour de résultats.</span><span class="sxs-lookup"><span data-stu-id="59a42-245">You can save queries, view results, save results toohello cluster storage, or download results tooyour local system.</span></span> <span data-ttu-id="59a42-246">Pour plus d’informations sur l’utilisation des affichages Hive, consultez [Utiliser des affichages Hive avec HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="59a42-246">For more information on using Hive Views, see [Use Hive Views with HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>

* <span data-ttu-id="59a42-247">Affichage de tez : hello Tez vue vous permet de toobetter comprendre et optimiser des travaux.</span><span class="sxs-lookup"><span data-stu-id="59a42-247">Tez View: hello Tez View allows you toobetter understand and optimize jobs.</span></span> <span data-ttu-id="59a42-248">Vous pouvez afficher des informations sur l’exécution des tâches Tez et les ressources utilisées.</span><span class="sxs-lookup"><span data-stu-id="59a42-248">You can view information on how Tez jobs are executed and what resources are used.</span></span>
