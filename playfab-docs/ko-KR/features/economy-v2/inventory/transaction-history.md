---
title: 트랜잭션 기록
author: wesjong
description: Overview of using Economy v2 Transaction History API.
ms.author: wesjong
ms.date: '09/07/2022'
ms.topic: article
ms.service: playfab
keywords: playfab, commerce, economy, monetization, inventory
ms.localizationpriority: medium
---

# 트랜잭션 기록

[!INCLUDE [notice](../../../includes/_economy-release.md)]

Economy v2 인벤토리 서비스에는 플레이어의 인벤토리에서 수행한 모든 작업을 볼 수 있는 트랜잭션 기록 API가 있습니다. 이 데이터는 게임 시스템의 사용량을 추적하고, 버그 문제를 해결하고, 악의적인 행위자를 식별하는 데 사용할 수 있습니다.

트랜잭션 기록은 플레이어의 다양한 인벤토리 컬렉션으로 그룹화되며 각 컬렉션은 고유한 기록을 갖습니다. `CollectionId`을(를) 사용하고 플레이어당 여러 인벤토리를 보유하는 방법에 대한 자세한 내용은 [여기](collections.md)에서 확인할 수 있습니다.

CollectionCreated 및 CollectionDeleted와 같은 일부 이벤트는 트랜잭션 기록에 표시되지 않습니다.

## 플레이어의 트랜잭션 기록 가져오기

### [게임 관리자](#tab/transaction-history-game-manager)

1. [게임 관리자](../../../gamemanager/index.md)에서 `Players`(으)로 이동
2. 보려는 플레이어를 선택한 다음, `Transaction History`(으)로 이동

### [API](#tab/transaction-history-api)

`GetTransactionHistory` API를 사용하여 플레이어의 트랜잭션 기록을 가져올 수 있습니다. `CollectionId` 매개 변수를 전달하여 보려고 하는 인벤토리 컬렉션의 기록을 나타냅니다. 플레이어는 자신의 트랜잭션 기록에만 액세스하도록 제한됩니다. 타이틀 엔터티는 `Entity` 매개 변수를 전달하여 액세스하려는 플레이어의 트랜잭션 기록을 나타낼 수 있습니다.

`Filter` 매개 변수를 사용하여 특정 트랜잭션 기간을 볼 수 있는 타임스탬프 제약 조건을 전달할 수 있습니다. `Filter`은(는) `timestamp ge`(크거나 같음) 및 `timestamp le`(작거나 같음)만 지원하며 트랜잭션 기록을 볼 수 있는 타임스탬프 기간은 최대 6개월로 제한됩니다.

예제 `GetTransactionHistory` 요청:

```json
{
    "Entity": {
        "Id": "ABCD12345678",
        "Type": "title_player_account",
    },
    "CollectionId": "default",
    "Count": 10,
    "Filter": "timestamp ge 2021-12-30T23:00Z and timestamp le 2021-12-31T23:00Z"
}
```

#### 연속 토큰

응답에서 반환되는 `ContinuationToken` 필드를 트랜잭션 기록 요청에 전달하여 여러 결과 수를 통해 페이지 매김할 수 있습니다.
