---
title: 인벤토리 컬렉션
author: wesjong
description: Overview of using Economy v2 Inventory Collections.
ms.author: wesjong
ms.date: '09/07/2022'
ms.topic: article
ms.service: playfab
keywords: playfab, commerce, economy, monetization, inventory
ms.localizationpriority: medium
---

# 컬렉션

[!INCLUDE [notice](../../../includes/_economy-release.md)]

Economy v2 인벤토리 서비스는 귀하의 인벤토리 요구에 더 큰 유연성과 지원을 추가할 수 있는 컬렉션의 개념을 도입합니다. 컬렉션은 단일 플레이어/PlayerId가 여러 인벤토리를 가질 수 있도록 하는 메커니즘입니다. 이 기능을 사용하여 동일한 플레이어의 여러 캐릭터에 대한 여러 인벤토리를 관리하고, 다른 플랫폼에 대해 별도의 인벤토리를 갖는 등의 작업을 수행할 수 있습니다!

Inventory API 호출은 작업을 수행할 컬렉션/인벤토리를 지정하는 `CollectionId` 매개 변수를 사용할 수 있습니다. 새 컬렉션 생성은 사용되지 않은 CollectionId에 항목/스택을 추가하여 수행됩니다.

## 인벤토리 컬렉션 관리

### GetInventoryCollectionIds

`GetInventoryCollectionIds` API를 사용하여 지정된 플레이어에 대한 `CollectionId` 목록을 가져올 수 있습니다. 플레이어는 자신의 ID 목록에만 액세스할 수 있습니다. 타이틀 엔티티는 액세스하려는 플레이어의 인벤토리를 나타내기 위해 `Entity` 매개 변수를 전달할 수 있습니다.

예제 `GetInventoryCollectionIds` 요청:

```csharp
{
  "Entity": {
    "Type": "title_player_account",
    "Id": "ABCD12345678"
  },
  "Count": 15,
  "ContinuationToken": "abc="
}
```

이 요청은 다음 응답을 반환합니다.

```csharp
{
  "data": {
  "CollectionIds": [
    "default".
    "main_character"
    ]
  }
}
```

#### 연속 토큰

검색 응답에서 반환된 `ContinuationToken` 필드는 인벤토리 요청에 전달되어 여러 결과 수를 통해 페이지를 매길 수 있습니다.

### 새 인벤토리 컬렉션 추가

새로운 CollectionId로 쓰기 요청을 수행하여 플레이어를 위한 새 컬렉션을 생성합니다.

예를 들어 다음 `AddInventoryItems` 요청은 collectionId `main_character`를 사용합니다.

```json
{
    "Entity": {
        "Type": "title_player_account",
        "Id": "ABCD12345678"
    },
    "CollectionId": "main_character",
    "Item": {
        "Id": "0b440353-bdbc-48d8-8873-f0988c1f9d8b",
    },
    "Amount": 10,
}
```

위 요청은 완전히 새로운 인벤토리 컬렉션을 생성하고 여기에 항목 5개를 추가하거나 이미 존재하는 경우 기존 `main_character` 인벤토리 컬렉션에 5개를 추가합니다.

### 인벤토리 수집 삭제

`DeleteInventoryCollectionId` API에서 삭제할 `CollectionId`를 정의할 수 있습니다. 삭제는 비동기 작업이며 컬렉션이 클 경우 더 오래 걸릴 수 있습니다. 삭제 작업이 완료될 때까지 컬렉션을 다시 만들 수 없습니다.

예제 `DeleteInventoryCollectionIds` 요청:

```json
{
  "Entity": {
    "Type": "title_player_account",
    "Id": "ABCD12345678"
  },
  "CollectionId": "main_character"
}
```

> [!NOTE] 현재 API는 인벤토리 컬렉션을 삭제하는 유일한 방법입니다. 게임 관리자는 현재 새 컬렉션과 기존 컬렉션에 항목을 보고 추가하는 데만 사용할 수 있습니다. 향후 추가 기능이 추가될 예정입니다.

### ExecuteInventoryOperations API

`ExecuteInventoryOperations` API에서 `CollectionId` 매개 변수를 설정할 수 있습니다. 이 매개 변수를 사용하면 작업을 수행할 컬렉션을 정의할 수 있습니다.

스택이 있는 `ExecuteInventoryOperations` 요청 예시:

```json
{
    "Entity": {
        "Type": "title_player_account",
        "Id": "ABCD12345678"
    },
    "CollectionId": "main_character",
    "Operations": [
        {
            "Update": {
                "Item" {
                    "Id": "0b440353-bdbc-48d8-8873-f0988c1f9d8b",
                    "Amount": 10
                }
            }
        },
        {
            "Subtract": {
                "Item" {
                    "Id": "0b440353-bdbc-48d8-8873-f0988c1f9d8b",
                },
                "Amount": 5
            }
        }
    ]
}
```
