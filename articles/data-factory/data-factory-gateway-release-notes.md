---
title: "notes d’aaaRelease pour la passerelle de gestion des données | Documents Microsoft"
description: "Notes de version pour la passerelle de gestion des données"
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: 14762e82-76d9-41c4-ba9f-14a54da29c36
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 3165d7537410a0531e0bb7f7fe584767f9155574
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="d52c0-103">Notes de version pour la passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="d52c0-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="d52c0-104">Un des défis hello pour l’intégration de données moderne est tooand de données toomove de local toocloud.</span><span class="sxs-lookup"><span data-stu-id="d52c0-104">One of hello challenges for modern data integration is toomove data tooand from on-premises toocloud.</span></span> <span data-ttu-id="d52c0-105">Fabrique de données permet l’intégration avec la passerelle de gestion des données, qui est un agent que vous pouvez installer le déplacement des données sur site tooenable hybride.</span><span class="sxs-lookup"><span data-stu-id="d52c0-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises tooenable hybrid data movement.</span></span>

<span data-ttu-id="d52c0-106">Consultez hello suivant des articles pour plus d’informations sur la passerelle de gestion des données et comment toouse il :</span><span class="sxs-lookup"><span data-stu-id="d52c0-106">See hello following articles for detailed information about Data Management Gateway and how toouse it:</span></span>

*  [<span data-ttu-id="d52c0-107">Passerelle de gestion de données</span><span class="sxs-lookup"><span data-stu-id="d52c0-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="d52c0-108">Déplacement de données entre des emplacements locaux et le cloud à l'aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="d52c0-109">VERSION ACTUELLE (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="d52c0-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d52c0-110">Améliorations</span><span class="sxs-lookup"><span data-stu-id="d52c0-110">Enhancements-</span></span>
- <span data-ttu-id="d52c0-111">Vous pouvez ajouter le bus des services DNS entrées toowhitelist plutôt que de création de listes autorisées toutes les adresses IP Azure à partir de votre pare-feu (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="d52c0-111">You can add DNS entries toowhitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="d52c0-112">Vous pouvez trouver l’entrée DNS concernée sur le portail Azure (Data Factory -> Créer et déployer > Passerelles > ServiceUrls (dans JSON))</span><span class="sxs-lookup"><span data-stu-id="d52c0-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="d52c0-113">Le connecteur HDFS prend désormais en charge le certificat public auto-signé en vous permettant d’ignorer la validation SSL.</span><span class="sxs-lookup"><span data-stu-id="d52c0-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="d52c0-114">Résolu : Problème avec la passerelle en mode hors connexion pendant la mise à jour (en raison d’inclinaison de tooclock)</span><span class="sxs-lookup"><span data-stu-id="d52c0-114">Fixed: Issue with gateway offline during update (due tooclock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="d52c0-115">Versions antérieures</span><span class="sxs-lookup"><span data-stu-id="d52c0-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="d52c0-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="d52c0-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d52c0-117">Améliorations</span><span class="sxs-lookup"><span data-stu-id="d52c0-117">Enhancements-</span></span>
-   <span data-ttu-id="d52c0-118">Vous pouvez ajouter toowhitelist des entrées DNS Service Bus au lieu des liste approuvées toutes les adresses IP Azure à partir de votre pare-feu (le cas échéant).</span><span class="sxs-lookup"><span data-stu-id="d52c0-118">You can add DNS entries toowhitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="d52c0-119">Plus de détails ici.</span><span class="sxs-lookup"><span data-stu-id="d52c0-119">More details here.</span></span>
-   <span data-ttu-id="d52c0-120">Vous pouvez maintenant copier les données vers/à partir d’un objet blob de bloc unique des too4.75 To, ce qui est la taille de hello maximale prise en charge de l’objet blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="d52c0-120">You can now copy data to/from a single block blob up too4.75 TB, which is hello max supported size of block blob.</span></span> <span data-ttu-id="d52c0-121">(la limite antérieure était de 195 Go).</span><span class="sxs-lookup"><span data-stu-id="d52c0-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="d52c0-122">Résolu : problème de mémoire insuffisante lors de la décompression de plusieurs petits fichiers pendant l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d52c0-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="d52c0-123">Problème résolu : Index hors problème plage lors de la copie à partir de la base de données de Document tooan local SQL Server avec la fonctionnalité d’idempotence.</span><span class="sxs-lookup"><span data-stu-id="d52c0-123">Fixed: Index out of range issue while copying from Document DB tooan on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="d52c0-124">Résolu : le script de nettoyage SQL ne fonctionne pas avec la version locale de SQL Server à partir de l’Assistant de copie.</span><span class="sxs-lookup"><span data-stu-id="d52c0-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="d52c0-125">Problème résolu : Nom de la colonne avec l’espace à la fin de hello ne fonctionne pas dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="d52c0-125">Fixed: Column name with space at hello end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="d52c0-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="d52c0-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d52c0-127">Améliorations</span><span class="sxs-lookup"><span data-stu-id="d52c0-127">Enhancements-</span></span>
- <span data-ttu-id="d52c0-128">Résolu : problème d’informations d’identification manquantes au redémarrage de l’ordinateur de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d52c0-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="d52c0-129">Résolu : problème lié à l’inscription lors de la restauration de la passerelle à l’aide d’un fichier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="d52c0-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="d52c0-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="d52c0-131">Améliorations</span><span class="sxs-lookup"><span data-stu-id="d52c0-131">Enhancements-</span></span>
- <span data-ttu-id="d52c0-132">Résolu : lecture incorrecte d’une valeur null décimale à partir d’Oracle comme source.</span><span class="sxs-lookup"><span data-stu-id="d52c0-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="d52c0-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="d52c0-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="d52c0-134">Nouveautés</span><span class="sxs-lookup"><span data-stu-id="d52c0-134">What’s new</span></span>
- <span data-ttu-id="d52c0-135">Les clients peuvent faire part de leurs commentaires sur l’expérience d’inscription à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d52c0-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="d52c0-136">Prise en charge d’un nouveau format de compression : ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="d52c0-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d52c0-137">Améliorations</span><span class="sxs-lookup"><span data-stu-id="d52c0-137">Enhancements-</span></span>
- <span data-ttu-id="d52c0-138">Amélioration des performances pour le récepteur d’Oracle, source HDFS.</span><span class="sxs-lookup"><span data-stu-id="d52c0-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="d52c0-139">Correctif de bogue pour la mise à jour automatique de la passerelle, capacité de traitement parallèle de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d52c0-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="d52c0-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="d52c0-141">Améliorations</span><span class="sxs-lookup"><span data-stu-id="d52c0-141">Enhancements</span></span>
- <span data-ttu-id="d52c0-142">Améliorée et plus robuste passerelle inscription expérience-maintenant vous pouvez suivre l’état de la progression pendant le processus de l’inscription hello passerelle, ce qui rend l’inscription de hello expérience plus réactive.</span><span class="sxs-lookup"><span data-stu-id="d52c0-142">Improved and more robust Gateway registration experience- Now you can track progress status during hello Gateway registration process, which makes hello registration experience more responsive.</span></span>
- <span data-ttu-id="d52c0-143">Amélioration de la passerelle restaurer processus - vous pouvez toujours récupérer passerelle même si vous n’avez pas de fichier de sauvegarde de passerelle hello avec cette mise à jour.</span><span class="sxs-lookup"><span data-stu-id="d52c0-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have hello gateway backup file with this update.</span></span> <span data-ttu-id="d52c0-144">Cette situation exigerait informations d’identification du Service lié tooreset dans le portail.</span><span class="sxs-lookup"><span data-stu-id="d52c0-144">This would require you tooreset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="d52c0-145">Résolution de bogue.</span><span class="sxs-lookup"><span data-stu-id="d52c0-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="d52c0-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="d52c0-147">Nouveautés</span><span class="sxs-lookup"><span data-stu-id="d52c0-147">What’s new</span></span>

- <span data-ttu-id="d52c0-148">Vous pouvez désormais stocker localement les informations d’identification de la source de données.</span><span class="sxs-lookup"><span data-stu-id="d52c0-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="d52c0-149">informations d’identification de Hello sont chiffrées.</span><span class="sxs-lookup"><span data-stu-id="d52c0-149">hello credentials are encrypted.</span></span> <span data-ttu-id="d52c0-150">informations d’identification de source de données Hello peuvent être récupérées et restaurées à l’aide du fichier de sauvegarde hello qui peut être exportée à partir de hello existant de passerelle, locaux.</span><span class="sxs-lookup"><span data-stu-id="d52c0-150">hello data source credentials can be recovered and restored using hello backup file that can be exported from hello existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="d52c0-151">Améliorations</span><span class="sxs-lookup"><span data-stu-id="d52c0-151">Enhancements-</span></span>

- <span data-ttu-id="d52c0-152">Expérience d’inscription de la passerelle améliorée et plus robuste.</span><span class="sxs-lookup"><span data-stu-id="d52c0-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="d52c0-153">Prend en charge la détection automatique de la configuration de l’élément QuoteChar pour le format de texte dans l’Assistant copie d’et améliorer hello format global de précision de la détection.</span><span class="sxs-lookup"><span data-stu-id="d52c0-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve hello overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="d52c0-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="d52c0-154">2.3.6100.2</span></span>

- <span data-ttu-id="d52c0-155">Prise en charge de la détection automatique firstRowAsHeader et SkipLineCount dans l’Assistant de copie pour les fichiers texte dans le système de fichiers local et HDFS.</span><span class="sxs-lookup"><span data-stu-id="d52c0-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="d52c0-156">Améliorer la stabilité hello de connexion réseau entre la passerelle et le Service Bus</span><span class="sxs-lookup"><span data-stu-id="d52c0-156">Enhance hello stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="d52c0-157">Résolution de quelques bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="d52c0-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-158">2.2.6072.1</span></span>

*  <span data-ttu-id="d52c0-159">Prend en charge la définition du proxy HTTP pour l’utilisation de passerelle hello hello Gestionnaire de Configuration de passerelle.</span><span class="sxs-lookup"><span data-stu-id="d52c0-159">Supports setting HTTP proxy for hello gateway using hello Gateway Configuration Manager.</span></span> <span data-ttu-id="d52c0-160">Si configurés, Azure Blob, Azure Table, Azure Data Lake et Document DB sont accessibles via le proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="d52c0-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="d52c0-161">En-tête prend en charge la gestion de TextFormat lors de la copie des données à partir de / tooAzure Blob, Azure Data Lake Store, système de fichiers local et HDFS local.</span><span class="sxs-lookup"><span data-stu-id="d52c0-161">Supports header handling for TextFormat when copying data from/tooAzure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="d52c0-162">Prend en charge la copie de données d’ajouter un objet Blob et l’objet Blob de pages, ainsi que de hello déjà pris en charge l’objet Blob de blocs.</span><span class="sxs-lookup"><span data-stu-id="d52c0-162">Supports copying data from Append Blob and Page Blob along with hello already supported Block Blob.</span></span>
*  <span data-ttu-id="d52c0-163">Introduit un nouvel état de la passerelle **en ligne (limité)**, ce qui signifie que hello principale fonctionnalité de passerelle de hello fonctionne à l’exception de prise en charge de hello opération interactive de l’Assistant copie de.</span><span class="sxs-lookup"><span data-stu-id="d52c0-163">Introduces a new gateway status **Online (Limited)**, which indicates that hello main functionality of hello gateway works except hello interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="d52c0-164">Améliore la robustesse de hello d’enregistrement de la passerelle à l’aide de la clé d’inscription.</span><span class="sxs-lookup"><span data-stu-id="d52c0-164">Enhances hello robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="d52c0-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="d52c0-165">2.1.6040.</span></span>

*  <span data-ttu-id="d52c0-166">Pilote DB2 est inclus dans le package d’installation hello passerelle maintenant.</span><span class="sxs-lookup"><span data-stu-id="d52c0-166">DB2 driver is included in hello gateway installation package now.</span></span> <span data-ttu-id="d52c0-167">Vous n’avez pas besoin de tooinstall il séparément.</span><span class="sxs-lookup"><span data-stu-id="d52c0-167">You do not need tooinstall it separately.</span></span>
*  <span data-ttu-id="d52c0-168">Pilote DB2 prend désormais en charge z/OS et DB2 pour i (AS / 400), ainsi que les plateformes hello déjà pris en charge (Windows, Unix et Linux).</span><span class="sxs-lookup"><span data-stu-id="d52c0-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with hello platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="d52c0-169">Prend en charge l’utilisation d’Azure Cosmos DB comme source ou destination des banques de données locales</span><span class="sxs-lookup"><span data-stu-id="d52c0-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="d52c0-170">Prend en charge la copie de stockage des données à partir de/toocold/attentivement les objets blob, ainsi que de hello déjà pris en charge le compte de stockage à usage général.</span><span class="sxs-lookup"><span data-stu-id="d52c0-170">Supports copying data from/toocold/hot blob storage along with hello already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="d52c0-171">Vous permet de tooconnect tooon local SQL Server via une passerelle avec des droits de connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="d52c0-171">Allows you tooconnect tooon-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="d52c0-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-172">2.0.6013.1</span></span>

*  <span data-ttu-id="d52c0-173">Vous pouvez sélectionner hello toobe de langue/culture utilisée par une passerelle de pendant l’installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="d52c0-173">You can select hello language/culture toobe used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="d52c0-174">Lors de la passerelle ne fonctionne pas comme prévu, vous pouvez choisir les journaux de la passerelle toosend dernière sept jours tooMicrosoft toofacilitate résolution des problèmes d’émission de hello.</span><span class="sxs-lookup"><span data-stu-id="d52c0-174">When gateway does not work as expected, you can choose toosend gateway logs of last seven days tooMicrosoft toofacilitate troubleshooting of hello issue.</span></span> <span data-ttu-id="d52c0-175">Si la passerelle n’est pas connecté toohello service de cloud, vous pouvez choisir toosave et archivez les journaux de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d52c0-175">If gateway is not connected toohello cloud service, you can choose toosave and archive gateway logs.</span></span>  

*  <span data-ttu-id="d52c0-176">Améliorations de l’interface utilisateur du gestionnaire de configuration de la passerelle :</span><span class="sxs-lookup"><span data-stu-id="d52c0-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="d52c0-177">Afficher l’état de la passerelle plus hello accueil onglet.</span><span class="sxs-lookup"><span data-stu-id="d52c0-177">Make gateway status more visible on hello Home tab.</span></span>

    *  <span data-ttu-id="d52c0-178">Commandes réorganisées et simplifiées.</span><span class="sxs-lookup"><span data-stu-id="d52c0-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="d52c0-179">Vous pouvez copier des données à partir d’un stockage à l’aide de hello [outil Aperçu de la copie sans code](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="d52c0-179">You can copy data from a storage using hello [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="d52c0-180">Pour plus d’informations sur cette fonctionnalité, consultez [Copie intermédiaire](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="d52c0-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="d52c0-181">Vous pouvez utiliser les données de tooingress de passerelle de gestion des données directement à partir d’une base de données SQL Server locale dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="d52c0-181">You can use Data Management Gateway tooingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="d52c0-182">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-182">Performance improvements</span></span>

    * <span data-ttu-id="d52c0-183">Amélioration des performances d’affichage du schéma/de l’aperçu par rapport à SQL Server dans l’outil de prévisualisation de copie sans code.</span><span class="sxs-lookup"><span data-stu-id="d52c0-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="d52c0-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-184">1.12.5953.1</span></span>

*  <span data-ttu-id="d52c0-185">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="d52c0-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-186">1.11.5918.1</span></span>

*  <span data-ttu-id="d52c0-187">Taille maximale du journal des événements hello passerelle a été augmentée à partir de 1 Mo too40 Mo.</span><span class="sxs-lookup"><span data-stu-id="d52c0-187">Maximum size of hello gateway event log has been increased from 1 MB too40 MB.</span></span>

*  <span data-ttu-id="d52c0-188">Une boîte de dialogue d’avertissement s’affiche si un redémarrage est nécessaire pendant la mise à jour automatique de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="d52c0-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="d52c0-189">Vous pouvez choisir toorestart droite puis ou version ultérieure.</span><span class="sxs-lookup"><span data-stu-id="d52c0-189">You can choose toorestart right then or later.</span></span>

*  <span data-ttu-id="d52c0-190">En cas d’échec de la mise à jour automatique, le programme d’installation de la passerelle retente la mise à jour automatique trois fois au maximum.</span><span class="sxs-lookup"><span data-stu-id="d52c0-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="d52c0-191">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-191">Performance improvements</span></span>

    * <span data-ttu-id="d52c0-192">Améliorez les performances lors du chargement de tables de grande taille à partir du serveur local dans le scénario de copie sans code.</span><span class="sxs-lookup"><span data-stu-id="d52c0-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="d52c0-193">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="d52c0-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-194">1.10.5892.1</span></span>

*  <span data-ttu-id="d52c0-195">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-195">Performance improvements</span></span>

*  <span data-ttu-id="d52c0-196">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="d52c0-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="d52c0-197">1.9.5865.2</span></span>

*  <span data-ttu-id="d52c0-198">Capacité de mise à jour automatique Zero Touch</span><span class="sxs-lookup"><span data-stu-id="d52c0-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="d52c0-199">Nouvelle icône de barre d’état système avec des indicateurs d’état de la passerelle</span><span class="sxs-lookup"><span data-stu-id="d52c0-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="d52c0-200">Possibilité de trop « mettre à jour maintenant » à partir du client de hello</span><span class="sxs-lookup"><span data-stu-id="d52c0-200">Ability too“Update now” from hello client</span></span>
*  <span data-ttu-id="d52c0-201">Heure de planification de capacité tooset mise à jour</span><span class="sxs-lookup"><span data-stu-id="d52c0-201">Ability tooset update schedule time</span></span>
*  <span data-ttu-id="d52c0-202">Script PowerShell disponible pour activer/désactiver la mise à jour automatique</span><span class="sxs-lookup"><span data-stu-id="d52c0-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="d52c0-203">Prise en charge du format JSON</span><span class="sxs-lookup"><span data-stu-id="d52c0-203">Support for JSON format</span></span>  
*  <span data-ttu-id="d52c0-204">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-204">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-205">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="d52c0-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-206">1.8.5822.1</span></span>

*  <span data-ttu-id="d52c0-207">Amélioration de l’expérience de résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="d52c0-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="d52c0-208">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-208">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-209">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="d52c0-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-210">1.7.5795.1</span></span>

*  <span data-ttu-id="d52c0-211">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-211">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-212">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="d52c0-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-213">1.7.5764.1</span></span>

*  <span data-ttu-id="d52c0-214">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-214">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-215">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="d52c0-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-216">1.6.5735.1</span></span>

*  <span data-ttu-id="d52c0-217">Prise en charge de la source/du récepteur HDFS en local</span><span class="sxs-lookup"><span data-stu-id="d52c0-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="d52c0-218">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-218">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-219">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="d52c0-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-220">1.6.5696.1</span></span>

*  <span data-ttu-id="d52c0-221">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-221">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-222">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="d52c0-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-223">1.6.5676.1</span></span>

*  <span data-ttu-id="d52c0-224">Prise en charge des outils de diagnostic dans le Gestionnaire de configuration</span><span class="sxs-lookup"><span data-stu-id="d52c0-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="d52c0-225">Prise en charge des colonnes de table pour les sources de données tabulaires pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-226">Prise en charge de SQL DW pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-227">Prise en charge de Reclusive dans BlobSource et FileSource pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-228">Prise en charge de CopyBehavior (MergeFiles, PreserveHierarchy et FlattenHierarchy) dans BlobSink et FileSink avec copie binaire pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-229">Prise en charge du signalement de progression de l’activité de copie pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-230">Prise en charge de la validation de connectivité des sources de données pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-231">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="d52c0-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-232">1.6.5672.1</span></span>

*  <span data-ttu-id="d52c0-233">Prise en charge des noms de tables pour la source de données ODBC pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-234">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-234">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-235">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="d52c0-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-236">1.6.5658.1</span></span>

*  <span data-ttu-id="d52c0-237">Prise en charge du récepteur de fichier pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-238">Prise en charge de la conservation de la hiérarchie dans une copie binaire pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-239">Prise en charge de l’idempotence de l’activité de copie pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-240">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="d52c0-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-241">1.6.5640.1</span></span>

*  <span data-ttu-id="d52c0-242">Prise en charge de 3 sources de données supplémentaires pour Microsoft Azure Data Factory (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="d52c0-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="d52c0-243">Prise en charge du caractère guillemet dans l’analyseur CSV pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-244">Prise en charge de la compression (BZip2)</span><span class="sxs-lookup"><span data-stu-id="d52c0-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="d52c0-245">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="d52c0-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-246">1.5.5612.1</span></span>

*  <span data-ttu-id="d52c0-247">Prise en charge de cinq bases de données relationnelles pour Microsoft Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata et Sybase)</span><span class="sxs-lookup"><span data-stu-id="d52c0-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="d52c0-248">Prise en charge de la compression (Gzip et Deflate)</span><span class="sxs-lookup"><span data-stu-id="d52c0-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="d52c0-249">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-249">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-250">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="d52c0-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-251">1.4.5549.1</span></span>

*  <span data-ttu-id="d52c0-252">Ajout de la prise en charge de source de données Oracle pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="d52c0-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="d52c0-253">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="d52c0-253">Performance improvements</span></span>
*  <span data-ttu-id="d52c0-254">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="d52c0-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="d52c0-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-255">1.4.5492.1</span></span>

*  <span data-ttu-id="d52c0-256">Binaire unifié qui prend en charge à la fois des services Microsoft Azure Data Factory et Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="d52c0-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="d52c0-257">Affiner le processus d’inscription et de l’interface utilisateur de Configuration de hello</span><span class="sxs-lookup"><span data-stu-id="d52c0-257">Refine hello Configuration UI and registration process</span></span>
*  <span data-ttu-id="d52c0-258">Microsoft Azure Data Factory : prise en charge des entrées et sorties Azure pour la source de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="d52c0-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="d52c0-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="d52c0-259">1.2.5303.1</span></span>

*  <span data-ttu-id="d52c0-260">Corrigez toosupport de problème de délai d’attente plus long connexions source de données.</span><span class="sxs-lookup"><span data-stu-id="d52c0-260">Fix timeout issue toosupport more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="d52c0-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="d52c0-261">1.1.5526.8</span></span>

*  <span data-ttu-id="d52c0-262">.NET Framework 4.5.1 est requis pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="d52c0-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="d52c0-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="d52c0-263">1.0.5144.2</span></span>

*  <span data-ttu-id="d52c0-264">Aucune modification affectant les scénarios Microsoft Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="d52c0-264">No changes that affect Azure Data Factory scenarios.</span></span>
