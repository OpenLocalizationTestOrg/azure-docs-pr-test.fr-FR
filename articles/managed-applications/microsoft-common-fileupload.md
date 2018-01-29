---
title: "Élément d’interface utilisateur FileUpload des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Common.FileUpload pour les applications gérées Azure"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/12/2017
ms.author: tomfitz
ms.openlocfilehash: 095880322ba801895a22efcf3476fa37d9e2ac3c
ms.sourcegitcommit: 3ab5ea589751d068d3e52db828742ce8ebed4761
ms.translationtype: HT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/27/2017
---
# <a name="microsoftcommonfileupload-ui-element"></a>Élément d’interface utilisateur Microsoft.Common.FileUpload
Contrôle qui permet à un utilisateur de spécifier un ou plusieurs fichiers à charger. Vous utilisez cet élément lors de la [création d’une application gérée Azure](publish-service-catalog-app.md).

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
- `constraints.accept` spécifie les types de fichiers qui figurent dans la boîte de dialogue du navigateur. Consultez la [spécification HTML5](http://www.w3.org/TR/html5/forms.html#attr-input-accept) pour connaître les valeurs autorisées. La valeur par défaut est **null**.
- Si `options.multiple` est défini sur **true**, l’utilisateur est autorisé à sélectionner plusieurs fichiers dans la boîte de dialogue du fichier du navigateur. La valeur par défaut est **false**.
- Cet élément prend en charge le chargement de fichiers dans deux modes basés sur la valeur de `options.uploadMode`. Si **file** est spécifié, la sortie contient le contenu du fichier sous la forme d’un objet blob. Si **url** est spécifié, le fichier est chargé sur un emplacement temporaire et la sortie contient l’URL de l’objet blob. Les objets blob temporaires sont purgés après 24 heures. La valeur par défaut est **file**.
- La valeur de `options.openMode` détermine la façon dont le fichier est lu. Si le fichier doit être du texte brut, spécifiez **text** ; sinon, spécifiez **binary**. La valeur par défaut est **text**.
- Si `options.uploadMode` est défini sur **file** et `options.openMode` sur **binary**, la sortie est codée en base64.
- `options.encoding` spécifie l’encodage à utiliser lors de la lecture du fichier. La valeur par défaut est **UTF-8**et est utilisée uniquement lorsque `options.openMode` est défini sur **text**.

## <a name="sample-output"></a>Exemple de sortie
Si options.multiple a la valeur false et options.uploadMode la valeur file, la sortie contient le contenu du fichier sous forme de chaîne JSON :

```json
"Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua."
```

Si options.multiple a la valeur true et options.uploadMode la valeur file, la sortie contient le contenu des fichiers sous forme de tableau JSON :

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

Lorsque vous testez un élément CreateUiDefinition, certains navigateurs (comme Google Chrome) tronquent les URL générées par l’élément Microsoft.Common.FileUpload dans la console du navigateur. Vous devrez peut-être cliquer avec le bouton droit sur des liens pour copier les URL complètes.


## <a name="next-steps"></a>Étapes suivantes
* Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](overview.md).
* Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](create-uidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](create-uidefinition-elements.md).
