---
title: "problèmes de déploiement de service de cloud aaaTroubleshoot | Documents Microsoft"
description: "Il existe quelques problèmes courants que vous risquez de rencontrer lors du déploiement d’un tooAzure de service cloud. Cet article fournit toosome solutions d'entre eux."
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: a18ae415-0d1c-4bc4-ab6c-c1ddea02c870
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 15aea4f2b2913d95f3378b2e9762b232531f3c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-cloud-service-deployment-problems"></a>Résoudre les problèmes de déploiement de service cloud
Lorsque vous déployez un tooAzure de package de cloud service application, vous pouvez obtenir des informations sur le déploiement de hello de hello **propriétés** volet Bonjour portail Azure. Vous pouvez utiliser les détails hello dans cette toohelp volet vous résoudre les problèmes de service de cloud computing hello, et vous pouvez fournir cette prise en charge de tooAzure informations lors de l’ouverture d’une nouvelle demande de prise en charge.

Vous pouvez trouver hello **propriétés** volet comme suit :

* Dans hello portail Azure, cliquez sur le déploiement de votre service cloud hello, cliquez sur **tous les paramètres**, puis cliquez sur **propriétés**.
* Dans hello portail Azure classic, cliquez sur le déploiement de votre service cloud hello, cliquez sur **tableau de bord**, situé dans le coin inférieur droit de hello de page de hello (sous **coup de œil rapide**). Notez que ce volet ne contient aucun étiquette Propriétés.

> [!NOTE]
> Vous pouvez copier le contenu de hello Hello **propriétés** Presse-papiers toohello de volet en cliquant sur l’icône hello dans hello haut à droite du volet de hello.
>
>

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="problem-i-cannot-access-my-website-but-my-deployment-is-started-and-all-role-instances-are-ready"></a>Problème : Je ne peux pas accéder à mon site web bien que mon déploiement soit démarré et que toutes les instances de rôle soient prêtes
lien d’URL du site Web Hello indiqué dans le portail hello n’inclut pas de port de hello. port par défaut de Hello pour les sites Web est 80. Si votre application est configurée toorun dans un autre port, vous devez ajouter les URL toohello de numéro de port correct hello lors de l’accès du site Web hello.

1. Bonjour portail Azure, cliquez sur déploiement hello de votre service cloud.
2. Bonjour **propriétés** volet Hello portail Azure, vérifiez les ports hello pour les instances de rôle hello (sous **les points de terminaison d’entrée**).
3. Si le port de hello n’est pas 80, ajoutez hello port correct valeur toohello URL lorsque vous accédez à application hello. toospecify un port non défini par défaut, tapez l’URL de hello, suivie du signe deux-points ( :), suivi d’un numéro de port hello, sans espaces.

## <a name="problem-my-role-instances-recycled-without-me-doing-anything"></a>Problème : Mes instances de rôle sont recyclées sans action de ma part
Réparation de service se produit automatiquement lorsque Azure détecte des nœuds du problème et par conséquent déplace les nœuds de toonew instances de rôle. Le cas échéant, il est possible que vos instances de rôle se recyclent automatiquement. toofind dès s’est produite lors de la réparation de service :

1. Bonjour portail Azure, cliquez sur déploiement hello de votre service cloud.
2. Bonjour **propriétés** volet Hello portail Azure, passez en revue les informations hello et déterminer si le service de réparation se produit au moment de hello observé de rôles hello recyclage.

Les rôles sont recyclés également environ une fois par mois pendant les mises à jour du système d’exploitation hôte et du système d’exploitation invité.  
Pour plus d’informations, voir blog de hello [rôle Instance redémarre en raison des mises à niveau de tooOS](http://blogs.msdn.com/b/kwill/archive/2012/09/19/role-instance-restarts-due-to-os-upgrades.aspx)

## <a name="problem-i-cannot-do-a-vip-swap-and-receive-an-error"></a>Problème : Impossible d’effectuer un échange d’adresses IP virtuelles, une erreur s’affiche
Un échange d’adresses IP virtuelles n’est pas autorisé si une mise à jour de déploiement est en cours. Les mises à jour de déploiement peuvent se produire automatiquement dans les situations suivantes :

* Un nouveau système d’exploitation invité est disponible et votre installation est configurée pour les mises à jour automatiques.
* Une réparation de service se produit.

toofind out si la mise à jour automatique vous empêche d’effectuer un échange d’adresses IP virtuelles :

1. Bonjour portail Azure, cliquez sur déploiement hello de votre service cloud.
2. Bonjour **propriétés** volet Hello portail Azure, examinez la valeur hello **état**. S’il s’agit **prêt**, puis vérifiez **de la dernière opération** toosee si une récente a peut empêcher l’échange de hello VIP.
3. Répétez les étapes 1 et 2 pour le déploiement de production hello.
4. Si une mise à jour automatique est en cours, attendez qu’elle toofinish avant la permutation de hello VIP toodo lors de la tentative.

## <a name="problem-a-role-instance-is-looping-between-started-initializing-busy-and-stopped"></a>Problème : Une instance de rôle est exécutée en boucle entre Démarrée, Initialisation, Occupée et Arrêtée
Cette condition peut indiquer un problème lié à votre code d’application, package ou fichier de configuration. Dans ce cas, vous devez être état de hello toosee peut changer en quelques minutes et hello portail Azure peut indiquer un nom tel que **recyclage**, **occupé**, ou **Initializing**. Cela indique qu’il existe un problème au niveau de hello application empêche l’instance de rôle hello de s’exécuter.

Pour plus d’informations sur la façon de tootroubleshoot pour ce problème, voir hello blog [données de diagnostic de calcul PaaS Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx) et [commun émet ce toorecycle de rôles cause](cloud-services-troubleshoot-common-issues-which-cause-roles-recycle.md).

## <a name="problem-my-application-stopped-working"></a>Problème : Mon application a cessé de fonctionner
1. Bonjour portail Azure, cliquez sur l’instance de rôle hello.
2. Bonjour **propriétés** volet Hello portail Azure, prenez hello suivant conditions tooresolve votre problème :
   * Si l’instance de rôle hello s’est arrêtée récemment (vous pouvez vérifier la valeur hello **nombre d’abandons**), déploiement de hello peut être mise à jour. Attente toosee si l’instance de rôle hello recommence à fonctionner sur son propre.
   * Si l’instance de rôle hello est **occupé**, vérifiez votre toosee de code d’application si hello [StatusCheck](https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleenvironment.statuscheck) événement est géré. Que vous deviez tooadd ou corriger le code qui gère cet événement.
   * Passez en revue les données de diagnostic hello et scénarios de dépannage dans le billet de blog hello [données de diagnostic de calcul PaaS Azure](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).

> [!WARNING]
> Si vous recyclez votre service cloud, vous réinitialisez propriétés hello pour le déploiement de hello, effacement efficacement les informations hello pour le problème d’origine de hello.
>
>

## <a name="next-steps"></a>Étapes suivantes
Affichez plus d’ [articles de résolution des problèmes](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) liés aux services cloud.

toolearn comment le rôle du service cloud tootroubleshoot problèmes à l’aide de données de diagnostic d’ordinateur PaaS Azure, consultez [série du blog de Kevin Williamson](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx).
