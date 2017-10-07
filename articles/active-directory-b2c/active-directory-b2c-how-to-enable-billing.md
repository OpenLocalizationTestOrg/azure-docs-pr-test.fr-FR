---
title: aaaHow tooLink un tooAzure abonnement Azure AD B2C | Documents Microsoft
description: "Guide pas à pas tooenable facturation pour Azure AD B2C locataire dans un abonnement Azure."
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>Liaison d’un toopay de locataire abonnement Azure tooan Azure B2C frais d’utilisation

Frais d’utilisation actuelles pour Azure Active Directory B2C (ou Azure AD B2C) sont facturé tooan abonnement Azure. Il est nécessaire pour hello client administrateur tooexplicitly lien hello Azure AD B2C locataire tooan abonnement Azure après la création du locataire hello B2C lui-même.  Ce lien est obtenu en créant un répertoire Azure AD « Tenant B2C » ressources dans la cible de hello abonnement Azure. Plusieurs clients B2C peuvent être lié tooa seul abonnement Azure, ainsi que d’autres ressources Windows Azure (par exemple, machines virtuelles, stockage de données, LogicApps)


> [!IMPORTANT]
> Hello les dernières informations sur l’utilisation de facturation et la tarification pour B2C est à hello suivant page : [tarification d’Azure AD B2C](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>Étape 1 - Création d’un client Azure AD B2C
Le client B2C doit être créé en premier. Ignorez cette étape si vous avez déjà créé votre client B2C. [Prise en main d’Azure Active Directory B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>Étape 2 : ouvrir le portail Azure Bonjour client Azure AD qui affiche votre abonnement Azure
Accédez toohello [portail Azure](https://portal.azure.com). Commutateur toohello client Azure AD qui affiche hello abonnement Azure que vous aimeriez toouse. Ce client Azure AD est différent de client de B2C hello. Hello portail Azure, sur, cliquez sur le nom de compte hello sur hello coin supérieur droit de hello tooselect de tableau de bord hello client Azure AD. Un abonnement Azure est tooproceed nécessaire. [Obtenir un abonnement Azure](https://account.windowsazure.com/signup?showCatalog=True)

![Commutation tooyour client Azure AD](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>Étape 3 - Création d’une ressource Client B2C dans Azure Marketplace
Ouvrez Marketplace en cliquant sur hello Marketplace icône, ou en sélectionnant hello vert « + » dans hello coin supérieur gauche du tableau de bord hello.  Recherchez et sélectionnez Azure Active Directory B2C. Sélectionnez Créer.

![Sélectionnez Place de marché](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![Rechercher AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

Hello Azure AD B2C ressources créez hello couvre de boîte de dialogue paramètres suivants :

1. Azure AD B2C client – Sélectionnez un locataire Azure AD B2C à partir de la liste déroulante de hello.  Seuls les clients Azure AD B2C éligibles s’affichent.  Les clients éligibles B2C remplissent ces conditions : vous êtes administrateur global de hello du client de hello B2C et client de hello B2C n’est pas associé actuellement tooan abonnement Azure

2. Nom de ressource de AD B2C Azure - désigne toomatch présélectionnées hello domaine hello B2C locataire

3. Abonnement - Il s’agit d’un abonnement Azure actif dans lequel vous êtes un administrateur ou un coadministrateur.  Tooone abonnement Azure peuvent être ajoutés à plusieurs locataires Azure AD B2C

4. Groupe de ressources et emplacement du groupe de ressources - Cet artefact vous permet d’organiser plusieurs ressources Azure.  Ce choix n’a aucun impact sur l’emplacement, les performances ou l’état de facturation du client B2C.

5. Épingler toodashboard pour le client de tooyour B2C accès plus facile et les paramètres client B2C hello et les informations de facturation ![créer une ressource B2C](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>Étape 4 - Gestion de vos ressources Client B2C (facultatif)
Une fois le déploiement terminé, une nouvelle ressource de « Tenant B2C » est créée dans le groupe de ressources cible hello et associées d’abonnement Azure.  Une nouvelle ressource de type « Client B2C » s’affiche à côté de vos autres ressources Azure.

![Créer une ressource B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

En cliquant sur des ressources du locataire hello B2C, vous ne pourrez
- Cliquez sur nom tooreview vos informations de facturation. (consultez Facturation et utilisation) ;
- Cliquez sur paramètres d’Azure AD B2C tooopen un nouvel onglet de navigateur directement dans le locataire tooyour B2C panneau des paramètres
- envoyer une demande de support ;
- Déplacez votre tooanother de ressource client B2C abonnement Azure ou tooanother groupe de ressources.  Ce choix modifie l’abonnement Azure qui reçoit les frais d’utilisation.

![Paramètres de ressource B2C](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>Problèmes connus
- Suppression d’un locataire B2C. Si un client B2C est créé, supprimé et recréé avec hello du même nom de domaine, Veuillez également supprimer et recréer ressource « Liaison » hello hello même nom de domaine.  Vous la trouverez « Liaison « ressource « sous « toutes les ressources dans le locataire d’abonnement hello via hello portail Azure.
- Restrictions auto-imposées sur l’emplacement des ressources régionales.  Dans de rares cas, un utilisateur peut avoir établi une restriction régionale pour la création de ressources Azure.  Cette restriction peut empêcher la création de hello Hello lien entre un abonnement Azure et un client B2C. toomitigate, veuillez assouplir cette restriction.

## <a name="next-steps"></a>Étapes suivantes
Une fois ces étapes effectuées pour chacun de vos clients B2C, votre abonnement Azure est facturé conformément aux détails de votre contrat Azure Direct ou Enterprise.
- Consulter l’utilisation et la facturation dans l’abonnement Azure sélectionné
- Passez en revue les rapports d’utilisation par jour détaillées à l’aide de hello [API de création de rapports d’utilisation](active-directory-b2c-reference-usage-reporting-api.md)
