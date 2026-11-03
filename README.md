# ShootingGame — UE5 멀티플레이 3인칭 슈팅

Unreal Engine 5.5 블루프린트로 만든 **접속 → 로비 → 전투**로 이어지는 멀티플레이 슈팅 게임입니다.
무기, 아이템, 버프 시스템을 구현했습니다.

<!-- 플레이 영상이나 스크린샷을 여기에 넣어 주세요 -->

## 개요

| 항목 | 내용 |
| --- | --- |
| 엔진 | Unreal Engine 5.5 |
| 구현 방식 | 블루프린트 |
| 장르 | 3인칭 멀티플레이 슈팅 |
| 기간 | 2025.06 (마지막 커밋 기준) |
| 인원 | 1인 |

## 게임 흐름

```
EntryMap (접속) → LobbyMap (대기·준비) → GameMap (전투)
```

단계마다 GameMode와 HUD를 따로 두었습니다.
(`BP_EntryGameMode` · `BP_LobbyGameMode` · `BP_ShootingGameMode`)

## 구성

- **무기**: 기본 무기(`BP_Weapon`)와 점사(`BP_Weapon_Burst`)·연사(`BP_Weapon_MachineGun`) 무기, 무기 스포너(`BP_WeaponSpawner`)
- **아이템과 버프**: 회복(`BP_Heal`), 무한 탄약(`BP_InfiniteAmmo`), 무적(`BP_Invincible`), 탄창(`BP_Mag`), 버프 컴포넌트(`BP_BuffComponent`), 아이템 스포너(`BP_ItemSpawner`)
- **멀티플레이**: PlayerState(`BP_ShootingPlayerState`), RPC 테스트 액터(`BP_RPC_Ball`)
- **플레이어 표시**: 이름표 컴포넌트(`BP_NameTagComponent`)
- **애니메이션**: Lyra 애니메이션 세트를 바탕으로 한 무기 상태별 애니메이션 블루프린트(`ABP_Rifle` 등)

## 폴더 구조

```
Content/
├── Shooting/            # 직접 만든 게임 콘텐츠 (맵, 게임모드, 무기, 아이템)
├── Lyra_Anim/           # 캐릭터 애니메이션 (외부 에셋)
├── FPS_Weapon_Bundle/   # 무기 모델 (외부 에셋)
└── StarterContent/      # 언리얼 기본 에셋
```

## 실행 방법

Unreal Engine 5.5에서 `ShootingGame.uproject`를 열고 `Content/Shooting/Maps/EntryMap`을 엽니다.
