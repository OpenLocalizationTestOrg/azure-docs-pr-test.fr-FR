---
title: "Runbook Worker hybride : une tâche de runbook se termine avec l’état suspendu | Microsoft Docs"
description: "Causes des problèmes et résolutions en cas d’erreur provoquant la fin de la tâche Runbook Worker hybride."
services: automation
documentationcenter: 
author: mgoedtel
manager: jwhit
editor: tysonn
ms.assetid: 02c6606e-8924-4328-a196-45630c2255e9
ms.service: automation
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/17/2016
ms.author: magoedte
ms.openlocfilehash: 513a90d144e7ade9c21cd7f3b718578989702c25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="hybrid-runbook-worker-a-runbook-job-terminates-with-a-status-of-suspended"></a>Runbook Worker hybride : une tâche de runbook se termine avec l’état suspendu
## <a name="summary"></a>Résumé
Le runbook est interrompu peu après la tentative de tooexecute il trois fois. Il existe des conditions susceptibles d’interrompre runbook hello de s’exécuter correctement et le message d’erreur lié hello n’inclut pas d’informations supplémentaires indiquant la raison pour laquelle. Cet article fournit des étapes de dépannage pour les problèmes connexes toohello Runbook Worker hybride runbook défaillantes.

Si votre problème Azure n’est pas abordé dans cet article, visitez hello forums Azure sur [MSDN et hello Stack Overflow](https://azure.microsoft.com/support/forums/). Vous pouvez publier votre problème sur ces forums ou trop[ @AzureSupport sur Twitter](https://twitter.com/AzureSupport). En outre, vous pouvez entrer une demande de support Azure en sélectionnant **obtenir un support technique** sur hello [prise en charge Azure](https://azure.microsoft.com/support/options/) site.

## <a name="symptom"></a>Symptôme
Échec de l’exécution du Runbook et hello erreur est retournée, « hello action de tâche 'Activate' ne peut pas être exécuté, car arrêt inattendu du processus de hello. action de tâche Hello a été tentée 3 fois. »

## <a name="cause"></a>Cause :
Il existe plusieurs causes possibles pour l’erreur de hello : 

1. processus de travail hybride Hello est derrière un pare-feu ou proxy
2. Hello worker hybride de hello ordinateur est en cours d’exécution est inférieure à la configuration matérielle minimale hello [configuration requise](automation-hybrid-runbook-worker.md#hybrid-runbook-worker-requirements) 
3. Hello runbook ne peut pas s’authentifier avec les ressources locales

## <a name="cause-1-hybrid-runbook-worker-is-behind-proxy-or-firewall"></a>Cause 1 : Le runbook worker hybride est derrière un proxy ou un pare-feu
hello d’ordinateur Hello que runbook Worker hybride est en cours d’exécution est derrière un pare-feu ou un serveur proxy et un accès réseau sortant est peut-être pas autorisé ou configuré correctement.

### <a name="solution"></a>Solution
Vérifiez que hello équipé d’un accès sortant too*.cloudapp .net sur les ports 443, 9354 et 30000 à 30199. 

## <a name="cause-2-computer-has-less-than-minimum-hardware-requirements"></a>Cause 2 : L’ordinateur ne dispose pas de la configuration minimale requise
Ordinateurs exécutant hello Runbook Worker hybride doit satisfaire aux hello configuration matérielle minimale requise avant de désigner toohost cette fonctionnalité. Sinon, en fonction de l’utilisation des ressources hello d’autres processus d’arrière-plan et la contention provoqué par des procédures opérationnelles lors de l’exécution, ordinateur de hello sera devenir surchargé et entraîner des retards de travail de runbook ou des délais d’attente. 

### <a name="solution"></a>Solution
Vérifiez tout d’abord hello désigné la fonctionnalité de Runbook Worker hybride toorun hello requise hello matérielle.  Dans ce cas, surveillez toodetermine de l’utilisation du processeur et mémoire toute corrélation entre les performances hello de processus de travail de Runbook hybride et Windows.  S’il existe de mémoire ou surcharge des ressources processeur, cela peut indiquer hello besoin tooupgrade ou ajoutez des processeurs supplémentaires ou augmentation mémoire tooaddress hello goulot d’étranglement des ressources et résoudre l’erreur de hello. Vous pouvez également sélectionner une ressource de calcul différents qui peut prendre en charge les exigences minimales hello et mettre à l’échelle lorsque les charges de travail indiquent qu'une augmentation est nécessaire.         

## <a name="cause-3-runbooks-cannot-authenticate-with-local-resources"></a>Cause 3 : Les runbooks ne peuvent pas s’authentifier auprès des ressources locales
### <a name="solution"></a>Solution
Vérifiez hello **Microsoft-SMA** journal des événements pour un événement correspondant avec la description *processus Win32 s’est terminé avec le code [4294967295]*.  cause Hello de cette erreur est vous n’avez pas encore configuré l’authentification dans les procédures opérationnelles ou spécifié hello exécuter en tant qu’informations d’identification pour le groupe de travail hybride hello.  Passez en revue [Runbook autorisations](automation-hybrid-runbook-worker.md#runbook-permissions) tooconfirm que vous avez correctement configuré l’authentification pour les procédures opérationnelles.  

