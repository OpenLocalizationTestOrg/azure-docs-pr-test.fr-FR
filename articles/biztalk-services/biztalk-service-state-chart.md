---
title: "aaaTasks autorisés dans les différents États ou des États dans BizTalk Services | Documents Microsoft"
description: "Hello actions/opérations autorisées dans un état différent MABS : arrêter, Démarrer, redémarrer, suspendre, reprendre, supprimer, mettre à l’échelle, mettez à jour la configuration et sauvegarde"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: aea738f3-ec76-4099-a41b-e17fea9e252f
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/08/2016
ms.author: mandia
ms.openlocfilehash: 643307ba6fa9b05c82b867912feab249c42b65dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="what-you-can-and-cant-do-using-hello-biztalk-service-state"></a>Vous pouvez et ne pouvez pas faire à l’aide de hello état du BizTalk Service

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

En fonction de l’état actuel de hello Hello service BizTalk, il existe des opérations que vous pouvez ou ne peut pas effectuer de hello service BizTalk.

Par exemple, vous devez configurer un service BizTalk Bonjour portail Azure classic. Lorsqu’il s’achève avec succès, hello service BizTalk est en `active` état. État actif de hello, vous pouvez arrêter, suspendre et supprimer le service BizTalk hello. Si vous arrêtez le service BizTalk hello, arrêt, puis hello BizTalk service passe tooa `StopFailed` état. Bonjour `StopFailed` d’état, vous pouvez redémarrer le service BizTalk hello. Si vous essayez d’une opération qui n’est pas autorisée, comme la reprise, hello l’erreur suivante se produit :

`Operation not allowed`

## <a name="view-hello-possible-states"></a>Afficher les états possibles de hello

les tables suivantes de Hello opérations hello de liste ou les actions qui peuvent être effectuées lorsque hello BizTalk Service est dans un état spécifique. Un ✔ signifie l’opération de hello est autorisée dans cet état. Une entrée vide signifie l’opération de hello ne peut pas être effectuée dans cet état.

| État du service | Démarrer | Arrêter | Redémarrer | Interrompre | Reprendre | Supprimer | Mettre à l'échelle | Mettre à jour <br/> Configuration | Backup  |
| --- | --- | --- | --- | --- | --- | --- |--- | --- | --- |
| Actif |  | ✔ | ✔ | ✔ |  | ✔ |✔ |✔ |✔ |
| Désactivé |  |  |  |  |  | ✔ | |  |  | 
| Interrompu |  |  |  |  | ✔ | ✔ | |  | ✔ |
| Arrêté | ✔ |  | ✔ |  |  | ✔ | |  | ✔ |
| Échec de mise à jour du service |  |  |  |  |  | ✔ | |  |  | 
| DisableFailed |  |  |  |  |  | ✔ | |  |  | 
| EnableFailed |  |  |  |  |  | ✔ | |  |  | 
| StartFailed <br/> StopFailed <br/> RestartFailed | ✔ | ✔ | ✔ |  |  | ✔ | | ✔ | |
| SuspendedFailed <br/> ResumeFailed|  |  |  | ✔ | ✔ | ✔ | |  |  | 
| CreatedFailed <br/> RestoreFailed |  |  |  |  |  | ✔ | |  |  | 
| ConfigUpdateFailed  |  |  | ✔ |  |  | ✔ | |✔ | |
| ScaleFailed |  |  |  |  |  | ✔ |✔ | |  |  | 



## <a name="see-also"></a>Voir aussi
* [Créez un BizTalk Service à l’aide de hello portail Azure classic](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [Ce que vous pouvez faire dans les onglets de tableau de bord, surveiller et échelle hello dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [Ce que vous obtenez avec les éditions Developer, Basic, Standard et Premium de hello dans BizTalk Services](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [Comment tooback et restaurez un BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [Qu’est-ce que la limitation dans BizTalk Services ?](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>
* [Récupérer hello Service Bus et contrôle d’accès au nom et à l’émetteur valeurs clé d’émetteur pour votre BizTalk Service](http://go.microsoft.com/fwlink/p/?LinkID=303941)<br/>
* [Comment puis-je démarrer à l’aide de hello SDK des Services BizTalk Azure](http://go.microsoft.com/fwlink/p/?LinkID=302335)

