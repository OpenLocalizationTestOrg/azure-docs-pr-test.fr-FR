---
title: "aaaImport et une zone de domaine d’exportation du fichier tooAzure DNS à l’aide d’Azure CLI 1.0 | Documents Microsoft"
description: "Découvrez comment tooimport et exporter un serveur DNS de la zone fichier tooAzure DNS à l’aide d’Azure CLI 1.0"
services: dns
documentationcenter: na
author: georgewallace
manager: timlt
ms.assetid: f5797782-3005-4663-a488-ac0089809010
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/16/2016
ms.author: gwallace
ms.openlocfilehash: 4c3163395e151e9934c730349b828c612491016f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="import-and-export-a-dns-zone-file-using-hello-azure-cli-10"></a><span data-ttu-id="2e113-103">Importer et exporter un fichier de zone DNS à l’aide de hello Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="2e113-103">Import and export a DNS zone file using hello Azure CLI 1.0</span></span> 

<span data-ttu-id="2e113-104">Cet article vous guide tout au long de la tooimport et exportation de fichiers de zone DNS pour Azure DNS à l’aide de hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="2e113-104">This article walks you through how tooimport and export DNS zone files for Azure DNS using hello Azure CLI 1.0.</span></span>

## <a name="introduction-toodns-zone-migration"></a><span data-ttu-id="2e113-105">Migration de zone de présentation tooDNS</span><span class="sxs-lookup"><span data-stu-id="2e113-105">Introduction tooDNS zone migration</span></span>

<span data-ttu-id="2e113-106">Un fichier de zone DNS est un fichier texte qui contient les détails de chaque enregistrement de nom de domaine (DNS) dans la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in hello zone.</span></span> <span data-ttu-id="2e113-107">Il suit un format standard, ce qui permet le transfert d’enregistrements DNS entre différents systèmes DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="2e113-108">À l’aide d’un fichier de zone est rapide, fiable et pratique tootransfer une zone DNS dans ou hors d’Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-108">Using a zone file is a quick, reliable, and convenient way tootransfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="2e113-109">DNS Azure prend en charge l’importation et exportation des fichiers de zone à l’aide de hello Azure interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="2e113-109">Azure DNS supports importing and exporting zone files by using hello Azure command-line interface (CLI).</span></span> <span data-ttu-id="2e113-110">Importation de fichier de zone est **pas** actuellement pris en charge via Azure PowerShell ou hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-110">Zone file import is **not** currently supported via Azure PowerShell or hello Azure portal.</span></span>

<span data-ttu-id="2e113-111">Bonjour Azure CLI 1.0 est un outil de ligne de commande multiplateforme utilisé pour la gestion des services Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-111">hello Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="2e113-112">Il est disponible pour les plateformes Windows, Mac et Linux de hello de hello [page Téléchargements Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="2e113-112">It is available for hello Windows, Mac, and Linux platforms from hello [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="2e113-113">Prise en charge multiplateforme est important pour l’importation et exportation de fichiers de zone, étant donné que hello courants logiciel de serveur de nom, [lier](https://www.isc.org/downloads/bind/), s’exécute généralement sur Linux.</span><span class="sxs-lookup"><span data-stu-id="2e113-113">Cross-platform support is important for importing and exporting zone files, because hello most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="2e113-114">Il existe actuellement deux versions de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-114">There are currently two versions of hello Azure CLI.</span></span> <span data-ttu-id="2e113-115">CLI1.0 est basé sur Node.js et offre des commandes commençant par « azure ».</span><span class="sxs-lookup"><span data-stu-id="2e113-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="2e113-116">CLI2.0 est basé sur Python et offre des commandes commençant par « az ».</span><span class="sxs-lookup"><span data-stu-id="2e113-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="2e113-117">Importation de fichier de zone est pris en charge dans les deux versions, nous vous recommandons l’utilisation des commandes CLI1.0 hello, comme décrit dans cette page.</span><span class="sxs-lookup"><span data-stu-id="2e113-117">While zone file import is supported in both versions, we recommend using hello CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="2e113-118">Comment obtenir votre fichier de zone DNS existant</span><span class="sxs-lookup"><span data-stu-id="2e113-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="2e113-119">Avant d’importer un fichier de zone DNS dans le système DNS Azure, vous devez tooobtain une copie du fichier de zone hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-119">Before you import a DNS zone file into Azure DNS, you need tooobtain a copy of hello zone file.</span></span> <span data-ttu-id="2e113-120">source de Hello de ce fichier dépend de la zone DNS de hello actuellement héberge.</span><span class="sxs-lookup"><span data-stu-id="2e113-120">hello source of this file depends on where hello DNS zone is currently hosted.</span></span>

* <span data-ttu-id="2e113-121">Si votre zone DNS est hébergé par un service partenaire (par exemple, un bureau d’enregistrement de domaine, dédié fournisseur d’hébergement DNS ou fournisseur de cloud autre), ce service doit fournir le fichier de zone DNS hello capacité toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide hello ability toodownload hello DNS zone file.</span></span>
* <span data-ttu-id="2e113-122">Si votre zone DNS est hébergé sur le DNS de Windows, le dossier par défaut de hello pour les fichiers de zone hello est **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="2e113-122">If your DNS zone is hosted on Windows DNS, hello default folder for hello zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="2e113-123">fichier de zone tooeach Hello chemin d’accès complet s’affiche également sur hello **général** onglet de la console DNS de hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-123">hello full path tooeach zone file also shows on hello **General** tab of hello DNS console.</span></span>
* <span data-ttu-id="2e113-124">Si votre zone DNS est hébergé à l’aide de BIND, emplacement hello hello du fichier de zone pour chaque zone est spécifié dans le fichier de configuration de liaison hello **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="2e113-124">If your DNS zone is hosted by using BIND, hello location of hello zone file for each zone is specified in hello BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="2e113-125">Le format des fichiers de zone téléchargés à partir de GoDaddy diffère légèrement du format standard.</span><span class="sxs-lookup"><span data-stu-id="2e113-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="2e113-126">Vous avez besoin toocorrect cela avant d’importer ces fichiers de zone DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-126">You need toocorrect this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="2e113-127">Les noms DNS Bonjour RDATA de chaque enregistrement DNS sont spécifiés en tant que noms complets, mais ils n’ont pas une fin «. » Cela signifie qu’ils sont interprétés comme des noms relatifs par d’autres systèmes DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-127">DNS names in hello RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="2e113-128">Vous devez terminer hello tooappend tooedit hello zone fichier «. » tootheir noms avant de les importer dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-128">You need tooedit hello zone file tooappend hello terminating "." tootheir names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="2e113-129">Par exemple, hello l’enregistrement CNAME « www 3600 CNAME contoso.com » doit être modifié trop « contoso.com IN CNAME de www 3600. »</span><span class="sxs-lookup"><span data-stu-id="2e113-129">For example, hello CNAME record "www 3600 IN CNAME contoso.com" should be changed too"www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="2e113-130">(avec un «. » final).</span><span class="sxs-lookup"><span data-stu-id="2e113-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="2e113-131">Importation d’un fichier de zone DNS dans Azure DNS</span><span class="sxs-lookup"><span data-stu-id="2e113-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="2e113-132">L’importation d’un fichier de zone crée une nouvelle zone dans Azure DNS si celle-ci n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="2e113-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="2e113-133">Si la zone de hello existe déjà, hello jeux d’enregistrements dans le fichier de zone hello doit être fusionnés avec les jeux d’enregistrements existants hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-133">If hello zone already exists, hello record sets in hello zone file must be merged with hello existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="2e113-134">Comportement de la fusion</span><span class="sxs-lookup"><span data-stu-id="2e113-134">Merge behavior</span></span>

* <span data-ttu-id="2e113-135">Par défaut, les nouveaux jeux d’enregistrements sont fusionnés avec les jeux d’enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="2e113-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="2e113-136">Les enregistrements identiques dans un jeu d’enregistrements fusionné sont dédupliqués.</span><span class="sxs-lookup"><span data-stu-id="2e113-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="2e113-137">Vous pouvez également, en spécifiant hello `--force` option, hello remplace de processus d’importation des jeux d’enregistrements existants avec les nouveaux jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="2e113-137">Alternatively, by specifying hello `--force` option, hello import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="2e113-138">Jeux d’enregistrements existants qui n’ont pas un enregistrement correspondant défini dans le fichier de zone importé hello ne sont pas supprimés.</span><span class="sxs-lookup"><span data-stu-id="2e113-138">Existing record sets that do not have a corresponding record set in hello imported zone file are not be removed.</span></span>
* <span data-ttu-id="2e113-139">Lors de la fusion de jeux d’enregistrements, hello toolive TTL (time) préexistants de jeux d’enregistrements est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2e113-139">When record sets are merged, hello time toolive (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="2e113-140">Lorsque `--force` est utilisé, hello durée de vie d’un nouvel ensemble d’enregistrements hello est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2e113-140">When `--force` is used, hello TTL of hello new record set is used.</span></span>
* <span data-ttu-id="2e113-141">Début de paramètres d’autorité principale (SOA) (à l’exception de `host`) sont toujours effectuées à partir du fichier de zone importé hello, indépendamment du fait que `--force` est utilisé.</span><span class="sxs-lookup"><span data-stu-id="2e113-141">Start of Authority (SOA) parameters (except `host`) are always taken from hello imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="2e113-142">De même, pour hello enregistrement de serveur de noms défini au sommet de zone hello, hello TTL toujours provient du fichier de zone importé hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-142">Similarly, for hello name server record set at hello zone apex, hello TTL is always taken from hello imported zone file.</span></span>
* <span data-ttu-id="2e113-143">Un enregistrement CNAME importé ne remplace pas un enregistrement CNAME existant enregistre par hello même nom, sauf si hello `--force` paramètre est spécifié.</span><span class="sxs-lookup"><span data-stu-id="2e113-143">An imported CNAME record does not replace an existing CNAME record with hello same name unless hello `--force` parameter is specified.</span></span>
* <span data-ttu-id="2e113-144">Lorsqu’un conflit se produit entre un enregistrement CNAME et un autre enregistrement de même nom, mais il est différent de hello tapez (indépendamment de ce qui est existant ou nouveau), enregistrement de hello existant est conservé.</span><span class="sxs-lookup"><span data-stu-id="2e113-144">When a conflict arises between a CNAME record and another record of hello same name but different type (regardless of which is existing or new), hello existing record is retained.</span></span> <span data-ttu-id="2e113-145">Cette valeur est indépendante d’utilisation hello de `--force`.</span><span class="sxs-lookup"><span data-stu-id="2e113-145">This is independent of hello use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="2e113-146">Informations supplémentaires sur l’importation</span><span class="sxs-lookup"><span data-stu-id="2e113-146">Additional information about importing</span></span>

<span data-ttu-id="2e113-147">Hello remarques suivantes fournissent des informations techniques sur fuseau de hello processus d’importation.</span><span class="sxs-lookup"><span data-stu-id="2e113-147">hello following notes provide additional technical details about hello zone import process.</span></span>

* <span data-ttu-id="2e113-148">Hello `$TTL` la directive est facultative et il est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2e113-148">hello `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="2e113-149">Lorsqu’aucun `$TTL` la directive est fournie, l’importation des enregistrements sans une durée de vie explicite définir la valeur par défaut de tooa durée de vie de 3 600 secondes.</span><span class="sxs-lookup"><span data-stu-id="2e113-149">When no `$TTL` directive is given, records without an explicit TTL are imported set tooa default TTL of 3600 seconds.</span></span> <span data-ttu-id="2e113-150">Lorsque deux enregistre dans le même jeu d’enregistrements hello spécifier TTLs différents, une valeur inférieure hello est utilisée.</span><span class="sxs-lookup"><span data-stu-id="2e113-150">When two records in hello same record set specify different TTLs, hello lower value is used.</span></span>
* <span data-ttu-id="2e113-151">Hello `$ORIGIN` la directive est facultative et il est pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2e113-151">hello `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="2e113-152">Lorsqu’aucun `$ORIGIN` est définie par défaut de hello valeur utilisée est le nom de la zone hello tel que spécifié sur la ligne de commande hello (ainsi que la fin d’exécution hello «. »).</span><span class="sxs-lookup"><span data-stu-id="2e113-152">When no `$ORIGIN` is set, hello default value used is hello zone name as specified on hello command line (plus hello terminating ".").</span></span>
* <span data-ttu-id="2e113-153">Hello `$INCLUDE` et `$GENERATE` directives ne sont pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2e113-153">hello `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="2e113-154">Les types d’enregistrements A, AAAA, CNAME, MX, NS, SOA, SRV et TXT sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="2e113-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="2e113-155">Hello enregistrement SOA est créé automatiquement par le système DNS Azure lors de la création d’une zone.</span><span class="sxs-lookup"><span data-stu-id="2e113-155">hello SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="2e113-156">Lorsque vous importez un fichier de zone, tous les paramètres SOA proviennent du fichier de zone hello *sauf* hello `host` paramètre.</span><span class="sxs-lookup"><span data-stu-id="2e113-156">When you import a zone file, all SOA parameters are taken from hello zone file *except* hello `host` parameter.</span></span> <span data-ttu-id="2e113-157">Ce paramètre utilise la valeur hello fournie par le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-157">This parameter uses hello value provided by Azure DNS.</span></span> <span data-ttu-id="2e113-158">Il s’agit, car ce paramètre doit désigner le serveur de noms principal toohello fournie par le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-158">This is because this parameter must refer toohello primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="2e113-159">Hello nom serveur jeu d’enregistrements au sommet de zone hello sont également créé automatiquement par le système DNS Azure lors de la zone de hello est créée.</span><span class="sxs-lookup"><span data-stu-id="2e113-159">hello name server record set at hello zone apex is also created automatically by Azure DNS when hello zone is created.</span></span> <span data-ttu-id="2e113-160">Uniquement hello durée de vie de ce jeu d’enregistrements est importée.</span><span class="sxs-lookup"><span data-stu-id="2e113-160">Only hello TTL of this record set is imported.</span></span> <span data-ttu-id="2e113-161">Ces enregistrements contiennent des noms de serveur de nom hello fournies par le système DNS Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-161">These records contain hello name server names provided by Azure DNS.</span></span> <span data-ttu-id="2e113-162">données d’enregistrement de Hello ne sont pas remplacées par valeurs hello contenues dans le fichier de zone importé hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-162">hello record data is not overwritten by hello values contained in hello imported zone file.</span></span>
* <span data-ttu-id="2e113-163">Pour la version préliminaire publique, Azure DNS prend uniquement en charge les enregistrements à chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="2e113-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="2e113-164">Chaîne multiple enregistrements TXT sont être concaténées et tronquée too255 caractères.</span><span class="sxs-lookup"><span data-stu-id="2e113-164">Multistring TXT records are be concatenated and truncated too255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="2e113-165">Format et valeurs de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="2e113-165">CLI format and values</span></span>

<span data-ttu-id="2e113-166">format Hello tooimport de commande CLI d’Azure hello une zone DNS est :</span><span class="sxs-lookup"><span data-stu-id="2e113-166">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2e113-167">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="2e113-167">Values:</span></span>

* <span data-ttu-id="2e113-168">`<resource group>`est le nom hello hello du groupe de ressources pour la zone DNS Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-168">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="2e113-169">`<zone name>`est le nom hello de zone de hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-169">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="2e113-170">`<zone file name>`est le nom de chemin/hello de toobe de fichier de zone hello importé.</span><span class="sxs-lookup"><span data-stu-id="2e113-170">`<zone file name>` is hello path/name of hello zone file toobe imported.</span></span>

<span data-ttu-id="2e113-171">Si une zone portant ce nom n’existe pas dans le groupe de ressources hello, il est créé pour vous.</span><span class="sxs-lookup"><span data-stu-id="2e113-171">If a zone with this name does not exist in hello resource group, it is created for you.</span></span> <span data-ttu-id="2e113-172">Si hello zone existe déjà, hello jeux d’enregistrements importés est fusionnés avec les jeux d’enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="2e113-172">If hello zone already exists, hello imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="2e113-173">toooverwrite hello existant jeux d’enregistrements, utilisez hello `--force` option.</span><span class="sxs-lookup"><span data-stu-id="2e113-173">toooverwrite hello existing record sets, use hello `--force` option.</span></span>

<span data-ttu-id="2e113-174">format de hello tooverify d’un fichier de zone sans réellement son importation, utilisez hello `--parse-only` option.</span><span class="sxs-lookup"><span data-stu-id="2e113-174">tooverify hello format of a zone file without actually importing it, use hello `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="2e113-175">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="2e113-175">Step 1.</span></span> <span data-ttu-id="2e113-176">Importer un fichier de zone</span><span class="sxs-lookup"><span data-stu-id="2e113-176">Import a zone file</span></span>

<span data-ttu-id="2e113-177">tooimport un fichier de zone de hello **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="2e113-177">tooimport a zone file for hello zone **contoso.com**.</span></span>

1. <span data-ttu-id="2e113-178">Se connecter tooyour abonnement Azure à l’aide de hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="2e113-178">Sign in tooyour Azure subscription by using hello Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2e113-179">Sélectionnez l’abonnement hello où vous souhaitez toocreate votre nouvelle zone DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-179">Select hello subscription where you want toocreate your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2e113-180">Azure DNS étant un service Gestionnaire de ressources uniquement Azure, hello CLI d’Azure doit être en mode de gestionnaire de tooResource commuté.</span><span class="sxs-lookup"><span data-stu-id="2e113-180">Azure DNS is an Azure Resource Manager-only service, so hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2e113-181">Avant d’utiliser service DNS Azure de hello, vous devez inscrire votre fournisseur de ressources abonnement toouse hello Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="2e113-181">Before you use hello Azure DNS service, you must register your subscription toouse hello Microsoft.Network resource provider.</span></span> <span data-ttu-id="2e113-182">(Cette opération n’est à effectuer qu’une fois pour chaque abonnement.)</span><span class="sxs-lookup"><span data-stu-id="2e113-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="2e113-183">Si vous n’avez pas déjà, vous devez également toocreate un groupe de ressources du Gestionnaire de ressources.</span><span class="sxs-lookup"><span data-stu-id="2e113-183">If you don't have one already, you also need toocreate a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="2e113-184">zone de hello tooimport **contoso.com** à partir du fichier de hello **contoso.com.txt** dans une zone DNS dans le groupe de ressources hello **myresourcegroup**, exécutez la commande de hello `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="2e113-184">tooimport hello zone **contoso.com** from hello file **contoso.com.txt** into a new DNS zone in hello resource group **myresourcegroup**, run hello command `azure network dns zone import`.</span></span><BR><span data-ttu-id="2e113-185">Cette commande charge le fichier de zone hello et l’analyser.</span><span class="sxs-lookup"><span data-stu-id="2e113-185">This command loads hello zone file and parse it.</span></span> <span data-ttu-id="2e113-186">commande Hello exécute une série de commandes sur fuseau de hello Azure DNS service toocreate hello et tous les enregistrements de hello définit dans la zone de hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-186">hello command executes a series of commands on hello Azure DNS service toocreate hello zone and all hello record sets in hello zone.</span></span> <span data-ttu-id="2e113-187">commande Hello signale la progression dans la fenêtre de console hello, ainsi que les erreurs ou avertissements.</span><span class="sxs-lookup"><span data-stu-id="2e113-187">hello command reports progress in hello console window, along with any errors or warnings.</span></span> <span data-ttu-id="2e113-188">Étant donné que les jeux d’enregistrements est créés dans la série, il peut prendre quelques minutes tooimport un fichier de zone volumineux.</span><span class="sxs-lookup"><span data-stu-id="2e113-188">Because record sets are created in series, it may take a few minutes tooimport a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-hello-zone"></a><span data-ttu-id="2e113-189">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="2e113-189">Step 2.</span></span> <span data-ttu-id="2e113-190">Vérifiez que la zone de hello</span><span class="sxs-lookup"><span data-stu-id="2e113-190">Verify hello zone</span></span>

<span data-ttu-id="2e113-191">tooverify hello zone DNS après avoir importé le fichier de hello, vous pouvez utiliser l’une des méthodes suivantes de hello :</span><span class="sxs-lookup"><span data-stu-id="2e113-191">tooverify hello DNS zone after you import hello file, you can use any one of hello following methods:</span></span>

* <span data-ttu-id="2e113-192">Vous pouvez répertorier les enregistrements hello à l’aide de hello suivant commande CLI d’Azure :</span><span class="sxs-lookup"><span data-stu-id="2e113-192">You can list hello records by using hello following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="2e113-193">Vous pouvez répertorier les enregistrements hello en utilisant l’applet de commande PowerShell hello `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="2e113-193">You can list hello records by using hello PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="2e113-194">Vous pouvez utiliser `nslookup` tooverify résolution de noms pour les enregistrements de hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-194">You can use `nslookup` tooverify name resolution for hello records.</span></span> <span data-ttu-id="2e113-195">Zone de hello n’est pas déléguées encore, vous devez explicitement toospecify hello correct Azure serveurs DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-195">Because hello zone isn't delegated yet, you need toospecify hello correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="2e113-196">Hello exemple suivant montre comment les noms de serveur de nom tooretrieve hello assignés toohello zone.</span><span class="sxs-lookup"><span data-stu-id="2e113-196">hello following sample shows how tooretrieve hello name server names assigned toohello zone.</span></span> <span data-ttu-id="2e113-197">INFORMATIQUE montre également comment enregistre des tooquery hello « www » à l’aide de `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="2e113-197">IT also shows how tooquery hello "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up hello DNS Record Set "@" of type "NS"
        data:Id: /subscriptions/.../resourceGroups/myresourcegroup/providers/Microsoft.Network/dnszones/contoso.com/NS/@
        data:Name: @
        data:Type: Microsoft.Network/dnszones/NS
        data:Location: global
        data:TTL : 3600
        data:NS records
        data:Name server domain name : ns1-01.azure-dns.com
        data:Name server domain name : ns2-01.azure-dns.net
        data:Name server domain name : ns3-01.azure-dns.org
        data:Name server domain name : ns4-01.azure-dns.info
        data:
        info:network dns record-set show command OK

        C:\> nslookup www.contoso.com ns1-01.azure-dns.com

        Server: ns1-01.azure-dns.com
        Address:  40.90.4.1

        Name:www.contoso.com
        Addresses:  134.170.185.46
        134.170.188.221

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="2e113-198">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="2e113-198">Step 3.</span></span> <span data-ttu-id="2e113-199">Mettre à jour la délégation DNS</span><span class="sxs-lookup"><span data-stu-id="2e113-199">Update DNS delegation</span></span>

<span data-ttu-id="2e113-200">Après avoir vérifié que zone de hello a été importé correctement, vous devez tooupdate hello DNS délégation toopoint toohello Azure serveurs de noms DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-200">After you have verified that hello zone has been imported correctly, you need tooupdate hello DNS delegation toopoint toohello Azure DNS name servers.</span></span> <span data-ttu-id="2e113-201">Pour plus d’informations, voir l’article hello [mettre à jour la délégation DNS hello](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="2e113-201">For more information, see hello article [Update hello DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="2e113-202">Exportation d’un fichier de zone DNS à partir d’Azure DNS</span><span class="sxs-lookup"><span data-stu-id="2e113-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="2e113-203">format Hello tooimport de commande CLI d’Azure hello une zone DNS est :</span><span class="sxs-lookup"><span data-stu-id="2e113-203">hello format of hello Azure CLI command tooimport a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="2e113-204">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="2e113-204">Values:</span></span>

* <span data-ttu-id="2e113-205">`<resource group>`est le nom hello hello du groupe de ressources pour la zone DNS Azure hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-205">`<resource group>` is hello name of hello resource group for hello zone in Azure DNS.</span></span>
* <span data-ttu-id="2e113-206">`<zone name>`est le nom hello de zone de hello.</span><span class="sxs-lookup"><span data-stu-id="2e113-206">`<zone name>` is hello name of hello zone.</span></span>
* <span data-ttu-id="2e113-207">`<zone file name>`est le nom de chemin/hello de toobe de fichier de zone hello exportée.</span><span class="sxs-lookup"><span data-stu-id="2e113-207">`<zone file name>` is hello path/name of hello zone file toobe exported.</span></span>

<span data-ttu-id="2e113-208">Comme avec l’importation de zone hello, vous devez d’abord toosign dans, choisissez votre abonnement et configurer le mode de gestionnaire de ressources toouse hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-208">As with hello zone import, you first need toosign in, choose your subscription, and configure hello Azure CLI toouse Resource Manager mode.</span></span>

### <a name="tooexport-a-zone-file"></a><span data-ttu-id="2e113-209">tooexport un fichier de zone</span><span class="sxs-lookup"><span data-stu-id="2e113-209">tooexport a zone file</span></span>

1. <span data-ttu-id="2e113-210">Se connecter tooyour abonnement Azure à l’aide de hello CLI d’Azure.</span><span class="sxs-lookup"><span data-stu-id="2e113-210">Sign in tooyour Azure subscription by using hello Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="2e113-211">Sélectionnez l’abonnement hello où vous souhaitez toocreate votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="2e113-211">Select hello subscription where you want toocreate your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="2e113-212">Azure DNS est un service Azure Resource Manager uniquement.</span><span class="sxs-lookup"><span data-stu-id="2e113-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="2e113-213">Hello CLI d’Azure doit être en mode de gestionnaire de tooResource commuté.</span><span class="sxs-lookup"><span data-stu-id="2e113-213">hello Azure CLI must be switched tooResource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="2e113-214">tooexport hello zone DNS Azure existante **contoso.com** dans le groupe de ressources **myresourcegroup** toohello fichier **contoso.com.txt** (dans le dossier actif hello), exécutez `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="2e113-214">tooexport hello existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** toohello file **contoso.com.txt** (in hello current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="2e113-215">Cette commande appelle hello tooenumerate du service DNS Azure jeux d’enregistrements dans la zone de hello et exporter le fichier de zone hello résultats tooa liaison compatible.</span><span class="sxs-lookup"><span data-stu-id="2e113-215">This command  calls hello Azure DNS service tooenumerate record sets in hello zone and export hello results tooa BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
