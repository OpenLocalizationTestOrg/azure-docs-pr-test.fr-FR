---
title: "aaaAdd votre nom de domaine personnalisé et de la configuration fédérée connectez-vous tooAzure Active Directory | Documents Microsoft"
description: "Comment tooadd des votre société noms de domaine tooset d’Active Directory tooAzure des connectez-vous fédérée entre Azure Active Directory et de votre solution de fédération local"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 27126c7e-e6d6-4ef3-a4fb-f5f0706e749d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/25/2017
ms.author: curtand
ms.openlocfilehash: 77f8cc87c27871ac96581360762aaa8d24c0eb8d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="add-your-custom-domain-name-tooazure-active-directory"></a>Ajouter votre tooAzure de nom de domaine personnalisé Active Directory
Vous pouvez configurer un nom de domaine personnalisé, par exemple « contoso.com », pour que les utilisateurs de contoso.com puissent disposer d’une expérience d’authentification unique fédérée à partir de votre réseau d’entreprise. Si vous avez déjà des Services de fédération Active Directory (AD FS) ou un serveur de fédération en cours d’exécution sur votre réseau d’entreprise, vous pouvez configurer votre nom de domaine personnalisé à l’aide d’outil d’Azure AD Connect hello toouse d’Azure AD. Vous pouvez également utiliser Azure AD Connect toodeploy un nouvel AD FS environnement et configurez cette option pour fédéré unique authentification tooAzure AD.

Si vous n’avez pas et que vous n’envisagez pas de toodeploy AD FS ou un autre serveur de fédération, suivez ces instructions : [ajouter un tooAzure de nom de domaine personnalisé Active Directory](active-directory-add-domain.md).

## <a name="add-a-custom-domain-name-tooyour-directory"></a>Ajouter un répertoire de tooyour de nom de domaine personnalisé
1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com/) avec un compte d’utilisateur qui est un administrateur global de votre annuaire Azure AD.
2. Dans **Active Directory**, ouvrez votre répertoire et sélectionnez hello **domaines** onglet.
3. Dans la barre de commandes hello, sélectionnez **ajouter**, puis entrez le nom hello de votre domaine personnalisé, par exemple, « contoso.com ». Être vraiment tooinclude hello .com, .net ou toute autre extension de niveau supérieur.
4. Sélectionnez hello **je prévois tooconfigure ce domaine pour l’authentification unique avec mon annuaire Active Directory local** case à cocher.
5. Sélectionnez **Ajouter**.

Exécutez l’entrée DNS de hello Azure AD Connect outil tooget hello qu’Azure AD utilise domaine de hello tooverify. Vous verrez une entrée DNS de hello Bonjour **domaine Azure AD** étape dans l’Assistant de hello. Vous pouvez voir quels cette étape dans l’Assistant hello ressemble à [dans ces instructions](connect/active-directory-aadconnect-get-started-custom.md#verify-the-azure-ad-domain-selected-for-federation). Si vous n’avez pas l’outil de hello Azure AD Connect, vous pouvez [télécharger ici](http://go.microsoft.com/fwlink/?LinkId=615771).

## <a name="add-hello-dns-entry-at-hello-domain-name-registrar-for-hello-domain"></a>Ajouter l’entrée DNS de hello au bureau d’enregistrement du nom de domaine hello pour le domaine de hello
toouse étape suivante de Hello, nom de votre domaine personnalisé avec Azure AD est un fichier de zone DNS tooupdate hello pour le domaine de hello. Cela permet de tooverify Azure AD que votre organisation possède le nom de domaine personnalisé hello.

1. Site Web de toohello pour l’enregistrement de domaines pour votre nom de domaine de connexion. Si vous n’avez pas accès toodo cela, demandez à hello personne ou une équipe dans votre organisation qui possède cette étape de toocomplete accès 2 et le toolet que vous savez lorsqu’elle est effectuée.
2. Fichier de zone de mise à jour hello DNS pour le domaine hello en ajoutant l’entrée DNS de hello fourni tooyou par Azure AD. Cette entrée DNS permet à Azure AD tooverify votre propriétaire du domaine de hello. Hello entrée DNS ne change pas tout comportement de routage du courrier électronique ou d’hébergement web.

Pour plus d’informations sur cette étape, voir [Instructions pour ajouter une entrée DNS à des Bureaux d’enregistrement DNS courants](https://support.office.com/article/Create-DNS-records-for-Office-365-when-you-manage-your-DNS-records-b0f3fdca-8a80-4e8e-9ef3-61e8a2a9ab23/)

## <a name="verify-hello-domain-name-with-azure-ad"></a>Vérifiez le nom de domaine hello avec Azure AD
Une fois que vous avez ajouté l’entrée DNS de hello, vous êtes prêt tooverify nom de domaine hello avec Azure AD.

domaine de hello tooverify, sélectionnez **suivant** sur hello **domaine Azure AD** étape de l’Assistant de connexion hello Azure AD. L’entrée DNS hello dans fichier de zone DNS hello pour le domaine de hello recherche Azure AD. Azure AD vérifier uniquement le nom de domaine hello une fois que les enregistrements DNS hello ont été propagées. La propagation ne prend généralement que quelques secondes, mais peut parfois nécessiter une heure ou davantage. Si la vérification ne fonctionne pas hello première fois, réessayez plus tard.

Ensuite, poursuivre hello restant des étapes de l’Assistant d’Azure AD Connect hello. Ceci synchronise les utilisateurs de votre tooAzure Active Directory de Windows Server Active Directory. Les utilisateurs synchronisés dans le domaine hello que vous avez configuré pour la fédération sera en mesure de tooget une seule authentification fédérée expérience à partir de votre réseau d’entreprise de tooAzure AD.

## <a name="troubleshooting"></a>Résolution des problèmes
Si vous ne pouvez pas vérifier un nom de domaine personnalisé, essayez suivante de hello. Nous allons commencer par hello plus courants et travail vers le bas toohello moins courants.

1. **Attendez une heure**. Enregistrements DNS doivent toopropagate Azure AD peut vérifier le domaine de hello. Cette opération peut prendre une heure ou davantage.
2. **Vérifiez hello enregistrement DNS a été entré, et qu’il est correct**. Effectuez cette étape sur le site Web de hello pour le Registre des noms de domaine pour le domaine de hello hello. Azure AD ne peut pas vérifier les nom de domaine hello si hello entrée DNS n’est pas présent Bonjour le fichier de zone DNS, ou si elle n’est pas une correspondance exacte avec l’entrée DNS de hello qu’Azure AD vous fourni. Si vous n’avez pas les enregistrements DNS de tooupdate d’accès pour le domaine hello au bureau d’enregistrement de nom de domaine hello, partager l’entrée DNS de hello avec hello personne ou une équipe de votre organisation qui possède cet accès et lui demander d’entrée DNS tooadd hello.
3. **Supprimer le nom de domaine hello à partir d’un autre annuaire dans Azure AD**. Un nom de domaine ne peut être vérifié que dans un seul annuaire. Si un nom de domaine a été précédemment vérifié dans un autre annuaire, vous devez le supprimer avant de pouvoir le vérifier dans votre nouvel annuaire. toolearn sur la suppression des noms de domaine, lire [gérer les noms de domaine personnalisé](active-directory-add-manage-domain-names.md).

## <a name="add-more-custom-domain-names"></a>Ajouter des noms de domaines personnalisés
Si votre organisation utilise plusieurs noms de domaines personnalisés, tels que « contoso.com » et « contosobank.com », vous pouvez les ajouter des tooa jusqu'à 900 noms de domaine. Utilisez hello même les étapes dans cette tooadd article chaque de vos noms de domaine.

## <a name="next-steps"></a>Étapes suivantes
* [Gérer les noms de domaine personnalisés](active-directory-add-manage-domain-names.md)
* [En savoir plus sur les concepts de gestion de domaine dans Azure AD](active-directory-add-domain-concepts.md)
* [Afficher la marque de votre société lorsque vos utilisateurs se connectent](active-directory-add-company-branding.md)
* [Utiliser des noms de domaine toomanage PowerShell dans Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)

