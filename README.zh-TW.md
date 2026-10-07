# One Half Light (New)

[English](README.md)

適合 Windows Terminal 的淺色配色，針對 PowerShell 的資料夾列表、命令文字與行內建議調整可讀性。

## 安裝與更新

1. 開啟 Windows Terminal 的「設定」，選擇「開啟 JSON 檔案」。
2. 將 [scheme.json](scheme.json) 的完整內容加入 `settings.json` 的 `schemes` 陣列。若已經有名稱為 `One Half Light (New)` 的配色，請替換原有物件。
3. 在要使用此配色的設定檔中，將 `colorScheme` 設為 `One Half Light (New)`，或在設定介面的「外觀」中選取此配色。
4. 儲存設定，再執行 `ls` 或輸入命令確認效果。

以下是設定檔選取配色的範例欄位，請加入既有的設定檔物件：

```json
"colorScheme": "One Half Light (New)"
```

## 配色調整

| 用途 | 欄位 | 顏色 | 效果 |
| --- | --- | --- | --- |
| 終端機背景 | `background` | `#FAFAFA` | 接近白色的背景 |
| 一般輸出文字 | `foreground` | `#383A42` | 深灰文字 |
| 資料夾背景 | `blue` | `#B8DDF0` | 淡藍底，搭配深灰文字 |
| 命令名稱 | `brightYellow` | `#9C6500` | 加深的琥珀色 |
| 一般輸入文字 | `white` | `#555760` | 較深的灰色 |
| 行內建議的基礎顏色 | `brightWhite` | `#FFFFFF` | 經 PSReadLine 變暗後呈現灰色 |

這些用途以 PowerShell 與 PSReadLine 的預設樣式為前提。自訂設定或不同版本可能使用其他顏色。

### 資料夾列表

PowerShell 7.2 以上的 `ls`（`Get-ChildItem`）預設會替資料夾名稱加上藍色背景。本配色將 `blue` 改為淡藍色，與深灰前景的對比約為 **7.9:1**，不必修改 PowerShell 設定檔。

ANSI 色盤的前景與背景共用同一個顏色，因此其他使用一般 ANSI 藍色的文字也會變淡。若偏好深藍文字，可以將 `blue` 改回 `#0184BC`，並在 PowerShell 使用以下設定，將資料夾改為深藍文字、移除背景色塊：

```powershell
$PSStyle.FileInfo.Directory = $PSStyle.Foreground.FromRgb(0x006B99)
```

此深藍文字與 `#FAFAFA` 背景的對比約為 **5.6:1**。

### 命令文字

PSReadLine 預設使用 ANSI 亮黃色顯示命令名稱。本配色將 `brightYellow` 改為較深的琥珀色，與背景的對比約為 **4.71:1**，讓命令在淺色背景上更清楚。

### 行內建議

較新的 PSReadLine 預設使用「變暗、斜體的 ANSI 亮白色」顯示行內建議。本配色提高 `brightWhite` 的亮度，並加深一般輸入文字使用的 `white`，拉開建議與已輸入文字的差異。建議文字的變暗與斜體效果仍由 PSReadLine 套用。

這也會影響其他程式使用 ANSI 白色與亮白色時的顯示。如果你的版本或自訂設定使用不同的建議樣式，或希望建議再淡一些，可直接設定為不帶變暗效果的斜體灰色 `#969696`：

```powershell
Set-PSReadLineOption -Colors @{ InlinePrediction = "`e[38;2;150;150;150;3m" }
```

## 保存選用的 PowerShell 設定

上述 PowerShell 命令只影響目前的工作階段。若要在新開的 PowerShell 中繼續套用，請將需要的命令加入 `$PROFILE`。

如果尚未建立設定檔，可執行：

```powershell
if (!(Test-Path -LiteralPath $PROFILE)) {
    New-Item -ItemType File -Path $PROFILE -Force | Out-Null
}
notepad $PROFILE
```

儲存後，重新開啟 PowerShell 即可套用。

## 參考文件

- [Windows Terminal 配色設定](https://learn.microsoft.com/zh-tw/windows/terminal/customize-settings/color-schemes)
- [PowerShell ANSI 終端機與 PSStyle](https://learn.microsoft.com/zh-tw/powershell/module/microsoft.powershell.core/about/about_ansi_terminals)
- [PSReadLine 預測功能](https://learn.microsoft.com/en-us/powershell/scripting/learn/shell/using-predictors)
