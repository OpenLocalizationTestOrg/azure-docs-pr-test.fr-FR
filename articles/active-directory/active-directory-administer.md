---
title: "aaaHow toouse une vue d’ensemble du répertoire de client Direcory Directory de Azure | Documents Microsoft"
description: "Explique ce qu’un locataire Azure AD est et comment toomanage Azure à l’aide d’Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/23/2017
ms.author: curtand
ms.reviewer: jeffsta
ms.custom: it-pro;oldportal
ms.openlocfilehash: ddb16d89bf06a3753ed5106bd95162130ad51b08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-your-azure-ad-directory"></a>Gérer votre répertoire Azure AD

## <a name="what-is-an-azure-ad-tenant"></a>Qu'est-ce qu'un locataire Azure AD ?
Dans Azure Active Directory (Azure AD), un locataire est une instance dédiée d’un répertoire Azure AD reçue par votre organisation lorsqu’elle s’inscrit à un service cloud de Microsoft tel qu’Azure ou Office 365. Chaque annuaire Azure AD est distinct et indépendant des autres annuaires Azure AD. Comme un immeuble de bureaux d’entreprise est un tooonly spécifique de ressource sécurisée de votre organisation, un annuaire Azure AD est également conçu toobe une ressource sécurisée pour une utilisation par votre entreprise. Hello architecture, Azure AD isole les informations de données et l’identité du client afin que les utilisateurs et les administrateurs d’un annuaire Azure AD ne peut pas par accident ou malveillance accéder aux données dans un autre répertoire.

![Gérer Azure Active Directory](./media/active-directory-administer/aad_portals.png)

## <a name="how-can-i-get-an-azure-ad-directory"></a>Comment puis-je obtenir un annuaire Azure AD ?
Azure AD fournit hello core annuaire et identité derrière la plupart des services de cloud de Microsoft, y compris les fonctionnalités de gestion :

* Microsoft Azure
* Microsoft Office 365
* Microsoft Dynamics CRM Online
* Microsoft Intune

Quand vous vous inscrivez à ces services cloud Microsoft, vous obtenez un annuaire Azure AD. Vous pouvez créer des annuaires supplémentaires en fonction des besoins. Par exemple, vous pouvez mettre à jour votre premier annuaire en tant qu’annuaire de production, puis créer un autre annuaire pour les tests ou l’environnement intermédiaire.

### <a name="using-hello-azure-ad-directory-that-comes-with-a-new-azure-subscription"></a>À l’aide de hello Windows Azure AD qui est fourni avec un nouvel abonnement Azure

Nous vous recommandons d’utiliser compte d’administrateur hello que vous avez utilisé pour votre premier service lorsque vous vous inscrivez pour d’autres services Microsoft. les informations que vous fournissez Hello hello première fois que vous vous inscrivez pour un service Microsoft est utilisé toocreate un nouvel Azure instance d’annuaire Active Directory pour votre organisation. Si vous utilisez que directory tooauthenticate tentatives de connexion lorsque vous vous abonnez tooother Microsoft services, ils peuvent utiliser hello des comptes d’utilisateur existants, de stratégies, paramètres ou intégration d’annuaire local que vous configurez dans votre répertoire par défaut.

Par exemple, si vous inscrire pour obtenir un abonnement Microsoft Intune et puis plus synchronisez votre annuaire Active Directory local avec votre annuaire Azure AD, vous pouvez inscrire un autre service Microsoft tels qu’Office 365 et facilement obtenir hello même répertoire avantages de l’intégration avec Microsoft Intune.

Pour plus d’informations sur l’intégration de votre annuaire local à Azure AD, consultez [Intégration de répertoire avec Azure AD Connect](active-directory-aadconnect.md).

### <a name="associate-an-existing-azure-ad-directory-with-a-new-azure-subscription"></a>Associer un annuaire Azure AD à un nouvel abonnement Azure
Vous pouvez associer un nouvel abonnement Azure hello même annuaire qui authentifie la connexion dans un abonnement Office 365 ou Microsoft Intune existant. Pour plus d’informations sur ce scénario, consultez [transférer la propriété d’un compte de tooanother abonnement Azure](../billing/billing-subscription-transfer.md)

### <a name="create-an-azure-ad-directory-by-signing-up-for-a-microsoft-cloud-service-as-an-organization"></a>Création d’un annuaire Azure AD en vous inscrivant à un service cloud Microsoft en tant qu’organisation
Si vous n’avez pas encore un tooa abonnement service cloud Microsoft, vous pouvez utiliser une des hello suivre des liens toosign. Un annuaire Azure AD est créé automatiquement dès votre inscription à un premier service.

* [Microsoft Azure](https://account.azure.com/organization)
* [Office 365](http://products.office.com/business/compare-office-365-for-business-plans/)
* [Microsoft Intune](https://portal.office.com/Signup/Signup.aspx?OfferId=40BE278A-DFD1-470a-9EF7-9F2596EA7FF9&dl=INTUNE_A&ali=1#0%20)

### <a name="how-toochange-hello-default-directory-for-a-subscription"></a>Comment toochange hello répertoire par défaut pour un abonnement

1. Connectez-vous à toohello [centre des comptes Azure](https://account.windowsazure.com/Home/Index) avec un compte qui est administrateur de compte de la propriété de hello abonnement tootransfer abonnement de hello.
2. Vérifiez que hello utilisateur propriétaire de l’abonnement toobe hello est dans le répertoire de hello ciblé.
3. Cliquez sur **Transférer la propriété de l’abonnement**.
4. Spécifiez le destinataire de hello. destinataire de Hello obtient automatiquement un message électronique contenant un lien d’acceptation.
5. destinataire de Hello clique sur le lien de hello et suit les instructions hello, y compris comment entrer leurs informations de paiement. Destinataire de hello réussit, l’abonnement de hello est transféré. 
6. Hello répertoire par défaut de l’abonnement de hello est modifié le répertoire toohello qui hello utilisateur présente si le transfert de la propriété d’abonnement hello a réussi.

### <a name="manage-hello-default-directory-in-azure"></a>Gérer le répertoire par défaut de hello dans Azure
Lorsque vous vous inscrivez à Azure, un annuaire Azure AD par défaut est associé à votre abonnement. L’utilisation d’Azure AD n’engendre aucun coût et vos répertoires sont une ressource gratuite. Certains services Azure AD payants sont concédés sous licence distincte et fournissent des fonctionnalités supplémentaires telles que des logos à l’inscription et une réinitialisation de mot de passe en libre-service. Vous pouvez également créer un domaine personnalisé à l’aide d’un nom DNS que vous possédez au lieu de la valeur par défaut hello *. onmicrosoft.com domaine.

## <a name="how-can-i-manage-directory-data"></a>Comment puis-je gérer les données d’un répertoire ?
tooadminister un ou plusieurs abonnements de service de cloud de Microsoft, vous pouvez utiliser hello [centre d’administration Azure AD](https://aad.portal.azure.com), hello portail du compte Microsoft Intune ou hello [centre d’administration Office 365](https://portal.office.com/) toomanage votre données d’annuaire de l’organisation. Vous pouvez également utiliser [applets de commande Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory) toohelp vous gérez les données stockées dans Azure AD.

À partir de ces portails (ou applets de commande), vous pouvez :

* créer et gérer des comptes d’utilisateurs et de groupe ;
* Gérer les services cloud associés pour les abonnements de votre organisation
* Configurer l’intégration locale avec les services d’identité et d’authentification Azure AD

Centre d’administration Active Directory Azure Hello, centre d’administration Office 365, portail du compte Microsoft Intune hello applets de commande Azure AD tous lire et écrire l’instance partagée unique de tooa d’Azure AD qui est associé au répertoire de votre organisation. Chacun de ces outils agit comme une interface frontale qui extrait ou modifie vos données d’annuaire.

Lorsque vous modifiez les données de votre organisation à l’aide d’un des portails de hello ou des applets de commande en étant connecté sous un contexte hello de l’un de ces services, les modifications de hello figurent également dans hello autres portails hello la prochaine fois que vous vous connectez. Ces données sont partagées entre hello Microsoft cloud services toowhich que vous abonnez.

Par exemple, si vous utilisez hello centre d’administration Office 365 tooblock un utilisateur de se connecter, cette action bloque hello utilisateur de se connecter tooany autres toowhich service votre organisation est abonnée. Si vous affichez hello même compte d’utilisateur dans le portail du compte Microsoft Intune hello, vous consultez également que l’utilisateur hello est bloqué.

## <a name="how-can-i-add-and-manage-multiple-directories"></a>Comment puis-je ajouter et gérer plusieurs annuaires ?
Vous pouvez [ajouter un annuaire Azure AD Bonjour Azure portal](https://portal.azure.com/#create/Microsoft.AzureActiveDirectory). Remplissez les informations hello et sélectionnez **créer**.

Vous pouvez gérer chaque répertoire comme une ressource entièrement indépendante : chaque répertoire est un homologue, entièrement sélectionné et logiquement indépendant des autres répertoires que vous gérez ; il n’existe aucune relation parent-enfant entre les répertoires. Cette indépendance entre les annuaires vaut pour les ressources, l’administration et la synchronisation.

* **Indépendance des ressources**. Si vous créez ou supprimez une ressource dans un seul annuaire, il n’a aucun impact sur les ressources dans un autre répertoire, à l’exception de partielle de hello des utilisateurs externes. Si vous utilisez un domaine personnalisé (par exemple, « contoso.com ») pour un annuaire, il ne peut être utilisé avec aucun autre annuaire.
* **Indépendance de l’administration**.  Si un utilisateur qui n’est pas un administrateur de répertoire « Contoso » crée un répertoire de test « Test », alors :
  
  * les administrateurs de Hello du répertoire « Contoso » n’ont aucun toodirectory des privilèges d’administrateur direct « Test », sauf si un administrateur de « Test » leur ait spécifiquement accordé ces privilèges. Les administrateurs de « Contoso » peuvent contrôler les accès toodirectory « Test » en vertu de leur contrôle hello du compte d’utilisateur qui a créé « Test ».
    
  * Si vous affecter ou supprimer un rôle d’administrateur d’un utilisateur dans un seul annuaire, modification de hello n’affecte pas le rôle d’administrateur que l’utilisateur peut avoir dans un autre répertoire.
* **Indépendance de la synchronisation**. Vous pouvez configurer chaque Azure AD de client indépendamment des données tooget synchronisées à partir d’un outil de synchronisation d’instance unique hello Azure AD Connect active.

Contrairement aux autres ressources Azure, vos annuaires ne sont pas des ressources enfants d’un abonnement Azure. Ainsi si vous annulez ou autoriser tooexpire de votre abonnement Azure, vous pouvez toujours accéder à vos données d’annuaire à l’aide de PowerShell Azure AD, hello API Azure Graph ou autres interfaces, telles que le centre d’administration de hello Office 365. Vous pouvez également associer un autre abonnement active de hello.

## <a name="how-tooprepare-toodelete-an-azure-ad-directory"></a>Comment tooprepare toodelete un annuaire Azure AD
Un administrateur global peut supprimer un annuaire Azure AD à partir du portail de hello. Lorsqu’un répertoire est supprimé, toutes les ressources qui sont contenus dans le répertoire de hello sont également supprimés. Vérifiez qu’il ne que vous avez besoin de hello active avant de le supprimer.

> [!NOTE]
> Si l’utilisateur de hello est connecté avec un compte professionnel ou scolaire, utilisateur de hello ne doit pas essayer de toodelete leur répertoire de base. Par exemple, si hello utilisateur est connecté en tant que joe@contoso.onmicrosoft.com, cet utilisateur ne peut pas supprimer le répertoire hello ayant contoso.onmicrosoft.com comme domaine par défaut.

Azure AD nécessite que certaines conditions sont rempli toodelete un répertoire. Cela réduit le risque que la suppression d’un répertoire a un impact négatif a un impact sur les utilisateurs ou applications, telles que hello capacité de toosign utilisateurs dans tooOffice 365 ou d’accéder aux ressources dans Azure. Par exemple, si un répertoire pour un abonnement est supprimé accidentellement, les utilisateurs ne peuvent pas accéder hello ressources Azure pour cet abonnement.

Hello conditions suivantes est vérifiée :

* Hello uniquement l’utilisateur dans le répertoire de hello doit être hello administrateur global qui est le répertoire de hello toodelete. Tous les autres utilisateurs doivent être supprimés avant de pouvoir supprimer le répertoire de hello. Si les utilisateurs sont synchronisés en local, puis synchronisation doit être désactivée, et les utilisateurs de hello doivent être supprimés dans l’annuaire du cloud hello à l’aide de hello portail Azure ou des applets de commande PowerShell de Azure. Aucun groupes toodelete de spécification ou les contacts, telles que les contacts ajoutés à partir du centre d’administration hello Office 365 est.
* Il ne peut y avoir aucune application dans le répertoire de hello. Toutes les applications doivent être supprimées avant de pouvoir supprimer le répertoire de hello.
* Aucun fournisseur d’authentification multifacteur ne peut être lié toohello active.
* Il ne peut y avoir aucun abonnement pour Microsoft Online Services tels que Microsoft Azure, Office 365, ou répertoire de hello associé à Azure AD Premium. Par exemple, si un annuaire par défaut a été créé pour vous dans Azure, vous ne pouvez pas le supprimer si votre abonnement Azure utilise toujours cet annuaire à des fins d’authentification. De même, vous ne pouvez pas supprimer un répertoire auquel un autre utilisateur a associé un abonnement. 


## <a name="next-steps"></a>Étapes suivantes
* [Forum Azure AD](https://social.msdn.microsoft.com/Forums/home?forum=WindowsAzureAD)
* [Forum Azure Multi-Factor Authentication](https://social.msdn.microsoft.com/Forums/home?forum=windowsazureactiveauthentication)
* [Questions relatives à Stack Overflow pour Azure](http://stackoverflow.com/questions/tagged/azure)
* [Azure Active Directory PowerShell](https://docs.microsoft.com/powershell/azure/active-directory)
* [Attribution de rôles d’administrateur dans Azure AD](active-directory-assign-admin-roles.md)
