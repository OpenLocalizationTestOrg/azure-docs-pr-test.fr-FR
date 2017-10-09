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
# <a name="change-a-key-vault-tenant-id-after-a-subscription-move"></a>Modifier l’ID de client du coffre de clés après un déplacement d’abonnement
### <a name="q-my-subscription-was-moved-from-tenant-a-tootenant-b-how-do-i-change-hello-tenant-id-for-my-existing-key-vault-and-set-correct-acls-for-principals-in-tenant-b"></a>Q : mon abonnement a été déplacé entre le client A tootenant B. Comment modifier l’ID de client hello pour mon coffre de clés existant et définir des ACL corrects pour les principaux dans le client B ?
Lorsque vous créez un coffre de clés dans un abonnement, il est ID de locataire Azure Active Directory toohello liée automatiquement par défaut pour cet abonnement. Toutes les entrées de stratégie d’accès sont également des ID de client toothis liée. Lorsque vous déplacez votre abonnement Azure à partir du client un tootenant B, votre clé de coffre est inaccessibles à hello principaux (utilisateurs et applications) dans le client B. toofix ce problème, vous devez :

* Modifier l’ID de client hello associé à tous les coffres de clé existants dans cette tootenant abonnement B.
* supprimer toutes les entrées de stratégie d’accès existantes ;
* ajouter de nouvelles entrées de stratégie d’accès associées au client B.

Par exemple, si vous avez coffre de clés 'myvault' dans un abonnement qui a été déplacé du locataire A tootenant B, ici comment toochange hello ID de locataire pour ce coffre de clés et supprimer les anciennes stratégies d’accès.

<pre>
$Select-AzureRmSubscription -SubscriptionId YourSubscriptionID
$vaultResourceId = (Get-AzureRmKeyVault -VaultName myvault).ResourceId
$vault = Get-AzureRmResource –ResourceId $vaultResourceId -ExpandProperties
$vault.Properties.TenantId = (Get-AzureRmContext).Tenant.TenantId
$vault.Properties.AccessPolicies = @()
Set-AzureRmResource -ResourceId $vaultResourceId -Properties $vault.Properties
</pre>

Étant donné que ce coffre se trouvait dans le locataire A avant le déplacement de hello, hello valeur d’origine de **$vault. Properties.TenantId** client a, while **(Get-AzureRmContext). Tenant.TenantId** est client B.

Maintenant que votre coffre est associé avec l’ID de locataire approprié hello et suppression des anciennes entrées de stratégie d’accès, les entrées de stratégie au nouvel accès définir [Set-AzureRmKeyVaultAccessPolicy](https://msdn.microsoft.com/library/mt603625.aspx).

## <a name="next-steps"></a>Étapes suivantes
Si vous avez des questions sur le coffre de clés Azure, visitez hello [Azure Key Vault Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault).

