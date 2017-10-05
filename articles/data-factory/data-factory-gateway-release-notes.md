---
title: "Notes de version pour la passerelle de gestion des données | Microsoft Docs"
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
ms.openlocfilehash: c052d7e9f757164429ce867201b96305e405dce9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="release-notes-for-data-management-gateway"></a><span data-ttu-id="af299-103">Notes de version pour la passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="af299-103">Release notes for Data Management Gateway</span></span>
<span data-ttu-id="af299-104">Un des défis de l’intégration de données modernes consiste à déplacer des données vers et depuis un site local et le cloud.</span><span class="sxs-lookup"><span data-stu-id="af299-104">One of the challenges for modern data integration is to move data to and from on-premises to cloud.</span></span> <span data-ttu-id="af299-105">Azure Data Factory effectue cette intégration avec la passerelle de gestion des données Microsoft, qui est un agent pouvant être installé en local pour activer le déplacement de données hybrides.</span><span class="sxs-lookup"><span data-stu-id="af299-105">Data Factory makes this integration with Data Management Gateway, which is an agent that you can install on-premises to enable hybrid data movement.</span></span>

<span data-ttu-id="af299-106">Consultez les articles suivants pour des informations détaillées sur la passerelle de gestion des données et son utilisation :</span><span class="sxs-lookup"><span data-stu-id="af299-106">See the following articles for detailed information about Data Management Gateway and how to use it:</span></span>

*  [<span data-ttu-id="af299-107">Passerelle de gestion de données</span><span class="sxs-lookup"><span data-stu-id="af299-107">Data Management Gateway</span></span>](data-factory-data-management-gateway.md)
*  [<span data-ttu-id="af299-108">Déplacement de données entre des emplacements locaux et le cloud à l'aide d’Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-108">Move data between on-premises and cloud using Azure Data Factory</span></span>](data-factory-move-data-between-onprem-and-cloud.md)


## <a name="current-version-21063477"></a><span data-ttu-id="af299-109">VERSION ACTUELLE (2.10.6347.7)</span><span class="sxs-lookup"><span data-stu-id="af299-109">CURRENT VERSION (2.10.6347.7)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="af299-110">Améliorations</span><span class="sxs-lookup"><span data-stu-id="af299-110">Enhancements-</span></span>
- <span data-ttu-id="af299-111">Vous pouvez ajouter des entrées DNS à la liste blanche Service Bus au lieu d’autoriser toutes les adresses IP Azure dans votre pare-feu (si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="af299-111">You can add DNS entries to whitelist service bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="af299-112">Vous pouvez trouver l’entrée DNS concernée sur le portail Azure (Data Factory -> Créer et déployer > Passerelles > ServiceUrls (dans JSON))</span><span class="sxs-lookup"><span data-stu-id="af299-112">You can find respective DNS entry on Azure portal (Data Factory -> ‘Author and Deploy’ -> ‘Gateways’ -> "serviceUrls" (in JSON)</span></span>
- <span data-ttu-id="af299-113">Le connecteur HDFS prend désormais en charge le certificat public auto-signé en vous permettant d’ignorer la validation SSL.</span><span class="sxs-lookup"><span data-stu-id="af299-113">HDFS connector now supports self-signed public certificate by letting you skip SSL validation.</span></span>
- <span data-ttu-id="af299-114">Résolu : problème lié à la passerelle en mode hors connexion pendant la mise à jour (en raison d’une différence d’heure)</span><span class="sxs-lookup"><span data-stu-id="af299-114">Fixed: Issue with gateway offline during update (due to clock skew)</span></span>



## <a name="earlier-versions"></a><span data-ttu-id="af299-115">Versions antérieures</span><span class="sxs-lookup"><span data-stu-id="af299-115">Earlier versions</span></span>

## <a name="2963132"></a><span data-ttu-id="af299-116">2.9.6313.2</span><span class="sxs-lookup"><span data-stu-id="af299-116">2.9.6313.2</span></span>
### <a name="enhancements-"></a><span data-ttu-id="af299-117">Améliorations</span><span class="sxs-lookup"><span data-stu-id="af299-117">Enhancements-</span></span>
-   <span data-ttu-id="af299-118">Vous pouvez ajouter des entrées DNS à la liste blanche Service Bus au lieu d’autoriser toutes les adresses IP Azure dans votre pare-feu (si nécessaire).</span><span class="sxs-lookup"><span data-stu-id="af299-118">You can add DNS entries to whitelist Service Bus rather than whitelisting all Azure IP addresses from your firewall (if needed).</span></span> <span data-ttu-id="af299-119">Plus de détails ici.</span><span class="sxs-lookup"><span data-stu-id="af299-119">More details here.</span></span>
-   <span data-ttu-id="af299-120">Vous pouvez maintenant copier les données vers ou à partir d’un seul objet blob de blocs jusqu’à 4,75 To. Il s’agit de la taille maximale prise en charge pour ces objets</span><span class="sxs-lookup"><span data-stu-id="af299-120">You can now copy data to/from a single block blob up to 4.75 TB, which is the max supported size of block blob.</span></span> <span data-ttu-id="af299-121">(la limite antérieure était de 195 Go).</span><span class="sxs-lookup"><span data-stu-id="af299-121">(earlier limit was 195 GB).</span></span>
-   <span data-ttu-id="af299-122">Résolu : problème de mémoire insuffisante lors de la décompression de plusieurs petits fichiers pendant l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="af299-122">Fixed: Out of memory issue while unzipping several small files during copy activity.</span></span>
-   <span data-ttu-id="af299-123">Résolu : problème d’index hors plage lors de la copie depuis Document DB vers le système SQL Server local avec la fonctionnalité d’idempotence.</span><span class="sxs-lookup"><span data-stu-id="af299-123">Fixed: Index out of range issue while copying from Document DB to an on-premises SQL Server with idempotency feature.</span></span>
-   <span data-ttu-id="af299-124">Résolu : le script de nettoyage SQL ne fonctionne pas avec la version locale de SQL Server à partir de l’Assistant de copie.</span><span class="sxs-lookup"><span data-stu-id="af299-124">Fixed: SQL cleanup script doesn't work with on-premises SQL Server from Copy Wizard.</span></span>
-   <span data-ttu-id="af299-125">Résolu : le nom de colonne avec un espace à la fin ne fonctionne pas dans l’activité de copie.</span><span class="sxs-lookup"><span data-stu-id="af299-125">Fixed: Column name with space at the end does not work in copy activity.</span></span>

## <a name="28662833"></a><span data-ttu-id="af299-126">2.8.66283.3</span><span class="sxs-lookup"><span data-stu-id="af299-126">2.8.66283.3</span></span>
### <a name="enhancements-"></a><span data-ttu-id="af299-127">Améliorations</span><span class="sxs-lookup"><span data-stu-id="af299-127">Enhancements-</span></span>
- <span data-ttu-id="af299-128">Résolu : problème d’informations d’identification manquantes au redémarrage de l’ordinateur de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="af299-128">Fixed: Issue with missing credentials on gateway machine reboot.</span></span>
- <span data-ttu-id="af299-129">Résolu : problème lié à l’inscription lors de la restauration de la passerelle à l’aide d’un fichier de sauvegarde.</span><span class="sxs-lookup"><span data-stu-id="af299-129">Fixed: Issue with registration during gateway restore using a backup file.</span></span>


## <a name="2762401"></a><span data-ttu-id="af299-130">2.7.6240.1</span><span class="sxs-lookup"><span data-stu-id="af299-130">2.7.6240.1</span></span>
### <a name="enhancements-"></a><span data-ttu-id="af299-131">Améliorations</span><span class="sxs-lookup"><span data-stu-id="af299-131">Enhancements-</span></span>
- <span data-ttu-id="af299-132">Résolu : lecture incorrecte d’une valeur null décimale à partir d’Oracle comme source.</span><span class="sxs-lookup"><span data-stu-id="af299-132">Fixed: Incorrect read of Decimal null value from Oracle as source.</span></span>

## <a name="2661922"></a><span data-ttu-id="af299-133">2.6.6192.2</span><span class="sxs-lookup"><span data-stu-id="af299-133">2.6.6192.2</span></span>
### <a name="whats-new"></a><span data-ttu-id="af299-134">Nouveautés</span><span class="sxs-lookup"><span data-stu-id="af299-134">What’s new</span></span>
- <span data-ttu-id="af299-135">Les clients peuvent faire part de leurs commentaires sur l’expérience d’inscription à la passerelle.</span><span class="sxs-lookup"><span data-stu-id="af299-135">Customers can provide feedback on gateway registering experience.</span></span>
- <span data-ttu-id="af299-136">Prise en charge d’un nouveau format de compression : ZIP (Deflate)</span><span class="sxs-lookup"><span data-stu-id="af299-136">Support a new compression format: ZIP (Deflate)</span></span>

### <a name="enhancements-"></a><span data-ttu-id="af299-137">Améliorations</span><span class="sxs-lookup"><span data-stu-id="af299-137">Enhancements-</span></span>
- <span data-ttu-id="af299-138">Amélioration des performances pour le récepteur d’Oracle, source HDFS.</span><span class="sxs-lookup"><span data-stu-id="af299-138">Performance improvement for Oracle Sink, HDFS source.</span></span>
- <span data-ttu-id="af299-139">Correctif de bogue pour la mise à jour automatique de la passerelle, capacité de traitement parallèle de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="af299-139">Bug fix for gateway auto update, gateway parallel processing capacity.</span></span>


## <a name="2561641"></a><span data-ttu-id="af299-140">2.5.6164.1</span><span class="sxs-lookup"><span data-stu-id="af299-140">2.5.6164.1</span></span>
### <a name="enhancements"></a><span data-ttu-id="af299-141">Améliorations</span><span class="sxs-lookup"><span data-stu-id="af299-141">Enhancements</span></span>
- <span data-ttu-id="af299-142">Expérience d’inscription de la passerelle améliorée et plus robuste. Vous pouvez maintenant suivre l’état d’avancement lors du processus d’inscription de la passerelle, ce qui rend l’expérience d’inscription plus réactive.</span><span class="sxs-lookup"><span data-stu-id="af299-142">Improved and more robust Gateway registration experience- Now you can track progress status during the Gateway registration process, which makes the registration experience more responsive.</span></span>
- <span data-ttu-id="af299-143">Amélioration du processus de restauration de la passerelle. Vous pouvez toujours récupérer la passerelle même si vous n’avez pas le fichier de sauvegarde de passerelle avec cette mise à jour.</span><span class="sxs-lookup"><span data-stu-id="af299-143">Improvement in Gateway Restore Process- You can still recover gateway even if you do not have the gateway backup file with this update.</span></span> <span data-ttu-id="af299-144">Cela vous oblige à réinitialiser les informations d’identification du Service lié dans le portail.</span><span class="sxs-lookup"><span data-stu-id="af299-144">This would require you to reset Linked Service credentials in Portal.</span></span>
- <span data-ttu-id="af299-145">Résolution de bogue.</span><span class="sxs-lookup"><span data-stu-id="af299-145">Bug fix.</span></span>

## <a name="2461511"></a><span data-ttu-id="af299-146">2.4.6151.1</span><span class="sxs-lookup"><span data-stu-id="af299-146">2.4.6151.1</span></span>

### <a name="whats-new"></a><span data-ttu-id="af299-147">Nouveautés</span><span class="sxs-lookup"><span data-stu-id="af299-147">What’s new</span></span>

- <span data-ttu-id="af299-148">Vous pouvez désormais stocker localement les informations d’identification de la source de données.</span><span class="sxs-lookup"><span data-stu-id="af299-148">You can now store data source credentials locally.</span></span> <span data-ttu-id="af299-149">Les informations d’identification sont chiffrées.</span><span class="sxs-lookup"><span data-stu-id="af299-149">The credentials are encrypted.</span></span> <span data-ttu-id="af299-150">Les informations d’identification de la source de données peuvent être récupérées et restaurées à l’aide du fichier de sauvegarde qui peut être exporté à partir de la passerelle existante, le tout localement.</span><span class="sxs-lookup"><span data-stu-id="af299-150">The data source credentials can be recovered and restored using the backup file that can be exported from the existing Gateway, all on-premises.</span></span>

### <a name="enhancements-"></a><span data-ttu-id="af299-151">Améliorations</span><span class="sxs-lookup"><span data-stu-id="af299-151">Enhancements-</span></span>

- <span data-ttu-id="af299-152">Expérience d’inscription de la passerelle améliorée et plus robuste.</span><span class="sxs-lookup"><span data-stu-id="af299-152">Improved and more robust Gateway registration experience.</span></span>
- <span data-ttu-id="af299-153">Prise en charge la détection automatique de la configuration de la propriété QuoteChar pour le format Texte dans l’Assistant de copie et amélioration la précision globale de la détection de format.</span><span class="sxs-lookup"><span data-stu-id="af299-153">Support auto detection of QuoteChar configuration for Text format in copy wizard, and improve the overall format detection accuracy.</span></span>

## <a name="2361002"></a><span data-ttu-id="af299-154">2.3.6100.2</span><span class="sxs-lookup"><span data-stu-id="af299-154">2.3.6100.2</span></span>

- <span data-ttu-id="af299-155">Prise en charge de la détection automatique firstRowAsHeader et SkipLineCount dans l’Assistant de copie pour les fichiers texte dans le système de fichiers local et HDFS.</span><span class="sxs-lookup"><span data-stu-id="af299-155">Support firstRowAsHeader and SkipLineCount auto detection in copy wizard for text files in on-premises File system and HDFS.</span></span>
- <span data-ttu-id="af299-156">Amélioration de la stabilité de la connexion réseau entre la passerelle et Service Bus</span><span class="sxs-lookup"><span data-stu-id="af299-156">Enhance the stability of network connection between gateway and Service Bus</span></span>
- <span data-ttu-id="af299-157">Résolution de quelques bogues</span><span class="sxs-lookup"><span data-stu-id="af299-157">A few bug fixes</span></span>


## <a name="2260721"></a><span data-ttu-id="af299-158">2.2.6072.1</span><span class="sxs-lookup"><span data-stu-id="af299-158">2.2.6072.1</span></span>

*  <span data-ttu-id="af299-159">Permet de paramétrer le proxy HTTP pour la passerelle à l’aide du Gestionnaire de configuration de passerelle.</span><span class="sxs-lookup"><span data-stu-id="af299-159">Supports setting HTTP proxy for the gateway using the Gateway Configuration Manager.</span></span> <span data-ttu-id="af299-160">Si configurés, Azure Blob, Azure Table, Azure Data Lake et Document DB sont accessibles via le proxy HTTP.</span><span class="sxs-lookup"><span data-stu-id="af299-160">If configured, Azure Blob, Azure Table, Azure Data Lake, and Document DB are accessed through HTTP proxy.</span></span>
*  <span data-ttu-id="af299-161">Prend en charge la gestion des en-têtes pour TextFormat lors de la copie des données depuis/vers un objet Blob Azure, Azure Data Lake Store, le système de fichiers local ou un système de fichiers HDFS local.</span><span class="sxs-lookup"><span data-stu-id="af299-161">Supports header handling for TextFormat when copying data from/to Azure Blob, Azure Data Lake Store, on-premises File System, and on-premises HDFS.</span></span>
*  <span data-ttu-id="af299-162">Prend en charge la copie des données d’objets blob d’ajouts et de pages, ainsi que des objets blob de blocs déjà pris en charge.</span><span class="sxs-lookup"><span data-stu-id="af299-162">Supports copying data from Append Blob and Page Blob along with the already supported Block Blob.</span></span>
*  <span data-ttu-id="af299-163">Introduit le nouvel état de passerelle **En ligne (limité)**, qui indique que la fonctionnalité principale de la passerelle fonctionne, à l’exception de la prise en charge de l’opération interactive pour l’assistant de copie.</span><span class="sxs-lookup"><span data-stu-id="af299-163">Introduces a new gateway status **Online (Limited)**, which indicates that the main functionality of the gateway works except the interactive operation support for Copy Wizard.</span></span>
*  <span data-ttu-id="af299-164">Améliore la robustesse de l’inscription de la passerelle avec la clé d’inscription.</span><span class="sxs-lookup"><span data-stu-id="af299-164">Enhances the robustness of gateway registration using registration key.</span></span>

## <a name="216040"></a><span data-ttu-id="af299-165">2.1.6040.</span><span class="sxs-lookup"><span data-stu-id="af299-165">2.1.6040.</span></span>

*  <span data-ttu-id="af299-166">Le pilote DB2 est désormais inclus dans le package d’installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="af299-166">DB2 driver is included in the gateway installation package now.</span></span> <span data-ttu-id="af299-167">Il est inutile de l’installer séparément.</span><span class="sxs-lookup"><span data-stu-id="af299-167">You do not need to install it separately.</span></span>
*  <span data-ttu-id="af299-168">Le pilote DB2 prend désormais en charge z/OS et DB2 pour i (AS/400), ainsi que les plateformes déjà prises en charge (Windows, Unix et Linux).</span><span class="sxs-lookup"><span data-stu-id="af299-168">DB2 driver now supports z/OS and DB2 for i (AS/400) along with the platforms already supported (Linux, Unix, and Windows).</span></span>
*  <span data-ttu-id="af299-169">Prend en charge l’utilisation d’Azure Cosmos DB comme source ou destination des banques de données locales</span><span class="sxs-lookup"><span data-stu-id="af299-169">Supports using Azure Cosmos DB as a source or destination for on-premises data stores</span></span>
*  <span data-ttu-id="af299-170">Prend en charge la copie de données depuis/vers un stockage d’objet blob à chaud ou à froid, ainsi que le compte de stockage à usage général déjà pris en charge.</span><span class="sxs-lookup"><span data-stu-id="af299-170">Supports copying data from/to cold/hot blob storage along with the already supported general-purpose storage account.</span></span>
*  <span data-ttu-id="af299-171">Permet de vous connecter l’instance SQL Server locale via la passerelle avec des droits de connexion à distance.</span><span class="sxs-lookup"><span data-stu-id="af299-171">Allows you to connect to on-premises SQL Server via gateway with remote login privileges.</span></span>  

## <a name="2060131"></a><span data-ttu-id="af299-172">2.0.6013.1</span><span class="sxs-lookup"><span data-stu-id="af299-172">2.0.6013.1</span></span>

*  <span data-ttu-id="af299-173">Vous pouvez sélectionner la langue/culture utilisée par une passerelle lors de l’installation manuelle.</span><span class="sxs-lookup"><span data-stu-id="af299-173">You can select the language/culture to be used by a gateway during manual installation.</span></span>

*  <span data-ttu-id="af299-174">Lorsqu’une passerelle ne fonctionne pas comme prévu, vous pouvez choisir d’envoyer les journaux des sept derniers jours de la passerelle à Microsoft pour faciliter la résolution du problème.</span><span class="sxs-lookup"><span data-stu-id="af299-174">When gateway does not work as expected, you can choose to send gateway logs of last seven days to Microsoft to facilitate troubleshooting of the issue.</span></span> <span data-ttu-id="af299-175">Si la passerelle n’est pas connectée au service cloud, vous pouvez choisir d’enregistrer et d’archiver les journaux de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="af299-175">If gateway is not connected to the cloud service, you can choose to save and archive gateway logs.</span></span>  

*  <span data-ttu-id="af299-176">Améliorations de l’interface utilisateur du gestionnaire de configuration de la passerelle :</span><span class="sxs-lookup"><span data-stu-id="af299-176">User interface improvements for gateway configuration manager:</span></span>

    *  <span data-ttu-id="af299-177">État de la passerelle plus visible dans l’onglet Accueil.</span><span class="sxs-lookup"><span data-stu-id="af299-177">Make gateway status more visible on the Home tab.</span></span>

    *  <span data-ttu-id="af299-178">Commandes réorganisées et simplifiées.</span><span class="sxs-lookup"><span data-stu-id="af299-178">Reorganized and simplified controls.</span></span>

    *  <span data-ttu-id="af299-179">Vous pouvez copier des données à partir d’un stockage à l’aide de [l’outil de prévisualisation de copie sans code](data-factory-copy-data-wizard-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="af299-179">You can copy data from a storage using the [code-free copy preview tool](data-factory-copy-data-wizard-tutorial.md).</span></span> <span data-ttu-id="af299-180">Pour plus d’informations sur cette fonctionnalité, consultez [Copie intermédiaire](data-factory-copy-activity-performance.md#staged-copy) .</span><span class="sxs-lookup"><span data-stu-id="af299-180">See [Staged Copy](data-factory-copy-activity-performance.md#staged-copy) for details about this feature in general.</span></span>
*  <span data-ttu-id="af299-181">Vous pouvez utiliser la passerelle de gestion des données pour entrer des données directement à partir d’une base de données SQL Server locale dans Azure Machine Learning.</span><span class="sxs-lookup"><span data-stu-id="af299-181">You can use Data Management Gateway to ingress data directly from an on-premises SQL Server database into Azure Machine Learning.</span></span>

*  <span data-ttu-id="af299-182">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-182">Performance improvements</span></span>

    * <span data-ttu-id="af299-183">Amélioration des performances d’affichage du schéma/de l’aperçu par rapport à SQL Server dans l’outil de prévisualisation de copie sans code.</span><span class="sxs-lookup"><span data-stu-id="af299-183">Improve performance on viewing Schema/Preview against SQL Server in code-free copy preview tool.</span></span>

## <a name="11259531"></a><span data-ttu-id="af299-184">1.12.5953.1</span><span class="sxs-lookup"><span data-stu-id="af299-184">1.12.5953.1</span></span>

*  <span data-ttu-id="af299-185">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-185">Bug fixes</span></span>

## <a name="11159181"></a><span data-ttu-id="af299-186">1.11.5918.1</span><span class="sxs-lookup"><span data-stu-id="af299-186">1.11.5918.1</span></span>

*  <span data-ttu-id="af299-187">La taille maximale du journal des événements de la passerelle a été augmentée de 1 Mo à 40 Mo.</span><span class="sxs-lookup"><span data-stu-id="af299-187">Maximum size of the gateway event log has been increased from 1 MB to 40 MB.</span></span>

*  <span data-ttu-id="af299-188">Une boîte de dialogue d’avertissement s’affiche si un redémarrage est nécessaire pendant la mise à jour automatique de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="af299-188">A warning dialog is displayed in case a restart is needed during gateway auto-update.</span></span> <span data-ttu-id="af299-189">Vous pouvez choisir de redémarrer immédiatement ou plus tard.</span><span class="sxs-lookup"><span data-stu-id="af299-189">You can choose to restart right then or later.</span></span>

*  <span data-ttu-id="af299-190">En cas d’échec de la mise à jour automatique, le programme d’installation de la passerelle retente la mise à jour automatique trois fois au maximum.</span><span class="sxs-lookup"><span data-stu-id="af299-190">In case auto-update fails, gateway installer retries auto-updating three times at maximum.</span></span>

*  <span data-ttu-id="af299-191">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-191">Performance improvements</span></span>

    * <span data-ttu-id="af299-192">Améliorez les performances lors du chargement de tables de grande taille à partir du serveur local dans le scénario de copie sans code.</span><span class="sxs-lookup"><span data-stu-id="af299-192">Improve performance for loading large tables from on-premises server in code-free copy scenario.</span></span>

*  <span data-ttu-id="af299-193">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-193">Bug fixes</span></span>

## <a name="11058921"></a><span data-ttu-id="af299-194">1.10.5892.1</span><span class="sxs-lookup"><span data-stu-id="af299-194">1.10.5892.1</span></span>

*  <span data-ttu-id="af299-195">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-195">Performance improvements</span></span>

*  <span data-ttu-id="af299-196">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-196">Bug fixes</span></span>

## <a name="1958652"></a><span data-ttu-id="af299-197">1.9.5865.2</span><span class="sxs-lookup"><span data-stu-id="af299-197">1.9.5865.2</span></span>

*  <span data-ttu-id="af299-198">Capacité de mise à jour automatique Zero Touch</span><span class="sxs-lookup"><span data-stu-id="af299-198">Zero touch auto update capability</span></span>
*  <span data-ttu-id="af299-199">Nouvelle icône de barre d’état système avec des indicateurs d’état de la passerelle</span><span class="sxs-lookup"><span data-stu-id="af299-199">New tray icon with gateway status indicators</span></span>
*  <span data-ttu-id="af299-200">Possibilité de mise à jour immédiate depuis le client</span><span class="sxs-lookup"><span data-stu-id="af299-200">Ability to “Update now” from the client</span></span>
*  <span data-ttu-id="af299-201">Possibilité de définir l’heure de planification de la mise à jour</span><span class="sxs-lookup"><span data-stu-id="af299-201">Ability to set update schedule time</span></span>
*  <span data-ttu-id="af299-202">Script PowerShell disponible pour activer/désactiver la mise à jour automatique</span><span class="sxs-lookup"><span data-stu-id="af299-202">PowerShell script for toggling auto-update on/off</span></span>
*  <span data-ttu-id="af299-203">Prise en charge du format JSON</span><span class="sxs-lookup"><span data-stu-id="af299-203">Support for JSON format</span></span>  
*  <span data-ttu-id="af299-204">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-204">Performance improvements</span></span>
*  <span data-ttu-id="af299-205">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-205">Bug fixes</span></span>

## <a name="1858221"></a><span data-ttu-id="af299-206">1.8.5822.1</span><span class="sxs-lookup"><span data-stu-id="af299-206">1.8.5822.1</span></span>

*  <span data-ttu-id="af299-207">Amélioration de l’expérience de résolution des problèmes</span><span class="sxs-lookup"><span data-stu-id="af299-207">Improve troubleshooting experience</span></span>
*  <span data-ttu-id="af299-208">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-208">Performance improvements</span></span>
*  <span data-ttu-id="af299-209">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-209">Bug fixes</span></span>

### <a name="1757951"></a><span data-ttu-id="af299-210">1.7.5795.1</span><span class="sxs-lookup"><span data-stu-id="af299-210">1.7.5795.1</span></span>

*  <span data-ttu-id="af299-211">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-211">Performance improvements</span></span>
*  <span data-ttu-id="af299-212">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-212">Bug fixes</span></span>

### <a name="1757641"></a><span data-ttu-id="af299-213">1.7.5764.1</span><span class="sxs-lookup"><span data-stu-id="af299-213">1.7.5764.1</span></span>

*  <span data-ttu-id="af299-214">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-214">Performance improvements</span></span>
*  <span data-ttu-id="af299-215">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-215">Bug fixes</span></span>

### <a name="1657351"></a><span data-ttu-id="af299-216">1.6.5735.1</span><span class="sxs-lookup"><span data-stu-id="af299-216">1.6.5735.1</span></span>

*  <span data-ttu-id="af299-217">Prise en charge de la source/du récepteur HDFS en local</span><span class="sxs-lookup"><span data-stu-id="af299-217">Support on-premises HDFS Source/Sink</span></span>
*  <span data-ttu-id="af299-218">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-218">Performance improvements</span></span>
*  <span data-ttu-id="af299-219">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-219">Bug fixes</span></span>

### <a name="1656961"></a><span data-ttu-id="af299-220">1.6.5696.1</span><span class="sxs-lookup"><span data-stu-id="af299-220">1.6.5696.1</span></span>

*  <span data-ttu-id="af299-221">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-221">Performance improvements</span></span>
*  <span data-ttu-id="af299-222">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-222">Bug fixes</span></span>

### <a name="1656761"></a><span data-ttu-id="af299-223">1.6.5676.1</span><span class="sxs-lookup"><span data-stu-id="af299-223">1.6.5676.1</span></span>

*  <span data-ttu-id="af299-224">Prise en charge des outils de diagnostic dans le Gestionnaire de configuration</span><span class="sxs-lookup"><span data-stu-id="af299-224">Support diagnostic tools on Configuration Manager</span></span>
*  <span data-ttu-id="af299-225">Prise en charge des colonnes de table pour les sources de données tabulaires pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-225">Support table columns for tabular data sources for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-226">Prise en charge de SQL DW pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-226">Support SQL DW for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-227">Prise en charge de Reclusive dans BlobSource et FileSource pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-227">Support Reclusive in BlobSource and FileSource for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-228">Prise en charge de CopyBehavior (MergeFiles, PreserveHierarchy et FlattenHierarchy) dans BlobSink et FileSink avec copie binaire pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-228">Support CopyBehavior – MergeFiles, PreserveHierarchy, and FlattenHierarchy in BlobSink and FileSink with Binary Copy for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-229">Prise en charge du signalement de progression de l’activité de copie pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-229">Support Copy Activity reporting progress for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-230">Prise en charge de la validation de connectivité des sources de données pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-230">Support Data Source Connectivity Validation for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-231">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-231">Bug fixes</span></span>

### <a name="1656721"></a><span data-ttu-id="af299-232">1.6.5672.1</span><span class="sxs-lookup"><span data-stu-id="af299-232">1.6.5672.1</span></span>

*  <span data-ttu-id="af299-233">Prise en charge des noms de tables pour la source de données ODBC pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-233">Support table name for ODBC data source for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-234">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-234">Performance improvements</span></span>
*  <span data-ttu-id="af299-235">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-235">Bug fixes</span></span>

### <a name="1656581"></a><span data-ttu-id="af299-236">1.6.5658.1</span><span class="sxs-lookup"><span data-stu-id="af299-236">1.6.5658.1</span></span>

*  <span data-ttu-id="af299-237">Prise en charge du récepteur de fichier pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-237">Support File Sink for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-238">Prise en charge de la conservation de la hiérarchie dans une copie binaire pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-238">Support preserving hierarchy in binary copy for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-239">Prise en charge de l’idempotence de l’activité de copie pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-239">Support Copy Activity Idempotency for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-240">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-240">Bug fixes</span></span>

### <a name="1656401"></a><span data-ttu-id="af299-241">1.6.5640.1</span><span class="sxs-lookup"><span data-stu-id="af299-241">1.6.5640.1</span></span>

*  <span data-ttu-id="af299-242">Prise en charge de 3 sources de données supplémentaires pour Microsoft Azure Data Factory (ODBC, OData, HDFS)</span><span class="sxs-lookup"><span data-stu-id="af299-242">Support 3 more data sources for Azure Data Factory (ODBC, OData, HDFS)</span></span>
*  <span data-ttu-id="af299-243">Prise en charge du caractère guillemet dans l’analyseur CSV pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-243">Support quote character in csv parser for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-244">Prise en charge de la compression (BZip2)</span><span class="sxs-lookup"><span data-stu-id="af299-244">Compression support (BZip2)</span></span>
*  <span data-ttu-id="af299-245">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-245">Bug fixes</span></span>

### <a name="1556121"></a><span data-ttu-id="af299-246">1.5.5612.1</span><span class="sxs-lookup"><span data-stu-id="af299-246">1.5.5612.1</span></span>

*  <span data-ttu-id="af299-247">Prise en charge de cinq bases de données relationnelles pour Microsoft Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata et Sybase)</span><span class="sxs-lookup"><span data-stu-id="af299-247">Support five relational databases for Azure Data Factory (MySQL, PostgreSQL, DB2, Teradata, and Sybase)</span></span>
*  <span data-ttu-id="af299-248">Prise en charge de la compression (Gzip et Deflate)</span><span class="sxs-lookup"><span data-stu-id="af299-248">Compression support (Gzip and Deflate)</span></span>
*  <span data-ttu-id="af299-249">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-249">Performance improvements</span></span>
*  <span data-ttu-id="af299-250">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-250">Bug fixes</span></span>

### <a name="1455491"></a><span data-ttu-id="af299-251">1.4.5549.1</span><span class="sxs-lookup"><span data-stu-id="af299-251">1.4.5549.1</span></span>

*  <span data-ttu-id="af299-252">Ajout de la prise en charge de source de données Oracle pour Microsoft Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="af299-252">Add Oracle data source support for Azure Data Factory</span></span>
*  <span data-ttu-id="af299-253">Amélioration des performances</span><span class="sxs-lookup"><span data-stu-id="af299-253">Performance improvements</span></span>
*  <span data-ttu-id="af299-254">Résolution des bogues</span><span class="sxs-lookup"><span data-stu-id="af299-254">Bug fixes</span></span>

### <a name="1454921"></a><span data-ttu-id="af299-255">1.4.5492.1</span><span class="sxs-lookup"><span data-stu-id="af299-255">1.4.5492.1</span></span>

*  <span data-ttu-id="af299-256">Binaire unifié qui prend en charge à la fois des services Microsoft Azure Data Factory et Office 365 Power BI</span><span class="sxs-lookup"><span data-stu-id="af299-256">Unified binary that supports both Microsoft Azure Data Factory and Office 365 Power BI services</span></span>
*  <span data-ttu-id="af299-257">Affinage du processus d’inscription et de l’interface utilisateur de configuration</span><span class="sxs-lookup"><span data-stu-id="af299-257">Refine the Configuration UI and registration process</span></span>
*  <span data-ttu-id="af299-258">Microsoft Azure Data Factory : prise en charge des entrées et sorties Azure pour la source de données SQL Server</span><span class="sxs-lookup"><span data-stu-id="af299-258">Azure Data Factory – Azure Ingress and Egress support for SQL Server data source</span></span>

### <a name="1253031"></a><span data-ttu-id="af299-259">1.2.5303.1</span><span class="sxs-lookup"><span data-stu-id="af299-259">1.2.5303.1</span></span>

*  <span data-ttu-id="af299-260">Correction du problème de délai d’expiration pour la prise en charge de connexions de source de données chronophages supplémentaires.</span><span class="sxs-lookup"><span data-stu-id="af299-260">Fix timeout issue to support more time-consuming data source connections.</span></span>

### <a name="1155268"></a><span data-ttu-id="af299-261">1.1.5526.8</span><span class="sxs-lookup"><span data-stu-id="af299-261">1.1.5526.8</span></span>

*  <span data-ttu-id="af299-262">.NET Framework 4.5.1 est requis pour l’installation.</span><span class="sxs-lookup"><span data-stu-id="af299-262">Requires .NET Framework 4.5.1 as a prerequisite during setup.</span></span>

### <a name="1051442"></a><span data-ttu-id="af299-263">1.0.5144.2</span><span class="sxs-lookup"><span data-stu-id="af299-263">1.0.5144.2</span></span>

*  <span data-ttu-id="af299-264">Aucune modification affectant les scénarios Microsoft Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="af299-264">No changes that affect Azure Data Factory scenarios.</span></span>
