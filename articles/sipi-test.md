---
title: Fichier de test Sipi | Documents Microsoft
description: "Tester les dépendances de fichier toocheck ReadyForTest"
services: active-directory-b2c
documentationcenter: 
author: Sipi
manager: Sipi
editor: Sipi
ms.assetid: 20e92275-b25d-45dd-9090-181a60c99f68
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 6/13/2017
ms.author: Sipi
ms.openlocfilehash: afd3dc94dfb30926b316256fb06a768a391004f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="a494c-103">Fichier de test Sipi</span><span class="sxs-lookup"><span data-stu-id="a494c-103">Sipi test file</span></span>

<span data-ttu-id="a494c-104">Ce démarrage rapide vous aide à inscrire une application dans un client B2C Microsoft Azure Active Directory (Azure AD) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="a494c-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="a494c-105">Lorsque vous avez terminé, votre application est enregistrée pour une utilisation dans le locataire de hello Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="a494c-105">When you're finished, your application is registered for use in hello Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a494c-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="a494c-106">Prerequisites</span></span>

<span data-ttu-id="a494c-107">toobuild une application qui accepte le consommateur d’inscription et de connexion, vous devez tout d’abord d’application de hello tooregister avec un locataire Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a494c-107">toobuild an application that accepts consumer sign-up and sign-in, you first need tooregister hello application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="a494c-108">Obtenir votre propre locataire à l’aide de hello étapes [créer un client Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a494c-108">Get your own tenant by using hello steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="a494c-109">Les applications créées à partir du panneau hello Azure AD B2C Bonjour portail Azure doivent être gérées à partir de hello même emplacement.</span><span class="sxs-lookup"><span data-stu-id="a494c-109">Applications created from hello Azure AD B2C blade in hello Azure portal must be managed from hello same location.</span></span> <span data-ttu-id="a494c-110">Si vous modifiez les applications B2C hello à l’aide de PowerShell ou un autre portail, ils deviennent non pris en charge et ne fonctionnent pas avec Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="a494c-110">If you edit hello B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="a494c-111">Consultez les détails dans hello [a généré une erreur d’applications](#faulted-apps) section.</span><span class="sxs-lookup"><span data-stu-id="a494c-111">See details in hello [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-toob2c-settings"></a><span data-ttu-id="a494c-112">Accédez tooB2C paramètres</span><span class="sxs-lookup"><span data-stu-id="a494c-112">Navigate tooB2C settings</span></span>

<span data-ttu-id="a494c-113">Connectez-vous à toohello [portail Azure](https://portal.azure.com/) comme hello administrateur Global du client de hello B2C.</span><span class="sxs-lookup"><span data-stu-id="a494c-113">Log in toohello [Azure portal](https://portal.azure.com/) as hello Global Administrator of hello B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="a494c-114">Choisissez les étapes suivantes, selon le type d’application hello que l’inscription :</span><span class="sxs-lookup"><span data-stu-id="a494c-114">Choose next steps based on hello application type you are registering:</span></span>
