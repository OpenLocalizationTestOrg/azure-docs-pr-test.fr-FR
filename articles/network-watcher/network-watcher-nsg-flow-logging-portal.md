---
title: "journaux de flux aaaManage réseau sécurité groupe avec l’Observateur de réseau Azure | Documents Microsoft"
description: "Cette page explique le fonctionnement des journaux toomanage flux du groupe de sécurité réseau dans l’Observateur réseau de Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 01606cbf-d70b-40ad-bc1d-f03bb642e0af
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: fb250337ab9d1a0c0d0d3569c00bc221dd102a3f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-network-security-group-flow-logs-in-hello-azure-portal"></a>Gérer les journaux de flux de groupe de sécurité réseau Bonjour portail Azure

> [!div class="op_single_selector"]
> - [Portail Azure](network-watcher-nsg-flow-logging-portal.md)
> - [PowerShell](network-watcher-nsg-flow-logging-powershell.md)
> - [CLI 1.0](network-watcher-nsg-flow-logging-cli-nodejs.md)
> - [CLI 2.0](network-watcher-nsg-flow-logging-cli.md)
> - [API REST](network-watcher-nsg-flow-logging-rest.md)

Journaux de flux de groupe de sécurité réseau sont une fonctionnalité de l’Observateur réseau qui vous permet de tooview d’informations sur le trafic IP entrant et sortant via un groupe de sécurité réseau. Ces journaux de flux, écrits au format JSON, fournissent des informations importantes, notamment : 

- les flux entrants et sortants, règle par règle ;
- Hello NIC hello flux s’applique à.
- 5-tuple plus d’informations sur le flux hello (source/destination IP, port source ou de destination, protocole).
- des informations indiquant si le trafic a été autorisé ou refusé.

## <a name="before-you-begin"></a>Avant de commencer

Ce scénario suppose que vous avez déjà suivi les étapes hello dans [créer une instance de l’Observateur réseau](network-watcher-create.md). scénario de Hello suppose également que vous disposez d’un groupe de ressources avec un ordinateur virtuel valide.

## <a name="register-insights-provider"></a>Inscription du fournisseur Insights

Pour le flux de journalisation toowork hello avec succès, **Microsoft.Insights** fournisseur doit être enregistré. fournisseur de hello tooregister, hello prennent comme suit : 

1. Accédez trop**abonnements**, puis sélectionnez abonnement hello pour lequel vous souhaitez tooenable flux journaux. 
2. Sur hello **abonnement** panneau, sélectionnez **fournisseurs de ressources**. 
3. Examinez la liste hello des fournisseurs et vérifiez que hello **microsoft.insights** fournisseur est inscrit. Sinon, sélectionnez **Inscrire**.

![Afficher les fournisseurs][providers]

## <a name="enable-flow-logs"></a>Activer les journaux des flux

Ces étapes vous guident tout au long des processus de hello d’activation des journaux de flux sur un groupe de sécurité réseau.

### <a name="step-1"></a>Étape 1

Passez l’instance de l’Observateur réseau tooa, puis sélectionnez **de flux de groupe de sécurité réseau consigne**.

![Vue d’ensemble des journaux de flux][1]

### <a name="step-2"></a>Étape 2

Sélectionnez un groupe de sécurité réseau à partir de la liste de hello.

![Vue d’ensemble des journaux de flux][2]

### <a name="step-3"></a>Étape 3 : 

Sur hello **paramètres des journaux de flux** panneau, définir le statut de hello trop**sur**, puis configurez un compte de stockage.  Quand vous avez terminé, sélectionnez **OK**. Ensuite, sélectionnez **Enregistrer**.

![Vue d’ensemble des journaux de flux][3]

## <a name="download-flow-logs"></a>Télécharger des journaux de flux

Les journaux des flux sont enregistrés dans un compte de stockage. Télécharger votre tooview de journaux flux les.

### <a name="step-1"></a>Étape 1

journaux de flux toodownload, sélectionnez **vous pouvez télécharger les journaux de flux à partir de comptes de stockage configuré**. Cette étape vous amène la vue de compte de stockage tooa où vous pouvez choisir quels toodownload journaux.

![Paramètres des journaux de flux][4]

### <a name="step-2"></a>Étape 2

Atteindre le compte de stockage correct toohello. Ensuite, sélectionnez **Conteneurs** > **insights-journal-networksecuritygroupflowevent**.

![Paramètres des journaux de flux][5]

### <a name="step-3"></a>Étape 3 :

Atteindre l’emplacement de toohello du journal de flux de hello, sélectionnez-le, puis sélectionnez **télécharger**.

![Paramètres des journaux de flux][6]

Pour plus d’informations sur la structure hello du journal de hello, visitez [vue d’ensemble du journal de flux groupe réseau sécurité](network-watcher-nsg-flow-logging-overview.md).

## <a name="next-steps"></a>Étapes suivantes

Découvrez comment trop[visualiser vos journaux de flux de groupe de sécurité réseau avec Power BI](network-watcher-visualize-nsg-flow-logs-power-bi.md).

<!-- Image references -->
[1]: ./media/network-watcher-nsg-flow-logging-portal/figure1.png
[2]: ./media/network-watcher-nsg-flow-logging-portal/figure2.png
[3]: ./media/network-watcher-nsg-flow-logging-portal/figure3.png
[4]: ./media/network-watcher-nsg-flow-logging-portal/figure4.png
[5]: ./media/network-watcher-nsg-flow-logging-portal/figure5.png
[6]: ./media/network-watcher-nsg-flow-logging-portal/figure6.png
[providers]: ./media/network-watcher-nsg-flow-logging-portal/providers.png
