---
layout: single
title: "맥OS 에이전트"
excerpt: "맥OS에이전트 설명과 사용법"
header:
  image: /assets/img/swift2.jpg
toc: true
toc_label: "목차"
toc_sticky: true
toc_icon: "tasks"
categories:
  - macos
tags:
  - Swift
  - Daemons
  - Agents
  - macOS
---

# macOS launch Agent?
맥북의 자동화관리 프로그램으로 macOS를 부팅할때 launchd가 자동으로 백그라운드에서 실행시킬 수 있는 모든 프로그램을 관리한다.
예를들어 우리가 흔히 사용하는 보안 프로그램이나 설치된 앱의 업데이트를 관리할 수 있다.

## LaunchDaemons vs LaunchAgents
LaunchDaemons 또한 LaunchAgents와 마찬가지로 지속적으로 실행되는 백그라운드 작업을 수행하는 프로그램이지만 차이점이있다
- LauchAgents는 유저가 로그인 해야지만 실행됩니다, 즉 실행권한이 사용자에게 있습니다
- LauchDaemons는 시스템이 부팅하면 시스템레벨에서 익명으로 백그라운드 작업을 수행합니다.
   예시로 사용자 계정관리, cloud서비스, bluetooth서비스 등이 있습니다.     
- LaunchAgents도 부팅할때 실행되는 프로그램들이있지만 오직 유저가 권한을 수락해야 실행됩니다.

## LauchAgents로 백그라운드에서 지속적으로 실행되는 프로그램을 만들기
### 1. 백그라운드에서 실행할 파이썬 코드를 작성 
launchd_test_script.py 라은 이름으로 텍스트파일을 생성하여 그안에 현재 시간을 기입하는 프로그램
```python
import os
from datetime import datetime 

suffix = datetime.now().strftime('%y%m%d')
title = suffix + '_launchd_test_file.txt'

def createText(title):
    try:
        currentTime = datetime.now().strftime('%X')
        with open(title, 'a') as f:
            f.write(f"current time is {currentTime} and it's working\n")
            f.close()
    except:
        if not os.path.exists(title):
            with open(title, 'w') as f:
                f.write(f"today is {suffix} and it's working")
                f.close()        
        
createText(title)
```
### 2. plist 파일을 생성
- plist?
프로퍼티 리스트(Property list) 파일로 애플에서 사용하는 속성 목록형식의 텍스트 파일. 각종 애플의 운영시스템 macOS, iOS, iPadOS등의 설정 및 데이터를 XML 구조로 저장
plist 파일을 생성할때는 두가지 방법이 있습니다.
#### 방법 1. Xcode에서 생성 : Xcode 아무 프로젝트에서 file -> new -> file -> macOS 탭선택 -> Property List
![image](https://github.com/PeasantJi/peasantji.github.io/assets/120621196/96e17b18-486d-413a-b61a-69b7326ef804)

*Xcode plist 생성*

![image](https://github.com/PeasantJi/peasantji.github.io/assets/120621196/7161dd42-9ef8-4416-92d0-34f81bcac210) 

*plist 작성 후 xcode에서 실행한 plist*


#### 방법 2. text editor나 다른 IDE에서 작성(vc code사용) : vc code에서 file -> new text file -> 아무제목.plist
![image](https://github.com/PeasantJi/peasantji.github.io/assets/120621196/077b0c7a-2755-41cb-a4ec-ecb2c79e9682)
vc code에서 작성된 plist

- 어떤 방법도 상관없지만 xcode를 사용하면 오타로 발생되는 실수를 줄일 수 있음

### 3. 생성한 plist 파일을 LaunchAgents 경로에 붙여넣기
![image](https://github.com/PeasantJi/peasantji.github.io/assets/120621196/554117e4-6e4e-4749-9303-23c47295c2c9)
LaunchAgents 경로

- Library 경로는 두곳이 존재하며 Users안의 user이름 -> Library -> LaunchAgents 붙여넣기
- plist를 붙여넣으면 알림이 뜨는데 login Items에 파이썬실행을 허락할 것인지 토글로 선택
### 4. 터미널실행
>launchctl load -w /Users/유저이름/Library/LaunchAgents/제목.plist 
### 5. 자동화 수행 종료
>launchctl unload -F /Users/유저이름/Library/LaunchAgents/제목.plist  
### 6. 실행 결과물 
![image](https://github.com/PeasantJi/peasantji.github.io/assets/120621196/d7a682ef-1f8f-49ba-8d5f-347d7a4dd673)

*30초 마다 작성된 결과물*
