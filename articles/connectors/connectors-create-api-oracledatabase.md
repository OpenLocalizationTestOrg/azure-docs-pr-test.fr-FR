---
title: "connecteur de base de données Oracle aaaAdd hello dans vos applications de la logique de Azure | Documents Microsoft"
description: "Utiliser le connecteur de base de données Oracle hello dans une application de logique"
services: 
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: mandia; ladocs
ms.openlocfilehash: 8a802a6c4782e210ff71848614152cb46ba5d651
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-oracle-database-connector"></a><span data-ttu-id="b6f66-103">Prise en main connecteur de base de données Oracle hello</span><span class="sxs-lookup"><span data-stu-id="b6f66-103">Get started with hello Oracle Database connector</span></span>

<span data-ttu-id="b6f66-104">À l’aide du connecteur de base de données Oracle hello, créer des workflows d’organisation qui utilisent des données dans votre base de données existante.</span><span class="sxs-lookup"><span data-stu-id="b6f66-104">Using hello Oracle Database connector, you create organizational workflows that use data in your existing database.</span></span> <span data-ttu-id="b6f66-105">Ce connecteur peut se connecter tooan de base de données Oracle locale ou une machine virtuelle Azure avec la base de données Oracle installée.</span><span class="sxs-lookup"><span data-stu-id="b6f66-105">This connector can connect tooan on-premises Oracle Database, or an Azure virtual machine with Oracle Database installed.</span></span> <span data-ttu-id="b6f66-106">Avec ce connecteur, vous pouvez :</span><span class="sxs-lookup"><span data-stu-id="b6f66-106">With this connector, you can:</span></span>

* <span data-ttu-id="b6f66-107">Créer votre flux de travail en ajoutant une nouvelle base de données client tooa clients ou une commande dans une base de données des commandes de mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b6f66-107">Build your workflow by adding a new customer tooa customers database, or updating an order in an orders database.</span></span>
* <span data-ttu-id="b6f66-108">Utilisez les actions tooget une ligne de données, insérer une nouvelle ligne, ou les supprimer.</span><span class="sxs-lookup"><span data-stu-id="b6f66-108">Use actions tooget a row of data, insert a new row, and even delete.</span></span> <span data-ttu-id="b6f66-109">Par exemple, quand un enregistrement est créé dans Dynamics CRM Online (déclencheur), insérez une ligne dans une base de données Oracle (action).</span><span class="sxs-lookup"><span data-stu-id="b6f66-109">For example, when a record is created in Dynamics CRM Online (a trigger), then insert a row in an Oracle Database (an action).</span></span> 

<span data-ttu-id="b6f66-110">Cette rubrique vous montre comment toouse hello dans une application de la logique d’un connecteur de base de données Oracle.</span><span class="sxs-lookup"><span data-stu-id="b6f66-110">This topic shows you how toouse hello Oracle Database connector in a logic app.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6f66-111">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b6f66-111">Prerequisites</span></span>

* <span data-ttu-id="b6f66-112">Versions d’Oracle prises en charge :</span><span class="sxs-lookup"><span data-stu-id="b6f66-112">Supported Oracle versions:</span></span> 
    * <span data-ttu-id="b6f66-113">Oracle 9 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="b6f66-113">Oracle 9 and later</span></span>
    * <span data-ttu-id="b6f66-114">Logiciel client Oracle 8.1.7 et versions ultérieures</span><span class="sxs-lookup"><span data-stu-id="b6f66-114">Oracle client software 8.1.7 and later</span></span>

* <span data-ttu-id="b6f66-115">Installez la passerelle de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-115">Install hello on-premises data gateway.</span></span> <span data-ttu-id="b6f66-116">[Se connecter tooon locale, les données à partir d’applications de logique](../logic-apps/logic-apps-gateway-connection.md) listes hello étapes.</span><span class="sxs-lookup"><span data-stu-id="b6f66-116">[Connect tooon-premises data from logic apps](../logic-apps/logic-apps-gateway-connection.md) lists hello steps.</span></span> <span data-ttu-id="b6f66-117">passerelle de Hello est requis tooconnect tooan base de données Oracle locale ou une machine virtuelle de Azure avec la base de données Oracle installée.</span><span class="sxs-lookup"><span data-stu-id="b6f66-117">hello gateway is required tooconnect tooan on-premises Oracle Database, or an Azure VM with Oracle DB installed.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="b6f66-118">passerelle de données locale Hello fait Office de pont et fournit un transfert sécurisé des données entre des données locales (les données qui ne sont pas dans le cloud de hello) et vos applications logiques.</span><span class="sxs-lookup"><span data-stu-id="b6f66-118">hello on-premises data gateway acts as a bridge, and provides a secure data transfer between on-premises data (data that is not in hello cloud) and your logic apps.</span></span> <span data-ttu-id="b6f66-119">Hello même passerelle peut être utilisé avec plusieurs services et plusieurs sources de données.</span><span class="sxs-lookup"><span data-stu-id="b6f66-119">hello same gateway can be used with multiple services, and multiple data sources.</span></span> <span data-ttu-id="b6f66-120">Par conséquent, vous devrez peut-être uniquement passerelle de hello tooinstall qu’une seule fois.</span><span class="sxs-lookup"><span data-stu-id="b6f66-120">So, you may only need tooinstall hello gateway once.</span></span>

* <span data-ttu-id="b6f66-121">Installez hello Client Oracle sur l’ordinateur hello où vous avez installé la passerelle de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-121">Install hello Oracle Client on hello machine where you installed hello on-premises data gateway.</span></span> <span data-ttu-id="b6f66-122">Veillez à tooinstall hello 64 bits du fournisseur de données Oracle pour .NET à partir d’Oracle :</span><span class="sxs-lookup"><span data-stu-id="b6f66-122">Be sure tooinstall hello 64-bit Oracle Data Provider for .NET from Oracle:</span></span>  

  [<span data-ttu-id="b6f66-123">ODAC 12C version 4 (12.1.0.2.4) 64 bits pour Windows x64</span><span class="sxs-lookup"><span data-stu-id="b6f66-123">64-bit ODAC 12c Release 4 (12.1.0.2.4) for Windows x64</span></span>](http://www.oracle.com/technetwork/database/windows/downloads/index-090165.html)

    > [!TIP]
    > <span data-ttu-id="b6f66-124">Si le client d’Oracle hello n’est pas installé, une erreur se produit lorsque vous essayez de toocreate ou utilisez hello connexion.</span><span class="sxs-lookup"><span data-stu-id="b6f66-124">If hello Oracle client is not installed, an error occurs when you try toocreate or use hello connection.</span></span> <span data-ttu-id="b6f66-125">Consultez les erreurs courantes hello dans cette rubrique.</span><span class="sxs-lookup"><span data-stu-id="b6f66-125">See hello common errors in this topic.</span></span>


## <a name="add-hello-connector"></a><span data-ttu-id="b6f66-126">Ajouter hello connecteur</span><span class="sxs-lookup"><span data-stu-id="b6f66-126">Add hello connector</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b6f66-127">Ce connecteur ne possède aucun déclencheur.</span><span class="sxs-lookup"><span data-stu-id="b6f66-127">This connector does not have any triggers.</span></span> <span data-ttu-id="b6f66-128">Il possède uniquement des actions.</span><span class="sxs-lookup"><span data-stu-id="b6f66-128">It has only actions.</span></span> <span data-ttu-id="b6f66-129">Par conséquent, lorsque vous créez votre application logique, ajoutez un autre déclencheur toostart votre application logique, tel que **planification - périodicité**, ou **demande / réponse - réponse**.</span><span class="sxs-lookup"><span data-stu-id="b6f66-129">So when you create your logic app, add another trigger toostart your logic app, such as **Schedule - Recurrence**, or **Request / Response - Response**.</span></span> 

1. <span data-ttu-id="b6f66-130">Bonjour [portail Azure](https://portal.azure.com), créer une application vide logique.</span><span class="sxs-lookup"><span data-stu-id="b6f66-130">In hello [Azure portal](https://portal.azure.com), create a blank logic app.</span></span>

2. <span data-ttu-id="b6f66-131">Au début de hello de votre application logique, sélectionnez hello **demande / réponse - demande** déclencheur :</span><span class="sxs-lookup"><span data-stu-id="b6f66-131">At hello start of your logic app, select hello **Request / Response - Request** trigger:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/request-trigger.png)

3. <span data-ttu-id="b6f66-132">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b6f66-132">Select **Save**.</span></span> <span data-ttu-id="b6f66-133">Au moment de l’enregistrement, une URL de requête est générée automatiquement.</span><span class="sxs-lookup"><span data-stu-id="b6f66-133">When you save, a request URL is automatically generated.</span></span> 

4. <span data-ttu-id="b6f66-134">Sélectionnez **Nouvelle étape**, puis sélectionnez **Ajouter une action**.</span><span class="sxs-lookup"><span data-stu-id="b6f66-134">Select **New step**, and select **Add an action**.</span></span> <span data-ttu-id="b6f66-135">Tapez dans `oracle` toosee hello actions disponibles :</span><span class="sxs-lookup"><span data-stu-id="b6f66-135">Type in `oracle` toosee hello available actions:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/oracledb-actions.png)

    > [!TIP]
    > <span data-ttu-id="b6f66-136">Il s’agit également toosee moyen le plus rapide de hello hello des déclencheurs et les actions disponibles pour tous les connecteurs.</span><span class="sxs-lookup"><span data-stu-id="b6f66-136">This is also hello quickest way toosee hello triggers and actions available for any connector.</span></span> <span data-ttu-id="b6f66-137">Tapez dans la partie du nom du connecteur hello, tel que `oracle`.</span><span class="sxs-lookup"><span data-stu-id="b6f66-137">Type in part of hello connector name, such as `oracle`.</span></span> <span data-ttu-id="b6f66-138">le Concepteur de Hello répertorie tous les déclencheurs et les actions.</span><span class="sxs-lookup"><span data-stu-id="b6f66-138">hello designer lists any triggers and any actions.</span></span> 

5. <span data-ttu-id="b6f66-139">Sélectionnez une des actions de hello, tel que **base de données Oracle - Get ligne**.</span><span class="sxs-lookup"><span data-stu-id="b6f66-139">Select one of hello actions, such as **Oracle Database - Get row**.</span></span> <span data-ttu-id="b6f66-140">Sélectionnez l’option **Se connecter via la passerelle de données locale**.</span><span class="sxs-lookup"><span data-stu-id="b6f66-140">Select **Connect via on-premises data gateway**.</span></span> <span data-ttu-id="b6f66-141">Entrez le nom du serveur Oracle hello, méthode d’authentification, nom d’utilisateur, mot de passe et sélectionnez hello passerelle :</span><span class="sxs-lookup"><span data-stu-id="b6f66-141">Enter hello Oracle server name, authentication method, username, password, and select hello gateway:</span></span>

    ![](./media/connectors-create-api-oracledatabase/create-oracle-connection.png)

6. <span data-ttu-id="b6f66-142">Une fois connecté, sélectionnez une table dans la liste de hello et entrez table tooyour des ID de ligne hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-142">Once connected, select a table from hello list, and enter hello row ID tooyour table.</span></span> <span data-ttu-id="b6f66-143">Vous avez besoin de table de toohello tooknow hello identificateur.</span><span class="sxs-lookup"><span data-stu-id="b6f66-143">You need tooknow hello identifier toohello table.</span></span> <span data-ttu-id="b6f66-144">Si vous ne connaissez pas, contactez votre administrateur de base de données Oracle et obtenir la sortie hello `select * from yourTableName`.</span><span class="sxs-lookup"><span data-stu-id="b6f66-144">If you don't know, contact your Oracle DB administrator, and get hello output from `select * from yourTableName`.</span></span> <span data-ttu-id="b6f66-145">Ceci permet de vous hello vous devez tooproceed informations d’identification personnelle.</span><span class="sxs-lookup"><span data-stu-id="b6f66-145">This gives you hello identifiable information you need tooproceed.</span></span>

    <span data-ttu-id="b6f66-146">Dans l’exemple suivant de hello, données de la tâche sont retournées depuis une base de données des ressources humaines :</span><span class="sxs-lookup"><span data-stu-id="b6f66-146">In hello following example, job data is being returned from a Human Resources database:</span></span> 

    ![](./media/connectors-create-api-oracledatabase/table-rowid.png)

7. <span data-ttu-id="b6f66-147">Dans cette étape, vous pouvez utiliser une des hello autres toobuild connecteurs votre flux de travail.</span><span class="sxs-lookup"><span data-stu-id="b6f66-147">In this next step, you can use any of hello other connectors toobuild your workflow.</span></span> <span data-ttu-id="b6f66-148">Si vous souhaitez tootest obtention de données à partir d’Oracle, puis vous envoyez un message électronique avec des données d’Oracle hello à l’aide de hello envoyer par courrier électronique connecteurs, Office 365 ou Gmail de ce type.</span><span class="sxs-lookup"><span data-stu-id="b6f66-148">If you want tootest getting data from Oracle, then send yourself an email with hello Oracle data using one of hello send email connectors, such Office 365 or Gmail.</span></span> <span data-ttu-id="b6f66-149">Utiliser des jetons de hello dynamique à partir de Bonjour Oracle table toobuild Bonjour `Subject` et `Body` de votre adresse de messagerie :</span><span class="sxs-lookup"><span data-stu-id="b6f66-149">Use hello dynamic tokens from hello Oracle table toobuild hello `Subject` and `Body` of your email:</span></span>

    ![](./media/connectors-create-api-oracledatabase/oracle-send-email.png)

8. <span data-ttu-id="b6f66-150">**Enregistrez** votre application logique, puis sélectionnez **Exécuter**.</span><span class="sxs-lookup"><span data-stu-id="b6f66-150">**Save** your logic app, and then select **Run**.</span></span> <span data-ttu-id="b6f66-151">Fermez le Générateur de hello et observez l’historique des exécutions hello pour l’état de hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-151">Close hello designer, and look at hello runs history for hello status.</span></span> <span data-ttu-id="b6f66-152">En cas d’échec, sélectionnez la ligne du message ayant échoué hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-152">If it fails, select hello failed message row.</span></span> <span data-ttu-id="b6f66-153">Hello concepteur s’ouvre et affiche les étape a échoué et indique hello des informations d’erreur.</span><span class="sxs-lookup"><span data-stu-id="b6f66-153">hello designer opens, and shows you which step failed, and also shows hello error information.</span></span> <span data-ttu-id="b6f66-154">Si elle réussit, vous devez recevoir un message électronique contenant les informations de hello que vous avez ajouté.</span><span class="sxs-lookup"><span data-stu-id="b6f66-154">If it succeeds, then you should receive an email with hello information you added.</span></span>


### <a name="workflow-ideas"></a><span data-ttu-id="b6f66-155">Idées de workflow</span><span class="sxs-lookup"><span data-stu-id="b6f66-155">Workflow ideas</span></span>

* <span data-ttu-id="b6f66-156">Vous souhaitez toomonitor hello #oracle #sqlhelp et que vous placez hello tweet dans une base de données afin qu’ils peuvent être consultés et utilisés dans d’autres applications.</span><span class="sxs-lookup"><span data-stu-id="b6f66-156">You want toomonitor hello #oracle hashtag, and put hello tweets in a database so they can be queried, and used within other applications.</span></span> <span data-ttu-id="b6f66-157">Dans une application logique, ajoutez hello `Twitter - When a new tweet is posted` déclencher et entrez hello **#oracle** #sqlhelp.</span><span class="sxs-lookup"><span data-stu-id="b6f66-157">In a logic app, add hello `Twitter - When a new tweet is posted` trigger, and enter hello **#oracle** hashtag.</span></span> <span data-ttu-id="b6f66-158">Ensuite, ajoutez hello `Oracle Database - Insert row` action, puis sélectionnez votre table :</span><span class="sxs-lookup"><span data-stu-id="b6f66-158">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/twitter-oracledb.png)

* <span data-ttu-id="b6f66-159">File d’attente du Service Bus tooa sont envoyés.</span><span class="sxs-lookup"><span data-stu-id="b6f66-159">Messages are sent tooa Service Bus queue.</span></span> <span data-ttu-id="b6f66-160">Vous voulez tooget ces messages et les placer dans une base de données.</span><span class="sxs-lookup"><span data-stu-id="b6f66-160">You want tooget these messages, and put them in a database.</span></span> <span data-ttu-id="b6f66-161">Dans une application logique, ajoutez hello `Service Bus - when a message is received in a queue` déclencheur file d’attente et sélectionnez hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-161">In a logic app, add hello `Service Bus - when a message is received in a queue` trigger, and select hello queue.</span></span> <span data-ttu-id="b6f66-162">Ensuite, ajoutez hello `Oracle Database - Insert row` action, puis sélectionnez votre table :</span><span class="sxs-lookup"><span data-stu-id="b6f66-162">Then, add hello `Oracle Database - Insert row` action, and select your table:</span></span>

    ![](./media/connectors-create-api-oracledatabase/sbqueue-oracledb.png)

## <a name="common-errors"></a><span data-ttu-id="b6f66-163">Erreurs courantes</span><span class="sxs-lookup"><span data-stu-id="b6f66-163">Common errors</span></span>

#### <a name="error-cannot-reach-hello-gateway"></a><span data-ttu-id="b6f66-164">**Erreur**: ne peut pas atteindre hello passerelle</span><span class="sxs-lookup"><span data-stu-id="b6f66-164">**Error**: Cannot reach hello Gateway</span></span>

<span data-ttu-id="b6f66-165">**Cause**: passerelle de données locale hello n’est pas en mesure de tooconnect toohello cloud.</span><span class="sxs-lookup"><span data-stu-id="b6f66-165">**Cause**: hello on-premises data gateway is not able tooconnect toohello cloud.</span></span> 

<span data-ttu-id="b6f66-166">**Atténuation**: Assurez-vous que votre passerelle s’exécute sur l’ordinateur local, hello où vous l’avez installé et qu’il peut se connecter toohello internet.</span><span class="sxs-lookup"><span data-stu-id="b6f66-166">**Mitigation**: Make sure your gateway is running on hello on-premises machine where you installed it, and that it can connect toohello internet.</span></span>  <span data-ttu-id="b6f66-167">Nous vous recommandons ne pas l’installation de passerelle de hello sur un ordinateur qui peut être mis hors tension ou le mode veille.</span><span class="sxs-lookup"><span data-stu-id="b6f66-167">We recommend not installing hello gateway on a computer that may be turned off or sleep.</span></span> <span data-ttu-id="b6f66-168">Vous pouvez également redémarrer le service de passerelle de données hello local (PBIEgwService).</span><span class="sxs-lookup"><span data-stu-id="b6f66-168">You can also restart hello on-premises data gateway service (PBIEgwService).</span></span>

#### <a name="error-hello-provider-being-used-is-deprecated-systemdataoracleclient-requires-oracle-client-software-version-817-or-greater-please-visit-httpsgomicrosoftcomfwlinkplinkid272376httpsgomicrosoftcomfwlinkplinkid272376-tooinstall-hello-official-provider"></a><span data-ttu-id="b6f66-169">**Erreur**: fournisseur hello utilisé est déconseillé : ' System.Data.OracleClient requiert le logiciel client Oracle version 8.1.7 ou ultérieure.'.</span><span class="sxs-lookup"><span data-stu-id="b6f66-169">**Error**: hello provider being used is deprecated: 'System.Data.OracleClient requires Oracle client software version 8.1.7 or greater.'.</span></span> <span data-ttu-id="b6f66-170">Visitez [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) fournisseur officiel de tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-170">Please visit [https://go.microsoft.com/fwlink/p/?LinkID=272376](https://go.microsoft.com/fwlink/p/?LinkID=272376) tooinstall hello official provider.</span></span>

<span data-ttu-id="b6f66-171">**Cause**: hello Oracle clients SDK n’est pas installé sur l’ordinateur de hello où hello locaux passerelle de données est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b6f66-171">**Cause**: hello Oracle client SDK is not installed on hello machine where hello on-premises data gateway is running.</span></span>  

<span data-ttu-id="b6f66-172">**Résolution**: télécharger et installer le Kit de développement logiciel du client Oracle hello sur hello même ordinateur en tant que passerelle de données locale hello.</span><span class="sxs-lookup"><span data-stu-id="b6f66-172">**Resolution**: Download and install hello Oracle client SDK on hello same computer as hello on-premises data gateway.</span></span>

#### <a name="error-table-tablename-does-not-define-any-key-columns"></a><span data-ttu-id="b6f66-173">**Erreur** : La table « [Tablename] » ne définit aucune colonne clé</span><span class="sxs-lookup"><span data-stu-id="b6f66-173">**Error**: Table '[Tablename]' does not define any key columns</span></span>

<span data-ttu-id="b6f66-174">**Cause**: table de hello n’a pas de clé primaire.</span><span class="sxs-lookup"><span data-stu-id="b6f66-174">**Cause**: hello table does not have any primary key.</span></span>  

<span data-ttu-id="b6f66-175">**Résolution**: connecteur de base de données Oracle hello requiert qu’une table avec une colonne clé primaire.</span><span class="sxs-lookup"><span data-stu-id="b6f66-175">**Resolution**: hello Oracle Database connector requires that a table with a primary key column be used.</span></span>

#### <a name="currently-not-supported"></a><span data-ttu-id="b6f66-176">Actuellement non pris en charge</span><span class="sxs-lookup"><span data-stu-id="b6f66-176">Currently not supported</span></span>

* <span data-ttu-id="b6f66-177">Vues et procédures stockées</span><span class="sxs-lookup"><span data-stu-id="b6f66-177">Views and stored procedures</span></span> 
* <span data-ttu-id="b6f66-178">Toute table avec des clés composites</span><span class="sxs-lookup"><span data-stu-id="b6f66-178">Any table with composite keys</span></span>
* <span data-ttu-id="b6f66-179">Types d’objet imbriqués dans des tables</span><span class="sxs-lookup"><span data-stu-id="b6f66-179">Nested object types in tables</span></span>
 
## <a name="connector-specific-details"></a><span data-ttu-id="b6f66-180">Détails spécifiques du connecteur</span><span class="sxs-lookup"><span data-stu-id="b6f66-180">Connector-specific details</span></span>

<span data-ttu-id="b6f66-181">Afficher les déclencheurs et les actions définies dans les swagger hello et également voir les limites Bonjour [détails du connecteur](/connectors/oracle/).</span><span class="sxs-lookup"><span data-stu-id="b6f66-181">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/oracle/).</span></span> 

## <a name="get-some-help"></a><span data-ttu-id="b6f66-182">Obtenir de l’aide</span><span class="sxs-lookup"><span data-stu-id="b6f66-182">Get some help</span></span>

<span data-ttu-id="b6f66-183">Hello [forum de Azure Logic Apps](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) est une bonne placez tooask questions, répondez aux questions et voir ce que font les autres utilisateurs Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="b6f66-183">hello [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps) is a great place tooask questions, answer questions, and see what other Logic Apps users are doing.</span></span> 

<span data-ttu-id="b6f66-184">Vous pouvez améliorer Logic Apps et les connecteurs en votant et en soumettant vos idées sur [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span><span class="sxs-lookup"><span data-stu-id="b6f66-184">You can help improve Logic Apps and connectors by voting and submitting your ideas at [http://aka.ms/logicapps-wish](http://aka.ms/logicapps-wish).</span></span> 


## <a name="next-steps"></a><span data-ttu-id="b6f66-185">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b6f66-185">Next steps</span></span>
<span data-ttu-id="b6f66-186">[Créer une application logique](../logic-apps/logic-apps-create-a-logic-app.md)et Explorer les connecteurs disponibles hello dans Logic Apps à notre [liste des API](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="b6f66-186">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md), and explore hello available connectors in Logic Apps at our [APIs list](apis-list.md).</span></span>
