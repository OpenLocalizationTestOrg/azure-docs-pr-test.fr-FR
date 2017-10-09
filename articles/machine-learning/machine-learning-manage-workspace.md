---
title: aaaManage un espace de travail Machine Learning | Documents Microsoft
description: "Gérer les espaces de travail access tooAzure Machine Learning et de déployer et de gérer les services web d’API de ML"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.author: garye
ms.openlocfilehash: 7bd378d82aa46f4340ca974c7dc5a612c089cdca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-machine-learning-workspace"></a><span data-ttu-id="4adca-103">Gestion d'un espace de travail Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="4adca-103">Manage an Azure Machine Learning workspace</span></span>

> [!NOTE]
> <span data-ttu-id="4adca-104">Pour plus d’informations sur la gestion des services Web dans le portail de Services Web de Machine Learning hello, consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md).</span><span class="sxs-lookup"><span data-stu-id="4adca-104">For information on managing Web services in hello Machine Learning Web Services portal, see [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md).</span></span>
> 
> 

<span data-ttu-id="4adca-105">Vous pouvez gérer les espaces de travail Machine Learning soit Bonjour portail Azure ou hello portail Azure classic.</span><span class="sxs-lookup"><span data-stu-id="4adca-105">You can manage Machine Learning workspaces in either hello Azure portal or hello Azure classic portal.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="use-hello-azure-portal"></a><span data-ttu-id="4adca-106">Utilisez hello portail Azure</span><span class="sxs-lookup"><span data-stu-id="4adca-106">Use hello Azure portal</span></span>

<span data-ttu-id="4adca-107">toomanage Bonjour portail Azure, un espace de travail :</span><span class="sxs-lookup"><span data-stu-id="4adca-107">toomanage a workspace in hello Azure portal:</span></span>

1. <span data-ttu-id="4adca-108">Connectez-vous à toohello [portail Azure](https://portal.azure.com/) à l’aide d’un compte d’administrateur abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="4adca-108">Sign in toohello [Azure portal](https://portal.azure.com/) using an Azure subscription administrator account.</span></span>
2. <span data-ttu-id="4adca-109">Dans la zone de recherche hello en hello haut hello, entrez « machine learning les espaces de travail », puis sélectionnez **espaces de travail Machine Learning**.</span><span class="sxs-lookup"><span data-stu-id="4adca-109">In hello search box at hello top of hello page, enter "machine learning workspaces" and then select **Machine Learning Workspaces**.</span></span>
3. <span data-ttu-id="4adca-110">Cliquez sur hello espace de travail toomanage.</span><span class="sxs-lookup"><span data-stu-id="4adca-110">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="4adca-111">En outre les informations de gestion de ressources standard toohello et les options disponibles, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="4adca-111">In addition toohello standard resource management information and options available, you can:</span></span>

- <span data-ttu-id="4adca-112">Vue **propriétés** : cette page affiche des informations d’espace de travail et des ressources hello, et vous pouvez modifier les abonnement hello et groupe de ressources qui n’est connecté à cet espace de travail.</span><span class="sxs-lookup"><span data-stu-id="4adca-112">View **Properties** - This page displays hello workspace and resource information, and you can change hello subscription and resource group that this workspace is connected with.</span></span>
- <span data-ttu-id="4adca-113">**Resynchroniser les clés de stockage** -espace de travail hello gère le compte de stockage de clés toohello.</span><span class="sxs-lookup"><span data-stu-id="4adca-113">**Resync Storage Keys** - hello workspace maintains keys toohello storage account.</span></span> <span data-ttu-id="4adca-114">Si le compte de stockage hello change les clés, puis vous pouvez cliquer sur **Resync clés** toosynchronize les clés de hello avec espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-114">If hello storage account changes keys, then you can click **Resync keys** toosynchronize hello keys with hello workspace.</span></span>

<span data-ttu-id="4adca-115">associé à cet espace de travail, les services web hello toomanage utiliser le portail de Services Web de Machine Learning hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-115">toomanage hello web services associated with this workspace, use hello Machine Learning Web Services portal.</span></span> <span data-ttu-id="4adca-116">Consultez [gérer un service Web à l’aide du portail de Services Web de Azure Machine Learning hello](machine-learning-manage-new-webservice.md) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="4adca-116">See [Manage a Web service using hello Azure Machine Learning Web Services portal](machine-learning-manage-new-webservice.md) for complete information.</span></span>

> [!NOTE]
> <span data-ttu-id="4adca-117">toodeploy ou gérer les nouveaux services web que vous devez avoir un contributeur ou rôle d’administrateur sur le service web hello hello abonnement toowhich est déployé.</span><span class="sxs-lookup"><span data-stu-id="4adca-117">toodeploy or manage New web services you must be assigned a contributor or administrator role on hello subscription toowhich hello web service is deployed.</span></span> <span data-ttu-id="4adca-118">Si vous invitez à un autre utilisateur tooa d’apprentissage espace de travail, vous devez les affecter tooa un rôle administrateur ou collaborateur sur les abonnement hello avant de pouvoir déployer ou gérer les services web.</span><span class="sxs-lookup"><span data-stu-id="4adca-118">If you invite another user tooa machine learning workspace, you must assign them tooa contributor or administrator role on hello subscription before they can deploy or manage web services.</span></span> 
> 
><span data-ttu-id="4adca-119">Pour plus d’informations sur la définition des autorisations d’accès, consultez [afficher les affectations d’accès des utilisateurs et groupes dans le portail Azure - version préliminaire publique de hello](../active-directory/role-based-access-control-manage-assignments.md).</span><span class="sxs-lookup"><span data-stu-id="4adca-119">For more information on setting access permissions, see [View access assignments for users and groups in hello Azure portal - Public preview](../active-directory/role-based-access-control-manage-assignments.md).</span></span>

## <a name="use-hello-azure-classic-portal"></a><span data-ttu-id="4adca-120">Utilisez hello portail Azure classic</span><span class="sxs-lookup"><span data-stu-id="4adca-120">Use hello Azure classic portal</span></span>

<span data-ttu-id="4adca-121">À l’aide de hello portail Azure classic, vous pouvez gérer vos espaces de travail Machine Learning :</span><span class="sxs-lookup"><span data-stu-id="4adca-121">Using hello Azure classic portal, you can manage your Machine Learning workspaces to:</span></span>

* <span data-ttu-id="4adca-122">Surveiller l’utilisation d’espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="4adca-122">Monitor how hello workspace is being used</span></span>
* <span data-ttu-id="4adca-123">Configurer tooallow d’espace de travail hello ou refuser l’accès</span><span class="sxs-lookup"><span data-stu-id="4adca-123">Configure hello workspace tooallow or deny access</span></span>
* <span data-ttu-id="4adca-124">Gérer les services Web créés dans l’espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="4adca-124">Manage Web services created in hello workspace</span></span>
* <span data-ttu-id="4adca-125">Supprimer l’espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="4adca-125">Delete hello workspace</span></span>

<span data-ttu-id="4adca-126">En outre, onglet de tableau de bord hello fournit une vue d’ensemble de l’utilisation de l’espace de travail et un aperçu rapide de vos informations d’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="4adca-126">In addition, hello dashboard tab provides an overview of your workspace usage and a quick glance of your workspace information.</span></span>  

> [!TIP]
> <span data-ttu-id="4adca-127">Dans Azure Machine Learning Studio, sur hello **SERVICES WEB** onglet, vous pouvez ajouter, mettre à jour ou supprimer un service Web de la Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="4adca-127">In Azure Machine Learning Studio, on hello **WEB SERVICES** tab, you can add, update, or delete a Machine Learning Web service.</span></span>
> 
> 

<span data-ttu-id="4adca-128">toomanage un espace de travail Bonjour portail Azure classic :</span><span class="sxs-lookup"><span data-stu-id="4adca-128">toomanage a workspace in hello Azure classic portal:</span></span>

1. <span data-ttu-id="4adca-129">Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) à l’aide de votre Microsoft Azure compte - utiliser le compte hello hello abonnement Azure associé.</span><span class="sxs-lookup"><span data-stu-id="4adca-129">Sign in toohello [Azure classic portal](https://manage.windowsazure.com/) using your Microsoft Azure account - use hello account that's associated with hello Azure subscription.</span></span>
2. <span data-ttu-id="4adca-130">Dans le panneau de configuration des services de Microsoft Azure de hello, cliquez sur **MACHINE LEARNING**.</span><span class="sxs-lookup"><span data-stu-id="4adca-130">In hello Microsoft Azure services panel, click **MACHINE LEARNING**.</span></span>
3. <span data-ttu-id="4adca-131">Cliquez sur hello espace de travail toomanage.</span><span class="sxs-lookup"><span data-stu-id="4adca-131">Click hello workspace you want toomanage.</span></span>

<span data-ttu-id="4adca-132">page d’espace de travail Hello comporte trois onglets :</span><span class="sxs-lookup"><span data-stu-id="4adca-132">hello workspace page has three tabs:</span></span>

* <span data-ttu-id="4adca-133">**Tableau de bord** -vous permet de l’utilisation de tooview espace de travail et des informations</span><span class="sxs-lookup"><span data-stu-id="4adca-133">**DASHBOARD** - Allows you tooview workspace usage and information</span></span>
* <span data-ttu-id="4adca-134">**CONFIGURER** -vous permet d’espace de travail toomanage access toohello</span><span class="sxs-lookup"><span data-stu-id="4adca-134">**CONFIGURE** - Allows you toomanage access toohello workspace</span></span>
* <span data-ttu-id="4adca-135">**SERVICES WEB** -vous permet de services Web toomanage qui ont été publiés à partir de cet espace de travail</span><span class="sxs-lookup"><span data-stu-id="4adca-135">**WEB SERVICES** - Allows you toomanage Web services that have been published from this workspace</span></span>

### <a name="toomonitor-how-hello-workspace-is-being-used"></a><span data-ttu-id="4adca-136">toomonitor utilisation espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="4adca-136">toomonitor how hello workspace is being used</span></span>
<span data-ttu-id="4adca-137">Cliquez sur hello **tableau de bord** onglet.</span><span class="sxs-lookup"><span data-stu-id="4adca-137">Click hello **DASHBOARD** tab.</span></span>

<span data-ttu-id="4adca-138">À partir du tableau de bord hello, vous pouvez afficher l’utilisation globale de votre espace de travail et obtenir un aperçu rapide des informations de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="4adca-138">From hello dashboard, you can view overall usage of your workspace and get a quick glance of workspace information.</span></span>

* <span data-ttu-id="4adca-139">Hello **de calcul** graphique montre les ressources de calcul hello utilisés par l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-139">hello **COMPUTE** chart shows hello compute resources being used by hello workspace.</span></span> <span data-ttu-id="4adca-140">Vous pouvez modifier toodisplay de vue hello relatif ou des valeurs absolues, et vous pouvez modifier la période de hello affichée dans le graphique de hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-140">You can change hello view toodisplay relative or absolute values, and you can change hello timeframe displayed in hello chart.</span></span>
* <span data-ttu-id="4adca-141">**Présentation de l’utilisation** affiche le stockage Azure utilisé par l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-141">**Usage overview** displays Azure storage being used by hello workspace.</span></span>
* <span data-ttu-id="4adca-142">**Aperçu rapide** fournit un résumé des informations de l’espace de travail ainsi que des liens utiles.</span><span class="sxs-lookup"><span data-stu-id="4adca-142">**Quick glance** provides a summary of workspace information and useful links.</span></span>

> [!NOTE]
> <span data-ttu-id="4adca-143">Hello **connexion tooML Studio** lien ouvre Machine Learning Studio à l’aide de hello Account Microsoft vous êtes actuellement connecté.</span><span class="sxs-lookup"><span data-stu-id="4adca-143">hello **Sign-in tooML Studio** link opens Machine Learning Studio using hello Microsoft Account you are currently signed into.</span></span> <span data-ttu-id="4adca-144">Hello Microsoft Account vous avez utilisé toosign dans toohello toocreate portail classique Azure un espace de travail automatiquement n’autorisation tooopen cet espace de travail.</span><span class="sxs-lookup"><span data-stu-id="4adca-144">hello Microsoft Account you used toosign in toohello Azure classic portal toocreate a workspace does not automatically have permission tooopen that workspace.</span></span> <span data-ttu-id="4adca-145">tooopen un espace de travail, vous devez être connecté toohello Account Microsoft qui a été défini en tant que propriétaire hello d’espace de travail hello, ou vous devez tooreceive une invitation à partir de l’espace de travail hello propriétaire toojoin hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-145">tooopen a workspace, you must be signed in toohello Microsoft Account that was defined as hello owner of hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span>
> 
> 

### <a name="toogrant-or-suspend-access-for-users"></a><span data-ttu-id="4adca-146">toogrant ou suspendre l’accès pour les utilisateurs</span><span class="sxs-lookup"><span data-stu-id="4adca-146">toogrant or suspend access for users</span></span>
<span data-ttu-id="4adca-147">Cliquez sur hello **configurer** onglet.</span><span class="sxs-lookup"><span data-stu-id="4adca-147">Click hello **CONFIGURE** tab.</span></span>

<span data-ttu-id="4adca-148">Vous pouvez effectuer les opérations suivantes à partir de l’onglet de configuration hello :</span><span class="sxs-lookup"><span data-stu-id="4adca-148">From hello configuration tab you can:</span></span>

* <span data-ttu-id="4adca-149">Suspendre l’espace de travail access toohello Machine Learning en cliquant sur Refuser.</span><span class="sxs-lookup"><span data-stu-id="4adca-149">Suspend access toohello Machine Learning workspace by clicking DENY.</span></span> <span data-ttu-id="4adca-150">Les utilisateurs ne seront plus en mesure de tooopen hello espace de travail Machine Learning Studio.</span><span class="sxs-lookup"><span data-stu-id="4adca-150">Users will no longer be able tooopen hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="4adca-151">toorestore access, cliquez sur Autoriser.</span><span class="sxs-lookup"><span data-stu-id="4adca-151">toorestore access, click ALLOW.</span></span>

<span data-ttu-id="4adca-152">toomanage autres comptes qui ont accès toohello espace de travail dans Machine Learning Studio, cliquez sur **connexion tooML Studio** Bonjour **tableau de bord** onglet (voir la remarque précédente de hello concernant  **Sign-in tooML Studio**).</span><span class="sxs-lookup"><span data-stu-id="4adca-152">toomanage additional accounts who have access toohello workspace in Machine Learning Studio, click **Sign-in tooML Studio** in hello **DASHBOARD** tab (see hello preceeding note regarding **Sign-in tooML Studio**).</span></span> <span data-ttu-id="4adca-153">Espace de travail hello dans Machine Learning Studio s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="4adca-153">This opens hello workspace in Machine Learning Studio.</span></span> <span data-ttu-id="4adca-154">À ce stade, cliquez sur hello **paramètres** onglet, puis **utilisateurs**.</span><span class="sxs-lookup"><span data-stu-id="4adca-154">From here, click hello **SETTINGS** tab and then **USERS**.</span></span> <span data-ttu-id="4adca-155">Vous pouvez cliquer sur **inviter des utilisateurs plus** toogive utilisateurs accéder toohello, espace de travail, ou sélectionnez un utilisateur, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="4adca-155">You can click **INVITE MORE USERS** toogive users access toohello workspace, or select a user and click **REMOVE**.</span></span>

### <a name="toomanage-web-services-in-this-workspace"></a><span data-ttu-id="4adca-156">services web toomanage dans cet espace de travail</span><span class="sxs-lookup"><span data-stu-id="4adca-156">toomanage web services in this workspace</span></span>
<span data-ttu-id="4adca-157">Cliquez sur hello **SERVICES WEB** onglet.</span><span class="sxs-lookup"><span data-stu-id="4adca-157">Click hello **WEB SERVICES** tab.</span></span>

<span data-ttu-id="4adca-158">Cela affiche une liste des services Web publiés à partir de cet espace de travail.</span><span class="sxs-lookup"><span data-stu-id="4adca-158">This displays a list of web services published from this workspace.</span></span>
<span data-ttu-id="4adca-159">toomanage un service web, cliquez sur nom hello dans la page du service Web hello liste tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-159">toomanage a web service, click hello name in hello list tooopen hello Web service page.</span></span>

<span data-ttu-id="4adca-160">Un service web peut avoir un ou plusieurs points de terminaison.</span><span class="sxs-lookup"><span data-stu-id="4adca-160">A Web service may have one or more endpoints defined.</span></span>

* <span data-ttu-id="4adca-161">Vous pouvez définir plusieurs points de terminaison dans le point de terminaison addition toohello « Default ».</span><span class="sxs-lookup"><span data-stu-id="4adca-161">You can define more endpoints in addition toohello "Default" endpoint.</span></span> <span data-ttu-id="4adca-162">tooadd hello du point de terminaison, cliquez sur **gérer les points de terminaison** bas hello du portail de Services Web de Azure Machine Learning hello du tableau de bord tooopen hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-162">tooadd hello endpoint, click **Manage Endpoints** at hello bottom of hello dashboard tooopen hello Azure Machine Learning Web Services portal.</span></span>
* <span data-ttu-id="4adca-163">toodelete un point de terminaison (vous ne pouvez pas supprimer de point de terminaison « Par défaut » hello), cliquez sur la case à cocher au début de hello de ligne de point de terminaison hello hello, puis cliquez sur **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="4adca-163">toodelete an endpoint (you cannot delete hello "Default" endpoint), click hello check box at hello beginning of hello endpoint row, and click **DELETE**.</span></span> <span data-ttu-id="4adca-164">Cela supprime les point de terminaison hello hello service Web.</span><span class="sxs-lookup"><span data-stu-id="4adca-164">This removes hello endpoint from hello Web service.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4adca-165">Si une application utilise le point de terminaison de service hello web lors de la suppression du point de terminaison hello, application hello recevra un hello erreur prochaine que tente de service de hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="4adca-165">If an application is using hello web service endpoint when hello endpoint is deleted, hello application will receive an error hello next time it tries tooaccess hello service.</span></span>
  > 
  > 

<span data-ttu-id="4adca-166">Cliquez sur nom hello d’un tooopen de point de terminaison de service Web il.</span><span class="sxs-lookup"><span data-stu-id="4adca-166">Click hello name of a Web service endpoint tooopen it.</span></span> 

<span data-ttu-id="4adca-167">À partir du tableau de bord hello, vous pouvez afficher l’utilisation globale de votre service Web sur une période de temps.</span><span class="sxs-lookup"><span data-stu-id="4adca-167">From hello dashboard, you can view overall usage of your Web service over a period of time.</span></span> <span data-ttu-id="4adca-168">Vous pouvez sélectionner les tooview période hello dans hello période liste déroulante dans le coin supérieur droit de hello de graphiques d’utilisation de hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-168">You can select hello period tooview from hello Period dropdown menu in hello upper right of hello usage charts.</span></span> <span data-ttu-id="4adca-169">tableau de bord Hello montre hello informations suivantes :</span><span class="sxs-lookup"><span data-stu-id="4adca-169">hello dashboard shows hello following information:</span></span>

* <span data-ttu-id="4adca-170">**Les demandes au fil du temps** affiche un graphique de l’étape du nombre de hello de demandes au hello période sélectionnée.</span><span class="sxs-lookup"><span data-stu-id="4adca-170">**Requests Over Time** displays a step graph of hello number of requests over hello selected time period.</span></span> <span data-ttu-id="4adca-171">Ce graphique vous permet d’identifier les pics d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="4adca-171">It can help identify if you are experiencing spikes in usage.</span></span>
* <span data-ttu-id="4adca-172">**Demandes de requête-réponse** affiche hello le nombre total d’appels de requête-réponse service de hello a reçu sur hello période sélectionnée et l’échec de nombre d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="4adca-172">**Request-Response Requests** displays hello total number of Request-Response calls hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="4adca-173">**Temps moyen de demande-réponse de calcul** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.</span><span class="sxs-lookup"><span data-stu-id="4adca-173">**Average Request-Response Compute Time** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="4adca-174">**Requêtes de lots** hello affiche le nombre total de service hello de requêtes de lots a reçu sur hello période sélectionnée et Échec de nombre d'entre eux.</span><span class="sxs-lookup"><span data-stu-id="4adca-174">**Batch Requests** displays hello total number of Batch Requests hello service has received over hello selected time period and how many of them failed.</span></span>
* <span data-ttu-id="4adca-175">**Latence de travail moyenne** affiche une moyenne de temps de hello nécessaire tooexecute hello reçu demandes.</span><span class="sxs-lookup"><span data-stu-id="4adca-175">**Average Job Latency** displays an average of hello time needed tooexecute hello received requests.</span></span>
* <span data-ttu-id="4adca-176">**Erreurs** numéro hello d’agrégation d’erreurs qui se sont produites sur le service web de toohello appels.</span><span class="sxs-lookup"><span data-stu-id="4adca-176">**Errors** displays hello aggregate number of errors that have occurred on calls toohello web service.</span></span>
* <span data-ttu-id="4adca-177">**Les coûts des services** affiche hello des frais pour le plan de facturation hello associé hello service.</span><span class="sxs-lookup"><span data-stu-id="4adca-177">**Services Costs** displays hello charges for hello billing plan associated with hello service.</span></span>

<span data-ttu-id="4adca-178">À partir de la page Configurer de hello, vous pouvez mettre à jour hello propriétés suivantes :</span><span class="sxs-lookup"><span data-stu-id="4adca-178">From hello Configure page, you can update hello following properties:</span></span>

* <span data-ttu-id="4adca-179">**Description** vous permet de tooenter une description de service Web de hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-179">**Description** allows you tooenter a description for hello Web service.</span></span> <span data-ttu-id="4adca-180">Le champ Description est obligatoire.</span><span class="sxs-lookup"><span data-stu-id="4adca-180">Description is a required field.</span></span>
* <span data-ttu-id="4adca-181">**Journalisation** vous permet d’erreur tooenable ou désactiver la connexion de point de terminaison hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-181">**Logging** allows you tooenable or disable error logging on hello endpoint.</span></span> <span data-ttu-id="4adca-182">Pour plus d’informations sur la journalisation, voir [Activation de la journalisation pour les services web Machine Learning](machine-learning-web-services-logging.md).</span><span class="sxs-lookup"><span data-stu-id="4adca-182">For more information on Logging, see Enable [logging for Machine Learning web services](machine-learning-web-services-logging.md).</span></span>
* <span data-ttu-id="4adca-183">**Activer les exemples de données** vous permet de tooprovide exemples de données que vous pouvez utiliser le service de requête-réponse de hello tootest.</span><span class="sxs-lookup"><span data-stu-id="4adca-183">**Enable Sample data** allows you tooprovide sample data that you can use tootest hello Request-Response service.</span></span> <span data-ttu-id="4adca-184">Si vous avez créé le service web de hello dans Machine Learning Studio, les données d’exemple hello sont effectuées à partir des données de hello votre tootrain utilisé votre modèle.</span><span class="sxs-lookup"><span data-stu-id="4adca-184">If you created hello web service in Machine Learning Studio, hello sample data is taken from hello data your used tootrain your model.</span></span> <span data-ttu-id="4adca-185">Si vous avez créé le service de hello par programme, les données de salutation provient de données d’exemple hello fournies en tant que partie du package JSON hello.</span><span class="sxs-lookup"><span data-stu-id="4adca-185">If you created hello service programmatically, hello data is taken from hello example data you provided as part of hello JSON package.</span></span>

