---
title: "technique d’aaaNon les conditions préalables requises pour la création d’une offre pour hello Azure Marketplace | Documents Microsoft"
description: "Comprendre les exigences de hello pour créer et déployer un toohello offre Azure Marketplace pour d’autres toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 3dae463b-8f48-4f52-8fa8-4e3975f09f43
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 08/18/2016
ms.author: hascipio
ms.openlocfilehash: 472096863084cc58dc921313419ab60b1a08a3bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="general-prerequisites-for-creating-an-offer-for-hello-azure-marketplace"></a>Configuration générale requise pour la création d’une offre pour hello Azure Marketplace
Comprendre hello général, orientées entreprise-processus conditions préalables qui sont nécessaire toomove vers l’avant avec hello offrent des processus de création.

## <a name="ensure-that-you-are-registered-as-a-seller-with-microsoft"></a>S’inscrire en tant que vendeur auprès de Microsoft
Pour obtenir des instructions détaillées sur l’enregistrement d’un compte vendeur avec Microsoft, consultez trop[la création et l’inscription du compte](marketplace-publishing-accounts-creation-registration.md).

* **Si votre entreprise est déjà inscrite en tant que vendeur Bonjour centre de développement et que vous souhaitez toocreate une offre,** puis connexion toohello publication portail avec hello même envoyer par courrier électronique d’id avec le centre de développement, l’inscription est terminée. Cette étape est requise afin que le centre de développement et de publication de portail hello sont liés entre eux.
* **Si votre entreprise est déjà inscrite en tant que vendeur Bonjour centre de développement et que vous souhaitez tooedit une offre existante,** puis soit toohello connexion publication portail de compte d’administrateur hello ou avec un compte qui est ajouté en tant qu’un administrateur de co Bonjour portail de publication . Étapes tooadd un compte d’administrateur de co est répertorié ci-dessous.

## <a name="steps-tooadd-a-co-admin-in-hello-publishing-portal"></a>Étapes tooadd un co-admin Bonjour portail de publication
Administrateurs de hello portail de publication peut ajouter hello d’autres membres de la société de hello, qui travaillent sur une application hello, comme un co-admin Bonjour portail de publication. **En supposant que vous êtes administrateur de hello,** ci-dessous est hello étapes tooadd un co-Admin.

> [!NOTE]
> Pour les nouveaux utilisateurs, avant d’ajouter un coadministrateur Bonjour la publication du portail, assurez-vous que vous avez créé au moins une application Bonjour portail de publication. Cela est nécessaire en tant que hello **éditeurs** onglet s’affiche seulement après avoir créé au moins une application Bonjour portail de publication.
> 
> 

1. Vérifiez que cet id de courrier électronique hello co-admin est un account(MSA) de Microsoft. Si ce n’est pas le cas, enregistrez-le comme MSA à l’aide de ce [lien](https://signup.live.com/signup?uaid=0089f09ccae94043a0f07c2aaf928831&lic=1).
2. Vérifiez qu’il existe au moins une application sous un compte d’administrateur hello avant d’essayer de tooadd un co-Admin.
3. Après avoir hello étapes ci-dessus sont effectuées, connexion toohello publication portail avec l’id de courrier électronique hello co-admin et puis fermer la session.
4. Maintenant connexion toohello portail avec l’id de courrier électronique hello admin de publication.
5. Accédez tooPublishers -> sélectionnez votre compte -> administrateurs -> Ajouter hello co-admin (capture d’écran ci-dessous)
   
    ![dessin](media/marketplace-publishing-pre-requisites/imgAddAdmin_05.png)
6. Vérifier qu’électroniques ID fourni à hello différentes étapes du processus (par exemple, centre de développement, portail de publication) de publication de hello sont surveillés pour toutes les communications à partir de Microsoft.
7. Pour l’inscription au centre de développement, évitez d’utiliser un compte associé à une seule personne. Cela est conseillé pour éviter la dépendance à un seul individu.
8. Si vous rencontrez des problèmes durant l’inscription sur le centre de développement, envoyez un ticket à l’aide de ce [lien](https://developer.microsoft.com/en-us/windows/support).

## <a name="steps-toodelete-a-co-admin-in-hello-publishing-portal"></a>Étapes toodelete un co-admin Bonjour portail de publication
**En supposant que vous êtes administrateur de hello,** ci-dessous est hello étapes toodelete un co-Admin.

1. Connexion toohello portail avec l’id de courrier électronique hello admin de publication.
2. Accédez trop**éditeurs** -> sélectionnez votre compte -> **administrateurs** -> **Coadministrateurs**.
3. Cliquez sur hello **X** co-admin toohello suivant bouton que vous souhaitez supprimer d’assurances (capture d’écran ci-dessous).
   
    ![dessin](media/marketplace-publishing-pre-requisites/imgDeleteAdmin_03.png)

> [!IMPORTANT]
> Vous n’avez pas les informations de taxe et de la banque de la société toocomplete si vous prévoyez de toopublish des offres uniquement libre (ou mettez votre propre licence).
> 
> l’enregistrement de Hello entreprise doit être terminé tooget a démarré. Toutefois, alors que votre entreprise fonctionne sur les informations de taxe et banque hello dans le compte de Microsoft Developer hello, les développeurs de hello peuvent commencer à travailler sur la création d’image de machine virtuelle hello Bonjour [portail de publication](https://publish.windowsazure.com), d’obtention certifié, et le tester Bonjour Azure environnement intermédiaire. Vous devez hello vendeur complète compte approbation uniquement pour hello dernière étape de publication de votre toohello offre Azure Marketplace.
> 
> 

## <a name="acquire-an-azure-pay-as-you-go-subscription"></a>Acquisition d’un abonnement Azure avec « paiement à l’utilisation »
Il s’agit d’abonnement hello que vous allez utiliser toocreate vos images de machine virtuelle et remettre hello images toohello [Azure Marketplace](https://azure.microsoft.com/marketplace/). Si vous n’avez pas d’abonnement, inscrivez-vous à l’adresse https://account.windowsazure.com/signup?offer=ms-azr-0003p.

## <a name="sell-from-countries"></a>Pays à partir duquel vous vendez
> [!WARNING]
> Dans l’ordre toosell vos services sur hello Azure Marketplace, vous devez vous assurer que votre entité inscrite est une des pays hello approuvé « donneur d’ordre-de ». Cette restriction s’applique pour des raisons de revenus et de taxes. Nous sommes recherche activement tooexpand cette liste de pays Bonjour futur proche, donc tenez-vous informé. Pour la liste complète de hello, consultez 1 b de section de hello [stratégies de participation Azure Marketplace](http://go.microsoft.com/fwlink/?LinkID=526833).
> 
> 

## <a name="next-steps"></a>Étapes suivantes
Une fois que les conditions préalables non technique hello sont remplies, est offre de hello conditions préalables de techniques spécifiques. Cliquez sur l’article toohello de lien hello pour le type d’offre respectifs hello que vous aimeriez toocreate pour hello Azure Marketplace.

* [Conditions préalables techniques des machines virtuelles](marketplace-publishing-vm-image-creation-prerequisites.md)
* [Conditions préalables techniques des modèles de solution](marketplace-publishing-solution-template-creation-prerequisites.md)

## <a name="see-also"></a>Voir aussi
* [Mise en route : comment toopublish une toohello offre Azure Marketplace](marketplace-publishing-getting-started.md)

