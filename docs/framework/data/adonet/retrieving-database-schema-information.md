---
title: "Recuperando informações de esquema de banco de dados"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-ado
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 79038d52-f122-4fd4-9bfb-aaa22d6a114b
caps.latest.revision: "3"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: dotnet
ms.openlocfilehash: 09a0ec444801d1fe2caccf9e25a68e3c6ae8f5c2
ms.sourcegitcommit: ed26cfef4e18f6d93ab822d8c29f902cff3519d1
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/17/2018
---
# <a name="retrieving-database-schema-information"></a>Recuperando informações de esquema de banco de dados
A obtenção de informações de esquema de um banco de dados é realizada com o processo de descoberta de esquema. Descoberta de esquema permite que os aplicativos solicitar que os provedores gerenciados localizar e retornam informações sobre o esquema de banco de dados, também conhecido como *metadados*, de um determinado banco de dados. Os diferentes elementos de esquema de banco de dados, como tabelas, colunas e procedimentos armazenados, são expostos por meio de coleções de esquema. Cada coleção de esquema contém uma variedade de informações de esquema específicas ao provedor em uso.  
  
 Cada a implementação de provedores gerenciados do .NET Framework a **GetSchema** método o **Conexão** classe e as informações de esquema que são retornadas o **GetSchema**método vem na forma de um <xref:System.Data.DataTable>. O **GetSchema** é um método sobrecarregado que fornece parâmetros opcionais para especificar a coleção de esquema para retornar e restringir a quantidade de informações retornadas.  
  
 Os provedores de dados .NET Framework para OLE DB, ODBC, Oracle e SqlClient fornecem um **GetSchemaTable** método que retorna um DataTable que descreve os metadados da coluna de **DataReader**.  
  
 O Provedor de Dados .NET Framework para OLE DB também expõe informações de esquema usando o método <xref:System.Data.OleDb.OleDbConnection.GetOleDbSchemaTable%2A> do objeto <xref:System.Data.OleDb.OleDbConnection>. Como argumentos, **GetOleDbSchemaTable** leva um <xref:System.Data.OleDb.OleDbSchemaGuid> que identifica as informações de esquema para retornar e uma matriz de restrições nas colunas retornadas. **GetOleDbSchemaTable** retorna um <xref:System.Data.DataTable> preenchido com as informações de esquema solicitada.  
  
## <a name="in-this-section"></a>Nesta seção  
 [GetSchema e coleções de esquema](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)  
 Descreve o **GetSchema** método e como ele pode ser usado para recuperar e restringir as informações de esquema de banco de dados.  
  
 Restrições de esquema  
 Descreve as restrições de esquema que podem ser usadas com **GetSchema**.  
  
 [Coleções de esquema comuns](../../../../docs/framework/data/adonet/common-schema-collections.md)  
 Descreve todas as coleções de esquema comuns com suporte em todos os provedores gerenciados .NET Framework.  
  
 [Coleções de esquema do SQL Server](../../../../docs/framework/data/adonet/sql-server-schema-collections.md)  
 Descreve a coleção de esquema com suporte pelo provedor .NET Framework para SQL Server.  
  
 [Coleções de esquema do Oracle](../../../../docs/framework/data/adonet/oracle-schema-collections.md)  
 Descreve a coleção de esquema com suporte pelo provedor .NET Framework para Oracle.  
  
 [Coleções de esquema ODBC](../../../../docs/framework/data/adonet/odbc-schema-collections.md)  
 Descreve as coleções de esquema para drivers ODBC.  
  
 [Coleções de esquema de OLE DB](../../../../docs/framework/data/adonet/ole-db-schema-collections.md)  
 Descreve as coleções de esquema para provedores OLE DB.  
  
## <a name="reference"></a>Referência  
 <xref:System.Data.Common.DbConnection.GetSchema%2A>  
 Descreve o **GetSchema** método o <xref:System.Data.Common.DbConnection> classe.  
  
 <xref:System.Data.Odbc.OdbcConnection.GetSchema%2A>  
 Descreve o **GetSchema** método o <xref:System.Data.Odbc.OdbcConnection> classe.  
  
 <xref:System.Data.OleDb.OleDbConnection.GetSchema%2A>  
 Descreve o **GetSchema** método o <xref:System.Data.OleDb.OleDbConnection> classe.  
  
 <xref:System.Data.OracleClient.OracleConnection.GetSchema%2A>  
 Descreve o **GetSchema** método o <xref:System.Data.OracleClient.OracleConnection> classe.  
  
 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>  
 Descreve o **GetSchema** método o <xref:System.Data.SqlClient.SqlConnection> classe.  
  
 <xref:System.Data.Common.DbDataReader.GetSchemaTable%2A>  
 Descreve o **GetSchemaTable** método o <xref:System.Data.Common.DbDataReader> classe.  
  
 <xref:System.Data.Odbc.OdbcDataReader.GetSchemaTable%2A>  
 Descreve o **GetSchemaTable** método o <xref:System.Data.Odbc.OdbcDataReader> classe.  
  
 <xref:System.Data.OleDb.OleDbDataReader.GetSchemaTable%2A>  
 Descreve o **GetSchemaTable** método o <xref:System.Data.OleDb.OleDbDataReader> classe.  
  
 <xref:System.Data.OracleClient.OracleDataReader.GetSchemaTable%2A>  
 Descreve o **GetSchemaTable** método o <xref:System.Data.OracleClient.OracleDataReader> classe.  
  
 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>  
 Descreve o **GetSchemaTable** método o <xref:System.Data.SqlClient.SqlDataReader> classe.  
  
## <a name="see-also"></a>Consulte também  
 [Retrieving and Modifying Data in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md) (Recuperando e modificando dados no ADO.NET)  
 [ADO.NET Managed Providers and DataSet Developer Center](http://go.microsoft.com/fwlink/?LinkId=217917) (Central de desenvolvedores do DataSet e de provedores gerenciados do ADO.NET)
