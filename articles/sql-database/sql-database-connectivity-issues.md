---
title: aaaFix une erreur de connexion SQL, erreur temporaire | Documents Microsoft
description: "Découvrez comment tootroubleshoot, diagnostiquer et empêcher une erreur de connexion SQL ou d’une erreur temporaire dans la base de données SQL Azure. "
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
ms.openlocfilehash: d225e610b9e88170ab53ca16d615bd07220603cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-diagnose-and-prevent-sql-connection-errors-and-transient-errors-for-sql-database"></a><span data-ttu-id="5610d-104">Diagnostiquer, résoudre et empêcher les erreurs de connexion SQL et les erreurs temporaires de Base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5610d-104">Troubleshoot, diagnose, and prevent SQL connection errors and transient errors for SQL Database</span></span>
<span data-ttu-id="5610d-105">Cet article décrit comment tooprevent, résoudre les problèmes, diagnostiquer et limiter les erreurs de connexion et les erreurs temporaires que votre application cliente rencontre lorsqu’il interagit avec la base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5610d-105">This article describes how tooprevent, troubleshoot, diagnose, and mitigate connection errors and transient errors that your client application encounters when it interacts with Azure SQL Database.</span></span> <span data-ttu-id="5610d-106">Découvrez comment tooconfigure logique de nouvelle tentative, générer la chaîne de connexion hello et ajuster d’autres paramètres de connexion.</span><span class="sxs-lookup"><span data-stu-id="5610d-106">Learn how tooconfigure retry logic, build hello connection string, and adjust other connection settings.</span></span>

<a id="i-transient-faults" name="i-transient-faults"></a>

## <a name="transient-errors-transient-faults"></a><span data-ttu-id="5610d-107">Erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="5610d-107">Transient errors (transient faults)</span></span>
<span data-ttu-id="5610d-108">Une erreur temporaire s’explique par une cause sous-jacente qui se résout d’elle-même en peu de temps.</span><span class="sxs-lookup"><span data-stu-id="5610d-108">A transient error - also, transient fault - has an underlying cause that will soon resolve itself.</span></span> <span data-ttu-id="5610d-109">Une cause occasionnelle d’erreurs temporaires est hello système Azure déplace rapidement matériel ressources toobetter l’équilibrage de charge différentes charges de travail.</span><span class="sxs-lookup"><span data-stu-id="5610d-109">An occasional cause of transient errors is when hello Azure system quickly shifts hardware resources toobetter load-balance various workloads.</span></span> <span data-ttu-id="5610d-110">La plupart de ces événements de reconfiguration se terminent souvent en moins de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="5610d-110">Most of these reconfiguration events often complete in less than 60 seconds.</span></span> <span data-ttu-id="5610d-111">Pendant ce laps de temps reconfiguration, peut avoir une connectivité émet tooAzure base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="5610d-111">During this reconfiguration time span, you may have connectivity issues tooAzure SQL Database.</span></span> <span data-ttu-id="5610d-112">Les applications se connectant tooAzure base de données SQL doit être générée tooexpect ces erreurs temporaires, handle en implémentant la logique dans leur code au lieu de les surfaces toousers comme des erreurs d’application de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="5610d-112">Applications connecting tooAzure SQL Database should be built tooexpect these transient errors, handle them by implementing retry logic in their code instead of surfacing them toousers as application errors.</span></span>

<span data-ttu-id="5610d-113">Si votre programme client utilise ADO.NET, votre programme est informé d’erreur temporaire de hello par throw hello d’un **SqlException**.</span><span class="sxs-lookup"><span data-stu-id="5610d-113">If your client program is using ADO.NET, your program is told about hello transient error by hello throw of an **SqlException**.</span></span> <span data-ttu-id="5610d-114">Hello **nombre** propriété peut être comparée à la liste hello des erreurs temporaires haut hello de rubrique de hello : [codes d’erreur SQL pour les applications clientes de base de données SQL](sql-database-develop-error-messages.md).</span><span class="sxs-lookup"><span data-stu-id="5610d-114">hello **Number** property can be compared against hello list of transient errors near hello top of hello topic: [SQL error codes for SQL Database client applications](sql-database-develop-error-messages.md).</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="5610d-115">Connexion ou commande</span><span class="sxs-lookup"><span data-stu-id="5610d-115">Connection versus command</span></span>
<span data-ttu-id="5610d-116">Vous allez tentatives de connexion de SQL hello ou établir de nouveau, selon les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="5610d-116">You'll retry hello SQL connection or establish it again, depending on hello following:</span></span>

* <span data-ttu-id="5610d-117">**Une erreur temporaire se produit pendant une tentative de connexion**: connexion de hello doit être renouvelée après retarder pendant quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="5610d-117">**A transient error occurs during a connection try**: hello connection should be retried after delaying for several seconds.</span></span>
* <span data-ttu-id="5610d-118">**Une erreur temporaire se produit pendant une commande de requête SQL**: commande hello ne doit pas être réessayée immédiatement.</span><span class="sxs-lookup"><span data-stu-id="5610d-118">**A transient error occurs during a SQL query command**: hello command should not be immediately retried.</span></span> <span data-ttu-id="5610d-119">Au lieu de cela, après un délai de connexion de hello fraîchement convient.</span><span class="sxs-lookup"><span data-stu-id="5610d-119">Instead, after a delay, hello connection should be freshly established.</span></span> <span data-ttu-id="5610d-120">Commande hello peut être retentée.</span><span class="sxs-lookup"><span data-stu-id="5610d-120">Then hello command can be retried.</span></span>

<a id="j-retry-logic-transient-faults" name="j-retry-logic-transient-faults"></a>

### <a name="retry-logic-for-transient-errors"></a><span data-ttu-id="5610d-121">Logique de nouvelle tentative pour les erreurs temporaires</span><span class="sxs-lookup"><span data-stu-id="5610d-121">Retry logic for transient errors</span></span>
<span data-ttu-id="5610d-122">Les programmes clients qui rencontrent occasionnellement une erreur temporaire sont plus solides lorsqu’ils contiennent une logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="5610d-122">Client programs that occasionally encounter a transient error are more robust when they contain retry logic.</span></span>

<span data-ttu-id="5610d-123">Lorsque votre programme communique avec la base de données SQL Azure via un intergiciel (middleware) tiers 3e, obtenir des informations auprès du fournisseur de hello si hello intergiciel (middleware) contient la logique de nouvelle tentative pour les erreurs temporaires.</span><span class="sxs-lookup"><span data-stu-id="5610d-123">When your program communicates with Azure SQL Database through a 3rd party middleware, inquire with hello vendor whether hello middleware contains retry logic for transient errors.</span></span>

<a id="principles-for-retry" name="principles-for-retry"></a>

#### <a name="principles-for-retry"></a><span data-ttu-id="5610d-124">Principes de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="5610d-124">Principles for retry</span></span>
* <span data-ttu-id="5610d-125">Une tentative de tooopen une connexion doit être renouvelé si l’erreur de hello est temporaire.</span><span class="sxs-lookup"><span data-stu-id="5610d-125">An attempt tooopen a connection should be retried if hello error is transient.</span></span>
* <span data-ttu-id="5610d-126">Une instruction SQL SELECT qui échoue avec une erreur temporaire ne doit pas être retentée directement.</span><span class="sxs-lookup"><span data-stu-id="5610d-126">A SQL SELECT statement that fails with a transient error should not be retried directly.</span></span>
  
  * <span data-ttu-id="5610d-127">Au lieu de cela, établir une nouvelle connexion et recommencez hello SELECT.</span><span class="sxs-lookup"><span data-stu-id="5610d-127">Instead, establish a fresh connection, and then retry hello SELECT.</span></span>
* <span data-ttu-id="5610d-128">Lorsqu’une instruction SQL UPDATE échoue avec une erreur temporaire, une nouvelle connexion doit être établie avant nouvelle tentative de mise à jour de hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-128">When a SQL UPDATE statement fails with a transient error, a fresh connection should be established before hello UPDATE is retried.</span></span>
  
  * <span data-ttu-id="5610d-129">logique de nouvelle tentative Hello doit s’assurer que, soit en utilisant transaction de base de données entière hello terminée que hello ensemble de la transaction est restaurée.</span><span class="sxs-lookup"><span data-stu-id="5610d-129">hello retry logic must ensure that either hello entire database transaction completed, or that hello entire transaction is rolled back.</span></span>

#### <a name="other-considerations-for-retry"></a><span data-ttu-id="5610d-130">Autres considérations</span><span class="sxs-lookup"><span data-stu-id="5610d-130">Other considerations for retry</span></span>
* <span data-ttu-id="5610d-131">Un programme de traitement par lots qui est démarré automatiquement après les heures de travail, et qui s’achève avant matin, supportent patient toovery avec des périodes de temps entre les nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="5610d-131">A batch program that is automatically started after work hours, and which will complete before morning, can afford toovery patient with long time intervals between its retry attempts.</span></span>
* <span data-ttu-id="5610d-132">Un programme de l’interface utilisateur doit prendre en compte hello tendance toogive d’après une attente de trop longue.</span><span class="sxs-lookup"><span data-stu-id="5610d-132">A user interface program should account for hello human tendency toogive up after too long a wait.</span></span>
  
  * <span data-ttu-id="5610d-133">Toutefois, hello solution ne doit pas être tooretry après quelques secondes, car cette stratégie peut inonder le système hello avec des requêtes.</span><span class="sxs-lookup"><span data-stu-id="5610d-133">However, hello solution must not be tooretry every few seconds, because that policy can flood hello system with requests.</span></span>

#### <a name="interval-increase-between-retries"></a><span data-ttu-id="5610d-134">Augmentation de l’intervalle entre les tentatives</span><span class="sxs-lookup"><span data-stu-id="5610d-134">Interval increase between retries</span></span>
<span data-ttu-id="5610d-135">Nous vous recommandons de patienter 5 secondes avant votre première tentative.</span><span class="sxs-lookup"><span data-stu-id="5610d-135">We recommend that you delay for 5 seconds before your first retry.</span></span> <span data-ttu-id="5610d-136">Une nouvelle tentative après un délai inférieur à 5 secondes risque de service de cloud hello insurmontable.</span><span class="sxs-lookup"><span data-stu-id="5610d-136">Retrying after a delay shorter than 5 seconds risks overwhelming hello cloud service.</span></span> <span data-ttu-id="5610d-137">Pour chaque nouvelle tentative ultérieure délai de hello doit croître de manière exponentielle, jusqu'à tooa maximale de 60 secondes.</span><span class="sxs-lookup"><span data-stu-id="5610d-137">For each subsequent retry hello delay should grow exponentially, up tooa maximum of 60 seconds.</span></span>

<span data-ttu-id="5610d-138">En savoir plus sur hello *la période de blocage* pour les clients qui utilisent ADO.NET est disponible dans [le regroupement de connexion SQL Server (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span><span class="sxs-lookup"><span data-stu-id="5610d-138">A discussion of hello *blocking period* for clients that use ADO.NET is available in [SQL Server Connection Pooling (ADO.NET)](http://msdn.microsoft.com/library/8xx3tyca.aspx).</span></span>

<span data-ttu-id="5610d-139">Vous pouvez également vous tooset un nombre maximal de tentatives avant que le programme de hello s’arrête automatiquement.</span><span class="sxs-lookup"><span data-stu-id="5610d-139">You might also want tooset a maximum number of retries before hello program self-terminates.</span></span>

#### <a name="code-samples-with-retry-logic"></a><span data-ttu-id="5610d-140">Exemples de code avec la logique de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="5610d-140">Code samples with retry logic</span></span>
<span data-ttu-id="5610d-141">Vous trouverez des exemples de code avec logique de nouvelle tentative dans divers langages de programmation ici :</span><span class="sxs-lookup"><span data-stu-id="5610d-141">Code samples with retry logic, in a variety of programming languages, are available at:</span></span>

* [<span data-ttu-id="5610d-142">Bibliothèques de connexions pour SQL Database et SQL Server</span><span class="sxs-lookup"><span data-stu-id="5610d-142">Connection libraries for SQL Database and SQL Server</span></span>](sql-database-libraries.md)

<a id="k-test-retry-logic" name="k-test-retry-logic"></a>

#### <a name="test-your-retry-logic"></a><span data-ttu-id="5610d-143">Tester votre logique de nouvelle tentative</span><span class="sxs-lookup"><span data-stu-id="5610d-143">Test your retry logic</span></span>
<span data-ttu-id="5610d-144">tootest votre logique de nouvelle tentative, vous devez simuler ou provoquer une erreur que peuvent être corrigées pendant que votre programme est en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="5610d-144">tootest your retry logic, you must simulate or cause an error than can be corrected while your program is still running.</span></span>

##### <a name="test-by-disconnecting-from-hello-network"></a><span data-ttu-id="5610d-145">En déconnectant hello réseau de test</span><span class="sxs-lookup"><span data-stu-id="5610d-145">Test by disconnecting from hello network</span></span>
<span data-ttu-id="5610d-146">Vous pouvez tester votre logique de nouvelle tentative consiste toodisconnect votre ordinateur client à partir de hello réseau pendant l’exécution du programme de hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-146">One way you can test your retry logic is toodisconnect your client computer from hello network while hello program is running.</span></span> <span data-ttu-id="5610d-147">Erreur de Hello sera :</span><span class="sxs-lookup"><span data-stu-id="5610d-147">hello error will be:</span></span>

* <span data-ttu-id="5610d-148">**SqlException.Number** = 11001</span><span class="sxs-lookup"><span data-stu-id="5610d-148">**SqlException.Number** = 11001</span></span>
* <span data-ttu-id="5610d-149">Message : « Hôte inconnu »</span><span class="sxs-lookup"><span data-stu-id="5610d-149">Message: "No such host is known"</span></span>

<span data-ttu-id="5610d-150">Comme tout d’abord, la partie de hello nouvelle tentative, votre programme peut corriger des fautes d’orthographe hello et tentez ensuite tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5610d-150">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="5610d-151">toomake ce pratique, vous déconnecter votre ordinateur à partir du réseau de hello avant de commencer votre programme.</span><span class="sxs-lookup"><span data-stu-id="5610d-151">toomake this practical, you unplug your computer from hello network before you start your program.</span></span> <span data-ttu-id="5610d-152">Ensuite, votre programme reconnaît un paramètre d’exécution qui provoque hello du programme :</span><span class="sxs-lookup"><span data-stu-id="5610d-152">Then your program recognizes a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="5610d-153">Ajoutez temporairement 11001 liste tooits des erreurs tooconsider comme temporaire.</span><span class="sxs-lookup"><span data-stu-id="5610d-153">Temporarily add 11001 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="5610d-154">Tente sa première connexion comme d’habitude.</span><span class="sxs-lookup"><span data-stu-id="5610d-154">Attempt its first connection as usual.</span></span>
3. <span data-ttu-id="5610d-155">Une fois l’erreur de hello est interceptée, supprimez 11001 hello liste.</span><span class="sxs-lookup"><span data-stu-id="5610d-155">After hello error is caught, remove 11001 from hello list.</span></span>
4. <span data-ttu-id="5610d-156">Afficher un message indiquant l’ordinateur de hello tooplug hello utilisateur dans un réseau de hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-156">Display a message telling hello user tooplug hello computer into hello network.</span></span>
   * <span data-ttu-id="5610d-157">Suspendre davantage d’exécution à l’aide soit hello **Console.ReadLine** méthode ou une boîte de dialogue avec un bouton OK.</span><span class="sxs-lookup"><span data-stu-id="5610d-157">Pause further execution by using either hello **Console.ReadLine** method or a dialog with an OK button.</span></span> <span data-ttu-id="5610d-158">utilisateur de Hello appuie sur la touche hello une fois que l’ordinateur de hello connecté hello réseau.</span><span class="sxs-lookup"><span data-stu-id="5610d-158">hello user presses hello Enter key after hello computer plugged into hello network.</span></span>
5. <span data-ttu-id="5610d-159">Essayez à nouveau tooconnect, attendu de réussite.</span><span class="sxs-lookup"><span data-stu-id="5610d-159">Attempt again tooconnect, expecting success.</span></span>

##### <a name="test-by-misspelling-hello-database-name-when-connecting"></a><span data-ttu-id="5610d-160">Lors de la connexion de test par le nom de base de données hello faute d’orthographe</span><span class="sxs-lookup"><span data-stu-id="5610d-160">Test by misspelling hello database name when connecting</span></span>
<span data-ttu-id="5610d-161">Votre programme peut faire volontairement mal orthographié le nom d’utilisateur hello avant la première tentative de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-161">Your program can purposely misspell hello user name before hello first connection attempt.</span></span> <span data-ttu-id="5610d-162">Erreur de Hello sera :</span><span class="sxs-lookup"><span data-stu-id="5610d-162">hello error will be:</span></span>

* <span data-ttu-id="5610d-163">**SqlException.Number** = 18456</span><span class="sxs-lookup"><span data-stu-id="5610d-163">**SqlException.Number** = 18456</span></span>
* <span data-ttu-id="5610d-164">Message : « Échec de la connexion pour l’utilisateur 'WRONG_MyUserName' »</span><span class="sxs-lookup"><span data-stu-id="5610d-164">Message: "Login failed for user 'WRONG_MyUserName'."</span></span>

<span data-ttu-id="5610d-165">Comme tout d’abord, la partie de hello nouvelle tentative, votre programme peut corriger des fautes d’orthographe hello et tentez ensuite tooconnect.</span><span class="sxs-lookup"><span data-stu-id="5610d-165">As part of hello first retry attempt, your program can correct hello misspelling, and then attempt tooconnect.</span></span>

<span data-ttu-id="5610d-166">toomake ce pratique, votre programme peut reconnaître un paramètre d’exécution qui provoque hello du programme :</span><span class="sxs-lookup"><span data-stu-id="5610d-166">toomake this practical, your program could recognize a run time parameter that causes hello program to:</span></span>

1. <span data-ttu-id="5610d-167">Ajoutez temporairement 18456 liste tooits des erreurs tooconsider comme temporaire.</span><span class="sxs-lookup"><span data-stu-id="5610d-167">Temporarily add 18456 tooits list of errors tooconsider as transient.</span></span>
2. <span data-ttu-id="5610d-168">Ajouter volontairement les nom d’utilisateur toohello 'WRONG_'.</span><span class="sxs-lookup"><span data-stu-id="5610d-168">Purposely add 'WRONG_' toohello user name.</span></span>
3. <span data-ttu-id="5610d-169">Une fois l’erreur de hello est interceptée, supprimez 18456 hello liste.</span><span class="sxs-lookup"><span data-stu-id="5610d-169">After hello error is caught, remove 18456 from hello list.</span></span>
4. <span data-ttu-id="5610d-170">Supprimez 'WRONG_' hello nom d’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="5610d-170">Remove 'WRONG_' from hello user name.</span></span>
5. <span data-ttu-id="5610d-171">Essayez à nouveau tooconnect, attendu de réussite.</span><span class="sxs-lookup"><span data-stu-id="5610d-171">Attempt again tooconnect, expecting success.</span></span>

<a id="net-sqlconnection-parameters-for-connection-retry" name="net-sqlconnection-parameters-for-connection-retry"></a>

### <a name="net-sqlconnection-parameters-for-connection-retry"></a><span data-ttu-id="5610d-172">Paramètres de connexion .NET Sql pour les nouvelles tentatives de connexion</span><span class="sxs-lookup"><span data-stu-id="5610d-172">.NET SqlConnection parameters for connection retry</span></span>
<span data-ttu-id="5610d-173">Si votre programme client connecte tootooAzure base de données SQL à l’aide de la classe de .NET Framework hello **System.Data.SqlClient.SqlConnection**, vous devez utiliser .NET 4.6.1 ou version ultérieure (ou .NET Core) afin de vous pouvez tirer parti de sa fonctionnalité de nouvelle tentative de connexion.</span><span class="sxs-lookup"><span data-stu-id="5610d-173">If your client program connects tootooAzure SQL Database by using hello .NET Framework class **System.Data.SqlClient.SqlConnection**, you should use .NET 4.6.1 or later (or .NET Core) so you can leverage its connection retry feature.</span></span> <span data-ttu-id="5610d-174">Détails de la fonctionnalité de hello sont [ici](http://go.microsoft.com/fwlink/?linkid=393996).</span><span class="sxs-lookup"><span data-stu-id="5610d-174">Details of hello feature are [here](http://go.microsoft.com/fwlink/?linkid=393996).</span></span>

<!--
2015-11-30, FwLink 393996 points toodn632678.aspx, which links tooa downloadable .docx related tooSqlClient and SQL Server 2014.
-->


<span data-ttu-id="5610d-175">Lorsque vous générez hello [chaîne de connexion](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) pour votre **SqlConnection** de l’objet, vous devez coordonner les valeurs hello entre hello paramètres suivants :</span><span class="sxs-lookup"><span data-stu-id="5610d-175">When you build hello [connection string](http://msdn.microsoft.com/library/System.Data.SqlClient.SqlConnection.connectionstring.aspx) for your **SqlConnection** object, you should coordinate hello values among hello following parameters:</span></span>

* <span data-ttu-id="5610d-176">ConnectRetryCount &nbsp;&nbsp;*(La valeur par défaut est 1. La plage s’étend de 0 à 255.)*</span><span class="sxs-lookup"><span data-stu-id="5610d-176">ConnectRetryCount &nbsp;&nbsp;*(Default is 1. Range is 0 through 255.)*</span></span>
* <span data-ttu-id="5610d-177">ConnectRetryInterval &nbsp;&nbsp;*(La valeur par défaut est 1 seconde. La plage s’étend de 1 à 60.)*</span><span class="sxs-lookup"><span data-stu-id="5610d-177">ConnectRetryInterval &nbsp;&nbsp;*(Default is 1 second. Range is 1 through 60.)*</span></span>
* <span data-ttu-id="5610d-178">Délai d’expiration de connexion &nbsp;&nbsp;*(La valeur par défaut est 15 secondes. La plage s’étend de 0 à 2147483647.)*</span><span class="sxs-lookup"><span data-stu-id="5610d-178">Connection Timeout &nbsp;&nbsp;*(Default is 15 seconds. Range is 0 through 2147483647)*</span></span>

<span data-ttu-id="5610d-179">Plus précisément, vos valeurs choisies doivent rendre hello suivant true d’égalité :</span><span class="sxs-lookup"><span data-stu-id="5610d-179">Specifically, your chosen values should make hello following equality true:</span></span>

* <span data-ttu-id="5610d-180">Délai d’expiration de connexion = ConnectRetryCount × ConnectionRetryInterval</span><span class="sxs-lookup"><span data-stu-id="5610d-180">Connection Timeout = ConnectRetryCount * ConnectionRetryInterval</span></span>

<span data-ttu-id="5610d-181">Par exemple, si hello count = 3 et l’intervalle = 10 secondes, un délai d’expiration uniquement 29 secondes pas assez donnerait système de hello suffisamment de temps pour son nouvelle 3e et dernière tentative de connexion : 29 < 3 * 10.</span><span class="sxs-lookup"><span data-stu-id="5610d-181">For example, if hello count = 3, and interval = 10 seconds, a timeout of only 29 seconds would not quite give hello system enough time for its 3rd and final retry at connecting: 29 < 3 * 10.</span></span>

<a id="connection-versus-command" name="connection-versus-command"></a>

### <a name="connection-versus-command"></a><span data-ttu-id="5610d-182">Connexion ou commande</span><span class="sxs-lookup"><span data-stu-id="5610d-182">Connection versus command</span></span>
<span data-ttu-id="5610d-183">Hello **ConnectRetryCount** et **ConnectRetryInterval** paramètres permettent de votre **SqlConnection** opération hello de nouvelle tentative d’objet de connexion sans indiquant ou déranger votre programme, telle que le programme de contrôle de tooyour de retour.</span><span class="sxs-lookup"><span data-stu-id="5610d-183">hello **ConnectRetryCount** and **ConnectRetryInterval** parameters let your **SqlConnection** object retry hello connect operation without telling or bothering your program, such as returning control tooyour program.</span></span> <span data-ttu-id="5610d-184">nouvelles tentatives de Hello peuvent se produire dans hello suivant situations :</span><span class="sxs-lookup"><span data-stu-id="5610d-184">hello retries can occur in hello following situations:</span></span>

* <span data-ttu-id="5610d-185">Appel de méthode mySqlConnection.Open</span><span class="sxs-lookup"><span data-stu-id="5610d-185">mySqlConnection.Open method call</span></span>
* <span data-ttu-id="5610d-186">Appel de méthode mySqlConnection.Execute</span><span class="sxs-lookup"><span data-stu-id="5610d-186">mySqlConnection.Execute method call</span></span>

<span data-ttu-id="5610d-187">Il existe une subtilité.</span><span class="sxs-lookup"><span data-stu-id="5610d-187">There is a subtlety.</span></span> <span data-ttu-id="5610d-188">Si une erreur temporaire se produit pendant que votre *requête* est en cours d’exécution, votre **SqlConnection** ne l’opération de connexion pas de nouvelle tentative hello et certainement qu’il ne tente pas de votre requête de l’objet.</span><span class="sxs-lookup"><span data-stu-id="5610d-188">If a transient error occurs while your *query* is being executed, your **SqlConnection** object does not retry hello connect operation, and it certainly does not retry your query.</span></span> <span data-ttu-id="5610d-189">Toutefois, **SqlConnection** très rapidement les vérifications hello connexion avant d’envoyer votre requête pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="5610d-189">However, **SqlConnection** very quickly checks hello connection before sending your query for execution.</span></span> <span data-ttu-id="5610d-190">Si la vérification rapide de hello détecte un problème de connexion, **SqlConnection** l’opération hello de nouvelles tentatives de connexion.</span><span class="sxs-lookup"><span data-stu-id="5610d-190">If hello quick check detects a connection problem, **SqlConnection** retries hello connect operation.</span></span> <span data-ttu-id="5610d-191">Si la nouvelle tentative de hello réussit, vous interrogez est envoyé pour l’exécution.</span><span class="sxs-lookup"><span data-stu-id="5610d-191">If hello retry succeeds, you query is sent for execution.</span></span>

#### <a name="should-connectretrycount-be-combined-with-application-retry-logic"></a><span data-ttu-id="5610d-192">Le paramètre ConnectRetryCount doit-il être combiné avec la logique de nouvelle tentative d’application ?</span><span class="sxs-lookup"><span data-stu-id="5610d-192">Should ConnectRetryCount be combined with application retry logic?</span></span>
<span data-ttu-id="5610d-193">Supposons que votre application possède une logique de nouvelle tentative personnalisée robuste.</span><span class="sxs-lookup"><span data-stu-id="5610d-193">Suppose your application has robust custom retry logic.</span></span> <span data-ttu-id="5610d-194">Il peut réessayer hello 4 fois l’opération de connexion.</span><span class="sxs-lookup"><span data-stu-id="5610d-194">It might retry hello connect operation 4 times.</span></span> <span data-ttu-id="5610d-195">Si vous ajoutez **ConnectRetryInterval** et **ConnectRetryCount** = 3 tooyour chaîne de connexion, vous augmenterez too4 de nombre de nouvelles tentatives hello * 3 = 12 effectue une nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="5610d-195">If you add **ConnectRetryInterval** and **ConnectRetryCount** =3 tooyour connection string, you will increase hello retry count too4 * 3 = 12 retries.</span></span> <span data-ttu-id="5610d-196">Vous ne souhaitez peut-être pas un si grand nombre de nouvelles tentatives.</span><span class="sxs-lookup"><span data-stu-id="5610d-196">You might not intend such a high number of retries.</span></span>

<a id="a-connection-connection-string" name="a-connection-connection-string"></a>

## <a name="connections-tooazure-sql-database"></a><span data-ttu-id="5610d-197">TooAzure de connexions de base de données SQL</span><span class="sxs-lookup"><span data-stu-id="5610d-197">Connections tooAzure SQL Database</span></span>
<a id="c-connection-string" name="c-connection-string"></a>

### <a name="connection-connection-string"></a><span data-ttu-id="5610d-198">Connexion : chaîne de connexion</span><span class="sxs-lookup"><span data-stu-id="5610d-198">Connection: Connection string</span></span>
<span data-ttu-id="5610d-199">chaîne de connexion Hello nécessaire pour la connexion tooAzure base de données SQL est légèrement différente de la chaîne hello pour la connexion tooMicrosoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="5610d-199">hello connection string necessary for connecting tooAzure SQL Database is slightly different from hello string for connecting tooMicrosoft SQL Server.</span></span> <span data-ttu-id="5610d-200">Vous pouvez copier la chaîne de connexion hello pour votre base de données à partir de hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5610d-200">You can copy hello connection string for your database from hello [Azure portal](https://portal.azure.com/).</span></span>

[!INCLUDE [sql-database-include-connection-string-20-portalshots](../../includes/sql-database-include-connection-string-20-portalshots.md)]

<a id="b-connection-ip-address" name="b-connection-ip-address"></a>

### <a name="connection-ip-address"></a><span data-ttu-id="5610d-201">Connexion : adresse IP</span><span class="sxs-lookup"><span data-stu-id="5610d-201">Connection: IP address</span></span>
<span data-ttu-id="5610d-202">Vous devez configurer hello de base de données SQL server tooaccept communication à partir de l’adresse IP de hello d’ordinateur hello qui héberge votre programme client.</span><span class="sxs-lookup"><span data-stu-id="5610d-202">You must configure hello SQL Database server tooaccept communication from hello IP address of hello computer that hosts your client program.</span></span> <span data-ttu-id="5610d-203">Pour ce faire, modification des paramètres de pare-feu hello via hello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="5610d-203">You do this by editing hello firewall settings through hello [Azure portal](https://portal.azure.com/).</span></span>

<span data-ttu-id="5610d-204">Si vous oubliez d’adresse IP de hello tooconfigure, votre programme échouera avec un message d’erreur pratique qui indique les adresses IP nécessaires hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-204">If you forget tooconfigure hello IP address, your program will fail with a handy error message that states hello necessary IP address.</span></span>

[!INCLUDE [sql-database-include-ip-address-22-portal](../../includes/sql-database-include-ip-address-22-v12portal.md)]

<span data-ttu-id="5610d-205">Pour plus d’informations, consultez [Procédure : configuration des paramètres du pare-feu sur SQL Database](sql-database-configure-firewall-settings.md)</span><span class="sxs-lookup"><span data-stu-id="5610d-205">For more information, see: [How to: Configure firewall settings on SQL Database](sql-database-configure-firewall-settings.md)</span></span>

<a id="c-connection-ports" name="c-connection-ports"></a>

### <a name="connection-ports"></a><span data-ttu-id="5610d-206">Connexion : ports</span><span class="sxs-lookup"><span data-stu-id="5610d-206">Connection: Ports</span></span>
<span data-ttu-id="5610d-207">En règle générale, vous devez uniquement tooensure que le port 1433 est ouvert pour les communications sortantes sur ordinateur hello hébergeant programme client.</span><span class="sxs-lookup"><span data-stu-id="5610d-207">Typically you only need tooensure that port 1433 is open for outbound communication, on hello computer that hosts you client program.</span></span>

<span data-ttu-id="5610d-208">Par exemple, lorsque votre programme client est hébergé sur un ordinateur Windows, hello le pare-feu Windows sur l’ordinateur hôte de hello vous permet de tooopen le port 1433 :</span><span class="sxs-lookup"><span data-stu-id="5610d-208">For example, when your client program is hosted on a Windows computer, hello Windows Firewall on hello host enables you tooopen port 1433:</span></span>

1. <span data-ttu-id="5610d-209">Ouvrez le panneau de configuration de hello</span><span class="sxs-lookup"><span data-stu-id="5610d-209">Open hello Control Panel</span></span>
2. <span data-ttu-id="5610d-210">&gt; Tous les éléments du Panneau de configuration</span><span class="sxs-lookup"><span data-stu-id="5610d-210">&gt; All Control Panel Items</span></span>
3. <span data-ttu-id="5610d-211">&gt; Pare-feu Windows</span><span class="sxs-lookup"><span data-stu-id="5610d-211">&gt; Windows Firewall</span></span>
4. <span data-ttu-id="5610d-212">&gt; Paramètres avancés</span><span class="sxs-lookup"><span data-stu-id="5610d-212">&gt; Advanced Settings</span></span>
5. <span data-ttu-id="5610d-213">&gt; Règles de trafic sortant</span><span class="sxs-lookup"><span data-stu-id="5610d-213">&gt; Outbound Rules</span></span>
6. <span data-ttu-id="5610d-214">&gt; Actions</span><span class="sxs-lookup"><span data-stu-id="5610d-214">&gt; Actions</span></span>
7. <span data-ttu-id="5610d-215">&gt; Nouvelle règle</span><span class="sxs-lookup"><span data-stu-id="5610d-215">&gt; New Rule</span></span>

<span data-ttu-id="5610d-216">Si votre programme client est hébergé sur une machine virtuelle Azure, consultez </span><span class="sxs-lookup"><span data-stu-id="5610d-216">If your client program is hosted on an Azure virtual machine (VM), you should read:</span></span><br/><span data-ttu-id="5610d-217">[Ports au-delà de 1433 pour ADO .NET 4.5 et SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span><span class="sxs-lookup"><span data-stu-id="5610d-217">[Ports beyond 1433 for ADO.NET 4.5 and SQL Database](sql-database-develop-direct-route-ports-adonet-v12.md).</span></span>

<span data-ttu-id="5610d-218">Pour obtenir des informations générales sur la configuration des ports et l’adresse IP, voir [Pare-feu Azure SQL Database](sql-database-firewall-configure.md)</span><span class="sxs-lookup"><span data-stu-id="5610d-218">For background information about cofiguration of ports and IP address, see: [Azure SQL Database firewall](sql-database-firewall-configure.md)</span></span>

<a id="d-connection-ado-net-4-5" name="d-connection-ado-net-4-5"></a>

### <a name="connection-adonet-461"></a><span data-ttu-id="5610d-219">Connexion : ADO.NET 4.6.1</span><span class="sxs-lookup"><span data-stu-id="5610d-219">Connection: ADO.NET 4.6.1</span></span>
<span data-ttu-id="5610d-220">Si votre programme utilise les classes ADO.NET comme **System.Data.SqlClient.SqlConnection** tooconnect tooAzure base de données SQL, nous vous recommandons d’utiliser .NET Framework version 4.6.1 ou une version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="5610d-220">If your program uses ADO.NET classes like **System.Data.SqlClient.SqlConnection** tooconnect tooAzure SQL Database, we recommend that you use .NET Framework version 4.6.1 or higher.</span></span>

<span data-ttu-id="5610d-221">ADO.NET 4.6.1 :</span><span class="sxs-lookup"><span data-stu-id="5610d-221">ADO.NET 4.6.1:</span></span>

* <span data-ttu-id="5610d-222">Pour la base de données SQL Azure, il existe une meilleure fiabilité, lorsque vous ouvrez une connexion à l’aide de hello **SqlConnection.Open** (méthode).</span><span class="sxs-lookup"><span data-stu-id="5610d-222">For Azure SQL Database, there is improved reliability when you open a connection by using hello **SqlConnection.Open** method.</span></span> <span data-ttu-id="5610d-223">Hello **ouvrir** méthode intègre désormais une meilleure mécanismes de nouvelle tentative efforts dans les erreurs de tootransient de réponse, pour certaines erreurs au sein de la période de délai de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-223">hello **Open** method now incorporates best effort retry mechanisms in response tootransient faults, for certain errors within hello Connection Timeout period.</span></span>
* <span data-ttu-id="5610d-224">Prend en charge le regroupement de connexions.</span><span class="sxs-lookup"><span data-stu-id="5610d-224">Supports connection pooling.</span></span> <span data-ttu-id="5610d-225">Cela inclut une vérification efficace qui hello connexion fonctionne objet il donne à votre programme.</span><span class="sxs-lookup"><span data-stu-id="5610d-225">This includes an efficient verification that hello connection object it gives your program is functioning.</span></span>

<span data-ttu-id="5610d-226">Lorsque vous utilisez un objet de connexion à partir d’un pool de connexions, nous recommandons que votre programme Fermez temporairement les connexion hello lorsque vous l’utilisez pas immédiatement.</span><span class="sxs-lookup"><span data-stu-id="5610d-226">When you use a connection object from a connection pool, we recommend that your program temporarily close hello connection when not immediately using it.</span></span> <span data-ttu-id="5610d-227">Ouvrir une connexion n’est pas coûteuse hello création d’une connexion consiste.</span><span class="sxs-lookup"><span data-stu-id="5610d-227">Re-opening a connection is not expensive hello way creating a new connection is.</span></span>

<span data-ttu-id="5610d-228">Si vous utilisez ADO.NET 4.0 ou version antérieure, nous vous conseillons toohello dernière ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="5610d-228">If you are using ADO.NET 4.0 or earlier, we recommend that you upgrade toohello latest ADO.NET.</span></span>

* <span data-ttu-id="5610d-229">Depuis novembre 2015, [ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx)est disponible au téléchargement.</span><span class="sxs-lookup"><span data-stu-id="5610d-229">As of November 2015, you can [download ADO.NET 4.6.1](http://blogs.msdn.com/b/dotnet/archive/2015/11/30/net-framework-4-6-1-is-now-available.aspx).</span></span>

<a id="e-diagnostics-test-utilities-connect" name="e-diagnostics-test-utilities-connect"></a>

## <a name="diagnostics"></a><span data-ttu-id="5610d-230">Diagnostics</span><span class="sxs-lookup"><span data-stu-id="5610d-230">Diagnostics</span></span>
<a id="d-test-whether-utilities-can-connect" name="d-test-whether-utilities-can-connect"></a>

### <a name="diagnostics-test-whether-utilities-can-connect"></a><span data-ttu-id="5610d-231">Diagnostic : vérifier si les utilitaires peuvent se connecter</span><span class="sxs-lookup"><span data-stu-id="5610d-231">Diagnostics: Test whether utilities can connect</span></span>
<span data-ttu-id="5610d-232">Si votre programme échoue tooconnect tooAzure base de données SQL, une option de diagnostic est tooconnect tootry avec un programme de l’utilitaire.</span><span class="sxs-lookup"><span data-stu-id="5610d-232">If your program is failing tooconnect tooAzure SQL Database, one diagnostic option is tootry tooconnect with a utility program.</span></span> <span data-ttu-id="5610d-233">Dans l’idéal, l’utilitaire de hello se connecte à l’aide de hello même bibliothèque que votre programme utilise.</span><span class="sxs-lookup"><span data-stu-id="5610d-233">Ideally hello utility would connect by using hello same library that your program uses.</span></span>

<span data-ttu-id="5610d-234">Sur un ordinateur Windows, vous pouvez essayer ces utilitaires :</span><span class="sxs-lookup"><span data-stu-id="5610d-234">On any Windows computer, you can try these utilities:</span></span>

* <span data-ttu-id="5610d-235">SQL Server Management Studio (ssms.exe), qui se connecte à l’aide d’ADO.NET.</span><span class="sxs-lookup"><span data-stu-id="5610d-235">SQL Server Management Studio (ssms.exe), which connects by using ADO.NET.</span></span>
* <span data-ttu-id="5610d-236">sqlcmd.exe, qui se connecte à l’aide d’ [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span><span class="sxs-lookup"><span data-stu-id="5610d-236">sqlcmd.exe, which connects by using [ODBC](http://msdn.microsoft.com/library/jj730308.aspx).</span></span>

<span data-ttu-id="5610d-237">Une fois connecté, faites un test avec une courte requête SQL SELECT.</span><span class="sxs-lookup"><span data-stu-id="5610d-237">Once connected, test whether a short SQL SELECT query works.</span></span>

<a id="f-diagnostics-check-open-ports" name="f-diagnostics-check-open-ports"></a>

### <a name="diagnostics-check-hello-open-ports"></a><span data-ttu-id="5610d-238">Diagnostics : Vérifiez les ports ouverts hello</span><span class="sxs-lookup"><span data-stu-id="5610d-238">Diagnostics: Check hello open ports</span></span>
<span data-ttu-id="5610d-239">Supposons que vous pensez que les tentatives de connexion échouent en raison de problèmes de tooport.</span><span class="sxs-lookup"><span data-stu-id="5610d-239">Suppose you suspect that connection attempts are failing due tooport issues.</span></span> <span data-ttu-id="5610d-240">Sur votre ordinateur, vous pouvez exécuter un utilitaire qui génère un rapport sur les configurations de port hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-240">On your computer you can run a utility that reports on hello port configurations.</span></span>

<span data-ttu-id="5610d-241">Sur Linux hello utilitaires suivants peuvent être utiles :</span><span class="sxs-lookup"><span data-stu-id="5610d-241">On Linux hello following utilities might be helpful:</span></span>

* `netstat -nap`
* `nmap -sS -O 127.0.0.1`
  * <span data-ttu-id="5610d-242">(Remplacez hello exemple valeur toobe votre adresse IP.)</span><span class="sxs-lookup"><span data-stu-id="5610d-242">(Change hello example value toobe your IP address.)</span></span>

<span data-ttu-id="5610d-243">Sur Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utilitaire peut être utile.</span><span class="sxs-lookup"><span data-stu-id="5610d-243">On Windows hello [PortQry.exe](http://www.microsoft.com/download/details.aspx?id=17148) utility might be helpful.</span></span> <span data-ttu-id="5610d-244">Voici une exécution de l’exemple qui interrogées situation de port hello sur un serveur de base de données SQL Azure, et qui a été exécuté sur un ordinateur portable :</span><span class="sxs-lookup"><span data-stu-id="5610d-244">Here is an example execution that queried hello port situation on an Azure SQL Database server, and which was run on a laptop computer:</span></span>

```
[C:\Users\johndoe\]
>> portqry.exe -n johndoesvr9.database.windows.net -p tcp -e 1433

Querying target system called:
 johndoesvr9.database.windows.net

Attempting tooresolve name tooIP address...
Name resolved too23.100.117.95

querying...
TCP port 1433 (ms-sql-s service): LISTENING

[C:\Users\johndoe\]
>>
```


<a id="g-diagnostics-log-your-errors" name="g-diagnostics-log-your-errors"></a>

### <a name="diagnostics-log-your-errors"></a><span data-ttu-id="5610d-245">Diagnostic : consignation des erreurs dans un journal</span><span class="sxs-lookup"><span data-stu-id="5610d-245">Diagnostics: Log your errors</span></span>
<span data-ttu-id="5610d-246">Un problème intermittent est parfois mieux diagnostiqué par la détection d’une tendance générale observée sur plusieurs jours ou semaines.</span><span class="sxs-lookup"><span data-stu-id="5610d-246">An intermittent problem is sometimes best diagnosed by detection of a general pattern over days or weeks.</span></span>

<span data-ttu-id="5610d-247">Votre client peut aider à consigner toutes les erreurs qu’il rencontre un diagnostic.</span><span class="sxs-lookup"><span data-stu-id="5610d-247">Your client can assist in a diagnosis by logging all errors it encounters.</span></span> <span data-ttu-id="5610d-248">Vous pouvez être entrées de journal en mesure de toocorrelate hello avec les données d’erreur base de données SQL Azure se connecte lui-même en interne.</span><span class="sxs-lookup"><span data-stu-id="5610d-248">You might be able toocorrelate hello log entries with error data that Azure SQL Database logs itself internally.</span></span>

<span data-ttu-id="5610d-249">Enterprise Library 6 (EntLib60) offre tooassist de classes managée .NET avec la journalisation :</span><span class="sxs-lookup"><span data-stu-id="5610d-249">Enterprise Library 6 (EntLib60) offers .NET managed classes tooassist with logging:</span></span>

* [<span data-ttu-id="5610d-250">5 - en tant que simple comme relevant hors tension un journal : à l’aide de hello bloc d’Application de journalisation</span><span class="sxs-lookup"><span data-stu-id="5610d-250">5 - As Easy As Falling Off a Log: Using hello Logging Application Block</span></span>](http://msdn.microsoft.com/library/dn440731.aspx)

<a id="h-diagnostics-examine-logs-errors" name="h-diagnostics-examine-logs-errors"></a>

### <a name="diagnostics-examine-system-logs-for-errors"></a><span data-ttu-id="5610d-251">Diagnostics : examinez les journaux d’erreur système</span><span class="sxs-lookup"><span data-stu-id="5610d-251">Diagnostics: Examine system logs for errors</span></span>
<span data-ttu-id="5610d-252">Voici certaines instructions Transact-SQL SELECT qui permettent d’interroger les journaux d’erreur et d’autres informations.</span><span class="sxs-lookup"><span data-stu-id="5610d-252">Here are some Transact-SQL SELECT statements that query logs of error and other information.</span></span>

| <span data-ttu-id="5610d-253">Interrogation de journaux</span><span class="sxs-lookup"><span data-stu-id="5610d-253">Query of log</span></span> | <span data-ttu-id="5610d-254">Description</span><span class="sxs-lookup"><span data-stu-id="5610d-254">Description</span></span> |
|:--- |:--- |
| `SELECT e.*`<br/>`FROM sys.event_log AS e`<br/>`WHERE e.database_name = 'myDbName'`<br/>`AND e.event_category = 'connectivity'`<br/>`AND 2 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, e.end_time, GetUtcDate())`<br/>`ORDER BY e.event_category,`<br/>&nbsp;&nbsp;`e.event_type, e.end_time;` |<span data-ttu-id="5610d-255">Hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) affichage propose des informations sur les événements individuels, y compris celles qui peut provoquer des erreurs temporaires ou des défaillances de connectivité.</span><span class="sxs-lookup"><span data-stu-id="5610d-255">hello [sys.event_log](http://msdn.microsoft.com/library/dn270018.aspx) view offers information about individual events, including some that can cause transient errors or connectivity failures.</span></span><br/><br/><span data-ttu-id="5610d-256">Dans l’idéal, vous pouvez mettre en corrélation hello **heure_début** ou **end_time** valeurs avec des informations lorsque votre programme client a rencontré des problèmes.</span><span class="sxs-lookup"><span data-stu-id="5610d-256">Ideally you can correlate hello **start_time** or **end_time** values with information about when your client program experienced problems.</span></span><br/><br/><span data-ttu-id="5610d-257">**Conseil :** vous devez vous connecter toohello **master** de base de données toorun cela.</span><span class="sxs-lookup"><span data-stu-id="5610d-257">**TIP:** You must connect toohello **master** database toorun this.</span></span> |
| `SELECT c.*`<br/>`FROM sys.database_connection_stats AS c`<br/>`WHERE c.database_name = 'myDbName'`<br/>`AND 24 >= DateDiff`<br/>&nbsp;&nbsp;`(hour, c.end_time, GetUtcDate())`<br/>`ORDER BY c.end_time;` |<span data-ttu-id="5610d-258">Hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) affichage offre le décompte agrégé des types d’événements de diagnostic supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="5610d-258">hello [sys.database_connection_stats](http://msdn.microsoft.com/library/dn269986.aspx) view offers aggregated counts of event types, for additional diagnostics.</span></span><br/><br/><span data-ttu-id="5610d-259">**Conseil :** vous devez vous connecter toohello **master** de base de données toorun cela.</span><span class="sxs-lookup"><span data-stu-id="5610d-259">**TIP:** You must connect toohello **master** database toorun this.</span></span> |

<a id="d-search-for-problem-events-in-the-sql-database-log" name="d-search-for-problem-events-in-the-sql-database-log"></a>

### <a name="diagnostics-search-for-problem-events-in-hello-sql-database-log"></a><span data-ttu-id="5610d-260">Diagnostics : Rechercher des événements de problème dans le journal de base de données SQL hello</span><span class="sxs-lookup"><span data-stu-id="5610d-260">Diagnostics: Search for problem events in hello SQL Database log</span></span>
<span data-ttu-id="5610d-261">Vous pouvez rechercher des entrées sur les événements du problème dans le journal hello de base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="5610d-261">You can search for entries about problem events in hello log of Azure SQL Database.</span></span> <span data-ttu-id="5610d-262">Essayez de hello suivant l’instruction Transact-SQL SELECT Bonjour **master** base de données :</span><span class="sxs-lookup"><span data-stu-id="5610d-262">Try hello following Transact-SQL SELECT statement in hello **master** database:</span></span>

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


#### <a name="a-few-returned-rows-from-sysfnxetelemetryblobtargetreadfile"></a><span data-ttu-id="5610d-263">quelques-unes d’entre elles ont renvoyé des lignes de sys.fn_xe_telemetry_blob_target_read_file</span><span class="sxs-lookup"><span data-stu-id="5610d-263">A few returned rows from sys.fn_xe_telemetry_blob_target_read_file</span></span>
<span data-ttu-id="5610d-264">Vous trouverez plus loin une ligne renvoyée qui ressemble à ce qui suit .</span><span class="sxs-lookup"><span data-stu-id="5610d-264">Next is what a returned row might look like.</span></span> <span data-ttu-id="5610d-265">les valeurs null Hello indiquées ne sont pas souvent null dans d’autres lignes.</span><span class="sxs-lookup"><span data-stu-id="5610d-265">hello null values shown are often not null in other rows.</span></span>

```
object_name                   timestamp                    error  state  is_success  database_name

database_xml_deadlock_report  2015-10-16 20:28:01.0090000  NULL   NULL   NULL        AdventureWorks
```


<a id="l-enterprise-library-6" name="l-enterprise-library-6"></a>

## <a name="enterprise-library-6"></a><span data-ttu-id="5610d-266">Enterprise Library 6</span><span class="sxs-lookup"><span data-stu-id="5610d-266">Enterprise Library 6</span></span>
<span data-ttu-id="5610d-267">Enterprise Library 6 (EntLib60) est une infrastructure de classes .NET qui vous permet d’implémenter des clients robustes de services de cloud computing, y compris service de base de données SQL Azure hello.</span><span class="sxs-lookup"><span data-stu-id="5610d-267">Enterprise Library 6 (EntLib60) is a framework of .NET classes that helps you implement robust clients of cloud services, one of which is hello Azure SQL Database service.</span></span> <span data-ttu-id="5610d-268">Vous pouvez localiser la zone tooeach dédié de rubriques dans lequel EntLib60 peut aider en premier sur le site :</span><span class="sxs-lookup"><span data-stu-id="5610d-268">You can locate topics dedicated tooeach area in which EntLib60 can assist by first visiting:</span></span>

* [<span data-ttu-id="5610d-269">Enterprise Library 6 - avril 2013</span><span class="sxs-lookup"><span data-stu-id="5610d-269">Enterprise Library 6 - April 2013</span></span>](http://msdn.microsoft.com/library/dn169621%28v=pandp.60%29.aspx)

<span data-ttu-id="5610d-270">La logique de nouvelle tentative pour la gestion des erreurs temporaires est un domaine où EntLib60 peut être utile :</span><span class="sxs-lookup"><span data-stu-id="5610d-270">Retry logic for handling transient errors is one area in which EntLib60 can assist:</span></span>

* [<span data-ttu-id="5610d-271">4 - perseverance, le Secret de toutes les luttes : à l’aide de hello bloc applicatif de défaillance de gestion</span><span class="sxs-lookup"><span data-stu-id="5610d-271">4 - Perseverance, Secret of All Triumphs: Using hello Transient Fault Handling Application Block</span></span>](http://msdn.microsoft.com/library/dn440719%28v=pandp.60%29.aspx)

> [!NOTE]
> <span data-ttu-id="5610d-272">Hello code source pour EntLib60 est disponible pour le public [télécharger](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span><span class="sxs-lookup"><span data-stu-id="5610d-272">hello source code for EntLib60 is available for public [download](http://go.microsoft.com/fwlink/p/?LinkID=290898).</span></span> <span data-ttu-id="5610d-273">Microsoft n’a aucune fonctionnalité supplémentaire de plans toomake mises à jour ou la maintenance des mises à jour tooEntLib.</span><span class="sxs-lookup"><span data-stu-id="5610d-273">Microsoft has no plans toomake further feature updates or maintenance updates tooEntLib.</span></span>
> 
> 

<a id="entlib60-classes-for-transient-errors-and-retry" name="entlib60-classes-for-transient-errors-and-retry"></a>

### <a name="entlib60-classes-for-transient-errors-and-retry"></a><span data-ttu-id="5610d-274">Classes EntLib60 pour les erreurs temporaires et les nouvelles tentatives</span><span class="sxs-lookup"><span data-stu-id="5610d-274">EntLib60 classes for transient errors and retry</span></span>
<span data-ttu-id="5610d-275">Hello EntLib60 classes suivantes est particulièrement utile pour la logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="5610d-275">hello following EntLib60 classes are particularly useful for retry logic.</span></span> <span data-ttu-id="5610d-276">Tous ces sont dans ou sont encore plus sous, hello d’espace de noms **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span><span class="sxs-lookup"><span data-stu-id="5610d-276">All these  are in, or are further under, hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:</span></span>

<span data-ttu-id="5610d-277">*Dans l’espace de noms hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span><span class="sxs-lookup"><span data-stu-id="5610d-277">*In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling**:*</span></span>

* <span data-ttu-id="5610d-278">**RetryPolicy**</span><span class="sxs-lookup"><span data-stu-id="5610d-278">**RetryPolicy** class</span></span>
  
  * <span data-ttu-id="5610d-279">**ExecuteAction**</span><span class="sxs-lookup"><span data-stu-id="5610d-279">**ExecuteAction** method</span></span>
* <span data-ttu-id="5610d-280">**ExponentialBackoff**</span><span class="sxs-lookup"><span data-stu-id="5610d-280">**ExponentialBackoff** class</span></span>
* <span data-ttu-id="5610d-281">**SqlDatabaseTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="5610d-281">**SqlDatabaseTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="5610d-282">**ReliableSqlConnection**</span><span class="sxs-lookup"><span data-stu-id="5610d-282">**ReliableSqlConnection** class</span></span>
  
  * <span data-ttu-id="5610d-283">**ExecuteCommand**</span><span class="sxs-lookup"><span data-stu-id="5610d-283">**ExecuteCommand** method</span></span>

<span data-ttu-id="5610d-284">Dans l’espace de noms hello **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span><span class="sxs-lookup"><span data-stu-id="5610d-284">In hello namespace **Microsoft.Practices.EnterpriseLibrary.TransientFaultHandling.TestSupport**:</span></span>

* <span data-ttu-id="5610d-285">**AlwaysTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="5610d-285">**AlwaysTransientErrorDetectionStrategy** class</span></span>
* <span data-ttu-id="5610d-286">**NeverTransientErrorDetectionStrategy**</span><span class="sxs-lookup"><span data-stu-id="5610d-286">**NeverTransientErrorDetectionStrategy** class</span></span>

<span data-ttu-id="5610d-287">Voici tooinformation liens sur EntLib60 :</span><span class="sxs-lookup"><span data-stu-id="5610d-287">Here are links tooinformation about EntLib60:</span></span>

* <span data-ttu-id="5610d-288">Libre [télécharger de Book : tooMicrosoft Guide du développeur Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span><span class="sxs-lookup"><span data-stu-id="5610d-288">Free [Book Download: Developer's Guide tooMicrosoft Enterprise Library, 2nd Edition](http://www.microsoft.com/download/details.aspx?id=41145)</span></span>
* <span data-ttu-id="5610d-289">Meilleures pratiques : [Conseils généraux sur les nouvelles tentatives](../best-practices-retry-general.md) comprend une excellente présentation approfondie de la logique de nouvelle tentative.</span><span class="sxs-lookup"><span data-stu-id="5610d-289">Best practices: [Retry general guidance](../best-practices-retry-general.md) has an excellent in-depth discussion of retry logic.</span></span>
* <span data-ttu-id="5610d-290">Téléchargement NuGet de [Bibliothèque d’entreprise - Bloc applicatif de gestion des erreurs 6.0 temporaires de Microsoft](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span><span class="sxs-lookup"><span data-stu-id="5610d-290">NuGet download of [Enterprise Library - Transient Fault Handling application block 6.0](http://www.nuget.org/packages/EnterpriseLibrary.TransientFaultHandling/)</span></span>

<a id="entlib60-the-logging-block" name="entlib60-the-logging-block"></a>

### <a name="entlib60-hello-logging-block"></a><span data-ttu-id="5610d-291">EntLib60 : bloc de journalisation hello</span><span class="sxs-lookup"><span data-stu-id="5610d-291">EntLib60: hello logging block</span></span>
* <span data-ttu-id="5610d-292">bloc de journalisation Hello est une solution souple et configurable qui vous permet de :</span><span class="sxs-lookup"><span data-stu-id="5610d-292">hello Logging block is a highly flexible and configurable solution that allows you to:</span></span>
  
  * <span data-ttu-id="5610d-293">Créer et stocker des messages du journal dans de nombreux emplacements.</span><span class="sxs-lookup"><span data-stu-id="5610d-293">Create and store log messages in a wide variety of locations.</span></span>
  * <span data-ttu-id="5610d-294">Classer et filtrer les messages.</span><span class="sxs-lookup"><span data-stu-id="5610d-294">Categorize and filter messages.</span></span>
  * <span data-ttu-id="5610d-295">Recueillir des informations contextuelles utiles pour le débogage et le suivi, ainsi que pour les exigences d’audit et de journalisation en général.</span><span class="sxs-lookup"><span data-stu-id="5610d-295">Collect contextual information that is useful for debugging and tracing, as well as for auditing and general logging requirements.</span></span>
* <span data-ttu-id="5610d-296">bloc de journalisation Hello résume hello journalisation des fonctionnalités à partir de la destination du journal hello afin que le code de l’application hello est cohérent, quelle que soit l’emplacement de hello et le type de banque de journalisation hello cible.</span><span class="sxs-lookup"><span data-stu-id="5610d-296">hello Logging block abstracts hello logging functionality from hello log destination so that hello application code is consistent, irrespective of hello location and type of hello target logging store.</span></span>

<span data-ttu-id="5610d-297">Pour plus d’informations, consultez : [5 - en tant que simple comme relevant hors tension un journal : à l’aide de hello bloc d’Application de journalisation](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span><span class="sxs-lookup"><span data-stu-id="5610d-297">For details see: [5 - As Easy As Falling Off a Log: Using hello Logging Application Block](https://msdn.microsoft.com/library/dn440731%28v=pandp.60%29.aspx)</span></span>

<a id="entlib60-istransient-method-source-code" name="entlib60-istransient-method-source-code"></a>

### <a name="entlib60-istransient-method-source-code"></a><span data-ttu-id="5610d-298">Code source de la méthode EntLib60 IsTransient</span><span class="sxs-lookup"><span data-stu-id="5610d-298">EntLib60 IsTransient method source code</span></span>
<span data-ttu-id="5610d-299">Ensuite, à partir de hello **SqlDatabaseTransientErrorDetectionStrategy** de classe, est le code source hello c# hello **IsTransient** (méthode).</span><span class="sxs-lookup"><span data-stu-id="5610d-299">Next, from hello **SqlDatabaseTransientErrorDetectionStrategy** class, is hello C# source code for hello **IsTransient** method.</span></span> <span data-ttu-id="5610d-300">code source de Hello clarifie les erreurs ont été analysés toobe temporaire et worthy de nouvelle tentative, à compter d’avril 2013.</span><span class="sxs-lookup"><span data-stu-id="5610d-300">hello source code clarifies which errors were considered toobe transient and worthy of retry, as of April 2013.</span></span>

<span data-ttu-id="5610d-301">Nombreuses **//comment** lignes ont été supprimées de cette lisibilité tooemphasize de copie.</span><span class="sxs-lookup"><span data-stu-id="5610d-301">Numerous **//comment** lines have been removed from this copy tooemphasize readability.</span></span>

```
public bool IsTransient(Exception ex)
{
  if (ex != null)
  {
    SqlException sqlException;
    if ((sqlException = ex as SqlException) != null)
    {
      // Enumerate through all errors found in hello exception.
      foreach (SqlError err in sqlException.Errors)
      {
        switch (err.Number)
        {
            // SQL Error Code: 40501
            // hello service is currently busy. Retry hello request after 10 seconds.
            // Code: (reason code toobe decoded).
          case ThrottlingCondition.ThrottlingErrorNumber:
            // Decode hello reason code from hello error message to
            // determine hello grounds for throttling.
            var condition = ThrottlingCondition.FromError(err);

            // Attach hello decoded values as additional attributes to
            // hello original SQL exception.
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
            // hello instance of SQL Server you attempted tooconnect to
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


## <a name="next-steps"></a><span data-ttu-id="5610d-302">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="5610d-302">Next steps</span></span>
* <span data-ttu-id="5610d-303">Pour le dépannage d’autres problèmes de connexion de base de données SQL Azure courants, visitez [connexion de résoudre les problèmes tooAzure base de données SQL](sql-database-troubleshoot-common-connection-issues.md).</span><span class="sxs-lookup"><span data-stu-id="5610d-303">For troubleshooting other common Azure SQL Database connection issues, visit [Troubleshoot connection issues tooAzure SQL Database](sql-database-troubleshoot-common-connection-issues.md).</span></span>
* [<span data-ttu-id="5610d-304">Regroupement de connexions SQL Server (ADO.NET)</span><span class="sxs-lookup"><span data-stu-id="5610d-304">SQL Server Connection Pooling (ADO.NET)</span></span>](http://msdn.microsoft.com/library/8xx3tyca.aspx)
* [<span data-ttu-id="5610d-305">*Une nouvelle tentative* est une Apache 2.0 concédé sous licence général d’une nouvelle tentative de la bibliothèque, écrite **Python**, tâche de hello toosimplify d’ajout de toojust de comportement de nouvelle tentative sur quoi que ce soit.</span><span class="sxs-lookup"><span data-stu-id="5610d-305">*Retrying* is an Apache 2.0 licensed general-purpose retrying library, written in **Python**, toosimplify hello task of adding retry behavior toojust about anything.</span></span>](https://pypi.python.org/pypi/retrying)

