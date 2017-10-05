---
title: "Accorder à plusieurs applications l'autorisation d'accéder à un coffre de clés Azure | Microsoft Docs"
description: "Découvrez comment accorder à plusieurs applications l'autorisation d'accéder à un coffre de clés"
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
ms.openlocfilehash: f58b633de2e4b5702ff2df9b3722662b09510200
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="grant-permission-to-many-applications-to-access-a-key-vault"></a><span data-ttu-id="f0c79-103">Accorder à plusieurs applications l'autorisation d'accéder à un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="f0c79-103">Grant permission to many applications to access a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-to-access-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="f0c79-104">Q : Je possède plusieurs applications (plus de 16) qui nécessitent un accès à un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="f0c79-104">Q: I have several (over 16) applications that need to access a key vault.</span></span> <span data-ttu-id="f0c79-105">Étant donné que le coffre de clés Key Vault n'autorise que 16 entrées de contrôle d’accès, comment dois-je procéder ?</span><span class="sxs-lookup"><span data-stu-id="f0c79-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="f0c79-106">La stratégie de contrôle d’accès Key Vault prend uniquement en charge 16 entrées.</span><span class="sxs-lookup"><span data-stu-id="f0c79-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="f0c79-107">Mais vous pouvez créer un groupe de sécurité Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0c79-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="f0c79-108">Ajoutez tous les principaux du service associés à ce groupe de sécurité et accordez à ce groupe de sécurité l'accès à Key Vault.</span><span class="sxs-lookup"><span data-stu-id="f0c79-108">Add all the associated service principals to this security group and then grant access to this security group to Key Vault.</span></span>

<span data-ttu-id="f0c79-109">Voici les conditions préalables requises :</span><span class="sxs-lookup"><span data-stu-id="f0c79-109">Here are the pre-requisites:</span></span>
* <span data-ttu-id="f0c79-110">[Installez le module Azure Active Directory V2 PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="f0c79-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="f0c79-111">[Installez Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0c79-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="f0c79-112">Pour exécuter les commandes suivantes, vous avez besoin d’autorisations pour créer/modifier des groupes dans le locataire Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="f0c79-112">To run the following commands, you need permissions to create/edit groups in the Azure Active Directory tenant.</span></span> <span data-ttu-id="f0c79-113">Si vous ne disposez pas des autorisations, vous devrez peut-être contacter votre administrateur Active Directory Azure.</span><span class="sxs-lookup"><span data-stu-id="f0c79-113">If you don't have permissions, you may need to contact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="f0c79-114">Exécutez à présent les commandes suivantes dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f0c79-114">Now run the following commands in PowerShell.</span></span>

```powershell
# Connect to Azure AD 
Connect-AzureAD 
 
# Create Azure Active Directory Security Group 
$aadGroup = New-AzureADGroup -Description "Contoso App Group" -DisplayName "ContosoAppGroup" -MailEnabled 0 -MailNickName none -SecurityEnabled 1 
 
# Find and add your applications (ServicePrincipal ObjectID) as members to this group 
$spn = Get-AzureADServicePrincipal –SearchString "ContosoApp1" 
Add-AzureADGroupMember –ObjectId $aadGroup.ObjectId -RefObjectId $spn.ObjectId 
 
# You can add several members to this group, in this fashion. 
 
# Set the Key Vault ACLs 
Set-AzureRmKeyVaultAccessPolicy –VaultName ContosoVault –ObjectId $aadGroup.ObjectId -PermissionToKeys all –PermissionToSecrets all –PermissionToCertificates all 
 
# Of course you can adjust the permissions as required 
```

<span data-ttu-id="f0c79-115">Si vous avez besoin d’accorder un autre jeu d’autorisations à un groupe d’applications, créez un groupe de sécurité Active Directory Azure distinct pour ces applications.</span><span class="sxs-lookup"><span data-stu-id="f0c79-115">If you need to grant a different set of permissions to a group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0c79-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="f0c79-116">Next steps</span></span>

<span data-ttu-id="f0c79-117">En savoir plus sur comment [sécuriser votre coffre de clés](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="f0c79-117">Learn more about how to [Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
