---
title: "élément de l’interface utilisateur de CredentialsCombo pour les applications gérées aaaAzure | Documents Microsoft"
description: "Décrit les hello élément d’interface utilisateur de Microsoft.Compute.CredentialsCombo pour des Applications managées Azure"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a>Élément d’interface utilisateur Microsoft.Compute.CredentialsCombo
Un groupe de contrôles avec validation intégrée pour les clés publiques SSH et les mots de passe Windows et Linux. Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).

## <a name="ui-sample"></a>Exemple d’interface utilisateur
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a>Schéma
Si `osPlatform` est **Windows**, hello schéma suivant est utilisé :
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

Si `osPlatform` est **Linux**, hello schéma suivant est utilisé :
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a>Remarques
- `osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.
- Si `constraints.required` est défini trop**true**, puis hello mot de passe ou les zones de texte de clé publique SSH doivent contenir des valeurs toovalidate avec succès. la valeur par défaut Hello est **true**.
- Si `options.hideConfirmation` est défini trop**true**, puis la deuxième zone de texte hello pour confirmer le mot de passe de l’utilisateur hello est masqué. la valeur par défaut Hello est **false**.
- Si `options.hidePassword` est défini trop**true**, puis hello option toouse mot de passe est masqué. Elle peut être utilisée uniquement lorsque `osPlatform` est **Linux**. La valeur par défaut est **false**.
- Des contraintes supplémentaires sur hello autorisées des mots de passe peuvent être implémentées à l’aide de hello `customPasswordRegex` propriété. Hello chaîne dans `customValidationMessage` s’affiche lorsqu’un mot de passe échoue la validation personnalisée. Hello pour les deux propriétés la valeur par défaut est **null**.

## <a name="sample-output"></a>Exemple de sortie
Si `osPlatform` est **Windows**, ou un mot de passe au lieu d’une clé publique SSH fourni par l’utilisateur de hello, puis hello est censée donner résultat suivant :

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

Si une clé publique SSH fourni par l’utilisateur de hello, puis hello sortie suivante est attendue :
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a>Étapes suivantes
* Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).
* Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).
* Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).
