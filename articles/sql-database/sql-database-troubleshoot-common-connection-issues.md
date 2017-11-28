---
title: "tooAzure de problèmes de connexion courantes aaaTroubleshoot base de données SQL"
description: "Étapes tooidentify et résoudre les connexions erreurs courantes pour la base de données SQL Azure."
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: ac463d1c-aec8-443d-b66e-fa5eadcccfa8
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: eb5f2d7b123a76942c7e4a84a7f475344fbcb144
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-connection-issues-tooazure-sql-database"></a><span data-ttu-id="03f7c-103">Résoudre les problèmes de connexion tooAzure de la base de données SQL</span><span class="sxs-lookup"><span data-stu-id="03f7c-103">Troubleshoot connection issues tooAzure SQL Database</span></span>
<span data-ttu-id="03f7c-104">En cas d’échec de la connexion de hello tooAzure base de données SQL, vous recevez [les messages d’erreur](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="03f7c-104">When hello connection tooAzure SQL Database fails, you receive [error messages](sql-database-develop-error-messages.md).</span></span> <span data-ttu-id="03f7c-105">Cet article est une rubrique centralisée qui vous permet de résoudre les problèmes de connectivité des bases de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="03f7c-105">This article is a centralized topic that helps you troubleshoot Azure SQL Database connectivity issues.</span></span> <span data-ttu-id="03f7c-106">Il introduit [hello des causes courantes](#cause) de problèmes de connexion, vous recommande de [un outil de dépannage](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) qui vous permet de problème de hello identité et fournit la résolution des problèmes étapes toosolve [ erreurs temporaires](#troubleshoot-transient-errors) et [erreurs persistants ou non temporaire](#troubleshoot-persistent-errors).</span><span class="sxs-lookup"><span data-stu-id="03f7c-106">It introduces [hello common causes](#cause) of connection issues, recommends [a troubleshooting tool](#try-the-troubleshooter-for-azure-sql-database-connectivity-issues) that helps you identity hello problem, and provides troubleshooting steps toosolve [transient errors](#troubleshoot-transient-errors) and [persistent or non-transient errors](#troubleshoot-persistent-errors).</span></span> 

<span data-ttu-id="03f7c-107">Si vous rencontrez des problèmes de connexion de hello, essayez de hello résoudre les étapes décrites dans cet article.</span><span class="sxs-lookup"><span data-stu-id="03f7c-107">If you encounter hello connection issues, try hello troubleshoot steps that are described in this article.</span></span>
[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="cause"></a><span data-ttu-id="03f7c-108">Cause :</span><span class="sxs-lookup"><span data-stu-id="03f7c-108">Cause</span></span>
<span data-ttu-id="03f7c-109">Problèmes de connexion peuvent être dû à un des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="03f7c-109">Connection problems may be caused by any of hello following:</span></span>

* <span data-ttu-id="03f7c-110">Échec tooapply meilleures pratiques et les règles de conception pendant le processus de conception d’application hello.</span><span class="sxs-lookup"><span data-stu-id="03f7c-110">Failure tooapply best practices and design guidelines during hello application design process.</span></span>  <span data-ttu-id="03f7c-111">Consultez [vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md) tooget a démarré.</span><span class="sxs-lookup"><span data-stu-id="03f7c-111">See [SQL Database Development Overview](sql-database-develop-overview.md) tooget started.</span></span>
* <span data-ttu-id="03f7c-112">Reconfiguration de la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="03f7c-112">Azure SQL Database reconfiguration</span></span>
* <span data-ttu-id="03f7c-113">Paramètres du pare-feu</span><span class="sxs-lookup"><span data-stu-id="03f7c-113">Firewall settings</span></span>
* <span data-ttu-id="03f7c-114">Expiration du délai de connexion</span><span class="sxs-lookup"><span data-stu-id="03f7c-114">Connection time-out</span></span>
* <span data-ttu-id="03f7c-115">Informations de connexion incorrectes</span><span class="sxs-lookup"><span data-stu-id="03f7c-115">Incorrect login information</span></span>
* <span data-ttu-id="03f7c-116">Dépassement de la limite maximale sur certaines ressources de la base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="03f7c-116">Maximum limit reached on some Azure SQL Database resources</span></span>

<span data-ttu-id="03f7c-117">En règle générale, tooAzure de problèmes de connexion de base de données SQL peut être classé comme suit :</span><span class="sxs-lookup"><span data-stu-id="03f7c-117">Generally, connection issues tooAzure SQL Database can be classified as follows:</span></span>

* [<span data-ttu-id="03f7c-118">Erreurs temporaires (de courte durée ou intermittentes)</span><span class="sxs-lookup"><span data-stu-id="03f7c-118">Transient errors (short-lived or intermittent)</span></span>](#troubleshoot-transient-errors)
* [<span data-ttu-id="03f7c-119">Erreurs persistantes ou non temporaires (erreurs qui se produisent régulièrement)</span><span class="sxs-lookup"><span data-stu-id="03f7c-119">Persistent or non-transient errors (errors that regularly recur)</span></span>](#troubleshoot-persistent-errors)

## <a name="try-hello-troubleshooter-for-azure-sql-database-connectivity-issues"></a><span data-ttu-id="03f7c-120">Essayez de résolution des problèmes hello pour les problèmes de connectivité de base de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="03f7c-120">Try hello troubleshooter for Azure SQL Database connectivity issues</span></span>
<span data-ttu-id="03f7c-121">Si vous rencontrez une erreur de connexion spécifique, essayez [cet outil](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), qui vous aidera à identifier et à résoudre rapidement votre problème.</span><span class="sxs-lookup"><span data-stu-id="03f7c-121">If you encounter a specific connection error, try [this tool](https://support.microsoft.com/help/10085/troubleshooting-connectivity-issues-with-microsoft-azure-sql-database), which will help you quickly identity and resolve your problem.</span></span>

## <a name="troubleshoot-transient-errors"></a><span data-ttu-id="03f7c-122">Résoudre les erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="03f7c-122">Troubleshoot transient errors</span></span>

<span data-ttu-id="03f7c-123">Lorsqu’une application connecte à base de données SQL Azure tooan, vous recevez hello message d’erreur suivant :</span><span class="sxs-lookup"><span data-stu-id="03f7c-123">When an application connects tooan Azure SQL database, you receive hello following error message:</span></span>

```
Error code 40613: "Database <x> on server <y> is not currently available. Please retry hello connection later. If hello problem persists, contact customer support, and provide them hello session tracing ID of <z>"
```

> [!NOTE]
> <span data-ttu-id="03f7c-124">Ce message d’erreur est généralement temporaire (de courte durée).</span><span class="sxs-lookup"><span data-stu-id="03f7c-124">This error message is typically transient (short-lived).</span></span>
> 
> 

<span data-ttu-id="03f7c-125">Cette erreur se produit lorsque hello est en cours d’une base de données Azure déplacé (ou reconfiguré) et votre application perd sa base de données SQL de connexion toohello.</span><span class="sxs-lookup"><span data-stu-id="03f7c-125">This error occurs when hello Azure database is being moved (or reconfigured) and your application loses its connection toohello SQL database.</span></span> <span data-ttu-id="03f7c-126">Les événements de reconfiguration de la base de données SQL sont liés à un événement planifié (par exemple, une mise à niveau logicielle) ou à un événement non planifié (par exemple, un arrêt de processus ou un équilibrage de charge).</span><span class="sxs-lookup"><span data-stu-id="03f7c-126">SQL database reconfiguration events occur because of a planned event (for example, a software upgrade) or an unplanned event (for example, a process crash, or load balancing).</span></span> <span data-ttu-id="03f7c-127">La plupart des événements de reconfiguration sont généralement de courte durée et se terminent en l’espace de 60 secondes maximum.</span><span class="sxs-lookup"><span data-stu-id="03f7c-127">Most reconfiguration events are generally short-lived and should be completed in less than 60 seconds at most.</span></span> <span data-ttu-id="03f7c-128">Toutefois, ces événements peuvent s’occasionnellement toofinish plus de temps, telles que lorsqu’une transaction de grande taille entraîne une récupération à long terme.</span><span class="sxs-lookup"><span data-stu-id="03f7c-128">However, these events can occasionally take longer toofinish, such as when a large transaction causes a long-running recovery.</span></span>

### <a name="steps-tooresolve-transient-connectivity-issues"></a><span data-ttu-id="03f7c-129">Problèmes de connectivité temporaire tooresolve étapes</span><span class="sxs-lookup"><span data-stu-id="03f7c-129">Steps tooresolve transient connectivity issues</span></span>

1. <span data-ttu-id="03f7c-130">Vérifiez hello [tableau de bord de Service Microsoft Azure](https://azure.microsoft.com/status) pour toutes les interruptions connues qui s’est produite pendant le temps de hello pendant le hello les erreurs sont signalées par l’application hello.</span><span class="sxs-lookup"><span data-stu-id="03f7c-130">Check hello [Microsoft Azure Service Dashboard](https://azure.microsoft.com/status) for any known outages that occurred during hello time during which hello errors were reported by hello application.</span></span>
2. <span data-ttu-id="03f7c-131">Applications qui se connectent tooa le service cloud, telles que la base de données SQL Azure doit attendre les événements de reconfiguration périodiques et implémenter recommencez logique toohandle ces erreurs au lieu des surfaces d’en tant qu’application erreurs toousers.</span><span class="sxs-lookup"><span data-stu-id="03f7c-131">Applications that connect tooa cloud service such as Azure SQL Database should expect periodic reconfiguration events and implement retry logic toohandle these errors instead of surfacing these as application errors toousers.</span></span> <span data-ttu-id="03f7c-132">Hello de révision [erreurs temporaires](sql-database-connectivity-issues.md) hello section meilleures pratiques et concevoir des instructions à [vue d’ensemble du développement de base de données SQL](sql-database-develop-overview.md) pour plus d’informations générales des stratégies de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="03f7c-132">Review hello [Transient errors](sql-database-connectivity-issues.md) section and hello best practices and design guidelines at [SQL Database Development Overview](sql-database-develop-overview.md) for more information and general retry strategies.</span></span> <span data-ttu-id="03f7c-133">Passez ensuite en revue les exemples de code dans l’article [Bibliothèques de connexions pour SQL Database et SQL Server](sql-database-libraries.md) pour obtenir des informations spécifiques.</span><span class="sxs-lookup"><span data-stu-id="03f7c-133">Then, see code samples at [Connection Libraries for SQL Database and SQL Server](sql-database-libraries.md) for specifics.</span></span>
3. <span data-ttu-id="03f7c-134">Une base de données approche de ses limites de ressources, il peut sembler toobe un problème de connectivité temporaire.</span><span class="sxs-lookup"><span data-stu-id="03f7c-134">As a database approaches its resource limits, it can seem toobe a transient connectivity issue.</span></span> <span data-ttu-id="03f7c-135">Consultez la page [Résolution des problèmes de performances](sql-database-troubleshoot-performance.md).</span><span class="sxs-lookup"><span data-stu-id="03f7c-135">See [Troubleshooting Performance Issues](sql-database-troubleshoot-performance.md).</span></span>
4. <span data-ttu-id="03f7c-136">Si des problèmes de connectivité se poursuivre, ou si hello durée pour laquelle votre application rencontre des erreurs de hello dépasse 60 secondes ou si vous voyez plusieurs occurrences de l’erreur de hello dans un jour donné, une demande de support Azure de fichiers en sélectionnant **obtenir prend en charge les** sur hello [prise en charge Azure](https://azure.microsoft.com/support/options) site.</span><span class="sxs-lookup"><span data-stu-id="03f7c-136">If connectivity problems continue, or if hello duration for which your application encounters hello error exceeds 60 seconds or if you see multiple occurrences of hello error in a given day, file an Azure support request by selecting **Get Support** on hello [Azure Support](https://azure.microsoft.com/support/options) site.</span></span>

## <a name="troubleshoot-persistent-errors"></a><span data-ttu-id="03f7c-137">Résoudre les erreurs persistantes</span><span class="sxs-lookup"><span data-stu-id="03f7c-137">Troubleshoot persistent errors</span></span>
<span data-ttu-id="03f7c-138">En cas d’application hello persistante tooconnect tooAzure base de données SQL, il indique généralement un problème avec l’un des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="03f7c-138">If hello application persistently fails tooconnect tooAzure SQL Database, it usually indicates an issue with one of hello following:</span></span>

* <span data-ttu-id="03f7c-139">Configuration du pare-feu.</span><span class="sxs-lookup"><span data-stu-id="03f7c-139">Firewall configuration.</span></span> <span data-ttu-id="03f7c-140">pare-feu de base de données ou côté client de SQL Azure Hello bloque les connexions tooAzure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="03f7c-140">hello Azure SQL database or client-side firewall is blocking connections tooAzure SQL Database.</span></span>
* <span data-ttu-id="03f7c-141">Réseau de reconfiguration côté client de hello : par exemple, une nouvelle adresse IP ou un serveur proxy.</span><span class="sxs-lookup"><span data-stu-id="03f7c-141">Network reconfiguration on hello client side: for example, a new IP address or a proxy server.</span></span>
* <span data-ttu-id="03f7c-142">Erreur de l’utilisateur : par exemple, saisi correctement les paramètres de connexion, telles que le nom de serveur hello dans la chaîne de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="03f7c-142">User error: for example, mistyped connection parameters, such as hello server name in hello connection string.</span></span>

### <a name="steps-tooresolve-persistent-connectivity-issues"></a><span data-ttu-id="03f7c-143">Problèmes de connectivité persistant tooresolve étapes</span><span class="sxs-lookup"><span data-stu-id="03f7c-143">Steps tooresolve persistent connectivity issues</span></span>
1. <span data-ttu-id="03f7c-144">Configurer [des règles de pare-feu](sql-database-configure-firewall-settings.md) tooallow adresse IP client en hello.</span><span class="sxs-lookup"><span data-stu-id="03f7c-144">Set up [firewall rules](sql-database-configure-firewall-settings.md) tooallow hello client IP address.</span></span> <span data-ttu-id="03f7c-145">Pour des raisons de tests temporaires, définir une règle de pare-feu à l’aide de 0.0.0.0 comme hello plage d’adresses IP de début et à l’aide de 255.255.255.255 comme hello fin de la plage d’adresses IP.</span><span class="sxs-lookup"><span data-stu-id="03f7c-145">For temporary testing purposes, set up a firewall rule using 0.0.0.0 as hello starting IP address range and using 255.255.255.255 as hello ending IP address range.</span></span> <span data-ttu-id="03f7c-146">Adresses IP tooall hello s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="03f7c-146">This will open hello server tooall IP addresses.</span></span> <span data-ttu-id="03f7c-147">Si elle résout votre problème de connectivité, supprimez cette règle et créez une règle de pare-feu pour une adresse ou une plage d’adresses IP correctement bornée.</span><span class="sxs-lookup"><span data-stu-id="03f7c-147">If this resolves your connectivity issue, remove this rule and create a firewall rule for an appropriately limited IP address or address range.</span></span> 
2. <span data-ttu-id="03f7c-148">Sur tous les pare-feu entre le client de hello et hello Internet, assurez-vous que le port 1433 est ouvert pour les connexions sortantes.</span><span class="sxs-lookup"><span data-stu-id="03f7c-148">On all firewalls between hello client and hello Internet, make sure that port 1433 is open for outbound connections.</span></span> <span data-ttu-id="03f7c-149">Révision [configurer le pare-feu Windows de hello tooAllow accès à SQL Server](https://msdn.microsoft.com/library/cc646023.aspx) et [hybride identité requis Ports et protocoles](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) des pointeurs supplémentaires liés tooadditional ports que vous avez besoin de tooopen pour Authentification Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="03f7c-149">Review [Configure hello Windows Firewall tooAllow SQL Server Access](https://msdn.microsoft.com/library/cc646023.aspx) and [Hybrid Identity Required Ports and Protocols](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect-ports) for additional pointers related tooadditional ports that you need tooopen for Azure Active Directory authentication.</span></span>
3. <span data-ttu-id="03f7c-150">Vérifiez votre chaîne de connexion et d’autres paramètres de connexion.</span><span class="sxs-lookup"><span data-stu-id="03f7c-150">Verify your connection string and other connection settings.</span></span> <span data-ttu-id="03f7c-151">Consultez hello section de chaîne de connexion dans hello [rubrique des problèmes de connectivité](sql-database-connectivity-issues.md#connections-to-azure-sql-database).</span><span class="sxs-lookup"><span data-stu-id="03f7c-151">See hello Connection String section in hello [connectivity issues topic](sql-database-connectivity-issues.md#connections-to-azure-sql-database).</span></span>
4. <span data-ttu-id="03f7c-152">Vérifiez l’intégrité du service dans le tableau de bord hello.</span><span class="sxs-lookup"><span data-stu-id="03f7c-152">Check service health in hello dashboard.</span></span> <span data-ttu-id="03f7c-153">Si vous pensez qu’une panne régionale, consultez [récupérer à partir d’une panne](sql-database-disaster-recovery.md) pour une nouvelle région étapes toorecover tooa.</span><span class="sxs-lookup"><span data-stu-id="03f7c-153">If you think there’s a regional outage, see [Recover from an outage](sql-database-disaster-recovery.md) for steps toorecover tooa new region.</span></span>

## <a name="next-steps"></a><span data-ttu-id="03f7c-154">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="03f7c-154">Next steps</span></span>
* [<span data-ttu-id="03f7c-155">Résoudre les problèmes de performances des bases de données SQL Azure</span><span class="sxs-lookup"><span data-stu-id="03f7c-155">Troubleshoot Azure SQL Database performance issues</span></span>](sql-database-troubleshoot-performance.md)
* [<span data-ttu-id="03f7c-156">Documentation de hello Search sur Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="03f7c-156">Search hello documentation on Microsoft Azure</span></span>](http://azure.microsoft.com/search/documentation/)
* [<span data-ttu-id="03f7c-157">Hello d’affichage des dernières mises à jour de service de base de données SQL Azure toohello</span><span class="sxs-lookup"><span data-stu-id="03f7c-157">View hello latest updates toohello Azure SQL Database service</span></span>](http://azure.microsoft.com/updates/?service=sql-database)

## <a name="additional-resources"></a><span data-ttu-id="03f7c-158">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="03f7c-158">Additional resources</span></span>
* [<span data-ttu-id="03f7c-159">Vue d’ensemble du développement de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="03f7c-159">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="03f7c-160">Aide générale sur le traitement des erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="03f7c-160">General transient fault-handling guidance</span></span>](../best-practices-retry-general.md)
* [<span data-ttu-id="03f7c-161">Bibliothèques de connexions pour SQL Database et SQL Server</span><span class="sxs-lookup"><span data-stu-id="03f7c-161">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)
