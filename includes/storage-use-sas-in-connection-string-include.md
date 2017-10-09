Si vous possédez une URL de signature (SAP) d’accès partagé qui vous permet de qu'accéder tooresources dans un compte de stockage, vous pouvez utiliser hello SAP dans une chaîne de connexion. Hello SAS contenant la demande d’hello hello information tooauthenticate requis, une chaîne de connexion avec une SAP fournit hello protocole, du point de terminaison de service hello et ressources de hello tooaccess hello informations d’identification nécessaires.

toocreate une chaîne de connexion qui inclut une signature d’accès partagé, spécifiez les chaîne hello Bonjour suivant le format :

```
BlobEndpoint=myBlobEndpoint;
QueueEndpoint=myQueueEndpoint;
TableEndpoint=myTableEndpoint;
FileEndpoint=myFileEndpoint;
SharedAccessSignature=sasToken
```

Chaque point de terminaison de service est facultative, bien que la chaîne de connexion hello doit contenir au moins un.

> [!NOTE]
> Il est recommandé d’utiliser le protocole HTTPS avec une SAS.
>
> Si vous spécifiez un SAS dans une chaîne de connexion dans un fichier de configuration, vous devrez peut-être tooencode des caractères spéciaux dans les URL hello.
>
>

### <a name="service-sas-example"></a>Exemple de SAP de service
Voici un exemple de chaîne de connexion incluant la SAS d’un service pour Blob Storage :

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&sr=b&si=tutorial-policy-635959936145100803&sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

Voici un exemple Hello même chaîne de connexion avec l’encodage de caractères spéciaux :

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
SharedAccessSignature=sv=2015-04-05&amp;sr=b&amp;si=tutorial-policy-635959936145100803&amp;sig=9aCzs76n0E7y5BpEi2GvsSv433BZa22leDOZXX%2BXXIU%3D
```

### <a name="account-sas-example"></a>Exemple de SAP de compte
Voici un exemple de chaîne de connexion incluant la SAS d’un compte pour Blob Storage et File Storage. Notez que les points de terminaison des deux services sont spécifiés :

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&spr=https&st=2016-04-12T03%3A24%3A31Z&se=2016-04-13T03%3A29%3A31Z&srt=s&ss=bf&sp=rwl
```

Voici un exemple Hello même chaîne de connexion avec l’encodage d’URL :

```
BlobEndpoint=https://storagesample.blob.core.windows.net;
FileEndpoint=https://storagesample.file.core.windows.net;
SharedAccessSignature=sv=2015-07-08&amp;sig=iCvQmdZngZNW%2F4vw43j6%2BVz6fndHF5LI639QJba4r8o%3D&amp;spr=https&amp;st=2016-04-12T03%3A24%3A31Z&amp;se=2016-04-13T03%3A29%3A31Z&amp;srt=s&amp;ss=bf&amp;sp=rwl
```

