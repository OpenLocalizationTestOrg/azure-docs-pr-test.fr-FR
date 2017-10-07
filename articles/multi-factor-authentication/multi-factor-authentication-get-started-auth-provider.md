---
title: "aaaGet a démarré le fournisseur d’authentification multifacteur Azure | Documents Microsoft"
description: "Découvrez comment toocreate un fournisseur de d’authentification multifacteur Azure."
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: a7dd5030-7d40-4654-8fbd-88e53ddc1ef5
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/28/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: 00ea967a80b43baff38c1de586c54d95c9abac2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-an-azure-multi-factor-auth-provider"></a>Prise en main du fournisseur Azure Multi-Factor Auth
La vérification en deux étapes est disponible par défaut pour les administrateurs généraux disposant d’Azure Active Directory et les utilisateurs Office 365. Toutefois, si vous le souhaitez parti tootake de [fonctionnalités avancées](multi-factor-authentication-whats-next.md) puis vous devez acheter la version complète de hello d’Azure multi-Factor Authentication (MFA).

Un fournisseur de d’authentification multifacteur Azure sert parti tootake des fonctionnalités offertes par la version complète de hello de l’authentification Multifacteur Azure. Il s’adresse aux utilisateurs **qui ne possèdent pas de licences via l’authentification multifacteur Azure (MFA), Azure AD Premium ou Enterprise Mobility + Security (EMS)**.  Azure MFA, Azure AD Premium et EMS incluent la version de hello complète de l’authentification Multifacteur Azure par défaut. Vous n’avez pas besoin d’un fournisseur d’authentification multifacteur Azure si vous possédez des licences.

Un fournisseur Azure multi-Factor Authentication est le hello toodownload requis Kit de développement logiciel.

> [!IMPORTANT]
> toodownload hello du Kit de développement logiciel, vous devez toocreate un fournisseur de d’authentification multifacteur Azure, même si vous disposez de licences Azure MFA, AAD Premium ou EMS.  Si vous créez un fournisseur d’authentification d’Azure multi-Factor à cet effet et que vous avez déjà des licences, être hello toocreate que fournisseur par hello **par utilisateur activé** modèle. Ensuite, liez hello fournisseur toohello répertoire qui contient les licences Azure MFA, Azure AD Premium ou EMS hello. Cette configuration garantit que vous êtes facturé uniquement si vous avez plusieurs utilisateurs uniques en deux étapes de vérification que nombre hello de licences que vous possédez.

## <a name="what-is-an-azure-multi-factor-auth-provider"></a>Qu’est-ce qu’un fournisseur Azure Multi-Factor Auth ?

Si vous ne disposez des licences pour Azure multi-Factor Authentication, vous pouvez créer une vérification en deux étapes de toorequire du fournisseur d’authentification pour vos utilisateurs. Si vous développez une application personnalisée et que vous souhaitez tooenable Azure MFA, créer un fournisseur d’authentification et [télécharger hello SDK](multi-factor-authentication-sdk.md).

Il existe deux types de fournisseurs d’authentification et distinction de hello est autour de la façon dont votre abonnement Azure est facturé. option d’authentification par Hello calcule nombre hello d’authentifications effectuées par rapport à votre client dans un mois. Cette option est recommandée si de nombreux utilisateurs ne s’authentifient qu’occasionnellement (par exemple, si vous avez besoin de MFA pour une application personnalisée). option de par l’utilisateur de Hello calcule nombre hello d’individus effectuer la vérification en deux étapes d’un mois dans votre client. Cette option est préférable si vous disposez d’utilisateurs dont les licences, mais les utilisateurs de toomore tooextend MFA au-delà des limites de votre licences.

## <a name="create-a-multi-factor-auth-provider"></a>Créer un fournisseur Multi-Factor Authentication
Utilisez hello suivant les étapes toocreate un fournisseur de d’authentification multifacteur Azure. Les fournisseurs d’authentification multifacteur Azure peuvent être créés uniquement dans hello portail Azure classic. Si vous ne pouvez pas connecter toohello portail Azure classic, vérifiez toomake assurer que votre client Azure AD est [associé à un abonnement Azure](../active-directory/active-directory-how-subscriptions-associated-directory.md). 

1. Connectez-vous à toohello [portail Azure classic](https://manage.windowsazure.com) en tant qu’administrateur.
2. Sur hello gauche, sélectionnez **Active Directory**.
3. Sur la page Active Directory hello, en haut hello, sélectionnez **fournisseurs d’authentification multifacteur**.
   
   ![Création d’un fournisseur d’authentification Multifacteur](./media/multi-factor-authentication-get-started-auth-provider/authprovider1.png)

4. Au bas de hello, cliquez sur **nouveau**.
   
   ![Création d’un fournisseur d’authentification Multifacteur](./media/multi-factor-authentication-get-started-auth-provider/authprovider2.png)

5. Sous App Services, sélectionnez **Fournisseur d’authentification multifacteur**
   
   ![Création d’un fournisseur d’authentification Multifacteur](./media/multi-factor-authentication-get-started-auth-provider/authprovider3.png)

6. Sélectionnez **Création rapide**.
   
   ![Création d’un fournisseur d’authentification Multifacteur](./media/multi-factor-authentication-get-started-auth-provider/authprovider4.png)

7. Renseignez hello suivant des champs, sélectionnez **créer**.
   1. **Nom** hello – nom du fournisseur d’authentification multifacteur de hello.
   2. **Modèle d’utilisation** : vous pouvez choisir l’une des deux options suivantes :
      * Par authentification – modèle d'achat facturé par authentification. Généralement utilisé pour les scénarios qui utilisent Azure Multi-Factor Authentication dans une application orientée client.
      * Par utilisateur activé – modèle d'achat facturé par utilisateur activé. Généralement utilisé pour tooapplications d’accès employé tels qu’Office 365. Choisissez cette option si vous avez des utilisateurs qui disposent déjà d’une licence pour l’authentification multifacteur Azure.
   3. **Répertoire** – hello Azure Active Directory de locataire que hello fournisseur d’authentification multifacteur est associé. Tenez compte des éléments suivants de hello :
      * Vous n’avez pas besoin d’un toocreate de répertoire Azure AD un fournisseur d’authentification multifacteur. Laissez cette zone vide si vous envisagez uniquement hello de toodownload serveur Azure multi-Factor Authentication ou le Kit de développement logiciel.
      * Hello fournisseur d’authentification multifacteur doit être associé à Azure AD directory tootake présente l’avantage de hello fonctionnalités avancées.
      * Un seul fournisseur Multi-Factor Auth peut être associé à un répertoire Azure AD.  
      ![Création d’un fournisseur d’authentification Multifacteur](./media/multi-factor-authentication-get-started-auth-provider/authprovider5.png)

8. Une fois que vous cliquez sur Créer, hello fournisseur d’authentification multifacteur est créé et que vous devez voir un message indiquant : **créé avec succès le fournisseur d’authentification multifacteur**. Cliquez sur **OK**.  
   
   ![Création d’un fournisseur d’authentification Multifacteur](./media/multi-factor-authentication-get-started-auth-provider/authprovider6.png)  

## <a name="manage-your-multi-factor-auth-provider"></a>Gérer votre fournisseur Multi-Factor Auth

Vous ne pouvez pas modifier l’utilisation de hello de modèle (par utilisateur activé ou par authentification) après avoir créé un fournisseur d’authentification Multifacteur. Toutefois, vous pouvez supprimer le fournisseur d’authentification Multifacteur hello et puis créer un avec un modèle d’utilisation différentes.

Si hello le fournisseur d’authentification multifacteur actuel est associé à un annuaire Azure AD (également appelé un locataire Azure AD), vous pouvez en toute sécurité supprimer le fournisseur d’authentification Multifacteur hello et créez-en un qui est lié toohello AD Azure même client. Si vous avez acheté suffisamment l’authentification Multifacteur, du Azure AD Premium, ou de l’entrepôt Enterprise Mobility + Security (EMS) licences toocover tous les utilisateurs qui sont activés pour l’authentification Multifacteur, vous pouvez également supprimer fournisseur d’authentification Multifacteur hello complètement.

Si votre fournisseur d’authentification Multifacteur n’est pas lié tooan Azure AD client, ou vous liez hello nouveau MFA fournisseur tooa AD Azure autre client, les paramètres utilisateur et les options de configuration ne sont pas transférées. En outre, les serveurs de l’authentification Multifacteur Azure existants doive toobe réactivé à l’aide des informations d’identification d’activation générées par le biais hello nouveau fournisseur d’authentification Multifacteur. Réactivation hello serveurs MFA toolink les toohello nouveau fournisseur d’authentification Multifacteur n’affecte pas l’appel téléphonique et l’authentification des messages texte, mais les applications mobiles notifications cessera de fonctionner pour tous les utilisateurs jusqu'à ce qu’ils réactiver l’application mobile hello.

## <a name="next-steps"></a>Étapes suivantes

[Télécharger hello SDK multi-Factor Authentication](multi-factor-authentication-sdk.md)

[Configurer les paramètres d’Azure Multi-Factor Authentication](multi-factor-authentication-whats-next.md)
