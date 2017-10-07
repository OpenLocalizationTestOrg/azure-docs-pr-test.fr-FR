---
title: aaaRegister Azure pile | Documents Microsoft
description: "Inscrire Azure Stack auprès de votre abonnement Azure."
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: erikje
ms.openlocfilehash: 3a3c8e82bec3e1e26ecfe591ecc27b2b91f6f91e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="register-azure-stack-with-your-azure-subscription"></a>Inscrire Azure Stack auprès de votre abonnement Azure

Pour les déploiements d’Azure Active Directory, vous pouvez inscrire Azure pile avec les éléments du marketplace toodownload Azure à partir d’Azure et tooset les données du rapport tooMicrosoft commerce. 

> [!NOTE]
>L’inscription est recommandée, car elle vous permet de tootest fonctionnalités importantes de la pile d’Azure, telles que la syndication de marketplace et des rapports d’utilisation. Après avoir enregistré la pile de Azure, l’utilisation est signalé tooAzure commerce. Vous pouvez le voir dans l’abonnement hello que vous avez utilisé pour l’inscription. Toute utilisation que les utilisateurs du kit de développement Azure Stack signalent ne leur sera pas facturée.
>


## <a name="get-azure-subscription"></a>Prendre un abonnement Azure

Avant d’inscrire Azure Stack auprès d’Azure, vous devez disposer des éléments suivants :

- ID d’abonnement Hello pour un abonnement Azure. ID de hello tooget, connectez-vous tooAzure, cliquez sur **davantage de services** > **abonnements**, cliquez sur abonnement hello toouse et sous **Essentials** vous pouvez recherche hello **ID d’abonnement**. Les abonnements au cloud du gouvernement de Chine, d’Allemagne et des États-Unis ne sont pas pris en charge pour le moment.
- Hello nom d’utilisateur et mot de passe d’un compte qui est propriétaire de l’abonnement de hello (MSA/2FA sont prises en charge)
- Bonjour Azure Active Directory pour hello abonnement Azure. Vous trouverez ce répertoire dans Azure, en pointant sur votre avatar à hello coin supérieur droit de hello portail Azure. 
- Fournisseur de ressources Azure pile hello inscrits (voir hello **inscrire le fournisseur de ressources Azure pile** section ci-dessous pour plus d’informations)

Si vous n’avez pas d’abonnement Azure répondant à ces exigences, vous pouvez [créer un compte Azure gratuit ici](https://azure.microsoft.com/en-us/free/?b=17.06). L’inscription d’Azure Stack n’entraîne aucun frais sur votre abonnement Azure.



## <a name="register-azure-stack-resource-provider-in-azure"></a>Inscrire un fournisseur de ressources Azure Stack dans Azure
> [!NOTE] 
> Cette étape doit seulement toobe effectuée une seule fois dans un environnement de la pile de Azure.
>

1. Démarrez PowerShell ISE en tant qu’administrateur.
2. Se connecter toohello compte Azure qui est propriétaire de hello abonnement Azure avec le paramètre - EnvironmentName défini trop « Cloud Azure ».
3. Inscrire le fournisseur de ressources Azure hello « Microsoft.AzureStack ».

Exemple : 
```Powershell
Login-AzureRmAccount -EnvironmentName "AzureCloud"
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.AzureStack -Force
```


## <a name="register-azure-stack-with-azure"></a>Inscrire Azure Stack auprès d’Azure

> [!NOTE]
>Toutes ces étapes doivent être effectuées sur l’ordinateur hôte hello.
>

1. [Installez PowerShell pour Azure Stack](azure-stack-powershell-install.md). 
2. Hello de copie [RegisterWithAzure.ps1 script](https://go.microsoft.com/fwlink/?linkid=842959) dossier tooa (tel que C:\Temp).
3. Démarrez PowerShell ISE en tant qu’administrateur.    
4. Exécutez hello RegisterWithAzure.ps1 script, en remplaçant hello suivant des espaces réservés :
    - *YourAccountName* est propriétaire de hello Hello abonnement Azure
    - *YourID* est l’ID d’abonnement Azure hello que vous souhaitez toouse tooregister pile d’Azure
    - *YourDirectory* hello désigne votre client Azure Active Directory dont fait partie de votre abonnement Azure.

    ```powershell
    RegisterWithAzure.ps1 -azureSubscriptionId YourID -azureDirectoryTenantName YourDirectory -azureAccountId YourAccountName
    ```
    
    Par exemple :
    
    ```powershell
    C:\temp\RegisterWithAzure.ps1 -azureSubscriptionId "5e0ae55d-0b7a-47a3-afbc-8b372650abd3" `
    -azureDirectoryTenantName "contoso.onmicrosoft.com" `
    -azureAccountId serviceadmin@contoso.onmicrosoft.com
    ```
    
5. Deux invites de hello, appuyez sur ENTRÉE.
6. Dans la fenêtre de connexion contextuelle hello, entrez vos informations d’identification de l’abonnement Azure.

## <a name="verify-hello-registration"></a>Vérification de l’inscription de hello

1. Se connecter dans le portail d’administration toohello (https://adminportal.local.azurestack.external).
2. Cliquez sur **Plus de services** > **Gestion de la Place de Marché** > **Ajouter à partir d’Azure**.
3. Si une liste d’éléments disponibles dans Azure (tels que WordPress) s’affiche, l’activation a réussi.

## <a name="next-steps"></a>Étapes suivantes

[Se connecter tooAzure pile](azure-stack-connect-azure-stack.md)

