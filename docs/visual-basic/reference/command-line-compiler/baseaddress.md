---
title: -baseaddress
ms.date: 08/09/2018
f1_keywords:
- /baseaddress
- baseaddress
helpviewer_keywords:
- -baseaddress compiler option [Visual Basic]
- /baseaddress compiler option [Visual Basic]
- baseaddress compiler option [Visual Basic]
ms.assetid: c982bcf2-46e5-47a2-bc8f-a5cc32b7dc47
ms.openlocfilehash: c794d1fc1c9d20e22ffa747e3175c846341ad8ad
ms.sourcegitcommit: bf5c5850654187705bc94cc40ebfb62fe346ab02
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91097755"
---
# <a name="-baseaddress"></a>-baseaddress

Especifica um endereço base padrão ao criar uma DLL.  
  
## <a name="syntax"></a>Sintaxe  
  
```console  
-baseaddress:address  
```  
  
## <a name="arguments"></a>Argumentos  
  
|Termo|Definição|  
|---|---|  
|`address`|Necessário. O endereço básico da DLL. Esse endereço deve ser especificado como um número hexadecimal.|  
  
## <a name="remarks"></a>Comentários  

 O endereço base padrão de uma DLL é definido pelo .NET Framework.  
  
 Lembre-se de que a palavra de ordem inferior nesse endereço é arredondada. Por exemplo, se você especificar 0x11110001, ele será arredondado para 0x11110000.  
  
 Para concluir o processo de assinatura de uma DLL, use a `–R` opção da ferramenta de nomeação forte (Sn.exe).  
  
 Essa opção será ignorada se o destino não for uma DLL.  
  
|Para Set-BaseAddress no IDE do Visual Studio|  
|---|  
|1. ter um projeto selecionado em **Gerenciador de soluções**. No menu **Projeto** , clique em **Propriedades**. <br />2. Clique na guia **Compilar** .<br />3. clique em **avançado**.<br />4. modifique o valor na caixa **endereço base do dll:** . **Observação:**      A caixa **endereço base de dll:** é somente leitura a menos que o destino seja uma dll.|  
  
## <a name="see-also"></a>Confira também

- [Compilador de linha de comando do Visual Basic](index.md)
- [-Target (Visual Basic)](target.md)
- [Linhas de Comando de Compilação de Exemplo](sample-compilation-command-lines.md)
- [Sn.exe (ferramenta de nome forte)](../../../framework/tools/sn-exe-strong-name-tool.md))
