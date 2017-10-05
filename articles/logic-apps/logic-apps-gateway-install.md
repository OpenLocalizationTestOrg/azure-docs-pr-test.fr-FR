---
title: "Installation d’une passerelle de données locale - Azure Logic Apps | Microsoft Docs"
description: "Avant d’accéder à des sources de données locales, installez la passerelle de données locale pour accélérer le transfert et le chiffrement de données entre les sources de données locales et les applications logiques."
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
ms.openlocfilehash: 34e68ae7d35019848b35c785a2715ec458dc6e73
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="install-the-on-premises-data-gateway-for-azure-logic-apps"></a><span data-ttu-id="2f50f-104">Installer la passerelle de données locale pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2f50f-104">Install the on-premises data gateway for Azure Logic Apps</span></span>

<span data-ttu-id="2f50f-105">Pour que vos applications logiques puissent accéder à des sources de données locales, vous devez installer et configurer la passerelle de données locale.</span><span class="sxs-lookup"><span data-stu-id="2f50f-105">Before your logic apps can access data sources on premises, you must install and set up the on-premises data gateway.</span></span> <span data-ttu-id="2f50f-106">La passerelle agit comme un pont permettant un transfert et un chiffrement de données rapides entre les systèmes locaux et vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="2f50f-106">The gateway acts as a bridge that provides quick data transfer and encryption between on-premises systems and your logic apps.</span></span> <span data-ttu-id="2f50f-107">La passerelle relaie les données des sources locales sur des canaux chiffrés via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2f50f-107">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="2f50f-108">Tout le trafic est initialisé en tant que trafic sortant de l’agent de passerelle sécurisé.</span><span class="sxs-lookup"><span data-stu-id="2f50f-108">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="2f50f-109">Pour en savoir plus, voir [Fonctionnement de la passerelle de données](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="2f50f-109">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

<span data-ttu-id="2f50f-110">La passerelle prend en charge les connexions aux sources de données locales suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f50f-110">The gateway supports connections to these data sources on premises:</span></span>

*   <span data-ttu-id="2f50f-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="2f50f-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="2f50f-112">DB2</span><span class="sxs-lookup"><span data-stu-id="2f50f-112">DB2</span></span>  
*   <span data-ttu-id="2f50f-113">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="2f50f-113">File System</span></span>
*   <span data-ttu-id="2f50f-114">Informix</span><span class="sxs-lookup"><span data-stu-id="2f50f-114">Informix</span></span>
*   <span data-ttu-id="2f50f-115">MQ</span><span class="sxs-lookup"><span data-stu-id="2f50f-115">MQ</span></span>
*   <span data-ttu-id="2f50f-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="2f50f-116">MySQL</span></span>
*   <span data-ttu-id="2f50f-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="2f50f-117">Oracle Database</span></span>
*   <span data-ttu-id="2f50f-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="2f50f-118">PostgreSQL</span></span>
*   <span data-ttu-id="2f50f-119">Serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="2f50f-119">SAP Application Server</span></span> 
*   <span data-ttu-id="2f50f-120">Serveur de messagerie SAP</span><span class="sxs-lookup"><span data-stu-id="2f50f-120">SAP Message Server</span></span>
*   <span data-ttu-id="2f50f-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="2f50f-121">SharePoint</span></span>
*   <span data-ttu-id="2f50f-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="2f50f-122">SQL Server</span></span>
*   <span data-ttu-id="2f50f-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="2f50f-123">Teradata</span></span>

<span data-ttu-id="2f50f-124">Ces étapes montrent comment installer la passerelle de données locale avant de [configurer une connexion entre la passerelle et vos applications logiques](./logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="2f50f-124">These steps show how to first install the on-premises data gateway before you [set up a connection between the gateway and your logic apps](./logic-apps-gateway-connection.md).</span></span> <span data-ttu-id="2f50f-125">Pour plus d’informations sur les connecteurs pris en charge, voir [Connecteurs pour Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span><span class="sxs-lookup"><span data-stu-id="2f50f-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](https://docs.microsoft.com/azure/connectors/apis-list).</span></span> 

<span data-ttu-id="2f50f-126">Pour plus d’informations sur l’utilisation de la passerelle avec d’autres services, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="2f50f-126">For information about how to use the gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="2f50f-127">Passerelle de données locale Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="2f50f-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="2f50f-128">Passerelle de données locale Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="2f50f-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="2f50f-129">Passerelle de données locale Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="2f50f-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="2f50f-130">Passerelle de données locale Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="2f50f-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

<a name="requirements"></a>
## <a name="requirements"></a><span data-ttu-id="2f50f-131">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="2f50f-131">Requirements</span></span>

<span data-ttu-id="2f50f-132">**Minimale** :</span><span class="sxs-lookup"><span data-stu-id="2f50f-132">**Minimum**:</span></span>

* <span data-ttu-id="2f50f-133">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="2f50f-133">.NET 4.5 Framework</span></span>
* <span data-ttu-id="2f50f-134">Version 64 bits de Windows 7 ou Windows Server 2008 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="2f50f-134">64-bit version of Windows 7 or Windows Server 2008 R2 (or later)</span></span>

<span data-ttu-id="2f50f-135">**Recommandée** :</span><span class="sxs-lookup"><span data-stu-id="2f50f-135">**Recommended**:</span></span>

* <span data-ttu-id="2f50f-136">Processeur 8 cœurs</span><span class="sxs-lookup"><span data-stu-id="2f50f-136">8 Core CPU</span></span>
* <span data-ttu-id="2f50f-137">8 Go de mémoire</span><span class="sxs-lookup"><span data-stu-id="2f50f-137">8 GB Memory</span></span>
* <span data-ttu-id="2f50f-138">Version 64 bits de Windows 2012 R2 (ou version ultérieure)</span><span class="sxs-lookup"><span data-stu-id="2f50f-138">64-bit version of Windows 2012 R2 (or later)</span></span>

<span data-ttu-id="2f50f-139">**Points importants à prendre en considération** :</span><span class="sxs-lookup"><span data-stu-id="2f50f-139">**Important considerations**:</span></span>

* <span data-ttu-id="2f50f-140">Installez la passerelle de données locale sur un seul ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="2f50f-140">Install the on-premises data gateway only on a local computer.</span></span>
<span data-ttu-id="2f50f-141">Vous ne pouvez pas installer la passerelle sur un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="2f50f-141">You can't install the gateway on a domain controller.</span></span>

   > [!TIP]
   > <span data-ttu-id="2f50f-142">Vous ne devez pas nécessairement installer la passerelle sur le même ordinateur que votre source de données.</span><span class="sxs-lookup"><span data-stu-id="2f50f-142">You don't have to install the gateway on the same computer as your data source.</span></span> <span data-ttu-id="2f50f-143">Pour réduire la latence, vous pouvez installer la passerelle le plus près possible de votre source de données, ou sur le même ordinateur, en supposant que vous disposiez des autorisations nécessaires.</span><span class="sxs-lookup"><span data-stu-id="2f50f-143">To minimize latency, you can install the gateway as close as possible to your data source, or on the same computer, assuming that you have permissions.</span></span>

* <span data-ttu-id="2f50f-144">N’installez pas la passerelle sur un ordinateur qui s’éteint, passe en mode veille ou ne se connecte pas à Internet, car la passerelle ne peut pas s’exécuter dans de telles circonstances.</span><span class="sxs-lookup"><span data-stu-id="2f50f-144">Don't install the gateway on a computer that turns off, goes to sleep, or doesn't connect to the Internet because the gateway can't run under those circumstances.</span></span> <span data-ttu-id="2f50f-145">De même, les performances de la passerelle peuvent être moindres sur un réseau sans fil.</span><span class="sxs-lookup"><span data-stu-id="2f50f-145">Also, gateway performance might suffer over a wireless network.</span></span>

* <span data-ttu-id="2f50f-146">Pendant l’installation, vous devez vous connecter avec un [compte professionnel ou scolaire](https://docs.microsoft.com/azure/active-directory/sign-up-organization) géré par Azure Active Directory (Azure AD), et non un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2f50f-146">During installation, you must sign in with a [work or school account](https://docs.microsoft.com/azure/active-directory/sign-up-organization) that's managed by Azure Active Directory (Azure AD), not a Microsoft account.</span></span> 

  <span data-ttu-id="2f50f-147">Vous devez utiliser le même compte professionnel ou scolaire par la suite dans le portail Azure lorsque vous créez et associez une ressource de passerelle à votre installation de passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-147">You have to use the same work or school account later in the Azure portal when you create and associate a gateway resource with your gateway installation.</span></span> <span data-ttu-id="2f50f-148">Vous sélectionnerez ensuite cette ressource de passerelle lors de la création de la connexion entre votre application logique et la source de données locale.</span><span class="sxs-lookup"><span data-stu-id="2f50f-148">You then select this gateway resource when you create the connection between your logic app and the on-premises data source.</span></span> [<span data-ttu-id="2f50f-149">Pourquoi dois-je utiliser un compte professionnel ou scolaire Azure AD ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-149">Why must I use an Azure AD work or school account?</span></span>](#why-azure-work-school-account)

  > [!TIP]
  > <span data-ttu-id="2f50f-150">Si vous avez souscrit une offre Office 365 sans fournir votre adresse de messagerie professionnelle réelle, votre adresse de connexion peut ressembler à ceci : jeff@contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="2f50f-150">If you signed up for an Office 365 offering and didn't supply your actual work email, your sign-in address might look like jeff@contoso.onmicrosoft.com.</span></span> 

* <span data-ttu-id="2f50f-151">Si vous disposez d’une passerelle existante que vous configurez avec un programme d’installation antérieur à la version 14.16.6317.4, vous ne pouvez pas modifier l’emplacement de votre passerelle en exécutant le programme d’installation le plus récent.</span><span class="sxs-lookup"><span data-stu-id="2f50f-151">If you have an existing gateway that you set up with an installer that's earlier than version 14.16.6317.4, you can't change your gateway's location by running the latest installer.</span></span> <span data-ttu-id="2f50f-152">Toutefois, vous pouvez utiliser le programme d’installation le plus récent pour configurer une nouvelle passerelle avec l’emplacement que vous souhaitez à la place.</span><span class="sxs-lookup"><span data-stu-id="2f50f-152">However, you can use the latest installer to set up a new gateway with the location that you want instead.</span></span>
  
  <span data-ttu-id="2f50f-153">Si vous avez un programme d’installation de passerelle antérieur à la version 14.16.6317.4, mais n’avez pas encore installé votre passerelle, vous pouvez télécharger et utiliser le programme d’installation le plus récent.</span><span class="sxs-lookup"><span data-stu-id="2f50f-153">If you have a gateway installer that's earlier than version 14.16.6317.4, but you haven't installed your gateway yet, you can download and use the latest installer.</span></span>

<a name="install-gateway"></a>

## <a name="install-the-data-gateway"></a><span data-ttu-id="2f50f-154">Installer la passerelle de données</span><span class="sxs-lookup"><span data-stu-id="2f50f-154">Install the data gateway</span></span>

1.  <span data-ttu-id="2f50f-155">[Téléchargez et exécutez le programme d’installation de passerelle sur un ordinateur local](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="2f50f-155">[Download and run the gateway installer on a local computer](http://go.microsoft.com/fwlink/?LinkID=820931&clcid=0x409).</span></span>

2. <span data-ttu-id="2f50f-156">Lisez et acceptez les conditions d’utilisation et la déclaration de confidentialité.</span><span class="sxs-lookup"><span data-stu-id="2f50f-156">Review and accept the terms of use and privacy statement.</span></span>

3. <span data-ttu-id="2f50f-157">Spécifiez le chemin d’accès sur votre ordinateur local où vous souhaitez installer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-157">Specify the path on your local computer where you want to install the gateway.</span></span>

4. <span data-ttu-id="2f50f-158">Lorsque vous y êtes invité, connectez-vous à votre compte Azure professionnel ou scolaire, pas à un compte Microsoft.</span><span class="sxs-lookup"><span data-stu-id="2f50f-158">When prompted, sign in with your Azure work or school account, not a Microsoft account.</span></span>

   ![Connexion avec le compte professionnel ou scolaire Azure](./media/logic-apps-gateway-install/sign-in-gateway-install.png)

5. <span data-ttu-id="2f50f-160">Inscrivez maintenant la passerelle installée auprès du [service cloud de passerelle](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="2f50f-160">Now register your installed gateway with the [gateway cloud service](#gateway-cloud-service).</span></span> <span data-ttu-id="2f50f-161">Choisissez **Inscrivez une nouvelle passerelle sur cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="2f50f-161">Choose **Register a new gateway on this computer**.</span></span>

   <span data-ttu-id="2f50f-162">Le service cloud de passerelle chiffre et stocke les informations d’identification de votre source de données et les détails de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-162">The gateway cloud service encrypts and stores your data source credentials and gateway details.</span></span> 
   <span data-ttu-id="2f50f-163">Le service achemine également les requêtes et leurs résultats entre votre application logique, la passerelle de données locale et votre source de données locale.</span><span class="sxs-lookup"><span data-stu-id="2f50f-163">The service also routes queries and their results between your logic app, the on-premises data gateway, and your data source on premises.</span></span>

6. <span data-ttu-id="2f50f-164">Entrez un nom pour votre installation de passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-164">Provide a name for your gateway installation.</span></span> <span data-ttu-id="2f50f-165">Créez une clé de récupération, puis confirmez votre clé de récupération.</span><span class="sxs-lookup"><span data-stu-id="2f50f-165">Create a recovery key, then confirm your recovery key.</span></span> 

   > [!IMPORTANT] 
   > <span data-ttu-id="2f50f-166">Votre clé de récupération doit contenir au moins huit caractères.</span><span class="sxs-lookup"><span data-stu-id="2f50f-166">Your recovery key must contain at least eight characters.</span></span> <span data-ttu-id="2f50f-167">Veillez à enregistrer et à conserver la clé en lieu sûr.</span><span class="sxs-lookup"><span data-stu-id="2f50f-167">Make sure that you save and keep the key in a safe place.</span></span> <span data-ttu-id="2f50f-168">Vous avez également besoin de cette clé pour migrer, restaurer ou contrôler une passerelle existante.</span><span class="sxs-lookup"><span data-stu-id="2f50f-168">You also need this key when you want to migrate, restore, or take over an existing gateway.</span></span>

   1. <span data-ttu-id="2f50f-169">Pour modifier la région par défaut pour le service cloud de passerelle et l’Azure Service Bus utilisé par votre installation de passerelle, choisissez **Changer la région**.</span><span class="sxs-lookup"><span data-stu-id="2f50f-169">To change the default region for the gateway cloud service and Azure Service Bus used by your gateway installation, choose **Change Region**.</span></span>

      ![Modification de la région](./media/logic-apps-gateway-install/change-region-gateway-install.png)

      <span data-ttu-id="2f50f-171">La région par défaut est la région associée à votre client Azure AD.</span><span class="sxs-lookup"><span data-stu-id="2f50f-171">The default region is the region associated with your Azure AD tenant.</span></span>

   2. <span data-ttu-id="2f50f-172">Dans le volet suivant, cliquez sur la liste déroulante **Sélectionnez une région** pour choisir une autre région.</span><span class="sxs-lookup"><span data-stu-id="2f50f-172">On the next pane, open the **Select Region** to choose a different region.</span></span>

      ![Sélection d’une autre région](./media/logic-apps-gateway-install/select-region-gateway-install.png)

      <span data-ttu-id="2f50f-174">Par exemple, vous pouvez sélectionner la même région que celle de votre application logique, ou sélectionner la région la plus proche de votre source de données locale afin de réduire la latence.</span><span class="sxs-lookup"><span data-stu-id="2f50f-174">For example, you might select the same region as your logic app, or select the region closest to your on-premises data source so you can reduce latency.</span></span> <span data-ttu-id="2f50f-175">Votre ressource de passerelle et votre application logique se trouvent dans des emplacements différents.</span><span class="sxs-lookup"><span data-stu-id="2f50f-175">Your gateway resource and logic app can have different locations.</span></span>

      > [!IMPORTANT]
      > <span data-ttu-id="2f50f-176">Vous ne pouvez pas modifier cette région après l’installation.</span><span class="sxs-lookup"><span data-stu-id="2f50f-176">You can't change this region after installation.</span></span> <span data-ttu-id="2f50f-177">Cette région détermine et restreint également l’emplacement où vous pouvez créer la ressource Azure pour votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-177">This region also determines and restricts the location where you can create the Azure resource for your gateway.</span></span> <span data-ttu-id="2f50f-178">Par conséquent, lorsque vous créez votre ressource de passerelle dans Azure, assurez-vous que l’emplacement de la ressource correspond à la région que vous avez sélectionnée lors de l’installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-178">So when you create your gateway resource in Azure, make sure that the resource location matches the region that you selected during gateway installation.</span></span>
      > 
      > <span data-ttu-id="2f50f-179">Si vous souhaitez utiliser une autre région pour votre passerelle ultérieurement, vous devrez configurer une nouvelle passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-179">If you want to use a different region for your gateway later, you must set up a new gateway.</span></span>

   3. <span data-ttu-id="2f50f-180">Une fois ces opérations effectuées, sélectionnez **Terminé**.</span><span class="sxs-lookup"><span data-stu-id="2f50f-180">When you're ready, choose **Done**.</span></span>

7. <span data-ttu-id="2f50f-181">Suivez à présent ces étapes dans le portail Azure pour [créer une ressource Azure pour votre passerelle](../logic-apps/logic-apps-gateway-connection.md).</span><span class="sxs-lookup"><span data-stu-id="2f50f-181">Now follow these steps in the Azure portal so you can [create an Azure resource for your gateway](../logic-apps/logic-apps-gateway-connection.md).</span></span> 

<span data-ttu-id="2f50f-182">Pour en savoir plus, voir [Fonctionnement de la passerelle de données](#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="2f50f-182">Learn more about [how the data gateway works](#gateway-cloud-service).</span></span>

## <a name="migrate-restore-or-take-over-an-existing-gateway"></a><span data-ttu-id="2f50f-183">Migrer, restaurer ou contrôler une passerelle existante</span><span class="sxs-lookup"><span data-stu-id="2f50f-183">Migrate, restore, or take over an existing gateway</span></span>

<span data-ttu-id="2f50f-184">Pour effectuer ces tâches, vous devez disposer de la clé de récupération spécifiée lors de l’installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-184">To perform these tasks, you must have the recovery key that was specified when the gateway was installed.</span></span>

1. <span data-ttu-id="2f50f-185">Dans le menu Démarrer de votre ordinateur, choisissez **Passerelle de données locale**.</span><span class="sxs-lookup"><span data-stu-id="2f50f-185">From your computer's Start menu, choose **On-premises data gateway**.</span></span>

2. <span data-ttu-id="2f50f-186">Une fois le programme d’installation ouvert, connectez-vous avec le compte professionnel ou scolaire utilisé précédemment pour installer la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-186">After the installer opens, sign in with the same Azure work or school account that was previously used to install the gateway.</span></span>

3. <span data-ttu-id="2f50f-187">Choisissez **Migrer, restaurer ou contrôler une passerelle existante**.</span><span class="sxs-lookup"><span data-stu-id="2f50f-187">Choose **Migrate, restore, or take over an existing gateway**.</span></span>

4. <span data-ttu-id="2f50f-188">Fournissez le nom et la clé de récupération de la passerelle que vous souhaitez migrer, restaurer ou contrôler.</span><span class="sxs-lookup"><span data-stu-id="2f50f-188">Provide the name and recovery key for the gateway that you want to migrate, restore, or take over.</span></span>

<a name="restart-gateway"></a>
## <a name="restart-the-gateway"></a><span data-ttu-id="2f50f-189">Redémarrez la passerelle</span><span class="sxs-lookup"><span data-stu-id="2f50f-189">Restart the gateway</span></span>

<span data-ttu-id="2f50f-190">La passerelle s’exécute en tant que service Windows.</span><span class="sxs-lookup"><span data-stu-id="2f50f-190">The gateway runs as a Windows service.</span></span> <span data-ttu-id="2f50f-191">Comme tout autre service Windows, vous pouvez démarrer et arrêter ce service de plusieurs façons.</span><span class="sxs-lookup"><span data-stu-id="2f50f-191">Like any other Windows service, you can start and stop the service in multiple ways.</span></span> <span data-ttu-id="2f50f-192">Par exemple, vous pouvez ouvrir une invite de commandes avec des autorisations élevées sur l’ordinateur sur lequel la passerelle s’exécute, puis exécuter l’une des commandes suivantes :</span><span class="sxs-lookup"><span data-stu-id="2f50f-192">For example, you can open a command prompt with elevated permissions on the computer where the gateway is running, and run either these commands:</span></span>

* <span data-ttu-id="2f50f-193">Pour arrêter le service, exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="2f50f-193">To stop the service, run this command:</span></span>
  
    `net stop PBIEgwService`

* <span data-ttu-id="2f50f-194">Pour démarrer le service, exécutez cette commande :</span><span class="sxs-lookup"><span data-stu-id="2f50f-194">To start the service, run this command:</span></span>
  
    `net start PBIEgwService`

### <a name="windows-service-account"></a><span data-ttu-id="2f50f-195">Compte de service Windows</span><span class="sxs-lookup"><span data-stu-id="2f50f-195">Windows service account</span></span>

<span data-ttu-id="2f50f-196">La passerelle de données locale est configurée pour utiliser `NT SERVICE\PBIEgwService` pour les informations d’identification de connexion au service Windows.</span><span class="sxs-lookup"><span data-stu-id="2f50f-196">The on-premises data gateway is set up to use `NT SERVICE\PBIEgwService` for the Windows service logon credentials.</span></span> <span data-ttu-id="2f50f-197">Par défaut, la passerelle dispose du droit « Ouvrir une session en tant que service » sur l’ordinateur sur lequel vous installez la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-197">By default, the gateway has the "Log on as a service" right for the machine where you install the gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="2f50f-198">Le compte de service Windows diffère du compte utilisé pour la connexion à des sources de données locales, et du compte professionnel ou scolaire Azure utilisé pour se connecter aux services cloud.</span><span class="sxs-lookup"><span data-stu-id="2f50f-198">The Windows service account differs from the account used for connecting to on-premises data sources, and from the Azure work or school account used to sign in to cloud services.</span></span>

## <a name="configure-a-firewall-or-proxy"></a><span data-ttu-id="2f50f-199">Configuration d’un pare-feu ou d’un proxy</span><span class="sxs-lookup"><span data-stu-id="2f50f-199">Configure a firewall or proxy</span></span>

<span data-ttu-id="2f50f-200">La passerelle crée une connexion sortante vers [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="2f50f-200">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="2f50f-201">Pour spécifier les informations proxy pour votre passerelle, consultez [Configurer les paramètres proxy](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span><span class="sxs-lookup"><span data-stu-id="2f50f-201">To provide proxy information for your gateway, see [Configure proxy settings](https://powerbi.microsoft.com/documentation/powerbi-gateway-proxy/).</span></span>

<span data-ttu-id="2f50f-202">Pour vérifier si votre pare-feu ou proxy risque de bloquer des connexions, vérifiez que votre ordinateur peut réellement se connecter à Internet et à [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span><span class="sxs-lookup"><span data-stu-id="2f50f-202">To check whether your firewall, or proxy, might block connections, confirm whether your machine can actually connect to the internet and the [Azure Service Bus](https://azure.microsoft.com/services/service-bus/).</span></span> <span data-ttu-id="2f50f-203">À partir d’une invite PowerShell, exécutez la commande suivante :</span><span class="sxs-lookup"><span data-stu-id="2f50f-203">From a PowerShell prompt, run this command:</span></span>

`Test-NetConnection -ComputerName watchdog.servicebus.windows.net -Port 9350`

> [!NOTE]
> <span data-ttu-id="2f50f-204">Cette commande teste uniquement la connectivité réseau et la connectivité à Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2f50f-204">This command only tests network connectivity and connectivity to the Azure Service Bus.</span></span> <span data-ttu-id="2f50f-205">Par conséquent, la commande n’a rien à voir avec la passerelle ou le service cloud de passerelle qui chiffre et stocke vos informations d’identification et les détails de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-205">So the command doesn't have anything to do with the gateway or the gateway cloud service that encrypts and stores your credentials and gateway details.</span></span> 
>
> <span data-ttu-id="2f50f-206">Par ailleurs, cette commande est disponible uniquement sur Windows Server 2012 R2 ou version ultérieure, et sur Windows 8.1 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="2f50f-206">Also, this command is only available on Windows Server 2012 R2 or later, and Windows 8.1 or later.</span></span> <span data-ttu-id="2f50f-207">Dans les versions de système d’exploitation antérieures, vous pouvez utiliser Telnet pour tester la connectivité.</span><span class="sxs-lookup"><span data-stu-id="2f50f-207">On earlier OS versions, you can use Telnet to test connectivity.</span></span> <span data-ttu-id="2f50f-208">Pour en savoir plus, voir [Solutions Azure Service Bus et hybrides](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="2f50f-208">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

<span data-ttu-id="2f50f-209">Les résultats devraient être similaires à cet exemple :</span><span class="sxs-lookup"><span data-stu-id="2f50f-209">Your results should look similar to this example:</span></span>

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

<span data-ttu-id="2f50f-210">Si **TcpTestSucceeded** n’est pas défini sur **true**, il se peut que vous soyez bloqué par un pare-feu.</span><span class="sxs-lookup"><span data-stu-id="2f50f-210">If **TcpTestSucceeded** is not set to **True**, you might be blocked by a firewall.</span></span> <span data-ttu-id="2f50f-211">Pour être exhaustif, remplacez les valeurs **ComputerName** et **Port** par celles répertoriées dans la section [Configurer les ports](#configure-ports) de cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="2f50f-211">If you want to be comprehensive, substitute the **ComputerName** and **Port** values with the values listed under [Configure ports](#configure-ports) in this topic.</span></span>

<span data-ttu-id="2f50f-212">Le pare-feu peut également bloquer des connexions qu’Azure Service Bus tente d’établir avec des centres de données Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f50f-212">The firewall might also block connections that the Azure Service Bus makes to the Azure datacenters.</span></span> <span data-ttu-id="2f50f-213">Si ce scénario se produit, approuvez (débloquez) toutes les adresses IP de ces centres de données dans votre région.</span><span class="sxs-lookup"><span data-stu-id="2f50f-213">If this scenario happens, approve (unblock) all the IP addresses for those datacenters in your region.</span></span> <span data-ttu-id="2f50f-214">Pour ces adresses IP, vous pouvez [obtenir la liste des adresses IP Azure ici](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="2f50f-214">For those IP addresses, [get the Azure IP addresses list here](https://www.microsoft.com/download/details.aspx?id=41653).</span></span>

## <a name="configure-ports"></a><span data-ttu-id="2f50f-215">Configuration des ports</span><span class="sxs-lookup"><span data-stu-id="2f50f-215">Configure ports</span></span>

<span data-ttu-id="2f50f-216">La passerelle crée une connexion sortante vers [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) et communique sur les ports de sortie suivants : TCP 443 (par défaut), 5671, 5672 et 9350 à 9354.</span><span class="sxs-lookup"><span data-stu-id="2f50f-216">The gateway creates an outbound connection to [Azure Service Bus](https://azure.microsoft.com/services/service-bus/) and communicates on outbound ports: TCP 443 (default), 5671, 5672, 9350 through 9354.</span></span> <span data-ttu-id="2f50f-217">La passerelle ne nécessite pas de ports entrants.</span><span class="sxs-lookup"><span data-stu-id="2f50f-217">The gateway doesn't require inbound ports.</span></span> <span data-ttu-id="2f50f-218">Pour en savoir plus, voir [Solutions Azure Service Bus et hybrides](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="2f50f-218">Learn more about [Azure Service Bus and hybrid solutions](../service-bus-messaging/service-bus-fundamentals-hybrid-solutions.md).</span></span>

| <span data-ttu-id="2f50f-219">NOMS DE DOMAINE</span><span class="sxs-lookup"><span data-stu-id="2f50f-219">DOMAIN NAMES</span></span> | <span data-ttu-id="2f50f-220">PORTS SORTANTS</span><span class="sxs-lookup"><span data-stu-id="2f50f-220">OUTBOUND PORTS</span></span> | <span data-ttu-id="2f50f-221">DESCRIPTION</span><span class="sxs-lookup"><span data-stu-id="2f50f-221">DESCRIPTION</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2f50f-222">*.analysis.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f50f-222">*.analysis.windows.net</span></span> | <span data-ttu-id="2f50f-223">443</span><span class="sxs-lookup"><span data-stu-id="2f50f-223">443</span></span> | <span data-ttu-id="2f50f-224">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2f50f-224">HTTPS</span></span> | 
| <span data-ttu-id="2f50f-225">*.login.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f50f-225">*.login.windows.net</span></span> | <span data-ttu-id="2f50f-226">443</span><span class="sxs-lookup"><span data-stu-id="2f50f-226">443</span></span> | <span data-ttu-id="2f50f-227">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2f50f-227">HTTPS</span></span> | 
| <span data-ttu-id="2f50f-228">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f50f-228">*.servicebus.windows.net</span></span> | <span data-ttu-id="2f50f-229">5671-5672</span><span class="sxs-lookup"><span data-stu-id="2f50f-229">5671-5672</span></span> | <span data-ttu-id="2f50f-230">Advanced Message Queuing Protocol (AMQP)</span><span class="sxs-lookup"><span data-stu-id="2f50f-230">Advanced Message Queuing Protocol (AMQP)</span></span> | 
| <span data-ttu-id="2f50f-231">*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f50f-231">*.servicebus.windows.net</span></span> | <span data-ttu-id="2f50f-232">443, 9350-9354</span><span class="sxs-lookup"><span data-stu-id="2f50f-232">443, 9350-9354</span></span> | <span data-ttu-id="2f50f-233">Récepteurs du Service Bus Relay sur TCP (nécessite le port 443 pour l’acquisition du jeton Access Control)</span><span class="sxs-lookup"><span data-stu-id="2f50f-233">Listeners on Service Bus Relay over TCP (requires 443 for Access Control token acquisition)</span></span> | 
| <span data-ttu-id="2f50f-234">*.frontend.clouddatahub.net</span><span class="sxs-lookup"><span data-stu-id="2f50f-234">*.frontend.clouddatahub.net</span></span> | <span data-ttu-id="2f50f-235">443</span><span class="sxs-lookup"><span data-stu-id="2f50f-235">443</span></span> | <span data-ttu-id="2f50f-236">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2f50f-236">HTTPS</span></span> | 
| <span data-ttu-id="2f50f-237">*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="2f50f-237">*.core.windows.net</span></span> | <span data-ttu-id="2f50f-238">443</span><span class="sxs-lookup"><span data-stu-id="2f50f-238">443</span></span> | <span data-ttu-id="2f50f-239">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2f50f-239">HTTPS</span></span> | 
| <span data-ttu-id="2f50f-240">login.microsoftonline.com</span><span class="sxs-lookup"><span data-stu-id="2f50f-240">login.microsoftonline.com</span></span> | <span data-ttu-id="2f50f-241">443</span><span class="sxs-lookup"><span data-stu-id="2f50f-241">443</span></span> | <span data-ttu-id="2f50f-242">HTTPS</span><span class="sxs-lookup"><span data-stu-id="2f50f-242">HTTPS</span></span> | 
| <span data-ttu-id="2f50f-243">*.msftncsi.com</span><span class="sxs-lookup"><span data-stu-id="2f50f-243">*.msftncsi.com</span></span> | <span data-ttu-id="2f50f-244">443</span><span class="sxs-lookup"><span data-stu-id="2f50f-244">443</span></span> | <span data-ttu-id="2f50f-245">Permet de tester la connectivité Internet lorsque la passerelle est inaccessible par le service Power BI.</span><span class="sxs-lookup"><span data-stu-id="2f50f-245">Used to test internet connectivity when the gateway is unreachable by the Power BI service.</span></span> | 

<span data-ttu-id="2f50f-246">Si vous devez mettre sur liste approuvée des adresses IP au lieu des domaines, vous pouvez télécharger et utiliser la [liste des plages d’adresses IP du centre de données Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=41653).</span><span class="sxs-lookup"><span data-stu-id="2f50f-246">If you have to approve IP addresses instead of the domains, you can download and use the [Microsoft Azure Datacenter IP ranges list](https://www.microsoft.com/download/details.aspx?id=41653).</span></span> <span data-ttu-id="2f50f-247">Dans certains cas, les connexions Azure Service Bus s’effectuent avec l’adresse IP plutôt qu’avec le nom de domaine complet.</span><span class="sxs-lookup"><span data-stu-id="2f50f-247">In some cases, the Azure Service Bus connections are made with IP Address rather than fully qualified domain names.</span></span>

<a name="gateway-cloud-service"></a>
## <a name="how-does-the-data-gateway-work"></a><span data-ttu-id="2f50f-248">Fonctionnement de la passerelle de données</span><span class="sxs-lookup"><span data-stu-id="2f50f-248">How does the data gateway work?</span></span>

<span data-ttu-id="2f50f-249">La passerelle de données assure une communication rapide et sécurisée entre votre application logique, le service cloud de passerelle et votre source de données locale.</span><span class="sxs-lookup"><span data-stu-id="2f50f-249">The data gateway facilitates quick and secure communication between your logic app, the gateway cloud service, and your on-premises data source.</span></span> 

![diagramme de flux de passerelle de données locale](./media/logic-apps-gateway-install/how-on-premises-data-gateway-works-flow-diagram.png)

<span data-ttu-id="2f50f-251">Ainsi, quand l’utilisateur dans le cloud interagit avec un élément connecté à votre source de données locale :</span><span class="sxs-lookup"><span data-stu-id="2f50f-251">So when the user in the cloud interacts with an element that's connected to your on-premises data source:</span></span>

1. <span data-ttu-id="2f50f-252">Le service cloud de passerelle crée une requête, ainsi que les informations d’identification chiffrées pour la source de données, puis envoie la requête vers la file d’attente afin que la passerelle la traite.</span><span class="sxs-lookup"><span data-stu-id="2f50f-252">The gateway cloud service creates a query, along with the encrypted credentials for the data source, and sends the query to the queue for the gateway to process.</span></span>

2. <span data-ttu-id="2f50f-253">Le service cloud de passerelle analyse la requête et envoie les demandes à Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2f50f-253">The gateway cloud service analyzes the query and pushes the request to the Azure Service Bus.</span></span>

3. <span data-ttu-id="2f50f-254">La passerelle de données locale interroge Azure Service Bus pour connaître les requêtes en attente.</span><span class="sxs-lookup"><span data-stu-id="2f50f-254">The on-premises data gateway polls the Azure Service Bus for pending requests.</span></span>

4. <span data-ttu-id="2f50f-255">La passerelle reçoit la requête, déchiffre les informations d’identification et se connecte à la source de données avec ces informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="2f50f-255">The gateway gets the query, decrypts the credentials, and connects to the data source with those credentials.</span></span>

5. <span data-ttu-id="2f50f-256">La passerelle envoie la requête à la source de données pour exécution.</span><span class="sxs-lookup"><span data-stu-id="2f50f-256">The gateway sends the query to the data source for execution.</span></span>

6. <span data-ttu-id="2f50f-257">Les résultats sont renvoyés de la source de données vers la passerelle, puis au service cloud de passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-257">The results are sent from the data source, back to the gateway, and then to the gateway cloud service.</span></span> <span data-ttu-id="2f50f-258">Le service cloud de passerelle utilise ensuite les résultats.</span><span class="sxs-lookup"><span data-stu-id="2f50f-258">The gateway cloud service then uses the results.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="2f50f-259">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="2f50f-259">Frequently asked questions</span></span>

### <a name="general"></a><span data-ttu-id="2f50f-260">Généralités</span><span class="sxs-lookup"><span data-stu-id="2f50f-260">General</span></span>

<span data-ttu-id="2f50f-261">**Q**: Ai-je besoin d’une passerelle pour des sources de données dans le cloud telles que SQL Azure ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-261">**Q**: Do I need a gateway for data sources in the cloud, such as SQL Azure?</span></span> <br/><span data-ttu-id="2f50f-262">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="2f50f-262">
**A**: No.</span></span> <span data-ttu-id="2f50f-263">Une passerelle se connecte uniquement aux sources de données locales.</span><span class="sxs-lookup"><span data-stu-id="2f50f-263">A gateway connects to on-premises data sources only.</span></span>

<span data-ttu-id="2f50f-264">**Q** : La passerelle doit-elle être installée sur le même ordinateur que la source de données ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-264">**Q**: Does the gateway have to be installed on the same machine as the data source?</span></span> <br/><span data-ttu-id="2f50f-265">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="2f50f-265">
**A**: No.</span></span> <span data-ttu-id="2f50f-266">La passerelle se connecte à la source de données en utilisant les informations de connexion fournies.</span><span class="sxs-lookup"><span data-stu-id="2f50f-266">The gateway connects to the data source using the connection information that was provided.</span></span> <span data-ttu-id="2f50f-267">En ce sens, considérez la passerelle comme une application cliente.</span><span class="sxs-lookup"><span data-stu-id="2f50f-267">Consider the gateway as a client application in this sense.</span></span> <span data-ttu-id="2f50f-268">La passerelle doit juste être en mesure de se connecter au nom du serveur qui a été fourni.</span><span class="sxs-lookup"><span data-stu-id="2f50f-268">The gateway just needs the capability to connect to the server name that was provided.</span></span>

<a name="why-azure-work-school-account"></a>

<span data-ttu-id="2f50f-269">**Q** : Pourquoi dois-je utiliser un compte professionnel ou scolaire Azure pour me connecter ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-269">**Q**: Why must I use an Azure work or school account to sign in?</span></span> <br/><span data-ttu-id="2f50f-270">
**R** : lorsque vous installez la passerelle de données locale, vous pouvez uniquement utiliser un compte professionnel ou scolaire Azure.</span><span class="sxs-lookup"><span data-stu-id="2f50f-270">
**A**: You can only use an Azure work or school account when you install the on-premises data gateway.</span></span> <span data-ttu-id="2f50f-271">Votre compte de connexion est stocké dans un client géré par Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="2f50f-271">Your sign-in account is stored in a tenant that's managed by Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="2f50f-272">En règle générale, le nom d’utilisateur principal (UPN) de votre compte Azure AD correspond à l’adresse de messagerie.</span><span class="sxs-lookup"><span data-stu-id="2f50f-272">Usually, your Azure AD account's user principal name (UPN) matches the email address.</span></span>

<span data-ttu-id="2f50f-273">**Q** : où mes informations d’identification sont-elles stockées ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-273">**Q**: Where are my credentials stored?</span></span> <br/><span data-ttu-id="2f50f-274">
**R** : Les informations d’identification que vous entrez pour une source de données sont chiffrées et stockées dans le service cloud de passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-274">
**A**: The credentials that you enter for a data source are encrypted and stored in the gateway cloud service.</span></span> <span data-ttu-id="2f50f-275">Les informations d’identification sont déchiffrées au niveau de la passerelle de données locale.</span><span class="sxs-lookup"><span data-stu-id="2f50f-275">The credentials are decrypted at the on-premises data gateway.</span></span>

<span data-ttu-id="2f50f-276">**Q** : Existe-t-il des exigences concernant la bande passante réseau ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-276">**Q**: Are there any requirements for network bandwidth?</span></span> <br/><span data-ttu-id="2f50f-277">
**R** : Nous vous recommandons d’utiliser une connexion réseau offrant un bon débit.</span><span class="sxs-lookup"><span data-stu-id="2f50f-277">
**A**: We recommend that your network connection has good throughput.</span></span> <span data-ttu-id="2f50f-278">Chaque environnement est différent et la quantité de données envoyées affecte les résultats.</span><span class="sxs-lookup"><span data-stu-id="2f50f-278">Every environment is different, and the amount of data being sent affects the results.</span></span> <span data-ttu-id="2f50f-279">ExpressRoute peut vous aider à garantir un niveau de débit approprié entre les centres de données locaux et les centres de données Azure.</span><span class="sxs-lookup"><span data-stu-id="2f50f-279">Using ExpressRoute could help to guarantee a level of throughput between on-premises and the Azure datacenters.</span></span>
<span data-ttu-id="2f50f-280">Vous pouvez utiliser l’application tierce Azure Speed Test pour mesurer votre débit.</span><span class="sxs-lookup"><span data-stu-id="2f50f-280">You can use the third-party tool Azure Speed Test app to help gauge your throughput.</span></span>

<span data-ttu-id="2f50f-281">**Q** : Quelle est la latence d’exécution des requêtes adressées à une source de données à partir de la passerelle ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-281">**Q**: What is the latency for running queries to a data source from the gateway?</span></span> <span data-ttu-id="2f50f-282">Quelle est la meilleure architecture ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-282">What is the best architecture?</span></span> <br/><span data-ttu-id="2f50f-283">
**R** : Pour réduire la latence du réseau, installez la passerelle le plus près possible de la source de données.</span><span class="sxs-lookup"><span data-stu-id="2f50f-283">
**A**: To reduce network latency, install the gateway as close to the data source as possible.</span></span> <span data-ttu-id="2f50f-284">Si vous pouvez installer la passerelle sur la source de données réelle, cette proximité réduit le temps de latence.</span><span class="sxs-lookup"><span data-stu-id="2f50f-284">If you can install the gateway on the actual data source, this proximity minimizes the latency introduced.</span></span> <span data-ttu-id="2f50f-285">Songez également aux centres de données.</span><span class="sxs-lookup"><span data-stu-id="2f50f-285">Consider the datacenters too.</span></span> <span data-ttu-id="2f50f-286">Par exemple, si votre service utilise le centre de données États-Unis de l’Ouest et que SQL Server est hébergé sur une machine virtuelle Azure, votre machine virtuelle Azure doit également se situer dans les États-Unis de l’Ouest.</span><span class="sxs-lookup"><span data-stu-id="2f50f-286">For example, if your service uses the West US datacenter, and you have SQL Server hosted in an Azure VM, your Azure VM should be in the West US too.</span></span> <span data-ttu-id="2f50f-287">Cette proximité réduit la latence et évite des frais d’acheminement sur la machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="2f50f-287">This proximity minimizes latency and avoids egress charges on the Azure VM.</span></span>

<span data-ttu-id="2f50f-288">**Q** : Comment les résultats sont-ils renvoyés vers le cloud ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-288">**Q**: How are results sent back to the cloud?</span></span> <br/><span data-ttu-id="2f50f-289">
**R** : Les résultats sont envoyés via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2f50f-289">
**A**: Results are sent through the Azure Service Bus.</span></span>

<span data-ttu-id="2f50f-290">**Q** : existe-t-il des connexions entrantes vers la passerelle à partir du cloud ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-290">**Q**: Are there any inbound connections to the gateway from the cloud?</span></span> <br/><span data-ttu-id="2f50f-291">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="2f50f-291">
**A**: No.</span></span> <span data-ttu-id="2f50f-292">La passerelle utilise des connexions sortantes vers Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="2f50f-292">The gateway uses outbound connections to Azure Service Bus.</span></span>

<span data-ttu-id="2f50f-293">**Q** : Que se passe-t-il si je bloque les connexions sortantes ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-293">**Q**: What if I block outbound connections?</span></span> <span data-ttu-id="2f50f-294">Que dois-je ouvrir ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-294">What do I need to open?</span></span> <br/><span data-ttu-id="2f50f-295">
**R** : Vérifiez les ports et les hôtes que la passerelle utilise.</span><span class="sxs-lookup"><span data-stu-id="2f50f-295">
**A**: See the ports and hosts that the gateway uses.</span></span>

<span data-ttu-id="2f50f-296">**Q** : Comment s’appelle le service Windows réel ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-296">**Q**: What is the actual Windows service called?</span></span><br/><span data-ttu-id="2f50f-297">
**R** : Dans Services, la passerelle est appelée Service Enterprise Gateway Power BI.</span><span class="sxs-lookup"><span data-stu-id="2f50f-297">
**A**: In Services, the gateway is called Power BI Enterprise Gateway Service.</span></span>

<span data-ttu-id="2f50f-298">**Q** : Le service Windows de passerelle peut-il s’exécuter avec un compte Azure Active Directory ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-298">**Q**: Can the gateway Windows service run with an Azure Active Directory account?</span></span> <br/><span data-ttu-id="2f50f-299">
**R** : Non.</span><span class="sxs-lookup"><span data-stu-id="2f50f-299">
**A**: No.</span></span> <span data-ttu-id="2f50f-300">Le service Windows doit avoir un compte Windows valide.</span><span class="sxs-lookup"><span data-stu-id="2f50f-300">The Windows service must have a valid Windows account.</span></span> <span data-ttu-id="2f50f-301">Par défaut, le service sera exécuté avec le SID du service, NT SERVICE\PBIEgwService.</span><span class="sxs-lookup"><span data-stu-id="2f50f-301">By default, the service runs with the Service SID, NT SERVICE\PBIEgwService.</span></span>

### <a name="high-availability-and-disaster-recovery"></a><span data-ttu-id="2f50f-302">Haute disponibilité et récupération d’urgence</span><span class="sxs-lookup"><span data-stu-id="2f50f-302">High availability and disaster recovery</span></span>

<span data-ttu-id="2f50f-303">**Q** : Quelles sont les options de récupération d’urgence disponibles ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-303">**Q**: What options are available for disaster recovery?</span></span> <br/><span data-ttu-id="2f50f-304">
**R**: Vous pouvez utiliser la clé de récupération pour restaurer ou déplacer une passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-304">
**A**: You can use the recovery key to restore or move a gateway.</span></span> <span data-ttu-id="2f50f-305">Lorsque vous installez la passerelle, spécifiez la clé de récupération.</span><span class="sxs-lookup"><span data-stu-id="2f50f-305">When you install the gateway, specify the recovery key.</span></span>

<span data-ttu-id="2f50f-306">**Q** : Quel avantage la clé de récupération offre-t-elle ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-306">**Q**: What is the benefit of the recovery key?</span></span> <br/><span data-ttu-id="2f50f-307">
**R** : La clé de récupération permet de migrer ou de récupérer les paramètres de votre passerelle en cas de récupération d’urgence.</span><span class="sxs-lookup"><span data-stu-id="2f50f-307">
**A**: The recovery key provides a way to migrate or recover your gateway settings after a disaster.</span></span>

<span data-ttu-id="2f50f-308">**Q** : Existe-t-il des plans pour activer des scénarios de haute disponibilité avec la passerelle ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-308">**Q**: Are there any plans for enabling high availability scenarios with the gateway?</span></span> <br/><span data-ttu-id="2f50f-309">
**R** : ces scénarios figurent sur notre feuille de route, mais leur chronologie n’est pas encore établie.</span><span class="sxs-lookup"><span data-stu-id="2f50f-309">
**A**: These scenarios are on the roadmap, but we don't have a timeline yet.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2f50f-310">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="2f50f-310">Troubleshooting</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

<span data-ttu-id="2f50f-311">**Q** : Comment puis-je voir les requêtes qui sont envoyées à la source de données locale ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-311">**Q**: How can I see what queries are being sent to the on-premises data source?</span></span> <br/><span data-ttu-id="2f50f-312">
**R** : Vous pouvez activer le traçage de requête qui inclut les requêtes envoyées.</span><span class="sxs-lookup"><span data-stu-id="2f50f-312">
**A**: You can enable query tracing, which includes the queries that are sent.</span></span> <span data-ttu-id="2f50f-313">N’oubliez pas de rétablir la valeur d’origine du traçage des requêtes une fois les problèmes résolus.</span><span class="sxs-lookup"><span data-stu-id="2f50f-313">Remember to change query tracing back to the original value when done troubleshooting.</span></span> <span data-ttu-id="2f50f-314">Le fait de laisser activé le traçage des requêtes contribue à augmenter la taille des journaux.</span><span class="sxs-lookup"><span data-stu-id="2f50f-314">Leaving query tracing turned on creates larger logs.</span></span>

<span data-ttu-id="2f50f-315">Vous pouvez également utiliser les outils de suivi des requêtes proposés par votre source de données.</span><span class="sxs-lookup"><span data-stu-id="2f50f-315">You can also look at tools that your data source has for tracing queries.</span></span> <span data-ttu-id="2f50f-316">Par exemple, vous pouvez utiliser Extended Events ou SQL Profiler for SQL Server et Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="2f50f-316">For example, you can use Extended Events or SQL Profiler for SQL Server and Analysis Services.</span></span>

<span data-ttu-id="2f50f-317">**Q** : Où se situent les journaux de la passerelle ?</span><span class="sxs-lookup"><span data-stu-id="2f50f-317">**Q**: Where are the gateway logs?</span></span> <br/><span data-ttu-id="2f50f-318">
**R**: Voir la section Outils plus loin dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="2f50f-318">
**A**: See Tools later in this topic.</span></span>

### <a name="update-to-the-latest-version"></a><span data-ttu-id="2f50f-319">Mise à jour avec la version la plus récente</span><span class="sxs-lookup"><span data-stu-id="2f50f-319">Update to the latest version</span></span>

<span data-ttu-id="2f50f-320">Beaucoup de problèmes peuvent survenir si la version de la passerelle est obsolète.</span><span class="sxs-lookup"><span data-stu-id="2f50f-320">Many issues can surface when the gateway version becomes outdated.</span></span> <span data-ttu-id="2f50f-321">En règle générale, veillez toujours à utiliser la version la plus récente.</span><span class="sxs-lookup"><span data-stu-id="2f50f-321">As good general practice, make sure that you use the latest version.</span></span> <span data-ttu-id="2f50f-322">Si vous n’avez pas mis à jour la passerelle depuis un mois ou plus, vous pouvez installer la dernière version de la passerelle pour vérifier si le problème se reproduit.</span><span class="sxs-lookup"><span data-stu-id="2f50f-322">If you haven't updated the gateway for a month or longer, you might consider installing the latest version of the gateway, and see if you can reproduce the issue.</span></span>

### <a name="error-failed-to-add-user-to-group--2147463168-pbiegwservice-performance-log-users"></a><span data-ttu-id="2f50f-323">Erreur : Impossible d’ajouter l’utilisateur au groupe.</span><span class="sxs-lookup"><span data-stu-id="2f50f-323">Error: Failed to add user to group.</span></span> <span data-ttu-id="2f50f-324">(-2147463168 PBIEgwService Performance Log Users)</span><span class="sxs-lookup"><span data-stu-id="2f50f-324">(-2147463168 PBIEgwService Performance Log Users)</span></span>

<span data-ttu-id="2f50f-325">Cette erreur peut apparaître si vous essayez d’installer la passerelle sur un contrôleur de domaine qui n’est pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2f50f-325">You might get this error if you try to install the gateway on a domain controller, which isn't supported.</span></span> <span data-ttu-id="2f50f-326">Veillez à déployer la passerelle sur un ordinateur qui n’est pas un contrôleur de domaine.</span><span class="sxs-lookup"><span data-stu-id="2f50f-326">Make sure that you deploy the gateway on a machine that isn't a domain controller.</span></span>

## <a name="tools"></a><span data-ttu-id="2f50f-327">Outils</span><span class="sxs-lookup"><span data-stu-id="2f50f-327">Tools</span></span>

### <a name="collect-logs-from-the-gateway-configurer"></a><span data-ttu-id="2f50f-328">Collecter des journaux à partir de l’outil de configuration de passerelle</span><span class="sxs-lookup"><span data-stu-id="2f50f-328">Collect logs from the gateway configurer</span></span>

<span data-ttu-id="2f50f-329">Vous pouvez recueillir plusieurs journaux pour la passerelle.</span><span class="sxs-lookup"><span data-stu-id="2f50f-329">You can collect several logs for the gateway.</span></span> <span data-ttu-id="2f50f-330">Commencez toujours par consulter les journaux !</span><span class="sxs-lookup"><span data-stu-id="2f50f-330">Always start with the logs!</span></span>

#### <a name="installer-logs"></a><span data-ttu-id="2f50f-331">Journaux du programme d’installation</span><span class="sxs-lookup"><span data-stu-id="2f50f-331">Installer logs</span></span>

`%localappdata%\Temp\Power_BI_Gateway_–Enterprise.log`

#### <a name="configuration-logs"></a><span data-ttu-id="2f50f-332">Journaux de configuration</span><span class="sxs-lookup"><span data-stu-id="2f50f-332">Configuration logs</span></span>

`%localappdata%\Microsoft\Power BI Enterprise Gateway\GatewayConfigurator.log`

#### <a name="enterprise-gateway-service-logs"></a><span data-ttu-id="2f50f-333">Journaux du service de passerelle Enterprise</span><span class="sxs-lookup"><span data-stu-id="2f50f-333">Enterprise gateway service logs</span></span>

`C:\Users\PBIEgwService\AppData\Local\Microsoft\Power BI Enterprise Gateway\EnterpriseGateway.log`

#### <a name="event-logs"></a><span data-ttu-id="2f50f-334">Journaux d’événements</span><span class="sxs-lookup"><span data-stu-id="2f50f-334">Event logs</span></span>

<span data-ttu-id="2f50f-335">Les journaux de passerelle de gestion des données et PowerBIGateway figurent sous **Journaux des applications et services**.</span><span class="sxs-lookup"><span data-stu-id="2f50f-335">You can find the Data Management Gateway and PowerBIGateway logs under **Application and Services Logs**.</span></span>

### <a name="fiddler-trace"></a><span data-ttu-id="2f50f-336">Trace Fiddler</span><span class="sxs-lookup"><span data-stu-id="2f50f-336">Fiddler Trace</span></span>

<span data-ttu-id="2f50f-337">[Fiddler](http://www.telerik.com/fiddler) est un outil gratuit développé par Telerik, qui surveille le trafic HTTP.</span><span class="sxs-lookup"><span data-stu-id="2f50f-337">[Fiddler](http://www.telerik.com/fiddler) is a free tool from Telerik that monitors HTTP traffic.</span></span> <span data-ttu-id="2f50f-338">Il permet de visualiser le trafic entre le service Power BI et l’ordinateur client.</span><span class="sxs-lookup"><span data-stu-id="2f50f-338">You can see this traffic with the Power BI service from the client machine.</span></span> <span data-ttu-id="2f50f-339">Ce service peut également indiquer les éventuelles erreurs et autres informations connexes.</span><span class="sxs-lookup"><span data-stu-id="2f50f-339">This service might show errors and other related information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f50f-340">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="2f50f-340">Next steps</span></span>
    
* [<span data-ttu-id="2f50f-341">Connexion à des données locales à partir d’applications logiques</span><span class="sxs-lookup"><span data-stu-id="2f50f-341">Connect to on-premises data from logic apps</span></span>](../logic-apps/logic-apps-gateway-connection.md)
* [<span data-ttu-id="2f50f-342">Fonctionnalités d’intégration d'entreprise</span><span class="sxs-lookup"><span data-stu-id="2f50f-342">Enterprise integration features</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="2f50f-343">Connecteurs pour Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="2f50f-343">Connectors for Azure Logic Apps</span></span>](../connectors/apis-list.md)
