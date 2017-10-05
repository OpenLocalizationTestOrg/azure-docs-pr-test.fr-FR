---
title: "Azure AD Connect sync : tâches et examen opérationnels | Microsoft Docs"
description: "Cette rubrique décrit les tâches opérationnelles de la synchronisation d’Azure AD Connect et explique comment se préparer pour utiliser ce composant."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: b29c1790-37a3-470f-ab69-3cee824d220d
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: b7583a1556bb1113f349a78890768451e39c6878
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="9f3ee-103">Azure Connect AD sync : tâches opérationnelles et examen</span><span class="sxs-lookup"><span data-stu-id="9f3ee-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="9f3ee-104">L’objectif de cette rubrique consiste à décrire les tâches opérationnelles de la synchronisation d’Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-104">The objective of this topic is to describe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="9f3ee-105">Mode intermédiaire</span><span class="sxs-lookup"><span data-stu-id="9f3ee-105">Staging mode</span></span>
<span data-ttu-id="9f3ee-106">Le mode intermédiaire peut être utilisé dans le cadre de plusieurs scénarios, notamment :</span><span class="sxs-lookup"><span data-stu-id="9f3ee-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="9f3ee-107">Haute disponibilité :</span><span class="sxs-lookup"><span data-stu-id="9f3ee-107">High availability.</span></span>
* <span data-ttu-id="9f3ee-108">Tester et déployer de nouvelles modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="9f3ee-109">Introduire un nouveau serveur et retirer l’ancien.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-109">Introduce a new server and decommission the old.</span></span>

<span data-ttu-id="9f3ee-110">Avec un serveur en mode intermédiaire, vous pouvez apporter des modifications à la configuration et visualiser les modifications avant de rendre le serveur actif.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-110">With a server in staging mode, you can make changes to the configuration and preview the changes before you make the server active.</span></span> <span data-ttu-id="9f3ee-111">Il permet également d’exécuter une importation et la synchronisation complètes afin de vérifier que toutes les modifications sont attendues avant de les appliquer dans un environnement de production.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-111">It also allows you to run full import and full synchronization to verify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="9f3ee-112">Lors de l’installation, vous pouvez sélectionner le serveur en **mode intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-112">During installation, you can select the server to be in **staging mode**.</span></span> <span data-ttu-id="9f3ee-113">Cette action rend le serveur actif pour l’importation et la synchronisation, mais n’exécute aucune exportation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-113">This action makes the server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="9f3ee-114">Un serveur en mode intermédiaire n’exécute pas la synchronisation de mot de passe et l’écriture différée de mot de passe même si vous avez sélectionné ces fonctions au cours de l’installation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="9f3ee-115">Lorsque vous désactivez le mode intermédiaire, le serveur lance l’exportation et active la synchronisation de mot de passe et l’écriture différée de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-115">When you disable staging mode, the server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="9f3ee-116">Vous pouvez toujours forcer une exportation en utilisant le gestionnaire de services de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-116">You can still force an export by using the synchronization service manager.</span></span>

<span data-ttu-id="9f3ee-117">Un serveur en mode intermédiaire continue de recevoir des modifications d’Active Directory et d’Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-117">A server in staging mode continues to receive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="9f3ee-118">Il dispose toujours d’une copie des modifications les plus récentes et peut très rapidement reprendre les responsabilités d’un autre serveur.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-118">It always has a copy of the latest changes and can very fast take over the responsibilities of another server.</span></span> <span data-ttu-id="9f3ee-119">Si vous apportez des modifications de configuration à votre serveur principal, la responsabilité d’apporter les mêmes modifications au serveur en mode intermédiaire vous incombe.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-119">If you make configuration changes to your primary server, it is your responsibility to make the same changes to the server in staging mode.</span></span>

<span data-ttu-id="9f3ee-120">Pour ceux qui connaissant les technologies de synchronisation plus anciennes, le mode intermédiaire est différent, dans la mesure où le serveur a sa propre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-120">For those of you with knowledge of older sync technologies, the staging mode is different since the server has its own SQL database.</span></span> <span data-ttu-id="9f3ee-121">Cette architecture permet au serveur en mode intermédiaire d’être situé dans un autre centre de données.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-121">This architecture allows the staging mode server to be located in a different datacenter.</span></span>

### <a name="verify-the-configuration-of-a-server"></a><span data-ttu-id="9f3ee-122">Vérifiez la configuration d’un serveur</span><span class="sxs-lookup"><span data-stu-id="9f3ee-122">Verify the configuration of a server</span></span>
<span data-ttu-id="9f3ee-123">Pour appliquer cette méthode, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="9f3ee-123">To apply this method, follow these steps:</span></span>

1. [<span data-ttu-id="9f3ee-124">Préparation</span><span class="sxs-lookup"><span data-stu-id="9f3ee-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="9f3ee-125">Configuration</span><span class="sxs-lookup"><span data-stu-id="9f3ee-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="9f3ee-126">Importer et synchroniser</span><span class="sxs-lookup"><span data-stu-id="9f3ee-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="9f3ee-127">Vérifier</span><span class="sxs-lookup"><span data-stu-id="9f3ee-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="9f3ee-128">Changer de serveur actif</span><span class="sxs-lookup"><span data-stu-id="9f3ee-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="9f3ee-129">Préparation</span><span class="sxs-lookup"><span data-stu-id="9f3ee-129">Prepare</span></span>
1. <span data-ttu-id="9f3ee-130">Installez Azure AD Connect, sélectionnez **mode intermédiaire**, puis désélectionnez **Démarrer la synchronisation** sur la dernière page de l’Assistant Installation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on the last page in the installation wizard.</span></span> <span data-ttu-id="9f3ee-131">Ce mode vous permet d’exécuter manuellement le moteur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-131">This mode allows you to run the sync engine manually.</span></span>
   <span data-ttu-id="9f3ee-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="9f3ee-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="9f3ee-133">Déconnectez-vous puis connectez-vous de nouveau et, dans le menu Démarrer, sélectionnez **Service de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-133">Sign off/sign in and from the start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="9f3ee-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="9f3ee-134">Configuration</span></span>
<span data-ttu-id="9f3ee-135">Si vous avez apporté des modifications personnalisées au serveur principal et que vous souhaitez comparer la configuration avec le serveur intermédiaire, utilisez la [Documentation de configuration d’Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="9f3ee-135">If you have made custom changes to the primary server and want to compare the configuration with the staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="9f3ee-136">Importer et synchroniser</span><span class="sxs-lookup"><span data-stu-id="9f3ee-136">Import and Synchronize</span></span>
1. <span data-ttu-id="9f3ee-137">Sélectionnez **Connecteurs**, puis sélectionnez le premier connecteur de type **Services de domaine Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-137">Select **Connectors**, and select the first Connector with the type **Active Directory Domain Services**.</span></span> <span data-ttu-id="9f3ee-138">Cliquez sur **Exécuter**, sélectionnez **Importation intégrale**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="9f3ee-139">Répétez cette procédure pour tous les connecteurs de ce type.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="9f3ee-140">Sélectionnez le connecteur de type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-140">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="9f3ee-141">Cliquez sur **Exécuter**, sélectionnez **Importation intégrale**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="9f3ee-142">Vérifiez que l’onglet Connecteurs est toujours sélectionné.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-142">Make sure the tab Connectors is still selected.</span></span> <span data-ttu-id="9f3ee-143">Pour chaque connecteur de type **Services de domaine Active Directory**, cliquez sur **Exécuter**, sélectionnez **Synchronisation Delta**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="9f3ee-144">Sélectionnez le connecteur de type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-144">Select the Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="9f3ee-145">Cliquez sur **Exécuter**, sélectionnez **Synchronisation Delta**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="9f3ee-146">Vous avez maintenant effectué une exportation intermédiaire vers Azure AD et Active Directory local (si vous utilisez un déploiement Exchange hybride).</span><span class="sxs-lookup"><span data-stu-id="9f3ee-146">You have now staged export changes to Azure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="9f3ee-147">Les prochaines étapes vous permettront d’inspecter les changements avant de commencer effectivement l’exportation vers les répertoires.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-147">The next steps allow you to inspect what is about to change before you actually start the export to the directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="9f3ee-148">Vérifier</span><span class="sxs-lookup"><span data-stu-id="9f3ee-148">Verify</span></span>
1. <span data-ttu-id="9f3ee-149">Démarrez une invite de commande et accédez à `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="9f3ee-149">Start a cmd prompt and go to `%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="9f3ee-150">Exécution : `csexport "Name of Connector" %temp%\export.xml /f:x` le nom du connecteur se trouve dans le service de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` The name of the Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="9f3ee-151">Le nom est similaire à « contoso.com – AAD » pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-151">It has a name similar to "contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="9f3ee-152">Copiez le script PowerShell à partir de la section [CSAnalyzer](#appendix-csanalyzer) dans un fichier nommé `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-152">Copy the PowerShell script from the section [CSAnalyzer](#appendix-csanalyzer) to a file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="9f3ee-153">Ouvrez une fenêtre PowerShell et accédez au dossier où vous avez créé le script PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-153">Open a PowerShell window and browse to the folder where you created the PowerShell script.</span></span>
5. <span data-ttu-id="9f3ee-154">Exécutez : `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="9f3ee-155">Vous disposez maintenant d’un fichier nommé **processedusers1.csv** qui peut être examiné dans Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="9f3ee-156">Toutes les modifications à exporter vers Azure AD sont trouvent dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-156">All changes staged to be exported to Azure AD are found in this file.</span></span>
7. <span data-ttu-id="9f3ee-157">Apportez les modifications nécessaires aux données ou à la configuration et réexécutez ces opérations (importer, synchroniser et vérifier) jusqu’à ce que les modifications sur le point d’être exportées soient attendues.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-157">Make necessary changes to the data or configuration and run these steps again (Import and Synchronize and Verify) until the changes that are about to be exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="9f3ee-158">Changer de serveur actif</span><span class="sxs-lookup"><span data-stu-id="9f3ee-158">Switch active server</span></span>
1. <span data-ttu-id="9f3ee-159">Sur le serveur actif, éteignez le serveur (DirSync/FIM/Azure AD Sync) pour qu’il ne soit pas exporté vers Azure AD ou définissez-le en mode intermédiaire (Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="9f3ee-159">On the currently active server, either turn off the server (DirSync/FIM/Azure AD Sync) so it is not exporting to Azure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="9f3ee-160">Exécutez l’Assistant Installation sur le serveur en **mode intermédiaire**, puis désactivez le **mode intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-160">Run the installation wizard on the server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="9f3ee-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="9f3ee-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="9f3ee-162">Récupération d'urgence</span><span class="sxs-lookup"><span data-stu-id="9f3ee-162">Disaster recovery</span></span>
<span data-ttu-id="9f3ee-163">Une partie de la conception de l’implémentation consiste à planifier les procédures à suivre si un sinistre occasionne la perte du serveur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-163">Part of the implementation design is to plan for what to do in case there is a disaster where you lose the sync server.</span></span> <span data-ttu-id="9f3ee-164">Il existe différents modèles et le choix de celui que vous devez utiliser dépend de plusieurs facteurs, notamment :</span><span class="sxs-lookup"><span data-stu-id="9f3ee-164">There are different models to use and which one to use depends on several factors including:</span></span>

* <span data-ttu-id="9f3ee-165">Dans quelle mesure pouvez-vous tolérer de ne pas pouvoir apporter des modifications aux objets dans Azure AD pendant les temps d’indisponibilité ?</span><span class="sxs-lookup"><span data-stu-id="9f3ee-165">What is your tolerance for not being able make changes to objects in Azure AD during the downtime?</span></span>
* <span data-ttu-id="9f3ee-166">Si vous utilisez la synchronisation de mot de passe, les utilisateurs acceptent-ils de devoir utiliser l’ancien mot de passe dans Azure AD dans le cas où il serait modifié en local ?</span><span class="sxs-lookup"><span data-stu-id="9f3ee-166">If you use password synchronization, do the users accept that they have to use the old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="9f3ee-167">Avez-vous une dépendance par rapport aux opérations en temps réel, notamment l’écriture différée de mot de passe ?</span><span class="sxs-lookup"><span data-stu-id="9f3ee-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="9f3ee-168">Selon les réponses à ces questions et la stratégie de votre organisation, une des stratégies suivantes peut être mise en œuvre :</span><span class="sxs-lookup"><span data-stu-id="9f3ee-168">Depending on the answers to these questions and your organization’s policy, one of the following strategies can be implemented:</span></span>

* <span data-ttu-id="9f3ee-169">Régénérer si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-169">Rebuild when needed.</span></span>
* <span data-ttu-id="9f3ee-170">Disposer d'un serveur de secours en attente, appelé **mode intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="9f3ee-171">Utiliser les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-171">Use virtual machines.</span></span>

<span data-ttu-id="9f3ee-172">Si vous n’utilisez pas la base de données SQL Express intégrée, vous devez vous reporter à la section [Haute disponibilité SQL](#sql-high-availability) .</span><span class="sxs-lookup"><span data-stu-id="9f3ee-172">If you do not use the built-in SQL Express database, then you should also review the [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="9f3ee-173">Régénérer lorsque nécessaire</span><span class="sxs-lookup"><span data-stu-id="9f3ee-173">Rebuild when needed</span></span>
<span data-ttu-id="9f3ee-174">Une stratégie viable consiste à planifier une régénération du serveur si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-174">A viable strategy is to plan for a server rebuild when needed.</span></span> <span data-ttu-id="9f3ee-175">Généralement, l’installation du moteur de synchronisation et l’exécution de l’importation et de la synchronisation initiales peuvent être effectuées en quelques heures.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-175">Usually, installing the sync engine and do the initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="9f3ee-176">Si aucun serveur n’est libre, il est possible d’utiliser provisoirement un contrôleur de domaine pour héberger le moteur de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-176">If there isn’t a spare server available, it is possible to temporarily use a domain controller to host the sync engine.</span></span>

<span data-ttu-id="9f3ee-177">Le serveur de moteur de synchronisation ne stocke aucun état relatif aux objets de sorte que la base de données peut être recréée à partir des données présentes dans Active Directory et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-177">The sync engine server does not store any state about the objects so the database can be rebuilt from the data in Active Directory and Azure AD.</span></span> <span data-ttu-id="9f3ee-178">L’attribut **sourceAnchor** est utilisé pour associer les objets à partir du site et du cloud.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-178">The **sourceAnchor** attribute is used to join the objects from on-premises and the cloud.</span></span> <span data-ttu-id="9f3ee-179">Si vous régénérez le serveur avec les objets existants en local et sur le cloud, le moteur de synchronisation les remet en correspondance de nouveau au cours de la réinstallation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-179">If you rebuild the server with existing objects on-premises and the cloud, then the sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="9f3ee-180">Vous devez documenter et enregistrer les modifications de configuration apportées au serveur, notamment aux règles de filtrage et de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-180">The things you need to document and save are the configuration changes made to the server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="9f3ee-181">Ces configurations personnalisées doivent être réappliquées avant de commencer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="9f3ee-182">Disposer d’un serveur de secours en attente, connu sous le nom de mode intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="9f3ee-183">Si vous disposez d’un environnement plus complexe, il est recommandé d’avoir un ou plusieurs serveurs de secours.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="9f3ee-184">Lors de l’installation, vous pouvez activer un serveur en **mode intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-184">During installation, you can enable a server to be in **staging mode**.</span></span>

<span data-ttu-id="9f3ee-185">Pour en savoir plus, voir [Mode intermédiaire](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="9f3ee-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="9f3ee-186">Utiliser les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="9f3ee-186">Use virtual machines</span></span>
<span data-ttu-id="9f3ee-187">Une méthode courante et prise en charge consiste à exécuter le moteur de synchronisation sur une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-187">A common and supported method is to run the sync engine in a virtual machine.</span></span> <span data-ttu-id="9f3ee-188">Si l’hôte rencontre un problème, l’image contenant le serveur de moteur de synchronisation peut être migrée vers un autre serveur.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-188">In case the host has an issue, the image with the sync engine server can be migrated to another server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="9f3ee-189">Haute disponibilité SQL</span><span class="sxs-lookup"><span data-stu-id="9f3ee-189">SQL High Availability</span></span>
<span data-ttu-id="9f3ee-190">Si vous n’utilisez pas SQL Server Express livré avec Azure AD Connect, la haute disponibilité pour SQL Server doit alors être prise en compte.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-190">If you are not using the SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="9f3ee-191">Les solutions de haute disponibilité prises en charge incluent la mise en clusters SQL et AOA (Groupes de disponibilité AlwaysOn).</span><span class="sxs-lookup"><span data-stu-id="9f3ee-191">The high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="9f3ee-192">Les solutions non prises en charge incluent la mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="9f3ee-193">La prise en charge de SQL AOA a été ajoutée à Azure AD Connect version 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-193">Support for SQL AOA was added to Azure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="9f3ee-194">Vous devez activer SQL AOA avant d’installer Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="9f3ee-195">Pendant l’installation, Azure AD Connect détecte si l’instance SQL spécifiée est activée ou non pour SQL AOA.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-195">During installation, Azure AD Connect detects whether the SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="9f3ee-196">Si SQL AOA est activé, Azure AD Connect détermine si SQL AOA est configuré pour utiliser une réplication synchrone ou asynchrone.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured to use synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="9f3ee-197">Lorsque vous configurez l’écouteur de groupe de disponibilité, il est recommandé de définir la propriété RegisterAllProvidersIP sur 0.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-197">When setting up the Availability Group Listener, it is recommended that you set the RegisterAllProvidersIP property to 0.</span></span> <span data-ttu-id="9f3ee-198">En effet, Azure AD Connect utilise actuellement SQL Native Client pour se connecter à SQL, et SQL Native Client ne prend pas en charge l’utilisation de la propriété MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-198">This is because Azure AD Connect currently uses SQL Native Client to connect to SQL and SQL Native Client does not support the use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="9f3ee-199">Annexe CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="9f3ee-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="9f3ee-200">Consultez la section [vérifier](#verify) pour découvrir comment utiliser ce script.</span><span class="sxs-lookup"><span data-stu-id="9f3ee-200">See the section [verify](#verify) on how to use this script.</span></span>

```
Param(
    [Parameter(Mandatory=$true, HelpMessage="Must be a file generated using csexport 'Name of Connector' export.xml /f:x)")]
    [string]$xmltoimport="%temp%\exportedStage1a.xml",
    [Parameter(Mandatory=$false, HelpMessage="Maximum number of users per output file")][int]$batchsize=1000,
    [Parameter(Mandatory=$false, HelpMessage="Show console output")][bool]$showOutput=$false
)

#LINQ isn't loaded automatically, so force it
[Reflection.Assembly]::Load("System.Xml.Linq, Version=3.5.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089") | Out-Null

[int]$count=1
[int]$outputfilecount=1
[array]$objOutputUsers=@()

#XML must be generated using "csexport "Name of Connector" export.xml /f:x"
write-host "Importing XML" -ForegroundColor Yellow

#XmlReader.Create won't properly resolve the file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader to deal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create the object placeholder
    #adding them up here means we can enforce consistency
    $objOutputUser=New-Object psobject
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name ID -Value ""
    Add-Member -InputObject $objOutputUser -MemberType NoteProperty -Name Type -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name DN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name operation -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name UPN -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name displayName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name sourceAnchor -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name alias -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name primarySMTP -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name onPremisesSamAccountName -Value ""
    Add-Member -inputobject $objOutputUser -MemberType NoteProperty -Name mail -Value ""

    $user = [System.Xml.Linq.XElement]::ReadFrom($reader)
    if ($showOutput) {Write-Host Found an exported object... -ForegroundColor Green}

    #object id
    $outID=$user.Attribute('id').Value
    if ($showOutput) {Write-Host ID: $outID}
    $objOutputUser.ID=$outID

    #object type
    $outType=$user.Attribute('object-type').Value
    if ($showOutput) {Write-Host Type: $outType}
    $objOutputUser.Type=$outType

    #dn
    $outDN= $user.Element('unapplied-export').Element('delta').Attribute('dn').Value
    if ($showOutput) {Write-Host DN: $outDN}
    $objOutputUser.DN=$outDN

    #operation
    $outOperation= $user.Element('unapplied-export').Element('delta').Attribute('operation').Value
    if ($showOutput) {Write-Host Operation: $outOperation}
    $objOutputUser.operation=$outOperation

    #now that we have the basics, go get the details

    foreach ($attr in $user.Element('unapplied-export-hologram').Element('entry').Elements("attr"))
    {
        $attrvalue=$attr.Attribute('name').Value
        $internalvalue= $attr.Element('value').Value

        switch ($attrvalue)
        {
            "userPrincipalName"
            {
                if ($showOutput) {Write-Host UPN: $internalvalue}
                $objOutputUser.UPN=$internalvalue
            }
            "displayName"
            {
                if ($showOutput) {Write-Host displayName: $internalvalue}
                $objOutputUser.displayName=$internalvalue
            }
            "sourceAnchor"
            {
                if ($showOutput) {Write-Host sourceAnchor: $internalvalue}
                $objOutputUser.sourceAnchor=$internalvalue
            }
            "alias"
            {
                if ($showOutput) {Write-Host alias: $internalvalue}
                $objOutputUser.alias=$internalvalue
            }
            "proxyAddresses"
            {
                if ($showOutput) {Write-Host primarySMTP: ($internalvalue -replace "SMTP:","")}
                $objOutputUser.primarySMTP=$internalvalue -replace "SMTP:",""
            }
        }
    }

    $objOutputUsers += $objOutputUser

    Write-Progress -activity "Processing ${xmltoimport} in batches of ${batchsize}" -status "Batch ${outputfilecount}: " -percentComplete (($objOutputUsers.Count / $batchsize) * 100)

    #every so often, dump the processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit the maximum users processed without completion... -ForegroundColor Yellow

        #export the collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment the output file counter
        $outputfilecount+=1

        #reset the collection and the user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need to bail out of the loop if no more users to process
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need to write out any users that didn't get picked up in a batch of 1000
#export the collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="9f3ee-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9f3ee-201">Next steps</span></span>
<span data-ttu-id="9f3ee-202">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="9f3ee-202">**Overview topics**</span></span>  

* [<span data-ttu-id="9f3ee-203">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="9f3ee-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="9f3ee-204">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9f3ee-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
