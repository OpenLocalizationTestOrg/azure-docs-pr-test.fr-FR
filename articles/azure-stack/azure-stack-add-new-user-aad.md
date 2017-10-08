---
title: aaaAdd un nouveau compte de locataire Azure pile dans Azure Active Directory | Documents Microsoft
description: "Après avoir déployé le Kit de développement de pile Microsoft Azure, vous devez toocreate au moins un compte d’utilisateur de client, vous pouvez explorer le portail de locataires hello."
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: a75d5c88-5b9e-4e9a-a6e3-48bbfa7069a7
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: f0cd380d4fc0b52f4e5f6f0c9ef80d3dd0d64443
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-new-azure-stack-tenant-account-in-azure-active-directory"></a>Ajouter un nouveau compte de locataire Azure Stack dans Azure Active Directory
Après avoir [déploiement hello Kit de développement Azure pile](azure-stack-run-powershell-script.md), vous aurez besoin à un compte d’utilisateur locataire pour pouvoir Explorer le portail de locataires hello et vos offres et les plans de test. Vous pouvez créer un compte de locataire par [à l’aide de hello portail Azure](#create-an-azure-stack-tenant-account-using-the-azure-portal) ou par [à l’aide de PowerShell](#create-an-azure-stack-tenant-account-using-powershell).

## <a name="create-an-azure-stack-tenant-account-using-hello-azure-portal"></a>Créer un compte de locataire Azure pile à l’aide de hello portail Azure
Vous devez avoir un hello de toouse abonnement Azure portail Azure.

1. Connectez-vous trop[Azure](http://manage.windowsazure.com).
2. Dans la barre de navigation gauche Microsoft Azure, cliquez sur **Active Directory**.
3. Dans la liste de répertoires hello, cliquez sur répertoire hello que vous souhaitez toouse pour la pile de Azure, ou créez un nouveau.
4. Sur la page de ce répertoire, cliquez sur **Utilisateurs**.
5. Cliquez sur **Add User**.
6. Bonjour **ajouter un utilisateur** Assistant Bonjour **Type d’utilisateur** , choisissez **nouvel utilisateur dans votre organisation**.
7. Bonjour **nom d’utilisateur** , tapez un nom d’utilisateur de hello.
8. Bonjour  **@**  , choisissez l’entrée appropriée de hello.
9. Cliquez sur flèche suivant de hello.
10. Bonjour **profil utilisateur** page de l’Assistant de hello, tapez un **prénom**, **nom**, et **nom d’affichage**.
11. Bonjour **rôle** , choisissez **utilisateur**.
12. Cliquez sur flèche suivant de hello.
13. Sur hello **mot de passe temporaire Get** , cliquez sur **créer**.
14. Hello de copie **nouveau mot de passe**.
15. Ouvrez une session dans tooMicrosoft Azure avec un nouveau compte de hello. Modifier le mot de passe hello lorsque vous y êtes invité.
16. Connectez-vous trop`https://portal.local.azurestack.external` avec le portail de locataires hello nouveau compte toosee hello.

## <a name="create-an-azure-stack-tenant-account-using-powershell"></a>Création d’un compte de locataire Azure Stack à l’aide de PowerShell
Si vous n’avez pas un abonnement Azure, vous ne pouvez pas utiliser hello tooadd portail Azure un compte d’utilisateur client. Dans ce cas, vous pouvez utiliser les hello Azure Module Active Directory pour Windows PowerShell à la place.

> [!NOTE]
> Si vous utilisez Microsoft Account (Live ID) toodeploy Kit de développement de pile Azure, vous ne pouvez pas utiliser le compte client AAD PowerShell toocreate. 
> 
> 

1. Installer hello [Assistant Microsoft Online Services Sign-In pour RTW de professionnels de l’informatique](https://www.microsoft.com/en-us/download/details.aspx?id=41950).
2. Installer hello [Azure Module Active Directory pour Windows PowerShell (version 64 bits)](http://go.microsoft.com/fwlink/p/?linkid=236297) et ouvrez-le.
3. Exécutez hello suivant d’applets de commande :

    ```powershell
    # Provide hello AAD credential you use toodeploy Azure Stack Development Kit

            $msolcred = get-credential

    # Add a tenant account "Tenant Admin <username>@<yourdomainname>" with hello initial password "<password>".

            connect-msolservice -credential $msolcred
            $user = new-msoluser -DisplayName "Tenant Admin" -UserPrincipalName <username>@<yourdomainname> -Password <password>
            Add-MsolRoleMember -RoleName "Company Administrator" -RoleMemberType User -RoleMemberObjectId $user.ObjectId

    ```

1. Connectez-vous tooMicrosoft Azure avec un nouveau compte de hello. Modifier le mot de passe hello lorsque vous y êtes invité.
2. Connectez-vous trop`https://portal.local.azurestack.external` avec le portail de locataires hello nouveau compte toosee hello.

