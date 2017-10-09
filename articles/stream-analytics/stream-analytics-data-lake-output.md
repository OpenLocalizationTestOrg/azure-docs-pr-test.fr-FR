---
title: "aaaStream la sortie de magasin de données Analytique Lake | Documents Microsoft"
description: "Configuration de l’authentification et de l’autorisation d’Azure Data Lake Store dans un travail Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a>Sortie de Stream Analytics Data Lake Store
Les travaux Stream Analytics prennent en charge plusieurs méthodes de sortie, dont [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/). Azure Data Lake Store est un référentiel d'entreprise à très grande échelle pour les charges de travail d'analyse du Big Data. Data Lake Store vous permet de toostore les données de n’importe quelle vitesse de taille, de type et de réception pour l’analytique opérationnelle et exploratoire.

## <a name="authorize-a-data-lake-store-account"></a>Autoriser un compte Data Lake Store
1. Si Data Lake Store est sélectionnée comme une sortie Bonjour portail Azure, vous devez utiliser tooauthorize votre Data Lake Store existant ou d’un toorequest accéder toohello Data Lake Store via hello portail classique.
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. Si vous avez déjà accès tooData Lake Store, cliquez sur « Autoriser » et pendant un bref instant une page s’affiche indiquant « Tooauthorization redirection ». page de Hello se fermera automatiquement et vous n’aurez page hello qui vous permettrait tooconfigure hello Data Lake Store sortie.

Si vous n'êtes pas inscrit à Data Lake Store, vous pouvez suivre la demande des hello de support pour les tooinitiate de lien hello « Connexion », ou suivez hello [obtenir des instructions démarrées](../data-lake-store/data-lake-store-get-started-portal.md).

## <a name="configure-hello-data-lake-store-output-properties"></a>Configurer les propriétés de sortie hello Data Lake Store
Une fois que vous avez compte Data Lake Store de hello authentifié, vous pouvez configurer les propriétés de hello pour votre sortie Data Lake Store. tableau Hello ci-dessous est liste hello des noms de propriétés et leur tooconfigure description que votre Data Lake Store de sortie.

<table>
<tbody>
<tr>
<td><B>NOM DE LA PROPRIÉTÉ</B></td>
<td><B>DESCRIPTION</B></td>
</tr>
<tr>
<td>Alias de sortie</td>
<td>Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis Data Lake Store.</td>
</tr>
<tr>
<td>Compte Data Lake Store</td>
<td>nom Hello hello du compte de stockage où vous envoyez votre sortie. Une liste des comptes Data Lake Store hello à l’utilisateur connecté a accès à s’affiche.</td>
</tr>
<tr>
<td>Séquence d’octets préfixe du chemin d’accès [<I>facultative</I>]</td>
<td>Hello toowrite de chemin d’accès du fichier vos fichiers au sein de hello spécifié le compte de magasin Data Lake. <BR>{date}, {time}<BR>Exemple 1 : dossier1/journaux/{date}/{heure}<BR>Exemple 2 : dossier1/journaux/{date}</td>
</tr>
<tr>
<td>Format de la date [<I>facultatif</I>]</td>
<td>Si le jeton de date hello est utilisé dans le chemin d’accès de hello préfixe, vous pouvez sélectionner le format de date hello dans lequel vos fichiers sont organisés. Exemple : JJ/MM/AAAA</td>
</tr>
<tr>
<td>Format de l’heure [<I>facultatif</I>]</td>
<td>Si le jeton de durée hello est utilisé dans le chemin d’accès de hello préfixe, spécifiez le format d’heure hello dans lequel vos fichiers sont organisés. Valeur de hello uniquement pris en charge actuellement est HH.</td>
</tr>
<tr>
<td>Format de sérialisation de l’événement</td>
<td>Format de sérialisation pour les données de sortie. JSON, CSV et Avro sont pris en charge.</td>
</tr>
<tr>
<td>Encodage</td>
<td>S’il s’agit du format CSV ou JSON, un encodage doit être spécifié. UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant.</td>
</tr>
<tr>
<td>Délimiteur</td>
<td>Applicable uniquement pour la sérialisation CSV. Stream Analytics prend en charge un certain nombre de délimiteurs communs pour sérialiser des données CSV. Valeurs prises en charge : virgule, point-virgule, espace, tabulation et barre verticale.</td>
</tr>
<tr>
<td>Format</td>
<td>Applicable uniquement pour la sérialisation JSON. Ligne séparée spécifie la sortie de hello sera formatée en par chaque objet JSON séparé par une nouvelle ligne. Le tableau spécifie que sortie de hello sera mise en forme en tant que tableau d’objets JSON.</td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a>Renouveler une autorisation Data Lake Store
Actuellement, il agit d’une limitation où le jeton d’authentification hello doit toobe actualisée manuellement tous les 90 jours pour tous les travaux avec une sortie de Data Lake Store. Vous devez également toore-authentifier votre compte Data Lake Store si vous avez modifié votre mot de passe depuis la création ou de dernière authentification de votre travail. Un symptôme de ce problème est aucune sortie de travail et une erreur dans les journaux des opérations de hello indiquant la nécessité pour l’autorisation de nouveau.

tooresolve ce problème, arrêtez votre travail en cours d’exécution et accédez de sortie tooyour Data Lake Store. Cliquez sur le lien de « Renouveler l’autorisation » hello et pendant une brève période une page s’affiche indiquant « Redirection tooauthorization.. ». page de Hello se fermera automatiquement et en cas de réussite, indiquera « Autorisation a été renouvelée ». Vous devez tooclick « Enregistrer » en bas de hello de page de hello, puis pouvez continuer en redémarrant votre travail à partir de la perte de données heure du dernier arrêt tooavoid de hello.

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

