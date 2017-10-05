---
title: "Ports au-delà de 1433 pour SQL Database | Microsoft Docs"
description: "Parfois, les connexions clientes entre ADO.NET et Azure SQL Database ignorent le proxy et interagissent directement avec la base de données. Les ports autres que le port 1433 deviennent importants."
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="7ee63-104">Ports au-delà de 1433 pour ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="7ee63-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="7ee63-105">Cette rubrique décrit le comportement de connexion d’Azure SQL Database pour les clients qui utilisent ADO.NET version 4.5 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="7ee63-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7ee63-106">Pour plus d’informations sur l’architecture de connectivité, consultez [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md) (Architecture de connectivité d’Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="7ee63-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="7ee63-107">À l’extérieur et à l’intérieur</span><span class="sxs-lookup"><span data-stu-id="7ee63-107">Outside vs inside</span></span>
<span data-ttu-id="7ee63-108">Pour les connexions à Azure SQL Database, nous devons d’abord déterminer si le programme client s’exécute *à l’extérieur* ou *à l’intérieur* de la limite du cloud Azure.</span><span class="sxs-lookup"><span data-stu-id="7ee63-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="7ee63-109">Les sous-sections suivantes abordent deux scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="7ee63-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="7ee63-110">*À l’extérieur :* le client s’exécute sur votre ordinateur de bureau</span><span class="sxs-lookup"><span data-stu-id="7ee63-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="7ee63-111">Le port 1433 est le seul port qui doit être ouvert sur votre ordinateur de bureau qui héberge votre application cliente SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7ee63-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="7ee63-112">*À l’intérieur :* le client s’exécute sur Azure</span><span class="sxs-lookup"><span data-stu-id="7ee63-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="7ee63-113">Quand votre client s’exécute à l’intérieur de la limite du cloud Azure, il utilise ce que nous pouvons appeler un *itinéraire direct* pour interagir avec le serveur de la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="7ee63-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="7ee63-114">Une fois une connexion établie, les interactions suivantes entre le client et la base de données n’impliquent aucun proxy d’intergiciel.</span><span class="sxs-lookup"><span data-stu-id="7ee63-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="7ee63-115">La séquence est la suivante :</span><span class="sxs-lookup"><span data-stu-id="7ee63-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="7ee63-116">ADO.NET 4.5 (ou version ultérieure) initie une brève interaction avec le cloud Azure et reçoit un numéro de port identifié de manière dynamique.</span><span class="sxs-lookup"><span data-stu-id="7ee63-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="7ee63-117">Le numéro de port identifié de manière dynamique appartient à la plage 11000-11999 ou 14000-14999.</span><span class="sxs-lookup"><span data-stu-id="7ee63-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="7ee63-118">ADO.NET se connecte ensuite au serveur SQL Database directement, sans passer par un intergiciel.</span><span class="sxs-lookup"><span data-stu-id="7ee63-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="7ee63-119">Les requêtes sont envoyées directement à la base de données et les résultats sont retournés directement au client.</span><span class="sxs-lookup"><span data-stu-id="7ee63-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="7ee63-120">Vérifiez que les plages de ports 11000-11999 et 14000-14999 sur votre ordinateur client Azure restent disponibles pour les interactions du client ADO.NET 4.5 avec SQL Database.</span><span class="sxs-lookup"><span data-stu-id="7ee63-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="7ee63-121">En particulier, les ports dans la plage doivent être libres de tout autre bloqueur sortant.</span><span class="sxs-lookup"><span data-stu-id="7ee63-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="7ee63-122">Sur votre machine virtuelle Azure, le **Pare-feu Windows avec fonctions avancées de sécurité** contrôle les paramètres des ports.</span><span class="sxs-lookup"><span data-stu-id="7ee63-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="7ee63-123">Vous pouvez utiliser [l’interface utilisateur du pare-feu](http://msdn.microsoft.com/library/cc646023.aspx) pour ajouter une règle dans laquelle vous spécifiez le protocole **TCP** et une plage de ports avec une syntaxe semblable à **11000-11999**.</span><span class="sxs-lookup"><span data-stu-id="7ee63-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="7ee63-124">Précisions concernant les versions</span><span class="sxs-lookup"><span data-stu-id="7ee63-124">Version clarifications</span></span>
<span data-ttu-id="7ee63-125">Cette section clarifie les monikers qui font référence aux versions du produit.</span><span class="sxs-lookup"><span data-stu-id="7ee63-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="7ee63-126">Elle répertorie également certaines paires de versions entre les produits.</span><span class="sxs-lookup"><span data-stu-id="7ee63-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="7ee63-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="7ee63-127">ADO.NET</span></span>
* <span data-ttu-id="7ee63-128">ADO.NET 4.0 prend en charge le protocole TDS 7.3, mais pas la version 7.4.</span><span class="sxs-lookup"><span data-stu-id="7ee63-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="7ee63-129">Les versions d’ADO.NET 4.5 et ultérieures prennent en charge le protocole TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="7ee63-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="7ee63-130">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="7ee63-130">Related links</span></span>
* <span data-ttu-id="7ee63-131">ADO.NET 4.6 a été publié le 20 juillet 2015.</span><span class="sxs-lookup"><span data-stu-id="7ee63-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="7ee63-132">Une annonce dans un billet de blog de l’équipe .NET est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ee63-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="7ee63-133">ADO.NET 4.5 a été publié le 15 août 2012.</span><span class="sxs-lookup"><span data-stu-id="7ee63-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="7ee63-134">Une annonce dans un billet de blog de l’équipe .NET est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ee63-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="7ee63-135">Un billet de blog sur ADO.NET 4.5.1 est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="7ee63-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="7ee63-136">Liste des versions du protocole TDS</span><span class="sxs-lookup"><span data-stu-id="7ee63-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="7ee63-137">Vue d’ensemble du développement de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="7ee63-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="7ee63-138">Pare-feu Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="7ee63-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="7ee63-139">Configuration des paramètres du pare-feu sur une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="7ee63-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

