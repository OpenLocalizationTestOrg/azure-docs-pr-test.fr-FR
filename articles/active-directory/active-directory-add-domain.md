---
title: "aaaAdd tooAzure Active Directory de nom de votre domaine personnalisé | Documents Microsoft"
description: "Comment tooadd des votre société noms de domaine tooAzure Active Directory, et comment tooverify hello nom de domaine."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 35a6e20a-9907-432b-9d36-16b916a5c249
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: eb208138f2633aaecc54f68dc947caf80d856d23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-custom-domain-name-tooazure-active-directory"></a>Ajouter un tooAzure de nom de domaine personnalisé Active Directory
> [!div class="op_single_selector"]
> * [Portail Azure](active-directory-domains-add-azure-portal.md)
> * [portail Azure Classic](active-directory-add-domain.md)
> 
> 

Vous avez un ou plusieurs noms de domaine que votre organisation utilise toodo business, et que vos utilisateurs se connectent tooyour de réseau d’entreprise à l’aide de votre nom de domaine d’entreprise. Maintenant que vous utilisez Azure Active Directory (Azure AD), vous pouvez ajouter votre tooAzure de nom du domaine d’entreprise Active Directory ainsi. Cela vous permet de noms d’utilisateur tooassign dans le répertoire de hello qui sont les utilisateurs tooyour familiers, tels que «alice@contoso.com. » processus de Hello est simple :

1. Ajouter un répertoire de tooyour de nom de domaine personnalisé hello
2. Ajouter une entrée DNS pour le nom de domaine hello au bureau d’enregistrement de nom de domaine hello
3. Vérifiez le nom de domaine personnalisé hello dans Azure AD

> [!IMPORTANT]
> Microsoft recommande de gérer Azure AD en utilisant hello [centre d’administration Azure AD](https://aad.portal.azure.com) Bonjour portail Azure au lieu d’utiliser hello portail Azure classic référencée dans cet article. Pour tooadd votre nom de domaine de société dans le centre d’administration hello Azure AD, voir [attribution de rôles d’administrateur dans Azure Active Directory](active-directory-domains-add-azure-portal.md).

Si vous envisagez de tooconfigure votre toobe de nom de domaine personnalisé utilisé avec les Services de fédération Active Directory (AD FS) ou un service de jeton de sécurité (STS) sur votre réseau d’entreprise, suivez les instructions de hello dans [ajouter et configurer un domaine pour fédération avec Azure Active Directory](active-directory-add-domain-federated.md). Cela est utile si vous envisagez de toosynchronize utilisateurs à partir de votre annuaire d’entreprise de tooAzure AD, et [synchronisation du hachage de mot de passe](active-directory-aadconnectsync-implement-password-synchronization.md) ne répondent pas à vos besoins.

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Ajouter un répertoire de tooyour de nom de domaine personnalisé
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) avec un compte d’utilisateur qui est un administrateur global de votre annuaire Azure AD.
2. Dans **Active Directory**, ouvrez votre répertoire et sélectionnez hello **domaines** onglet.
3. Dans la barre de commandes hello, sélectionnez **ajouter**. Entrez le nom hello de votre domaine personnalisé, par exemple, « contoso.com ». Assurez-vous que tooinclude hello .com, .net ou une autre extension de niveau supérieur et laissez la case à cocher hello pour « single sign-on » (fédération) est désactivée.
4. Sélectionnez **Ajouter**.
5. Hello deuxième page de l’Assistant Ajouter un domaine de hello, obtenir hello entrée DNS que Azure AD utilise tooverify que votre organisation possède le nom de domaine personnalisé hello.

Maintenant que vous avez ajouté le nom de domaine hello, Azure AD doit vérifier que votre organisation possède le nom de domaine hello. Avant d’Azure AD peut effectuer cette vérification, vous devez ajouter une entrée DNS dans le fichier de zone DNS hello pour le nom de domaine hello. Cette tâche est effectuée sur le site Web de hello pour le bureau d’enregistrement du nom de domaine pour le nom de domaine hello.

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Ajouter l’entrée DNS de hello au bureau d’enregistrement du nom de domaine hello pour le domaine de hello
toouse étape suivante de Hello, nom de votre domaine personnalisé avec Azure AD est un fichier de zone DNS tooupdate hello pour le domaine de hello. Cela permet de tooverify Azure AD que votre organisation possède le nom de domaine personnalisé hello.

1. Se connecter dans le Registre des noms de domaine pour le domaine de hello toohello. Si vous n’avez pas hello de tooupdate accès entrée DNS, demandez à personne de hello ou équipe disposant de cette étape de toocomplete accès 2 et toolet que vous savez lorsqu’elle est effectuée.
2. Fichier de zone de mise à jour hello DNS pour le domaine hello en ajoutant l’entrée DNS de hello fourni tooyou par Azure AD. Cette entrée DNS permet à Azure AD tooverify votre propriétaire du domaine de hello. Hello entrée DNS ne change pas tout comportement de routage du courrier électronique ou d’hébergement web.

Pour plus d’informations cet ajout de l’entrée DNS hello, lire [Instructions pour l’ajout d’une entrée DNS à des bureaux d’enregistrement DNS populaires](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Vérifiez le nom de domaine hello avec Azure AD
Une fois que vous avez ajouté l’entrée DNS de hello, vous êtes prêt tooverify nom de domaine hello avec Azure AD.

Si vous avez toujours hello **ajouter un domaine** Assistant, sélectionnez Ouvrir, **Vérifiez** sur hello troisième page de hello Assistant. Lorsque vous sélectionnez **Vérifiez**, Azure AD recherchera l’entrée DNS hello dans fichier de zone DNS hello pour le domaine de hello. Azure AD peut vérifier les nom de domaine hello uniquement après la propagation des enregistrements DNS de hello. Cette propagation ne prend généralement que quelques secondes, mais peut parfois nécessiter une heure ou davantage. Si la vérification ne fonctionne pas hello première fois, réessayez plus tard.

Si hello **ajouter un domaine** Assistant n’est pas encore ouvert, vous pouvez vérifier le domaine hello Bonjour [portail Azure classic](https://manage.windowsazure.com/):

1. Connectez-vous à l’aide d’un compte d’administrateur général de votre annuaire Azure AD.
2. Ouvrez votre hello directory et sélectionnez **domaines** onglet.
3. Nom de domaine Sélectionnez hello que vous souhaitez tooverify, sélectionnez **Vérifiez** sur la barre de commandes hello.
4. Sélectionnez **Vérifiez** dans la vérification hello toocomplete hello boîte de dialogue zone.

Vous pouvez désormais [affecter des noms d’utilisateur incluant votre nom de domaine personnalisé](active-directory-add-domain-add-users.md).

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous ne pouvez pas vérifier un nom de domaine personnalisé, essayez suivante de hello. Nous allons commencer par hello plus courants et travail vers le bas toohello moins courants.

1. **Attendez une heure**. Enregistrements DNS doivent toopropagate Azure AD peut vérifier le domaine de hello. Cette opération peut prendre une heure ou davantage.
2. **Vérifiez hello enregistrement DNS a été entré, et qu’il est correct**. Effectuez cette étape sur le site Web de hello pour le Registre des noms de domaine pour le domaine de hello hello. Azure AD ne peut pas vérifier les nom de domaine hello si hello entrée DNS n’est pas présent Bonjour le fichier de zone DNS, ou si elle n’est pas une correspondance exacte avec l’entrée DNS de hello qu’Azure AD vous fourni. Si vous n’avez pas les enregistrements DNS de tooupdate d’accès pour le domaine hello au bureau d’enregistrement de nom de domaine hello, partager l’entrée DNS de hello avec hello personne ou une équipe de votre organisation qui possède cet accès et lui demander d’entrée DNS tooadd hello.
3. **Supprimer le nom de domaine hello à partir d’un autre annuaire dans Azure AD**. Un nom de domaine ne peut être vérifié que dans un seul annuaire. Si un nom de domaine a été précédemment vérifié dans un autre annuaire, vous devez le supprimer avant de pouvoir le vérifier dans votre nouvel annuaire. toolearn sur la suppression des noms de domaine, lire [gérer les noms de domaine personnalisé](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Ajouter des noms de domaines personnalisés
Si votre organisation utilise plusieurs noms de domaines personnalisés, tels que « contoso.com » et « contosobank.com », vous pouvez les ajouter des tooa jusqu'à 900 noms de domaine. Utilisez hello même les étapes dans cette tooadd article chaque de vos noms de domaine.

## <a name="next-steps"></a>Étapes suivantes
* [Affecter des noms d’utilisateur qui incluent votre nom de domaine personnalisé](active-directory-add-domain-add-users.md)
* [Gérer les noms de domaine personnalisés](active-directory-add-manage-domain-names.md)
* [En savoir plus sur les concepts de gestion de domaine dans Azure AD](active-directory-add-domain-concepts.md)
* [Afficher la marque de votre société lorsque vos utilisateurs se connectent](active-directory-add-company-branding.md)
* [Utiliser des noms de domaine toomanage PowerShell dans Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

