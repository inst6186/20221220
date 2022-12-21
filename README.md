# 20221220


# CppCheck
## 커맨드라인 실행
```
cppcheck  --enable=all --inconclusive --xml --xml-version=2 src 2> cppcheck.xml
```

## MISRA 분석을 위한 실행
### 사전조건
Python 설치

### Misra_2012.txt 파일 복사
- 위치: C:\DevTools\misra

### 설정 파일 생성: misra.json
- 위치: C:\DevTools\misra
- 파일 구성
```
{
    "script": "misra.py",
    "args": [
        "--rule-texts=C:\\DevTools\\misra\\Misra_2012.txt"
    ]
}
```

### 실행명령
```
cppcheck.exe --addon="C:\DevTools\misra\misra.json"  --xml --xml-version=2 . 2> cppcheck.xml
```

## Doxygen
### 명령줄 실행
```
"c:\Program Files\doxygen\bin\doxygen.exe" Doxyfile
```

### HTML 결과가 Jenkins에서 제대로 표시 안될 때
- CSS 적용 기본 값 변경 방법
- Jenkins 관리 -> Script Console 이동
- 다음 명령 실행
```
System.setProperty("hudson.model.DirectoryBrowserSupport.CSP", "")
```

# Lizard
## 설치
```
pip install lizard
```

## 명령줄 실행 명령
```
lizard.exe -C 10 --csv > lizard_result.csv
```

![image](https://user-images.githubusercontent.com/8405564/208821320-26f0c90f-7f4d-43ba-b7ac-5c86c2852a82.png)


## Jenkins 실행 명령
```
lizard ./src -C 10 -L 80 --xml > lizard.xml
```
or
```
"C:\Users\cypark\AppData\Local\Programs\Python\Python310\Scripts\lizard" ./src -C 10 -L 80 --xml > lizard.xml
```


# CPD
### 명령줄 실행
```
cpd.bat --minimum-tokens 100 --files . --language cpp --format csv > result.csv
```

## Jenkins 실행 명령
```
C:\DevTools\pmd\bin\cpd --minimum-tokens 100 --files src --language cpp --format xml > cpd.xml || exit 0
```

# 실습
## 소스코드 위치
https://github.com/curl/curl

## 구성
- 빌드: dir
- Cppcheck
- CPD: Tocken 50
- Lizard

실행 -> 결과 정상 표시까지.
