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
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="4ac11-103">Élément d’interface utilisateur Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="4ac11-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="4ac11-104">Un groupe de contrôles avec validation intégrée pour les clés publiques SSH et les mots de passe Windows et Linux.</span><span class="sxs-lookup"><span data-stu-id="4ac11-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="4ac11-105">Vous utilisez cet élément lors de la [création d’une application gérée Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4ac11-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4ac11-106">Exemple d’interface utilisateur</span><span class="sxs-lookup"><span data-stu-id="4ac11-106">UI sample</span></span>
![Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="4ac11-108">Schéma</span><span class="sxs-lookup"><span data-stu-id="4ac11-108">Schema</span></span>
<span data-ttu-id="4ac11-109">Si `osPlatform` est **Windows**, hello schéma suivant est utilisé :</span><span class="sxs-lookup"><span data-stu-id="4ac11-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
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

<span data-ttu-id="4ac11-110">Si `osPlatform` est **Linux**, hello schéma suivant est utilisé :</span><span class="sxs-lookup"><span data-stu-id="4ac11-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
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

## <a name="remarks"></a><span data-ttu-id="4ac11-111">Remarques</span><span class="sxs-lookup"><span data-stu-id="4ac11-111">Remarks</span></span>
- <span data-ttu-id="4ac11-112">`osPlatform` doit être spécifié. Il peut s’agir de **Windows** ou de **Linux**.</span><span class="sxs-lookup"><span data-stu-id="4ac11-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="4ac11-113">Si `constraints.required` est défini trop**true**, puis hello mot de passe ou les zones de texte de clé publique SSH doivent contenir des valeurs toovalidate avec succès.</span><span class="sxs-lookup"><span data-stu-id="4ac11-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="4ac11-114">la valeur par défaut Hello est **true**.</span><span class="sxs-lookup"><span data-stu-id="4ac11-114">hello default value is **true**.</span></span>
- <span data-ttu-id="4ac11-115">Si `options.hideConfirmation` est défini trop**true**, puis la deuxième zone de texte hello pour confirmer le mot de passe de l’utilisateur hello est masqué.</span><span class="sxs-lookup"><span data-stu-id="4ac11-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="4ac11-116">la valeur par défaut Hello est **false**.</span><span class="sxs-lookup"><span data-stu-id="4ac11-116">hello default value is **false**.</span></span>
- <span data-ttu-id="4ac11-117">Si `options.hidePassword` est défini trop**true**, puis hello option toouse mot de passe est masqué.</span><span class="sxs-lookup"><span data-stu-id="4ac11-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="4ac11-118">Elle peut être utilisée uniquement lorsque `osPlatform` est **Linux**.</span><span class="sxs-lookup"><span data-stu-id="4ac11-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="4ac11-119">La valeur par défaut est **false**.</span><span class="sxs-lookup"><span data-stu-id="4ac11-119">The default value is **false**.</span></span>
- <span data-ttu-id="4ac11-120">Des contraintes supplémentaires sur hello autorisées des mots de passe peuvent être implémentées à l’aide de hello `customPasswordRegex` propriété.</span><span class="sxs-lookup"><span data-stu-id="4ac11-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="4ac11-121">Hello chaîne dans `customValidationMessage` s’affiche lorsqu’un mot de passe échoue la validation personnalisée.</span><span class="sxs-lookup"><span data-stu-id="4ac11-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="4ac11-122">Hello pour les deux propriétés la valeur par défaut est **null**.</span><span class="sxs-lookup"><span data-stu-id="4ac11-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="4ac11-123">Exemple de sortie</span><span class="sxs-lookup"><span data-stu-id="4ac11-123">Sample output</span></span>
<span data-ttu-id="4ac11-124">Si `osPlatform` est **Windows**, ou un mot de passe au lieu d’une clé publique SSH fourni par l’utilisateur de hello, puis hello est censée donner résultat suivant :</span><span class="sxs-lookup"><span data-stu-id="4ac11-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="4ac11-125">Si une clé publique SSH fourni par l’utilisateur de hello, puis hello sortie suivante est attendue :</span><span class="sxs-lookup"><span data-stu-id="4ac11-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="4ac11-126">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4ac11-126">Next steps</span></span>
* <span data-ttu-id="4ac11-127">Pour une introduction toomanaged les applications, voir [vue d’ensemble de l’Application Azure géré](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ac11-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="4ac11-128">Pour les définitions d’interface utilisateur toocreating une présentation, consultez [prise en main de CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4ac11-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="4ac11-129">Pour obtenir une description des propriétés communes des éléments d’interface utilisateur, consultez la page [Éléments de CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="4ac11-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
