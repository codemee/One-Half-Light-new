[繁體中文](README.zh-TW.md)

Just copy the content of  [scheme.json](scheme.json) and paste into your settings.json:

```json
{
    ...,
    "schemes": 
    [
        {
            "background": "#FAFAFA",
            "black": "#383A42",
            "blue": "#B8DDF0",
            "brightBlack": "#4F525D",
            "brightBlue": "#61AFEF",
            "brightCyan": "#56B5C1",
            "brightGreen": "#98C379",
            "brightPurple": "#C577DD",
            "brightRed": "#DF6C75",
            "brightWhite": "#FFFFFF",
            "brightYellow": "#9C6500",
            "cursorColor": "#4F525D",
            "cyan": "#0997B3",
            "foreground": "#383A42",
            "green": "#50A14F",
            "name": "One Half Light (New)",
            "purple": "#A626A4",
            "red": "#E45649",
            "selectionBackground": "#383A42",
            "white": "#555760",
            "yellow": "#C18301"
        }
    ],
    ...
}
```

### Readable command text in PowerShell

PSReadLine uses ANSI bright yellow for command names by default. This scheme
uses a darker amber (`#9C6500`) for `brightYellow` to keep commands readable
against the light background. Apply the updated scheme in Windows Terminal's
`settings.json`; no PowerShell profile change is needed for the default style.

### Distinguishable inline suggestions in PowerShell

Recent PSReadLine versions use dim, italic ANSI bright white for inline
predictions. This scheme sets `brightWhite` to `#FFFFFF` to lighten those
suggestions, while `white` is a darker gray (`#555760`) for ordinary input text.
The prediction's dim effect still applies. These palette changes also affect
other applications using ANSI white or bright white.

If your PSReadLine version or profile uses a different prediction style, or you
want still lighter suggestions, set the prediction color explicitly:

```powershell
Set-PSReadLineOption -Colors @{ InlinePrediction = "`e[38;2;150;150;150;3m" }
```

This uses italic gray (`#969696`) without the dim effect. Add the line to
`$PROFILE` to keep it for new sessions.

### Readable directory names in PowerShell

PowerShell 7.2 and later applies a blue background to directory names in `ls`
(`Get-ChildItem`) by default. This scheme uses pale blue (`#B8DDF0`) so the dark
foreground (`#383A42`) remains readable on directory backgrounds. Update the
scheme in Windows Terminal's `settings.json` to apply this fix; no PowerShell
profile change is needed.

ANSI colors are shared by foreground and background styles. This also makes
regular ANSI blue text pale against the light terminal background. If you
prefer dark blue text throughout, restore `blue` to `#0184BC` and use the
optional PowerShell configuration below instead.

Optionally, run this in PowerShell to use dark blue directory text without a
background:

```powershell
$PSStyle.FileInfo.Directory = $PSStyle.Foreground.FromRgb(0x006B99)
```

The text color has approximately 5.6:1 contrast against this scheme's `#FAFAFA`
background. To keep the setting for new PowerShell sessions, add the same line
to your PowerShell profile (`$PROFILE`). If you do not have a profile yet:

```powershell
if (!(Test-Path -LiteralPath $PROFILE)) {
    New-Item -ItemType File -Path $PROFILE -Force | Out-Null
}
notepad $PROFILE
```

See Microsoft's [ANSI terminal documentation](https://learn.microsoft.com/en-us/powershell/module/microsoft.powershell.core/about/about_ansi_terminals#psstyle)
for more information about `$PSStyle.FileInfo`.
