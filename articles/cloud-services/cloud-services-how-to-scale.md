---
title: "aaaAuto faire évoluer un service cloud dans le portail classique de hello | Documents Microsoft"
description: "(classique) Découvrez comment toouse hello tooconfigure portail classique des règles de mise à l’échelle automatique pour un rôle web de service cloud ou le rôle de travail dans Azure."
services: cloud-services
documentationcenter: 
author: Thraka
manager: timlt
editor: 
ms.assetid: eb167d70-4eba-42a4-b157-d8d0688abf4b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: adegeo
ms.openlocfilehash: ddb5816d4d22192c6d2f51d7508e390779742078
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-auto-scaling-for-a-cloud-service-in-hello-classic-portal"></a>Comment tooconfigure mise à l’échelle d’un Service Cloud dans le portail classique de hello
> [!div class="op_single_selector"]
> * [Portail Azure](cloud-services-how-to-scale-portal.md)
> * [portail Azure Classic](cloud-services-how-to-scale.md)

Page de mise à l’échelle hello Hello portail Azure classic, vous pouvez configurer les paramètres de mise à l’échelle automatique pour votre rôle web ou d’un rôle de travail. Vous pouvez également configurer une mise à l’échelle manuelle au lieu d’une mise à l’échelle automatique basée sur des règles.

> [!NOTE]
> Cet article porte essentiellement sur les rôles web et de travail d’un service cloud. Lorsque vous créez directement une machine virtuelle (Classic), elle est hébergée dans un service cloud. Certaines de ces informations s’applique types toothese d’ordinateurs virtuels. Mise à l’échelle d’un ensemble de disponibilité des machines virtuelles est simplement en cours d’arrêt les désactiver selon les règles de mise à l’échelle hello que vous configurez. Pour plus d’informations sur les ordinateurs virtuels et des groupes à haute disponibilité, consultez [gérer hello disponibilité des Machines virtuelles](../virtual-machines/windows/classic/configure-availability.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)

Vous devez envisager hello informations suivantes avant de configurer la mise à l’échelle de votre application :

* L'utilisation des cœurs a une incidence sur la mise à l'échelle.

    Le nombre de cœurs utilisés varie en fonction de la taille des instances de rôle. Vous pouvez faire évoluer une application uniquement dans la limite de hello de cœurs de votre abonnement. Par exemple, si la limite de votre abonnement est de 20 cœurs. Si vous exécutez une application avec les deux services de cloud de taille moyenne (un total de 4 cœurs), vous pouvez uniquement l’échelle autres déploiements de service cloud dans votre abonnement en 16 cœurs restants de hello. Pour plus d’informations sur les tailles, consultez [Tailles de services cloud](cloud-services-sizes-specs.md).

* Vous devez créer une file d’attente et l’associer à un rôle avant de pouvoir mettre à l’échelle une application en fonction d’un seuil de messages. Pour plus d’informations, consultez [comment toouse hello Service de stockage de file d’attente](../storage/queues/storage-dotnet-how-to-use-queues.md).

* Vous pouvez faire évoluer les ressources qui sont lié tooyour service cloud. Pour plus d’informations sur la liaison des ressources, consultez [Comment : lier un service de cloud de ressource tooa](cloud-services-how-to-manage.md#how-to-link-a-resource-to-a-cloud-service).

* tooenable haute disponibilité de votre application, vous devez vous assurer qu’il est déployé avec deux ou plusieurs instances de rôle. Pour plus d'informations, consultez la page [Contrats de niveau de service](https://azure.microsoft.com/support/legal/sla/).

## <a name="schedule-scaling"></a>Planifier la mise à l'échelle
Par défaut, tous les rôles ne suivent pas une planification spécifique. Par conséquent, les paramètres modifiés s’appliquent tooall fois et tous les jours pendant toute année de hello. Si vous le souhaitez, vous pouvez configurer la mise à l’échelle manuelle ou automatique pour l’une des hello suivant modes :

* Les jours de la semaine
* Les week-ends
* Les nuits de la semaine
* Les matinées de la semaine
* Des dates spécifiques
* Des plages de dates spécifiques

paramètre de planification Hello est configuré dans hello [portail Azure classic](https://manage.windowsazure.com/) sur hello  
**Services cloud** > **\[Votre service cloud\]** > **Mise à l’échelle** > **\[Production ou intermédiaire\]**.

Cliquez sur hello **configurer des heures de planification** bouton pour chaque rôle, vous souhaitez toochange.

![Mise à l’échelle automatique d’un service cloud en fonction d’une planification][scale_schedules]

## <a name="manual-scale"></a>Mise à l’échelle manuelle
Sur hello **échelle** page, vous pouvez manuellement augmenter ou réduire hello nombre d’instances en cours d’exécution dans un service cloud. Ce paramètre est configuré pour chaque planification que vous avez créé ou tooall si vous n’avez pas créé une planification.

1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.
   
   > [!TIP]
   > Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.

2. Cliquez sur **Scale**.
3. Sélectionnez l’agenda hello toochange mise à l’échelle des options pour. *Ne moments planifiés* est par défaut de hello si vous ne disposez d’aucune planification définie.
4. Recherche hello **mise à l’échelle par métrique** section et sélectionnez **NONE**. Ce paramètre est par défaut de hello pour tous les rôles.
5. Chaque rôle dans le service cloud hello dispose d’un curseur pour modifier le nombre de hello d’instances toouse.
   
    ![Mise à l’échelle manuelle d’un rôle de service cloud][manual_scale]
   
    Si vous avez besoin de plusieurs instances, vous devrez peut-être toochange hello [taille de machine virtuelle de service de cloud computing](cloud-services-sizes-specs.md).
6. Cliquez sur **Enregistrer**.  
   Les instances de rôle sont ajoutées ou supprimées en fonction de vos sélections.

> [!TIP]
> Chaque fois que vous voyez ![][tip_icon] déplacer votre tooit de la souris, et vous pouvez obtenir de l’aide sur le paramètre spécifique fait.

## <a name="automatic-scale---cpu"></a>Mise à l’échelle automatique - UC
Ce mode met à l’échelle si le pourcentage moyen de hello d’utilisation du processeur passe au-dessus ou en dessous des seuils spécifiés. Dans ce cas, des instances de rôle sont créées ou supprimées.

1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.
   
   > [!TIP]
   > Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.

2. Cliquez sur **Scale**.
3. Sélectionnez l’agenda hello toochange mise à l’échelle des options pour. *Ne moments planifiés* est par défaut de hello si vous ne disposez d’aucune planification définie.
4. Recherche hello **mise à l’échelle par métrique** section et sélectionnez **processeur**.
5. Vous pouvez maintenant configurer une plage minimale et maximale des instances de rôles, hello UC cible l’utilisation de (tootrigger une montée en puissance), et nombre d’instances tooscale haut et bas par.

![Mise à l’échelle d’un rôle de service cloud par charge d’UC][cpu_scale]

> [!TIP]
> Chaque fois que vous voyez ![][tip_icon] déplacer votre tooit de la souris, et vous pouvez obtenir de l’aide sur le paramètre spécifique fait.

## <a name="automatic-scale---queue"></a>Mise à l’échelle automatique - File d’attente
Ce mode s’ajuste automatiquement en cas de nombre de hello de messages dans une file d’attente au-dessus ou en dessous d’un seuil spécifié. Dans ce cas, des instances de rôle sont créées ou supprimées.

1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.
   
   > [!TIP]
   > Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.

2. Cliquez sur **Scale**.
3. Recherche hello **mise à l’échelle par métrique** section et sélectionnez **file d’attente**.
4. Vous pouvez désormais configurer une plage minimale et maximale d’instances de rôles, file d’attente hello et nombre de tooprocess de messages de file d’attente pour chaque instance et combien de tooscale instances haut et bas par.

![Mise à l’échelle d’un rôle de service cloud par une file d’attente de messages][queue_scale]

> [!TIP]
> Chaque fois que vous voyez ![][tip_icon] déplacer votre tooit de la souris, et vous pouvez obtenir de l’aide sur le paramètre spécifique fait.

## <a name="scale-linked-resources"></a>Mise à l'échelle des ressources liées
Souvent, lorsque vous l’échelle d’un rôle, il est bénéfique tooscale hello base de données qui utilise également application hello. Si vous liez le service de cloud toohello hello de base de données, vous pouvez accéder à hello mise à l’échelle des paramètres pour cette ressource en cliquant sur le lien approprié de hello.

1. Bonjour [portail Azure classic](https://manage.windowsazure.com/), cliquez sur **Services de cloud computing**, puis cliquez sur nom hello du tableau de bord de hello tooopen hello cloud service.
   
   > [!TIP]
   > Si vous ne voyez pas votre service cloud, vous devrez peut-être toochange de **Production** trop**intermédiaire** ou vice versa.

2. Cliquez sur **Scale**.
3. Recherche hello **de ressources liées** et cliquez sur **gérer la mise à l’échelle pour cette base de données**.
   
   > [!NOTE]
   > Si vous ne voyez pas de section **Ressources liées** , c’est que vous n’avez probablement pas de ressources liées.

![][linked_resource]

[manual_scale]: ./media/cloud-services-how-to-scale/manual-scale.png
[queue_scale]: ./media/cloud-services-how-to-scale/queue-scale.png
[cpu_scale]: ./media/cloud-services-how-to-scale/cpu-scale.png
[tip_icon]: ./media/cloud-services-how-to-scale/tip.png
[scale_schedules]: ./media/cloud-services-how-to-scale/schedules.png
[scale_popup]: ./media/cloud-services-how-to-scale/schedules-dialog.png
[linked_resource]: ./media/cloud-services-how-to-scale/linked-resources.png
