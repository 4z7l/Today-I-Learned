# My Android Coding Convention


[Kotlin Coding Conventions](https://kotlinlang.org/docs/reference/coding-conventions.html)

[Kotlin style guide](https://developer.android.com/kotlin/style-guide)

# Resource Naming Convention

## Id

- Pascal Case를 축약하여 Snake Case로 작성
- `<WHAT>_<DESCRIPTION>`
- ex) `tv_login`

|View|Naming|
|-|-|
|TextView|`tv_`|
|ImageView|`iv_`|
|EditText|`et`|
|Button, ImageButton|`btn_`|
|Toolbar|`tb_`|
|ConstraintLayout|`cl_`|
|LinearLayout|`ll_`|
|BottomNavigationView|`bnv_`|

등등

## Layout

- `<WHAT>_<DESCRIPTION>`
- ex) SignInActivity -> `activity_sign_in`

- `activity_`
- `fragment_`
- `dialog_` : 다이알로그 layout
- `view_` : CustomView에 쓰이는 layout
- `item_` : RecyclerView, GridView등에 쓰이는 item layout
- `layout_` : <include/>에 들어가는 layout

## Drawable
- `<WHAT>_<DESCRIPTION>`
- ex) `ic_error`
- `ic_` : 아이콘
- `bg_` : 백그라운드
- `img_` : 이미지
- `모양_색깔_Radius` : ex) `rectangle_yellow_raius_20.xml`

## Menu

- `menu_` : tab, navigation 등에 쓰이는 메뉴 layout

## Values

### Color

- 직관적으로 판단할 수 있도록
- https://chir.ag/projects/name-that-color/#6195ED 참고
- `<COLOR>`
ex)

```
<color name="purple_200">#FFBB86FC</color>
<color name="purple_500">#FF6200EE</color>
<color name="black">#FF000000</color>
<color name="white">#FFFFFFFF</color>
```

### String

- 주석을 통해 string 범위 구분하기

```
<!--Main Menu-->
<string name="menu_daily">하루의 기록</string>
<string name="menu_remind">평가 및 회고</string>
<string name="menu_my">My</string>

<!--탭,툴바 타이틀-->
<string name="title_search">검색</string>
<string name="title_settings">환경설정</string>
```

- `<WHERE>_<DESCRIPTION>` : ex) menu_daily
- 기타
  - `msg_` : 다이알로그나 토스트에 쓰이는 텍스트
  - `title_` : 탭, 툴바 타이틀

### Style
- Pascal Case
- `XXViewStyle` : ex) LoginEditTextStyle, MainDialogStyle ..
