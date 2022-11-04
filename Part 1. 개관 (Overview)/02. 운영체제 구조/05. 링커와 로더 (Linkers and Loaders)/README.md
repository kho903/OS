# 2.5 링커와 로더 (Linkers and Loaders)
- 일반적으로 프로그램은 디스크에 이진 실행 파일(예 : a.out 또는 prog.exe)로 존재한다. CPU에서 실행하려면 프로그램을 메모리로 가져와 프로세스 컨텍스트에 배치해야 한다.
이 절에서는 프로그램을 컴파일하고 메모리에 배치하여 사용 가능한 CPU 코어에서 실행할 수 있게 되기까지의 이러한 절차를 단계별로 살펴보자.
- 소스 파일은 임의의 물리 메모리 위치에 적재되도록 설계된 오브젝트 파일로 컴파일된다. 이러한 형식을 재배치 가능 오브젝트 파일이라고 한다. 다음으로 링커는 이러한 재배치 가능
오브젝트 파일을 하나의 이진 실행 파일로 결합한다. 링킹 단계에서 표준 C 또는 수학 라이브러리(플래그 -lm으로 지정)와 같은 다른 오브젝트 파일 또는 라이브러도 포함될 수 있다.
- 로더는 이진 실행 파일을 메모리에 적재하는 데 사용되며, CPU 코어에서 실행될 수 있는 상태가 됨. 링크 및 로드와 관련된 활동은 재배치로, 프로그램 부분에서 최종 주소를 할당하고
프로그램 코드와 데이터를 해당 주소와 일치하도록 조정하여 프로그램이 실행될 떄 코드가 라이브러리 함수를 호출하고 변수에 접근할 수 있게 한다. 로더를 실행하려면 명령어 라인에 실행
파일의 이름을 입력하기만 하면 된다. UNIX 시스템 (예 : ./main)의 명령어 라인에 프로그램 이름을 입력하면 셸은 먼저 fork() 시스템 콜을 사용하여 프로그램을 실행하기 위한
새 프로세스를 생성한다. 그런 다음 셸은 exec() 시스템 콜로 로더를 호출하고, exec()에 실행 파일 이름을 전달한다. 그런 다음 로더는 새로 생성된 프로세스의 주소 공간을 사용하여
지정된 프로그램을 메모리에 적재한다. GUI 인터페이스를 사용하는 경우, 실행 파일과 연관된 아이콘을 두 번 클릭하면 유사한 메커니즘을 사용하여 로더를 호출한다.
- 이 과정에서는 모든 라이브러리가 실행 파일에 링크되어 메모리에 적재된다고 가정한다. 실제로 시스템 대부분에서는 프로그램이 적재될 때, 라이브러리를 동적으로 링크할 수 있게 된다.
예를 들어, Windows는 동적 링킹 라이브러리(dynamically linked library, DLL)을 지원한다. 이 방법의 장점은 실행 파일에서 사용되지 않을 수 있는 라이브러리를 링크하고 
로드하지 않아도 된다는 것이다. 대신 라이브러리는 조건부로 링크되며 프로그램 실행 시간에 필요한 경우 적재된다. 예를 들어, math 라이브러리는 실행 파일 main에 링크되어 있지
않다. 대신 링커는 프로그램이 적재될 때 동적으로 링크되고 적재될 수 있도록 재배치 정보를 삽입한다. 여러 프로세스가 동적으로 링크된 라이브러리를 공유할 수 있어, 메모리 사용이
크게 절약될 수 있음을 알 수 있다.
- 오브젝트 파일과 실행 파일은 일반적으로 표준화된 형식을 가진다. 이 표준 형식은 컴파일된 기계 코드 및 프로그램에서 참조되는 함수 및 변수에 대한 메타데이터를 포함하는 기호
테이블을 포함한다. UNIX 및 Linux 시스템의 경우 이 표준 형식을 ELF (Executable and Linkable Format)라고 한다. 재배치 기능 파일과 실행 파일 각각을 위한 별도의
ELF 형식이 사용된다. 실행 가능 파일의 ELF 파일의 정보 중 하나는 프로그램의 시작점이며, 프로그램을 실행할 때, 실행할 첫 번째 명령어의 주소가 저장되어 있다. Windows 시스템은
PE (Portable Executable) 형식을 사용하고 macOS 는 Mach-O 형식을 사용한다.

## ELF 형식
- Linux는 ELF 파일을 식별하고 분석하기 위한 다양한 명령을 제공한다. 예를 들어, file 명령은 파일 유형을 결정한다. main.o 가 오브젝트 파일이고 main 이 실행 파일인
경우 명령 `file main.o`는 main.o 가 ELF 재배치 가능 파일이라고 보고하며, 명령 `file main`은 main이 ELF 실행 파일이라고 보고한다. ELF 파일은 여러 섹션으로
구분되며 readelf 명령을 사용하여 분석할 수 있다.




Object files and executable files typically have standard formats that
include the compiled machine code and a symbol table containing metadata
about functions and variables that are referenced in the program. For UNIX
and Linux systems, this standard format is known as ELF (for Executable
and Linkable Format). There are separate ELF formats for relocatable and
executable files. One piece of information in the ELF file for executable files is
the program’s entry point, which contains the address of the first instruction
to be executed when the program runs. Windows systems use the Portable
Executable (PE) format, and macOS uses the Mach-O format.