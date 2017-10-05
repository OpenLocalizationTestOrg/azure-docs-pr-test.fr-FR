---
title: "Déployer un service de fractionnement et de fusion | Microsoft Docs"
description: "Fractionnement et fusion avec les outils de bases de données élastiques"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6e2fea882c248fa095a9d450ed54a7b4e64b45e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="abb87-103">Déployer un service de fractionnement et de fusion</span><span class="sxs-lookup"><span data-stu-id="abb87-103">Deploy a split-merge service</span></span>
<span data-ttu-id="abb87-104">L’outil de fractionnement et de fusion vous permet de déplacer les données entre les différentes bases de données partitionnées.</span><span class="sxs-lookup"><span data-stu-id="abb87-104">The split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="abb87-105">Consultez [Déplacement de données entre des bases de données cloud montées en charge](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="abb87-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-the-split-merge-packages"></a><span data-ttu-id="abb87-106">Téléchargement des packages du service de fractionnement/fusion</span><span class="sxs-lookup"><span data-stu-id="abb87-106">Download the Split-Merge packages</span></span>
1. <span data-ttu-id="abb87-107">Téléchargez la dernière version de NuGet à partir de [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="abb87-107">Download the latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="abb87-108">Ouvrez une invite de commandes et accédez au répertoire où vous avez téléchargé nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="abb87-108">Open a command prompt and navigate to the directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="abb87-109">Le téléchargement inclut les commandes PowerShell.</span><span class="sxs-lookup"><span data-stu-id="abb87-109">The download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="abb87-110">Téléchargez le dernier package de fractionnement/fusion dans le répertoire actif à l’aide de la commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="abb87-110">Download the latest Split-Merge package into the current directory with the below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="abb87-111">Les fichiers sont placés dans un répertoire nommé **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** où *x.x.xxx.x* correspond au numéro de version.</span><span class="sxs-lookup"><span data-stu-id="abb87-111">The files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects the version number.</span></span> <span data-ttu-id="abb87-112">Recherchez les fichiers du service de fractionnement et de fusion dans le sous-répertoire **content\splitmerge\service** et les scripts PowerShell de fractionnement et de fusion (ainsi que les .dll clients requis) dans le sous-répertoire **content\splitmerge\powershell**.</span><span class="sxs-lookup"><span data-stu-id="abb87-112">Find the split-merge Service files in the **content\splitmerge\service** sub-directory, and the Split-Merge PowerShell scripts (and required client .dlls) in the **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="abb87-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="abb87-113">Prerequisites</span></span>
1. <span data-ttu-id="abb87-114">Créez une base de données Azure SQL DB qui servira de base de données d’état du service de fractionnement/fusion.</span><span class="sxs-lookup"><span data-stu-id="abb87-114">Create an Azure SQL DB database that will be used as the split-merge status database.</span></span> <span data-ttu-id="abb87-115">Accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abb87-115">Go to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="abb87-116">Créez une **base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="abb87-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="abb87-117">Nommez la base de données et créez un administrateur ainsi qu’un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="abb87-117">Give the database a name and create a new administrator and password.</span></span> <span data-ttu-id="abb87-118">Veillez à enregistrer le nom et le mot de passe pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="abb87-118">Be sure to record the name and password for later use.</span></span>
2. <span data-ttu-id="abb87-119">Vérifiez que votre serveur Azure SQL DB autorise les services Azure à s’y connecter.</span><span class="sxs-lookup"><span data-stu-id="abb87-119">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="abb87-120">Dans le portail, dans **Paramètres du pare-feu**, assurez-vous que le paramètre **Autoriser l’accès aux services Azure** est défini sur **Activé**.</span><span class="sxs-lookup"><span data-stu-id="abb87-120">In the portal, in the **Firewall Settings**, ensure that the **Allow access to Azure Services** setting is set to **On**.</span></span> <span data-ttu-id="abb87-121">Cliquez sur l’icône « Enregistrer ».</span><span class="sxs-lookup"><span data-stu-id="abb87-121">Click the "save" icon.</span></span>
   
   ![Services autorisés][1]
3. <span data-ttu-id="abb87-123">Créez un compte de Stockage Azure qui sera utilisé comme emplacement de destination pour les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="abb87-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="abb87-124">Accédez au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="abb87-124">Go to the Azure Portal.</span></span> <span data-ttu-id="abb87-125">Dans la barre à gauche, cliquez successivement sur **Nouveau**, **Données + stockage** et **Stockage**.</span><span class="sxs-lookup"><span data-stu-id="abb87-125">In the left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="abb87-126">Créez un service cloud Azure qui contient votre service de fractionnement/fusion.</span><span class="sxs-lookup"><span data-stu-id="abb87-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="abb87-127">Accédez au portail Azure.</span><span class="sxs-lookup"><span data-stu-id="abb87-127">Go to the Azure Portal.</span></span> <span data-ttu-id="abb87-128">Dans la barre à gauche, cliquez successivement sur **Nouveau**, **Compute**, **Service cloud** et **Créer**.</span><span class="sxs-lookup"><span data-stu-id="abb87-128">In the left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="abb87-129">Configurer votre service de fractionnement et de fusion</span><span class="sxs-lookup"><span data-stu-id="abb87-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="abb87-130">Configuration du service de fractionnement/fusion</span><span class="sxs-lookup"><span data-stu-id="abb87-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="abb87-131">Dans le dossier où vous avez téléchargé les assemblys de fractionnement et de fusion, créez une copie du fichier **ServiceConfiguration.Template.cscfg** fourni avec **SplitMergeService.cspkg** et renommez-le **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="abb87-131">In the folder where you downloaded the Split-Merge assemblies, create a copy of the **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="abb87-132">Ouvrez **ServiceConfiguration.cscfg** dans un éditeur de texte de type Visual Studio qui valide les entrées telles que le format des empreintes numériques de certificat.</span><span class="sxs-lookup"><span data-stu-id="abb87-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as the format of certificate thumbprints.</span></span>
3. <span data-ttu-id="abb87-133">Créez une base de données ou sélectionnez-en une qui fera office de base de données d’état pour les opérations de fractionnement-fusion et qui permettra de récupérer la chaîne de connexion de la base de données concernée.</span><span class="sxs-lookup"><span data-stu-id="abb87-133">Create a new database or choose an existing database to serve as the status database for Split-Merge operations and retrieve the connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="abb87-134">À ce stade, la base de données de l’état doit utiliser le classement Latin (SQL\_Latin1\_General\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="abb87-134">At this time, the status database must use the Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="abb87-135">Pour plus d'informations, consultez la rubrique [Nom de classement Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="abb87-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="abb87-136">Dans Azure SQL DB, la chaîne de connexion se présente généralement sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="abb87-136">With Azure SQL DB, the connection string typically is of the form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="abb87-137">Entrez cette chaîne de connexion dans le fichier cscfg dans les sections de rôle **SplitMergeWeb** et **SplitMergeWorker** du paramètre ElasticScaleMetadata.</span><span class="sxs-lookup"><span data-stu-id="abb87-137">Enter this connection string in the cscfg file in both the **SplitMergeWeb** and **SplitMergeWorker** role sections in the ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="abb87-138">Pour le rôle **SplitMergeWorker**, entrez une chaîne de connexion valide pour le stockage Azure pour le paramètre **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="abb87-138">For the **SplitMergeWorker** role, enter a valid connection string to Azure storage for the **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="abb87-139">Configurer la sécurité</span><span class="sxs-lookup"><span data-stu-id="abb87-139">Configure security</span></span>
<span data-ttu-id="abb87-140">Pour obtenir des instructions détaillées permettant de configurer la sécurité du service, reportez-vous à la [configuration de la sécurité de la fusion et du fractionnement](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="abb87-140">For detailed instructions to configure the security of the service, refer to the [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="abb87-141">Dans le cadre d’un simple déploiement de test pour ce didacticiel, le bon fonctionnement du service nécessite d’effectuer un nombre minimum d’étapes de configuration.</span><span class="sxs-lookup"><span data-stu-id="abb87-141">For the purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed to get the service up and running.</span></span> <span data-ttu-id="abb87-142">Ces dernières permettent uniquement à l’ordinateur/au compte qui les exécute de communiquer avec le service.</span><span class="sxs-lookup"><span data-stu-id="abb87-142">These steps enable only the one machine/account executing them to communicate with the service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="abb87-143">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="abb87-143">Create a self-signed certificate</span></span>
<span data-ttu-id="abb87-144">Créez un répertoire à partir duquel vous allez exécuter la commande suivante à l’aide d’une fenêtre [d’invite de commandes développeur pour Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) :</span><span class="sxs-lookup"><span data-stu-id="abb87-144">Create a new directory and from this directory execute the following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="abb87-145">Un mot de passe vous est demandé pour protéger la clé privée.</span><span class="sxs-lookup"><span data-stu-id="abb87-145">You are asked for a password to protect the private key.</span></span> <span data-ttu-id="abb87-146">Entrez un mot de passe fort et confirmez-le.</span><span class="sxs-lookup"><span data-stu-id="abb87-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="abb87-147">Vous êtes ensuite de nouveau invité à entrer le mot de passe.</span><span class="sxs-lookup"><span data-stu-id="abb87-147">You are then prompted for the password to be used once more after that.</span></span> <span data-ttu-id="abb87-148">Cliquez sur **Oui** à la fin pour l’importer dans le magasin racine des autorités de certification approuvées.</span><span class="sxs-lookup"><span data-stu-id="abb87-148">Click **Yes** at the end to import it to the Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="abb87-149">Création d’un fichier PFX</span><span class="sxs-lookup"><span data-stu-id="abb87-149">Create a PFX file</span></span>
<span data-ttu-id="abb87-150">Exécutez la commande suivante à partir de la même fenêtre que celle où makecert a été exécuté. Utilisez le même mot de passe que celui utilisé pour créer le certificat :</span><span class="sxs-lookup"><span data-stu-id="abb87-150">Execute the following command from the same window where makecert was executed; use the same password that you used to create the certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-the-client-certificate-into-the-personal-store"></a><span data-ttu-id="abb87-151">Importation du certificat client dans le magasin personnel</span><span class="sxs-lookup"><span data-stu-id="abb87-151">Import the client certificate into the personal store</span></span>
1. <span data-ttu-id="abb87-152">Dans l’Explorateur Windows, double-cliquez sur **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="abb87-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="abb87-153">Dans **l’Assistant Importation de certificat**, sélectionnez **Utilisateur actuel** et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="abb87-153">In the **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="abb87-154">Vérifiez le chemin d’accès au fichier et cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="abb87-154">Confirm the file path and click **Next**.</span></span>
4. <span data-ttu-id="abb87-155">Tapez le mot de passe, laissez l’option **Inclure toutes les propriétés étendues** activée, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="abb87-155">Type the password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="abb87-156">Laissez l’option **Sélectionner automatiquement le magasin de certificats…** activée, puis cliquez sur **Suivant**.</span><span class="sxs-lookup"><span data-stu-id="abb87-156">Leave **Automatically select the certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="abb87-157">Cliquez sur **Terminer** et sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="abb87-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-the-pfx-file-to-the-cloud-service"></a><span data-ttu-id="abb87-158">Téléchargement du fichier PFX dans le service cloud</span><span class="sxs-lookup"><span data-stu-id="abb87-158">Upload the PFX file to the cloud service</span></span>
1. <span data-ttu-id="abb87-159">Accédez au [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="abb87-159">Go to the [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="abb87-160">Sélectionnez **Services Cloud**.</span><span class="sxs-lookup"><span data-stu-id="abb87-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="abb87-161">Sélectionnez le service cloud créé ci-dessus pour le service de fractionnement/fusion.</span><span class="sxs-lookup"><span data-stu-id="abb87-161">Select the cloud service you created above for the Split/Merge service.</span></span>
4. <span data-ttu-id="abb87-162">Dans le menu supérieur, cliquez sur **Certificats** .</span><span class="sxs-lookup"><span data-stu-id="abb87-162">Click **Certificates** on the top menu.</span></span>
5. <span data-ttu-id="abb87-163">Cliquez sur **Télécharger** dans la barre inférieure.</span><span class="sxs-lookup"><span data-stu-id="abb87-163">Click **Upload** in the bottom bar.</span></span>
6. <span data-ttu-id="abb87-164">Sélectionnez le fichier PFX et entrez le même mot de passe que ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="abb87-164">Select the PFX file and enter the same password as above.</span></span>
7. <span data-ttu-id="abb87-165">Lorsque vous avez terminé, copiez l’empreinte de certificat à partir de la nouvelle entrée dans la liste.</span><span class="sxs-lookup"><span data-stu-id="abb87-165">Once completed, copy the certificate thumbprint from the new entry in the list.</span></span>

### <a name="update-the-service-configuration-file"></a><span data-ttu-id="abb87-166">Mise à jour du fichier de configuration de service</span><span class="sxs-lookup"><span data-stu-id="abb87-166">Update the service configuration file</span></span>
<span data-ttu-id="abb87-167">Collez l’empreinte de certificat copiée précédemment dans l’attribut d’empreinte/de valeur des paramètres suivants.</span><span class="sxs-lookup"><span data-stu-id="abb87-167">Paste the certificate thumbprint copied above into the thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="abb87-168">Pour le rôle de travail :</span><span class="sxs-lookup"><span data-stu-id="abb87-168">For the worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="abb87-169">Pour le rôle web :</span><span class="sxs-lookup"><span data-stu-id="abb87-169">For the web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="abb87-170">Veuillez noter que pour les déploiements de production, des certificats distincts doivent être utilisés pour l’autorité de certification, le chiffrement, le certificat de serveur et les certificats clients.</span><span class="sxs-lookup"><span data-stu-id="abb87-170">Please note that for production deployments separate certificates should be used for the CA, for encryption, the Server certificate and client certificates.</span></span> <span data-ttu-id="abb87-171">Pour plus d’informations, consultez la rubrique [Configuration de la sécurité](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="abb87-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="abb87-172">Déployer votre service</span><span class="sxs-lookup"><span data-stu-id="abb87-172">Deploy your service</span></span>
1. <span data-ttu-id="abb87-173">Accédez au [portail Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="abb87-173">Go to the [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="abb87-174">Cliquez sur l’onglet **Services cloud** à gauche et sélectionnez le service cloud que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="abb87-174">Click the **Cloud Services** tab on the left, and select the cloud service that you created earlier.</span></span>
3. <span data-ttu-id="abb87-175">Cliquez sur **Tableau de bord**.</span><span class="sxs-lookup"><span data-stu-id="abb87-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="abb87-176">Choisissez l’environnement intermédiaire, puis cliquez sur **Télécharger un nouveau déploiement intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="abb87-176">Choose the staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Staging][3]
5. <span data-ttu-id="abb87-178">Dans la boîte de dialogue, entrez une étiquette de déploiement.</span><span class="sxs-lookup"><span data-stu-id="abb87-178">In the dialog box, enter a deployment label.</span></span> <span data-ttu-id="abb87-179">Pour « Package » et « Configuration », cliquez sur « À partir de local » et choisissez le fichier **SplitMergeService.cspkg** et le fichier .cscfg que vous avez configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="abb87-179">For both 'Package' and 'Configuration', click 'From Local' and choose the **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="abb87-180">Assurez-vous que la case **Déployer même si un ou plusieurs rôles contiennent une seule instance** est cochée.</span><span class="sxs-lookup"><span data-stu-id="abb87-180">Ensure that the checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="abb87-181">Appuyez sur le bouton en forme de coche dans le coin inférieur droit pour commencer le déploiement.</span><span class="sxs-lookup"><span data-stu-id="abb87-181">Hit the tick button in the bottom right to begin the deployment.</span></span> <span data-ttu-id="abb87-182">Cette opération peut prendre plusieurs minutes.</span><span class="sxs-lookup"><span data-stu-id="abb87-182">Expect it to take a few minutes to complete.</span></span>

   ![Télécharger][4]

## <a name="troubleshoot-the-deployment"></a><span data-ttu-id="abb87-184">Résoudre les problèmes de déploiement</span><span class="sxs-lookup"><span data-stu-id="abb87-184">Troubleshoot the deployment</span></span>
<span data-ttu-id="abb87-185">Si votre rôle web ne parvient pas à être en ligne, il s’agit probablement d’un problème avec la configuration de sécurité.</span><span class="sxs-lookup"><span data-stu-id="abb87-185">If your web role fails to come online, it is likely a problem with the security configuration.</span></span> <span data-ttu-id="abb87-186">Vérifiez que le protocole SSL est configuré comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="abb87-186">Check that the SSL is configured as described above.</span></span>

<span data-ttu-id="abb87-187">Si votre rôle de travail ne parvient pas à être en ligne, mais que votre rôle web réussit, il s’agit probablement d’un problème de connexion à la base de données d’états que vous avez créée précédemment.</span><span class="sxs-lookup"><span data-stu-id="abb87-187">If your worker role fails to come online, but your web role succeeds, it is most likely a problem connecting to the status database that you created earlier.</span></span>

* <span data-ttu-id="abb87-188">Assurez-vous que la chaîne de connexion du fichier .cscfg ne contient aucune erreur.</span><span class="sxs-lookup"><span data-stu-id="abb87-188">Make sure that the connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="abb87-189">Vérifiez que le serveur et la base de données existent et que l’identifiant utilisateur et le mot de passe sont corrects.</span><span class="sxs-lookup"><span data-stu-id="abb87-189">Check that the server and database exist, and that the user id and password are correct.</span></span>
* <span data-ttu-id="abb87-190">Dans Azure SQL DB, la chaîne de connexion doit se présenter sous la forme suivante :</span><span class="sxs-lookup"><span data-stu-id="abb87-190">For Azure SQL DB, the connection string should be of the form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="abb87-191">Assurez-vous que le nom du serveur ne commence pas par **https://**.</span><span class="sxs-lookup"><span data-stu-id="abb87-191">Ensure that the server name does not begin with **https://**.</span></span>
* <span data-ttu-id="abb87-192">Vérifiez que votre serveur Azure SQL DB autorise les services Azure à s’y connecter.</span><span class="sxs-lookup"><span data-stu-id="abb87-192">Ensure that your Azure SQL DB server allows Azure Services to connect to it.</span></span> <span data-ttu-id="abb87-193">Pour ce faire, ouvrez https://manage.windowsazure.com et cliquez sur « Bases de données SQL » sur la gauche, puis sur « Serveurs » en haut et sélectionnez votre serveur.</span><span class="sxs-lookup"><span data-stu-id="abb87-193">To do this, open https://manage.windowsazure.com, click “SQL Databases” on the left, click “Servers” at the top, and select your server.</span></span> <span data-ttu-id="abb87-194">Cliquez sur **Configurer** en haut et assurez-vous que le paramètre **Services Azure** est défini sur « Oui ».</span><span class="sxs-lookup"><span data-stu-id="abb87-194">Click **Configure** at the top and ensure that the **Azure Services** setting is set to “Yes”.</span></span> <span data-ttu-id="abb87-195">(voir la section « Configuration requise » en haut de cet article).</span><span class="sxs-lookup"><span data-stu-id="abb87-195">(See the Prerequisites section at the top of this article).</span></span>

## <a name="test-the-service-deployment"></a><span data-ttu-id="abb87-196">Tester le déploiement du service</span><span class="sxs-lookup"><span data-stu-id="abb87-196">Test the service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="abb87-197">Se connecter avec un navigateur Web</span><span class="sxs-lookup"><span data-stu-id="abb87-197">Connect with a web browser</span></span>
<span data-ttu-id="abb87-198">Déterminez le point de terminaison web de votre service de fractionnement/fusion.</span><span class="sxs-lookup"><span data-stu-id="abb87-198">Determine the web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="abb87-199">Vous pouvez le trouver dans le portail Azure Classic en accédant au **Tableau de bord** de votre service cloud et en effectuant une recherche dans la zone **URL du site** sur le côté droit.</span><span class="sxs-lookup"><span data-stu-id="abb87-199">You can find this in the Azure Classic Portal by going to the **Dashboard** of your cloud service and looking under **Site URL** on the right side.</span></span> <span data-ttu-id="abb87-200">Remplacez **http://** par **https://**, car les paramètres de sécurité par défaut désactivent le point de terminaison HTTP.</span><span class="sxs-lookup"><span data-stu-id="abb87-200">Replace **http://** with **https://** since the default security settings disable the HTTP endpoint.</span></span> <span data-ttu-id="abb87-201">Chargez la page correspondant à cette URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="abb87-201">Load the page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="abb87-202">Effectuer des tests avec des scripts PowerShell</span><span class="sxs-lookup"><span data-stu-id="abb87-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="abb87-203">Le déploiement et votre environnement peuvent être testés en exécutant les exemples de scripts PowerShell fournis.</span><span class="sxs-lookup"><span data-stu-id="abb87-203">The deployment and your environment can be tested by running the included sample PowerShell scripts.</span></span>

<span data-ttu-id="abb87-204">Les fichiers de script inclus sont les suivants :</span><span class="sxs-lookup"><span data-stu-id="abb87-204">The script files included are:</span></span>

1. <span data-ttu-id="abb87-205">**SetupSampleSplitMergeEnvironment.ps1** : configure une couche de données de test pour la fusion et le fractionnement (voir le tableau ci-dessous pour obtenir une description détaillée)</span><span class="sxs-lookup"><span data-stu-id="abb87-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="abb87-206">**ExecuteSampleSplitMerge.ps1** : exécute les opérations de test sur la couche de données de test (voir le tableau ci-dessous pour obtenir une description détaillée)</span><span class="sxs-lookup"><span data-stu-id="abb87-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on the test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="abb87-207">**GetMappings.ps1** : exemple de script de niveau supérieur qui imprime l’état actuel des mappages de partitions.</span><span class="sxs-lookup"><span data-stu-id="abb87-207">**GetMappings.ps1** - top-level sample script that prints out the current state of the shard mappings.</span></span>
4. <span data-ttu-id="abb87-208">**ShardManagement.psm1** : script d’assistance qui encapsule l’API ShardManagement</span><span class="sxs-lookup"><span data-stu-id="abb87-208">**ShardManagement.psm1**  - helper script that wraps the ShardManagement API</span></span>
5. <span data-ttu-id="abb87-209">**SqlDatabaseHelpers.psm1** : script d’assistance pour la création et la gestion des bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="abb87-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="abb87-210">Fichier PowerShell</span><span class="sxs-lookup"><span data-stu-id="abb87-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="abb87-211">Étapes</span><span class="sxs-lookup"><span data-stu-id="abb87-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="abb87-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="abb87-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="abb87-213">Crée une base de données pour le Gestionnaire de cartes de partitions</span><span class="sxs-lookup"><span data-stu-id="abb87-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="abb87-214">Crée 2&#160;bases de données de partition.</span><span class="sxs-lookup"><span data-stu-id="abb87-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="abb87-215">Crée une carte de partitions pour les bases de données concernées (supprime les cartes de partitions existantes sur ces dernières).</span><span class="sxs-lookup"><span data-stu-id="abb87-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="abb87-216">Crée un petit exemple de table dans les deux partitions et remplit la table dans l’une des partitions.</span><span class="sxs-lookup"><span data-stu-id="abb87-216">Creates a small sample table in both the shards, and populates the table in one of the shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="abb87-217">Déclare le SchemaInfo pour la table partitionnée.</span><span class="sxs-lookup"><span data-stu-id="abb87-217">Declares the SchemaInfo for the sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="abb87-218">Fichier PowerShell</span><span class="sxs-lookup"><span data-stu-id="abb87-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="abb87-219">Étapes</span><span class="sxs-lookup"><span data-stu-id="abb87-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="abb87-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="abb87-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="abb87-221">Envoie une demande de fractionnement vers le serveur web frontal du service de fractionnement/fusion, qui fractionne la moitié des données de la première partition et les envoie vers la deuxième partition.</span><span class="sxs-lookup"><span data-stu-id="abb87-221">Sends a split request to the Split-Merge Service web frontend, which splits half the data from the first shard to the second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="abb87-222">Interroge le serveur Web frontal sur l’état de la demande de fractionnement et attend jusqu’à ce que la demande soit terminée.</span><span class="sxs-lookup"><span data-stu-id="abb87-222">Polls the web frontend for the split request status and waits until the request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="abb87-223">Envoie une demande de fusion vers le serveur Web frontal du service de fractionnement/fusion, qui déplace les données de la deuxième partition vers la première partition.</span><span class="sxs-lookup"><span data-stu-id="abb87-223">Sends a merge request to the Split-Merge Service web frontend, which moves the data from the second shard back to the first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="abb87-224">Interroge le serveur web frontal sur l’état de la demande de fusion et attend jusqu’à ce que la demande soit terminée.</span><span class="sxs-lookup"><span data-stu-id="abb87-224">Polls the web frontend for the merge request status and waits until the request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-to-verify-your-deployment"></a><span data-ttu-id="abb87-225">Utiliser PowerShell pour vérifier le déploiement</span><span class="sxs-lookup"><span data-stu-id="abb87-225">Use PowerShell to verify your deployment</span></span>
1. <span data-ttu-id="abb87-226">Ouvrez une nouvelle fenêtre PowerShell et accédez au répertoire dans lequel vous avez téléchargé le package de fractionnement/fusion, puis accédez au répertoire « powershell ».</span><span class="sxs-lookup"><span data-stu-id="abb87-226">Open a new PowerShell window and navigate to the directory where you downloaded the Split-Merge package, and then navigate into the “powershell” directory.</span></span>
2. <span data-ttu-id="abb87-227">Créez un serveur de base de données SQL Azure (ou choisissez un serveur existant) dans lequel le Gestionnaire des cartes de partitions et les partitions seront créés.</span><span class="sxs-lookup"><span data-stu-id="abb87-227">Create an Azure SQL database server (or choose an existing server) where the shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="abb87-228">le script SetupSampleSplitMergeEnvironment.ps1 crée, par défaut, ces bases de données sur le même serveur pour simplifier le script.</span><span class="sxs-lookup"><span data-stu-id="abb87-228">The SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on the same server by default to keep the script simple.</span></span> <span data-ttu-id="abb87-229">Il ne s’agit pas d’une restriction du service de fractionnement/fusion.</span><span class="sxs-lookup"><span data-stu-id="abb87-229">This is not a restriction of the Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="abb87-230">Une connexion d’authentification SQL avec un accès en lecture/écriture aux bases de données est requis pour le service de fractionnement/fusion afin de déplacer les données et de mettre à jour la carte de partitions.</span><span class="sxs-lookup"><span data-stu-id="abb87-230">A SQL authentication login with read/write access to the DBs will be needed for the Split-Merge service to move data and update the shard map.</span></span> <span data-ttu-id="abb87-231">Le service de fractionnement/fusion s’exécutant dans le cloud, il ne prend pas actuellement en charge l’authentification intégrée.</span><span class="sxs-lookup"><span data-stu-id="abb87-231">Since the Split-Merge Service runs in the cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="abb87-232">Assurez-vous que le serveur SQL Azure est configuré pour autoriser l’accès à partir de l’adresse IP de l’ordinateur exécutant les scripts.</span><span class="sxs-lookup"><span data-stu-id="abb87-232">Make sure the Azure SQL server is configured to allow access from the IP address of the machine running these scripts.</span></span> <span data-ttu-id="abb87-233">Pour accéder à ce paramètre, sélectionnez Serveur SQL Azure / Configuration / Adresses IP autorisées.</span><span class="sxs-lookup"><span data-stu-id="abb87-233">You can find this setting under the Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="abb87-234">Exécutez le script SetupSampleSplitMergeEnvironment.ps1 pour créer l’exemple d’environnement.</span><span class="sxs-lookup"><span data-stu-id="abb87-234">Execute the SetupSampleSplitMergeEnvironment.ps1 script to create the sample environment.</span></span>
   
   <span data-ttu-id="abb87-235">L’exécution de ce script efface toutes les structures de données de gestion des cartes de partitions existantes dans la base de données du Gestionnaire des cartes de partitions et dans les partitions.</span><span class="sxs-lookup"><span data-stu-id="abb87-235">Running this script will wipe out any existing shard map management data structures on the shard map manager database and the shards.</span></span> <span data-ttu-id="abb87-236">Il peut être utile de réexécuter le script si vous souhaitez réinitialiser la carte de partitions ou les partitions.</span><span class="sxs-lookup"><span data-stu-id="abb87-236">It may be useful to rerun the script if you wish to re-initialize the shard map or shards.</span></span>
   
   <span data-ttu-id="abb87-237">Exemple de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="abb87-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="abb87-238">Exécutez le script Getmappings.ps1 pour afficher les mappages qui existent actuellement dans l’exemple d’environnement.</span><span class="sxs-lookup"><span data-stu-id="abb87-238">Execute the Getmappings.ps1 script to view the mappings that currently exist in the sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="abb87-239">Exécutez le script ExecuteSampleSplitMerge.ps1 pour exécuter une opération de fractionnement (déplacement de la moitié des données de la première partition vers la deuxième partition), puis une opération de fusion (redéplacement des données sur la première partition).</span><span class="sxs-lookup"><span data-stu-id="abb87-239">Execute the ExecuteSampleSplitMerge.ps1 script to execute a split operation (moving half the data on the first shard to the second shard) and then a merge operation (moving the data back onto the first shard).</span></span> <span data-ttu-id="abb87-240">Si vous avez configuré SSL et laissé le point de terminaison http désactivé, assurez-vous d’utiliser le point de terminaison https:// à la place.</span><span class="sxs-lookup"><span data-stu-id="abb87-240">If you configured SSL and left the http endpoint disabled, ensure that you use the https:// endpoint instead.</span></span>
   
   <span data-ttu-id="abb87-241">Exemple de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="abb87-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="abb87-242">Si vous recevez l’erreur ci-dessous, il s’agit probablement d’un problème avec le certificat de votre point de terminaison web.</span><span class="sxs-lookup"><span data-stu-id="abb87-242">If you receive the below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="abb87-243">Essayez de vous connecter au point de terminaison web avec votre navigateur web préféré et vérifiez s’il existe une erreur de certificat.</span><span class="sxs-lookup"><span data-stu-id="abb87-243">Try connecting to the Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="abb87-244">Si l’opération s’est déroulée sans erreur, le résultat doit ressembler à ce qui suit :</span><span class="sxs-lookup"><span data-stu-id="abb87-244">If it succeeded, the output should look like the below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C to end
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source to target shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing the request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="abb87-245">Faites des essais avec d’autres types de données.</span><span class="sxs-lookup"><span data-stu-id="abb87-245">Experiment with other data types!</span></span> <span data-ttu-id="abb87-246">Tous ces scripts nécessitent un paramètre -ShardKeyType facultatif qui vous permet de spécifier le type de clé.</span><span class="sxs-lookup"><span data-stu-id="abb87-246">All of these scripts take an optional -ShardKeyType parameter that allows you to specify the key type.</span></span> <span data-ttu-id="abb87-247">La valeur par défaut est Int32, mais vous pouvez également spécifier Int64, Guid ou Binary.</span><span class="sxs-lookup"><span data-stu-id="abb87-247">The default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="abb87-248">Créer des requêtes</span><span class="sxs-lookup"><span data-stu-id="abb87-248">Create requests</span></span>
<span data-ttu-id="abb87-249">Le service peut être utilisé à l’aide de l’interface utilisateur Web ou par l’importation et l’utilisation du module PowerShell SplitMerge.psm1 qui envoie vos demandes via le rôle Web.</span><span class="sxs-lookup"><span data-stu-id="abb87-249">The service can be used either by using the web UI or by importing and using the SplitMerge.psm1 PowerShell module which will submit your requests through the web role.</span></span>

<span data-ttu-id="abb87-250">Ce service peut déplacer les données dans les tables partitionnées et les tables de référence.</span><span class="sxs-lookup"><span data-stu-id="abb87-250">The service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="abb87-251">Une table partitionnée possède une colonne de clés de partitionnement et comporte des données de ligne différentes sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="abb87-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="abb87-252">Une table de référence n’est pas partitionnée. De ce fait, elle comporte les mêmes données de ligne sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="abb87-252">A reference table is not sharded so it contains the same row data on every shard.</span></span> <span data-ttu-id="abb87-253">Les tables de référence sont utiles pour les données qui ne changent pas souvent et qui sont utilisées pour S’ASSOCIER à des tables partitionnées dans les requêtes.</span><span class="sxs-lookup"><span data-stu-id="abb87-253">Reference tables are useful for data that does not change often and is used to JOIN with sharded tables in queries.</span></span>

<span data-ttu-id="abb87-254">Pour effectuer une opération de fractionnement/fusion, vous devez déclarer les tables partitionnées et les tables de référence que vous souhaitez déplacer.</span><span class="sxs-lookup"><span data-stu-id="abb87-254">In order to perform a split-merge operation, you must declare the sharded tables and reference tables that you want to have moved.</span></span> <span data-ttu-id="abb87-255">Cette opération est effectuée avec l’API **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="abb87-255">This is accomplished with the **SchemaInfo** API.</span></span> <span data-ttu-id="abb87-256">Cette API se trouve dans l’espace de noms **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** .</span><span class="sxs-lookup"><span data-stu-id="abb87-256">This API is in the **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="abb87-257">Pour chaque table partitionnée, créez un objet **ShardedTableInfo** décrivant le nom du schéma parent de la table (facultatif, la valeur par défaut est « dbo »), le nom de la table et le nom de la colonne de cette table qui comporte la clé de partitionnement.</span><span class="sxs-lookup"><span data-stu-id="abb87-257">For each sharded table, create a **ShardedTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”), the table name, and the column name in that table that contains the sharding key.</span></span>
2. <span data-ttu-id="abb87-258">Pour chaque table de référence, créez un objet **ReferenceTableInfo** décrivant le nom du schéma parent de la table (facultatif, la valeur par défaut est « dbo ») et le nom de la table.</span><span class="sxs-lookup"><span data-stu-id="abb87-258">For each reference table, create a **ReferenceTableInfo** object describing the table’s parent schema name (optional, defaults to “dbo”) and the table name.</span></span>
3. <span data-ttu-id="abb87-259">Ajoutez les objets TableInfo ci-dessus à un nouvel objet **SchemaInfo** .</span><span class="sxs-lookup"><span data-stu-id="abb87-259">Add the above TableInfo objects to a new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="abb87-260">Obtenez une référence à un objet **ShardMapManager** et appelez **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="abb87-260">Get a reference to a **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="abb87-261">Ajoutez **SchemaInfo** à **SchemaInfoCollection**, en fournissant le nom du mappage de partitions.</span><span class="sxs-lookup"><span data-stu-id="abb87-261">Add the **SchemaInfo** to the **SchemaInfoCollection**, providing the shard map name.</span></span>

<span data-ttu-id="abb87-262">Le script SetupSampleSplitMergeEnvironment.ps1 contient un exemple de cette opération.</span><span class="sxs-lookup"><span data-stu-id="abb87-262">An example of this can be seen in the SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="abb87-263">Le service de fractionnement/fusion ne crée pas la base de données cible (ou le schéma pour les tables de la base de données) à votre place.</span><span class="sxs-lookup"><span data-stu-id="abb87-263">The Split-Merge service does not create the target database (or schema for any tables in the database) for you.</span></span> <span data-ttu-id="abb87-264">Ils doivent être créés au préalable avant d’envoyer une demande au service.</span><span class="sxs-lookup"><span data-stu-id="abb87-264">They must be pre-created before sending a request to the service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="abb87-265">Résolution de problèmes</span><span class="sxs-lookup"><span data-stu-id="abb87-265">Troubleshooting</span></span>
<span data-ttu-id="abb87-266">Le message ci-dessous peut apparaître lors de l’exécution des exemples de scripts PowerShell :</span><span class="sxs-lookup"><span data-stu-id="abb87-266">You may see the below message when running the sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : The underlying connection was closed: Could not establish trust relationship for the SSL/TLS secure channel.
   ```

<span data-ttu-id="abb87-267">Cette erreur signifie que votre certificat SSL n’est pas correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="abb87-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="abb87-268">Suivez les instructions de la section « Connexion avec un navigateur web ».</span><span class="sxs-lookup"><span data-stu-id="abb87-268">Please follow the instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="abb87-269">Si vous ne pouvez pas soumettre les demandes, vous pouvez voir ceci :</span><span class="sxs-lookup"><span data-stu-id="abb87-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="abb87-270">Dans ce cas, vérifiez votre fichier de configuration, notamment le paramètre pour **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="abb87-270">In this case, check your configuration file, in particular the setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="abb87-271">Cette erreur indique généralement que le rôle de travail n’a pas pu initialiser avec succès la base de données de métadonnées à la première utilisation.</span><span class="sxs-lookup"><span data-stu-id="abb87-271">This error typically indicates that the worker role could not successfully initialize the metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

