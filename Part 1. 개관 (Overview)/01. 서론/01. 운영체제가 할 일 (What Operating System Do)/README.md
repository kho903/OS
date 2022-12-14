# 1.1 운영체제가 할 일
- 컴퓨팅 시스템은 네 가지 구성요소 하드웨어, 운영체제, 응용 프로그램 및 사용자로 구분 가능
- 하드웨어는 중앙 처리 장치 (CPU), 메모리 및 입출력 (I/O) 장치로 구성되어, 기본 계산용 자원 제공
- 응용프로그램인 워드, 스프레드 시트, 컴파일러, 웹 브라우저 등은 사용자의 계산 문제 해결 위해 이들 자원이 어떻게 사용될지 정의
- 운영체제는 다양한 사용자를 위해 다양한 응용 프로그램 간의 하드웨어 사용을 제어하고 조정
- 그리고, 우리는 컴퓨터 시스템이 하드웨어, 소프트웨어 및 데이터로 구성되어 있다고 볼 수 있따. 운영체제는 컴퓨터 시스템이 동작할 때 이들 자원을 적절하게 사용할 수
있는 방법을 제공한다. 따라서, 정부(government)와 유사하다고 볼 수 있는데, 정부처럼 그 자체로는 유용한 기능을 수행하지 못한다. 단순히 다른 프로그램이 유용한 작업을
할 수 있는 환경 제공.

## 1.1.1 사용자 관점 (User View)
- 컴퓨터에 대한 사용자의 관점은 사용되는 인터페이스에 따라 달다진다. 주로 랩톱, 모니터, 키보드, 마우스로 구성된 PC 앞에서 작업하는데, 이러한 시스템은 한 사용자가
자원을 독점하도록 설계되었으며 목표는 사용자가 수행하는 작업을 최대화하는 것
- 이러한 경우 대부분 사용의 용이성을 위해 설계되고 성능에 약간 신경을 쓰고 다양한 하드웨어와 소프트웨어 자원이 어떻게 공유되느냐의 자원의 이용에는 전혀 신경을 쓰지
않는다.
- 스마트폰, 태블릿과 같은 모바일 장치(일부 사용자의 데스크톱 및 랩탑 컴퓨터 시스템을 대체하는)와 상호작용하는 사용자가 늘어난다. 이러한 장치는
일반적으로 셀룰러 또는 기타 무선 기술로 네트워크에 연결됨. 인터페이스는 화면에서 손가락을 누르고 스와이프하여 상호 작용하는 터치스크린이 특징이다.
또한, Apple의 Siri 같은 음성 인식 인터페이스를 통해 상호 작용 할 수 있다.
- 일부 컴퓨터는 사용자 관점이 없다. 예를 들어, 가전제품이나 자동차 내의 내장형(임베디드) 컴퓨터는 숫자 키패드를 가지고, 상태 표시등을 켜고 끌
수 있지만, 이들 컴퓨터나 운영체제와 응용 프로그램은 사용자의 개입 없이 작동하도록 설계되어 있다.

## 1.1.2 시스템 관점 (System View)
- 컴퓨터 관점에서 운영체제는 하드웨어와 가장 밀접하게 연관된 프로그램.
- 따라서, 우리는 운영 체제를 자원 할당자(resource allocator)로 볼 수 있다. 문제를 해결하기 위해 요구되는 여러 자원들(하드웨어, 소프트웨어),
즉, CPU 시간, 메모리 공간, 저장장치 공간, 입출력 장치 등을 가진다. 운영체제는 이들 자원의 관리자로서 동작.
- 서로 상충되는 많은 요청이 있으므로, 운영체제는 컴퓨터 시스템을 효율적이고 공정하게 운영할 수 있도록 어느 요청에
자원을 할당할지 정해야 한다.
- 운영체제에 대한 서로 다른 관점은 여러 입출력 장치와 사용자 프로그램을 제어할 필요성을 강조. 
- 운영체제는 제어 프로그램(control program)이다. 제어 프로그램은 컴퓨터의 부적절한 사용과 오류를 방지하기 위해 사용자 
프로그램의 수행을 제어한다. 특히 입출력 장치의 제어와 동작에 깊이 관여한다.

## 1.1.3 운영체제의 정의
- 컴퓨터의 설계와 용도가 수없이 많아 운영 체제가 많은 역할과 기능을 수행한다.
- 다양성을 위해 컴퓨터의 역사를 알아야 한다. 짧지만 급격하게 발전해 왔다. 컴퓨팅은 수행할 수 있는 작업을 결정하기 위한 실험으로 
시작되었으며 암호 해독 및 탄도 계산과 같은 군사 용도와 인구 조사 계산과 같은 정부 업무 등의 고정 목적 시스템으로 빠르게 이동하였다.
- 이러한 초기 컴퓨터는 범용 다기능대형 컴퓨터로 발전하였고, 이 때 운영체제게 탄생하였다.
- 1960년대 무어의 법칙은 집적회로의 트랜지스터의 수가 18개월마다 2배로 증가할 것이라고 예측했고, 지켜져왔다. 컴퓨터는 기능면에서 향상되고
크기가 축소되어 수많은 용도와 다양한 운영체제로 이어졌다.
- 일반적으로 운영체제에 대한 적절한 정의는 없다. 운영체제는 유용한 컴퓨팅 시스템을 만드는 문제를 해결할 수 있는 합리적인 방법을 제공하기
때문에 존재한다.
- 컴퓨터 시스템의 기본 목표는 프로그램 실행, 사용자 문제 쉽게 해결이다. 하드웨어는 이 목표를 위해 구성된다. 하드웨어만으로는 사용하기 쉽지 않기
때문에 응용 프로그램이 개발된다. 이러한 프로그램에는 입출력 장치 제어와 같은 특정 공통 작업이 필요. 자원을 제어하고 할당하는 일반적인 기능은
운영체제라는 하나의 소프트웨어로 통합된다.
- 또한 운영 체제에 포함되는 요소에 보편적인 정의는 없다. 단순한 관점은 "운영체제"를 주문할 때 공급 업체가 제공하는 모든 것을 포함한다는 것이다.
그러나 포함된 기능은 시스템에 따라 크게 달라 일부는 메가바이트 미만의 전체 화면 편집기가 없고, 어떤 시스템은 기가 바이트 공간에 그래픽 윈도 시스템을
기반으로 한다. 보다 일반적인 정의는 운영 체제가 컴퓨터에서 항상 실행되는 프로그램 (보통 커널이라 함)이다. 커널과 함께 두 가지 다른 유형의 프로그램이
있다. 운영체제와 관련되어 있지만 반드시 커널의 일부는 아닌 시스템 프로그램과 시스템 작동과 관련되지 않은 모든 프로그램을 포함하는 응용 프로그램이다.
- 개인용 컴퓨터가 널리 보급되고 운영 체제가 점점 정교해짐에 따라 운영체제의 구성요소가 더 중요해졌다. 1998년 미국 법무부는 Microsoft가
운영체제에 너무 많은 기능을 포함하여 응용 프로그램 공급 업체의 경쟁을 막았다고 주장하면서 소송을 제기했다. 결과적으로 Microsoft는 경쟁을
제한하기 위해 운영 체제 독점에 유죄 판결을 받았다.
- 그러나 오늘날 모바일 운영체제를 보면, 구성하는 기능이 다시 증가하고 있음을 알 수 있따. 종종 핵심 커널 뿐만아니라 미들웨어 (응용 프로그램
개발자에게 추가 서비스를 제공하는 소프트웨어 프레임워크)도 포함된다. 예를 들어 Apple iOS 및 Google Android는 각각 데이터베이스,
멀티미디어 및 그래픽을 지원하는 미들웨어와 함께 핵심 커널을 갖추고 있다.
- 요약하면, 운영체제는 항상 실행 중인 커널, 응용프로그램 개발을 용이하게 하는 미들웨어 프레임워크 및 실행 중에 시스템 관리하는 데 도움이 되는
시스템 프로그램이 포함됨. 


