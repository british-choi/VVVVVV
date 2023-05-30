=== I N T R O D U C T I O N ===

이 파일은 폰트 포맷에 대해 설명합니다.

게임에서 읽을 수 있는 포맷으로 변환된 폰트(예: TTF)가 필요한 경우, 현재로서는 관련 툴을 가지고 있는 Dav에게 문의하는 것이 좋습니다.



=== F O N T   F O R M A T ===

폰트는 두 개의 파일, 즉 .png와 .fontmeta로 구성됩니다. .png에는 모든 glyph에 대한 모든 "image"가 포함되어 있으며, .fontmeta는 파일에 있는 문자에 대한 모든 정보 및 기타 메타데이터가 포함된 XML 문서입니다.

예를 들어 한국어 글꼴은 font_ko.png 및 font_ko.fontmeta라고 할 수 있습니다.

폰트 메타 파일은 다음과 같습니다:


<?xml version="1.0" encoding="UTF-8"?>
<font_metadata>
    <display_name>한국어</display_name>
    <width>12</width>
    <height>12</height>
    <white_teeth>1</white_teeth>
    <chars>
        <range start="0x20" end="0x7F"/>
        <range start="0xA0" end="0x17F"/>
        <range start="0x18F" end="0x18F"/>
        <range start="0x218" end="0x21B"/>
        <range start="0x259" end="0x25A"/>
        <!-- ... -->
    </chars>
    <special>
        <range start="0x00" end="0x1F" advance="6"/>
        <range start="0xEB00" end="0xEBFF" color="1"/>
    </special>
    <fallback>buttons_12x12</fallback>
</font_metadata>


* type: normal font에는 사용되지 않습니다. button glyph font에는 <type>buttons</type>이 사용됩니다.

* display_name: font가 특별히 사용되는 언어의 이름 - 언어 자체에 표시됩니다. 사용자는 레벨 에디터에서 사용할 font를 선택할 때 이 정보를 볼 수 있습니다. 이 font가 여러 번역에서 동일하게 사용되는 경우 "繁體中文/한국어"와 같은 조합으로 설정할 수 있습니다. (커스텀 플레이어 레벨을 생성하는 경우: 걱정하지 마세요.)

* width/height: font에 있는 각 glyph의 width와 height입니다. 모든 문자는 항상 이 크기의 직사각형으로 그려집니다. VVVVVV는 최대 12 pixel 높이의 font를 지원하며, 그 이상이면 텍스트가 겹치거나 제자리에 맞지 않을 수 있습니다.

* white_teeth: font의 모든 문자가 white임을 나타내므로 게임 자체에서 이전 버전의 게임처럼 이미지에서 모든 색상을 제거하고 모든 픽셀을 흰색으로 만들지 않아도 됩니다. 이 값을 1로 설정하지 않으면 이 font에 color (button) glyph를 사용할 수 없으며, 게임이 로드될 때마다 font를 특별히 처리해야 하므로 1로 설정하는 것이 좋습니다.

* chars: 이미지에 포함할 문자를 정의합니다. 이미지의 왼쪽 상단부터 각 문자는 왼쪽에서 오른쪽, 위에서 아래로 동일한 크기(<width> 와 <height>로 정의됨)의 직사각형입니다. 위의 예시에서 이미지에는 먼저 U+0020부터 U+007F까지 모든 문자가 유니코드화되어 있고, 그 다음에는 U+00A0부터 U+017F까지 모든 문자가 유니코드화되어 있습니다. 단일 문자를 포함하려면 start와 end attribute가 동일한 범위를 가지면 됩니다.

* special: 문자 범위에 적용될 special attribute를 정의합니다. 다음 attribute 중 하나 이상을 사용할 수 있습니다:

 - color: 해당 glyph가 원래 색상으로 그려져야 하는 경우 1로 설정합니다(button glyph 또는 이모티콘 등).

 - advance: <width> 대신 다음 문자를 그리기 위한 커서를 오른쪽으로 설정한 값의 pixel수 만큼 이동시켜야 합니다. 이것은 문자의 너비를 제어하지만 이미지에서 문자가 배열되는 방식에는 영향을 미치지 않으며 전체 glyph가 계속 그려집니다. font 시스템이 가변폭 font를 지원한다는 의미이지만 이 옵션은 사용하지 않는 것이 좋습니다. 가변폭 font를 사용할 경우(특히 텍스트 상자에서) 몇 가지 문제가 발생할 수 있으므로 글꼴의 전각문자 형태(U+FF01-U+FF5E)를 ASCII U+0021-U+007E로 복사하는 것을 고려하시기 바랍니다. 고정폭 font가 게임 스타일에 더 잘 어울린다는 의견도 있습니다.

* fallback: 사용할 button glyph font를 지정합니다. font는 [width]x[height] 사각형에 딱맞는 것을 선택해야 하므로, 8x12 글꼴의 경우 buttons_12x12가 아닌 buttons_8x8을 선택해야 합니다.

