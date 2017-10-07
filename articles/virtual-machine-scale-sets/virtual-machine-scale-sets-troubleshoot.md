---
title: "mise à l’échelle d’aaaTroubleshoot avec des machines virtuelles identiques | Documents Microsoft"
description: "Dépanner la mise à l’échelle automatique avec des jeux de mise à l’échelle de machine virtuelle Comprendre les problèmes courants rencontrés et comment tooresolve les."
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: c7d87b72-ee24-4e52-9377-a42f337f76fa
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: windows
ms.devlang: na
ms.topic: article
ms.date: 10/28/2016
ms.author: guybo
ms.openlocfilehash: 4c9a70992348d87fb43646421a90a027bf400a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-autoscale-with-virtual-machine-scale-sets"></a>Dépannage de la mise à l’échelle automatique avec des jeux de mise à l’échelle de machine virtuelle
**Problème** : vous avez créé une infrastructure de l’échelle automatique dans Azure Resource Manager à l’aide de jeux de mise à l’échelle de machine virtuelle – par exemple par le déploiement d’un modèle comme suit : https://github.com/Azure/azure-quickstart-templates/tree/master/201- mise d’eau échelle – que vous avez vos règles de mise à l’échelle définies, et il fonctionne très bien, sauf que, quel que soit la quantité de charge vous placer sur hello machines virtuelles, il ne sera pas mise à l’échelle.

## <a name="troubleshooting-steps"></a>Étapes de dépannage
Tooconsider de certains éléments sont les suivantes :

* Nombre de noyaux chaque machine virtuelle et vous chargez chaque cœur ? modèle de démarrage rapide d’Azure exemple Hello ci-dessus dispose d’un script de do_work.php, ce qui charge un seul cœur. Si vous utilisez une machine virtuelle supérieure à un seul cœur de taille de machine virtuelle comme Standard_A1 ou D1, vous devez toorun cette charge plusieurs fois. Vérifiez le nombre de cœurs de vos machines virtuelles en consultant [Tailles des machines virtuelles Windows dans Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
* Le nombre de machines virtuelles dans hello ensemble d’échelle de machine virtuelle, vous effectuez travail sur chacun d’eux ?
  
    Une montée en charge l’événement a lieu uniquement lorsque hello moyenne du processeur sur **tous les** hello machines virtuelles dans un ensemble d’échelle dépasse hello valeur de seuil, au fil du temps hello internes défini dans les règles de mise à l’échelle hello.
* Vous avez manqué un événement de mise à l’échelle ?
  
    Vérifiez les journaux de d’audit de hello Bonjour portail Azure pour les événements de mise à l’échelle. Peut-être qu’une mise à l’échelle vers le haut ou vers le bas a été ignorée. Vous pouvez filtrer sur « Mise à l’échelle ».
  
    ![Journaux d’audit][audit]
* Les seuils d’augmentation et de diminution de la taille des instances sont-ils suffisamment différents ?
  
    Supposons que vous définir un tooscale règle out lorsque l’UC moyenne est supérieure à 50 % plus de 5 minutes et tooscale dans lorsque la moyenne du processeur est inférieure à 50 %. Cela entraînerait un problème « battements » lors de l’utilisation du processeur est le seuil de fermer toothis, avec des actions de mise à l’échelle en permanence l’augmentation et diminution hello taille du jeu de hello. Pour cette raison, hello mise à l’échelle le service tente tooprevent « bagottement », ce qui peut se manifester par ne pas mise à l’échelle. Par conséquent, assurez-vous que votre montée en puissance parallèle et seuils d’échelle sont tooallow assez différent de l’espace entre la mise à l’échelle.
* Avez-vous écrit votre propre modèle JSON ?
  
    Il est facile de toomake erreurs, par conséquent, démarrer avec un modèle comme hello celle ci-dessus qui s’avère toowork et apporter les modifications incrémentielles. 
* Pouvez vous procéder manuellement à une augmentation ou à une diminution de la taille des instances ?
  
    Essayez de redéploiement hello ensemble d’échelle de machine virtuelle de ressource avec un autre « capacity » définition toochange hello du nombre de machines virtuelles manuellement. Un toodo de modèle exemple il s’agit ici : https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-scale-existing – vous devrez peut-être tooedit hello modèle toomake qu’elle a hello même de taille de l’ordinateur qu’utilise votre ensemble d’échelle. Si vous pouvez modifier correctement manuellement de nombre hello d’ordinateurs virtuels, vous savez que problème de hello est tooautoscale isolé.
* Vérifiez votre Microsoft.Compute/virtualMachineScaleSet et les ressources Microsoft.Insights hello [Explorateur de ressources Azure](https://resources.azure.com/)
  
    Il s’agit d’une indispensable outil qui vous indique de dépannage hello l’état de vos ressources Azure Resource Manager. Cliquez sur votre abonnement et examinez hello groupe de ressources de dépannage. Sous le fournisseur de ressources de calcul hello examiner hello ensemble d’échelle de machine virtuelle vous avez créé et vérifier hello vue d’Instance, qui vous indique l’état d’un déploiement de hello. Vérifiez également la vue d’instance hello de machines virtuelles dans hello ensemble d’échelle de machine virtuelle. Aller dans le fournisseur de ressources Microsoft.Insights hello, puis vérifiez les règles de mise à l’échelle hello bonnes.
* Hello extension Diagnostic fonctionne et l’émission de données de performances ?
  
    **Mise à jour :** échelle automatique Azure a été améliorée toouse un ordinateur hôte en fonction de pipeline de mesures qui ne requiert plus un toobe d’extension de diagnostics installé. Cela signifie hello prochains paragraphes ne s’appliquent plus si vous créez une application de l’échelle automatique à l’aide du nouveau pipeline de hello. Est un exemple de modèles Azure auxquels ont été pipeline d’hôte toouse converti hello : https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale. 
  
    À l’aide de mesures de l’ordinateur hôte en fonction de mise à l’échelle est préférable pour hello suivant raisons :
  
  * Moins de pièces mobiles en tant qu’aucune extension de diagnostics doivent toobe installé.
  * Les modèles sont plus simples. Ajoutez simplement le modèle de jeu d’insights échelle règles tooan existante mise à l’échelle.
  * Reporting plus fiable et lancement plus rapide de nouvelles machines virtuelles.
    
    Hello uniquement les raisons souhaité à l’aide d’une extension de diagnostic de tookeep serait si vous avez besoin de mémoire diagnostics reporting/mise à l’échelle. Les mesures basées sur l’hôte ne génèrent aucun rapport sur la mémoire.
    
    Dans cette optique, seulement suivez hello cet article si vous utilisez toujours des extensions de diagnostic pour votre échelle.
    
    Mise à l’échelle dans Azure Resource Manager peut fonctionner (mais n’a plus à) au moyen d’une extension de machine virtuelle appelée hello Extension des Diagnostics. Il émet un compte de stockage performances données tooa que vous définissez dans le modèle de hello. Ces données sont agrégées puis par service du moniteur de Windows Azure hello.
    
    Si hello service Insights ne peut pas lire les données à partir de machines virtuelles de hello, il est supposé toosend un message électronique, par exemple, si les machines virtuelles de hello ont été vers le bas, vérifiez votre adresse de messagerie (hello une vous avez spécifié lors de la création de hello compte Azure).
    
    Vous pouvez également et consulter les données de hello vous-même. Examinez hello compte de stockage Azure à l’aide d’un Explorateur de cloud. Par exemple à l’aide de hello [Visual Studio Cloud Explorer](https://visualstudiogallery.msdn.microsoft.com/aaef6e67-4d99-40bc-aacf-662237db85a2), connectez-vous et choisissez hello abonnement Azure que vous utilisez, et hello compte de stockage de Diagnostics nom référencé dans hello définition d’extension de Diagnostics dans votre déploiement modèle...
    
    ![Cloud Explorer][explorer]
    
    Ici, vous verrez un certain nombre de tables où les données hello à partir de chaque ordinateur virtuel sont stockées. Prenant Linux et hello métrique de l’UC par exemple, examinez de lignes les plus récentes hello. Hello Visual Studio cloud explorer prend en charge un langage de requête afin de pouvoir exécuter une requête semblable à « Timestamp gt datetime'2016-02-02T21:20:00Z » « toomake que vous obtenez les événements les plus récents hello (à supposer que heure est au format UTC). Données hello que vous voyez dans il correspondent toohello évolue des règles définies ? Dans l’exemple hello ci-dessous, hello du processeur pour l’ordinateur 20 démarrée augmente de too100 % dans hello 5 dernières minutes...
    
    ![Tables de stockage][tables]
    
    Si les données de salutation n’y ne figurent pas, il implique des problème de hello est avec extension de diagnostic hello en hello machines virtuelles. Si les données de salutation n’y figure, il implique soit un problème avec vos règles de mise à l’échelle ou service de Insights hello. Vérifiez le [statut Azure](https://azure.microsoft.com/status/).
    
    Une fois que vous avez effectué ces étapes, si vous rencontrez toujours des problèmes de mise à l’échelle, vous pouvez essayer les forums hello [MSDN](https://social.msdn.microsoft.com/forums/azure/home?category=windowsazureplatform%2Cazuremarketplace%2Cwindowsazureplatformctp), ou [débordement de pile](http://stackoverflow.com/questions/tagged/azure), ou un journal d’un appel de la prise en charge. Être modèle hello de tooshare préparée et une vue des données de performances hello.

[audit]: ./media/virtual-machine-scale-sets-troubleshoot/image3.png
[explorer]: ./media/virtual-machine-scale-sets-troubleshoot/image1.png
[tables]: ./media/virtual-machine-scale-sets-troubleshoot/image4.png
