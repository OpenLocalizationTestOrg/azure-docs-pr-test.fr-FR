---
title: Fichier de test Sipi | Documents Microsoft
description: "Fichier de test pour vérifier les dépendances ReadyForTest"
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
ms.openlocfilehash: 871d58818dcbaee5f7a5f07c19e2297ec6459a6f
ms.sourcegitcommit: b0af2a2cf44101a1b1ff41bd2ad795eaef29612a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 09/28/2017
---
# <a name="sipi-test-file"></a><span data-ttu-id="88d3c-103">Fichier de test Sipi</span><span class="sxs-lookup"><span data-stu-id="88d3c-103">Sipi test file</span></span>

<span data-ttu-id="88d3c-104">Ce démarrage rapide vous aide à inscrire une application dans un client B2C Microsoft Azure Active Directory (Azure AD) en quelques minutes.</span><span class="sxs-lookup"><span data-stu-id="88d3c-104">This Quickstart helps you register an application in a Microsoft Azure Active Directory (Azure AD) B2C tenant in a few minutes.</span></span> <span data-ttu-id="88d3c-105">Lorsque vous avez terminé, votre application est inscrite comme utilisable dans le client Azure B2C.</span><span class="sxs-lookup"><span data-stu-id="88d3c-105">When you're finished, your application is registered for use in the Azure B2C tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="88d3c-106">Composants requis</span><span class="sxs-lookup"><span data-stu-id="88d3c-106">Prerequisites</span></span>

<span data-ttu-id="88d3c-107">Pour générer une application acceptant l’inscription et la connexion des consommateurs, vous devez commencer par inscrire cette application auprès d’un client Azure Active Directory B2C.</span><span class="sxs-lookup"><span data-stu-id="88d3c-107">To build an application that accepts consumer sign-up and sign-in, you first need to register the application with an Azure Active Directory B2C tenant.</span></span> <span data-ttu-id="88d3c-108">Obtenez votre propre client en suivant la procédure décrite dans [Création d’un client Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88d3c-108">Get your own tenant by using the steps outlined in [Create an Azure AD B2C tenant](active-directory-b2c-get-started.md).</span></span>

<span data-ttu-id="88d3c-109">Les applications créées dans le panneau Azure AD B2C dans le portail Azure doivent être gérées à partir du même emplacement.</span><span class="sxs-lookup"><span data-stu-id="88d3c-109">Applications created from the Azure AD B2C blade in the Azure portal must be managed from the same location.</span></span> <span data-ttu-id="88d3c-110">Si vous modifiez des applications B2C à l’aide de PowerShell ou d’un autre portail, ces dernières ne sont plus prises en charge et ne fonctionnent pas avec Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="88d3c-110">If you edit the B2C applications using PowerShell or another portal, they become unsupported and do not work with Azure AD B2C.</span></span> <span data-ttu-id="88d3c-111">Consultez les détails dans la section [Applications ayant généré une erreur](#faulted-apps).</span><span class="sxs-lookup"><span data-stu-id="88d3c-111">See details in the [faulted apps](#faulted-apps) section.</span></span> 

## <a name="navigate-to-b2c-settings"></a><span data-ttu-id="88d3c-112">Accéder aux paramètres B2C</span><span class="sxs-lookup"><span data-stu-id="88d3c-112">Navigate to B2C settings</span></span>

<span data-ttu-id="88d3c-113">Connectez-vous au [portail Azure](https://portal.azure.com/) en tant qu’administrateur général du client B2C.</span><span class="sxs-lookup"><span data-stu-id="88d3c-113">Log in to the [Azure portal](https://portal.azure.com/) as the Global Administrator of the B2C tenant.</span></span> 

[!INCLUDE [active-directory-b2c-switch-b2c-tenant](../includes/active-directory-b2c-switch-b2c-tenant.md)]

<span data-ttu-id="88d3c-114">Choisissez les étapes suivantes en fonction du type d’application que vous inscrivez :</span><span class="sxs-lookup"><span data-stu-id="88d3c-114">Choose next steps based on the application type you are registering:</span></span>
