---
title: "ID de client de coffre de clés aaaChange hello après le déplacement d’un abonnement | Documents Microsoft"
description: "Découvrez comment tooswitch hello client ID pour un coffre de clés après qu’un abonnement est déplacé tooa autre client"
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
ms.openlocfilehash: 4d0607208c61c57959439d2d0bd8feade4141fee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a><span data-ttu-id="aad58-103">Modifier l’ID de client du coffre de clés après un déplacement d’abonnement</span><span class="sxs-lookup"><span data-stu-id="aad58-103">Change a key vault tenant ID after a subscription move</span></span>
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a><span data-ttu-id="aad58-104">Q : mon abonnement a été déplacé entre le client A tootenant B. Comment modifier l’ID de client hello pour mon coffre de clés existant et définir des ACL corrects pour les principaux dans le client B ?</span><span class="sxs-lookup"><span data-stu-id="aad58-104">Q: My subscription was moved from tenant A tootenant B. How do I change hello tenant ID for my existing key vault and set correct ACLs for principals in tenant B?</span></span>
<span data-ttu-id="aad58-105">Lorsque vous créez un coffre de clés dans un abonnement, il est ID de locataire Azure Active Directory toohello liée automatiquement par défaut pour cet abonnement.</span><span class="sxs-lookup"><span data-stu-id="aad58-105">When you create a new key vault in a subscription, it is automatically tied toohello default Azure Active Directory tenant ID for that subscription.</span></span> <span data-ttu-id="aad58-106">Toutes les entrées de stratégie d’accès sont également des ID de client toothis liée.</span><span class="sxs-lookup"><span data-stu-id="aad58-106">All access policy entries are also tied toothis tenant ID.</span></span> <span data-ttu-id="aad58-107">Lorsque vous déplacez votre abonnement Azure à partir du client un tootenant B, votre clé de coffre est inaccessibles à hello principaux (utilisateurs et applications) dans le client B. toofix ce problème, vous devez :</span><span class="sxs-lookup"><span data-stu-id="aad58-107">When you move your Azure subscription from tenant A tootenant B, your existing key vaults are inaccessible by hello principals (users and applications) in tenant B. toofix this issue, you need to:</span></span>

* <span data-ttu-id="aad58-108">Modifier l’ID de client hello associé à tous les coffres de clé existants dans cette tootenant abonnement B.</span><span class="sxs-lookup"><span data-stu-id="aad58-108">Change hello tenant ID associated with all existing key vaults in this subscription tootenant B.</span></span>
* <span data-ttu-id="aad58-109">supprimer toutes les entrées de stratégie d’accès existantes ;</span><span class="sxs-lookup"><span data-stu-id="aad58-109">Remove all existing access policy entries.</span></span>
* <span data-ttu-id="aad58-110">ajouter de nouvelles entrées de stratégie d’accès associées au client B.</span><span class="sxs-lookup"><span data-stu-id="aad58-110">Add new access policy entries that are associated with tenant B.</span></span>

<span data-ttu-id="aad58-111">Par exemple, si vous avez coffre de clés 'myvault' dans un abonnement qui a été déplacé du locataire A tootenant B, ici comment toochange hello ID de locataire pour ce coffre de clés et supprimer les anciennes stratégies d’accès.</span><span class="sxs-lookup"><span data-stu-id="aad58-111">For example, if you have key vault 'myvault' in a subscription that has been moved from tenant A tootenant B, here's how toochange hello tenant ID for this key vault and remove old access policies.</span></span>

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

<span data-ttu-id="aad58-112">Étant donné que ce coffre se trouvait dans le locataire A avant le déplacement de hello, hello valeur d’origine de **$vault. Properties.TenantId** client a, while **(Get-AzureRmContext). Tenant.TenantId** est client B.</span><span class="sxs-lookup"><span data-stu-id="aad58-112">Because this vault was in tenant A before hello move, hello original value of **$vault.Properties.TenantId** is tenant A, while **(Get-AzureRmContext).Tenant.TenantId** is tenant B.</span></span>

<span data-ttu-id="aad58-113">Maintenant que votre coffre est associé avec l’ID de locataire approprié hello et suppression des anciennes entrées de stratégie d’accès, les entrées de stratégie au nouvel accès définir [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span><span class="sxs-lookup"><span data-stu-id="aad58-113">Now that your vault is associated with hello correct tenant ID and old access policy entries are removed, set new access policy entries with [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aad58-114">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="aad58-114">Next steps</span></span>
<span data-ttu-id="aad58-115">Si vous avez des questions sur le coffre de clés Azure, visitez hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span><span class="sxs-lookup"><span data-stu-id="aad58-115">If you have questions about Azure Key Vault, visit hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).</span></span>

