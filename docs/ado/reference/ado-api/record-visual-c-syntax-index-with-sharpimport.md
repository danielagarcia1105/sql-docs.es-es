---
title: 'Registro (Visual C++ índice de sintaxis con #import) | Microsoft Docs'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
apitype: COM
dev_langs:
- C++
helpviewer_keywords:
- 'Record collection [ADO], Visual C++ syntax index with #import'
ms.assetid: ba6dd186-9552-4b6c-960b-3ee6cd589afd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 05b2ab826fd5afe9b91b3dcfb314af176b1cb9da
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/01/2018
ms.locfileid: "47645743"
---
# <a name="record-visual-c-syntax-index-with-import"></a>Registro (Visual C++ índice de sintaxis con #import)
## <a name="methods"></a>Métodos  
  
```  
HRESULT Cancel( );  
  
HRESULT Close( );  
  
_bstr_t CopyRecord( _bstr_t Source, _bstr_t Destination,  
    _bstr_t     UserName, _bstr_t Password, enum CopyRecordOptionsEnum  
    Options,     VARIANT_BOOL Async );  
  
HRESULT DeleteRecord( _bstr_t Source, VARIANT_BOOL Async );  
  
_RecordsetPtr GetChildren( );  
  
_bstr_t MoveRecord( _bstr_t Source, _bstr_t Destination,  
    _bstr_t     UserName, _bstr_t Password, enum MoveRecordOptionsEnum  
    Options,     VARIANT_BOOL Async );  
  
HRESULT Open( const _variant_t & Source, const _variant_t  
&     ActiveConnection, enum ConnectModeEnum Mode, enum  
    RecordCreateOptionsEnum CreateOptions, enum RecordOpenOptionsEnum  
    Options, _bstr_t UserName, _bstr_t Password );  
```  
  
## <a name="properties"></a>Propiedades  
  
```  
_variant_t GetActiveConnection( );  
void PutActiveConnection( _bstr_t pvar );  
void PutRefActiveConnection( struct _Connection * pvar );  
  
FieldsPtr GetFields( );  
__declspec(property(get=GetFields)) FieldsPtr Fields;  
  
enum ConnectModeEnum GetMode( );  
void PutMode( enum ConnectModeEnum pMode );  
__declspec(property(get=GetMode,put=PutMode)) enum ConnectModeEnum Mode;  
  
_bstr_t GetParentURL( );  
__declspec(property(get=GetParentURL)) _bstr_t ParentURL;  
  
enum RecordTypeEnum GetRecordType( );  
__declspec(property(get=GetRecordType)) enum RecordTypeEnum  
    RecordType;  
  
_variant_t GetSource( );  
void PutSource( _bstr_t pvar );  
void PutRefSource( IDispatch * pvar );  
  
enum ObjectStateEnum GetState( );  
__declspec(property(get=GetState)) enum ObjectStateEnum State;  
```  
  
## <a name="see-also"></a>Vea también  
 [Objeto Record (ADO)](../../../ado/reference/ado-api/record-object-ado.md)
