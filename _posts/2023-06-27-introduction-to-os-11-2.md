---
layout:       post
title:        "chapter 11-2. 디렉터리의 구조."
author:       "yunki kim"
header-style: text
catalog:      true
tags:
- 도서
- OS
- 쉽게 배우는 운영체제
- ComputerScience
---

# 디렉터리의 개념
디렉터리는 관련 있는 파일을 하나로 모아놓은 곳입니다. 하나의 디렉터리 내에는 한 개 이상의 파일과 한 개 이상의 자식 디렉터리(sub directory)를 가질 수 있습니다. 디렉터리는 여러 층으로 구성되어 있고 최상위 층의 디렉터리를 root directory라 부릅니다.
# 디렉터리 파일
디렉터리도 파일입니다. 일반 파일에는 데이터가 담겨 있고 디렉터리에는 파일 정보다 담겨 있습니다. 디렉터리의 헤더에는 디럭터리의 이름, 만든 시간, 접근 권한 등 정보가 기록되어 있습니다.
디렉터리 헤더는 디렉터리 정보가 시작하는 위치를 가리킵니다. 디렉터리에는 '.'과 '..'이 존재하는데 '.'는 자신의 디렉터리를, '..'는 상위 디렉터리를 가리킵니다. 루트 디렉터리의 예는 다음과 같습니다.
![root directory](/img/2023-06-27-introduction-to-os-11-2/img.png)
# 경로
경로는 파일이 전체 디럭터리 중 어디에 있는지를 나타냅니다. 같은 경로에 존재하는 파일 이름은 모두 고유합니다. 루트 디렉터리를 기준으로 파일 위치를 나타내는 방식을 절대 경로(absolute path)라고 하고 현재 위치를 기준으로 파일 위치를 표기하는 것을 상대 경로(relative path)라고 합니다.
# 디렉터리 구조
초기 파일 시스템의 디렉터리는 1단계 구조였습니다. 당시에는 파일이 많지 않아서 많은 디렉터리가 필요하지 않았기 때문에 구조가 단순했습니다. 1 단계 디렉터리 구조에서는 루트 디렉터리에 새로운 디렉터리를 만들 수 있지만 디렉터리 안에 자식 디렉터리를 만들 수 없습니다.
![1 level directory structure](/img/2023-06-27-introduction-to-os-11-2/img_1.png)
파일이 많아지면서 다단계 디렉터리 구조가 등강했습니다. 다단계 디렉터리 구조는 루트 디렉터리를 시작점으로 트리 형태를 하고 있습니다. 때문에 트리 디렉터리 구조라고도 합니다. 다단계 디렉터리 구조는 단계 확장에 제약이 없고 디렉터리에 파일과 자식 디렉터리를 모두 저장할 수 있습니다.
![multi level directory structure](/img/2023-06-27-introduction-to-os-11-2/img_2.png)
트리는 순환이 없는 그래프라고도 불리지만 현대 디렉터리 구조에는 순환이 있습니다. 디렉터리와 디렉터리를 연결하는 링크가 존재하기 때문이다. 예컨대 윈도우의 바로 가기는 다른 디렉터리로 바로 이동하는 기능을 제공합니다.
# 마운트
파티션은 논리적인 디스크 분할로, 한 개 이상의 디스크를 파티션으로 나누어 사용할 수 있습니다. 윈도우에서 각 파티션이 따로 보이는데, 이는 파티션마다 파일 테이블이 따로 존재하기 때문입니다. 
윈도우는 초기에 FAT16 파일 시스템을 사용했습니다. FAT16의 최대 디스크 크기는 32GB여서 그보다 큰 디스크를 사용하면 어쩔 수 없이 파티션을 나누어서 서로 다른 파일 테이블을 사용해야 했습니다.
반면 유닉스는 서버용으로 만들어진 운영체제이므로 파일 테이블 크기에 제한이 없습니다. 또 한, 하나의 파일 테이블로 여러 개의 디스크나 파티션을 통합해 관리할 수 있습니다. 마운트는 여러 개의 파티션을 통합하는 명령어입니다. 마운트를 통해 파티션을 하나로 합친 뒤 합친 디렉터리로 이동하면 실제로는 다른 파티션으로 넘어가지만 사용자는 이를 알아차리지 못합니다. 