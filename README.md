# ShootingGame — UE5 멀티플레이 3인칭 슈팅

Unreal Engine 5.5 블루프린트로 만든 **로비 → 매칭 → 전투**가 이어지는 멀티플레이 슈팅 게임입니다.
네트워크 복제(Replication)와 RPC를 공부하며, 무기·아이템·버프 시스템을 직접 설계하고 구현했습니다.

<!-- 플레이 영상이나 스크린샷을 여기에 넣어 주세요 -->
<!-- ![gameplay](docs/gameplay.gif) -->

## 개요

| 항목 | 내용 |
| --- | --- |
| 엔진 | Unreal Engine 5.5 |
| 구현 방식 | 블루프린트 |
| 장르 | 3인칭 멀티플레이 슈팅 |
| 기간 | 2025.06 |
| 인원 | 1인 |

## 게임 흐름

```
EntryMap (접속) → LobbyMap (대기·준비) → GameMap (전투)
```

각 단계마다 GameMode와 HUD를 따로 두어 화면과 규칙을 분리했습니다.
(`BP_EntryGameMode` · `BP_LobbyGameMode` · `BP_ShootingGameMode`)

## 구현한 시스템

- **무기 시스템**: `BP_Weapon`을 부모로 점사(`BP_Weapon_Burst`)와 연사(`BP_Weapon_MachineGun`) 무기를 상속 구조로 확장했습니다. 맵의 `BP_WeaponSpawner`에서 무기가 생성됩니다
- **아이템과 버프**: 회복(`BP_Heal`), 무한 탄약(`BP_InfiniteAmmo`), 무적(`BP_Invincible`), 탄창(`BP_Mag`) 아이템을 만들고, `BP_BuffComponent`로 버프 적용과 해제를 한곳에서 관리했습니다
- **네트워크 동기화**: `BP_RPC_Ball`로 서버와 클라이언트 사이의 RPC 호출을 실험하고, 플레이어 상태는 `BP_ShootingPlayerState`로 복제했습니다
- **플레이어 표시**: `BP_NameTagComponent`로 캐릭터 머리 위에 이름을 표시했습니다
- **애니메이션**: Lyra 애니메이션 세트를 바탕으로 맨손·권총·소총 상태별 애니메이션 블루프린트와 Aim Offset을 구성했습니다

## 폴더 구조

```
Content/
├── Shooting/            # 직접 만든 게임 콘텐츠 (맵, 게임모드, 무기, 아이템)
├── Lyra_Anim/           # 캐릭터 애니메이션 (외부 에셋)
├── FPS_Weapon_Bundle/   # 무기 모델 (외부 에셋)
└── StarterContent/      # 언리얼 기본 에셋
```

## 실행 방법

1. Unreal Engine 5.5에서 `ShootingGame.uproject`를 엽니다
2. `Content/Shooting/Maps/EntryMap`을 열고 실행합니다
3. 멀티플레이 테스트는 에디터 Play 설정에서 플레이어 수를 2명 이상, Net Mode를 Listen Server로 설정합니다

## 배운 점

- 서버 권한(Authority)과 클라이언트 예측의 차이, 어떤 값을 복제해야 하는지 판단하는 기준
- 상속과 컴포넌트로 무기와 버프를 확장하기 쉬운 구조로 설계하는 방법
