=== I N T R O D U C T I O N ===

이 파일은 VVVVVV를 번역할 때 알아야 할 모든 것을 설명합니다.

이 파일은 UTF-8로 인코딩되어 있습니다.



=== A D D I N G   A   N E W   L A N G U A G E ===

영어 파일은 기본적으로 다른 언어에 대한 템플릿입니다(모든 번역이 비어 있습니다).

새 언어를 만들려면 `en` 폴더를 복사한 다음 meta.xml을 작성하기만 하면 됩니다(아래에서 자세히 설명합니다).



=== E X C E L ===

이 게임은 번역을 저장하기 위해 XML 파일을 사용합니다. 원하는 경우 편집기로 사용할 수 있는 .xlsm 파일이 있습니다. 이 파일은 모든 XML 파일을 로드한 다음 변경 사항을 다시 XML로 저장할 수 있습니다.

공식 번역가라면 이 스프레드시트 버전을 받았을 것입니다. 그렇지 않은 경우 여기에서 빈 버전을 찾을 수 있습니다: https://github.com/Dav999-v/TranslationEditor



=== T R A N S L A T O R   M E N U ===

번역기 메뉴에는 번역가와 관리자 모두를 위한 옵션이 있으며, 메뉴 테스트, 게임 내 room name 번역, 모든 언어 파일을 영어 템플릿 파일과 동기화, 번역 진행률 통계 조회 등이 가능합니다. 번역기 메뉴는 일반 버전의 게임에서는 플레이어에게 숨겨져 있습니다.

번역기 메뉴가 잠금 해제되면 게임 내 어디에서나 F12 키를 눌러 현재 언어 파일을 다시 로드할 수도 있습니다. 따라서 번역을 저장하고 즉시 미리 볼 수 있습니다(메뉴 버튼과 현재 cutscene dialogue는 즉시 다시 로드할 수 없음). 언어 파일이 F12를 통해 다시 로드되면 coin sound가 들립니다.



=== L O W E R C A S E   A N D   U P P E R C A S E ===

사용하는 언어(예: 중국어, 일본어, 한국어)에 소문자와 대문자가 없는 경우 meta.xml에서 toupper를 0으로 설정하고 소문자 또는 대문자 사용에 대한 지침을 무시할 수 있습니다.

예를 들어 VVVVVV의 메뉴 시스템은 선택하지 않은 옵션에는 소문자를, 선택한 옵션에는 대문자를 사용하는 스타일입니다:

  play
    levels
    [ OPTIONS ]
        translator
          credits
            quit

메뉴 옵션은 전체 소문자 버전으로 저장되며 번역 파일에서 일반적으로 "메뉴 옵션"으로 주석 처리됩니다. 필요에 따라 소문자 텍스트를 대문자로 자동 변환하는 내장 함수(Localization.cpp의 toupper)가 있습니다. 이 함수는 키릴 문자와 그리스어 등 다양한 악센트 문자를 지원하지만 필요에 따라 더 추가할 수 있습니다. 또한 터키어와 아일랜드어의 특수한 경우도 처리합니다.

터키어: i의 대문자는 İ입니다(예: "dil"은 "DIL"이 아니라 "DİL"이 됩니다. 이를 활성화하려면 meta.xml에서 toupper_i_dot을 1로 설정하세요.

아일랜드어: 문자열을 대문자로 만들 때 특정 문자는 소문자로 유지할 수 있습니다. 예를 들어, "mac tíre na hainnise"는 "MAC TÍRE NA HAINNISE"가 아니라 "MAC TÍRE NA hAINNISE"가 되어야 합니다. 활성화된 경우 소문자로 강제 입력해야 하는 문자 앞에 ~ 문자를 사용할 수 있습니다: "mac tíre na ~hainnise". 이 ~ 문자는 자동 대문자가 적용되는 문자열에만 효과가 있습니다(그렇지 않으면 å로 표시됨). 이 기능은 meta.xml에서 toupper_lower_escape_char를 1로 설정하여 활성화할 수 있습니다.



=== W O R D W R A P P I N G   A N D   L E N G T H   L I M I T S ===

대부분의 언어에서 VVVVVV는 공백을 기준으로 자동으로 단어 줄 바꿈이 가능합니다. 중국어, 일본어, 한국어 등 일부 언어에서는 이 기능이 작동하지 않을 수 있으므로 대신 수동으로 개행(아래 참조)을 삽입하고 meta.xml에서 자동 단어 줄 바꿈을 비활성화할 수 있습니다.

VVVVVV의 해상도는 320x240이고 기본 글꼴은 8x8이므로 40x30 문자 표시가 가능합니다(UI에서 이 표시를 준수하지는 않지만 좋은 표시를 제공합니다). font의 크기가 12x12와 같이 다른 경우 당연히 화면에 표시되는 글자 수도 줄어듭니다.

문자열에는 일반적으로 limit가 주석으로 지정됩니다(예: max="38*3"). 이 형식은 다음 중 하나로 지정할 수 있습니다:
  (A) 33
  (B) 33*3

(A) 단일 숫자(예: "33")인 경우: 맞는 것으로 알려진 최대 글자 수입니다. 제한에 정확히 맞으면 보기에 좋지 않을 수 있으므로 가능하면 한 글자 이상 줄여서 넣으세요.

(B) X*Y(예: 33*3)인 경우: text는 너비 X자, 높이 Y줄의 영역에 맞아야 합니다. meta.xml에서 비활성화하지 않은 경우 text는 자동 줄바꿈 됩니다. 자동 줄바꿈이 비활성화되어 있으면 |를 사용하여 수동으로 개행을 삽입하거나 리터럴 개행으로 삽입해야 합니다.

언어에서 8x8이 아닌 다른 크기의 font를 사용하는 경우 두 가지 제한이 있습니다: 8x8 font를 기준의 원래 제한인 'max'와 font 크기에 맞게 조정된 'max_local'이 있습니다. 이 표기법을 사용하려면 maintenance option을 사용하여 VVVVVV 내에서 language file을 동기화하세요. 먼저 meta.xml에 올바른 font가 설정되어 있는지 확인하세요.

번역기 메뉴에는 주어진 제한을 위반하는 문자열을 자동으로 찾아내는 옵션("limits check")이 있습니다. 이 감지가 완벽하지 않은 경우가 몇 가지 있을 수 있지만 유용한 품질 보증 도구가 될 것입니다.

max length가 항상 제공되는 것은 아닙니다. 메뉴 옵션 버튼은 대각선으로 배치되어 있어 최대 길이를 찾기가 어렵습니다. 더군다나 한 옵션의 길이가 다른 옵션과 너무 많이 다르면 어색해 보일 수 있습니다. 가장 좋은 방법은 평소처럼 번역한 다음 번역기 메뉴의 'menu test' 옵션을 통해 모든 메뉴를 테스트하는 것입니다. 그러나 메뉴는 텍스트 길이에 따라 자동으로 위치가 변경되므로 최악의 경우 옵션의 길이가 36자인 경우 모든 옵션이 서로 바로 아래에 표시됩니다.



=== F O N T S ===

이 게임은 기본적으로 8x8 pixel font를 사용합니다("font" 폴더에 있는 font.png 와 font.fontmeta). 언어를 8x8 문자로 표현할 수 있는 경우 이 font를 사용하거나 이 font를 확장하는 것이 좋습니다.

font directory에는 font format의 동작 방식을 설명하는 README.txt file도 있습니다.



=== N U M B E R S   A N D   P L U R A L   F O R M S ===

특정 위치에서, VVVVVV는 (아마도 관례에 어긋나게) 숫자를 전체 단어로 기록합니다. 예를 들면:

  - One out of Fifteen (열다섯 중 하나)
  - Two crewmates remaining (승무원 둘 남았습니다)
  - Two remaining (둘 남았습니다)

이러한 단어는 numbers.xml에서 찾을 수 있습니다. 0에서 20까지의 숫자가 가장 일반적으로 표시됩니다. 하지만 최대 100까지의 숫자가 표시될 수도 있습니다(플레이어는 사용자 지정 레벨에 trinkets와 crewmates를 최대 100명까지 배치할 수 있습니다).

사용 중인 언어에 따라 같은 숫자에 같은 단어를 사용하는 것이 허용되지 않을 수 있습니다. 예를 들면, 폴란드어에서 "twenty out of twenty"는 "dwadzieścia z dwudziestu"가 될 수 있습니다. 이러한 "단어형" 숫자를 사용할 때와 숫자 형식(20 out of 20)을 사용할 때를 선택할 수 있습니다(아래의 "STRING FORMATTING" 참조). 모든 숫자의 번역을 비워 둘 수도 있습니다. 이 경우 항상 숫자 형식이 사용됩니다.

영어에서는 제목 케이스를 사용하는 것이 적절하지만, 대부분의 다른 언어에서는 그렇지 않을 수 있습니다. 따라서 "Twenty out of Twenty"보다 "twenty out of twenty"를 사용하는 것이 더 적절한 경우 모든 숫자를 소문자로 번역하는 것이 좋습니다. 그런 다음 선택한 placeholder에 자동 대소문자 적용을 적용하면(아래의 "STRING FORMATTING" 참조) "Twenty out of twenty"를 표시할 수 있습니다.

복수형에 관해서: 영어와 일부 다른 언어에는 단수형(승무원 1명)과 복수형(승무원 2명)이 있습니다. 일부 언어에는 다른 규칙이 있을 수 있습니다(예: 0 또는 2, 3, 4로 끝나는 숫자에 대한 규칙). VVVVVV는 이러한 규칙을 수용할 수 있으며 숫자에 따라 특정 문자열(strings_plural.xml)을 다른 방식으로 번역할 수 있습니다. numbers.xml에서 각 숫자의 "form" 속성을 변경하여 다양한 형식을 정의할 수 있습니다. 영어의 경우 단수에는 form "1"을 사용하고 복수에는 form "0"을 사용합니다. 필요한 만큼 복수형을 설정할 수 있습니다.

form을 식별하는 숫자는 반드시 순차적일 필요는 없으며, 0에서 254 사이의 숫자를 사용하여 다른 form을 식별할 수 있습니다. 따라서 양식 0, 1, 2, 3을 사용하는 대신 1, 2, 5, 7로 이름을 지정할 수도 있습니다.

숫자 1, 숫자 2-4 및 기타 모든 숫자에 대해 서로 다른 form이 필요하다고 가정해 보겠습니다. 숫자 1에는 "form 1", 2-4에는 "form 2", 그 외 모든 숫자에는 "form 0"을 사용할 수 있습니다:

<numbers>
    <number value="0"  form="0"  ... />
    <number value="1"  form="1"  ... />
    <number value="2"  form="2"  ... />
    <number value="3"  form="2"  ... />
    <number value="4"  form="2"  ... />
    <number value="5"  form="0"  ... />
    <number value="6"  form="0"  ... />
    ...

복수 문자열을 번역할 때 모든 고유한 형식에 대해 번역을 추가할 수 있습니다. 예를 들면:

    <string english_plural="You rescued {n_crew} crewmates" english_singular="You rescued {n_crew} crewmate">
        <translation form="0" translation="You saved {n_crew} crewmates"/>
        <translation form="1" translation="You saved {n_crew} crewmate"/>
        <translation form="2" translation="You saved {n_crew} crewmateys"/>
    </string>

복수형은 단어형 숫자("you saved one crewmate")뿐만 아니라 숫자형 숫자("you died 136 times in this room")에도 나타날 수 있으므로 100보다 더 많은 숫자를 표시하려면 복수형이 필요합니다.

100 이상의 숫자의 경우: 제가 찾을 수 있는 한(160가지 언어의 복수형 규칙에 대한 정보 포함) 복수형은 항상 100개의 숫자마다 반복됩니다. 따라서 숫자 100-199는 200-299, 300-399 등과 항상 같은 형태를 갖습니다. 하지만 100-119(200-219 등)는 0-19와 항상 동일하게 작동하는 것은 아닙니다(예를 들어 영어의 경우 01로 끝나는데도 "101 trinket"가 아닙니다). 따라서 100-119에 대한 양식도 작성할 수 있습니다. 시스템은 120-199의 경우 20-99를 복사하기만 하면 0부터 무한대까지 모든 숫자를 커버할 수 있습니다. 기술적으로 시스템은 199까지 양식을 제공할 수 있도록 지원하지만 119보다 높은 숫자를 입력할 필요는 없으므로 기본적으로 언어 파일에 포함되어 있지 않습니다.

100보다 큰 숫자는 문자 변환을 할 수 없습니다("one hundred and one"은 존재하지 않습니다).



=== S T R I N G   F O R M A T T I N G ===

문자열에는 {name} 또는 {name|flags}처럼 보이는 placeholder가 있는 경우가 있습니다. 예를 들면 "{n_trinkets} of {max_trinkets}" 등이 있습니다.

Placeholder는 동작을 수정하는 "flags"를 가질 수도 있습니다. 필요에 따라 번역에서 추가하거나 제거할 수 있습니다. 플래그는 | (pipe)로 구분합니다.

예를 들어, "{n_trinkets|wordy}"는 trinket 개수를 "단어형" 숫자(twenty instead of 20)로 표시합니다("NUMBERS AND PLURAL FORMS" 참조). "{n_trinkets|wordy|upper}"는 해당 단어가 대문자로 시작하도록 합니다(Twenty instead of twenty). 예를 들어 "{n_trinkets|wordy|upper} of {max_trinkets|wordy}"는 numbers.xml이 모두 소문자로 번역되었다고 가정할 때 "Twenty out of twenty"로 표시될 수 있습니다.

유효한 flags는 다음과 같습니다:
  - wordy         [ints only] 숫자(20) 대신 숫자 단어(Twenty) 사용
  - digits=n      [ints only] n=5 --> 00031과 같이 최소 n 자리 강제 적용
  - spaces        [only if using digits=n] 0 대신 space 문자 사용
  - upper         loc::toupper_ch 처럼 첫 번째 문자를 대문자화함



=== S T O R Y   A N D   C H A R A C T E R   I N F O R M A T I O N ===

참고용으로 간략한 스토리와 캐릭터 개요를 소개합니다. 추가 질문이 있는 경우 Terry(https://distractionware.com/email/)에게 문의하세요.

== The Crewmates ==

VVVVVV는 호기심 많고 지능이 뛰어난 외계인 승무원들이 우주를 탐험하는 이야기입니다. 우주선에는 여섯 가지 색을 가진 여섯 명의 승무원이 있습니다. 바로 그들입니다:

* Viridian (Cyan, 플레이어 캐릭터)
* Verdigris (Green)
* Vitellary (Yellow)
* Vermilion (Red)
* Victoria (Blue)
* Violet (Purple)

여섯 명의 승무원 이름은 모두 V로 시작하며, 각 승무원의 이름은 색을 암시하는 모호한 단어로 되어 있습니다(예: 버디그리스는 구리가 산화될 때 형성되는 녹색 안료의 이름입니다). 번역하기 어려울 수도 있습니다! (따라서 번역 방법에 대한 좋은 아이디어가 있는 경우, 예를 들어 해당 언어에서 V로 시작하는 동일한 색상/이름을 트릭으로 표현할 수 있다면 이름을 아예 번역하지 않는 것이 더 나을 수도 있습니다.)

각 승무원은 다음과 같은 "계급", 즉 우주선에서의 직업을 가지고 있습니다. 이들은 모두 기본적으로 스타트렉에서 영감을 받은 역할입니다:

* "선장" Viridian (리더의 캡틴)
* "수석" Verdigris (수석 엔지니어와 같은 치프)
* "교수" Vitellary (선내 선임 과학자의 일종)
* "장교" Vermilion (원정 장교의 장교, 보통 탐사를 나가는 사람)
* "박사" Victoria (과학적 의미의 박사)
* "박사" Violet (의학적인 의미의 박사)

Verdigris, Vitellary, Vermilion은 남성입니다. Victoria와 Violet은 여성입니다. Viridian은 의도적으로 성별을 지정하지 않았습니다. 컷신을 번역할 때는 어색한 표현이 나오거나 해당 언어의 최신 문법 트릭을 사용해야 하는 경우라도 가능하면 성별을 지정하지 않도록 하세요.

== Personalities ==

어조에 도움이 될지 모르겠지만, 6명의 캐릭터가 모두 지능이 매우 뛰어난 신동임에도 불구하고 마치 어린아이처럼 서로에게 말을 건다는 점이 VVVVVV의 글에서 자주 나오는 농담입니다. 예: 비리디안 "그냥 가지고 놀고 있었어!", 버밀리온 "도와주고 있어!", 버디그리스 "난 엔지니어야!" 등. 더 구체적으로 말하면:

* Viridian은 위험에 굴하지 않고 걱정하지 않으며 항상 모든 것을 해결할 수 있다고 확신하는 고전적인 영웅입니다.
* Verdigris는 는 로맨틱한 사람입니다. 그는 바이올렛에게 엄청난 애정을 가지고 있는데, 그는 그것을 비밀로 하는 끔찍하게 노력합니다.
* Vitellary는 학자입니다. 과학을 좋아해서 거의 모든 컷신에서 과학에 대해 건조하고 장황하게 이야기합니다.
* Vermilion은 대담하고 모험적입니다 - 그를 구출한 후, 나머지 대원들을 찾기 위해 혼자서 세계 곳곳을 탐험하는 모습을 볼 수 있습니다(하지만 큰 도움은 되지 못합니다).
* Victoria는 걱정이 많고 절망감에 빨리 빠져듭니다. 빅토리아의 영혼은 거의 항상 슬픕니다!
* Violet은 우주선의 주치의이며, 대부분의 컷신에서 다른 승무원들의 상태를 업데이트합니다.

== Dimension VVVVVV ==

여러분이 탐험하는 세계는 터미널로 가득 차 있으며, 우리가 볼 수 없는 이전 거주자의 텍스트 로그가 남아 있습니다. 우리는 그들에 대해 아는 것이 많지 않습니다.

여러분 모두가 타고 있는 우주선은 작은 이스터에그인 "D.S.S. Souleye"라고 불립니다. D.S.S.는 "Dimensional Space Ship(차원 우주선)"의 약자로, 여러 차원 사이를 오가는 우주선입니다. Souleye는 게임 작곡가인 Magnus Pålsson의 가명입니다.



=== F I L E S ===

== meta.xml ==
이 파일에는 이 번역에 대한 몇 가지 일반 정보가 포함되어 있습니다. 이 파일에는 다음과 같은 속성이 포함되어 있습니다:

* active: 0이면 이 언어는 언어 메뉴에 표시되지 않습니다.

* nativename: 언어 자체의 이름은 완전히 소문자로 되어 있습니다(따라서 "spanish"나 "Español"이 아니라 "español"). 언어 이름은 최대 16자까지 입력할 수 있습니다(8x8 font 사용시)

* credit: 여기에 "스페인어 번역 X"와 같이 언어 화면에 표시되는 크레딧을 입력할 수 있습니다. 귀하의 언어로 입력할 수 있습니다. 최대 38*2 @8x8

* action_hint: 언어가 강조 표시된 경우 언어 화면 하단에 표시되어 Space/Z/V가 선택한 옵션을 언어로 설정했음을 나타냅니다. 최대 40 @8x8

* autowordwrap: 자동 단어 줄 바꿈 사용 여부. CJK에서는 비활성화할 수 있습니다(이 경우 텍스트에 줄 바꿈을 수동으로 삽입해야 함).

* toupper: 메뉴 옵션의 자동 대문자 사용 여부(unselected, SELECTED). 소문자와 대문자가 없는 CJK와 같은 언어의 경우 비활성화될 수 있습니다.

* toupper_i_dot: 자동으로 대문자를 사용할 때는 터키어에서처럼 i를 İ로 매핑합니다.

* toupper_lower_escape_char: 자동으로 대문자를 사용할 때 아일랜드어의 경우 ~를 사용하여 다음 문자가 대문자가 되지 않도록 할 수 있습니다.

* menu_select: 특정 메뉴 옵션 또는 버튼이 선택되었음을 나타내는 표시로, "toupper"가 활성화된 경우 자동으로 대문자로 바뀝니다. 예를 들어 "[ {label} ]"은 "[ SELECTED ]"처럼 보입니다.

* menu_select_tight: menu_select과 비슷하지만, 지도 화면처럼 공간이 좀 더 제한적인 경우에 사용된다는 점을 제외하면 다릅니다. "[{label}]"은 "[SELECTED]"처럼 보입니다.


== strings.xml ==
이 파일에는 인터페이스와 게임의 일부에 대한 일반 문자열이 포함되어 있습니다. XML에서 한 문자열의 태그는 다음과 같습니다:

    <string english="Game paused" translation="" explanation="pause screen" max="40"/>

문자열을 번역하려면 다음과 같이 translation 속성을 입력하기만 하면 됩니다:

    <string english="Game paused" translation="Spel gepauzeerd" explanation="pause screen" max="40"/>

번역을 비워두면 영어 텍스트로 대체됩니다. 그러나 텍스트가 동일한 경우 번역을 일부러 공백으로 남겨두면 번역되지 않은 문자열로 간주되어 새로운 내용을 추적하기가 더 어려워지므로 번역을 일부러 공백으로 두어서는 안 됩니다. 이 경우 항상 영어 문자열을 번역에 copy-paste하세요.

각 문자열에는 다음과 같은 속성이 있습니다:

* english: 영어 텍스트.

* translation: 번역.

* case: 영어로는 동일하지만 다른 번역이 필요할 수 있는 별도의 문자열에 대한 숫자(1, 2 등).

* explanation: 컨텍스트, 위치 및 형식에 대한 설명.

* max: 길이 제한, "WORDWRAPPING AND LENGTH LIMITS"에 설명되어 있음.


== strings_plural.xml ==

위의 "NUMBERS AND PLURAL FORMS"을 참조하세요.

numbers.xml에서 복수형을 정의할 수 있습니다.

그런 다음 numbers.xml에서 설정한 각 양식에 대한 번역을 추가하기만 하면 됩니다. 예를 들면:

    <translation form="0" translation="Shows up for all numbers with form=0"/>
    <translation form="1" translation="Shows up for all numbers with form=1"/>
    <translation form="2" translation="Shows up for all numbers with form=2"/>

"wordy" 플래그는 단어가 채워질 것(예: twelve)을 나타내며, 그렇지 않으면 숫자(12)가 채워집니다. 위의 "STRING FORMATTING"에서 설명한 대로 번역에서 필요에 따라 이 값을 변경할 수 있습니다.

`var` 속성은 입력할 placeholder를 나타내고, `expect` 속성은 입력할 것으로 예상되는 값의 높이를 나타냅니다. 예를 들어, expect="20"은 20을 초과하는 값은 이 문자열에 사용되지 않을 수 있음을 의미합니다. 이는 주로 제한 검사에서 "seventy seven"과 같은 숫자가 문자열을 너무 길게 만들지 않도록 하기 위해 필요하지만 유용한 컨텍스트 단서가 될 수도 있습니다.


== numbers.xml ==
이 파일에는 0에서 100까지의 모든 숫자(Zero, One, etc)가 기록되어 있습니다.

이것은 다음과 같은 문자열로 채워집니다:
- One out of Fifteen (열다섯 중 하나)
- Two crewmates remaining (승무원 둘 남았습니다)
- Two remaining (둘 남았습니다)

이 방법이 언어에 맞지 않거나 단어형 숫자가 정말 적합하지 않은 경우, 이 모든 항목을 비워두면 숫자가 사용됩니다(20 out of 20).

영어식 타이틀 케이스를 사용하지 않으려면 모두 소문자로 작성하는 것이 좋습니다. "Twenty out of Twenty"는 많은 언어에서 문법적으로 올바르지 않을 수 있으며 "twenty out of twenty"가 더 나을 수 있습니다. 숫자를 모두 소문자로 번역하면 "Twenty out of twenty"와 같이 상황에 맞는 대문자를 적용할 수 있습니다(위의 "STRING FORMATTING" 참조).

이 파일을 사용하면 strings_plural.xml에서 사용되는 복수형도 정의할 수 있습니다.

자세한 내용은 위의 "NUMBERS AND PLURAL FORMS"을 참조하세요.


== cutscenes.xml ==
이 파일에는 메인 게임에 등장하는 거의 모든 컷신이 포함되어 있습니다. 각 대사에는 "speaker" 속성이 있는데, 이 속성은 게임에서는 사용되지 않으며 번역가가 누가 무슨 말을 하는지 파악하고 문맥을 설정하기 위한 것입니다.

meta.xml에서 자동 줄 바꿈이 비활성화되어 있는 경우를 제외하고 대화 상자는 자동으로 텍스트 줄 바꿈이 적용됩니다. 이 경우 최대 줄 길이는 8x8 문자 36개(288픽셀) 또는 12x12 문자 24개입니다.

컷씬에서 같은 텍스트가 여러 번 나타나는 경우, "case" 속성이 추가되어 있으므로(예: case="1", case="2" 등) 필요한 경우 별도로 번역할 수 있습니다. (스크립트 자체의 textcase(x) 명령과 일치합니다.)

각 <dialogue> tag에 몇 가지 추가 서식 속성이 있을 수 있습니다. 이러한 속성은 번역의 간격 및 서식을 원본 영어 텍스트와 일관되게 만드는 데 사용됩니다(예: 텍스트 중앙 정렬, 양쪽 패딩 등). 필요한 경우 이러한 속성 중 하나를 변경할 수 있으며, 모든 dialogue tag에 직접 추가할 수도 있습니다.

* tt: teletype. "1"이면 meta.xml에서 자동 줄 바꿈이 활성화되어 있더라도 자동 줄 바꿈을 비활성화합니다. 이 textbox에 hard enter를 사용하거나 |를 사용하여 수동으로 줄 바꿈을 추가해야 합니다.

* wraplimit: 단어 줄 바꿈 전 텍스트의 max width를 pixel 단위로 변경합니다. tt가 활성화되지 않은 경우에만 해당합니다. 예제:
    [Hello world!]  --[wraplimit="56"]-->  [Hello ]   (56=7*8)
                                           [world!]
  meta.xml에서 자동 단어 줄 바꿈이 비활성화되어 있으면 이 기능도 작동하지 않지만 권장 max text width를 제공합니다.
  기본값은 288입니다(36*8 또는 24*12).

* centertext: 텍스트 가운데 정렬 (단, 그리드에 맞춰 정렬), 예제:
    [You have rescued]  --[centertext="1"]-->  [You have rescued]
    [a crewmember!]                            [ a crewmember!  ]

* pad: 텍스트의 각 줄에 공백을 채웁니다(기본값은 0), 예제:
    [You have rescued]  --[pad="2"]-->  [  You have rescued  ]
    [ a crewmember!  ]                  [   a crewmember!    ]
  custom wraplimit를 지정하지 않는 한 자동으로 그에 따라 wrap limit를 더 작게 설정합니다.

* pad_left/pad_right: 패드와 동일하지만 왼쪽 또는 오른쪽에만 영향을 줍니다. 예제:
    [You have rescued]  --[ pad_left="5"]--\  [     You have rescued  ]
    [ a crewmember!  ]  --[pad_right="2"]--/  [      a crewmember!    ]

* padtowidth: 이 픽셀 너비가 아닌 경우 양쪽에 텍스트를 채웁니다. 예제:
    [-= Personal Log =-]  --[padtowidth="224"]--> [     -= Personal Log =-     ]   (224=28*8)


== roomnames.xml ==
이 파일에는 메인 게임의 거의 모든 room name이 포함되어 있습니다. 제한은 항상 8x8 문자 40자(320픽셀) 또는 12x12 문자 26자입니다.

게임 내에서 room name을 번역하여 모든 room name이 왜 그렇게 불리는지 확인하는 것이 좋습니다. 번역기 > 번역기 옵션 > room name 번역에서 room name 번역 모드를 활성화하세요.


== roomnames_special.xml ==
이 파일에는 room name에 대한 몇 가지 특수한 경우, 일반적으로 일반 room으로 표시되지 않는 room name(예: The Ship), 일반적인 지역 이름이 포함되어 있습니다.

한 방("Prize for the Reckless")은 time trial과 no death mode에서 의도적으로 스파이크가 누락되어 플레이어가 그곳에서 죽을 필요가 없으며, 두 경우 모두 방의 이름이 다르게 불립니다(time trial의 경우 "Imagine Spikes There, if You Like", no death mode의 경우 "I Can't Believe You Got This Far").

게임 내에는 점차 다른 room으로 바뀌거나 약간의 변형을 거쳐 순환하는 room name도 있습니다.

