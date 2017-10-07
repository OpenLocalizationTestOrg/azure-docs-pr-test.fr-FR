---
title: "aaaGrant autorisation réduire applications tooaccess un coffre de clés Azure | Documents Microsoft"
description: "Découvrez comment toogrant autorisation réduire applications tooaccess une clé de coffre"
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 785d4e40-fb7b-485a-8cbc-d9c8c87708e6
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/01/2016
ms.author: ambapat
ms.openlocfilehash: 5258149f939856f91b3848fc50399e58e5894f0d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a>Accorder l’autorisation réduire applications tooaccess un coffre de clés

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a>Q : j’ai plusieurs applications (16) qui doivent tooaccess un coffre de clés. Étant donné que le coffre de clés Key Vault n'autorise que 16 entrées de contrôle d’accès, comment dois-je procéder ?

La stratégie de contrôle d’accès Key Vault prend uniquement en charge 16 entrées. Mais vous pouvez créer un groupe de sécurité Azure Active Directory. Ajouter hello tous les groupe de sécurité de service principaux toothis associé et accorder l’accès toothis sécurité groupe tooKey coffre.

Voici les conditions préalables hello :
* [Installez le module Azure Active Directory V2 PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).
* [Installez Azure PowerShell](/powershell/azure/overview).
* les commandes suivantes de hello toorun, groupes de toocreate/modifier des autorisations dans le locataire d’Azure Active Directory hello. Si vous n’êtes pas autorisé, vous devrez peut-être toocontact votre administrateur Azure Active Directory.

Maintenant, exécutez hello suivant les commandes dans PowerShell.

```powershell
# Connect tooAzure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members toothis group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members toothis group, in this fashion. 
 
# Set hello Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust hello permissions as required 
```

Si vous avez besoin de toogrant un ensemble différent d’un groupe d’autorisations tooa d’applications, créez un groupe de sécurité Azure Active Directory distinct pour des applications.

## <a name="next-steps"></a>Étapes suivantes

En savoir plus sur la façon trop[sécuriser votre coffre de clés](key-vault-secure-your-key-vault.md).
