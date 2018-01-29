---
title: "Décisions de déploiement connecté à Azure pour les systèmes intégrés Azure Stack | Microsoft Docs"
description: "Déterminez les décisions relatives à la planification du déploiement pour les déploiements à plusieurs nœuds de Azure Stack connectés à Azure."
services: azure-stack
documentationcenter: 
author: jeffgilb
manager: femila
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/16/2018
ms.author: jeffgilb
ms.reviewer: wfayed
ms.openlocfilehash: c1a3b2107abdc3ef19a314616518c494687d81bf
ms.sourcegitcommit: 5108f637c457a276fffcf2b8b332a67774b05981
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 01/17/2018
---
# <a name="azure-connected-deployment-planning-decisions-for-azure-stack-integrated-systems"></a>Décisions relatives à la planification du déploiement connecté à Azure pour les systèmes intégrés Azure Stack
Une fois que vous avez décidé [comment vous allez intégrer Azure Stack dans votre environnement de cloud hybride](azure-stack-deployment-decisions.md), vous pouvez finaliser vos décisions de déploiement de Azure Stack.

Un déploiement connecté de Azure Stack à Azure signifie que vous pouvez sélectionner Azure Active Directory (Azure AD) ou les services de fédération Active Directory (AD FS) comme magasin d’identités. Vous pouvez également choisir entre un modèle de facturation à l’utilisation ou un modèle de facturation selon la capacité. Le déploiement connecté constitue l’option par défaut car il permet aux clients de tirer le meilleur parti de Azure Stack, en particulier pour les scénarios de cloud hybride impliquant à la fois Azure et Azure Stack. 

## <a name="choose-an-identity-store"></a>Choisir un magasin d’identités
Dans le cas d’un déploiement connecté, vous pouvez choisir Azure AD ou AD FS comme magasin d’identités. Dans le cas d’un déploiement déconnecté, sans connexion Internet, vous ne pouvez utiliser que AD FS.

Le choix du magasin d’identités n’a aucune incidence sur les machines virtuelles de locataire. Les machines virtuelles de locataire peuvent choisir le magasin d’identités auquel elles seront connectées en fonction de leur configuration : Azure AD, Windows Server Active Directory joint à un domaine, groupe de travail, etc. Cela n’a aucun lien avec le choix du fournisseur d’identités Azure Stack. 

Par exemple, vous pourrez toujours déployer des machines virtuelles de locataire IaaS en plus de Azure Stack et les joindre à un domaine Active Directory d’entreprise afin d’accéder aux comptes associés. Vous n’êtes pas obligé d’utiliser le magasin d’identités Azure AD que vous sélectionnez ici pour ces comptes.

### <a name="azure-ad-identity-store"></a>Magasin d’identités Azure AD
Lorsque vous utilisez Azure AD comme magasin d’identités, vous avez besoin de deux comptes Azure AD : un compte administrateur général et un compte de facturation. Ces comptes peuvent être les mêmes comptes ou des comptes distincts. S’il est plus facile et pratique d’utiliser le même compte d’utilisateur lorsque vous disposez d’un nombre limité de comptes Azure, il sera parfois nécessaire d’utiliser deux comptes pour répondre aux besoins de votre entreprise :

1. **Compte administrateur général** (requis uniquement pour les déploiements connectés). Ce compte Azure est utilisé pour créer des applications et des principaux de service pour les services d’infrastructure Azure Stack dans Azure Active Directory. Ce compte doit disposer d’autorisations d’administrateur de répertoire pour le répertoire dans lequel vous allez déployer votre système Azure Stack. Il deviendra l’administrateur général de l’opérateur cloud pour le locataire Azure AD et sera utilisé : 
    - Pour provisionner et déléguer des applications et des principaux de service pour tous les services Azure Stack qui doivent interagir avec Azure Active Directory et l’API Graph. 
    - Comme compte de l’administrateur de service. Il s’agit du propriétaire de l’abonnement du fournisseur par défaut (vous pouvez modifier ce paramètre ultérieurement). Vous pouvez vous connecter au portail d’administration Azure Stack à l’aide de ce compte et vous pouvez l’utiliser pour créer des offres et des plans, définir des quotas et effectuer d’autres fonctions d’administration dans Azure Stack.
2. **Compte de facturation** (requis pour les déploiements connectés et déconnectés). Ce compte Azure est utilisé pour établir la relation de facturation entre votre système Azure Stack intégré et le serveur principal Azure Commerce. Il s’agit du compte sur lequel seront facturés les frais relatifs à Azure Stack. Ce compte sera également utilisé pour la syndication de marketplace et d’autres scénarios hybrides. 

### <a name="ad-fs-identity-store"></a>MAGASIN D’IDENTITÉS AD FS
Choisissez cette option si vous souhaitez utiliser votre propre magasin d’identités, tel que votre instance Active Directory d’entreprise, pour vos comptes d’administrateur de service.  

## <a name="choose-a-billing-model"></a>Choisir un modèle de facturation
Vous pouvez choisir un modèle de facturation **à l’utilisation** ou **selon la capacité**. Les déploiements avec modèle de facturation à l’utilisation impliquent l’envoi d’un rapport d’utilisation via une connexion à Azure au moins une fois tous les 30 jours. Par conséquent, si aucune connexion n’est possible, le modèle de facturation selon la capacité est la seule option disponible. 

### <a name="pay-as-you-use"></a>Facturation à l’utilisation
Avec le modèle de facturation à l’utilisation, les ressources utilisées sont facturées sur un abonnement Azure. Vous payez uniquement lorsque vous utilisez les services Azure Stack. Si vous choisissez ce modèle, vous aurez besoin d’un abonnement Azure et de l’ID de compte associé à cet abonnement (par exemple, serviceadmin@contoso.onmicrosoft.com). Les abonnements EA, CSP et CSL sont pris en charge. Le rapport d’utilisation est configuré lors de [l’inscription de Azure Stack](azure-stack-registration.md).

> [!NOTE]
> Dans la plupart des cas, les entreprises utiliseront des abonnements EA et les fournisseurs de services utiliseront des abonnements CSP ou CSL.

Si vous vous apprêtez à utiliser un abonnement CSP, consultez le tableau ci-dessous pour savoir quel abonnement CSP utiliser en fonction de votre situation :

|Scénario|Domaine et options d'abonnement|
|-----|-----|
|Vous êtes un partenaire CSP direct ou indirect et vous allez déployer Azure Stack|Utilisez un abonnement CSL (Common Service Layer).|
|Vous êtes un partenaire CSP direct ou indirect et vous allez déployer Azure Stack|Dans l’Espace Partenaires, créez un locataire Azure AD avec un nom descriptif, par exemple <your organization>CSPAdmin, et un abonnement CSP Azure associé.|
|Vous êtes un revendeur CSP indirect et vous allez déployer Azure Stack|Demandez à votre fournisseur CSP indirect de créer, dans l’Espace Partenaires, un locataire Azure AD pour votre entreprise, ainsi qu’un abonnement CSP Azure associé.|

### <a name="capacity-based-billing"></a>Facturation selon la capacité
Si vous décidez d’utiliser le modèle de facturation selon la capacité, vous devez acheter une référence (SKU) de plan de capacité Azure Stack correspondant à la capacité de votre système. Vous devrez connaître le nombre de cœurs physiques composant votre système Azure Stack pour pouvoir acheter la quantité appropriée. 

La facturation selon la capacité nécessite un abonnement Azure EA (Enterprise Agreement) à des fins d’inscription. Cela s’explique par le fait que l’inscription configure la syndication, ce qui requiert un abonnement Azure. L’abonnement n’est pas utilisé pour l’utilisation de Azure Stack.

## <a name="learn-more"></a>En savoir plus
- Pour plus d’informations sur les cas d’usage, l’achat, les partenaires et les fabricants de matériel OEM, consultez la page produit [Azure Stack](https://azure.microsoft.com/overview/azure-stack/).
- Pour plus d’informations sur la feuille de route et la disponibilité géographique des systèmes intégrés Azure Stack, consultez le livre blanc : [Azure Stack : une extension de Azure](https://azure.microsoft.com/resources/azure-stack-an-extension-of-azure/). 
- Pour en savoir plus sur l’empaquetage et la tarification de Microsoft Azure Stack, [téléchargez le fichier PDF](https://azure.microsoft.com/mediahandler/files/resourcefiles/5bc3f30c-cd57-4513-989e-056325eb95e1/Azure-Stack-packaging-and-pricing-datasheet.pdf). 
