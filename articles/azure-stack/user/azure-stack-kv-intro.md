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
ms.openlocfilehash: ecb542e967669fc4e4465ae59b3e9c37e4a5c332
ms.sourcegitcommit: 90e2cced6a773b1b52f999ba73cd8877305d270b
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/13/2017
---
# <a name="introduction-to-key-vault-in-azure-stack"></a><span data-ttu-id="07580-103">Introduction à Key Vault dans Azure Stack</span><span class="sxs-lookup"><span data-stu-id="07580-103">Introduction to Key Vault in Azure Stack</span></span>

## <a name="before-you-start"></a><span data-ttu-id="07580-104">Avant de commencer</span><span class="sxs-lookup"><span data-stu-id="07580-104">Before you start</span></span>
<span data-ttu-id="07580-105">Cet article part des principes suivants :</span><span class="sxs-lookup"><span data-stu-id="07580-105">This article assumes the following:</span></span>

* <span data-ttu-id="07580-106">Les utilisateurs doivent s’abonner à une offre qui inclut le service Key Vault.</span><span class="sxs-lookup"><span data-stu-id="07580-106">You must must subscribe to an offer that includes the Key Vault service.</span></span>  
* [<span data-ttu-id="07580-107">PowerShell est configuré pour une utilisation avec Azure Stack</span><span class="sxs-lookup"><span data-stu-id="07580-107">PowerShell is configured for use with Azure Stack</span></span>](azure-stack-powershell-configure-user.md) 
 
## <a name="key-vault-basics"></a><span data-ttu-id="07580-108">Principes fondamentaux de Key Vault</span><span class="sxs-lookup"><span data-stu-id="07580-108">Key Vault basics</span></span>
<span data-ttu-id="07580-109">Key Vault dans Azure Stack permet de protéger les clés de chiffrement et les secrets utilisés par les services et les applications cloud.</span><span class="sxs-lookup"><span data-stu-id="07580-109">Key Vault in Azure Stack helps safeguard cryptographic keys and secrets that cloud applications and services use.</span></span> <span data-ttu-id="07580-110">En utilisant Key Vault, vous pouvez chiffrer les clés et les secrets (comme les clés d’authentification, les clés des comptes de stockage, les clés de chiffrement de données, les fichiers .pfx et les mots de passe).</span><span class="sxs-lookup"><span data-stu-id="07580-110">By using Key Vault, you can encrypt keys and secrets (such as authentication keys, storage account keys, data encryption keys, .pfx files, and passwords).</span></span>

<span data-ttu-id="07580-111">Key Vault rationalise le processus de gestion de clés et vous permet de garder le contrôle des clés qui accèdent à vos données et les chiffrent.</span><span class="sxs-lookup"><span data-stu-id="07580-111">Key Vault streamlines the key management process and enables you to maintain control of keys that access and encrypt your data.</span></span> <span data-ttu-id="07580-112">Les développeurs peuvent créer des clés pour le développement et le test en quelques minutes, puis les migrer en toute transparence en clés de production.</span><span class="sxs-lookup"><span data-stu-id="07580-112">Developers can create keys for development and testing in minutes, and then seamlessly migrate them to production keys.</span></span> <span data-ttu-id="07580-113">Les administrateurs de sécurité peuvent accorder (et annuler) les autorisations sur les clés, si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="07580-113">Security administrators can grant (and revoke) permission to keys, as needed.</span></span>

<span data-ttu-id="07580-114">Toute personne disposant d’un abonnement Azure Stack peut créer et utiliser des coffres de clés.</span><span class="sxs-lookup"><span data-stu-id="07580-114">Anybody with an Azure Stack subscription can create and use key vaults.</span></span> <span data-ttu-id="07580-115">Bien que Key Vault procure des avantages aux développeurs et aux administrateurs de sécurité, il peut être implémenté et géré par l’opérateur qui gère les autres services Azure Stack pour une organisation.</span><span class="sxs-lookup"><span data-stu-id="07580-115">Although Key Vault benefits developers and security administrators, it can be implemented and managed by the operator who manages other Azure Stack services for an organization.</span></span> <span data-ttu-id="07580-116">Par exemple, cet opérateur Azure Stack peut se connecter avec un abonnement Azure Stack, créer un coffre pour l’organisation où stocker les clés, puis avoir la responsabilité de ces tâches opérationnelles :</span><span class="sxs-lookup"><span data-stu-id="07580-116">For example, the Azure Stack operator can sign in with an Azure Stack subscription, create a vault for the organization in which to store keys, and then be responsible for these operational tasks:</span></span>

* <span data-ttu-id="07580-117">créer ou importer une clé ou un secret ;</span><span class="sxs-lookup"><span data-stu-id="07580-117">Create or import a key or secret</span></span>
* <span data-ttu-id="07580-118">supprimer ou effacer une clé ou un secret ;</span><span class="sxs-lookup"><span data-stu-id="07580-118">Revoke or delete a key or secret</span></span>
* <span data-ttu-id="07580-119">autoriser des utilisateurs ou des applications à accéder au coffre de clés, afin qu’ils puissent gérer ou utiliser ses clés et ses clés secrètes ;</span><span class="sxs-lookup"><span data-stu-id="07580-119">Authorize users or applications to access the key vault, so they can   then manage or use its keys and secrets</span></span>
* <span data-ttu-id="07580-120">configurer l’utilisation de la clé (par exemple, signer ou chiffrer) ;</span><span class="sxs-lookup"><span data-stu-id="07580-120">Configure key usage (for example, sign or encrypt)</span></span>

<span data-ttu-id="07580-121">Cet opérateur peut ensuite fournir aux développeurs des URI à appeler à partir de leurs applications et fournir à un administrateur de sécurité des informations de journalisation sur l’utilisation des clés.</span><span class="sxs-lookup"><span data-stu-id="07580-121">The operator can then provide developers with URIs to call from their applications, and provide a security administrator with key usage logging information.</span></span>

<span data-ttu-id="07580-122">Les développeurs peuvent également gérer les clés directement à l’aide d’API.</span><span class="sxs-lookup"><span data-stu-id="07580-122">Developers can also manage the keys directly, by using APIs.</span></span> <span data-ttu-id="07580-123">Pour plus d’informations, consultez le guide du développeur Key Vault.</span><span class="sxs-lookup"><span data-stu-id="07580-123">For more information, see the Key Vault developer's guide.</span></span>

## <a name="scenarios"></a><span data-ttu-id="07580-124">Scénarios</span><span class="sxs-lookup"><span data-stu-id="07580-124">Scenarios</span></span>
<span data-ttu-id="07580-125">Le tableau suivant décrit certains des scénarios où Key Vault peut permettre de répondre aux besoins des développeurs et des administrateurs de sécurité :</span><span class="sxs-lookup"><span data-stu-id="07580-125">The following table depicts some of the scenarios where Key Vault can help meet the needs of developers and security administrators:</span></span>

### <a name="developer-for-an-azure-stack-application"></a><span data-ttu-id="07580-126">Développeur d’une application Azure Stack</span><span class="sxs-lookup"><span data-stu-id="07580-126">Developer for an Azure Stack application</span></span>
<span data-ttu-id="07580-127">**Problème** : Je veux écrire une application pour Azure Stack qui utilise des clés pour la signature et le chiffrement, mais je veux que ces clés soient externes à mon application, afin que la solution soit adaptée à une application répartie au niveau géographique.</span><span class="sxs-lookup"><span data-stu-id="07580-127">**Problem**: I want to write an application for Azure Stack that uses keys for signing and encryption, but I want these to be external from my application so that the solution is suitable for an application that is geographically distributed.</span></span>

<span data-ttu-id="07580-128">**Solution** : Les clés sont stockées dans un coffre et appelées par un URI quand c’est nécessaire.</span><span class="sxs-lookup"><span data-stu-id="07580-128">**Statement**: Keys are stored in a vault and invoked by URI when needed.</span></span>

### <a name="developer-for-software-as-a-service-saas"></a><span data-ttu-id="07580-129">Développeur de logiciels SaaS (Software as a service)</span><span class="sxs-lookup"><span data-stu-id="07580-129">Developer for software as a service (SaaS)</span></span>
<span data-ttu-id="07580-130">**Problème** : Je ne veux pas prendre la responsabilité des clés et des secrets pour mes clients.</span><span class="sxs-lookup"><span data-stu-id="07580-130">**Problem:** I don’t want the responsibility or potential liability for my customer's keys and secrets.</span></span>

<span data-ttu-id="07580-131">**Solution :** Les clients peuvent importer leurs propres clés dans Azure Stack et les gérer.</span><span class="sxs-lookup"><span data-stu-id="07580-131">**Statement:** Customers can import their own keys into Azure Stack, and manage them.</span></span> <span data-ttu-id="07580-132">Je veux que les clients détiennent et gèrent leurs clés, pour pouvoir me concentrer sur ce que je fais le mieux, c’est-à-dire fournir les principales fonctionnalités du logiciel.</span><span class="sxs-lookup"><span data-stu-id="07580-132">I want customers to own and manage their keys so that I can concentrate on doing what I do best, which is providing the core software features.</span></span>

### <a name="chief-security-officer-cso"></a><span data-ttu-id="07580-133">Responsable de la sécurité</span><span class="sxs-lookup"><span data-stu-id="07580-133">Chief Security Officer (CSO)</span></span>
<span data-ttu-id="07580-134">**Problème** : Je veux être sûr que mon organisation contrôle le cycle de vie des clés et puisse surveiller leur utilisation.</span><span class="sxs-lookup"><span data-stu-id="07580-134">**Problem:** I want to make sure that my organization is in control of the key life cycle and can monitor key usage.</span></span>

<span data-ttu-id="07580-135">**Solution :** Key Vault a été conçu de façon que Microsoft ne puisse pas voir ni extraire vos clés.</span><span class="sxs-lookup"><span data-stu-id="07580-135">**Statement** Key Vault is designed so that Microsoft does not see or extract your keys.</span></span>  <span data-ttu-id="07580-136">Quand une application doit effectuer des opérations de chiffrement en utilisant des clés des clients, Key Vault le fait à la place de l’application.</span><span class="sxs-lookup"><span data-stu-id="07580-136">When an application needs to perform cryptographic operations by using customers’ keys, Key Vault does this on behalf of the application.</span></span> <span data-ttu-id="07580-137">L’application ne voit pas les clés des clients.</span><span class="sxs-lookup"><span data-stu-id="07580-137">The application does not see the customers’ keys.</span></span>  <span data-ttu-id="07580-138">Même si nous utilisons plusieurs services et ressources Azure Stack, je veux gérer les clés à partir d’un seul emplacement dans Azure.</span><span class="sxs-lookup"><span data-stu-id="07580-138">Although we use multiple Azure Stack services and resources, I want to manage the keys from a single location in Azure Stack.</span></span> <span data-ttu-id="07580-139">Le coffre fournit une interface unique, indépendamment du nombre de coffres dont vous disposez dans Azure Stack, des régions qui sont prises en charge et des applications qui les utilisent.</span><span class="sxs-lookup"><span data-stu-id="07580-139">The vault provides a single interface, regardless of how many vaults you have in Azure Stack, which regions they support, and which applications use them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="07580-140">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="07580-140">Next Steps</span></span>

* [<span data-ttu-id="07580-141">Gérer Key Vault dans Azure Stack en utilisant le portail</span><span class="sxs-lookup"><span data-stu-id="07580-141">Manage Key Vault in Azure Stack using the portal</span></span>](azure-stack-kv-manage-portal.md)  
* [<span data-ttu-id="07580-142">Gérer Key Vault dans Azure Stack en utilisant PowerShell</span><span class="sxs-lookup"><span data-stu-id="07580-142">Manage Key Vault in Azure Stack using PowerShell</span></span>](azure-stack-kv-manage-powershell.md)
