---
title: "aaaConnect tooan local système SAP dans Azure Logic Apps | Documents Microsoft"
description: "Se connecter de système SAP tooan local à partir de votre flux de travail application logique via la passerelle de données locale hello"
services: logic-apps
author: padmavc
manager: anneta
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/01/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: 594ec5fed337398bf931d396684630ee9f907d2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooan-on-premises-sap-system-from-logic-apps-with-hello-sap-connector"></a><span data-ttu-id="36321-103">Se connecter de système SAP tooan local à partir de la logique d’applications avec le connecteur SAP hello</span><span class="sxs-lookup"><span data-stu-id="36321-103">Connect tooan on-premises SAP system from logic apps with hello SAP connector</span></span> 

<span data-ttu-id="36321-104">passerelle de données locale Hello vous permet de toomanage données et accéder en toute sécurité les ressources locales.</span><span class="sxs-lookup"><span data-stu-id="36321-104">hello on-premises data gateway enables you toomanage data, and securely access resources that are on-premises.</span></span> <span data-ttu-id="36321-105">Cette rubrique montre comment vous pouvez connecter le système SAP local logique applications tooan.</span><span class="sxs-lookup"><span data-stu-id="36321-105">This topic shows how you can connect logic apps tooan on-premises SAP system.</span></span> <span data-ttu-id="36321-106">Dans cet exemple, votre application logique demande un IDOC via HTTP et envoie la réponse hello.</span><span class="sxs-lookup"><span data-stu-id="36321-106">In this example, your logic app requests an IDOC over HTTP and sends hello response back.</span></span>    

> [!NOTE]
> <span data-ttu-id="36321-107">Limitations actuelles :</span><span class="sxs-lookup"><span data-stu-id="36321-107">Current limitations:</span></span> 
> - <span data-ttu-id="36321-108">Votre application logique expire si toutes les étapes nécessaires pour la réponse de hello ne se terminent dans hello [limite de délai d’attente de demandes](./logic-apps-limits-and-config.md).</span><span class="sxs-lookup"><span data-stu-id="36321-108">Your logic app times out if all steps required for hello response don't finish within hello [request timeout limit](./logic-apps-limits-and-config.md).</span></span> <span data-ttu-id="36321-109">Dans ce scénario, les demandes peuvent être bloquées.</span><span class="sxs-lookup"><span data-stu-id="36321-109">In this scenario, requests might get blocked.</span></span> 
> - <span data-ttu-id="36321-110">Sélecteur de fichier Hello n’affiche pas tous les champs disponibles hello.</span><span class="sxs-lookup"><span data-stu-id="36321-110">hello file picker does not display all hello available fields.</span></span> <span data-ttu-id="36321-111">Dans ce scénario, vous pouvez ajouter manuellement des chemins d’accès.</span><span class="sxs-lookup"><span data-stu-id="36321-111">In this scenario, you can manually add paths.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36321-112">Composants requis</span><span class="sxs-lookup"><span data-stu-id="36321-112">Prerequisites</span></span>

- <span data-ttu-id="36321-113">Installer et configurer hello dernières [passerelle de données locale](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="36321-113">Install and configure hello latest [on-premises data gateway](https://www.microsoft.com/download/details.aspx?id=53127) version 1.15.6150.1 or newer.</span></span> <span data-ttu-id="36321-114">[Comment tooconnect toohello local passerelle de données dans une application logique](http://aka.ms/logicapps-gateway) listes hello étapes.</span><span class="sxs-lookup"><span data-stu-id="36321-114">[How tooconnect toohello on-premises data gateway in a logic app](http://aka.ms/logicapps-gateway) lists hello steps.</span></span> <span data-ttu-id="36321-115">passerelle de Hello doit être installé sur un ordinateur local avant de pouvoir continuer.</span><span class="sxs-lookup"><span data-stu-id="36321-115">hello gateway must be installed on an on-premises machine before you can proceed.</span></span>

- <span data-ttu-id="36321-116">Téléchargement et installation hello dernière SAP bibliothèque cliente sur hello même de l’ordinateur où vous avez installé la passerelle de données hello.</span><span class="sxs-lookup"><span data-stu-id="36321-116">Download and install hello latest SAP client library on hello same machine where you installed hello data gateway.</span></span> <span data-ttu-id="36321-117">Utiliser les hello SAP versions suivantes :</span><span class="sxs-lookup"><span data-stu-id="36321-117">Use any of hello following SAP versions:</span></span> 
    - <span data-ttu-id="36321-118">Serveur SAP</span><span class="sxs-lookup"><span data-stu-id="36321-118">SAP Server</span></span>
        - <span data-ttu-id="36321-119">N’importe quel serveur SAP que hello prise en charge le connecteur .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="36321-119">Any SAP Server that support hello .NET Connector (NCo) 3.0</span></span>
 
    - <span data-ttu-id="36321-120">Client SAP</span><span class="sxs-lookup"><span data-stu-id="36321-120">SAP Client</span></span>
        - <span data-ttu-id="36321-121">Connecteur SAP .NET (NCo) 3.0</span><span class="sxs-lookup"><span data-stu-id="36321-121">SAP .NET Connector (NCo) 3.0</span></span>

## <a name="add-triggers-and-actions-for-connecting-tooyour-sap-system"></a><span data-ttu-id="36321-122">Ajouter des déclencheurs et les actions pour la connexion de système de tooyour SAP</span><span class="sxs-lookup"><span data-stu-id="36321-122">Add triggers and actions for connecting tooyour SAP system</span></span>

<span data-ttu-id="36321-123">le connecteur SAP Hello possède des actions, mais pas les déclencheurs.</span><span class="sxs-lookup"><span data-stu-id="36321-123">hello SAP connector has actions, but not triggers.</span></span> <span data-ttu-id="36321-124">Par conséquent, nous avons toouse un autre déclencheur au début de hello du flux de travail hello.</span><span class="sxs-lookup"><span data-stu-id="36321-124">So, we have toouse another trigger at hello start of hello workflow.</span></span> 

1. <span data-ttu-id="36321-125">Ajouter le déclencheur de demande/réponse hello et sélectionnez **nouvelle étape**.</span><span class="sxs-lookup"><span data-stu-id="36321-125">Add hello Request/Response trigger, and then select **New step**.</span></span>

2. <span data-ttu-id="36321-126">Sélectionnez **ajouter une action**, puis sélectionnez le connecteur SAP hello en tapant `SAP` dans le champ de recherche hello :</span><span class="sxs-lookup"><span data-stu-id="36321-126">Select **Add an action**, and then select hello SAP connector by typing `SAP` in hello search field:</span></span>    

     ![Sélectionnez le serveur d’applications SAP ou le serveur de messagerie SAP.](media/logic-apps-using-sap-connector/sap-action.png)

3. <span data-ttu-id="36321-128">Sélectionnez [**Serveur d’applications SAP**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) ou [**Serveur de messagerie SAP**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), selon votre installation SAP.</span><span class="sxs-lookup"><span data-stu-id="36321-128">Select [**SAP Application Server**](https://wiki.scn.sap.com/wiki/display/ABAP/ABAP+Application+Server) or [**SAP Message Server**](http://help.sap.com/saphelp_nw70/helpdata/en/40/c235c15ab7468bb31599cc759179ef/frameset.htm), based on your SAP setup.</span></span> <span data-ttu-id="36321-129">Si vous n’avez pas une connexion existante, vous êtes invité à toocreate une.</span><span class="sxs-lookup"><span data-stu-id="36321-129">If you don't have an existing connection, you are prompted toocreate one.</span></span>

   1. <span data-ttu-id="36321-130">Sélectionnez **se connecter via la passerelle de données locale**et entrez les détails de hello pour votre système SAP :</span><span class="sxs-lookup"><span data-stu-id="36321-130">Select **Connect via on-premises data gateway**, and enter hello details for your SAP system:</span></span>   

       ![Ajouter tooSAP de chaîne de connexion](media/logic-apps-using-sap-connector/picture2.png)  

   2. <span data-ttu-id="36321-132">Sous **passerelle**, sélectionnez une passerelle existante, ou tooinstall une passerelle, sélectionnez **installer une passerelle**.</span><span class="sxs-lookup"><span data-stu-id="36321-132">Under **Gateway**, select an existing gateway, or tooinstall a new gateway, select **Install Gateway**.</span></span>

        ![Installer une nouvelle passerelle](media/logic-apps-using-sap-connector/install-gateway.png)
  
   3. <span data-ttu-id="36321-134">Après avoir entré tous les détails de hello, sélectionnez **créer**.</span><span class="sxs-lookup"><span data-stu-id="36321-134">After you enter all hello details, select **Create**.</span></span> 
   <span data-ttu-id="36321-135">Logique d’applications configure et teste la connexion hello, s’assurer que les connexions hello fonctionnement correctement.</span><span class="sxs-lookup"><span data-stu-id="36321-135">Logic Apps configures and tests hello connection, making sure that hello connection works properly.</span></span>

4. <span data-ttu-id="36321-136">Entrez un nom pour votre connexion SAP.</span><span class="sxs-lookup"><span data-stu-id="36321-136">Enter a name for your SAP connection.</span></span>

5. <span data-ttu-id="36321-137">différentes options de SAP Hello sont désormais disponibles.</span><span class="sxs-lookup"><span data-stu-id="36321-137">hello different SAP options are now available.</span></span> <span data-ttu-id="36321-138">toofind catégorie IDOC, sélectionnez à partir de la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="36321-138">toofind your IDOC category, select from hello list.</span></span> <span data-ttu-id="36321-139">Ou tapez manuellement dans le chemin d’accès hello et réponse hello sélectionnez HTTP dans hello **corps** champ :</span><span class="sxs-lookup"><span data-stu-id="36321-139">Or manually type in hello path, and select hello HTTP response in hello **body** field:</span></span>

     ![Action SAP](media/logic-apps-using-sap-connector/picture3.png)

6. <span data-ttu-id="36321-141">Ajouter une action hello pour la création d’un **réponse HTTP**.</span><span class="sxs-lookup"><span data-stu-id="36321-141">Add hello action for creating an **HTTP Response**.</span></span> <span data-ttu-id="36321-142">message de réponse Hello doit provenir de la sortie SAP hello.</span><span class="sxs-lookup"><span data-stu-id="36321-142">hello response message should be from hello SAP output.</span></span>

7. <span data-ttu-id="36321-143">Enregistrez votre application logique.</span><span class="sxs-lookup"><span data-stu-id="36321-143">Save your logic app.</span></span> <span data-ttu-id="36321-144">Testez-le en envoyant un IDOC via l’URL du déclencheur hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="36321-144">Test it by sending an IDOC through hello HTTP trigger URL.</span></span> <span data-ttu-id="36321-145">Après hello QU'IDOC est envoyé, attendez réponse hello à partir de l’application logique de hello :</span><span class="sxs-lookup"><span data-stu-id="36321-145">After hello IDOC is sent, wait for hello response from hello logic app:</span></span>   

     > [!TIP]
     > <span data-ttu-id="36321-146">Découvrez comment faire trop[surveiller vos applications logiques](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="36321-146">Check out how too[monitor your Logic Apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<span data-ttu-id="36321-147">Maintenant que le connecteur SAP hello est ajouté l’application logique de tooyour, commencer à Explorer les autres fonctionnalités :</span><span class="sxs-lookup"><span data-stu-id="36321-147">Now that hello SAP connector is added tooyour logic app, start exploring other functionalities:</span></span>

- <span data-ttu-id="36321-148">BAPI</span><span class="sxs-lookup"><span data-stu-id="36321-148">BAPI</span></span>
- <span data-ttu-id="36321-149">RFC</span><span class="sxs-lookup"><span data-stu-id="36321-149">RFC</span></span>

## <a name="get-help"></a><span data-ttu-id="36321-150">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="36321-150">Get help</span></span>

<span data-ttu-id="36321-151">tooask questions, répondre aux questions et savoir quels autres Azure Logic Apps font les utilisateurs, visitez hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span><span class="sxs-lookup"><span data-stu-id="36321-151">tooask questions, answer questions, and learn what other Azure Logic Apps users are doing, visit hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).</span></span>

<span data-ttu-id="36321-152">toohelp améliorer Azure Logic Apps et connecteurs, voter pour ou envoyer vos idées à hello [site de commentaires utilisateur Azure Logic Apps](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="36321-152">toohelp improve Azure Logic Apps and connectors, vote on or submit ideas at hello [Azure Logic Apps user feedback site](http://aka.ms/logicapps-wish).</span></span>

## <a name="next-steps"></a><span data-ttu-id="36321-153">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="36321-153">Next steps</span></span>

- <span data-ttu-id="36321-154">Découvrez comment toovalidate, transformation et autres fonctions de BizTalk de type Bonjour [Pack d’intégration Enterprise](../logic-apps/logic-apps-enterprise-integration-overview.md).</span><span class="sxs-lookup"><span data-stu-id="36321-154">Learn how toovalidate, transform, and other BizTalk-like functions in hello [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).</span></span> 
- <span data-ttu-id="36321-155">[Se connecter aux données local tooon](../logic-apps/logic-apps-gateway-connection.md) à partir d’applications de logique</span><span class="sxs-lookup"><span data-stu-id="36321-155">[Connect tooon-premises data](../logic-apps/logic-apps-gateway-connection.md) from logic apps</span></span>
