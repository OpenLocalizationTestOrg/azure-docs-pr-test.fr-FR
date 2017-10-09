---
title: "élément de l’interface utilisateur de FileUpload pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Common.FileUpload pour des Applications managées Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 7af5bec992e3f120afb1bdf56d8b4c19a8e5e834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Élément d’interface utilisateur Microsoft.Common.FileUpload
Un contrôle qui permet une toospecify d’utilisateur, un ou plusieurs fichiers tooupload. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Common.FileUpload](./media/managed-application-elements/microsoft.common.fileupload.png)

## <a name="schema"></a>Schéma
```json
{
  "name": "element1",
  "type": "Microsoft.Common.FileUpload",
  "label": "Some file upload",
  "toolTip": "",
  "constraints": {
    "required": true,
    "accept": ".doc,.docx,.xml,application/msword"
  },
  "options": {
    "multiple": false,
    "uploadMode": "file",
    "openMode": "text",
    "encoding": "UTF-8"
  },
  "visible": true
}
```

## <a name="remarks"></a>Remarques
- `constraints.accept`Spécifie les types de hello de fichiers qui figurent dans la boîte de dialogue de fichier du navigateur hello. Consultez hello [spécification HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) pour les valeurs autorisées. la valeur par défaut Hello est **null**.
- Si `options.multiple` est défini trop**true**, utilisateur de hello est autorisé tooselect, et plusieurs fichiers dans la boîte de dialogue de fichier du navigateur hello. la valeur par défaut Hello est **false**.
- Cet élément prend en charge le téléchargement de fichiers dans les deux modes, selon la valeur hello `options.uploadMode`. Si **fichier** est spécifié, la sortie de hello contient contenu hello du fichier hello comme un objet blob. Si **url** est spécifié, le fichier de hello est alors téléchargé tooa un emplacement temporaire et sortie de hello contient hello des URL de blob de hello. Les objets blob temporaires sont purgés après 24 heures. la valeur par défaut Hello est **fichier**.
- Hello valeur `options.openMode` détermine la façon dont les fichiers hello sont en lecture. Si le fichier de hello est toobe attendu du texte brut, spécifiez **texte**; sinon, spécifiez **binaire**. la valeur par défaut Hello est **texte**.
- Si `options.uploadMode` est défini trop**fichier** et `options.openMode` est défini trop**binaire**, sortie de hello est codée en base64.
- `options.encoding`Spécifie les toouse codage hello lors de la lecture du fichier de hello. la valeur par défaut Hello est **UTF-8**et est utilisée uniquement lorsque `options.openMode` est défini trop**texte**.

## <a name="sample-output"></a>Exemple de sortie
Si options.multiple a la valeur false et options.uploadMode est le fichier, la sortie contient contenu hello du fichier de hello sous forme de chaîne JSON :

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Si options.multiple a la valeur true and'options.uploadMode est le fichier, puis la sortie contient du contenu hello des fichiers de hello en un tableau JSON :

```json
[
  "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
  "Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat.",
  "Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.",
  "Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum."
]
```

Si options.multiple a la valeur false et options.uploadMode la valeur url, la sortie contient une URL sous forme de chaîne JSON :

```json
"https://myaccount.blob.core.windows.net/pictures/profile.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
```

Si options.multiple a la valeur true et options.uploadMode la valeur url, la sortie contient une liste d’URL sous forme de tableau JSON :
```json
[
  "https://myaccount.blob.core.windows.net/pictures/profile1.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile2.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d",
  "https://myaccount.blob.core.windows.net/pictures/profile3.jpg?sv=2013-08-15&st=2013-08-16&se=2013-08-17&sr=c&sp=r&rscd=file;%20attachment&rsct=binary &sig=YWJjZGVmZw%3d%3d&sig=a39%2BYozJhGp6miujGymjRpN8tsrQfLo9Z3i8IRyIpnQ%3d"
]
```

Lorsque vous testez une CreateUiDefinition, certains navigateurs (comme Google Chrome) tronquent les URL générées par l’élément de Microsoft.Common.FileUpload hello dans la console du navigateur hello. Vous devrez peut-être tooright-cliquez sur les liens toocopy hello URL complètes.


## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
