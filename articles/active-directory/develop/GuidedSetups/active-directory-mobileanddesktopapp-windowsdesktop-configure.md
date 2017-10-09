---
title: aaaAzure AD v2 Windows Desktop mise en route - Config | Documents Microsoft
description: "Cet article explique comment une application de bureau Windows .NET (XAML) peut obtenir un jeton d’accès et appeler une API protégée par un point de terminaison Azure Active Directory v2. | Microsoft Azure | Microsoft Azure"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Créer une application (Express)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:
1. Inscrire votre application via hello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Entrez un nom pour votre application, ainsi que votre adresse e-mail.
3.  Assurez-vous que l’option hello pour le programme d’installation interactive est activée
4.  Suivez l’ID de l’application hello instructions tooobtain hello et collez-le dans votre code

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Ajoutez votre solution de tooyour d’application d’enregistrement d’informations (Avancé)
Maintenant vous devez tooregister votre application Bonjour *portail de l’enregistrement d’Application Microsoft*:
1. Accédez toohello [portail de l’enregistrement d’Application Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister une application
2. Entrez un nom pour votre application, ainsi que votre adresse e-mail. 
3. Assurez-vous que l’option hello pour le programme d’installation interactive est désactivée
4. Cliquez sur `Add Platform`, puis sélectionnez `Native Application` et appuyez sur Save (Enregistrer).
5. Copiez hello GUID dans l’ID de l’Application, revenez en arrière tooVisual Studio, ouvrez `App.xaml.cs` et remplacez `your_client_id_here` par hello ID d’Application vous venez d’enregistrer :

```csharp
private static string ClientId = "your_application_id_here";
```
