---
title: "Application locale avec stockage d’objets blob (Java) | Microsoft Docs"
description: "Découvrez comment créer une application console qui charge une image dans Azure, puis l'affiche dans votre navigateur. Les exemples de code sont écrits en Java."
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
ms.openlocfilehash: a172b881fa38a69f4510df94f5797b7a56940c52
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: fr-FR
ms.lasthandoff: 07/11/2017
---
# <a name="on-premises-application-with-blob-storage"></a><span data-ttu-id="cea04-104">Application locale avec stockage d’objets blob</span><span class="sxs-lookup"><span data-stu-id="cea04-104">On-premises application with blob storage</span></span>
## <a name="overview"></a><span data-ttu-id="cea04-105">Vue d'ensemble</span><span class="sxs-lookup"><span data-stu-id="cea04-105">Overview</span></span>
<span data-ttu-id="cea04-106">L'exemple suivant montre comment utiliser le stockage Azure pour stocker des images dans Azure.</span><span class="sxs-lookup"><span data-stu-id="cea04-106">The following example shows you how you can use Azure storage to store images in Azure.</span></span> <span data-ttu-id="cea04-107">Le code figurant dans cet article concerne une application de console qui charge une image dans Azure, puis crée un fichier HTML affichant cette image dans votre navigateur.</span><span class="sxs-lookup"><span data-stu-id="cea04-107">The code in this article is for a console application that uploads an image to Azure, and then creates an HTML file that displays the image in your browser.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cea04-108">Composants requis</span><span class="sxs-lookup"><span data-stu-id="cea04-108">Prerequisites</span></span>
* <span data-ttu-id="cea04-109">Le Kit de développement logiciel Java (JDK) version 1.6 ou ultérieure est installé.</span><span class="sxs-lookup"><span data-stu-id="cea04-109">A Java Developer Kit (JDK), version 1.6 or later, is installed.</span></span>
* <span data-ttu-id="cea04-110">Le Kit de développement logiciel (SDK) Azure est installé.</span><span class="sxs-lookup"><span data-stu-id="cea04-110">The Azure SDK is installed.</span></span>
* <span data-ttu-id="cea04-111">L'archive Java (JAR) des bibliothèques Azure pour Java et les dépendances applicables JAR sont installées et se trouvent dans le chemin d'accès de build utilisé par votre compilateur Java.</span><span class="sxs-lookup"><span data-stu-id="cea04-111">The JAR for the Azure Libraries for Java, and any applicable dependency JARs, are installed and are in the build path used by your Java compiler.</span></span> <span data-ttu-id="cea04-112">Pour plus d’informations sur l’installation des bibliothèques Azure pour Java, consultez la page [Téléchargement du Kit de développement logiciel (SDK) Azure pour Java](../java-download-azure-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="cea04-112">For information about installing the Azure Libraries for Java, see [Download the Azure SDK for Java](../java-download-azure-sdk.md).</span></span>
* <span data-ttu-id="cea04-113">Un compte de stockage Azure a été configuré.</span><span class="sxs-lookup"><span data-stu-id="cea04-113">An Azure storage account has been set up.</span></span> <span data-ttu-id="cea04-114">Le nom et la clé du compte de stockage sont utilisés par le code figurant dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cea04-114">The account name and account key for the storage account will be used by the code in this article.</span></span> <span data-ttu-id="cea04-115">Consultez la page [Création d’un compte de stockage](storage-create-storage-account.md#create-a-storage-account) pour des informations sur la création d’un compte de stockage et la page [Afficher et copier les clés d’accès de stockage](storage-create-storage-account.md#view-and-copy-storage-access-keys) pour des informations sur la récupération de la clé de compte.</span><span class="sxs-lookup"><span data-stu-id="cea04-115">See [How to Create a Storage Account](storage-create-storage-account.md#create-a-storage-account) for information about creating a storage account, and [View and copy storage access keys](storage-create-storage-account.md#view-and-copy-storage-access-keys) for information about retrieving the account key.</span></span>
* <span data-ttu-id="cea04-116">Vous avez créé un fichier image local nommé et stocké sous le chemin d’accès c:\\myimages\\image1.jpg.</span><span class="sxs-lookup"><span data-stu-id="cea04-116">You have created a local image file named stored at the path c:\\myimages\\image1.jpg.</span></span> <span data-ttu-id="cea04-117">Vous pouvez également modifier le constructeur **FileInputStream** dans l’exemple pour utiliser un chemin d’accès à l’image et un nom de fichier différents.</span><span class="sxs-lookup"><span data-stu-id="cea04-117">Alternatively, modify the **FileInputStream** constructor in the example to use a different image path and file name.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="to-use-azure-blob-storage-to-upload-a-file"></a><span data-ttu-id="cea04-118">Utilisation du stockage d’objets blob Azure pour charger un fichier</span><span class="sxs-lookup"><span data-stu-id="cea04-118">To use Azure blob storage to upload a file</span></span>
<span data-ttu-id="cea04-119">La procédure présentée ici détaille chaque étape.</span><span class="sxs-lookup"><span data-stu-id="cea04-119">A step-by-step procedure is presented here.</span></span> <span data-ttu-id="cea04-120">Si vous souhaitez la passer, le code est intégralement présenté plus avant dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cea04-120">If you'd like to skip ahead, the entire code is presented later in this article.</span></span>

<span data-ttu-id="cea04-121">Commencez le code en important les classes de stockage de base Azure, les classes du client d’objets blob Azure, les classes d’E/S Java et la classe **URISyntaxException** :</span><span class="sxs-lookup"><span data-stu-id="cea04-121">Begin the code by including imports for the Azure core storage classes, the Azure blob client classes, the Java IO classes, and the **URISyntaxException** class.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;
```

<span data-ttu-id="cea04-122">Déclarez une classe nommée **StorageSample**, puis incluez le crochet ouvrant **{**.</span><span class="sxs-lookup"><span data-stu-id="cea04-122">Declare a class named **StorageSample**, and include the open bracket, **{**.</span></span>

```java
public class StorageSample {
```

<span data-ttu-id="cea04-123">Dans la classe **StorageSample** , déclarez une variable de chaîne qui contient le protocole du point de terminaison par défaut, le nom de votre compte de stockage et votre clé d'accès de stockage, comme spécifié dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cea04-123">Within the **StorageSample** class, declare a string variable that will contain the default endpoint protocol, your storage account name, and your storage access key, as specified in your Azure storage account.</span></span> <span data-ttu-id="cea04-124">Remplacez les valeurs des espaces réservés **your\_account\_name** et **your\_account\_key** par respectivement votre nom et votre clé de compte.</span><span class="sxs-lookup"><span data-stu-id="cea04-124">Replace the placeholder values **your\_account\_name** and **your\_account\_key** with your own account name and account key, respectively.</span></span>

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_account_name;" +
    "AccountKey=your_account_name";
```

<span data-ttu-id="cea04-125">Ajoutez votre déclaration pour **main**, incluez un bloc **try** ainsi que les crochets ouvrants nécessaires **{**.</span><span class="sxs-lookup"><span data-stu-id="cea04-125">Add in your declaration for **main**, include a **try** block, and include the necessary open brackets, **{**.</span></span>

```java
    public static void main(String[] args)
    {
        try
        {
```

<span data-ttu-id="cea04-126">Déclarez les variables du type suivant (les descriptions se rapportent à la façon dont elles sont utilisées dans cet exemple) :</span><span class="sxs-lookup"><span data-stu-id="cea04-126">Declare variables of the following type (the descriptions are for how they are used in this example):</span></span>

* <span data-ttu-id="cea04-127">**CloudStorageAccount**: permet d’initialiser le compte avec le nom et la clé de votre compte de stockage Azure, et de créer l’objet client du blob.</span><span class="sxs-lookup"><span data-stu-id="cea04-127">**CloudStorageAccount**: Used to initialize the account object with your Azure storage account name and key, and to create the blob client object.</span></span>
* <span data-ttu-id="cea04-128">**CloudBlobClient**: permet d’accéder au service BLOB.</span><span class="sxs-lookup"><span data-stu-id="cea04-128">**CloudBlobClient**: Used to access the blob service.</span></span>
* <span data-ttu-id="cea04-129">**CloudBlobContainer**: permet de créer un conteneur d’objets blob, de répertorier les objets blob dans le conteneur et de supprimer ce dernier.</span><span class="sxs-lookup"><span data-stu-id="cea04-129">**CloudBlobContainer**: Used to create a blob container, list the blobs in the container, and delete the container.</span></span>
* <span data-ttu-id="cea04-130">**CloudBlockBlob**: permet de charger un fichier image local dans le conteneur.</span><span class="sxs-lookup"><span data-stu-id="cea04-130">**CloudBlockBlob**: Used to upload a local image file to the container.</span></span>

<!-- -->

```java
    CloudStorageAccount account;
    CloudBlobClient serviceClient;
    CloudBlobContainer container;
    CloudBlockBlob blob;
```

<span data-ttu-id="cea04-131">Attribuez une valeur à la variable **account** .</span><span class="sxs-lookup"><span data-stu-id="cea04-131">Assign a value to the **account** variable.</span></span>

```java
account = CloudStorageAccount.parse(storageConnectionString);
```

<span data-ttu-id="cea04-132">Attribuez une valeur à la variable **serviceClient** .</span><span class="sxs-lookup"><span data-stu-id="cea04-132">Assign a value to the **serviceClient** variable.</span></span>

```java
serviceClient = account.createCloudBlobClient();
```

<span data-ttu-id="cea04-133">Attribuez une valeur à la variable **container** .</span><span class="sxs-lookup"><span data-stu-id="cea04-133">Assign a value to the **container** variable.</span></span> <span data-ttu-id="cea04-134">Nous obtenons une référence pointant vers un conteneur nommé **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="cea04-134">We'll get a reference to a container named **gettingstarted**.</span></span>

```java
// Container name must be lower case.
container = serviceClient.getContainerReference("gettingstarted");
```

<span data-ttu-id="cea04-135">Création du conteneur.</span><span class="sxs-lookup"><span data-stu-id="cea04-135">Create the container.</span></span> <span data-ttu-id="cea04-136">Cette méthode crée le conteneur s’il n’existe pas (et renvoie **true**).</span><span class="sxs-lookup"><span data-stu-id="cea04-136">This method will create the container if it doesn't exist (and return **true**).</span></span> <span data-ttu-id="cea04-137">Si le conteneur existe, elle renvoie **false**.</span><span class="sxs-lookup"><span data-stu-id="cea04-137">If the container does exist, it will return **false**.</span></span> <span data-ttu-id="cea04-138">La méthode **create** (qui renvoie une erreur si le conteneur existe déjà) constitue une alternative à **createIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="cea04-138">An alternative to **createIfNotExists** is the **create** method (which will return an error if the container already exists).</span></span>

```java
container.createIfNotExists();
```

<span data-ttu-id="cea04-139">Définissez un accès anonyme pour le conteneur.</span><span class="sxs-lookup"><span data-stu-id="cea04-139">Set anonymous access for the container.</span></span>

```java
// Set anonymous access on the container.
BlobContainerPermissions containerPermissions;
containerPermissions = new BlobContainerPermissions();
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
container.uploadPermissions(containerPermissions);
```

<span data-ttu-id="cea04-140">Obtenez une référence pointant vers l'objet blob de blocs qui représente l'objet blob dans le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cea04-140">Get a reference to the block blob, which will represent the blob in Azure storage.</span></span>

```java
blob = container.getBlockBlobReference("image1.jpg");
```

<span data-ttu-id="cea04-141">Utilisez le constructeur **File** pour obtenir une référence pointant vers le fichier créé en local que vous allez charger.</span><span class="sxs-lookup"><span data-stu-id="cea04-141">Use the **File** constructor to get a reference to the locally created file that you will upload.</span></span> <span data-ttu-id="cea04-142">Assurez-vous d’avoir créé ce fichier avant d’exécuter le code.</span><span class="sxs-lookup"><span data-stu-id="cea04-142">Ensure you have created this file before running the code.</span></span>

```java
File fileReference = new File ("c:\\myimages\\image1.jpg");
```

<span data-ttu-id="cea04-143">Chargez le fichier local en appelant la méthode **CloudBlockBlob.upload** .</span><span class="sxs-lookup"><span data-stu-id="cea04-143">Upload the local file through a call to the **CloudBlockBlob.upload** method.</span></span> <span data-ttu-id="cea04-144">Le premier paramètre de la méthode **CloudBlockBlob.upload** est un objet **FileInputStream** qui représente le fichier local à charger sur le stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cea04-144">The first parameter to the **CloudBlockBlob.upload** method is a **FileInputStream** object that represents the local file that will be uploaded to Azure storage.</span></span> <span data-ttu-id="cea04-145">Le deuxième paramètre est la taille du fichier en octets.</span><span class="sxs-lookup"><span data-stu-id="cea04-145">The second parameter is the size, in bytes, of the file.</span></span>

```java
blob.upload(new FileInputStream(fileReference), fileReference.length());
```

<span data-ttu-id="cea04-146">Appelez une fonction d’assistance nommée **MakeHTMLPage** pour créer une page HTML de base contenant un élément **&lt;image&gt;** dont la source est définie sur l’objet blob qui est désormais dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cea04-146">Call a helper function named **MakeHTMLPage**, to make a basic HTML page that contains an **&lt;image&gt;** element with the source set to the blob that is now in your Azure storage account.</span></span> <span data-ttu-id="cea04-147">Le code de **MakeHTMLPage** est abordé plus avant dans cet article.</span><span class="sxs-lookup"><span data-stu-id="cea04-147">The code for **MakeHTMLPage** will be discussed later in this article.</span></span>

```java
MakeHTMLPage(container);
```

<span data-ttu-id="cea04-148">Imprimez un message d'état et des informations sur la page HTML créée.</span><span class="sxs-lookup"><span data-stu-id="cea04-148">Print out a status message and information about the created HTML page.</span></span>

```java
System.out.println("Processing complete.");
System.out.println("Open index.html to see the images stored in your storage account.");
```

<span data-ttu-id="cea04-149">Fermez le bloc **try** en insérant une parenthèse fermante : **}**</span><span class="sxs-lookup"><span data-stu-id="cea04-149">Close the **try** block by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cea04-150">Gérez les exceptions suivantes :</span><span class="sxs-lookup"><span data-stu-id="cea04-150">Handle the following exceptions:</span></span>

* <span data-ttu-id="cea04-151">**FileNotFoundException** : peut être émise par les constructeurs **FileInputStream** et **FileOutputStream**.</span><span class="sxs-lookup"><span data-stu-id="cea04-151">**FileNotFoundException**: Can be thrown by the **FileInputStream** or **FileOutputStream** constructors.</span></span>
* <span data-ttu-id="cea04-152">**StorageException**: peut être émise par la bibliothèque de stockage cliente Azure.</span><span class="sxs-lookup"><span data-stu-id="cea04-152">**StorageException**: Can be thrown by the Azure client storage library.</span></span>
* <span data-ttu-id="cea04-153">**URISyntaxException** : peut être émise par la méthode **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="cea04-153">**URISyntaxException**: Can be thrown by the **ListBlobItem.getUri** method.</span></span>
* <span data-ttu-id="cea04-154">**Exception**: traitement d’une exception générique.</span><span class="sxs-lookup"><span data-stu-id="cea04-154">**Exception**: Generic exception handling.</span></span>

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

<span data-ttu-id="cea04-155">Fermez **main** en insérant une parenthèse fermante : **}**</span><span class="sxs-lookup"><span data-stu-id="cea04-155">Close **main** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cea04-156">Pour créer une page HTML de base, créez une méthode nommée **MakeHTMLPage** .</span><span class="sxs-lookup"><span data-stu-id="cea04-156">Create a method named **MakeHTMLPage** to create a basic HTML page.</span></span> <span data-ttu-id="cea04-157">Cette méthode dispose d'un paramètre du type **CloudBlobContainer**qui est utilisé pour effectuer une itération dans la liste des objets blob chargés.</span><span class="sxs-lookup"><span data-stu-id="cea04-157">This method has a parameter of type **CloudBlobContainer**, which will be used to iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="cea04-158">Cette méthode lève des exceptions du type **FileNotFoundException** pouvant être levées par le constructeur **FileOutputStream** et du type **URISyntaxException** pouvant être levées par la méthode **ListBlobItem.getUri**.</span><span class="sxs-lookup"><span data-stu-id="cea04-158">This method will throw exceptions of type **FileNotFoundException**, which can be thrown by the **FileOutputStream** constructor, and **URISyntaxException**, which can be thrown by the **ListBlobItem.getUri** method.</span></span> <span data-ttu-id="cea04-159">Incluez le crochet ouvrant **{**.</span><span class="sxs-lookup"><span data-stu-id="cea04-159">Include the opening bracket, **{**.</span></span>

```java
public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
{
```

<span data-ttu-id="cea04-160">Créez un fichier local nommé **index.html**.</span><span class="sxs-lookup"><span data-stu-id="cea04-160">Create a local file named **index.html**.</span></span>

```java
PrintStream stream;
stream = new PrintStream(new FileOutputStream("index.html"));
```

<span data-ttu-id="cea04-161">Écrivez dans le fichier local en y ajoutant les éléments **&lt;html&gt;**, **&lt;header&gt;** et **&lt;body&gt;**.</span><span class="sxs-lookup"><span data-stu-id="cea04-161">Write to the local file, adding in the **&lt;html&gt;**, **&lt;header&gt;**, and **&lt;body&gt;** elements.</span></span>

```java
stream.println("<html>");
stream.println("<header/>");
stream.println("<body>");
```

<span data-ttu-id="cea04-162">Effectuez une itération dans la liste des objets blob chargés.</span><span class="sxs-lookup"><span data-stu-id="cea04-162">Iterate through the list of uploaded blobs.</span></span> <span data-ttu-id="cea04-163">Pour chaque objet blob, créez dans la page HTML un élément **&lt;img&gt;** dont l’attribut **src** est envoyé à l’URI de l’objet blob tel qu’il existe dans votre compte de stockage Azure.</span><span class="sxs-lookup"><span data-stu-id="cea04-163">For each blob, in the HTML page create an **&lt;img&gt;** element that has its **src** attribute sent to the URI of the blob as it exists in your Azure storage account.</span></span>
<span data-ttu-id="cea04-164">Dans cet exemple, vous avez ajouté une seule image, mais si vous en ajoutiez plus, ce code effectuerait une itération pour chacune d'entre elles.</span><span class="sxs-lookup"><span data-stu-id="cea04-164">Although you added only one image in this sample, if you added more, this code would iterate all of them.</span></span>

<span data-ttu-id="cea04-165">Par souci de simplification, cet exemple part du principe que chaque objet blob chargé est une image.</span><span class="sxs-lookup"><span data-stu-id="cea04-165">For simplicity, this example assumes each uploaded blob is an image.</span></span> <span data-ttu-id="cea04-166">Si vous avez chargé des objets blob qui ne sont pas des images ou des objets blob de pages au lieu d'objets blob de blocs, modifiez le code en conséquence.</span><span class="sxs-lookup"><span data-stu-id="cea04-166">If you've updated blobs other than images, or page blobs instead of block blobs, adjust the code as needed.</span></span>

```java
// Enumerate the uploaded blobs.
for (ListBlobItem blobItem : container.listBlobs()) {
// List each blob as an <img> element in the HTML body.
stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
}
```

<span data-ttu-id="cea04-167">Fermez les éléments **&lt;body&gt;** et **&lt;html&gt;**.</span><span class="sxs-lookup"><span data-stu-id="cea04-167">Close the **&lt;body&gt;** element and the **&lt;html&gt;** element.</span></span>

```java
stream.println("</body>");
stream.println("</html>");
```

<span data-ttu-id="cea04-168">Fermez le fichier local.</span><span class="sxs-lookup"><span data-stu-id="cea04-168">Close the local file.</span></span>

```java
stream.close();
```

<span data-ttu-id="cea04-169">Fermez **MakeHTMLPage** en insérant une parenthèse fermante : **}**</span><span class="sxs-lookup"><span data-stu-id="cea04-169">Close **MakeHTMLPage** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cea04-170">Fermez **StorageSample** en insérant une parenthèse fermante : **}**</span><span class="sxs-lookup"><span data-stu-id="cea04-170">Close **StorageSample** by inserting a close bracket: **}**</span></span>

<span data-ttu-id="cea04-171">Voici le code complet pour cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cea04-171">The following is the complete code for this example.</span></span> <span data-ttu-id="cea04-172">N’oubliez pas de modifier les valeurs des espaces réservés **your\_account\_name** et **your\_account\_key** pour utiliser respectivement votre nom et votre clé de compte.</span><span class="sxs-lookup"><span data-stu-id="cea04-172">Remember to modify the placeholder values **your\_account\_name** and **your\_account\_key** to use your account name and account key, respectively.</span></span>

```java
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
import java.io.*;
import java.net.URISyntaxException;

// Create an image, c:\myimages\image1.jpg, prior to running this sample.
// Alternatively, change the value used by the FileInputStream constructor
// to use a different image path and file that you have already created.
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

            // Set anonymous access on the container.
            BlobContainerPermissions containerPermissions;
            containerPermissions = new BlobContainerPermissions();
            containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);
            container.uploadPermissions(containerPermissions);

            // Upload an image file.
            blob = container.getBlockBlobReference("image1.jpg");

            File fileReference = new File("c:\\myimages\\image1.jpg");
            blob.upload(new FileInputStream(fileReference), fileReference.length());

            // At this point the image is uploaded.
            // Next, create an HTML page that lists all of the uploaded images.
            MakeHTMLPage(container);

            System.out.println("Processing complete.");
            System.out.println("Open index.html to see the images stored in your storage account.");

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

    // Create an HTML page that can be used to display the uploaded images.
    // This example assumes all of the blobs are for images.
    public static void MakeHTMLPage(CloudBlobContainer container) throws FileNotFoundException, URISyntaxException
    {
        PrintStream stream;
        stream = new PrintStream(new FileOutputStream("index.html"));

        // Create the opening <html>, <header>, and <body> elements.
        stream.println("<html>");
        stream.println("<header/>");
        stream.println("<body>");

        // Enumerate the uploaded blobs.
        for (ListBlobItem blobItem : container.listBlobs()) {
            // List each blob as an <img> element in the HTML body.
            stream.println("<img src='" + blobItem.getUri() + "'/><br/>");
        }

        stream.println("</body>");

        // Complete the <html> element and close the file.
        stream.println("</html>");
        stream.close();
    }
}
```

<span data-ttu-id="cea04-173">En plus de charger votre fichier image local dans le stockage Azure, l’exemple de code crée un fichier local nommé index.html que vous pouvez ouvrir dans votre navigateur pour voir votre image chargée.</span><span class="sxs-lookup"><span data-stu-id="cea04-173">In addition to uploading your local image file to Azure storage, the example code creates a local file namedindex.html, which you can open in your browser to see your uploaded image.</span></span>

<span data-ttu-id="cea04-174">Comme le code contient votre nom et votre clé de compte, veillez à la sécurité de votre code source.</span><span class="sxs-lookup"><span data-stu-id="cea04-174">Because the code contains your account name and account key, ensure that your source code is secure.</span></span>

## <a name="to-delete-a-container"></a><span data-ttu-id="cea04-175">Suppression d'un conteneur</span><span class="sxs-lookup"><span data-stu-id="cea04-175">To delete a container</span></span>
<span data-ttu-id="cea04-176">Étant donné que le stockage vous est facturé, vous pouvez supprimer le conteneur **gettingstarted** une fois que vous avez fini d'utiliser cet exemple.</span><span class="sxs-lookup"><span data-stu-id="cea04-176">Because you are charged for storage, you may want to delete the **gettingstarted** container after you are done experimenting with this example.</span></span> <span data-ttu-id="cea04-177">Pour supprimer un conteneur, utilisez la méthode **CloudBlobContainer.delete** .</span><span class="sxs-lookup"><span data-stu-id="cea04-177">To delete a container, use the **CloudBlobContainer.delete** method.</span></span>

```java
container = serviceClient.getContainerReference("gettingstarted");
container.delete();
```

<span data-ttu-id="cea04-178">Pour appeler la méthode **CloudBlobContainer.delete**, le processus d’initialisation des objets **CloudStorageAccount**, **ClodBlobClient** et **CloudBlobContainer** est le même que celui de la méthode **createIfNotExist**.</span><span class="sxs-lookup"><span data-stu-id="cea04-178">To call the **CloudBlobContainer.delete** method, the process of initializing **CloudStorageAccount**, **ClodBlobClient**, and **CloudBlobContainer** objects is the same as shown for the **createIfNotExist** method.</span></span> <span data-ttu-id="cea04-179">Voici un exemple complet permettant de supprimer le conteneur nommé **gettingstarted**.</span><span class="sxs-lookup"><span data-stu-id="cea04-179">The following is a complete example that deletes the container named **gettingstarted**.</span></span>

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

<span data-ttu-id="cea04-180">Pour une présentation d’autres classes et méthodes de stockage d’objets blob, consultez la page [Utilisation du stockage d’objets blob à partir de Java](storage-java-how-to-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="cea04-180">For an overview of other blob storage classes and methods, see [How to use Blob storage from Java](storage-java-how-to-use-blob-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="cea04-181">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="cea04-181">Next steps</span></span>
<span data-ttu-id="cea04-182">Pour en savoir plus sur les tâches de stockage plus complexes, cliquez sur les liens ci-dessous.</span><span class="sxs-lookup"><span data-stu-id="cea04-182">Follow these links to learn more about more complex storage tasks.</span></span>

* [<span data-ttu-id="cea04-183">Kit de développement logiciel (SDK) Azure Storage pour Java</span><span class="sxs-lookup"><span data-stu-id="cea04-183">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="cea04-184">Référence du Kit de développement logiciel (SDK) du client Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cea04-184">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="cea04-185">API REST des services d’Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cea04-185">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="cea04-186">Blog de l'équipe Azure Storage</span><span class="sxs-lookup"><span data-stu-id="cea04-186">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)

