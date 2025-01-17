---
author: rothja
ms.service: virtual-machines-sql
ms.topic: include
ms.date: 10/26/2018
ms.author: jroth
ms.openlocfilehash: 22f16a7382cb0fe1f3fe2a6ef5e7c00a6989623c
ms.sourcegitcommit: 778e7376853b69bbd5455ad260d2dc17109d05c1
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 05/23/2019
ms.locfileid: "66165342"
---
## <a name="next-steps"></a>次の手順

Azure Key Vault 統合を有効にしたら、SQL VM で SQL Server 暗号化を有効にできます。 最初に、Key Vault 内で非対称鍵を作成し、VM の SQL Server 内で対称鍵を作成する必要があります。 これでデータベースとバックアップの暗号化を有効にする T-SQL ステートメントを実行できます。

次のような形式の暗号化を活用できます。

* [透過的なデータ暗号化 (TDE)](https://msdn.microsoft.com/library/bb934049.aspx)
* [暗号化バックアップ](https://msdn.microsoft.com/library/dn449489.aspx)
* [列レベルの暗号化 (CLE)](https://msdn.microsoft.com/library/ms173744.aspx)

次の Transact-SQL スクリプトにはこれらの各領域の例があります。

### <a name="prerequisites-for-examples"></a>例の前提条件

例はいずれも 2 つ前提条件に基づきます。Key Vault からの "**CONTOSO_KEY**" という名前の非対称鍵と AKV 統合機能により作成された "**Azure_EKM_TDE_cred**" という名前の資格情報です。 以下の Transact-SQL コマンドは、これらの前提条件を準備して、例を実行できるようにするためのものです。

``` sql
USE master;
GO

--create credential
--The <<SECRET>> here requires the <Application ID> (without hyphens) and <Secret> to be passed together without a space between them.
CREATE CREDENTIAL sysadmin_ekm_cred
    WITH IDENTITY = 'keytestvault', --keyvault
    SECRET = '<<SECRET>>'
FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov;


--Map the credential to a SQL login that has sysadmin permissions. This allows the SQL login to access the key vault when creating the asymmetric key in the next step.
ALTER LOGIN [SQL_Login]
ADD CREDENTIAL sysadmin_ekm_cred;


CREATE ASYMMETRIC KEY CONTOSO_KEY
FROM PROVIDER [AzureKeyVault_EKM_Prov]
WITH PROVIDER_KEY_NAME = 'KeyName_in_KeyVault',  --The key name here requires the key we created in the key vault
CREATION_DISPOSITION = OPEN_EXISTING;
```

### <a name="transparent-data-encryption-tde"></a>透過的なデータ暗号化 (TDE)

1. TDE のためにデータベース エンジンで使用される SQL Server を作成し、それに資格情報を追加します。

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it loads a database
   -- encrypted by TDE.
   CREATE LOGIN EKM_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the TDE Login to add the credential for use by the
   -- Database Engine to access the key vault
   ALTER LOGIN EKM_Login
   ADD CREDENTIAL Azure_EKM_cred;
   GO
   ```

1. TDE に使用されるデータベース暗号化鍵を作成します。

   ``` sql
   USE ContosoDatabase;
   GO

   CREATE DATABASE ENCRYPTION KEY 
   WITH ALGORITHM = AES_128 
   ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the database to enable transparent data encryption.
   ALTER DATABASE ContosoDatabase
   SET ENCRYPTION ON;
   GO
   ```

### <a name="encrypted-backups"></a>暗号化バックアップ

1. バックアップを暗号化するためにデータベース エンジンで使用される SQL Server を作成し、それに資格情報を追加します。

   ``` sql
   USE master;
   -- Create a SQL Server login associated with the asymmetric key
   -- for the Database engine to use when it is encrypting the backup.
   CREATE LOGIN EKM_Login
   FROM ASYMMETRIC KEY CONTOSO_KEY;
   GO

   -- Alter the Encrypted Backup Login to add the credential for use by
   -- the Database Engine to access the key vault
   ALTER LOGIN EKM_Login
   ADD CREDENTIAL Azure_EKM_cred ;
   GO
   ```

1. Key Vault に保存されている非対称鍵で暗号化を指定し、データベースをバックアップします。

   ``` sql
   USE master;
   BACKUP DATABASE [DATABASE_TO_BACKUP]
   TO DISK = N'[PATH TO BACKUP FILE]'
   WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,
   ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);
   GO
   ```

### <a name="column-level-encryption-cle"></a>列レベルの暗号化 (CLE)

このスクリプトにより、Key Vault の非対称鍵で保護される対称鍵が作成され、その対称鍵を利用し、データベースのデータが暗号化されます。

``` sql
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY
WITH ALGORITHM=AES_256
ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

DECLARE @DATA VARBINARY(MAX);

--Open the symmetric key for use in this session
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;

--Encrypt syntax
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));

-- Decrypt syntax
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));

--Close the symmetric key
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;
```

## <a name="additional-resources"></a>その他のリソース

これらの暗号化機能の使用方法の詳細については、「 [SQL Server 暗号化機能で EKM を使用する](https://msdn.microsoft.com/library/dn198405.aspx#UsesOfEKM)」を参照してください。

この記事の手順では、Azure 仮想マシンで SQL Server を既に実行していることを前提としています。 実行していない場合、[Azure での SQL Server 仮想マシンのプロビジョニング](../articles/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision.md)に関するページを参照してください。 Azure VM で SQL Server を実行する方法については、「[Azure Virtual Machines における SQL Server の概要](../articles/virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)」を参照してください。
