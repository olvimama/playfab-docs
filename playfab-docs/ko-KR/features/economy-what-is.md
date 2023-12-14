---
title: PlayFab 경제란?
author: thomasgu
description: Landing page for Economy.
ms.author: thomg
ms.date: 07/01/2023
ms.topic: article
ms.service: playfab
keywords: playfab, commerce, economy, game, items, virtual, currencies, stores, ugc, user generated content
ms.localizationpriority: medium
---

# PlayFab 경제란?

가상 경제는 단순히 게임 내 아이템을 사고 파는 것이 아닙니다. 강력한 가상 경제는 플레이어 진행에서 수익 창출 및 참여에 이르기까지 모든 것을 포괄하며 게임 디자인 및 아키텍처의 최대 과제 중 하나입니다.

참여도가 높은 플레이어와 가볍게 참여하는 플레이어를 모두 지원하는 동시에 게임에서 획득할 수 있는 아이템과 구매할 수 있는 아이템 간에 균형을 유지해야 합니다. 이는 확장성이 뛰어난 백 엔드 콘텐츠 관리 시스템 및 마켓플레이스 상환 추상화 유지에 전적으로 기반합니다.

PlayFab Economy는 [여러 SDK](../sdks/playfab-sdk-intro.md)가 포함된 [REST APIs](/rest/api/playfab/economy) 제품군이며, 플레이어를 참여시키면서 게임을 빌드, 반복 및 스케일링하는 데 도움이 되는 도구를 갖춘 [Game Manager](../gamemanager/index.md)라는 포털입니다.

> [!NOTE] Economy v2 GA가 출시되었습니다. [v2 개요](economy-v2/overview.md)에서 v1과 v2의 차이점에 대해 자세히 알아볼 수 있습니다.

PlayFab Economy는 아이템, 통화, 스토어, 사용자 생성 콘텐츠와 같은 게임의 가상 경제의 다양한 측면을 포함합니다. 다음은 알아야 할 몇 가지 주요 개념 및 API입니다.

## 주요 개념 &amp; API

- **[카탈로그](economy-v2/catalog/catalog-overview.md)** - 카탈로그는 게임의 가상 아이템을 관리하는 쉬운 방법을 제공합니다. 여기에는 게임에서 사용할 수 있는 모든 항목의 목록이 포함되어 있습니다.
- **[카탈로그 아이템](economy-v2/inventory/items-and-inventory-overview.md)** - PlayFab 아이템은 내구재에서 번들, UGC까지, 귀하가 사용할 수 있는 거의 모든 종류의 가상 재화입니다.
- **[인벤토리 컬렉션](economy-v2/inventory/index.md)** - 플레이어 인벤토리에는 모든 소유 아이템 인스턴스가 포함됩니다.
- **[가상 통화](economy/tutorials/currencies.md)** - 통화는 카탈로그 또는 스토어에서 아이템을 구입하기 위해 사용하거나, 앱내 구매에서 변환된 연화를 나타내거나, 게임 플레이를 촉진하는 메커니즘으로 사용할 수 있습니다.
- **[스토어](economy-v2/stores.md)** - 스토어는 대체 가격으로 제공할 수 있는 카탈로그 항목의 하위 집합을 제공합니다.
- **[사용자 생성 콘텐츠](economy-v2/ugc/index.md)** - 플레이어가 중재된 콘텐츠를 생성, 업로드, 검색할 수 있도록 역량을 강화합니다. PlayFab UGC 사용을 시작하는 방법에 대한 자세한 내용은 [UGC 빠른 시작](economy-v2/ugc/quickstart.md)을 참조하세요.

PlayFab Economy는 게임 경제 모범 사례를 지원하는 도구 모음도 제공합니다. **모범 사례 도구는 다음과 같습니다.**

- **카탈로그 검색** : 카탈로그 검색: V2는 대규모 카탈로그를 지원하기 위해 처음부터 빌드되었으며, 필터링, 이에 대한 핵심 구성 요소는 필터링, 선택 항목 및 주문을 지원하는 SearchItems API입니다. 자세한 내용은 [SearchItems](economy-v2/catalog/search.md) 설명서를 참조하세요.

- **여러 통화** : 대부분의 게임에서 두 가지 이상의 가상 통화를 지원합니다. 대부분이 게임내 플레이를 통해 딸 수 있는 “소프트” 통화와 살 수 있는 “하드” 통화를 사용합니다. 두 통화를 모두 사용하면 어떤 아이템을 구입할 수 있는지 귀하가 결정할 수 있기 때문에 경제성을 더 잘 관리할 수 있습니다. [통화](economy/tutorials/currencies.md)에 대한 자습서를 참조하십시오.

- **서버 측 영수증 검증** : 사기를 방지하고 귀하가 만들고 있다고 생각하는 돈이 실제로 만들어지고 있는지 확인합니다. [Unity 및 Android를 사용한 시작 자습서](economy-v2/tutorials/getting-started-with-unity-and-android.md) 튜토리얼을 참조하세요.

- **번들** : 번들은 일반적으로 가상 상품을 그룹으로 판매하는 아이템을 그룹화하기 위한 유용한 구조입니다. 번들을 사용하는 방법에 대한 자세한 내용은 [번들](economy-v2/bundles.md) 설명서를 참조하세요.

- **가상 구독** : 구독을 사용하여 내구제에 대한 시간 기반 액세스 권한을 부여합니다. [Economy V2 구독](economy-v2/subscriptions.md) 설명서를 참조하세요.

- **트랜잭션 기록** : 트랜잭션 기록 API는 플레이어의 인벤토리에서 수행된 모든 작업을 검색하여 사용량을 추적하고 문제를 해결할 수 있습니다. [Economy V2 컬렉션](economy-v2/inventory/collections.md) 설명서를 참조하세요.

- **인벤토리 컬렉션** : 이 기능을 사용하여 플레이어에게 여러 인벤토리를 제공합니다. [Economy V2 트랜잭션 기록](economy-v2/inventory/transaction-history.md) 설명서를 참조하세요.

- **인벤토리 스택** : 스택을 사용하면 인벤토리에서 아이템 스택 또는 동일한 아이템의 개별 인스턴스를 저장할 수 있습니다. [Economy V2 스택](economy-v2/inventory/stacks.md) 설명서를 참조하세요.

- **딥 링크** : 딥 링크를 사용하면 게임 내 또는 플랫폼 스토어에 직접 연결할 수 있습니다. [딥 링크](economy-v2/catalog/deep-links.md) 설명서를 참조하세요.

- **Etags** : Etag를 사용하여 아이템 업데이트 중에 동시성을 관리할 수 있습니다. [Etags](economy-v2/catalog/etags.md) 설명서를 참조하세요.

- **등급 및 리뷰** : 등급 및 리뷰를 사용하여 플레이어 피드백을 수집하고 게임의 품질을 향상시킬 수 있습니다. [ 등급 및 리뷰](economy-v2/catalog/ratings.md) 문서를 참조하세요.

> 이전 버전의 PlayFab Economy(V1 또는 레거시)에 관심이 있는 경우 [레거시 Economy](economy/index.yml) 에서 해당 설명서를 찾을 수 있습니다.
