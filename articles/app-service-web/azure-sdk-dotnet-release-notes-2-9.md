---
title: aaaAzure SDK pour .NET 2.9 Notes de publication
description: "Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.9"
services: app-service\web
documentationcenter: .net
author: chrissfanos
editor: 
ms.assetid: c83d815b-fc19-4260-821e-7d2a7206dffc
ms.service: app-service
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 02/24/2017
ms.author: juliako
ms.openlocfilehash: 96df2b80224190cc2093e6bf350eaec224ac2e98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sdk-for-net-29-release-notes"></a><span data-ttu-id="ed930-103">Notes de publication du Kit de développement logiciel (SDK) Azure pour .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="ed930-103">Azure SDK for .NET 2.9 release notes</span></span>

<span data-ttu-id="ed930-104">Cette rubrique comprend des notes de publication relatives aux versions 2.9 et 2.9.6 du Kit SDK Azure pour .NET.</span><span class="sxs-lookup"><span data-stu-id="ed930-104">This topic includes release notes for versions 2.9 and 2.9.6 of Azure SDK for .NET.</span></span>

##<a name="azure-sdk-for-net-296-release-summary"></a><span data-ttu-id="ed930-105">Synthèse de publication du Kit SDK Azure pour .NET 2.9.6</span><span class="sxs-lookup"><span data-stu-id="ed930-105">Azure SDK for .NET 2.9.6 release summary</span></span>

<span data-ttu-id="ed930-106">Date de lancement : 16/11/2016</span><span class="sxs-lookup"><span data-stu-id="ed930-106">Release date: 11/16/2016</span></span>
 
<span data-ttu-id="ed930-107">Aucune toohello de modifications avec rupture Azure SDK 2.9 n’ont été introduites dans cette version.</span><span class="sxs-lookup"><span data-stu-id="ed930-107">No breaking changes toohello Azure SDK 2.9 have been introduced in this release.</span></span> <span data-ttu-id="ed930-108">Il n’existe également aucune tooleverage de mise à niveau si nécessaire ce SDK avec les projets de Service Cloud existants.</span><span class="sxs-lookup"><span data-stu-id="ed930-108">There is also no upgrade process needed tooleverage this SDK with existing Cloud Service projects.</span></span>

### <a name="visual-studio-2017-release-candidate"></a><span data-ttu-id="ed930-109">Version finale de Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="ed930-109">Visual Studio 2017 Release Candidate</span></span>

- <span data-ttu-id="ed930-110">Dans Visual Studio 2017 RC, cette version de hello Azure SDK pour .NET est intégrée dans hello la charge de travail Azure.</span><span class="sxs-lookup"><span data-stu-id="ed930-110">In Visual Studio 2017 RC, this release of hello Azure SDK for .NET is built in in hello Azure Workload.</span></span> <span data-ttu-id="ed930-111">Tous les outils hello vous devez toodo le développement Azure feront partie de Visual Studio RC 2017 à l’avenir.</span><span class="sxs-lookup"><span data-stu-id="ed930-111">All hello tools you need toodo Azure development will be part of Visual Studio 2017 RC going forward.</span></span> <span data-ttu-id="ed930-112">Pour Visual Studio 2015 et Visual Studio 2013, hello SDK seront toujours disponible via WebPI.</span><span class="sxs-lookup"><span data-stu-id="ed930-112">For Visual Studio 2015 and Visual Studio 2013, hello SDK will still be available through WebPI.</span></span> <span data-ttu-id="ed930-113">Nous arrêterons d’équiper les versions du Kit SDK Azure pour .NET pour Visual Studio 2013 au moment du lancement de la version finale de Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="ed930-113">We will be discontinuing Azure SDK for .NET releases for Visual Studio 2013, when Visual Studio 2017 releases as a final product.</span></span> <span data-ttu-id="ed930-114">Suivez cette toodownload lien Visual Studio 2017 RC : https://www.visualstudio.com/vs/visual-studio-2017-rc/</span><span class="sxs-lookup"><span data-stu-id="ed930-114">Follow this link toodownload Visual Studio 2017 RC: https://www.visualstudio.com/vs/visual-studio-2017-rc/</span></span>

### <a name="azure-diagnostics"></a><span data-ttu-id="ed930-115">Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="ed930-115">Azure Diagnostics</span></span>

- <span data-ttu-id="ed930-116">Tooonly de comportement modifié hello stocker une chaîne de connexion partielle avec clé hello remplacé par un jeton de chaîne de connexion de stockage de diagnostics Services de cloud computing.</span><span class="sxs-lookup"><span data-stu-id="ed930-116">Changed hello behavior tooonly store a partial connection string with hello key replaced by a token for Cloud Services diagnostics storage connection string.</span></span> <span data-ttu-id="ed930-117">clé de stockage réel Hello est maintenant stockée dans le dossier du profil utilisateur hello pour son accès peut être contrôlé.</span><span class="sxs-lookup"><span data-stu-id="ed930-117">hello actual storage key is now stored in hello user profile folder so its access can be controlled.</span></span> <span data-ttu-id="ed930-118">Visual Studio lit la clé de stockage hello dans le dossier de profil utilisateur pour le débogage local et le processus de publication.</span><span class="sxs-lookup"><span data-stu-id="ed930-118">Visual Studio will read hello storage key from user profile folder for local debugging and publishing process.</span></span> 
- <span data-ttu-id="ed930-119">Dans la réponse toohello modification est décrite ci-dessus, Visual Studio Online de l’équipe étendu hello modèle de tâche de déploiement de Services de cloud computing Azure utilisateurs peuvent spécifier la clé de stockage hello pour définir l’extension diagnostics lors de la publication tooAzure dans l’intégration continue et le déploiement.</span><span class="sxs-lookup"><span data-stu-id="ed930-119">In response toohello change described above, Visual Studio Online team enhanced hello Azure Cloud Services deployment task template so users could specify hello storage key for setting diagnostics extension when publishing tooAzure in Continuous Integration and Deployment.</span></span>
- <span data-ttu-id="ed930-120">Nous nous efforçons de chaîne de connexion sécurisée toostore possibles et la création de jetons pour Azure Diagnostics (WAD), toohelp vous résoudre des problèmes de configuration entre multiprotocole.</span><span class="sxs-lookup"><span data-stu-id="ed930-120">We’ve made it possible toostore secure connection string and tokenization for Azure Diagnostics (WAD), toohelp you solve problems with configuration across environements.</span></span>
 
### <a name="windows-server-2016-virtual-machines"></a><span data-ttu-id="ed930-121">Machines virtuelles Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ed930-121">Windows Server 2016 virtual machines</span></span>

- <span data-ttu-id="ed930-122">Visual Studio prend désormais en charge le déploiement des Services de Cloud tooOS ordinateurs virtuels de famille 5 (Windows Server 2016).</span><span class="sxs-lookup"><span data-stu-id="ed930-122">Visual Studio now supports deploying Cloud Services tooOS Family 5 (Windows Server 2016) virtual machines.</span></span> <span data-ttu-id="ed930-123">Pour les services cloud existants, vous pouvez modifier votre tootarget paramètres hello nouvelle famille de systèmes d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ed930-123">For existing cloud services, you can change your settings tootarget hello new OS Family.</span></span> <span data-ttu-id="ed930-124">Lors de la création de nouveaux services de cloud, si vous choisissez le service de hello toocreate à l’aide de .net 4.6 ou ultérieure, il prend par défaut hello service toouse 5 de famille du système d’exploitation.</span><span class="sxs-lookup"><span data-stu-id="ed930-124">When creating new cloud services, if you choose toocreate hello service using .net 4.6 or higher, it will default hello service toouse OS Family 5.</span></span>  <span data-ttu-id="ed930-125">Pour plus d’informations, vous pouvez consulter hello [famille de systèmes d’exploitation invité prend en charge la table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span><span class="sxs-lookup"><span data-stu-id="ed930-125">For more information, you can review hello [Guest OS Family support table](https://azure.microsoft.com/en-us/documentation/articles/cloud-services-guestos-update-matrix/).</span></span>

#### <a name="known-issues"></a><span data-ttu-id="ed930-126">Problèmes connus</span><span class="sxs-lookup"><span data-stu-id="ed930-126">Known issues</span></span>

- <span data-ttu-id="ed930-127">Azure SDK .NET 2.9.6 a introduit une restriction qui bloque le déploiement de projets à l’aide de tooany d’infrastructures (telles que .NET 4.6) non pris en charge .NET famille de système d’exploitation < 5.</span><span class="sxs-lookup"><span data-stu-id="ed930-127">Azure .NET SDK 2.9.6 introduced a restriction that blocks deployment of projects using unsupported .NET frameworks (such as .NET 4.6) tooany OS Family < 5.</span></span> <span data-ttu-id="ed930-128">Une solution de contournement est fournie [ici](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span><span class="sxs-lookup"><span data-stu-id="ed930-128">A workaround is provided [here](https://github.com/MicrosoftDocs/azure-cloud-services-files/tree/master/Azure%20Targets%20SDK%202.9).</span></span>

 
### <a name="azure-in-role-cache"></a><span data-ttu-id="ed930-129">In-Role Cache Azure</span><span class="sxs-lookup"><span data-stu-id="ed930-129">Azure In-Role Cache</span></span> 

- <span data-ttu-id="ed930-130">La prise en charge d’Azure In-Role Cache prend fin le 30 novembre 2016.</span><span class="sxs-lookup"><span data-stu-id="ed930-130">Support for Azure In-Role Cache ends on November 30, 2016.</span></span> <span data-ttu-id="ed930-131">Pour plus de détails, cliquez [ici](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span><span class="sxs-lookup"><span data-stu-id="ed930-131">For more details, click [here](https://azure.microsoft.com/en-us/blog/azure-managed-cache-and-in-role-cache-services-to-be-retired-on-11-30-2016/).</span></span>

### <a name="azure-resource-manager-templates-for-azure-stack"></a><span data-ttu-id="ed930-132">Modèles Azure Resource Manager pour Azure Stack</span><span class="sxs-lookup"><span data-stu-id="ed930-132">Azure Resource Manager Templates for Azure Stack</span></span>

- <span data-ttu-id="ed930-133">Nous avons introduit Azure Stack en tant que cible de déploiement pour vos modèles Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed930-133">We’ve introduced Azure Stack as a deployment target for your Azure Resource Manager Templates.</span></span>


## <a name="azure-sdk-for-net-29-summary"></a><span data-ttu-id="ed930-134">Synthèse du Kit SDK Azure pour .NET 2.9</span><span class="sxs-lookup"><span data-stu-id="ed930-134">Azure SDK for .NET 2.9 summary</span></span>

## <a name="overview"></a><span data-ttu-id="ed930-135">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="ed930-135">Overview</span></span>
<span data-ttu-id="ed930-136">Ce document contient les notes de publication hello pour hello Azure SDK pour .NET 2.9 version.</span><span class="sxs-lookup"><span data-stu-id="ed930-136">This document contains hello release notes for hello Azure SDK for .NET 2.9 release.</span></span> 

<span data-ttu-id="ed930-137">Pour plus d’informations sur les mises à jour dans cette version, consultez hello [post d’annonce Azure SDK 2.9](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span><span class="sxs-lookup"><span data-stu-id="ed930-137">For detailed information about updates in this release, see hello [Azure SDK 2.9 announcement post](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/).</span></span>

## <a name="azure-sdk-29-for-visual-studio-2015-update-2-and-visual-studio-15-preview"></a><span data-ttu-id="ed930-138">Aperçu du Kit de développement logiciel (SDK) 2.9 pour Visual Studio 2015 Update 2 et Visual Studio "15"</span><span class="sxs-lookup"><span data-stu-id="ed930-138">Azure SDK 2.9 for Visual Studio 2015 Update 2 and Visual Studio "15" Preview</span></span>
<span data-ttu-id="ed930-139">Cette mise à jour inclut hello suivant les correctifs de bogues :</span><span class="sxs-lookup"><span data-stu-id="ed930-139">This update includes hello following bug fixes:</span></span>

* <span data-ttu-id="ed930-140">Émettre tooREST connexe API Client génération dans la chaîne hello « Type inconnu » apparaît en tant que nom hello du dossier de génération de code hello et/ou nom hello d’espace de noms hello déposé dans le code de hello généré.</span><span class="sxs-lookup"><span data-stu-id="ed930-140">Issue related tooREST API Client Generation in in which hello string "Unknown Type” would appear as hello name of hello code-gen folder and/or hello name of hello namespace dropped into hello generated code.</span></span>
* <span data-ttu-id="ed930-141">Émettre WebJobs tooScheduled connexes dans le hello, informations d’authentification a échoué toobe passé le processus d’approvisionnement toohello du planificateur.</span><span class="sxs-lookup"><span data-stu-id="ed930-141">Issue related tooScheduled WebJobs in which hello authentication information was failing toobe passed toohello Scheduler provisioning process.</span></span>

<span data-ttu-id="ed930-142">Cette mise à jour inclut hello suivant la nouvelle fonctionnalité :</span><span class="sxs-lookup"><span data-stu-id="ed930-142">This update includes hello following new feature:</span></span>

* <span data-ttu-id="ed930-143">Prise en charge pour les Services d’application secondaire hello onglet « Services » de hello boîte de dialogue Configuration du Service d’applications.</span><span class="sxs-lookup"><span data-stu-id="ed930-143">Support for secondary App Services in hello "Services" tab of hello App Service provisioning dialog.</span></span> 

## <a name="azure-data-lake-tools-for-visual-studio-2015-update-2"></a><span data-ttu-id="ed930-144">Outils Azure Data Lake pour Visual Studio 2015 Update 2</span><span class="sxs-lookup"><span data-stu-id="ed930-144">Azure Data Lake Tools for Visual Studio 2015 Update 2</span></span>
<span data-ttu-id="ed930-145">Cette mise à jour inclut hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="ed930-145">This updates includes hello following:</span></span>

* <span data-ttu-id="ed930-146">**Azure Data Lake Tools** pour Visual Studio est maintenant fusionnée à hello Azure SDK pour cette version de .NET.</span><span class="sxs-lookup"><span data-stu-id="ed930-146">**Azure Data Lake Tools** for Visual Studio is now merged into hello Azure SDK for .NET release.</span></span> <span data-ttu-id="ed930-147">Hello outil est automatiquement installé lorsque vous installez le Kit de développement logiciel Azure.</span><span class="sxs-lookup"><span data-stu-id="ed930-147">hello tool is automatically installed when you install Azure SDK.</span></span> 
  
    <span data-ttu-id="ed930-148">outil de Hello est fréquemment mis à jour, accédez [ici](http://aka.ms/datalaketool) tooget hello les mises à jour.</span><span class="sxs-lookup"><span data-stu-id="ed930-148">hello tool is updated frequently, go [here](http://aka.ms/datalaketool) tooget hello updates.</span></span>
* <span data-ttu-id="ed930-149">**L’Explorateur de serveurs** maintenant vous tooview tous les et créer des entités de métadonnées U-SQL.</span><span class="sxs-lookup"><span data-stu-id="ed930-149">**Server Explorer** now enables you tooview all and create some U-SQL metadata entities.</span></span> <span data-ttu-id="ed930-150">Pour plus d’informations, consultez [ce](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span><span class="sxs-lookup"><span data-stu-id="ed930-150">For more information, see [this](https://azure.microsoft.com/documentation/services/data-lake-analytics/) blog.</span></span>

## <a name="hdinsight-tools"></a><span data-ttu-id="ed930-151">Outils HDInsight</span><span class="sxs-lookup"><span data-stu-id="ed930-151">HDInsight Tools</span></span>
<span data-ttu-id="ed930-152">**Outils HDInsight** pour Visual Studio prennent maintenant en charge HDInsight version 3.3, y compris l'affichage des graphiques Tez et d'autres correctifs de langage.</span><span class="sxs-lookup"><span data-stu-id="ed930-152">**HDInsight Tools** for Visual Studio now supports HDInsight version 3.3, including showing Tez graphs and other language fixes.</span></span>

## <a name="azure-resource-manager"></a><span data-ttu-id="ed930-153">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ed930-153">Azure Resource Manager</span></span>
<span data-ttu-id="ed930-154">Cette version ajoute la prise en charge de [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) pour les modèles Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ed930-154">This release adds [KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) support for Resource Manager templates.</span></span>

## <a name="see-also"></a><span data-ttu-id="ed930-155">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="ed930-155">See also</span></span>
[<span data-ttu-id="ed930-156">Billet d’annonce du Kit de développement logiciel (SDK) Azure 2.9</span><span class="sxs-lookup"><span data-stu-id="ed930-156">Azure SDK 2.9 announcement post</span></span>](https://azure.microsoft.com/blog/announcing-visual-studio-azure-tools-and-sdk-2-9/)

