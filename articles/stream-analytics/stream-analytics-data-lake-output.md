---
title: "aaaStream la sortie de magasin de données Analytique Lake | Documents Microsoft"
description: "Configuration de l’authentification et de l’autorisation d’Azure Data Lake Store dans un travail Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: ea5baafa-0054-4c70-973a-6a3a8c6eaffc
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 183cf51edb2e49ac3e42257e67a8077b95777258
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="stream-analytics-data-lake-store-output"></a><span data-ttu-id="d2c86-103">Sortie de Stream Analytics Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d2c86-103">Stream Analytics Data Lake Store output</span></span>
<span data-ttu-id="d2c86-104">Les travaux Stream Analytics prennent en charge plusieurs méthodes de sortie, dont [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span><span class="sxs-lookup"><span data-stu-id="d2c86-104">Stream Analytics jobs support several output methods, one being an [Azure Data Lake Store](https://azure.microsoft.com/services/data-lake-store/).</span></span> <span data-ttu-id="d2c86-105">Azure Data Lake Store est un référentiel d'entreprise à très grande échelle pour les charges de travail d'analyse du Big Data.</span><span class="sxs-lookup"><span data-stu-id="d2c86-105">Azure Data Lake Store is an enterprise-wide hyper-scale repository for big data analytic workloads.</span></span> <span data-ttu-id="d2c86-106">Data Lake Store vous permet de toostore les données de n’importe quelle vitesse de taille, de type et de réception pour l’analytique opérationnelle et exploratoire.</span><span class="sxs-lookup"><span data-stu-id="d2c86-106">Data Lake Store enables you toostore data of any size, type and ingestion speed for operational and exploratory analytics.</span></span>

## <a name="authorize-a-data-lake-store-account"></a><span data-ttu-id="d2c86-107">Autoriser un compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d2c86-107">Authorize a Data Lake Store account</span></span>
1. <span data-ttu-id="d2c86-108">Si Data Lake Store est sélectionnée comme une sortie Bonjour portail Azure, vous devez utiliser tooauthorize votre Data Lake Store existant ou d’un toorequest accéder toohello Data Lake Store via hello portail classique.</span><span class="sxs-lookup"><span data-stu-id="d2c86-108">When Data Lake Store is selected as an output in hello Azure portal, you will be prompted tooauthorize use of your existing Data Lake Store or toorequest access toohello Data Lake Store via hello Classic Portal.</span></span>
   
   ![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-authorization.png)  
   
2. <span data-ttu-id="d2c86-109">Si vous avez déjà accès tooData Lake Store, cliquez sur « Autoriser » et pendant un bref instant une page s’affiche indiquant « Tooauthorization redirection ».</span><span class="sxs-lookup"><span data-stu-id="d2c86-109">If you already have access tooData Lake Store, click “Authorize Now” and for a brief time a page will pop up indicating “Redirecting tooauthorization”.</span></span> <span data-ttu-id="d2c86-110">page de Hello se fermera automatiquement et vous n’aurez page hello qui vous permettrait tooconfigure hello Data Lake Store sortie.</span><span class="sxs-lookup"><span data-stu-id="d2c86-110">hello page will automatically close and you will be presented with hello page that would allow you tooconfigure hello Data Lake Store output.</span></span>

<span data-ttu-id="d2c86-111">Si vous n'êtes pas inscrit à Data Lake Store, vous pouvez suivre la demande des hello de support pour les tooinitiate de lien hello « Connexion », ou suivez hello [obtenir des instructions démarrées](../data-lake-store/data-lake-store-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="d2c86-111">If you have not signed up for Data Lake Store, you can follow hello “Sign up now” link tooinitiate hello request, or follow hello [get started instructions](../data-lake-store/data-lake-store-get-started-portal.md).</span></span>

## <a name="configure-hello-data-lake-store-output-properties"></a><span data-ttu-id="d2c86-112">Configurer les propriétés de sortie hello Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d2c86-112">Configure hello Data Lake Store output properties</span></span>
<span data-ttu-id="d2c86-113">Une fois que vous avez compte Data Lake Store de hello authentifié, vous pouvez configurer les propriétés de hello pour votre sortie Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d2c86-113">Once you have hello Data Lake Store account authenticated, you can configure hello properties for your Data Lake Store output.</span></span> <span data-ttu-id="d2c86-114">tableau Hello ci-dessous est liste hello des noms de propriétés et leur tooconfigure description que votre Data Lake Store de sortie.</span><span class="sxs-lookup"><span data-stu-id="d2c86-114">hello table below is hello list of property names and their description tooconfigure your Data Lake Store output.</span></span>

<table>
<tbody>
<tr>
<td><span data-ttu-id="d2c86-115"><B>NOM DE LA PROPRIÉTÉ</B></span><span class="sxs-lookup"><span data-stu-id="d2c86-115"><B>PROPERTY NAME</B></span></span></td>
<td><span data-ttu-id="d2c86-116"><B>DESCRIPTION</B></span><span class="sxs-lookup"><span data-stu-id="d2c86-116"><B>DESCRIPTION</B></span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-117">Alias de sortie</span><span class="sxs-lookup"><span data-stu-id="d2c86-117">Output Alias</span></span></td>
<td><span data-ttu-id="d2c86-118">Il s’agit d’un nom convivial utilisé dans les requêtes toodirect hello requête sortie toothis Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d2c86-118">This is a friendly name used in queries toodirect hello query output toothis Data Lake Store.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-119">Compte Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d2c86-119">Data Lake Store Account</span></span></td>
<td><span data-ttu-id="d2c86-120">nom Hello hello du compte de stockage où vous envoyez votre sortie.</span><span class="sxs-lookup"><span data-stu-id="d2c86-120">hello name of hello storage account where you are sending your output.</span></span> <span data-ttu-id="d2c86-121">Une liste des comptes Data Lake Store hello à l’utilisateur connecté a accès à s’affiche.</span><span class="sxs-lookup"><span data-stu-id="d2c86-121">You will be presented with a list of Data Lake Store accounts  hello logged in user has access to.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-122">Séquence d’octets préfixe du chemin d’accès [<I>facultative</I>]</span><span class="sxs-lookup"><span data-stu-id="d2c86-122">Path Prefix Pattern [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="d2c86-123">Hello toowrite de chemin d’accès du fichier vos fichiers au sein de hello spécifié le compte de magasin Data Lake.</span><span class="sxs-lookup"><span data-stu-id="d2c86-123">hello file path used toowrite your files within hello specified Data Lake Store Account.</span></span> <BR><span data-ttu-id="d2c86-124">{date}, {time}</span><span class="sxs-lookup"><span data-stu-id="d2c86-124">{date}, {time}</span></span><BR><span data-ttu-id="d2c86-125">Exemple 1 : dossier1/journaux/{date}/{heure}</span><span class="sxs-lookup"><span data-stu-id="d2c86-125">Example 1: folder1/logs/{date}/{time}</span></span><BR><span data-ttu-id="d2c86-126">Exemple 2 : dossier1/journaux/{date}</span><span class="sxs-lookup"><span data-stu-id="d2c86-126">Example 2: folder1/logs/{date}</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-127">Format de la date [<I>facultatif</I>]</span><span class="sxs-lookup"><span data-stu-id="d2c86-127">Date Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="d2c86-128">Si le jeton de date hello est utilisé dans le chemin d’accès de hello préfixe, vous pouvez sélectionner le format de date hello dans lequel vos fichiers sont organisés.</span><span class="sxs-lookup"><span data-stu-id="d2c86-128">If hello date token is used in hello prefix path, you can select hello date format in which your files are organized.</span></span> <span data-ttu-id="d2c86-129">Exemple : JJ/MM/AAAA</span><span class="sxs-lookup"><span data-stu-id="d2c86-129">Example: YYYY/MM/DD</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-130">Format de l’heure [<I>facultatif</I>]</span><span class="sxs-lookup"><span data-stu-id="d2c86-130">Time Format [<I>optional</I>]</span></span></td>
<td><span data-ttu-id="d2c86-131">Si le jeton de durée hello est utilisé dans le chemin d’accès de hello préfixe, spécifiez le format d’heure hello dans lequel vos fichiers sont organisés.</span><span class="sxs-lookup"><span data-stu-id="d2c86-131">If hello time token is used in hello prefix path, specify hello time format in which your files are organized.</span></span> <span data-ttu-id="d2c86-132">Valeur de hello uniquement pris en charge actuellement est HH.</span><span class="sxs-lookup"><span data-stu-id="d2c86-132">Currently hello only supported value is HH.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-133">Format de sérialisation de l’événement</span><span class="sxs-lookup"><span data-stu-id="d2c86-133">Event Serialization Format</span></span></td>
<td><span data-ttu-id="d2c86-134">Format de sérialisation pour les données de sortie.</span><span class="sxs-lookup"><span data-stu-id="d2c86-134">Serialization format for output data.</span></span> <span data-ttu-id="d2c86-135">JSON, CSV et Avro sont pris en charge.</span><span class="sxs-lookup"><span data-stu-id="d2c86-135">JSON, CSV, and Avro are supported.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-136">Encodage</span><span class="sxs-lookup"><span data-stu-id="d2c86-136">Encoding</span></span></td>
<td><span data-ttu-id="d2c86-137">S’il s’agit du format CSV ou JSON, un encodage doit être spécifié.</span><span class="sxs-lookup"><span data-stu-id="d2c86-137">If CSV or JSON format, an encoding must be specified.</span></span> <span data-ttu-id="d2c86-138">UTF-8 est hello uniquement une prise en charge de format d’encodage pour l’instant.</span><span class="sxs-lookup"><span data-stu-id="d2c86-138">UTF-8 is hello only supported encoding format at this time.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-139">Délimiteur</span><span class="sxs-lookup"><span data-stu-id="d2c86-139">Delimiter</span></span></td>
<td><span data-ttu-id="d2c86-140">Applicable uniquement pour la sérialisation CSV.</span><span class="sxs-lookup"><span data-stu-id="d2c86-140">Only applicable for CSV serialization.</span></span> <span data-ttu-id="d2c86-141">Stream Analytics prend en charge un certain nombre de délimiteurs communs pour sérialiser des données CSV.</span><span class="sxs-lookup"><span data-stu-id="d2c86-141">Stream Analytics supports a number of common delimiters for serializing CSV data.</span></span> <span data-ttu-id="d2c86-142">Valeurs prises en charge : virgule, point-virgule, espace, tabulation et barre verticale.</span><span class="sxs-lookup"><span data-stu-id="d2c86-142">Supported values are comma, semicolon, space, tab and vertical bar.</span></span></td>
</tr>
<tr>
<td><span data-ttu-id="d2c86-143">Format</span><span class="sxs-lookup"><span data-stu-id="d2c86-143">Format</span></span></td>
<td><span data-ttu-id="d2c86-144">Applicable uniquement pour la sérialisation JSON.</span><span class="sxs-lookup"><span data-stu-id="d2c86-144">Only applicable for JSON serialization.</span></span> <span data-ttu-id="d2c86-145">Ligne séparée spécifie la sortie de hello sera formatée en par chaque objet JSON séparé par une nouvelle ligne.</span><span class="sxs-lookup"><span data-stu-id="d2c86-145">Line separated specifies that hello output will be formatted by having each JSON object separated by a new line.</span></span> <span data-ttu-id="d2c86-146">Le tableau spécifie que sortie de hello sera mise en forme en tant que tableau d’objets JSON.</span><span class="sxs-lookup"><span data-stu-id="d2c86-146">Array specifies that hello output will be formatted as an array of JSON objects.</span></span></td>
</tr>
</tbody>
</table>

## <a name="renew-data-lake-store-authorization"></a><span data-ttu-id="d2c86-147">Renouveler une autorisation Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="d2c86-147">Renew Data Lake Store Authorization</span></span>
<span data-ttu-id="d2c86-148">Actuellement, il agit d’une limitation où le jeton d’authentification hello doit toobe actualisée manuellement tous les 90 jours pour tous les travaux avec une sortie de Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d2c86-148">Currently, there is a limitation where hello authentication token needs toobe manually refreshed every 90 days for all jobs with Data Lake Store output.</span></span> <span data-ttu-id="d2c86-149">Vous devez également toore-authentifier votre compte Data Lake Store si vous avez modifié votre mot de passe depuis la création ou de dernière authentification de votre travail.</span><span class="sxs-lookup"><span data-stu-id="d2c86-149">You will also need toore-authenticate your Data Lake Store account if you have changed your password since your job was created or last authenticated.</span></span> <span data-ttu-id="d2c86-150">Un symptôme de ce problème est aucune sortie de travail et une erreur dans les journaux des opérations de hello indiquant la nécessité pour l’autorisation de nouveau.</span><span class="sxs-lookup"><span data-stu-id="d2c86-150">A symptom of this issue is no job output and an error in hello Operation Logs indicating need for re-authorization.</span></span>

<span data-ttu-id="d2c86-151">tooresolve ce problème, arrêtez votre travail en cours d’exécution et accédez de sortie tooyour Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="d2c86-151">tooresolve this issue, stop your running job and go tooyour Data Lake Store output.</span></span> <span data-ttu-id="d2c86-152">Cliquez sur le lien de « Renouveler l’autorisation » hello et pendant une brève période une page s’affiche indiquant « Redirection tooauthorization.. ».</span><span class="sxs-lookup"><span data-stu-id="d2c86-152">Click hello “Renew authorization” link, and for a brief time a page will pop up indicating “Redirecting tooauthorization..”.</span></span> <span data-ttu-id="d2c86-153">page de Hello se fermera automatiquement et en cas de réussite, indiquera « Autorisation a été renouvelée ».</span><span class="sxs-lookup"><span data-stu-id="d2c86-153">hello page will automatically close and if successful, will indicate “Authorization has been successfully renewed”.</span></span> <span data-ttu-id="d2c86-154">Vous devez tooclick « Enregistrer » en bas de hello de page de hello, puis pouvez continuer en redémarrant votre travail à partir de la perte de données heure du dernier arrêt tooavoid de hello.</span><span class="sxs-lookup"><span data-stu-id="d2c86-154">You then need tooclick “Save” at hello bottom of hello page, and can proceed by restarting your job from hello Last Stopped Time tooavoid data loss.</span></span>

![](media/stream-analytics-data-lake-output/stream-analytics-data-lake-output-renew-authorization.png)

