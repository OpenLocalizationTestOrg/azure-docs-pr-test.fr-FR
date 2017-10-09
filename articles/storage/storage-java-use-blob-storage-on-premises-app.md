---
title: "application aaaOn local avec le stockage d’objets blob (Java) | Documents Microsoft"
description: "Découvrez comment toocreate une application console qui télécharge un tooAzure d’image, puis affiche hello image dans votre navigateur. Les exemples de code sont écrits en Java."
services: storage
documentationcenter: java
author: mmacy
manager: carmonm
editor: tysonn
ms.assetid: ccc9a7d7-6fe4-467b-b7fd-a73f17539e3f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 11/17/2016
ms.author: marsma
ms.openlocfilehash: ed8eb4c1045691c25abe94bf6c1b18b797adc3e3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 10/06/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="79881-104">Application locale avec stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="79881-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="79881-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="79881-105">Overview</span></span>
<span data-ttu-id="79881-106">Hello suivant montre comment vous pouvez utiliser le stockage Azure pour stocker les images dans Azure.</span><span class="sxs-lookup"><span data-stu-id="79881-106">hello following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="79881-107">code Hello dans cet article est pour une application console qui télécharge un tooAzure d’image, puis crée un fichier HTML qui affiche l’image de hello dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="79881-107">hello code in this article is for a console application that uploads an image tooAzure, and then creates an HTML file that displays hello image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79881-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="79881-108">Prerequisites</span></span>
* <span data-ttu-id="79881-109">Le Kit de développement logiciel Java (JDK) version 1.6 ou ultérieure est installé.</span><span class="sxs-lookup"><span data-stu-id="79881-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="79881-110">Bonjour Azure SDK est installé.</span><span class="sxs-lookup"><span data-stu-id="79881-110">hello Azure SDK is installed.</span></span>
* <span data-ttu-id="79881-111">Bonjour JAR pour hello les bibliothèques Azure pour Java et les fichiers JAR dépendance applicable, est installés et se trouvent dans le chemin d’accès de build hello utilisé par le compilateur Java.</span><span class="sxs-lookup"><span data-stu-id="79881-111">hello JAR for hello Azure Libraries for Java, and any applicable dependency JARs, are installed and are in hello build path used by your Java compiler.</span></span> <span data-ttu-id="79881-112">Pour plus d’informations sur l’installation des bibliothèques de Azure hello pour Java, consultez [téléchargement hello SDK Azure pour Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="79881-112">For information about installing hello Azure Libraries for Java, see [Download hello Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="79881-113">Un compte de stockage Azure a été configuré.</span><span class="sxs-lookup"><span data-stu-id="79881-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="79881-114">Hello nom de compte et de la clé de compte pour le compte de stockage hello servira par code hello dans cet article.</span><span class="sxs-lookup"><span data-stu-id="79881-114">hello account name and account key for hello storage account will be used by hello code in this article.</span></span> <span data-ttu-id="79881-115">Consultez [comment tooCreate un compte de stockage](storage-create-storage-account.md#create-a-storage-account) pour plus d’informations sur la création d’un compte de stockage et [clés d’accès afficher et copier](storage-create-storage-account.md#view-and-copy-storage-access-keys) pour plus d’informations sur la récupération de clé de compte hello.</span><span class="sxs-lookup"><span data-stu-id="79881-115">See [How tooCreate a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving hello account key.</span></span>
* <span data-ttu-id="79881-116">Vous avez créé un fichier d’image locale nommé stockés sur hello path c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="79881-116">You have created a local image file named stored at hello path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="79881-117">Vous pouvez également modifier le **FileInputStream** constructeur dans hello exemple toouse un image différente chemin d’accès et nom de fichier.</span><span class="sxs-lookup"><span data-stu-id="79881-117">Alternatively, modify the **FileInputStream** constructor in hello example toouse a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="toouse-azure-blob-storage-tooupload-a-file"></a><span data-ttu-id="79881-118">tooupload de stockage d’objets blob Azure toouse un fichier</span><span class="sxs-lookup"><span data-stu-id="79881-118">toouse Azure blob storage tooupload a file</span></span>
<span data-ttu-id="79881-119">La procédure présentée ici détaille chaque étape.</span><span class="sxs-lookup"><span data-stu-id="79881-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="79881-120">Si vous souhaitez que tooskip de manière anticipée, code d’entier hello est présenté plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="79881-120">If you'd like tooskip ahead, hello entire code is presented later in this article.</span></span>

<span data-ttu-id="79881-121">Commencer le code de hello en incluant des imports pour les classes de stockage Azure de base hello, classes de client d’objets blob Azure hello, classes d’e/s Java hello et hello **URISyntaxException** classe.</span><span class="sxs-lookup"><span data-stu-id="79881-121">Begin hello code by including imports for hello Azure core storage classes, hello Azure blob client classes, hello Java IO classes, and hello **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="79881-122">Déclarez une classe nommée **StorageSample**et inclure le crochet hello, **{**.</span><span class="sxs-lookup"><span data-stu-id="79881-122">Declare a class named **StorageSample**, and include hello open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="79881-123">Au sein de hello **StorageSample** de classe, déclarez une variable de chaîne qui contiendra le protocole de point de terminaison hello par défaut, le nom de votre compte de stockage et votre clé d’accès, tel que spécifié dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="79881-123">Within hello **StorageSample** class, declare a string variable that will contain hello default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="79881-124">Remplacez les valeurs d’espace réservé hello **votre\_compte\_nom** et **votre\_compte\_clé** avec votre propre nom de compte et de la clé de compte, respectivement.</span><span class="sxs-lookup"><span data-stu-id="79881-124">Replace hello placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="79881-125">Ajouter dans votre déclaration de **principal**, inclure un **essayez** bloquer et inclure des crochets ouvrants nécessaires de hello, **{**.</span><span class="sxs-lookup"><span data-stu-id="79881-125">Add in your declaration for **main**, include a **try** block, and include hello necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="79881-126">Déclarer des variables de hello suite type (hello sont des descriptions de la façon dont elles sont utilisées dans cet exemple) :</span><span class="sxs-lookup"><span data-stu-id="79881-126">Declare variables of hello following type (hello descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="79881-127">**CloudStorageAccount**: objet avec votre nom de compte de stockage Azure et la clé et la toocreate du compte utilisé tooinitialize hello l’objet blob du client.</span><span class="sxs-lookup"><span data-stu-id="79881-127">**CloudStorageAccount**: Used tooinitialize hello account object with your Azure storage account name and key, and toocreate the blob client object.</span></span>
* <span data-ttu-id="79881-128">**CloudBlobClient**: tooaccess hello blob service utilisés.</span><span class="sxs-lookup"><span data-stu-id="79881-128">**CloudBlobClient**: Used tooaccess hello blob service.</span></span>
* <span data-ttu-id="79881-129">**CloudBlobContainer**: toocreate utilisé un conteneur d’objets blob, liste d’objets BLOB dans le conteneur de hello et delete hello conteneur.</span><span class="sxs-lookup"><span data-stu-id="79881-129">**CloudBlobContainer**: Used toocreate a blob container, list the blobs in hello container, and delete hello container.</span></span>
* <span data-ttu-id="79881-130">**CloudBlockBlob**: tooupload utilisé un conteneur toothe du fichier image locale.</span><span class="sxs-lookup"><span data-stu-id="79881-130">**CloudBlockBlob**: Used tooupload a local image file toothe container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="79881-131">Affecter une valeur toohello **compte** variable.</span><span class="sxs-lookup"><span data-stu-id="79881-131">Assign a value toohello **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="79881-132">Affecter une valeur toohello **serviceClient** variable.</span><span class="sxs-lookup"><span data-stu-id="79881-132">Assign a value toohello **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="79881-133">Affecter une valeur toohello **conteneur** variable.</span><span class="sxs-lookup"><span data-stu-id="79881-133">Assign a value toohello **container** variable.</span></span> <span data-ttu-id="79881-134">Nous obtenons un conteneur de tooa référence nommé **mise en route**.</span><span class="sxs-lookup"><span data-stu-id="79881-134">We'll get a reference tooa container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="79881-135">Créer un conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="79881-135">Create hello container.</span></span> <span data-ttu-id="79881-136">Cette méthode crée le conteneur de hello si elle n’existe pas (et retourner **true**).</span><span class="sxs-lookup"><span data-stu-id="79881-136">This method will create hello container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="79881-137">Si le conteneur de hello existe, elle retournera **false**.</span><span class="sxs-lookup"><span data-stu-id="79881-137">If hello container does exist, it will return **false**.</span></span> <span data-ttu-id="79881-138">Une alternative trop**createIfNotExists** est hello **créer** (méthode) (qui retourne une erreur si le conteneur de hello existe déjà).</span><span class="sxs-lookup"><span data-stu-id="79881-138">An alternative too**createIfNotExists** is hello **create** method (which will return an error if hello container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="79881-139">Définir l’accès anonyme pour le conteneur de hello.</span><span class="sxs-lookup"><span data-stu-id="79881-139">Set anonymous access for hello container.</span></span>

```java
// Set anonymous access on hello container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="79881-140">Obtenir un référence toohello objet blob de blocs, qui représente les blob hello dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="79881-140">Get a reference toohello block blob, which will represent hello blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="79881-141">Hello d’utilisation **fichier** constructeur tooget un fichier toohello créé localement de référence que vous allez télécharger.</span><span class="sxs-lookup"><span data-stu-id="79881-141">Use hello **File** constructor tooget a reference toohello locally created file that you will upload.</span></span> <span data-ttu-id="79881-142">Assurez-vous que vous avez créé ce fichier avant d’exécuter le code de hello.</span><span class="sxs-lookup"><span data-stu-id="79881-142">Ensure you have created this file before running hello code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="79881-143">Télécharger hello le fichier local via un appel de toohello **CloudBlockBlob.upload** (méthode).</span><span class="sxs-lookup"><span data-stu-id="79881-143">Upload hello local file through a call toohello **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="79881-144">Hello premier paramètre toohello **CloudBlockBlob.upload** méthode est un **FileInputStream** ce fichier local de hello représente qui sera téléchargé tooAzure stockage de l’objet.</span><span class="sxs-lookup"><span data-stu-id="79881-144">hello first parameter toohello **CloudBlockBlob.upload** method is a **FileInputStream** object that represents hello local file that will be uploaded tooAzure storage.</span></span> <span data-ttu-id="79881-145">Hello deuxième paramètre est hello taille, en octets, du fichier de hello.</span><span class="sxs-lookup"><span data-stu-id="79881-145">hello second parameter is hello size, in bytes, of hello file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="79881-146">Appeler une fonction d’assistance nommée **MakeHTMLPage**, page toomake un contenu HTML de base qui contient un  **&lt;image&gt;**  élément avec hello ensemble toohello objet blob source qui est désormais dans votre Azure compte de stockage.</span><span class="sxs-lookup"><span data-stu-id="79881-146">Call a helper function named **MakeHTMLPage**, toomake a basic HTML page that contains an **&lt;image&gt;** element with hello source set toohello blob that is now in your Azure storage account.</span></span> <span data-ttu-id="79881-147">Hello code **MakeHTMLPage** l’aborderons plus loin dans cet article.</span><span class="sxs-lookup"><span data-stu-id="79881-147">hello code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="79881-148">Imprime un message d’état et les informations sur hello créé de page HTML.</span><span class="sxs-lookup"><span data-stu-id="79881-148">Print out a status message and information about hello created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html toosee hello images stored in your storage account.");
```

<span data-ttu-id="79881-149">Fermer hello **essayez** bloc en insérant un crochet fermant : **}**</span><span class="sxs-lookup"><span data-stu-id="79881-149">Close hello **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="79881-150">Gérer hello suivant des exceptions :</span><span class="sxs-lookup"><span data-stu-id="79881-150">Handle hello following exceptions:</span></span>

* <span data-ttu-id="79881-151">**FileNotFoundException**: pouvant être levées par hello **FileInputStream** ou **FileOutputStream** constructeurs.</span><span class="sxs-lookup"><span data-stu-id="79881-151">**FileNotFoundException**: Can be thrown by hello **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="79881-152">**StorageException**: pouvant être levées par la bibliothèque de stockage Azure client hello.</span><span class="sxs-lookup"><span data-stu-id="79881-152">**StorageException**: Can be thrown by hello Azure client storage library.</span></span>
* <span data-ttu-id="79881-153">**URISyntaxException**: pouvant être levées par hello **ListBlobItem.getUri** (méthode).</span><span class="sxs-lookup"><span data-stu-id="79881-153">**URISyntaxException**: Can be thrown by hello **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="79881-154">**Exception**: traitement d’une exception générique.</span><span class="sxs-lookup"><span data-stu-id="79881-154">**Exception**: Generic exception handling.</span></span>

<!-- -->

```java
catch (FileNotFoundException fileNotFoundException)
{
    System.out.print("FileNotFoundException encountered: ");
    System.out.println(fileNotFoundException.getMessage());
    System.exit(-1);
}
catch (StorageException storageException)
{
    System.out.print("StorageException encountered: ");
    System.out.println(storageException.getMessage());
    System.exit(-1);
}
catch (URISyntaxException uriSyntaxException)
{
    System.out.print("URISyntaxException encountered: ");
    System.out.println(uriSyntaxException.getMessage());
    System.exit(-1);
}
catch (Exception e)
{
    System.out.print("Exception encountered: ");
    System.out.println(e.getMessage());
    System.exit(-1);
}
```

<span data-ttu-id="79881-155">Fermez **main** en insérant une parenthèse fermante : **}**</span><span class="sxs-lookup"><span data-stu-id="79881-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="79881-156">Créez une méthode nommée **MakeHTMLPage** page de toocreate un contenu HTML de base.</span><span class="sxs-lookup"><span data-stu-id="79881-156">Create a method named **MakeHTMLPage** toocreate a basic HTML page.</span></span> <span data-ttu-id="79881-157">Cette méthode a un paramètre de type **CloudBlobContainer**, qui sera utilisé tooiterate liste hello d’objets BLOB téléchargés.</span><span class="sxs-lookup"><span data-stu-id="79881-157">This method has a parameter of type **CloudBlobContainer**, which will be used tooiterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="79881-158">Cette méthode lève les exceptions de type **FileNotFoundException**, qui peuvent être levé par hello **FileOutputStream** constructeur, et **URISyntaxException**, ce qui risque levée par hello **ListBlobItem.getUri** (méthode).</span><span class="sxs-lookup"><span data-stu-id="79881-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by hello **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by hello **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="79881-159">Incluez le crochet ouvrant **{**.</span><span class="sxs-lookup"><span data-stu-id="79881-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="79881-160">Créez un fichier local nommé **index.html**.</span><span class="sxs-lookup"><span data-stu-id="79881-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="79881-161">Écrire le fichier local toohello, ajout Bonjour  **&lt;html&gt;**,  **&lt;en-tête&gt;**, et  **&lt;corps&gt;**  éléments.</span><span class="sxs-lookup"><span data-stu-id="79881-161">Write toohello local file, adding in hello **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="79881-162">Parcourir la liste hello d’objets BLOB téléchargés.</span><span class="sxs-lookup"><span data-stu-id="79881-162">Iterate through hello list of uploaded blobs.</span></span> <span data-ttu-id="79881-163">Pour chaque objet blob, dans la page de hello HTML, créez un  **&lt;img&gt;**  élément qui a son **src** attribut envoyé Hello URI d’objet blob de hello telle qu’elle existe dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="79881-163">For each blob, in hello HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to hello URI of hello blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="79881-164">Dans cet exemple, vous avez ajouté une seule image, mais si vous en ajoutiez plus, ce code effectuerait une itération pour chacune d'entre elles.</span><span class="sxs-lookup"><span data-stu-id="79881-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="79881-165">Par souci de simplification, cet exemple part du principe que chaque objet blob chargé est une image.</span><span class="sxs-lookup"><span data-stu-id="79881-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="79881-166">Si vous avez mis à jour des objets BLOB autres que des images ou des objets BLOB de pages au lieu d’objets BLOB de blocs, ajustez le code hello en fonction des besoins.</span><span class="sxs-lookup"><span data-stu-id="79881-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust hello code as needed.</span></span>

```java
// Enumerate hello uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in hello HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="79881-167">Fermer hello  **&lt;corps&gt;**  élément et hello  **&lt;html&gt;**  élément.</span><span class="sxs-lookup"><span data-stu-id="79881-167">Close hello **&lt;body&gt;** element and hello **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="79881-168">Fichier local de fermer hello.</span><span class="sxs-lookup"><span data-stu-id="79881-168">Close hello local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="79881-169">Fermez **MakeHTMLPage** en insérant une parenthèse fermante : **}**</span><span class="sxs-lookup"><span data-stu-id="79881-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="79881-170">Fermez **StorageSample** en insérant une parenthèse fermante : **}**</span><span class="sxs-lookup"><span data-stu-id="79881-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="79881-171">Hello Voici code complet de hello pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="79881-171">hello following is hello complete code for this example.</span></span> <span data-ttu-id="79881-172">N’oubliez pas de valeurs d’espace réservé hello toomodify **votre\_compte\_nom** et **votre\_compte\_clé** toouse votre nom de compte et un compte la clé, respectivement.</span><span class="sxs-lookup"><span data-stu-id="79881-172">Remember toomodify hello placeholder values **your\_account\_name** and **your\_account\_key** toouse your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior toorunning this sample.
// Alternatively, change hello value used by hello FileInputStream constructor
// toouse a different image path and file that you have already created.
public class StorageSample {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                    "AccountName=your_account_name;" +
                    "AccountKey=your_account_name";

    public static void main(String[] args) {
        try {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;
            CloudBlockBlob blob;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.createIfNotExists();

            // Set anonymous access on hello container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point hello image is uploaded.
            // Next, create an HTML page that lists all of hello uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html toosee hello images stored in your storage account.");

        } catch (FileNotFoundException fileNotFoundException) {
            System.out.print("FileNotFoundException encountered: ");
            System.out.println(fileNotFoundException.getMessage());
            System.exit(-1);
        } catch (StorageException storageException) {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        } catch (URISyntaxException uriSyntaxException) {
            System.out.print("URISyntaxException encountered: ");
            System.out.println(uriSyntaxException.getMessage());
            System.exit(-1);
        } catch (Exception e) {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }

    // Create an HTML page that can be used toodisplay hello uploaded images.
    // This example assumes all of hello blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create hello opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate hello uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in hello HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete hello <html> element and close hello file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="79881-173">Dans Ajout toouploading votre stockage tooAzure du fichier image locale, hello exemple de code crée un fichier local namedindex.html, que vous pouvez ouvrir dans votre navigateur toosee votre image téléchargée.</span><span class="sxs-lookup"><span data-stu-id="79881-173">In addition toouploading your local image file tooAzure storage, hello example code creates a local file namedindex.html, which you can open in your browser toosee your uploaded image.</span></span>

<span data-ttu-id="79881-174">Étant donné que le code de hello contient votre nom de compte et votre clé de compte, assurez-vous que votre code source est sécurisé.</span><span class="sxs-lookup"><span data-stu-id="79881-174">Because hello code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="toodelete-a-container"></a><span data-ttu-id="79881-175">toodelete un conteneur</span><span class="sxs-lookup"><span data-stu-id="79881-175">toodelete a container</span></span>
<span data-ttu-id="79881-176">Vous êtes facturé pour le stockage, il est souhaitable toodelete le **mise en route** conteneur une fois que vous avez terminé expérimenter de cet exemple.</span><span class="sxs-lookup"><span data-stu-id="79881-176">Because you are charged for storage, you may want toodelete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="79881-177">toodelete un conteneur, utilisez hello **CloudBlobContainer.delete** (méthode).</span><span class="sxs-lookup"><span data-stu-id="79881-177">toodelete a container, use hello **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="79881-178">toocall hello **CloudBlobContainer.delete** (méthode), le processus hello d’initialisation **CloudStorageAccount**, **ClodBlobClient**, et  **CloudBlobContainer** objets est hello identique à celui décrit pour le **createIfNotExist** (méthode).</span><span class="sxs-lookup"><span data-stu-id="79881-178">toocall hello **CloudBlobContainer.delete** method, hello process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is hello same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="79881-179">Hello Voici un exemple complet que les suppressions hello conteneur nommé **mise en route**.</span><span class="sxs-lookup"><span data-stu-id="79881-179">hello following is a complete example that deletes hello container named **gettingstarted**.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;

public class DeleteContainer {

    public static final String storageConnectionString =
            "DefaultEndpointsProtocol=http;" +
                "AccountName=your_account_name;" +
                "AccountKey=your_account_key";

    public static void main(String[] args)
    {
        try
        {
            CloudStorageAccount account;
            CloudBlobClient serviceClient;
            CloudBlobContainer container;

            account = CloudStorageAccount.parse(storageConnectionString);
            serviceClient = account.createCloudBlobClient();
            // Container name must be lower case.
            container = serviceClient.getContainerReference("gettingstarted");
            container.delete();

            System.out.println("Container deleted.");

        }
        catch (StorageException storageException)
        {
            System.out.print("StorageException encountered: ");
            System.out.println(storageException.getMessage());
            System.exit(-1);
        }
        catch (Exception e)
        {
            System.out.print("Exception encountered: ");
            System.out.println(e.getMessage());
            System.exit(-1);
        }
    }
}
```

<span data-ttu-id="79881-180">Pour une vue d’ensemble des autres classes de stockage d’objets blob et les méthodes, consultez [comment toouse stockage d’objets Blob à partir de Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="79881-180">For an overview of other blob storage classes and methods, see [How toouse Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="79881-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="79881-181">Next steps</span></span>
<span data-ttu-id="79881-182">Suivez ces liens de toolearn plus d’informations sur les tâches de stockage plus complexes.</span><span class="sxs-lookup"><span data-stu-id="79881-182">Follow these links toolearn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="79881-183">Kit de développement logiciel (SDK) Azure Storage pour Java</span><span class="sxs-lookup"><span data-stu-id="79881-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="79881-184">Référence du Kit de développement logiciel (SDK) du client Azure Storage</span><span class="sxs-lookup"><span data-stu-id="79881-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="79881-185">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="79881-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="79881-186">Blog de l'équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="79881-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

