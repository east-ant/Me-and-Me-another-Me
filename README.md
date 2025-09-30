# Me-and-Me-another-Me

**3D 타임루프 퍼즐 게임**  
📅 개발 기간: 2025.05.13 - 2025.06.22  

## 📖 프로젝트 개요

Unreal Engine 5를 활용한 3D 타임루프 퍼즐 게임입니다.  
30초 타임루프 동안 플레이어의 행동을 기록하고, 과거의 자신(고스트)과 협동하여 퍼즐을 해결하는 독특한 게임플레이를 제공합니다.

## ✨ 주요 기능

### 1. 타임루프 시스템
- 30초 단위로 반복되는 타임루프 구현
- 루프가 끝나면 자동으로 시간 되감기 및 재시작

### 2. 플레이어 행동 녹화 & 재생

    // 플레이어의 위치, 회전, 액션을 프레임 단위로 기록
    struct FPlayerRecord {
        FVector Location;
        FRotator Rotation;
        EPlayerAction Action;
        float Timestamp;
    };

플레이어의 모든 움직임과 상호작용을 기록
다음 루프에서 고스트로 재생

3. 고스트 협동 시스템

이전 루프의 자신이 고스트로 등장
여러 고스트와 협력하여 퍼즐 해결
타이밍 기반 협동 메커니즘

🎮 게임 스크린샷


<img width="758" height="530" alt="image" src="https://github.com/user-attachments/assets/9c2c0adb-e44b-4d1c-a1ab-c6d09576a078" />

🛠️ 기술 스택

엔진: Unreal Engine 5
언어: C++
주요 기술:

타임루프 게임 로직 구현
플레이어 행동 녹화 및 재생 시스템
AI Navigation & Pathfinding
Blueprint와 C++ 연동



📂 프로젝트 구조
<pre>
Me-and-Me-another-Me/
├── Source/
│   ├── Player/
│   │   ├── PlayerCharacter.cpp       # 플레이어 캐릭터 클래스
│   │   └── PlayerRecorder.cpp        # 행동 녹화 시스템
│   ├── Ghost/
│   │   └── GhostCharacter.cpp        # 고스트 재생 시스템
│   ├── GameMode/
│   │   └── TimeLoopGameMode.cpp      # 타임루프 관리
│   └── Puzzle/
│       └── PuzzleManager.cpp         # 퍼즐 로직
├── Content/
│   ├── Maps/                         # 게임 레벨
│   ├── Blueprints/                   # 블루프린트 에셋
│   └── Materials/                    # 머티리얼 및 텍스처
└── Config/                           # 프로젝트 설정
</pre>
🎯 핵심 구현 사항
타임루프 시스템
    cppvoid ATimeLoopGameMode::StartTimeLoop()
    {
        CurrentLoopTime = 0.0f;
        PlayerRecorder->StartRecording();
        SpawnPreviousGhosts();
    }
    
    void ATimeLoopGameMode::ResetTimeLoop()
    {
        PlayerRecorder->StopRecording();
        SaveRecordedData();
        ResetLevel();
    }
행동 녹화 시스템

프레임마다 플레이어의 Transform 데이터 저장
상호작용 이벤트 타임스탬프 기록
메모리 최적화를 위한 데이터 압축

고스트 재생

녹화된 데이터를 기반으로 정확한 재현
다중 고스트 동시 재생 지원
물리 충돌 및 상호작용 구현



📝 개발 과정에서 배운 점

타임루프 게임의 시간 관리 및 동기화 기법
대용량 플레이어 데이터의 효율적인 저장 및 불러오기
Unreal Engine의 Replication 시스템 이해
C++와 Blueprint의 효과적인 연동 방법
