## <a name="next-steps"></a>Étapes suivantes

Après avoir activé Azure Key Vault Integration, vous pouvez activer le chiffrement SQL Server sur votre machine virtuelle SQL. Tout d’abord, vous devez toocreate une clé asymétrique à l’intérieur de votre coffre de clés et une clé symétrique dans SQL Server sur votre machine virtuelle. Ensuite, vous serez cryptage de tooenable instructions tooexecute en mesure de T-SQL pour vos bases de données et les sauvegardes.

Il existe plusieurs types de chiffrement que vous pouvez exploiter :

* [Chiffrement transparent des données (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [Sauvegardes chiffrées](https://msdn.microsoft.com/library/dn449489.aspx)
* [Chiffrement au niveau des colonnes (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

Hello des scripts Transact-SQL suivantes fournissent des exemples pour chacun de ces domaines.

### <a name="prerequisites-for-examples"></a>Configuration requise pour les exemples

Chaque exemple est basé sur la configuration requise de hello deux : une clé asymétrique à partir de votre coffre de clés appelé **CONTOSO_KEY** et les informations d’identification créé par la fonctionnalité d’intégration de AKV hello appelée **Azure_EKM_TDE_cred**. Hello commandes Transact-SQL suivantes d’installation ces conditions préalables pour exécuter les exemples hello.

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

### <a name="transparent-data-encryption-tde"></a>Chiffrement transparent des données (TDE)

1. Créer un toobe de connexion SQL Server utilisé par hello du moteur de base de données pour le chiffrement transparent des données, puis ajouter tooit des informations d’identification hello.

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

1. Créer la clé de chiffrement de base de données hello qui sera utilisé pour le chiffrement transparent des données.

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

### <a name="encrypted-backups"></a>Sauvegardes chiffrées

1. Créer un toobe de connexion SQL Server utilisé par hello du moteur de base de données pour le chiffrement des sauvegardes et ajoutez tooit des informations d’identification hello.

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

1. Base de données de sauvegarde hello en spécifiant le chiffrement à clé asymétrique de hello stockée dans le coffre de clés hello.

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   tooDISK = N'[PATH tooBACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>Chiffrement au niveau des colonnes (CLE)

Ce script crée une clé symétrique protégée par hello la clé asymétrique dans le coffre de clés hello et utilise ensuite les données de salutation tooencrypt clé symétrique dans la base de données hello.

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

## <a name="additional-resources"></a>Ressources supplémentaires

Pour plus d’informations sur comment toouse ces fonctionnalités de chiffrement, consultez [à l’aide de gestion de clés extensible avec les fonctionnalités de chiffrement SQL Server](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM).

Notez que hello dans cet article suppose que vous avez déjà SQL Server s’exécutant sur une machine virtuelle Azure. Dans le cas contraire, consultez l’article [Approvisionnement d’une machine virtuelle SQL Server dans Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md). Pour d’autres conseils sur l’utilisation de SQL Server sur des machines virtuelles Azure, consultez l’article [Présentation de SQL Server sur les machines virtuelles Azure](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md).
