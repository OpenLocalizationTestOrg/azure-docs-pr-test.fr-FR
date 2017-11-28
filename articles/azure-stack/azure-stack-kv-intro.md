---
title: "Présentation de coffre de clés de pile aaaAzure | Documents Microsoft"
description: "Découvrez comment Azure Stack Key Vault gère les clés et les secrets"
services: azure-stack
documentationcenter: 
author: SnehaGunda
manager: byronr
editor: 
ms.assetid: 70f1684a-3fbb-4cd1-bf29-9f9882e98fe9
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/04/2017
ms.author: sngun
ms.openlocfilehash: 12bf9c219c4b2bba37467cafca721a632caa9f70
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tookey-vault-in-azure-stack"></a><span data-ttu-id="b175e-103">Introduction tooKey coffre dans la pile de Azure</span><span class="sxs-lookup"><span data-stu-id="b175e-103">Introduction tooKey Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="b175e-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="b175e-104">Before you start</span></span>
<span data-ttu-id="b175e-105">Cet article suppose hello qui suit :</span><span class="sxs-lookup"><span data-stu-id="b175e-105">This article assumes hello following:</span></span>

* <span data-ttu-id="b175e-106">Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="b175e-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes hello Key Vault service.</span></span>  
* <span data-ttu-id="b175e-107">Les utilisateurs doivent [s’abonner tooan offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service de coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="b175e-107">Users must [subscribe tooan offer](azure-stack-subscribe-plan-provision-vm.md) that includes hello Key Vault service.</span></span>  
* [<span data-ttu-id="b175e-108">PowerShell est configuré pour une utilisation avec Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b175e-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="b175e-109">Principes fondamentaux de Key Vault</span><span class="sxs-lookup"><span data-stu-id="b175e-109">Key Vault basics</span></span>
<span data-ttu-id="b175e-110">Key Vault dans Azure Stack permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.</span><span class="sxs-lookup"><span data-stu-id="b175e-110">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="b175e-111">En utilisant Key Vault, vous pouvez chiffrer les clés et les secrets (comme les clés d’authentification, les clés des comptes de stockage, les clés de chiffrement de données, les fichiers .pfx et les mots de passe).</span><span class="sxs-lookup"><span data-stu-id="b175e-111">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="b175e-112">Coffre de clés rationalise le processus de gestion de clés hello et vous permet de contrôler toomaintain clés d’accès et de chiffrer vos données.</span><span class="sxs-lookup"><span data-stu-id="b175e-112">Key Vault streamlines hello key management process and enables you toomaintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="b175e-113">Les développeurs peuvent créer des clés pour le développement et de test en quelques minutes et puis migrez en toute transparence les clés de tooproduction.</span><span class="sxs-lookup"><span data-stu-id="b175e-113">Developers can create keys for development and testing in minutes, and then seamlessly migrate them tooproduction keys.</span></span> <span data-ttu-id="b175e-114">Les administrateurs de sécurité peuvent accorder (et révoquer) tookeys d’autorisation, en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="b175e-114">Security administrators can grant (and revoke) permission tookeys, as needed.</span></span>

<span data-ttu-id="b175e-115">Toute personne disposant d’un abonnement Azure Stack peut créer et utiliser des coffres de clés.</span><span class="sxs-lookup"><span data-stu-id="b175e-115">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="b175e-116">Bien que le coffre de clés avantages aux développeurs et administrateurs de sécurité, peut être implémenté et géré par l’administrateur du cloud hello qui gère les autres services Azure pile pour une organisation.</span><span class="sxs-lookup"><span data-stu-id="b175e-116">Although Key Vault benefits developers and security administrators, it can be implemented and managed by hello cloud administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="b175e-117">Par exemple, administrateur du cloud hello peut se connecter avec un abonnement Azure pile, créer un archivage de l’organisation de hello dans les clés de toostore, puis être responsable de ces tâches opérationnelles :</span><span class="sxs-lookup"><span data-stu-id="b175e-117">For example, hello cloud administrator can sign in with an Azure Stack subscription, create a vault for hello organization in which toostore keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="b175e-118">créer ou importer une clé ou un secret ;</span><span class="sxs-lookup"><span data-stu-id="b175e-118">Create or import a key or secret</span></span>
* <span data-ttu-id="b175e-119">supprimer ou effacer une clé ou un secret ;</span><span class="sxs-lookup"><span data-stu-id="b175e-119">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="b175e-120">Autoriser les utilisateurs ou applications tooaccess hello coffre de clés, afin qu’ils peuvent ensuite gérer ou utiliser ses clés et les clés secrètes</span><span class="sxs-lookup"><span data-stu-id="b175e-120">Authorize users or applications tooaccess hello key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="b175e-121">configurer l’utilisation de la clé (par exemple, signer ou chiffrer) ;</span><span class="sxs-lookup"><span data-stu-id="b175e-121">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="b175e-122">administrateur du cloud Hello peut ensuite fournir aux développeurs toocall URI à partir de leurs applications et fournir un administrateur de sécurité avec les informations de journalisation de l’utilisation de la clé.</span><span class="sxs-lookup"><span data-stu-id="b175e-122">hello cloud administrator can then provide developers with URIs toocall from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="b175e-123">Les développeurs peuvent également gérer les clés hello directement, en utilisant les API.</span><span class="sxs-lookup"><span data-stu-id="b175e-123">Developers can also manage hello keys directly, by using APIs.</span></span> <span data-ttu-id="b175e-124">Pour plus d’informations, consultez le guide du développeur hello coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="b175e-124">For more information, see hello Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="b175e-125">Scénarios</span><span class="sxs-lookup"><span data-stu-id="b175e-125">Scenarios</span></span>
<span data-ttu-id="b175e-126">Hello tableau suivant décrit certains des scénarios hello où le coffre de clés peuvent aider à répondre aux besoins de hello de développeurs et administrateurs de sécurité :</span><span class="sxs-lookup"><span data-stu-id="b175e-126">hello following table depicts some of hello scenarios where Key Vault can help meet hello needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="b175e-127">Développeur d’une application Azure Stack</span><span class="sxs-lookup"><span data-stu-id="b175e-127">Developer for an Azure Stack application</span></span>
<span data-ttu-id="b175e-128">**Problème**: je veux toowrite une application pour la pile de Azure qui utilise des clés de signature et de chiffrement, mais je veux ces toobe externe à partir de mon application afin que la solution de hello est adaptée à une application qui est distribuée géographiquement.</span><span class="sxs-lookup"><span data-stu-id="b175e-128">**Problem**: I want toowrite an application for Azure Stack that uses keys for signing and encryption, but I want these toobe external from my application so that hello solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="b175e-129">**Solution** : Les clés sont stockées dans un coffre et appelées par un URI quand c’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="b175e-129">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="b175e-130">Développeur de logiciels SaaS (Software as a service)</span><span class="sxs-lookup"><span data-stu-id="b175e-130">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="b175e-131">**Problème :** je ne souhaite pas responsabilité de responsabilité ou potentiel hello pour les clés et les secrets de mon client.</span><span class="sxs-lookup"><span data-stu-id="b175e-131">**Problem:** I don’t want hello responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="b175e-132">**Solution :** Les clients peuvent importer leurs propres clés dans Azure Stack et les gérer.</span><span class="sxs-lookup"><span data-stu-id="b175e-132">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="b175e-133">Je souhaite tooown des clients et que vous gérer leurs clés, je peux vous concentrer sur les effectuant que faire mieux, qui est fournissant des fonctionnalités de logiciel hello core.</span><span class="sxs-lookup"><span data-stu-id="b175e-133">I want customers tooown and manage their keys so that I can concentrate on doing what I do best, which is providing hello core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="b175e-134">Responsable de la sécurité</span><span class="sxs-lookup"><span data-stu-id="b175e-134">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="b175e-135">**Problème :** je souhaite toomake que mon organisation se trouve dans le contrôle du cycle de vie de clé hello et que vous pouvez surveiller l’utilisation de la clé.</span><span class="sxs-lookup"><span data-stu-id="b175e-135">**Problem:** I want toomake sure that my organization is in control of hello key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="b175e-136">**Solution :** Key Vault a été conçu de façon que Microsoft ne puisse pas voir ni extraire vos clés.</span><span class="sxs-lookup"><span data-stu-id="b175e-136">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="b175e-137">Lorsqu’une application doit tooperform les opérations de chiffrement à l’aide de clés de clients, le coffre de clés procède au nom de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="b175e-137">When an application needs tooperform cryptographic operations by using customers’ keys, Key Vault does this on behalf of hello application.</span></span> <span data-ttu-id="b175e-138">application Hello ne voit pas les clés de clients hello.</span><span class="sxs-lookup"><span data-stu-id="b175e-138">hello application does not see hello customers’ keys.</span></span>  <span data-ttu-id="b175e-139">Bien que nous utilisons plusieurs services de la pile d’Azure et les ressources, je veux clés de hello toomanage à partir d’un emplacement unique dans la pile de Azure.</span><span class="sxs-lookup"><span data-stu-id="b175e-139">Although we use multiple Azure Stack services and resources, I want toomanage hello keys from a single location in Azure Stack.</span></span> <span data-ttu-id="b175e-140">coffre de Hello fournit une interface unique, quelle que soit la coffres combien vous avez dans la pile d’Azure, les régions de leur prise en charge et les applications qui utilisent les.</span><span class="sxs-lookup"><span data-stu-id="b175e-140">hello vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b175e-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="b175e-141">Next Steps</span></span>

* [<span data-ttu-id="b175e-142">Gérer le coffre de clés dans la pile d’Azure à l’aide du portail de hello</span><span class="sxs-lookup"><span data-stu-id="b175e-142">Manage Key Vault in Azure Stack using hello portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="b175e-143">Gérer Key Vault dans Azure Stack en utilisant PowerShell</span><span class="sxs-lookup"><span data-stu-id="b175e-143">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
