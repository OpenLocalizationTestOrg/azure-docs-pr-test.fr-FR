---
title: "aaaTask prédéfini pour Azure Media Indexer"
description: "Cette rubrique offre une vue d’ensemble des tâches prédéfinies pour Azure Media Indexer."
services: media-services
documentationcenter: 
author: Asolanki
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/03/2017
ms.author: adsolank;juliako;
ms.openlocfilehash: ca0b3e7aa9f6dd9fdecddfc5b3137281ed5cef35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="task-preset-for-azure-media-indexer"></a>Tâches prédéfinies pour Azure Media Indexer

Azure Media Indexer est un processeur multimédia que vous utilisez hello tooperform tâches suivantes : effectuer des recherches des fichiers multimédias et contenu, générer des mots clés et des pistes de sous-titres, fichiers d’éléments multimédias qui font partie de votre élément multimédia d’index.

Cette rubrique décrit hello de présélection des tâches que vous devez tooyour toopass l’indexation de travail. Pour obtenir un exemple complet, consultez [Indexation des fichiers multimédias avec Azure Media Indexer](media-services-index-content.md).

## <a name="azure-media-indexer-configuration-xml"></a>Fichier de configuration XML d’Azure Media Indexer

Hello tableau suivant explique les éléments et attributs du fichier XML de configuration hello.

|Nom|Require|Description|
|---|---|---|
|Entrée|true|Fichier (s) actif que vous souhaitez tooindex.<br/>Azure Media Indexer prend en charge hello suivant les formats de fichiers multimédias : MP4, MOV, WMV, MP3, M4A, WMA, AAC, WAV. <br/><br/>Vous pouvez spécifier le nom de fichier hello (s) Bonjour **nom** ou **liste** attribut Hello **d’entrée** élément (comme indiqué ci-dessous). Si vous ne spécifiez pas le tooindex de fichier actif, le fichier primaire de hello est choisi. Si aucun fichier principal n’est définie, le premier fichier de ressource en entrée hello hello est indexé.<br/><br/>tooexplicitly spécifier le nom du fichier multimédia hello, procédez comme :<br/>```<input name="TestFile.wmv" />```<br/><br/>Vous pouvez également indexer plusieurs fichiers d’éléments multimédias à la fois (des fichiers de too10). toodo cela :<br/>- Créez un fichier texte (fichier manifeste) et affectez-lui une extension .lst.<br/>-Ajouter une liste de tous les noms de fichier actif hello dans votre fichier de manifeste toothis élément multimédia d’entrée.<br/>-Ajoutez (Téléchargez) thanifest fichier toohello actif.<br/>-Spécifiez le nom hello du fichier de manifeste hello dans l’attribut de la liste de l’entrée hello.<br/>```<input list="input.lst">```<br/><br/>**Remarque :** si vous ajoutez le fichier manifeste de plus de 10 fichiers toohello, la tâche d’indexation hello échoue avec le code d’erreur hello 2006.|
|metadata|false|Les métadonnées pour hello spécifiées ou les fichiers actifs.<br/>```<metadata key="..." value="..." />```<br/><br/>Vous pouvez fournir des valeurs de clés prédéfinies. <br/><br/>Actuellement, hello suivant clés est pris en charge :<br/><br/>**titre** et **description** -utilisé la précision de reconnaissance vocale tooimprove de modèle de tooupdate hello language.<br/>```<metadata key="title" value="[Title of hello media file]" /><metadata key="description" value="[Description of hello media file]" />```<br/><br/>**username** et **password** : utilisées à des fins d’authentification lors du téléchargement de fichiers Internet via HTTP ou HTTPS.<br/>```<metadata key="username" value="[UserName]" /><metadata key="password" value="[Password]" />```<br/>Hello nom d’utilisateur et les valeurs de mot de passe s’appliquent tooall URL de média dans le manifeste d’entrée de hello.|
|features<br/><br/>ajoutées dans la version 1.2. Actuellement, la fonctionnalité de hello uniquement pris en charge est la reconnaissance vocale (« ASR »).|false|fonctionnalité de reconnaissance vocale Hello a hello suivant les clés de paramètres :<br/><br/>Language :<br/>-hello toobe de langage naturel reconnu dans le fichier multimédia de hello.<br/>- English, Spanish<br/><br/>CaptionFormats :<br/>-une liste délimitée par des points-virgules de hello souhaitée des formats de sortie de légende (le cas échéant)<br/>- ttml;sami;webvtt<br/><br/><br/>GenerateAIB :<br/>-Un indicateur booléen indiquant si un fichier AIB est requis (pour une utilisation avec SQL Server et hello Indexer IFilter client). Pour plus d’informations, consultez Utilisation de fichiers AIB avec Azure Media Indexer et SQL Server.<br/>- true, false<br/><br/>GenerateKeywords :<br/>- Indicateur booléen spécifiant si un fichier XML de mot-clé est requis ou non.<br/>- true, false|

## <a name="azure-media-indexer-configuration-xml-example"></a>Exemple de fichier de configuration XML d’Azure Media Indexer

``` 
<?xml version="1.0" encoding="utf-8"?>  
<configuration version="2.0">  
  <input>  
    <metadata key="title" value="[Title of hello media file]" />  
    <metadata key="description" value="[Description of hello media file]" />  
  </input>  
  <settings>  
  </settings>  
  
  <features>  
    <feature name="ASR">    
      <settings>  
        <add key="Language" value="English"/>  
        <add key="CaptionFormats" value="ttml;sami;webvtt"/>  
        <add key="GenerateAIB" value ="true" />  
        <add key="GenerateKeywords" value ="true" />  
      </settings>  
    </feature>  
  </features>  
  
</configuration>  
```
  
## <a name="next-steps"></a>Étapes suivantes

Consultez [Indexation de fichiers multimédias avec Azure Media Indexer](media-services-index-content.md).

