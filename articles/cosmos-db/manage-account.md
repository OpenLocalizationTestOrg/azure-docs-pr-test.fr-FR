---
title: "aaaManage un compte de base de données Azure Cosmos via hello portail Azure | Documents Microsoft"
description: "Découvrez comment toomanage votre base de données Azure Cosmos compte via hello portail Azure. Rechercher un guide sur l’utilisation de tooview du portail Azure hello, copier, supprimer et l’accès des comptes."
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
ms.openlocfilehash: 77ad953cf558a519674be08ad913a12202f69496
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomanage-an-azure-cosmos-db-account"></a><span data-ttu-id="a73d5-105">Comment toomanage un compte de base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="a73d5-105">How toomanage an Azure Cosmos DB account</span></span>
<span data-ttu-id="a73d5-106">Découvrez comment la cohérence tooset, travailler avec les clés et supprimer un compte de base de données Azure Cosmos Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="a73d5-106">Learn how tooset global consistency, work with keys, and delete an Azure Cosmos DB account in hello Azure portal.</span></span>

## <span data-ttu-id="a73d5-107"><a id="consistency"></a>Gérer les paramètres de cohérence Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a73d5-107"><a id="consistency"></a>Manage Azure Cosmos DB consistency settings</span></span>
<span data-ttu-id="a73d5-108">En sélectionnant le niveau de cohérence droite hello dépend de la sémantique de hello de votre application.</span><span class="sxs-lookup"><span data-stu-id="a73d5-108">Selecting hello right consistency level depends on hello semantics of your application.</span></span> <span data-ttu-id="a73d5-109">Vous devez vous familiariser avec les niveaux de cohérence disponible hello dans la base de données Azure Cosmos en lisant [à l’aide de la cohérence des niveaux de disponibilité de toomaximize et les performances dans la base de données Azure Cosmos][consistency].</span><span class="sxs-lookup"><span data-stu-id="a73d5-109">You should familiarize yourself with hello available consistency levels in Azure Cosmos DB by reading [Using consistency levels toomaximize availability and performance in Azure Cosmos DB][consistency].</span></span> <span data-ttu-id="a73d5-110">Azure Cosmos DB fournit les garanties de cohérence, de disponibilité et de performance, à tous les niveaux de cohérence disponibles pour votre compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="a73d5-110">Azure Cosmos DB provides consistency, availability, and performance guarantees, at every consistency level available for your database account.</span></span> <span data-ttu-id="a73d5-111">Configuration de votre compte de base de données avec un niveau de cohérence de fort requiert que vos données sont confiné tooa une seule région Azure et non globalement disponible.</span><span class="sxs-lookup"><span data-stu-id="a73d5-111">Configuring your database account with a consistency level of Strong requires that your data is confined tooa single Azure region and not globally available.</span></span> <span data-ttu-id="a73d5-112">On hello d’autre part, hello des niveaux de cohérence souple - obsolescence limitée, de session ou d’activer éventuelle vous tooassociate n’importe quel nombre de régions Azure avec votre compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="a73d5-112">On hello other hand, hello relaxed consistency levels - bounded staleness, session or eventual enable you tooassociate any number of Azure regions with your database account.</span></span> <span data-ttu-id="a73d5-113">Hello suivant étapes simples vous montre comment tooselect hello le niveau de cohérence par défaut pour votre compte de base de données.</span><span class="sxs-lookup"><span data-stu-id="a73d5-113">hello following simple steps show you how tooselect hello default consistency level for your database account.</span></span> 

### <a name="toospecify-hello-default-consistency-for-an-azure-cosmos-db-account"></a><span data-ttu-id="a73d5-114">toospecify hello par défaut la cohérence pour un compte de base de données Azure Cosmos</span><span class="sxs-lookup"><span data-stu-id="a73d5-114">toospecify hello default consistency for an Azure Cosmos DB account</span></span>
1. <span data-ttu-id="a73d5-115">Bonjour [portail Azure](https://portal.azure.com/), accéder à votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-115">In hello [Azure portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="a73d5-116">Dans le panneau de compte hello, cliquez sur **par défaut de la cohérence**.</span><span class="sxs-lookup"><span data-stu-id="a73d5-116">In hello account blade, click **Default consistency**.</span></span>
3. <span data-ttu-id="a73d5-117">Bonjour **cohérence par défaut** panneau, niveau de cohérence hello sélectionnez Nouveau, cliquez sur **enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="a73d5-117">In hello **Default Consistency** blade, select hello new consistency level and click **Save**.</span></span>
    <span data-ttu-id="a73d5-118">![Cohérence par défaut Session][5]</span><span class="sxs-lookup"><span data-stu-id="a73d5-118">![Default consistency session][5]</span></span>

## <span data-ttu-id="a73d5-119"><a id="keys"></a>Affichage, copie et régénération des clés d’accès</span><span class="sxs-lookup"><span data-stu-id="a73d5-119"><a id="keys"></a>View, copy, and regenerate access keys</span></span>
<span data-ttu-id="a73d5-120">Lorsque vous créez un compte de base de données Azure Cosmos, service de hello génère deux clés d’accès maître qui peuvent être utilisés pour l’authentification lors de l’accès hello compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-120">When you create an Azure Cosmos DB account, hello service generates two master access keys that can be used for authentication when hello Azure Cosmos DB account is accessed.</span></span> <span data-ttu-id="a73d5-121">En fournissant deux clés d’accès, base de données Azure Cosmos vous permet de clés de hello tooregenerate avec aucune tooyour d’interruption du compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-121">By providing two access keys, Azure Cosmos DB enables you tooregenerate hello keys with no interruption tooyour Azure Cosmos DB account.</span></span> 

<span data-ttu-id="a73d5-122">Bonjour [portail Azure](https://portal.azure.com/), hello d’accès **clés** panneau à partir du menu ressources hello hello **compte de base de données Azure Cosmos** panneau tooview, copier et régénérer hello touches d’accès sont tooaccess utilisé votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-122">In hello [Azure portal](https://portal.azure.com/), access hello **Keys** blade from hello resource menu on hello **Azure Cosmos DB account** blade tooview, copy, and regenerate hello access keys that are used tooaccess your Azure Cosmos DB account.</span></span>

![Capture d’écran du portail Azure, panneau Clés](./media/manage-account/keys.png)

> [!NOTE]
> <span data-ttu-id="a73d5-124">Hello **clés** panneau inclut également principal et de chaînes de connexion secondaire qui peuvent être utilisé tooconnect tooyour compte du hello [outil de Migration de données](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="a73d5-124">hello **Keys** blade also includes primary and secondary connection strings that can be used tooconnect tooyour account from hello [Data Migration Tool](import-data.md).</span></span>
> 
> 

<span data-ttu-id="a73d5-125">Des clés en lecture seule sont également disponibles sur ce panneau.</span><span class="sxs-lookup"><span data-stu-id="a73d5-125">Read-only keys are also available on this blade.</span></span> <span data-ttu-id="a73d5-126">Les lectures et les demandes sont des opérations en lecture seule, contrairement aux opérations de création, de suppression et de remplacement.</span><span class="sxs-lookup"><span data-stu-id="a73d5-126">Reads and queries are read-only operations, while creates, deletes, and replaces are not.</span></span>

### <a name="copy-an-access-key-in-hello-azure-portal"></a><span data-ttu-id="a73d5-127">Copier une clé d’accès Bonjour portail Azure</span><span class="sxs-lookup"><span data-stu-id="a73d5-127">Copy an access key in hello Azure Portal</span></span>
<span data-ttu-id="a73d5-128">Sur hello **clés** panneau, cliquez sur hello **copie** toohello bouton à droite de la clé de hello que vous souhaitez toocopy.</span><span class="sxs-lookup"><span data-stu-id="a73d5-128">On hello **Keys** blade, click hello **Copy** button toohello right of hello key you wish toocopy.</span></span>

![Afficher et copier une clé d’accès Bonjour Azure Portal, panneau de clés](./media/manage-account/copykeys.png)

### <a name="regenerate-access-keys"></a><span data-ttu-id="a73d5-130">Régénération de clés d'accès</span><span class="sxs-lookup"><span data-stu-id="a73d5-130">Regenerate access keys</span></span>
<span data-ttu-id="a73d5-131">Vous devez modifier le compte de base de données Azure Cosmos tooyour hello accès clés périodiquement toohelp renforcer vos connexions.</span><span class="sxs-lookup"><span data-stu-id="a73d5-131">You should change hello access keys tooyour Azure Cosmos DB account periodically toohelp keep your connections more secure.</span></span> <span data-ttu-id="a73d5-132">Deux clés d’accès sont affectés tooenable connexions toomaintain vous toohello compte de base de données Azure Cosmos à l’aide d’une clé d’accès pendant la régénération de hello autre clé d’accès.</span><span class="sxs-lookup"><span data-stu-id="a73d5-132">Two access keys are assigned tooenable you toomaintain connections toohello Azure Cosmos DB account using one access key while you regenerate hello other access key.</span></span>

> [!WARNING]
> <span data-ttu-id="a73d5-133">Régénérer vos clés d’accès affecte toutes les applications qui dépendent de la clé actuelle de hello.</span><span class="sxs-lookup"><span data-stu-id="a73d5-133">Regenerating your access keys affects any applications that are dependent on hello current key.</span></span> <span data-ttu-id="a73d5-134">Tous les clients qui utilisent le compte de base de données Azure Cosmos hello accès tooaccess clé hello doivent être la nouvelle clé de hello toouse mis à jour.</span><span class="sxs-lookup"><span data-stu-id="a73d5-134">All clients that use hello access key tooaccess hello Azure Cosmos DB account must be updated toouse hello new key.</span></span>
> 
> 

<span data-ttu-id="a73d5-135">Si vous avez des applications ou services de cloud computing à l’aide du compte de base de données Azure Cosmos de hello, vous perdrez les connexions hello si vous régénérez des clés, sauf si vous régénérez vos clés.</span><span class="sxs-lookup"><span data-stu-id="a73d5-135">If you have applications or cloud services using hello Azure Cosmos DB account, you will lose hello connections if you regenerate keys, unless you roll your keys.</span></span> <span data-ttu-id="a73d5-136">Hello étapes suivantes décrivent les processus hello de transfert de vos clés.</span><span class="sxs-lookup"><span data-stu-id="a73d5-136">hello following steps outline hello process involved in rolling your keys.</span></span>

1. <span data-ttu-id="a73d5-137">Mettre à jour la clé d’accès hello dans votre clé d’accès secondaire application code tooreference hello Hello compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-137">Update hello access key in your application code tooreference hello secondary access key of hello Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="a73d5-138">Régénérer la clé d’accès primaire hello pour votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-138">Regenerate hello primary access key for your Azure Cosmos DB account.</span></span> <span data-ttu-id="a73d5-139">Bonjour [Azure Portal](https://portal.azure.com/), accéder à votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-139">In hello [Azure Portal](https://portal.azure.com/), access your Azure Cosmos DB account.</span></span>
3. <span data-ttu-id="a73d5-140">Bonjour **compte de base de données Azure Cosmos** panneau, cliquez sur **clés**.</span><span class="sxs-lookup"><span data-stu-id="a73d5-140">In hello **Azure Cosmos DB Account** blade, click **Keys**.</span></span>
4. <span data-ttu-id="a73d5-141">Sur hello **clés** panneau, cliquez sur hello régénérer, puis cliquez sur **Ok** tooconfirm que vous souhaitez toogenerate une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="a73d5-141">On hello **Keys** blade, click hello regenerate button, then click **Ok** tooconfirm that you want toogenerate a new key.</span></span>
    <span data-ttu-id="a73d5-142">![Régénération des clés d’accès](./media/manage-account/regenerate-keys.png)</span><span class="sxs-lookup"><span data-stu-id="a73d5-142">![Regenerate access keys](./media/manage-account/regenerate-keys.png)</span></span>
5. <span data-ttu-id="a73d5-143">Une fois que vous avez vérifié de cette nouvelle clé de hello est disponible pour une utilisation (environ 5 minutes après la régénération), mettre à jour la clé d’accès hello dans votre application code tooreference hello nouvelle clé primaire.</span><span class="sxs-lookup"><span data-stu-id="a73d5-143">Once you have verified that hello new key is available for use (approximately 5 minutes after regeneration), update hello access key in your application code tooreference hello new primary access key.</span></span>
6. <span data-ttu-id="a73d5-144">Régénérer la clé d’accès secondaire hello.</span><span class="sxs-lookup"><span data-stu-id="a73d5-144">Regenerate hello secondary access key.</span></span>
   
    ![Régénération de clés d'accès](./media/manage-account/regenerate-secondary-key.png)

> [!NOTE]
> <span data-ttu-id="a73d5-146">Il peut prendre plusieurs minutes avant d’une clé qui vient d’être générée peut être tooaccess utilisé votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-146">It can take several minutes before a newly generated key can be used tooaccess your Azure Cosmos DB account.</span></span>
> 
> 

## <a name="get-hello--connection-string"></a><span data-ttu-id="a73d5-147">Obtenir la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="a73d5-147">Get hello  connection string</span></span>
<span data-ttu-id="a73d5-148">tooretrieve votre connexion de chaîne, hello suivant :</span><span class="sxs-lookup"><span data-stu-id="a73d5-148">tooretrieve your connection string, do hello following:</span></span> 

1. <span data-ttu-id="a73d5-149">Bonjour [portail Azure](https://portal.azure.com), accéder à votre compte de base de données Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="a73d5-149">In hello [Azure portal](https://portal.azure.com), access your Azure Cosmos DB account.</span></span>
2. <span data-ttu-id="a73d5-150">Dans le menu de ressource hello, cliquez sur **clés**.</span><span class="sxs-lookup"><span data-stu-id="a73d5-150">In hello resource menu, click **Keys**.</span></span>
3. <span data-ttu-id="a73d5-151">Cliquez sur hello **copie** toohello suivant du bouton **chaîne de connexion principal** ou **chaîne de connexion secondaire** boîte.</span><span class="sxs-lookup"><span data-stu-id="a73d5-151">Click hello **Copy** button next toohello **Primary Connection String** or **Secondary Connection String** box.</span></span> 

<span data-ttu-id="a73d5-152">Si vous utilisez une chaîne de connexion hello Bonjour [outil de Migration de base de données Azure Cosmos DB](import-data.md), ajouter hello de base de données nom toohello end hello de chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="a73d5-152">If you are using hello connection string in hello [Azure Cosmos DB Database Migration Tool](import-data.md), append hello database name toohello end of hello connection string.</span></span> <span data-ttu-id="a73d5-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span><span class="sxs-lookup"><span data-stu-id="a73d5-153">`AccountEndpoint=< >;AccountKey=< >;Database=< >`.</span></span>

## <span data-ttu-id="a73d5-154"><a id="delete"></a> Supprimer un compte Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="a73d5-154"><a id="delete"></a> Delete an Azure Cosmos DB account</span></span>
<span data-ttu-id="a73d5-155">tooremove une base de données Azure Cosmos compte hello portail Azure que vous n’utilisez plus, nom du compte hello avec le bouton droit, puis cliquez sur **supprimer le compte**.</span><span class="sxs-lookup"><span data-stu-id="a73d5-155">tooremove an Azure Cosmos DB account from hello Azure Portal that you are no longer using, right-click hello account name, and click **Delete account**.</span></span>

![Procédure toodelete une base de données Azure Cosmos compte dans hello portail Azure](./media/manage-account/deleteaccount.png)

1. <span data-ttu-id="a73d5-157">Bonjour [portail Azure](https://portal.azure.com/), accéder au compte de base de données Azure Cosmos hello toodelete vous le souhaitez.</span><span class="sxs-lookup"><span data-stu-id="a73d5-157">In hello [Azure portal](https://portal.azure.com/), access hello Azure Cosmos DB account you wish toodelete.</span></span>
2. <span data-ttu-id="a73d5-158">Sur hello **compte de base de données Azure Cosmos** panneau, cliquez sur le compte de hello, puis cliquez sur **supprimer un compte**.</span><span class="sxs-lookup"><span data-stu-id="a73d5-158">On hello **Azure Cosmos DB account** blade, right-click hello account, and then click **Delete Account**.</span></span> 
3. <span data-ttu-id="a73d5-159">Sur le panneau de confirmation qui en résulte hello, tapez tooconfirm de nom du compte de base de données Azure Cosmos hello toodelete hello compte.</span><span class="sxs-lookup"><span data-stu-id="a73d5-159">On hello resulting confirmation blade, type hello Azure Cosmos DB account name tooconfirm that you want toodelete hello account.</span></span>
4. <span data-ttu-id="a73d5-160">Cliquez sur hello **supprimer** bouton.</span><span class="sxs-lookup"><span data-stu-id="a73d5-160">Click hello **Delete** button.</span></span>

![Procédure toodelete une base de données Azure Cosmos compte dans hello portail Azure](./media/manage-account/delete-account-confirm.png)

## <span data-ttu-id="a73d5-162"><a id="next"></a>Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a73d5-162"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="a73d5-163">Découvrez comment trop[prise en main votre compte de base de données Azure Cosmos](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span><span class="sxs-lookup"><span data-stu-id="a73d5-163">Learn how too[get started with your Azure Cosmos DB account](http://go.microsoft.com/fwlink/p/?LinkId=402364).</span></span>

<!--Image references-->
[5]: ./media/manage-account/documentdb_change_consistency-1.png

<!--Reference style links - using these makes hello source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: consistency-levels.md
[azureregions]: https://azure.microsoft.com/regions/#services
[offers]: https://azure.microsoft.com/pricing/details/cosmos-db/
