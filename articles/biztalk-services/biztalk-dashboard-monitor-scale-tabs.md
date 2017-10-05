---
title: "Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexions hybrides dans BizTalk Services | Microsoft Docs"
description: "Découvrez les commandes et surveillez les performances sous les onglets du portail Azure Classic de BizTalk Services : Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexions hybrides. MABS, WABS"
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
ms.openlocfilehash: 4ec88d9a681a5692b31f7e3990d1c153296b18ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="review-the-dashboard-monitor-scale-configure-and-hybrid-connection-tabs"></a><span data-ttu-id="080dd-104">Passer en revue les onglets Tableau de bord, Surveiller, Mettre à l’échelle, Configurer et Connexion hybride</span><span class="sxs-lookup"><span data-stu-id="080dd-104">Review the Dashboard, Monitor, Scale, Configure, and Hybrid Connection tabs</span></span>

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

<span data-ttu-id="080dd-105">Après avoir créé votre service BizTalk et déployé votre application, vous pouvez modifier certains paramètres du service BizTalk et surveiller les performances de l'application.</span><span class="sxs-lookup"><span data-stu-id="080dd-105">After you create your BizTalk Service and deploy your application, you can change some of the BizTalk Service settings and monitor the application performance.</span></span> 

<span data-ttu-id="080dd-106">La première fois que vous ouvrez le portail Azure Classic, l’onglet **TOUS LES ÉLÉMENTS** s’affiche automatiquement.</span><span class="sxs-lookup"><span data-stu-id="080dd-106">When you open the Azure classic portal, you are automatically placed at the **ALL ITEMS** tab.</span></span> <span data-ttu-id="080dd-107">Pour afficher votre service BizTalk, sélectionnez-le sous l’onglet **Tous les éléments**. Vous pouvez aussi sélectionner l’onglet **BIZTALK SERVICES**, puis le nom de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-107">To view your BizTalk Service, select your BizTalk Service in the **ALL ITEMS** tab or select the **BIZTALK SERVICES** tab; and then select your BizTalk Service name.</span></span>

<span data-ttu-id="080dd-108">Une nouvelle fenêtre apparaît avec les onglets suivants :</span><span class="sxs-lookup"><span data-stu-id="080dd-108">This opens a new window with the following tabs.</span></span> <span data-ttu-id="080dd-109">Cette rubrique décrit ces onglets.</span><span class="sxs-lookup"><span data-stu-id="080dd-109">This topic describes these tabs.</span></span>

## <a name="quickstart-quickstartquickstart"></a><span data-ttu-id="080dd-110">Démarrage rapide (</span><span class="sxs-lookup"><span data-stu-id="080dd-110">Quickstart (</span></span>![Démarrage rapide][Quickstart]<span data-ttu-id="080dd-112">)</span><span class="sxs-lookup"><span data-stu-id="080dd-112">)</span></span>
<span data-ttu-id="080dd-113">Selon l'édition de BizTalk Services, toutes les options énumérées peuvent ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="080dd-113">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<table border="1">
    <tr>
        <td><span data-ttu-id="080dd-114"><strong>Obtention des outils</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-114"><strong>Get the tools</strong></span></span></td>
        <td><span data-ttu-id="080dd-115">Téléchargez le Kit SDK de BizTalk Services pour installer les modèles de projet Visual Studio sur votre ordinateur de développement local.</span><span class="sxs-lookup"><span data-stu-id="080dd-115">Download the BizTalk Services SDK to install the Visual Studio project templates on your on-premises development computer.</span></span> <span data-ttu-id="080dd-116">Ces modèles créent les projets Visual Studio <strong>BizTalk Services</strong> (pont) et <strong>Artefacts de service BizTalk</strong> (Transformation) qui sont déployés sur votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-116">These templates create the <strong>BizTalk Services</strong> (bridge) and the <strong>BizTalk Service Artifacts</strong> (Transform) Visual Studio projects that are deployed to your BizTalk Service.</span></span>
        <br/><br/><span data-ttu-id="080dd-117">Les rubriques 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335">Utilisation du Kit de développement logiciel (SDK) Azure BizTalk Services</a> et <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installation du Kit de développement logiciel (SDK) Azure BizTalk Services</a> présentent les procédures de prise en main.</span><span class="sxs-lookup"><span data-stu-id="080dd-117">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302335"> How do I Start Using the Azure BizTalk Services SDK </a> and <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=241589">Installing the Azure BizTalk Services SDK</a> lists the steps to get started.</span></span>
        </td>
    </tr>
    <tr>
        <td><span data-ttu-id="080dd-118"><strong>Créer des accords partenaires</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-118"><strong>Create partner agreements</strong></span></span></td>
        <td><span data-ttu-id="080dd-119">Ouvre le portail Azure BizTalk Services hébergé sur Azure, qui vous permet d'ajouter des partenaires et de créer des contrats EDI X12, AS2 et EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="080dd-119">Opens the Azure BizTalk Services Portal hosted on Azure where you add partners and create X12, AS2, and EDIFACT EDI agreements.</span></span>
        <br/><br/><span data-ttu-id="080dd-120">La rubrique 
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration d'EDI, d'AS2 et d'EDIFACT sur le portail BizTalk Services</a> décrit la procédure de prise en main.</span><span class="sxs-lookup"><span data-stu-id="080dd-120">
        <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> lists the steps to get started.</span></span>
        </td>
    </tr>

<tr>
        <td><span data-ttu-id="080dd-121"><strong>En savoir plus sur les services BizTalk</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-121"><strong>Learn more about BizTalk Services</strong></span></span></td>
        <td><span data-ttu-id="080dd-122">Pour en savoir plus sur les services BizTalk d’Azure, accédez à l’<a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">Espace formations</a>.</span><span class="sxs-lookup"><span data-stu-id="080dd-122">Go to the <a HREF="http://azure.microsoft.com/documentation/services/biztalk-services/">learning center</a> to learn more about Azure BizTalk Services.</span></span></td>
</tr>
</table>


<span data-ttu-id="080dd-123">Dans la barre des tâches située en bas, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="080dd-123">In the task bar at the bottom, you can:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="080dd-124"><strong>Gérer</strong> le déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="080dd-124"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="080dd-125">Ouvre le portail Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="080dd-125">Opens the Azure BizTalk Services portal.</span></span> <span data-ttu-id="080dd-126">Celui-ci représente l'accès à la configuration de l'échange de données informatisé (EDI, Electronic Data Interchange), y compris en ce qui concerne l'ajout de partenaires et la création de contrats X12, AS2 et EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="080dd-126">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="080dd-127">Cela revient à utiliser <strong>Créer des accords partenaires</strong> sous l’onglet <strong>Démarrage rapide</strong>.</span><span class="sxs-lookup"><span data-stu-id="080dd-127">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="080dd-128">La rubrique 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration de composants pour la messagerie EDI sur le portail BizTalk Services</a> fournit des informations supplémentaires sur le portail BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="080dd-128">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="080dd-129"><strong>Informations de connexion</strong> de l’espace de noms Access Control</span><span class="sxs-lookup"><span data-stu-id="080dd-129"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="080dd-130">Lorsque vous sélectionnez Informations de connexion, l'espace de noms Access Control, l'émetteur par défaut et la clé par défaut s'affichent.</span><span class="sxs-lookup"><span data-stu-id="080dd-130">When you select Connection Information, then the Access Control Namespace, Default Issuer, and Default Key are displayed.</span></span> <span data-ttu-id="080dd-131">Vous pouvez copier ces valeurs.</span><span class="sxs-lookup"><span data-stu-id="080dd-131">You can copy these values.</span></span>
<br/><br/>
<span data-ttu-id="080dd-132">Vous pouvez également ouvrir le portail Access Control.</span><span class="sxs-lookup"><span data-stu-id="080dd-132">You can also open the Access Control Portal.</span></span> <span data-ttu-id="080dd-133">La rubrique <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Créer un espace de noms Access Control</a> fournit des informations supplémentaires sur le portail Access Control.</span><span class="sxs-lookup"><span data-stu-id="080dd-133"><a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Create an Access control Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="080dd-134"><strong>Synchroniser les clés</strong> dans le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="080dd-134"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="080dd-135">Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="080dd-135">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="080dd-136">Ces clés de chiffrement contrôlent l'accès à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="080dd-136">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="080dd-137">Votre service BizTalk utilise automatiquement la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-137">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="080dd-138">Les <strong>Clés de synchronisation</strong> permettent aux utilisateurs de basculer entre la clé primaire et la clé secondaire sans interrompre le service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-138"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="080dd-139">Supposons que vous vouliez que le service BizTalk utilise une nouvelle clé primaire pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="080dd-139">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="080dd-140">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="080dd-140">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="080dd-141">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="080dd-141">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="080dd-142">Sélectionnez la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-142">Select the Secondary Key.</span></span> <span data-ttu-id="080dd-143">Une fois que c'est fait, le service BizTalk commence à utiliser la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-143">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="080dd-144">Dans le portail Azure Classic, sélectionnez votre compte de stockage et régénérez la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-144">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="080dd-145">Rappelez-vous que votre service BizTalk utilise la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-145">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="080dd-146">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="080dd-146">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="080dd-147">À présent, sélectionnez la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-147">Now, select the Primary Key.</span></span> <span data-ttu-id="080dd-148">Il s'agit de la nouvelle clé primaire que vous avez régénérée.</span><span class="sxs-lookup"><span data-stu-id="080dd-148">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="080dd-149">Dans le portail Azure Classic, sélectionnez votre compte de stockage et régénérez la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-149">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="080dd-150">On parle de « clés de substitution » pour décrire ce processus.</span><span class="sxs-lookup"><span data-stu-id="080dd-150">This process is called "rollover keys".</span></span> <span data-ttu-id="080dd-151">L'objectif est de permettre aux utilisateurs de basculer entre la clé primaire et la clé secondaire sans interrompre le service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-151">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="080dd-152"><strong>Supprimer</strong> votre application</span><span class="sxs-lookup"><span data-stu-id="080dd-152"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="080dd-153">Lorsque vous sélectionnez Supprimer, votre service BizTalk et tous les éléments qui y ont été déployés sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="080dd-153">When you select Delete, your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="dashboard"></a><span data-ttu-id="080dd-154">Tableau de bord</span><span class="sxs-lookup"><span data-stu-id="080dd-154">Dashboard</span></span>
<span data-ttu-id="080dd-155">Selon l'édition de BizTalk Services, toutes les options énumérées peuvent ne pas être disponibles.</span><span class="sxs-lookup"><span data-stu-id="080dd-155">Depending on the BizTalk Services Edition, all options listed may not be available.</span></span> 

<span data-ttu-id="080dd-156">Lorsque vous sélectionnez le nom de votre service BizTalk, l'onglet Tableau de bord apparaît.</span><span class="sxs-lookup"><span data-stu-id="080dd-156">When you select your BizTalk Service name, the Dashboard tab is displayed.</span></span> <span data-ttu-id="080dd-157">Dans le tableau de bord, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="080dd-157">In Dashboard, you can:</span></span>

##### <a name="usage-overview-shows-the-number-of-used-hybrid-connections"></a><span data-ttu-id="080dd-158">Vue d’ensemble de l’utilisation : montre le nombre de connexions hybrides utilisées.</span><span class="sxs-lookup"><span data-stu-id="080dd-158">Usage Overview: Shows the number of used Hybrid Connections</span></span>
<span data-ttu-id="080dd-159">Affiche également l'utilisation des données en Go.</span><span class="sxs-lookup"><span data-stu-id="080dd-159">Also displays the data usage in GB.</span></span> 

##### <a name="metric-graph-shows-a-fixed-list-of-performance-metrics"></a><span data-ttu-id="080dd-160">Graphique métrique : illustre une liste fixe de mesures de performances.</span><span class="sxs-lookup"><span data-stu-id="080dd-160">Metric Graph: Shows a fixed list of performance metrics</span></span>
<span data-ttu-id="080dd-161">Ces mesures fournissent des valeurs en temps réel concernant l'intégrité du service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-161">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="080dd-162">Vous pouvez également spécifier les valeurs **Relatives** et **Absolues**, ainsi que l’**Intervalle** de temps des mesures affichées sur le graphique.</span><span class="sxs-lookup"><span data-stu-id="080dd-162">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed in the graph.</span></span> 

<span data-ttu-id="080dd-163">Pour obtenir une description de ces mesures de performances, accédez à la section [Mesures disponibles](#Metrics) de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="080dd-163">For a description of these performance metrics, go to [Available Metrics](#Metrics) in this topic.</span></span>

##### <a name="quick-glance-lists-your-biztalk-service-properties"></a><span data-ttu-id="080dd-164">Aperçu rapide : dresse la liste des propriétés de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-164">Quick Glance: Lists your BizTalk Service properties</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="080dd-165"><strong>Mettre à jour les informations d’identification de la base de données de suivi</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-165"><strong>Update Tracking Database credentials</strong></span></span></td>
<td><span data-ttu-id="080dd-166">Modifie le nom d'utilisateur et le mot de passe utilisés pour se connecter à la base de données de suivi.</span><span class="sxs-lookup"><span data-stu-id="080dd-166">Changes the user name and password used to log into the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-167"><strong>Mettre à jour le certificat SSL</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-167"><strong>Update SSL Certificate</strong></span></span></td>
<td><span data-ttu-id="080dd-168">Permet de mettre à jour le service BizTalk pour utiliser un autre certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="080dd-168">Can update the BizTalk Service to use a different SSL certificate.</span></span> <span data-ttu-id="080dd-169">Un certificat SSL auto-signé est automatiquement créé lorsque vous <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">créez le service BizTalk</a>.</span><span class="sxs-lookup"><span data-stu-id="080dd-169">A self-signed SSL certificate is automatically created when you <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">create the BizTalk Service</a>.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-170"><strong>Télécharger le certificat</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-170"><strong>Download Certificate</strong></span></span></td>
<td><span data-ttu-id="080dd-171">Vous pouvez télécharger le certificat SSL utilisé par votre service BizTalk sur une machine locale.</span><span class="sxs-lookup"><span data-stu-id="080dd-171">You can download the SSL certificate used by your BizTalk Service to a local machine.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-172"><strong>État</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-172"><strong>Status</strong></span></span></td>
<td><span data-ttu-id="080dd-173">Affiche le statut actuel de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-173">Displays the current status of your BizTalk Service.</span></span> <span data-ttu-id="080dd-174">Voir <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">Tableau comparatif des états de BizTalk Services</a>.</span><span class="sxs-lookup"><span data-stu-id="080dd-174">See <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=329870">BizTalk Services: Service state chart</a>.</span></span> </td>
</tr>
<tr>
<td><span data-ttu-id="080dd-175"><strong>URL du service</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-175"><strong>Service URL</strong></span></span></td>
<td><span data-ttu-id="080dd-176">URL de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-176">The URL for your BizTalk Service.</span></span> <span data-ttu-id="080dd-177">Il s’agit de l’<strong>URL de domaine</strong> entrée lors de la création de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-177">This is the same as the <strong>Domain URL</strong> entered when your BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-178"><strong>Adresse IP virtuelle (VIP) publique</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-178"><strong>Public Virtual IP (VIP) Address</strong></span></span></td>
<td><span data-ttu-id="080dd-179">Adresse IP attribuée à votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-179">The IP address assigned to your BizTalk Service.</span></span> <span data-ttu-id="080dd-180">Elle est utilisée pour tous les points de terminaison d’entrée et représente l'adresse source pour le trafic sortant.</span><span class="sxs-lookup"><span data-stu-id="080dd-180">It is used for all input endpoints and is the source address for outbound traffic.</span></span> <span data-ttu-id="080dd-181">L'adresse IP appartient à votre service BizTalk si il est créé.</span><span class="sxs-lookup"><span data-stu-id="080dd-181">This IP address belongs to your BizTalk Service as long as it is created.</span></span> <span data-ttu-id="080dd-182">Si vous supprimez le service BizTalk, l'adresse IP est attribuée à un autre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-182">If you delete the BizTalk Service, the IP address is assigned to another BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-183"><strong>Espace de noms ACS</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-183"><strong>ACS Namespace</strong></span></span></td>
<td><span data-ttu-id="080dd-184">Permet de s'authentifier auprès du service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-184">Authenticates with the BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-185"><strong>Édition</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-185"><strong>Edition</strong></span></span></td>
<td><span data-ttu-id="080dd-186">Répertorie l'édition entrée lorsque le service BizTalk est créé.</span><span class="sxs-lookup"><span data-stu-id="080dd-186">Lists the Edition entered when the BizTalk Service is created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-187"><strong>Emplacement</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-187"><strong>Location</strong></span></span></td>
<td><span data-ttu-id="080dd-188">Affiche la région géographique hébergeant votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-188">Displays the geographic region that hosts your BizTalk Service.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-189"><strong>Créé</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-189"><strong>Created</strong></span></span></td>
<td><span data-ttu-id="080dd-190">Affiche la date et l'heure de la création du service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-190">Displays the date and time the BizTalk Service was created.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-191"><strong>Base de données des suivis</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-191"><strong>Tracking Database</strong></span></span></td>
<td><span data-ttu-id="080dd-192">Nom de la base de données SQL Azure stockant les tables de suivi utilisées par votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-192">The Azure SQL Database name that stores the tracking tables used by your BizTalk Service.</span></span> 
<br/><br/><span data-ttu-id="080dd-193">La rubrique 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Explication des exigences</a> fournit des détails sur la base de données de suivi.</span><span class="sxs-lookup"><span data-stu-id="080dd-193">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Tracking Database.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-194"><strong>Stockage de surveillance/archivage</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-194"><strong>Monitoring/Archiving Storage</strong></span></span></td>
<td><span data-ttu-id="080dd-195">Nom du compte de stockage Azure stockant la sortie de la surveillance de votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-195">The Azure Storage account name that stores the monitoring output of your BizTalk Service.</span></span>
<br/><br/><span data-ttu-id="080dd-196">La rubrique 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Explication des exigences</a> fournit des détails sur le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="080dd-196">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302280">Requirements Explained</a>  provides details on the Storage account.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-197"><strong>Nom d’abonnement</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-197"><strong>Subscription Name</strong></span></span></td>
<td><span data-ttu-id="080dd-198">Répertorie l’abonnement qui héberge votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-198">Lists the subscription that hosts your BizTalk Service.</span></span> <span data-ttu-id="080dd-199">L’abonnement régit l’accès au portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="080dd-199">The subscription governs access to the Azure classic portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-200"><strong>Identifiant d’abonnement</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-200"><strong>Subscription ID</strong></span></span></td>
<td><span data-ttu-id="080dd-201">Lorsqu’un abonnement est créé, un ID d’abonnement est automatiquement généré.</span><span class="sxs-lookup"><span data-stu-id="080dd-201">When a subscription is created, a subscription ID is automatically generated.</span></span> <span data-ttu-id="080dd-202">Lors de l’utilisation d’API REST, il vous faudra peut-être entrer l’ID d’abonnement.</span><span class="sxs-lookup"><span data-stu-id="080dd-202">When using REST APIs, you may need to enter the Subscription ID.</span></span></td>
</tr>
</table>

<span data-ttu-id="080dd-203">[BizTalk Services : approvisionnement à l’aide du portail Azure Classic](http://go.microsoft.com/fwlink/p/?LinkID=302280) indique la procédure de création d’un service BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="080dd-203">[BizTalk Services: Provisioning Using Azure classic portal](http://go.microsoft.com/fwlink/p/?LinkID=302280) lists the steps to create a BizTalk Service.</span></span>

##### <a name="manage-connection-information-sync-keys-and-delete-in-the-task-bar"></a><span data-ttu-id="080dd-204">Gérer, Informations de connexion, Clés de synchronisation et Supprimer dans la barre des tâches :</span><span class="sxs-lookup"><span data-stu-id="080dd-204">Manage, Connection Information, Sync Keys, and Delete in the task bar:</span></span>
<table border="1">

<tr>
<td><span data-ttu-id="080dd-205"><strong>Gérer</strong> le déploiement de votre application</span><span class="sxs-lookup"><span data-stu-id="080dd-205"><strong>Manage</strong> your application deployment</span></span></td>
<td><span data-ttu-id="080dd-206">Ouvre le portail Azure BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="080dd-206">Opens the Azure BizTalk Services Portal.</span></span> <span data-ttu-id="080dd-207">Celui-ci représente l'accès à la configuration de l'échange de données informatisé (EDI, Electronic Data Interchange), y compris en ce qui concerne l'ajout de partenaires et la création de contrats X12, AS2 et EDIFACT.</span><span class="sxs-lookup"><span data-stu-id="080dd-207">The BizTalk Services Portal is the entrance to EDI configuration, including adding partners and creating X12, AS2, and EDIFACT agreements.</span></span>
<br/><br/>
<span data-ttu-id="080dd-208">Cela revient à utiliser <strong>Créer des accords partenaires</strong> sous l’onglet <strong>Démarrage rapide</strong>.</span><span class="sxs-lookup"><span data-stu-id="080dd-208">This is the same as <strong>Create partner agreements</strong> on the <strong>Quick Start</strong> tab.</span></span>
<br/><br/><span data-ttu-id="080dd-209">La rubrique 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuration de composants pour la messagerie EDI sur le portail BizTalk Services</a> fournit des informations supplémentaires sur le portail BizTalk Services.</span><span class="sxs-lookup"><span data-stu-id="080dd-209">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=303653">Configuring Components for EDI Messaging on BizTalk Services Portal</a> provides more information on the BizTalk Services Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-210"><strong>Informations de connexion</strong> de l’espace de noms Access Control</span><span class="sxs-lookup"><span data-stu-id="080dd-210"><strong>Connection Information</strong> of the Access Control Namespace</span></span></td>
<td><span data-ttu-id="080dd-211">Affiche l'espace de noms Access Control, l'émetteur par défaut et les valeurs de clé par défaut qui peuvent être copiés.</span><span class="sxs-lookup"><span data-stu-id="080dd-211">Displays the Access Control Namespace, Default Issuer, and Default Key values; which can be copied.</span></span>
<br/><br/>
<span data-ttu-id="080dd-212">Vous pouvez également ouvrir le portail Access Control.</span><span class="sxs-lookup"><span data-stu-id="080dd-212">You can also open the Access Control Portal.</span></span> <span data-ttu-id="080dd-213">Utiliser ce portail équivaut à utiliser l’option Active Directory dans le volet de navigation de gauche.</span><span class="sxs-lookup"><span data-stu-id="080dd-213">This Access Control Portal is the same as using the Active Directory option in the left navigation pane.</span></span>
<br/><br/><span data-ttu-id="080dd-214">La rubrique 
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Créer un espace de noms Access Control</a> fournit des informations supplémentaires sur le portail Access Control.</span><span class="sxs-lookup"><span data-stu-id="080dd-214">
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285670">Managing Your ACS Namespace</a> provides more information on the Access Control Portal.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-215"><strong>Synchroniser les clés</strong> dans le compte de stockage</span><span class="sxs-lookup"><span data-stu-id="080dd-215"><strong>Sync Keys</strong> in the Storage Account</span></span></td>
<td><span data-ttu-id="080dd-216">Lorsque vous créez un compte de stockage, une clé primaire et une clé secondaire sont automatiquement créées.</span><span class="sxs-lookup"><span data-stu-id="080dd-216">When you create a Storage account, a Primary Key and Secondary Key are automatically created.</span></span> <span data-ttu-id="080dd-217">Ces clés de chiffrement contrôlent l'accès à votre compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="080dd-217">These encryption Keys control access to your Storage Account.</span></span> <span data-ttu-id="080dd-218">Votre service BizTalk utilise automatiquement la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-218">Your BizTalk Service automatically uses the Primary Key.</span></span> <span data-ttu-id="080dd-219">Les <strong>Clés de synchronisation</strong> permettent aux utilisateurs de basculer entre la clé primaire et la clé secondaire sans interrompre le service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-219"><strong>Sync Keys</strong> enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span>
<br/><br/>
<span data-ttu-id="080dd-220">Supposons que vous vouliez que le service BizTalk utilise une nouvelle clé primaire pour le compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="080dd-220">For example, you want the BizTalk Service to use a new Primary Key for the Storage Account.</span></span> <span data-ttu-id="080dd-221">Pour ce faire :</span><span class="sxs-lookup"><span data-stu-id="080dd-221">To do this:</span></span>
<br/><br/>
<ol>
<li><span data-ttu-id="080dd-222">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="080dd-222">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="080dd-223">Sélectionnez la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-223">Select the Secondary Key.</span></span> <span data-ttu-id="080dd-224">Une fois que c'est fait, le service BizTalk commence à utiliser la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-224">When you do this, the BizTalk Service starts using the Secondary Key.</span></span></li>
<li><span data-ttu-id="080dd-225">Dans le portail Azure Classic, sélectionnez votre compte de stockage et régénérez la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-225">In the Azure classic portal, select your Storage account and Regenerate the Primary Key.</span></span> <span data-ttu-id="080dd-226">Rappelez-vous que votre service BizTalk utilise la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-226">Remember, your BizTalk Service is using the Secondary Key.</span></span></li>
<li><span data-ttu-id="080dd-227">Sélectionnez votre service BizTalk, puis <strong>Clés de synchronisation</strong>.</span><span class="sxs-lookup"><span data-stu-id="080dd-227">Select your BizTalk Service and select <strong>Sync Keys</strong>.</span></span> <span data-ttu-id="080dd-228">À présent, sélectionnez la clé primaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-228">Now, select the Primary Key.</span></span> <span data-ttu-id="080dd-229">Il s'agit de la nouvelle clé primaire que vous avez régénérée.</span><span class="sxs-lookup"><span data-stu-id="080dd-229">This is the new Primary Key you regenerated.</span></span></li>
<li><span data-ttu-id="080dd-230">Dans le portail Azure Classic, sélectionnez votre compte de stockage et régénérez la clé secondaire.</span><span class="sxs-lookup"><span data-stu-id="080dd-230">In the Azure classic portal, select your Storage account and Regenerate the Secondary Key.</span></span></li>
</ol>
<br/>
<span data-ttu-id="080dd-231">On parle de « clés de substitution » pour décrire ce processus.</span><span class="sxs-lookup"><span data-stu-id="080dd-231">This process is called "rollover keys".</span></span> <span data-ttu-id="080dd-232">L'objectif est de permettre aux utilisateurs de basculer entre la clé primaire et la clé secondaire sans interrompre le service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-232">The purpose is to enable users to switch between the Primary Key and the Secondary Key without disrupting the BizTalk Service.</span></span></td>
</tr>

<tr>
<td><span data-ttu-id="080dd-233"><strong>Supprimer</strong> votre application</span><span class="sxs-lookup"><span data-stu-id="080dd-233"><strong>Delete</strong> your application</span></span></td>
<td><span data-ttu-id="080dd-234">Votre service BizTalk et tous les éléments qui y ont été déployés sont supprimés.</span><span class="sxs-lookup"><span data-stu-id="080dd-234">Your BizTalk Service and all items deployed to it are removed.</span></span></td>
</tr>
</table>


## <a name="monitor"></a><span data-ttu-id="080dd-235">Surveiller</span><span class="sxs-lookup"><span data-stu-id="080dd-235">Monitor</span></span>
<span data-ttu-id="080dd-236">Ne s'applique pas à l'édition gratuite.</span><span class="sxs-lookup"><span data-stu-id="080dd-236">Does not apply to the Free Edition.</span></span>

<span data-ttu-id="080dd-237">Lorsque vous sélectionnez le nom de votre service BizTalk, l'onglet Surveiller est disponible et affiche les éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="080dd-237">When you select your BizTalk Service name, the Monitor tab is available and displays the following:</span></span>

##### <a name="metric-graph-displays-the-selected-performance-metrics"></a><span data-ttu-id="080dd-238">Graphique métrique : affiche les mesures de performances sélectionnées.</span><span class="sxs-lookup"><span data-stu-id="080dd-238">Metric Graph: Displays the selected performance metrics</span></span>
<span data-ttu-id="080dd-239">Ces mesures fournissent des valeurs en temps réel concernant l'intégrité du service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-239">These metrics provide real-time values regarding the health of the BizTalk Service.</span></span> <span data-ttu-id="080dd-240">Vous choisissez les mesures de performances devant s'afficher</span><span class="sxs-lookup"><span data-stu-id="080dd-240">You choose which performance metrics are displayed.</span></span> <span data-ttu-id="080dd-241">(jusqu'à six mesures de performances simultanément).</span><span class="sxs-lookup"><span data-stu-id="080dd-241">A maximum of six performance metrics can be displayed simultaneously.</span></span> 

<span data-ttu-id="080dd-242">Vous pouvez également spécifier les valeurs **Relatives** et **Absolues**, ainsi que l’**Intervalle** de temps des mesures affichées.</span><span class="sxs-lookup"><span data-stu-id="080dd-242">You can also choose the **Relative** or **Absolute** values and the time range **Interval** of the metrics that are displayed.</span></span> 

##### <a name="to-remove-or-display-metrics-in-the-graph"></a><span data-ttu-id="080dd-243">Pour supprimer ou afficher des mesures dans le graphique :</span><span class="sxs-lookup"><span data-stu-id="080dd-243">To remove or display metrics in the graph:</span></span>
1. <span data-ttu-id="080dd-244">Sélectionnez l'onglet **Surveiller** .</span><span class="sxs-lookup"><span data-stu-id="080dd-244">Select the **Monitor** tab.</span></span>
2. <span data-ttu-id="080dd-245">Sélectionnez **Ajouter des métriques** dans la barre des tâches :</span><span class="sxs-lookup"><span data-stu-id="080dd-245">Select **Add Metrics** in the task bar:</span></span>  
   <span data-ttu-id="080dd-246">![Sélectionnez Ajouter des métriques.][AddMetrics]</span><span class="sxs-lookup"><span data-stu-id="080dd-246">![Select Add Metrics][AddMetrics]</span></span>
3. <span data-ttu-id="080dd-247">Vérifiez les mesures de performances que vous souhaitez afficher.</span><span class="sxs-lookup"><span data-stu-id="080dd-247">Check the performance metrics you want to display.</span></span>
4. <span data-ttu-id="080dd-248">Sélectionnez la coche pour revenir à l'onglet **Surveiller** .</span><span class="sxs-lookup"><span data-stu-id="080dd-248">Select the checkmark to return to the **Monitor** tab.</span></span>
5. <span data-ttu-id="080dd-249">Sélectionnez le cercle en regard de la mesure pour afficher la valeur associée dans le graphique.</span><span class="sxs-lookup"><span data-stu-id="080dd-249">Select the circle next to the metric to display that metric's value in the graph.</span></span>  
   
    <span data-ttu-id="080dd-250">Par exemple, la mesure **Utilisation du processeur** apparaît en grisé et son résultat n’apparaît pas dans le graphique :</span><span class="sxs-lookup"><span data-stu-id="080dd-250">For example, the **CPU Usage** metric is grayed out; its output is not displayed in the graph:</span></span>  
   <span data-ttu-id="080dd-251">![La mesure Utilisation du processeur apparaît en grisé][GrayedMetric]</span><span class="sxs-lookup"><span data-stu-id="080dd-251">![CPU Usage metric is grayed out][GrayedMetric]</span></span>  
   
    <span data-ttu-id="080dd-252">Sélectionnez le cercle grisé pour activer la mesure **Utilisation du processeur** et afficher son résultat dans le graphique :</span><span class="sxs-lookup"><span data-stu-id="080dd-252">Select the grayed out circle to enable the **CPU Usage** metric to display its output in the graph:</span></span>  
   <span data-ttu-id="080dd-253">![La mesure Utilisation du processeur est activée][EnabledMetric]</span><span class="sxs-lookup"><span data-stu-id="080dd-253">![CPU Usage metric is enabled][EnabledMetric]</span></span>
6. <span data-ttu-id="080dd-254">Pour supprimer une mesure du graphique affiché et de la liste, sélectionnez **Supprimer une métrique** dans la barre des tâches.</span><span class="sxs-lookup"><span data-stu-id="080dd-254">To remove a metric from the display graph and the list, select **Delete Metric** in the task bar.</span></span> <span data-ttu-id="080dd-255">Pour réintégrer la mesure dans la liste, sélectionnez **Ajouter des métriques** dans la barre des tâches, vérifiez la mesure, puis cochez la case pour revenir à l’onglet **Surveiller**.</span><span class="sxs-lookup"><span data-stu-id="080dd-255">To add the metric back to the list, select **Add Metrics** in the task bar, check the metric, and select the checkmark to return to the **Monitor** tab.</span></span> <span data-ttu-id="080dd-256">Sélectionnez le cercle en grisé pour activer la mesure.</span><span class="sxs-lookup"><span data-stu-id="080dd-256">Select the grayed out circle to enable the metric.</span></span>

## <span data-ttu-id="080dd-257"><a name="Metrics"></a>Mesures disponibles</span><span class="sxs-lookup"><span data-stu-id="080dd-257"><a name="Metrics"></a>Available Metrics</span></span>
<span data-ttu-id="080dd-258">Les mesures/compteurs de performances suivants sont disponibles :</span><span class="sxs-lookup"><span data-stu-id="080dd-258">The following performance counters/metrics are available:</span></span>

<table border="1">

<tr>
<td><span data-ttu-id="080dd-259"><strong>Latence aller-retour</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-259"><strong>RountdTrip Latency</strong></span></span></td>
<td><span data-ttu-id="080dd-260">Affiche le temps moyen en millisecondes (ms) nécessaire au traitement d'un message depuis sa réception jusqu'à son traitement complet par le service BizTalk sur tous les ponts.</span><span class="sxs-lookup"><span data-stu-id="080dd-260">Displays the average time taken in milliseconds (ms) to process a message from the time the message is received until the message is fully processed by the BizTalk Service across all bridges.</span></span> <span data-ttu-id="080dd-261">Seuls les messages correctement traités sont comptabilisés.</span><span class="sxs-lookup"><span data-stu-id="080dd-261">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="080dd-262">Lorsque les événements suivants se produisent, un horodatage est créé :</span><span class="sxs-lookup"><span data-stu-id="080dd-262">When the following events occur, a timestamp is created:</span></span>
<ul>
<li><span data-ttu-id="080dd-263">Le message accède à la passerelle</span><span class="sxs-lookup"><span data-stu-id="080dd-263">Message enters the gateway</span></span></li>
<li><span data-ttu-id="080dd-264">Le message est acheminé vers la destination</span><span class="sxs-lookup"><span data-stu-id="080dd-264">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="080dd-265">Une réponse de la destination est reçue</span><span class="sxs-lookup"><span data-stu-id="080dd-265">Destination response is received</span></span></li>
<li><span data-ttu-id="080dd-266">Un accusé de réception est envoyé à la passerelle par la destination</span><span class="sxs-lookup"><span data-stu-id="080dd-266">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/>
<span data-ttu-id="080dd-267">Cette mesure affiche le résultat du calcul suivant :</span><span class="sxs-lookup"><span data-stu-id="080dd-267">This metric shows the result of the following calculation:</span></span>
<br/><br/>
<span data-ttu-id="080dd-268">[Accusé de réception envoyé à la passerelle par la destination] - [Le message accède à la passerelle]</span><span class="sxs-lookup"><span data-stu-id="080dd-268">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-269"><strong>Défaillances à la source</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-269"><strong>Failures At Source</strong></span></span></td>
<td><span data-ttu-id="080dd-270">Affiche le nombre total de messages n'ayant pas pu être traités par le service BizTalk lors de l'extraction de messages à partir des points de terminaison sources.</span><span class="sxs-lookup"><span data-stu-id="080dd-270">Displays the total number of messages that failed by the BizTalk Service when pulling messages from the source endpoints.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-271"><strong>Utilisation du processeur</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-271"><strong>CPU Usage</strong></span></span></td>
<td><span data-ttu-id="080dd-272">Indique le pourcentage de temps processeur de toutes les instances de rôle.</span><span class="sxs-lookup"><span data-stu-id="080dd-272">Lists the average %Processor Time of all role instances.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-273"><strong>Latence de traitement</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-273"><strong>Processing Latency</strong></span></span></td>
<td><span data-ttu-id="080dd-274">Affiche le délai moyen en millisecondes (ms) requis pour le traitement d'un message par le service BizTalk sur tous les ponts, à l'exclusion du temps passé au niveau des destinations.</span><span class="sxs-lookup"><span data-stu-id="080dd-274">Displays the average time taken In milliseconds (ms) to process a message by the BizTalk Service across all bridges, excluding the time spent in destinations.</span></span> <span data-ttu-id="080dd-275">Seuls les messages correctement traités sont comptabilisés.</span><span class="sxs-lookup"><span data-stu-id="080dd-275">Only messages successfully processed are counted.</span></span><br/><br/>
<span data-ttu-id="080dd-276">Lorsque l'un des événements suivants se produit, un horodatage est créé :</span><span class="sxs-lookup"><span data-stu-id="080dd-276">When each of the following events occur, a timestamp is created:</span></span>

<ul>
<li><span data-ttu-id="080dd-277">Le message accède à la passerelle</span><span class="sxs-lookup"><span data-stu-id="080dd-277">Message enters the gateway</span></span></li>
<li><span data-ttu-id="080dd-278">Le message est acheminé vers la destination</span><span class="sxs-lookup"><span data-stu-id="080dd-278">Message is routed to the destination</span></span></li>
<li><span data-ttu-id="080dd-279">Une réponse de la destination est reçue</span><span class="sxs-lookup"><span data-stu-id="080dd-279">Destination response is received</span></span></li>
<li><span data-ttu-id="080dd-280">Un accusé de réception est envoyé à la passerelle par la destination</span><span class="sxs-lookup"><span data-stu-id="080dd-280">Destination acknowledgement response sent to the gateway</span></span></li>
</ul>
<br/><span data-ttu-id="080dd-281">Cette mesure affiche le résultat du calcul suivant :</span><span class="sxs-lookup"><span data-stu-id="080dd-281">This metric shows the result of the following calculation:</span></span><br/><br/>
<span data-ttu-id="080dd-282">[Un accusé de réception est envoyé à la passerelle par la destination] - [Le message accède à la passerelle] - [Une réponse de la destination est reçue] + [Le message est acheminé vers la destination]</span><span class="sxs-lookup"><span data-stu-id="080dd-282">[Destination acknowledgement response sent to the gateway] - [Message enters the gateway] - [Destination response is received] + [Message is routed to the destination]</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-283"><strong>Défaillances dans le processus</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-283"><strong>Failures In Process</strong></span></span></td>
<td><span data-ttu-id="080dd-284">Affiche le nombre total de messages ayant échoué pendant le traitement par le service BizTalk sur tous les ponts pendant un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="080dd-284">Displays the total number of messages that failed during processing by the BizTalk Service across all the bridges within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-285"><strong>Messages envoyés</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-285"><strong>Messages Sent</strong></span></span></td>
<td><span data-ttu-id="080dd-286">Affiche le nombre total de messages envoyés par le service BizTalk sur tous les ponts pendant un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="080dd-286">Displays the total number of messages sent by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="080dd-287">Cette mesure est incrémentée lorsqu'un message envoyé à partir d'un pipeline atteint la destination d'itinéraire.</span><span class="sxs-lookup"><span data-stu-id="080dd-287">This metric is incremented when a message sent from a pipeline reaches the route destination.</span></span> <span data-ttu-id="080dd-288">Cette mesure n'indique pas qu'un message a été traité correctement.</span><span class="sxs-lookup"><span data-stu-id="080dd-288">This metric does not indicate that a message is successfully processed.</span></span><br/><br/>
<span data-ttu-id="080dd-289">Dans un scénario de réponse à la demande, la mesure est incrémentée lorsque la destination d'itinéraire renvoie un accusé de réception au pipeline.</span><span class="sxs-lookup"><span data-stu-id="080dd-289">In a Request-Reply scenario, the metric is incremented when the route destination sends a receipt acknowledgement back to the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-290"><strong>Messages reçus</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-290"><strong>Messages Received</strong></span></span></td>
<td><span data-ttu-id="080dd-291">Affiche le nombre total de messages reçus par le service BizTalk sur tous les ponts pendant un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="080dd-291">Displays the total number of messages received by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="080dd-292">Cette mesure est incrémentée lorsqu'un nouveau message est reçu par le pipeline.</span><span class="sxs-lookup"><span data-stu-id="080dd-292">This metric is incremented when a new message is received by the pipeline.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-293"><strong>Messages en cours de traitement</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-293"><strong>Messages In Process</strong></span></span></td>
<td><span data-ttu-id="080dd-294">Affiche le nombre total de messages en cours de traitement par le service BizTalk pendant un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="080dd-294">Displays the total number of messages currently being processed by the BizTalk Service within a time interval.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="080dd-295"><strong>Messages traités</strong></span><span class="sxs-lookup"><span data-stu-id="080dd-295"><strong>Messages Processed</strong></span></span></td>
<td><span data-ttu-id="080dd-296">Affiche le nombre total de messages correctement traités par le service BizTalk sur tous les ponts pendant un intervalle de temps.</span><span class="sxs-lookup"><span data-stu-id="080dd-296">Displays the total number of messages successfully processed by the BizTalk Service across all bridges within a time interval.</span></span> <span data-ttu-id="080dd-297">Cette mesure est incrémentée lorsqu'un message est correctement reçu par le pipeline et acheminé vers la destination.</span><span class="sxs-lookup"><span data-stu-id="080dd-297">This metric is incremented when a message is successfully received by the pipeline and successfully routed to the destination.</span></span></td>
</tr>
</table>


## <a name="scale"></a><span data-ttu-id="080dd-298">Mettre à l'échelle</span><span class="sxs-lookup"><span data-stu-id="080dd-298">Scale</span></span>
<span data-ttu-id="080dd-299">Dans l'onglet Mettre à l'échelle, vous pouvez ajouter ou soustraire le nombre d'unités utilisées par votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-299">In the Scale tab, you can add or subtract the number of units used by your BizTalk Service.</span></span> <span data-ttu-id="080dd-300">Par défaut, une seule unité est configurée.</span><span class="sxs-lookup"><span data-stu-id="080dd-300">By default, there is one Unit configured.</span></span> <span data-ttu-id="080dd-301">Vous pouvez ajouter des unités supplémentaires afin de mettre à l'échelle votre service BizTalk.</span><span class="sxs-lookup"><span data-stu-id="080dd-301">Additional Units can be added to scale your BizTalk Service.</span></span> <span data-ttu-id="080dd-302">Lorsque vous augmentez la mise à l'échelle, vous augmentez le débit.</span><span class="sxs-lookup"><span data-stu-id="080dd-302">When you increase the scale, you are increasing throughput.</span></span> <span data-ttu-id="080dd-303">La quantité de ressources augmente également, y compris les ponts déployés, les contrats, les connexions métier et la puissance de traitement.</span><span class="sxs-lookup"><span data-stu-id="080dd-303">The amount of resources also increases, including deployed bridges, agreements, LOB connections, and processing power.</span></span> <span data-ttu-id="080dd-304">Par exemple, vous augmentez la mise à l'échelle de 1 à 2 unités.</span><span class="sxs-lookup"><span data-stu-id="080dd-304">For example, you increase the scale from 1 Unit to 2 Units.</span></span> <span data-ttu-id="080dd-305">Dans ce cas, vous pouvez doubler le nombre de ponts, les contrats, les connexions métier et la puissance de traitement.</span><span class="sxs-lookup"><span data-stu-id="080dd-305">In this situation, you can deploy double the number of bridges, double the agreements, double the LOB connections, and double the processing power.</span></span>

<span data-ttu-id="080dd-306">Certaines éditions BizTalk n'offrent pas de possibilité de mise à l'échelle.</span><span class="sxs-lookup"><span data-stu-id="080dd-306">Some BizTalk editions do not offer a scale option.</span></span> <span data-ttu-id="080dd-307">Dans ce cas, une seule unité est autorisée.</span><span class="sxs-lookup"><span data-stu-id="080dd-307">In this situation, one Unit is permitted.</span></span> <span data-ttu-id="080dd-308">Pour déterminer le nombre d'unités auquel votre édition peut être mise à l'échelle, consultez le [Tableau comparatif des éditions de BizTalk Services](biztalk-editions-feature-chart.md).</span><span class="sxs-lookup"><span data-stu-id="080dd-308">To determine how many units your edition can be scaled, refer to [BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md).</span></span>

<span data-ttu-id="080dd-309">L'augmentation du nombre d'unités peut avoir un impact sur les tarifs.</span><span class="sxs-lookup"><span data-stu-id="080dd-309">Increasing the number of units may impact pricing.</span></span> <span data-ttu-id="080dd-310">Si vous augmentez les unités, sélectionnez **Enregistrer** pour afficher un message indiquant s'il y a un impact sur la facturation.</span><span class="sxs-lookup"><span data-stu-id="080dd-310">If you increase the Units, selecting **Save** displays a message that tells you if billing is impacted.</span></span> <span data-ttu-id="080dd-311">Vous choisissez ensuite de continuer.</span><span class="sxs-lookup"><span data-stu-id="080dd-311">You then choose to continue.</span></span> <span data-ttu-id="080dd-312">Lorsque vous augmentez le nombre d'unités, le statut du service BizTalk passe d'Actif à Mis à jour.</span><span class="sxs-lookup"><span data-stu-id="080dd-312">When you increase the number of Units, the BizTalk Service status changes from Active to Updating.</span></span> <span data-ttu-id="080dd-313">En état de mise à jour, votre service BizTalk continue de s'exécuter.</span><span class="sxs-lookup"><span data-stu-id="080dd-313">In the Updating state, your BizTalk Service continues to run.</span></span>

<span data-ttu-id="080dd-314">[Tableau comparatif des éditions de BizTalk Services](biztalk-editions-feature-chart.md) définit une « unité ».</span><span class="sxs-lookup"><span data-stu-id="080dd-314">[BizTalk Services: Editions Chart](biztalk-editions-feature-chart.md) defines a "Unit".</span></span>

## <a name="configure"></a><span data-ttu-id="080dd-315">Configuration</span><span class="sxs-lookup"><span data-stu-id="080dd-315">Configure</span></span>
<span data-ttu-id="080dd-316">Ne s'applique pas aux connexions hybrides.</span><span class="sxs-lookup"><span data-stu-id="080dd-316">Does not apply to Hybrid Connections.</span></span>

<span data-ttu-id="080dd-317">Définit l'état de la sauvegarde sur Aucun ou Automatique.</span><span class="sxs-lookup"><span data-stu-id="080dd-317">Sets the Backup Status to None or Automatic.</span></span> <span data-ttu-id="080dd-318">Lorsqu'il est défini sur Aucun, aucune sauvegarde n'est automatiquement créée.</span><span class="sxs-lookup"><span data-stu-id="080dd-318">When set to None, no backups are automatically created.</span></span> <span data-ttu-id="080dd-319">Lorsqu'il est défini sur Automatique, vous configurez l'emplacement de la sauvegarde, la fréquence de la sauvegarde et la durée de conservation des fichiers de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="080dd-319">When set to Automatic, you configure the backup location, the frequency of the backup, and how long to keep the backup files.</span></span> 

<span data-ttu-id="080dd-320">[Sauvegarde et restauration de BizTalk Services](biztalk-backup-restore.md) fournit les détails.</span><span class="sxs-lookup"><span data-stu-id="080dd-320">[BizTalk Services: Backup and Restore](biztalk-backup-restore.md) provides the details.</span></span> 

## <span data-ttu-id="080dd-321"><a name="HybridConnections"></a>Connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="080dd-321"><a name="HybridConnections"></a>Hybrid Connections</span></span>
<span data-ttu-id="080dd-322">Les connexions hybrides connectent une application Azure, telle que Web Apps ou Mobile Services dans Azure App Service, à une ressource locale utilisant un port TCP statique, tel que SQL Server, MySQL, les API web HTTP et la plupart des services web personnalisés.</span><span class="sxs-lookup"><span data-stu-id="080dd-322">Hybrid Connections connect an Azure application, like Web Apps or Mobile Apps in Azure App Service, to an on-premises resource that uses a static TCP port, such as SQL Server, MySQL, HTTP Web APIs, and most custom Web Services.</span></span> <span data-ttu-id="080dd-323">Les connexions hybrides sont gérées dans BizTalk Services au sein du portail Azure Classic.</span><span class="sxs-lookup"><span data-stu-id="080dd-323">Hybrid Connections are managed in  BizTalk Services in the Azure classic portal.</span></span>

<span data-ttu-id="080dd-324">Pour créer des connexions hybrides dans Azure App Service, voir [Accéder à des ressources locales à l’aide de connexions hybrides dans Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="080dd-324">To create Hybrid Connections in Azure App Service, see [Access on-premises resources using hybrid connections in Azure App Service](../app-service-web/web-sites-hybrid-connection-get-started.md).</span></span>

<span data-ttu-id="080dd-325">Pour créer ou gérer des connexions hybrides dans Azure BizTalk Services, consultez [Connexions hybrides](integration-hybrid-connection-overview.md).</span><span class="sxs-lookup"><span data-stu-id="080dd-325">To create or manage Hybrid Connections in Azure BizTalk Services, see [Hybrid Connections](integration-hybrid-connection-overview.md).</span></span>

## <a name="next"></a><span data-ttu-id="080dd-326">Suivant</span><span class="sxs-lookup"><span data-stu-id="080dd-326">Next</span></span>
<span data-ttu-id="080dd-327">À présent que vous connaissez bien les différents onglets, vous pouvez accéder à davantage d'informations sur les fonctionnalités Azure BizTalk Services :</span><span class="sxs-lookup"><span data-stu-id="080dd-327">Now that you're familiar with the different tabs, you can learn more about the Azure BizTalk Services features:</span></span>

* [<span data-ttu-id="080dd-328">Limitation dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="080dd-328">BizTalk Services: Throttling</span></span>](biztalk-throttling-thresholds.md)  
* [<span data-ttu-id="080dd-329">Nom et clé de l'émetteur dans BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="080dd-329">BizTalk Services: Issuer Name and Issuer Key</span></span>](biztalk-issuer-name-issuer-key.md)  
* [<span data-ttu-id="080dd-330">Sauvegarde et restauration de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="080dd-330">BizTalk Services: Backup and Restore</span></span>](biztalk-backup-restore.md)

## <a name="see-also"></a><span data-ttu-id="080dd-331">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="080dd-331">See Also</span></span>
* [<span data-ttu-id="080dd-332">Connexions hybrides</span><span class="sxs-lookup"><span data-stu-id="080dd-332">Hybrid Connections</span></span>](integration-hybrid-connection-overview.md)  
* [<span data-ttu-id="080dd-333">Tableau comparatif des éditions Développeur, De base, Standard et Premium de BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="080dd-333">BizTalk Services: Developer, Basic, Standard and Premium Editions Chart</span></span>](biztalk-editions-feature-chart.md)  
* [<span data-ttu-id="080dd-334">BizTalk Services : approvisionnement à l’aide du portail Azure Classic</span><span class="sxs-lookup"><span data-stu-id="080dd-334">BizTalk Services: Provisioning Using Azure classic portal</span></span>](biztalk-provision-services.md)  
* [<span data-ttu-id="080dd-335">BizTalk Services : tableau comparatif des états du service BizTalk</span><span class="sxs-lookup"><span data-stu-id="080dd-335">BizTalk Services: BizTalk Service State Chart</span></span>](biztalk-service-state-chart.md)  
* [<span data-ttu-id="080dd-336">Utilisation du Kit de développement logiciel (SDK) Azure BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="080dd-336">How do I Start Using the Azure BizTalk Services SDK</span></span>](http://go.microsoft.com/fwlink/p/?LinkID=302335)

[Quickstart]: ./media/biztalk-dashboard-monitor-scale-tabs/QuickStartIcon.png
[AddMetrics]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_AddMetrics.png
[GrayedMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_GrayedMetric.png
[EnabledMetric]: ./media/biztalk-dashboard-monitor-scale-tabs/WABS_EnabledMetric.png

