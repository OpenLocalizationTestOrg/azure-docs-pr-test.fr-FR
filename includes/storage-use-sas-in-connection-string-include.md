<span data-ttu-id="045b7-101">Si vous possédez une URL de signature (SAP) d’accès partagé qui vous permet de qu'accéder tooresources dans un compte de stockage, vous pouvez utiliser hello SAP dans une chaîne de connexion.</span><span class="sxs-lookup"><span data-stu-id="045b7-101">If you possess a shared access signature (SAS) URL that grants you access tooresources in a storage account, you can use hello SAS in a connection string.</span></span> <span data-ttu-id="045b7-102">Hello SAS contenant la demande d’hello hello information tooauthenticate requis, une chaîne de connexion avec une SAP fournit hello protocole, du point de terminaison de service hello et ressources de hello tooaccess hello informations d’identification nécessaires.</span><span class="sxs-lookup"><span data-stu-id="045b7-102">Because hello SAS contains hello information required tooauthenticate hello request, a connection string with a SAS provides hello protocol, hello service endpoint, and hello necessary credentials tooaccess hello resource.</span></span>

<span data-ttu-id="045b7-103">toocreate une chaîne de connexion qui inclut une signature d’accès partagé, spécifiez les chaîne hello Bonjour suivant le format :</span><span class="sxs-lookup"><span data-stu-id="045b7-103">toocreate a connection string that includes a shared access signature, specify hello string in hello following format:</span></span>

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

<span data-ttu-id="045b7-104">Chaque point de terminaison de service est facultative, bien que la chaîne de connexion hello doit contenir au moins un.</span><span class="sxs-lookup"><span data-stu-id="045b7-104">Each service endpoint is optional, although hello connection string must contain at least one.</span></span>

> [!NOTE]
> <span data-ttu-id="045b7-105">Il est recommandé d’utiliser le protocole HTTPS avec une SAS.</span><span class="sxs-lookup"><span data-stu-id="045b7-105">Using HTTPS with a SAS is recommended as a best practice.</span></span>
>
> <span data-ttu-id="045b7-106">Si vous spécifiez un SAS dans une chaîne de connexion dans un fichier de configuration, vous devrez peut-être tooencode des caractères spéciaux dans les URL hello.</span><span class="sxs-lookup"><span data-stu-id="045b7-106">If you are specifying a SAS in a connection string in a configuration file, you may need tooencode special characters in hello URL.</span></span>
>
>

### <a name="service-sas-example"></a><span data-ttu-id="045b7-107">Exemple de SAP de service</span><span class="sxs-lookup"><span data-stu-id="045b7-107">Service SAS example</span></span>
<span data-ttu-id="045b7-108">Voici un exemple de chaîne de connexion incluant la SAS d’un service pour Blob Storage :</span><span class="sxs-lookup"><span data-stu-id="045b7-108">Here's an example of a connection string that includes a service SAS for Blob storage:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

<span data-ttu-id="045b7-109">Voici un exemple Hello même chaîne de connexion avec l’encodage de caractères spéciaux :</span><span class="sxs-lookup"><span data-stu-id="045b7-109">And here's an example of hello same connection string with encoding of special characters:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a><span data-ttu-id="045b7-110">Exemple de SAP de compte</span><span class="sxs-lookup"><span data-stu-id="045b7-110">Account SAS example</span></span>
<span data-ttu-id="045b7-111">Voici un exemple de chaîne de connexion incluant la SAS d’un compte pour Blob Storage et File Storage.</span><span class="sxs-lookup"><span data-stu-id="045b7-111">Here's an example of a connection string that includes an account SAS for Blob and File storage.</span></span> <span data-ttu-id="045b7-112">Notez que les points de terminaison des deux services sont spécifiés :</span><span class="sxs-lookup"><span data-stu-id="045b7-112">Note that endpoints for both services are specified:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

<span data-ttu-id="045b7-113">Voici un exemple Hello même chaîne de connexion avec l’encodage d’URL :</span><span class="sxs-lookup"><span data-stu-id="045b7-113">And here's an example of hello same connection string with URL encoding:</span></span>

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

