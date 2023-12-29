# Arm 어셈블리 명령어 정리

* C(Carry) : 덧셈의 결과가 $2^32$ 로 

## 목차
| 목차 링크 | 명령어 |
| :-: | :-: |
| [어셈블리 명령어의 기본 형식 ](#어셈블리-명령어의-기본-형식) | MOV, MVN |
| [Move 명령어](#move-명령어) | MOV, MVN |
| [산술 명령어](#산술-명령어)   | MOV, MVN |
| [비트 시프트 명령어](#비트-시프트-명령어)  | MOV, MVN |
| [논리 비트 명령어](#논리-비트-명령어) | MOV, MVN |


1. [어셈블리 명령어의 기본 형식 ](#어셈블리-명령어의-기본-형식)adfa  
2. [Move 명령어](#move-명령어)  
3. [산술 명령어](#산술-명령어)  
4. [비트 시프트 명령어](#비트-시프트-명령어)  
5. [논리 비트 명령어](#논리-비트-명령어)  

## 어셈블리 명령어의 기본 형식
```swift
'OP CODE' <Rd>, <Rn>, <Rm>
            ┃     ┗━━━━┛
            ┃   명령어를 실행
            ┃        ┃
            ┗━━━━━━ 저장 
```
* &lt;Rd&gt; (Register Destination) : 결과를 저장할 레지스터. 연산 결과를 저장하거나 데이터를 로드할 때 사용
* &lt;Rn&gt; (Register Operand 1) : 첫 번째 소스 레지스터. 보통 연산의 왼쪽 피연산자로 사용됩니다.
* &lt;Rm&gt; (Register Operand 2) : 두 번째 소스 레지스터. 보통 연산의 오른쪽 피연산자로 사용됩니다.

## Move 명령어
| 명령어 | 약자 | 설명 | 예시 | 동작 |
| :-: | :---| :------ | :------ | :------ |
| MOV | Move | • 레지스터에 상수 설정 </br> • 레지스터 간 데이터 복사 | • MOV R0, #7 </br> • MOV R0, R13 | • R0 레지스터에 7을 저장 </br> • R0 레지스터에 R13 레지스터의 값을 이동 |
| MVN | Move NOT | • 오퍼랜드의 값에 '비트 NOT' 연산을 </br>수행한 결과를 레지스터에 저장 | • MVN R0, #7 | • R0 레지스터에 0xFFFF_FFF8(~7)을 저장 |

## 산술 명령어
| 명령어 | 약자 | 설명 | 예시 | 동작 |
| :-: | :---| :------ | :------ | :------ |
| ADD | Add | • 레지스터 간 데이터 덧셈 | • ADD R0, R1, #7 </br> • ADD R0, R1, R13 | • R0 = R1 + 7 </br> • R0 = R1 + R13 |
| ADC | Add with Carry | • 캐리와 함께 레지스터 간 데이터 덧셈 | • ADD R0, R1, #7 </br> • ADD R0, R1, R13 | • R0 = R1 + 7 + 캐리 </br> • R0 = R1 + R13 캐리 |
| SUB | Subtract | • 레지스터 간 데이터 뺄셈 | • SUB R0, R1, #7 </br> • SUB R0, R1, R13 | • R0 = R1 - 7 </br> • R0 = R1 - R13 |
| SBC | Subtract with Carry | • 캐리와 함께 레지스터 간 데이터 뺄셈 | • SBC R0, R1, #7 </br> • SBC R0, R1, R13 | • R0 = R1 - 7 - (~캐리)</br> • R0 = R1 - R13 - (~캐리) |
| RSB | Reverse Subtract | • 오퍼랜드의 순서를 바꿔서 뺄셈 연산 | • RSB R0, R1, #7 </br> • RSB R0, R1, R13 | • R0 = 7 - R1 </br> • R0 = R13 - R1 |
| RSC | Reverse Subtract </br> with Carry | • 캐리를 적용해</br> 오퍼렌드의 순서를 바꿔서 뺄셈 연산 | • RSC R0, R1, #7 </br> • RSC R0, R1, R13 | • R0 = 7 - R1 - (~캐리) </br> • R0 = R13 - R1 - (~캐리)|

## 비트 시프트 명령어
| 명령어 | 약자 | 설명 | 예시 | 동작 |
| :-: | :---| :------ | :------ | :------ |
| LSL | Logical Shift Left | • 왼쪽으로 비트를 이동 </br> (빈 자리는 0으로 채워짐) | • LSL R0, R1, R2 | • R0 = R1 << R2 |
| LSR | Logical Shift Right | • 오른쪽으로 비트를 이동 </br> (빈 자리는 0으로 채워짐) | • LSR R0, R1, R2 | • R0 = R1 >> R2 |
| ASR | Arithmetic Shift Right | • 오른쪽으로 비트를 이동 </br> (최상위 비트(부호 비트)를 유지) | • LSR R0, R1, R2 | • R0 = R1 >>> R2 |
| ROR | Rotate Right | • 오른쪽으로 비트를 회전 </br> (최상위 비트가 최하위 비트로 이동) | • ROR R0, R1, R2 | • Rd = R1를 R2만큼 </br> 오른쪽으로 Rotate한 결과 |

## 논리 비트 명령어
| 명령어 | 약자 | 설명 | 예시 | 동작 |
| :-: | :---| :------ | :------ | :------ |
| AND | AND | • 비트 AND 연산 | • AND R0, R1, R2 | • R0 = R1 AND R2 |
| ORR | OR | • 비트 OR 연산 | • ORR R0, R1, R2 | • R0 = R1 OR R2 |
| ORN | OR NOT | • 비트 OR NOT 연산 | • ORN R0, R1, R2 | • R0 = R1 OR ~R2 |
| EOR | Exclusive OR | • 비트 Exclusive OR 연산 | • EOR R0, R1, R2 | • R0 = R1 EOR R2 |
| BIC | Bit Clear | • 비트 클리어 연산 | • BIC R0, R1, R2 | • R0 = R1 AND ~R2 |


