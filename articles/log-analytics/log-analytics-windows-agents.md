---
title: "Connecter des ordinateurs Windows à Azure Log Analytics | Microsoft Docs"
description: "Cet article décrit les étapes à suivre pour connecter directement au service Log Analytics les ordinateurs Windows de votre infrastructure locale en utilisant une version personnalisée de Microsoft Monitoring Agent (MMA)."
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
ms.openlocfilehash: 48a0eaeb10d406d551c9e5870edde06809bd7544
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-windows-computers-to-the-log-analytics-service-in-azure"></a><span data-ttu-id="e5220-103">Connecter des ordinateurs Windows au service Log Analytics dans Azure</span><span class="sxs-lookup"><span data-stu-id="e5220-103">Connect Windows computers to the Log Analytics service in Azure</span></span>

<span data-ttu-id="e5220-104">Cet article décrit les étapes à suivre pour connecter à des espaces de travail OMS les ordinateurs Windows de votre infrastructure locale en utilisant une version personnalisée de Microsoft Monitoring Agent (MMA).</span><span class="sxs-lookup"><span data-stu-id="e5220-104">This article shows the steps to connect Windows computers in your on-premises infrastructure to OMS workspaces by using a customized version of the Microsoft Monitoring Agent (MMA).</span></span> <span data-ttu-id="e5220-105">Vous devez installer et connecter les agents pour tous les ordinateurs que vous souhaitez intégrer afin qu’ils puissent envoyer des données au service Log Analytics, puis les afficher et agir sur ces données.</span><span class="sxs-lookup"><span data-stu-id="e5220-105">You need to install and connect agents for all of the computers that you want to onboard in order for them to send data to the Log Analytics service and to view and act on that data.</span></span> <span data-ttu-id="e5220-106">Chaque agent peut fournir des rapports à plusieurs espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="e5220-106">Each agent can report to multiple workspaces.</span></span>

<span data-ttu-id="e5220-107">Vous pouvez installer des agents à l’aide du programme d’installation, de la ligne de commande, ou de la fonction Desired State Configuration (DSC) d’Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5220-107">You can install agents using Setup, command line, or with Desired State Configuration (DSC) in Azure Automation.</span></span>  

>[!NOTE]
<span data-ttu-id="e5220-108">Pour les machines virtuelles s’exécutant dans Azure, vous pouvez simplifier l’installation à l’aide de l’[extension de machine virtuelle](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e5220-108">For virtual machines running in Azure, you can simplify installation by using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="e5220-109">Sur les ordinateurs disposant d’une connexion à Internet, l’agent utilise cette dernière pour envoyer des données à OMS.</span><span class="sxs-lookup"><span data-stu-id="e5220-109">On computers with Internet connectivity, the agent uses the connection to the Internet to send data to OMS.</span></span> <span data-ttu-id="e5220-110">Pour les ordinateurs qui ne disposent pas de connectivité Internet, vous pouvez utiliser un serveur proxy ou la [passerelle OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="e5220-110">For computers that do not have Internet connectivity, you can use a proxy or the [OMS Gateway](log-analytics-oms-gateway.md).</span></span>

<span data-ttu-id="e5220-111">Vous pouvez connecter très simplement vos ordinateurs Windows à OMS en 3 étapes :</span><span class="sxs-lookup"><span data-stu-id="e5220-111">Connecting your Windows computers to OMS is straightforward using three simple steps:</span></span>

1. <span data-ttu-id="e5220-112">Télécharger le fichier de configuration de l’agent sur le portail OMS</span><span class="sxs-lookup"><span data-stu-id="e5220-112">Download the agent setup file from the OMS portal</span></span>
2. <span data-ttu-id="e5220-113">Installer l’agent selon la méthode de votre choix</span><span class="sxs-lookup"><span data-stu-id="e5220-113">Install the agent using the method you choose</span></span>
3. <span data-ttu-id="e5220-114">Configurer l’agent ou ajouter des espaces de travail supplémentaires, si nécessaire</span><span class="sxs-lookup"><span data-stu-id="e5220-114">Configure the agent or add additional workspaces, if necessary</span></span>

<span data-ttu-id="e5220-115">Le schéma suivant illustre la relation entre vos ordinateurs Windows et OMS après installation et configuration des agents.</span><span class="sxs-lookup"><span data-stu-id="e5220-115">The following diagram shows the relationship between your Windows computers and OMS after you’ve installed and configured agents.</span></span>

![oms-direct-agent-diagram](./media/log-analytics-windows-agents/oms-direct-agent-diagram.png)

<span data-ttu-id="e5220-117">Si vos stratégies de sécurité informatique n’autorisent pas les ordinateurs de votre réseau à se connecter à Internet, vous pouvez configurer vos ordinateurs pour qu’ils se connectent à la passerelle OMS.</span><span class="sxs-lookup"><span data-stu-id="e5220-117">If your IT security policies do not allow computers on your network to connect to the Internet, you can configure your computers to connect to the OMS Gateway.</span></span> <span data-ttu-id="e5220-118">Pour plus d’informations et pour savoir comment configurer vos serveurs pour qu’ils communiquent par le biais d’une passerelle OMS avec le service OMS, consultez [Connecter des ordinateurs à OMS en utilisant la passerelle OMS](log-analytics-oms-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="e5220-118">For more information and steps on how to configure your servers to communicate through an OMS Gateway to the OMS service, see [Connect computers to OMS using the OMS Gateway](log-analytics-oms-gateway.md).</span></span>

## <a name="system-requirements-and-required-configuration"></a><span data-ttu-id="e5220-119">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="e5220-119">System requirements and required configuration</span></span>
<span data-ttu-id="e5220-120">Avant d’installer ou de déployer des agents, passez en revue les informations suivantes afin d’avoir la certitude de répondre aux conditions requises.</span><span class="sxs-lookup"><span data-stu-id="e5220-120">Before you install or deploy agents, review the following details to ensure you meet the requirements.</span></span>

- <span data-ttu-id="e5220-121">Vous ne pouvez installer OMS MMA que sur les ordinateurs fonctionnant sous Windows Server 2008 SP 1 ou version ultérieure ou sous Windows 7 SP1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="e5220-121">You can only install the OMS MMA on computers running Windows Server 2008 SP 1 or later or Windows 7 SP1 or later.</span></span>
- <span data-ttu-id="e5220-122">Vous avez besoin d’un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="e5220-122">You need an Azure subscription.</span></span>  <span data-ttu-id="e5220-123">Pour plus d’informations, consultez l’article [Prise en main de Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e5220-123">For more information, see [Get started with Log Analytics](log-analytics-get-started.md).</span></span>
- <span data-ttu-id="e5220-124">Chaque ordinateur Windows doit pouvoir se connecter à Internet à l’aide du protocole HTTPS ou de la passerelle OMS.</span><span class="sxs-lookup"><span data-stu-id="e5220-124">Each Windows computer must be able to connect to the Internet using HTTPS or to the OMS Gateway.</span></span> <span data-ttu-id="e5220-125">Il peut s’agir d’une connexion directe, d’une connexion obtenue par un proxy ou bien établie via la passerelle OMS.</span><span class="sxs-lookup"><span data-stu-id="e5220-125">This connection can be direct, via a proxy, or through the OMS Gateway.</span></span>
- <span data-ttu-id="e5220-126">Vous pouvez installer OMS MMA sur des ordinateurs autonomes, des serveurs et des machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e5220-126">You can install the OMS MMA on stand-alone computers, servers, and virtual machines.</span></span> <span data-ttu-id="e5220-127">Si vous souhaitez connecter à OMS des machines virtuelles hébergées dans Azure, voir [Connecter des machines virtuelles Azure à Log Analytics](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="e5220-127">If you want to connect Azure-hosted virtual machines to OMS, see [Connect Azure virtual machines to Log Analytics](log-analytics-azure-vm-extension.md).</span></span>
- <span data-ttu-id="e5220-128">L’agent doit utiliser le port TCP 443 pour les différentes ressources.</span><span class="sxs-lookup"><span data-stu-id="e5220-128">The agent needs to use TCP port 443 for various resources.</span></span>

### <a name="network"></a><span data-ttu-id="e5220-129">Réseau</span><span class="sxs-lookup"><span data-stu-id="e5220-129">Network</span></span>

<span data-ttu-id="e5220-130">Pour que les agents Windows se connectent et s’inscrivent auprès du service OMS, ils doivent accéder aux ressources réseau, y compris les numéros de port et les URL de domaine.</span><span class="sxs-lookup"><span data-stu-id="e5220-130">For Windows agents to connect to and register with the OMS service, they must have access to network resources, including the port numbers and domain URLs.</span></span>

- <span data-ttu-id="e5220-131">Pour les serveurs proxy, vous devez vous assurer que les ressources de serveur proxy appropriées sont configurées dans les paramètres de l’agent.</span><span class="sxs-lookup"><span data-stu-id="e5220-131">For proxy servers, you need to ensure that the appropriate proxy server resources are configured in agent settings.</span></span>
- <span data-ttu-id="e5220-132">Pour les pare-feu qui limitent l’accès à Internet, vous ou vos ingénieurs réseau devez configurer votre pare-feu pour qu’il autorise l’accès à OMS.</span><span class="sxs-lookup"><span data-stu-id="e5220-132">For firewalls that restrict access to the Internet, you or your networking engineers need to configure your firewall to permit access to OMS.</span></span> <span data-ttu-id="e5220-133">Aucune action n’est nécessaire dans les paramètres de l’agent.</span><span class="sxs-lookup"><span data-stu-id="e5220-133">No action is needed in agent settings.</span></span>

<span data-ttu-id="e5220-134">Le tableau suivant présente les ressources nécessaires pour la communication.</span><span class="sxs-lookup"><span data-stu-id="e5220-134">The following table shows resources needed for communication.</span></span>

>[!NOTE]
><span data-ttu-id="e5220-135">Certaines des ressources suivantes mentionnent Operational Insights, qui est l’ancien nom de Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e5220-135">Some of the following resources mention Operational Insights, which was a previous name for Log Analytics.</span></span>

| <span data-ttu-id="e5220-136">Ressource de l'agent</span><span class="sxs-lookup"><span data-stu-id="e5220-136">Agent Resource</span></span> | <span data-ttu-id="e5220-137">Ports</span><span class="sxs-lookup"><span data-stu-id="e5220-137">Ports</span></span> | <span data-ttu-id="e5220-138">Ignorer l’inspection HTTPS</span><span class="sxs-lookup"><span data-stu-id="e5220-138">Bypass HTTPS inspection</span></span> |
|---|---|---|
| <span data-ttu-id="e5220-139">*.ods.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e5220-139">*.ods.opinsights.azure.com</span></span> | <span data-ttu-id="e5220-140">443</span><span class="sxs-lookup"><span data-stu-id="e5220-140">443</span></span> | <span data-ttu-id="e5220-141">Oui</span><span class="sxs-lookup"><span data-stu-id="e5220-141">Yes</span></span> |
| <span data-ttu-id="e5220-142">*.oms.opinsights.azure.com</span><span class="sxs-lookup"><span data-stu-id="e5220-142">*.oms.opinsights.azure.com</span></span> | <span data-ttu-id="e5220-143">443</span><span class="sxs-lookup"><span data-stu-id="e5220-143">443</span></span> | <span data-ttu-id="e5220-144">Oui</span><span class="sxs-lookup"><span data-stu-id="e5220-144">Yes</span></span> |
| <span data-ttu-id="e5220-145">*.blob.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="e5220-145">*.blob.core.windows.net</span></span> | <span data-ttu-id="e5220-146">443</span><span class="sxs-lookup"><span data-stu-id="e5220-146">443</span></span> | <span data-ttu-id="e5220-147">Oui</span><span class="sxs-lookup"><span data-stu-id="e5220-147">Yes</span></span> |
| <span data-ttu-id="e5220-148">*.azure-automation.net</span><span class="sxs-lookup"><span data-stu-id="e5220-148">*.azure-automation.net</span></span> | <span data-ttu-id="e5220-149">443</span><span class="sxs-lookup"><span data-stu-id="e5220-149">443</span></span> | <span data-ttu-id="e5220-150">Oui</span><span class="sxs-lookup"><span data-stu-id="e5220-150">Yes</span></span> |



## <a name="download-the-agent-setup-file-from-oms"></a><span data-ttu-id="e5220-151">Télécharger le fichier de configuration de l’agent sur OMS</span><span class="sxs-lookup"><span data-stu-id="e5220-151">Download the agent setup file from OMS</span></span>
1. <span data-ttu-id="e5220-152">Dans le portail OMS, sur la page **Vue d’ensemble**, cliquez sur la mosaïque **Paramètres**.</span><span class="sxs-lookup"><span data-stu-id="e5220-152">In the OMS portal, on the **Overview** page, click the **Settings** tile.</span></span>  <span data-ttu-id="e5220-153">Cliquez sur l’onglet **Sources connectées** , situé en haut de la page.</span><span class="sxs-lookup"><span data-stu-id="e5220-153">Click the **Connected Sources** tab at the top.</span></span>  
    <span data-ttu-id="e5220-154">![onglet Sources connectées](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span><span class="sxs-lookup"><span data-stu-id="e5220-154">![Connected Sources tab](./media/log-analytics-windows-agents/oms-direct-agent-connected-sources.png)</span></span>
2. <span data-ttu-id="e5220-155">Cliquez sur **Serveurs Windows**, puis sur **Télécharger l’Agent Windows** correspondant au type de processeur de votre ordinateur pour télécharger le fichier d’installation.</span><span class="sxs-lookup"><span data-stu-id="e5220-155">Click **Windows Servers** and then click **Download Windows Agent** applicable to your computer processor type to download the setup file.</span></span>
3. <span data-ttu-id="e5220-156">À droite du champ **ID de l’espace de travail**, cliquez sur l’icône de copie et collez l’ID dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e5220-156">On the right of **Workspace ID**, click the copy icon and paste the ID into Notepad.</span></span>
4. <span data-ttu-id="e5220-157">À droite du champ **Clé primaire**, cliquez sur l’icône de copie et collez la clé dans le Bloc-notes.</span><span class="sxs-lookup"><span data-stu-id="e5220-157">On the right of **Primary Key**, click the copy icon and paste the key into Notepad.</span></span>     

## <a name="install-the-agent-using-setup"></a><span data-ttu-id="e5220-158">Installation de l’agent à l’aide du programme d’installation</span><span class="sxs-lookup"><span data-stu-id="e5220-158">Install the agent using setup</span></span>
1. <span data-ttu-id="e5220-159">Exécutez le programme d’installation pour installer l’agent sur un ordinateur que vous souhaitez gérer.</span><span class="sxs-lookup"><span data-stu-id="e5220-159">Run Setup to install the agent on a computer that you want to manage.</span></span>
2. <span data-ttu-id="e5220-160">Sur la page d'accueil, cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5220-160">On the Welcome page, click **Next**.</span></span>
3. <span data-ttu-id="e5220-161">Dans la page Termes du contrat de licence, lisez les conditions de licence et cliquez sur **J’accepte**.</span><span class="sxs-lookup"><span data-stu-id="e5220-161">On the License Terms page, read the license and then click **I Agree**.</span></span>
4. <span data-ttu-id="e5220-162">Dans la page Dossier de destination, modifiez ou conservez le dossier d’installation par défaut, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5220-162">On the Destination Folder page, change or keep the default installation folder and then click **Next**.</span></span>
5. <span data-ttu-id="e5220-163">Dans la page Options d’installation de l’Agent, vous pouvez soit connecter l’agent à Azure Log Analytics (OMS) ou à Operations Manager, soit laisser les options vides si vous souhaitez configurer l’agent ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="e5220-163">On the Agent Setup Options page, you can choose to connect the agent to Azure Log Analytics (OMS), Operations Manager, or you can leave the choices blank if you want to configure the agent later.</span></span> <span data-ttu-id="e5220-164">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5220-164">Click **Next**.</span></span>   
    - <span data-ttu-id="e5220-165">Si vous choisissez de vous connecter à Azure Log Analytics (OMS), collez l’**ID de l’espace de travail** et la **Clé de l’espace de travail (clé primaire)** que vous avez copiés dans le bloc-notes dans la procédure précédente, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5220-165">If you chose to connect to Azure Log Analytics (OMS), paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in the previous procedure and then click **Next**.</span></span>  
        <span data-ttu-id="e5220-166">![Coller l’ID et la clé primaire de l’espace de travail](./media/log-analytics-windows-agents/connect-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="e5220-166">![paste Workspace ID and Primary Key](./media/log-analytics-windows-agents/connect-workspace.png)</span></span>
    - <span data-ttu-id="e5220-167">Si vous choisissez de vous connecter à Operations Manager, saisissez le **Nom du groupe d’administration**, le nom du **Serveur d’administration** et le **Port du serveur d’administration**, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5220-167">If you chose to connect to Operations Manager, type the **Management Group Name**, **Management Server** name, and **Management Server Port**, and then click **Next**.</span></span> <span data-ttu-id="e5220-168">Sur la page Compte d’action d’agent, choisissez le compte système local ou un compte de domaine local, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="e5220-168">On the Agent Action Account page, choose either the Local System account or a local domain account and then click **Next**.</span></span>  
        <span data-ttu-id="e5220-169">![Configuration du groupe d’administration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![compte d’action d’agent](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span><span class="sxs-lookup"><span data-stu-id="e5220-169">![management group configuration](./media/log-analytics-windows-agents/oms-mma-om-setup01.png)![agent action account](./media/log-analytics-windows-agents/oms-mma-om-setup02.png)</span></span>

6. <span data-ttu-id="e5220-170">Sur la page Prêt pour l’installation, passez en revue vos choix, puis cliquez sur **Installer**.</span><span class="sxs-lookup"><span data-stu-id="e5220-170">On the Ready to Install page, review your choices and then click **Install**.</span></span>
7. <span data-ttu-id="e5220-171">Sur la page Configuration effectuée, cliquez sur **Terminer**.</span><span class="sxs-lookup"><span data-stu-id="e5220-171">On the Configuration completed successfully page, click **Finish**.</span></span>
8. <span data-ttu-id="e5220-172">Lorsque vous avez terminé, **Microsoft Monitoring Agent** apparaît dans le **Panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="e5220-172">When complete, the **Microsoft Monitoring Agent** appears in **Control Panel**.</span></span> <span data-ttu-id="e5220-173">Vous pouvez y contrôler votre configuration et vérifier que l’agent est bien connecté à Operational Insights (OMS).</span><span class="sxs-lookup"><span data-stu-id="e5220-173">You can review your configuration there and verify that the agent is connected to Operational Insights (OMS).</span></span> <span data-ttu-id="e5220-174">Une fois connecté à OMS, l’agent affiche un message indiquant : **Microsoft Monitoring Agent est bien connecté au service Microsoft Operations Management Suite**</span><span class="sxs-lookup"><span data-stu-id="e5220-174">When connected to OMS, the agent displays a message stating: **The Microsoft Monitoring Agent has successfully connected to the Microsoft Operations Management Suite service.**</span></span>

## <a name="configure-proxy-settings"></a><span data-ttu-id="e5220-175">Configuration des paramètres de proxy</span><span class="sxs-lookup"><span data-stu-id="e5220-175">Configure proxy settings</span></span>

<span data-ttu-id="e5220-176">Vous pouvez utiliser la procédure suivante pour configurer les paramètres de proxy de Microsoft Monitoring Agent dans le Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="e5220-176">You can use the following procedure to configure proxy settings for the Microsoft Monitoring Agent using Control Panel.</span></span> <span data-ttu-id="e5220-177">Vous devez utiliser cette procédure pour chaque serveur.</span><span class="sxs-lookup"><span data-stu-id="e5220-177">You need to use this procedure for each server.</span></span> <span data-ttu-id="e5220-178">Si vous devez configurer plusieurs serveurs, utilisez un script pour automatiser ce processus.</span><span class="sxs-lookup"><span data-stu-id="e5220-178">If you have many servers that you need to configure, you might find it easier to use a script to automate this process.</span></span> <span data-ttu-id="e5220-179">Dans ce cas, suivez la procédure [Pour configurer les paramètres de proxy de Microsoft Monitoring Agent à l'aide d'un script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span><span class="sxs-lookup"><span data-stu-id="e5220-179">If so, see the next procedure [To configure proxy settings for the Microsoft Monitoring Agent using a script](#to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script).</span></span>

### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-control-panel"></a><span data-ttu-id="e5220-180">Pour configurer les paramètres de proxy de Microsoft Monitoring Agent dans le Panneau de configuration</span><span class="sxs-lookup"><span data-stu-id="e5220-180">To configure proxy settings for the Microsoft Monitoring Agent using Control Panel</span></span>
1. <span data-ttu-id="e5220-181">Ouvrez le **Panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="e5220-181">Open **Control Panel**.</span></span>
2. <span data-ttu-id="e5220-182">Ouvrez **Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="e5220-182">Open **Microsoft Monitoring Agent**.</span></span>
3. <span data-ttu-id="e5220-183">Cliquez sur l'onglet **Paramètres de proxy** .</span><span class="sxs-lookup"><span data-stu-id="e5220-183">Click the **Proxy Settings** tab.</span></span>  
    <span data-ttu-id="e5220-184">![Onglet Paramètres de proxy](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span><span class="sxs-lookup"><span data-stu-id="e5220-184">![proxy settings tab](./media/log-analytics-windows-agents/proxy-direct-agent-proxy.png)</span></span>
4. <span data-ttu-id="e5220-185">Sélectionnez **Utiliser un serveur proxy** et tapez l'URL et le numéro de port, si nécessaire, comme indiqué dans l'exemple.</span><span class="sxs-lookup"><span data-stu-id="e5220-185">Select **Use a proxy server** and type the URL and port number, if one is needed, similar to the example shown.</span></span> <span data-ttu-id="e5220-186">Si votre serveur proxy requiert une authentification, tapez le nom d'utilisateur et le mot de passe pour accéder au serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="e5220-186">If your proxy server requires authentication, type the username and password to access the proxy server.</span></span>


### <a name="verify-agent-connectivity-to-oms"></a><span data-ttu-id="e5220-187">Vérifier la connectivité de l’agent à OMS</span><span class="sxs-lookup"><span data-stu-id="e5220-187">Verify agent connectivity to OMS</span></span>

<span data-ttu-id="e5220-188">Vous pouvez facilement vérifier si vos agents communiquent avec OMS en procédant comme suit :</span><span class="sxs-lookup"><span data-stu-id="e5220-188">You can easily verify whether your agents are communicating with OMS using the following procedure:</span></span>

1.  <span data-ttu-id="e5220-189">Sur l’ordinateur sur lequel l’agent Windows est installé, ouvrez le Panneau de configuration.</span><span class="sxs-lookup"><span data-stu-id="e5220-189">On the computer with the Windows agent, open Control Panel.</span></span>
2.  <span data-ttu-id="e5220-190">Ouvrez Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="e5220-190">Open Microsoft Monitoring Agent.</span></span>
3.  <span data-ttu-id="e5220-191">Cliquez sur l’onglet Azure Log Analytics (OMS).</span><span class="sxs-lookup"><span data-stu-id="e5220-191">Click the Azure Log Analytics (OMS) tab.</span></span>
4.  <span data-ttu-id="e5220-192">Dans la colonne État, vous devez voir que l’agent est correctement connecté au service Operations Management Suite.</span><span class="sxs-lookup"><span data-stu-id="e5220-192">In the Status column, you should see that the agent connected successfully to the Operations Management Suite service.</span></span>

![agent connecté](./media/log-analytics-windows-agents/mma-connected.png)


### <a name="to-configure-proxy-settings-for-the-microsoft-monitoring-agent-using-a-script"></a><span data-ttu-id="e5220-194">Pour configurer les paramètres de proxy de Microsoft Monitoring Agent à l'aide d'un script</span><span class="sxs-lookup"><span data-stu-id="e5220-194">To configure proxy settings for the Microsoft Monitoring Agent using a script</span></span>
<span data-ttu-id="e5220-195">Copiez l'exemple suivant, mettez-le à jour avec les informations spécifiques à votre environnement, enregistrez-le avec l'extension de nom de fichier PS1, puis exécutez le script sur chaque ordinateur qui se connecte directement au service OMS.</span><span class="sxs-lookup"><span data-stu-id="e5220-195">Copy the following sample, update it with information specific to your environment, save it with a PS1 file name extension, and then run the script on each computer that connects directly to the OMS service.</span></span>

    param($ProxyDomainName="http://proxy.contoso.com:80", $cred=(Get-Credential))

    # First we get the Health Service configuration object.  We need to determine if we
    #have the right update rollup with the API we need.  If not, no need to run the rest of the script.
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

    Write-Output "Setting proxy to $ProxyDomainName with proxy username $ProxyUserName."
    $healthServiceSettings.SetProxyInfo($ProxyDomainName, $ProxyUserName, $cred.GetNetworkCredential().password)



## <a name="install-the-agent-using-the-command-line"></a><span data-ttu-id="e5220-196">Installation de l’agent à l’aide de la ligne de commande</span><span class="sxs-lookup"><span data-stu-id="e5220-196">Install the agent using the command line</span></span>
- <span data-ttu-id="e5220-197">Modifiez, puis utilisez l’exemple suivant pour installer l’agent à l’aide de la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="e5220-197">Modify and then use the following example to install the agent using the command line.</span></span> <span data-ttu-id="e5220-198">L’exemple effectue une installation entièrement sans assistance.</span><span class="sxs-lookup"><span data-stu-id="e5220-198">The example performs a fully silent installation.</span></span>

    >[!NOTE]
    <span data-ttu-id="e5220-199">Si vous souhaitez mettre à niveau un agent, vous devez utiliser l’API de script Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="e5220-199">If you want to upgrade an agent, you need to use the Log Analytics scripting API.</span></span> <span data-ttu-id="e5220-200">Pour mettre à niveau un agent, consultez la section suivante.</span><span class="sxs-lookup"><span data-stu-id="e5220-200">See the next section to upgrade an agent.</span></span>

    ```dos
    MMASetup-AMD64.exe /Q:A /R:N /C:"setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1"
    ```

<span data-ttu-id="e5220-201">L’agent utilise IExpress comme son auto-extracteur à l’aide de la commande `/c`.</span><span class="sxs-lookup"><span data-stu-id="e5220-201">The agent uses IExpress as its self-extractor using the `/c` command.</span></span> <span data-ttu-id="e5220-202">Vous pouvez voir les commutateurs de ligne de commande à la page [Commutateurs de ligne de commande pour les packages de mise à jour logicielle IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages), puis mettre à jour l’exemple pour répondre à vos besoins.</span><span class="sxs-lookup"><span data-stu-id="e5220-202">You can see the command-line switches at [Command-line switches for IExpress](https://support.microsoft.com/help/197147/command-line-switches-for-iexpress-software-update-packages) and then update the example to suit your needs.</span></span>

|<span data-ttu-id="e5220-203">Options propres à MMA</span><span class="sxs-lookup"><span data-stu-id="e5220-203">MMA-specific options</span></span>                   |<span data-ttu-id="e5220-204">Remarques</span><span class="sxs-lookup"><span data-stu-id="e5220-204">Notes</span></span>         |
|---------------------------------------|--------------|
|<span data-ttu-id="e5220-205">ADD_OPINSIGHTS_WORKSPACE</span><span class="sxs-lookup"><span data-stu-id="e5220-205">ADD_OPINSIGHTS_WORKSPACE</span></span>               | <span data-ttu-id="e5220-206">1 = Configurer l’agent de façon à ce qu’il se connecte à un espace de travail</span><span class="sxs-lookup"><span data-stu-id="e5220-206">1 = Configure the agent to report to a workspace</span></span>                |
|<span data-ttu-id="e5220-207">OPINSIGHTS_WORKSPACE_ID</span><span class="sxs-lookup"><span data-stu-id="e5220-207">OPINSIGHTS_WORKSPACE_ID</span></span>                | <span data-ttu-id="e5220-208">ID d’espace de travail (GUID) de l’espace de travail à ajouter</span><span class="sxs-lookup"><span data-stu-id="e5220-208">Workspace Id (guid) for the workspace to add</span></span>                    |
|<span data-ttu-id="e5220-209">OPINSIGHTS_WORKSPACE_KEY</span><span class="sxs-lookup"><span data-stu-id="e5220-209">OPINSIGHTS_WORKSPACE_KEY</span></span>               | <span data-ttu-id="e5220-210">Clé d’espace de travail utilisée initialement pour l’authentification auprès de l’espace de travail</span><span class="sxs-lookup"><span data-stu-id="e5220-210">Workspace key used to initially authenticate with the workspace</span></span> |
|<span data-ttu-id="e5220-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span><span class="sxs-lookup"><span data-stu-id="e5220-211">OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE</span></span>  | <span data-ttu-id="e5220-212">Spécifie l’environnement cloud où se trouve l’espace de travail</span><span class="sxs-lookup"><span data-stu-id="e5220-212">Specify the cloud environment where the workspace is located</span></span> <br> <span data-ttu-id="e5220-213">0 = cloud commercial Azure (par défaut)</span><span class="sxs-lookup"><span data-stu-id="e5220-213">0 = Azure commercial cloud (default)</span></span> <br> <span data-ttu-id="e5220-214">1 = Azure Government</span><span class="sxs-lookup"><span data-stu-id="e5220-214">1 = Azure Government</span></span> |
|<span data-ttu-id="e5220-215">OPINSIGHTS_PROXY_URL</span><span class="sxs-lookup"><span data-stu-id="e5220-215">OPINSIGHTS_PROXY_URL</span></span>               | <span data-ttu-id="e5220-216">URI du proxy à utiliser</span><span class="sxs-lookup"><span data-stu-id="e5220-216">URI for the proxy to use</span></span> |
|<span data-ttu-id="e5220-217">OPINSIGHTS_PROXY_USERNAME</span><span class="sxs-lookup"><span data-stu-id="e5220-217">OPINSIGHTS_PROXY_USERNAME</span></span>               | <span data-ttu-id="e5220-218">Nom d’utilisateur permettant d’accéder à un proxy authentifié</span><span class="sxs-lookup"><span data-stu-id="e5220-218">Username to access an authenticated proxy</span></span> |
|<span data-ttu-id="e5220-219">OPINSIGHTS_PROXY_PASSWORD</span><span class="sxs-lookup"><span data-stu-id="e5220-219">OPINSIGHTS_PROXY_PASSWORD</span></span>               | <span data-ttu-id="e5220-220">Mot de passe permettant d’accéder à un proxy authentifié</span><span class="sxs-lookup"><span data-stu-id="e5220-220">Password to access an authenticated proxy</span></span> |

>[!NOTE]
<span data-ttu-id="e5220-221">Pour éviter d’atteindre la limite de longueur de ligne de commande d’IExpress, installez l’agent sans aucun espace de travail configuré et utilisez un script pour définir la configuration de l’espace de travail.</span><span class="sxs-lookup"><span data-stu-id="e5220-221">To avoid hitting the command-line length limit of IExpress, install the agent with no workspace configured and then use a script to set configuration for the workspace.</span></span>

>[!NOTE]
<span data-ttu-id="e5220-222">Si vous obtenez `Command line option syntax error.` lors de l’utilisation du paramètre `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE`, vous pouvez utiliser la solution de contournement suivante :</span><span class="sxs-lookup"><span data-stu-id="e5220-222">If you get a `Command line option syntax error.` when using the `OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE` parameter, you can use the following workaround:</span></span>
```dos
MMASetup-AMD64.exe /C /T:.\MMAExtract
cd .\MMAExtract
setup.exe /qn ADD_OPINSIGHTS_WORKSPACE=1 OPINSIGHTS_WORKSPACE_AZURE_CLOUD_TYPE=1 OPINSIGHTS_WORKSPACE_ID=<your workspace id> OPINSIGHTS_WORKSPACE_KEY=<your workspace key> AcceptEndUserLicenseAgreement=1
```

## <a name="add-a-workspace-using-a-script"></a><span data-ttu-id="e5220-223">Ajouter un espace de travail à l’aide d’un script</span><span class="sxs-lookup"><span data-stu-id="e5220-223">Add a workspace using a script</span></span>
<span data-ttu-id="e5220-224">Ajoutez un espace de travail à l’aide de l’API de script de l’agent Log Analytics avec l’exemple suivant :</span><span class="sxs-lookup"><span data-stu-id="e5220-224">Add a workspace using the Log Analytics agent scripting API with the following example:</span></span>

```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey)
$mma.ReloadConfiguration()
```

<span data-ttu-id="e5220-225">Pour ajouter un espace de travail dans Azure pour US Government, utilisez l’exemple de script suivant :</span><span class="sxs-lookup"><span data-stu-id="e5220-225">To add a workspace in Azure for US Government, use the following script sample:</span></span>
```PowerShell
$mma = New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg'
$mma.AddCloudWorkspace($workspaceId, $workspaceKey, 1)
$mma.ReloadConfiguration()
```

>[!NOTE]
<span data-ttu-id="e5220-226">Si vous avez utilisé précédemment la ligne de commande ou un script pour installer ou configurer l’agent, `EnableAzureOperationalInsights` a été remplacé par `AddCloudWorkspace`.</span><span class="sxs-lookup"><span data-stu-id="e5220-226">If you've used the command line or script previously to install or configure the agent, `EnableAzureOperationalInsights` was replaced by `AddCloudWorkspace`.</span></span>

## <a name="install-the-agent-using-dsc-in-azure-automation"></a><span data-ttu-id="e5220-227">Installer l’agent à l’aide de DSC dans Azure Automation</span><span class="sxs-lookup"><span data-stu-id="e5220-227">Install the agent using DSC in Azure Automation</span></span>

<span data-ttu-id="e5220-228">Vous pouvez utiliser l’exemple de script suivant pour installer l’agent à l’aide de DSC dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5220-228">You can use the following script example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="e5220-229">L’exemple installe l’agent 64 bits, identifié par la valeur `URI`.</span><span class="sxs-lookup"><span data-stu-id="e5220-229">The example installs the 64-bit agent, identified by the `URI` value.</span></span> <span data-ttu-id="e5220-230">Vous pouvez également utiliser la version 32 bits en remplaçant la valeur de l’URI.</span><span class="sxs-lookup"><span data-stu-id="e5220-230">You can also use the 32-bit version by replacing the URI value.</span></span> <span data-ttu-id="e5220-231">Les URI pour les deux versions sont :</span><span class="sxs-lookup"><span data-stu-id="e5220-231">The URIs for both versions are:</span></span>

- <span data-ttu-id="e5220-232">Agent Windows 64 bits - https://go.microsoft.com/fwlink/?LinkId=828603</span><span class="sxs-lookup"><span data-stu-id="e5220-232">Windows 64-bit agent - https://go.microsoft.com/fwlink/?LinkId=828603</span></span>
- <span data-ttu-id="e5220-233">Agent Windows 32 bits - https://go.microsoft.com/fwlink/?LinkId=828604</span><span class="sxs-lookup"><span data-stu-id="e5220-233">Windows 32-bit agent - https://go.microsoft.com/fwlink/?LinkId=828604</span></span>


>[!NOTE]
<span data-ttu-id="e5220-234">Cette procédure et cet exemple de script ne mettent pas à niveau un agent existant.</span><span class="sxs-lookup"><span data-stu-id="e5220-234">This procedure and script example will not upgrade an existing agent.</span></span>

1. <span data-ttu-id="e5220-235">Importez le module DSC xPSDesiredStateConfiguration à partir de [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5220-235">Import the xPSDesiredStateConfiguration DSC Module from [http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration](http://www.powershellgallery.com/packages/xPSDesiredStateConfiguration) into Azure Automation.</span></span>  
2.  <span data-ttu-id="e5220-236">Créez des ressources variables Azure Automation pour *OPSINSIGHTS_WS_ID* et *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="e5220-236">Create Azure Automation variable assets for *OPSINSIGHTS_WS_ID* and *OPSINSIGHTS_WS_KEY*.</span></span> <span data-ttu-id="e5220-237">Affectez votre ID d’espace de travail OMS Log Analytics comme valeur *OPSINSIGHTS_WS_ID* et affectez la clé primaire de votre espace de travail comme valeur *OPSINSIGHTS_WS_KEY*.</span><span class="sxs-lookup"><span data-stu-id="e5220-237">Set *OPSINSIGHTS_WS_ID* to your OMS Log Analytics workspace ID and set *OPSINSIGHTS_WS_KEY* to the primary key of your workspace.</span></span>
3.  <span data-ttu-id="e5220-238">Utilisez le script suivant et enregistrez-le sous le nom MMAgent.ps1</span><span class="sxs-lookup"><span data-stu-id="e5220-238">Use the following script and save it as MMAgent.ps1</span></span>
4.  <span data-ttu-id="e5220-239">Modifiez puis utilisez l’exemple suivant pour installer l’agent à l’aide de DSC dans Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5220-239">Modify and then use the following example to install the agent using DSC in Azure Automation.</span></span> <span data-ttu-id="e5220-240">Importez MMAgent.ps1 dans Azure Automation à l’aide de l’interface ou de l’applet de commande Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="e5220-240">Import MMAgent.ps1 into Azure Automation by using the Azure Automation interface or cmdlet.</span></span>
5.  <span data-ttu-id="e5220-241">Affectez un nœud à la configuration.</span><span class="sxs-lookup"><span data-stu-id="e5220-241">Assign a node to the configuration.</span></span> <span data-ttu-id="e5220-242">En moins de 15 minutes, le nœud vérifie sa configuration et l’agent MMA est poussé vers le nœud.</span><span class="sxs-lookup"><span data-stu-id="e5220-242">Within 15 minutes, the node checks its configuration and the MMA is pushed to the node.</span></span>

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

### <a name="get-the-latest-productid-value"></a><span data-ttu-id="e5220-243">Obtention de la dernière valeur de ProductId</span><span class="sxs-lookup"><span data-stu-id="e5220-243">Get the latest ProductId value</span></span>

<span data-ttu-id="e5220-244">La `ProductId value` dans le script MMAgent.ps1 est propre à chaque version de l’agent.</span><span class="sxs-lookup"><span data-stu-id="e5220-244">The `ProductId value` in the MMAgent.ps1 script is unique to each agent version.</span></span> <span data-ttu-id="e5220-245">Lorsqu’une version mise à jour de chaque agent est publiée, la valeur ProductId change.</span><span class="sxs-lookup"><span data-stu-id="e5220-245">When an updated version of each agent is published, the ProductId value changes.</span></span> <span data-ttu-id="e5220-246">Par conséquent, lors du changement de la valeur ProductId à l’avenir, vous trouverez la version de l’agent à l’aide d’un script simple.</span><span class="sxs-lookup"><span data-stu-id="e5220-246">So, when the ProductId changes in the future, you can find the agent version using a simple script.</span></span> <span data-ttu-id="e5220-247">Une fois la dernière version de l’agent installée sur un serveur de test, vous pouvez utiliser le script suivant pour obtenir la valeur ProductId installée.</span><span class="sxs-lookup"><span data-stu-id="e5220-247">After you have the latest agent version installed on a test server, you can use the following script to get the installed ProductId value.</span></span> <span data-ttu-id="e5220-248">À l’aide de la dernière valeur ProductId, vous pouvez mettre à jour la valeur dans le script MMAgent.ps1.</span><span class="sxs-lookup"><span data-stu-id="e5220-248">Using the latest ProductId value, you can update the value in the MMAgent.ps1 script.</span></span>

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

## <a name="configure-an-agent-manually-or-add-additional-workspaces"></a><span data-ttu-id="e5220-249">Configurer un agent manuellement ou ajouter des espaces de travail supplémentaires</span><span class="sxs-lookup"><span data-stu-id="e5220-249">Configure an agent manually or add additional workspaces</span></span>
<span data-ttu-id="e5220-250">Si vous avez installé des agents mais que vous ne les avez pas configurés, ou si vous souhaitez que l’agent fournisse des rapports à plusieurs espaces de travail, vous pouvez utiliser les informations suivantes pour activer un agent ou le reconfigurer.</span><span class="sxs-lookup"><span data-stu-id="e5220-250">If you've installed agents but did not configure them or if you want the agent to report to multiple workspaces, you can use the following information to enable an agent or reconfigure it.</span></span> <span data-ttu-id="e5220-251">Une fois que vous avez configuré l’agent, il s’inscrira auprès du service de l’agent et obtiendra les informations de configuration nécessaires, ainsi que les packs d’administration contenant les informations de la solution.</span><span class="sxs-lookup"><span data-stu-id="e5220-251">After you've configured the agent, it will register with the agent service and will get necessary configuration information and management packs that contain solution information.</span></span>

1. <span data-ttu-id="e5220-252">Après avoir installé l’agent Microsoft Monitoring Agent, ouvrez le **Panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="e5220-252">After you've installed the Microsoft Monitoring Agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="e5220-253">Ouvrez l’agent **Microsoft Monitoring Agent**, puis cliquez sur l’onglet **Azure Log Analytics (OMS)**.</span><span class="sxs-lookup"><span data-stu-id="e5220-253">Open **Microsoft Monitoring Agent** and then click the **Azure Log Analytics (OMS)** tab.</span></span>   
3. <span data-ttu-id="e5220-254">Cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Ajouter un espace de travail Log Analytics**.</span><span class="sxs-lookup"><span data-stu-id="e5220-254">Click **Add** to open the **Add a Log Analytics Workspace** box.</span></span>
4. <span data-ttu-id="e5220-255">Collez l’**ID de l’espace de travail** et la **Clé de l’espace de travail (clé primaire)** que vous avez copiés dans le bloc-notes au cours d’une étape précédente pour l’espace de travail que vous souhaitez ajouter, puis cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="e5220-255">Paste the **Workspace ID** and **Workspace Key (Primary Key)** that you copied into Notepad in a previous procedure for the workspace that you want to add and then click **OK**.</span></span>  
    <span data-ttu-id="e5220-256">![Configurer Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span><span class="sxs-lookup"><span data-stu-id="e5220-256">![configure Operational Insights](./media/log-analytics-windows-agents/add-workspace.png)</span></span>

<span data-ttu-id="e5220-257">Une fois que les données des ordinateurs analysés ont été collectées par l’agent, le nombre d’ordinateurs analysés par OMS apparaît dans le portail OMS sous l’onglet **Sources connectées**, dans **Paramètres**, sous **Serveurs connectés**.</span><span class="sxs-lookup"><span data-stu-id="e5220-257">After data is collected from computers monitored by the agent, the number of computers monitored by OMS will appear in the OMS portal on the **Connected Sources** tab in **Settings** as **Servers Connected**.</span></span>


## <a name="to-disable-an-agent"></a><span data-ttu-id="e5220-258">Désactivation d’un agent</span><span class="sxs-lookup"><span data-stu-id="e5220-258">To disable an agent</span></span>
1. <span data-ttu-id="e5220-259">Après avoir installé l’agent, ouvrez le **Panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="e5220-259">After installing the agent, open **Control Panel**.</span></span>
2. <span data-ttu-id="e5220-260">Ouvrez l’agent Microsoft Monitoring Agent, puis cliquez sur l’onglet **Azure Log Analytics (OMS)** .</span><span class="sxs-lookup"><span data-stu-id="e5220-260">Open Microsoft Monitoring Agent and then click the **Azure Log Analytics (OMS)** tab.</span></span>
3. <span data-ttu-id="e5220-261">Sélectionnez un espace de travail, puis cliquez sur **Supprimer**.</span><span class="sxs-lookup"><span data-stu-id="e5220-261">Select a workspace and then click **Remove**.</span></span> <span data-ttu-id="e5220-262">Répétez cette étape pour tous les autres espaces de travail.</span><span class="sxs-lookup"><span data-stu-id="e5220-262">Repeat this step for all other workspaces.</span></span>


## <a name="optionally-configure-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="e5220-263">Vous pouvez éventuellement configurer les agents pour émettre des rapports dans un groupe d’administration Operations Manager</span><span class="sxs-lookup"><span data-stu-id="e5220-263">Optionally, configure agents to report to an Operations Manager management group</span></span>

<span data-ttu-id="e5220-264">Si vous utilisez Operations Manager dans votre infrastructure informatique, vous pouvez également utiliser l’agent MMA en tant qu’agent Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="e5220-264">If you use Operations Manager in your IT infrastructure, you can also use the MMA agent as an Operations Manager agent.</span></span>

### <a name="to-configure-mma-agents-to-report-to-an-operations-manager-management-group"></a><span data-ttu-id="e5220-265">Configurer les agents afin qu’ils émettent des rapports dans un groupe d’administration Operations Manager</span><span class="sxs-lookup"><span data-stu-id="e5220-265">To configure MMA agents to report to an Operations Manager management group</span></span>
1.  <span data-ttu-id="e5220-266">Sur l’ordinateur sur lequel l’agent est installé, ouvrez le **Panneau de configuration**.</span><span class="sxs-lookup"><span data-stu-id="e5220-266">On the computer where the agent is installed, open **Control Panel**.</span></span>  
2.  <span data-ttu-id="e5220-267">Ouvrez l’agent **Microsoft Monitoring Agent**, puis cliquez sur l’onglet **Operations Manager**.</span><span class="sxs-lookup"><span data-stu-id="e5220-267">Open **Microsoft Monitoring Agent** and then click the **Operations Manager** tab.</span></span>  
    <span data-ttu-id="e5220-268">![onglet Operations Manager de Microsoft Monitoring Agent](./media/log-analytics-windows-agents/om-mg01.png)</span><span class="sxs-lookup"><span data-stu-id="e5220-268">![Microsoft Monitoring Agent Operations Manager tab](./media/log-analytics-windows-agents/om-mg01.png)</span></span>
3.  <span data-ttu-id="e5220-269">Si vos serveurs Operations Manager sont intégrés à Active Directory, cliquez sur **Met à jour automatiquement les attributions du groupe d’administration à partir d’AD DS**.</span><span class="sxs-lookup"><span data-stu-id="e5220-269">If your Operations Manager servers have integration with Active Directory, click **Automatically update management group assignments from AD DS**.</span></span>
4.  <span data-ttu-id="e5220-270">Cliquez sur **Ajouter** pour ouvrir la boîte de dialogue **Ajouter un groupe d’administration**.</span><span class="sxs-lookup"><span data-stu-id="e5220-270">Click **Add** to open the **Add a Management Group** dialog box.</span></span>  
    <span data-ttu-id="e5220-271">![Microsoft Monitoring Agent Ajouter un groupe d’administration](./media/log-analytics-windows-agents/oms-mma-om02.png)</span><span class="sxs-lookup"><span data-stu-id="e5220-271">![Microsoft Monitoring Agent Add a Management Group](./media/log-analytics-windows-agents/oms-mma-om02.png)</span></span>
5.  <span data-ttu-id="e5220-272">Dans la zone **Nom du groupe d’administration** , entrez le nom de votre groupe d’administration.</span><span class="sxs-lookup"><span data-stu-id="e5220-272">In **Management group name** box, type the name of your management group.</span></span>
6.  <span data-ttu-id="e5220-273">Dans la zone **Serveur d’administration principal** , entrez le nom d’ordinateur du serveur d’administration principal.</span><span class="sxs-lookup"><span data-stu-id="e5220-273">In the **Primary management server** box, type the computer name of the primary management server.</span></span>
7.  <span data-ttu-id="e5220-274">Dans la zone **Port du serveur d’administration** , entrez le numéro de port TCP.</span><span class="sxs-lookup"><span data-stu-id="e5220-274">In the **Management server port** box, type the TCP port number.</span></span>
8.  <span data-ttu-id="e5220-275">Sous **Compte d’action d’agent**, choisissez le compte système local ou un compte de domaine local.</span><span class="sxs-lookup"><span data-stu-id="e5220-275">Under **Agent Action Account**, choose either the Local System account or a local domain account.</span></span>
9.  <span data-ttu-id="e5220-276">Cliquez sur **OK** pour fermer la boîte de dialogue **Ajouter un groupe d’administration**, puis cliquez sur **OK** pour fermer la boîte de dialogue **Propriétés de l’agent Microsoft Monitoring Agent**.</span><span class="sxs-lookup"><span data-stu-id="e5220-276">Click **OK** to close the **Add a Management Group** dialog box and then click **OK** to close the **Microsoft Monitoring Agent Properties** dialog box.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e5220-277">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e5220-277">Next steps</span></span>

- <span data-ttu-id="e5220-278">[Ajoutez des solutions Log Analytics à partir de la galerie de solutions](log-analytics-add-solutions.md) pour ajouter des fonctionnalités et collecter des données.</span><span class="sxs-lookup"><span data-stu-id="e5220-278">[Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md) to add functionality and gather data.</span></span>
