---
title: "aaaAzure AD v2 JS SPA guidée par le programme d’installation - configuration (ARP) | Documents Microsoft"
description: "Comment les applications JavaScript SPA peuvent appeler une API qui nécessite des jetons d’accès à partir d’un point de terminaison Azure Active Directory v2 (ARP)"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 157f4e342cd684294e24da6ee1fad8a7c2fc266a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a><span data-ttu-id="8a58f-103">Ajouter des informations tooyour application de l’application hello d’inscription</span><span class="sxs-lookup"><span data-stu-id="8a58f-103">Add hello application’s registration information tooyour App</span></span>

<span data-ttu-id="8a58f-104">Dans cette étape, vous devez les URL de redirection hello tooconfigure de vos informations d’inscription de l’application et ajoutez application de JavaScript SPA tooyour hello Id d’Application.</span><span class="sxs-lookup"><span data-stu-id="8a58f-104">In this step, you need tooconfigure hello Redirect URL of your application registration information and then add hello Application Id tooyour JavaScript SPA application.</span></span>

### <a name="configure-redirect-url"></a><span data-ttu-id="8a58f-105">Configurer l’URL de redirection</span><span class="sxs-lookup"><span data-stu-id="8a58f-105">Configure redirect URL</span></span>

<span data-ttu-id="8a58f-106">Configurer hello `Redirect URL` champ ci-dessus avec l’URL de hello pour votre page index.html basée sur votre serveur web, puis cliquez sur *mise à jour*.</span><span class="sxs-lookup"><span data-stu-id="8a58f-106">Configure hello `Redirect URL` field above with hello URL for your index.html page based on your web server, then click *Update*.</span></span>


> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a><span data-ttu-id="8a58f-107">Instructions Visual Studio pour obtenir l’URL de redirection</span><span class="sxs-lookup"><span data-stu-id="8a58f-107">Visual Studio instructions for obtaining redirect URL</span></span>
> <span data-ttu-id="8a58f-108">tooobtain votre URL de redirection, suivez les instructions hello ci-dessous :</span><span class="sxs-lookup"><span data-stu-id="8a58f-108">tooobtain your redirect URL, follow hello instructions below:</span></span>
> 1.    <span data-ttu-id="8a58f-109">Dans *l’Explorateur de solutions*, sélectionnez le projet de hello et examinez hello `Properties` fenêtre (si vous ne voyez pas une fenêtre de propriétés, appuyez sur `F4`)</span><span class="sxs-lookup"><span data-stu-id="8a58f-109">In *Solution Explorer*, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press `F4`)</span></span>
> 2.    <span data-ttu-id="8a58f-110">Copier la valeur hello à partir de `URL` toohello Presse-papiers :</span><span class="sxs-lookup"><span data-stu-id="8a58f-110">Copy hello value from `URL` toohello clipboard:</span></span><br/> <span data-ttu-id="8a58f-111">![Propriétés du projet](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span><span class="sxs-lookup"><span data-stu-id="8a58f-111">![Project properties](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)</span></span><br />
> 3.    <span data-ttu-id="8a58f-112">Collez la valeur hello comme un `Redirect URL` sur hello en haut de cette page, puis cliquez sur`Update`</span><span class="sxs-lookup"><span data-stu-id="8a58f-112">Paste hello value as a `Redirect URL` on hello top of this page, then click `Update`</span></span>

<p/>

> #### <a name="setting-redirect-url-for-python"></a><span data-ttu-id="8a58f-113">Configuration d’une URL de redirection pour Python</span><span class="sxs-lookup"><span data-stu-id="8a58f-113">Setting Redirect URL for Python</span></span>
> <span data-ttu-id="8a58f-114">Pour Python, vous pouvez définir le port du serveur web hello via la ligne de commande.</span><span class="sxs-lookup"><span data-stu-id="8a58f-114">For Python, you can set hello web server port via command line.</span></span> <span data-ttu-id="8a58f-115">Cet Assistant d’installation utilise le port 8080 hello pour référence, mais vous êtes libre toouse tout port disponible.</span><span class="sxs-lookup"><span data-stu-id="8a58f-115">This guided setup uses hello port 8080 for reference but feel free toouse any other port available.</span></span> <span data-ttu-id="8a58f-116">Dans tous les cas, suivez les instructions de hello sous tooset une URL de redirection dans les informations d’inscription de l’application hello :</span><span class="sxs-lookup"><span data-stu-id="8a58f-116">In any case, follow hello instructions below tooset up a redirect URL in hello application registration information:</span></span><br/>
> <span data-ttu-id="8a58f-117">Définir `http://localhost:8080/` comme un `Redirect URL` hello haut de cette page, ou utilisez `http://localhost:[port]/` si vous utilisez un port TCP personnalisé (où *[port]* est le numéro de port TCP personnalisée hello), puis cliquez sur 'Update'</span><span class="sxs-lookup"><span data-stu-id="8a58f-117">Set `http://localhost:8080/` as a `Redirect URL` on hello top of this page, or use `http://localhost:[port]/` if you are using a custom TCP port (where *[port]* is hello custom TCP port number), and then click 'Update'</span></span>

### <a name="configure-your-javascript-spa-application"></a><span data-ttu-id="8a58f-118">Configurer votre application SPA JavaScript</span><span class="sxs-lookup"><span data-stu-id="8a58f-118">Configure your JavaScript SPA application</span></span>

1.  <span data-ttu-id="8a58f-119">Créez un fichier nommé `msalconfig.js` contenant les informations d’inscription de l’application hello.</span><span class="sxs-lookup"><span data-stu-id="8a58f-119">Create a file named `msalconfig.js` containing hello application registration information.</span></span> <span data-ttu-id="8a58f-120">Si vous utilisez un projet Visual Studio, sélectionnez hello (dossier racine du projet), avec le bouton droit et sélectionnez : `Add`  >  `New Item`  >  `JavaScript File`.</span><span class="sxs-lookup"><span data-stu-id="8a58f-120">If you are using Visual Studio, select hello project (project root folder), right-click and select: `Add` > `New Item` > `JavaScript File`.</span></span> <span data-ttu-id="8a58f-121">Nommez-le `msalconfig.js`.</span><span class="sxs-lookup"><span data-stu-id="8a58f-121">Name it `msalconfig.js`</span></span>
2.  <span data-ttu-id="8a58f-122">Ajouter hello suivant code tooyour `msalconfig.js` fichier :</span><span class="sxs-lookup"><span data-stu-id="8a58f-122">Add hello following code tooyour `msalconfig.js` file:</span></span>

```javascript
var msalconfig = {
    clientID: "[Enter hello application Id here]",
    redirectUri: location.origin
};
``` 
