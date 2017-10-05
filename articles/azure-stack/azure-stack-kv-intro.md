---
title: "Présentation d’Azure Stack Key Vault | Microsoft Docs"
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
ms.openlocfilehash: dc8b5cb299da74c88aa5ae82636dc345ddd45a2c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="caa2d-103">Introduction à Key Vault dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="caa2d-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="caa2d-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="caa2d-104">Before you start</span></span>
<span data-ttu-id="caa2d-105">Cet article part des principes suivants :</span><span class="sxs-lookup"><span data-stu-id="caa2d-105">This article assumes the following:</span></span>

* <span data-ttu-id="caa2d-106">Les administrateurs de cloud Azure pile doivent avoir [créé une offre](azure-stack-create-offer.md) qui inclut le service de coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="caa2d-106">Azure Stack cloud administrators must have [created an offer](azure-stack-create-offer.md) that includes the Key Vault service.</span></span>  
* <span data-ttu-id="caa2d-107">Les utilisateurs doivent [s’abonner à une offre](azure-stack-subscribe-plan-provision-vm.md) qui inclut le service Key Vault.</span><span class="sxs-lookup"><span data-stu-id="caa2d-107">Users must [subscribe to an offer](azure-stack-subscribe-plan-provision-vm.md) that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="caa2d-108">PowerShell est configuré pour une utilisation avec Azure Stack</span><span class="sxs-lookup"><span data-stu-id="caa2d-108">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="caa2d-109">Principes fondamentaux de Key Vault</span><span class="sxs-lookup"><span data-stu-id="caa2d-109">Key Vault basics</span></span>
<span data-ttu-id="caa2d-110">Key Vault dans Azure Stack permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.</span><span class="sxs-lookup"><span data-stu-id="caa2d-110">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="caa2d-111">En utilisant Key Vault, vous pouvez chiffrer les clés et les secrets (comme les clés d’authentification, les clés des comptes de stockage, les clés de chiffrement de données, les fichiers .pfx et les mots de passe).</span><span class="sxs-lookup"><span data-stu-id="caa2d-111">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="caa2d-112">Key Vault rationalise le processus de gestion de clés et vous permet de garder le contrôle des clés qui accèdent à vos données et les chiffrent.</span><span class="sxs-lookup"><span data-stu-id="caa2d-112">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="caa2d-113">Les développeurs peuvent créer des clés pour le développement et le test en quelques minutes, puis les migrer en toute transparence en clés de production.</span><span class="sxs-lookup"><span data-stu-id="caa2d-113">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="caa2d-114">Les administrateurs de sécurité peuvent accorder (et annuler) les autorisations sur les clés, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="caa2d-114">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="caa2d-115">Toute personne disposant d’un abonnement Azure Stack peut créer et utiliser des coffres de clés.</span><span class="sxs-lookup"><span data-stu-id="caa2d-115">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="caa2d-116">Bien que le coffre de clés avantages aux développeurs et administrateurs de sécurité, peut être implémenté et géré par l’administrateur du cloud qui gère les autres services Azure pile pour une organisation.</span><span class="sxs-lookup"><span data-stu-id="caa2d-116">Although Key Vault benefits developers and security administrators, it can be implemented and managed by the cloud administrator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="caa2d-117">Par exemple, l’administrateur du cloud pouvez vous connecter avec un abonnement Azure pile, créez un coffre pour l’organisation dans lequel stocker les clés, puis être responsable de ces tâches opérationnelles :</span><span class="sxs-lookup"><span data-stu-id="caa2d-117">For example, the cloud administrator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="caa2d-118">créer ou importer une clé ou un secret ;</span><span class="sxs-lookup"><span data-stu-id="caa2d-118">Create or import a key or secret</span></span>
* <span data-ttu-id="caa2d-119">supprimer ou effacer une clé ou un secret ;</span><span class="sxs-lookup"><span data-stu-id="caa2d-119">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="caa2d-120">autoriser des utilisateurs ou des applications à accéder au coffre de clés, afin qu’ils puissent gérer ou utiliser ses clés et ses clés secrètes ;</span><span class="sxs-lookup"><span data-stu-id="caa2d-120">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="caa2d-121">configurer l’utilisation de la clé (par exemple, signer ou chiffrer) ;</span><span class="sxs-lookup"><span data-stu-id="caa2d-121">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="caa2d-122">L’administrateur du cloud peut ensuite fournir aux développeurs des URI à appeler à partir de leurs applications et fournir un administrateur de sécurité avec les informations de journalisation de l’utilisation de la clé.</span><span class="sxs-lookup"><span data-stu-id="caa2d-122">The cloud administrator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="caa2d-123">Les développeurs peuvent également gérer les clés directement à l’aide d’API.</span><span class="sxs-lookup"><span data-stu-id="caa2d-123">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="caa2d-124">Pour plus d’informations, consultez le guide du développeur Key Vault.</span><span class="sxs-lookup"><span data-stu-id="caa2d-124">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="caa2d-125">Scénarios</span><span class="sxs-lookup"><span data-stu-id="caa2d-125">Scenarios</span></span>
<span data-ttu-id="caa2d-126">Le tableau suivant décrit certains des scénarios où Key Vault peut permettre de répondre aux besoins des développeurs et des administrateurs de sécurité :</span><span class="sxs-lookup"><span data-stu-id="caa2d-126">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="caa2d-127">Développeur d’une application Azure Stack</span><span class="sxs-lookup"><span data-stu-id="caa2d-127">Developer for an Azure Stack application</span></span>
<span data-ttu-id="caa2d-128">**Problème** : Je veux écrire une application pour Azure Stack qui utilise des clés pour la signature et le chiffrement, mais je veux que ces clés soient externes à mon application, afin que la solution soit adaptée à une application répartie au niveau géographique.</span><span class="sxs-lookup"><span data-stu-id="caa2d-128">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="caa2d-129">**Solution** : Les clés sont stockées dans un coffre et appelées par un URI quand c’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="caa2d-129">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="caa2d-130">Développeur de logiciels SaaS (Software as a service)</span><span class="sxs-lookup"><span data-stu-id="caa2d-130">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="caa2d-131">**Problème** : Je ne veux pas prendre la responsabilité des clés et des secrets pour mes clients.</span><span class="sxs-lookup"><span data-stu-id="caa2d-131">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="caa2d-132">**Solution :** Les clients peuvent importer leurs propres clés dans Azure Stack et les gérer.</span><span class="sxs-lookup"><span data-stu-id="caa2d-132">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="caa2d-133">Je veux que les clients détiennent et gèrent leurs clés, pour pouvoir me concentrer sur ce que je fais le mieux, c’est-à-dire fournir les principales fonctionnalités du logiciel.</span><span class="sxs-lookup"><span data-stu-id="caa2d-133">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="caa2d-134">Responsable de la sécurité</span><span class="sxs-lookup"><span data-stu-id="caa2d-134">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="caa2d-135">**Problème** : Je veux être sûr que mon organisation contrôle le cycle de vie des clés et puisse surveiller leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="caa2d-135">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="caa2d-136">**Solution :** Key Vault a été conçu de façon que Microsoft ne puisse pas voir ni extraire vos clés.</span><span class="sxs-lookup"><span data-stu-id="caa2d-136">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="caa2d-137">Quand une application doit effectuer des opérations de chiffrement en utilisant des clés des clients, Key Vault le fait à la place de l’application.</span><span class="sxs-lookup"><span data-stu-id="caa2d-137">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="caa2d-138">L’application ne voit pas les clés des clients.</span><span class="sxs-lookup"><span data-stu-id="caa2d-138">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="caa2d-139">Même si nous utilisons plusieurs services et ressources Azure Stack, je veux gérer les clés à partir d’un seul emplacement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="caa2d-139">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="caa2d-140">Le coffre fournit une interface unique, indépendamment du nombre de coffres dont vous disposez dans Azure Stack, des régions qui sont prises en charge et des applications qui les utilisent.</span><span class="sxs-lookup"><span data-stu-id="caa2d-140">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="caa2d-141">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="caa2d-141">Next Steps</span></span>

* [<span data-ttu-id="caa2d-142">Gérer Key Vault dans Azure Stack en utilisant le portail</span><span class="sxs-lookup"><span data-stu-id="caa2d-142">Manage Key Vault in Azure Stack using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="caa2d-143">Gérer Key Vault dans Azure Stack en utilisant PowerShell</span><span class="sxs-lookup"><span data-stu-id="caa2d-143">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
