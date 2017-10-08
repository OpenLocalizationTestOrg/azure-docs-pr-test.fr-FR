---
title: "Bien démarrer avec Azure Active Directory Domain Services | Microsoft Docs"
description: "Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: ace1ed4a-bf7f-43c1-a64a-6b51a2202473
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: maheshu
ms.openlocfilehash: 7695dabb11df8d9dcfdac24996edf021af2e7f52
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-azure-active-directory-domain-services-using-hello-azure-portal-preview"></a>Activer Azure Active Directory Domain Services à l’aide de hello portail Azure (aperçu)


## <a name="before-you-begin"></a>Avant de commencer
Consultez trop[considérations relatives à la mise en réseau pour les Services de domaine Active Directory Azure](active-directory-ds-networking.md).


## <a name="task-2-configure-network-settings"></a>Tâche 2 : Configurer les paramètres réseau
tâche de configuration suivante Hello est toocreate un réseau virtuel Azure et un sous-réseau dédié qu’il contient. Vous activez Azure Active Directory Domain Services dans ce sous-réseau de votre réseau virtuel. Vous pouvez également sélectionner un réseau virtuel existant et créer des sous-réseaux hello dédié qu’il contient.

1. Cliquez sur **réseau virtuel** tooselect un réseau virtuel.
2. Sur hello **réseau virtuel de choisir** panneau, vous voyez tous les réseaux virtuels existants. Vous voyez uniquement hello réseaux virtuels qui font partie de groupe de ressources toohello et l’emplacement Azure que vous avez sélectionné sur hello **notions de base** page de l’Assistant.

3. Choisissez hello de réseau virtuel dans lequel les Services de domaine Active Directory de Azure doivent être activées. Cliquez sur **nouvel**, si vous préférez toocreate un réseau virtuel. Nous vous recommandons vivement d’utiliser un sous-réseau dédié pour Azure AD Domain Services. Si vous sélectionnez un réseau virtuel existant, [créer un sous-réseau dédié à l’aide d’extension de réseaux virtuels hello](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) et choisir ce sous-réseau. 

    ![Sélectionner un réseau virtuel](./media/getting-started/domain-services-blade-network-pick-vnet.png)

4. Cliquez sur **sous-réseau** toopick hello sous-réseau dédié dans ce réseau virtuel, dans quel tooenable votre nouvelle gérés domaine. Bonjour **créer sous-réseau** panneau, spécifiez un nom pour le sous-réseau de hello, puis cliquez sur **OK** lorsque vous avez terminé. Par exemple, créer un sous-réseau portant le nom hello 'DomainServices', ce qui facilite d’autres administrateurs toounderstand ce qui est déployé dans le sous-réseau de hello.

    ![Choisissez le sous-réseau au sein du réseau virtuel de hello](./media/getting-started/domain-services-blade-network-pick-subnet.png)

  > [!NOTE]
  > **Indications pour la sélection d’un sous-réseau**
  > 1. Utilisez un sous-réseau dédié pour Azure AD Domain Services. Ne déployez pas un autre sous-réseau toothis de machines virtuelles. Cette configuration permet de tooconfigure les groupes de sécurité réseau (NSG) pour vos ordinateurs virtuels ou les charges de travail sans interrompre votre domaine géré. Pour plus de détails, consultez [Considérations relatives à la mise en réseau pour Azure Active Directory Domain Services](active-directory-ds-networking.md).
  2. Ne sélectionnez pas de sous-réseau de passerelle hello pour le déploiement des Services de domaine Active Directory de Azure, car il n’est pas une configuration prise en charge.
  3. Assurez-vous que vous avez sélectionné le sous-réseau hello possède suffisamment d’espace disponible adresse - les adresses IP disponibles au moins de 3 à 5.
  >

5. Lorsque vous avez terminé, cliquez sur **OK** toomove sur toohello **groupe administrateur** page d’Assistant de hello.


## <a name="next-step"></a>Étape suivante
[Tâche 3 : Configurer le groupe d’administration et activer Azure AD Domain Services](active-directory-ds-getting-started-admingroup.md)
