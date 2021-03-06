---
title: SqlTypes e DataSet
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
ms.assetid: 9172c20a-9876-4b3b-9c97-1963c02b1993
ms.openlocfilehash: 04f95cd7d3f6e52f644f23dd8a32c77d56a5ddda
ms.sourcegitcommit: 5b475c1855b32cf78d2d1bbb4295e4c236f39464
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/24/2020
ms.locfileid: "91147502"
---
# <a name="sqltypes-and-the-dataset"></a>SqlTypes e DataSet

O ADO.NET 2.0 introduziu a compatibilidade com tipo avançada para `DataSet` por meio do namespace <xref:System.Data.SqlTypes>. Os tipos em <xref:System.Data.SqlTypes> são projetados para fornecer tipos de dados com a mesma semântica e precisão que os tipos de dados em um banco de dados SQL Server. Cada tipo de dados no <xref:System.Data.SqlTypes> tem um tipo de dados equivalente em SQL Server, com a mesma representação de dados subjacente.  
  
 Usar <xref:System.Data.SqlTypes> diretamente em um <xref:System.Data.DataSet> confere vários benefícios ao trabalhar com tipos de dados do SQL Server. <xref:System.Data.SqlTypes> é compatível com a mesma semântica que os tipos de dados nativos do SQL Server. A especificação de um dos <xref:System.Data.SqlTypes> na definição de um <xref:System.Data.DataColumn> elimina a perda de precisão que pode ocorrer ao converter tipos de dados decimais ou numéricos em um dos tipos de dados de CLR (Common Language Runtime).  
  
## <a name="example"></a>Exemplo  

 O exemplo a seguir cria um objeto <xref:System.Data.DataTable>, definindo explicitamente os tipos de dados de <xref:System.Data.DataColumn> usando <xref:System.Data.SqlTypes> em vez de tipos CLR. O código preenche a <xref:System.Data.DataTable> com os dados da tabela Sales.SalesOrderDetail no banco de dados AdventureWorks no SQL Server. A saída exibida na janela do console mostra o tipo de dados de cada coluna e os valores recuperados do SQL Server.  
  
 [!code-csharp[DataWorks SqlTypes.GetTypeAW#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlTypes.GetTypeAW/CS/source.cs#1)]
 [!code-vb[DataWorks SqlTypes.GetTypeAW#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlTypes.GetTypeAW/VB/source.vb#1)]  
  
## <a name="see-also"></a>Confira também

- [Mapeamentos de tipos de dados do SQL Server](../sql-server-data-type-mappings.md)
- [Configurar parâmetros e tipos de dados de parâmetro](../configuring-parameters-and-parameter-data-types.md)
- [Visão geral do ADO.NET](../ado-net-overview.md)
