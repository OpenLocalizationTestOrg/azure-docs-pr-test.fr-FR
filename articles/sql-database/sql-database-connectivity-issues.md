---
title: "Corriger une erreur de connexion SQL, erreur temporaire | Microsoft Docs"
description: "Découvrez comment diagnostiquer, résoudre et empêcher une erreur de connexion SQL ou une erreur temporaire dans Base de données SQL Azure. "
keywords: "connexion SQL,chaîne de connexion,problèmes de connectivité,erreur temporaire,erreur de connexion"
services: sql-database
documentationcenter: 
author: dalechen
manager: cshepard
editor: 
ms.assetid: efb35451-3fed-4264-bf86-72b350f67d50
ms.service: sql-database
ms.custom: develop apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: daleche
ms.openlocfilehash: ae081fc0432e36bf9f4d4f06f289386ddce37990
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="a6dea-104">Diagnostiquer, résoudre et empêcher les erreurs de connexion SQL et les erreurs temporaires de Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="a6dea-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="a6dea-105">Cet article décrit comment empêcher, résoudre, diagnostiquer et limiter les erreurs de connexion et les erreurs temporaires que votre application cliente rencontre lorsqu’elle interagit avec Base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a6dea-105">This article describes how to prevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="a6dea-106">Découvrez comment configurer une logique de nouvelle tentative, générer la chaîne de connexion et ajuster les autres paramètres de connexion.</span><span class="sxs-lookup"><span data-stu-id="a6dea-106">Learn how to configure retry logic, build the connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="a6dea-107">Erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="a6dea-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="a6dea-108">Une erreur temporaire s’explique par une cause sous-jacente qui se résout d’elle-même en peu de temps.</span><span class="sxs-lookup"><span data-stu-id="a6dea-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="a6dea-109">Les erreurs temporaires surviennent de temps en temps lorsque le système Azure réaffecte rapidement des ressources matérielles pour mieux équilibrer les différentes charges de travail.</span><span class="sxs-lookup"><span data-stu-id="a6dea-109">An occasional cause of transient errors is when the Azure system quickly shifts hardware resources to better load-balance various workloads.</span></span> <span data-ttu-id="a6dea-110">La plupart de ces événements de reconfiguration se terminent souvent en moins de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="a6dea-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="a6dea-111">Durant cette reconfiguration, vous pouvez connaître des problèmes de connectivité avec Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a6dea-111">During this reconfiguration time span, you may have connectivity issues to Azure SQL Database.</span></span> <span data-ttu-id="a6dea-112">Les applications se connectant à Azure SQL Database doivent pouvoir tenir compte de ces erreurs temporaires, et les gérer en implémentant une logique de nouvelle tentative dans leur code au lieu de les exposer aux utilisateurs en cas d'erreurs d'application.</span><span class="sxs-lookup"><span data-stu-id="a6dea-112">Applications connecting to Azure SQL Database should be built to expect these transient errors, handle them by implementing retry logic in their code instead of surfacing them to users as application errors.</span></span>

<span data-ttu-id="a6dea-113">Si votre programme client utilise ADO.NET, votre programme est informé de l’erreur temporaire par la levée d’une exception **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="a6dea-113">If your client program is using ADO.NET, your program is told about the transient error by the throw of an **SqlException**.</span></span> <span data-ttu-id="a6dea-114">La propriété **Number** peut être comparée à la liste des erreurs temporaires au début de la rubrique : [Codes d’erreur SQL pour les applications clientes SQL Database](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="a6dea-114">The **Number** property can be compared against the list of transient errors near the top of the topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="a6dea-115">Connexion ou commande</span><span class="sxs-lookup"><span data-stu-id="a6dea-115">Connection versus command</span></span>
<span data-ttu-id="a6dea-116">Vous allez réessayer la connexion SQL ou la rétablir, en fonction de ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="a6dea-116">You'll retry the SQL connection or establish it again, depending on the following:</span></span>

* <span data-ttu-id="a6dea-117">**Une erreur temporaire survient pendant une tentative de connexion**: la connexion doit être retentée après un délai de quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="a6dea-117">**A transient error occurs during a connection try**: The connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="a6dea-118">**Une erreur temporaire se produit pendant une commande de requête SQL** : cette dernière ne doit pas être retentée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="a6dea-118">**A transient error occurs during a SQL query command**: The command should not be immediately retried.</span></span> <span data-ttu-id="a6dea-119">Au lieu de cela, après qu’un certain délai se soit écoulé, la connexion doit être établie.</span><span class="sxs-lookup"><span data-stu-id="a6dea-119">Instead, after a delay, the connection should be freshly established.</span></span> <span data-ttu-id="a6dea-120">Ensuite, la commande peut être relancée.</span><span class="sxs-lookup"><span data-stu-id="a6dea-120">Then the command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="a6dea-121">Logique de nouvelle tentative pour les erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="a6dea-121">Retry logic for transient errors</span></span>
<span data-ttu-id="a6dea-122">Les programmes clients qui rencontrent occasionnellement une erreur temporaire sont plus solides lorsqu’ils contiennent une logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="a6dea-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="a6dea-123">Si votre programme communique avec Azure SQL Database via un intergiciel (middleware) tiers, renseignez-vous auprès du fournisseur pour savoir s’il contient une logique de nouvelle tentative pour les erreurs temporaires.</span><span class="sxs-lookup"><span data-stu-id="a6dea-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with the vendor whether the middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="a6dea-124">Principes de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="a6dea-124">Principles for retry</span></span>
* <span data-ttu-id="a6dea-125">Une tentative d’ouverture de connexion doit être renouvelée si l’erreur est temporaire.</span><span class="sxs-lookup"><span data-stu-id="a6dea-125">An attempt to open a connection should be retried if the error is transient.</span></span>
* <span data-ttu-id="a6dea-126">Une instruction SQL SELECT qui échoue avec une erreur temporaire ne doit pas être retentée directement.</span><span class="sxs-lookup"><span data-stu-id="a6dea-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="a6dea-127">Au lieu de cela, établir une nouvelle connexion et relancer l’instruction SELECT.</span><span class="sxs-lookup"><span data-stu-id="a6dea-127">Instead, establish a fresh connection, and then retry the SELECT.</span></span>
* <span data-ttu-id="a6dea-128">Si une instruction SQL UPDATE échoue avec une erreur temporaire, une nouvelle connexion doit être établie avant que l’instruction UPDATE ne soit retentée.</span><span class="sxs-lookup"><span data-stu-id="a6dea-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before the UPDATE is retried.</span></span>
  
  * <span data-ttu-id="a6dea-129">La logique de nouvelle tentative doit s’assurer que la transaction de base de données est complètement terminée ou que la transaction a été annulée.</span><span class="sxs-lookup"><span data-stu-id="a6dea-129">The retry logic must ensure that either the entire database transaction completed, or that the entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="a6dea-130">Autres considérations</span><span class="sxs-lookup"><span data-stu-id="a6dea-130">Other considerations for retry</span></span>
* <span data-ttu-id="a6dea-131">Un programme de commandes démarré automatiquement après les heures de travail et qui s’achève avant le matin peut être très patient entre deux tentatives.</span><span class="sxs-lookup"><span data-stu-id="a6dea-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford to very patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="a6dea-132">Un programme d’interface utilisateur doit prendre en compte la tendance qu’ont les hommes à l’abandon en cas d’attente trop longue.</span><span class="sxs-lookup"><span data-stu-id="a6dea-132">A user interface program should account for the human tendency to give up after too long a wait.</span></span>
  
  * <span data-ttu-id="a6dea-133">Toutefois, la solution ne consiste pas à retenter l’opération à chaque seconde, car une telle stratégie pourrait submerger le système de requêtes.</span><span class="sxs-lookup"><span data-stu-id="a6dea-133">However, the solution must not be to retry every few seconds, because that policy can flood the system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="a6dea-134">Augmentation de l’intervalle entre les tentatives</span><span class="sxs-lookup"><span data-stu-id="a6dea-134">Interval increase between retries</span></span>
<span data-ttu-id="a6dea-135">Nous vous recommandons de patienter 5 secondes avant votre première tentative.</span><span class="sxs-lookup"><span data-stu-id="a6dea-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="a6dea-136">Si vous effectuez une nouvelle tentative avant 5 secondes, vous risquez de submerger le service cloud.</span><span class="sxs-lookup"><span data-stu-id="a6dea-136">Retrying after a delay shorter than 5 seconds risks overwhelming the cloud service.</span></span> <span data-ttu-id="a6dea-137">Pour chaque nouvelle tentative, le délai doit augmenter de manière exponentielle, sans dépasser 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="a6dea-137">For each subsequent retry the delay should grow exponentially, up to a maximum of 60 seconds.</span></span>

<span data-ttu-id="a6dea-138">Pour en savoir plus sur la *période de blocage* des clients qui utilisent ADO.NET, consultez la page [Regroupement de connexions SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6dea-138">A discussion of the *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="a6dea-139">Vous pouvez également définir le nombre maximal de tentatives avant l’arrêt automatique du programme.</span><span class="sxs-lookup"><span data-stu-id="a6dea-139">You might also want to set a maximum number of retries before the program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="a6dea-140">Exemples de code avec la logique de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="a6dea-140">Code samples with retry logic</span></span>
<span data-ttu-id="a6dea-141">Vous trouverez des exemples de code avec logique de nouvelle tentative dans divers langages de programmation ici :</span><span class="sxs-lookup"><span data-stu-id="a6dea-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="a6dea-142">Bibliothèques de connexions pour SQL Database et SQL Server</span><span class="sxs-lookup"><span data-stu-id="a6dea-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="a6dea-143">Tester votre logique de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="a6dea-143">Test your retry logic</span></span>
<span data-ttu-id="a6dea-144">Pour tester la logique de nouvelle tentative, vous devez simuler ou provoquer une erreur pouvant être corrigée alors que votre programme est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="a6dea-144">To test your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-the-network"></a><span data-ttu-id="a6dea-145">Test par le biais de la déconnexion du réseau</span><span class="sxs-lookup"><span data-stu-id="a6dea-145">Test by disconnecting from the network</span></span>
<span data-ttu-id="a6dea-146">Pour tester votre logique de nouvelle tentative, vous pouvez déconnecter votre ordinateur client du réseau pendant l’exécution du programme.</span><span class="sxs-lookup"><span data-stu-id="a6dea-146">One way you can test your retry logic is to disconnect your client computer from the network while the program is running.</span></span> <span data-ttu-id="a6dea-147">Vous obtiendrez l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="a6dea-147">The error will be:</span></span>

* <span data-ttu-id="a6dea-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="a6dea-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="a6dea-149">Message : « Hôte inconnu »</span><span class="sxs-lookup"><span data-stu-id="a6dea-149">Message: "No such host is known"</span></span>

<span data-ttu-id="a6dea-150">Dans le cadre de la première nouvelle tentative, votre programme peut corriger les fautes d’orthographe et tenter de se connecter.</span><span class="sxs-lookup"><span data-stu-id="a6dea-150">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="a6dea-151">Pour concrétiser cela, vous pouvez débrancher votre ordinateur du réseau avant lancer votre programme.</span><span class="sxs-lookup"><span data-stu-id="a6dea-151">To make this practical, you unplug your computer from the network before you start your program.</span></span> <span data-ttu-id="a6dea-152">Votre programme reconnaît alors un paramètre d’exécution qui fait en sorte que le programme :</span><span class="sxs-lookup"><span data-stu-id="a6dea-152">Then your program recognizes a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="a6dea-153">Ajoute temporairement 11001 à sa liste d’erreurs à considérer comme provisoire.</span><span class="sxs-lookup"><span data-stu-id="a6dea-153">Temporarily add 11001 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="a6dea-154">Tente sa première connexion comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="a6dea-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="a6dea-155">Une fois l’erreur détectée, supprime 11001 de sa liste.</span><span class="sxs-lookup"><span data-stu-id="a6dea-155">After the error is caught, remove 11001 from the list.</span></span>
4. <span data-ttu-id="a6dea-156">Affiche un message indiquant à l’utilisateur de connecter l’ordinateur au réseau.</span><span class="sxs-lookup"><span data-stu-id="a6dea-156">Display a message telling the user to plug the computer into the network.</span></span>
   * <span data-ttu-id="a6dea-157">Suspend toute exécution à l’aide de la méthode **Console.ReadLine** ou d’une boîte de dialogue contenant un bouton OK.</span><span class="sxs-lookup"><span data-stu-id="a6dea-157">Pause further execution by using either the **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="a6dea-158">L’utilisateur appuie sur la touche Entrée après la connexion de l’ordinateur au réseau.</span><span class="sxs-lookup"><span data-stu-id="a6dea-158">The user presses the Enter key after the computer plugged into the network.</span></span>
5. <span data-ttu-id="a6dea-159">Essaie de nouveau de se connecter, et attend la réussite.</span><span class="sxs-lookup"><span data-stu-id="a6dea-159">Attempt again to connect, expecting success.</span></span>

##### <a name="test-by-misspelling-the-database-name-when-connecting"></a><span data-ttu-id="a6dea-160">Teste en fournissant un nom de base de données mal orthographié au moment de la connexion</span><span class="sxs-lookup"><span data-stu-id="a6dea-160">Test by misspelling the database name when connecting</span></span>
<span data-ttu-id="a6dea-161">Votre programme peut délibérément mal orthographier le nom d’utilisateur avant la première tentative de connexion.</span><span class="sxs-lookup"><span data-stu-id="a6dea-161">Your program can purposely misspell the user name before the first connection attempt.</span></span> <span data-ttu-id="a6dea-162">Vous obtiendrez l’erreur suivante :</span><span class="sxs-lookup"><span data-stu-id="a6dea-162">The error will be:</span></span>

* <span data-ttu-id="a6dea-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="a6dea-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="a6dea-164">Message : « Échec de la connexion pour l’utilisateur 'WRONG_MyUserName' »</span><span class="sxs-lookup"><span data-stu-id="a6dea-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="a6dea-165">Dans le cadre de la première nouvelle tentative, votre programme peut corriger les fautes d’orthographe et tenter de se connecter.</span><span class="sxs-lookup"><span data-stu-id="a6dea-165">As part of the first retry attempt, your program can correct the misspelling, and then attempt to connect.</span></span>

<span data-ttu-id="a6dea-166">Pour mettre cela en pratique, votre programme peut reconnaître un paramètre d’exécution, qui fait en sorte que le programme :</span><span class="sxs-lookup"><span data-stu-id="a6dea-166">To make this practical, your program could recognize a run time parameter that causes the program to:</span></span>

1. <span data-ttu-id="a6dea-167">Ajoute temporairement 18456 à sa liste d’erreurs à prendre en compte comme provisoire.</span><span class="sxs-lookup"><span data-stu-id="a6dea-167">Temporarily add 18456 to its list of errors to consider as transient.</span></span>
2. <span data-ttu-id="a6dea-168">Ajoute volontairement ’WRONG_’ au nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6dea-168">Purposely add 'WRONG_' to the user name.</span></span>
3. <span data-ttu-id="a6dea-169">Une fois l’erreur détectée, supprime 18456 de la liste.</span><span class="sxs-lookup"><span data-stu-id="a6dea-169">After the error is caught, remove 18456 from the list.</span></span>
4. <span data-ttu-id="a6dea-170">Supprime ’WRONG_’ du nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="a6dea-170">Remove 'WRONG_' from the user name.</span></span>
5. <span data-ttu-id="a6dea-171">Essaie de nouveau de se connecter, et attend la réussite.</span><span class="sxs-lookup"><span data-stu-id="a6dea-171">Attempt again to connect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="a6dea-172">Paramètres de connexion .NET Sql pour les nouvelles tentatives de connexion</span><span class="sxs-lookup"><span data-stu-id="a6dea-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="a6dea-173">Si votre programme client se connecte à Azure SQL Database à l’aide de la classe .NET Framework **System.Data.SqlClient.SqlConnection**, vous devez utiliser .NET 4.6.1 ou une version ultérieure (ou .NET Core) afin de pouvoir tirer parti de la fonctionnalité de nouvelle tentative de connexion.</span><span class="sxs-lookup"><span data-stu-id="a6dea-173">If your client program connects to to Azure SQL Database by using the .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="a6dea-174">Les détails de la fonctionnalité sont disponibles [ici](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="a6dea-174">Details of the feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points to dn632678.aspx, which links to a downloadable .docx related to SqlClient and SQL Server 2014.
-->


<span data-ttu-id="a6dea-175">Lorsque vous générez la [chaîne de connexion](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) pour votre objet **SqlConnection** , vous devez coordonner les valeurs entre les paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="a6dea-175">When you build the [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate the values among the following parameters:</span></span>

* <span data-ttu-id="a6dea-176">ConnectRetryCount &nbsp;&nbsp;*(La valeur par défaut est 1. La plage s’étend de 0 à 255.)*</span><span class="sxs-lookup"><span data-stu-id="a6dea-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="a6dea-177">ConnectRetryInterval &nbsp;&nbsp;*(La valeur par défaut est 1 seconde. La plage s’étend de 1 à 60.)*</span><span class="sxs-lookup"><span data-stu-id="a6dea-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="a6dea-178">Délai d’expiration de connexion &nbsp;&nbsp;*(La valeur par défaut est 15 secondes. La plage s’étend de 0 à 2147483647.)*</span><span class="sxs-lookup"><span data-stu-id="a6dea-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="a6dea-179">Plus précisément, les valeurs que vous choisissez doivent vérifier la formule suivante :</span><span class="sxs-lookup"><span data-stu-id="a6dea-179">Specifically, your chosen values should make the following equality true:</span></span>

* <span data-ttu-id="a6dea-180">Délai d’expiration de connexion = ConnectRetryCount × ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="a6dea-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="a6dea-181">Par exemple, si ConnectRetryCount = 3 et ConnectionRetryInterval = 10 secondes, un délai d’expiration de 29 secondes seulement ne laissera pas suffisamment de temps au système pour sa 3e et dernière tentative de connexion, 29 étant inférieur à 3 × 10.</span><span class="sxs-lookup"><span data-stu-id="a6dea-181">For example, if the count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give the system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="a6dea-182">Connexion ou commande</span><span class="sxs-lookup"><span data-stu-id="a6dea-182">Connection versus command</span></span>
<span data-ttu-id="a6dea-183">Les paramètres **ConnectRetryCount** et **ConnectRetryInterval** permettent à votre objet **SqlConnection** de recommencer l’opération de connexion sans notification à votre programme ou renvoi du contrôle à celui-ci.</span><span class="sxs-lookup"><span data-stu-id="a6dea-183">The **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry the connect operation without telling or bothering your program, such as returning control to your program.</span></span> <span data-ttu-id="a6dea-184">Les nouvelles tentatives peuvent se produire dans les situations suivantes :</span><span class="sxs-lookup"><span data-stu-id="a6dea-184">The retries can occur in the following situations:</span></span>

* <span data-ttu-id="a6dea-185">Appel de méthode mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="a6dea-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="a6dea-186">Appel de méthode mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="a6dea-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="a6dea-187">Il existe une subtilité.</span><span class="sxs-lookup"><span data-stu-id="a6dea-187">There is a subtlety.</span></span> <span data-ttu-id="a6dea-188">Si une erreur temporaire se produit pendant l’exécution de votre *requête* , votre objet **SqlConnection** ne retente pas l’opération de connexion, et ne relance certainement pas votre requête.</span><span class="sxs-lookup"><span data-stu-id="a6dea-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry the connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="a6dea-189">Toutefois, **SqlConnection** vérifie très rapidement la connexion avant d’envoyer votre requête pour exécution.</span><span class="sxs-lookup"><span data-stu-id="a6dea-189">However, **SqlConnection** very quickly checks the connection before sending your query for execution.</span></span> <span data-ttu-id="a6dea-190">Si la vérification rapide détecte un problème de connexion, **SqlConnection** réessaye l’opération de connexion.</span><span class="sxs-lookup"><span data-stu-id="a6dea-190">If the quick check detects a connection problem, **SqlConnection** retries the connect operation.</span></span> <span data-ttu-id="a6dea-191">Si la nouvelle tentative réussit, votre requête est envoyée pour exécution.</span><span class="sxs-lookup"><span data-stu-id="a6dea-191">If the retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="a6dea-192">Le paramètre ConnectRetryCount doit-il être combiné avec la logique de nouvelle tentative d’application ?</span><span class="sxs-lookup"><span data-stu-id="a6dea-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="a6dea-193">Supposons que votre application possède une logique de nouvelle tentative personnalisée robuste.</span><span class="sxs-lookup"><span data-stu-id="a6dea-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="a6dea-194">Elle peut réessayer l’opération de connexion 4 fois.</span><span class="sxs-lookup"><span data-stu-id="a6dea-194">It might retry the connect operation 4 times.</span></span> <span data-ttu-id="a6dea-195">Si vous ajoutez **ConnectRetryInterval** et **ConnectRetryCount** = 3 à votre chaîne de connexion, vous augmentez le nombre de nouvelles tentatives à 4 * 3, soit 12 nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="a6dea-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 to your connection string, you will increase the retry count to 4 * 3 = 12 retries.</span></span> <span data-ttu-id="a6dea-196">Vous ne souhaitez peut-être pas un si grand nombre de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="a6dea-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-to-azure-sql-database"></a><span data-ttu-id="a6dea-197">Connexion à Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="a6dea-197">Connections to Azure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="a6dea-198">Connexion : chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="a6dea-198">Connection: Connection string</span></span>
<span data-ttu-id="a6dea-199">La chaîne de connexion nécessaire à la connexion à Azure SQL Database est légèrement différente de celle qui sert à se connecter à Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="a6dea-199">The connection string necessary for connecting to Azure SQL Database is slightly different from the string for connecting to Microsoft SQL Server.</span></span> <span data-ttu-id="a6dea-200">Il est possible de copier la chaîne de connexion de votre base de données à partir du [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6dea-200">You can copy the connection string for your database from the [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="a6dea-201">Connexion : adresse IP</span><span class="sxs-lookup"><span data-stu-id="a6dea-201">Connection: IP address</span></span>
<span data-ttu-id="a6dea-202">Vous devez configurer le serveur de base de données SQL pour accepter les communications à partir de l’adresse IP de l’ordinateur qui héberge votre programme client.</span><span class="sxs-lookup"><span data-stu-id="a6dea-202">You must configure the SQL Database server to accept communication from the IP address of the computer that hosts your client program.</span></span> <span data-ttu-id="a6dea-203">Pour ce faire, vous devez modifier les paramètres du pare-feu via le [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="a6dea-203">You do this by editing the firewall settings through the [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="a6dea-204">Si vous oubliez de configurer l’adresse IP, votre programme échouera en envoyant un message d’erreur pratique indiquant l’adresse IP nécessaire.</span><span class="sxs-lookup"><span data-stu-id="a6dea-204">If you forget to configure the IP address, your program will fail with a handy error message that states the necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="a6dea-205">Pour plus d’informations, consultez [Procédure : configuration des paramètres du pare-feu sur SQL Database](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="a6dea-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="a6dea-206">Connexion : ports</span><span class="sxs-lookup"><span data-stu-id="a6dea-206">Connection: Ports</span></span>
<span data-ttu-id="a6dea-207">En règle générale, vous devez simplement vous assurer que le port 1433 est ouvert pour la communication sortante sur l’ordinateur qui héberge le programme client.</span><span class="sxs-lookup"><span data-stu-id="a6dea-207">Typically you only need to ensure that port 1433 is open for outbound communication, on the computer that hosts you client program.</span></span>

<span data-ttu-id="a6dea-208">Par exemple, lorsque votre programme client est hébergé sur un ordinateur Windows, le pare-feu Windows sur l’ordinateur hôte vous permet d’ouvrir le port 1433 :</span><span class="sxs-lookup"><span data-stu-id="a6dea-208">For example, when your client program is hosted on a Windows computer, the Windows Firewall on the host enables you to open port 1433:</span></span>

1. <span data-ttu-id="a6dea-209">Ouvrir le panneau de configuration</span><span class="sxs-lookup"><span data-stu-id="a6dea-209">Open the Control Panel</span></span>
2. <span data-ttu-id="a6dea-210">&gt; Tous les éléments du Panneau de configuration</span><span class="sxs-lookup"><span data-stu-id="a6dea-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="a6dea-211">&gt; Pare-feu Windows</span><span class="sxs-lookup"><span data-stu-id="a6dea-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="a6dea-212">&gt; Paramètres avancés</span><span class="sxs-lookup"><span data-stu-id="a6dea-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="a6dea-213">&gt; Règles de trafic sortant</span><span class="sxs-lookup"><span data-stu-id="a6dea-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="a6dea-214">&gt; Actions</span><span class="sxs-lookup"><span data-stu-id="a6dea-214">&gt; Actions</span></span>
7. <span data-ttu-id="a6dea-215">&gt; Nouvelle règle</span><span class="sxs-lookup"><span data-stu-id="a6dea-215">&gt; New Rule</span></span>

<span data-ttu-id="a6dea-216">Si votre programme client est hébergé sur une machine virtuelle Azure, consultez </span><span class="sxs-lookup"><span data-stu-id="a6dea-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="a6dea-217">[Ports au-delà de 1433 pour ADO .NET 4.5 et SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="a6dea-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="a6dea-218">Pour obtenir des informations générales sur la configuration des ports et l’adresse IP, voir [Pare-feu Azure SQL Database](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="a6dea-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="a6dea-219">Connexion : ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="a6dea-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="a6dea-220">Si votre programme utilise des classes ADO.NET comme **System.Data.SqlClient.SqlConnection** pour se connecter à Azure SQL Database, nous vous recommandons d’utiliser .NET Framework version 4.6.1 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="a6dea-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** to connect to Azure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="a6dea-221">ADO.NET 4.6.1 :</span><span class="sxs-lookup"><span data-stu-id="a6dea-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="a6dea-222">Pour Azure SQL Database, l’ouverture d’une connexion à l’aide de la méthode **SqlConnection.Open** garantit une meilleure fiabilité.</span><span class="sxs-lookup"><span data-stu-id="a6dea-222">For Azure SQL Database, there is improved reliability when you open a connection by using the **SqlConnection.Open** method.</span></span> <span data-ttu-id="a6dea-223">La méthode **Open** intègre désormais de meilleurs mécanismes de nouvelle tentative en réponse à des défaillances temporaires, pour certaines erreurs se produisant avant le délai d’expiration de la connexion.</span><span class="sxs-lookup"><span data-stu-id="a6dea-223">The **Open** method now incorporates best effort retry mechanisms in response to transient faults, for certain errors within the Connection Timeout period.</span></span>
* <span data-ttu-id="a6dea-224">Prend en charge le regroupement de connexions.</span><span class="sxs-lookup"><span data-stu-id="a6dea-224">Supports connection pooling.</span></span> <span data-ttu-id="a6dea-225">Cela contribue à garantir que l’objet de connexion qu’il donne à votre programme fonctionne.</span><span class="sxs-lookup"><span data-stu-id="a6dea-225">This includes an efficient verification that the connection object it gives your program is functioning.</span></span>

<span data-ttu-id="a6dea-226">Lorsque vous utilisez un objet de connexion à partir d’un pool de connexions, nous conseillons de faire en sorte que votre programme interrompe temporairement la connexion lorsque vous ne l’utilisez pas immédiatement.</span><span class="sxs-lookup"><span data-stu-id="a6dea-226">When you use a connection object from a connection pool, we recommend that your program temporarily close the connection when not immediately using it.</span></span> <span data-ttu-id="a6dea-227">La réouverture d’une connexion n’est pas aussi coûteuse que la création d’une nouvelle connexion.</span><span class="sxs-lookup"><span data-stu-id="a6dea-227">Re-opening a connection is not expensive the way creating a new connection is.</span></span>

<span data-ttu-id="a6dea-228">Si vous utilisez ADO.NET 4.0 ou une version antérieure, nous vous recommandons d’effectuer une mise à niveau vers la dernière version d’ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="a6dea-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade to the latest ADO.NET.</span></span>

* <span data-ttu-id="a6dea-229">Depuis novembre 2015, [ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)est disponible au téléchargement.</span><span class="sxs-lookup"><span data-stu-id="a6dea-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="a6dea-230">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="a6dea-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="a6dea-231">Diagnostic : vérifier si les utilitaires peuvent se connecter</span><span class="sxs-lookup"><span data-stu-id="a6dea-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="a6dea-232">Si votre programme ne peut pas se connecter à Azure SQL Database, une option de diagnostic consiste à essayer de se connecter à un programme utilitaire.</span><span class="sxs-lookup"><span data-stu-id="a6dea-232">If your program is failing to connect to Azure SQL Database, one diagnostic option is to try to connect with a utility program.</span></span> <span data-ttu-id="a6dea-233">Dans l’idéal, l’utilitaire se connecte à l’aide de la bibliothèque que votre programme utilise.</span><span class="sxs-lookup"><span data-stu-id="a6dea-233">Ideally the utility would connect by using the same library that your program uses.</span></span>

<span data-ttu-id="a6dea-234">Sur un ordinateur Windows, vous pouvez essayer ces utilitaires :</span><span class="sxs-lookup"><span data-stu-id="a6dea-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="a6dea-235">SQL Server Management Studio (ssms.exe), qui se connecte à l’aide d’ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="a6dea-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="a6dea-236">sqlcmd.exe, qui se connecte à l’aide d’ [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="a6dea-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="a6dea-237">Une fois connecté, faites un test avec une courte requête SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="a6dea-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-the-open-ports"></a><span data-ttu-id="a6dea-238">Diagnostic : vérifier les ports ouverts</span><span class="sxs-lookup"><span data-stu-id="a6dea-238">Diagnostics: Check the open ports</span></span>
<span data-ttu-id="a6dea-239">Supposons que vous soupçonnez que les tentatives de connexion échouent en raison de problèmes de port.</span><span class="sxs-lookup"><span data-stu-id="a6dea-239">Suppose you suspect that connection attempts are failing due to port issues.</span></span> <span data-ttu-id="a6dea-240">Depuis votre ordinateur, vous pouvez exécuter un utilitaire qui génère des rapports sur les configurations de port.</span><span class="sxs-lookup"><span data-stu-id="a6dea-240">On your computer you can run a utility that reports on the port configurations.</span></span>

<span data-ttu-id="a6dea-241">Sous Linux, les utilitaires suivants peuvent vous être utiles :</span><span class="sxs-lookup"><span data-stu-id="a6dea-241">On Linux the following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="a6dea-242">(Modifiez la valeur de l’exemple pour refléter votre adresse IP).</span><span class="sxs-lookup"><span data-stu-id="a6dea-242">(Change the example value to be your IP address.)</span></span>

<span data-ttu-id="a6dea-243">Sous Windows, l’utilitaire [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) peut s’avérer utile.</span><span class="sxs-lookup"><span data-stu-id="a6dea-243">On Windows the [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="a6dea-244">Voici une exécution de l’exemple qui demandé l’état d’un port sur un serveur de base de données SQL Azure, et qui a été exécuté sur un ordinateur portable :</span><span class="sxs-lookup"><span data-stu-id="a6dea-244">Here is an example execution that queried the port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting to resolve name to IP address...
Name resolved to 23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="a6dea-245">Diagnostic : consignation des erreurs dans un journal</span><span class="sxs-lookup"><span data-stu-id="a6dea-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="a6dea-246">Un problème intermittent est parfois mieux diagnostiqué par la détection d’une tendance générale observée sur plusieurs jours ou semaines.</span><span class="sxs-lookup"><span data-stu-id="a6dea-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="a6dea-247">Votre client peut aider à consigner toutes les erreurs qu’il rencontre un diagnostic.</span><span class="sxs-lookup"><span data-stu-id="a6dea-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="a6dea-248">Vous pourrez mettre en corrélation les entrées de journal avec des informations sur les erreurs de base consignées en interne par Azure SQL Database elle-même.</span><span class="sxs-lookup"><span data-stu-id="a6dea-248">You might be able to correlate the log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="a6dea-249">Enterprise Library 6 (EntLib60) offre des classes .NET gérées afin de faciliter la journalisation :</span><span class="sxs-lookup"><span data-stu-id="a6dea-249">Enterprise Library 6 (EntLib60) offers .NET managed classes to assist with logging:</span></span>

* [<span data-ttu-id="a6dea-250">5 - Un jeu d’enfants : utilisation du bloc d’application de journalisation</span><span class="sxs-lookup"><span data-stu-id="a6dea-250">5 - As Easy As Falling Off a Log: Using the Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="a6dea-251">Diagnostics : examinez les journaux d’erreur système</span><span class="sxs-lookup"><span data-stu-id="a6dea-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="a6dea-252">Voici certaines instructions Transact-SQL SELECT qui permettent d’interroger les journaux d’erreur et d’autres informations.</span><span class="sxs-lookup"><span data-stu-id="a6dea-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="a6dea-253">Interrogation de journaux</span><span class="sxs-lookup"><span data-stu-id="a6dea-253">Query of log</span></span> | <span data-ttu-id="a6dea-254">Description</span><span class="sxs-lookup"><span data-stu-id="a6dea-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="a6dea-255">La vue [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) propose des informations sur les événements individuels, notamment ceux qui peuvent causer des erreurs temporaires ou des problèmes de connectivité.</span><span class="sxs-lookup"><span data-stu-id="a6dea-255">The [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="a6dea-256">Dans l’idéal, vous pouvez mettre en corrélation les valeurs **start_time** ou **end_time** avec les informations indiquant quand votre programme client a rencontré des problèmes.</span><span class="sxs-lookup"><span data-stu-id="a6dea-256">Ideally you can correlate the **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="a6dea-257">**CONSEIL :** vous devez vous connecter à la base de données **principale** pour exécuter cette procédure.</span><span class="sxs-lookup"><span data-stu-id="a6dea-257">**TIP:** You must connect to the **master** database to run this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="a6dea-258">La vue [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) agrège des nombres de différents types d’événements, pour permettre des diagnostics supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="a6dea-258">The [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="a6dea-259">**CONSEIL :** vous devez vous connecter à la base de données **principale** pour exécuter cette procédure.</span><span class="sxs-lookup"><span data-stu-id="a6dea-259">**TIP:** You must connect to the **master** database to run this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-the-sql-database-log"></a><span data-ttu-id="a6dea-260">Diagnostics : Rechercher les événements liés aux problèmes dans le journal de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="a6dea-260">Diagnostics: Search for problem events in the SQL Database log</span></span>
<span data-ttu-id="a6dea-261">Vous pouvez rechercher des entrées sur les problèmes survenus dans le journal de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a6dea-261">You can search for entries about problem events in the log of Azure SQL Database.</span></span> <span data-ttu-id="a6dea-262">Essayez l’instruction Transact-SQL SELECT qui suit dans la base de données **MASTER** :</span><span class="sxs-lookup"><span data-stu-id="a6dea-262">Try the following Transact-SQL SELECT statement in the **master** database:</span></span>

```
SELECT
   object_name
  ,CAST(f.event_data as XML).value
      ('(/event/@timestamp)[1]', 'datetime2')                      AS [timestamp]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="error"]/value)[1]', 'int')             AS [error]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="state"]/value)[1]', 'int')             AS [state]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="is_success"]/value)[1]', 'bit')        AS [is_success]
  ,CAST(f.event_data as XML).value
      ('(/event/data[@name="database_name"]/value)[1]', 'sysname') AS [database_name]
FROM
  sys.fn_xe_telemetry_blob_target_read_file('el', null, null, null) AS f
WHERE
  object_name != 'login_event'  -- Login events are numerous.
  and
  '2015-06-21' < CAST(f.event_data as XML).value
        ('(/event/@timestamp)[1]', 'datetime2')
ORDER BY
  [timestamp] DESC
;
```


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="a6dea-263">quelques-unes d’entre elles ont renvoyé des lignes de sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="a6dea-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="a6dea-264">Vous trouverez plus loin une ligne renvoyée qui ressemble à ce qui suit .</span><span class="sxs-lookup"><span data-stu-id="a6dea-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="a6dea-265">Les valeurs null indiquées ne sont en général pas nulles dans d’autres lignes.</span><span class="sxs-lookup"><span data-stu-id="a6dea-265">The null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="a6dea-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="a6dea-266">Enterprise Library 6</span></span>
<span data-ttu-id="a6dea-267">Enterprise Library 6 (EntLib60) est une infrastructure de classes .NET qui vous permet d’implémenter des clients de cloud fiables, et notamment le service Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="a6dea-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is the Azure SQL Database service.</span></span> <span data-ttu-id="a6dea-268">Vous pouvez rechercher des rubriques dédiées à chaque zone dans laquelle EntLib60 peut être utile en visitant dans un premier temps :</span><span class="sxs-lookup"><span data-stu-id="a6dea-268">You can locate topics dedicated to each area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="a6dea-269">Enterprise Library 6 - avril 2013</span><span class="sxs-lookup"><span data-stu-id="a6dea-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="a6dea-270">La logique de nouvelle tentative pour la gestion des erreurs temporaires est un domaine où EntLib60 peut être utile :</span><span class="sxs-lookup"><span data-stu-id="a6dea-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="a6dea-271">4 - La persévérance, le secret de la réussite : utilisation du bloc applicatif de gestion des erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="a6dea-271">4 - Perseverance, Secret of All Triumphs: Using the Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="a6dea-272">Le code source pour EntLib60 est disponible au public en [téléchargement](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="a6dea-272">The source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="a6dea-273">Microsoft ne prévoit pas d’apporter des mises à jour de maintenance ou de fonctionnalité supplémentaires à EntLib.</span><span class="sxs-lookup"><span data-stu-id="a6dea-273">Microsoft has no plans to make further feature updates or maintenance updates to EntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="a6dea-274">Classes EntLib60 pour les erreurs temporaires et les nouvelles tentatives</span><span class="sxs-lookup"><span data-stu-id="a6dea-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="a6dea-275">Les classes EntLib60 suivantes sont particulièrement utiles pour la logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="a6dea-275">The following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="a6dea-276">Toutes se trouvent dans ou sous l’espace de noms **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling** :</span><span class="sxs-lookup"><span data-stu-id="a6dea-276">All these  are in, or are further under, the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="a6dea-277">*Dans l’espace de noms **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling** :*</span><span class="sxs-lookup"><span data-stu-id="a6dea-277">*In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="a6dea-278">**RetryPolicy** </span><span class="sxs-lookup"><span data-stu-id="a6dea-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="a6dea-279">**ExecuteAction** </span><span class="sxs-lookup"><span data-stu-id="a6dea-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="a6dea-280">**ExponentialBackoff** </span><span class="sxs-lookup"><span data-stu-id="a6dea-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="a6dea-281">**SqlDatabaseTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="a6dea-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="a6dea-282">**ReliableSqlConnection** </span><span class="sxs-lookup"><span data-stu-id="a6dea-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="a6dea-283">**ExecuteCommand** </span><span class="sxs-lookup"><span data-stu-id="a6dea-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="a6dea-284">Dans l’espace de noms **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="a6dea-284">In the namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="a6dea-285">**AlwaysTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="a6dea-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="a6dea-286">**NeverTransientErrorDetectionStrategy** </span><span class="sxs-lookup"><span data-stu-id="a6dea-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="a6dea-287">Voici des liens vers des informations sur EntLib60 :</span><span class="sxs-lookup"><span data-stu-id="a6dea-287">Here are links to information about EntLib60:</span></span>

* <span data-ttu-id="a6dea-288">[Livre électronique : Guide du développeur de Microsoft Enterprise Library, 2e édition](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="a6dea-288">Free [Book Download: Developer's Guide to Microsoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="a6dea-289">Meilleures pratiques : [Conseils généraux sur les nouvelles tentatives](../best-practices-retry-general.md) comprend une excellente présentation approfondie de la logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="a6dea-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="a6dea-290">Téléchargement NuGet de [Bibliothèque d’entreprise - Bloc applicatif de gestion des erreurs 6.0 temporaires de Microsoft](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="a6dea-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-the-logging-block"></a><span data-ttu-id="a6dea-291">EntLib60 : le bloc de journalisation</span><span class="sxs-lookup"><span data-stu-id="a6dea-291">EntLib60: The logging block</span></span>
* <span data-ttu-id="a6dea-292">Le bloc de journalisation est une solution très flexible et configurable qui vous permet de :</span><span class="sxs-lookup"><span data-stu-id="a6dea-292">The Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="a6dea-293">Créer et stocker des messages du journal dans de nombreux emplacements.</span><span class="sxs-lookup"><span data-stu-id="a6dea-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="a6dea-294">Classer et filtrer les messages.</span><span class="sxs-lookup"><span data-stu-id="a6dea-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="a6dea-295">Recueillir des informations contextuelles utiles pour le débogage et le suivi, ainsi que pour les exigences d’audit et de journalisation en général.</span><span class="sxs-lookup"><span data-stu-id="a6dea-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="a6dea-296">Le bloc de journalisation extrait les fonctionnalités issues de la destination de journalisation de façon que le code d’application soit cohérent, quels que soient l’emplacement et le type du magasin de journalisation cible.</span><span class="sxs-lookup"><span data-stu-id="a6dea-296">The Logging block abstracts the logging functionality from the log destination so that the application code is consistent, irrespective of the location and type of the target logging store.</span></span>

<span data-ttu-id="a6dea-297">Pour plus de détails, consultez [5 - Un jeu d’enfants : utilisation du bloc d’application de journalisation](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="a6dea-297">For details see: [5 - As Easy As Falling Off a Log: Using the Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="a6dea-298">Code source de la méthode EntLib60 IsTransient</span><span class="sxs-lookup"><span data-stu-id="a6dea-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="a6dea-299">Ensuite, à partir de la classe **SqlDatabaseTransientErrorDetectionStrategy**, le code source C# pour la méthode **IsTransient**.</span><span class="sxs-lookup"><span data-stu-id="a6dea-299">Next, from the **SqlDatabaseTransientErrorDetectionStrategy** class, is the C# source code for the **IsTransient** method.</span></span> <span data-ttu-id="a6dea-300">Le code source clarifie les erreurs considérées comme temporaires qui peuvent faire l’objet de nouvelles tentatives depuis avril 2013.</span><span class="sxs-lookup"><span data-stu-id="a6dea-300">The source code clarifies which errors were considered to be transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="a6dea-301">De nombreuses lignes **//comment** ont été supprimées de cette copie pour en augmenter la lisibilité.</span><span class="sxs-lookup"><span data-stu-id="a6dea-301">Numerous **//comment** lines have been removed from this copy to emphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in the exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // The service is currently busy. Retry the request after 10 seconds.
            // Code: (reason code to be decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode the reason code from the error message to
            // determine the grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach the decoded values as additional attributes to
            // the original SQL exception.
            sqlException.Data[condition.ThrottlingMode.GetType().Name] =
              condition.ThrottlingMode.ToString();
            sqlException.Data[condition.GetType().Name] = condition;

            return true;

          case 10928:
          case 10929:
          case 10053:
          case 10054:
          case 10060:
          case 40197:
          case 40540:
          case 40613:
          case 40143:
          case 233:
          case 64:
            // DBNETLIB Error Code: 20
            // The instance of SQL Server you attempted to connect to
            // does not support encryption.
          case (int)ProcessNetLibErrorCode.EncryptionNotSupported:
            return true;
        }
      }
    }
    else if (ex is TimeoutException)
    {
      return true;
    }
    else
    {
      EntityException entityException;
      if ((entityException = ex as EntityException) != null)
      {
        return this.IsTransient(entityException.InnerException);
      }
    }
  }

  return false;
}
```


## <a name="next-steps"></a><span data-ttu-id="a6dea-302">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a6dea-302">Next steps</span></span>
* <span data-ttu-id="a6dea-303">Pour résoudre les autres problèmes de connexion courants à Azure SQL Database, consultez [Résolution des problèmes de connexion à Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="a6dea-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues to Azure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="a6dea-304">Regroupement de connexions SQL Server (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="a6dea-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="a6dea-305">*Nouvelle tentative* est une bibliothèque de nouvelle tentative sous licence Apache 2.0 à usage général écrite en langage **Python**, pour simplifier la tâche consistant à ajouter des comportements de nouvelle tentative dans toutes les situations.</span><span class="sxs-lookup"><span data-stu-id="a6dea-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, to simplify the task of adding retry behavior to just about anything.</span></span>](https://pypi.python.org/pypi/retrying)

