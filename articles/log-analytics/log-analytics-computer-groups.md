---
title: "groupes d’aaaComputer dans le journal Analytique ouvrir recherche | Documents Microsoft"
description: "Groupes d’ordinateurs dans le journal Analytique autoriser tooscope journal recherches tooa particulier ensemble d’ordinateurs.  Cet article décrit les méthodes différentes hello vous pouvez utiliser des groupes d’ordinateurs toocreate et comment toouse dans un journal de recherche."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: a28b9e8a-6761-4ead-aa61-c8451ca90125
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: bwren
ms.openlocfilehash: 7dafea9829e541f5582a1d855fafb82aa4d94430
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="computer-groups-in-log-analytics-log-searches"></a>Groupes d’ordinateurs dans les recherches de journal Log Analytics

>[!NOTE]
> Cet article décrit l’utilisation hello des groupes d’ordinateurs à l’aide du langage de requête journal Anayltics hello actuel.    Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis les groupes d’ordinateurs fonctionnent différemment.  Notes sont fournies dans cet article avec une syntaxe différente hello et le comportement d’un nouveau langage de requête hello.  


Groupes d’ordinateurs dans le journal Analytique permettent tooscope [recherche de journal](log-analytics-log-searches.md) tooa d’ensemble spécifique d’ordinateurs.  Vous peuplez chaque groupe d’ordinateurs soit à l’aide d’une requête que vous définissez, soit en important des groupes à partir de différentes sources.  Lorsque le groupe de hello est inclus dans une recherche de journal, les résultats de hello sont limitées toorecords qui correspondent aux ordinateurs hello dans le groupe de hello.

## <a name="creating-a-computer-group"></a>Création d’un groupe d’ordinateurs
Vous pouvez créer un groupe d’ordinateurs dans Analytique de journal à l’aide d’une des méthodes de hello Bonjour tableau suivant.  Vous trouverez des détails sur chaque méthode dans les sections hello ci-dessous. 

| Méthode | Description |
|:--- |:--- |
| Recherche dans les journaux |Créer une recherche de journal qui retourne une liste d’ordinateurs et enregistrer les résultats de hello sous un groupe d’ordinateurs. |
| API Recherche de journal |Utilisez hello API de recherche de journal tooprogrammatically créer un groupe d’ordinateurs basé sur les résultats de hello d’une recherche de journal. |
| Active Directory |Analyser automatiquement l’appartenance au groupe de hello de tous les ordinateurs de l’agent qui sont membres d’un domaine Active Directory et créer un groupe dans le journal Analytique pour chaque groupe de sécurité. |
| WSUS |Analyser automatiquement des serveurs ou clients WSUS pour des groupes de ciblage, et créer un groupe pour chacun d’eux dans Log Analytics. |

### <a name="log-search"></a>Recherche dans les journaux
Groupes d’ordinateurs créés à partir d’une recherche de journal contient tous les ordinateurs de hello retournés par une requête de recherche que vous définissez.  Cette requête est exécutée à chaque utilisation de groupe d’ordinateurs hello afin qu’elles reflètent toutes les modifications depuis la création de groupe de hello.

Utilisez hello suivant la procédure toocreate un groupe d’ordinateurs à partir d’une recherche de journal.

1. [Créez une recherche de journal](log-analytics-log-searches.md) qui retourne une liste d’ordinateurs.  Hello recherche doit retourner un ensemble distinct d’ordinateurs à l’aide de quelque chose comme **Distinct Computer** ou **measure count() par ordinateur** dans la requête de hello.  
2. Cliquez sur hello **enregistrer** bouton haut hello écran hello.
3. Sélectionnez **Oui** trop**enregistrer cette requête en tant qu’un groupe d’ordinateurs**.
4. Tapez un **nom** et un **catégorie** pour le groupe de hello.  Si une recherche avec hello le même nom et la catégorie déjà existe, puis vous être invité à toooverwrite il.  Vous pouvez avoir plusieurs recherches avec le même nom dans différentes catégories de hello. 

Voici des exemples de recherches que vous pouvez enregistrer en tant que groupe d’ordinateurs.

    Computer="Computer1" OR Computer="Computer2" | distinct Computer 
    Computer=*srv* | measure count() by Computer

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md) hello modifications suivantes sont effectuées toohello procédure toocreate un groupe d’ordinateurs.
>  
> - Hello toocreate requête un groupe d’ordinateurs doit inclure `distinct Computer`.  Voici un exemple d’une requête de toocreate un groupe d’ordinateurs.<br>`Heartbeat | where Computer contains "srv" `
> - Lorsque vous créez un groupe d’ordinateurs, vous devez spécifier un alias dans le nom de toohello d’addition.  Vous utilisez des alias de hello lors de l’utilisation de groupe d’ordinateurs hello dans une requête comme décrit ci-dessous.  

### <a name="log-search-api"></a>API Recherche de journal
Groupes d’ordinateurs créés avec hello API de recherche de journal sont même hello en tant que recherches créées avec une recherche de journal.

Pour plus d’informations sur la création d’un groupe d’ordinateurs à l’aide des API de recherche de journal de hello, consultez [API REST de recherche de groupes d’ordinateurs dans le journal d’Analytique de journal](log-analytics-log-search-api.md#computer-groups).

### <a name="active-directory"></a>Active Directory
Lorsque vous configurez des appartenances aux groupes Active Directory Analytique de journal tooimport, il analyse l’appartenance au groupe de hello de tous les ordinateurs joints à un domaine avec l’agent OMS a hello.  Un groupe d’ordinateurs est créé dans le journal Analytique pour chaque groupe de sécurité dans Active Directory, et chaque ordinateur est ajouté à des groupes d’ordinateurs toohello correspondant toohello les groupes de sécurité qu’ils sont membres de.  Cet appartenance est mise à jour toutes les 4 heures.  

Vous configurez des groupes de sécurité Active Directory Analytique de journal tooimport de hello **groupes d’ordinateurs** menu Analytique de journal **paramètres**.  Sélectionnez **Automation** puis **Importer les appartenances à des groupes Active Directory depuis les ordinateurs**.  Aucune configuration supplémentaire n’est requise.

![Groupes d’ordinateurs d’Active Directory](media/log-analytics-computer-groups/configure-activedirectory.png)

Lorsque les groupes ont été importés, hello menu listes hello nombre d’ordinateurs avec l’appartenance au groupe a détecté et hello du nombre de groupes importés.  Vous pouvez cliquer sur un de ces hello tooreturn de liens **ComputerGroup** enregistrements avec ces informations.

### <a name="windows-server-update-service"></a>Windows Server Update Service
Lorsque vous configurez Analytique de journal tooimport WSUS les appartenances au groupe, il analyse hello ciblant l’appartenance au groupe de tous les ordinateurs avec l’agent OMS a hello.  Si vous utilisez côté client cible, n’importe quel ordinateur qui est connecté tooOMS et fait partie de n’importe quel WSUS ciblage de groupes a son appartenance au groupe importé tooLog Analytique. Si vous utilisez un serveur cible, hello agent OMS doit être installé sur hello WSUS serveur pour toobe d’informations de l’appartenance de groupe hello importé tooOMS.  Cet appartenance est mise à jour toutes les 4 heures. 

Vous configurez des groupes de sécurité Active Directory Analytique de journal tooimport de hello **groupes d’ordinateurs** menu Analytique de journal **paramètres**.  Sélectionnez **Active Directory** puis **Importer les appartenances à des groupes Active Directory depuis les ordinateurs**.  Aucune configuration supplémentaire n’est requise.

![Groupes d’ordinateurs d’Active Directory](media/log-analytics-computer-groups/configure-wsus.png)

Lorsque les groupes ont été importés, hello menu listes hello nombre d’ordinateurs avec l’appartenance au groupe a détecté et hello du nombre de groupes importés.  Vous pouvez cliquer sur un de ces hello tooreturn de liens **ComputerGroup** enregistrements avec ces informations.

## <a name="managing-computer-groups"></a>Gestion de groupes d’ordinateurs
Vous pouvez afficher les groupes d’ordinateurs qui ont été créés à partir d’une recherche de journal ou hello API de recherche de journal à partir de hello **groupes d’ordinateurs** menu Analytique de journal **paramètres**.  Cliquez sur hello **x** Bonjour **supprimer** groupe d’ordinateurs colonne toodelete hello.  Cliquez sur hello **afficher les membres** icône de recherche de journal de groupe toorun hello d’un groupe qui retourne ses membres. 

![Groupes d’ordinateurs enregistrés](media/log-analytics-computer-groups/configure-saved.png)

toomodify hello de groupe, créez un groupe avec hello même **catégorie** et **nom** groupe de toooverwrite hello d’origine.

## <a name="using-a-computer-group-in-a-log-search"></a>Utilisation d’un groupe d’ordinateurs dans une recherche de journal
Vous utilisez hello suivant du groupe d’ordinateurs syntaxe toorefer tooa dans une recherche de journal.  En spécifiant hello **catégorie** est facultatif et uniquement requis si vous avez des groupes d’ordinateurs avec le même nom dans différentes catégories de hello. 

    $ComputerGroups[Category: Name]

Lorsqu’une recherche est exécutée, les membres de groupes d’ordinateurs inclus dans la recherche de hello hello sont d’abord résolus.  Si le groupe de hello est basé sur une recherche de journal, alors que la recherche est exécutée tooreturn les membres de hello du groupe de hello avant d’effectuer la recherche de journal de niveau supérieur de hello.

Groupes d’ordinateurs sont généralement utilisés avec hello **IN** clause dans recherche de journaux hello comme hello l’exemple suivant :

    Type=UpdateSummary Computer IN $ComputerGroups[My Computer Group]

>[!NOTE]
> Si votre espace de travail a été mis à niveau toohello [Analytique de journal nouveau langage de requête](log-analytics-log-search-upgrade.md), puis vous utilisez un groupe d’ordinateurs dans une requête en traitant de son alias comme une fonction comme hello l’exemple suivant :
> 
>  `UpdateSummary | where Computer IN (MyComputerGroup)`

## <a name="computer-group-records"></a>Enregistrements de groupe d’ordinateurs
Un enregistrement est créé dans le référentiel d’OMS hello pour chaque appartenance au groupe d’ordinateurs créé à partir d’Active Directory ou les services WSUS.  Ces enregistrements ont un type de **ComputerGroup** et ont des propriétés de hello Bonjour tableau suivant.  Des enregistrements ne sont pas créés pour des groupes d’ordinateurs basés sur des recherches de journal.

| Propriété | Description |
|:--- |:--- |
| Type |*ComputerGroup* |
| SourceSystem |*SourceSystem* |
| Ordinateur |Nom d’ordinateur du membre hello. |
| Groupe |Nom du groupe de hello. |
| GroupFullName |Groupe de toohello de chemin d’accès complet, y compris la source de hello et le nom de la source. |
| GroupSource |Source à partir de laquelle ce groupe a été collecté. <br><br>Active Directory<br>WSUS<br>WSUSClientTargeting |
| GroupSourceName |Nom de source de hello hello groupe ont été collectée à partir de.  Pour Active Directory, il s’agit de nom de domaine hello. |
| ManagementGroupName |Nom du groupe d’administration hello pour les agents SCOM.  Pour les autres agents, il s’agit d’AOI-\<workspace ID\> |
| TimeGenerated |Date et heure de groupe d’ordinateurs hello a été créé ou mis à jour. |

## <a name="next-steps"></a>Étapes suivantes
* En savoir plus sur [recherche de journal](log-analytics-log-searches.md) tooanalyze les données de salutation collectées à partir de sources de données et les solutions possibles.  

