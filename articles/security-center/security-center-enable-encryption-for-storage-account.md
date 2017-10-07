---
title: "chiffrement aaaEnable pour le compte de stockage dans le centre de sécurité Azure | Documents Microsoft"
description: "Ce document vous montre comment tooimplement hello recommandations du centre de sécurité Azure ** activer le chiffrement pour Azure Storage compte **."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a><span data-ttu-id="0ffcb-103">Activation du chiffrement pour le compte de stockage Azure dans Azure Security Center | Microsoft Docs</span><span class="sxs-lookup"><span data-stu-id="0ffcb-103">Enable encryption for Azure storage account in Azure Security Center</span></span>
<span data-ttu-id="0ffcb-104">Azure Security Center peut vous recommander d’activer le chiffrement du service Azure Storage pour les données au repos.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-104">Azure Security Center may recommend that you enable Azure Storage Service Encryption for data at rest.</span></span>

<span data-ttu-id="0ffcb-105">Chiffrement de Service de stockage (SSE) fonctionne par chiffrement des données de hello lorsqu’elle est écrite tooAzure stockage et le déchiffrement des données hello avant la récupération.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-105">Storage Service Encryption (SSE) works by encrypting hello data when it is written tooAzure storage and decrypting hello data before retrieval.</span></span>  <span data-ttu-id="0ffcb-106">SSE n’est actuellement disponible uniquement pour hello service Blob Azure et peut être utilisé pour les objets BLOB de blocs, objets BLOB de pages et ajoute des objets BLOB.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-106">SSE is currently available only for hello Azure Blob service and can be used for block blobs, page blobs, and append blobs.</span></span>  <span data-ttu-id="0ffcb-107">toolearn, voir [chiffrement de Service de stockage pour les données au repos](../storage/common/storage-service-encryption.md).</span><span class="sxs-lookup"><span data-stu-id="0ffcb-107">toolearn more, see [Storage Service Encryption for data at rest](../storage/common/storage-service-encryption.md).</span></span>


> [!Note]
> <span data-ttu-id="0ffcb-108">Après l’activation du chiffrement, seules les nouvelles données sont chiffrées.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-108">After enabling encryption, only new data is encrypted.</span></span> <span data-ttu-id="0ffcb-109">Tous les objets blob existants dans votre compte de stockage restent non chiffrés.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-109">Any existing blobs in your storage account remain unencrypted.</span></span> <span data-ttu-id="0ffcb-110">tooencrypt des objets BLOB, consultez hello [FAQ de chiffrement de Service de stockage](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span><span class="sxs-lookup"><span data-stu-id="0ffcb-110">tooencrypt existing blobs, see hello [Storage Service Encryption FAQ](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest).</span></span>
>
>

<span data-ttu-id="0ffcb-111">SSE est uniquement pris en charge sur les comptes de stockage Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-111">Storage Service Encryption is only supported on Resource Manager storage accounts.</span></span> <span data-ttu-id="0ffcb-112">Les comptes de stockage classiques ne sont actuellement pas pris en charge.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-112">Classic storage accounts are not currently supported.</span></span> <span data-ttu-id="0ffcb-113">hello toounderstand classique et les modèles de déploiement du Gestionnaire de ressources, consultez [modèles de déploiement Azure](../azure-classic-rm.md).</span><span class="sxs-lookup"><span data-stu-id="0ffcb-113">toounderstand hello classic and Resource Manager deployment models, see [Azure deployment models](../azure-classic-rm.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0ffcb-114">Ce document présente le service de hello à l’aide d’un exemple de déploiement.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-114">This document introduces hello service by using an example deployment.</span></span>  <span data-ttu-id="0ffcb-115">Ce document n'est pas un guide pas à pas.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-115">This document is not a step-by-step guide.</span></span>
>
>

## <a name="implement-hello-recommendation"></a><span data-ttu-id="0ffcb-116">Implémenter la recommandation de hello</span><span class="sxs-lookup"><span data-stu-id="0ffcb-116">Implement hello recommendation</span></span>
1. <span data-ttu-id="0ffcb-117">Bonjour **recommandations** panneau, sélectionnez **activer le chiffrement pour le compte de stockage Azure**.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-117">In hello **Recommendations** blade, select **Enable encryption for Azure Storage Account**.</span></span>
   <span data-ttu-id="0ffcb-118">![Activer le chiffrement pour le compte Azure Storage][1]</span><span class="sxs-lookup"><span data-stu-id="0ffcb-118">![Enable encryption for storage account][1]</span></span>
2. <span data-ttu-id="0ffcb-119">Hello **activer le chiffrement de stockage** panneau s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-119">hello **Enable storage encryption** blade opens.</span></span> <span data-ttu-id="0ffcb-120">Ce panneau répertorie les comptes de stockage Azure hello où le chiffrement de stockage est désactivé.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-120">This blade lists hello Azure storage accounts where storage encryption is disabled.</span></span> <span data-ttu-id="0ffcb-121">Dans cet exemple, sélectionnons **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-121">In this example, let's select **storageacct1**.</span></span>
   <span data-ttu-id="0ffcb-122">![Activer le chiffrement du stockage][2]</span><span class="sxs-lookup"><span data-stu-id="0ffcb-122">![Enable storage encryption][2]</span></span>
3. <span data-ttu-id="0ffcb-123">Hello **chiffrement** panneau pour **storageacct1** s’ouvre.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-123">hello **Encryption** blade for **storageacct1** opens.</span></span> <span data-ttu-id="0ffcb-124">Sélectionnez **Enabled**.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-124">Select **Enabled**.</span></span>
   <span data-ttu-id="0ffcb-125">![Panneau Chiffrement][3]</span><span class="sxs-lookup"><span data-stu-id="0ffcb-125">![Encryption blade][3]</span></span>
4. <span data-ttu-id="0ffcb-126">Sélectionnez **Enregistrer**.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-126">Select **Save**.</span></span>

<span data-ttu-id="0ffcb-127">Vous avez activé le chiffrement de stockage pour **storageacct1**.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-127">You have now enabled storage encryption for **storageacct1**.</span></span>


## <a name="see-also"></a><span data-ttu-id="0ffcb-128">Voir aussi</span><span class="sxs-lookup"><span data-stu-id="0ffcb-128">See also</span></span>
<span data-ttu-id="0ffcb-129">Ce document vous a montré comment tooimplement hello centre de sécurité recommandation « activer le chiffrement pour le compte de stockage Azure. »</span><span class="sxs-lookup"><span data-stu-id="0ffcb-129">This document showed you how tooimplement hello Security Center recommendation "Enable encryption for Azure Storage Account."</span></span> <span data-ttu-id="0ffcb-130">toolearn en savoir plus sur le chiffrement de Service de stockage Azure, voir hello :</span><span class="sxs-lookup"><span data-stu-id="0ffcb-130">toolearn more about Azure Storage Service Encryption, see hello following:</span></span>

* [<span data-ttu-id="0ffcb-131">Azure Storage Service Encryption pour les données au repos</span><span class="sxs-lookup"><span data-stu-id="0ffcb-131">Azure Storage Service Encryption for Data at Rest</span></span>](../storage/common/storage-service-encryption.md)

<span data-ttu-id="0ffcb-132">toolearn en savoir plus sur le centre de sécurité, voir hello :</span><span class="sxs-lookup"><span data-stu-id="0ffcb-132">toolearn more about Security Center, see hello following:</span></span>

* <span data-ttu-id="0ffcb-133">[Définition des stratégies de sécurité dans le centre de sécurité Azure](security-center-policies.md) -en savoir comment les stratégies de sécurité tooconfigure pour vos abonnements Azure et les groupes de ressources.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-133">[Setting security policies in Azure Security Center](security-center-policies.md) - Learn how tooconfigure security policies for your Azure subscriptions and resource groups.</span></span>
* <span data-ttu-id="0ffcb-134">[Contrôle d’intégrité de la sécurité dans le centre de sécurité Azure](security-center-monitoring.md) -en savoir comment toomonitor hello d’intégrité de vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-134">[Security health monitoring in Azure Security Center](security-center-monitoring.md) - Learn how toomonitor hello health of your Azure resources.</span></span>
* <span data-ttu-id="0ffcb-135">[Gestion et répond toosecurity alertes dans le centre de sécurité Azure](security-center-managing-and-responding-alerts.md) -en savoir comment les alertes toosecurity toomanage et y répondre.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-135">[Managing and responding toosecurity alerts in Azure Security Center](security-center-managing-and-responding-alerts.md) - Learn how toomanage and respond toosecurity alerts.</span></span>
* <span data-ttu-id="0ffcb-136">[Gestion des recommandations de sécurité dans Azure Security Center](security-center-recommendations.md) : découvrez la façon dont les recommandations peuvent vous aider à protéger vos ressources Azure.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-136">[Managing security recommendations in Azure Security Center](security-center-recommendations.md) - Learn how recommendations help you protect your Azure resources.</span></span>
* <span data-ttu-id="0ffcb-137">[Forum aux questions sur Azure Security Center](security-center-faq.md) -Forum aux questions sur l’utilisation hello service de recherche.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-137">[Azure Security Center FAQ](security-center-faq.md) - Find frequently asked questions about using hello service.</span></span>
* <span data-ttu-id="0ffcb-138">[Blog sur la sécurité Azure](http://blogs.msdn.com/b/azuresecurity/) : accédez à des billets de blog sur la sécurité et la conformité Azure.</span><span class="sxs-lookup"><span data-stu-id="0ffcb-138">[Azure Security blog](http://blogs.msdn.com/b/azuresecurity/) - Find blog posts about Azure security and compliance.</span></span>

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
