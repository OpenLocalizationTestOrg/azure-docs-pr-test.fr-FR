---
title: "Élément d’interface utilisateur CredentialsCombo des applications gérées Azure | Microsoft Docs"
description: "Décrit l’élément d’interface utilisateur Microsoft.Compute.CredentialsCombo pour les applications gérées Azure"
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
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="57927-103">Élément d’interface utilisateur Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="57927-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="57927-104">Un groupe de contrôles avec validation intégrée pour les clés publiques SSH et les mots de passe Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="57927-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="57927-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="57927-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="57927-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="57927-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="57927-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="57927-108">Schema</span></span>
<span data-ttu-id="57927-109">Si `osPlatform` est **Windows**, le schéma suivant est utilisé :</span><span class="sxs-lookup"><span data-stu-id="57927-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
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
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="57927-110">Si `osPlatform` est **Linux**, le schéma suivant est utilisé :</span><span class="sxs-lookup"><span data-stu-id="57927-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
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
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="57927-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="57927-111">Remarks</span></span>
- <span data-ttu-id="57927-112">`osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.</span><span class="sxs-lookup"><span data-stu-id="57927-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="57927-113">Si `constraints.required` a **true**, puis le mot de passe ou les zones de texte de la clé publique SSH doivent contenir des valeurs à valider correctement.</span><span class="sxs-lookup"><span data-stu-id="57927-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="57927-114">La valeur par défaut est **true**.</span><span class="sxs-lookup"><span data-stu-id="57927-114">The default value is **true**.</span></span>
- <span data-ttu-id="57927-115">Si `options.hideConfirmation` est défini sur **true**, la deuxième zone de texte de confirmation du mot de passe utilisateur est masquée.</span><span class="sxs-lookup"><span data-stu-id="57927-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="57927-116">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="57927-116">The default value is **false**.</span></span>
- <span data-ttu-id="57927-117">Si `options.hidePassword` est défini sur **true**, l’option permettant d’utiliser l’authentification par mot de passe est masquée.</span><span class="sxs-lookup"><span data-stu-id="57927-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="57927-118">Elle peut être utilisée uniquement lorsque `osPlatform` est **Linux**.</span><span class="sxs-lookup"><span data-stu-id="57927-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="57927-119">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="57927-119">The default value is **false**.</span></span>
- <span data-ttu-id="57927-120">Il est possible d’implémenter des contraintes supplémentaires sur les mots de passe autorisés à l’aide de la propriété `customPasswordRegex`.</span><span class="sxs-lookup"><span data-stu-id="57927-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="57927-121">La chaîne de `customValidationMessage` s’affiche lorsque la validation personnalisée du mot de passe échoue.</span><span class="sxs-lookup"><span data-stu-id="57927-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="57927-122">La valeur par défaut pour les deux propriétés est **null**.</span><span class="sxs-lookup"><span data-stu-id="57927-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="57927-123">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="57927-123">Sample output</span></span>
<span data-ttu-id="57927-124">Si `osPlatform` est **Windows**, ou si l’utilisateur a fourni un mot de passe au lieu d’une clé publique SSH, la sortie suivante est attendue :</span><span class="sxs-lookup"><span data-stu-id="57927-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="57927-125">Si l’utilisateur a fourni une clé publique SSH, la sortie suivante est attendue :</span><span class="sxs-lookup"><span data-stu-id="57927-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="57927-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="57927-126">Next steps</span></span>
* <span data-ttu-id="57927-127">Pour voir une présentation des applications gérées, consultez [Vue d’ensemble des applications gérées Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57927-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="57927-128">Pour voir une présentation de la création de définitions d’interface utilisateur, consultez la page [Prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57927-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="57927-129">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="57927-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
