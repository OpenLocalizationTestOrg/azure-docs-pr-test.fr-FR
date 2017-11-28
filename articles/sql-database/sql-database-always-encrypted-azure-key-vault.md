---
title: "Always Encrypted : SQL Database - Azure Key Vault | Microsoft Docs"
description: "Cet article vous explique comment toosecure des données sensibles dans une base de données SQL à l’aide du chiffrement de données hello Assistant Always Encrypted dans SQL Server Management Studio. Il contient également des instructions qui vous indiquent comment toostore chaque clé de chiffrement dans Azure Key Vault."
keywords: "chiffrement des données, clé de chiffrement, chiffrement cloud"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a><span data-ttu-id="0bd1f-105">Chiffrement intégral : Protéger les données sensibles dans Base de données SQL et stocker vos clés de chiffrement dans Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="0bd1f-105">Always Encrypted: Protect sensitive data in SQL Database and store your encryption keys in Azure Key Vault</span></span>

<span data-ttu-id="0bd1f-106">Cet article vous explique comment toosecure des données sensibles dans un SQL de base de données avec le chiffrement de données à l’aide de hello [Assistant Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx) dans [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-106">This article shows you how toosecure sensitive data in a SQL database with data encryption using hello [Always Encrypted Wizard](https://msdn.microsoft.com/library/mt459280.aspx) in [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx).</span></span> <span data-ttu-id="0bd1f-107">Il contient également des instructions qui vous indiquent comment toostore chaque clé de chiffrement dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-107">It also includes instructions that will show you how toostore each encryption key in Azure Key Vault.</span></span>

<span data-ttu-id="0bd1f-108">Always Encrypted est une nouvelle technologie de chiffrement de données dans la base de données SQL Azure et SQL Server qui vous aide à protéger les données sensibles au repos sur le serveur de hello, lors de déplacements entre client et serveur, et pendant que les données de salutation sont en cours d’utilisation.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-108">Always Encrypted is a new data encryption technology in Azure SQL Database and SQL Server that helps protect sensitive data at rest on hello server, during movement between client and server, and while hello data is in use.</span></span> <span data-ttu-id="0bd1f-109">Always Encrypted garantit que les données sensibles n’apparaissent jamais en texte clair à l’intérieur du système de base de données hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-109">Always Encrypted ensures that sensitive data never appears as plaintext inside hello database system.</span></span> <span data-ttu-id="0bd1f-110">Après avoir configuré le chiffrement des données, uniquement les applications clientes ou les serveurs d’applications qui ont des clés d’accès toohello peuvent accéder aux données de texte en clair.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-110">After you configure data encryption, only client applications or app servers that have access toohello keys can access plaintext data.</span></span> <span data-ttu-id="0bd1f-111">Pour plus d’informations, consultez [Chiffrement intégral (moteur de base de données)](https://msdn.microsoft.com/library/mt163865.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-111">For detailed information, see [Always Encrypted (Database Engine)](https://msdn.microsoft.com/library/mt163865.aspx).</span></span>

<span data-ttu-id="0bd1f-112">Après avoir configuré hello toouse de base de données Always Encrypted, vous allez créer une application cliente en c# avec toowork de Visual Studio avec des données hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-112">After you configure hello database toouse Always Encrypted, you will create a client application in C# with Visual Studio toowork with hello encrypted data.</span></span>

<span data-ttu-id="0bd1f-113">Suivez les étapes de hello dans cet article et découvrez comment tooset d’Always Encrypted pour une base de données SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-113">Follow hello steps in this article and learn how tooset up Always Encrypted for an Azure SQL database.</span></span> <span data-ttu-id="0bd1f-114">Dans cet article, vous allez apprendre des tâches de hello tooperform suivant :</span><span class="sxs-lookup"><span data-stu-id="0bd1f-114">In this article you will learn how tooperform hello following tasks:</span></span>

* <span data-ttu-id="0bd1f-115">Utilisez l’Assistant Always Encrypted hello dans SSMS toocreate [clés Always Encrypted](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-115">Use hello Always Encrypted wizard in SSMS toocreate [Always Encrypted keys](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).</span></span>
  * <span data-ttu-id="0bd1f-116">Créer une [clé principale de colonne (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-116">Create a [column master key (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).</span></span>
  * <span data-ttu-id="0bd1f-117">Créer une [clé de chiffrement de colonne (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-117">Create a [column encryption key (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).</span></span>
* <span data-ttu-id="0bd1f-118">Créer une table de base de données et chiffrer des colonnes.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-118">Create a database table and encrypt columns.</span></span>
* <span data-ttu-id="0bd1f-119">Créer une application qui insère, sélectionne et affiche les données des colonnes de hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-119">Create an application that inserts, selects, and displays data from hello encrypted columns.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bd1f-120">Composants requis</span><span class="sxs-lookup"><span data-stu-id="0bd1f-120">Prerequisites</span></span>
<span data-ttu-id="0bd1f-121">Pour ce didacticiel, vous devez disposer des éléments suivants :</span><span class="sxs-lookup"><span data-stu-id="0bd1f-121">For this tutorial, you'll need:</span></span>

* <span data-ttu-id="0bd1f-122">Un compte et un abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-122">An Azure account and subscription.</span></span> <span data-ttu-id="0bd1f-123">Si vous n’en avez pas, inscrivez-vous pour un [essai gratuit](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-123">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="0bd1f-124">[SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx) , version 13.0.700.242 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-124">[SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) version 13.0.700.242 or later.</span></span>
* <span data-ttu-id="0bd1f-125">[.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) ou version ultérieure (sur l’ordinateur client de hello).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-125">[.NET Framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) or later (on hello client computer).</span></span>
* <span data-ttu-id="0bd1f-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-126">[Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx).</span></span>
* <span data-ttu-id="0bd1f-127">[Azure PowerShell](/powershell/azure/overview), version 1.0 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-127">[Azure PowerShell](/powershell/azure/overview), version  1.0 or later.</span></span> <span data-ttu-id="0bd1f-128">Type **(Get-Module - ListAvailable azure). Version** toosee quelle version de PowerShell vous sont en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-128">Type **(Get-Module azure -ListAvailable).Version** toosee what version of PowerShell you are running.</span></span>

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a><span data-ttu-id="0bd1f-129">Activer votre service de base de données SQL client application tooaccess hello</span><span class="sxs-lookup"><span data-stu-id="0bd1f-129">Enable your client application tooaccess hello SQL Database service</span></span>
<span data-ttu-id="0bd1f-130">Vous devez activer votre service de base de données SQL client application tooaccess hello en configurant l’authentification obligatoire hello et hello lors de l’acquisition *ClientId* et *Secret* que vous devez tooauthenticate votre application Bonjour suivant de code.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-130">You must enable your client application tooaccess hello SQL Database service by setting up hello required authentication and acquiring hello *ClientId* and *Secret* that you will need tooauthenticate your application in hello following code.</span></span>

1. <span data-ttu-id="0bd1f-131">Ouvrez hello [portail Azure classic](http://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-131">Open hello [Azure classic portal](http://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="0bd1f-132">Sélectionnez **Active Directory** et cliquez sur une instance Active Directory hello que votre application utilisera.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-132">Select **Active Directory** and click hello Active Directory instance that your application will use.</span></span>
3. <span data-ttu-id="0bd1f-133">Cliquez sur **Applications**, puis sur **AJOUTER**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-133">Click **Applications**, and then click **ADD**.</span></span>
4. <span data-ttu-id="0bd1f-134">Tapez un nom pour votre application (par exemple : *myClientApp*), sélectionnez **APPLICATION WEB**, puis cliquez sur hello flèche toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-134">Type a name for your application (for example: *myClientApp*), select **WEB APPLICATION**, and click hello arrow toocontinue.</span></span>
5. <span data-ttu-id="0bd1f-135">Pourquoi **URL de connexion** et **URI ID d’application** vous pouvez taper une URL valide (par exemple, *http://myClientApp*) et continuer.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-135">For hello **SIGN-ON URL** and **APP ID URI** you can type a valid URL (for example, *http://myClientApp*) and continue.</span></span>
6. <span data-ttu-id="0bd1f-136">Cliquez sur **CONFIGURER**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-136">Click **CONFIGURE**.</span></span>
7. <span data-ttu-id="0bd1f-137">Copiez votre **ID CLIENT**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-137">Copy your **CLIENT ID**.</span></span> <span data-ttu-id="0bd1f-138">(vous aurez besoin cette valeur dans votre code ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-138">(You will need this value in your code later.)</span></span>
8. <span data-ttu-id="0bd1f-139">Bonjour **clés** section, sélectionnez **1 an** de hello **sélectionner une durée** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-139">In hello **keys** section, select **1 year** from hello  **Select duration** drop-down list.</span></span> <span data-ttu-id="0bd1f-140">(Vous allez copier la clé de hello après avoir enregistré à l’étape 13.)</span><span class="sxs-lookup"><span data-stu-id="0bd1f-140">(You will copy hello key after you save in step 13.)</span></span>
9. <span data-ttu-id="0bd1f-141">Faites défiler et cliquez sur **Ajouter une application**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-141">Scroll down and click **Add application**.</span></span>
10. <span data-ttu-id="0bd1f-142">Laissez **afficher** défini trop**Microsoft Apps** et sélectionnez **API de gestion Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-142">Leave **SHOW** set too**Microsoft Apps** and select **Microsoft Azure Service Management API**.</span></span> <span data-ttu-id="0bd1f-143">Cliquez sur hello coche toocontinue.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-143">Click hello checkmark toocontinue.</span></span>
11. <span data-ttu-id="0bd1f-144">Sélectionnez **accéder à la gestion des services Azure...**  de hello **autorisations déléguées** liste déroulante.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-144">Select **Access Azure Service Management...** from hello **Delegated Permissions** drop-down list.</span></span>
12. <span data-ttu-id="0bd1f-145">Cliquez sur **ENREGISTRER**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-145">Click **SAVE**.</span></span>
13. <span data-ttu-id="0bd1f-146">Après avoir hello de sauvegarde se termine, copiez la valeur de clé de hello Bonjour **clés** section.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-146">After hello save finishes, copy hello key value in hello **keys** section.</span></span> <span data-ttu-id="0bd1f-147">(vous aurez besoin cette valeur dans votre code ultérieurement).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-147">(You will need this value in your code later.)</span></span>

## <a name="create-a-key-vault-toostore-your-keys"></a><span data-ttu-id="0bd1f-148">Créer un coffre de clés de toostore vos clés</span><span class="sxs-lookup"><span data-stu-id="0bd1f-148">Create a key vault toostore your keys</span></span>
<span data-ttu-id="0bd1f-149">Maintenant que votre application cliente est configurée et que votre ID client, il est temps toocreate un coffre de clés et configurer sa stratégie d’accès pour vous et votre application peuvent accéder aux clés secrètes du coffre hello (clés de chiffrement intégral hello).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-149">Now that your client app is configured and you have your client ID, it's time toocreate a key vault and configure its access policy so you and your application can access hello vault's secrets (hello Always Encrypted keys).</span></span> <span data-ttu-id="0bd1f-150">Hello *créer*, *obtenir*, *liste*, *signe*, *vérifier*, *wrapKey*, et *unwrapKey* autorisations sont requises pour la création d’une nouvelle clé principale de colonne et de configuration de chiffrement avec SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-150">hello *create*, *get*, *list*, *sign*, *verify*, *wrapKey*, and *unwrapKey* permissions are required for creating a new column master key and for setting up encryption with SQL Server Management Studio.</span></span>

<span data-ttu-id="0bd1f-151">Vous pouvez rapidement créer un coffre de clés en exécutant le script suivant de hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-151">You can quickly create a key vault by running hello following script.</span></span> <span data-ttu-id="0bd1f-152">Pour obtenir une explication détaillée de ces applets de commande et plus d’informations sur la création et la configuration d’un coffre de clés, voir [Prise en main d’Azure Key Vault](../key-vault/key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-152">For a detailed explanation of these cmdlets and more information about creating and configuring a key vault, see [Get started with Azure Key Vault](../key-vault/key-vault-get-started.md).</span></span>

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a><span data-ttu-id="0bd1f-153">Créer une base de données SQL vide</span><span class="sxs-lookup"><span data-stu-id="0bd1f-153">Create a blank SQL database</span></span>
1. <span data-ttu-id="0bd1f-154">Connectez-vous à toohello [portail Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-154">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="0bd1f-155">Accédez trop**nouveau** > **données + stockage** > **base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-155">Go too**New** > **Data + Storage** > **SQL Database**.</span></span>
3. <span data-ttu-id="0bd1f-156">Créez une base de données **vide** nommée **Clinique** sur un serveur nouveau ou existant.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-156">Create a **Blank** database named **Clinic** on a new or existing server.</span></span> <span data-ttu-id="0bd1f-157">Pour obtenir des instructions détaillées sur toocreate une base de données hello portail Azure, voir [votre première base de données SQL Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-157">For detailed directions about how toocreate a database in hello Azure portal, see [Your first Azure SQL database](sql-database-get-started-portal.md).</span></span>
   
    ![Créer une base de données vide](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

<span data-ttu-id="0bd1f-159">Vous devez serez hello chaîne de connexion plus loin dans le didacticiel de hello, par conséquent, après avoir créé la base de données hello, parcourir toohello nouvelle clinique de base de données et copie hello chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-159">You will need hello connection string later in hello tutorial, so after you create hello database, browse toohello new  Clinic database and copy hello connection string.</span></span> <span data-ttu-id="0bd1f-160">Vous pouvez obtenir la chaîne de connexion hello à tout moment, mais il est facile toocopy dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-160">You can get hello connection string at any time, but it's easy toocopy it in hello Azure portal.</span></span>

1. <span data-ttu-id="0bd1f-161">Accédez trop**bases de données SQL** > **Clinic** > **afficher les chaînes de connexion de base de données**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-161">Go too**SQL databases** > **Clinic** > **Show database connection strings**.</span></span>
2. <span data-ttu-id="0bd1f-162">Copier la chaîne de connexion hello pour **ADO.NET**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-162">Copy hello connection string for **ADO.NET**.</span></span>
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a><span data-ttu-id="0bd1f-164">Connexion de base de données toohello avec SSMS</span><span class="sxs-lookup"><span data-stu-id="0bd1f-164">Connect toohello database with SSMS</span></span>
<span data-ttu-id="0bd1f-165">Ouvrez SSMS et se connecter toohello server avec base de données de la clinique hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-165">Open SSMS and connect toohello server with hello Clinic database.</span></span>

1. <span data-ttu-id="0bd1f-166">Ouvrez SSMS.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-166">Open SSMS.</span></span> <span data-ttu-id="0bd1f-167">(Accédez trop**Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre si elle n’est pas ouverte.)</span><span class="sxs-lookup"><span data-stu-id="0bd1f-167">(Go too**Connect** > **Database Engine** tooopen hello **Connect tooServer** window if it isn't open.)</span></span>
2. <span data-ttu-id="0bd1f-168">Entrez le nom du serveur et vos informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-168">Enter your server name and credentials.</span></span> <span data-ttu-id="0bd1f-169">nom du serveur Hello se trouve sur le panneau de base de données SQL hello et dans la chaîne de connexion hello que vous avez copiée précédemment.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-169">hello server name can be found on hello SQL database blade and in hello connection string you copied earlier.</span></span> <span data-ttu-id="0bd1f-170">Nom de type hello complète du serveur, y compris *database.windows.net*.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-170">Type hello complete server name, including *database.windows.net*.</span></span>
   
    ![Copier la chaîne de connexion hello](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

<span data-ttu-id="0bd1f-172">Si hello **nouvelle règle de pare-feu** s’affiche, connectez-vous à tooAzure et SSMS permettent de créer une règle de pare-feu pour vous.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-172">If hello **New Firewall Rule** window opens, sign in tooAzure and let SSMS create a new firewall rule for you.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="0bd1f-173">Création d’une table</span><span class="sxs-lookup"><span data-stu-id="0bd1f-173">Create a table</span></span>
<span data-ttu-id="0bd1f-174">Dans cette section, vous allez créer des données patient toohold table.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-174">In this section, you will create a table toohold patient data.</span></span> <span data-ttu-id="0bd1f-175">Il n’est pas initialement chiffré--vous allez configurer le chiffrement dans la section suivante de hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-175">It's not initially encrypted--you will configure encryption in hello next section.</span></span>

1. <span data-ttu-id="0bd1f-176">Développez **Bases de données**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-176">Expand **Databases**.</span></span>
2. <span data-ttu-id="0bd1f-177">Avec le bouton hello **Clinic** de base de données et cliquez sur **nouvelle requête**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-177">Right-click hello **Clinic** database and click **New Query**.</span></span>
3. <span data-ttu-id="0bd1f-178">Hello coller suivant Transact-SQL (T-SQL) dans la nouvelle fenêtre de requête hello et **Execute** il.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-178">Paste hello following Transact-SQL (T-SQL) into hello new query window and **Execute** it.</span></span>

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a><span data-ttu-id="0bd1f-179">Chiffrer des colonnes (configurer le chiffrement intégral)</span><span class="sxs-lookup"><span data-stu-id="0bd1f-179">Encrypt columns (configure Always Encrypted)</span></span>
<span data-ttu-id="0bd1f-180">SSMS fournit un Assistant qui vous permet de facilement configurer Always Encrypted en définissant des colonnes chiffrées, clé principale de colonne hello et clé de chiffrement de colonne pour vous.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-180">SSMS provides a wizard that helps you easily configure Always Encrypted by setting up hello column master key, column encryption key, and encrypted columns for you.</span></span>

1. <span data-ttu-id="0bd1f-181">Développez **Bases de données** > **Clinique** > **Tables**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-181">Expand **Databases** > **Clinic** > **Tables**.</span></span>
2. <span data-ttu-id="0bd1f-182">Avec le bouton hello **Patients** de table et sélectionnez **chiffrer les colonnes** Assistant de chiffrement intégral hello tooopen :</span><span class="sxs-lookup"><span data-stu-id="0bd1f-182">Right-click hello **Patients** table and select **Encrypt Columns** tooopen hello Always Encrypted wizard:</span></span>
   
    ![Chiffrer les colonnes](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

<span data-ttu-id="0bd1f-184">Assistant Always Encrypted Hello comprend les sections suivantes de hello : **sélection de la colonne**, **Configuration de la clé principale de**, **Validation**, et **résumé** .</span><span class="sxs-lookup"><span data-stu-id="0bd1f-184">hello Always Encrypted wizard includes hello following sections: **Column Selection**, **Master Key Configuration**, **Validation**, and **Summary**.</span></span>

### <a name="column-selection"></a><span data-ttu-id="0bd1f-185">Sélection de colonnes</span><span class="sxs-lookup"><span data-stu-id="0bd1f-185">Column Selection</span></span>
<span data-ttu-id="0bd1f-186">Cliquez sur **suivant** sur hello **Introduction** hello tooopen de page **sélection de la colonne** page.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-186">Click **Next** on hello **Introduction** page tooopen hello **Column Selection** page.</span></span> <span data-ttu-id="0bd1f-187">Dans cette page, vous sélectionnerez quelles colonnes vous souhaitez tooencrypt, [hello du type de chiffrement et quelle clé de chiffrement de colonne (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-187">On this page, you will select which columns you want tooencrypt, [hello type of encryption, and what column encryption key (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.</span></span>

<span data-ttu-id="0bd1f-188">Chiffrez les informations **SSN** et **BirthDate** pour chaque patient.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-188">Encrypt **SSN** and **BirthDate** information for each patient.</span></span> <span data-ttu-id="0bd1f-189">Hello SSN colonne utilise le chiffrement déterministe, qui prend en charge les recherches d’égalité, de jointures et de group by.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-189">hello SSN column will use deterministic encryption, which supports equality lookups, joins, and group by.</span></span> <span data-ttu-id="0bd1f-190">colonne de date de naissance Hello utilise le chiffrement aléatoire, qui ne prend pas en charge les opérations.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-190">hello BirthDate column will use randomized encryption, which does not support operations.</span></span>

<span data-ttu-id="0bd1f-191">Ensemble hello **le Type de chiffrement** pour la colonne de hello SSN trop**déterministe** et hello colonne BirthDate trop**aléatoire**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-191">Set hello **Encryption Type** for hello SSN column too**Deterministic** and hello BirthDate column too**Randomized**.</span></span> <span data-ttu-id="0bd1f-192">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-192">Click **Next**.</span></span>

![Chiffrer les colonnes](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a><span data-ttu-id="0bd1f-194">Configuration de la clé principale</span><span class="sxs-lookup"><span data-stu-id="0bd1f-194">Master Key Configuration</span></span>
<span data-ttu-id="0bd1f-195">Hello **Master Key Configuration** page est où vous configurez votre clé CMK et le fournisseur de magasin de clés hello sélectionnez où hello CMK sera stocké.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-195">hello **Master Key Configuration** page is where you set up your CMK and select hello key store provider where hello CMK will be stored.</span></span> <span data-ttu-id="0bd1f-196">Actuellement, vous pouvez stocker une clé CMK dans le magasin de certificats Windows hello, Azure Key Vault ou un module de sécurité matériel (HSM).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-196">Currently, you can store a CMK in hello Windows certificate store, Azure Key Vault, or a hardware security module (HSM).</span></span>

<span data-ttu-id="0bd1f-197">Ce didacticiel montre comment toostore vos clés dans le coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-197">This tutorial shows how toostore your keys in Azure Key Vault.</span></span>

1. <span data-ttu-id="0bd1f-198">Sélectionnez **Azure Key Vault**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-198">Select **Azure Key Vault**.</span></span>
2. <span data-ttu-id="0bd1f-199">Sélectionnez le coffre de clés souhaitée hello à partir de la liste déroulante de hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-199">Select hello desired key vault from hello drop-down list.</span></span>
3. <span data-ttu-id="0bd1f-200">Cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-200">Click **Next**.</span></span>

![Configuration de la clé principale](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a><span data-ttu-id="0bd1f-202">Validation</span><span class="sxs-lookup"><span data-stu-id="0bd1f-202">Validation</span></span>
<span data-ttu-id="0bd1f-203">Vous pouvez chiffrer les colonnes hello maintenant ou enregistrer un toorun de script PowerShell plus tard.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-203">You can encrypt hello columns now or save a PowerShell script toorun later.</span></span> <span data-ttu-id="0bd1f-204">Pour ce didacticiel, sélectionnez **continuer toofinish maintenant** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-204">For this tutorial, select **Proceed toofinish now** and click **Next**.</span></span>

### <a name="summary"></a><span data-ttu-id="0bd1f-205">Résumé</span><span class="sxs-lookup"><span data-stu-id="0bd1f-205">Summary</span></span>
<span data-ttu-id="0bd1f-206">Vérifiez que les paramètres de hello sont correctes, cliquez sur **Terminer** le programme d’installation de toocomplete hello pour Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-206">Verify that hello settings are all correct and click **Finish** toocomplete hello setup for Always Encrypted.</span></span>

![Résumé](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a><span data-ttu-id="0bd1f-208">Vérifier les actions de l’Assistant hello</span><span class="sxs-lookup"><span data-stu-id="0bd1f-208">Verify hello wizard's actions</span></span>
<span data-ttu-id="0bd1f-209">Une fois hello Assistant terminé, votre base de données est configurée pour Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-209">After hello wizard is finished, your database is set up for Always Encrypted.</span></span> <span data-ttu-id="0bd1f-210">Bonjour Bonjour d’Assistant effectué suivant des actions :</span><span class="sxs-lookup"><span data-stu-id="0bd1f-210">hello wizard performed hello following actions:</span></span>

* <span data-ttu-id="0bd1f-211">Création d’une clé principale de colonne et stockage de celle-ci dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-211">Created a column master key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="0bd1f-212">Création d’une clé de chiffrement de colonne et stockage de celle-ci dans Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-212">Created a column encryption key and stored it in Azure Key Vault.</span></span>
* <span data-ttu-id="0bd1f-213">Hello configuré sélectionné des colonnes pour le chiffrement.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-213">Configured hello selected columns for encryption.</span></span> <span data-ttu-id="0bd1f-214">table de Patients Hello a actuellement pas de données, mais toutes les données existantes dans les colonnes hello sélectionné sont désormais chiffrées.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-214">hello Patients table currently has no data, but any existing data in hello selected columns is now encrypted.</span></span>

<span data-ttu-id="0bd1f-215">Vous pouvez vérifier la création de hello de clés hello dans SSMS en développant **Clinic** > **sécurité** > **clés Always Encrypted**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-215">You can verify hello creation of hello keys in SSMS by expanding **Clinic** > **Security** > **Always Encrypted Keys**.</span></span>

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a><span data-ttu-id="0bd1f-216">Créer une application cliente qui fonctionne avec les données de salutation chiffrée</span><span class="sxs-lookup"><span data-stu-id="0bd1f-216">Create a client application that works with hello encrypted data</span></span>
<span data-ttu-id="0bd1f-217">Maintenant que le chiffrement intégral est configuré, vous pouvez générer une application qui effectue *insère* et *sélectionne* sur hello des colonnes chiffrées.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-217">Now that Always Encrypted is set up, you can build an application that performs *inserts* and *selects* on hello encrypted columns.</span></span>  

> [!IMPORTANT]
> <span data-ttu-id="0bd1f-218">Votre application doit utiliser [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objets lors du passage du serveur de toohello de données de texte en clair avec des colonnes toujours chiffrées.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-218">Your application must use [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) objects when passing plaintext data toohello server with Always Encrypted columns.</span></span> <span data-ttu-id="0bd1f-219">La transmission de valeurs littérales sans objets SqlParameter entraînera une exception.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-219">Passing literal values without using SqlParameter objects will result in an exception.</span></span>
> 
> 

1. <span data-ttu-id="0bd1f-220">Ouvrez Visual Studio et créez une **application console** C# (Visual Studio 2015 et versions antérieures) ou une **application console (.NET Framework)** (Visual Studio 2017 et versions ultérieures).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-220">Open Visual Studio and create a new C# **Console Application** (Visual Studio 2015 and earlier) or **Console App (.NET Framework)** (Visual Studio 2017 and later).</span></span> <span data-ttu-id="0bd1f-221">Assurez-vous que votre projet est trop**.NET Framework 4.6** ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-221">Make sure your project is set too**.NET Framework 4.6** or later.</span></span>
2. <span data-ttu-id="0bd1f-222">Projet de hello nom **AlwaysEncryptedConsoleAKVApp** et cliquez sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-222">Name hello project **AlwaysEncryptedConsoleAKVApp** and click **OK**.</span></span>
3. <span data-ttu-id="0bd1f-223">Installer hello suivant les packages NuGet en accédant trop**outils** > **Gestionnaire de Package NuGet** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-223">Install hello following NuGet packages by going too**Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

<span data-ttu-id="0bd1f-224">Exécutez ces deux lignes de code dans la Console du Gestionnaire de Package de hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-224">Run these two lines of code in hello Package Manager Console.</span></span>

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a><span data-ttu-id="0bd1f-225">Modifier votre tooenable de chaîne de connexion Always Encrypted</span><span class="sxs-lookup"><span data-stu-id="0bd1f-225">Modify your connection string tooenable Always Encrypted</span></span>
<span data-ttu-id="0bd1f-226">Cette section explique comment tooenable toujours chiffré dans votre chaîne de connexion de base de données.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-226">This section  explains how tooenable Always Encrypted in your database connection string.</span></span>

<span data-ttu-id="0bd1f-227">tooenable Always Encrypted, vous devez tooadd hello **Column Encryption Setting** connexion tooyour de mot clé de chaîne et la définir trop**activé**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-227">tooenable Always Encrypted, you need tooadd hello **Column Encryption Setting** keyword tooyour connection string and set it too**Enabled**.</span></span>

<span data-ttu-id="0bd1f-228">Vous pouvez définir cette option directement dans la chaîne de connexion hello, ou vous pouvez la définir à l’aide de [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-228">You can set this directly in hello connection string, or you can set it by using [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx).</span></span> <span data-ttu-id="0bd1f-229">exemple d’application Hello Bonjour section suivante montre comment toouse **SqlConnectionStringBuilder**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-229">hello sample application in hello next section shows how toouse **SqlConnectionStringBuilder**.</span></span>

### <a name="enable-always-encrypted-in-hello-connection-string"></a><span data-ttu-id="0bd1f-230">Activer le chiffrement intégral dans la chaîne de connexion hello</span><span class="sxs-lookup"><span data-stu-id="0bd1f-230">Enable Always Encrypted in hello connection string</span></span>
<span data-ttu-id="0bd1f-231">Ajoutez hello suivant de chaîne de connexion mot clé tooyour.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-231">Add hello following keyword tooyour connection string.</span></span>

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a><span data-ttu-id="0bd1f-232">Activer le chiffrement intégral avec le paramètre SqlConnectionStringBuilder</span><span class="sxs-lookup"><span data-stu-id="0bd1f-232">Enable Always Encrypted with SqlConnectionStringBuilder</span></span>
<span data-ttu-id="0bd1f-233">Hello suivant de code montre comment tooenable Always Encrypted en définissant [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) trop[activé](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-233">hello following code shows how tooenable Always Encrypted by setting [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) too[Enabled](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).</span></span>

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a><span data-ttu-id="0bd1f-234">Inscrire le fournisseur de coffre de clés Azure hello</span><span class="sxs-lookup"><span data-stu-id="0bd1f-234">Register hello Azure Key Vault provider</span></span>
<span data-ttu-id="0bd1f-235">Hello de code suivant montre comment tooregister hello fournisseur Azure Key Vault avec le pilote d’ADO.NET hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-235">hello following code shows how tooregister hello Azure Key Vault provider with hello ADO.NET driver.</span></span>

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a><span data-ttu-id="0bd1f-236">Exemple d’application console intégralement chiffrée</span><span class="sxs-lookup"><span data-stu-id="0bd1f-236">Always Encrypted sample console application</span></span>
<span data-ttu-id="0bd1f-237">Cet exemple montre comment :</span><span class="sxs-lookup"><span data-stu-id="0bd1f-237">This sample demonstrates how to:</span></span>

* <span data-ttu-id="0bd1f-238">Modifiez votre tooenable de chaîne de connexion Always Encrypted.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-238">Modify your connection string tooenable Always Encrypted.</span></span>
* <span data-ttu-id="0bd1f-239">Inscrire Azure Key Vault comme fournisseur de magasin de clés de l’application de hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-239">Register Azure Key Vault as hello application's key store provider.</span></span>  
* <span data-ttu-id="0bd1f-240">Insérer des données dans des colonnes de hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-240">Insert data into hello encrypted columns.</span></span>
* <span data-ttu-id="0bd1f-241">Sélectionner un enregistrement en filtrant une valeur spécifique dans une colonne chiffrée.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-241">Select a record by filtering for a specific value in an encrypted column.</span></span>

<span data-ttu-id="0bd1f-242">Remplacez le contenu hello de **Program.cs** avec hello suivant de code.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-242">Replace hello contents of **Program.cs** with hello following code.</span></span> <span data-ttu-id="0bd1f-243">Remplacez la chaîne de connexion de hello pour la variable de connectionString global hello dans la ligne hello qui précède directement la méthode Main hello avec votre chaîne de connexion valide à partir de hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-243">Replace hello connection string for hello global connectionString variable in hello line that directly precedes hello Main method with your valid connection string from hello Azure portal.</span></span> <span data-ttu-id="0bd1f-244">Il s’agit de hello seule modification que vous avez besoin de toomake toothis code.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-244">This is hello only change you need toomake toothis code.</span></span>

<span data-ttu-id="0bd1f-245">Exécuter toosee d’application hello Always Encrypted en action.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-245">Run hello app toosee Always Encrypted in action.</span></span>

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a><span data-ttu-id="0bd1f-246">Vérifiez que les données de salutation sont chiffrées.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-246">Verify that hello data is encrypted</span></span>
<span data-ttu-id="0bd1f-247">Vous pouvez vérifier rapidement le chiffrement des données réelles de hello sur le serveur de hello en interrogeant les données de Patients hello avec SSMS (à l’aide de votre connexion actuelle où **Column Encryption Setting** n’est pas encore activée).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-247">You can quickly check that hello actual data on hello server is encrypted by querying hello Patients data with SSMS (using your current connection where **Column Encryption Setting** is not yet enabled).</span></span>

<span data-ttu-id="0bd1f-248">Exécutez hello suivant de requête de base de données de la clinique hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-248">Run hello following query on hello Clinic database.</span></span>

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

<span data-ttu-id="0bd1f-249">Vous pouvez voir que les colonnes hello chiffré ne contiennent pas toutes les données en texte clair.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-249">You can see that hello encrypted columns do not contain any plaintext data.</span></span>

   ![Nouvelle application de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

<span data-ttu-id="0bd1f-251">toouse SSMS tooaccess hello des données en texte brut, vous pouvez ajouter des hello *paramètre de chiffrement de colonne = activé* connexion toohello de paramètre.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-251">toouse SSMS tooaccess hello plaintext data, you can add hello *Column Encryption Setting=enabled* parameter toohello connection.</span></span>

1. <span data-ttu-id="0bd1f-252">Dans SSMS, cliquez avec le bouton droit sur votre serveur dans **l’Explorateur d’objets**, puis choisissez **Déconnecter**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-252">In SSMS, right-click your server in **Object Explorer** and choose **Disconnect**.</span></span>
2. <span data-ttu-id="0bd1f-253">Cliquez sur **Connect** > **moteur de base de données** tooopen hello **connecter tooServer** fenêtre et cliquez sur **Options**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-253">Click **Connect** > **Database Engine** tooopen hello **Connect tooServer** window and click **Options**.</span></span>
3. <span data-ttu-id="0bd1f-254">Cliquez sur **Paramètres de connexion supplémentaires** et tapez **Column Encryption Setting=enabled**.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-254">Click **Additional Connection Parameters** and type **Column Encryption Setting=enabled**.</span></span>
   
    ![Nouvelle application de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. <span data-ttu-id="0bd1f-256">Exécutez hello suivant de requête de base de données de la clinique hello.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-256">Run hello following query on hello Clinic database.</span></span>
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     <span data-ttu-id="0bd1f-257">Vous pouvez maintenant voir les données de texte en clair hello dans les colonnes hello chiffré.</span><span class="sxs-lookup"><span data-stu-id="0bd1f-257">You can now see hello plaintext data in hello encrypted columns.</span></span>

    ![Nouvelle application de console](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a><span data-ttu-id="0bd1f-259">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0bd1f-259">Next steps</span></span>
<span data-ttu-id="0bd1f-260">Après avoir créé une base de données qui utilise le chiffrement intégral, vous souhaiterez peut-être suivant de hello toodo :</span><span class="sxs-lookup"><span data-stu-id="0bd1f-260">After you create a database that uses Always Encrypted, you may want toodo hello following:</span></span>

* <span data-ttu-id="0bd1f-261">[Faire pivoter et nettoyer vos clés](https://msdn.microsoft.com/library/mt607048.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-261">[Rotate and clean up your keys](https://msdn.microsoft.com/library/mt607048.aspx).</span></span>
* <span data-ttu-id="0bd1f-262">[Migrer des données déjà chiffrées avec le chiffrement intégral](https://msdn.microsoft.com/library/mt621539.aspx).</span><span class="sxs-lookup"><span data-stu-id="0bd1f-262">[Migrate data that is already encrypted with Always Encrypted](https://msdn.microsoft.com/library/mt621539.aspx).</span></span>

## <a name="related-information"></a><span data-ttu-id="0bd1f-263">Informations connexes</span><span class="sxs-lookup"><span data-stu-id="0bd1f-263">Related information</span></span>
* [<span data-ttu-id="0bd1f-264">Chiffrement intégral (développement client)</span><span class="sxs-lookup"><span data-stu-id="0bd1f-264">Always Encrypted (client development)</span></span>](https://msdn.microsoft.com/library/mt147923.aspx)
* [<span data-ttu-id="0bd1f-265">Chiffrement transparent des données</span><span class="sxs-lookup"><span data-stu-id="0bd1f-265">Transparent data encryption</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="0bd1f-266">Chiffrement SQL Server</span><span class="sxs-lookup"><span data-stu-id="0bd1f-266">SQL Server encryption</span></span>](https://msdn.microsoft.com/library/bb510663.aspx)
* [<span data-ttu-id="0bd1f-267">Assistant Chiffrement intégral</span><span class="sxs-lookup"><span data-stu-id="0bd1f-267">Always Encrypted wizard</span></span>](https://msdn.microsoft.com/library/mt459280.aspx)
* [<span data-ttu-id="0bd1f-268">Blog Chiffrement intégral</span><span class="sxs-lookup"><span data-stu-id="0bd1f-268">Always Encrypted blog</span></span>](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

