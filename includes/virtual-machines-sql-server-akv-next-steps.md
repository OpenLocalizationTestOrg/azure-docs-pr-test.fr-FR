## <a name="next-steps"></a><span data-ttu-id="4a1d2-101">Étapes suivantes</span><span class="sxs-lookup"><span data-stu-id="4a1d2-101">Next steps</span></span>

<span data-ttu-id="4a1d2-102">Après avoir activé Azure Key Vault Integration, vous pouvez activer le chiffrement SQL Server sur votre machine virtuelle SQL.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-102">After enabling Azure Key Vault Integration, you can enable SQL Server encryption on your SQL VM.</span></span> <span data-ttu-id="4a1d2-103">Tout d’abord, vous devez toocreate une clé asymétrique à l’intérieur de votre coffre de clés et une clé symétrique dans SQL Server sur votre machine virtuelle.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-103">First, you will need toocreate an asymmetric key inside your key vault and a symmetric key within SQL Server on your VM.</span></span> <span data-ttu-id="4a1d2-104">Ensuite, vous serez cryptage de tooenable instructions tooexecute en mesure de T-SQL pour vos bases de données et les sauvegardes.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-104">Then, you will be able tooexecute T-SQL statements tooenable encryption for your databases and backups.</span></span>

<span data-ttu-id="4a1d2-105">Il existe plusieurs types de chiffrement que vous pouvez exploiter :</span><span class="sxs-lookup"><span data-stu-id="4a1d2-105">There are several forms of encryption you can take advantage of:</span></span>

* [<span data-ttu-id="4a1d2-106">Chiffrement transparent des données (TDE)</span><span class="sxs-lookup"><span data-stu-id="4a1d2-106">Transparent Data Encryption (TDE)</span></span>](https://msdn.microsoft.com/library/bb934049.aspx)
* [<span data-ttu-id="4a1d2-107">Sauvegardes chiffrées</span><span class="sxs-lookup"><span data-stu-id="4a1d2-107">Encrypted backups</span></span>](https://msdn.microsoft.com/library/dn449489.aspx)
* [<span data-ttu-id="4a1d2-108">Chiffrement au niveau des colonnes (CLE)</span><span class="sxs-lookup"><span data-stu-id="4a1d2-108">Column Level Encryption (CLE)</span></span>](https://msdn.microsoft.com/library/ms173744.aspx)

<span data-ttu-id="4a1d2-109">Hello des scripts Transact-SQL suivantes fournissent des exemples pour chacun de ces domaines.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-109">hello following Transact-SQL scripts provide examples for each of these areas.</span></span>

### <a name="prerequisites-for-examples"></a><span data-ttu-id="4a1d2-110">Configuration requise pour les exemples</span><span class="sxs-lookup"><span data-stu-id="4a1d2-110">Prerequisites for examples</span></span>

<span data-ttu-id="4a1d2-111">Chaque exemple est basé sur la configuration requise de hello deux : une clé asymétrique à partir de votre coffre de clés appelé **CONTOSO_KEY** et les informations d’identification créé par la fonctionnalité d’intégration de AKV hello appelée **Azure_EKM_TDE_cred**.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-111">Each example is based on hello two prerequisites: an asymmetric key from your key vault called **CONTOSO_KEY** and a credential created by hello AKV Integration feature called **Azure_EKM_TDE_cred**.</span></span> <span data-ttu-id="4a1d2-112">Hello commandes Transact-SQL suivantes d’installation ces conditions préalables pour exécuter les exemples hello.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-112">hello following Transact-SQL commands setup these prerequisites for running hello examples.</span></span>

``` sql
USE master;
GO

sp_configure [show advanced options], 1;
GO
RECONFIGURE;
GO

-- Enable EKM provider
sp_configure [EKM provider enabled], 1;
GO
RECONFIGURE;

--create provider
CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov
FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';
GO

--create credential
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--must have sysadmin
ALTER LOGIN [TDE_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'keytestvault',  --key name
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a><span data-ttu-id="4a1d2-113">Chiffrement transparent des données (TDE)</span><span class="sxs-lookup"><span data-stu-id="4a1d2-113">Transparent Data Encryption (TDE)</span></span>

1. <span data-ttu-id="4a1d2-114">Créer un toobe de connexion SQL Server utilisé par hello du moteur de base de données pour le chiffrement transparent des données, puis ajouter tooit des informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-114">Create a SQL Server login toobe used by hello Database Engine for TDE, then add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN TDE_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello TDE Login tooadd hello credential for use by the
   -- Database Engine tooaccess hello key vault
   ALTER LOGIN TDE_Login
   ADD CREDENTIAL Azure_EKM_TDE_cred;
   GO
   ```

1. <span data-ttu-id="4a1d2-115">Créer la clé de chiffrement de base de données hello qui sera utilisé pour le chiffrement transparent des données.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-115">Create hello database encryption key that will be used for TDE.</span></span>

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello database tooenable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a><span data-ttu-id="4a1d2-116">Sauvegardes chiffrées</span><span class="sxs-lookup"><span data-stu-id="4a1d2-116">Encrypted backups</span></span>

1. <span data-ttu-id="4a1d2-117">Créer un toobe de connexion SQL Server utilisé par hello du moteur de base de données pour le chiffrement des sauvegardes et ajoutez tooit des informations d’identification hello.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-117">Create a SQL Server login toobe used by hello Database Engine for encrypting backups, and add hello credential tooit.</span></span>

   ``` sql
   USE master;
   -- Create a SQL Server login associated with hello asymmetric key
   -- for hello Database engine toouse when it is encrypting hello backup.
   CREATE LOGIN Backup_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter hello Encrypted Backup Login tooadd hello credential for use by
   -- hello Database Engine tooaccess hello key vault
   ALTER LOGIN Backup_Login
   ADD CREDENTIAL Azure_EKM_Backup_cred ;
   GO
   ```

1. <span data-ttu-id="4a1d2-118">Base de données de sauvegarde hello en spécifiant le chiffrement à clé asymétrique de hello stockée dans le coffre de clés hello.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-118">Backup hello database specifying encryption with hello asymmetric key stored in hello key vault.</span></span>

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a><span data-ttu-id="4a1d2-119">Chiffrement au niveau des colonnes (CLE)</span><span class="sxs-lookup"><span data-stu-id="4a1d2-119">Column Level Encryption (CLE)</span></span>

<span data-ttu-id="4a1d2-120">Ce script crée une clé symétrique protégée par hello la clé asymétrique dans le coffre de clés hello et utilise ensuite les données de salutation tooencrypt clé symétrique dans la base de données hello.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-120">This script creates a symmetric key protected by hello asymmetric key in hello key vault, and then uses hello symmetric key tooencrypt data in hello database.</span></span>

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open hello symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data tooencrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close hello symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a><span data-ttu-id="4a1d2-121">Ressources supplémentaires</span><span class="sxs-lookup"><span data-stu-id="4a1d2-121">Additional resources</span></span>

<span data-ttu-id="4a1d2-122">Pour plus d’informations sur comment toouse ces fonctionnalités de chiffrement, consultez [à l’aide de gestion de clés extensible avec les fonctionnalités de chiffrement SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span><span class="sxs-lookup"><span data-stu-id="4a1d2-122">For more information on how toouse these encryption features, see [Using EKM with SQL Server Encryption Features](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).</span></span>

<span data-ttu-id="4a1d2-123">Notez que hello dans cet article suppose que vous avez déjà SQL Server s’exécutant sur une machine virtuelle Azure.</span><span class="sxs-lookup"><span data-stu-id="4a1d2-123">Note that hello steps in this article assume that you already have SQL Server running on an Azure virtual machine.</span></span> <span data-ttu-id="4a1d2-124">Dans le cas contraire, consultez l’article [Approvisionnement d’une machine virtuelle SQL Server dans Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span><span class="sxs-lookup"><span data-stu-id="4a1d2-124">If not, see [Provision a SQL Server virtual machine in Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md).</span></span> <span data-ttu-id="4a1d2-125">Pour d’autres conseils sur l’utilisation de SQL Server sur des machines virtuelles Azure, consultez l’article [Présentation de SQL Server sur les machines virtuelles Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4a1d2-125">For other guidance on running SQL Server on Azure VMs, see [SQL Server on Azure Virtual Machines overview](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).</span></span>
