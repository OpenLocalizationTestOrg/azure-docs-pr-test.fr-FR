---
title: "aaaHow toogenerate transfert protégée par HSM clés et d’Azure Key Vault | Documents Microsoft"
description: "Utilisez cette toohelp article vous planifiez, générez et transférez votre propre toouse clés protégées par HSM avec Azure Key Vault. Cette méthode est également appelée BYOK (Bring Your Own Key, ou apportez votre propre clé)."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 51abafa1-812b-460f-a129-d714fdc391da
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/09/2017
ms.author: ambapat
ms.openlocfilehash: 3bb234bd1c4b81770542ccf7110e256385ca3309
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toogenerate-and-transfer-hsm-protected-keys-for-azure-key-vault"></a><span data-ttu-id="ba604-104">Comment toogenerate et transfert de clés protégées par HSM pour Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ba604-104">How toogenerate and transfer HSM-protected keys for Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="ba604-105">Introduction</span><span class="sxs-lookup"><span data-stu-id="ba604-105">Introduction</span></span>
<span data-ttu-id="ba604-106">Pour plus de sûreté, lorsque vous utilisez le coffre de clés Azure, vous pouvez importer ou générer des clés dans les modules de sécurité matériel (HSM) qui ne quittent jamais les limites HSM hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-106">For added assurance, when you use Azure Key Vault, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="ba604-107">Ce scénario est souvent désignée tooas *mettre votre propre clé*, ou BYOK.</span><span class="sxs-lookup"><span data-stu-id="ba604-107">This scenario is often referred tooas *bring your own key*, or BYOK.</span></span> <span data-ttu-id="ba604-108">Hello HSM sont FIPS 140-2 niveau 2 validé.</span><span class="sxs-lookup"><span data-stu-id="ba604-108">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="ba604-109">Coffre de clés Azure utilise famille nShield de Thales de modules de sécurité matériels tooprotect vos clés.</span><span class="sxs-lookup"><span data-stu-id="ba604-109">Azure Key Vault uses Thales nShield family of HSMs tooprotect your keys.</span></span>

<span data-ttu-id="ba604-110">Utilisez les informations de hello dans cette toohelp de rubrique, vous planifiez, générez et transférez votre propre toouse clés protégées par HSM avec Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ba604-110">Use hello information in this topic toohelp you plan for, generate, and then transfer your own HSM-protected keys toouse with Azure Key Vault.</span></span>

<span data-ttu-id="ba604-111">Cette fonctionnalité n’est pas disponible pour Azure en Chine.</span><span class="sxs-lookup"><span data-stu-id="ba604-111">This functionality is not available for Azure China.</span></span>

> [!NOTE]
> <span data-ttu-id="ba604-112">Pour plus d’informations sur le coffre de clés Azure, consultez la page [Présentation du coffre de clés Azure](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="ba604-112">For more information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>  
>
> <span data-ttu-id="ba604-113">Pour voir un didacticiel de mise en route incluant un coffre de clés pour les clés protégées par HSM, consultez la section [Prise en main du coffre de clés Azure](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ba604-113">For a getting started tutorial, which includes creating a key vault for HSM-protected keys, see [Get started with Azure Key Vault](key-vault-get-started.md).</span></span>
>
>

<span data-ttu-id="ba604-114">Plus d’informations sur la génération et transfert d’une clé protégée par HSM sur hello Internet :</span><span class="sxs-lookup"><span data-stu-id="ba604-114">More information about generating and transferring an HSM-protected key over hello Internet:</span></span>

* <span data-ttu-id="ba604-115">Vous générez la clé de hello à partir d’une station de travail hors connexion, ce qui réduit la surface d’attaque hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-115">You generate hello key from an offline workstation, which reduces hello attack surface.</span></span>
* <span data-ttu-id="ba604-116">clé de Hello est chiffré avec une clé d’échange de clé (clés), qui reste chiffrée jusqu'à ce qu’il est transféré toohello HSM de coffre de clés Azure.</span><span class="sxs-lookup"><span data-stu-id="ba604-116">hello key is encrypted with a Key Exchange Key (KEK), which stays encrypted until it is transferred toohello Azure Key Vault HSMs.</span></span> <span data-ttu-id="ba604-117">Hello uniquement une version chiffrée de votre clé quitte la station de travail d’origine hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-117">Only hello encrypted version of your key leaves hello original workstation.</span></span>
* <span data-ttu-id="ba604-118">ensemble d’outils Hello définit des propriétés sur votre clé de locataire qui lie votre clé toohello monde de sécurité Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ba604-118">hello toolset sets properties on your tenant key that binds your key toohello Azure Key Vault security world.</span></span> <span data-ttu-id="ba604-119">Par conséquent, après que HSM de coffre de clés Azure hello reçu et déchiffré votre clé, ils sont les seuls pouvez l’utiliser.</span><span class="sxs-lookup"><span data-stu-id="ba604-119">So after hello Azure Key Vault HSMs receive and decrypt your key, only these HSMs can use it.</span></span> <span data-ttu-id="ba604-120">Il est impossible d’exporter votre clé.</span><span class="sxs-lookup"><span data-stu-id="ba604-120">Your key cannot be exported.</span></span> <span data-ttu-id="ba604-121">Cette liaison est appliquée par hello de sécurité matériels Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-121">This binding is enforced by hello Thales HSMs.</span></span>
* <span data-ttu-id="ba604-122">Hello Key Exchange Key (KEK) qui est utilisé tooencrypt votre clé est générée au sein des HSM de coffre de clés Azure hello et n’est pas exportable.</span><span class="sxs-lookup"><span data-stu-id="ba604-122">hello Key Exchange Key (KEK) that is used tooencrypt your key is generated inside hello Azure Key Vault HSMs and is not exportable.</span></span> <span data-ttu-id="ba604-123">les modules HSM Hello appliquent qu’il ne peut y avoir aucune version claire de hello veillent à l’extérieur de hello HSM.</span><span class="sxs-lookup"><span data-stu-id="ba604-123">hello HSMs enforce that there can be no clear version of hello KEK outside hello HSMs.</span></span> <span data-ttu-id="ba604-124">En outre, ensemble d’outils hello inclut une attestation de Thales indiquant que hello n’est pas exportable et a été généré à l’intérieur d’un HSM authentique conçu par Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-124">In addition, hello toolset includes attestation from Thales that hello KEK is not exportable and was generated inside a genuine HSM that was manufactured by Thales.</span></span>
* <span data-ttu-id="ba604-125">ensemble d’outils Hello inclut une attestation de Thales indiquant que le coffre de clés Azure monde de sécurité a également été généré sur un module de sécurité matériel authentique conçu par Thales hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-125">hello toolset includes attestation from Thales that hello Azure Key Vault security world was also generated on a genuine HSM manufactured by Thales.</span></span> <span data-ttu-id="ba604-126">Cette attestation s’avère tooyou que Microsoft utilise du matériel authentique.</span><span class="sxs-lookup"><span data-stu-id="ba604-126">This attestation proves tooyou that Microsoft is using genuine hardware.</span></span>
* <span data-ttu-id="ba604-127">Microsoft utilise des KEK et des mondes de sécurité séparés dans chaque région géographique.</span><span class="sxs-lookup"><span data-stu-id="ba604-127">Microsoft uses separate KEKs and separate Security Worlds in each geographical region.</span></span> <span data-ttu-id="ba604-128">Cette séparation garantit que votre clé peut être utilisée uniquement dans les centres de données dans la région de hello dans lequel vous l’avez chiffrée.</span><span class="sxs-lookup"><span data-stu-id="ba604-128">This separation ensures that your key can be used only in data centers in hello region in which you encrypted it.</span></span> <span data-ttu-id="ba604-129">Par exemple, la clé d’un client européen ne peut pas être utilisée dans des centres de données d’Amérique du Nord ou d’ Asie.</span><span class="sxs-lookup"><span data-stu-id="ba604-129">For example, a key from a European customer cannot be used in data centers in North American or Asia.</span></span>

## <a name="more-information-about-thales-hsms-and-microsoft-services"></a><span data-ttu-id="ba604-130">Autres informations sur les services de sécurité matériels Thales et Microsoft</span><span class="sxs-lookup"><span data-stu-id="ba604-130">More information about Thales HSMs and Microsoft services</span></span>
<span data-ttu-id="ba604-131">Thales e-Security est des principaux fournisseurs mondiaux le chiffrement des données et des services financiers cyber sécurité solutions toohello haute technologie, fabrication, gouvernement et secteurs de la technologie.</span><span class="sxs-lookup"><span data-stu-id="ba604-131">Thales e-Security is a leading global provider of data encryption and cyber security solutions toohello financial services, high technology, manufacturing, government, and technology sectors.</span></span> <span data-ttu-id="ba604-132">Avec un 40 ans de protection et les gouvernements des informations, les solutions Thales sont utilisées par quatre hello cinq plus grandes aérospatial d’énergie et de sociétés de.</span><span class="sxs-lookup"><span data-stu-id="ba604-132">With a 40-year track record of protecting corporate and government information, Thales solutions are used by four of hello five largest energy and aerospace companies.</span></span> <span data-ttu-id="ba604-133">Leurs solutions sont également utilisées par 22 pays de l’OTAN, et sécurisent plus de 80 % des transactions de paiement dans le monde.</span><span class="sxs-lookup"><span data-stu-id="ba604-133">Their solutions are also used by 22 NATO countries, and secure more than 80 per cent of worldwide payment transactions.</span></span>

<span data-ttu-id="ba604-134">Microsoft a collaboré avec l’état de hello Thales tooenhance clipart modules de sécurité matériels.</span><span class="sxs-lookup"><span data-stu-id="ba604-134">Microsoft has collaborated with Thales tooenhance hello state of art for HSMs.</span></span> <span data-ttu-id="ba604-135">Ces améliorations permettent d’avantages de types hello tooget des services hébergés sans renoncer au contrôle de vos clés.</span><span class="sxs-lookup"><span data-stu-id="ba604-135">These enhancements enable you tooget hello typical benefits of hosted services without relinquishing control over your keys.</span></span> <span data-ttu-id="ba604-136">Plus précisément, ces améliorations permettent à Microsoft de gérer hello modules de sécurité matériels afin que vous n’avez pas à.</span><span class="sxs-lookup"><span data-stu-id="ba604-136">Specifically, these enhancements let Microsoft manage hello HSMs so that you do not have to.</span></span> <span data-ttu-id="ba604-137">Comme un cloud que service, Azure Key Vault passe à la mention abrégée toomeet pics se produisent l’utilisation de votre organisation.</span><span class="sxs-lookup"><span data-stu-id="ba604-137">As a cloud service, Azure Key Vault scales up at short notice toomeet your organization’s usage spikes.</span></span> <span data-ttu-id="ba604-138">AT hello même temps, votre clé est protégée à l’intérieur de Microsoft : vous conservez le contrôle hello son cycle de vie, car vous générez hello clé et la transférez HSM du tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="ba604-138">At hello same time, your key is protected inside Microsoft’s HSMs: You retain control over hello key lifecycle because you generate hello key and transfer it tooMicrosoft’s HSMs.</span></span>

## <a name="implementing-bring-your-own-key-byok-for-azure-key-vault"></a><span data-ttu-id="ba604-139">Mise en œuvre du principe BYOK (Apportez votre propre clé, pour le coffre de clés Azure</span><span class="sxs-lookup"><span data-stu-id="ba604-139">Implementing bring your own key (BYOK) for Azure Key Vault</span></span>
<span data-ttu-id="ba604-140">Hello d’utilisation suivante des informations et des procédures si vous allez générer votre propre clé protégée par HSM et transférez-le tooAzure le coffre de clés : hello apportez votre propre scénario key (BYOK).</span><span class="sxs-lookup"><span data-stu-id="ba604-140">Use hello following information and procedures if you will generate your own HSM-protected key and then transfer it tooAzure Key Vault—hello bring your own key (BYOK) scenario.</span></span>

## <a name="prerequisites-for-byok"></a><span data-ttu-id="ba604-141">Configuration requise pour BYOK</span><span class="sxs-lookup"><span data-stu-id="ba604-141">Prerequisites for BYOK</span></span>
<span data-ttu-id="ba604-142">Consultez hello tableau pour obtenir la liste des composants requis pour mettre votre propre key (BYOK) pour Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ba604-142">See hello following table for a list of prerequisites for bring your own key (BYOK) for Azure Key Vault.</span></span>

| <span data-ttu-id="ba604-143">Prérequis</span><span class="sxs-lookup"><span data-stu-id="ba604-143">Requirement</span></span> | <span data-ttu-id="ba604-144">Plus d’informations</span><span class="sxs-lookup"><span data-stu-id="ba604-144">More information</span></span> |
| --- | --- |
| <span data-ttu-id="ba604-145">Un abonnement tooAzure</span><span class="sxs-lookup"><span data-stu-id="ba604-145">A subscription tooAzure</span></span> |<span data-ttu-id="ba604-146">toocreate un coffre de clés Azure, vous avez besoin d’un abonnement Azure : [s’inscrire pour la version d’évaluation gratuite](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="ba604-146">toocreate an Azure Key Vault, you need an Azure subscription: [Sign up for free trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> |
| <span data-ttu-id="ba604-147">clés protégées par HSM Hello Azure Key Vault Premium service couche toosupport</span><span class="sxs-lookup"><span data-stu-id="ba604-147">hello Azure Key Vault Premium service tier toosupport HSM-protected keys</span></span> |<span data-ttu-id="ba604-148">Pour plus d’informations sur les fonctionnalités et les niveaux de service hello pour Azure Key Vault, consultez hello [tarification d’Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/) site Web.</span><span class="sxs-lookup"><span data-stu-id="ba604-148">For more information about hello service tiers and capabilities for Azure Key Vault, see hello [Azure Key Vault Pricing](https://azure.microsoft.com/pricing/details/key-vault/) website.</span></span> |
| <span data-ttu-id="ba604-149">Modules de sécurité matérielle, cartes à puces et logiciel d’assistance de Thales</span><span class="sxs-lookup"><span data-stu-id="ba604-149">Thales HSM, smartcards, and support software</span></span> |<span data-ttu-id="ba604-150">Vous devez avoir accès tooa Module de sécurité matériel Thales et opérationnelle notions de sécurité matériels Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-150">You must have access tooa Thales Hardware Security Module and basic operational knowledge of Thales HSMs.</span></span> <span data-ttu-id="ba604-151">Consultez [Module de sécurité matériel Thales](https://www.thales-esecurity.com/msrms/buy) pour la liste des modèles compatibles ou toopurchase un HSM si vous n’avez pas un hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-151">See [Thales Hardware Security Module](https://www.thales-esecurity.com/msrms/buy) for hello list of compatible models, or toopurchase an HSM if you do not have one.</span></span> |
| <span data-ttu-id="ba604-152">Hello matériel et logiciels suivants :</span><span class="sxs-lookup"><span data-stu-id="ba604-152">hello following hardware and software:</span></span><ol><li><span data-ttu-id="ba604-153">Une station de travail x64 hors connexion avec le système d’exploitation Windows 7 ou version ultérieure, et le logiciel Thales nShield version 11.50 ou ultérieure.</span><span class="sxs-lookup"><span data-stu-id="ba604-153">An offline x64 workstation with a minimum Windows operation system of Windows 7 and Thales nShield software that is at least version 11.50.</span></span><br/><br/><span data-ttu-id="ba604-154">Si cette station de travail exécute Windows 7, vous devez [installer Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span><span class="sxs-lookup"><span data-stu-id="ba604-154">If this workstation runs Windows 7, you must [install Microsoft .NET Framework 4.5](http://download.microsoft.com/download/b/a/4/ba4a7e71-2906-4b2d-a0e1-80cf16844f5f/dotnetfx45_full_x86_x64.exe).</span></span></li><li><span data-ttu-id="ba604-155">Une station de travail qui est connecté toohello Internet et possède un système d’exploitation Windows minimal de Windows 7 et [Azure PowerShell](/powershell/azure/overview) **minimale version 1.1.0** installé.</span><span class="sxs-lookup"><span data-stu-id="ba604-155">A workstation that is connected toohello Internet and has a minimum Windows operating system of Windows 7 and [Azure PowerShell](/powershell/azure/overview) **minimum version 1.1.0** installed.</span></span></li><li><span data-ttu-id="ba604-156">Un lecteur USB ou tout autre appareil de stockage portable offrant au moins 16 Mo d’espace libre.</span><span class="sxs-lookup"><span data-stu-id="ba604-156">A USB drive or other portable storage device that has at least 16 MB free space.</span></span></li></ol> |<span data-ttu-id="ba604-157">Pour des raisons de sécurité, nous vous recommandons de que cette première station de travail hello n’est pas connecté tooa réseau.</span><span class="sxs-lookup"><span data-stu-id="ba604-157">For security reasons, we recommend that hello first workstation is not connected tooa network.</span></span> <span data-ttu-id="ba604-158">Toutefois, cette recommandation n’est pas appliquée par programmation.</span><span class="sxs-lookup"><span data-stu-id="ba604-158">However, this recommendation is not programmatically enforced.</span></span><br/><br/><span data-ttu-id="ba604-159">Notez que dans les instructions hello ci-après, cette station de travail est désignée tooas hello déconnecté station de travail.</span><span class="sxs-lookup"><span data-stu-id="ba604-159">Note that in hello instructions that follow, this workstation is referred tooas hello disconnected workstation.</span></span></p></blockquote><br/><span data-ttu-id="ba604-160">En outre, si votre clé de locataire est pour un réseau de production, nous vous recommandons d’utiliser un deuxième poste de travail toodownload hello ensemble d’outils et de téléchargement hello clé de locataire.</span><span class="sxs-lookup"><span data-stu-id="ba604-160">In addition, if your tenant key is for a production network, we recommend that you use a second, separate workstation toodownload hello toolset and upload hello tenant key.</span></span> <span data-ttu-id="ba604-161">Mais à des fins de test, vous pouvez utiliser hello même station de travail comme hello premier.</span><span class="sxs-lookup"><span data-stu-id="ba604-161">But for testing purposes, you can use hello same workstation as hello first one.</span></span><br/><br/><span data-ttu-id="ba604-162">Notez que dans les instructions hello ci-après, cette deuxième station de travail est station de travail référencé tooas hello connecté à Internet.</span><span class="sxs-lookup"><span data-stu-id="ba604-162">Note that in hello instructions that follow, this second workstation is referred tooas hello Internet-connected workstation.</span></span></p></blockquote><br/> |

## <a name="generate-and-transfer-your-key-tooazure-key-vault-hsm"></a><span data-ttu-id="ba604-163">Générer et transférer votre clé tooAzure HSM pour coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ba604-163">Generate and transfer your key tooAzure Key Vault HSM</span></span>
<span data-ttu-id="ba604-164">Vous allez utiliser hello suivant cinq étapes toogenerate et transférer votre clé tooan HSM pour coffre de clés Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-164">You will use hello following five steps toogenerate and transfer your key tooan Azure Key Vault HSM:</span></span>

* [<span data-ttu-id="ba604-165">Étape 1 : Préparez votre station de travail connectée à Internet</span><span class="sxs-lookup"><span data-stu-id="ba604-165">Step 1: Prepare your Internet-connected workstation</span></span>](#step-1-prepare-your-internet-connected-workstation)
* [<span data-ttu-id="ba604-166">Étape 2 : Préparez votre station de travail déconnectée</span><span class="sxs-lookup"><span data-stu-id="ba604-166">Step 2: Prepare your disconnected workstation</span></span>](#step-2-prepare-your-disconnected-workstation)
* [<span data-ttu-id="ba604-167">Étape 3 : Générez votre clé</span><span class="sxs-lookup"><span data-stu-id="ba604-167">Step 3: Generate your key</span></span>](#step-3-generate-your-key)
* [<span data-ttu-id="ba604-168">Étape 4 : Réparez votre clé pour le transfert</span><span class="sxs-lookup"><span data-stu-id="ba604-168">Step 4: Prepare your key for transfer</span></span>](#step-4-prepare-your-key-for-transfer)
* [<span data-ttu-id="ba604-169">Étape 5 : Transférer votre clé tooAzure le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ba604-169">Step 5: Transfer your key tooAzure Key Vault</span></span>](#step-5-transfer-your-key-to-azure-key-vault)

## <a name="step-1-prepare-your-internet-connected-workstation"></a><span data-ttu-id="ba604-170">Étape 1 : Préparez votre station de travail connectée à Internet</span><span class="sxs-lookup"><span data-stu-id="ba604-170">Step 1: Prepare your Internet-connected workstation</span></span>
<span data-ttu-id="ba604-171">Pour cette première étape, hello procédures suivantes sur votre station de travail qui est connecté toohello Internet.</span><span class="sxs-lookup"><span data-stu-id="ba604-171">For this first step, do hello following procedures on your workstation that is connected toohello Internet.</span></span>

### <a name="step-11-install-azure-powershell"></a><span data-ttu-id="ba604-172">Étape 1.1 : installer Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ba604-172">Step 1.1: Install Azure PowerShell</span></span>
<span data-ttu-id="ba604-173">À partir de hello Internet station de travail connectée, téléchargez et installez les module PowerShell Azure hello qui inclut des applets de commande de hello toomanage Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ba604-173">From hello Internet-connected workstation, download and install hello Azure PowerShell module that includes hello cmdlets toomanage Azure Key Vault.</span></span> <span data-ttu-id="ba604-174">Cela nécessite au moins la version 0.8.13.</span><span class="sxs-lookup"><span data-stu-id="ba604-174">This requires a minimum version of 0.8.13.</span></span>

<span data-ttu-id="ba604-175">Pour obtenir des instructions d’installation, consultez [comment tooinstall et configurer Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ba604-175">For installation instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

### <a name="step-12-get-your-azure-subscription-id"></a><span data-ttu-id="ba604-176">Étape 1.2 : Obtenez votre ID d’abonnement Azure.</span><span class="sxs-lookup"><span data-stu-id="ba604-176">Step 1.2: Get your Azure subscription ID</span></span>
<span data-ttu-id="ba604-177">Démarrez une session Azure PowerShell et connectez-vous tooyour compte Azure à l’aide de hello de commande suivante :</span><span class="sxs-lookup"><span data-stu-id="ba604-177">Start an Azure PowerShell session and sign in tooyour Azure account by using hello following command:</span></span>

        Add-AzureAccount
<span data-ttu-id="ba604-178">Dans la fenêtre contextuelle du navigateur de hello, entrez votre nom d’utilisateur de compte Azure et un mot de passe.</span><span class="sxs-lookup"><span data-stu-id="ba604-178">In hello pop-up browser window, enter your Azure account user name and password.</span></span> <span data-ttu-id="ba604-179">Ensuite, utilisez hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) commande :</span><span class="sxs-lookup"><span data-stu-id="ba604-179">Then, use hello [Get-AzureSubscription](/powershell/module/azure/get-azuresubscription?view=azuresmps-3.7.0) command:</span></span>

        Get-AzureSubscription
<span data-ttu-id="ba604-180">À partir de la sortie de hello, recherchez les ID de hello pour l’abonnement hello que vous utiliserez pour Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ba604-180">From hello output, locate hello ID for hello subscription you will use for Azure Key Vault.</span></span> <span data-ttu-id="ba604-181">Vous aurez besoin cet ID d’abonnement ultérieurement.</span><span class="sxs-lookup"><span data-stu-id="ba604-181">You will need this subscription ID later.</span></span>

<span data-ttu-id="ba604-182">Ne fermez pas la fenêtre d’Azure PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-182">Do not close hello Azure PowerShell window.</span></span>

### <a name="step-13-download-hello-byok-toolset-for-azure-key-vault"></a><span data-ttu-id="ba604-183">Étape 1.3 : Télécharger un ensemble d’outils BYOK de hello pour Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="ba604-183">Step 1.3: Download hello BYOK toolset for Azure Key Vault</span></span>
<span data-ttu-id="ba604-184">Accédez toohello Microsoft Download Center et [télécharger l’ensemble d’outils de la solution BYOK d’Azure Key Vault hello](http://www.microsoft.com/download/details.aspx?id=45345) pour votre instance Azure ou une région géographique.</span><span class="sxs-lookup"><span data-stu-id="ba604-184">Go toohello Microsoft Download Center and [download hello Azure Key Vault BYOK toolset](http://www.microsoft.com/download/details.aspx?id=45345) for your geographic region or instance of Azure.</span></span> <span data-ttu-id="ba604-185">Utilisez hello suit hachage du package toodownload de nom package informations tooidentify hello et son SHA-256 correspondante :</span><span class="sxs-lookup"><span data-stu-id="ba604-185">Use hello following information tooidentify hello package name toodownload and its corresponding SHA-256 package hash:</span></span>

- - -
<span data-ttu-id="ba604-186">**États-Unis**</span><span class="sxs-lookup"><span data-stu-id="ba604-186">**United States:**</span></span>

<span data-ttu-id="ba604-187">KeyVault-BYOK-Tools-UnitedStates.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-187">KeyVault-BYOK-Tools-UnitedStates.zip</span></span>

<span data-ttu-id="ba604-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span><span class="sxs-lookup"><span data-stu-id="ba604-188">760EE9BD6445C87CFF0E8B032577118704B3BEAA045AA55977C10EF68BC67E2B</span></span>

- - -
<span data-ttu-id="ba604-189">**Europe :**</span><span class="sxs-lookup"><span data-stu-id="ba604-189">**Europe:**</span></span>

<span data-ttu-id="ba604-190">KeyVault-BYOK-outils-Europe.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-190">KeyVault-BYOK-Tools-Europe.zip</span></span>

<span data-ttu-id="ba604-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span><span class="sxs-lookup"><span data-stu-id="ba604-191">7A64B94225F59B847C5C27C2200BAD7D16C901E1687767EDBBB8B09BB285011D</span></span>

- - -
<span data-ttu-id="ba604-192">**Asie :**</span><span class="sxs-lookup"><span data-stu-id="ba604-192">**Asia:**</span></span>

<span data-ttu-id="ba604-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-193">KeyVault-BYOK-Tools-AsiaPacific.zip</span></span>

<span data-ttu-id="ba604-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span><span class="sxs-lookup"><span data-stu-id="ba604-194">813DC94B23079CF7A5CEA71D5B444E86B292F463C53EE47AED25D4F7CD58E7D8</span></span>

- - -
<span data-ttu-id="ba604-195">**Amérique latine :**</span><span class="sxs-lookup"><span data-stu-id="ba604-195">**Latin America:**</span></span>

<span data-ttu-id="ba604-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-196">KeyVault-BYOK-Tools-LatinAmerica.zip</span></span>

<span data-ttu-id="ba604-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span><span class="sxs-lookup"><span data-stu-id="ba604-197">3F29069E3500F95C0E156F4B8914E1DC60C20FB64B464306A299EA5145D755C0</span></span>

- - -
<span data-ttu-id="ba604-198">**Japon :**</span><span class="sxs-lookup"><span data-stu-id="ba604-198">**Japan:**</span></span>

<span data-ttu-id="ba604-199">KeyVault-BYOK-Tools-Japan.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-199">KeyVault-BYOK-Tools-Japan.zip</span></span>

<span data-ttu-id="ba604-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span><span class="sxs-lookup"><span data-stu-id="ba604-200">453FFEA2F8F410720B68B8BAC4CF79135A7F37F4E491FF840BE9E69E88A98C90</span></span>

- - -
<span data-ttu-id="ba604-201">**Corée :**</span><span class="sxs-lookup"><span data-stu-id="ba604-201">**Korea:**</span></span>

<span data-ttu-id="ba604-202">KeyVault-BYOK-Tools-Korea.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-202">KeyVault-BYOK-Tools-Korea.zip</span></span>

<span data-ttu-id="ba604-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span><span class="sxs-lookup"><span data-stu-id="ba604-203">C17B7E93224DA80F5668E09CF7DAE2F92527E8226179995BBE2E43DA4323595A</span></span>

- - -
<span data-ttu-id="ba604-204">**Australie :**</span><span class="sxs-lookup"><span data-stu-id="ba604-204">**Australia:**</span></span>

<span data-ttu-id="ba604-205">KeyVault-BYOK-Tools-Australia.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-205">KeyVault-BYOK-Tools-Australia.zip</span></span>

<span data-ttu-id="ba604-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span><span class="sxs-lookup"><span data-stu-id="ba604-206">4AD893396E86F2D2A71682876A6A8EA59E3C7895BEAD2F7E7C8516682582C34B</span></span>

- - -
[<span data-ttu-id="ba604-207">**Azure Government :**</span><span class="sxs-lookup"><span data-stu-id="ba604-207">**Azure Government:**</span></span>](https://azure.microsoft.com/features/gov/)

<span data-ttu-id="ba604-208">KeyVault-BYOK-Tools-USGovCloud.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-208">KeyVault-BYOK-Tools-USGovCloud.zip</span></span>

<span data-ttu-id="ba604-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span><span class="sxs-lookup"><span data-stu-id="ba604-209">3AAE1A96B9D15B899B8126CFC0380719EB54FDF2EA94489B43FAD21ECC745F64</span></span>

- - -
<span data-ttu-id="ba604-210">**Département de la Défense des États-Unis :**</span><span class="sxs-lookup"><span data-stu-id="ba604-210">**US Government DOD:**</span></span>

<span data-ttu-id="ba604-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-211">KeyVault-BYOK-Tools-USGovernmentDoD.zip</span></span>

<span data-ttu-id="ba604-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span><span class="sxs-lookup"><span data-stu-id="ba604-212">A61E78297B0732DF2682FDE63D7B572CE4D23B0BC27CC48AFF620BD060BB9E9D</span></span>

- - -
<span data-ttu-id="ba604-213">**Canada :**</span><span class="sxs-lookup"><span data-stu-id="ba604-213">**Canada:**</span></span>

<span data-ttu-id="ba604-214">KeyVault-BYOK-Tools-Canada.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-214">KeyVault-BYOK-Tools-Canada.zip</span></span>

<span data-ttu-id="ba604-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span><span class="sxs-lookup"><span data-stu-id="ba604-215">30B87A0BA8208F6B7241C30C794FED1C370D7445ACA179685816E4E156CD2AF7</span></span>

- - -
<span data-ttu-id="ba604-216">**Allemagne :**</span><span class="sxs-lookup"><span data-stu-id="ba604-216">**Germany:**</span></span>

<span data-ttu-id="ba604-217">KeyVault-BYOK-Tools-Germany.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-217">KeyVault-BYOK-Tools-Germany.zip</span></span>

<span data-ttu-id="ba604-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span><span class="sxs-lookup"><span data-stu-id="ba604-218">5E3E4AA54715E4F93C3C145035B18275B7C6815A06D7ABB212E7FADBF2929261</span></span>

- - -
<span data-ttu-id="ba604-219">**Inde :**</span><span class="sxs-lookup"><span data-stu-id="ba604-219">**India:**</span></span>

<span data-ttu-id="ba604-220">KeyVault-BYOK-Tools-India.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-220">KeyVault-BYOK-Tools-India.zip</span></span>

<span data-ttu-id="ba604-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span><span class="sxs-lookup"><span data-stu-id="ba604-221">136733A6C6A71D75571BB80819B3D55A9B83CCAD5C996C686BC5682A3F369BF7</span></span>

- - -
<span data-ttu-id="ba604-222">**Royaume-Uni :**</span><span class="sxs-lookup"><span data-stu-id="ba604-222">**United Kingdom:**</span></span>

<span data-ttu-id="ba604-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span><span class="sxs-lookup"><span data-stu-id="ba604-223">KeyVault-BYOK-Tools-UnitedKingdom.zip</span></span>

<span data-ttu-id="ba604-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span><span class="sxs-lookup"><span data-stu-id="ba604-224">ED331A6F1D34A402317D3F27D5396046AF0E5C2D44B5D10CCCE293472942D268</span></span>

- - -

<span data-ttu-id="ba604-225">l’intégrité de hello toovalidate de votre d’outils BYOK téléchargé, à partir de votre session Azure PowerShell, utilisez hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) applet de commande.</span><span class="sxs-lookup"><span data-stu-id="ba604-225">toovalidate hello integrity of your downloaded BYOK toolset, from your Azure PowerShell session, use hello [Get-FileHash](https://technet.microsoft.com/library/dn520872.aspx) cmdlet.</span></span>

    Get-FileHash KeyVault-BYOK-Tools-*.zip

<span data-ttu-id="ba604-226">ensemble d’outils Hello inclut des éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="ba604-226">hello toolset includes hello following:</span></span>

* <span data-ttu-id="ba604-227">Un package Key Exchange Key (KEK) dont le nom commence par **BYOK-KEK-pkg-**</span><span class="sxs-lookup"><span data-stu-id="ba604-227">A Key Exchange Key (KEK) package that has a name beginning with **BYOK-KEK-pkg-.**</span></span>
* <span data-ttu-id="ba604-228">Un package Security World dont le nom commence par **BYOK-SecurityWorld-pkg-**</span><span class="sxs-lookup"><span data-stu-id="ba604-228">A Security World package that has a name beginning with **BYOK-SecurityWorld-pkg-.**</span></span>
* <span data-ttu-id="ba604-229">Un script python nommé **verifykeypackage.py**.</span><span class="sxs-lookup"><span data-stu-id="ba604-229">A python script named **verifykeypackage.py.**</span></span>
* <span data-ttu-id="ba604-230">Un fichier exécutable de ligne de commande nommé **KeyTransferRemote.exe** et les DLL associées.</span><span class="sxs-lookup"><span data-stu-id="ba604-230">A command-line executable file named **KeyTransferRemote.exe** and associated DLLs.</span></span>
* <span data-ttu-id="ba604-231">Un package redistribuable Visual C++ nommé **vcredist_x64.exe**.</span><span class="sxs-lookup"><span data-stu-id="ba604-231">A Visual C++ Redistributable Package, named **vcredist_x64.exe.**</span></span>

<span data-ttu-id="ba604-232">Copiez hello package tooa USB ou un autre support de stockage portable.</span><span class="sxs-lookup"><span data-stu-id="ba604-232">Copy hello package tooa USB drive or other portable storage.</span></span>

## <a name="step-2-prepare-your-disconnected-workstation"></a><span data-ttu-id="ba604-233">Étape 2 : Préparez votre station de travail déconnectée</span><span class="sxs-lookup"><span data-stu-id="ba604-233">Step 2: Prepare your disconnected workstation</span></span>
<span data-ttu-id="ba604-234">Pour cette deuxième étape, hello suivant les procédures de station de travail hello qui n’est pas connecté tooa réseau (hello Internet ou votre réseau interne).</span><span class="sxs-lookup"><span data-stu-id="ba604-234">For this second step, do hello following procedures on hello workstation that is not connected tooa network (either hello Internet or your internal network).</span></span>

### <a name="step-21-prepare-hello-disconnected-workstation-with-thales-hsm"></a><span data-ttu-id="ba604-235">Étape 2.1 : Préparer la station de travail hello déconnecté de sécurité matériel Thales</span><span class="sxs-lookup"><span data-stu-id="ba604-235">Step 2.1: Prepare hello disconnected workstation with Thales HSM</span></span>
<span data-ttu-id="ba604-236">Installer le logiciel de support nCipher (Thales) hello sur un ordinateur Windows, puis joignez un ordinateur toothat de sécurité matériel Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-236">Install hello nCipher (Thales) support software on a Windows computer, and then attach a Thales HSM toothat computer.</span></span>

<span data-ttu-id="ba604-237">Assurez-vous que hello des outils Thales se trouvent dans votre chemin d’accès (**%nfast_home%\bin**).</span><span class="sxs-lookup"><span data-stu-id="ba604-237">Ensure that hello Thales tools are in your path (**%nfast_home%\bin**).</span></span> <span data-ttu-id="ba604-238">Par exemple, tapez Bonjour suivante :</span><span class="sxs-lookup"><span data-stu-id="ba604-238">For example, type hello following:</span></span>

        set PATH=%PATH%;"%nfast_home%\bin"

<span data-ttu-id="ba604-239">Pour plus d’informations, consultez hello Guide d’utilisation inclus avec hello HSM Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-239">For more information, see hello user guide included with hello Thales HSM.</span></span>

### <a name="step-22-install-hello-byok-toolset-on-hello-disconnected-workstation"></a><span data-ttu-id="ba604-240">Étape 2.2 : Ensemble d’outils installation hello BYOK sur la station de travail hello déconnecté</span><span class="sxs-lookup"><span data-stu-id="ba604-240">Step 2.2: Install hello BYOK toolset on hello disconnected workstation</span></span>
<span data-ttu-id="ba604-241">Copier le package de l’ensemble d’outils BYOK hello de hello USB ou un autre support de stockage portable, puis hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ba604-241">Copy hello BYOK toolset package from hello USB drive or other portable storage, and then do hello following:</span></span>

1. <span data-ttu-id="ba604-242">Extrayez les fichiers de hello hello téléchargé package dans n’importe quel dossier.</span><span class="sxs-lookup"><span data-stu-id="ba604-242">Extract hello files from hello downloaded package into any folder.</span></span>
2. <span data-ttu-id="ba604-243">Depuis ce dossier, exécutez vcredist_x64.exe.</span><span class="sxs-lookup"><span data-stu-id="ba604-243">From that folder, run vcredist_x64.exe.</span></span>
3. <span data-ttu-id="ba604-244">Suivez les instructions de hello toohello installer les composants d’exécution hello Visual C++ pour Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="ba604-244">Follow hello instructions toohello install hello Visual C++ runtime components for Visual Studio 2013.</span></span>

## <a name="step-3-generate-your-key"></a><span data-ttu-id="ba604-245">Étape 3 : Générez votre clé</span><span class="sxs-lookup"><span data-stu-id="ba604-245">Step 3: Generate your key</span></span>
<span data-ttu-id="ba604-246">Pour cette troisième étape, hello suivant les procédures de station de travail hello déconnecté.</span><span class="sxs-lookup"><span data-stu-id="ba604-246">For this third step, do hello following procedures on hello disconnected workstation.</span></span> <span data-ttu-id="ba604-247">toocomplete cette étape de votre module de sécurité matériel doit être en mode d’initialisation.</span><span class="sxs-lookup"><span data-stu-id="ba604-247">toocomplete this step your HSM must be in initialization mode.</span></span> 


### <a name="step-31-change-hello-hsm-mode-tooi"></a><span data-ttu-id="ba604-248">Étape 3.1 : Modifier hello HSM mode too'I'</span><span class="sxs-lookup"><span data-stu-id="ba604-248">Step 3.1: Change hello HSM mode too'I'</span></span>
<span data-ttu-id="ba604-249">Si vous utilisez Thales nShield Edge, le mode hello toochange : 1.</span><span class="sxs-lookup"><span data-stu-id="ba604-249">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="ba604-250">Utilisez hello Mode bouton toohighlight hello mode requis.</span><span class="sxs-lookup"><span data-stu-id="ba604-250">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="ba604-251">2.</span><span class="sxs-lookup"><span data-stu-id="ba604-251">2.</span></span> <span data-ttu-id="ba604-252">Après quelques secondes, maintenez effacer hello pendant quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="ba604-252">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="ba604-253">Si la modification du mode de hello, hello DEL du nouveau mode cesse de clignoter et reste allumé.</span><span class="sxs-lookup"><span data-stu-id="ba604-253">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="ba604-254">Hello voyant d’état peut flash irrégulière pendant quelques secondes et puis clignote régulièrement lorsque le périphérique de hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="ba604-254">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="ba604-255">Dans le cas contraire, hello périphérique reste dans le mode actuel hello, avec le mode approprié hello voyant allumé.</span><span class="sxs-lookup"><span data-stu-id="ba604-255">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>

### <a name="step-32-create-a-security-world"></a><span data-ttu-id="ba604-256">Étape 3.2 : Créez un monde de sécurité</span><span class="sxs-lookup"><span data-stu-id="ba604-256">Step 3.2: Create a security world</span></span>
<span data-ttu-id="ba604-257">Démarrez une invite de commandes et exécutez hello programme de nouveau monde Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-257">Start a command prompt and run hello Thales new-world program.</span></span>

    new-world.exe --initialize --cipher-suite=DLf1024s160mRijndael --module=1 --acs-quorum=2/3

<span data-ttu-id="ba604-258">Ce programme crée un **Security World** fichier % NFAST_KMDATA%\local\world, qui correspond toohello c:\programdata\ncipher\key Management C:\ProgramData\nCipher\Key dossier.</span><span class="sxs-lookup"><span data-stu-id="ba604-258">This program creates a **Security World** file at %NFAST_KMDATA%\local\world, which corresponds toohello C:\ProgramData\nCipher\Key Management Data\local folder.</span></span> <span data-ttu-id="ba604-259">Vous pouvez utiliser des valeurs différentes pour le quorum de hello, mais dans notre exemple, vous êtes tooenter demandées trois cartes et nuls pour chacun d’eux des codes confidentiels.</span><span class="sxs-lookup"><span data-stu-id="ba604-259">You can use different values for hello quorum but in our example, you’re prompted tooenter three blank cards and pins for each one.</span></span> <span data-ttu-id="ba604-260">Ensuite, deux des trois cartes donnent monde de sécurité toohello un accès complet.</span><span class="sxs-lookup"><span data-stu-id="ba604-260">Then, any two cards give full access toohello security world.</span></span> <span data-ttu-id="ba604-261">Ces cartes constituent hello **ensemble de cartes administrateur** nouveau monde de sécurité hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-261">These cards become hello **Administrator Card Set** for hello new security world.</span></span>

<span data-ttu-id="ba604-262">Puis la hello suivant :</span><span class="sxs-lookup"><span data-stu-id="ba604-262">Then do hello following:</span></span>

* <span data-ttu-id="ba604-263">Sauvegardez le fichier de hello world.</span><span class="sxs-lookup"><span data-stu-id="ba604-263">Back up hello world file.</span></span> <span data-ttu-id="ba604-264">Sécuriser et protéger le fichier de hello world, les cartes administrateur hello et leurs codes confidentiels et assurez-vous ne qu’aucune personne seule toomore d’accès à une carte.</span><span class="sxs-lookup"><span data-stu-id="ba604-264">Secure and protect hello world file, hello Administrator Cards, and their pins, and make sure that no single person has access toomore than one card.</span></span>

### <a name="step-33-change-hello-hsm-mode-tooo"></a><span data-ttu-id="ba604-265">Étape 3.3 : Modifier hello HSM mode too'O'</span><span class="sxs-lookup"><span data-stu-id="ba604-265">Step 3.3: Change hello HSM mode too'O'</span></span>
<span data-ttu-id="ba604-266">Si vous utilisez Thales nShield Edge, le mode hello toochange : 1.</span><span class="sxs-lookup"><span data-stu-id="ba604-266">If you are using Thales nShield Edge, toochange hello mode: 1.</span></span> <span data-ttu-id="ba604-267">Utilisez hello Mode bouton toohighlight hello mode requis.</span><span class="sxs-lookup"><span data-stu-id="ba604-267">Use hello Mode button toohighlight hello required mode.</span></span> <span data-ttu-id="ba604-268">2.</span><span class="sxs-lookup"><span data-stu-id="ba604-268">2.</span></span> <span data-ttu-id="ba604-269">Après quelques secondes, maintenez effacer hello pendant quelques secondes.</span><span class="sxs-lookup"><span data-stu-id="ba604-269">Within a few seconds, press and hold hello Clear button for a couple of seconds.</span></span> <span data-ttu-id="ba604-270">Si la modification du mode de hello, hello DEL du nouveau mode cesse de clignoter et reste allumé.</span><span class="sxs-lookup"><span data-stu-id="ba604-270">If hello mode changes, hello new mode’s LED stops flashing and remains lit.</span></span> <span data-ttu-id="ba604-271">Hello voyant d’état peut flash irrégulière pendant quelques secondes et puis clignote régulièrement lorsque le périphérique de hello est prêt.</span><span class="sxs-lookup"><span data-stu-id="ba604-271">hello Status LED might flash irregularly for a few seconds and then flashes regularly when hello device is ready.</span></span> <span data-ttu-id="ba604-272">Dans le cas contraire, hello périphérique reste dans le mode actuel hello, avec le mode approprié hello voyant allumé.</span><span class="sxs-lookup"><span data-stu-id="ba604-272">Otherwise, hello device remains in hello current mode, with hello appropriate mode LED lit.</span></span>


### <a name="step-34-validate-hello-downloaded-package"></a><span data-ttu-id="ba604-273">Étape 3.4 : Valider le package de hello téléchargé</span><span class="sxs-lookup"><span data-stu-id="ba604-273">Step 3.4: Validate hello downloaded package</span></span>
<span data-ttu-id="ba604-274">Cette étape est facultative mais recommandée afin que vous pouvez valider les éléments suivants de hello :</span><span class="sxs-lookup"><span data-stu-id="ba604-274">This step is optional but recommended so that you can validate hello following:</span></span>

* <span data-ttu-id="ba604-275">Hello clé d’échange de clés qui est inclus dans l’ensemble d’outils hello a été généré à partir d’un HSM Thales authentique.</span><span class="sxs-lookup"><span data-stu-id="ba604-275">hello Key Exchange Key that is included in hello toolset has been generated from a genuine Thales HSM.</span></span>
* <span data-ttu-id="ba604-276">hachage Hello Hello World de sécurité qui est inclus dans l’ensemble d’outils hello a été généré dans un HSM Thales authentique.</span><span class="sxs-lookup"><span data-stu-id="ba604-276">hello hash of hello Security World that is included in hello toolset has been generated in a genuine Thales HSM.</span></span>
* <span data-ttu-id="ba604-277">Hello clé d’échange n’est pas exportable.</span><span class="sxs-lookup"><span data-stu-id="ba604-277">hello Key Exchange Key is non-exportable.</span></span>

> [!NOTE]
> <span data-ttu-id="ba604-278">toovalidate hello téléchargé le package, hello HSM doit être connectée, sous tension et doit avoir un monde de sécurité (par exemple hello une que vous avez créé).</span><span class="sxs-lookup"><span data-stu-id="ba604-278">toovalidate hello downloaded package, hello HSM must be connected, powered on, and must have a security world on it (such as hello one you’ve just created).</span></span>
>
>

<span data-ttu-id="ba604-279">toovalidate hello téléchargé package :</span><span class="sxs-lookup"><span data-stu-id="ba604-279">toovalidate hello downloaded package:</span></span>

1. <span data-ttu-id="ba604-280">Exécutez hello script verifykeypackage.py en tapant hello suivantes, selon votre région géographique ou d’une instance d’Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-280">Run hello verifykeypackage.py script by typing one of hello following, depending on your geographic region or instance of Azure:</span></span>

   * <span data-ttu-id="ba604-281">Pour l’Amérique du Nord :</span><span class="sxs-lookup"><span data-stu-id="ba604-281">For North America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-NA-1 -w BYOK-SecurityWorld-pkg-NA-1
   * <span data-ttu-id="ba604-282">Pour l’Europe :</span><span class="sxs-lookup"><span data-stu-id="ba604-282">For Europe:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-EU-1 -w BYOK-SecurityWorld-pkg-EU-1
   * <span data-ttu-id="ba604-283">Pour l’Asie :</span><span class="sxs-lookup"><span data-stu-id="ba604-283">For Asia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AP-1 -w BYOK-SecurityWorld-pkg-AP-1
   * <span data-ttu-id="ba604-284">Pour l’Amérique latine :</span><span class="sxs-lookup"><span data-stu-id="ba604-284">For Latin America:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-LATAM-1 -w BYOK-SecurityWorld-pkg-LATAM-1
   * <span data-ttu-id="ba604-285">Pour le Japon :</span><span class="sxs-lookup"><span data-stu-id="ba604-285">For Japan:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-JPN-1 -w BYOK-SecurityWorld-pkg-JPN-1
   * <span data-ttu-id="ba604-286">Pour la Corée :</span><span class="sxs-lookup"><span data-stu-id="ba604-286">For Korea:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-KOREA-1 -w BYOK-SecurityWorld-pkg-KOREA-1
   * <span data-ttu-id="ba604-287">Pour l’Australie :</span><span class="sxs-lookup"><span data-stu-id="ba604-287">For Australia:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-AUS-1 -w BYOK-SecurityWorld-pkg-AUS-1
   * <span data-ttu-id="ba604-288">Pour [Azure Government](https://azure.microsoft.com/features/gov/), qui utilise l’instance hello US government Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-288">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USGOV-1 -w BYOK-SecurityWorld-pkg-USGOV-1
   * <span data-ttu-id="ba604-289">Pour le Département de la Défense des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="ba604-289">For US Government DOD:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-USDOD-1 -w BYOK-SecurityWorld-pkg-USDOD-1
   * <span data-ttu-id="ba604-290">Pour le Canada :</span><span class="sxs-lookup"><span data-stu-id="ba604-290">For Canada:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-CANADA-1 -w BYOK-SecurityWorld-pkg-CANADA-1
   * <span data-ttu-id="ba604-291">Pour l’Allemagne :</span><span class="sxs-lookup"><span data-stu-id="ba604-291">For Germany:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-GERMANY-1 -w BYOK-SecurityWorld-pkg-GERMANY-1
   * <span data-ttu-id="ba604-292">Pour l’Inde :</span><span class="sxs-lookup"><span data-stu-id="ba604-292">For India:</span></span>

         "%nfast_home%\python\bin\python" verifykeypackage.py -k BYOK-KEK-pkg-INDIA-1 -w BYOK-SecurityWorld-pkg-INDIA-1
     > [!TIP]
     > <span data-ttu-id="ba604-293">Hello logiciel Thales inclut python à %NFAST_HOME%\python\bin</span><span class="sxs-lookup"><span data-stu-id="ba604-293">hello Thales software includes python at %NFAST_HOME%\python\bin</span></span>
     >
     >
2. <span data-ttu-id="ba604-294">Vérifiez que vous voyez suivants de hello, qui indiquent une validation réussie : **résultat : réussite**</span><span class="sxs-lookup"><span data-stu-id="ba604-294">Confirm that you see hello following, which indicates successful validation: **Result: SUCCESS**</span></span>

<span data-ttu-id="ba604-295">Ce script valide la chaîne de signataire hello des toohello clé racine Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-295">This script validates hello signer chain up toohello Thales root key.</span></span> <span data-ttu-id="ba604-296">hachage Hello de cette clé racine est incorporé dans le script de hello et sa valeur doit être **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span><span class="sxs-lookup"><span data-stu-id="ba604-296">hello hash of this root key is embedded in hello script and its value should be **59178a47 de508c3f 291277ee 184f46c4 f1d9c639**.</span></span> <span data-ttu-id="ba604-297">Vous pouvez également confirmer cette valeur séparément en visitant hello [site Web de Thales](http://www.thalesesec.com/).</span><span class="sxs-lookup"><span data-stu-id="ba604-297">You can also confirm this value separately by visiting hello [Thales website](http://www.thalesesec.com/).</span></span>

<span data-ttu-id="ba604-298">Vous êtes maintenant prêt toocreate une nouvelle clé.</span><span class="sxs-lookup"><span data-stu-id="ba604-298">You’re now ready toocreate a new key.</span></span>

### <a name="step-35-create-a-new-key"></a><span data-ttu-id="ba604-299">Étape 3.5 : Créez une clé</span><span class="sxs-lookup"><span data-stu-id="ba604-299">Step 3.5: Create a new key</span></span>
<span data-ttu-id="ba604-300">Générer une clé à l’aide de hello Thales **generatekey** programme.</span><span class="sxs-lookup"><span data-stu-id="ba604-300">Generate a key by using hello Thales **generatekey** program.</span></span>

<span data-ttu-id="ba604-301">Exécutez hello commande toogenerate hello clé suivante :</span><span class="sxs-lookup"><span data-stu-id="ba604-301">Run hello following command toogenerate hello key:</span></span>

    generatekey --generate simple type=RSA size=2048 protect=module ident=contosokey plainname=contosokey nvram=no pubexp=

<span data-ttu-id="ba604-302">Lorsque vous exécutez cette commande, utilisez ces instructions :</span><span class="sxs-lookup"><span data-stu-id="ba604-302">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="ba604-303">Hello paramètre *protéger* doit avoir la valeur toohello valeur **module**, comme indiqué.</span><span class="sxs-lookup"><span data-stu-id="ba604-303">hello parameter *protect* must be set toohello value **module**, as shown.</span></span> <span data-ttu-id="ba604-304">Ce paramétrage crée une clé protégée par module.</span><span class="sxs-lookup"><span data-stu-id="ba604-304">This creates a module-protected key.</span></span> <span data-ttu-id="ba604-305">ensemble d’outils de Hello BYOK ne prend pas en charge les clés protégées par OCS.</span><span class="sxs-lookup"><span data-stu-id="ba604-305">hello BYOK toolset does not support OCS-protected keys.</span></span>
* <span data-ttu-id="ba604-306">Remplacez la valeur hello *contosokey* pour hello **ident** et **plainname** avec une valeur de chaîne.</span><span class="sxs-lookup"><span data-stu-id="ba604-306">Replace hello value of *contosokey* for hello **ident** and **plainname** with any string value.</span></span> <span data-ttu-id="ba604-307">toominimize charge administrative et de réduire hello risque d’erreurs, nous vous recommandons d’utiliser hello même valeur pour les deux.</span><span class="sxs-lookup"><span data-stu-id="ba604-307">toominimize administrative overheads and reduce hello risk of errors, we recommend that you use hello same value for both.</span></span> <span data-ttu-id="ba604-308">Hello **ident** valeur doit contenir uniquement des chiffres, des tirets et des lettres minuscules.</span><span class="sxs-lookup"><span data-stu-id="ba604-308">hello **ident** value must contain only numbers, dashes, and lower case letters.</span></span>
* <span data-ttu-id="ba604-309">Hello pubexp est vide (par défaut) dans cet exemple, mais vous pouvez spécifier des valeurs spécifiques.</span><span class="sxs-lookup"><span data-stu-id="ba604-309">hello pubexp is left blank (default) in this example, but you can specify specific values.</span></span> <span data-ttu-id="ba604-310">Pour plus d’informations, consultez hello documentation Thales.</span><span class="sxs-lookup"><span data-stu-id="ba604-310">For more information, see hello Thales documentation.</span></span>

<span data-ttu-id="ba604-311">Cette commande crée un fichier de clé Tokénisée dans votre dossier %NFAST_KMDATA%\local avec un nom commençant par **key_simple_**, suivi par hello **ident** qui a été spécifié dans la commande hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-311">This command creates a Tokenized Key file in your %NFAST_KMDATA%\local folder with a name starting with **key_simple_**, followed by hello **ident** that was specified in hello command.</span></span> <span data-ttu-id="ba604-312">Par exemple : **key_simple_contosokey**.</span><span class="sxs-lookup"><span data-stu-id="ba604-312">For example: **key_simple_contosokey**.</span></span> <span data-ttu-id="ba604-313">Ce fichier contient une clé chiffrée.</span><span class="sxs-lookup"><span data-stu-id="ba604-313">This file contains an encrypted key.</span></span>

<span data-ttu-id="ba604-314">Sauvegardez ce fichier de clé à jeton dans un emplacement sûr.</span><span class="sxs-lookup"><span data-stu-id="ba604-314">Back up this Tokenized Key File in a safe location.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ba604-315">Lorsque vous transférerez ultérieurement votre clé tooAzure le coffre de clés, Microsoft ne peut pas exporter cette clé tooyou précédent, il est donc extrêmement important de sauvegarder votre monde de sécurité et de la clé en toute sécurité.</span><span class="sxs-lookup"><span data-stu-id="ba604-315">When you later transfer your key tooAzure Key Vault, Microsoft cannot export this key back tooyou so it becomes extremely important that you back up your key and security world safely.</span></span> <span data-ttu-id="ba604-316">Contactez Thales pour connaître les conseils et meilleures pratiques pour sauvegarder votre clé.</span><span class="sxs-lookup"><span data-stu-id="ba604-316">Contact Thales for guidance and best practices for backing up your key.</span></span>
>
>

<span data-ttu-id="ba604-317">Vous est désormais prêt tootransfer votre clé tooAzure le coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ba604-317">You are now ready tootransfer your key tooAzure Key Vault.</span></span>

## <a name="step-4-prepare-your-key-for-transfer"></a><span data-ttu-id="ba604-318">Étape 4 : Réparez votre clé pour le transfert</span><span class="sxs-lookup"><span data-stu-id="ba604-318">Step 4: Prepare your key for transfer</span></span>
<span data-ttu-id="ba604-319">Pour cette étape quatrième, hello suivant les procédures de station de travail hello déconnecté.</span><span class="sxs-lookup"><span data-stu-id="ba604-319">For this fourth step, do hello following procedures on hello disconnected workstation.</span></span>

### <a name="step-41-create-a-copy-of-your-key-with-reduced-permissions"></a><span data-ttu-id="ba604-320">Étape 4.1 : Créez une copie de votre clé avec des autorisations réduites</span><span class="sxs-lookup"><span data-stu-id="ba604-320">Step 4.1: Create a copy of your key with reduced permissions</span></span>

<span data-ttu-id="ba604-321">Ouvrez une nouvelle invite de commandes et modifier hello actuel toohello emplacement du répertoire où vous avez décompressé le fichier zip BYOK hello.</span><span class="sxs-lookup"><span data-stu-id="ba604-321">Open a new command prompt and change hello current directory toohello location where you unzipped hello BYOK zip file.</span></span> <span data-ttu-id="ba604-322">autorisations de hello tooreduce sur votre clé, à partir d’une invite de commandes, exécutez une des hello suivantes, selon votre région géographique ou d’une instance d’Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-322">tooreduce hello permissions on your key, from a command prompt, run one of hello following, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="ba604-323">Pour l’Amérique du Nord :</span><span class="sxs-lookup"><span data-stu-id="ba604-323">For North America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1
* <span data-ttu-id="ba604-324">Pour l’Europe :</span><span class="sxs-lookup"><span data-stu-id="ba604-324">For Europe:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1
* <span data-ttu-id="ba604-325">Pour l’Asie :</span><span class="sxs-lookup"><span data-stu-id="ba604-325">For Asia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1
* <span data-ttu-id="ba604-326">Pour l’Amérique latine :</span><span class="sxs-lookup"><span data-stu-id="ba604-326">For Latin America:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1
* <span data-ttu-id="ba604-327">Pour le Japon :</span><span class="sxs-lookup"><span data-stu-id="ba604-327">For Japan:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1
* <span data-ttu-id="ba604-328">Pour la Corée :</span><span class="sxs-lookup"><span data-stu-id="ba604-328">For Korea:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1
* <span data-ttu-id="ba604-329">Pour l’Australie :</span><span class="sxs-lookup"><span data-stu-id="ba604-329">For Australia:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1
* <span data-ttu-id="ba604-330">Pour [Azure Government](https://azure.microsoft.com/features/gov/), qui utilise l’instance hello US government Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-330">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1
* <span data-ttu-id="ba604-331">Pour le Département de la Défense des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="ba604-331">For US Government DOD:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1
* <span data-ttu-id="ba604-332">Pour le Canada :</span><span class="sxs-lookup"><span data-stu-id="ba604-332">For Canada:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1
* <span data-ttu-id="ba604-333">Pour l’Allemagne :</span><span class="sxs-lookup"><span data-stu-id="ba604-333">For Germany:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1
* <span data-ttu-id="ba604-334">Pour l’Inde :</span><span class="sxs-lookup"><span data-stu-id="ba604-334">For India:</span></span>

        KeyTransferRemote.exe -ModifyAcls -KeyAppName simple -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1

<span data-ttu-id="ba604-335">Lorsque vous exécutez cette commande, remplacez *contosokey* par hello même valeur spécifiée dans **étape 3.5 : créer une nouvelle clé** de hello [générer votre clé](#step-3-generate-your-key) étape.</span><span class="sxs-lookup"><span data-stu-id="ba604-335">When you run this command, replace *contosokey* with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

<span data-ttu-id="ba604-336">Vous êtes invité tooplug dans vos cartes administrateur de monde de sécurité.</span><span class="sxs-lookup"><span data-stu-id="ba604-336">You are asked tooplug in your security world admin cards.</span></span>

<span data-ttu-id="ba604-337">Commande hello issue, vous voyez **résultat : réussite** et copie hello de votre clé avec autorisations réduites sont dans le fichier hello nommé key_xferacId_<contosokey>.</span><span class="sxs-lookup"><span data-stu-id="ba604-337">When hello command completes, you see **Result: SUCCESS** and hello copy of your key with reduced permissions are in hello file named key_xferacId_<contosokey>.</span></span>

<span data-ttu-id="ba604-338">Vous pouvez inspecte hello ACL à l’aide de l’aide des commandes suivantes hello aux utilitaires Thales :</span><span class="sxs-lookup"><span data-stu-id="ba604-338">You may inspects hello ACLS using following commands using hello Thales utilities:</span></span>

* <span data-ttu-id="ba604-339">aclprint.py :</span><span class="sxs-lookup"><span data-stu-id="ba604-339">aclprint.py:</span></span>

        "%nfast_home%\bin\preload.exe" -m 1 -A xferacld -K contosokey "%nfast_home%\python\bin\python" "%nfast_home%\python\examples\aclprint.py"
* <span data-ttu-id="ba604-340">kmfile-dump.exe :</span><span class="sxs-lookup"><span data-stu-id="ba604-340">kmfile-dump.exe:</span></span>

        "%nfast_home%\bin\kmfile-dump.exe" "%NFAST_KMDATA%\local\key_xferacld_contosokey"
  <span data-ttu-id="ba604-341">Lorsque vous exécutez ces commandes, remplacez contosokey hello même valeur que vous avez spécifié dans **étape 3.5 : créer une nouvelle clé** de hello [générer votre clé](#step-3-generate-your-key) étape.</span><span class="sxs-lookup"><span data-stu-id="ba604-341">When you run these commands, replace contosokey with hello same value you specified in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>

### <a name="step-42-encrypt-your-key-by-using-microsofts-key-exchange-key"></a><span data-ttu-id="ba604-342">Étape 4.2 : Chiffrez votre clé à l’aide clé de Microsoft Exchange</span><span class="sxs-lookup"><span data-stu-id="ba604-342">Step 4.2: Encrypt your key by using Microsoft’s Key Exchange Key</span></span>
<span data-ttu-id="ba604-343">Exécutez une des hello suivant de commandes, selon votre région géographique ou d’une instance d’Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-343">Run one of hello following commands, depending on your geographic region or instance of Azure:</span></span>

* <span data-ttu-id="ba604-344">Pour l’Amérique du Nord :</span><span class="sxs-lookup"><span data-stu-id="ba604-344">For North America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-NA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-NA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-345">Pour l’Europe :</span><span class="sxs-lookup"><span data-stu-id="ba604-345">For Europe:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-EU-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-EU-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-346">Pour l’Asie :</span><span class="sxs-lookup"><span data-stu-id="ba604-346">For Asia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AP-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AP-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-347">Pour l’Amérique latine :</span><span class="sxs-lookup"><span data-stu-id="ba604-347">For Latin America:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-LATAM-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-LATAM-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-348">Pour le Japon :</span><span class="sxs-lookup"><span data-stu-id="ba604-348">For Japan:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-JPN-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-JPN-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-349">Pour la Corée :</span><span class="sxs-lookup"><span data-stu-id="ba604-349">For Korea:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-KOREA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-KOREA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-350">Pour l’Australie :</span><span class="sxs-lookup"><span data-stu-id="ba604-350">For Australia:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-AUS-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-AUS-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-351">Pour [Azure Government](https://azure.microsoft.com/features/gov/), qui utilise l’instance hello US government Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-351">For [Azure Government](https://azure.microsoft.com/features/gov/), which uses hello US government instance of Azure:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USGOV-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USGOV-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-352">Pour le Département de la Défense des États-Unis :</span><span class="sxs-lookup"><span data-stu-id="ba604-352">For US Government DOD:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-USDOD-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-USDOD-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-353">Pour le Canada :</span><span class="sxs-lookup"><span data-stu-id="ba604-353">For Canada:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-CANADA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-CANADA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-354">Pour l’Allemagne :</span><span class="sxs-lookup"><span data-stu-id="ba604-354">For Germany:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-GERMANY-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-GERMANY-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey
* <span data-ttu-id="ba604-355">Pour l’Inde :</span><span class="sxs-lookup"><span data-stu-id="ba604-355">For India:</span></span>

        KeyTransferRemote.exe -Package -KeyIdentifier contosokey -ExchangeKeyPackage BYOK-KEK-pkg-INDIA-1 -NewSecurityWorldPackage BYOK-SecurityWorld-pkg-INDIA-1 -SubscriptionId SubscriptionID -KeyFriendlyName ContosoFirstHSMkey

<span data-ttu-id="ba604-356">Lorsque vous exécutez cette commande, utilisez ces instructions :</span><span class="sxs-lookup"><span data-stu-id="ba604-356">When you run this command, use these instructions:</span></span>

* <span data-ttu-id="ba604-357">Remplacez *contosokey* avec l’identificateur hello que vous avez utilisé la clé de hello toogenerate dans **étape 3.5 : créer une nouvelle clé** de hello [générer votre clé](#step-3-generate-your-key) étape.</span><span class="sxs-lookup"><span data-stu-id="ba604-357">Replace *contosokey* with hello identifier that you used toogenerate hello key in **Step 3.5: Create a new key** from hello [Generate your key](#step-3-generate-your-key) step.</span></span>
* <span data-ttu-id="ba604-358">Remplacez *SubscriptionID* avec l’ID de hello Hello abonnement Azure qui contient votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ba604-358">Replace *SubscriptionID* with hello ID of hello Azure subscription that contains your key vault.</span></span> <span data-ttu-id="ba604-359">Vous avez extrait cette valeur auparavant, dans **étape 1.2 : obtenir votre ID d’abonnement Azure** de hello [préparer votre station de travail connectée à Internet](#step-1-prepare-your-internet-connected-workstation) étape.</span><span class="sxs-lookup"><span data-stu-id="ba604-359">You retrieved this value previously, in **Step 1.2: Get your Azure subscription ID** from hello [Prepare your Internet-connected workstation](#step-1-prepare-your-internet-connected-workstation) step.</span></span>
* <span data-ttu-id="ba604-360">Remplacez *ContosoFirstHSMKey* par une étiquette à utiliser pour votre nom de fichier de sortie.</span><span class="sxs-lookup"><span data-stu-id="ba604-360">Replace *ContosoFirstHSMKey* with a label that is used for your output file name.</span></span>

<span data-ttu-id="ba604-361">Lorsque cette opération terminée avec succès, elle affiche **résultat : réussite** et un nouveau fichier dans le dossier actuel hello a hello suivant le nom : KeyTransferPackage -*ContosoFirstHSMkey*.byok</span><span class="sxs-lookup"><span data-stu-id="ba604-361">When this completes successfully, it displays **Result: SUCCESS** and there is a new file in hello current folder that has hello following name: KeyTransferPackage-*ContosoFirstHSMkey*.byok</span></span>

### <a name="step-43-copy-your-key-transfer-package-toohello-internet-connected-workstation"></a><span data-ttu-id="ba604-362">Étape 4.3 : Copie de transfert de clé package toohello connecté à Internet poste de travail</span><span class="sxs-lookup"><span data-stu-id="ba604-362">Step 4.3: Copy your key transfer package toohello Internet-connected workstation</span></span>
<span data-ttu-id="ba604-363">Utiliser un lecteur USB ou un autre fichier de sortie de stockage portable toocopy hello de hello précédente (KeyTransferPackage-ContosoFirstHSMkey.byok) d’étape tooyour connecté à Internet station de travail.</span><span class="sxs-lookup"><span data-stu-id="ba604-363">Use a USB drive or other portable storage toocopy hello output file from hello previous step (KeyTransferPackage-ContosoFirstHSMkey.byok) tooyour Internet-connected workstation.</span></span>

## <a name="step-5-transfer-your-key-tooazure-key-vault"></a><span data-ttu-id="ba604-364">Étape 5 : Transférer votre clé tooAzure le coffre de clés</span><span class="sxs-lookup"><span data-stu-id="ba604-364">Step 5: Transfer your key tooAzure Key Vault</span></span>
<span data-ttu-id="ba604-365">Pour cette étape finale, sur hello Internet station de travail connectée, utilisez hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) applet de commande tooupload hello package de transfert clé que vous avez copié à partir de hello déconnecté de station de travail toohello HSM pour coffre de clés Azure :</span><span class="sxs-lookup"><span data-stu-id="ba604-365">For this final step, on hello Internet-connected workstation, use hello [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurermkeyvaultkey) cmdlet tooupload hello key transfer package that you copied from hello disconnected workstation toohello Azure Key Vault HSM:</span></span>

    Add-AzureKeyVaultKey -VaultName 'ContosoKeyVaultHSM' -Name 'ContosoFirstHSMkey' -KeyFilePath 'c:\KeyTransferPackage-ContosoFirstHSMkey.byok' -Destination 'HSM'

<span data-ttu-id="ba604-366">Si hello téléchargement réussit, vous consultez les propriétés affichées hello de clé hello que vous venez d’ajouter.</span><span class="sxs-lookup"><span data-stu-id="ba604-366">If hello upload is successful, you see displayed hello properties of hello key that you just added.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba604-367">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="ba604-367">Next steps</span></span>
<span data-ttu-id="ba604-368">Vous pouvez maintenant utiliser cette clé protégée HSM dans votre coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="ba604-368">You can now use this HSM-protected key in your key vault.</span></span> <span data-ttu-id="ba604-369">Pour plus d’informations, consultez hello **si vous souhaitez un module de sécurité matériel (HSM) de toouse** section Bonjour [prise en main d’Azure Key Vault](key-vault-get-started.md) didacticiel.</span><span class="sxs-lookup"><span data-stu-id="ba604-369">For more information, see hello **If you want toouse a hardware security module (HSM)** section in hello [Getting started with Azure Key Vault](key-vault-get-started.md) tutorial.</span></span>
