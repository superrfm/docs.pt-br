---
title: "Método ICorDebugMetaDataLocator::GetMetaData"
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology: dotnet-clr
ms.tgt_pltfrm: 
ms.topic: reference
api_name: ICorDebugMetaDataLocator.GetMetaData
api_location: mscordbi.dll
api_type: COM
f1_keywords: ICorDebugMetaDataLocator::GetMetaData
helpviewer_keywords:
- ICorDebugMetaDataLocator::GetMetaData method [.NET Framework debugging]
- GetMetaData method, ICorDebugMetaDataLocator interface [.NET Framework debugging]
ms.assetid: f9b0ff22-54db-45eb-9cc3-508000a3141d
topic_type: apiref
caps.latest.revision: "8"
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.workload: dotnet
ms.openlocfilehash: 4883ee56c7dd027f053dd072d7c8613f606ff2be
ms.sourcegitcommit: 16186c34a957fdd52e5db7294f291f7530ac9d24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/22/2017
---
# <a name="icordebugmetadatalocatorgetmetadata-method"></a>Método ICorDebugMetaDataLocator::GetMetaData
Solicita que o depurador para retornar o caminho completo para um módulo cujos metadados é necessária para concluir uma operação solicitado do depurador.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
HRESULT GetMetaData(  
      [in] LPCWSTR wszImagePath,  
      [in] DWORD   dwImageTimeStamp,  
      [in] DWORD   dwImageSize,  
      [in] ULONG32 cchPathBuffer,  
      [out] ULONG32 * pcchPathBuffer,  
      [out, size_is(cchPathBuffer), length_is(*pcchPathBuffer)]  
               WCHAR wszPathBuffer[]  
      );  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `wszImagePath`  
 [in] Uma cadeia terminada em nulo que representa o caminho completo para o arquivo. Se o caminho completo não estiver disponível, o nome e a extensão do arquivo (*filename*. *extensão*).  
  
 `dwImageTimeStamp`  
 [in] O carimbo de hora de cabeçalhos de arquivo PE da imagem. Esse parâmetro potencialmente pode ser usado para um servidor de símbolos ([SymSrv](http://msdn.microsoft.com/library/cc266470.aspx)) pesquisa.  
  
 `dwImageSize`  
 [in] O tamanho da imagem de cabeçalhos de arquivo PE. Esse parâmetro potencialmente pode ser usado para uma pesquisa SymSrv.  
  
 `cchPathBuffer`  
 [in] O caractere de contagem no `wszPathBuffer`.  
  
 `pcchPathBuffer`  
 [out] A contagem de `WCHAR`s gravados `wszPathBuffer`.  
  
 Se o método retornar E_NOT_SUFFICIENT_BUFFER, contém a contagem de `WCHAR`s necessários para o caminho do repositório.  
  
 `wszPathBuffer`  
 [out] Ponteiro para um buffer no qual o depurador irá copiar o caminho completo do arquivo que contém os metadados solicitados.  
  
 O `ofReadOnly` sinalizador do [CorOpenFlags](../../../../docs/framework/unmanaged-api/metadata/coropenflags-enumeration.md) enumeração é usada para solicitar o acesso somente leitura para os metadados deste arquivo.  
  
## <a name="return-value"></a>Valor de retorno  
 Este método retorna a seguintes HRESULTs específicos, bem como o HRESULT erros que indicam falha do método. Todos os outros HRESULTs falha indicam que o arquivo não é recuperável.  
  
|HRESULT|Descrição|  
|-------------|-----------------|  
|S_OK|O método foi concluído com êxito. `wszPathBuffer`contém o caminho completo para o arquivo e é terminada em nulo.|  
|E_NOT_SUFFICIENT_BUFFER|O tamanho atual de `wszPathBuffer` não é suficiente para conter o caminho completo. Nesse caso, `pcchPathBuffer` contém a quantidade necessária de `WCHAR`s, incluindo o caractere null de terminação e `GetMetaData` é chamado uma segunda vez com o tamanho do buffer solicitado.|  
  
## <a name="remarks"></a>Comentários  
 Se `wszImagePath` contém um caminho completo para um módulo de um despejo, especifica o caminho do computador onde o despejo de memória foi coletado. O arquivo pode não existir neste local, ou um arquivo incorreto com o mesmo nome pode ser armazenado no caminho.  
  
## <a name="requirements"></a>Requisitos  
 **Plataformas:** consulte [requisitos de sistema](../../../../docs/framework/get-started/system-requirements.md).  
  
 **Cabeçalho:** CorDebug.idl, CorDebug.h  
  
 **Biblioteca:** CorGuids.lib  
  
 **Versões do .NET framework:**[!INCLUDE[net_current_v40plus](../../../../includes/net-current-v40plus-md.md)]  
  
## <a name="see-also"></a>Consulte também  
 [Interface ICorDebugThread4](../../../../docs/framework/unmanaged-api/debugging/icordebugthread4-interface.md)  
 [Depurando interfaces](../../../../docs/framework/unmanaged-api/debugging/debugging-interfaces.md)  
 [Depuração](../../../../docs/framework/unmanaged-api/debugging/index.md)
