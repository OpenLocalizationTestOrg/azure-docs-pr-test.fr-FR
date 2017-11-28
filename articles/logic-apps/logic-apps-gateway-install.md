---
title: "passerelle de données locale aaaInstall - Azure Logic Apps | Documents Microsoft"
description: "Accéder aux sources de données sur site, installer la passerelle de données locale hello pour le transfert de données rapide et le chiffrement entre les sources de données sur site et les applications de la logique"
keywords: "accéder aux données, localement, transfert de données, chiffrement, sources de données"
services: logic-apps
documentationcenter: 
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 47e3024e-88a0-4017-8484-8f392faec89d
ms.service: logic-apps
ms.devlang: 
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 01386a904d856ff545f2eca8eb1b008dcdc08574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="install-hello-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="9463f-104">Installer la passerelle de données locale hello pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9463f-104">Install hello on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="9463f-105">Avant que vos applications logiques peuvent accéder à des sources de données sur site, vous devez installer et configurer la passerelle de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-105">Before your logic apps can access data sources on premises, you must install and set up hello on-premises data gateway.</span></span> <span data-ttu-id="9463f-106">Hello passerelle fait Office de pont qui fournit le transfert de données rapide et le chiffrement entre systèmes sur site et vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="9463f-106">hello gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="9463f-107">passerelle de Hello transmet des données à partir de sources locales sur des canaux chiffrés via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9463f-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="9463f-108">Tout le trafic provient sécurisé trafic sortant à partir de l’agent de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="9463f-109">En savoir plus sur [le fonctionnement de la passerelle de données hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="9463f-109">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="9463f-110">passerelle de Hello prend en charge les sources de données de connexions toothese sur site :</span><span class="sxs-lookup"><span data-stu-id="9463f-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="9463f-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="9463f-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="9463f-112">DB2</span><span class="sxs-lookup"><span data-stu-id="9463f-112">DB2</span></span>  
*   <span data-ttu-id="9463f-113">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="9463f-113">File System</span></span>
*   <span data-ttu-id="9463f-114">Informix</span><span class="sxs-lookup"><span data-stu-id="9463f-114">Informix</span></span>
*   <span data-ttu-id="9463f-115">MQ</span><span class="sxs-lookup"><span data-stu-id="9463f-115">MQ</span></span>
*   <span data-ttu-id="9463f-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="9463f-116">MySQL</span></span>
*   <span data-ttu-id="9463f-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="9463f-117">Oracle Database</span></span>
*   <span data-ttu-id="9463f-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="9463f-118">PostgreSQL</span></span>
*   <span data-ttu-id="9463f-119">Serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="9463f-119">SAP Application Server</span></span> 
*   <span data-ttu-id="9463f-120">Serveur de messagerie SAP</span><span class="sxs-lookup"><span data-stu-id="9463f-120">SAP Message Server</span></span>
*   <span data-ttu-id="9463f-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="9463f-121">SharePoint</span></span>
*   <span data-ttu-id="9463f-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="9463f-122">SQL Server</span></span>
*   <span data-ttu-id="9463f-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="9463f-123">Teradata</span></span>

<span data-ttu-id="9463f-124">Ces étapes indiquent comment toofirst installation hello local passerelle de données avant de vous [configurer une connexion entre la passerelle de hello et vos applications logiques](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="9463f-124">These steps show how toofirst install hello on-premises data gateway before you [set up a connection between hello gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="9463f-125">Pour plus d’informations sur les connecteurs pris en charge, voir [Connecteurs pour Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="9463f-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="9463f-126">Pour plus d’informations sur la façon dont toouse hello passerelle avec d’autres services, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="9463f-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="9463f-127">Passerelle de données locale Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="9463f-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="9463f-128">Passerelle de données locale Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="9463f-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="9463f-129">Passerelle de données locale Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="9463f-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="9463f-130">Passerelle de données locale Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="9463f-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="9463f-131">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="9463f-131">Requirements</span></span>

<span data-ttu-id="9463f-132">**Minimale** :</span><span class="sxs-lookup"><span data-stu-id="9463f-132">**Minimum**:</span></span>

* <span data-ttu-id="9463f-133">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="9463f-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="9463f-134">Version 64 bits de Windows 7 ou Windows Server 2008 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="9463f-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="9463f-135">**Recommandée** :</span><span class="sxs-lookup"><span data-stu-id="9463f-135">**Recommended**:</span></span>

* <span data-ttu-id="9463f-136">Processeur 8 cœurs</span><span class="sxs-lookup"><span data-stu-id="9463f-136">8 Core CPU</span></span>
* <span data-ttu-id="9463f-137">8 Go de mémoire</span><span class="sxs-lookup"><span data-stu-id="9463f-137">8 GB Memory</span></span>
* <span data-ttu-id="9463f-138">Version 64 bits de Windows 2012 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="9463f-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="9463f-139">**Points importants à prendre en considération** :</span><span class="sxs-lookup"><span data-stu-id="9463f-139">**Important considerations**:</span></span>

* <span data-ttu-id="9463f-140">Installez la passerelle de données locale hello uniquement sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="9463f-140">Install hello on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="9463f-141">Vous ne pouvez pas installer la passerelle de hello sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="9463f-141">You can't install hello gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="9463f-142">Vous n’avez pas passerelle de hello tooinstall sur hello même ordinateur que votre source de données.</span><span class="sxs-lookup"><span data-stu-id="9463f-142">You don't have tooinstall hello gateway on hello same computer as your data source.</span></span> <span data-ttu-id="9463f-143">latence de toominimize, vous pouvez installer passerelle hello aussi proche en tant que source de données tooyour possibles, ou sur hello même ordinateur, en supposant que vous disposez des autorisations.</span><span class="sxs-lookup"><span data-stu-id="9463f-143">toominimize latency, you can install hello gateway as close as possible tooyour data source, or on hello same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="9463f-144">N’installez pas les passerelle hello sur un ordinateur qui désactive, passe toosleep ou ne connecte pas toohello Internet, car la passerelle de hello ne peut pas s’exécuter dans ces circonstances.</span><span class="sxs-lookup"><span data-stu-id="9463f-144">Don't install hello gateway on a computer that turns off, goes toosleep, or doesn't connect toohello Internet because hello gateway can't run under those circumstances.</span></span> <span data-ttu-id="9463f-145">De même, les performances de la passerelle peuvent être moindres sur un réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="9463f-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="9463f-146">Pendant l’installation, vous devez vous connecter avec un [compte professionnel ou scolaire](https://docs.microsoft.com/azure/active-directory/sign-up-organization) géré par Azure Active Directory (Azure AD), et non un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9463f-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="9463f-147">Vous avez toouse hello même travail ou d’établissement scolaire compte plus tard en hello Azure portal lorsque vous créez et associez une ressource de passerelle à votre installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-147">You have toouse hello same work or school account later in hello Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="9463f-148">Puis, vous sélectionnez cette ressource passerelle lorsque vous créez la connexion de hello entre votre source de données de local application et hello logique.</span><span class="sxs-lookup"><span data-stu-id="9463f-148">You then select this gateway resource when you create hello connection between your logic app and hello on-premises data source.</span></span> [<span data-ttu-id="9463f-149">Pourquoi dois-je utiliser un compte professionnel ou scolaire Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="9463f-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="9463f-150">Si vous avez souscrit une offre Office 365 sans fournir votre adresse de messagerie professionnelle réelle, votre adresse de connexion peut ressembler à ceci : jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="9463f-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="9463f-151">Si vous disposez d’une passerelle existante que vous configurez avec un programme d’installation est antérieure à la version 14.16.6317.4, vous ne pouvez pas modifier l’emplacement de votre passerelle par installer de dernière hello en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="9463f-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running hello latest installer.</span></span> <span data-ttu-id="9463f-152">Toutefois, vous pouvez utiliser hello dernière tooset de programme d’installation d’une nouvelle passerelle avec emplacement hello souhaitées à la place.</span><span class="sxs-lookup"><span data-stu-id="9463f-152">However, you can use hello latest installer tooset up a new gateway with hello location that you want instead.</span></span>
  
  <span data-ttu-id="9463f-153">Si vous disposez d’un programme d’installation de passerelle est antérieure à la version 14.16.6317.4, mais vous n’avez pas installé votre passerelle encore, vous pouvez télécharger et utiliser le programme d’installation de la dernière hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use hello latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-hello-data-gateway"></a><span data-ttu-id="9463f-154">Installer la passerelle de données hello</span><span class="sxs-lookup"><span data-stu-id="9463f-154">Install hello data gateway</span></span>

1.  <span data-ttu-id="9463f-155">[Téléchargez et exécutez le programme d’installation de la passerelle hello sur un ordinateur local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="9463f-155">[Download and run hello gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="9463f-156">Lisez et acceptez les termes du contrat de hello d’utilisation et déclaration de confidentialité.</span><span class="sxs-lookup"><span data-stu-id="9463f-156">Review and accept hello terms of use and privacy statement.</span></span>

3. <span data-ttu-id="9463f-157">Spécifier le chemin d’accès hello sur votre ordinateur local où vous souhaitez la passerelle de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="9463f-157">Specify hello path on your local computer where you want tooinstall hello gateway.</span></span>

4. <span data-ttu-id="9463f-158">Lorsque vous y êtes invité, connectez-vous à votre compte Azure professionnel ou scolaire, pas à un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="9463f-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Connexion avec le compte professionnel ou scolaire Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="9463f-160">Maintenant inscrire votre passerelle installée avec hello [service cloud de passerelle](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="9463f-160">Now register your installed gateway with hello [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="9463f-161">Choisissez **Inscrivez une nouvelle passerelle sur cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="9463f-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="9463f-162">service de cloud de passerelle Hello chiffre et stocke vos informations d’identification de source de données et les détails de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-162">hello gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="9463f-163">service de Hello achemine les requêtes et leurs résultats entre votre application logique, la passerelle de données locale hello et votre source de données sur site.</span><span class="sxs-lookup"><span data-stu-id="9463f-163">hello service also routes queries and their results between your logic app, hello on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="9463f-164">Entrez un nom pour votre installation de passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="9463f-165">Créez une clé de récupération, puis confirmez votre clé de récupération.</span><span class="sxs-lookup"><span data-stu-id="9463f-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="9463f-166">Votre clé de récupération doit contenir au moins huit caractères.</span><span class="sxs-lookup"><span data-stu-id="9463f-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="9463f-167">Assurez-vous que vous enregistrez et clé de hello de conserver en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="9463f-167">Make sure that you save and keep hello key in a safe place.</span></span> <span data-ttu-id="9463f-168">Vous avez besoin de cette clé lorsque vous souhaitez toomigrate, restaurer ou reprendre une passerelle existante.</span><span class="sxs-lookup"><span data-stu-id="9463f-168">You also need this key when you want toomigrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="9463f-169">Cliquez sur la région par défaut pour le service de cloud de passerelle hello et utilisés par votre installation de la passerelle, Azure Service Bus toochange hello **modification région**.</span><span class="sxs-lookup"><span data-stu-id="9463f-169">toochange hello default region for hello gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Modification de la région](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="9463f-171">région de Hello par défaut est région hello associée à votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9463f-171">hello default region is hello region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="9463f-172">Dans le volet suivant de hello, ouvrez hello **sélectionner une région** trop choisir une autre région.</span><span class="sxs-lookup"><span data-stu-id="9463f-172">On hello next pane, open hello **Select Region** too choose a different region.</span></span>

      ![Sélection d’une autre région](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="9463f-174">Par exemple, vous peut sélectionner hello même région que votre application logique, ou sélectionnez hello région le plus proche tooyour des données locales source afin de réduire la latence.</span><span class="sxs-lookup"><span data-stu-id="9463f-174">For example, you might select hello same region as your logic app, or select hello region closest tooyour on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="9463f-175">Votre ressource de passerelle et votre application logique se trouvent dans des emplacements différents.</span><span class="sxs-lookup"><span data-stu-id="9463f-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="9463f-176">Vous ne pouvez pas modifier cette région après l’installation.</span><span class="sxs-lookup"><span data-stu-id="9463f-176">You can't change this region after installation.</span></span> <span data-ttu-id="9463f-177">Cette zone détermine également et restreint l’emplacement hello où vous pouvez créer des ressources Azure de hello pour votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-177">This region also determines and restricts hello location where you can create hello Azure resource for your gateway.</span></span> <span data-ttu-id="9463f-178">Par conséquent, lorsque vous créez votre ressource de passerelle dans Azure, assurez-vous qu’emplacement de la ressource hello correspond à la région de hello que vous avez sélectionné lors de l’installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-178">So when you create your gateway resource in Azure, make sure that hello resource location matches hello region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="9463f-179">Si vous souhaitez toouse une autre région pour votre passerelle ultérieurement, vous devez configurer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-179">If you want toouse a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="9463f-180">Une fois ces opérations effectuées, sélectionnez **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="9463f-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="9463f-181">Maintenant, suivez ces étapes dans hello portail Azure afin de pouvoir [créer une ressource Azure pour votre passerelle](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="9463f-181">Now follow these steps in hello Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="9463f-182">En savoir plus sur [le fonctionnement de la passerelle de données hello](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="9463f-182">Learn more about [how hello data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="9463f-183">Migrer, restaurer ou contrôler une passerelle existante</span><span class="sxs-lookup"><span data-stu-id="9463f-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="9463f-184">tooperform ces tâches, vous devez disposer de clé de récupération hello qui a été spécifié lors de la passerelle de hello a été installée.</span><span class="sxs-lookup"><span data-stu-id="9463f-184">tooperform these tasks, you must have hello recovery key that was specified when hello gateway was installed.</span></span>

1. <span data-ttu-id="9463f-185">Dans le menu Démarrer de votre ordinateur, choisissez **Passerelle de données locale**.</span><span class="sxs-lookup"><span data-stu-id="9463f-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="9463f-186">Une fois que hello s’ouvre le programme d’installation et connectez-vous avec hello même Azure fonctionne ou compte scolaire qui était précédemment utilisé la passerelle de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="9463f-186">After hello installer opens, sign in with hello same Azure work or school account that was previously used tooinstall hello gateway.</span></span>

3. <span data-ttu-id="9463f-187">Choisissez **Migrer, restaurer ou contrôler une passerelle existante**.</span><span class="sxs-lookup"><span data-stu-id="9463f-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="9463f-188">Fournir la clé de nom et de récupération hello pour la passerelle hello que vous souhaitez toomigrate, restaurez ou remplacez par.</span><span class="sxs-lookup"><span data-stu-id="9463f-188">Provide hello name and recovery key for hello gateway that you want toomigrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-hello-gateway"></a><span data-ttu-id="9463f-189">Redémarrez la passerelle de hello</span><span class="sxs-lookup"><span data-stu-id="9463f-189">Restart hello gateway</span></span>

<span data-ttu-id="9463f-190">passerelle de Hello s’exécute comme un service Windows.</span><span class="sxs-lookup"><span data-stu-id="9463f-190">hello gateway runs as a Windows service.</span></span> <span data-ttu-id="9463f-191">Comme tout autre service Windows, vous pouvez démarrer et arrêter le service hello de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="9463f-191">Like any other Windows service, you can start and stop hello service in multiple ways.</span></span> <span data-ttu-id="9463f-192">Par exemple, vous pouvez ouvrir une invite de commandes avec des autorisations élevées sur ordinateur hello où passerelle de hello est en cours d’exécution et exécuter ces deux commandes :</span><span class="sxs-lookup"><span data-stu-id="9463f-192">For example, you can open a command prompt with elevated permissions on hello computer where hello gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="9463f-193">service de hello toostop, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9463f-193">toostop hello service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="9463f-194">service de hello toostart, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9463f-194">toostart hello service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="9463f-195">Compte de service Windows</span><span class="sxs-lookup"><span data-stu-id="9463f-195">Windows service account</span></span>

<span data-ttu-id="9463f-196">passerelle de données locale Hello est configurée toouse `NT SERVICE\PBIEgwService` pour hello Windows service informations d’identification d’ouverture de session.</span><span class="sxs-lookup"><span data-stu-id="9463f-196">hello on-premises data gateway is set up toouse `NT SERVICE\PBIEgwService` for hello Windows service logon credentials.</span></span> <span data-ttu-id="9463f-197">Par défaut, passerelle de hello a le droit de « Une session en tant que service » hello pour l’ordinateur de hello sur lequel vous installez la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-197">By default, hello gateway has hello "Log on as a service" right for hello machine where you install hello gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="9463f-198">Hello compte de service Windows diffère compte hello utilisés pour la connexion des sources de données tooon local et de hello travail Azure ou compte scolaire utilisé toosign dans les services toocloud.</span><span class="sxs-lookup"><span data-stu-id="9463f-198">hello Windows service account differs from hello account used for connecting tooon-premises data sources, and from hello Azure work or school account used toosign in toocloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="9463f-199">Configuration d’un pare-feu ou d’un proxy</span><span class="sxs-lookup"><span data-stu-id="9463f-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="9463f-200">passerelle de Hello crée une connexion sortante trop [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="9463f-200">hello gateway creates an outbound connection too [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="9463f-201">tooprovide les informations de proxy pour votre passerelle, consultez [configurer les paramètres de proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="9463f-201">tooprovide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="9463f-202">toocheck si votre pare-feu ou proxy, peut bloquer les connexions, vérifiez si votre ordinateur peut connecter réellement toohello internet et hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="9463f-202">toocheck whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect toohello internet and hello [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="9463f-203">À partir d’une invite PowerShell, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="9463f-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="9463f-204">Cette commande teste uniquement la connectivité réseau et connectivité toohello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9463f-204">This command only tests network connectivity and connectivity toohello Azure Service Bus.</span></span> <span data-ttu-id="9463f-205">Afin de la commande hello ne concerne pas toodo avec la passerelle de hello ou un service de cloud de passerelle hello qui chiffre et stocke vos informations d’identification et les détails de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-205">So hello command doesn't have anything toodo with hello gateway or hello gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="9463f-206">Par ailleurs, cette commande est disponible uniquement sur Windows Server 2012 R2 ou version ultérieure, et sur Windows 8.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="9463f-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="9463f-207">Dans les versions antérieures du système d’exploitation, vous pouvez utiliser Telnet trop tester la connectivité.</span><span class="sxs-lookup"><span data-stu-id="9463f-207">On earlier OS versions, you can use Telnet too test connectivity.</span></span> <span data-ttu-id="9463f-208">Pour en savoir plus, voir [Solutions Azure Service Bus et hybrides](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="9463f-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="9463f-209">Vos résultats doivent être similaires toothis exemple :</span><span class="sxs-lookup"><span data-stu-id="9463f-209">Your results should look similar toothis example:</span></span>

```text
ComputerName           : watchdog.servicebus.windows.net
RemoteAddress          : 70.37.104.240
RemotePort             : 5672
InterfaceAlias         : vEthernet (Broadcom NetXtreme Gigabit Ethernet - Virtual Switch)
SourceAddress          : 10.120.60.105
PingSucceeded          : False
PingReplyDetails (RTT) : 0 ms
TcpTestSucceeded       : True
```

<span data-ttu-id="9463f-210">Si **TcpTestSucceeded** n’est pas défini trop**True**, vous pouvez être bloqué par un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="9463f-210">If **TcpTestSucceeded** is not set too**True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="9463f-211">Si vous souhaitez toobe complète, substituer hello **Nom_Ordinateur** et **Port** valeurs avec les valeurs hello répertoriés sous [configurer des ports](#configure-ports) dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="9463f-211">If you want toobe comprehensive, substitute hello **ComputerName** and **Port** values with hello values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="9463f-212">les pare-feu Hello peuvent également bloquer les connexions que hello Qu'azure Service Bus rend toohello centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="9463f-212">hello firewall might also block connections that hello Azure Service Bus makes toohello Azure datacenters.</span></span> <span data-ttu-id="9463f-213">Si ce scénario se produit, approuver (débloquer) toutes hello des adresses IP pour les centres de données dans votre région.</span><span class="sxs-lookup"><span data-stu-id="9463f-213">If this scenario happens, approve (unblock) all hello IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="9463f-214">Pour les adresses IP, [get hello Azure liste d’adresses IP ici](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="9463f-214">For those IP addresses, [get hello Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="9463f-215">Configuration des ports</span><span class="sxs-lookup"><span data-stu-id="9463f-215">Configure ports</span></span>

<span data-ttu-id="9463f-216">passerelle de Hello crée une connexion sortante trop[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) et communique sur des ports sortants : TCP 443 (valeur par défaut), 5671, 5672, 9350 à 9354.</span><span class="sxs-lookup"><span data-stu-id="9463f-216">hello gateway creates an outbound connection too[Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="9463f-217">passerelle de Hello ne requiert pas les ports entrants.</span><span class="sxs-lookup"><span data-stu-id="9463f-217">hello gateway doesn't require inbound ports.</span></span> <span data-ttu-id="9463f-218">Pour en savoir plus, voir [Solutions Azure Service Bus et hybrides](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="9463f-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="9463f-219">NOMS DE DOMAINE</span><span class="sxs-lookup"><span data-stu-id="9463f-219">DOMAIN NAMES</span></span> | <span data-ttu-id="9463f-220">PORTS SORTANTS</span><span class="sxs-lookup"><span data-stu-id="9463f-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="9463f-221">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="9463f-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9463f-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="9463f-222">*.analysis.windows.net</span></span> | <span data-ttu-id="9463f-223">443</span><span class="sxs-lookup"><span data-stu-id="9463f-223">443</span></span> | <span data-ttu-id="9463f-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="9463f-224">HTTPS</span></span> | 
| <span data-ttu-id="9463f-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="9463f-225">*.login.windows.net</span></span> | <span data-ttu-id="9463f-226">443</span><span class="sxs-lookup"><span data-stu-id="9463f-226">443</span></span> | <span data-ttu-id="9463f-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="9463f-227">HTTPS</span></span> | 
| <span data-ttu-id="9463f-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="9463f-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="9463f-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="9463f-229">5671-5672</span></span> | <span data-ttu-id="9463f-230">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="9463f-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="9463f-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="9463f-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="9463f-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="9463f-232">443, 9350-9354</span></span> | <span data-ttu-id="9463f-233">Récepteurs du Service Bus Relay sur TCP (nécessite le port 443 pour l’acquisition du jeton Access Control)</span><span class="sxs-lookup"><span data-stu-id="9463f-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="9463f-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="9463f-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="9463f-235">443</span><span class="sxs-lookup"><span data-stu-id="9463f-235">443</span></span> | <span data-ttu-id="9463f-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="9463f-236">HTTPS</span></span> | 
| <span data-ttu-id="9463f-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="9463f-237">*.core.windows.net</span></span> | <span data-ttu-id="9463f-238">443</span><span class="sxs-lookup"><span data-stu-id="9463f-238">443</span></span> | <span data-ttu-id="9463f-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="9463f-239">HTTPS</span></span> | 
| <span data-ttu-id="9463f-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="9463f-240">login.microsoftonline.com</span></span> | <span data-ttu-id="9463f-241">443</span><span class="sxs-lookup"><span data-stu-id="9463f-241">443</span></span> | <span data-ttu-id="9463f-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="9463f-242">HTTPS</span></span> | 
| <span data-ttu-id="9463f-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="9463f-243">*.msftncsi.com</span></span> | <span data-ttu-id="9463f-244">443</span><span class="sxs-lookup"><span data-stu-id="9463f-244">443</span></span> | <span data-ttu-id="9463f-245">Utilisé une connectivité internet tootest lors de la passerelle de hello est inaccessible par hello service Power BI.</span><span class="sxs-lookup"><span data-stu-id="9463f-245">Used tootest internet connectivity when hello gateway is unreachable by hello Power BI service.</span></span> | 

<span data-ttu-id="9463f-246">Si vous avez des adresses IP tooapprove plutôt que des domaines de hello, vous pouvez télécharger et utiliser hello [liste les plages IP de centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="9463f-246">If you have tooapprove IP addresses instead of hello domains, you can download and use hello [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="9463f-247">Dans certains cas, les connexions Azure Service Bus hello sont effectuées avec l’adresse IP plutôt que des noms de domaine qualifié complet.</span><span class="sxs-lookup"><span data-stu-id="9463f-247">In some cases, hello Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-hello-data-gateway-work"></a><span data-ttu-id="9463f-248">Comment fonctionne la passerelle de données hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-248">How does hello data gateway work?</span></span>

<span data-ttu-id="9463f-249">passerelle de données Hello facilite la communication rapide et sécurisée entre votre application logique, service de cloud de passerelle hello et votre source de données locale.</span><span class="sxs-lookup"><span data-stu-id="9463f-249">hello data gateway facilitates quick and secure communication between your logic app, hello gateway cloud service, and your on-premises data source.</span></span> 

![diagramme de flux de passerelle de données locale](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="9463f-251">Par conséquent, lorsque les utilisateur hello dans le cloud de hello interagit avec un élément qui s’est connecté tooyour local source de données :</span><span class="sxs-lookup"><span data-stu-id="9463f-251">So when hello user in hello cloud interacts with an element that's connected tooyour on-premises data source:</span></span>

1. <span data-ttu-id="9463f-252">service de cloud de passerelle Hello crée une requête avec informations d’identification hello chiffré de source de données hello et envoie la file d’attente de toohello de requêtes hello pour hello passerelle tooprocess.</span><span class="sxs-lookup"><span data-stu-id="9463f-252">hello gateway cloud service creates a query, along with hello encrypted credentials for hello data source, and sends hello query toohello queue for hello gateway tooprocess.</span></span>

2. <span data-ttu-id="9463f-253">service de cloud de passerelle Hello analyse hello requête et exécute un push de hello demande toohello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9463f-253">hello gateway cloud service analyzes hello query and pushes hello request toohello Azure Service Bus.</span></span>

3. <span data-ttu-id="9463f-254">passerelle de données locale Hello interroge hello Azure Service Bus pour les demandes en attente.</span><span class="sxs-lookup"><span data-stu-id="9463f-254">hello on-premises data gateway polls hello Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="9463f-255">passerelle de Hello obtient hello requête, déchiffre les informations d’identification hello et connecte la source de données toohello avec ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="9463f-255">hello gateway gets hello query, decrypts hello credentials, and connects toohello data source with those credentials.</span></span>

5. <span data-ttu-id="9463f-256">passerelle de Hello envoie hello toohello récupérer les données pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="9463f-256">hello gateway sends hello query toohello data source for execution.</span></span>

6. <span data-ttu-id="9463f-257">résultats de Hello sont envoyés à partir de la source de données hello, arrière toohello passerelle, puis toohello service de cloud de passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-257">hello results are sent from hello data source, back toohello gateway, and then toohello gateway cloud service.</span></span> <span data-ttu-id="9463f-258">Hello service cloud de passerelle utilise ensuite les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-258">hello gateway cloud service then uses hello results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="9463f-259">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="9463f-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="9463f-260">Généralités</span><span class="sxs-lookup"><span data-stu-id="9463f-260">General</span></span>

<span data-ttu-id="9463f-261">**Q**: ai-je besoin d’une passerelle pour les sources de données dans le cloud hello, telles que SQL Azure ?</span><span class="sxs-lookup"><span data-stu-id="9463f-261">**Q**: Do I need a gateway for data sources in hello cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="9463f-262">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="9463f-262">
**A**: No.</span></span> <span data-ttu-id="9463f-263">Une passerelle connecte à des sources de données tooon local uniquement.</span><span class="sxs-lookup"><span data-stu-id="9463f-263">A gateway connects tooon-premises data sources only.</span></span>

<span data-ttu-id="9463f-264">**Q**: passerelle de hello a-t-elle toobe installé sur hello même ordinateur en tant que source de données hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-264">**Q**: Does hello gateway have toobe installed on hello same machine as hello data source?</span></span> <br/><span data-ttu-id="9463f-265">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="9463f-265">
**A**: No.</span></span> <span data-ttu-id="9463f-266">passerelle de Hello connecte toohello source de données à l’aide des informations de connexion hello qui a été fournies.</span><span class="sxs-lookup"><span data-stu-id="9463f-266">hello gateway connects toohello data source using hello connection information that was provided.</span></span> <span data-ttu-id="9463f-267">Envisagez de passerelle de hello comme une application cliente en ce sens.</span><span class="sxs-lookup"><span data-stu-id="9463f-267">Consider hello gateway as a client application in this sense.</span></span> <span data-ttu-id="9463f-268">passerelle de Hello doit simplement hello capacité tooconnect toohello nom du serveur qui a été fourni.</span><span class="sxs-lookup"><span data-stu-id="9463f-268">hello gateway just needs hello capability tooconnect toohello server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="9463f-269">**Q**: Pourquoi dois-je utiliser un travail Azure ou établissement scolaire toosign compte dans ?</span><span class="sxs-lookup"><span data-stu-id="9463f-269">**Q**: Why must I use an Azure work or school account toosign in?</span></span> <br/><span data-ttu-id="9463f-270">
**Un**: vous pouvez uniquement utiliser un travail Azure ou scolaire compte lorsque vous installez la passerelle de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-270">
**A**: You can only use an Azure work or school account when you install hello on-premises data gateway.</span></span> <span data-ttu-id="9463f-271">Votre compte de connexion est stocké dans un client géré par Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9463f-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9463f-272">En règle générale, le nom de principal d’utilisateur (UPN) de votre compte Azure AD correspond à adresse de messagerie hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-272">Usually, your Azure AD account's user principal name (UPN) matches hello email address.</span></span>

<span data-ttu-id="9463f-273">**Q** : où mes informations d’identification sont-elles stockées ?</span><span class="sxs-lookup"><span data-stu-id="9463f-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="9463f-274">
**A**: informations d’identification hello que vous entrez pour une source de données sont chiffrées et stockées dans le service de cloud de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-274">
**A**: hello credentials that you enter for a data source are encrypted and stored in hello gateway cloud service.</span></span> <span data-ttu-id="9463f-275">informations d’identification Hello sont déchiffrées au niveau de la passerelle de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-275">hello credentials are decrypted at hello on-premises data gateway.</span></span>

<span data-ttu-id="9463f-276">**Q** : Existe-t-il des exigences concernant la bande passante réseau ?</span><span class="sxs-lookup"><span data-stu-id="9463f-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="9463f-277">
**R** : Nous vous recommandons d’utiliser une connexion réseau offrant un bon débit.</span><span class="sxs-lookup"><span data-stu-id="9463f-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="9463f-278">Chaque environnement est différent, et quantité hello des données envoyées affecte les résultats hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-278">Every environment is different, and hello amount of data being sent affects hello results.</span></span> <span data-ttu-id="9463f-279">À l’aide d’ExpressRoute peut aider à tooguarantee un niveau de débit entre hello centres de données Azure et locaux.</span><span class="sxs-lookup"><span data-stu-id="9463f-279">Using ExpressRoute could help tooguarantee a level of throughput between on-premises and hello Azure datacenters.</span></span>
<span data-ttu-id="9463f-280">Vous pouvez utiliser hello un outil tiers Azure Speed Test application toohelp jauge votre débit.</span><span class="sxs-lookup"><span data-stu-id="9463f-280">You can use hello third-party tool Azure Speed Test app toohelp gauge your throughput.</span></span>

<span data-ttu-id="9463f-281">**Q**: quelle est la latence hello pour la source de données en cours d’exécution des requêtes tooa à partir de la passerelle de hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-281">**Q**: What is hello latency for running queries tooa data source from hello gateway?</span></span> <span data-ttu-id="9463f-282">Quelle est la meilleure architecture de hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-282">What is hello best architecture?</span></span> <br/><span data-ttu-id="9463f-283">
**A**: tooreduce latence du réseau, passerelle de hello installer en tant que source de données toohello fermer que possible.</span><span class="sxs-lookup"><span data-stu-id="9463f-283">
**A**: tooreduce network latency, install hello gateway as close toohello data source as possible.</span></span> <span data-ttu-id="9463f-284">Si vous pouvez installer la passerelle de hello sur la source de données réelle hello, cette proximité réduit la latence de hello introduite.</span><span class="sxs-lookup"><span data-stu-id="9463f-284">If you can install hello gateway on hello actual data source, this proximity minimizes hello latency introduced.</span></span> <span data-ttu-id="9463f-285">Envisagez de centres de données hello trop.</span><span class="sxs-lookup"><span data-stu-id="9463f-285">Consider hello datacenters too.</span></span> <span data-ttu-id="9463f-286">Par exemple, si votre service utilise hello ouest des États-Unis centre de données, et que SQL Server est hébergé dans une machine virtuelle Azure, votre machine virtuelle Azure doit être trop Bonjour ouest des États-Unis.</span><span class="sxs-lookup"><span data-stu-id="9463f-286">For example, if your service uses hello West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in hello West US too.</span></span> <span data-ttu-id="9463f-287">Cette proximité réduit la latence et évite les frais de sortie sur hello machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="9463f-287">This proximity minimizes latency and avoids egress charges on hello Azure VM.</span></span>

<span data-ttu-id="9463f-288">**Q**: comment sont envoyées toohello arrière cloud ?</span><span class="sxs-lookup"><span data-stu-id="9463f-288">**Q**: How are results sent back toohello cloud?</span></span> <br/><span data-ttu-id="9463f-289">
**A**: les résultats sont envoyés via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9463f-289">
**A**: Results are sent through hello Azure Service Bus.</span></span>

<span data-ttu-id="9463f-290">**Q**: existe-t-il toute passerelle toohello de connexions entrantes à partir du cloud de hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-290">**Q**: Are there any inbound connections toohello gateway from hello cloud?</span></span> <br/><span data-ttu-id="9463f-291">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="9463f-291">
**A**: No.</span></span> <span data-ttu-id="9463f-292">passerelle de Hello utilise des connexions sortantes tooAzure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9463f-292">hello gateway uses outbound connections tooAzure Service Bus.</span></span>

<span data-ttu-id="9463f-293">**Q** : Que se passe-t-il si je bloque les connexions sortantes ?</span><span class="sxs-lookup"><span data-stu-id="9463f-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="9463f-294">Comment dois-je tooopen ?</span><span class="sxs-lookup"><span data-stu-id="9463f-294">What do I need tooopen?</span></span> <br/><span data-ttu-id="9463f-295">
**A**: consultez les ports hello et les hôtes qui hello passerelle utilise.</span><span class="sxs-lookup"><span data-stu-id="9463f-295">
**A**: See hello ports and hosts that hello gateway uses.</span></span>

<span data-ttu-id="9463f-296">**Q**: ce que le service de Windows hello réel est appelé ?</span><span class="sxs-lookup"><span data-stu-id="9463f-296">**Q**: What is hello actual Windows service called?</span></span><br/><span data-ttu-id="9463f-297">
**A**: dans les Services, passerelle de hello est appelé le Service Power BI Enterprise Gateway.</span><span class="sxs-lookup"><span data-stu-id="9463f-297">
**A**: In Services, hello gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="9463f-298">**Q**: pouvez hello service Windows de passerelle s’exécuter avec un compte Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="9463f-298">**Q**: Can hello gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="9463f-299">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="9463f-299">
**A**: No.</span></span> <span data-ttu-id="9463f-300">Hello service Windows doit avoir un compte Windows valide.</span><span class="sxs-lookup"><span data-stu-id="9463f-300">hello Windows service must have a valid Windows account.</span></span> <span data-ttu-id="9463f-301">Par défaut, le service de hello s’exécute avec hello SID de Service, NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="9463f-301">By default, hello service runs with hello Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="9463f-302">Haute disponibilité et récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="9463f-302">High availability and disaster recovery</span></span>

<span data-ttu-id="9463f-303">**Q** : Quelles sont les options de récupération d’urgence disponibles ?</span><span class="sxs-lookup"><span data-stu-id="9463f-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="9463f-304">
**Un**: vous pouvez utiliser toorestore de clé de récupération hello ou déplacer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="9463f-304">
**A**: You can use hello recovery key toorestore or move a gateway.</span></span> <span data-ttu-id="9463f-305">Lorsque vous installez la passerelle de hello, spécifiez la clé de récupération hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-305">When you install hello gateway, specify hello recovery key.</span></span>

<span data-ttu-id="9463f-306">**Q**: quels sont les avantages de hello de clé de récupération hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-306">**Q**: What is hello benefit of hello recovery key?</span></span> <br/><span data-ttu-id="9463f-307">
**A**: clé de récupération hello fournit un moyen toomigrate ou récupérer vos paramètres de passerelle après un sinistre.</span><span class="sxs-lookup"><span data-stu-id="9463f-307">
**A**: hello recovery key provides a way toomigrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="9463f-308">**Q**: existe-t-il des plans pour activer les scénarios de haute disponibilité avec la passerelle de hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-308">**Q**: Are there any plans for enabling high availability scenarios with hello gateway?</span></span> <br/><span data-ttu-id="9463f-309">
**A**: ces scénarios sont sur la feuille de route hello, mais nous n’avons pas encore une chronologie.</span><span class="sxs-lookup"><span data-stu-id="9463f-309">
**A**: These scenarios are on hello roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="9463f-310">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="9463f-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="9463f-311">**Q**: Comment puis-je savoir quelles requêtes sont envoyées source de données locale toohello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-311">**Q**: How can I see what queries are being sent toohello on-premises data source?</span></span> <br/><span data-ttu-id="9463f-312">
**Un**: vous pouvez activer le traçage de requête, qui inclut les requêtes hello qui sont envoyées.</span><span class="sxs-lookup"><span data-stu-id="9463f-312">
**A**: You can enable query tracing, which includes hello queries that are sent.</span></span> <span data-ttu-id="9463f-313">N’oubliez pas de requête toochange en remontant la valeur d’origine de toohello faite le problème résolu.</span><span class="sxs-lookup"><span data-stu-id="9463f-313">Remember toochange query tracing back toohello original value when done troubleshooting.</span></span> <span data-ttu-id="9463f-314">Le fait de laisser activé le traçage des requêtes contribue à augmenter la taille des journaux.</span><span class="sxs-lookup"><span data-stu-id="9463f-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="9463f-315">Vous pouvez également utiliser les outils de suivi des requêtes proposés par votre source de données.</span><span class="sxs-lookup"><span data-stu-id="9463f-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="9463f-316">Par exemple, vous pouvez utiliser Extended Events ou SQL Profiler for SQL Server et Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="9463f-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="9463f-317">**Q**: où se trouvent les journaux de passerelle hello ?</span><span class="sxs-lookup"><span data-stu-id="9463f-317">**Q**: Where are hello gateway logs?</span></span> <br/><span data-ttu-id="9463f-318">
**R**: Voir la section Outils plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="9463f-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-toohello-latest-version"></a><span data-ttu-id="9463f-319">Mettre à jour la version la plus récente toohello</span><span class="sxs-lookup"><span data-stu-id="9463f-319">Update toohello latest version</span></span>

<span data-ttu-id="9463f-320">Nombreux problèmes peuvent apparaître lors de la version de la passerelle hello devient obsolète.</span><span class="sxs-lookup"><span data-stu-id="9463f-320">Many issues can surface when hello gateway version becomes outdated.</span></span> <span data-ttu-id="9463f-321">Comme recommandé, assurez-vous d’utiliser la version la plus récente hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-321">As good general practice, make sure that you use hello latest version.</span></span> <span data-ttu-id="9463f-322">Si vous n’avez pas mis à jour de passerelle de hello pendant un mois ou plus, vous pouvez envisager d’installer la version la plus récente de la passerelle de hello hello et voir si vous pouvez reproduire le problème de hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-322">If you haven't updated hello gateway for a month or longer, you might consider installing hello latest version of hello gateway, and see if you can reproduce hello issue.</span></span>

### <a name="error-failed-tooadd-user-toogroup--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="9463f-323">Erreur : Échec de tooadd utilisateur toogroup.</span><span class="sxs-lookup"><span data-stu-id="9463f-323">Error: Failed tooadd user toogroup.</span></span> <span data-ttu-id="9463f-324">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="9463f-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="9463f-325">Vous pouvez obtenir cette erreur si vous essayez de passerelle de hello tooinstall sur un contrôleur de domaine, ce qui n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="9463f-325">You might get this error if you try tooinstall hello gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="9463f-326">Assurez-vous que vous déployez la passerelle de hello sur un ordinateur qui n’est pas un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="9463f-326">Make sure that you deploy hello gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="9463f-327">Outils</span><span class="sxs-lookup"><span data-stu-id="9463f-327">Tools</span></span>

### <a name="collect-logs-from-hello-gateway-configurer"></a><span data-ttu-id="9463f-328">Collecter les journaux à partir de la configurer de passerelle hello</span><span class="sxs-lookup"><span data-stu-id="9463f-328">Collect logs from hello gateway configurer</span></span>

<span data-ttu-id="9463f-329">Vous pouvez collecter plusieurs journaux pour la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-329">You can collect several logs for hello gateway.</span></span> <span data-ttu-id="9463f-330">Commencez toujours par les journaux de hello !</span><span class="sxs-lookup"><span data-stu-id="9463f-330">Always start with hello logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="9463f-331">Journaux du programme d’installation</span><span class="sxs-lookup"><span data-stu-id="9463f-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="9463f-332">Journaux de configuration</span><span class="sxs-lookup"><span data-stu-id="9463f-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="9463f-333">Journaux du service de passerelle Enterprise</span><span class="sxs-lookup"><span data-stu-id="9463f-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="9463f-334">Journaux d’événements</span><span class="sxs-lookup"><span data-stu-id="9463f-334">Event logs</span></span>

<span data-ttu-id="9463f-335">Vous trouverez hello les journaux de passerelle de gestion des données et PowerBIGateway sous **journaux des applications et Services**.</span><span class="sxs-lookup"><span data-stu-id="9463f-335">You can find hello Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="9463f-336">Trace Fiddler</span><span class="sxs-lookup"><span data-stu-id="9463f-336">Fiddler Trace</span></span>

<span data-ttu-id="9463f-337">[Fiddler](http://www.telerik.com/fiddler) est un outil gratuit développé par Telerik, qui surveille le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="9463f-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="9463f-338">Vous pouvez voir le trafic par le service Power BI à partir de l’ordinateur client de hello de hello.</span><span class="sxs-lookup"><span data-stu-id="9463f-338">You can see this traffic with hello Power BI service from hello client machine.</span></span> <span data-ttu-id="9463f-339">Ce service peut également indiquer les éventuelles erreurs et autres informations connexes.</span><span class="sxs-lookup"><span data-stu-id="9463f-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9463f-340">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="9463f-340">Next steps</span></span>
    
* [<span data-ttu-id="9463f-341">Se connecter tooon locale, les données à partir d’applications de logique</span><span class="sxs-lookup"><span data-stu-id="9463f-341">Connect tooon-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="9463f-342">Fonctionnalités d’intégration d'entreprise</span><span class="sxs-lookup"><span data-stu-id="9463f-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="9463f-343">Connecteurs pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="9463f-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
