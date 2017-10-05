---
title: "Importer et exporter un fichier de zone de domaine vers Azure DNS avec Azure CLI 1.0 | Microsoft Docs"
description: "Apprenez à importer et exporter un fichier de zone DNS vers Azure DNS à l’aide d’Azure CLI 1.0"
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
ms.openlocfilehash: d6d3fa7aa0e8b2462b3a6b4b66d3d87ab5535314
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="import-and-export-a-dns-zone-file-using-the-azure-cli-10"></a><span data-ttu-id="ada1b-103">Importer et exporter un fichier de zone DNS en utilisant Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="ada1b-103">Import and export a DNS zone file using the Azure CLI 1.0</span></span> 

<span data-ttu-id="ada1b-104">Cet article vous guide dans l’importation et l’exportation de fichiers de zone DNS pour Azure DNS à l’aide d’Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="ada1b-104">This article walks you through how to import and export DNS zone files for Azure DNS using the Azure CLI 1.0.</span></span>

## <a name="introduction-to-dns-zone-migration"></a><span data-ttu-id="ada1b-105">Introduction à la migration de zone DNS</span><span class="sxs-lookup"><span data-stu-id="ada1b-105">Introduction to DNS zone migration</span></span>

<span data-ttu-id="ada1b-106">Un fichier de zone DNS est un fichier texte qui contient les détails de tous les enregistrements DNS contenus dans la zone.</span><span class="sxs-lookup"><span data-stu-id="ada1b-106">A DNS zone file is a text file that contains details of every Domain Name System (DNS) record in the zone.</span></span> <span data-ttu-id="ada1b-107">Il suit un format standard, ce qui permet le transfert d’enregistrements DNS entre différents systèmes DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-107">It follows a standard format, making it suitable for transferring DNS records between DNS systems.</span></span> <span data-ttu-id="ada1b-108">L’utilisation d’un fichier de zone offre un moyen rapide, fiable et pratique de transférer une zone DNS vers ou depuis Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-108">Using a zone file is a quick, reliable, and convenient way to transfer a DNS zone into or out of Azure DNS.</span></span>

<span data-ttu-id="ada1b-109">Azure DNS prend en charge l’importation et l’exportation de fichiers de zone à l’aide de l’interface de ligne de commande (CLI).</span><span class="sxs-lookup"><span data-stu-id="ada1b-109">Azure DNS supports importing and exporting zone files by using the Azure command-line interface (CLI).</span></span> <span data-ttu-id="ada1b-110">L’importation de fichier de zone n’est actuellement **pas** prise en charge via Azure PowerShell ou le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="ada1b-110">Zone file import is **not** currently supported via Azure PowerShell or the Azure portal.</span></span>

<span data-ttu-id="ada1b-111">Azure CLI 1.0 est un outil de ligne de commande multiplateforme permettant de gérer des services Azure.</span><span class="sxs-lookup"><span data-stu-id="ada1b-111">The Azure CLI 1.0 is a cross-platform command-line tool used for managing Azure services.</span></span> <span data-ttu-id="ada1b-112">Elles est disponible pour les plateformes Windows, Mac et Linux sur la [page des téléchargements d’Azure](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ada1b-112">It is available for the Windows, Mac, and Linux platforms from the [Azure downloads page](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="ada1b-113">La prise en charge multiplateforme est importante pour l’importation et l’exportation de fichiers de zone car le logiciel serveur de noms le plus courant, [BIND](https://www.isc.org/downloads/bind/), s’exécute en général sur Linux.</span><span class="sxs-lookup"><span data-stu-id="ada1b-113">Cross-platform support is important for importing and exporting zone files, because the most common name server software, [BIND](https://www.isc.org/downloads/bind/), typically runs on Linux.</span></span>

> [!NOTE]
> <span data-ttu-id="ada1b-114">Il existe actuellement deux versions d’Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ada1b-114">There are currently two versions of the Azure CLI.</span></span> <span data-ttu-id="ada1b-115">CLI1.0 est basé sur Node.js et offre des commandes commençant par « azure ».</span><span class="sxs-lookup"><span data-stu-id="ada1b-115">CLI1.0 is based on Node.js, and has commands beginning with "azure".</span></span>
> <span data-ttu-id="ada1b-116">CLI2.0 est basé sur Python et offre des commandes commençant par « az ».</span><span class="sxs-lookup"><span data-stu-id="ada1b-116">CLI2.0 is based on Python and has commands beginning with "az".</span></span> <span data-ttu-id="ada1b-117">Si l’importation de fichier de zone est prise en charge dans les deux versions, nous recommandons d’utiliser les commandes CLI1.0, comme décrit dans cette page.</span><span class="sxs-lookup"><span data-stu-id="ada1b-117">While zone file import is supported in both versions, we recommend using the CLI1.0 commands, as described in this page.</span></span>

## <a name="obtain-your-existing-dns-zone-file"></a><span data-ttu-id="ada1b-118">Comment obtenir votre fichier de zone DNS existant</span><span class="sxs-lookup"><span data-stu-id="ada1b-118">Obtain your existing DNS zone file</span></span>

<span data-ttu-id="ada1b-119">Avant d’importer un fichier de zone DNS dans Azure DNS, vous devez obtenir une copie du fichier de zone.</span><span class="sxs-lookup"><span data-stu-id="ada1b-119">Before you import a DNS zone file into Azure DNS, you need to obtain a copy of the zone file.</span></span> <span data-ttu-id="ada1b-120">La source de ce fichier dépend de l’emplacement où la zone DNS est actuellement hébergée.</span><span class="sxs-lookup"><span data-stu-id="ada1b-120">The source of this file depends on where the DNS zone is currently hosted.</span></span>

* <span data-ttu-id="ada1b-121">Si votre zone DNS est hébergée par un service tiers (comme un bureau d’enregistrement de domaines, un hébergeur DNS dédié ou un autre fournisseur de cloud), ce service doit fournir la possibilité de télécharger le fichier de zone DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-121">If your DNS zone is hosted by a partner service (such as a domain registrar, dedicated DNS hosting provider, or alternative cloud provider), that service should provide the ability to download the DNS zone file.</span></span>
* <span data-ttu-id="ada1b-122">Si votre zone DNS est hébergée sur le DNS Windows, le dossier par défaut pour les fichiers de zone est **%systemroot%\system32\dns**.</span><span class="sxs-lookup"><span data-stu-id="ada1b-122">If your DNS zone is hosted on Windows DNS, the default folder for the zone files is **%systemroot%\system32\dns**.</span></span> <span data-ttu-id="ada1b-123">Le chemin complet vers chaque fichier de zone s’affiche également sous l’onglet **Général** de la console DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-123">The full path to each zone file also shows on the **General** tab of the DNS console.</span></span>
* <span data-ttu-id="ada1b-124">Si votre zone DNS est hébergée via BIND, l’emplacement du fichier de zone pour chaque zone est spécifié dans le fichier de configuration BIND, **named.conf**.</span><span class="sxs-lookup"><span data-stu-id="ada1b-124">If your DNS zone is hosted by using BIND, the location of the zone file for each zone is specified in the BIND configuration file **named.conf**.</span></span>

> [!NOTE]
> <span data-ttu-id="ada1b-125">Le format des fichiers de zone téléchargés à partir de GoDaddy diffère légèrement du format standard.</span><span class="sxs-lookup"><span data-stu-id="ada1b-125">Zone files downloaded from GoDaddy have a slightly nonstandard format.</span></span> <span data-ttu-id="ada1b-126">Vous devez corriger ce problème avant d’importer ces fichiers de zone dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-126">You need to correct this before you import these zone files into Azure DNS.</span></span>
>
> <span data-ttu-id="ada1b-127">Les noms DNS dans le RDATA de chaque enregistrement DNS sont considérés comme étant des noms complets, mais ils ne se terminent pas par un « . » Cela signifie qu’ils sont interprétés comme des noms relatifs par d’autres systèmes DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-127">DNS names in the RDATA of each DNS record are specified as fully qualified names, but they don't have a terminating "." This means they are interpreted by other DNS systems as relative names.</span></span> <span data-ttu-id="ada1b-128">Vous devez modifier le fichier de zone pour ajouter le point final à ces noms avant de les importer dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-128">You need to edit the zone file to append the terminating "." to their names before you import them into Azure DNS.</span></span>
>
> <span data-ttu-id="ada1b-129">Par exemple, l’enregistrement CNAME « www 3600 IN CNAME contoso.com » doit être remplacé par « www 3600 IN CNAME contoso.com. »</span><span class="sxs-lookup"><span data-stu-id="ada1b-129">For example, the CNAME record "www 3600 IN CNAME contoso.com" should be changed to "www 3600 IN CNAME contoso.com."</span></span>
> <span data-ttu-id="ada1b-130">(avec un «. » final).</span><span class="sxs-lookup"><span data-stu-id="ada1b-130">(with a terminating ".").</span></span>

## <a name="import-a-dns-zone-file-into-azure-dns"></a><span data-ttu-id="ada1b-131">Importation d’un fichier de zone DNS dans Azure DNS</span><span class="sxs-lookup"><span data-stu-id="ada1b-131">Import a DNS zone file into Azure DNS</span></span>

<span data-ttu-id="ada1b-132">L’importation d’un fichier de zone crée une nouvelle zone dans Azure DNS si celle-ci n’existe pas.</span><span class="sxs-lookup"><span data-stu-id="ada1b-132">Importing a zone file creates a new zone in Azure DNS if one does not already exist.</span></span> <span data-ttu-id="ada1b-133">Si la zone existe déjà, les jeux d’enregistrements du fichier de zone doivent être fusionnés avec les jeux d’enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="ada1b-133">If the zone already exists, the record sets in the zone file must be merged with the existing record sets.</span></span>

### <a name="merge-behavior"></a><span data-ttu-id="ada1b-134">Comportement de la fusion</span><span class="sxs-lookup"><span data-stu-id="ada1b-134">Merge behavior</span></span>

* <span data-ttu-id="ada1b-135">Par défaut, les nouveaux jeux d’enregistrements sont fusionnés avec les jeux d’enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="ada1b-135">By default, existing and new record sets are merged.</span></span> <span data-ttu-id="ada1b-136">Les enregistrements identiques dans un jeu d’enregistrements fusionné sont dédupliqués.</span><span class="sxs-lookup"><span data-stu-id="ada1b-136">Identical records within a merged record set are de-duplicated.</span></span>
* <span data-ttu-id="ada1b-137">Si vous spécifiez l’option `--force`, le processus d’importation remplace les jeux d’enregistrements existants par les nouveaux jeux d’enregistrements.</span><span class="sxs-lookup"><span data-stu-id="ada1b-137">Alternatively, by specifying the `--force` option, the import process replaces existing record sets with new record sets.</span></span> <span data-ttu-id="ada1b-138">Les jeux d’enregistrements existants qui ne correspondent pas à des jeux d’enregistrements du fichier de zone importé ne sont pas supprimés.</span><span class="sxs-lookup"><span data-stu-id="ada1b-138">Existing record sets that do not have a corresponding record set in the imported zone file are not be removed.</span></span>
* <span data-ttu-id="ada1b-139">Lorsque les jeux d’enregistrements sont fusionnés, la TTL des jeux d’enregistrements existants est utilisée.</span><span class="sxs-lookup"><span data-stu-id="ada1b-139">When record sets are merged, the time to live (TTL) of preexisting record sets is used.</span></span> <span data-ttu-id="ada1b-140">Quand l’option `--force` est utilisée, la durée de vie du nouveau jeu d’enregistrements est utilisée.</span><span class="sxs-lookup"><span data-stu-id="ada1b-140">When `--force` is used, the TTL of the new record set is used.</span></span>
* <span data-ttu-id="ada1b-141">Les paramètres SOA (Start of Authority) (excepté `host`) sont toujours pris dans le fichier de zone importé, que l’option `--force` soit ou non utilisée.</span><span class="sxs-lookup"><span data-stu-id="ada1b-141">Start of Authority (SOA) parameters (except `host`) are always taken from the imported zone file, regardless of whether `--force` is used.</span></span> <span data-ttu-id="ada1b-142">De même, pour le jeu d’enregistrements du serveur de noms à l’extrémité de la zone, la TTL est toujours dérivée du fichier de zone importé.</span><span class="sxs-lookup"><span data-stu-id="ada1b-142">Similarly, for the name server record set at the zone apex, the TTL is always taken from the imported zone file.</span></span>
* <span data-ttu-id="ada1b-143">Un enregistrement CNAME importé ne remplace pas un enregistrement CNAME existant portant le même nom, sauf si le paramètre `--force` est spécifié.</span><span class="sxs-lookup"><span data-stu-id="ada1b-143">An imported CNAME record does not replace an existing CNAME record with the same name unless the `--force` parameter is specified.</span></span>
* <span data-ttu-id="ada1b-144">En cas de conflit entre un enregistrement CNAME et un autre enregistrement du même nom ayant un type différent (qu’il soit nouveau ou existant), l’enregistrement existant est conservé.</span><span class="sxs-lookup"><span data-stu-id="ada1b-144">When a conflict arises between a CNAME record and another record of the same name but different type (regardless of which is existing or new), the existing record is retained.</span></span> <span data-ttu-id="ada1b-145">Ceci est indépendant de l’utilisation de `--force`.</span><span class="sxs-lookup"><span data-stu-id="ada1b-145">This is independent of the use of `--force`.</span></span>

### <a name="additional-information-about-importing"></a><span data-ttu-id="ada1b-146">Informations supplémentaires sur l’importation</span><span class="sxs-lookup"><span data-stu-id="ada1b-146">Additional information about importing</span></span>

<span data-ttu-id="ada1b-147">Les remarques suivantes fournissent des informations techniques supplémentaires concernant le processus d’importation de zones.</span><span class="sxs-lookup"><span data-stu-id="ada1b-147">The following notes provide additional technical details about the zone import process.</span></span>

* <span data-ttu-id="ada1b-148">La directive `$TTL` , facultative, est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="ada1b-148">The `$TTL` directive is optional, and it is supported.</span></span> <span data-ttu-id="ada1b-149">Quand aucune directive `$TTL` n’est spécifiée, les enregistrements sans durée de vie explicite sont importés avec une durée de vie de 3 600 secondes par défaut.</span><span class="sxs-lookup"><span data-stu-id="ada1b-149">When no `$TTL` directive is given, records without an explicit TTL are imported set to a default TTL of 3600 seconds.</span></span> <span data-ttu-id="ada1b-150">Lorsque deux enregistrements du même jeu d’enregistrements spécifient des TTL différentes, la moindre valeur est utilisée.</span><span class="sxs-lookup"><span data-stu-id="ada1b-150">When two records in the same record set specify different TTLs, the lower value is used.</span></span>
* <span data-ttu-id="ada1b-151">La directive `$ORIGIN` , facultative, est prise en charge.</span><span class="sxs-lookup"><span data-stu-id="ada1b-151">The `$ORIGIN` directive is optional, and it is supported.</span></span> <span data-ttu-id="ada1b-152">Quand aucune directive `$ORIGIN` n’est définie, la valeur utilisée par défaut est le nom de zone tel qu’il est spécifié sur la ligne de commande (avec le point final).</span><span class="sxs-lookup"><span data-stu-id="ada1b-152">When no `$ORIGIN` is set, the default value used is the zone name as specified on the command line (plus the terminating ".").</span></span>
* <span data-ttu-id="ada1b-153">Les directives `$INCLUDE` et `$GENERATE` ne sont pas prises en charge.</span><span class="sxs-lookup"><span data-stu-id="ada1b-153">The `$INCLUDE` and `$GENERATE` directives are not supported.</span></span>
* <span data-ttu-id="ada1b-154">Les types d’enregistrements A, AAAA, CNAME, MX, NS, SOA, SRV et TXT sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="ada1b-154">These record types are supported: A, AAAA, CNAME, MX, NS, SOA, SRV, and TXT.</span></span>
* <span data-ttu-id="ada1b-155">L’enregistrement SOA est créé automatiquement par Azure DNS lors de la création d’une zone.</span><span class="sxs-lookup"><span data-stu-id="ada1b-155">The SOA record is created automatically by Azure DNS when a zone is created.</span></span> <span data-ttu-id="ada1b-156">Quand vous importez un fichier de zone, tous les paramètres SOA sont pris dans le fichier de zone, *sauf* le paramètre `host`.</span><span class="sxs-lookup"><span data-stu-id="ada1b-156">When you import a zone file, all SOA parameters are taken from the zone file *except* the `host` parameter.</span></span> <span data-ttu-id="ada1b-157">Ce paramètre utilise la valeur fournie par Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-157">This parameter uses the value provided by Azure DNS.</span></span> <span data-ttu-id="ada1b-158">Ce paramètre doit en effet faire référence au serveur de noms principal fourni par Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-158">This is because this parameter must refer to the primary name server provided by Azure DNS.</span></span>
* <span data-ttu-id="ada1b-159">Le jeu d’enregistrements du serveur de noms, à l’extrémité de la zone, est créé automatiquement par Azure DNS au moment de la création de la zone.</span><span class="sxs-lookup"><span data-stu-id="ada1b-159">The name server record set at the zone apex is also created automatically by Azure DNS when the zone is created.</span></span> <span data-ttu-id="ada1b-160">Seule la durée de vie de ce jeu d’enregistrements est importée.</span><span class="sxs-lookup"><span data-stu-id="ada1b-160">Only the TTL of this record set is imported.</span></span> <span data-ttu-id="ada1b-161">Ces enregistrements contiennent les noms de serveurs de nom fournis par Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-161">These records contain the name server names provided by Azure DNS.</span></span> <span data-ttu-id="ada1b-162">Les données d’enregistrement ne sont pas remplacées par les valeurs contenues dans le fichier de zone importé.</span><span class="sxs-lookup"><span data-stu-id="ada1b-162">The record data is not overwritten by the values contained in the imported zone file.</span></span>
* <span data-ttu-id="ada1b-163">Pour la version préliminaire publique, Azure DNS prend uniquement en charge les enregistrements à chaîne unique.</span><span class="sxs-lookup"><span data-stu-id="ada1b-163">During Public Preview, Azure DNS supports only single-string TXT records.</span></span> <span data-ttu-id="ada1b-164">Les enregistrements TXT MultiString sont concaténés et tronqués à 255 caractères.</span><span class="sxs-lookup"><span data-stu-id="ada1b-164">Multistring TXT records are be concatenated and truncated to 255 characters.</span></span>

### <a name="cli-format-and-values"></a><span data-ttu-id="ada1b-165">Format et valeurs de l’interface CLI</span><span class="sxs-lookup"><span data-stu-id="ada1b-165">CLI format and values</span></span>

<span data-ttu-id="ada1b-166">Le format de la commande de l’interface CLI Azure pour importer une zone DNS est : </span><span class="sxs-lookup"><span data-stu-id="ada1b-166">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone import [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="ada1b-167">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="ada1b-167">Values:</span></span>

* <span data-ttu-id="ada1b-168">`<resource group>` est le nom du groupe de ressources correspondant à la zone dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-168">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="ada1b-169">`<zone name>` est le nom de la zone.</span><span class="sxs-lookup"><span data-stu-id="ada1b-169">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="ada1b-170">`<zone file name>` est le chemin/nom du fichier de zone à importer.</span><span class="sxs-lookup"><span data-stu-id="ada1b-170">`<zone file name>` is the path/name of the zone file to be imported.</span></span>

<span data-ttu-id="ada1b-171">S’il n’existe aucune zone de ce nom dans le groupe de ressources, cette zone est automatiquement créée.</span><span class="sxs-lookup"><span data-stu-id="ada1b-171">If a zone with this name does not exist in the resource group, it is created for you.</span></span> <span data-ttu-id="ada1b-172">Si la zone existe déjà, les jeux d’enregistrements importés sont fusionnés avec les jeux d’enregistrements existants.</span><span class="sxs-lookup"><span data-stu-id="ada1b-172">If the zone already exists, the imported record sets are merged with existing record sets.</span></span> <span data-ttu-id="ada1b-173">Pour remplacer les jeux d’enregistrements existants, utilisez l’option `--force` .</span><span class="sxs-lookup"><span data-stu-id="ada1b-173">To overwrite the existing record sets, use the `--force` option.</span></span>

<span data-ttu-id="ada1b-174">Pour vérifier le format d’un fichier de zone sans l’importer, utilisez l’option `--parse-only` .</span><span class="sxs-lookup"><span data-stu-id="ada1b-174">To verify the format of a zone file without actually importing it, use the `--parse-only` option.</span></span>

### <a name="step-1-import-a-zone-file"></a><span data-ttu-id="ada1b-175">Étape 1.</span><span class="sxs-lookup"><span data-stu-id="ada1b-175">Step 1.</span></span> <span data-ttu-id="ada1b-176">Importer un fichier de zone</span><span class="sxs-lookup"><span data-stu-id="ada1b-176">Import a zone file</span></span>

<span data-ttu-id="ada1b-177">Pour importer un fichier de zone pour la zone **contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="ada1b-177">To import a zone file for the zone **contoso.com**.</span></span>

1. <span data-ttu-id="ada1b-178">Connectez-vous à votre abonnement Azure à l’aide d’Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="ada1b-178">Sign in to your Azure subscription by using the Azure CLI 1.0.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="ada1b-179">Sélectionnez l’abonnement dans lequel vous souhaitez créer votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-179">Select the subscription where you want to create your new DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="ada1b-180">Azure DNS est un service Azure Resource Manager uniquement ; vous devez donc basculer la CLI Azure en mode Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ada1b-180">Azure DNS is an Azure Resource Manager-only service, so the Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="ada1b-181">Avant d’utiliser le service Azure DNS, vous devez inscrire votre abonnement pour utiliser le fournisseur de ressources Microsoft.Network.</span><span class="sxs-lookup"><span data-stu-id="ada1b-181">Before you use the Azure DNS service, you must register your subscription to use the Microsoft.Network resource provider.</span></span> <span data-ttu-id="ada1b-182">(Cette opération n’est à effectuer qu’une fois pour chaque abonnement.)</span><span class="sxs-lookup"><span data-stu-id="ada1b-182">(This is a one-time operation for each subscription.)</span></span>

    ```azurecli
    azure provider register Microsoft.Network
    ```

5. <span data-ttu-id="ada1b-183">Si ce n’est déjà fait, vous devez également créer un groupe de ressources Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ada1b-183">If you don't have one already, you also need to create a Resource Manager resource group.</span></span>

    ```azurecli
    azure group create myresourcegroup westeurope
    ```

6. <span data-ttu-id="ada1b-184">Pour importer la zone **contoso.com** à partir du fichier **contoso.com.txt** dans une nouvelle zone DNS du groupe de ressources **myresourcegroup**, exécutez la commande `azure network dns zone import`.</span><span class="sxs-lookup"><span data-stu-id="ada1b-184">To import the zone **contoso.com** from the file **contoso.com.txt** into a new DNS zone in the resource group **myresourcegroup**, run the command `azure network dns zone import`.</span></span><BR><span data-ttu-id="ada1b-185">Cette commande charge le fichier de zone et l’analyse.</span><span class="sxs-lookup"><span data-stu-id="ada1b-185">This command loads the zone file and parse it.</span></span> <span data-ttu-id="ada1b-186">Cette commande exécute une série de commandes sur le service Azure DNS, afin de créer la zone et tous les jeux d’enregistrements associés.</span><span class="sxs-lookup"><span data-stu-id="ada1b-186">The command executes a series of commands on the Azure DNS service to create the zone and all the record sets in the zone.</span></span> <span data-ttu-id="ada1b-187">Elle rend compte de la progression dans la fenêtre de console et signale les éventuels avertissements ou erreurs.</span><span class="sxs-lookup"><span data-stu-id="ada1b-187">The command reports progress in the console window, along with any errors or warnings.</span></span> <span data-ttu-id="ada1b-188">Étant donné que les jeux d’enregistrements sont créés en série, l’importation d’un fichier de zone volumineux peut prendre quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="ada1b-188">Because record sets are created in series, it may take a few minutes to import a large zone file.</span></span>

    ```azurecli
    azure network dns zone import myresourcegroup contoso.com contoso.com.txt
    ```

### <a name="step-2-verify-the-zone"></a><span data-ttu-id="ada1b-189">Étape 2.</span><span class="sxs-lookup"><span data-stu-id="ada1b-189">Step 2.</span></span> <span data-ttu-id="ada1b-190">Vérifier la zone</span><span class="sxs-lookup"><span data-stu-id="ada1b-190">Verify the zone</span></span>

<span data-ttu-id="ada1b-191">Pour vérifier la zone DNS après avoir importé le fichier, vous pouvez utiliser une des méthodes suivantes :</span><span class="sxs-lookup"><span data-stu-id="ada1b-191">To verify the DNS zone after you import the file, you can use any one of the following methods:</span></span>

* <span data-ttu-id="ada1b-192">Vous pouvez répertorier les enregistrements à l’aide de la commande Azure CLI suivante :</span><span class="sxs-lookup"><span data-stu-id="ada1b-192">You can list the records by using the following Azure CLI command:</span></span>

    ```azurecli
    azure network dns record-set list myresourcegroup contoso.com
    ```

* <span data-ttu-id="ada1b-193">Vous pouvez répertorier les enregistrements à l’aide de l’applet de commande PowerShell `Get-AzureRmDnsRecordSet`.</span><span class="sxs-lookup"><span data-stu-id="ada1b-193">You can list the records by using the PowerShell cmdlet `Get-AzureRmDnsRecordSet`.</span></span>
* <span data-ttu-id="ada1b-194">Vous pouvez également utiliser `nslookup` pour vérifier la résolution des noms pour les enregistrements.</span><span class="sxs-lookup"><span data-stu-id="ada1b-194">You can use `nslookup` to verify name resolution for the records.</span></span> <span data-ttu-id="ada1b-195">Puisque la zone n’est pas encore déléguée, vous devez spécifier explicitement les serveurs de noms DNS Azure appropriés.</span><span class="sxs-lookup"><span data-stu-id="ada1b-195">Because the zone isn't delegated yet, you need to specify the correct Azure DNS name servers explicitly.</span></span> <span data-ttu-id="ada1b-196">L’exemple suivant montre comment récupérer les noms du serveur de noms assignés à la zone.</span><span class="sxs-lookup"><span data-stu-id="ada1b-196">The following sample shows how to retrieve the name server names assigned to the zone.</span></span> <span data-ttu-id="ada1b-197">Il montre également comment interroger l’enregistrement « www » à l’aide de `nslookup`.</span><span class="sxs-lookup"><span data-stu-id="ada1b-197">IT also shows how to query the "www" record by using `nslookup`.</span></span>

        C:\>azure network dns record-set show myresourcegroup contoso.com @ NS
        info:Executing command network dns record-set show
        + Looking up the DNS Record Set "@" of type "NS"
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

### <a name="step-3-update-dns-delegation"></a><span data-ttu-id="ada1b-198">Étape 3.</span><span class="sxs-lookup"><span data-stu-id="ada1b-198">Step 3.</span></span> <span data-ttu-id="ada1b-199">Mettre à jour la délégation DNS</span><span class="sxs-lookup"><span data-stu-id="ada1b-199">Update DNS delegation</span></span>

<span data-ttu-id="ada1b-200">Après avoir vérifié que la zone a été importée correctement, vous devez mettre à jour la délégation DNS afin qu’elle pointe vers les serveurs de noms Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-200">After you have verified that the zone has been imported correctly, you need to update the DNS delegation to point to the Azure DNS name servers.</span></span> <span data-ttu-id="ada1b-201">Pour plus d’informations, consultez l’article [Mettre à jour la délégation DNS](dns-domain-delegation.md).</span><span class="sxs-lookup"><span data-stu-id="ada1b-201">For more information, see the article [Update the DNS delegation](dns-domain-delegation.md).</span></span>

## <a name="export-a-dns-zone-file-from-azure-dns"></a><span data-ttu-id="ada1b-202">Exportation d’un fichier de zone DNS à partir d’Azure DNS</span><span class="sxs-lookup"><span data-stu-id="ada1b-202">Export a DNS zone file from Azure DNS</span></span>

<span data-ttu-id="ada1b-203">Le format de la commande de l’interface CLI Azure pour importer une zone DNS est : </span><span class="sxs-lookup"><span data-stu-id="ada1b-203">The format of the Azure CLI command to import a DNS zone is:</span></span>

```azurecli
azure network dns zone export [options] <resource group> <zone name> <zone file name>
```

<span data-ttu-id="ada1b-204">Valeurs :</span><span class="sxs-lookup"><span data-stu-id="ada1b-204">Values:</span></span>

* <span data-ttu-id="ada1b-205">`<resource group>` est le nom du groupe de ressources correspondant à la zone dans Azure DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-205">`<resource group>` is the name of the resource group for the zone in Azure DNS.</span></span>
* <span data-ttu-id="ada1b-206">`<zone name>` est le nom de la zone.</span><span class="sxs-lookup"><span data-stu-id="ada1b-206">`<zone name>` is the name of the zone.</span></span>
* <span data-ttu-id="ada1b-207">`<zone file name>` est le chemin d’accès/nom du fichier de zone à exporter.</span><span class="sxs-lookup"><span data-stu-id="ada1b-207">`<zone file name>` is the path/name of the zone file to be exported.</span></span>

<span data-ttu-id="ada1b-208">Pour importer une zone, vous devez d’abord vous connecter, sélectionner votre abonnement, puis configurer l’interface de ligne de commande Azure pour utiliser le mode Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ada1b-208">As with the zone import, you first need to sign in, choose your subscription, and configure the Azure CLI to use Resource Manager mode.</span></span>

### <a name="to-export-a-zone-file"></a><span data-ttu-id="ada1b-209">Pour exporter un fichier de zone</span><span class="sxs-lookup"><span data-stu-id="ada1b-209">To export a zone file</span></span>

1. <span data-ttu-id="ada1b-210">Connectez-vous à votre abonnement Azure à l’aide de la CLI Azure.</span><span class="sxs-lookup"><span data-stu-id="ada1b-210">Sign in to your Azure subscription by using the Azure CLI.</span></span>

    ```azurecli
    azure login
    ```

2. <span data-ttu-id="ada1b-211">Sélectionnez l’abonnement dans lequel vous souhaitez créer votre zone DNS.</span><span class="sxs-lookup"><span data-stu-id="ada1b-211">Select the subscription where you want to create your DNS zone.</span></span>

    ```azurecli
    azure account set <subscription name>
    ```

3. <span data-ttu-id="ada1b-212">Azure DNS est un service Azure Resource Manager uniquement.</span><span class="sxs-lookup"><span data-stu-id="ada1b-212">Azure DNS is an Azure Resource Manager-only service.</span></span> <span data-ttu-id="ada1b-213">La CLI Azure doit être basculée en mode Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ada1b-213">The Azure CLI must be switched to Resource Manager mode.</span></span>

    ```azurecli
    azure config mode arm
    ```

4. <span data-ttu-id="ada1b-214">Pour exporter la zone Azure DNS existante **contoso.com** du groupe de ressources **myresourcegroup** vers le fichier **contoso.com.txt** (dans le dossier actuel), exécutez `azure network dns zone export`.</span><span class="sxs-lookup"><span data-stu-id="ada1b-214">To export the existing Azure DNS zone **contoso.com** in resource group **myresourcegroup** to the file **contoso.com.txt** (in the current folder), run `azure network dns zone export`.</span></span> <span data-ttu-id="ada1b-215">Cette commande appelle le service Azure DNS pour énumérer les jeux d’enregistrements dans la zone et exporter les résultats dans un fichier de zone compatible BIND.</span><span class="sxs-lookup"><span data-stu-id="ada1b-215">This command  calls the Azure DNS service to enumerate record sets in the zone and export the results to a BIND-compatible zone file.</span></span>

    ```azurecli
    azure network dns zone export myresourcegroup contoso.com contoso.com.txt
    ```
