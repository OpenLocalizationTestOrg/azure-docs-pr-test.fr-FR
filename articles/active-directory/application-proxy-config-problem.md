---
title: "Problèmes lors de la création d’une application de proxy d’application | Microsoft Docs"
description: "Comment résoudre les problèmes de création d’applications de proxy d’application dans le portail d’administration Azure AD"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="0e2b8-103">Problèmes lors de la création d’une application de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="0e2b8-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="0e2b8-104">Cet article aborde certains problèmes courants auxquels sont confrontés les utilisateurs lors de la création d’une application de proxy d’application.</span><span class="sxs-lookup"><span data-stu-id="0e2b8-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="0e2b8-105">Documents recommandés</span><span class="sxs-lookup"><span data-stu-id="0e2b8-105">Recommended documents</span></span> 

<span data-ttu-id="0e2b8-106">Pour en savoir plus sur la création d’une application de proxy d’application par le biais du portail d’administration, consultez [Publier des applications avec le Proxy d’application Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="0e2b8-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="0e2b8-107">Si vous suivez les étapes décrites dans ce document et si vous obtenez une erreur lors de création de l’application, consultez les détails de l’erreur pour en savoir plus et découvrir des suggestions afin de corriger l’application.</span><span class="sxs-lookup"><span data-stu-id="0e2b8-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="0e2b8-108">La plupart des messages d’erreur incluent la suggestion d’un correctif.</span><span class="sxs-lookup"><span data-stu-id="0e2b8-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="0e2b8-109">Éléments spécifiques à vérifier</span><span class="sxs-lookup"><span data-stu-id="0e2b8-109">Specific things to check</span></span>

<span data-ttu-id="0e2b8-110">Pour éviter les erreurs courantes, vérifiez les points suivants :</span><span class="sxs-lookup"><span data-stu-id="0e2b8-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="0e2b8-111">Vous êtes un administrateur autorisé à créer une application de proxy d’application</span><span class="sxs-lookup"><span data-stu-id="0e2b8-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="0e2b8-112">L’URL interne est unique</span><span class="sxs-lookup"><span data-stu-id="0e2b8-112">The internal URL is unique</span></span>

-   <span data-ttu-id="0e2b8-113">L’URL externe est unique</span><span class="sxs-lookup"><span data-stu-id="0e2b8-113">The external URL is unique</span></span>

-   <span data-ttu-id="0e2b8-114">Les URL commencent par http ou https et se terminent par un signe « / »</span><span class="sxs-lookup"><span data-stu-id="0e2b8-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="0e2b8-115">L’URL doit être un nom de domaine et non une adresse IP</span><span class="sxs-lookup"><span data-stu-id="0e2b8-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="0e2b8-116">Le message d’erreur doit s’afficher dans le coin supérieur droit lorsque vous créez l’application.</span><span class="sxs-lookup"><span data-stu-id="0e2b8-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="0e2b8-117">Vous pouvez également sélectionner l’icône de notification pour afficher les messages d’erreur.</span><span class="sxs-lookup"><span data-stu-id="0e2b8-117">You can also select the notification icon to see the error messages.</span></span>

   ![Invite de notification](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="0e2b8-119">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="0e2b8-119">Next steps</span></span>
[<span data-ttu-id="0e2b8-120">Activer le proxy d’application dans le portail Azure</span><span class="sxs-lookup"><span data-stu-id="0e2b8-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
