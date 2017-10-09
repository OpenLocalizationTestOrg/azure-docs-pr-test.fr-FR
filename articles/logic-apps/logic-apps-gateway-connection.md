---
title: "sources de données aaaAccess localement pour Azure Logic Apps | Documents Microsoft"
description: "Configurer la passerelle de données locale hello pour pouvoir accéder à des sources de données sur site à partir d’applications de logique"
keywords: "accéder aux données, localement, transfert de données, chiffrement, sources de données"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a><span data-ttu-id="f6260-104">Accès aux sources de données sur site à partir de la logique d’applications avec la passerelle de données locale hello</span><span class="sxs-lookup"><span data-stu-id="f6260-104">Access data sources on premises from logic apps with hello on-premises data gateway</span></span>

<span data-ttu-id="f6260-105">tooaccess des sources de données sur site à partir de vos applications logiques, configurez une passerelle de données local qui logique applications peuvent utiliser avec les connecteurs pris en charge.</span><span class="sxs-lookup"><span data-stu-id="f6260-105">tooaccess data sources on premises from your logic apps, set up an on-premises data gateway that logic apps can use with supported connectors.</span></span> <span data-ttu-id="f6260-106">Hello passerelle fait Office de pont qui fournit le transfert de données rapide et le chiffrement entre les sources de données sur site et vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="f6260-106">hello gateway acts as a bridge that provides quick data transfer and encryption between data sources on premises and your logic apps.</span></span> <span data-ttu-id="f6260-107">passerelle de Hello transmet des données à partir de sources locales sur des canaux chiffrés via hello Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="f6260-107">hello gateway relays data from on-premises sources on encrypted channels through hello Azure Service Bus.</span></span> <span data-ttu-id="f6260-108">Tout le trafic provient sécurisé trafic sortant à partir de l’agent de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="f6260-108">All traffic originates as secure outbound traffic from hello gateway agent.</span></span> <span data-ttu-id="f6260-109">En savoir plus sur [le fonctionnement de la passerelle de données hello](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="f6260-109">Learn more about [how hello data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span> 

<span data-ttu-id="f6260-110">passerelle de Hello prend en charge les sources de données de connexions toothese sur site :</span><span class="sxs-lookup"><span data-stu-id="f6260-110">hello gateway supports connections toothese data sources on premises:</span></span>

*   <span data-ttu-id="f6260-111">BizTalk Server 2016</span><span class="sxs-lookup"><span data-stu-id="f6260-111">BizTalk Server 2016</span></span>
*   <span data-ttu-id="f6260-112">DB2</span><span class="sxs-lookup"><span data-stu-id="f6260-112">DB2</span></span>  
*   <span data-ttu-id="f6260-113">Système de fichiers</span><span class="sxs-lookup"><span data-stu-id="f6260-113">File System</span></span>
*   <span data-ttu-id="f6260-114">Informix</span><span class="sxs-lookup"><span data-stu-id="f6260-114">Informix</span></span>
*   <span data-ttu-id="f6260-115">MQ</span><span class="sxs-lookup"><span data-stu-id="f6260-115">MQ</span></span>
*   <span data-ttu-id="f6260-116">MySQL</span><span class="sxs-lookup"><span data-stu-id="f6260-116">MySQL</span></span>
*   <span data-ttu-id="f6260-117">Oracle Database</span><span class="sxs-lookup"><span data-stu-id="f6260-117">Oracle Database</span></span>
*   <span data-ttu-id="f6260-118">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f6260-118">PostgreSQL</span></span>
*   <span data-ttu-id="f6260-119">Serveur d’applications SAP</span><span class="sxs-lookup"><span data-stu-id="f6260-119">SAP Application Server</span></span> 
*   <span data-ttu-id="f6260-120">Serveur de messagerie SAP</span><span class="sxs-lookup"><span data-stu-id="f6260-120">SAP Message Server</span></span>
*   <span data-ttu-id="f6260-121">SharePoint</span><span class="sxs-lookup"><span data-stu-id="f6260-121">SharePoint</span></span>
*   <span data-ttu-id="f6260-122">SQL Server</span><span class="sxs-lookup"><span data-stu-id="f6260-122">SQL Server</span></span>
*   <span data-ttu-id="f6260-123">Teradata</span><span class="sxs-lookup"><span data-stu-id="f6260-123">Teradata</span></span>

<span data-ttu-id="f6260-124">Ces étapes indiquent comment tooset des hello local toowork de passerelle de données avec vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="f6260-124">These steps show how tooset up hello on-premises data gateway toowork with your logic apps.</span></span> <span data-ttu-id="f6260-125">Pour plus d’informations sur les connecteurs pris en charge, voir [Connecteurs pour Azure Logic Apps](../connectors/apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="f6260-125">For more information about supported connectors, see [Connectors for Azure Logic Apps](../connectors/apis-list.md).</span></span> 

<span data-ttu-id="f6260-126">Pour plus d’informations sur la façon dont toouse hello passerelle avec d’autres services, consultez les articles suivants :</span><span class="sxs-lookup"><span data-stu-id="f6260-126">For information about how toouse hello gateway with other services, see these articles:</span></span>

*   [<span data-ttu-id="f6260-127">Passerelle de données locale Microsoft Power BI</span><span class="sxs-lookup"><span data-stu-id="f6260-127">Microsoft Power BI on-premises data gateway</span></span>](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [<span data-ttu-id="f6260-128">Passerelle de données locale Azure Analysis Services</span><span class="sxs-lookup"><span data-stu-id="f6260-128">Azure Analysis Services on-premises data gateway</span></span>](../analysis-services/analysis-services-gateway.md)
*   [<span data-ttu-id="f6260-129">Passerelle de données locale Microsoft Flow</span><span class="sxs-lookup"><span data-stu-id="f6260-129">Microsoft Flow on-premises data gateway</span></span>](https://flow.microsoft.com/documentation/gateway-manage/)
*   [<span data-ttu-id="f6260-130">Passerelle de données locale Microsoft PowerApps</span><span class="sxs-lookup"><span data-stu-id="f6260-130">Microsoft PowerApps on-premises data gateway</span></span>](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a><span data-ttu-id="f6260-131">Configuration requise</span><span class="sxs-lookup"><span data-stu-id="f6260-131">Requirements</span></span>

* <span data-ttu-id="f6260-132">Vous devez d’abord [installé la passerelle de données hello sur un ordinateur local](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="f6260-132">You must have already [installed hello data gateway on a local computer](logic-apps-gateway-install.md).</span></span>

* <span data-ttu-id="f6260-133">Lorsque vous vous connectez dans toohello portail Azure, vous avez toouse hello même travail ou d’établissement scolaire compte qui a été utilisé trop[installer la passerelle de données locale hello](logic-apps-gateway-install.md#requirements).</span><span class="sxs-lookup"><span data-stu-id="f6260-133">When you sign in toohello Azure portal, you have toouse hello same work or school account that was used too[install hello on-premises data gateway](logic-apps-gateway-install.md#requirements).</span></span> <span data-ttu-id="f6260-134">Votre compte de connexion doit également avoir un toouse abonnement Azure lorsque vous créez une ressource de la passerelle Bonjour portail Azure pour votre installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="f6260-134">Your sign-in account must also have an Azure subscription toouse when you create a gateway resource in hello Azure portal for your gateway installation.</span></span>

* <span data-ttu-id="f6260-135">L’installation de votre passerelle ne peut pas être revendiquée par une autre ressource de passerelle Azure.</span><span class="sxs-lookup"><span data-stu-id="f6260-135">Your gateway installation can't already be claimed by an Azure gateway resource.</span></span> <span data-ttu-id="f6260-136">Vous pouvez associer votre passerelle installation tooonly une passerelle Azure ressource.</span><span class="sxs-lookup"><span data-stu-id="f6260-136">You can associate your gateway installation tooonly one Azure gateway resource.</span></span> <span data-ttu-id="f6260-137">Revendication se produit lorsque vous créez une ressource de la passerelle hello afin que l’installation de hello n’est pas disponible pour d’autres ressources.</span><span class="sxs-lookup"><span data-stu-id="f6260-137">Claim happens when you create hello gateway resource so that hello installation is unavailable for other resources.</span></span>

## <a name="set-up-hello-data-gateway-connection"></a><span data-ttu-id="f6260-138">Configurer la connexion de passerelle de données hello</span><span class="sxs-lookup"><span data-stu-id="f6260-138">Set up hello data gateway connection</span></span>

### <a name="1-install-hello-on-premises-data-gateway"></a><span data-ttu-id="f6260-139">1. Installer la passerelle de données locale hello</span><span class="sxs-lookup"><span data-stu-id="f6260-139">1. Install hello on-premises data gateway</span></span>

<span data-ttu-id="f6260-140">Si vous n’avez pas encore, suivez hello [passerelle de données locale étapes tooinstall hello](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="f6260-140">If you haven't already, follow hello [steps tooinstall hello on-premises data gateway](logic-apps-gateway-install.md).</span></span> <span data-ttu-id="f6260-141">Avant de continuer avec hello autres étapes, assurez-vous que vous avez installé la passerelle de données hello sur un ordinateur local.</span><span class="sxs-lookup"><span data-stu-id="f6260-141">Before you continue with hello other steps, make sure that you installed hello data gateway on a local computer.</span></span>

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a><span data-ttu-id="f6260-142">2. Créer une ressource Azure pour la passerelle de données locale hello</span><span class="sxs-lookup"><span data-stu-id="f6260-142">2. Create an Azure resource for hello on-premises data gateway</span></span>

<span data-ttu-id="f6260-143">Après avoir installé la passerelle de hello sur un ordinateur local, vous devez créer votre passerelle de données en tant que ressource dans Azure.</span><span class="sxs-lookup"><span data-stu-id="f6260-143">After you install hello gateway on a local computer, you must create your data gateway as a resource in Azure.</span></span> <span data-ttu-id="f6260-144">Cette étape associe également votre ressource de passerelle à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f6260-144">This step also associates your gateway resource with your Azure subscription.</span></span>

1. <span data-ttu-id="f6260-145">Connectez-vous à toohello [portail Azure](https://portal.azure.com "portail Azure").</span><span class="sxs-lookup"><span data-stu-id="f6260-145">Sign in toohello [Azure portal](https://portal.azure.com "Azure portal").</span></span> <span data-ttu-id="f6260-146">Assurez-vous que toouse hello même travail Azure ou l’adresse de messagerie de l’école utilisée passerelle de hello tooinstall.</span><span class="sxs-lookup"><span data-stu-id="f6260-146">Make sure toouse hello same Azure work or school email address used tooinstall hello gateway.</span></span>

2. <span data-ttu-id="f6260-147">Dans le menu de gauche hello dans Azure, choisissez **nouveau** > **intégration** > **passerelle de données locale** comme indiqué ici :</span><span class="sxs-lookup"><span data-stu-id="f6260-147">On hello left menu in Azure, choose **New** > **Enterprise Integration** > **On-premises data gateway** as shown here:</span></span>

   ![Cherchez « Passerelle de données locale »](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. <span data-ttu-id="f6260-149">Sur hello **créer une passerelle connexion** panneau, fournissez ces toocreate détails votre ressource de passerelle de données :</span><span class="sxs-lookup"><span data-stu-id="f6260-149">On hello **Create connection gateway** blade, provide these details toocreate your data gateway resource:</span></span>

    * <span data-ttu-id="f6260-150">**Nom** : entrez un nom pour votre ressource de passerelle.</span><span class="sxs-lookup"><span data-stu-id="f6260-150">**Name**: Enter a name for your gateway resource.</span></span> 

    * <span data-ttu-id="f6260-151">**Abonnement**: sélectionnez hello tooassociate abonnement Azure avec votre ressource de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="f6260-151">**Subscription**: Select hello Azure subscription tooassociate with your gateway resource.</span></span> 
    <span data-ttu-id="f6260-152">Cet abonnement doit être hello même abonnement que votre application logique.</span><span class="sxs-lookup"><span data-stu-id="f6260-152">This subscription should be hello same subscription as your logic app.</span></span>
   
      <span data-ttu-id="f6260-153">abonnement de Hello par défaut est basée sur hello compte Azure que vous avez utilisé toosign dans.</span><span class="sxs-lookup"><span data-stu-id="f6260-153">hello default subscription is based on hello Azure account that you used toosign in.</span></span>

    * <span data-ttu-id="f6260-154">**Groupe de ressources** : créez un groupe de ressources ou sélectionnez un groupe de ressources existant pour le déploiement de votre ressource de passerelle.</span><span class="sxs-lookup"><span data-stu-id="f6260-154">**Resource group**: Create a resource group or select an existing resource group for deploying your gateway resource.</span></span> 
    <span data-ttu-id="f6260-155">Les groupes de ressources vous aident à gérer des ressources Azure associées en tant que collection.</span><span class="sxs-lookup"><span data-stu-id="f6260-155">Resource groups help you manage related Azure assets as a collection.</span></span>

    * <span data-ttu-id="f6260-156">**Emplacement**: Azure limite ce toohello emplacement même région a été sélectionnée pour le service de cloud de passerelle hello pendant [installation de la passerelle](logic-apps-gateway-install.md).</span><span class="sxs-lookup"><span data-stu-id="f6260-156">**Location**: Azure restricts this location toohello same region that was selected for hello gateway cloud service during [gateway installation](logic-apps-gateway-install.md).</span></span> 

      > [!NOTE]
      > <span data-ttu-id="f6260-157">Assurez-vous que l’emplacement de ressource hello passerelle correspond à l’emplacement de service cloud hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="f6260-157">Make sure that hello gateway resource location matches hello gateway cloud service location.</span></span> <span data-ttu-id="f6260-158">Dans le cas contraire, votre installation de passerelle peuvent ne pas apparaît dans la liste des passerelles hello installé pour vous tooselect à l’étape suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="f6260-158">Otherwise, your gateway installation might not appear in hello installed gateways list for you tooselect in hello next step.</span></span>
      > 
      > <span data-ttu-id="f6260-159">Vous pouvez utiliser des régions différentes pour votre ressource de passerelle et votre application logique.</span><span class="sxs-lookup"><span data-stu-id="f6260-159">You can use different regions for your gateway resource and for your logic app.</span></span>

    * <span data-ttu-id="f6260-160">**Nom de l’installation**: Si votre installation de la passerelle n’est pas déjà sélectionnée, sélectionnez passerelle hello que vous avez installé précédemment.</span><span class="sxs-lookup"><span data-stu-id="f6260-160">**Installation Name**: If your gateway installation isn't already selected, select hello gateway that you previously installed.</span></span> 

    <span data-ttu-id="f6260-161">tooadd hello passerelle ressource tooyour tableau de bord Azure, choisissez **toodashboard du code confidentiel**.</span><span class="sxs-lookup"><span data-stu-id="f6260-161">tooadd hello gateway resource tooyour Azure dashboard, choose **Pin toodashboard**.</span></span> 
    <span data-ttu-id="f6260-162">Lorsque vous êtes prêt, choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f6260-162">When you're done, choose **Create**.</span></span>

    <span data-ttu-id="f6260-163">Par exemple :</span><span class="sxs-lookup"><span data-stu-id="f6260-163">For example:</span></span>

    ![Fournir des détails toocreate votre passerelle de données locale](./media/logic-apps-gateway-connection/createblade.png)

    <span data-ttu-id="f6260-165">toofind ou afficher votre passerelle de données à tout moment, depuis hello Azure gauche menu principal, accédez trop **plus Services** > **intégration** > **des données locales Passerelles**.</span><span class="sxs-lookup"><span data-stu-id="f6260-165">toofind or view your data gateway at any time,  from hello main Azure left menu, go too  **More Services** > **Enterprise Integration** > **On-premises Data Gateways**.</span></span>

    ![Accédez trop « Plus services », « Intégration d’entreprise », « Passerelles de données locales »](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a><span data-ttu-id="f6260-167">3. Connecter votre passerelle de données logique application toohello local</span><span class="sxs-lookup"><span data-stu-id="f6260-167">3. Connect your logic app toohello on-premises data gateway</span></span>

<span data-ttu-id="f6260-168">Maintenant que vous avez créé votre ressource de passerelle de données et votre abonnement Azure associé à cette ressource, créez une connexion entre votre passerelle de données logique app et hello.</span><span class="sxs-lookup"><span data-stu-id="f6260-168">Now that you've created your data gateway resource and associated your Azure subscription with that resource, create a connection between your logic app and hello data gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="f6260-169">L’emplacement de votre connexion de passerelle doit exister dans hello même région que votre application logique, mais vous pouvez utiliser une passerelle de données qui existe dans une autre région.</span><span class="sxs-lookup"><span data-stu-id="f6260-169">Your gateway connection location must exist in hello same region as your logic app, but you can use a data gateway that exists in a different region.</span></span>

1. <span data-ttu-id="f6260-170">Bonjour portail Azure, créez ou ouvrez votre application de logique dans le Concepteur de la logique d’application.</span><span class="sxs-lookup"><span data-stu-id="f6260-170">In hello Azure portal, create or open your logic app in Logic App Designer.</span></span>

2. <span data-ttu-id="f6260-171">Ajoutez un connecteur prenant en charge des connexions locales, tel que SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f6260-171">Add a connector that supports on-premises connections, like SQL Server.</span></span>

3. <span data-ttu-id="f6260-172">Ordre de hello indiqué, sélectionnez **se connecter via la passerelle de données locale**, fournissez un nom de connexion unique hello les informations requises et sélectionnez les ressources de passerelle de données hello que vous souhaitez toouse.</span><span class="sxs-lookup"><span data-stu-id="f6260-172">Following hello order shown, select **Connect via on-premises data gateway**, provide a unique connection name and hello required information, and select hello data gateway resource that you want toouse.</span></span> <span data-ttu-id="f6260-173">Lorsque vous êtes prêt, choisissez **Créer**.</span><span class="sxs-lookup"><span data-stu-id="f6260-173">When you're done, choose **Create**.</span></span>

   > [!TIP]
   > <span data-ttu-id="f6260-174">Un nom de connexion unique vous aidera à identifier facilement cette connexion ultérieurement, en particulier si vous créez plusieurs connexions.</span><span class="sxs-lookup"><span data-stu-id="f6260-174">A unique connection name helps you easily identify that connection later, especially when you create multiple connections.</span></span> <span data-ttu-id="f6260-175">Le cas échéant, également inclure hello de domaine complet pour votre nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="f6260-175">If applicable, also include hello qualified domain for your username.</span></span> 

   ![Créer une connexion entre une application logique et une passerelle de données](./media/logic-apps-gateway-connection/blankconnection.png)

<span data-ttu-id="f6260-177">Félicitations, votre connexion de passerelle est maintenant prête pour votre toouse d’application logique.</span><span class="sxs-lookup"><span data-stu-id="f6260-177">Congratulations, your gateway connection is now ready for your logic app toouse.</span></span>

## <a name="edit-your-gateway-connection-settings"></a><span data-ttu-id="f6260-178">Modifier vos paramètres de connexion de passerelle</span><span class="sxs-lookup"><span data-stu-id="f6260-178">Edit your gateway connection settings</span></span>

<span data-ttu-id="f6260-179">Après avoir créé une connexion de passerelle pour votre application logique, vous pouvez choisir les paramètres de hello toolater mise à jour pour cette connexion spécifique.</span><span class="sxs-lookup"><span data-stu-id="f6260-179">After you create a gateway connection for your logic app, you might want toolater update hello settings for that specific connection.</span></span>

1. <span data-ttu-id="f6260-180">connexion à la passerelle toofind hello :</span><span class="sxs-lookup"><span data-stu-id="f6260-180">toofind hello gateway connection:</span></span>

   * <span data-ttu-id="f6260-181">Dans le panneau de l’application hello logique, sous **outils de développement**, sélectionnez **API connexions**.</span><span class="sxs-lookup"><span data-stu-id="f6260-181">On hello logic app blade, under **Development Tools**, select **API Connections**.</span></span> 
   
     <span data-ttu-id="f6260-182">Hello **API connexions** volet affiche toutes les connexions d’API associées à votre application logique, y compris les connexions de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="f6260-182">hello **API Connections** pane shows all API connections associated with your logic app, including gateway connections.</span></span>

     ![Accédez à tooyour logique application, sélectionnez « Connexions API »](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * <span data-ttu-id="f6260-184">Ou, à partir de hello Azure gauche menu principal, accédez trop **plus Services** > **Web et les Services mobiles** > **API connexions** pour toutes les connexions d’API, y compris les connexions de la passerelle, qui sont associés à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f6260-184">Or, from hello main Azure left menu, go too **More Services** > **Web & Mobile Services** > **API Connections** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span> 

   * <span data-ttu-id="f6260-185">Ou, sur hello Azure gauche menu principal, accédez trop**toutes les ressources** pour toutes les connexions d’API, y compris les connexions de la passerelle, qui sont associées à votre abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="f6260-185">Or, on hello main Azure left menu, go too**All resources** for all API connections, including gateway connections, that are associated with your Azure subscription.</span></span>

2. <span data-ttu-id="f6260-186">Sélectionnez la connexion à la passerelle hello que vous tooview ou modifier, puis cliquez **connexion modifier l’API**.</span><span class="sxs-lookup"><span data-stu-id="f6260-186">Select hello gateway connection that you want tooview or edit, and choose **Edit API connection**.</span></span>

   > [!TIP]
   > <span data-ttu-id="f6260-187">Si vos mises à jour n’entrent en vigueur, essayez de [arrêter et redémarrer le service Windows de passerelle hello](./logic-apps-gateway-install.md#restart-gateway).</span><span class="sxs-lookup"><span data-stu-id="f6260-187">If your updates don't take effect, try [stopping and restarting hello gateway Windows service](./logic-apps-gateway-install.md#restart-gateway).</span></span>

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a><span data-ttu-id="f6260-188">Basculer ou supprimer votre ressource de passerelle de données locale</span><span class="sxs-lookup"><span data-stu-id="f6260-188">Switch or delete your on-premises data gateway resource</span></span>

<span data-ttu-id="f6260-189">toocreate une ressource passerelle différents, associer votre passerelle avec une autre ressource, ou supprimez la ressource de la passerelle hello, vous pouvez supprimer des ressources de passerelle hello sans affecter l’installation de la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="f6260-189">toocreate a different gateway resource, associate your gateway with a different resource, or remove hello gateway resource, you can delete hello gateway resource without affecting hello gateway installation.</span></span> 

1. <span data-ttu-id="f6260-190">À partir de hello Azure gauche menu principal, accédez trop**toutes les ressources**.</span><span class="sxs-lookup"><span data-stu-id="f6260-190">From hello main Azure left menu, go too**All resources**.</span></span> 
2. <span data-ttu-id="f6260-191">Cherchez et sélectionnez votre ressource de passerelle de données.</span><span class="sxs-lookup"><span data-stu-id="f6260-191">Find and select your data gateway resource.</span></span>
3. <span data-ttu-id="f6260-192">Choisissez **passerelle de données locale**, dans la barre d’outils de la ressource hello, choisissez **supprimer**.</span><span class="sxs-lookup"><span data-stu-id="f6260-192">Choose **On-premises Data Gateway**, and on hello resource toolbar, choose **Delete**.</span></span>

<a name="faq"></a>
## <a name="frequently-asked-questions"></a><span data-ttu-id="f6260-193">Forum Aux Questions</span><span class="sxs-lookup"><span data-stu-id="f6260-193">Frequently asked questions</span></span>

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a><span data-ttu-id="f6260-194">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f6260-194">Next steps</span></span>

* [<span data-ttu-id="f6260-195">Sécuriser vos applications logiques</span><span class="sxs-lookup"><span data-stu-id="f6260-195">Secure your logic apps</span></span>](./logic-apps-securing-a-logic-app.md)
* [<span data-ttu-id="f6260-196">Exemples et scénarios courants pour les applications logiques</span><span class="sxs-lookup"><span data-stu-id="f6260-196">Common examples and scenarios for logic apps</span></span>](./logic-apps-examples-and-scenarios.md)
