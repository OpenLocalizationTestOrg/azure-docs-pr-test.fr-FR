---
title: expressions aaaRegular Analytique des journaux OMS journal recherche | Documents Microsoft
description: "Vous pouvez utiliser le mot clé de RegEx hello dans Analytique de journal journal recherches toohello hello résultats du filtrage en fonction de tooa des expressions régulières.  Cet article fournit la syntaxe de hello pour ces expressions avec plusieurs exemples."
services: log-analytics
documentationcenter: 
author: bwren
manager: carmonm
editor: 
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/08/2017
ms.author: bwren
ms.openlocfilehash: 3033593dac2c50e911fc69054947d40d4a74369b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="using-regular-expressions-toofilter-log-searches-in-log-analytics"></a>À l’aide d’expressions régulières toofilter journal recherche Analytique de journal

[Recherche de journal](log-analytics-log-searches.md) vous permettent d’informations de tooextract du référentiel d’Analytique de journal hello.  [Expressions de filtre](log-analytics-search-reference.md#filter-expressions) permettent de résultats de hello toofilter de recherche hello en fonction de critères de toospecific.  Hello **RegEx** mot clé vous permet de toospecify une expression régulière pour ce filtre.  

Cet article fournit des détails sur la syntaxe d’expression régulière hello utilisée par le journal Analytique.

> [!NOTE]
> Vous pouvez uniquement utiliser RegEx avec des champs pouvant faire l’objet d’une recherche.  Pour plus d’informations sur les champs pouvant faire l’objet d’une recherche, consultez **Types de champs** dans [Trouver des données avec les recherches dans les journaux dans Log Analytics](log-analytics-log-searches.md#use-additional-filters).


## <a name="regex-keyword"></a>Mot clé RegEx

Hello utilisation suivant hello toouse de syntaxe **RegEx** mot clé dans une recherche de journal.  Vous pouvez utiliser hello autres sections de cette syntaxe de hello article toodetermine d’expression régulière de hello lui-même.

    field:Regex("Regular Expression")
    field=Regex("Regular Expression")

Par exemple, des enregistrements toouse une alerte tooreturn d’expression régulière avec un type de *avertissement* ou *erreur*, vous utiliseriez hello suivant recherche de journal.

    Type=Alert AlertSeverity=RegEx("Warning|Error")

## <a name="partial-matches"></a>Correspondances partielles
Notez que les expressions régulières hello doivent correspondre à hello tout texte de propriété de hello.  Les correspondances partielles ne renvoient aucun enregistrement.  Par exemple, si vous essayez de tooreturn des enregistrements à partir d’un ordinateur nommé srv01.contoso.com, hello suivant recherche de journal sera **pas** retourner tous les enregistrements.

    Computer=RegEx("srv..")

Il s’agit, car seuls hello première partie du nom de hello correspond à l’expression régulière de hello.  Hello suivant recherche dans les deux journaux retourne les enregistrements à partir de cet ordinateur, car ils correspondent à la totalité du nom hello.

    Computer=RegEx("srv..@")
    Computer=RegEx("srv...contoso.com")

## <a name="characters"></a>Caractères
Cette section décrit les méthodes vous permettant de spécifier différents caractères.

| Caractère | Description | Exemple | Exemples de correspondances |
|:--|:--|:--|:--|
| a | Une occurrence du caractère de hello. | Computer=RegEx("srv01.contoso.com") | srv01.contoso.com |
| . | N’importe quel caractère unique. | Computer=RegEx("srv...contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| a? | Zéro ou une occurrence du caractère de hello. | Computer=RegEx("srv01?.contoso.com") | srv0.contoso.com<br>srv01.contoso.com |
| a* | Zéro ou plusieurs occurrences d’un caractère hello. | Computer=RegEx("srv01*.contoso.com") | srv0.contoso.com<br>srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| a+ | Une ou plusieurs occurrences d’un caractère hello. | Computer=RegEx("srv01+.contoso.com") | srv01.contoso.com<br>srv011.contoso.com<br>srv0111.contoso.com |
| [*abc*] | Correspond à n’importe quel caractère unique entre les crochets hello | Computer=RegEx("srv0[123].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [*a*-*z*] | Correspond à un caractère unique dans la plage de hello.  Peut inclure plusieurs plages. | Computer=RegEx("srv0[1-3].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| [^*abc*] | Aucun des caractères de hello de crochets de hello | Computer=RegEx("srv0[^123].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [^*a*-*z*] | Aucun des caractères hello dans la plage de hello. | Computer=RegEx("srv0[^1-3].contoso.com") | srv05.contoso.com<br>srv06.contoso.com<br>srv07.contoso.com |
| [*n*-*m*] | Correspondance avec une plage de caractères numériques. | Computer=RegEx("srv[01-03].contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |
| @ | N’importe quelle chaîne de caractères. | Computer=RegEx("srv@.contoso.com") | srv01.contoso.com<br>srv02.contoso.com<br>srv03.contoso.com |


## <a name="multiple-occurences-of-character"></a>Plusieurs occurrences d’un caractère
Cette section décrit les méthodes vous permettant de spécifier plusieurs occurrences d’un caractère spécifique.

| Caractère | Description | Exemple | Exemples de correspondances |
|:--|:--|:--|:--|
| a{n} |  *n*occurrences d’un caractère hello. | Computer=RegEx("bw-win-sc01{3}.bwren.lab") | bw-win-sc0111.bwren.lab |
| a{n,} |  *n*ou plusieurs occurrences d’un caractère hello. | Computer=RegEx("bw-win-sc01{3,}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab<br>bw-win-sc0111111.bwren.lab |
| a{n,m} |  *n*trop*m* occurrences d’un caractère hello. | Computer=RegEx("bw-win-sc01{3,5}.bwren.lab") | bw-win-sc0111.bwren.lab<br>bw-win-sc01111.bwren.lab<br>bw-win-sc011111.bwren.lab |


## <a name="logical-expressions"></a>Expressions logiques
Cette section décrit les méthodes vous permettant de spécifier une sélection parmi plusieurs valeurs.

| Caractère | Description | Exemple | Exemples de correspondances |
|:--|:--|:--|:--|
| &#124; | OR logique.  Renvoie un résultat en cas de correspondance avec l’une des expressions. | Type=Alert AlertSeverity=RegEx("Avertissement&#124;Erreur") | Avertissement<br>Erreur |
| & | AND logique.  Renvoie un résultat en cas de correspondance avec les deux expressions. | EventData=regex("(sécurité.\*&.\*réussi.\*)") | Audit de sécurité réussi |


## <a name="literals"></a>Littéraux
Convertit les caractères spéciaux tooliteral caractères.  Cela inclut des caractères qui fournissent des fonctionnalités tooregular expressions comme ?-\*^\[\]{}\(\)+\|. &.

| Caractère | Description | Exemple | Exemples de correspondances |
|:--|:--|:--|:--|
| \\ | Convertit un littéral de tooa de caractère spécial. | Status_CF=\\[Erreur\\]@<br>Status_CF=Erreur\\-@ | [Erreur]Fichier introuvable.<br>Erreur-Fichier introuvable. |


## <a name="next-steps"></a>Étapes suivantes

* Se familiariser avec [recherche de journal](log-analytics-log-searches.md) tooview et analyser les données dans le référentiel d’Analytique de journal hello.
