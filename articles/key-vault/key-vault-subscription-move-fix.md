---
title: "Modifier l’ID de client du coffre de clés après un déplacement d’abonnement | Microsoft Docs"
description: "Apprenez à changer l’ID de client d’un coffre de clés après le déplacement d’un abonnement vers un autre client"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 46d7bc21-fa79-49e4-8c84-032eef1d813e
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 2f007dd4f877b48003cddcefa5f4321049853361
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="a00f5-103">Modifier l’ID de client du coffre de clés après un déplacement d’abonnement</span><span class="sxs-lookup"><span data-stu-id="a00f5-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-to-tenant-b-how-do-i-change-the-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="a00f5-104">Q : Mon abonnement a été déplacé du client A vers le client B. Comment modifier l’ID de client du coffre de clés existant et définir des ACL correctes pour les principaux dans le client B ?</span><span class="sxs-lookup"><span data-stu-id="a00f5-104">Q: My subscription was moved from tenant A to tenant B. How do I change the tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="a00f5-105">Lorsque vous créez un coffre de clés dans un abonnement, il est automatiquement lié à l’ID de client Azure Active Directory par défaut pour cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="a00f5-105">When you create a new key vault in a subscription, it is automatically tied to the default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="a00f5-106">Toutes les entrées de stratégie d’accès sont également liées à cet ID de client.</span><span class="sxs-lookup"><span data-stu-id="a00f5-106">All access policy entries are also tied to this tenant ID.</span></span> <span data-ttu-id="a00f5-107">Lorsque vous déplacez votre abonnement Azure du client A vers le client B, vos coffres de clés existants ne sont pas accessibles par les principaux (utilisateurs et applications) dans le client B. Pour résoudre ce problème, vous devez :</span><span class="sxs-lookup"><span data-stu-id="a00f5-107">When you move your Azure subscription from tenant A to tenant B, your existing key vaults are inaccessible by the principals (users and applications) in tenant B. To fix this issue, you need to:</span></span>

* <span data-ttu-id="a00f5-108">modifier l’ID de client associé à tous les coffres de clés existants dans cet abonnement pour le client B ;</span><span class="sxs-lookup"><span data-stu-id="a00f5-108">Change the tenant ID associated with all existing key vaults in this subscription to tenant B.</span></span>
* <span data-ttu-id="a00f5-109">supprimer toutes les entrées de stratégie d’accès existantes ;</span><span class="sxs-lookup"><span data-stu-id="a00f5-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="a00f5-110">ajouter de nouvelles entrées de stratégie d’accès associées au client B.</span><span class="sxs-lookup"><span data-stu-id="a00f5-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="a00f5-111">Par exemple, si vous avez un coffre de clés 'myvault' dans un abonnement qui a été déplacé du client A vers le client B, voici comment modifier l’ID de client de ce coffre de clés et supprimer d’anciennes stratégies d’accès.</span><span class="sxs-lookup"><span data-stu-id="a00f5-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A to tenant B, here's how to change the tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="a00f5-112">Dans la mesure où ce coffre se trouvait dans le client A avant son déplacement, la valeur d’origine de **$vault. Properties.TenantId** est le client A, tandis que **(Get-AzureRmContext).Tenant.TenantId** est le client B.</span><span class="sxs-lookup"><span data-stu-id="a00f5-112">Because this vault was in tenant A before the move, the original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="a00f5-113">Maintenant que votre coffre est associé avec l’ID de client correct et que les anciennes entrées de stratégie d’accès sont supprimées, définissez les nouvelles entrées de stratégie d’accès avec [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="a00f5-113">Now that your vault is associated with the correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a00f5-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="a00f5-114">Next steps</span></span>
<span data-ttu-id="a00f5-115">Pour toute question concernant le coffre de clés Azure, rendez-vous sur les [forums sur les coffres de clés Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="a00f5-115">If you have questions about Azure Key Vault, visit the [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

