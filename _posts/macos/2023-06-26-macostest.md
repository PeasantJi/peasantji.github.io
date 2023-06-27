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
- LauchDaemons는 시스템이 부팅하면 시스템레벨에서 익명으로 백그라운드 작업을 수행합니다.  예로는 사용자 계정관리, cloud서비스, bluetooth서비스 등이 있습니다.     
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
  
### 3. 생성한 plist 파일을 LaunchAgents 경로에 붙여넣기
### 4. 터미널실행
### 5. launchctl load -w /Users/ji/Library/LaunchAgents/com.jisung.test.plist 
### 6. 자동화 수행 종료
### 7. launchctl unload -F /Users/ji/Library/LaunchAgents/com.jisung.test.plist 
