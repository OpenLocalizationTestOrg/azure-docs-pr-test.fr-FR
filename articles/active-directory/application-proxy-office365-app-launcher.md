---
title: "aaaSet une page d’accueil personnalisée pour les applications publiées à l’aide du Proxy d’Application Azure AD | Documents Microsoft"
description: "Décrit les principes de base hello des connecteurs de Proxy d’Application Azure AD"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 5bb695e904d285c3b440520f107c7bf63ba5cac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="set-a-custom-home-page-for-published-apps-by-using-azure-ad-application-proxy"></a>Définir une page d’accueil personnalisée pour les applications publiées à l’aide du proxy d’application Azure AD

Cet article explique comment tooconfigure applications toodirect utilisateurs tooa page d’accueil personnalisée. Lorsque vous publiez une application avec le Proxy d’Application, vous définissez une URL interne, mais qui n’est parfois pas page hello que vos utilisateurs doivent tout d’abord voir. Définir une page d’accueil personnalisée afin que vos utilisateurs atteindre la page de droite toohello lorsqu’ils accèdent à des applications de hello de hello volet d’accès Azure Active Directory ou le Lanceur d’applications hello Office 365.

Lorsque les utilisateurs lancent l’application hello, ils sont dirigés par URL de domaine par défaut toohello racine pour l’application publiée hello. page d’accueil Hello est généralement définie en tant qu’URL de la page d’accueil hello. Utilisez des URL de page d’accueil personnalisée hello Azure AD PowerShell module toodefine tooland d’utilisateurs d’application sur une page spécifique au sein de l’application hello. 

Par exemple :
- À l’intérieur de votre réseau d’entreprise, les utilisateurs accéder trop*https://ExpenseApp/login/login.aspx* toosign dans et accéder à votre application.
- Étant donné que vous disposez d’autres ressources comme les images que le Proxy d’Application doit tooaccess au niveau supérieur de hello hello structure des dossiers, vous publiez application hello avec *https://ExpenseApp* comme hello URL interne.
- Hello URL externe par défaut est *https://ExpenseApp-contoso.msappproxy.net*, qui ne prend pas vos informations d’identification toohello les utilisateurs dans la page.  
- Définissez *https://ExpenseApp-contoso.msappproxy.net/login/login.aspx* comme hello toogive URL de page d’accueil de vos utilisateurs une expérience transparente. 

>[!NOTE]
>Lorsque vous accordez aux utilisateurs un accès toopublished applications, les applications de hello s’affichent dans hello [panneau d’accès Azure AD](active-directory-saas-access-panel-introduction.md) et hello [Lanceur d’applications Office 365](https://blogs.office.com/2016/09/27/introducing-the-new-office-365-app-launcher).

## <a name="before-you-start"></a>Avant de commencer

Avant de définir des URL de la page d’accueil hello, gardez Bonjour esprit suivant les exigences :

* Vérifiez que ce chemin d’accès hello que vous spécifiez est un chemin d’accès de sous-domaine de hello URL racine du domaine.

  Si l’URL de domaine à la racine de hello est, par exemple, https://apps.contoso.com/app1/, URL de page d’accueil hello que vous configurez doit commencer par https://apps.contoso.com/app1/.

* Si vous apportez une modification toohello publié l’application, la modification de hello peut réinitialiser la valeur hello d’URL de la page d’accueil hello. Lorsque vous mettez à jour application hello Bonjour futures, vous devez vérifier de nouveau et, si nécessaire, mettez à jour les URL de la page d’accueil hello.

## <a name="change-hello-home-page-in-hello-azure-portal"></a>Modifier la page d’accueil hello hello portail Azure

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) en tant qu’administrateur.
2. Accédez trop**Azure Active Directory** > **inscriptions d’application** et choisissez votre application à partir de la liste de hello. 
3. Sélectionnez **propriétés** à partir des paramètres de hello.
4. Hello de mise à jour **URL de la page d’accueil** champ avec votre nouveau chemin d’accès. 

   ![Fournir la nouvelle URL de la page d’accueil](./media/application-proxy-office365-app-launcher/homepage.png)

5. Sélectionnez **Enregistrer**.

## <a name="change-hello-home-page-with-powershell"></a>Modifier la page d’accueil hello avec PowerShell

### <a name="install-hello-azure-ad-powershell-module"></a>Installer le module PowerShell Azure AD de hello

Avant de définir une URL de la page d’accueil personnalisée à l’aide de PowerShell, installer le module PowerShell Azure AD de hello. Vous pouvez télécharger le package de hello de hello [PowerShell Gallery](https://www.powershellgallery.com/packages/AzureAD/2.0.0.131), qui utilise hello de point de terminaison de l’API Graph. 

tooinstall hello du package, procédez comme suit :

1. Ouvrez une fenêtre PowerShell standard et puis exécutez hello de commande suivante :

    ```
     Install-Module -Name AzureAD
    ```
    Si vous exécutez la commande hello en tant que non-administrateur, utilisez hello `-scope currentuser` option.
2. Pendant l’installation de hello, sélectionnez **Y** tooinstall deux packages de Nuget.org. Les deux packages sont requis. 

### <a name="find-hello-objectid-of-hello-app"></a>Recherche hello ObjectID de l’application hello

Obtenir hello ObjectID de l’application hello et recherchez application hello par sa page d’accueil.

1. Ouvrez PowerShell et importer le module de hello Azure AD.

    ```
    Import-Module AzureAD
    ```

2. Se connecter toohello module Azure AD en tant qu’administrateur de locataire hello.

    ```
    Connect-AzureAD
    ```
3. Recherchez l’application hello en fonction de son URL de la page d’accueil. Vous pouvez trouver des URL de hello dans le portail de hello en accédant trop**Azure Active Directory** > **des applications d’entreprise** > **toutes les applications**. Cet exemple utilise *sharepoint-iddemo*.

    ```
    Get-AzureADApplication | where { $_.Homepage -like “sharepoint-iddemo” } | fl DisplayName, Homepage, ObjectID
    ```
4. Vous devez obtenir un résultat similaire toohello celui présenté ici. Copiez hello ObjectID GUID toouse dans la section suivante de hello.

    ```
    DisplayName : SharePoint
    Homepage    : https://sharepoint-iddemo.msappproxy.net/
    ObjectId    : 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

### <a name="update-hello-home-page-url"></a>Mettre à jour des URL de la page d’accueil hello

Bonjour même module PowerShell que vous avez utilisé pour l’étape 1, effectuez hello comme suit :

1. Vérifiez que vous disposez hello corriger l’application, puis remplacez *8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4* avec hello ObjectID que vous avez copié dans hello précédant l’étape.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4.
    ```

 Maintenant que vous avez confirmé l’application hello, vous êtes prêt tooupdate hello page d’accueil, comme suit.

2. Créer des modifications hello à toomake un toohold d’objet application vide. Cette variable contient des valeurs hello que vous souhaitez tooupdate. Rien n’est créé lors de cette étape.

    ```
    $appnew = New-Object “Microsoft.Open.AzureAD.Model.Application”
    ```

3. La valeur hello page d’accueil URL toohello souhaité. valeur de Hello doit être un chemin d’accès de sous-domaine de l’application publiée hello. Par exemple, si vous modifiez hello URL de page d’accueil à partir de *https://sharepoint-iddemo.msappproxy.net/* trop*https://sharepoint-iddemo.msappproxy.net/hybrid/*, application utilisateurs accèdent directement toohello personnalisé page d’accueil.

    ```
    $homepage = “https://sharepoint-iddemo.msappproxy.net/hybrid/”
    ```
4. Rendre hello mise à jour à l’aide de hello GUID (ObjectID) que vous avez copié dans « étape 1 : rechercher hello ObjectID de l’application hello. »

    ```
    Set-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4 -Homepage $homepage
    ```
5. tooconfirm que la modification de hello a réussi, redémarrez l’application hello.

    ```
    Get-AzureADApplication -ObjectId 8af89bfa-eac6-40b0-8a13-c2c4e3ee22a4
    ```

>[!NOTE]
>Les modifications que vous apportez toohello application peuvent réinitialiser les URL de la page d’accueil hello. Si l’URL de votre page d’accueil se réinitialise, répétez l’étape 2.

## <a name="next-steps"></a>Étapes suivantes

- [Activer tooSharePoint l’accès à distance avec le Proxy d’Application Azure AD](application-proxy-enable-remote-access-sharepoint.md)
- [Activer le Proxy d’Application Bonjour portail Azure](active-directory-application-proxy-enable.md)
