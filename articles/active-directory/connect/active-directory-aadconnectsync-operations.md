---
title: "Azure AD Connect sync : tâches et examen opérationnels | Microsoft Docs"
description: "Cette rubrique décrit les tâches opérationnelles pour la synchronisation Azure AD Connect et comment tooprepare pour l’exploitation de ce composant."
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
ms.openlocfilehash: e6b21262e0924785808888d66f08a04a56581edc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-operational-tasks-and-consideration"></a><span data-ttu-id="e31a4-103">Azure Connect AD sync : tâches opérationnelles et examen</span><span class="sxs-lookup"><span data-stu-id="e31a4-103">Azure AD Connect sync: Operational tasks and consideration</span></span>
<span data-ttu-id="e31a4-104">objectif Hello de cette rubrique est toodescribe des tâches opérationnelles pour la synchronisation Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e31a4-104">hello objective of this topic is toodescribe operational tasks for Azure AD Connect sync.</span></span>

## <a name="staging-mode"></a><span data-ttu-id="e31a4-105">Mode intermédiaire</span><span class="sxs-lookup"><span data-stu-id="e31a4-105">Staging mode</span></span>
<span data-ttu-id="e31a4-106">Le mode intermédiaire peut être utilisé dans le cadre de plusieurs scénarios, notamment :</span><span class="sxs-lookup"><span data-stu-id="e31a4-106">Staging mode can be used for several scenarios, including:</span></span>

* <span data-ttu-id="e31a4-107">Haute disponibilité :</span><span class="sxs-lookup"><span data-stu-id="e31a4-107">High availability.</span></span>
* <span data-ttu-id="e31a4-108">Tester et déployer de nouvelles modifications de configuration.</span><span class="sxs-lookup"><span data-stu-id="e31a4-108">Test and deploy new configuration changes.</span></span>
* <span data-ttu-id="e31a4-109">Introduire un nouveau serveur et retirer hello ancien.</span><span class="sxs-lookup"><span data-stu-id="e31a4-109">Introduce a new server and decommission hello old.</span></span>

<span data-ttu-id="e31a4-110">Avec un serveur en mode de préproduction, vous pouvez modifier modifications toohello configuration et l’aperçu hello avant d’apporter les serveur hello active.</span><span class="sxs-lookup"><span data-stu-id="e31a4-110">With a server in staging mode, you can make changes toohello configuration and preview hello changes before you make hello server active.</span></span> <span data-ttu-id="e31a4-111">Il vous permet également de l’importation intégrale toorun et tooverify de synchronisation complète que toutes les modifications sont censées avant d’apporter ces modifications dans votre environnement de production.</span><span class="sxs-lookup"><span data-stu-id="e31a4-111">It also allows you toorun full import and full synchronization tooverify that all changes are expected before you make these changes into your production environment.</span></span>

<span data-ttu-id="e31a4-112">Pendant l’installation, vous pouvez sélectionner toobe de serveur hello dans **mode de préproduction**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-112">During installation, you can select hello server toobe in **staging mode**.</span></span> <span data-ttu-id="e31a4-113">Cette action permet de serveur de hello active pour l’importation et synchronisation, mais il ne s’exécute pas des exportations.</span><span class="sxs-lookup"><span data-stu-id="e31a4-113">This action makes hello server active for import and synchronization, but it does not run any exports.</span></span> <span data-ttu-id="e31a4-114">Un serveur en mode intermédiaire n’exécute pas la synchronisation de mot de passe et l’écriture différée de mot de passe même si vous avez sélectionné ces fonctions au cours de l’installation.</span><span class="sxs-lookup"><span data-stu-id="e31a4-114">A server in staging mode is not running password sync or password writeback, even if you selected these features during installation.</span></span> <span data-ttu-id="e31a4-115">Lorsque vous désactivez le mode de préproduction, hello server lance l’exportation, permet la synchronisation de mot de passe et l’écriture différée de mot de passe.</span><span class="sxs-lookup"><span data-stu-id="e31a4-115">When you disable staging mode, hello server starts exporting, enables password sync, and enables password writeback.</span></span>

<span data-ttu-id="e31a4-116">Vous pouvez toujours forcer une exportation à l’aide du Gestionnaire de service de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="e31a4-116">You can still force an export by using hello synchronization service manager.</span></span>

<span data-ttu-id="e31a4-117">Un serveur en mode de mise en lots continue tooreceive des modifications à partir d’Active Directory et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e31a4-117">A server in staging mode continues tooreceive changes from Active Directory and Azure AD.</span></span> <span data-ttu-id="e31a4-118">Il a toujours une copie des modifications les plus récentes hello et peuvent durer de très rapide sur les responsabilités hello d’un autre serveur.</span><span class="sxs-lookup"><span data-stu-id="e31a4-118">It always has a copy of hello latest changes and can very fast take over hello responsibilities of another server.</span></span> <span data-ttu-id="e31a4-119">Si vous effectuez le serveur principal de configuration modifications tooyour, il est toomake de votre responsabilité hello même serveur toohello de modifications dans le mode de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="e31a4-119">If you make configuration changes tooyour primary server, it is your responsibility toomake hello same changes toohello server in staging mode.</span></span>

<span data-ttu-id="e31a4-120">Pour ceux avec des connaissances des technologies plus anciennes de synchronisation, hello en mode de mise en lots est différent, car le serveur de hello possède sa propre base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="e31a4-120">For those of you with knowledge of older sync technologies, hello staging mode is different since hello server has its own SQL database.</span></span> <span data-ttu-id="e31a4-121">Cette architecture permet hello mode toobe de serveur situé dans un autre centre de données de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="e31a4-121">This architecture allows hello staging mode server toobe located in a different datacenter.</span></span>

### <a name="verify-hello-configuration-of-a-server"></a><span data-ttu-id="e31a4-122">Vérifier la configuration d’un serveur de hello</span><span class="sxs-lookup"><span data-stu-id="e31a4-122">Verify hello configuration of a server</span></span>
<span data-ttu-id="e31a4-123">tooapply cette méthode, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="e31a4-123">tooapply this method, follow these steps:</span></span>

1. [<span data-ttu-id="e31a4-124">Préparation</span><span class="sxs-lookup"><span data-stu-id="e31a4-124">Prepare</span></span>](#prepare)
2. [<span data-ttu-id="e31a4-125">Configuration</span><span class="sxs-lookup"><span data-stu-id="e31a4-125">Configuration</span></span>](#configuration)
3. [<span data-ttu-id="e31a4-126">Importer et synchroniser</span><span class="sxs-lookup"><span data-stu-id="e31a4-126">Import and Synchronize</span></span>](#import-and-synchronize)
4. [<span data-ttu-id="e31a4-127">Vérifier</span><span class="sxs-lookup"><span data-stu-id="e31a4-127">Verify</span></span>](#verify)
5. [<span data-ttu-id="e31a4-128">Changer de serveur actif</span><span class="sxs-lookup"><span data-stu-id="e31a4-128">Switch active server</span></span>](#switch-active-server)

#### <a name="prepare"></a><span data-ttu-id="e31a4-129">Préparation</span><span class="sxs-lookup"><span data-stu-id="e31a4-129">Prepare</span></span>
1. <span data-ttu-id="e31a4-130">Installer Azure AD Connect, sélectionnez **mode de préproduction**et désélectionnez **démarrer la synchronisation** sur hello dernière page de l’Assistant installation hello.</span><span class="sxs-lookup"><span data-stu-id="e31a4-130">Install Azure AD Connect, select **staging mode**, and unselect **start synchronization** on hello last page in hello installation wizard.</span></span> <span data-ttu-id="e31a4-131">Ce mode vous permet de moteur de synchronisation hello toorun manuellement.</span><span class="sxs-lookup"><span data-stu-id="e31a4-131">This mode allows you toorun hello sync engine manually.</span></span>
   <span data-ttu-id="e31a4-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span><span class="sxs-lookup"><span data-stu-id="e31a4-132">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/readytoconfigure.png)</span></span>
2. <span data-ttu-id="e31a4-133">Connexion hors tension et à la connexion et à partir de hello démarrer menu, sélectionnez **Service de synchronisation**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-133">Sign off/sign in and from hello start menu select **Synchronization Service**.</span></span>

#### <a name="configuration"></a><span data-ttu-id="e31a4-134">Configuration</span><span class="sxs-lookup"><span data-stu-id="e31a4-134">Configuration</span></span>
<span data-ttu-id="e31a4-135">Si vous avez apporté des modifications personnalisées toohello principal configuration du serveur et que vous souhaitez toocompare hello avec hello serveur intermédiaire, puis utilisez [documentation de configuration Azure AD Connect](https://github.com/Microsoft/AADConnectConfigDocumenter).</span><span class="sxs-lookup"><span data-stu-id="e31a4-135">If you have made custom changes toohello primary server and want toocompare hello configuration with hello staging server, then use [Azure AD Connect configuration documenter](https://github.com/Microsoft/AADConnectConfigDocumenter).</span></span>

#### <a name="import-and-synchronize"></a><span data-ttu-id="e31a4-136">Importer et synchroniser</span><span class="sxs-lookup"><span data-stu-id="e31a4-136">Import and Synchronize</span></span>
1. <span data-ttu-id="e31a4-137">Sélectionnez **connecteurs**, et sélectionnez hello premier connecteur avec type de hello **les Services de domaine Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-137">Select **Connectors**, and select hello first Connector with hello type **Active Directory Domain Services**.</span></span> <span data-ttu-id="e31a4-138">Cliquez sur **Exécuter**, sélectionnez **Importation intégrale**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-138">Click **Run**, select **Full import**, and **OK**.</span></span> <span data-ttu-id="e31a4-139">Répétez cette procédure pour tous les connecteurs de ce type.</span><span class="sxs-lookup"><span data-stu-id="e31a4-139">Do these steps for all Connectors of this type.</span></span>
2. <span data-ttu-id="e31a4-140">Sélectionnez hello connecteur avec type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-140">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="e31a4-141">Cliquez sur **Exécuter**, sélectionnez **Importation intégrale**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-141">Click **Run**, select **Full import**, and **OK**.</span></span>
3. <span data-ttu-id="e31a4-142">Assurez-vous que l’onglet hello connecteurs est toujours sélectionné.</span><span class="sxs-lookup"><span data-stu-id="e31a4-142">Make sure hello tab Connectors is still selected.</span></span> <span data-ttu-id="e31a4-143">Pour chaque connecteur de type **Services de domaine Active Directory**, cliquez sur **Exécuter**, sélectionnez **Synchronisation Delta**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-143">For each Connector with type **Active Directory Domain Services**, click **Run**, select **Delta Synchronization**, and **OK**.</span></span>
4. <span data-ttu-id="e31a4-144">Sélectionnez hello connecteur avec type **Azure Active Directory (Microsoft)**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-144">Select hello Connector with type **Azure Active Directory (Microsoft)**.</span></span> <span data-ttu-id="e31a4-145">Cliquez sur **Exécuter**, sélectionnez **Synchronisation Delta**, puis **OK**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-145">Click **Run**, select **Delta Synchronization**, and **OK**.</span></span>

<span data-ttu-id="e31a4-146">Vous avez maintenant une exportation intermédiaire change tooAzure AD et AD local (si vous utilisez un déploiement Exchange hybride).</span><span class="sxs-lookup"><span data-stu-id="e31a4-146">You have now staged export changes tooAzure AD and on-premises AD (if you are using Exchange hybrid deployment).</span></span> <span data-ttu-id="e31a4-147">les étapes suivantes Hello autoriser tooinspect Nouveautés sur toochange avant de commencer réellement hello exporter toohello les répertoires.</span><span class="sxs-lookup"><span data-stu-id="e31a4-147">hello next steps allow you tooinspect what is about toochange before you actually start hello export toohello directories.</span></span>

#### <a name="verify"></a><span data-ttu-id="e31a4-148">Vérifier</span><span class="sxs-lookup"><span data-stu-id="e31a4-148">Verify</span></span>
1. <span data-ttu-id="e31a4-149">Démarrez une invite de commandes et accédez trop`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span><span class="sxs-lookup"><span data-stu-id="e31a4-149">Start a cmd prompt and go too`%ProgramFiles%\Microsoft Azure AD Sync\bin`</span></span>
2. <span data-ttu-id="e31a4-150">Ensuite, exécutez : `csexport "Name of Connector" %temp%\export.xml /f:x` nom hello Hello connecteur sont accessibles dans le Service de synchronisation.</span><span class="sxs-lookup"><span data-stu-id="e31a4-150">Run: `csexport "Name of Connector" %temp%\export.xml /f:x` hello name of hello Connector can be found in Synchronization Service.</span></span> <span data-ttu-id="e31a4-151">Il a un too"contoso.com similaire nom – AAD » pour Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e31a4-151">It has a name similar too"contoso.com – AAD" for Azure AD.</span></span>
3. <span data-ttu-id="e31a4-152">Copiez le script PowerShell de hello à partir de la section de hello [CSAnalyzer](#appendix-csanalyzer) fichier tooa nommé `csanalyzer.ps1`.</span><span class="sxs-lookup"><span data-stu-id="e31a4-152">Copy hello PowerShell script from hello section [CSAnalyzer](#appendix-csanalyzer) tooa file named `csanalyzer.ps1`.</span></span>
4. <span data-ttu-id="e31a4-153">Ouvrez une fenêtre PowerShell et parcourir le dossier toohello où vous avez créé le script PowerShell de hello.</span><span class="sxs-lookup"><span data-stu-id="e31a4-153">Open a PowerShell window and browse toohello folder where you created hello PowerShell script.</span></span>
5. <span data-ttu-id="e31a4-154">Exécutez : `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span><span class="sxs-lookup"><span data-stu-id="e31a4-154">Run: `.\csanalyzer.ps1 -xmltoimport %temp%\export.xml`.</span></span>
6. <span data-ttu-id="e31a4-155">Vous disposez maintenant d’un fichier nommé **processedusers1.csv** qui peut être examiné dans Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="e31a4-155">You now have a file named **processedusers1.csv** that can be examined in Microsoft Excel.</span></span> <span data-ttu-id="e31a4-156">Toutes les modifications intermédiaires de toobe exporté tooAzure AD se trouvent dans ce fichier.</span><span class="sxs-lookup"><span data-stu-id="e31a4-156">All changes staged toobe exported tooAzure AD are found in this file.</span></span>
7. <span data-ttu-id="e31a4-157">Apportez les modifications nécessaires des données de toohello ou configuration et exécuter ces étapes à nouveau (importation et synchronisation et vérifiez) jusqu'à ce que hello modifications concernent toobe exportée sont attendus.</span><span class="sxs-lookup"><span data-stu-id="e31a4-157">Make necessary changes toohello data or configuration and run these steps again (Import and Synchronize and Verify) until hello changes that are about toobe exported are expected.</span></span>

#### <a name="switch-active-server"></a><span data-ttu-id="e31a4-158">Changer de serveur actif</span><span class="sxs-lookup"><span data-stu-id="e31a4-158">Switch active server</span></span>
1. <span data-ttu-id="e31a4-159">Sur le serveur actif de hello, désactivez le serveur hello (DirSync/FIM/Azure AD Sync) afin qu’il n’exporte pas tooAzure AD ou la définir dans le mode (Azure AD Connect) de mise en lots.</span><span class="sxs-lookup"><span data-stu-id="e31a4-159">On hello currently active server, either turn off hello server (DirSync/FIM/Azure AD Sync) so it is not exporting tooAzure AD or set it in staging mode (Azure AD Connect).</span></span>
2. <span data-ttu-id="e31a4-160">Exécuter l’Assistant installation hello sur serveur hello **mode de préproduction** et désactiver **mode de préproduction**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-160">Run hello installation wizard on hello server in **staging mode** and disable **staging mode**.</span></span>
   <span data-ttu-id="e31a4-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span><span class="sxs-lookup"><span data-stu-id="e31a4-161">![ReadyToConfigure](./media/active-directory-aadconnectsync-operations/additionaltasks.png)</span></span>

## <a name="disaster-recovery"></a><span data-ttu-id="e31a4-162">Récupération d'urgence</span><span class="sxs-lookup"><span data-stu-id="e31a4-162">Disaster recovery</span></span>
<span data-ttu-id="e31a4-163">Partie de la conception de l’implémentation hello est tooplan pour le toodo en cas de sinistre dans lequel vous perdez le serveur de synchronisation hello.</span><span class="sxs-lookup"><span data-stu-id="e31a4-163">Part of hello implementation design is tooplan for what toodo in case there is a disaster where you lose hello sync server.</span></span> <span data-ttu-id="e31a4-164">Il existe différents modèles toouse et l’un toouse dépend de plusieurs facteurs, notamment :</span><span class="sxs-lookup"><span data-stu-id="e31a4-164">There are different models toouse and which one toouse depends on several factors including:</span></span>

* <span data-ttu-id="e31a4-165">Quelle est votre tolérance des modifications n’est ne pas en mesure de créer de tooobjects dans Azure AD au cours du temps d’arrêt hello ?</span><span class="sxs-lookup"><span data-stu-id="e31a4-165">What is your tolerance for not being able make changes tooobjects in Azure AD during hello downtime?</span></span>
* <span data-ttu-id="e31a4-166">Si vous utilisez la synchronisation de mot de passe, procédez comme hello les utilisateurs accepter que toouse hello ancien mot de passe dans Azure AD dans le cas où ils modifier localement ?</span><span class="sxs-lookup"><span data-stu-id="e31a4-166">If you use password synchronization, do hello users accept that they have toouse hello old password in Azure AD in case they change it on-premises?</span></span>
* <span data-ttu-id="e31a4-167">Avez-vous une dépendance par rapport aux opérations en temps réel, notamment l’écriture différée de mot de passe ?</span><span class="sxs-lookup"><span data-stu-id="e31a4-167">Do you have a dependency on real-time operations, such as password writeback?</span></span>

<span data-ttu-id="e31a4-168">En fonction des questions de toothese réponses hello et la stratégie de votre organisation, un des hello suivant des stratégies peut être implémenté :</span><span class="sxs-lookup"><span data-stu-id="e31a4-168">Depending on hello answers toothese questions and your organization’s policy, one of hello following strategies can be implemented:</span></span>

* <span data-ttu-id="e31a4-169">Régénérer si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e31a4-169">Rebuild when needed.</span></span>
* <span data-ttu-id="e31a4-170">Disposer d'un serveur de secours en attente, appelé **mode intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-170">Have a spare standby server, known as **staging mode**.</span></span>
* <span data-ttu-id="e31a4-171">Utiliser les machines virtuelles.</span><span class="sxs-lookup"><span data-stu-id="e31a4-171">Use virtual machines.</span></span>

<span data-ttu-id="e31a4-172">Si vous n’utilisez pas hello intégrée SQL Express de base de données, vous devez également examiner hello [haute disponibilité SQL](#sql-high-availability) section.</span><span class="sxs-lookup"><span data-stu-id="e31a4-172">If you do not use hello built-in SQL Express database, then you should also review hello [SQL High Availability](#sql-high-availability) section.</span></span>

### <a name="rebuild-when-needed"></a><span data-ttu-id="e31a4-173">Régénérer lorsque nécessaire</span><span class="sxs-lookup"><span data-stu-id="e31a4-173">Rebuild when needed</span></span>
<span data-ttu-id="e31a4-174">Une stratégie viable consiste tooplan une reconstruction du serveur si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="e31a4-174">A viable strategy is tooplan for a server rebuild when needed.</span></span> <span data-ttu-id="e31a4-175">En règle générale, l’installation de hello du moteur de synchronisation et de hello importation initiale et la synchronisation peut être effectuée en quelques heures.</span><span class="sxs-lookup"><span data-stu-id="e31a4-175">Usually, installing hello sync engine and do hello initial import and sync can be completed within a few hours.</span></span> <span data-ttu-id="e31a4-176">S’il n’est pas un serveur de rechange disponibles, il est possible tootemporarily un moteur de synchronisation de domaine contrôleur toohost hello.</span><span class="sxs-lookup"><span data-stu-id="e31a4-176">If there isn’t a spare server available, it is possible tootemporarily use a domain controller toohost hello sync engine.</span></span>

<span data-ttu-id="e31a4-177">serveur du moteur de synchronisation Hello ne stocke pas d’état sur les objets de hello afin de la base de données hello peut être reconstruit à partir des données hello dans Active Directory et Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e31a4-177">hello sync engine server does not store any state about hello objects so hello database can be rebuilt from hello data in Active Directory and Azure AD.</span></span> <span data-ttu-id="e31a4-178">Hello **sourceAnchor** l’attribut est utilisé toojoin hello des objets du site et hello cloud.</span><span class="sxs-lookup"><span data-stu-id="e31a4-178">hello **sourceAnchor** attribute is used toojoin hello objects from on-premises and hello cloud.</span></span> <span data-ttu-id="e31a4-179">Si vous régénérez hello du serveur avec les objets locale existante et hello cloud, puis le moteur de synchronisation hello correspond à ces objets ensemble à nouveau sur la réinstallation.</span><span class="sxs-lookup"><span data-stu-id="e31a4-179">If you rebuild hello server with existing objects on-premises and hello cloud, then hello sync engine matches those objects together again on reinstallation.</span></span> <span data-ttu-id="e31a4-180">éléments Hello vous devez toodocument et enregistrez les modifications de configuration de hello apportées serveur toohello, tels que les règles de filtrage et de synchronisation sont.</span><span class="sxs-lookup"><span data-stu-id="e31a4-180">hello things you need toodocument and save are hello configuration changes made toohello server, such as filtering and synchronization rules.</span></span> <span data-ttu-id="e31a4-181">Ces configurations personnalisées doivent être réappliquées avant de commencer la synchronisation.</span><span class="sxs-lookup"><span data-stu-id="e31a4-181">These custom configurations must be reapplied before you start synchronizing.</span></span>

### <a name="have-a-spare-standby-server---staging-mode"></a><span data-ttu-id="e31a4-182">Disposer d’un serveur de secours en attente, connu sous le nom de mode intermédiaire.</span><span class="sxs-lookup"><span data-stu-id="e31a4-182">Have a spare standby server - staging mode</span></span>
<span data-ttu-id="e31a4-183">Si vous disposez d’un environnement plus complexe, il est recommandé d’avoir un ou plusieurs serveurs de secours.</span><span class="sxs-lookup"><span data-stu-id="e31a4-183">If you have a more complex environment, then having one or more standby servers is recommended.</span></span> <span data-ttu-id="e31a4-184">Pendant l’installation, vous pouvez activer une toobe de serveur dans **mode de préproduction**.</span><span class="sxs-lookup"><span data-stu-id="e31a4-184">During installation, you can enable a server toobe in **staging mode**.</span></span>

<span data-ttu-id="e31a4-185">Pour en savoir plus, voir [Mode intermédiaire](#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="e31a4-185">For more information, see [staging mode](#staging-mode).</span></span>

### <a name="use-virtual-machines"></a><span data-ttu-id="e31a4-186">Utiliser les machines virtuelles</span><span class="sxs-lookup"><span data-stu-id="e31a4-186">Use virtual machines</span></span>
<span data-ttu-id="e31a4-187">Une méthode courante et prises en charge est le moteur de synchronisation toorun hello dans une machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="e31a4-187">A common and supported method is toorun hello sync engine in a virtual machine.</span></span> <span data-ttu-id="e31a4-188">Au cas où l’hôte de hello a un problème, image hello avec le serveur du moteur de synchronisation hello peut être migré tooanother server.</span><span class="sxs-lookup"><span data-stu-id="e31a4-188">In case hello host has an issue, hello image with hello sync engine server can be migrated tooanother server.</span></span>

### <a name="sql-high-availability"></a><span data-ttu-id="e31a4-189">Haute disponibilité SQL</span><span class="sxs-lookup"><span data-stu-id="e31a4-189">SQL High Availability</span></span>
<span data-ttu-id="e31a4-190">Si vous n’utilisez pas hello SQL Server Express qui est fourni avec Azure AD Connect, haute disponibilité pour SQL Server doit également à envisager.</span><span class="sxs-lookup"><span data-stu-id="e31a4-190">If you are not using hello SQL Server Express that comes with Azure AD Connect, then high availability for SQL Server should also be considered.</span></span> <span data-ttu-id="e31a4-191">solutions de haute disponibilité Hello pris en charge incluent AOA (groupes de disponibilité AlwaysOn) et gestion de clusters SQL.</span><span class="sxs-lookup"><span data-stu-id="e31a4-191">hello high availability solutions supported include SQL clustering and AOA (Always On Availability Groups).</span></span> <span data-ttu-id="e31a4-192">Les solutions non prises en charge incluent la mise en miroir.</span><span class="sxs-lookup"><span data-stu-id="e31a4-192">Unsupported solutions include mirroring.</span></span>

<span data-ttu-id="e31a4-193">Une prise en charge pour SQL AOA tooAzure AD Connect version 1.1.524.0.</span><span class="sxs-lookup"><span data-stu-id="e31a4-193">Support for SQL AOA was added tooAzure AD Connect in version 1.1.524.0.</span></span> <span data-ttu-id="e31a4-194">Vous devez activer SQL AOA avant d’installer Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="e31a4-194">You must enable SQL AOA before installing Azure AD Connect.</span></span> <span data-ttu-id="e31a4-195">Pendant l’installation, Azure AD Connect détecte si instance SQL de hello fournie est activée pour SQL AOA ou non.</span><span class="sxs-lookup"><span data-stu-id="e31a4-195">During installation, Azure AD Connect detects whether hello SQL instance provided is enabled for SQL AOA or not.</span></span> <span data-ttu-id="e31a4-196">Si SQL AOA est activée, Azure AD Connect davantage détermine si SQL AOA est toouse configuré une réplication synchrone ou asynchrone.</span><span class="sxs-lookup"><span data-stu-id="e31a4-196">If SQL AOA is enabled, Azure AD Connect further figures out if SQL AOA is configured toouse synchronous replication or asynchronous replication.</span></span> <span data-ttu-id="e31a4-197">Lorsque vous configurez hello écouteur du groupe de disponibilité, il est recommandé de définir hello RegisterAllProvidersIP propriété too0.</span><span class="sxs-lookup"><span data-stu-id="e31a4-197">When setting up hello Availability Group Listener, it is recommended that you set hello RegisterAllProvidersIP property too0.</span></span> <span data-ttu-id="e31a4-198">Il s’agit, car Azure AD Connect utilise actuellement SQL Native Client tooconnect tooSQL et SQL Native Client ne prend pas en charge hello propriété MultiSubNetFailover.</span><span class="sxs-lookup"><span data-stu-id="e31a4-198">This is because Azure AD Connect currently uses SQL Native Client tooconnect tooSQL and SQL Native Client does not support hello use of MultiSubNetFailover property.</span></span>

## <a name="appendix-csanalyzer"></a><span data-ttu-id="e31a4-199">Annexe CSAnalyzer</span><span class="sxs-lookup"><span data-stu-id="e31a4-199">Appendix CSAnalyzer</span></span>
<span data-ttu-id="e31a4-200">Consultez la section de hello [vérifier](#verify) sur la façon de toouse ce script.</span><span class="sxs-lookup"><span data-stu-id="e31a4-200">See hello section [verify](#verify) on how toouse this script.</span></span>

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

#XmlReader.Create won't properly resolve hello file location,
#so expand and then resolve it
$resolvedXMLtoimport=Resolve-Path -Path ([Environment]::ExpandEnvironmentVariables($xmltoimport))

#use an XmlReader toodeal with even large files
$result=$reader = [System.Xml.XmlReader]::Create($resolvedXMLtoimport) 
$result=$reader.ReadToDescendant('cs-object')
do 
{
    #create hello object placeholder
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

    #now that we have hello basics, go get hello details

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

    #every so often, dump hello processed users in case we blow up somewhere
    if ($count % $batchsize -eq 0)
    {
        Write-Host Hit hello maximum users processed without completion... -ForegroundColor Yellow

        #export hello collection of users as as CSV
        Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
        $objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation

        #increment hello output file counter
        $outputfilecount+=1

        #reset hello collection and hello user counter
        $objOutputUsers = $null
        $count=0
    }

    $count+=1

    #need toobail out of hello loop if no more users tooprocess
    if ($reader.NodeType -eq [System.Xml.XmlNodeType]::EndElement)
    {
        break
    }

} while ($reader.Read)

#need toowrite out any users that didn't get picked up in a batch of 1000
#export hello collection of users as as CSV
Write-Host Writing processedusers${outputfilecount}.csv -ForegroundColor Yellow
$objOutputUsers | Export-Csv -path processedusers${outputfilecount}.csv -NoTypeInformation
```

## <a name="next-steps"></a><span data-ttu-id="e31a4-201">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="e31a4-201">Next steps</span></span>
<span data-ttu-id="e31a4-202">**Rubriques de présentation**</span><span class="sxs-lookup"><span data-stu-id="e31a4-202">**Overview topics**</span></span>  

* [<span data-ttu-id="e31a4-203">Azure AD Connect Sync - Présentation et personnalisation des options de synchronisation</span><span class="sxs-lookup"><span data-stu-id="e31a4-203">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)  
* [<span data-ttu-id="e31a4-204">Intégration de vos identités locales avec Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e31a4-204">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)  
