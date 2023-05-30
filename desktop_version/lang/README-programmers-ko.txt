=== I N T R O D U C T I O N ===

이 파일에서는 새 문자열을 추가하고 언어 간에 동기화하는 등 VVVVVV 번역을 유지 관리할 때 알아야 할 사항을 설명합니다.



=== A D D I N G   N E W   S T R I N G S ===

게임에 새 텍스트를 추가하려면 일반적으로 코드의 원 문자열을 loc::gettext()로 감싸고(#include "Localization.h"를 추가해야 할 수도 있음) 영어 파일에 동일한 문자열을 추가하기만 하면 번역이 가능하도록 만들 수 있습니다. 새 문자열은 번역기 메뉴를 사용하여 영어에서 다른 모든 언어 파일로 자동 동기화할 수 있습니다.

예를 들어 "Game paused"는 loc::gettext("Game paused")로 변경하여 번역이 가능하도록 만들 수 있습니다. 영어 파일에서 해당 항목은 다음과 같이 표시될 수 있습니다:

    <string english="Game paused" translation="" explanation="pause screen" max="40"/>

max 값은 text에 공백이 몇 자 있는지를 나타내며 아래에 자세히 설명되어 있습니다. single-line text의 경우 "40", multi-line text의 경우 "38*5"와 같이 표시됩니다. max 값을 적용할 수 없거나 정의하기 어려울 수 있으므로 이 속성을 완전히 생략할 수 있습니다. 예를 들어 대각선으로 배치된 메뉴 옵션이거나 조이스틱 메뉴의 낮음/중간/높음과 같이 다른 문자열의 길이에 따라 제한이 달라지거나 문자열이 길어질수록 점점 보기가 나빠지는 경우 등이 이에 해당합니다. 일반적으로 엄격한 제한을 정의하는 것이 오해의 소지가 있는 경우 제한을 지정하지 않을 수 있습니다.



=== E D I T I N G   E X I S T I N G   S T R I N G S ===

이미 번역된 텍스트를 부분적으로 변경해야 하는 경우가 있습니다.

예를 들어 "Press ENTER to stop"라는 문자열을 "Press {button} to stop"으로 변경해야 합니다(해당 단축키를 구성 가능하게 만들었기 때문입니다).

language file에서 단순히 텍스트를 찾아서 바꾸거나 새 문자열을 추가할 때 이전 문자열을 제거하지 마세요. (번역을 유지하든 유지하지 않든 상관없습니다.)

English language file에 문자열을 복제하여 이전 버전 아래에 새 버전을 넣고 이전 버전에 "***OUTDATED***"라는 설명과 함께 표시합니다.

예를 들면 다음과 같습니다:

    <string english="Press ENTER to stop" translation="" explanation="stop super gravitron"/>

        ↓  ↓  ↓

    <string english="Press ENTER to stop" translation="" explanation="***OUTDATED***"/>
    <string english="Press {button} to stop" translation="" explanation="stop super gravitron"/>


게임에서는 더 이상 오래된 문자열을 사용하지 않으며 참조용으로 기존 번역을 전달하기 위해 language files에 남아 있을 뿐입니다. 번역가가 언어 파일을 업데이트하면 이전 번역의 일부를 새 버전의 문자열에 재사용할 수 있습니다.

             english        |           translation           |     explanation
    =================================================================================
       Press ENTER to stop  | Appuyez sur ENTRÉE pour arrêter |    ***OUTDATED*** 
    ---------------------------------------------------------------------------------
     Press {button} to stop |              ? ? ?              | stop super gravitron 


결국 모든 언어가 최신 버전으로 업데이트되면 이러한 오래된 문자열을 정리할 수 있습니다.

물론 문자열을 교체하지 않고 제거할 때는 (영어) 언어 파일에서 문자열을 제거하면 됩니다.



=== T E X T   P R I N T I N G ===

다음은 텍스트 출력 기능입니다:

 font::print(flags, x, y, text, r, g, b)
 font::print(flags, x, y, text, r, g, b, linespacing = -1, maxwidth = -1)

flags 인수는 0이거나 중앙 배치, 확대 등과 같은 작업을 수행하는 flag set일 수 있습니다.

몇 가지 예제(Font.h에서도 찾을 수 있음):

 표준 출력
     font::print(0, 50, 50, "Hello world!", 255, 255, 255);

 텍스트 가운데 정렬
     font::print(PR_CEN, -1, 50, "Hello world!", 255, 255, 255);
     (set X to -1, unless you want to center *around* X)

 2배 확대
     font::print(PR_2X, 50, 50, "V", 255, 255, 255);

 가운데 정렬, 2배 확대
     font::print(PR_CEN | PR_2X, -1, 50, "V", 255, 255, 255);

 오른쪽 정렬, 3배 확대, 테두리(border)
     font::print(PR_RIGHT | PR_3X | PR_BOR, 320, 50, "V", 255, 255, 255);

 워드랩 가운데 정렬
     font::print_wrap(PR_CEN, -1, 50, "Hello world, this will wordwrap to the screen width", 255, 255, 255);

기술적으로 완전하지 않은 모든 플래그 목록(Font.h에 정의됨):

- PR_2X/PR_3X/.../PR_8X  더 큰 크기로 출력(default: PR_1X)
- PR_FONT_INTERFACE      [DEFAULT] 인터페이스(VVVVVV language) font 사용
- PR_FONT_LEVEL          레벨별 font 사용(방 이름, 컷신 등)
- PR_FONT_8X8            어떤 상황에서도 8x8 font 사용
- PR_BRIGHTNESS(value)   0-255의 brightness 사용  (이 값은 알파 효과를 위해 
                         R, G, B와 혼합되어 컬러 glyph를 올바르게 처리합니다)
- PR_BOR                 text를 주위에 검은색 테두리(border) 그리기
- PR_LEFT                [DEFAULT] 텍스트 왼쪽 정렬 / X 좌표에 배치
- PR_CEN                 X를 기준으로 텍스트를 가운데 정렬(X는 가운데) 
                         또는 X == -1인 경우 화면에 맞게 정렬
- PR_RIGHT               text를 X 좌표에 오른쪽 정렬
                         (X 좌표는 이제 왼쪽 테두리가 아닌 오른쪽 테두리입니다)
- PR_CJK_CEN             [DEFAULT] 8x8 font에 비해 큰 font(중국어/일본어/한국어)은 
                         위와 아래로 튀어나오도록 합니다
- PR_CJK_LOW             큰 font는 아래로만 튀어나오도록 합니다
                         (Y좌표에 그림)
- PR_CJK_HIGH            큰 font는 위로만 튀어나오도록 합니다



=== S T R I N G   F O R M A T T I N G ===

sprintf 계열 함수 대신 VVVVVV의 자체 포맷 시스템인 VFormat을 사용하는 것이 좋습니다.

문자열에는 {name} 또는 {name|flags}처럼 보이는 placeholder가 있는 경우가 있습니다. 예를 들어 "{n_trinkets} of {max_trinkets}" 등이 있습니다.

placeholder는 동작을 수정하는 "flags"를 가질 수도 있습니다. 필요에 따라 번역에서 추가하거나 제거할 수 있습니다. flag는 | (pipe)로 구분합니다.

자세한 내용은 VFormat.h 상단의 documentation을 참조하세요.

전체 예시:

 char buffer[100];
 vformat_buf(buffer, sizeof(buffer),
     "{crewmate} got {number} out of {total} trinkets in {m}:{s|digits=2}.{ms|digits=3}",
     "number:int, total:int, crewmate:str, m:int, s:int, ms:int",
     2, 20, "Vermilion", 2, 3, 1
 );

 => "Vermilion got 2 out of 20 trinkets in 2:03.001"



=== T R A N S L A T O R   M E N U ===

번역기 메뉴에는 번역가와 관리자 모두를 위한 옵션이 있으며, 메뉴 테스트, 게임 내 방 이름 번역, 모든 언어 파일을 영어 템플릿 파일과 동기화, 번역 진행률 통계 확인 등이 가능합니다.

아래 하나라도 해당하는 경우 VVVVVV 메인 메뉴에 '번역기' 메뉴가 표시됩니다:
- "lang" 폴더가 data.zip 과 함께 있지 않고, 게임이 "desktop_version" 폴더 내에서 실행되고 있으며, desktop_version/lang 가 있음. 이는 일반적으로 소스에서 게임을 컴파일할 때 발생함;
- 명령줄 인수(또는 실행 옵션)로 "-translator"를 사용
- ALWAYS_SHOW_TRANSLATOR_MENU를 정의해서 컴파일함(Localization.h 상단 참조)

새 문자열을 추가하려면 English strings.xml 또는 strings_plural.xml에만 추가하고, 번역기 메뉴에서 모든 언어를 동기화하는 옵션을 사용하세요. 이렇게 하면 새 문자열이 번역된 모든 언어 파일에 복사됩니다.

language file sync 옵션은 language file에 대한 지원 방식이 다릅니다. 메뉴 자체에 표시된 대로 각 파일을 다음과 같이 처리합니다:

[Full syncing EN→All]
이러한 파일의 경우 영어 버전의 파일이 완전히 복사되어 모든 언어의 버전을 덮어쓰고 기존의 모든 번역 및 사용자 지정이 모든 언어에 대해 삽입됩니다. 즉, 새로 추가된 문자열은 모든 언어에 복사되고, 제거된 문자열은 모든 언어에서 동시에 제거되어 완전히 최신 상태로 유지됩니다.
  - meta.xml
  - strings.xml
  - strings_plural.xml
  - cutscenes.xml
  - roomnames.xml
  - roomnames_special.xml

[Syncing not supported]
이러한 파일은 동기화 기능으로 변경되지 않습니다.
  - numbers.xml



=== F I L E S ===

* meta.xml: 이 파일에는 번역에 대한 몇 가지 일반적인 정보가 포함되어 있습니다.

* strings.xml: 이 파일에는 인터페이스와 게임의 일부에 대한 일반 문자열이 포함되어 있습니다.

* strings_plural.xml: strings.xml과 사용법은 비슷하지만 다른 복수형이 필요한 문자열에 사용됩니다 ("1 trinket", "2 trinkets")

* numbers.xml: 이 파일에는 0에서 100까지의 모든 숫자(영, 하나 등)가 기록되어 있습니다. 또한 이 파일을 사용하면 strings_plural.xml에서 사용되는 복수형을 정의할 수 있습니다.

* cutscenes.xml: 이 파일에는 메인 게임에 등장하는 거의 모든 컷신이 포함되어 있습니다.

* roomnames.xml: 이 파일에는 메인 게임의 거의 모든 방 이름이 포함되어 있습니다.

* roomnames_special.xml: 이 파일에는 방 이름에 대한 특수 사례, 일반적으로 일반 방으로 표시되지 않는 방 이름(예: The Ship) 및 일반적인 지역 이름이 들어 있습니다.
