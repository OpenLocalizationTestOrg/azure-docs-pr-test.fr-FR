---
title: "aaaAdmins gérer les utilisateurs et périphériques - l’authentification Multifacteur Azure | Documents Microsoft"
description: "Cette section décrit comment toochange les paramètres utilisateur tels que forcer hello utilisateurs toodo hello processus preuve à nouveau."
documentationcenter: 
services: multi-factor-authentication
author: kgremban
manager: femila
ms.assetid: aac3b922-7cc1-428c-9044-273579aa7b5a
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 8c35435e4f6504014d9a4f6f1b837639c3b53481
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-user-settings-with-azure-multi-factor-authentication-in-hello-cloud"></a>Gérer les paramètres de l’utilisateur avec Azure multi-Factor Authentication dans le cloud de hello
En tant qu’administrateur, vous pouvez gérer hello suivant les paramètres utilisateur et périphérique :

* Exiger des méthodes de contact tooprovide les utilisateurs à nouveau
* Supprimer des mots de passe d’application
* Exiger l’authentification MFA sur tous les appareils de confiance 

## <a name="require-users-tooprovide-contact-methods-again"></a>Exiger des méthodes de contact tooprovide les utilisateurs à nouveau
Ce paramètre oblige le processus d’inscription hello hello utilisateur toocomplete à nouveau. Les applications sans navigateur continuent toowork si utilisateur de hello possède des mots de passe d’application pour eux.  Vous pouvez supprimer des mots de passe d’application aux utilisateurs hello en choisissant **supprimer mots de passe d’application existant toutes générées par les utilisateurs de hello sélectionné**.

### <a name="how-toorequire-users-tooprovide-contact-methods-again"></a>Comment toorequire utilisateurs tooprovide méthodes de contact à nouveau
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur hello gauche, sélectionnez **Azure Active Directory** > **utilisateurs et groupes** > **tous les utilisateurs**.
3. Sélectionnez **Multi-Factor Authentication**. page de l’authentification multifacteur Hello s’ouvre. 
4. Vérifiez hello boîte suivant toohello ou les utilisateurs que vous souhaitez toomanage. Une liste d’options d’étape rapide apparaissent sur hello droite. 
5. Sélectionnez **Gérer les paramètres utilisateur**.
6. Case de hello pour **obliger les utilisateurs sélectionnés à nouveau des méthodes de contact de tooprovide**.
   ![Fournir des méthodes de contact](./media/multi-factor-authentication-manage-users-and-devices/reproofup.png)
7. Cliquez sur **save**.
8. Cliquez sur **Fermer**.

## <a name="delete-users-existing-app-passwords"></a>Supprimer les mots de passe d’application existants des utilisateurs
Ce paramètre supprime tous les hello application des mots de passe un utilisateur a créé. Les applications sans navigateur qui ont été associées à ces mots de passe d’application cessent de fonctionner jusqu’à la création d’un nouveau mot de passe d’application.

### <a name="how-toodelete-users-existing-app-passwords"></a>Comment les utilisateurs toodelete existante des mots de passe d’application
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur hello gauche, sélectionnez **Azure Active Directory** > **utilisateurs et groupes** > **tous les utilisateurs**.
3. Sélectionnez **Multi-Factor Authentication**. page de l’authentification multifacteur Hello s’ouvre. 
6. Vérifiez hello boîte suivant toohello ou les utilisateurs que vous souhaitez toomanage. Une liste d’options d’étape rapide apparaissent sur hello droite. 
7. Sélectionnez **Gérer les paramètres utilisateur**.
8. Case de hello pour **supprimer mots de passe d’application existant toutes générées par les utilisateurs de hello sélectionné**.
   ![Supprimer des mots de passe d'application](./media/multi-factor-authentication-manage-users-and-devices/deleteapppasswords.png)
9. Cliquez sur **save**.
10. Cliquez sur **Fermer**.

## <a name="restore-mfa-on-all-remembered-devices-for-a-user"></a>Restaurer MFA sur tous les appareils mémorisés d’un utilisateur
Une des fonctionnalités configurables de hello d’Azure multi-Factor Authentication est distribution périphériques de toomark option hello un niveau de confiance à vos utilisateurs. Pour plus d’informations, consultez [Configurer les paramètres d’Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md#remember-multi-factor-authentication-for-devices-that-users-trust).

Les utilisateurs peuvent refuser la vérification en deux étapes pendant un nombre configurable de jours sur les appareils qu’ils utilisent régulièrement. Si un compte est compromis, ou un périphérique de confiance est perdu, vous devez les toobe tooremove en mesure de hello approuvé état et exiger la vérification en deux étapes à nouveau.

Hello **restaurer l’authentification multifacteur sur tous les appareils mémorisés** paramètre signifie que l’utilisateur hello sera hello de vérification en deux étapes récusé tooperform leur prochaine connexion, quel que soit le qu’ils ont choisi toomark leurs périphérique un niveau de confiance. 

### <a name="how-toorestore-mfa-on-all-suspended-devices-for-a-user"></a>Comment toorestore l’authentification Multifacteur sur tous les appareils suspendus pour un utilisateur
1. Connectez-vous à toohello [portail Azure](https://portal.azure.com).
2. Sur hello gauche, sélectionnez **Azure Active Directory** > **utilisateurs et groupes** > **tous les utilisateurs**.
3. Sélectionnez **Multi-Factor Authentication**. page de l’authentification multifacteur Hello s’ouvre. 
6. Vérifiez hello boîte suivant toohello ou les utilisateurs que vous souhaitez toomanage. Une liste d’options d’étape rapide apparaissent sur hello droite. 
7. Sélectionnez **Gérer les paramètres utilisateur**.
8. Case de hello pour **restaurer l’authentification multifacteur sur tous les appareils mémorisés**
   ![supprimer des mots de passe d’application](./media/multi-factor-authentication-manage-users-and-devices/rememberdevices.png)
9. Cliquez sur **save**.
10. Cliquez sur **Fermer**.

## <a name="next-steps"></a>Étapes suivantes

- Obtenir plus d’informations sur la façon de trop[les paramètres de configuration de l’authentification multifacteur Azure](multi-factor-authentication-whats-next.md)

- Si vos utilisateurs ont besoin d’aide, faire pointer vers hello [guide de l’utilisateur pour la vérification en deux étapes](./end-user/multi-factor-authentication-end-user.md)
