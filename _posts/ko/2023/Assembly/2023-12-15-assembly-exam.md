---
title: Assembly -  Writing 'Hello, World!' in Assembly Language using NASM and GCC
author_profile: true
read_time: true
comments: true
share: true
related: true
categories:
- Assembly
tags:
- Assembly
toc: true
toc_sticky: true
toc_label: 목차
description: Assembly 실습
article_tag1: assembly
article_tag2: nasm
article_tag3: gcc
article_section: Assembly
meta_keywords: assembly
last_modified_at: '2023-12-15 21:00:00 +0800'
---

# 어셈블리 언어를 알아보기 앞서서

어셈블리 언어에 대해서 공부하면, 컴퓨터에 대해 더욱 이해할 수 있을까 하여, 한번 실습해보기로 하였다.

이 실습 과정을 통해 NASM, GCC에 대해 이해하고, 어셈블리 언어로 작성한 파일이 어떻게 실행파일로 변환되고 실행되는지 과정을 이해해본다.

우선, 나의 PC 아키텍처에 맞는 기계어 코드에 직접적으로 대응하는 어셈블리 언어가 무엇인지 알아야되었다. 나의 PC 환경은 Windows 10이며, 프로세서는 64비트이다.이 환경에 맞는 어셈블러는 NASM 가 있어서, 이것을 선택하였다. 그리고 gcc로 컴파일해보기로 하였다.


# 어셈블리?

"어셈블리(Assembly)"는 컴퓨터 과학 및 프로그래밍에서 사용되는 용어로, 저급 언어(low-level language)에 속하는 프로그래밍 언어를 가리킨다. 어셈블리 언어는 사람이 이해하기 쉽도록 기계어 명령어를 텍스트 기반으로 표현한 언어로, 주로 특정 컴퓨터 아키텍처의 기계 코드를 생성하기 위해 사용된다.

어셈블리 코드는 CPU의 명령어 세트와 밀접하게 관련되어 있으며, 프로그래머는 어셈블리 언어를 사용하여 특정 하드웨어 아키텍처에서 직접적으로 작업할 수 있다.

주로 하드웨어 제어, 성능 최적화, 임베디드 시스템, 운영 체제 커널, 드라이버 등의 시스템 프로그래밍과 관련된 작업에서 사용된다.

# 어셈블리 언어로 코딩해서 할 수 있는 것들은?

(1) 시스템 수준 프로그래밍:

어셈블리 언어는 운영 체제, 부트로더, 커널 모듈 개발과 같은 시스템 수준 프로그래밍에 자주 사용된다.

(2) 임베디드 시스템 개발:

어셈블리는 하드웨어 리소스에 대한 직접적인 제어가 필요한 임베디드 시스템 프로그래밍에 매우 중요하다. 여기에는 마이크로컨트롤러용 펌웨어 개발과 같은 작업이 포함된다.

(3) 장치 드라이버:

어셈블리 언어는 운영 체제와 하드웨어 장치 간의 통신을 가능하게 하는 소프트웨어 구성 요소인 장치 드라이버 개발에 일반적으로 사용된다.

# NASM, GCC란?

## NASM 
NASM은 Netwide Assembler의 약자로, x86 아키텍처를 위한 어셈블리 언어로 사용되는 어셈블러이다. **어셈블러**는 어셈블리 언어로 작성된 소스 코드를 **기계어**로 변환하는 역할을 한다.

## GCC
GCC는 GNU Compiler Collection의 약자로, 여러 언어를 지원하는 **컴파일러** 집합이다. 주로 C, C++, Fortran 등의 언어를 지원하며, 여러 플랫폼에서 실행 가능한 기계어 코드로 소스 코드를 컴파일하는 데 사용된다. gcc는 여러 프로그래밍 언어에 대한 풍부한 기능을 제공하며, 많은 리눅스 시스템과 다른 플랫폼에서 표준 컴파일러로 사용된다.

이 두 도구는 프로그래밍 및 컴파일 과정에서 중요한 역할을 한다. 특히, 어셈블러는 어셈블리 코드를 생성하고, 컴파일러는 고수준 언어로 작성된 소스 코드를 **기계어**로 변환한다.


## 코드 작성 및 실행 순서

어셈블리 언어로 코드를 작성한다. 이 코드는 "hello world"를 출력한다.
이 코드가 작성된 파일은 .asm 확장자로 되어있다.

(1) Assembling (어셈블링)

 어셈블링은 사람이 읽을 수 있는 어셈블리 코드를 -> 기계가 읽을 수 있는 개체 코드로 변환하는 과정이다.
이때, NASM(Netwide Assembler) 와 같은 어셈블러에 의해 변환 작업을 수행된다.

어셈블러를 사용하면 어셈블리 코드 파일(.asm)을 처리하여, 개체 파일(.obj)을 생성한다. 
개체 파일은 일반적으로 Unix 계열 시스템(Linux)에서는 .o 확장자를 가지며 Windows에서는 .obj 확장자를 갖다.

> hello_world.asm -> hello_world.obj

(2) Linking (링킹)

 링킹이란 어셈블러에서 생성된 객체 코드(.obj)와 필요한 다른 객체 코드를 결합하여 실행 파일(.exe)을 만드는 과정이다.

> hello_world.obj -> hello_world.exe

(3) 실행 

위 과정을 통해 실행 파일(.exe)이 생성되면, 실행해본다.


### 순서 요약

- 텍스트 파일(예: hello_world.asm)에 어셈블리 코드를 작성한다.
- NASM(nasm -f win64 -o hello_world.obj hello_world.asm)을 사용하여 코드를 어셈블하여 객체 파일을 생성한다.
- 개체 파일을 GCC(gcc -o hello_world.exe hello_world.obj)와 같은 컴파일러와 연결하여 실행 파일을 만든 다음 실행한다.


## 이러한 과정이 필요한 이유

### (1) 모듈화 및 재사용:

프로그램이 여러 개의 소스 파일로 구성되어 있을 때, 각 소스 파일을 개별적으로 어셈블하여 목적 파일로 만들 수 있다. 이렇게 하면 코드를 모듈화하고 재사용할 수 있다. 목적 파일은 해당 모듈의 기계어 코드와 관련된 정보를 가지고 있다.

### (2) 라이브러리와 외부 의존성:

프로그램이 외부 라이브러리를 사용할 경우, 해당 라이브러리의 목적 파일이나 라이브러리 파일이 필요한다. 링크 단계에서 이러한 외부 의존성을 해결하여 실행 파일에 필요한 모든 코드와 데이터를 통합한다.

### (3) 주소 해결 및 최적화:

링크 단계에서는 주소를 할당하고, 심볼들 간의 참조 관계를 해결하여 최종적인 실행 파일을 생성한다. 또한 여러 목적 파일의 코드와 데이터를 통합하면서 최적화 작업도 수행할 수 있다.
이러한 과정을 통해 목적 파일과 최종 실행 파일 간의 추상화를 유지하면서, 대규모 프로젝트를 효과적으로 관리하고 여러 모듈 간에 재사용성을 확보할 수 있다.


## 필요한 도구들 설치하기

### (1) nasm 다운로드, 설치

mingw-w64-install.exe 파일을 다운받아서 설치한다.

> mingw-w64-install.exe

- 다운로드 링크

https://www.nasm.us/

https://www.nasm.us/pub/nasm/releasebuilds/2.16rc12/win64/

### nasm, 환경 변수 설정

> C:\Users\hong\AppData\Local\bin\NASM


### (2) gcc 다운로드, 설치

MinGW-W64 파일을 다운받아서 설치한다.

> mingwInstaller.exe

- 다운로드 링크
https://sourceforge.net/projects/mingw-w64/
https://www.mingw-w64.org/downloads/#mingw-builds

https://github.com/niXman/mingw-builds-binaries


### gcc, 환경 변수 설정

>  C:\Users\hong\mingw64\bin

### 확인

>  $ gcc --version 


## 파일 변환하기

### 명령어

### nasm

> $ nasm -f win64 -o hello_world.obj hello_world.asm

### gcc

> $ gcc -o hello_world.exe hello_world.obj -luser32 -lkernel32 -lmsvcrt -nostartfiles -Wl,--build-id=none

-o 옵션은 생성해야 하는 출력 파일을 의미한다.

## 생성된 파일

### nasm

hello_world.asm -> hello_world.obj

### gcc

hello_world.obj -> hello_world.exe



## NASM 코드의 기본 구조

NASM(Netwide Assembler) 코드는 일반적으로 지시문(directives) 및 지침(instructions)과 함께 데이터 및 텍스트 섹션을 포함하는 구조를 따른다. NASM 코드의 기본 구조는 다음과 같다.

### 1. 섹션 선언:

NASM 코드는 주로 데이터용 .data와 코드용 .text 섹션으로 구분된다.

```asm
section .data
; Data declarations go here

section .text
; Code goes here
```

### 2. 데이터 섹션:

.data 섹션은 변수와 상수를 선언하는 데 사용된다.

section .data
variable_name db 10  ; Declare a byte variable with initial value 10

### 3. 텍스트 섹션:

.text 섹션에는 실제 어셈블리 지침이 포함되어 있다.

```asm
section .text
global _start  ; Entry point for the program
_start:
    ; Assembly instructions go here
```

### 4. 글로벌 선언:

global 지시문은 다른 모듈이나 프로그램에서 액세스할 수 있는 기호를 선언한다.

```asm
global _start
```

### 5. 라벨 및 지침:

라벨은 코드에서 위치를 표시하는 데 사용되며 명령어는 CPU가 수행하는 실제 작업이다.

```asm
_start:
    mov eax, 1  ; Move the value 1 into the eax register
```

### 6. 지침:

지시문은 코드 처리 방법에 대한 추가 정보를 어셈블러에 제공한다.

```asm
section .data
msg db 'Hello, World!', 0  ; Null-terminated string
```

### 7. 코멘트:

주석은 세미콜론(;)으로 시작하며 문서화에 사용된다.

```asm
; This is a comment
mov eax, 1
```



## 소스 코드 (hello_world.asm)

- 안되던 코드

```asm
section .data
    hello db 'Hello, World!', 0

section .text
    extern MessageBoxA, ExitProcess
    global _start

_start:
    ; Display the message box
    mov     rdx, hello       ; Message text for MessageBoxA
    xor     rcx, rcx         ; hWnd (null for message box)
    xor     r8d, r8d         ; Caption (null for message box)
    xor     r9d, r9d         ; Flags (OK button)
    call    MessageBoxA

    ; Exit the program
    mov     rcx, 0           ; Exit code 0
    call    ExitProcess
```

- 되는 코드

```asm
section .data
    hello db 'Hello, World!', 0
    format db '%s', 0 ; Format string for printf

section .text
    extern printf, ExitProcess
    global start

_start:
    ; Display the message in the console
    mov rdx, hello ; Message text for printf
    mov rcx, format ; Format string for printf
    call printf

    ; Exit the program
    mov rcx, 0 ; Exit code 0
    call ExitProcess
```


## 코드 설명

```asm
section .data
    hello db 'Hello, World!', 0
    format db '%s', 0 ; Format string for printf
```

### .data 섹션은 데이터를 정의하는 부분이다.

- hello: 'Hello, World!' 문자열을 저장하는 변수로, 문자열 끝에 널 문자(0)가 포함되어 있다.

- format: printf 함수에 전달할 포맷 문자열로, %s는 문자열을 나타낸다.

```asm
section .text
    extern printf, ExitProcess
    global start

_start:
```

### .text 섹션은 코드를 정의하는 부분이다.

- extern 지시어는 프로그램이 외부에서 정의된 함수를 사용한다고 알려준다. 여기서는 printf와 ExitProcess 함수를 외부에서 참조한다.

- global start는 프로그램의 진입점을 _start로 설정한다.

```asm
   ; Display the message in the console
    mov rdx, hello ; Message text for printf
    mov rcx, format ; Format string for printf
    call printf
```

### 이 부분은 콘솔에 "Hello, World!"를 출력하는 역할을 한다.

 - mov rdx, hello는 printf 함수에 전달할 메시지 텍스트의 주소를 rdx 레지스터에 저장한다.

- mov rcx, format는 포맷 문자열의 주소를 rcx 레지스터에 저장한다.

- call printf는 printf 함수를 호출하여 메시지를 출력한다.

```asm
  ; Exit the program
    mov rcx, 0 ; Exit code 0
    call ExitProcess
```

### 이 부분은 프로그램을 종료하는 역할을 한다.

- mov rcx, 0은 종료 코드를 rcx 레지스터에 0으로 설정한다.

- call ExitProcess는 프로그램을 종료하는 함수를 호출한다.



## (추가) obj 파일 안에는 무엇이? (hello_world.obj)

obj 확장자로 된 파일을 열어보면, 이렇게 사람이 알아볼 수 없는 데이터로 보인다.

```
d? ?{e?         .data              d   u           @ 0?text           #   u   ?           P`Hello, World! %s H?       H?       ?   ?   ?                    	       
    .file       ?  ghello_world.asm   .data                           .text          #                .absolut       hello           format         printf                           start              ExitProcess 
```

끝.