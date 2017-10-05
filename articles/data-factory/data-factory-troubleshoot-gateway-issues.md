---
title: "Résoudre les problèmes de la passerelle de gestion des données | Microsoft Docs"
description: "Fournit des conseils pour résoudre les problèmes liés à la passerelle de gestion des données."
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
ms.openlocfilehash: b8e50a4e3c0b9c535ccc2344ff22261a356d5acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="0f2a2-103">Résoudre les problèmes liés à l’utilisation de la passerelle de gestion des données</span><span class="sxs-lookup"><span data-stu-id="0f2a2-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="0f2a2-104">Cet article fournit des informations sur la résolution des problèmes liés à l’utilisation de la passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="0f2a2-105">Pour obtenir des informations détaillées sur la passerelle, consultez l’article [Passerelle de gestion des données](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="0f2a2-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="0f2a2-106">Pour connaître la procédure de déplacement de données d’une base de données SQL Server locale vers un stockage Blob Microsoft Azure avec la passerelle, consultez l’article [Déplacer des données entre un site local et le cloud](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="0f2a2-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>
>
>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="0f2a2-107">Échec de l’inscription ou de l’installation de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0f2a2-107">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="0f2a2-108">1. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-108">1. Problem</span></span>
<span data-ttu-id="0f2a2-109">Ce message d’erreur s’affiche lors de l’installation et de l’enregistrement d’une passerelle, en particulier lors du téléchargement du fichier d’installation de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="0f2a2-110">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-110">Cause</span></span>
<span data-ttu-id="0f2a2-111">L’ordinateur sur lequel vous essayez d’installer la passerelle n’a pas pu télécharger le fichier d’installation de la dernière version de la passerelle à partir du Centre de téléchargement en raison d’un problème réseau.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-112">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-112">Resolution</span></span>
<span data-ttu-id="0f2a2-113">Vérifiez si les paramètres de serveur proxy de votre pare-feu bloquent la connexion réseau de l’ordinateur vers le [Centre de téléchargement](https://download.microsoft.com/) et modifiez ces paramètres si nécessaire.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="0f2a2-114">Vous pouvez également télécharger le fichier d’installation de la dernière version de la passerelle à partir du [Centre de téléchargement](https://www.microsoft.com/download/details.aspx?id=39717) sur d’autres ordinateurs qui peuvent accéder à ce dernier.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="0f2a2-115">Copiez ensuite le fichier du programme d’installation sur l’ordinateur hôte de la passerelle et exécutez-le manuellement pour installer et mettre à jour la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="0f2a2-116">2. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-116">2. Problem</span></span>
<span data-ttu-id="0f2a2-117">Cette erreur s’affiche lorsque vous tentez d’installer une passerelle en cliquant sur **Installer directement sur cet ordinateur** dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="0f2a2-118">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-118">Cause</span></span>
<span data-ttu-id="0f2a2-119">Une passerelle est déjà installée sur l’ordinateur.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-119">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-120">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-120">Resolution</span></span>
<span data-ttu-id="0f2a2-121">Désinstallez la passerelle existante sur l’ordinateur et cliquez de nouveau sur le lien **Installer directement sur cet ordinateur**.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="0f2a2-122">3. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-122">3. Problem</span></span>
<span data-ttu-id="0f2a2-123">Cette erreur peut s’afficher lorsque vous inscrivez une nouvelle passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-123">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="0f2a2-124">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-124">Cause</span></span>
<span data-ttu-id="0f2a2-125">Ce message peut s’afficher pour l’une des raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-125">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="0f2a2-126">Le format de la clé de passerelle n’est pas valide.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-126">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="0f2a2-127">La clé de passerelle a été invalidée.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-127">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="0f2a2-128">La clé de passerelle a été régénérée à partir du portail.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-128">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="0f2a2-129">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-129">Resolution</span></span>
<span data-ttu-id="0f2a2-130">Vérifiez que vous utilisez la bonne clé de passerelle du portail.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-130">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="0f2a2-131">Si besoin, régénérez une clé et utilisez cette clé pour inscrire la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-131">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="0f2a2-132">4. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-132">4. Problem</span></span>
<span data-ttu-id="0f2a2-133">Le message d’erreur suivant peut s’afficher lors de l’inscription d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-133">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![Contenu ou format de clé non valide](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="0f2a2-135">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-135">Cause</span></span>
<span data-ttu-id="0f2a2-136">Le contenu ou le format de la clé de passerelle est incorrect.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-136">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="0f2a2-137">Vous avez peut-être copié uniquement une partie de la clé dans le portail ou vous utilisez une clé non valide.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-138">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-138">Resolution</span></span>
<span data-ttu-id="0f2a2-139">Générez une clé de passerelle dans le portail et utilisez le bouton Copier pour copier la clé entière.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="0f2a2-140">Collez-la ensuite dans cette fenêtre pour inscrire la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-140">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="0f2a2-141">5. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-141">5. Problem</span></span>
<span data-ttu-id="0f2a2-142">Le message d’erreur suivant peut s’afficher lors de l’inscription d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-142">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![La clé de passerelle n’est pas valide ou est vide.](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="0f2a2-144">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-144">Cause</span></span>
<span data-ttu-id="0f2a2-145">La clé de passerelle a été régénérée ou la passerelle a été supprimée dans le portail Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="0f2a2-146">Cela peut également se produire si vous n’utilisez pas la configuration de passerelle de gestion des données la plus récente.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-146">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-147">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-147">Resolution</span></span>
<span data-ttu-id="0f2a2-148">Vérifiez que la configuration de la passerelle de gestion des données correspond à la dernière version (vous trouverez la dernière version dans le [centre de téléchargement](https://go.microsoft.com/fwlink/p/?LinkId=271260) Microsoft).</span><span class="sxs-lookup"><span data-stu-id="0f2a2-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="0f2a2-149">Si la configuration est à jour/correspond à la dernière version et que la passerelle existe encore sur le portail, régénérez la clé de la passerelle dans le portail Azure, utilisez le bouton Copier pour copier la clé et collez-la dans cette fenêtre pour inscrire la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="0f2a2-150">Sinon, recréez la passerelle et recommencez.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-150">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="0f2a2-151">6. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-151">6. Problem</span></span>
<span data-ttu-id="0f2a2-152">Le message d’erreur suivant peut s’afficher lors de l’inscription d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-152">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![La clé de passerelle n’est pas valide ou est vide.](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="0f2a2-154">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-154">Cause</span></span>
<span data-ttu-id="0f2a2-155">Cette erreur peut se produire si la passerelle a été supprimée ou la clé de passerelle associée a été régénérée.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-156">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-156">Resolution</span></span>
<span data-ttu-id="0f2a2-157">Si la passerelle a été supprimée, recréez-la à partir du portail, cliquez sur **Inscrire**, copiez la clé dans le portail, collez-la et essayez d’inscrire la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="0f2a2-158">Si la passerelle existe encore, mais que sa clé a été régénérée, utilisez la nouvelle clé pour inscrire la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="0f2a2-159">Si vous n’avez pas la clé, régénérez-la sur le portail.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-159">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="0f2a2-160">7. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-160">7. Problem</span></span>
<span data-ttu-id="0f2a2-161">Lorsque vous inscrivez une passerelle, il se peut que vous deviez entrer le chemin d’accès et le mot de passe d’un certificat.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Indiquer un certificat](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="0f2a2-163">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-163">Cause</span></span>
<span data-ttu-id="0f2a2-164">La passerelle a été inscrite sur d’autres ordinateurs auparavant.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-164">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="0f2a2-165">Lors de l’inscription initiale de la passerelle, un certificat de chiffrement lui a été associé.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="0f2a2-166">Le certificat peut avoir été généré automatiquement par la passerelle ou fourni par l’utilisateur.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-166">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="0f2a2-167">Ce certificat est utilisé pour chiffrer les informations d’identification de la banque de données (service lié).</span><span class="sxs-lookup"><span data-stu-id="0f2a2-167">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Exportation du certificat](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="0f2a2-169">Lorsque vous restaurez la passerelle sur un autre ordinateur hôte, l’Assistant Inscription demande ce certificat afin de déchiffrer les informations d’identification précédemment chiffrées avec ce certificat.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="0f2a2-170">Sans ce certificat, les informations d’identification ne peuvent pas être déchiffrées par la nouvelle passerelle et les exécutions d’activités de copie suivantes associées à cette nouvelle passerelle échouent.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="0f2a2-171">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-171">Resolution</span></span>
<span data-ttu-id="0f2a2-172">Si vous avez exporté le certificat d’informations d’identification de l’ordinateur d’origine de la passerelle avec le bouton **Exporter** de l’onglet **Paramètres** du Gestionnaire de configuration de passerelle de gestion des données, utilisez le certificat ici.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="0f2a2-173">Vous ne pouvez pas ignorer cette étape lors de la récupération d’une passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="0f2a2-174">Si le certificat est manquant, vous devez supprimer la passerelle depuis le portail et en recréer une.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="0f2a2-175">Mettez également à jour tous les services liés associés à la passerelle en entrant à nouveau leurs informations d’identification.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="0f2a2-176">8. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-176">8. Problem</span></span>
<span data-ttu-id="0f2a2-177">Le message d’erreur suivant peut s’afficher.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-177">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="0f2a2-178">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-178">Cause</span></span>
<span data-ttu-id="0f2a2-179">Cette erreur se produit lorsque votre passerelle se trouve dans un environnement qui exige un proxy HTTP pour accéder aux ressources Internet ou lorsque le mot de passe d’authentification de votre serveur proxy est modifié, mais n’est pas actualisé dans votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-180">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-180">Resolution</span></span>
<span data-ttu-id="0f2a2-181">Suivez les instructions de la section [Considérations relatives aux serveurs proxy](#proxy-server-considerations) de cet article et configurez les paramètres de proxy à l’aide du Gestionnaire de configuration de passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="0f2a2-182">La passerelle est en ligne avec des fonctionnalités limitées</span><span class="sxs-lookup"><span data-stu-id="0f2a2-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="0f2a2-183">1. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-183">1. Problem</span></span>
<span data-ttu-id="0f2a2-184">Vous constatez que la passerelle est connectée avec des fonctionnalités limitées.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-184">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="0f2a2-185">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-185">Cause</span></span>
<span data-ttu-id="0f2a2-186">La passerelle peut être connectée avec des fonctionnalités limitées pour l’une des raisons suivantes :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="0f2a2-187">La passerelle ne peut pas se connecter au service cloud via Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-187">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="0f2a2-188">Le service cloud ne peut pas se connecter à la passerelle via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-188">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="0f2a2-189">Lorsque la passerelle est connectée avec des fonctionnalités limitées, il se peut que vous ne soyez pas en mesure d’utiliser l’Assistant de copie Data Factory afin de créer des pipelines de données pour la copie de données vers des banques de données locales ou à partir de celles-ci.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="0f2a2-190">Pour résoudre ce problème, vous pouvez utiliser Data Factory Editor dans le portail, Visual Studio ou Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-191">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-191">Resolution</span></span>
<span data-ttu-id="0f2a2-192">La procédure de résolution de ce problème (passerelle connectée avec des fonctionnalités limitées) n’est pas la même si la passerelle ne peut pas se connecter au service cloud ou si c’est l’inverse.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="0f2a2-193">Les sections suivantes fournissent des solutions.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-193">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="0f2a2-194">2. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-194">2. Problem</span></span>
<span data-ttu-id="0f2a2-195">Vous obtenez l’erreur suivante.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-195">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![La passerelle ne peut pas se connecter au service cloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="0f2a2-197">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-197">Cause</span></span>
<span data-ttu-id="0f2a2-198">La passerelle ne peut pas se connecter au service cloud via Service Bus.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-198">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-199">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-199">Resolution</span></span>
<span data-ttu-id="0f2a2-200">Suivez ces étapes pour remettre la passerelle en ligne :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-200">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="0f2a2-201">Autorisez les règles de trafic sortant d’adresse IP sur l’ordinateur de la passerelle et le pare-feu d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="0f2a2-202">Vous trouverez les adresses IP dans le journal des événements Windows (ID == 401) : Une tentative d’accès à un socket de manière interdite par ses autorisations d’accès a été tentée XX. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="0f2a2-203">Configurez les paramètres de proxy de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-203">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="0f2a2-204">Pour plus d’informations, consultez la section [Considérations relatives aux serveurs proxy](#proxy-server-considerations).</span><span class="sxs-lookup"><span data-stu-id="0f2a2-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="0f2a2-205">Activez les ports sortants 5671 et 9350 à 9354 sur le pare-feu Windows de l’ordinateur passerelle et le pare-feu d’entreprise.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="0f2a2-206">Pour plus d’informations, consultez la section [Ports et pare-feu](#ports-and-firewall).</span><span class="sxs-lookup"><span data-stu-id="0f2a2-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="0f2a2-207">Cette étape est facultative, mais elle est recommandée pour des questions de performances.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="0f2a2-208">3. Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-208">3. Problem</span></span>
<span data-ttu-id="0f2a2-209">Vous obtenez l’erreur suivante.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-209">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="0f2a2-210">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-210">Cause</span></span>
<span data-ttu-id="0f2a2-211">erreur temporaire de connectivité réseau.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-212">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-212">Resolution</span></span>
<span data-ttu-id="0f2a2-213">Suivez ces étapes pour remettre la passerelle en ligne :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-213">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="0f2a2-214">Attendez quelques minutes. La connectivité est récupérée automatiquement une fois que l’erreur a disparu.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="0f2a2-215">Si l’erreur persiste, redémarrez le service de passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-215">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="0f2a2-216">Impossible de créer le service lié</span><span class="sxs-lookup"><span data-stu-id="0f2a2-216">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="0f2a2-217">Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-217">Problem</span></span>
<span data-ttu-id="0f2a2-218">Cette erreur peut s’afficher lorsque vous essayez d’utiliser le Gestionnaire d’informations d’identification dans le portail pour entrer les informations d’identification d’un nouveau service lié ou pour mettre à jour les informations d’identification d’un service lié existant.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="0f2a2-219">Lorsque vous obtenez cette erreur, la page de paramètres du Gestionnaire de configuration de passerelle de gestion des données peut se présenter comme dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![Impossible de contacter la base de données](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="0f2a2-221">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-221">Cause</span></span>
<span data-ttu-id="0f2a2-222">Le certificat SSL a peut-être été perdu sur l’ordinateur de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-222">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="0f2a2-223">L’ordinateur de la passerelle ne peut pas charger le certificat actuellement utilisé pour le chiffrement SSL.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="0f2a2-224">Un message d’erreur similaire au message suivant peut également être affiché dans le journal des événements.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-224">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="0f2a2-225">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-225">Resolution</span></span>
<span data-ttu-id="0f2a2-226">Procédez comme suit pour résoudre le problème :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-226">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="0f2a2-227">Lancez le Gestionnaire de configuration de passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="0f2a2-228">Basculez vers l’onglet **Paramètres** .</span><span class="sxs-lookup"><span data-stu-id="0f2a2-228">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="0f2a2-229">Cliquez sur le bouton **Modifier** pour modifier le certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-229">Click the **Change** button to change the SSL certificate.</span></span>

   ![Bouton de modification du certificat](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="0f2a2-231">Sélectionnez un nouveau certificat comme certificat SSL.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-231">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="0f2a2-232">Vous pouvez utiliser n’importe quel certificat SSL généré par vos soins ou par une organisation quelconque.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Indiquer un certificat](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="0f2a2-234">Échec de l’activité de copie</span><span class="sxs-lookup"><span data-stu-id="0f2a2-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="0f2a2-235">Problème</span><span class="sxs-lookup"><span data-stu-id="0f2a2-235">Problem</span></span>
<span data-ttu-id="0f2a2-236">Vous pouvez obtenir l’erreur « UserErrorFailedToConnectToSqlserver » suivante après avoir configuré un pipeline dans le portail.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="0f2a2-237">Cause :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-237">Cause</span></span>
<span data-ttu-id="0f2a2-238">Cela peut se produire pour différentes raisons et la procédure de résolution varie en conséquence.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="0f2a2-239">Résolution :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-239">Resolution</span></span>
<span data-ttu-id="0f2a2-240">Autorisez les connexions TCP sortantes sur le port TCP/1433 côté client de la passerelle de gestion des données avant la connexion à une base de données SQL.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="0f2a2-241">Si la base de données cible est une base de données SQL Azure, vérifiez également les paramètres de pare-feu SQL Server pour Azure.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="0f2a2-242">Consultez la section suivante pour tester la connexion à la banque de données locale.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-242">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="0f2a2-243">Erreurs liées à la connexion à la banque de données ou au pilote</span><span class="sxs-lookup"><span data-stu-id="0f2a2-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="0f2a2-244">Si vous obtenez des erreurs liées à la connexion à la banque de données ou au pilote, procédez comme suit :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-244">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="0f2a2-245">Lancez le Gestionnaire de configuration de passerelle de gestion des données sur l’ordinateur de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="0f2a2-246">Basculez vers l’onglet **Diagnostics** .</span><span class="sxs-lookup"><span data-stu-id="0f2a2-246">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="0f2a2-247">Dans **Tester la connexion**, ajoutez les valeurs de groupe de la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-247">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="0f2a2-248">Cliquez sur **Tester la connexion** pour vérifier si vous pouvez vous connecter à la source de données locale à partir de l’ordinateur de la passerelle en utilisant les informations de connexion et d’identification.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="0f2a2-249">Si le test de connexion échoue encore après l'installation d'un pilote, redémarrez la passerelle pour récupérer les dernières modifications.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Tester la connexion dans l’onglet Diagnostics](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="0f2a2-251">Journaux de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0f2a2-251">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="0f2a2-252">Envoyer les journaux de la passerelle à Microsoft</span><span class="sxs-lookup"><span data-stu-id="0f2a2-252">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="0f2a2-253">Lorsque vous contactez le Support Microsoft pour résoudre des problèmes de passerelle, il peut vous être demandé de fournir les journaux de votre passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="0f2a2-254">Avec la dernière version de la passerelle, vous pouvez partager les journaux de passerelle requis en deux clics de bouton dans le Gestionnaire de configuration de passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="0f2a2-255">Basculez vers l’onglet **Diagnostics** du Gestionnaire de configuration de passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Onglet Diagnostics de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="0f2a2-257">Cliquez sur **Envoyer des journaux** pour afficher la boîte de dialogue suivante.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-257">Click **Send Logs** to see the following dialog box.</span></span>

    ![Lien Envoyer des journaux de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="0f2a2-259">(Facultatif) Cliquez sur **Afficher les journaux** pour consulter les journaux dans l’Observateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-259">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="0f2a2-260">(Facultatif) Cliquez sur **Confidentialité** pour consulter la déclaration de confidentialité relative aux services web Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="0f2a2-261">Lorsque vous êtes satisfait des éléments que vous vous apprêtez à charger, cliquez sur **Envoyer des journaux** pour envoyer les journaux des sept derniers jours à Microsoft en vue de résoudre les problèmes.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="0f2a2-262">L’état de l’opération d’envoi des journaux devrait s’afficher comme dans la capture d’image suivante.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-262">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![État de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="0f2a2-264">Une fois l’opération terminée, la boîte de dialogue illustrée dans la capture d’écran suivante s’affiche.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![État de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="0f2a2-266">Notez l’**ID du rapport** et communiquez-le au Support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-266">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="0f2a2-267">L’ID du rapport permet de localiser les journaux de la passerelle que vous avez chargés pour la résolution des problèmes.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="0f2a2-268">L’ID du rapport est également enregistré dans l’Observateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-268">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="0f2a2-269">Vous pouvez le trouver en recherchant l’ID d’événement « 25 » et en vérifiant la date et l’heure.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-269">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![ID du rapport de l’opération Envoyer des journaux pour la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="0f2a2-271">La passerelle d’archive ouvre une session sur l’ordinateur hôte de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0f2a2-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="0f2a2-272">Dans certains cas, il se peut que vous ayez des problèmes avec la passerelle et que vous ne puissiez pas partager directement les journaux de la passerelle :</span><span class="sxs-lookup"><span data-stu-id="0f2a2-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="0f2a2-273">Vous installez et inscrivez manuellement la passerelle.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-273">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="0f2a2-274">Vous essayez d’inscrire la passerelle avec une clé régénérée dans le Gestionnaire de configuration de passerelle de gestion des données.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="0f2a2-275">Vous tentez d’envoyer des journaux et le service hôte de la passerelle ne peut pas être connecté.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-275">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="0f2a2-276">Dans ces cas de figure, vous pouvez enregistrer les journaux de la passerelle dans un fichier zip et fournir celui-ci au Support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="0f2a2-277">Par exemple, si vous recevez une erreur lorsque vous inscrivez la passerelle, comme illustré dans la capture d’écran suivante.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Erreur d’inscription de la passerelle de gestion des données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="0f2a2-279">Cliquez sur le lien **Archiver les journaux de la passerelle** pour archiver et enregistrer les journaux, puis fournissez le fichier zip au Support Microsoft.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Lien Archiver les journaux de la passerelle de gestion de données](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="0f2a2-281">Rechercher dans les journaux de la passerelle</span><span class="sxs-lookup"><span data-stu-id="0f2a2-281">Locate gateway logs</span></span>
<span data-ttu-id="0f2a2-282">Vous pouvez accéder à des informations détaillées sur les journaux de la passerelle dans les journaux d’événements Windows.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-282">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="0f2a2-283">Démarrez l’**Observateur d’événements** Windows.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="0f2a2-284">Localisez les journaux dans le dossier **Journaux des applications et services** > **Passerelle de gestion des données**.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="0f2a2-285">Lors de la résolution de problèmes liés à la passerelle, recherchez les événements de niveau Erreur dans l’Observateur d’événements.</span><span class="sxs-lookup"><span data-stu-id="0f2a2-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Journaux de la passerelle de gestion des données dans l’Observateur d’événements](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
