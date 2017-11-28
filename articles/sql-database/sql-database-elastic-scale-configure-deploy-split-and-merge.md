---
title: "un service de fusion et fractionnement d’aaaDeploy | Documents Microsoft"
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
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a><span data-ttu-id="b0f1a-103">Déployer un service de fractionnement et de fusion</span><span class="sxs-lookup"><span data-stu-id="b0f1a-103">Deploy a split-merge service</span></span>
<span data-ttu-id="b0f1a-104">outil de fusion et fractionnement Hello vous permet de déplacer des données entre des bases de données partitionnées.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-104">hello split-merge tool lets you move data between sharded databases.</span></span> <span data-ttu-id="b0f1a-105">Consultez [Déplacement de données entre des bases de données cloud montées en charge](sql-database-elastic-scale-overview-split-and-merge.md)</span><span class="sxs-lookup"><span data-stu-id="b0f1a-105">See [Moving data between scaled-out cloud databases](sql-database-elastic-scale-overview-split-and-merge.md)</span></span>

## <a name="download-hello-split-merge-packages"></a><span data-ttu-id="b0f1a-106">Télécharger les packages de fusion et fractionnement hello</span><span class="sxs-lookup"><span data-stu-id="b0f1a-106">Download hello Split-Merge packages</span></span>
1. <span data-ttu-id="b0f1a-107">Télécharger la dernière version de NuGet hello à partir de [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-107">Download hello latest NuGet version from [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).</span></span>
2. <span data-ttu-id="b0f1a-108">Ouvrez une invite de commandes et accédez répertoire toohello où vous avez téléchargé nuget.exe.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-108">Open a command prompt and navigate toohello directory where you downloaded nuget.exe.</span></span> <span data-ttu-id="b0f1a-109">Hello inclut commmands de PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-109">hello download includes PowerShell commmands.</span></span>
3. <span data-ttu-id="b0f1a-110">Téléchargez hello dernière fusion et fractionnement dans l’annuaire actuel de hello avec hello commande ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-110">Download hello latest Split-Merge package into hello current directory with hello below command:</span></span>
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

<span data-ttu-id="b0f1a-111">fichiers de Hello sont placés dans un répertoire nommé **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** où *x.x.xxx.x* reflète le numéro de version hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-111">hello files are placed in a directory named **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** where *x.x.xxx.x* reflects hello version number.</span></span> <span data-ttu-id="b0f1a-112">Recherche des fichiers de Service de fusion et fractionnement hello Bonjour **content\splitmerge\service** sous-répertoire et hello scripts PowerShell de fusion et fractionnement (et les DLL client requis) Bonjour **content\splitmerge\powershell** sous-répertoire.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-112">Find hello split-merge Service files in hello **content\splitmerge\service** sub-directory, and hello Split-Merge PowerShell scripts (and required client .dlls) in hello **content\splitmerge\powershell** sub-directory.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0f1a-113">Composants requis</span><span class="sxs-lookup"><span data-stu-id="b0f1a-113">Prerequisites</span></span>
1. <span data-ttu-id="b0f1a-114">Créer une base de données de la base de données SQL Azure qui sera utilisé comme base de données de fusion et fractionnement état hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-114">Create an Azure SQL DB database that will be used as hello split-merge status database.</span></span> <span data-ttu-id="b0f1a-115">Accédez toohello [portail Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-115">Go toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="b0f1a-116">Créez une **base de données SQL**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-116">Create a new **SQL Database**.</span></span> <span data-ttu-id="b0f1a-117">Donnez un nom à base de données hello et créer un nouvel administrateur et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-117">Give hello database a name and create a new administrator and password.</span></span> <span data-ttu-id="b0f1a-118">Être assuré que nom de hello toorecord et le mot de passe pour une utilisation ultérieure.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-118">Be sure toorecord hello name and password for later use.</span></span>
2. <span data-ttu-id="b0f1a-119">Vérifiez que votre serveur de base de données SQL Azure autorise des Services Azure tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-119">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="b0f1a-120">Dans le portail de hello hello **les paramètres de pare-feu**, vérifiez que hello **autoriser l’accès des Services de tooAzure** est défini trop**sur**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-120">In hello portal, in hello **Firewall Settings**, ensure that hello **Allow access tooAzure Services** setting is set too**On**.</span></span> <span data-ttu-id="b0f1a-121">Cliquez sur hello « enregistrer » de l’icône.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-121">Click hello "save" icon.</span></span>
   
   ![Services autorisés][1]
3. <span data-ttu-id="b0f1a-123">Créez un compte de Stockage Azure qui sera utilisé comme emplacement de destination pour les diagnostics.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-123">Create an Azure Storage account that will be used for diagnostics output.</span></span> <span data-ttu-id="b0f1a-124">Accédez toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-124">Go toohello Azure Portal.</span></span> <span data-ttu-id="b0f1a-125">Dans la barre de gauche hello, cliquez sur **nouveau**, cliquez sur **données + stockage**, puis **stockage**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-125">In hello left bar, click **New**, click **Data + Storage**, then **Storage**.</span></span>
4. <span data-ttu-id="b0f1a-126">Créez un service cloud Azure qui contient votre service de fractionnement/fusion.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-126">Create an Azure Cloud Service that will contain your Split-Merge service.</span></span>  <span data-ttu-id="b0f1a-127">Accédez toohello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-127">Go toohello Azure Portal.</span></span> <span data-ttu-id="b0f1a-128">Dans la barre de gauche hello, cliquez sur **nouveau**, puis **de calcul**, **Service Cloud**, et **créer**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-128">In hello left bar, click **New**, then **Compute**, **Cloud Service**, and **Create**.</span></span> 

## <a name="configure-your-split-merge-service"></a><span data-ttu-id="b0f1a-129">Configurer votre service de fractionnement et de fusion</span><span class="sxs-lookup"><span data-stu-id="b0f1a-129">Configure your Split-Merge service</span></span>
### <a name="split-merge-service-configuration"></a><span data-ttu-id="b0f1a-130">Configuration du service de fractionnement/fusion</span><span class="sxs-lookup"><span data-stu-id="b0f1a-130">Split-Merge service configuration</span></span>
1. <span data-ttu-id="b0f1a-131">Dans le dossier hello où vous avez téléchargé les assemblys hello fusion et fractionnement, créer une copie de hello **ServiceConfiguration.Template.cscfg** fichier livré avec **SplitMergeService.cspkg** et renommez-la **ServiceConfiguration.cscfg**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-131">In hello folder where you downloaded hello Split-Merge assemblies, create a copy of hello **ServiceConfiguration.Template.cscfg** file that shipped alongside **SplitMergeService.cspkg** and rename it **ServiceConfiguration.cscfg**.</span></span>
2. <span data-ttu-id="b0f1a-132">Ouvrez **ServiceConfiguration.cscfg** dans un éditeur de texte tel que Visual Studio qui valide les entrées telles que format hello des empreintes numériques de certificat.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-132">Open **ServiceConfiguration.cscfg** in a text editor such as Visual Studio that validates inputs such as hello format of certificate thumbprints.</span></span>
3. <span data-ttu-id="b0f1a-133">Créer une base de données ou choisissez un tooserve de base de données existante comme base de données de statut hello pour les opérations de fusion et fractionnement et récupérer la chaîne de connexion hello de cette base de données.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-133">Create a new database or choose an existing database tooserve as hello status database for Split-Merge operations and retrieve hello connection string of that database.</span></span> 
   
   > [!IMPORTANT]
   > <span data-ttu-id="b0f1a-134">À ce stade, base de données de statut hello doit utiliser classement Latin de hello (SQL\_Latin1\_général\_CP1\_CI\_AS).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-134">At this time, hello status database must use hello Latin  collation (SQL\_Latin1\_General\_CP1\_CI\_AS).</span></span> <span data-ttu-id="b0f1a-135">Pour plus d'informations, consultez la rubrique [Nom de classement Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-135">For more information, see [Windows Collation Name (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).</span></span>
   >

   <span data-ttu-id="b0f1a-136">Avec la base de données SQL Azure, chaîne de connexion hello est généralement sous forme de hello :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-136">With Azure SQL DB, hello connection string typically is of hello form:</span></span>
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. <span data-ttu-id="b0f1a-137">Entrez cette chaîne de connexion dans le fichier cscfg de hello dans les deux hello **SplitMergeWeb** et **SplitMergeWorker** sections de rôle dans le paramètre de ElasticScaleMetadata hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-137">Enter this connection string in hello cscfg file in both hello **SplitMergeWeb** and **SplitMergeWorker** role sections in hello ElasticScaleMetadata setting.</span></span>
5. <span data-ttu-id="b0f1a-138">Pourquoi **SplitMergeWorker** rôle, entrez un stockage de tooAzure de chaîne de connexion valide pour hello **WorkerRoleSynchronizationStorageAccountConnectionString** paramètre.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-138">For hello **SplitMergeWorker** role, enter a valid connection string tooAzure storage for hello **WorkerRoleSynchronizationStorageAccountConnectionString** setting.</span></span>

### <a name="configure-security"></a><span data-ttu-id="b0f1a-139">Configurer la sécurité</span><span class="sxs-lookup"><span data-stu-id="b0f1a-139">Configure security</span></span>
<span data-ttu-id="b0f1a-140">Pour obtenir des instructions détaillées tooconfigure hello sécurité hello service, consultez toohello [configuration de sécurité de fusion et fractionnement](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-140">For detailed instructions tooconfigure hello security of hello service, refer toohello [Split-Merge security configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

<span data-ttu-id="b0f1a-141">Pour des raisons de hello d’un déploiement de test simple pour ce didacticiel, un ensemble minimal de configuration des étapes seront effectuées service de hello tooget haut et en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-141">For hello purposes of a simple test deployment for this tutorial, a minimal set of configuration steps will be performed tooget hello service up and running.</span></span> <span data-ttu-id="b0f1a-142">Les étapes suivantes permettent uniquement hello un ordinateur/compte qui exécute les toocommunicate avec le service de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-142">These steps enable only hello one machine/account executing them toocommunicate with hello service.</span></span>

### <a name="create-a-self-signed-certificate"></a><span data-ttu-id="b0f1a-143">Créer un certificat auto-signé</span><span class="sxs-lookup"><span data-stu-id="b0f1a-143">Create a self-signed certificate</span></span>
<span data-ttu-id="b0f1a-144">Créer un nouveau répertoire et à partir de cette hello execute de répertoire suivant à l’aide de la commande une [invite de commandes développeur pour Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) fenêtre :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-144">Create a new directory and from this directory execute hello following command using a [Developer Command Prompt for Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) window:</span></span>

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

<span data-ttu-id="b0f1a-145">Vous êtes invité à entrer une clé privée de mot de passe tooprotect hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-145">You are asked for a password tooprotect hello private key.</span></span> <span data-ttu-id="b0f1a-146">Entrez un mot de passe fort et confirmez-le.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-146">Enter a strong password and confirm it.</span></span> <span data-ttu-id="b0f1a-147">Vous êtes ensuite invité pour hello toobe de mot de passe utilisé après une fois de plus.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-147">You are then prompted for hello password toobe used once more after that.</span></span> <span data-ttu-id="b0f1a-148">Cliquez sur **Oui** à hello fin tooimport il magasin racine des autorités de Certification approuvées de toohello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-148">Click **Yes** at hello end tooimport it toohello Trusted Certification Authorities Root store.</span></span>

### <a name="create-a-pfx-file"></a><span data-ttu-id="b0f1a-149">Création d’un fichier PFX</span><span class="sxs-lookup"><span data-stu-id="b0f1a-149">Create a PFX file</span></span>
<span data-ttu-id="b0f1a-150">Exécutez hello de commande suivante à partir de hello même fenêtre où makecert a été exécuté ; Utilisez hello même mot de passe que vous toocreate utilisé hello le certificat :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-150">Execute hello following command from hello same window where makecert was executed; use hello same password that you used toocreate hello certificate:</span></span>

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a><span data-ttu-id="b0f1a-151">Importer un certificat client hello dans le magasin personnel de hello</span><span class="sxs-lookup"><span data-stu-id="b0f1a-151">Import hello client certificate into hello personal store</span></span>
1. <span data-ttu-id="b0f1a-152">Dans l’Explorateur Windows, double-cliquez sur **MyCert.pfx**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-152">In Windows Explorer, double-click **MyCert.pfx**.</span></span>
2. <span data-ttu-id="b0f1a-153">Bonjour **Assistant Importation de certificat** sélectionnez **utilisateur actuel** et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-153">In hello **Certificate Import Wizard** select **Current User** and click **Next**.</span></span>
3. <span data-ttu-id="b0f1a-154">Vérifiez le chemin d’accès du fichier hello et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-154">Confirm hello file path and click **Next**.</span></span>
4. <span data-ttu-id="b0f1a-155">Type hello un mot de passe, laissez le champ **inclure toutes les propriétés étendues** activée et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-155">Type hello password, leave **Include all extended properties** checked and click **Next**.</span></span>
5. <span data-ttu-id="b0f1a-156">Laissez **magasin de certificats de sélectionner automatiquement hello [...]**  activée et cliquez sur **suivant**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-156">Leave **Automatically select hello certificate store[…]** checked and click **Next**.</span></span>
6. <span data-ttu-id="b0f1a-157">Cliquez sur **Terminer** et sur **OK**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-157">Click **Finish** and **OK**.</span></span>

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a><span data-ttu-id="b0f1a-158">Télécharger le service cloud toohello hello PFX fichier</span><span class="sxs-lookup"><span data-stu-id="b0f1a-158">Upload hello PFX file toohello cloud service</span></span>
1. <span data-ttu-id="b0f1a-159">Accédez toohello [Azure Portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-159">Go toohello [Azure Portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b0f1a-160">Sélectionnez **Services Cloud**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-160">Select **Cloud Services**.</span></span>
3. <span data-ttu-id="b0f1a-161">Sélectionnez le service de cloud computing hello que vous avez créé précédemment pour le service de fractionnement/fusion hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-161">Select hello cloud service you created above for hello Split/Merge service.</span></span>
4. <span data-ttu-id="b0f1a-162">Cliquez sur **certificats** sur le menu du haut hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-162">Click **Certificates** on hello top menu.</span></span>
5. <span data-ttu-id="b0f1a-163">Cliquez sur **télécharger** dans la barre inférieure de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-163">Click **Upload** in hello bottom bar.</span></span>
6. <span data-ttu-id="b0f1a-164">Sélectionnez le fichier PFX hello et entrez hello même mot de passe comme indiqué ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-164">Select hello PFX file and enter hello same password as above.</span></span>
7. <span data-ttu-id="b0f1a-165">Une fois terminé, copiez l’empreinte numérique du certificat hello hello nouvelle entrée dans la liste de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-165">Once completed, copy hello certificate thumbprint from hello new entry in hello list.</span></span>

### <a name="update-hello-service-configuration-file"></a><span data-ttu-id="b0f1a-166">Mettre à jour le fichier de configuration de service hello</span><span class="sxs-lookup"><span data-stu-id="b0f1a-166">Update hello service configuration file</span></span>
<span data-ttu-id="b0f1a-167">Collez l’empreinte numérique du certificat hello copié ci-dessus dans l’attribut de valeur d’empreinte numérique hello de ces paramètres.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-167">Paste hello certificate thumbprint copied above into hello thumbprint/value attribute of these settings.</span></span>
<span data-ttu-id="b0f1a-168">Pour le rôle de travail hello :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-168">For hello worker role:</span></span>
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="b0f1a-169">Pour le rôle web hello :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-169">For hello web role:</span></span>

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

<span data-ttu-id="b0f1a-170">Notez que pour les déploiements de production des certificats doivent être utilisées pour hello autorité de certification pour le chiffrement, hello du certificat de serveur et les certificats clients.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-170">Please note that for production deployments separate certificates should be used for hello CA, for encryption, hello Server certificate and client certificates.</span></span> <span data-ttu-id="b0f1a-171">Pour plus d’informations, consultez la rubrique [Configuration de la sécurité](sql-database-elastic-scale-split-merge-security-configuration.md).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-171">For detailed instructions on this, see [Security Configuration](sql-database-elastic-scale-split-merge-security-configuration.md).</span></span>

## <a name="deploy-your-service"></a><span data-ttu-id="b0f1a-172">Déployer votre service</span><span class="sxs-lookup"><span data-stu-id="b0f1a-172">Deploy your service</span></span>
1. <span data-ttu-id="b0f1a-173">Accédez toohello [portail Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-173">Go toohello [Azure portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="b0f1a-174">Cliquez sur hello **Services de cloud computing** sur hello gauche et sélectionnez le service de cloud computing hello que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-174">Click hello **Cloud Services** tab on hello left, and select hello cloud service that you created earlier.</span></span>
3. <span data-ttu-id="b0f1a-175">Cliquez sur **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-175">Click **Dashboard**.</span></span>
4. <span data-ttu-id="b0f1a-176">Choisissez hello environnement intermédiaire, puis cliquez sur **Téléchargez un nouveau déploiement intermédiaire**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-176">Choose hello staging environment, then click **Upload a new staging deployment**.</span></span>
   
   ![Staging][3]
5. <span data-ttu-id="b0f1a-178">Dans la boîte de dialogue hello, entrez une étiquette de déploiement.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-178">In hello dialog box, enter a deployment label.</span></span> <span data-ttu-id="b0f1a-179">« Package » et « Configuration », cliquez sur 'À partir de Local', puis choisissez hello **SplitMergeService.cspkg** de fichiers et votre fichier .cscfg que vous avez configuré précédemment.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-179">For both 'Package' and 'Configuration', click 'From Local' and choose hello **SplitMergeService.cspkg** file and your .cscfg file that you configured earlier.</span></span>
6. <span data-ttu-id="b0f1a-180">Vérifiez cette case à cocher hello **déployer même si un ou plusieurs rôles contiennent une seule instance** est activée.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-180">Ensure that hello checkbox labeled **Deploy even if one or more roles contain a single instance** is checked.</span></span>
7. <span data-ttu-id="b0f1a-181">Hello graduation bouton dans le déploiement de hello hello bas toobegin droit d’accès.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-181">Hit hello tick button in hello bottom right toobegin hello deployment.</span></span> <span data-ttu-id="b0f1a-182">Tootake attendez quelques minutes toocomplete.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-182">Expect it tootake a few minutes toocomplete.</span></span>

   ![Télécharger][4]

## <a name="troubleshoot-hello-deployment"></a><span data-ttu-id="b0f1a-184">Résoudre les problèmes de déploiement de hello</span><span class="sxs-lookup"><span data-stu-id="b0f1a-184">Troubleshoot hello deployment</span></span>
<span data-ttu-id="b0f1a-185">Si votre rôle web échoue toocome en ligne, il est probablement un problème de configuration de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-185">If your web role fails toocome online, it is likely a problem with hello security configuration.</span></span> <span data-ttu-id="b0f1a-186">Vérifiez que hello que SSL est configuré comme décrit ci-dessus.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-186">Check that hello SSL is configured as described above.</span></span>

<span data-ttu-id="b0f1a-187">Si votre rôle de travail échoue toocome en ligne, mais il se peut que votre rôle web réussit, il est très probablement un problème de connexion toohello état de base de données que vous avez créé précédemment.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-187">If your worker role fails toocome online, but your web role succeeds, it is most likely a problem connecting toohello status database that you created earlier.</span></span>

* <span data-ttu-id="b0f1a-188">Assurez-vous que la chaîne de connexion hello dans votre fichier .cscfg est exact.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-188">Make sure that hello connection string in your .cscfg is accurate.</span></span>
* <span data-ttu-id="b0f1a-189">Vérification de la base de données et serveur de hello existent et que l’id d’utilisateur hello et le mot de passe sont corrects.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-189">Check that hello server and database exist, and that hello user id and password are correct.</span></span>
* <span data-ttu-id="b0f1a-190">Pour la base de données SQL Azure, la chaîne de connexion hello doit être sous forme de hello :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-190">For Azure SQL DB, hello connection string should be of hello form:</span></span>

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* <span data-ttu-id="b0f1a-191">Vérifiez que nom de serveur hello ne commence pas par **https://**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-191">Ensure that hello server name does not begin with **https://**.</span></span>
* <span data-ttu-id="b0f1a-192">Vérifiez que votre serveur de base de données SQL Azure autorise des Services Azure tooconnect tooit.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-192">Ensure that your Azure SQL DB server allows Azure Services tooconnect tooit.</span></span> <span data-ttu-id="b0f1a-193">toodo, ouvrez https://manage.windowsazure.com et cliquez sur « Bases de données SQL » sur hello gauche, cliquez sur « Serveurs » en haut de hello, sélectionnez votre serveur.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-193">toodo this, open https://manage.windowsazure.com, click “SQL Databases” on hello left, click “Servers” at hello top, and select your server.</span></span> <span data-ttu-id="b0f1a-194">Cliquez sur **configurer** à hello principaux et vous assurer que hello **Services Azure** est défini trop « Oui ».</span><span class="sxs-lookup"><span data-stu-id="b0f1a-194">Click **Configure** at hello top and ensure that hello **Azure Services** setting is set too“Yes”.</span></span> <span data-ttu-id="b0f1a-195">(Consultez les conditions préalables de hello section haut hello de cet article).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-195">(See hello Prerequisites section at hello top of this article).</span></span>

## <a name="test-hello-service-deployment"></a><span data-ttu-id="b0f1a-196">Tester le déploiement du service hello</span><span class="sxs-lookup"><span data-stu-id="b0f1a-196">Test hello service deployment</span></span>
### <a name="connect-with-a-web-browser"></a><span data-ttu-id="b0f1a-197">Se connecter avec un navigateur Web</span><span class="sxs-lookup"><span data-stu-id="b0f1a-197">Connect with a web browser</span></span>
<span data-ttu-id="b0f1a-198">Déterminer le point de terminaison hello web de votre service de fusion et fractionnement.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-198">Determine hello web endpoint of your Split-Merge service.</span></span> <span data-ttu-id="b0f1a-199">Vous pouvez le trouver dans hello portail classique Azure en accédant de toohello **tableau de bord** de votre service cloud et sous **URL du Site** sur le côté droit de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-199">You can find this in hello Azure Classic Portal by going toohello **Dashboard** of your cloud service and looking under **Site URL** on hello right side.</span></span> <span data-ttu-id="b0f1a-200">Remplacez **http://** avec **https://** étant donné que les paramètres de sécurité par défaut hello désactivent le point de terminaison hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-200">Replace **http://** with **https://** since hello default security settings disable hello HTTP endpoint.</span></span> <span data-ttu-id="b0f1a-201">Charger la page hello pour cette URL dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-201">Load hello page for this URL into your browser.</span></span>

### <a name="test-with-powershell-scripts"></a><span data-ttu-id="b0f1a-202">Effectuer des tests avec des scripts PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0f1a-202">Test with PowerShell scripts</span></span>
<span data-ttu-id="b0f1a-203">déploiement de Hello et votre environnement peuvent être testés en exécutant des scripts PowerShell d’exemple hello inclus.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-203">hello deployment and your environment can be tested by running hello included sample PowerShell scripts.</span></span>

<span data-ttu-id="b0f1a-204">les fichiers de script Hello inclus sont :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-204">hello script files included are:</span></span>

1. <span data-ttu-id="b0f1a-205">**SetupSampleSplitMergeEnvironment.ps1** : configure une couche de données de test pour la fusion et le fractionnement (voir le tableau ci-dessous pour obtenir une description détaillée)</span><span class="sxs-lookup"><span data-stu-id="b0f1a-205">**SetupSampleSplitMergeEnvironment.ps1** - sets up a test data tier for Split/Merge (see table below for detailed description)</span></span>
2. <span data-ttu-id="b0f1a-206">**ExecuteSampleSplitMerge.ps1** -exécute des opérations de test sur le test de hello couche données (voir le tableau ci-dessous pour une description détaillée)</span><span class="sxs-lookup"><span data-stu-id="b0f1a-206">**ExecuteSampleSplitMerge.ps1** - executes test operations on hello test data tier (see table below for detailed description)</span></span>
3. <span data-ttu-id="b0f1a-207">**GetMappings.ps1** - niveau supérieur exemple de script qui imprime état actuel de hello de mappages de partition hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-207">**GetMappings.ps1** - top-level sample script that prints out hello current state of hello shard mappings.</span></span>
4. <span data-ttu-id="b0f1a-208">**ShardManagement.psm1** -script d’assistance qui encapsule hello ShardManagement API</span><span class="sxs-lookup"><span data-stu-id="b0f1a-208">**ShardManagement.psm1**  - helper script that wraps hello ShardManagement API</span></span>
5. <span data-ttu-id="b0f1a-209">**SqlDatabaseHelpers.psm1** : script d’assistance pour la création et la gestion des bases de données SQL</span><span class="sxs-lookup"><span data-stu-id="b0f1a-209">**SqlDatabaseHelpers.psm1** - helper script for creating and managing SQL databases</span></span>
   
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="b0f1a-210">Fichier PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0f1a-210">PowerShell file</span></span></th>
       <th><span data-ttu-id="b0f1a-211">Étapes</span><span class="sxs-lookup"><span data-stu-id="b0f1a-211">Steps</span></span></th>
     </tr>
     <tr>
       <th rowspan="5"><span data-ttu-id="b0f1a-212">SetupSampleSplitMergeEnvironment.ps1</span><span class="sxs-lookup"><span data-stu-id="b0f1a-212">SetupSampleSplitMergeEnvironment.ps1</span></span></th>
       <td>1.    <span data-ttu-id="b0f1a-213">Crée une base de données pour le Gestionnaire de cartes de partitions</span><span class="sxs-lookup"><span data-stu-id="b0f1a-213">Creates a shard map manager database</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="b0f1a-214">Crée 2&#160;bases de données de partition.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-214">Creates 2 shard databases.</span></span>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="b0f1a-215">Crée une carte de partitions pour les bases de données concernées (supprime les cartes de partitions existantes sur ces dernières).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-215">Creates a shard map for those database (deletes any existing shard maps on those databases).</span></span> </td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="b0f1a-216">Crée un petit exemple de table dans les deux partitions hello et remplit la table hello dans une des partitions de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-216">Creates a small sample table in both hello shards, and populates hello table in one of hello shards.</span></span></td>
     </tr>
     <tr>
       <td>5.    <span data-ttu-id="b0f1a-217">Déclare hello SchemaInfo pour une table partitionnée de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-217">Declares hello SchemaInfo for hello sharded table.</span></span></td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th><span data-ttu-id="b0f1a-218">Fichier PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0f1a-218">PowerShell file</span></span></th>
       <th><span data-ttu-id="b0f1a-219">Étapes</span><span class="sxs-lookup"><span data-stu-id="b0f1a-219">Steps</span></span></th>
     </tr>
   <tr>
       <th rowspan="4"><span data-ttu-id="b0f1a-220">ExecuteSampleSplitMerge.ps1</span><span class="sxs-lookup"><span data-stu-id="b0f1a-220">ExecuteSampleSplitMerge.ps1</span></span> </th>
       <td>1.    <span data-ttu-id="b0f1a-221">Envoie un fractionnement demande toohello fusion et fractionnement Service serveur web frontal, qui fractionne les données de salutation moitié à partir de la partition deuxième hello première partition toohello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-221">Sends a split request toohello Split-Merge Service web frontend, which splits half hello data from hello first shard toohello second shard.</span></span></td>
     </tr>
     <tr>
       <td>2.    <span data-ttu-id="b0f1a-222">Interroge hello serveur web frontal pour hello fractionner le statut de la demande et attend jusqu'à ce que la demande de hello se termine.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-222">Polls hello web frontend for hello split request status and waits until hello request completes.</span></span></td>
     </tr>
     <tr>
       <td>3.    <span data-ttu-id="b0f1a-223">Envoie un fusion demande toohello fusion et fractionnement Service serveur web frontal, ce qui déplace les données de salutation à partir de la partition première hello deuxième partition toohello précédent.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-223">Sends a merge request toohello Split-Merge Service web frontend, which moves hello data from hello second shard back toohello first shard.</span></span></td>
     </tr>
     <tr>
       <td>4.    <span data-ttu-id="b0f1a-224">Interroge hello serveur web frontal pour l’état de demande de fusion de hello et attend la fin de la demande de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-224">Polls hello web frontend for hello merge request status and waits until hello request completes.</span></span></td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a><span data-ttu-id="b0f1a-225">Utilisez PowerShell tooverify votre déploiement</span><span class="sxs-lookup"><span data-stu-id="b0f1a-225">Use PowerShell tooverify your deployment</span></span>
1. <span data-ttu-id="b0f1a-226">Ouvrez une nouvelle fenêtre PowerShell et accédez répertoire toohello où vous avez téléchargé le package de fusion et fractionnement hello puis naviguez jusqu’au répertoire de « powershell » hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-226">Open a new PowerShell window and navigate toohello directory where you downloaded hello Split-Merge package, and then navigate into hello “powershell” directory.</span></span>
2. <span data-ttu-id="b0f1a-227">Créer un serveur de base de données SQL Azure (ou choisissez un serveur existant) où le Gestionnaire de carte de partitions hello et partitions seront créées.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-227">Create an Azure SQL database server (or choose an existing server) where hello shard map manager and shards will be created.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="b0f1a-228">Hello SetupSampleSplitMergeEnvironment.ps1 script crée ces bases de données sur hello même serveur par le script de hello tookeep par défaut simple.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-228">hello SetupSampleSplitMergeEnvironment.ps1 script creates all these databases on hello same server by default tookeep hello script simple.</span></span> <span data-ttu-id="b0f1a-229">Cela n’est pas une restriction de hello fusion et fractionnement Service lui-même.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-229">This is not a restriction of hello Split-Merge Service itself.</span></span>
   >
   
   <span data-ttu-id="b0f1a-230">Une connexion d’authentification SQL avec toohello d’accès en lecture/écriture qu'aux bases de données seront nécessaires pour hello toomove données du service de fusion et fractionnement et de la carte de partitions hello mise à jour.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-230">A SQL authentication login with read/write access toohello DBs will be needed for hello Split-Merge service toomove data and update hello shard map.</span></span> <span data-ttu-id="b0f1a-231">Étant donné que hello fusion et fractionnement Service s’exécute dans le cloud de hello, il ne prend pas en charge l’authentification intégrée.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-231">Since hello Split-Merge Service runs in hello cloud, it does not currently support Integrated Authentication.</span></span>
   
   <span data-ttu-id="b0f1a-232">Vérifiez que hello Azure SQL server est configuré tooallow l’accès à partir de l’adresse IP de hello d’ordinateur hello ces scripts en cours d’exécution.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-232">Make sure hello Azure SQL server is configured tooallow access from hello IP address of hello machine running these scripts.</span></span> <span data-ttu-id="b0f1a-233">Vous pouvez trouver ce paramètre sous hello Azure SQL server / configuration / adresses IP autorisées.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-233">You can find this setting under hello Azure SQL server / configuration / allowed IP addresses.</span></span>
3. <span data-ttu-id="b0f1a-234">Exécutez hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello exemple d’environnement.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-234">Execute hello SetupSampleSplitMergeEnvironment.ps1 script toocreate hello sample environment.</span></span>
   
   <span data-ttu-id="b0f1a-235">Ce script en cours d’exécution sera effacer toutes les données de gestion de carte partitions existantes des structures sur la base de données du gestionnaire carte hello partitions et les partitions hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-235">Running this script will wipe out any existing shard map management data structures on hello shard map manager database and hello shards.</span></span> <span data-ttu-id="b0f1a-236">Il peut être script de hello toorerun utile si vous le souhaitez carte de partitions hello toore d’initialiser ou de partitions.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-236">It may be useful toorerun hello script if you wish toore-initialize hello shard map or shards.</span></span>
   
   <span data-ttu-id="b0f1a-237">Exemple de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-237">Sample command line:</span></span>

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. <span data-ttu-id="b0f1a-238">Exécutez hello Getmappings.ps1 tooview hello mappages de script qui existent actuellement dans l’environnement d’exemple hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-238">Execute hello Getmappings.ps1 script tooview hello mappings that currently exist in hello sample environment.</span></span>
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. <span data-ttu-id="b0f1a-239">Exécutez hello ExecuteSampleSplitMerge.ps1 script tooexecute une opération split (déplacement de données de hello moitié sur les partitions deuxième hello première partition toohello), puis une opération de fusion (déplacement des données de hello sur les partitions première hello).</span><span class="sxs-lookup"><span data-stu-id="b0f1a-239">Execute hello ExecuteSampleSplitMerge.ps1 script tooexecute a split operation (moving half hello data on hello first shard toohello second shard) and then a merge operation (moving hello data back onto hello first shard).</span></span> <span data-ttu-id="b0f1a-240">Si vous avez configuré SSL et le point de terminaison http hello gauche désactivé, assurez-vous que vous utilisez point de terminaison hello https:// à la place.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-240">If you configured SSL and left hello http endpoint disabled, ensure that you use hello https:// endpoint instead.</span></span>
   
   <span data-ttu-id="b0f1a-241">Exemple de ligne de commande :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-241">Sample command line:</span></span>

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   <span data-ttu-id="b0f1a-242">Si vous recevez hello erreur ci-dessous, il s’agit probablement d’un problème avec le certificat du votre point de terminaison Web.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-242">If you receive hello below error, it is most likely a problem with your Web endpoint’s certificate.</span></span> <span data-ttu-id="b0f1a-243">Essayez de vous connecter le point de terminaison toohello Web avec votre navigateur Web favoris et vérifier s’il existe une erreur de certificat.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-243">Try connecting toohello Web endpoint with your favorite Web browser and check if there is a certificate error.</span></span>
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   <span data-ttu-id="b0f1a-244">Si elle a réussi, sortie de hello doit ressembler à hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-244">If it succeeded, hello output should look like hello below:</span></span>
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. <span data-ttu-id="b0f1a-245">Faites des essais avec d’autres types de données.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-245">Experiment with other data types!</span></span> <span data-ttu-id="b0f1a-246">Tous ces scripts prennent un paramètre - ShardKeyType facultatif qui vous permet de type de clé toospecify hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-246">All of these scripts take an optional -ShardKeyType parameter that allows you toospecify hello key type.</span></span> <span data-ttu-id="b0f1a-247">valeur par défaut Hello est Int32, mais vous pouvez également spécifier Int64, Guid ou binaire.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-247">hello default is Int32, but you can also specify Int64, Guid, or Binary.</span></span>

## <a name="create-requests"></a><span data-ttu-id="b0f1a-248">Créer des requêtes</span><span class="sxs-lookup"><span data-stu-id="b0f1a-248">Create requests</span></span>
<span data-ttu-id="b0f1a-249">service de Hello peut être utilisé à l’aide de l’interface utilisateur web de hello ou par l’importation et à l’aide du module de SplitMerge.psm1 PowerShell hello qui envoie vos demandes via le rôle web de hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-249">hello service can be used either by using hello web UI or by importing and using hello SplitMerge.psm1 PowerShell module which will submit your requests through hello web role.</span></span>

<span data-ttu-id="b0f1a-250">service de Hello peut déplacer des données dans les tables partitionnées et les tables de référence.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-250">hello service can move data in both sharded tables and reference tables.</span></span> <span data-ttu-id="b0f1a-251">Une table partitionnée possède une colonne de clés de partitionnement et comporte des données de ligne différentes sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-251">A sharded table has a sharding key column and has different row data on each shard.</span></span> <span data-ttu-id="b0f1a-252">Une table de référence n’est pas partitionnée afin qu’il contient hello même ligne de données sur chaque partition.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-252">A reference table is not sharded so it contains hello same row data on every shard.</span></span> <span data-ttu-id="b0f1a-253">Tables de référence sont utiles pour les données qui ne changent pas souvent et sont tooJOIN utilisé avec des tables partitionnées dans les requêtes.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-253">Reference tables are useful for data that does not change often and is used tooJOIN with sharded tables in queries.</span></span>

<span data-ttu-id="b0f1a-254">Dans l’ordre tooperform une opération de fusion et fractionnement, vous devez déclarer les tables partitionnées hello et les tables de référence que vous souhaitez toohave déplacé.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-254">In order tooperform a split-merge operation, you must declare hello sharded tables and reference tables that you want toohave moved.</span></span> <span data-ttu-id="b0f1a-255">Cela est accompli par hello **SchemaInfo** API.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-255">This is accomplished with hello **SchemaInfo** API.</span></span> <span data-ttu-id="b0f1a-256">Cette API méthode est Bonjour **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** espace de noms.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-256">This API is in hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** namespace.</span></span>

1. <span data-ttu-id="b0f1a-257">Pour chaque table partitionnée, créez un **ShardedTableInfo** objet décrivant le nom de schéma de la table hello parent (facultatif, par défaut est trop « dbo »), hello du nom de la table et hello nom de colonne dans la table qui contient la clé de partitionnement hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-257">For each sharded table, create a **ShardedTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”), hello table name, and hello column name in that table that contains hello sharding key.</span></span>
2. <span data-ttu-id="b0f1a-258">Pour chaque table de référence, créez un **ReferenceTableInfo** objet décrivant le nom de schéma de la table hello parent (facultatif, par défaut est trop « dbo ») et le nom de la table hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-258">For each reference table, create a **ReferenceTableInfo** object describing hello table’s parent schema name (optional, defaults too“dbo”) and hello table name.</span></span>
3. <span data-ttu-id="b0f1a-259">Ajouter hello ci-dessus tooa d’objets TableInfo nouvelle **SchemaInfo** objet.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-259">Add hello above TableInfo objects tooa new **SchemaInfo** object.</span></span>
4. <span data-ttu-id="b0f1a-260">Obtenir une référence tooa **ShardMapManager** objet, puis appelez **GetSchemaInfoCollection**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-260">Get a reference tooa **ShardMapManager** object, and call **GetSchemaInfoCollection**.</span></span>
5. <span data-ttu-id="b0f1a-261">Ajouter hello **SchemaInfo** toohello **SchemaInfoCollection**, en fournissant le nom de mappage de partitions hello.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-261">Add hello **SchemaInfo** toohello **SchemaInfoCollection**, providing hello shard map name.</span></span>

<span data-ttu-id="b0f1a-262">Un exemple de cette peut être consulté dans hello SetupSampleSplitMergeEnvironment.ps1 script.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-262">An example of this can be seen in hello SetupSampleSplitMergeEnvironment.ps1 script.</span></span>

<span data-ttu-id="b0f1a-263">service de fusion et fractionnement de Hello ne crée pas de base de données cible hello (ou le schéma des tables de base de données hello) pour vous.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-263">hello Split-Merge service does not create hello target database (or schema for any tables in hello database) for you.</span></span> <span data-ttu-id="b0f1a-264">Ils doivent être créés au préalable avant l’envoi d’un service de toohello de demande.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-264">They must be pre-created before sending a request toohello service.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="b0f1a-265">Résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="b0f1a-265">Troubleshooting</span></span>
<span data-ttu-id="b0f1a-266">Vous pouvez voir hello message ci-après lors de l’exécution des scripts powershell hello exemple :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-266">You may see hello below message when running hello sample powershell scripts:</span></span>

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

<span data-ttu-id="b0f1a-267">Cette erreur signifie que votre certificat SSL n’est pas correctement configuré.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-267">This error means that your SSL certificate is not configured correctly.</span></span> <span data-ttu-id="b0f1a-268">Suivez les instructions de hello dans la section « Connexion avec un navigateur web ».</span><span class="sxs-lookup"><span data-stu-id="b0f1a-268">Please follow hello instructions in section 'Connecting with a web browser'.</span></span>

<span data-ttu-id="b0f1a-269">Si vous ne pouvez pas soumettre les demandes, vous pouvez voir ceci :</span><span class="sxs-lookup"><span data-stu-id="b0f1a-269">If you cannot submit requests you may see this:</span></span>

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

<span data-ttu-id="b0f1a-270">Dans ce cas, recherchez votre fichier de configuration, dans le paramètre hello particulier pour **WorkerRoleSynchronizationStorageAccountConnectionString**.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-270">In this case, check your configuration file, in particular hello setting for **WorkerRoleSynchronizationStorageAccountConnectionString**.</span></span> <span data-ttu-id="b0f1a-271">Cette erreur indique en général, que ce rôle de travail hello a pas pu initialiser la base de données des métadonnées de hello sur la première utilisation.</span><span class="sxs-lookup"><span data-stu-id="b0f1a-271">This error typically indicates that hello worker role could not successfully initialize hello metadata database on first use.</span></span> 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

