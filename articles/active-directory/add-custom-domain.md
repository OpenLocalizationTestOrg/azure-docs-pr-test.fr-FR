---
title: "aaaAdd un tooAzure de domaine personnalisé AD | Documents Microsoft"
description: "Explique comment tooadd un domaine personnalisé dans Azure Active Directory."
services: active-directory
author: jeffgilb
manager: femila
ms.assetid: 0a90c3c5-4e0e-43bd-a606-6ee00f163038
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: jeffgilb
ms.reviewer: jsnow
ms.custom: it-pro
ms.openlocfilehash: 878cecad364ec47f1c6755d742aaccbce627dc5e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-add-a-custom-domain-name-tooazure-active-directory"></a>Démarrage rapide : Ajouter un tooAzure de nom de domaine personnalisé Active Directory

Chaque annuaire Azure AD est fourni avec un nom de domaine sous forme de hello de *domainname*. onmicrosoft.com. nom de domaine initial hello ne peut pas être modifiée ou supprimée, mais vous pouvez ajouter votre tooAzure de nom du domaine d’entreprise Active Directory ainsi. Par exemple, votre organisation a probablement autres domaine noms utilisés toodo entreprise et les utilisateurs de se connecter à l’aide de votre nom de domaine d’entreprise. Ajout des noms de domaine personnalisé tooAzure AD vous permet de noms d’utilisateur tooassign dans le répertoire de hello qui sont les utilisateurs tooyour familiers, tels que «alice@contoso.com. » au lieu d’« alice@*<domain name>*.onmicrosoft.com ». processus de Hello est simple :

1. Ajouter un répertoire de tooyour de nom de domaine personnalisé hello
2. Ajouter une entrée DNS pour le nom de domaine hello au bureau d’enregistrement de nom de domaine hello
3. Vérifiez le nom de domaine personnalisé hello dans Azure AD

## <a name="add-your-custom-domain"></a>Ajouter un domaine personnalisé
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **davantage de services**, entrez **Azure Active Directory** dans hello de zone de texte, puis sélectionnez **entrée**.
   
   ![Ouvrir la gestion des utilisateurs](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Sur hello ***-nom du répertoire*** panneau, sélectionnez **les noms de domaine**.
4. Sur hello  ***-nom du répertoire* -les noms de domaine** panneau, sélectionnez hello **ajouter** commande.
   
   ![En sélectionnant Ajouter une commande hello](./media/active-directory-domains-add-azure-portal/add-command.png)
5. Sur hello **nom de domaine** panneau, entrez le nom hello de votre domaine personnalisé dans la zone de hello, par exemple, « contoso.com » et puis **ajouter un domaine**. Être vraiment tooinclude hello .com, .net ou toute autre extension de niveau supérieur.
6. Sur hello ***nom de domaine*** blade (avec le nom de votre domaine personnalisé dans le titre de hello), obtenir hello DNS entrée informations toouse tooverify que votre organisation possède le nom de domaine personnalisé hello.
   
   ![obtenir les informations d’entrée DNS](./media/active-directory-domains-add-azure-portal/get-dns-info.png)

> [!TIP]
> Si vous envisagez de toofederate local Windows Server Active Directory avec Azure AD, vous devez tooselect hello **je prévois tooconfigure ce domaine pour l’authentification unique avec mon annuaire Active Directory local** case à cocher lorsque vous exécutez l’outil de hello Azure AD Connect toosynchronize vos annuaires. Vous devez également tooregister hello du même nom de domaine vous sélectionnez pour fédérer avec votre annuaire local Bonjour **domaine Azure AD** étape dans l’Assistant de hello. Vous pouvez voir quels cette étape dans l’Assistant hello ressemble à [dans ces instructions](./connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Si vous n’avez pas l’outil de hello Azure AD Connect, vous pouvez [télécharger ici](http://go.microsoft.com/fwlink/?LinkId=615771).

Maintenant que vous avez ajouté le nom de domaine hello, Azure AD doit vérifier que votre organisation possède le nom de domaine hello. Avant d’Azure AD peut effectuer cette vérification, vous devez ajouter une entrée DNS dans le fichier de zone DNS hello pour le nom de domaine hello. Cette tâche est effectuée sur le site Web de hello pour le bureau d’enregistrement du nom de domaine pour le nom de domaine hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Ajouter l’entrée DNS de hello au bureau d’enregistrement du nom de domaine hello pour le domaine de hello
toouse étape suivante de Hello, nom de votre domaine personnalisé avec Azure AD est un fichier de zone DNS tooupdate hello pour le domaine de hello. Azure AD peut ensuite vérifier que votre organisation possède le nom de domaine personnalisé hello.

1. Se connecter dans le Registre des noms de domaine pour le domaine de hello toohello. Si vous n’avez pas hello de tooupdate accès entrée DNS, demandez à personne de hello ou équipe disposant de cette étape de toocomplete accès 2 et toolet que vous savez lorsqu’elle est effectuée.
2. Fichier de zone de mise à jour hello DNS pour le domaine hello en ajoutant l’entrée DNS de hello fourni tooyou par Azure AD. Cette entrée DNS permet à Azure AD tooverify votre propriétaire du domaine de hello. Hello entrée DNS ne change pas tout comportement de routage du courrier électronique ou d’hébergement web.

Pour plus d’informations cet ajout de l’entrée DNS hello, lire [Instructions pour l’ajout d’une entrée DNS à des bureaux d’enregistrement DNS populaires](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Vérifiez le nom de domaine hello avec Azure AD
Une fois que vous avez ajouté l’entrée DNS de hello, vous êtes prêt tooverify nom de domaine hello avec Azure AD.

Un nom de domaine peut être vérifié uniquement après la propagation des enregistrements DNS de hello. Cette propagation ne prend généralement que quelques secondes, mais peut parfois nécessiter une heure ou davantage. Si la vérification ne fonctionne pas hello première fois, réessayez plus tard.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com) avec un compte qui est un administrateur global pour le répertoire de hello.
2. Sélectionnez **Parcourir**, entrez la gestion des utilisateurs dans la zone de texte hello et sélectionnez **entrée**.
   
   ![Ouvrir la gestion des utilisateurs](./media/active-directory-domains-add-azure-portal/user-management.png)
3. Sur hello **les noms de domaine - gestion des utilisateurs** panneau, nom de domaine non vérifié hello select que vous souhaitez tooverify.
4. Sur hello ***nom de domaine*** blade (autrement dit, hello panneau qui s’ouvre contenant votre nouveau nom de domaine dans le titre de hello), sélectionnez **Vérifiez** vérification de hello toocomplete.

> [!TIP]
> Vous pouvez ajouter des noms de domaine personnalisé too900, mais une seule peut être [définir en tant que nom de domaine principal hello pour votre annuaire Azure AD](active-directory-domains-manage-azure-portal.md#set-the-primary-domain-name-for-your-azure-ad-directory) utilisé par défaut lorsque vous créez de nouveaux comptes.

Vous pouvez désormais créer des comptes d’utilisateur basés sur le cloud et mettre à jour des informations de compte d’utilisateur local précédemment synchronisées, à l’aide de votre nom de domaine personnalisé. Vous pouvez également modifier utilisateur précédemment synchronisé compte domaine suffixe informations à l’aide [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) ou hello [API Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous ne pouvez pas vérifier un nom de domaine personnalisé, essayez hello dépannage comme suit :

1. **Attendez une heure**. Enregistrements DNS doivent toopropagate Azure AD peut vérifier le domaine de hello. Cette opération peut prendre une heure ou davantage.
2. **Vérifiez hello enregistrement DNS a été entré, et qu’il est correct**. Effectuez cette étape sur le site Web de hello pour le Registre des noms de domaine pour le domaine de hello hello. Azure AD ne peut pas vérifier les nom de domaine hello si hello entrée DNS n’est pas présent Bonjour le fichier de zone DNS, ou si elle n’est pas une correspondance exacte avec l’entrée DNS de hello qu’Azure AD vous fourni. Si vous n’avez pas les enregistrements DNS de tooupdate d’accès pour le domaine hello au bureau d’enregistrement de nom de domaine hello, partager l’entrée DNS de hello avec hello personne ou une équipe de votre organisation qui possède cet accès et lui demander d’entrée DNS tooadd hello.
3. **Supprimer le nom de domaine hello à partir d’un autre annuaire dans Azure AD**. Un nom de domaine ne peut être vérifié que dans un seul annuaire. Si un nom de domaine a été précédemment vérifié dans un autre annuaire, vous devez le supprimer avant de pouvoir le vérifier dans votre nouvel annuaire. toolearn sur la suppression des noms de domaine, lire [gérer les noms de domaine personnalisé](active-directory-domains-manage-azure-portal.md).    

## <a name="add-more-custom-domain-names"></a>Ajouter des noms de domaines personnalisés
Si votre organisation utilise plusieurs noms de domaine personnalisé, tel que « contoso.com » et « contosobank.com », vous pouvez ajouter des too900 plus en répétant les étapes de hello dans cet article pour chacun.

### <a name="learn-more"></a>En savoir plus
[Présentation conceptuelle des noms de domaine personnalisés dans Azure AD](active-directory-add-domain-concepts.md)

[Gérer les noms de domaine personnalisés](active-directory-domains-manage-azure-portal.md)


## <a name="next-steps"></a>Étapes suivantes
Ce guide de démarrage rapide, vous avez appris comment tooadd un tooAzure personnalisé de domaine Active Directory. 

Vous pouvez utiliser hello suivant le lien tooadd un domaine personnalisé dans Azure AD à partir de hello portail Azure.

> [!div class="nextstepaction"]
> [Ajouter un domaine personnalisé](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/QuickStart) 