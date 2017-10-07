---
title: "aaaCreate personnalisé sonde - passerelle d’Application Azure - Azure Portal | Documents Microsoft"
description: "Découvrez comment toocreate personnalisé sondage pour la passerelle d’Application à l’aide du portail de hello"
services: application-gateway
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 33fd5564-43a7-4c54-a9ec-b1235f661f97
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 04/26/2017
ms.author: gwallace
ms.openlocfilehash: 9e9309045ef33ba1010868783949b4fde31619ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-custom-probe-for-application-gateway-by-using-hello-portal"></a>Créer une sonde personnalisée pour la passerelle d’Application à l’aide du portail de hello

> [!div class="op_single_selector"]
> * [Portail Azure](application-gateway-create-probe-portal.md)
> * [Commandes PowerShell pour Azure Resource Manager](application-gateway-create-probe-ps.md)
> * [Azure Classic PowerShell](application-gateway-create-probe-classic-ps.md)

Dans cet article, vous ajoutez une passerelle existante d’application sonde personnalisée tooan via hello portail Azure. Les sondes personnalisés sont utiles pour les applications qui ont une page de vérification d’intégrité spécifique ou pour les applications qui ne fournissent pas une réponse correcte sur l’application web de hello par défaut.

## <a name="before-you-begin"></a>Avant de commencer

Si vous n’avez pas déjà d’une passerelle d’application, visitez [créer une passerelle d’Application](application-gateway-create-gateway-portal.md) toocreate un toowork de passerelle d’application avec.

## <a name="createprobe"></a>Création de la sonde de hello

Sondes sont configurés dans un processus en deux étapes via le portail de hello. première étape de Hello est sonde de hello toocreate. Dans la deuxième étape de hello, vous ajoutez des paramètres hello sonde toohello principal http de la passerelle d’application hello.

1. Connectez-vous à toohello [portail Azure](https://portal.azure.com). Si vous ne possédez pas encore de compte, vous pouvez [vous inscrire pour bénéficier d’un essai gratuit d’un mois](https://azure.microsoft.com/free).

1. Bonjour Azure portal volet Favoris, cliquez sur toutes les ressources. Cliquez sur passerelle d’application hello Bonjour toutes les lames de ressources. Si l’abonnement hello que déjà sélectionné comporte plusieurs ressources, vous pouvez entrer partners.contoso.net Bonjour filtre par nom... passerelle d’application hello boîte tooeasily accès.

1. Cliquez sur **sondes** et cliquez sur hello **ajouter** bouton tooadd une sonde.

  ![Ajouter un panneau Sonde contenant toutes les informations][1]

1. Sur hello **sonde d’intégrité ajouter** panneau, indiquez les informations de hello requis pour la sonde de hello et lorsque vous avez terminé cliquez **OK**.

  |**Paramètre** | **Valeur** | **Détails**|
  |---|---|---|
  |**Nom**|customProbe|Cette valeur est une sonde toohello nom convivial qui est accessible dans le portail de hello.|
  |**Protocole**|HTTP ou HTTPS | protocole Hello hello sonde d’intégrité utilise.|
  |**Hôte**|Par exemple, contoso.com|Cette valeur est le nom d’hôte hello qui est utilisé pour la sonde de hello. S’applique uniquement lorsque plusieurs sites sont configurés sur Application Gateway, sinon utilisez '127.0.0.1'. Cette valeur diffère du nom d’hôte de machine virtuelle de hello.|
  |**Chemin d’accès**|/ ou un autre chemin|Bonjour reste d’une url complète pour la sonde personnalisée de hello hello. Un chemin valide commence par « / ». Chemin d’accès par défaut de hello de http://contoso.com simplement utiliser '/' |
  |**Intervalle (secondes)**|30|La fréquence à laquelle hello sonde est exécuté toocheck pour le contrôle d’intégrité. Il n’est pas recommandé hello tooset inférieure à 30 secondes.|
  |**Délai d’expiration (secondes)**|30|Hello de sonde de hello temps délai avant expiration. Hello du délai d’attente intervalle besoins toobe suffisamment élevée pour qu’un appel http peut être effectué page de contrôle d’intégrité tooensure hello principal est disponible.|
  |**Seuil de défaillance sur le plan de l’intégrité**|3|Nombre d’échecs toobe tentatives considéré comme non intègre. Un seuil de 0 signifie que si un contrôle d’intégrité échoue hello back-end est déterminé non intègre immédiatement.|

  > [!IMPORTANT]
  > nom d’hôte Hello n’est pas hello identique au nom du serveur. Cette valeur est le nom hello d’hôte virtuel de hello en cours d’exécution sur le serveur d’applications hello. Sonde de Hello est envoyé toohttp : / /(host name) :(port from httpsetting)/urlPath

## <a name="add-probe-toohello-gateway"></a>Ajouter la passerelle toohello de sonde

Maintenant que hello sondage a été créé, il est temps tooadd il toohello passerelle. Paramètres de sonde sont définies sur les paramètres http hello principal de la passerelle d’application hello.

1. Cliquez sur **paramètres HTTP** sur la passerelle d’application hello, toobring de panneau de configuration hello, cliquez sur hello actuel principaux paramètres http répertoriées dans la fenêtre hello.

  ![fenêtre de paramètres https][2]

1. Sur hello **appGatewayBackEndHttpSettings** panneau Paramètres, cocher hello **sonde personnalisée d’utilisation** case à cocher et choisissez sonde hello créé Bonjour [la sonde Create hello](#createprobe) section sur hello **sonde de personnalisée** déroulante...
Lorsque vous avez terminé, cliquez sur **enregistrer** et hello paramètres sont appliqués.

Sonde de Hello par défaut vérifie l’application web de toohello d’accès par défaut de hello. Maintenant qu’une sonde personnalisée a été créée, passerelle d’application hello utilise le contrôle d’intégrité toomonitor hello chemin personnalisé défini pour les serveurs principaux de hello. En fonction de critères hello a été défini, la passerelle d’application hello vérifie chemin hello dans sonde de hello. Si hello appeler toohost:Port / chemin d’accès ne retourne pas HTTP de réponse d’état 200-399, serveur de hello est extraite de rotation après hello défectueux est atteint. Détection continue sur hello instance défectueux toodetermine dès qu’elle est sain. Une fois les instance hello ajoutée pool de serveurs toohealthy précédent, le trafic commence tooit flux à nouveau et détection toohello instance se poursuit à l’intervalle spécifié d’utilisateur comme d’habitude.

## <a name="next-steps"></a>Étapes suivantes

toolearn tooconfigure le déchargement SSL avec la passerelle d’Application Azure, voir [configurer le déchargement SSL](application-gateway-ssl-portal.md)

[1]: ./media/application-gateway-create-probe-portal/figure1.png
[2]: ./media/application-gateway-create-probe-portal/figure2.png

