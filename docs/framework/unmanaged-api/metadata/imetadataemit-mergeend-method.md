---
title: IMetaDataEmit::MergeEnd 方法
ms.date: 03/30/2017
api_name:
- IMetaDataEmit.MergeEnd
api_location:
- mscoree.dll
api_type:
- COM
f1_keywords:
- IMetaDataEmit::MergeEnd
helpviewer_keywords:
- MergeEnd method [.NET Framework metadata]
- IMetaDataEmit::MergeEnd method [.NET Framework metadata]
ms.assetid: 2d64315a-1af1-4c60-aedf-f8a781914aea
topic_type:
- apiref
ms.openlocfilehash: 34ecfc2f01f22971e135358806adeea632e02f8b
ms.sourcegitcommit: 9a39f2a06f110c9c7ca54ba216900d038aa14ef3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/23/2019
ms.locfileid: "74448036"
---
# <a name="imetadataemitmergeend-method"></a>IMetaDataEmit::MergeEnd 方法

合并到当前作用域中由一个或多个之前调用[IMetaDataEmit：： Merge](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-merge-method.md)指定的元数据作用域。

## <a name="syntax"></a>语法

```cppcpp
HRESULT MergeEnd ();
```

## <a name="parameters"></a>参数

此方法不采用任何参数。

## <a name="remarks"></a>备注

此例程触发元数据的实际合并，这些元数据由前面对 `IMetaDataEmit::Merge`的调用指定的所有导入范围合并到当前输出范围内。

以下特殊条件适用于合并：

- 永远不会导入模块版本标识符（MVID），因为它对于导入范围内的元数据是唯一的。

- 不会覆盖现有的模块范围的属性。

  如果已为当前作用域设置了模块属性，则不会导入任何模块属性。 但是，如果未在当前范围中设置模块属性，则在第一次遇到时，它们只会导入一次。 如果再次遇到这些模块属性，则它们是重复的。 如果比较所有模块属性（MVID 除外）的值，并且找不到重复项，则会引发错误。

- 对于类型定义（`TypeDef`），无重复项合并到当前作用域中。 针对每个*完全限定的对象名称* + *GUID* + *版本号*检查 `TypeDef` 对象是否存在重复项。 如果名称或 GUID 上存在匹配项，并且其他两个元素不同，则会引发错误。 否则，如果所有三个项均匹配，`MergeEnd` 将粗略检查以确保条目确实重复;如果不是，则会引发错误。 此粗略检查查找：

  - 相同的成员声明，按相同顺序发生。 标记为 `mdPrivateScope` 的成员（请参阅[CorMethodAttr](../../../../docs/framework/unmanaged-api/metadata/cormethodattr-enumeration.md)枚举）未包含在此检查中;它们是专门合并的。

  - 相同的类布局。

  这意味着 `TypeDef` 对象必须始终在声明它的每个元数据范围内完全一致地定义;如果其成员实现（对于某个类）分布在多个编译单元中，则假定该完整定义存在于每个作用域中，而不是增量分配给每个作用域。 例如，如果参数名称与协定相关，则必须在每个范围中以相同方式发出它们;如果不相关，则不应将其发送到元数据中。

  例外情况是 `TypeDef` 对象可以具有标记为 `mdPrivateScope`的增量成员。 如果遇到这些问题，`MergeEnd` 将以增量方式将它们添加到当前作用域，而不考虑重复项。 由于编译器理解专用范围，因此编译器必须负责强制执行规则。

- 相对虚拟地址（Rva）不会导入或合并;编译器应重新发出此信息。

- 自定义特性仅在其附加到的项合并时进行合并。 例如，当第一次遇到类时，将合并与类关联的自定义属性。 如果自定义属性与特定于编译单元的 `TypeDef` 或 `MemberDef` （如成员编译的时间戳）关联，则不会合并这些属性，而是由编译器删除或更新此类元数据。

## <a name="requirements"></a>要求

**平台：** 请参阅[系统要求](../../../../docs/framework/get-started/system-requirements.md)。

**标头：** Cor

**库：** 用作 Mscoree.dll 中的资源

**.NET Framework 版本：** [!INCLUDE[net_current_v11plus](../../../../includes/net-current-v11plus-md.md)]

## <a name="see-also"></a>另请参阅

- [IMetaDataEmit Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit-interface.md)
- [IMetaDataEmit2 Interface](../../../../docs/framework/unmanaged-api/metadata/imetadataemit2-interface.md)
