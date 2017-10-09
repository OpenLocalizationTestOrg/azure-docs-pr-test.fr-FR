---
title: "architecture mutualisée dans Azure pile aaaEnable | Documents Microsoft"
description: "Découvrez comment toosupport plusieurs annuaires Azure Active Directory dans la pile de Azure"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: d7e404894a65f6786c42c5c27f76d46f353cb8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a>Activer l’architecture multilocataire dans Azure Stack

Vous pouvez configurer les utilisateurs toosupport de pile de Azure à partir de plusieurs services toouse de locataires Azure Active Directory (Azure AD) dans la pile de Azure. Par exemple, considérez hello scénario :

 - Vous êtes hello administrateur du Service de contoso.onmicrosoft.com, où la pile de Azure est installé.
 - Mary est hello administrateur d’annuaire de fabrikam.onmicrosoft.com, dans lequel se trouvent les utilisateurs invités. 
 - Société de Mary reçoit des services IaaS et PaaS à partir de votre entreprise et doit tooallow hello invité active (fabrikam.onmicrosoft.com) toosign dans utilisateurs et utilise des ressources de la pile d’Azure dans contoso.onmicrosoft.com.

Ce guide fournit les étapes hello requis dans le contexte de hello de ce scénario, tooconfigure une architecture mutualisée de pile de Azure.  Dans ce scénario, vous Mary doit effectuer les étapes que l’utilisateur à partir de toosign Fabrikam dans tooenable et consommer des services à partir de hello déploiement Azure pile de Contoso.  

## <a name="before-you-begin"></a>Avant de commencer
Il existe quelques tooaccount de conditions préalables pour avant de configurer une architecture mutualisée de pile de Azure :
  
 - Vous Mary doit coordonner des étapes administratives sur les deux annuaires hello Azure pile est installé dans (Contoso) et hello active de l’invité (Fabrikam).  
 - Vérifiez que vous avez [installé](azure-stack-powershell-install.md) et [configuré](azure-stack-powershell-configure-admin.md) PowerShell pour Azure Stack.
 - [Télécharger les outils de pile Azure hello](azure-stack-powershell-download.md)et importer des modules de se connecter et d’identité hello :

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - Mary nécessitera [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) tooAzure pile d’accès. 

## <a name="configure-azure-stack-directory"></a>Configurer l’annuaire Azure Stack
Dans cette section, vous configurez Azure pile tooallow les connexions depuis des clients d’annuaire Azure AD de Fabrikam.

### <a name="onboard-guest-directory-tenant"></a>Intégrer le locataire d’annuaire invité
TooAzure du locataire d’annuaire invité (Fabrikam) suivant, intégrer hello pile.  Cette étape configure le Gestionnaire de ressources Azure tooaccept utilisateurs et principaux de service à partir du locataire d’annuaire hello invité.

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace hello value below with hello Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a>Configurer l’annuaire invité
Après avoir terminé les étapes décrites dans le répertoire de pile de Azure hello, Mary doit fournir son consentement tooAzure pile accès hello invité annuaire et Azure pile auprès active d’invité hello. 

### <a name="registering-azure-stack-with-hello-guest-directory"></a>L’inscription de la pile d’Azure avec le répertoire d’invité hello
Une fois que l’administrateur d’annuaire hello invité a fourni le consentement pour le répertoire de la pile de Azure tooaccess Fabrikam, ils doivent s’inscrire à Azure pile de locataire d’annuaire de Fabrikam.

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-toosign-in"></a>Toosign de diriger les utilisateurs dans
Maintenant que vous et Mary terminées active de hello étapes tooonboard Mary, Mary peut diriger toosign les utilisateurs de Fabrikam dans.  Les utilisateurs de Fabrikam (autrement dit, les utilisateurs avec le suffixe de fabrikam.onmicrosoft.com hello) se connectent en visitant https://portal.local.azurestack.external.  

Mary dirigera les [étrangère principaux](../active-directory/active-directory-understanding-resource-access.md) dans toosign de répertoire (autrement dit, les utilisateurs dans le répertoire de Fabrikam hello sans suffixe hello fabrikam.onmicrosoft.com) hello Fabrikam à l’aide de https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  Si elles n’utilisent pas cette URL, ils sont envoyés de répertoire par défaut de tootheir (Fabrikam) et vous recevez une erreur indiquant que leur administrateur n’a pas donné son consentement.

## <a name="next-steps"></a>Étapes suivantes

- [Gérer les fournisseurs délégués](azure-stack-delegated-provider.md)
- [Concepts clés d’Azure Stack](azure-stack-key-features.md)
