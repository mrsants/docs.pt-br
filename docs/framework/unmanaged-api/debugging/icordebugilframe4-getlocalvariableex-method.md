---
title: ICorDebugILFrame4::Método GetLocalVariableEx
ms.date: 03/30/2017
dev_langs:
- cpp
api_name:
- ICorDebugILFrame4.GetCodeEx
api_location:
- mscordbi.dll
api_type:
- COM
ms.assetid: 0c8676f8-ca0d-4998-b64d-fefac7e38912
topic_type:
- apiref
ms.openlocfilehash: 7c43c32e10d8e10b0f843795bbc3f0f3bc20529c
ms.sourcegitcommit: 27a15a55019f6b5f2733961738babe94aec0def3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/15/2020
ms.locfileid: "90544239"
---
# <a name="icordebugilframe4getlocalvariableex-method"></a>ICorDebugILFrame4::Método GetLocalVariableEx
[Com suporte no .NET Framework 4.5.2 e versões posteriores]  
  
 Obtém o valor da variável local especificada neste quadro de pilha de linguagem intermediária (IL) e, opcionalmente, acessa uma variável adicionada na instrumentação do criador de perfil ReJIT.  
  
## <a name="syntax"></a>Sintaxe  
  
```cpp
HRESULT GetLocalVariableEx(  
   [in] ILCodeKind flags,
   [in] DWORD dwIndex,
   [out] ICorDebugValue **ppValue  
);  
```  
  
## <a name="parameters"></a>Parâmetros  
 `flags`  
 no Um membro de enumeração [ILCodeKind](ilcodekind-enumeration.md) que especifica se uma variável adicionada na instrumentação do profiler ReJIT está incluída no quadro.  
  
 `dwIndex`  
 [in] O índice da variável local no quadro de pilha IL.  
  
 `ppValue`  
 fora Um ponteiro para o endereço de um objeto "ICorDebugValue" que representa o valor recuperado.  
  
## <a name="remarks"></a>Comentários  
 Esse método é semelhante ao método [GetLocalVariable](icordebugilframe-getlocalvariable-method.md) , exceto que ele, opcionalmente, acessa uma variável adicionada na instrumentação do profiler ReJIT. Chamar esse método com um `flags` valor de `ILCODE_ORIGINAL_IL` é equivalente a chamar [GetLocalVariable](icordebugilframe-getlocalvariable-method.md); se o método for instrumentado com variáveis locais adicionais, essas variáveis não poderão ser acessadas. `ILCODE_REJIT_IL` permite ao depurador acessar as variáveis locais adicionadas na instrumentação do criador de perfil ReJIT. Se o IL não for instrumentado, o método retorna `E_INVALIDARG`.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** confira [Requisitos do sistema](../../get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **.NET Framework versões:**[!INCLUDE[net_current_v452plus](../../../../includes/net-current-v452plus-md.md)]  
  
## <a name="see-also"></a>Confira também

- [Interface ICorDebugILFrame4](icordebugilframe4-interface.md)
- [Depurando interfaces](debugging-interfaces.md)
- [ReJIT: um guia de instruções](/archive/blogs/davbr/rejit-a-how-to-guide)
