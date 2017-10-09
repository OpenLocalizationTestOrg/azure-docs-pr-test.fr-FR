---
title: "aaaDashboard, analyse, l’échelle, configurer et connexions hybrides dans BizTalk Services | Documents Microsoft"
description: "En savoir plus sur les contrôles hello et surveiller les performances sur les onglets de portail classique hello pour les Services BizTalk : tableau de bord, analyse, l’échelle, configurer et connexions hybrides. MABS, WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7a1815db-0de2-4274-8be0-198c1b077324
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: c9fafdad20489571ee3849bbacd2c2b10933154f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="review-hello-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="13181-104">Passez en revue les onglets de tableau de bord, analyse, l’échelle, configurer et la connexion hybride hello</span><span class="sxs-lookup"><span data-stu-id="13181-104">Review hello Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="13181-105">Après avoir créé votre BizTalk Service et que vous déployez votre application, vous pouvez modifier certains des paramètres de Service BizTalk hello et surveiller les performances de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="13181-105">After you create your BizTalk Service and deploy your application, you can change some of hello BizTalk Service settings and monitor hello application performance.</span></span> 

<span data-ttu-id="13181-106">Lorsque vous ouvrez hello portail Azure classic, vous accédez automatiquement à hello **tous les éléments** onglet tooview votre BizTalk Service, sélectionnez votre BizTalk Service Bonjour **tous les éléments** onglet ou sélectionnez hello **BIZTALK SERVICES** onglet ; puis sélectionnez le nom de votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-106">When you open hello Azure classic portal, you are automatically placed at hello **ALL ITEMS** tab. tooview your BizTalk Service, select your BizTalk Service in hello **ALL ITEMS** tab or select hello **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="13181-107">Une nouvelle fenêtre s’ouvre avec hello suivant des onglets.</span><span class="sxs-lookup"><span data-stu-id="13181-107">This opens a new window with hello following tabs.</span></span> <span data-ttu-id="13181-108">Cette rubrique décrit ces onglets.</span><span class="sxs-lookup"><span data-stu-id="13181-108">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="13181-109">Démarrage rapide (</span><span class="sxs-lookup"><span data-stu-id="13181-109">Quickstart (</span></span>![Démarrage rapide][Quickstart]<span data-ttu-id="13181-111">)</span><span class="sxs-lookup"><span data-stu-id="13181-111">)</span></span>
<span data-ttu-id="13181-112">En fonction de hello BizTalk Services Édition, toutes les options répertoriées n’est peut-être pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="13181-112">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="13181-113"><strong>Obtenir les outils de hello</strong></span><span class="sxs-lookup"><span data-stu-id="13181-113"><strong>Get hello tools</strong></span></span></td>
        <td><span data-ttu-id="13181-114">Télécharger les modèles projet hello SDK des Services BizTalk tooinstall hello Visual Studio sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="13181-114">Download hello BizTalk Services SDK tooinstall hello Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="13181-115">Ces modèles créent des hello <strong>BizTalk Services</strong> (pont) et hello <strong>artefacts BizTalk Service</strong> projets (transformer) de Visual Studio qui sont déployé tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-115">These templates create hello <strong>BizTalk Services</strong> (bridge) and hello <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed tooyour BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="13181-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Comment puis-je démarrer à l’aide de hello Azure BizTalk Services SDK </a> et <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">installation Bonjour Azure BizTalk Services SDK</a> listes hello tooget étapes a démarré.</span><span class="sxs-lookup"><span data-stu-id="13181-116">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using hello Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing hello Azure BizTalk Services SDK</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="13181-117"><strong>Créer des accords partenaires</strong></span><span class="sxs-lookup"><span data-stu-id="13181-117"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="13181-118">Ouvre hello hébergé sur Azure où vous ajoutez des partenaires et créez X12, AS2, le portail Azure BizTalk Services et des accords EDIFACT EDI.</span><span class="sxs-lookup"><span data-stu-id="13181-118">Opens hello Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="13181-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration des composants de messagerie EDI sur le portail BizTalk Services</a> listes hello tooget étapes a démarré.</span><span class="sxs-lookup"><span data-stu-id="13181-119">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists hello steps tooget started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="13181-120"><strong>En savoir plus sur les services BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="13181-120"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="13181-121">Accédez toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">centre de formation</a> toolearn plus d’informations sur les Services BizTalk Azure.</span><span class="sxs-lookup"><span data-stu-id="13181-121">Go toohello <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> toolearn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="13181-122">Dans la barre des tâches hello bas hello, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="13181-122">In hello task bar at hello bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="13181-123"><strong>Gérer</strong> le déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="13181-123"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="13181-124">Ouvre le portail Azure BizTalk Services hello.</span><span class="sxs-lookup"><span data-stu-id="13181-124">Opens hello Azure BizTalk Services portal.</span></span> <span data-ttu-id="13181-125">Hello portail BizTalk Services hello entrée tooEDI configuration soit, y compris l’ajout de partenaires et la création de X12, AS2 et les accords EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="13181-125">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="13181-126">Cela est hello identique <strong>créer des accords de partenariat</strong> sur hello <strong>Quick Start</strong> onglet.</span><span class="sxs-lookup"><span data-stu-id="13181-126">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="13181-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration des composants de messagerie EDI sur le portail BizTalk Services</a> fournit des informations sur hello portail BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="13181-127">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="13181-128"><strong>Informations de connexion</strong> de hello Namespace de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="13181-128"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="13181-129">Lorsque vous sélectionnez des informations de connexion, puis hello Namespace de contrôle d’accès, émetteur par défaut, et la clé par défaut sont affichés.</span><span class="sxs-lookup"><span data-stu-id="13181-129">When you select Connection Information, then hello Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="13181-130">Vous pouvez copier ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="13181-130">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="13181-131">Vous pouvez également ouvrir hello portail de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="13181-131">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="13181-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Créer un contrôle d’accès Namespace</a> fournit des informations sur le portail de contrôle d’accès de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-132"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="13181-133"><strong>Synchroniser les clés</strong> Bonjour compte de stockage</span><span class="sxs-lookup"><span data-stu-id="13181-133"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="13181-134">Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="13181-134">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="13181-135">Ces clés de chiffrement de contrôlent l’accès tooyour compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13181-135">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="13181-136">Votre BizTalk Service utilise automatiquement hello clé primaire.</span><span class="sxs-lookup"><span data-stu-id="13181-136">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="13181-137"><strong>Synchroniser les clés</strong> activer tooswitch utilisateurs entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-137"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="13181-138">Par exemple, vous souhaitez hello BizTalk Service toouse une nouvelle clé primaire pour hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13181-138">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="13181-139">toodo cela :</span><span class="sxs-lookup"><span data-stu-id="13181-139">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="13181-140">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="13181-140">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="13181-141">Sélectionnez hello clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="13181-141">Select hello Secondary Key.</span></span> <span data-ttu-id="13181-142">Lorsque vous effectuez cette opération, hello BizTalk Service démarre à l’aide de la clé secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-142">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="13181-143">Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé primaire.</span><span class="sxs-lookup"><span data-stu-id="13181-143">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="13181-144">N’oubliez pas, votre BizTalk Service est hello clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="13181-144">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="13181-145">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="13181-145">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="13181-146">À présent, sélectionnez hello clé primaire.</span><span class="sxs-lookup"><span data-stu-id="13181-146">Now, select hello Primary Key.</span></span> <span data-ttu-id="13181-147">Cela est hello nouvelle clé primaire vous régénéré.</span><span class="sxs-lookup"><span data-stu-id="13181-147">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="13181-148">Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="13181-148">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="13181-149">On parle de « clés de substitution » pour décrire ce processus.</span><span class="sxs-lookup"><span data-stu-id="13181-149">This process is called "rollover keys".</span></span> <span data-ttu-id="13181-150">objectif de Hello est tooswitch d’utilisateurs tooenable entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-150">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="13181-151"><strong>Supprimer</strong> votre application</span><span class="sxs-lookup"><span data-stu-id="13181-151"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="13181-152">Lorsque vous sélectionnez Supprimer, votre BizTalk Service et tous les éléments déployés tooit sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="13181-152">When you select Delete, your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="13181-153">tableau de bord</span><span class="sxs-lookup"><span data-stu-id="13181-153">Dashboard</span></span>
<span data-ttu-id="13181-154">En fonction de hello BizTalk Services Édition, toutes les options répertoriées n’est peut-être pas disponibles.</span><span class="sxs-lookup"><span data-stu-id="13181-154">Depending on hello BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="13181-155">Lorsque vous sélectionnez le nom de votre BizTalk Service, onglet de tableau de bord hello s’affiche.</span><span class="sxs-lookup"><span data-stu-id="13181-155">When you select your BizTalk Service name, hello Dashboard tab is displayed.</span></span> <span data-ttu-id="13181-156">Dans le tableau de bord, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="13181-156">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-hello-number-of-used-hybrid-connections"></a><span data-ttu-id="13181-157">Présentation de l’utilisation : Montre le nombre de hello de connexions hybrides utilisées</span><span class="sxs-lookup"><span data-stu-id="13181-157">Usage Overview: Shows hello number of used Hybrid Connections</span></span>
<span data-ttu-id="13181-158">Affiche également l’utilisation des données hello en Go.</span><span class="sxs-lookup"><span data-stu-id="13181-158">Also displays hello data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="13181-159">Graphique métrique : illustre une liste fixe de mesures de performances.</span><span class="sxs-lookup"><span data-stu-id="13181-159">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="13181-160">Ces métriques fournissent des valeurs en temps réel concernant l’intégrité hello hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-160">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="13181-161">Vous pouvez également choisir hello **relatif** ou **absolu** intervalle de temps de valeurs et hello **intervalle** des métriques hello sont affichées dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-161">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed in hello graph.</span></span> 

<span data-ttu-id="13181-162">Pour obtenir une description de ces métriques de performances, consultez trop[métriques disponibles](#Metrics) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="13181-162">For a description of these performance metrics, go too[Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="13181-163">Aperçu rapide : dresse la liste des propriétés de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="13181-163">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="13181-164"><strong>Mettre à jour les informations d’identification de la base de données de suivi</strong></span><span class="sxs-lookup"><span data-stu-id="13181-164"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="13181-165">Modifications hello nom d’utilisateur et mot de passe utilisé toolog dans hello de base de données de suivi.</span><span class="sxs-lookup"><span data-stu-id="13181-165">Changes hello user name and password used toolog into hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-166"><strong>Mettre à jour le certificat SSL</strong></span><span class="sxs-lookup"><span data-stu-id="13181-166"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="13181-167">Peut mettre à jour hello BizTalk Service toouse un autre certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="13181-167">Can update hello BizTalk Service toouse a different SSL certificate.</span></span> <span data-ttu-id="13181-168">Un certificat SSL auto-signé est créé automatiquement lorsque vous <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">créer hello BizTalk Service</a>.</span><span class="sxs-lookup"><span data-stu-id="13181-168">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create hello BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-169"><strong>Télécharger le certificat</strong></span><span class="sxs-lookup"><span data-stu-id="13181-169"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="13181-170">Vous pouvez télécharger le certificat SSL de hello utilisé par votre ordinateur local tooa de BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-170">You can download hello SSL certificate used by your BizTalk Service tooa local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-171"><strong>État</strong></span><span class="sxs-lookup"><span data-stu-id="13181-171"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="13181-172">Affiche l’état actuel de hello de votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-172">Displays hello current status of your BizTalk Service.</span></span> <span data-ttu-id="13181-173">Voir <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Tableau comparatif des états de BizTalk Services</a>.</span><span class="sxs-lookup"><span data-stu-id="13181-173">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="13181-174"><strong>URL du service</strong></span><span class="sxs-lookup"><span data-stu-id="13181-174"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="13181-175">URL de Hello pour votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-175">hello URL for your BizTalk Service.</span></span> <span data-ttu-id="13181-176">Cela est hello même comme hello <strong>URL de domaine</strong> entré lors de la création de votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-176">This is hello same as hello <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-177"><strong>Adresse IP virtuelle (VIP) publique</strong></span><span class="sxs-lookup"><span data-stu-id="13181-177"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="13181-178">adresse IP de Hello affecté tooyour BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-178">hello IP address assigned tooyour BizTalk Service.</span></span> <span data-ttu-id="13181-179">Il est utilisé pour tous les points de terminaison d’entrée et est l’adresse de la source hello pour le trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="13181-179">It is used for all input endpoints and is hello source address for outbound traffic.</span></span> <span data-ttu-id="13181-180">Cette adresse IP appartient tooyour BizTalk Service tant qu’il est créé.</span><span class="sxs-lookup"><span data-stu-id="13181-180">This IP address belongs tooyour BizTalk Service as long as it is created.</span></span> <span data-ttu-id="13181-181">Si vous supprimez hello BizTalk Service, adresse IP de hello est affecté tooanother BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-181">If you delete hello BizTalk Service, hello IP address is assigned tooanother BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-182"><strong>Espace de noms ACS</strong></span><span class="sxs-lookup"><span data-stu-id="13181-182"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="13181-183">Authentifie avec hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-183">Authenticates with hello BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-184"><strong>Édition</strong></span><span class="sxs-lookup"><span data-stu-id="13181-184"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="13181-185">Répertorie les hello que Édition entrée lors de la création de hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-185">Lists hello Edition entered when hello BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-186"><strong>Emplacement</strong></span><span class="sxs-lookup"><span data-stu-id="13181-186"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="13181-187">Affiche hello région géographique qui héberge votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-187">Displays hello geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-188"><strong>Créé</strong></span><span class="sxs-lookup"><span data-stu-id="13181-188"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="13181-189">Hello de date et heure de hello affiche le BizTalk Service a été créé.</span><span class="sxs-lookup"><span data-stu-id="13181-189">Displays hello date and time hello BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-190"><strong>Base de données des suivis</strong></span><span class="sxs-lookup"><span data-stu-id="13181-190"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="13181-191">nom de base de données SQL Azure Hello qui stocke hello suivi des tables utilisées par votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-191">hello Azure SQL Database name that stores hello tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="13181-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Configuration requise expliqué</a> fournit des détails sur hello de base de données de suivi.</span><span class="sxs-lookup"><span data-stu-id="13181-192">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-193"><strong>Stockage de surveillance/archivage</strong></span><span class="sxs-lookup"><span data-stu-id="13181-193"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="13181-194">nom de compte du stockage Azure Hello qui stocke hello surveillent la sortie de votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-194">hello Azure Storage account name that stores hello monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="13181-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Configuration requise expliqué</a> fournit des détails sur hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13181-195">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on hello Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-196"><strong>Nom d’abonnement</strong></span><span class="sxs-lookup"><span data-stu-id="13181-196"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="13181-197">Répertorie les abonnement hello qui héberge votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-197">Lists hello subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="13181-198">abonnement de Hello régit l’accès toohello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="13181-198">hello subscription governs access toohello Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-199"><strong>Identifiant d’abonnement</strong></span><span class="sxs-lookup"><span data-stu-id="13181-199"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="13181-200">Lorsqu’un abonnement est créé, un ID d’abonnement est automatiquement généré.</span><span class="sxs-lookup"><span data-stu-id="13181-200">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="13181-201">Lorsque vous utilisez l’API REST, vous devrez peut-être hello tooenter ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="13181-201">When using REST APIs, you may need tooenter hello Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="13181-202">[BizTalk Services : Mise en service portail classique d’à l’aide de Azure](http://go.microsoft.com/fwlink/p/?LinkID=302280) listes hello étapes toocreate un BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-202">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists hello steps toocreate a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-hello-task-bar"></a><span data-ttu-id="13181-203">Gérer les informations de connexion, synchroniser les clés et les supprimer dans la barre des tâches hello :</span><span class="sxs-lookup"><span data-stu-id="13181-203">Manage, Connection Information, Sync Keys, and Delete in hello task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="13181-204"><strong>Gérer</strong> le déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="13181-204"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="13181-205">Hello ouvre le portail Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="13181-205">Opens hello Azure BizTalk Services Portal.</span></span> <span data-ttu-id="13181-206">Hello portail BizTalk Services hello entrée tooEDI configuration soit, y compris l’ajout de partenaires et la création de X12, AS2 et les accords EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="13181-206">hello BizTalk Services Portal is hello entrance tooEDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="13181-207">Cela est hello identique <strong>créer des accords de partenariat</strong> sur hello <strong>Quick Start</strong> onglet.</span><span class="sxs-lookup"><span data-stu-id="13181-207">This is hello same as <strong>Create partner agreements</strong> on hello <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="13181-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration des composants de messagerie EDI sur le portail BizTalk Services</a> fournit des informations sur hello portail BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="13181-208">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on hello BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-209"><strong>Informations de connexion</strong> de hello Namespace de contrôle d’accès</span><span class="sxs-lookup"><span data-stu-id="13181-209"><strong>Connection Information</strong> of hello Access Control Namespace</span></span></td>
<td><span data-ttu-id="13181-210">Affiche hello Namespace de contrôle d’accès, émetteur par défaut et les valeurs de clé par défaut ; qui peut être copié.</span><span class="sxs-lookup"><span data-stu-id="13181-210">Displays hello Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="13181-211">Vous pouvez également ouvrir hello portail de contrôle d’accès.</span><span class="sxs-lookup"><span data-stu-id="13181-211">You can also open hello Access Control Portal.</span></span> <span data-ttu-id="13181-212">Ce portail de contrôle d’accès est hello même fonction que l’option d’Active Directory hello dans le volet de navigation gauche hello.</span><span class="sxs-lookup"><span data-stu-id="13181-212">This Access Control Portal is hello same as using hello Active Directory option in hello left navigation pane.</span></span>
<br/><br/><span data-ttu-id="13181-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">La gestion de votre ACS Namespace</a> fournit des informations sur le portail de contrôle d’accès de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-213">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on hello Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-214"><strong>Synchroniser les clés</strong> Bonjour compte de stockage</span><span class="sxs-lookup"><span data-stu-id="13181-214"><strong>Sync Keys</strong> in hello Storage Account</span></span></td>
<td><span data-ttu-id="13181-215">Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="13181-215">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="13181-216">Ces clés de chiffrement de contrôlent l’accès tooyour compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13181-216">These encryption Keys control access tooyour Storage Account.</span></span> <span data-ttu-id="13181-217">Votre BizTalk Service utilise automatiquement hello clé primaire.</span><span class="sxs-lookup"><span data-stu-id="13181-217">Your BizTalk Service automatically uses hello Primary Key.</span></span> <span data-ttu-id="13181-218"><strong>Synchroniser les clés</strong> activer tooswitch utilisateurs entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-218"><strong>Sync Keys</strong> enable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="13181-219">Par exemple, vous souhaitez hello BizTalk Service toouse une nouvelle clé primaire pour hello compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="13181-219">For example, you want hello BizTalk Service toouse a new Primary Key for hello Storage Account.</span></span> <span data-ttu-id="13181-220">toodo cela :</span><span class="sxs-lookup"><span data-stu-id="13181-220">toodo this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="13181-221">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="13181-221">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="13181-222">Sélectionnez hello clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="13181-222">Select hello Secondary Key.</span></span> <span data-ttu-id="13181-223">Lorsque vous effectuez cette opération, hello BizTalk Service démarre à l’aide de la clé secondaire de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-223">When you do this, hello BizTalk Service starts using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="13181-224">Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé primaire.</span><span class="sxs-lookup"><span data-stu-id="13181-224">In hello Azure classic portal, select your Storage account and Regenerate hello Primary Key.</span></span> <span data-ttu-id="13181-225">N’oubliez pas, votre BizTalk Service est hello clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="13181-225">Remember, your BizTalk Service is using hello Secondary Key.</span></span></li>
<li><span data-ttu-id="13181-226">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="13181-226">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="13181-227">À présent, sélectionnez hello clé primaire.</span><span class="sxs-lookup"><span data-stu-id="13181-227">Now, select hello Primary Key.</span></span> <span data-ttu-id="13181-228">Cela est hello nouvelle clé primaire vous régénéré.</span><span class="sxs-lookup"><span data-stu-id="13181-228">This is hello new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="13181-229">Bonjour portail Azure classic, sélectionnez votre compte de stockage et régénérer hello clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="13181-229">In hello Azure classic portal, select your Storage account and Regenerate hello Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="13181-230">On parle de « clés de substitution » pour décrire ce processus.</span><span class="sxs-lookup"><span data-stu-id="13181-230">This process is called "rollover keys".</span></span> <span data-ttu-id="13181-231">objectif de Hello est tooswitch d’utilisateurs tooenable entre hello Primary Key et hello clé secondaire sans interrompre hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-231">hello purpose is tooenable users tooswitch between hello Primary Key and hello Secondary Key without disrupting hello BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="13181-232"><strong>Supprimer</strong> votre application</span><span class="sxs-lookup"><span data-stu-id="13181-232"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="13181-233">Votre BizTalk Service et tous les éléments déployés tooit sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="13181-233">Your BizTalk Service and all items deployed tooit are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="13181-234">Surveiller</span><span class="sxs-lookup"><span data-stu-id="13181-234">Monitor</span></span>
<span data-ttu-id="13181-235">Ne s’applique pas toohello édition gratuite.</span><span class="sxs-lookup"><span data-stu-id="13181-235">Does not apply toohello Free Edition.</span></span>

<span data-ttu-id="13181-236">Lorsque vous sélectionnez le nom de votre BizTalk Service, onglet de surveillance hello est disponible et hello les informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="13181-236">When you select your BizTalk Service name, hello Monitor tab is available and displays hello following:</span></span>

##### <a name="metric-graph-displays-hello-selected-performance-metrics"></a><span data-ttu-id="13181-237">Graphique de métrique : Hello d’affiche sélectionné des métriques de performances</span><span class="sxs-lookup"><span data-stu-id="13181-237">Metric Graph: Displays hello selected performance metrics</span></span>
<span data-ttu-id="13181-238">Ces métriques fournissent des valeurs en temps réel concernant l’intégrité hello hello BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-238">These metrics provide real-time values regarding hello health of hello BizTalk Service.</span></span> <span data-ttu-id="13181-239">Vous choisissez les mesures de performances devant s'afficher</span><span class="sxs-lookup"><span data-stu-id="13181-239">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="13181-240">(jusqu'à six mesures de performances simultanément).</span><span class="sxs-lookup"><span data-stu-id="13181-240">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="13181-241">Vous pouvez également choisir hello **relatif** ou **absolu** intervalle de temps de valeurs et hello **intervalle** des métriques hello sont affichées.</span><span class="sxs-lookup"><span data-stu-id="13181-241">You can also choose hello **Relative** or **Absolute** values and hello time range **Interval** of hello metrics that are displayed.</span></span> 

##### <a name="tooremove-or-display-metrics-in-hello-graph"></a><span data-ttu-id="13181-242">tooremove ou l’affichage des métriques dans le graphique de hello :</span><span class="sxs-lookup"><span data-stu-id="13181-242">tooremove or display metrics in hello graph:</span></span>
1. <span data-ttu-id="13181-243">Sélectionnez hello **moniteur** onglet.</span><span class="sxs-lookup"><span data-stu-id="13181-243">Select hello **Monitor** tab.</span></span>
2. <span data-ttu-id="13181-244">Sélectionnez **ajouter des métriques** dans la barre des tâches hello :</span><span class="sxs-lookup"><span data-stu-id="13181-244">Select **Add Metrics** in hello task bar:</span></span>  
   <span data-ttu-id="13181-245">![Sélectionnez Ajouter des métriques.][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="13181-245">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="13181-246">Vérifiez les mesures de performances hello souhaité toodisplay.</span><span class="sxs-lookup"><span data-stu-id="13181-246">Check hello performance metrics you want toodisplay.</span></span>
4. <span data-ttu-id="13181-247">Sélectionnez hello coche tooreturn toohello **moniteur** onglet.</span><span class="sxs-lookup"><span data-stu-id="13181-247">Select hello checkmark tooreturn toohello **Monitor** tab.</span></span>
5. <span data-ttu-id="13181-248">Sélectionnez hello cercle suivant toohello métrique toodisplay les valeur de cette mesure dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-248">Select hello circle next toohello metric toodisplay that metric's value in hello graph.</span></span>  
   
    <span data-ttu-id="13181-249">Par exemple, hello **l’utilisation du processeur** métrique est grisée ; sa sortie n’est pas affichée dans le graphique de hello :</span><span class="sxs-lookup"><span data-stu-id="13181-249">For example, hello **CPU Usage** metric is grayed out; its output is not displayed in hello graph:</span></span>  
   <span data-ttu-id="13181-250">![La mesure Utilisation du processeur apparaît en grisé][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="13181-250">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="13181-251">Sélectionnez hello grisée hello tooenable de cercle **l’utilisation du processeur** toodisplay métrique sa sortie dans le graphique de hello :</span><span class="sxs-lookup"><span data-stu-id="13181-251">Select hello grayed out circle tooenable hello **CPU Usage** metric toodisplay its output in hello graph:</span></span>  
   <span data-ttu-id="13181-252">![La mesure Utilisation du processeur est activée][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="13181-252">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="13181-253">tooremove une métrique de graphique d’affichage hello et de la liste de hello, sélectionnez **supprimer une métrique** dans la barre des tâches hello.</span><span class="sxs-lookup"><span data-stu-id="13181-253">tooremove a metric from hello display graph and hello list, select **Delete Metric** in hello task bar.</span></span> <span data-ttu-id="13181-254">tooadd hello métrique toohello précédent la liste, sélectionnez **ajouter des métriques** dans la barre des tâches hello, vérifiez la métrique de hello et sélectionnez hello coche tooreturn toohello **moniteur** onglet. Sélectionnez hello grisée métrique de cercle tooenable hello.</span><span class="sxs-lookup"><span data-stu-id="13181-254">tooadd hello metric back toohello list, select **Add Metrics** in hello task bar, check hello metric, and select hello checkmark tooreturn toohello **Monitor** tab. Select hello grayed out circle tooenable hello metric.</span></span>

## <span data-ttu-id="13181-255"><a name="Metrics"></a>Mesures disponibles</span><span class="sxs-lookup"><span data-stu-id="13181-255"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="13181-256">Hello suivant des compteurs de performances est disponible :</span><span class="sxs-lookup"><span data-stu-id="13181-256">hello following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="13181-257"><strong>Latence aller-retour</strong></span><span class="sxs-lookup"><span data-stu-id="13181-257"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="13181-258">Affiche le temps moyen de hello nécessaire en millisecondes (ms) les tooprocess que réception d’un message à partir du message de type hello hello temps jusqu'à ce que le message de type hello est entièrement traité par hello BizTalk Service sur tous les ponts.</span><span class="sxs-lookup"><span data-stu-id="13181-258">Displays hello average time taken in milliseconds (ms) tooprocess a message from hello time hello message is received until hello message is fully processed by hello BizTalk Service across all bridges.</span></span> <span data-ttu-id="13181-259">Seuls les messages correctement traités sont comptabilisés.</span><span class="sxs-lookup"><span data-stu-id="13181-259">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="13181-260">En cas de hello suivant des événements, un horodatage est créé :</span><span class="sxs-lookup"><span data-stu-id="13181-260">When hello following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="13181-261">Message entre dans la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="13181-261">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="13181-262">Message est routé toohello destination</span><span class="sxs-lookup"><span data-stu-id="13181-262">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="13181-263">Une réponse de la destination est reçue</span><span class="sxs-lookup"><span data-stu-id="13181-263">Destination response is received</span></span></li>
<li><span data-ttu-id="13181-264">Destination accusé de réception réponse envoyée toohello passerelle</span><span class="sxs-lookup"><span data-stu-id="13181-264">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="13181-265">Cette mesure indique le résultat hello Hello après le calcul :</span><span class="sxs-lookup"><span data-stu-id="13181-265">This metric shows hello result of hello following calculation:</span></span>
<br/><br/>
<span data-ttu-id="13181-266">[Destination accusé de réception réponse envoyée toohello passerelle] - [Message entre dans la passerelle de hello]</span><span class="sxs-lookup"><span data-stu-id="13181-266">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-267"><strong>Défaillances à la source</strong></span><span class="sxs-lookup"><span data-stu-id="13181-267"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="13181-268">Affiche le nombre total de hello de messages qui ont échoué par hello BizTalk Service lors de l’extraction des messages à partir de points de terminaison source hello.</span><span class="sxs-lookup"><span data-stu-id="13181-268">Displays hello total number of messages that failed by hello BizTalk Service when pulling messages from hello source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-269"><strong>Utilisation du processeur</strong></span><span class="sxs-lookup"><span data-stu-id="13181-269"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="13181-270">Répertorie les hello % temps processeur moyen de toutes les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="13181-270">Lists hello average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-271"><strong>Latence de traitement</strong></span><span class="sxs-lookup"><span data-stu-id="13181-271"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="13181-272">Affiche la durée moyenne hello dans tooprocess millisecondes (ms) un message par hello BizTalk Service sur tous les ponts, à l’exclusion hello temps passé dans les destinations.</span><span class="sxs-lookup"><span data-stu-id="13181-272">Displays hello average time taken In milliseconds (ms) tooprocess a message by hello BizTalk Service across all bridges, excluding hello time spent in destinations.</span></span> <span data-ttu-id="13181-273">Seuls les messages correctement traités sont comptabilisés.</span><span class="sxs-lookup"><span data-stu-id="13181-273">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="13181-274">Lorsque chaque hello suivant des événements se produisent, un horodatage est créé :</span><span class="sxs-lookup"><span data-stu-id="13181-274">When each of hello following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="13181-275">Message entre dans la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="13181-275">Message enters hello gateway</span></span></li>
<li><span data-ttu-id="13181-276">Message est routé toohello destination</span><span class="sxs-lookup"><span data-stu-id="13181-276">Message is routed toohello destination</span></span></li>
<li><span data-ttu-id="13181-277">Une réponse de la destination est reçue</span><span class="sxs-lookup"><span data-stu-id="13181-277">Destination response is received</span></span></li>
<li><span data-ttu-id="13181-278">Destination accusé de réception réponse envoyée toohello passerelle</span><span class="sxs-lookup"><span data-stu-id="13181-278">Destination acknowledgement response sent toohello gateway</span></span></li>
</ul>
<br/><span data-ttu-id="13181-279">Cette mesure indique le résultat hello Hello après le calcul :</span><span class="sxs-lookup"><span data-stu-id="13181-279">This metric shows hello result of hello following calculation:</span></span><br/><br/>
<span data-ttu-id="13181-280">[Destination accusé de réception réponse envoyée toohello passerelle] - [Message entre dans la passerelle de hello] - [Destination réponse] + [Message est routé toohello destination]</span><span class="sxs-lookup"><span data-stu-id="13181-280">[Destination acknowledgement response sent toohello gateway] - [Message enters hello gateway] - [Destination response is received] + [Message is routed toohello destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-281"><strong>Défaillances dans le processus</strong></span><span class="sxs-lookup"><span data-stu-id="13181-281"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="13181-282">Affiche le nombre total de hello de messages ayant échoué au cours du traitement par hello BizTalk Service sur tous les ponts hello dans un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="13181-282">Displays hello total number of messages that failed during processing by hello BizTalk Service across all hello bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-283"><strong>Messages envoyés</strong></span><span class="sxs-lookup"><span data-stu-id="13181-283"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="13181-284">Affiche hello le nombre total de messages envoyés par hello BizTalk Service sur tous les ponts dans un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="13181-284">Displays hello total number of messages sent by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="13181-285">Cette mesure est incrémentée lorsqu’un message envoyé à partir d’un pipeline atteint la destination de routage hello.</span><span class="sxs-lookup"><span data-stu-id="13181-285">This metric is incremented when a message sent from a pipeline reaches hello route destination.</span></span> <span data-ttu-id="13181-286">Cette mesure n'indique pas qu'un message a été traité correctement.</span><span class="sxs-lookup"><span data-stu-id="13181-286">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="13181-287">Dans un scénario de demande-réponse, la métrique de hello est incrémenté lorsque la destination de routage hello envoie un pipeline toohello arrière d’accusé de réception accusé de réception.</span><span class="sxs-lookup"><span data-stu-id="13181-287">In a Request-Reply scenario, hello metric is incremented when hello route destination sends a receipt acknowledgement back toohello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-288"><strong>Messages reçus</strong></span><span class="sxs-lookup"><span data-stu-id="13181-288"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="13181-289">Affiche hello le nombre total de messages reçus par hello BizTalk Service sur tous les ponts dans un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="13181-289">Displays hello total number of messages received by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="13181-290">Cette mesure est incrémentée lorsqu’un nouveau message est reçu par le pipeline de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-290">This metric is incremented when a new message is received by hello pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-291"><strong>Messages en cours de traitement</strong></span><span class="sxs-lookup"><span data-stu-id="13181-291"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="13181-292">Affiche hello nombre total de messages actuellement traités par hello BizTalk Service dans un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="13181-292">Displays hello total number of messages currently being processed by hello BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="13181-293"><strong>Messages traités</strong></span><span class="sxs-lookup"><span data-stu-id="13181-293"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="13181-294">Affiche hello nombre total de messages traités correctement par hello BizTalk Service sur tous les ponts dans un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="13181-294">Displays hello total number of messages successfully processed by hello BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="13181-295">Cette mesure est incrémentée lorsqu’un message est reçu avec succès par le pipeline de hello et de destination de toohello routé avec succès.</span><span class="sxs-lookup"><span data-stu-id="13181-295">This metric is incremented when a message is successfully received by hello pipeline and successfully routed toohello destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="13181-296">Mettre à l'échelle</span><span class="sxs-lookup"><span data-stu-id="13181-296">Scale</span></span>
<span data-ttu-id="13181-297">Dans l’onglet échelle hello, vous pouvez ajouter ou soustraire nombre hello d’unités utilisées par votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-297">In hello Scale tab, you can add or subtract hello number of units used by your BizTalk Service.</span></span> <span data-ttu-id="13181-298">Par défaut, une seule unité est configurée.</span><span class="sxs-lookup"><span data-stu-id="13181-298">By default, there is one Unit configured.</span></span> <span data-ttu-id="13181-299">Unités supplémentaires peuvent être ajoutées tooscale votre BizTalk Service.</span><span class="sxs-lookup"><span data-stu-id="13181-299">Additional Units can be added tooscale your BizTalk Service.</span></span> <span data-ttu-id="13181-300">Lorsque vous augmentez la montée en puissance hello, vous augmentez le débit.</span><span class="sxs-lookup"><span data-stu-id="13181-300">When you increase hello scale, you are increasing throughput.</span></span> <span data-ttu-id="13181-301">quantité Hello de ressources augmente également, y compris les ponts déployés, les contrats, les connexions métier et la puissance de traitement.</span><span class="sxs-lookup"><span data-stu-id="13181-301">hello amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="13181-302">Par exemple, vous augmentez échelle hello de 1 unité too2 unités.</span><span class="sxs-lookup"><span data-stu-id="13181-302">For example, you increase hello scale from 1 Unit too2 Units.</span></span> <span data-ttu-id="13181-303">Dans ce cas, vous pouvez déployer hello double nombre de ponts, double accords de hello, double hello LOB connexions et une puissance de traitement hello double.</span><span class="sxs-lookup"><span data-stu-id="13181-303">In this situation, you can deploy double hello number of bridges, double hello agreements, double hello LOB connections, and double hello processing power.</span></span>

<span data-ttu-id="13181-304">Certaines éditions BizTalk n'offrent pas de possibilité de mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="13181-304">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="13181-305">Dans ce cas, une seule unité est autorisée.</span><span class="sxs-lookup"><span data-stu-id="13181-305">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="13181-306">toodetermine le nombre d’unités peut être monté en votre édition, consultez trop[Services BizTalk : tableau comparatif des éditions](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="13181-306">toodetermine how many units your edition can be scaled, refer too[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="13181-307">Augmentation du nombre hello d’unités peut affecter la tarification.</span><span class="sxs-lookup"><span data-stu-id="13181-307">Increasing hello number of units may impact pricing.</span></span> <span data-ttu-id="13181-308">Si vous augmentez les unités hello, en sélectionnant **enregistrer** affiche un message qui vous indique si la facturation est affectée.</span><span class="sxs-lookup"><span data-stu-id="13181-308">If you increase hello Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="13181-309">Vous choisissez ensuite toocontinue.</span><span class="sxs-lookup"><span data-stu-id="13181-309">You then choose toocontinue.</span></span> <span data-ttu-id="13181-310">Lorsque vous augmentez le nombre de hello d’unités, hello état du BizTalk Service remplace tooUpdating Active.</span><span class="sxs-lookup"><span data-stu-id="13181-310">When you increase hello number of Units, hello BizTalk Service status changes from Active tooUpdating.</span></span> <span data-ttu-id="13181-311">Dans l’état de mise à jour de hello, votre BizTalk Service se poursuit toorun.</span><span class="sxs-lookup"><span data-stu-id="13181-311">In hello Updating state, your BizTalk Service continues toorun.</span></span>

<span data-ttu-id="13181-312">[Tableau comparatif des éditions de BizTalk Services](biztalk-editions-feature-chart.md) définit une « unité ».</span><span class="sxs-lookup"><span data-stu-id="13181-312">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="13181-313">Configuration</span><span class="sxs-lookup"><span data-stu-id="13181-313">Configure</span></span>
<span data-ttu-id="13181-314">Ne s’applique pas les connexions tooHybrid.</span><span class="sxs-lookup"><span data-stu-id="13181-314">Does not apply tooHybrid Connections.</span></span>

<span data-ttu-id="13181-315">Définit tooNone d’état de la sauvegarde hello ou automatique.</span><span class="sxs-lookup"><span data-stu-id="13181-315">Sets hello Backup Status tooNone or Automatic.</span></span> <span data-ttu-id="13181-316">Lorsque la valeur tooNone, aucune sauvegarde n’est créés automatiquement.</span><span class="sxs-lookup"><span data-stu-id="13181-316">When set tooNone, no backups are automatically created.</span></span> <span data-ttu-id="13181-317">Lorsque la valeur tooAutomatic, vous configurez l’emplacement de sauvegarde hello, fréquence de sauvegarde de hello, combien de temps tookeep hello sauvegarder des fichiers et de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-317">When set tooAutomatic, you configure hello backup location, hello frequency of hello backup, and how long tookeep hello backup files.</span></span> 

<span data-ttu-id="13181-318">[Les Services BizTalk : Sauvegarde et restauration](biztalk-backup-restore.md) fournit des détails de hello.</span><span class="sxs-lookup"><span data-stu-id="13181-318">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides hello details.</span></span> 

## <span data-ttu-id="13181-319"><a name="HybridConnections"></a>Connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="13181-319"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="13181-320">Connexions hybrides connectent à une application Windows Azure, telles que les applications Web ou des applications mobiles dans Azure App Service, la ressource locale tooan qui utilise un port TCP statique, tels que SQL Server, MySQL, API Web de HTTP et plus les Services Web personnalisés.</span><span class="sxs-lookup"><span data-stu-id="13181-320">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, tooan on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="13181-321">Connexions hybrides sont gérées dans les Services BizTalk Bonjour portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="13181-321">Hybrid Connections are managed in  BizTalk Services in hello Azure classic portal.</span></span>

<span data-ttu-id="13181-322">toocreate connexions hybrides dans Azure App Service, consultez [accès aux ressources locales à l’aide de connexions hybrides dans Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="13181-322">toocreate Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="13181-323">toocreate ou gérer des connexions hybrides dans Azure BizTalk Services, consultez [connexions hybrides](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="13181-323">toocreate or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="13181-324">Suivant</span><span class="sxs-lookup"><span data-stu-id="13181-324">Next</span></span>
<span data-ttu-id="13181-325">Maintenant que vous êtes familiarisé avec les différents onglets de hello, vous pouvez en savoir plus sur les fonctionnalités des Services BizTalk Azure hello :</span><span class="sxs-lookup"><span data-stu-id="13181-325">Now that you're familiar with hello different tabs, you can learn more about hello Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="13181-326">Limitation dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="13181-326">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="13181-327">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="13181-327">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="13181-328">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="13181-328">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="13181-329">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="13181-329">See Also</span></span>
* [<span data-ttu-id="13181-330">Connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="13181-330">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="13181-331">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="13181-331">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="13181-332">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="13181-332">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="13181-333">BizTalk Services : tableau comparatif des états du service BizTalk</span><span class="sxs-lookup"><span data-stu-id="13181-333">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="13181-334">Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure</span><span class="sxs-lookup"><span data-stu-id="13181-334">How do I Start Using hello Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

