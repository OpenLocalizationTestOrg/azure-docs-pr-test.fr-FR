---
title: aaaDelegating offre une pile de Azure | Documents Microsoft
description: "Découvrez comment tooput autres personnes en charge de la création d’offres et la signature des utilisateurs pour vous."
services: azure-stack
documentationcenter: 
author: AlfredoPizzirani
manager: byronr
editor: 
ms.assetid: 157f0207-bddc-42e5-8351-197ec23f9d46
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: alfredop
ms.openlocfilehash: d539cac3ed56f342338c830d95fbec7e93175929
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="delegating-offers-in-azure-stack"></a>Délégation des offres dans Azure Stack

En tant qu’opérateur de cloud Azure pile hello, il est souvent nécessaire tooput autres personnes en charge de la création d’offres et la signature des utilisateurs pour vous. Par exemple, si vous êtes un fournisseur de services et que vous souhaitez toosign revendeurs des clients et les gérez à votre place. Il peut également se produire dans une entreprise si vous faites partie d’un groupe informatique centralisé et souhaitez que les divisions ou toosign filiales des utilisateurs sans votre intervention.

Délégation contrainte vous aident à effectuer ces tâches, vous aidant à tooreach et gérer plus d’utilisateurs que vous serez en mesure de toodo directement. Hello l’illustration suivante montre un niveau de délégation, mais la pile de Azure prend en charge plusieurs niveaux. Fournisseurs de délégués peuvent déléguer à son tour fournisseurs tooother, les niveaux de toofive.

![](media/azure-stack-delegated-provider/image1.png)

Les opérateurs cloud pile Azure peuvent déléguer la création de hello d’utilisateurs de tooother offres et des locataires en utilisant la fonctionnalité de délégation hello.

## <a name="roles-and-steps-in-delegation"></a>Rôles et étapes de la délégation
délégation de toounderstand, n’oubliez pas qu’il existe trois rôles impliqués :

* Hello **opérateur cloud** gère l’infrastructure de pile de Azure hello, crée un modèle d’offre et délègue à proposer aux utilisateurs de tootheir.
* Hello cloud déléguée administrateurs sont appelés **déléguée fournisseurs**. Ils peuvent appartenir aux organisations de tooother (par exemple, d’autres clients Azure Active Directory).
* **Les utilisateurs** s’inscrire pour les offres de hello et de les utiliser pour la gestion de leurs charges de travail, de création de machines virtuelles, le stockage des données, etc..

Comme indiqué dans le graphique suivant de hello, il existe deux étapes de configuration de la délégation.

1. **Identifier les fournisseurs de hello déléguée** par leur abonnement tooan offre basé sur un plan qui contient uniquement les abonnements de hello service.
   D’acquérir certaines des fonctionnalités de l’administrateur de cloud hello, y compris les offres de tooextend possibilité hello et connecter les utilisateurs pour les utilisateurs de s’abonner toothis offre.
2. **Délégué un toohello offre déléguée fournisseur**, cette offre fonctionne comme un modèle pour que hello fournisseur déléguée peut offrir. Hello fournisseur délégué est désormais en mesure de tootake hello offre, choisissez un nom (mais pas modifier ses services et les quotas) et elle offre toocustomers.

![](media/azure-stack-delegated-provider/image2.png)

tooact en tant que fournisseurs de délégués, les utilisateurs doivent tooestablish une relation avec les fournisseur principal hello ; en d’autres termes, ils doivent toocreate un abonnement. Dans ce scénario, cet abonnement identifie les fournisseurs de délégués comme ayant hello droit toopresent offre pour le compte du fournisseur principal de hello.

Une fois que cette relation est établie, opérateur de cloud hello peut déléguer à un fournisseur de délégué toohello offre. Hello fournisseur délégué est désormais en mesure de tootake hello offre, renommez-le (mais pas modifier sa substance) et elle offre tooits clients.

Hello les sections suivantes décrire comment les tooestablish un fournisseur de délégués, déléguer une offre et vérifiez que les utilisateurs peuvent souscrire pour celle-ci.

## <a name="set-up-roles"></a>Configurer les rôles

toosee un fournisseur de délégué au travail, vous avez besoin des comptes Azure Active Directory supplémentaires dans le compte d’opérateur addition tooyour cloud. Si vous ne les avez pas, vous pouvez créer hello deux comptes. les comptes Hello peuvent appartenir client AAD de tooany. Nous nous référons toothem hello délégués fournisseur (DP) et l’utilisateur de hello.

| **Rôle** | **Droits d’organisation** |
| --- | --- |
| Fournisseur délégué |Utilisateur |
| Utilisateur |Utilisateur |

## <a name="identify-hello-delegated-providers"></a>Identifier les fournisseurs de hello déléguée
1. Connectez-vous en tant qu’opérateur cloud.
2. Créer une offre de hello qui permet aux fournisseurs de toobecome déléguée aux utilisateurs. Pour ce faire, vous devez créer un plan et une offre basée sur celui-ci :
   
   a.  [Créer un plan](azure-stack-create-plan.md).
       Ce plan doit inclure seulement le service d’abonnements hello. Dans cet article, nous utilisons un plan appelé PlanForDelegation.
   
   b.  [Créer une offre](azure-stack-create-offer.md) basée sur ce plan. Dans cet article, nous utilisons une offre appelée OfferToDP.
   
   c.  Une fois terminée, la création de l’offre de hello hello ajouter fournisseur de délégué hello en tant qu’une offre de toothis abonné en cliquant sur **abonnements** &gt; **ajouter** &gt; **nouveau Abonnement de locataire**.
   
   ![](media/azure-stack-delegated-provider/image3.png)

> [!NOTE]
> Comme avec toutes les offres Azure pile, vous pouvez hello de fabrication offre de hello public et permettre aux utilisateurs Inscrivez-vous à, ou protéger la confidentialité et ont opérateur cloud de hello gérer hello d’abonnement. Délégué fournisseurs sont généralement un petit groupe et que vous souhaitez toocontrol qui est admis tooit, afin de protéger la confidentialité de cette offre une signification dans la plupart des cas.
> 
> 

## <a name="cloud-operator-creates-hello-delegated-offer"></a>Opérateur de cloud crée offre de délégué hello

Vous avez désormais établi votre fournisseur délégué. Hello suivant consiste à créer le plan de hello et offre que vous allez toodelegate, et qui seront utilisés par vos clients. Vous devez définir cette offre exactement comme vous souhaitez que le clients toosee, hello déléguées fournisseur ne sera pas en mesure de modifier les plans de hello et il inclut des quotas.

1. En tant qu’opérateur cloud, [créez un plan](azure-stack-create-plan.md) et [une offre](azure-stack-create-offer.md) basée sur celui-ci. Dans cet article, nous utilisons une offre appelée DelegatedOffer.
   
   > [!NOTE]
   > Cette offre n’a pas de toobe public. Elle peut être rendue publique si vous choisissez, mais, dans la plupart des cas, vous souhaitez seulement déléguée fournisseurs toohave accès tooit. Une fois que vous déléguez une offre privée comme décrit dans hello comme suit, fournisseur de délégué hello a accès tooit.
   > 
   > 
1. Offre de hello de délégué. Accédez tooDelegatedOffer et dans le volet de paramètres hello, cliquez sur **fournisseurs de délégué** &gt; **ajouter**.
2. Sélectionnez l’abonnement du fournisseur hello délégué à partir de la zone de liste déroulante hello et cliquez sur **délégué**.

> ![](media/azure-stack-delegated-provider/image4.png)
> 
> 

## <a name="delegated-provider-customizes-hello-offer"></a>Délégué de fournisseur personnalise offre de hello

Connectez-vous à toohello **portail locataire** comme hello déléguée au fournisseur et créer une offre à l’aide d’offre de délégué hello en tant que modèle.

1. Cliquez sur **Nouveau** &gt; **Offres + Plans clients** &gt; **Offre**.

    ![](media/azure-stack-delegated-provider/image5.png)


1. Affecter une offre de toohello de nom. Ici, nous avons choisi le nom ResellerOffer. Sélectionnez hello déléguée offre toobase sur, puis cliquez sur **créer**.
   
   ![](media/azure-stack-delegated-provider/image6.png)

    >[!NOTE] 
    > Remarque hello différence par rapport à la création de toooffer comme rencontrés par l’opérateur de cloud hello. fournisseur de délégué Hello n’en construit pas offre hello à partir de plans de base et les plans de module complémentaire ; ils peuvent uniquement choisir à partir des offres qui ont été déléguée toothem et ne peut pas apporter des modifications toothose offres.

1. Rendre hello offrent public en cliquant sur **Parcourir** &gt; **offre**, en sélectionnant l’offre de hello et en cliquant sur **changement d’état**.
2. Hello déléguée fournisseur expose ces offres via le portail de leur propre URL. Ces offres sont visibles uniquement via le portail de hello déléguée. toofind et modifier cette URL :
   
    a.  Cliquez sur **Parcourir** &gt; **davantage de services** &gt; **abonnements** &gt; hello sélectionnez déléguée d’abonnement du fournisseur, dans le cas présent son *DPSubscription* &gt; **propriétés**.
   
    b.  Copiez hello portail URL tooa emplacement distinct, tel que le bloc-notes.
   
    ![](media/azure-stack-delegated-provider/dpportaluri.png)  
   
   Vous avez maintenant terminé la création de hello d’une offre de délégué en tant que délégué fournisseur. Se déconnecter comme hello fournisseur déléguée. Fermer un onglet de navigateur hello que vous avez utilisé.

## <a name="sign-up-for-hello-offer"></a>S’inscrire pour l’offre de hello
1. Dans une nouvelle fenêtre de navigateur, accédez au portail de délégué toohello URL que vous avez enregistré à l’étape précédente de hello. Connectez-vous toohello portail en tant qu’utilisateur. Remarque : Hello d’utilisation déléguée portail pour cette étape. offre de délégué Hello ne sont pas visibles dans le cas contraire.
2. Dans le tableau de bord hello, cliquez sur **obtenir un abonnement**. Vous verrez qu’offre hello déléguée uniquement créé par le fournisseur de hello délégué est présentées toohello utilisateur :

> ![](media/azure-stack-delegated-provider/image8.png)
> 
> 

Ceci conclut le processus hello de délégation de l’offre. utilisateur de Hello peut désormais s’inscrire pour cette offre en obtenant un abonnement pour celle-ci.

## <a name="multiple-tier-delegation"></a>Délégation à plusieurs niveaux

Délégation contrainte à plusieurs niveaux permet hello déléguée fournisseur toodelegate les entités de tooother offre. Ainsi, par exemple, la création de revendeurs plus approfondies, dans lequel hello fournisseur de gestion Azure pile délègue un distributeur de tooa offre, qui à son tour délègue tooreseller hello.
Pile Azure prend en charge les niveaux de toofive de délégation.

toocreate plusieurs couches offrent la délégation, fournisseur de délégué hello délègue à son tour fournisseur suivant du toohello offre hello. processus de Hello est hello même pour le fournisseur de délégué hello telle qu’elle était pour l’opérateur de cloud hello (consultez [opérateur Cloud crée offre de délégué hello](#cloud-operator-creates-the-delegated-offer)).

## <a name="next-steps"></a>Étapes suivantes
[Approvisionner une machine virtuelle](azure-stack-provision-vm.md)

