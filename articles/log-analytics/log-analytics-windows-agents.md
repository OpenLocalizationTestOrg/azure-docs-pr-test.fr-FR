---
title: aaaConnect Windows ordinateurs tooAzure Analytique de journal | Documents Microsoft
description: "Cet article explique les ordinateurs Windows hello hello étapes tooconnect dans votre toohello d’infrastructure sur site service d’Analytique de journal à l’aide d’une version personnalisée de hello Microsoft Monitoring Agent (MMA)."
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: 932f7b8c-485c-40c1-98e3-7d4c560876d2
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: magoedte
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 7e15f9eeb0440bd2f6557d7215df701526e4f9aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-windows-computers-toohello-log-analytics-service-in-azure"></a><span data-ttu-id="f10f8-103">Connecter Windows ordinateurs toohello Analytique de journal service dans Azure</span><span class="sxs-lookup"><span data-stu-id="f10f8-103">Connect Windows computers toohello Log Analytics service in Azure</span></span>

<span data-ttu-id="f10f8-104">Cet article explique les étapes hello tooconnect les ordinateurs Windows dans les espaces de travail local infrastructure tooOMS à l’aide d’une version personnalisée de hello Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="f10f8-104">This article shows hello steps tooconnect Windows computers in your on-premises infrastructure tooOMS workspaces by using a customized version of hello Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="f10f8-105">Vous devez tooinstall et connectez les agents pour tous les ordinateurs hello que vous souhaitez tooonboard pour permettre leur service de journal Analytique toosend données toohello et tooview et agir sur ces données.</span><span class="sxs-lookup"><span data-stu-id="f10f8-105">You need tooinstall and connect agents for all of hello computers that you want tooonboard in order for them toosend data toohello Log Analytics service and tooview and act on that data.</span></span> <span data-ttu-id="f10f8-106">Chaque agent peut signaler des espaces de travail toomultiple.</span><span class="sxs-lookup"><span data-stu-id="f10f8-106">Each agent can report toomultiple workspaces.</span></span>

<span data-ttu-id="f10f8-107">Vous pouvez installer des agents à l’aide du programme d’installation, de la ligne de commande, ou de la fonction Desired State Configuration (DSC) d’Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f10f8-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="f10f8-108">Pour les ordinateurs virtuels s’exécutant dans Azure, vous pouvez simplifier l’installation à l’aide de hello [extension de machine virtuelle](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f10f8-108">For virtual machines running in Azure, you can simplify installation by using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="f10f8-109">Sur les ordinateurs avec une connexion Internet, l’agent de hello utilise hello connexion toohello Internet toosend données tooOMS.</span><span class="sxs-lookup"><span data-stu-id="f10f8-109">On computers with Internet connectivity, hello agent uses hello connection toohello Internet toosend data tooOMS.</span></span> <span data-ttu-id="f10f8-110">Pour les ordinateurs qui n’ont pas de connectivité Internet, vous pouvez utiliser un proxy ou un hello [OMS passerelle](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f10f8-110">For computers that do not have Internet connectivity, you can use a proxy or hello [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="f10f8-111">La connexion de votre tooOMS d’ordinateurs Windows est simple à l’aide de trois étapes simples :</span><span class="sxs-lookup"><span data-stu-id="f10f8-111">Connecting your Windows computers tooOMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="f10f8-112">Télécharger le fichier d’installation de l’agent hello à partir du portail OMS hello</span><span class="sxs-lookup"><span data-stu-id="f10f8-112">Download hello agent setup file from hello OMS portal</span></span>
2. <span data-ttu-id="f10f8-113">Installer l’agent hello à l’aide de la méthode hello choisie</span><span class="sxs-lookup"><span data-stu-id="f10f8-113">Install hello agent using hello method you choose</span></span>
3. <span data-ttu-id="f10f8-114">Configurer l’agent de hello ou ajouter des espaces de travail supplémentaires, si nécessaire</span><span class="sxs-lookup"><span data-stu-id="f10f8-114">Configure hello agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="f10f8-115">Hello diagramme suivant montre hello relation entre vos ordinateurs Windows et OMS une fois que vous avez installé et configuré des agents.</span><span class="sxs-lookup"><span data-stu-id="f10f8-115">hello following diagram shows hello relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="f10f8-117">Si vos stratégies de sécurité informatique n’autorisent pas les ordinateurs sur votre toohello de tooconnect réseau Internet, vous pouvez configurer votre toohello de tooconnect ordinateurs OMS passerelle.</span><span class="sxs-lookup"><span data-stu-id="f10f8-117">If your IT security policies do not allow computers on your network tooconnect toohello Internet, you can configure your computers tooconnect toohello OMS Gateway.</span></span> <span data-ttu-id="f10f8-118">Pour plus d’informations sur comment tooconfigure toocommunicate de vos serveurs via un service OMS toohello de passerelle d’OMS, consultez [connecter tooOMS d’ordinateurs à l’aide de hello OMS passerelle](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="f10f8-118">For more information and steps on how tooconfigure your servers toocommunicate through an OMS Gateway toohello OMS service, see [Connect computers tooOMS using hello OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="f10f8-119">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="f10f8-119">System requirements and required configuration</span></span>
<span data-ttu-id="f10f8-120">Avant d’installer ou de déployer des agents, passez en revue hello suivant tooensure détails hello requise.</span><span class="sxs-lookup"><span data-stu-id="f10f8-120">Before you install or deploy agents, review hello following details tooensure you meet hello requirements.</span></span>

- <span data-ttu-id="f10f8-121">Vous ne pouvez installer hello OMS MMA sur les ordinateurs exécutant Windows Server 2008 SP 1 ou version ultérieure ou Windows 7 SP1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="f10f8-121">You can only install hello OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="f10f8-122">Vous avez besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f10f8-122">You need an Azure subscription.</span></span>  <span data-ttu-id="f10f8-123">Pour plus d’informations, consultez l’article [Prise en main de Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f10f8-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="f10f8-124">Chaque ordinateur Windows doit être en mesure de tooconnect toohello Internet à l’aide de HTTPS ou toohello OMS passerelle.</span><span class="sxs-lookup"><span data-stu-id="f10f8-124">Each Windows computer must be able tooconnect toohello Internet using HTTPS or toohello OMS Gateway.</span></span> <span data-ttu-id="f10f8-125">Cette connexion peut être directe, via un proxy, ou hello OMS passerelle.</span><span class="sxs-lookup"><span data-stu-id="f10f8-125">This connection can be direct, via a proxy, or through hello OMS Gateway.</span></span>
- <span data-ttu-id="f10f8-126">Vous pouvez installer hello OMS MMA sur les ordinateurs autonomes, des serveurs et des ordinateurs virtuels.</span><span class="sxs-lookup"><span data-stu-id="f10f8-126">You can install hello OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="f10f8-127">Si vous souhaitez tooconnect les ordinateurs virtuels hébergés par Azure tooOMS, consultez [tooLog de machines virtuelles Azure de se connecter Analytique](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="f10f8-127">If you want tooconnect Azure-hosted virtual machines tooOMS, see [Connect Azure virtual machines tooLog Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="f10f8-128">l’agent Hello doit toouse le port TCP 443 pour les différentes ressources.</span><span class="sxs-lookup"><span data-stu-id="f10f8-128">hello agent needs toouse TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="f10f8-129">Réseau</span><span class="sxs-lookup"><span data-stu-id="f10f8-129">Network</span></span>

<span data-ttu-id="f10f8-130">Pour Windows agents tooconnect tooand inscrire auprès de service d’OMS hello, ils doivent avoir accès toonetwork ressources, notamment les numéros de port hello et les URL de domaine.</span><span class="sxs-lookup"><span data-stu-id="f10f8-130">For Windows agents tooconnect tooand register with hello OMS service, they must have access toonetwork resources, including hello port numbers and domain URLs.</span></span>

- <span data-ttu-id="f10f8-131">Pour les serveurs proxy, vous devez tooensure qui hello du serveur proxy approprié ressources sont configurés dans les paramètres de l’agent.</span><span class="sxs-lookup"><span data-stu-id="f10f8-131">For proxy servers, you need tooensure that hello appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="f10f8-132">Pour les pare-feu qui limitent l’accès toohello Internet, vous ou vos ingénieurs réseau doivent tooconfigure votre tooOMS d’accès de toopermit pare-feu.</span><span class="sxs-lookup"><span data-stu-id="f10f8-132">For firewalls that restrict access toohello Internet, you or your networking engineers need tooconfigure your firewall toopermit access tooOMS.</span></span> <span data-ttu-id="f10f8-133">Aucune action n’est nécessaire dans les paramètres de l’agent.</span><span class="sxs-lookup"><span data-stu-id="f10f8-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="f10f8-134">Hello tableau suivant montre les ressources nécessaires pour la communication.</span><span class="sxs-lookup"><span data-stu-id="f10f8-134">hello following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="f10f8-135">Certains hello suivant des ressources mentionnent Operational Insights, qui était un ancien nom d’Analytique de journal.</span><span class="sxs-lookup"><span data-stu-id="f10f8-135">Some of hello following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="f10f8-136">Ressource de l'agent</span><span class="sxs-lookup"><span data-stu-id="f10f8-136">Agent Resource</span></span> | <span data-ttu-id="f10f8-137">Ports</span><span class="sxs-lookup"><span data-stu-id="f10f8-137">Ports</span></span> | <span data-ttu-id="f10f8-138">Ignorer l’inspection HTTPS</span><span class="sxs-lookup"><span data-stu-id="f10f8-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="f10f8-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f10f8-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="f10f8-140">443</span><span class="sxs-lookup"><span data-stu-id="f10f8-140">443</span></span> | <span data-ttu-id="f10f8-141">Oui</span><span class="sxs-lookup"><span data-stu-id="f10f8-141">Yes</span></span> |
| <span data-ttu-id="f10f8-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="f10f8-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="f10f8-143">443</span><span class="sxs-lookup"><span data-stu-id="f10f8-143">443</span></span> | <span data-ttu-id="f10f8-144">Oui</span><span class="sxs-lookup"><span data-stu-id="f10f8-144">Yes</span></span> |
| <span data-ttu-id="f10f8-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="f10f8-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="f10f8-146">443</span><span class="sxs-lookup"><span data-stu-id="f10f8-146">443</span></span> | <span data-ttu-id="f10f8-147">Oui</span><span class="sxs-lookup"><span data-stu-id="f10f8-147">Yes</span></span> |
| <span data-ttu-id="f10f8-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="f10f8-148">*.azure-automation.net</span></span> | <span data-ttu-id="f10f8-149">443</span><span class="sxs-lookup"><span data-stu-id="f10f8-149">443</span></span> | <span data-ttu-id="f10f8-150">Oui</span><span class="sxs-lookup"><span data-stu-id="f10f8-150">Yes</span></span> |



## <a name="download-hello-agent-setup-file-from-oms"></a><span data-ttu-id="f10f8-151">Télécharger le fichier d’installation de l’agent hello d’OMS</span><span class="sxs-lookup"><span data-stu-id="f10f8-151">Download hello agent setup file from OMS</span></span>
1. <span data-ttu-id="f10f8-152">Dans le portail OMS hello, sur hello **vue d’ensemble** , cliquez sur hello **paramètres** vignette.</span><span class="sxs-lookup"><span data-stu-id="f10f8-152">In hello OMS portal, on hello **Overview** page, click hello **Settings** tile.</span></span>  <span data-ttu-id="f10f8-153">Cliquez sur hello **Sources connectées** onglet en haut de hello.</span><span class="sxs-lookup"><span data-stu-id="f10f8-153">Click hello **Connected Sources** tab at hello top.</span></span>  
    <span data-ttu-id="f10f8-154">![onglet Sources connectées](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="f10f8-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="f10f8-155">Cliquez sur **serveurs Windows** puis cliquez sur **télécharger l’Agent Windows** tooyour applicable ordinateur processeur toodownload hello fichier des paramètres.</span><span class="sxs-lookup"><span data-stu-id="f10f8-155">Click **Windows Servers** and then click **Download Windows Agent** applicable tooyour computer processor type toodownload hello setup file.</span></span>
3. <span data-ttu-id="f10f8-156">Sur hello à droite de **ID de l’espace de travail**, cliquez sur icône de copie hello et collez hello ID dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="f10f8-156">On hello right of **Workspace ID**, click hello copy icon and paste hello ID into Notepad.</span></span>
4. <span data-ttu-id="f10f8-157">Sur hello à droite de **clé primaire**, cliquez sur icône de copie hello et collez la clé de hello dans le bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="f10f8-157">On hello right of **Primary Key**, click hello copy icon and paste hello key into Notepad.</span></span>     

## <a name="install-hello-agent-using-setup"></a><span data-ttu-id="f10f8-158">Installer l’agent de hello à l’aide du programme d’installation</span><span class="sxs-lookup"><span data-stu-id="f10f8-158">Install hello agent using setup</span></span>
1. <span data-ttu-id="f10f8-159">Exécutez l’agent hello de tooinstall le programme d’installation sur un ordinateur que vous souhaitez toomanage.</span><span class="sxs-lookup"><span data-stu-id="f10f8-159">Run Setup tooinstall hello agent on a computer that you want toomanage.</span></span>
2. <span data-ttu-id="f10f8-160">Dans la page d’accueil hello, cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-160">On hello Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="f10f8-161">Dans la page termes du contrat de licence de hello, lisez hello de licence, puis sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-161">On hello License Terms page, read hello license and then click **I Agree**.</span></span>
4. <span data-ttu-id="f10f8-162">Sur la page dossier de Destination de hello, modifier ou conservez le dossier d’installation par défaut hello et puis cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-162">On hello Destination Folder page, change or keep hello default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="f10f8-163">Sur la page d’Options d’installation de l’Agent hello, vous pouvez choisir tooconnect hello agent tooAzure Analytique des journaux (OMS), Operations Manager, ou vous pouvez laisser le choix de hello vide si vous souhaitez que l’agent de tooconfigure hello plus tard.</span><span class="sxs-lookup"><span data-stu-id="f10f8-163">On hello Agent Setup Options page, you can choose tooconnect hello agent tooAzure Log Analytics (OMS), Operations Manager, or you can leave hello choices blank if you want tooconfigure hello agent later.</span></span> <span data-ttu-id="f10f8-164">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-164">Click **Next**.</span></span>   
    - <span data-ttu-id="f10f8-165">Si vous avez choisi tooconnect tooAzure Analytique des journaux (OMS), collez hello **ID de l’espace de travail** et **clé de l’espace de travail (clé primaire)** que vous avez copié dans le bloc-notes, dans la procédure précédente de hello puis cliquez sur  **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-165">If you chose tooconnect tooAzure Log Analytics (OMS), paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in hello previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="f10f8-166">![Coller l’ID et la clé primaire de l’espace de travail](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="f10f8-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="f10f8-167">Si vous avez choisi tooconnect tooOperations Manager, tapez Bonjour **nom du groupe d’administration**, **Management Server** nom, et **Port serveur d’administration**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-167">If you chose tooconnect tooOperations Manager, type hello **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="f10f8-168">Sur la page compte d’Action de l’Agent de hello, choisissez le compte système Local de hello ou d’un compte de domaine local, puis sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-168">On hello Agent Action Account page, choose either hello Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="f10f8-169">![Configuration du groupe d’administration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![compte d’action d’agent](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="f10f8-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="f10f8-170">Dans la page de prêt tooInstall hello, passez en revue vos choix, puis sur **installer**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-170">On hello Ready tooInstall page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="f10f8-171">Page hello Configuration terminée, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-171">On hello Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="f10f8-172">Lorsque vous avez terminé, hello **Microsoft Monitoring Agent** s’affiche dans **le panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-172">When complete, hello **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="f10f8-173">Vous pouvez vérifier votre configuration il et vérifiez que l’agent hello est connecté tooOperational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="f10f8-173">You can review your configuration there and verify that hello agent is connected tooOperational Insights (OMS).</span></span> <span data-ttu-id="f10f8-174">Lorsque tooOMS connectés, hello agent affiche un message indiquant : **hello Microsoft Monitoring Agent n’est pas connecté service de Microsoft Operations Management Suite toohello.**</span><span class="sxs-lookup"><span data-stu-id="f10f8-174">When connected tooOMS, hello agent displays a message stating: **hello Microsoft Monitoring Agent has successfully connected toohello Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="f10f8-175">Configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="f10f8-175">Configure proxy settings</span></span>

<span data-ttu-id="f10f8-176">Vous pouvez utiliser hello suivant les paramètres du proxy tooconfigure procédure pour hello Microsoft Monitoring Agent dans le panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="f10f8-176">You can use hello following procedure tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="f10f8-177">Vous devez toouse de cette procédure pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="f10f8-177">You need toouse this procedure for each server.</span></span> <span data-ttu-id="f10f8-178">Si vous avez plusieurs serveurs que vous avez besoin de tooconfigure, il peut s’avérer plus facile toouse un tooautomate script ce processus.</span><span class="sxs-lookup"><span data-stu-id="f10f8-178">If you have many servers that you need tooconfigure, you might find it easier toouse a script tooautomate this process.</span></span> <span data-ttu-id="f10f8-179">Dans ce cas, consultez la procédure suivante de hello [tooconfigure les paramètres de proxy de Microsoft Monitoring Agent à l’aide d’un script de hello](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="f10f8-179">If so, see hello next procedure [tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="f10f8-180">paramètres de proxy tooconfigure pourquoi Microsoft Monitoring Agent dans le panneau de configuration</span><span class="sxs-lookup"><span data-stu-id="f10f8-180">tooconfigure proxy settings for hello Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="f10f8-181">Ouvrez le **Panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="f10f8-182">Ouvrez **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="f10f8-183">Cliquez sur hello **paramètres Proxy** onglet.</span><span class="sxs-lookup"><span data-stu-id="f10f8-183">Click hello **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="f10f8-184">![Onglet Paramètres de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="f10f8-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="f10f8-185">Sélectionnez **utiliser un serveur proxy** et tapez Bonjour URL et le numéro de port, si une est exemple toohello nécessaire, comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="f10f8-185">Select **Use a proxy server** and type hello URL and port number, if one is needed, similar toohello example shown.</span></span> <span data-ttu-id="f10f8-186">Si votre serveur proxy requiert une authentification, tapez Bonjour nom d’utilisateur et mot de passe tooaccess hello serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="f10f8-186">If your proxy server requires authentication, type hello username and password tooaccess hello proxy server.</span></span>


### <a name="verify-agent-connectivity-toooms"></a><span data-ttu-id="f10f8-187">Vérifiez tooOMS de connectivité de l’agent</span><span class="sxs-lookup"><span data-stu-id="f10f8-187">Verify agent connectivity tooOMS</span></span>

<span data-ttu-id="f10f8-188">Vous pouvez facilement vérifier si vos agents communiquent avec OMS à l’aide de la procédure de hello :</span><span class="sxs-lookup"><span data-stu-id="f10f8-188">You can easily verify whether your agents are communicating with OMS using hello following procedure:</span></span>

1.  <span data-ttu-id="f10f8-189">Sur l’ordinateur hello avec l’agent Windows hello, ouvrez le panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="f10f8-189">On hello computer with hello Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="f10f8-190">Ouvrez Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="f10f8-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="f10f8-191">Cliquez sur onglet d’Analytique des journaux (OMS) Azure hello.</span><span class="sxs-lookup"><span data-stu-id="f10f8-191">Click hello Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="f10f8-192">Dans la colonne d’état hello, vous devez voir que l’agent hello correctement toohello Operations Management Suite service connecté.</span><span class="sxs-lookup"><span data-stu-id="f10f8-192">In hello Status column, you should see that hello agent connected successfully toohello Operations Management Suite service.</span></span>

![agent connecté](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="tooconfigure-proxy-settings-for-hello-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="f10f8-194">paramètres de proxy tooconfigure pourquoi Microsoft Monitoring Agent à l’aide d’un script</span><span class="sxs-lookup"><span data-stu-id="f10f8-194">tooconfigure proxy settings for hello Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="f10f8-195">Copiez hello suivantes exemple, de mises à jour spécifiques tooyour environnement, enregistrement avec une extension de nom de fichier PS1 et puis exécutez le script de hello sur chaque ordinateur qui se connecte directement service OMS de toohello.</span><span class="sxs-lookup"><span data-stu-id="f10f8-195">Copy hello following sample, update it with information specific tooyour environment, save it with a PS1 file name extension, and then run hello script on each computer that connects directly toohello OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get hello Health Service configuration object.  We need toodetermine if we
    #have hello right update rollup with hello API we need.  If not, no need toorun hello rest of hello script.
    $healthServiceSettings = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'

    $proxyMethod = $healthServiceSettings | Get-Member -Name 'SetProxyInfo'

    if (!$proxyMethod)
    {
         Write-Output 'Health Service proxy API not present, will not update settings.'
         return
    }

    Write-Output "Clearing proxy settings."
    $healthServiceSettings.SetProxyInfo('', '', '')

    $ProxyUserName = $cred.username

    Write-Output "Setting proxy too$ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-hello-agent-using-hello-command-line"></a><span data-ttu-id="f10f8-196">Installer l’agent de hello à l’aide de la ligne de commande hello</span><span class="sxs-lookup"><span data-stu-id="f10f8-196">Install hello agent using hello command line</span></span>
- <span data-ttu-id="f10f8-197">Modifier, puis utilisez hello suivant de l’agent hello exemple tooinstall à l’aide de la ligne de commande hello.</span><span class="sxs-lookup"><span data-stu-id="f10f8-197">Modify and then use hello following example tooinstall hello agent using hello command line.</span></span> <span data-ttu-id="f10f8-198">exemple de Hello effectue une installation entièrement sans assistance.</span><span class="sxs-lookup"><span data-stu-id="f10f8-198">hello example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="f10f8-199">Si vous voulez tooupgrade un agent, vous devez toouse hello Analytique de journal API de script.</span><span class="sxs-lookup"><span data-stu-id="f10f8-199">If you want tooupgrade an agent, you need toouse hello Log Analytics scripting API.</span></span> <span data-ttu-id="f10f8-200">Consultez hello suivant section tooupgrade un agent.</span><span class="sxs-lookup"><span data-stu-id="f10f8-200">See hello next section tooupgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="f10f8-201">l’agent de Hello utilise IExpress comme son Self-extractor à l’aide de hello `/c` commande.</span><span class="sxs-lookup"><span data-stu-id="f10f8-201">hello agent uses IExpress as its self-extractor using hello `/c` command.</span></span> <span data-ttu-id="f10f8-202">Vous pouvez voir les commutateurs de ligne de commande hello [des commutateurs de ligne de commande pour IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) et puis mise à jour hello exemple toosuit vos besoins.</span><span class="sxs-lookup"><span data-stu-id="f10f8-202">You can see hello command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update hello example toosuit your needs.</span></span>

|<span data-ttu-id="f10f8-203">Options propres à MMA</span><span class="sxs-lookup"><span data-stu-id="f10f8-203">MMA-specific options</span></span>                   |<span data-ttu-id="f10f8-204">Remarques</span><span class="sxs-lookup"><span data-stu-id="f10f8-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="f10f8-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="f10f8-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="f10f8-206">1 = espace de travail de l’agent tooreport tooa configurer hello</span><span class="sxs-lookup"><span data-stu-id="f10f8-206">1 = Configure hello agent tooreport tooa workspace</span></span>                |
|<span data-ttu-id="f10f8-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="f10f8-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="f10f8-208">Espace de travail Id (guid) pour tooadd d’espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="f10f8-208">Workspace Id (guid) for hello workspace tooadd</span></span>                    |
|<span data-ttu-id="f10f8-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="f10f8-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="f10f8-210">Espace de travail de tooinitially utilisé clé s’authentifier avec un espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="f10f8-210">Workspace key used tooinitially authenticate with hello workspace</span></span> |
|<span data-ttu-id="f10f8-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="f10f8-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="f10f8-212">Spécifier l’environnement en nuage hello où se trouve espace de travail hello</span><span class="sxs-lookup"><span data-stu-id="f10f8-212">Specify hello cloud environment where hello workspace is located</span></span> <br> <span data-ttu-id="f10f8-213">0 = cloud commercial Azure (par défaut)</span><span class="sxs-lookup"><span data-stu-id="f10f8-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="f10f8-214">1 = Azure Government</span><span class="sxs-lookup"><span data-stu-id="f10f8-214">1 = Azure Government</span></span> |
|<span data-ttu-id="f10f8-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="f10f8-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="f10f8-216">URI pour hello proxy toouse</span><span class="sxs-lookup"><span data-stu-id="f10f8-216">URI for hello proxy toouse</span></span> |
|<span data-ttu-id="f10f8-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="f10f8-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="f10f8-218">Nom d’utilisateur tooaccess un proxy authentifié</span><span class="sxs-lookup"><span data-stu-id="f10f8-218">Username tooaccess an authenticated proxy</span></span> |
|<span data-ttu-id="f10f8-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="f10f8-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="f10f8-220">Mot de passe tooaccess un proxy authentifié</span><span class="sxs-lookup"><span data-stu-id="f10f8-220">Password tooaccess an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="f10f8-221">limite de longueur de ligne de commande de hello atteinte tooavoid de IExpress, installez l’agent de hello avec aucun espace de travail configuré, puis utilisez une configuration de tooset de script pour l’espace de travail hello.</span><span class="sxs-lookup"><span data-stu-id="f10f8-221">tooavoid hitting hello command-line length limit of IExpress, install hello agent with no workspace configured and then use a script tooset configuration for hello workspace.</span></span>

>[!NOTE]
<span data-ttu-id="f10f8-222">Si vous obtenez un `Command line option syntax error.` lors de l’utilisation de hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` paramètre, vous pouvez utiliser hello suivant la solution de contournement :</span><span class="sxs-lookup"><span data-stu-id="f10f8-222">If you get a `Command line option syntax error.` when using hello `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use hello following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="f10f8-223">Ajouter un espace de travail à l’aide d’un script</span><span class="sxs-lookup"><span data-stu-id="f10f8-223">Add a workspace using a script</span></span>
<span data-ttu-id="f10f8-224">Ajouter un espace de travail à l’aide des API de script de l’agent hello Analytique de journal avec hello l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="f10f8-224">Add a workspace using hello Log Analytics agent scripting API with hello following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="f10f8-225">tooadd un espace de travail dans Azure pour le gouvernement, hello utilisation suivant l’exemple de script :</span><span class="sxs-lookup"><span data-stu-id="f10f8-225">tooadd a workspace in Azure for US Government, use hello following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="f10f8-226">Si vous avez utilisé de ligne de commande hello ou un script précédemment tooinstall ou configurer l’agent hello, `EnableAzureOperationalInsights` a été remplacé par `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="f10f8-226">If you've used hello command line or script previously tooinstall or configure hello agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-hello-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="f10f8-227">Installer l’agent de hello à l’aide de DSC dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="f10f8-227">Install hello agent using DSC in Azure Automation</span></span>

<span data-ttu-id="f10f8-228">Vous pouvez utiliser hello suivant script exemple tooinstall hello l’agent à l’aide de DSC dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f10f8-228">You can use hello following script example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="f10f8-229">exemple Hello installe hello agent 64 bits, identifié par hello `URI` valeur.</span><span class="sxs-lookup"><span data-stu-id="f10f8-229">hello example installs hello 64-bit agent, identified by hello `URI` value.</span></span> <span data-ttu-id="f10f8-230">Vous pouvez également utiliser la version 32 bits de hello en remplaçant la valeur de l’URI hello.</span><span class="sxs-lookup"><span data-stu-id="f10f8-230">You can also use hello 32-bit version by replacing hello URI value.</span></span> <span data-ttu-id="f10f8-231">Hello URI pour les deux versions sont les suivantes :</span><span class="sxs-lookup"><span data-stu-id="f10f8-231">hello URIs for both versions are:</span></span>

- <span data-ttu-id="f10f8-232">Agent Windows 64 bits - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="f10f8-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="f10f8-233">Agent Windows 32 bits - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="f10f8-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="f10f8-234">Cette procédure et cet exemple de script ne mettent pas à niveau un agent existant.</span><span class="sxs-lookup"><span data-stu-id="f10f8-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="f10f8-235">Importer hello xPSDesiredStateConfiguration Module DSC de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f10f8-235">Import hello xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="f10f8-236">Créez des ressources variables Azure Automation pour *OPSINSIGHTS_WS_ID* et *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="f10f8-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="f10f8-237">Définissez *OPSINSIGHTS_WS_ID* ID d’espace de travail Analytique des journaux OMS tooyour et *OPSINSIGHTS_WS_KEY* toohello la clé primaire de votre espace de travail.</span><span class="sxs-lookup"><span data-stu-id="f10f8-237">Set *OPSINSIGHTS_WS_ID* tooyour OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* toohello primary key of your workspace.</span></span>
3.  <span data-ttu-id="f10f8-238">Utilisez hello suivants de script et l’enregistrement en tant que MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="f10f8-238">Use hello following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="f10f8-239">Modifier, puis utilisez hello suivant de l’agent hello exemple tooinstall à l’aide de DSC dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="f10f8-239">Modify and then use hello following example tooinstall hello agent using DSC in Azure Automation.</span></span> <span data-ttu-id="f10f8-240">Importer MMAgent.ps1 dans Azure Automation en utilisant l’interface d’Azure Automation hello ou l’applet de commande.</span><span class="sxs-lookup"><span data-stu-id="f10f8-240">Import MMAgent.ps1 into Azure Automation by using hello Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="f10f8-241">Attribuer une configuration toohello de nœud.</span><span class="sxs-lookup"><span data-stu-id="f10f8-241">Assign a node toohello configuration.</span></span> <span data-ttu-id="f10f8-242">Dans les 15 minutes, nœud de hello vérifie sa configuration et hello MMA est transmise toohello nœud.</span><span class="sxs-lookup"><span data-stu-id="f10f8-242">Within 15 minutes, hello node checks its configuration and hello MMA is pushed toohello node.</span></span>

```PowerShell
Configuration MMAgent
{
    $OIPackageLocalPath = "C:\MMASetup-AMD64.exe"
    $OPSINSIGHTS_WS_ID = Get-AutomationVariable -Name "OPSINSIGHTS_WS_ID"
    $OPSINSIGHTS_WS_KEY = Get-AutomationVariable -Name "OPSINSIGHTS_WS_KEY"


    Import-DscResource -ModuleName xPSDesiredStateConfiguration

    Node OMSnode {
        Service OIService
        {
            Name = "HealthService"
            State = "Running"
            DependsOn = "[Package]OI"
        }

        xRemoteFile OIPackage {
            Uri = "https://go.microsoft.com/fwlink/?LinkId=828603"
            DestinationPath = $OIPackageLocalPath
        }

        Package OI {
            Ensure = "Present"
            Path  = $OIPackageLocalPath
            Name = "Microsoft Monitoring Agent"
            ProductId = "8A7F2C51-4C7D-4BFD-9014-91D11F24AAE2"
            Arguments = '/C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=' + $OPSINSIGHTS_WS_ID + ' OPINSIGHTS_WORKSPACE_KEY=' + $OPSINSIGHTS_WS_KEY + ' AcceptEndUserLicenseAgreement=1"'
            DependsOn = "[xRemoteFile]OIPackage"
        }
    }
}


```

### <a name="get-hello-latest-productid-value"></a><span data-ttu-id="f10f8-243">Obtenir la dernière valeur de ProductId hello</span><span class="sxs-lookup"><span data-stu-id="f10f8-243">Get hello latest ProductId value</span></span>

<span data-ttu-id="f10f8-244">Hello `ProductId value` Bonjour MMAgent.ps1 script est la version de l’agent tooeach unique.</span><span class="sxs-lookup"><span data-stu-id="f10f8-244">hello `ProductId value` in hello MMAgent.ps1 script is unique tooeach agent version.</span></span> <span data-ttu-id="f10f8-245">Lorsqu’une version mise à jour de chaque agent est publiée, hello ProductId valeur change.</span><span class="sxs-lookup"><span data-stu-id="f10f8-245">When an updated version of each agent is published, hello ProductId value changes.</span></span> <span data-ttu-id="f10f8-246">Par conséquent, lorsqu’il modifie hello ProductId Bonjour futures, vous trouverez version de l’agent hello à l’aide d’un script simple.</span><span class="sxs-lookup"><span data-stu-id="f10f8-246">So, when hello ProductId changes in hello future, you can find hello agent version using a simple script.</span></span> <span data-ttu-id="f10f8-247">Après avoir configuré hello agent version la plus récente installée sur un serveur de test, vous pouvez utiliser hello script tooget hello installé ProductId valeur suivante.</span><span class="sxs-lookup"><span data-stu-id="f10f8-247">After you have hello latest agent version installed on a test server, you can use hello following script tooget hello installed ProductId value.</span></span> <span data-ttu-id="f10f8-248">À l’aide de la dernière valeur de ProductId hello, vous pouvez mettre à jour hello Bonjour MMAgent.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="f10f8-248">Using hello latest ProductId value, you can update hello value in hello MMAgent.ps1 script.</span></span>

```PowerShell
$InstalledApplications  = Get-ChildItem hklm:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall


foreach ($Application in $InstalledApplications)

{

     $Key = Get-ItemProperty $Application.PSPath

     if ($Key.DisplayName -eq "Microsoft Monitoring Agent")

     {

        $Key.DisplayName

        Write-Output ("Product ID is: " + $Key.PSChildName.Substring(1,$Key.PSChildName.Length -2))

     }

}  
```

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="f10f8-249">Configurer un agent manuellement ou ajouter des espaces de travail supplémentaires</span><span class="sxs-lookup"><span data-stu-id="f10f8-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="f10f8-250">Si vous avez installé les agents, mais n’a ne pas configuré les ou si vous souhaitez que les espaces de travail toomultiple hello agent tooreport, vous pouvez utiliser des hello suivant informations tooenable un agent ou le reconfigurer.</span><span class="sxs-lookup"><span data-stu-id="f10f8-250">If you've installed agents but did not configure them or if you want hello agent tooreport toomultiple workspaces, you can use hello following information tooenable an agent or reconfigure it.</span></span> <span data-ttu-id="f10f8-251">Une fois que vous avez configuré l’agent de hello, il s’inscrire auprès du service de l’agent de hello et obtenir des informations de configuration nécessaires et les packs d’administration qui contiennent des informations sur la solution.</span><span class="sxs-lookup"><span data-stu-id="f10f8-251">After you've configured hello agent, it will register with hello agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="f10f8-252">Une fois que vous avez installé hello Microsoft Monitoring Agent, ouvrez **le panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-252">After you've installed hello Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="f10f8-253">Ouvrez **Microsoft Monitoring Agent** puis cliquez sur hello **Analytique des journaux (OMS) Azure** onglet.</span><span class="sxs-lookup"><span data-stu-id="f10f8-253">Open **Microsoft Monitoring Agent** and then click hello **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="f10f8-254">Cliquez sur **ajouter** tooopen hello **ajouter un espace de travail Analytique de journal** boîte.</span><span class="sxs-lookup"><span data-stu-id="f10f8-254">Click **Add** tooopen hello **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="f10f8-255">Hello de coller **ID de l’espace de travail** et **clé de l’espace de travail (clé primaire)** que vous avez copié dans le bloc-notes dans une procédure précédente pour l’espace de travail hello que vous souhaitez tooadd, puis sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-255">Paste hello **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for hello workspace that you want tooadd and then click **OK**.</span></span>  
    <span data-ttu-id="f10f8-256">![configurer Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="f10f8-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="f10f8-257">Une fois que les données sont collectées à partir des ordinateurs analysés par agent de hello, nombre de hello d’ordinateurs analysés par OMS apparaît dans le portail OMS est hello sur hello **Sources connectées** onglet **paramètres** comme  **Serveurs connectés**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-257">After data is collected from computers monitored by hello agent, hello number of computers monitored by OMS will appear in hello OMS portal on hello **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="toodisable-an-agent"></a><span data-ttu-id="f10f8-258">toodisable un agent</span><span class="sxs-lookup"><span data-stu-id="f10f8-258">toodisable an agent</span></span>
1. <span data-ttu-id="f10f8-259">Après avoir installé l’agent de hello, ouvrez **le panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-259">After installing hello agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="f10f8-260">Ouvrez Microsoft Monitoring Agent, puis cliquez sur hello **Analytique des journaux (OMS) Azure** onglet.</span><span class="sxs-lookup"><span data-stu-id="f10f8-260">Open Microsoft Monitoring Agent and then click hello **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="f10f8-261">Sélectionnez un espace de travail, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="f10f8-262">Répétez cette étape pour tous les autres espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="f10f8-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="f10f8-263">Éventuellement, configurez le groupe d’administration Operations Manager agents tooreport tooan</span><span class="sxs-lookup"><span data-stu-id="f10f8-263">Optionally, configure agents tooreport tooan Operations Manager management group</span></span>

<span data-ttu-id="f10f8-264">Si vous utilisez Operations Manager dans votre infrastructure informatique, vous pouvez également utiliser l’agent de hello MMA comme un agent Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="f10f8-264">If you use Operations Manager in your IT infrastructure, you can also use hello MMA agent as an Operations Manager agent.</span></span>

### <a name="tooconfigure-mma-agents-tooreport-tooan-operations-manager-management-group"></a><span data-ttu-id="f10f8-265">groupe d’administration tooconfigure MMA agents tooreport tooan Operations Manager</span><span class="sxs-lookup"><span data-stu-id="f10f8-265">tooconfigure MMA agents tooreport tooan Operations Manager management group</span></span>
1.  <span data-ttu-id="f10f8-266">Sur ordinateur hello où hello agent est installé, ouvrez **le panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-266">On hello computer where hello agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="f10f8-267">Ouvrez **Microsoft Monitoring Agent** puis cliquez sur hello **Operations Manager** onglet.</span><span class="sxs-lookup"><span data-stu-id="f10f8-267">Open **Microsoft Monitoring Agent** and then click hello **Operations Manager** tab.</span></span>  
    <span data-ttu-id="f10f8-268">![onglet Operations Manager de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="f10f8-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="f10f8-269">Si vos serveurs Operations Manager sont intégrés à Active Directory, cliquez sur **Met à jour automatiquement les attributions du groupe d’administration à partir d’AD DS**.</span><span class="sxs-lookup"><span data-stu-id="f10f8-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="f10f8-270">Cliquez sur **ajouter** tooopen hello **ajouter un groupe d’administration** boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f10f8-270">Click **Add** tooopen hello **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="f10f8-271">![Microsoft Monitoring Agent Ajouter un groupe d’administration](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="f10f8-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="f10f8-272">Dans **nom de groupe d’administration** zone, entrez un nom hello de votre groupe d’administration.</span><span class="sxs-lookup"><span data-stu-id="f10f8-272">In **Management group name** box, type hello name of your management group.</span></span>
6.  <span data-ttu-id="f10f8-273">Bonjour **serveur d’administration principal** zone, le nom d’ordinateur de type hello hello principal du serveur d’administration.</span><span class="sxs-lookup"><span data-stu-id="f10f8-273">In hello **Primary management server** box, type hello computer name of hello primary management server.</span></span>
7.  <span data-ttu-id="f10f8-274">Bonjour **port serveur d’administration** zone, le numéro de port TCP de type hello.</span><span class="sxs-lookup"><span data-stu-id="f10f8-274">In hello **Management server port** box, type hello TCP port number.</span></span>
8.  <span data-ttu-id="f10f8-275">Sous **compte Action d’Agent**, choisissez le compte système Local de hello ou d’un compte de domaine local.</span><span class="sxs-lookup"><span data-stu-id="f10f8-275">Under **Agent Action Account**, choose either hello Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="f10f8-276">Cliquez sur **OK** tooclose hello **ajouter un groupe d’administration** boîte de dialogue, puis cliquez sur **OK** tooclose hello **Microsoft des propriétés de l’Agent d’analyse**boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="f10f8-276">Click **OK** tooclose hello **Add a Management Group** dialog box and then click **OK** tooclose hello **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="f10f8-277">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f10f8-277">Next steps</span></span>

- <span data-ttu-id="f10f8-278">[Ajouter des solutions d’Analytique de journal à partir de la galerie des Solutions de hello](log-analytics-add-solutions.md) tooadd fonctionnalité et collecter les données.</span><span class="sxs-lookup"><span data-stu-id="f10f8-278">[Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md) tooadd functionality and gather data.</span></span>
