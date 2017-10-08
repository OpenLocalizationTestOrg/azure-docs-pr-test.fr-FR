---
title: "à l’aide des données aaaGet hello Azure API de création de rapports AD avec les certificats | Documents Microsoft"
description: "Explique comment toouse hello Azure API de création de rapports AD avec des données de tooget informations d’identification de certificat à partir d’annuaires sans intervention de l’utilisateur."
services: active-directory
documentationcenter: 
author: ramical
writer: v-lorisc
manager: kannar
ms.assetid: 
ms.service: active-directory
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/24/2017
ms.author: ramical
ms.openlocfilehash: 00ddfaefe32ea6ae48f276c974a17ddcf84f7894
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="get-data-using-hello-azure-ad-reporting-api-with-certificates"></a>Obtenir des données à l’aide des API de création de rapports Azure AD hello avec des certificats
Cet article explique comment toouse hello Azure API de création de rapports AD avec des données de tooget informations d’identification de certificat à partir d’annuaires sans intervention de l’utilisateur. 

## <a name="use-hello-azure-ad-reporting-api"></a>Utilisez hello API de création de rapports AD Azure 
API de création de rapports AD Azure nécessite que vous avez terminé de hello comme suit :
 *  Installation des composants requis
 *  Définissez le certificat hello dans votre application
 *  Obtention d’un jeton d’accès
 *  Utilisez hello de jeton toocall hello accès API Graph

Pour plus d’informations sur le code source, consultez [Leverage Report API Module](https://github.com/AzureAD/azure-activedirectory-powershell/tree/gh-pages/Modules/AzureADUtils) (Utiliser le module d’API Génération de rapports). 

### <a name="install-prerequisites"></a>Installation des composants requis
Vous devez toohave Azure AD PowerShell V2 et module AzureADUtils installé.

1. Téléchargez et installez Azure AD Powershell V2, suivant les instructions de hello sur [Azure Active Directory PowerShell](https://github.com/Azure/azure-docs-powershell-azuread/blob/master/Azure AD Cmdlets/AzureAD/index.md).
2. Télécharger le module Azure AD Utils hello [organisation/azure-Active Directory-powershell](https://github.com/AzureAD/azure-activedirectory-powershell/blob/gh-pages/Modules/AzureADUtils/AzureADUtils.psm1). 
  Ce module fournit plusieurs applets de commande d’utilitaire, notamment :
   * version la plus récente de la bibliothèque ADAL à l’aide de Nuget Hello
   * Les jetons d’accès d’utilisateur, de clés d’application et de certificats à l’aide d’ADAL
   * L’API Graph gérant les résultats paginés

**module de Azure AD Utils tooinstall hello :**

1. Créer un module d’utilitaires de répertoire toosave hello (par exemple, c:\azureAD) et télécharger le module de hello à partir de GitHub.
2. Ouvrez une session PowerShell et accédez répertoire toohello que vous venez de créer. 
3. Importer le module de hello et installez-le dans le chemin du module PowerShell hello à l’aide d’applet de commande hello AzureADUtilsModule de l’installation. 

session de Hello doit se présenter comme écran de toothis :

  ![Windows PowerShell](./media/active-directory-report-api-with-certificates/windows-powershell.png)

### <a name="set-hello-certificate-in-your-app"></a>Définissez le certificat hello dans votre application
1. Si vous disposez déjà d’une application, obtenir son ID d’objet à partir de hello portail Azure. 

  ![Portail Azure](./media/active-directory-report-api-with-certificates/azure-portal.png)

2. Ouvrez une session PowerShell et se connecter tooAzure AD à l’aide d’applet de commande hello organisation de se connecter.

  ![Portail Azure](./media/active-directory-report-api-with-certificates/connect-azuaread-cmdlet.png)

3. Utilisez hello applet de commande New-AzureADApplicationCertificateCredential de AzureADUtils tooadd un tooit d’informations d’identification de certificat. 

>[!Note]
>Vous avez besoin d’application de hello tooprovide ID d’objet que vous avez capturés précédemment, ainsi que hello d’objet de certificat (obtenir à l’aide de cette hello Cert : lecteur).
>


  ![Portail Azure](./media/active-directory-report-api-with-certificates/add-certificate-credential.png)
  
### <a name="get-an-access-token"></a>Obtention d’un jeton d’accès

tooget un jeton d’accès, utilisez hello applet de commande Get-AzureADGraphAPIAccessTokenFromCert de AzureADUtils. 

>[!NOTE]
>Vous devez toouse hello ID d’Application au lieu de hello ID d’objet que vous avez utilisé dans la dernière section de hello.
>

 ![Portail Azure](./media/active-directory-report-api-with-certificates/application-id.png)

### <a name="use-hello-access-token-toocall-hello-graph-api"></a>Utilisez hello de jeton toocall hello accès API Graph

Vous pouvez désormais créer le script de hello. Voici un exemple utilisant l’applet de commande Invoke-AzureADGraphAPIQuery de hello hello AzureADUtils. Cette applet de commande gère les résultats composé de plusieurs pages, puis envoie ces pipeline PowerShell de toohello résultats. 

 ![Portail Azure](./media/active-directory-report-api-with-certificates/script-completed.png)

Vous êtes maintenant prêt tooexport tooa volume partagé de cluster et que vous enregistrez tooa SIEM système. Vous pouvez également encapsuler votre script dans une tâche planifiée de tooget données Azure AD à partir de votre client régulièrement sans avoir des clés de l’application toostore dans le code source de hello. 

## <a name="next-steps"></a>Étapes suivantes
[Notions de base Hello de gestion des identités de Azure](https://docs.microsoft.com/en-us/azure/active-directory/fundamentals-identity)<br>



