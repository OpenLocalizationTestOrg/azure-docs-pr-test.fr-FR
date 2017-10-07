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
# <a name="grant-permission-toomany-applications-tooaccess-a-key-vault"></a><span data-ttu-id="eab4f-103">Accorder l’autorisation réduire applications tooaccess un coffre de clés</span><span class="sxs-lookup"><span data-stu-id="eab4f-103">Grant permission toomany applications tooaccess a key vault</span></span>

## <a name="q-i-have-several-over-16-applications-that-need-tooaccess-a-key-vault-since-key-vault-only-allows-16-access-control-entries-how-can-i-achieve-that"></a><span data-ttu-id="eab4f-104">Q : j’ai plusieurs applications (16) qui doivent tooaccess un coffre de clés.</span><span class="sxs-lookup"><span data-stu-id="eab4f-104">Q: I have several (over 16) applications that need tooaccess a key vault.</span></span> <span data-ttu-id="eab4f-105">Étant donné que le coffre de clés Key Vault n'autorise que 16 entrées de contrôle d’accès, comment dois-je procéder ?</span><span class="sxs-lookup"><span data-stu-id="eab4f-105">Since Key Vault only allows 16 access control entries, how can I achieve that?</span></span>

<span data-ttu-id="eab4f-106">La stratégie de contrôle d’accès Key Vault prend uniquement en charge 16 entrées.</span><span class="sxs-lookup"><span data-stu-id="eab4f-106">Key Vault access control policy only supports 16 entries.</span></span> <span data-ttu-id="eab4f-107">Mais vous pouvez créer un groupe de sécurité Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eab4f-107">However you can create an Azure Active Directory security group.</span></span> <span data-ttu-id="eab4f-108">Ajouter hello tous les groupe de sécurité de service principaux toothis associé et accorder l’accès toothis sécurité groupe tooKey coffre.</span><span class="sxs-lookup"><span data-stu-id="eab4f-108">Add all hello associated service principals toothis security group and then grant access toothis security group tooKey Vault.</span></span>

<span data-ttu-id="eab4f-109">Voici les conditions préalables hello :</span><span class="sxs-lookup"><span data-stu-id="eab4f-109">Here are hello pre-requisites:</span></span>
* <span data-ttu-id="eab4f-110">[Installez le module Azure Active Directory V2 PowerShell](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span><span class="sxs-lookup"><span data-stu-id="eab4f-110">[Install Azure Active Directory V2 PowerShell module](https://www.powershellgallery.com/packages/AzureAD/2.0.0.30).</span></span>
* <span data-ttu-id="eab4f-111">[Installez Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="eab4f-111">[Install Azure PowerShell](/powershell/azure/overview).</span></span>
* <span data-ttu-id="eab4f-112">les commandes suivantes de hello toorun, groupes de toocreate/modifier des autorisations dans le locataire d’Azure Active Directory hello.</span><span class="sxs-lookup"><span data-stu-id="eab4f-112">toorun hello following commands, you need permissions toocreate/edit groups in hello Azure Active Directory tenant.</span></span> <span data-ttu-id="eab4f-113">Si vous n’êtes pas autorisé, vous devrez peut-être toocontact votre administrateur Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="eab4f-113">If you don't have permissions, you may need toocontact your Azure Active Directory administrator.</span></span>

<span data-ttu-id="eab4f-114">Maintenant, exécutez hello suivant les commandes dans PowerShell.</span><span class="sxs-lookup"><span data-stu-id="eab4f-114">Now run hello following commands in PowerShell.</span></span>

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

<span data-ttu-id="eab4f-115">Si vous avez besoin de toogrant un ensemble différent d’un groupe d’autorisations tooa d’applications, créez un groupe de sécurité Azure Active Directory distinct pour des applications.</span><span class="sxs-lookup"><span data-stu-id="eab4f-115">If you need toogrant a different set of permissions tooa group of applications, create a separate Azure Active Directory security group for such applications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eab4f-116">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="eab4f-116">Next steps</span></span>

<span data-ttu-id="eab4f-117">En savoir plus sur la façon trop[sécuriser votre coffre de clés](key-vault-secure-your-key-vault.md).</span><span class="sxs-lookup"><span data-stu-id="eab4f-117">Learn more about how too[Secure your key vault](key-vault-secure-your-key-vault.md).</span></span>
