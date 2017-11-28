---
title: "problèmes de passerelle de gestion des données aaaTroubleshoot | Documents Microsoft"
description: "Fournit des conseils tootroubleshoot problèmes connexes tooData passerelle de gestion."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="aa6a7-103">Résoudre les problèmes liés à l’utilisation de la passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="aa6a7-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="aa6a7-104">Cet article fournit des informations sur la résolution des problèmes liés à l’utilisation de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="aa6a7-105">Consultez hello [passerelle de gestion des données](data-factory-data-management-gateway.md) article pour plus d’informations sur la passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="aa6a7-106">Consultez hello [déplacement des données entre locaux et cloud](data-factory-move-data-between-onprem-and-cloud.md) article pour une procédure pas à pas de déplacement des données à partir d’un tooMicrosoft de base de données locale SQL Server le stockage Blob Azure à l’aide de passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="aa6a7-107">Passerelle tooinstall ou le Registre en échec</span><span class="sxs-lookup"><span data-stu-id="aa6a7-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="aa6a7-108">1. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-108">1. Problem</span></span>
<span data-ttu-id="aa6a7-109">Vous voyez ce message d’erreur lors de l’installation et l’inscription d’une passerelle, en particulier, lors du téléchargement du fichier d’installation de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="aa6a7-110">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-110">Cause</span></span>
<span data-ttu-id="aa6a7-111">ordinateur Hello sur lequel vous essayez de passerelle de hello tooinstall a échoué toodownload hello dernier passerelle fichier d’installation à partir du centre de téléchargement de hello en raison du problème de réseau tooa.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-112">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-112">Resolution</span></span>
<span data-ttu-id="aa6a7-113">Vérifiez votre toosee de paramètres de serveur proxy pare-feu si les paramètres hello bloquent la connexion de réseau de hello de hello ordinateur toohello [centre de téléchargement](https://download.microsoft.com/)et mettre à jour les paramètres de hello en conséquence.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="aa6a7-114">Ou bien, vous pouvez télécharger le fichier d’installation hello pour la passerelle la plus récente hello de hello [centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=39717) sur d’autres ordinateurs qui peuvent accéder au centre de téléchargement hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="aa6a7-115">Vous pouvez ensuite l’ordinateur hôte et l’exécuter manuellement tooinstall et mise à jour de la passerelle hello passerelle toohello de copie hello installer fichiers.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="aa6a7-116">2. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-116">2. Problem</span></span>
<span data-ttu-id="aa6a7-117">Vous recevez cette erreur lorsque vous essayez de tooinstall une passerelle en cliquant sur **installer directement sur cet ordinateur** Bonjour portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="aa6a7-118">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-118">Cause</span></span>
<span data-ttu-id="aa6a7-119">Une passerelle est déjà installée sur l’ordinateur de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-120">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-120">Resolution</span></span>
<span data-ttu-id="aa6a7-121">Désinstaller la passerelle existante de hello sur l’ordinateur de hello et cliquez sur hello **installer directement sur cet ordinateur** lier de nouveau.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="aa6a7-122">3. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-122">3. Problem</span></span>
<span data-ttu-id="aa6a7-123">Cette erreur peut s’afficher lorsque vous inscrivez une nouvelle passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="aa6a7-124">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-124">Cause</span></span>
<span data-ttu-id="aa6a7-125">Vous pouvez voir ce message pour l’une des hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="aa6a7-126">format Hello de clé de passerelle hello n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="aa6a7-127">clé de passerelle Hello a été invalidée.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="aa6a7-128">clé de passerelle Hello a été régénérée à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="aa6a7-129">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-129">Resolution</span></span>
<span data-ttu-id="aa6a7-130">Vérifiez si vous utilisez la clé de passerelle appropriée hello à partir du portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="aa6a7-131">Si nécessaire, régénérer une clé et utiliser la passerelle de hello tooregister clé hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="aa6a7-132">4. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-132">4. Problem</span></span>
<span data-ttu-id="aa6a7-133">Vous pouvez voir hello message d’erreur suivant lorsque vous utilisez l’inscription d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Contenu ou format de clé non valide](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="aa6a7-135">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-135">Cause</span></span>
<span data-ttu-id="aa6a7-136">Hello contenu ou le format de clé de passerelle d’entrée hello est incorrect.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="aa6a7-137">Une des raisons de hello peut être que vous avez copié uniquement une partie de clé de hello à partir du portail de hello ou que vous utilisez une clé non valide.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-138">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-138">Resolution</span></span>
<span data-ttu-id="aa6a7-139">Générer une clé de passerelle dans le portail de hello et utiliser hello copie bouton toocopy hello toute clé.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="aa6a7-140">Puis collez-la dans cette passerelle de hello tooregister fenêtre.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="aa6a7-141">5. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-141">5. Problem</span></span>
<span data-ttu-id="aa6a7-142">Vous pouvez voir hello message d’erreur suivant lorsque vous utilisez l’inscription d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![La clé de passerelle n’est pas valide ou est vide.](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="aa6a7-144">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-144">Cause</span></span>
<span data-ttu-id="aa6a7-145">clé de passerelle Hello a été régénérée ou passerelle de hello a été supprimé dans hello portail Azure.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="aa6a7-146">Il peut également se produire si le programme d’installation de hello passerelle de gestion des données n’est pas la plus récente.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-147">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-147">Resolution</span></span>
<span data-ttu-id="aa6a7-148">Vérifiez si le programme d’installation de hello passerelle de gestion des données est la version la plus récente hello, vous trouverez une version la plus récente hello sur hello Microsoft [centre de téléchargement](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="aa6a7-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="aa6a7-149">Si le programme d’installation est en cours / dernière et passerelle existe toujours sur le portail, régénérer la clé de passerelle hello Bonjour portail Azure et utilisez hello copier bouton toocopy hello ensemble la clé, puis collez-la dans cette passerelle de hello tooregister fenêtre.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="aa6a7-150">Sinon, recréez la passerelle de hello et recommencer.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="aa6a7-151">6. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-151">6. Problem</span></span>
<span data-ttu-id="aa6a7-152">Vous pouvez voir hello message d’erreur suivant lorsque vous utilisez l’inscription d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![La clé de passerelle n’est pas valide ou est vide.](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="aa6a7-154">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-154">Cause</span></span>
<span data-ttu-id="aa6a7-155">Cette erreur peut se produire parce que hello passerelle a été supprimée ou hello passerelle associé a été régénérée.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-156">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-156">Resolution</span></span>
<span data-ttu-id="aa6a7-157">Si la passerelle de hello a été supprimée, recréez passerelle hello à partir du portail de hello, cliquez sur **inscrire**, copiez hello clé à partir du portail de hello, coller et essayez de passerelle de hello tooregister.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="aa6a7-158">Si la passerelle de hello existe toujours, mais sa clé a été régénérée, utilisez hello tooregister clé hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="aa6a7-159">Si vous n’avez pas la clé de hello, régénérer la clé hello de portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="aa6a7-160">7. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-160">7. Problem</span></span>
<span data-ttu-id="aa6a7-161">Lorsque vous vous inscrivez une passerelle, vous devrez peut-être le chemin d’accès tooenter et le mot de passe pour un certificat.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Indiquer un certificat](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="aa6a7-163">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-163">Cause</span></span>
<span data-ttu-id="aa6a7-164">passerelle de Hello a été inscrit sur avant les autres ordinateurs.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="aa6a7-165">Au cours de hello l’inscription initiale d’une passerelle, un certificat de chiffrement a été associé à une passerelle de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="aa6a7-166">certificat de Hello peut être généré automatiquement par la passerelle de hello ou fournie par l’utilisateur de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="aa6a7-167">Ce certificat est utilisé tooencrypt les informations d’identification hello du magasin de données (service lié).</span><span class="sxs-lookup"><span data-stu-id="aa6a7-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Exportation du certificat](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="aa6a7-169">Lorsque la restauration passerelle hello sur un ordinateur hôte différent, l’Assistant Inscription hello demande pour ce toodecrypt certificat des informations d’identification précédemment chiffrées avec ce certificat.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="aa6a7-170">Sans ce certificat, informations d’identification hello ne peut pas être déchiffrées par passerelle hello et exécutions d’activité de copie suivantes associées à cette nouvelle passerelle échouent.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="aa6a7-171">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-171">Resolution</span></span>
<span data-ttu-id="aa6a7-172">Si vous avez exporté le certificat des informations d’identification hello à partir de l’ordinateur de passerelle hello d’origine à l’aide de hello **exporter** bouton sur hello **paramètres** onglet du Gestionnaire de Configuration passerelle de gestion de données, utilisez hello certificat ici.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="aa6a7-173">Vous ne pouvez pas ignorer cette étape lors de la récupération d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="aa6a7-174">Si le certificat de hello est manquant, vous devez de passerelle de hello toodelete à partir du portail de hello et recréez une nouvelle passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="aa6a7-175">En outre, mettre à jour de tous les services liés qui sont associées toohello passerelle en tapant de nouveau leurs informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="aa6a7-176">8. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-176">8. Problem</span></span>
<span data-ttu-id="aa6a7-177">Vous pouvez voir hello message d’erreur suivant.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="aa6a7-178">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-178">Cause</span></span>
<span data-ttu-id="aa6a7-179">Cette erreur se produit lorsque votre passerelle est dans un environnement qui nécessite une tooaccess de proxy HTTP ressources Internet, ou le mot de passe de votre proxy d’authentification est modifié, mais il n’est pas actualisé en conséquence dans votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-180">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-180">Resolution</span></span>
<span data-ttu-id="aa6a7-181">Suivez les instructions de hello Bonjour [considérations sur les serveurs Proxy](#proxy-server-considerations) section de cet article et configurer les paramètres de proxy du Gestionnaire de Configuration passerelle de gestion avec des données.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="aa6a7-182">La passerelle est en ligne avec des fonctionnalités limitées</span><span class="sxs-lookup"><span data-stu-id="aa6a7-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="aa6a7-183">1. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-183">1. Problem</span></span>
<span data-ttu-id="aa6a7-184">Vous consultez État hello de passerelle de hello en ligne avec des fonctionnalités limitées.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="aa6a7-185">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-185">Cause</span></span>
<span data-ttu-id="aa6a7-186">Vous consultez État hello de passerelle de hello en ligne avec des fonctionnalités limitées pour l’une des hello suivant raisons :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="aa6a7-187">Impossible de connecter passerelle toocloud service via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="aa6a7-188">Service cloud ne peut pas se connecter à toogateway via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="aa6a7-189">Hello passerelle est en ligne avec des fonctionnalités limitées, vous peut-être pas en mesure de toouse hello Assistant Copier les données fabrique toocreate des pipelines de données pour la copie des données tooor à partir de banques de données locales.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="aa6a7-190">Comme solution de contournement, vous pouvez utiliser l’éditeur Data Factory dans le portail hello, Visual Studio ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-191">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-191">Resolution</span></span>
<span data-ttu-id="aa6a7-192">Résolution de ce problème (en ligne avec des fonctionnalités limitées) est basée sur la passerelle de hello ne peut pas se connecter le service de cloud computing toohello ou hello autre façon.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="aa6a7-193">Hello les sections suivantes fournit ces résolutions.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="aa6a7-194">2. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-194">2. Problem</span></span>
<span data-ttu-id="aa6a7-195">Hello, l’erreur suivante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Impossible de connecter passerelle toocloud service](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="aa6a7-197">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-197">Cause</span></span>
<span data-ttu-id="aa6a7-198">Passerelle ne peut pas se connecter le service cloud toohello via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-199">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-199">Resolution</span></span>
<span data-ttu-id="aa6a7-200">Suivez ces étapes tooget hello passerelle qui en ligne :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="aa6a7-201">Autoriser l’adresse IP des règles de trafic sortant sur l’ordinateur de passerelle hello et les pare-feu d’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="aa6a7-202">Vous pouvez trouver les adresses IP à partir de hello journal des événements Windows (ID == 401) : une tentative a été effectuée tooaccess un socket de manière interdite par ses autorisations d’accès XX. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="aa6a7-203">Configurer les paramètres de proxy sur la passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="aa6a7-204">Consultez hello [considérations sur les serveurs Proxy](#proxy-server-considerations) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="aa6a7-205">Activer les ports sortants 5671 et 9350-9354 sur les deux hello le pare-feu Windows sur l’ordinateur de passerelle hello et les pare-feu d’entreprise hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="aa6a7-206">Consultez hello [pare-feu et Ports](#ports-and-firewall) pour plus d’informations.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="aa6a7-207">Cette étape est facultative, mais elle est recommandée pour des questions de performances.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="aa6a7-208">3. Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-208">3. Problem</span></span>
<span data-ttu-id="aa6a7-209">Hello, l’erreur suivante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="aa6a7-210">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-210">Cause</span></span>
<span data-ttu-id="aa6a7-211">erreur temporaire de connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-212">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-212">Resolution</span></span>
<span data-ttu-id="aa6a7-213">Suivez ces étapes tooget hello passerelle qui en ligne :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="aa6a7-214">Attendez quelques minutes, la connectivité de hello est récupérée automatiquement lors de l’erreur de hello a disparu.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="aa6a7-215">Si hello erreur persiste, redémarrez le service de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="aa6a7-216">Service de tooauthor Échec lié</span><span class="sxs-lookup"><span data-stu-id="aa6a7-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="aa6a7-217">Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-217">Problem</span></span>
<span data-ttu-id="aa6a7-218">Vous pouvez voir cette erreur lorsque vous essayez de toouse le Gestionnaire d’informations d’identification dans informations d’identification du portail tooinput hello pour un service lié, ou mettre à jour les informations d’identification pour un service lié existant.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="aa6a7-219">Lorsque vous voyez cette erreur, page de paramètres hello du Gestionnaire de Configuration passerelle de gestion des données peut se présenter comme hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Impossible de contacter la base de données](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="aa6a7-221">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-221">Cause</span></span>
<span data-ttu-id="aa6a7-222">certificat SSL de Hello peut avoir été perdu sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="aa6a7-223">ordinateur de passerelle Hello ne peut pas charger hello certificat actuellement utilisé pour le chiffrement SSL.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="aa6a7-224">Vous pouvez également voir un message d’erreur dans le journal des événements hello qui est similaire toohello message suivant.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="aa6a7-225">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-225">Resolution</span></span>
<span data-ttu-id="aa6a7-226">Suivez ces problèmes de hello toosolve comme suit :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="aa6a7-227">Lancez le Gestionnaire de configuration de passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="aa6a7-228">Commutateur toohello **paramètres** onglet.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="aa6a7-229">Cliquez sur hello **modification** certificat SSL de bouton toochange hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![Bouton de modification du certificat](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="aa6a7-231">Sélectionnez un nouveau certificat en tant que certificat SSL de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="aa6a7-232">Vous pouvez utiliser n’importe quel certificat SSL généré par vos soins ou par une organisation quelconque.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Indiquer un certificat](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="aa6a7-234">Échec de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="aa6a7-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="aa6a7-235">Problème</span><span class="sxs-lookup"><span data-stu-id="aa6a7-235">Problem</span></span>
<span data-ttu-id="aa6a7-236">Vous pouvez remarquer hello après une panne de « UserErrorFailedToConnectToSqlserver » après avoir configuré un pipeline dans le portail de hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="aa6a7-237">Cause :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-237">Cause</span></span>
<span data-ttu-id="aa6a7-238">Cela peut se produire pour différentes raisons et la procédure de résolution varie en conséquence.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="aa6a7-239">Résolution :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-239">Resolution</span></span>
<span data-ttu-id="aa6a7-240">Autoriser les connexions TCP sortantes sur le port TCP/1433 sur hello côté client de passerelle de gestion des données avant la connexion de base de données SQL tooan.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="aa6a7-241">Si la base de données cible hello est une base de données SQL Azure, vérifiez SQL Server paramètres du pare-feu pour Azure également.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="aa6a7-242">Consultez hello suivant du magasin de données local toohello de connexion de section tootest hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="aa6a7-243">Erreurs liées à la connexion à la banque de données ou au pilote</span><span class="sxs-lookup"><span data-stu-id="aa6a7-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="aa6a7-244">Si vous voyez les données à stocker de connexion ou des erreurs liées au pilote, effectuez hello comme suit :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="aa6a7-245">Démarrez le Gestionnaire de Configuration de passerelle de gestion de données sur l’ordinateur de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="aa6a7-246">Commutateur toohello **Diagnostics** onglet.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="aa6a7-247">Dans **tester la connexion**, ajouter des valeurs de groupe de passerelle hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="aa6a7-248">Cliquez sur **Test** toosee si vous pouvez vous connecter toohello local source de données à partir de l’ordinateur de passerelle hello à l’aide des informations d’identification et les informations de connexion hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="aa6a7-249">En cas de tester la connexion hello toujours après l’installation d’un pilote, redémarrage hello passerelle pour qu’il toopick des modifications les plus récentes hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Tester la connexion dans l’onglet Diagnostics](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="aa6a7-251">Journaux de la passerelle</span><span class="sxs-lookup"><span data-stu-id="aa6a7-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="aa6a7-252">Envoyer tooMicrosoft des journaux de passerelle</span><span class="sxs-lookup"><span data-stu-id="aa6a7-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="aa6a7-253">Lorsque vous contactez le Support technique de Microsoft tooget aide Résolution des problèmes de passerelle, vous pouvez être invité tooshare vos journaux de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="aa6a7-254">Avec la version de hello de passerelle de hello, vous pouvez partager des journaux de la passerelle requises avec deux clics de bouton du Gestionnaire de Configuration passerelle de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="aa6a7-255">Commutateur toohello **Diagnostics** onglet du Gestionnaire de Configuration passerelle de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Onglet Diagnostics de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="aa6a7-257">Cliquez sur **d’envoi de journaux** hello toosee suivant la boîte de dialogue.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Lien Envoyer des journaux de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="aa6a7-259">(Facultatif) Cliquez sur **afficher les journaux** tooreview journaux dans l’Observateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="aa6a7-260">(Facultatif) Cliquez sur **confidentialité** déclaration de confidentialité des services web de Microsoft tooreview.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="aa6a7-261">Lorsque vous êtes satisfait que vous êtes sur le tooupload, cliquez sur **d’envoi de journaux** tooactually envoyer les journaux de hello de hello dernière tooMicrosoft de sept jours pour la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="aa6a7-262">Vous devez voir État hello d’opération d’envoi-journaux hello comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![État de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="aa6a7-264">Après que l’opération de hello est terminée, vous voyez une boîte de dialogue comme illustré hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![État de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="aa6a7-266">Enregistrer hello **ID état** et le partager avec le Support technique de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="aa6a7-267">ID du rapport Hello est toolocate utilisé les journaux de passerelle hello que vous avez téléchargé pour le dépannage.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="aa6a7-268">ID du rapport Hello est également enregistrée dans l’Observateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="aa6a7-269">Vous pouvez le trouver en examinant les ID d’événement hello « 25 » et vérifiez hello date et heure.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![ID du rapport de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="aa6a7-271">La passerelle d’archive ouvre une session sur l’ordinateur hôte de la passerelle</span><span class="sxs-lookup"><span data-stu-id="aa6a7-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="aa6a7-272">Dans certains cas, il se peut que vous ayez des problèmes avec la passerelle et que vous ne puissiez pas partager directement les journaux de la passerelle :</span><span class="sxs-lookup"><span data-stu-id="aa6a7-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="aa6a7-273">Manuellement, vous installez hello passerelle et inscrivez hello passerelle.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="aa6a7-274">Vous essayez de passerelle de hello tooregister avec une clé régénérée du Gestionnaire de Configuration passerelle de gestion de données.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="aa6a7-275">Vous essayez de toosend journaux et le service hôte de passerelle hello ne peut pas être connecté.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="aa6a7-276">Dans ces cas de figure, vous pouvez enregistrer les journaux de la passerelle dans un fichier zip et fournir celui-ci au Support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="aa6a7-277">Par exemple, si vous recevez une erreur pendant que vous inscrivez la passerelle hello comme indiqué dans hello suivant capture d’écran.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Erreur d’inscription de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="aa6a7-279">Cliquez sur hello **archiver les journaux de la passerelle** link tooarchive et enregistrer les journaux, puis partager le fichier zip de hello avec prise en charge de Microsoft.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Lien Archiver les journaux de la passerelle de gestion de données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="aa6a7-281">Rechercher dans les journaux de la passerelle</span><span class="sxs-lookup"><span data-stu-id="aa6a7-281">Locate gateway logs</span></span>
<span data-ttu-id="aa6a7-282">Vous trouverez des informations détaillées de passerelle du journal dans les journaux des événements Windows hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="aa6a7-283">Démarrez l’**Observateur d’événements** Windows.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="aa6a7-284">Recherchez les journaux Bonjour **journaux des applications et Services** > **passerelle de gestion des données** dossier.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="aa6a7-285">Lorsque vous êtes à résoudre les problèmes liés à la passerelle, recherchez les événements de niveau erreur dans l’Observateur d’événements hello.</span><span class="sxs-lookup"><span data-stu-id="aa6a7-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Journaux de la passerelle de gestion des données dans l’Observateur d’événements](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
