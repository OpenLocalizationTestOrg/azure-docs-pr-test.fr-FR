---
title: "aaaPorts au-delà de 1433 pour la base de données SQL | Documents Microsoft"
description: "Parfois, les connexions client à partir d’ADO.NET tooAzure base de données SQL ignorer hello proxy et interagissent directement avec la base de données hello. Les ports autres que le port 1433 deviennent importants."
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="ede47-104">Ports au-delà de 1433 pour ADO.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ede47-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="ede47-105">Cette rubrique décrit le comportement de connexion de base de données SQL Azure hello pour les clients qui utilisent ADO.NET 4.5 ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ede47-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ede47-106">Pour plus d’informations sur l’architecture de connectivité, consultez [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md) (Architecture de connectivité d’Azure SQL Database).</span><span class="sxs-lookup"><span data-stu-id="ede47-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="ede47-107">À l’extérieur et à l’intérieur</span><span class="sxs-lookup"><span data-stu-id="ede47-107">Outside vs inside</span></span>
<span data-ttu-id="ede47-108">Pour les connexions tooAzure base de données SQL, nous devons tout d’abord demander si votre programme client s’exécute *en dehors de* ou *à l’intérieur de* limite de cloud computing Azure hello.</span><span class="sxs-lookup"><span data-stu-id="ede47-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="ede47-109">les sous-sections Hello présentent deux scénarios courants.</span><span class="sxs-lookup"><span data-stu-id="ede47-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="ede47-110">*À l’extérieur :* le client s’exécute sur votre ordinateur de bureau</span><span class="sxs-lookup"><span data-stu-id="ede47-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="ede47-111">Le port 1433 est hello seul le port qui doit être ouvert sur votre ordinateur de bureau qui héberge votre application cliente de base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="ede47-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="ede47-112">*À l’intérieur :* le client s’exécute sur Azure</span><span class="sxs-lookup"><span data-stu-id="ede47-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="ede47-113">Lorsque votre client s’exécute à l’intérieur des limites de cloud computing Azure hello, il utilise ce que nous pouvons appeler un *itinéraire direct* toointeract avec le serveur de base de données SQL hello.</span><span class="sxs-lookup"><span data-stu-id="ede47-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="ede47-114">Une fois une connexion est établie, d’autres interactions entre le client de hello et la base de données n’impliquent aucun proxy de l’intergiciel (middleware).</span><span class="sxs-lookup"><span data-stu-id="ede47-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="ede47-115">séquence de Hello est comme suit :</span><span class="sxs-lookup"><span data-stu-id="ede47-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="ede47-116">ADO.NET 4.5 (ou version ultérieure) initie une interaction brève avec hello cloud Azure et reçoit un numéro de port identifié de manière dynamique.</span><span class="sxs-lookup"><span data-stu-id="ede47-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="ede47-117">numéro de port Hello identifié de manière dynamique est hello de 11000-11999 ou 14000-14999.</span><span class="sxs-lookup"><span data-stu-id="ede47-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="ede47-118">ADO.NET se connecte ensuite serveur de base de données SQL toohello directement avec aucun intergiciel (middleware) entre les deux.</span><span class="sxs-lookup"><span data-stu-id="ede47-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="ede47-119">Les requêtes sont envoyées directement toohello de base de données, et les résultats sont retournés directement toohello client.</span><span class="sxs-lookup"><span data-stu-id="ede47-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="ede47-120">Vérifiez que ce port hello plages de 11000-11999 et 14000-14999 sur votre ordinateur client Azure restent disponibles pour les interactions du client ADO.NET 4.5 avec la base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="ede47-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="ede47-121">En particulier, les ports dans la plage de hello doivent être de n’importe quel autre bloqueur sortant.</span><span class="sxs-lookup"><span data-stu-id="ede47-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="ede47-122">Sur votre machine virtuelle Azure, hello **pare-feu Windows avec fonctions avancées de sécurité** contrôles hello des paramètres de port.</span><span class="sxs-lookup"><span data-stu-id="ede47-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="ede47-123">Vous pouvez utiliser hello [interface utilisateur du pare-feu](http://msdn.microsoft.com/library/cc646023.aspx) tooadd une règle pour lesquels vous spécifiez hello **TCP** telles que le protocole ainsi que d’une plage de ports avec la syntaxe hello **11000-11999**.</span><span class="sxs-lookup"><span data-stu-id="ede47-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="ede47-124">Précisions concernant les versions</span><span class="sxs-lookup"><span data-stu-id="ede47-124">Version clarifications</span></span>
<span data-ttu-id="ede47-125">Cette section clarifie les monikers hello qui font référence à des versions tooproduct.</span><span class="sxs-lookup"><span data-stu-id="ede47-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="ede47-126">Elle répertorie également certaines paires de versions entre les produits.</span><span class="sxs-lookup"><span data-stu-id="ede47-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="ede47-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="ede47-127">ADO.NET</span></span>
* <span data-ttu-id="ede47-128">ADO.NET 4.0 prend en charge le protocole de hello TDS 7.3, mais pas 7.4.</span><span class="sxs-lookup"><span data-stu-id="ede47-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="ede47-129">ADO.NET 4.5 et versions ultérieures prend en charge le protocole de hello TDS 7.4.</span><span class="sxs-lookup"><span data-stu-id="ede47-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="ede47-130">Liens connexes</span><span class="sxs-lookup"><span data-stu-id="ede47-130">Related links</span></span>
* <span data-ttu-id="ede47-131">ADO.NET 4.6 a été publié le 20 juillet 2015.</span><span class="sxs-lookup"><span data-stu-id="ede47-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="ede47-132">Annonce de blog à partir de l’équipe de .NET hello est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span><span class="sxs-lookup"><span data-stu-id="ede47-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="ede47-133">ADO.NET 4.5 a été publié le 15 août 2012.</span><span class="sxs-lookup"><span data-stu-id="ede47-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="ede47-134">Annonce de blog à partir de l’équipe de .NET hello est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span><span class="sxs-lookup"><span data-stu-id="ede47-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="ede47-135">Un billet de blog sur ADO.NET 4.5.1 est disponible [ici](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span><span class="sxs-lookup"><span data-stu-id="ede47-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="ede47-136">Liste des versions du protocole TDS</span><span class="sxs-lookup"><span data-stu-id="ede47-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="ede47-137">Vue d’ensemble du développement de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="ede47-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="ede47-138">Pare-feu Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="ede47-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="ede47-139">Configuration des paramètres du pare-feu sur une base de données SQL</span><span class="sxs-lookup"><span data-stu-id="ede47-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

