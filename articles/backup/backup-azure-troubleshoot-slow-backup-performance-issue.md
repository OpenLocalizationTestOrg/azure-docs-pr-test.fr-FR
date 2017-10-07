---
title: "sauvegarde lente d’aaaTroubleshoot des fichiers et dossiers dans la sauvegarde Azure | Documents Microsoft"
description: "Fournit des toohelp des conseils de dépannage vous diagnostiquez cause hello de problèmes de performances de sauvegarde Azure"
services: backup
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.assetid: e379180a-db13-4e0c-90e4-28e5dd6f5b14
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/13/2017
ms.author: genli
ms.openlocfilehash: 21d79bbd03c2706bc43fcc7c14020cffd6b919c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-slow-backup-of-files-and-folders-in-azure-backup"></a>Résolution des problèmes de sauvegarde lente de fichiers et de dossiers dans Azure Backup
Cet article fournit des conseils de dépannage toohelp vous diagnostiquez cause hello de ralentissement des performances de sauvegarde des fichiers et des dossiers lorsque vous utilisez Azure Backup. Lorsque vous utilisez hello Azure Backup agent tooback des fichiers, les processus de sauvegarde hello peut prendre plus longtemps que prévu. Ce délai peut résulter d’une ou plusieurs des éléments suivants de hello :

* [Sur l’ordinateur de hello est en cours de sauvegarde sont les goulots d’étranglement de performances.](#cause1)
* [Un autre processus ou un logiciel antivirus interfère avec hello les processus de sauvegarde Azure.](#cause2)
* [l’agent de sauvegarde Hello est en cours d’exécution sur une machine virtuelle Azure (VM).](#cause3)  
* [Vous sauvegardez un grand nombre de fichiers (plusieurs millions).](#cause4)

Avant de commencer la résolution des problèmes, nous vous recommandons de télécharger et installer hello [dernier agent Azure Backup](http://aka.ms/azurebackup_agent). Nous apporter des mises à jour fréquentes toohello sauvegarde agent toofix différents problèmes, ajouter des fonctionnalités et améliorer les performances.

Nous vous recommandons également fortement de consulter hello [FAQ de service Azure Backup](backup-azure-backup-faq.md) toomake que vous n’êtes pas confronté un des problèmes courants de configuration hello.

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

<a id="cause1"></a>

## <a name="cause-performance-bottlenecks-on-hello-computer"></a>Cause : Les goulots d’étranglement sur les ordinateur hello
Les goulots d’étranglement sur ordinateur hello qui est en cours de sauvegarde peuvent entraîner des délais. Par exemple, hello toodisk de tooread ou d’écriture de capacité de l’ordinateur, ou données toosend de la bande passante disponible sur le réseau de hello, peut provoquer des goulots d’étranglement.

Windows fournit un outil intégré appelé [l’Analyseur de performances](https://technet.microsoft.com/magazine/2008.08.pulse.aspx) (Perfmon) toodetect ces goulots d’étranglement.

Voici quelques compteurs de performances et plages qui peuvent être utiles pour diagnostiquer les goulots d’étranglement et permettre des sauvegardes optimales.

| Compteur | État |
| --- | --- |
| Disque logique (disque physique)--% temps d’inactivité |• too50 inactif de 100 % %Idle = sain</br>• too20 inactif de 49 % %Idle = avertissement ou l’analyse</br>• too0 inactif de 19 % %Idle = critique ou des spécifications |
| Disque logique (disque physique)--% moy. disque s/lecture ou disque s/écriture |• 0,001 ms de too0.015 ms = sain</br>• 0,015 ms de too0.025 ms = avertissement ou l’analyse</br>• 0,026 ms ou plus = critique ou hors spécifications |
| Disque logique (disque physique)--Taille de file d’attente du disque actuelle (pour toutes les instances) |80 demandes pendant plus de 6 minutes |
| Mémoire--Octets de réserve non paginée |• Moins de 60 % de la réserve utilisée = sain<br>• 61 % too80 % du pool consommée = avertissement ou l’analyse</br>• Plus de 80 % de la réserve utilisée = critique ou hors spécifications |
| Mémoire--Octets de réserve paginée |• Moins de 60 % de la réserve utilisée = sain</br>• 61 % too80 % du pool consommée = avertissement ou l’analyse</br>• Plus de 80 % de la réserve utilisée = critique ou hors spécifications |
| Mémoire--Mégaoctets disponibles |• 50 % de mémoire disponible ou plus = sain</br>• 25 % de mémoire disponible = analyse</br>• 10 % de mémoire disponible = avertissement</br>• Moins de 100 Mo ou 5 % de mémoire disponible = critique ou hors spécifications |
| Processeur--\%temps processeur (toutes les instances) |• Moins de 60 % utilisés = sain</br>• 61 % too90 % consommée = analyse ou une attention</br>• 91 % too100 % consommée = critique |

> [!NOTE]
> Si vous déterminez que l’infrastructure hello est responsable de hello, nous recommandons que vous défragmentez disques hello régulièrement pour de meilleures performances.
>
>

<a id="cause2"></a>

## <a name="cause-another-process-or-antivirus-software-interfering-with-azure-backup"></a>Cause : un autre processus ou logiciel antivirus interfère avec Azure Backup
Nous avons vu plusieurs instances où autres processus Bonjour système Windows ont dégrader les performances de hello processus de l’agent Azure Backup. Par exemple, si vous utilisez hello Azure Backup agent et un autre programme tooback, les données, ou si un logiciel antivirus est en cours d’exécution et a un verrou sur les fichiers toobe sauvegardée, hello plusieurs verrous sur les fichiers peuvent entraîner des conflits. Dans ce cas, hello peut échouer ou tâche de hello peut prendre plus longtemps que prévu.

Hello recommandation la mieux adaptée dans ce scénario est tooturn off hello autres toosee du programme de sauvegarde si l’heure de la sauvegarde hello pour l’agent de sauvegarde Azure hello change. En règle générale, s’assurer que plusieurs opérations de sauvegarde ne sont pas exécutés simultanément hello est suffisamment tooprevent de mutuel.

Pour les programmes antivirus, nous vous recommandons d’exclure les suivant hello fichiers et emplacements :

* C:\Program Files\Microsoft Azure Recovery Services Agent\bin\cbengine.exe as a process
* C:\Program Files\Microsoft Azure Recovery Services Agent\ folders
* Emplacement de travail (si vous n’utilisez pas les emplacement standard hello)

<a id="cause3"></a>

## <a name="cause-backup-agent-running-on-an-azure-virtual-machine"></a>Cause : l’agent de sauvegarde est en cours d’exécution sur une machine virtuelle Azure
Si vous exécutez l’agent de sauvegarde hello sur une machine virtuelle, les performances seront plus lente que lorsque vous l’exécutez sur un ordinateur physique. Ce comportement est attendu en raison de limitations de tooIOPS.  Toutefois, vous pouvez optimiser les performances de hello en basculant les lecteurs de données hello tooAzure stockage Premium sont en cours de sauvegarde. Nous travaillons sur la résolution de ce problème, et correction de hello sera disponible dans une version ultérieure.

<a id="cause4"></a>

## <a name="cause-backing-up-a-large-number-millions-of-files"></a>Cause : vous sauvegardez un grand nombre de fichiers (plusieurs millions)
Le déplacement d’un volume important de données prend plus de temps que le déplacement d’un volume plus restreint de données. Dans certains cas, l’heure de la sauvegarde est lié toonot hello uniquement la taille des données de hello, mais également nombre hello des fichiers ou dossiers. Cela est particulièrement vrai lorsque des millions de petits fichiers (quelques octets tooa quelques kilo-octets) sont en cours de sauvegarde.

Ce comportement se produit parce que pendant que vous êtes sauvegarde des données de hello et en la déplaçant tooAzure, Azure est catalogage simultanément vos fichiers. Dans certains cas rares, l’opération de catalogue hello peut prendre plus longtemps que prévu.

Hello suivant indicateurs peut vous aider à comprendre le goulot d’étranglement hello et de travail en conséquence sur les étapes suivantes de hello :

* **L’interface utilisateur affiche la progression hello pour transférer des données**. Hello données sont toujours transférées. la bande passante du réseau Hello ou taille hello des données pourrait provoquer des délais.
* **L’interface utilisateur ne s’affichent pas progression hello pour transférer des données**. Ouvrez hello journaux situé C:\Microsoft Azure Recovery Services Agent\Temp, puis recherchent à hello entrée FileProvider::EndData dans les journaux hello. Cette entrée signifie que hello le transfert de données terminé et opération de catalogue hello se produit. Ne pas annuler les travaux de sauvegarde hello. Au lieu de cela, attendez un peu plus longtemps hello catalogue opération toofinish. Si hello problème persiste, contactez [prise en charge Azure](https://portal.azure.com/#create/Microsoft.Support).
