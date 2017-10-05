---
title: "Gestion d’un compte Azure Cosmos DB via le portail Azure | Microsoft Docs"
description: "Apprenez à gérer votre compte Azure Cosmos DB via le portail Azure. Trouvez un guide vous expliquant comment utiliser le portail Azure pour afficher, copier, supprimer et accéder aux comptes."
keywords: Portail Azure, documentdb, azure, Microsoft azure
services: cosmos-db
documentationcenter: 
author: kirillg
manager: jhubbard
editor: cgronlun
ms.assetid: 00fc172f-f86c-44ca-8336-11998dcab45c
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: kirillg
ms.openlocfilehash: a0c6ec8d490e1adacc96758971ab91d8eaeab45c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-manage-an-azure-cosmos-db-account"></a><span data-ttu-id="b7578-105">Comment gérer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7578-105">How to manage an Azure Cosmos DB account</span></span>
<span data-ttu-id="b7578-106">Découvrez comment définir la cohérence globale, utiliser les clés et supprimer un compte Azure Cosmos DB dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b7578-106">Learn how to set global consistency, work with keys, and delete an Azure Cosmos DB account in the Azure portal.</span></span>

## <span data-ttu-id="b7578-107"><a id="consistency"></a>Gérer les paramètres de cohérence Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7578-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="b7578-108">La sélection du niveau de cohérence adéquat dépend de la sémantique de votre application.</span><span class="sxs-lookup"><span data-stu-id="b7578-108">Selecting the right consistency level depends on the semantics of your application.</span></span> <span data-ttu-id="b7578-109">Vous devez vous familiariser avec les niveaux de cohérence disponibles dans Azure Cosmos DB en lisant l’article relatif à [l’utilisation des niveaux de cohérence pour optimiser la disponibilité et les performances dans Azure Cosmos DB][consistency].</span><span class="sxs-lookup"><span data-stu-id="b7578-109">You should familiarize yourself with the available consistency levels in Azure Cosmos DB by reading [Using consistency levels to maximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="b7578-110">Azure Cosmos DB fournit les garanties de cohérence, de disponibilité et de performance, à tous les niveaux de cohérence disponibles pour votre compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="b7578-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="b7578-111">La configuration de votre compte de base de données avec un niveau de cohérence Fort nécessite que vos données se limitent à une seule région Azure et ne soient pas disponibles mondialement.</span><span class="sxs-lookup"><span data-stu-id="b7578-111">Configuring your database account with a consistency level of Strong requires that your data is confined to a single Azure region and not globally available.</span></span> <span data-ttu-id="b7578-112">En revanche, les niveaux de cohérence souples (Obsolescence limitée, Session ou Éventuel) vous permettent d’associer autant de régions Azure que vous le souhaitez à votre compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="b7578-112">On the other hand, the relaxed consistency levels - bounded staleness, session or eventual enable you to associate any number of Azure regions with your database account.</span></span> <span data-ttu-id="b7578-113">Les étapes simples suivantes vous montrent comment sélectionner le niveau de cohérence par défaut pour votre compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="b7578-113">The following simple steps show you how to select the default consistency level for your database account.</span></span> 

### <a name="to-specify-the-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="b7578-114">Pour spécifier le niveau de cohérence par défaut d’un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7578-114">To specify the default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="b7578-115">Dans le [portail Azure](https://portal.azure.com/), accédez à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-115">In the [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="b7578-116">Dans le panneau du compte, cliquez sur **Cohérence par défaut**.</span><span class="sxs-lookup"><span data-stu-id="b7578-116">In the account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="b7578-117">Dans le panneau **Cohérence par défaut**, sélectionnez le nouveau niveau de cohérence et cliquez sur **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="b7578-117">In the **Default Consistency** blade, select the new consistency level and click **Save**.</span></span>
    <span data-ttu-id="b7578-118">![Cohérence par défaut Session][5]</span><span class="sxs-lookup"><span data-stu-id="b7578-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="b7578-119"><a id="keys"></a>Affichage, copie et régénération des clés d’accès</span><span class="sxs-lookup"><span data-stu-id="b7578-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="b7578-120">Lorsque vous créez un compte Azure Cosmos DB, le service génère deux clés d’accès maître qui peuvent être utilisées pour l’authentification lors de l’accès au compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-120">When you create an Azure Cosmos DB account, the service generates two master access keys that can be used for authentication when the Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="b7578-121">En fournissant deux clés d'accès, Azure Cosmos DB vous permet de régénérer les clés sans interruption de votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-121">By providing two access keys, Azure Cosmos DB enables you to regenerate the keys with no interruption to your Azure Cosmos DB account.</span></span> 

<span data-ttu-id="b7578-122">Dans le [portail Azure](https://portal.azure.com/), accédez au panneau **Clés** à partir du menu de ressources dans le panneau **Compte Azure Cosmos DB** pour afficher, copier et régénérer les clés d’accès à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-122">In the [Azure portal](https://portal.azure.com/), access the **Keys** blade from the resource menu on the **Azure Cosmos DB account** blade to view, copy, and regenerate the access keys that are used to access your Azure Cosmos DB account.</span></span>

![Capture d’écran du portail Azure, panneau Clés](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="b7578-124">Le panneau **Clés** inclut également des chaînes de connexion primaire et secondaire qui peuvent être utilisées pour la connexion à votre compte à partir de [l’outil de migration de données](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="b7578-124">The **Keys** blade also includes primary and secondary connection strings that can be used to connect to your account from the [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="b7578-125">Des clés en lecture seule sont également disponibles sur ce panneau.</span><span class="sxs-lookup"><span data-stu-id="b7578-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="b7578-126">Les lectures et les demandes sont des opérations en lecture seule, contrairement aux opérations de création, de suppression et de remplacement.</span><span class="sxs-lookup"><span data-stu-id="b7578-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-the-azure-portal"></a><span data-ttu-id="b7578-127">Copie d’une touche d’accès rapide dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="b7578-127">Copy an access key in the Azure Portal</span></span>
<span data-ttu-id="b7578-128">Dans le panneau **Clés**, cliquez sur le bouton **Copier** à droite de la clé que vous souhaitez copier.</span><span class="sxs-lookup"><span data-stu-id="b7578-128">On the **Keys** blade, click the **Copy** button to the right of the key you wish to copy.</span></span>

![Affichage et copie d’une touche d’accès rapide dans le portail Azure, panneau Clés](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="b7578-130">Régénération de clés d'accès</span><span class="sxs-lookup"><span data-stu-id="b7578-130">Regenerate access keys</span></span>
<span data-ttu-id="b7578-131">Vous devez modifier périodiquement les clés d'accès à votre compte Azure Cosmos DB pour garantir la sécurité des connexions.</span><span class="sxs-lookup"><span data-stu-id="b7578-131">You should change the access keys to your Azure Cosmos DB account periodically to help keep your connections more secure.</span></span> <span data-ttu-id="b7578-132">Deux clés d’accès vous sont affectées afin de vous permettre de conserver des connexions au compte Azure Cosmos DB à l’aide d’une clé d’accès lorsque vous régénérez l’autre clé.</span><span class="sxs-lookup"><span data-stu-id="b7578-132">Two access keys are assigned to enable you to maintain connections to the Azure Cosmos DB account using one access key while you regenerate the other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="b7578-133">La régénération de vos clés d'accès affecte toutes les applications qui dépendent de la clé actuelle.</span><span class="sxs-lookup"><span data-stu-id="b7578-133">Regenerating your access keys affects any applications that are dependent on the current key.</span></span> <span data-ttu-id="b7578-134">Tous les clients qui utilisent la clé d’accès pour accéder au compte Azure Cosmos DB doivent être mis à jour pour utiliser la nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="b7578-134">All clients that use the access key to access the Azure Cosmos DB account must be updated to use the new key.</span></span>
> 
> 

<span data-ttu-id="b7578-135">Si certains de vos services cloud ou applications utilisent le compte Azure Cosmos DB, vous perdrez les connexions en régénérant les clés, sauf si vous remplacez vos clés.</span><span class="sxs-lookup"><span data-stu-id="b7578-135">If you have applications or cloud services using the Azure Cosmos DB account, you will lose the connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="b7578-136">Les étapes suivantes décrivent le processus de remplacement de vos clés.</span><span class="sxs-lookup"><span data-stu-id="b7578-136">The following steps outline the process involved in rolling your keys.</span></span>

1. <span data-ttu-id="b7578-137">Mettez à jour la clé d’accès dans le code de votre application afin de référencer la clé d’accès secondaire du compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-137">Update the access key in your application code to reference the secondary access key of the Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="b7578-138">Régénérez la clé d’accès principale de votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-138">Regenerate the primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="b7578-139">Dans le [portail Azure](https://portal.azure.com/), accédez à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-139">In the [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="b7578-140">Dans le panneau **Compte Azure Cosmos DB**, cliquez sur **Clés**.</span><span class="sxs-lookup"><span data-stu-id="b7578-140">In the **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="b7578-141">Dans le panneau **Clés**, cliquez sur le bouton Régénérer, puis sur **OK** pour confirmer que vous souhaitez générer une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="b7578-141">On the **Keys** blade, click the regenerate button, then click **Ok** to confirm that you want to generate a new key.</span></span>
    <span data-ttu-id="b7578-142">![Régénération des clés d’accès](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="b7578-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="b7578-143">Une fois que vous avez vérifié que la nouvelle clé peut être utilisée(environ 5 minutes après la régénération), mettez à jour la clé d'accès dans le code de votre application afin de référencer la nouvelle clé d'accès primaire.</span><span class="sxs-lookup"><span data-stu-id="b7578-143">Once you have verified that the new key is available for use (approximately 5 minutes after regeneration), update the access key in your application code to reference the new primary access key.</span></span>
6. <span data-ttu-id="b7578-144">Régénérez la clé d’accès secondaire.</span><span class="sxs-lookup"><span data-stu-id="b7578-144">Regenerate the secondary access key.</span></span>
   
    ![Régénération de clés d'accès](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="b7578-146">Il faut parfois attendre plusieurs minutes avant de pouvoir utiliser une clé qui vient d’être générée pour accéder à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-146">It can take several minutes before a newly generated key can be used to access your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-the--connection-string"></a><span data-ttu-id="b7578-147">Obtention de la chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="b7578-147">Get the  connection string</span></span>
<span data-ttu-id="b7578-148">Procédez comme suit pour récupérer votre chaîne de connexion :</span><span class="sxs-lookup"><span data-stu-id="b7578-148">To retrieve your connection string, do the following:</span></span> 

1. <span data-ttu-id="b7578-149">Dans le [portail Azure](https://portal.azure.com), accédez à votre compte Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b7578-149">In the [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="b7578-150">Dans le menu de ressources, cliquez sur **Clés**.</span><span class="sxs-lookup"><span data-stu-id="b7578-150">In the resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="b7578-151">Cliquez sur le bouton **Copier** situé en regard de la case **Chaîne de connexion principale** ou de la case **Chaîne de connexion secondaire**.</span><span class="sxs-lookup"><span data-stu-id="b7578-151">Click the **Copy** button next to the **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="b7578-152">Si vous utilisez la chaîne de connexion dans [l’outil de migration de base de données Azure Cosmos DB](import-data.md), ajoutez le nom de la base de données à la fin de la chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="b7578-152">If you are using the connection string in the [Azure Cosmos DB Database Migration Tool](import-data.md), append the database name to the end of the connection string.</span></span> <span data-ttu-id="b7578-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="b7578-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="b7578-154"><a id="delete"></a> Supprimer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="b7578-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="b7578-155">Pour supprimer du portail Azure un compte Azure Cosmos DB dont vous ne vous servez plus, cliquez avec le bouton droit sur le nom du compte, puis cliquez sur **Supprimer le compte**.</span><span class="sxs-lookup"><span data-stu-id="b7578-155">To remove an Azure Cosmos DB account from the Azure Portal that you are no longer using, right-click the account name, and click **Delete account**.</span></span>

![Comment supprimer un compte Azure Cosmos DB dans le portail Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="b7578-157">Dans le [portail Azure](https://portal.azure.com/), accédez au compte Azure Cosmos DB à supprimer.</span><span class="sxs-lookup"><span data-stu-id="b7578-157">In the [Azure portal](https://portal.azure.com/), access the Azure Cosmos DB account you wish to delete.</span></span>
2. <span data-ttu-id="b7578-158">Dans le panneau **Compte Azure Cosmos DB**, cliquez avec le bouton droit sur le compte, puis cliquez sur **Supprimer le compte**.</span><span class="sxs-lookup"><span data-stu-id="b7578-158">On the **Azure Cosmos DB account** blade, right-click the account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="b7578-159">Dans le volet de confirmation qui s'affiche, entrez le nom du compte Azure Cosmos DB pour confirmer que vous souhaitez le supprimer.</span><span class="sxs-lookup"><span data-stu-id="b7578-159">On the resulting confirmation blade, type the Azure Cosmos DB account name to confirm that you want to delete the account.</span></span>
4. <span data-ttu-id="b7578-160">Cliquez sur le bouton **Supprimer** .</span><span class="sxs-lookup"><span data-stu-id="b7578-160">Click the **Delete** button.</span></span>

![Comment supprimer un compte Azure Cosmos DB dans le portail Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="b7578-162"><a id="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b7578-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="b7578-163">Découvrez comment [prendre en main votre compte Azure Cosmos DB](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="b7578-163">Learn how to [get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
