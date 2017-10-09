---
title: "aaaAuto faire évoluer un service cloud dans le portail de hello | Documents Microsoft"
description: "Découvrez comment toouse hello tooconfigure portail règles de mise à l’échelle automatique pour un rôle web de service cloud ou le rôle de travail dans Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: 701d4404-5cc0-454b-999c-feb94c1685c0
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: 265f4c8ec5e1ec2f85585df25f18cd0d0c9946a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-portal"></a>Comment tooconfigure mise à l’échelle d’un Service Cloud dans le portail de hello
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-how-to-scale-portal.md)
> * [Portail Azure Classic](cloud-services-how-to-scale.md)

Des conditions peuvent être définies pour un rôle de travail de service cloud qui déclenchent une opération de diminution et d’augmentation de la taille des instances. conditions de Hello pour le rôle de hello peuvent reposer sur hello processeur, disque ou de la charge réseau du rôle de hello. Vous pouvez également définir une condition basée sur une mesure de file d’attente ou hello message d’une autre ressource Azure associé à votre abonnement.

> [!NOTE]
> Cet article porte essentiellement sur les rôles web et de travail d’un service cloud. Lorsque vous créez directement une machine virtuelle (Classic), elle est hébergée dans un service cloud. Vous pouvez mettre à l’échelle une machine virtuelle standard en l’associant à un [groupe à haute disponibilité](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) et en l’activant ou la désactivant manuellement.

## <a name="considerations"></a>Considérations
Vous devez envisager hello informations suivantes avant de configurer la mise à l’échelle de votre application :

* L'utilisation des cœurs a une incidence sur la mise à l'échelle.

    Le nombre de cœurs utilisés varie en fonction de la taille des instances de rôle. Vous pouvez faire évoluer une application uniquement dans la limite de hello de cœurs de votre abonnement. Par exemple, si la limite de votre abonnement est de 20 cœurs. Si vous exécutez une application avec les deux services de cloud de taille moyenne (un total de 4 cœurs), vous pouvez uniquement l’échelle autres déploiements de service cloud dans votre abonnement en 16 cœurs restants de hello. Pour plus d’informations sur les tailles, consultez [Tailles de services cloud](cloud-services-sizes-specs.md).

* Vous pouvez mettre à l’échelle en fonction d’un seuil de messages de file d’attente. Pour plus d’informations sur la façon toouse les files d’attente, consultez [comment toouse hello Service de stockage de file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Vous pouvez également mettre à l’échelle d’autres ressources associées à votre abonnement.

* tooenable haute disponibilité de votre application, vous devez vous assurer qu’il est déployé avec deux ou plusieurs instances de rôle. Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).


## <a name="where-scale-is-located"></a>Emplacement de la mise à l’échelle
Une fois que vous sélectionnez votre service cloud, vous devez avoir Panneau de service de cloud hello visible.

1. Dans Panneau de service cloud hello, sur hello **rôles et Instances** vignette, nom sélectionnez hello du service de cloud hello.   
   **IMPORTANT**: rendre cloud de hello tooclick que service de rôle, pas hello instance de rôle qui est sous le rôle de hello.

    ![](./media/cloud-services-how-to-scale-portal/roles-instances.png)
2. Sélectionnez hello **échelle** vignette.

    ![](./media/cloud-services-how-to-scale-portal/scale-tile.png)

## <a name="automatic-scale"></a>Mise à l’échelle automatique
Vous pouvez configurer les paramètres de mise à l’échelle d’un rôle avec deux modes : **manuel** ou **automatique**. Manuel est attendue, vous définissez le nombre absolu de hello d’instances. Automatique vous permet cependant tooset règles déterminant comment et à quel beaucoup vous devant mettre à l’échelle.

Ensemble hello **l’échelle** option trop**les règles de performances et planification**.

![Paramètres de mise à l’échelle de services cloud avec profil et règle](./media/cloud-services-how-to-scale-portal/schedule-basics.png)

1. Un profil existant.
2. Ajouter une règle pour le profil de hello parent.
3. Ajoutez un autre profil.

Sélectionnez **Ajouter un profil**. profil Hello détermine le mode souhaité pour la montée en puissance hello toouse : **toujours**, **périodicité**, **date fixe**.

Après avoir configuré les règles et les profils de hello, sélectionnez hello **enregistrer** icône haut hello.

#### <a name="profile"></a>Profil
profil de Hello définit minimale et mettre à l’échelle d’instances maximales pour hello et également lorsque cette plage de l’échelle est active.

* **Toujours**

    Toujours conserver cette plage d’instances disponible.  

    ![Service cloud toujours mis à l’échelle](./media/cloud-services-how-to-scale-portal/select-always.png)
* **Périodicité**

    Choisissez un ensemble de jours de hello semaine tooscale.

    ![Mise à l’échelle du service cloud avec une planification périodique](./media/cloud-services-how-to-scale-portal/select-recurrence.png)
* **Date fixe**

    Un rôle de hello tooscale de plage date fixe.

    ![Mise à l’échelle du service cloud avec une date fixe](./media/cloud-services-how-to-scale-portal/select-fixed.png)

Une fois que vous avez configuré le profil de hello, sélectionnez hello **OK** bouton bas hello du Panneau de profil hello.

#### <a name="rule"></a>Règle
Les règles sont ajoutées tooa profil et représentent une condition qui déclenche la montée en puissance hello.

déclencheur de la règle Hello est basé sur une mesure du service de cloud hello (utilisation de l’UC, l’activité du disque ou une activité de réseau) toowhich, vous pouvez ajouter une valeur conditionnelle. En outre, vous pouvez avoir déclencheur hello basé sur une mesure de file d’attente ou hello message d’une autre ressource Azure associé à votre abonnement.

![](./media/cloud-services-how-to-scale-portal/rule-settings.png)

Une fois que vous avez configuré la règle de hello, sélectionnez hello **OK** bouton bas hello du Panneau de règle hello.

## <a name="back-toomanual-scale"></a>Mise à l’échelle toomanual précédent
Accédez toohello [paramètres d’échelle](#where-scale-is-located) et ensemble hello **l’échelle** option trop**un nombre d’instances que j’entre manuellement**.

![Paramètres de mise à l’échelle de services cloud avec profil et règle](./media/cloud-services-how-to-scale-portal/manual-basics.png)

Ce paramètre supprime la mise à l’échelle automatique du rôle de hello et vous pouvez définir le nombre d’instances hello directement.

1. option de mise à l’échelle (manuels ou automatisés) Hello.
2. Un rôle instance curseur tooset hello instances tooscale à.
3. Instances de tooscale de rôle hello pour.

Après avoir configuré les paramètres d’échelle hello, sélectionnez hello **enregistrer** icône haut hello.
