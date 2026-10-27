# VS Code 확장 프로그램 VSIX 백업 및 오프라인 설치 가이드

Mac과 Windows에서 현재 VS Code에 설치된 확장 프로그램을 확인하고,
`.vsix` 파일로 일괄 수집한 뒤 인터넷이 없는 폐쇄망 PC에 설치하는
방법입니다.

## 1. 기본 개념

VS Code 확장 프로그램 패키지의 확장자는 `.vsix`입니다.

``` text
.vixx  X
.vsix  O
```

## 2. VS Code에 설치된 확장 프로그램 위치

### Mac

``` bash
~/.vscode/extensions/
```

확인:

``` bash
ls ~/.vscode/extensions/
```

Finder에서 열기:

``` bash
open ~/.vscode/extensions/
```

Cursor:

``` bash
~/.cursor/extensions/
```

### Windows

``` text
%USERPROFILE%\.vscode\extensions
```

PowerShell에서 열기:

``` powershell
explorer "$env:USERPROFILE\.vscode\extensions"
```

## 3. 중요한 차이

`.vscode/extensions`에 있는 것은 `.vsix` 파일이 아니라 VSIX 설치 후 압축
해제된 확장 프로그램 폴더입니다.

``` text
VSIX 패키지
  ↓
xxx.vsix
  ↓
VS Code 설치
  ↓
.vscode/extensions/
  ↓
확장 프로그램 폴더
```

따라서 Mac에서 다음 명령을 실행했을 때:

``` bash
cd ~/.vscode/extensions
ls *.vsix
```

다음 오류가 발생할 수 있습니다.

``` text
zsh: no matches found: *.vsix
```

현재 폴더에 `.vsix`가 없기 때문입니다.

# Mac

## 4. 현재 설치된 확장 프로그램 확인

``` bash
code --list-extensions
```

버전 포함:

``` bash
code --list-extensions --show-versions
```

목록 저장:

``` bash
code --list-extensions --show-versions > ~/Downloads/extensions.txt
```

## 5. 설치된 확장 폴더 자체를 ZIP으로 백업

``` bash
cd ~/.vscode
zip -r ~/Downloads/vscode-extensions-backup.zip extensions
```

Finder에서 확인:

``` bash
open ~/Downloads
```

주의: 이 방법은 `.vsix`를 생성하는 것이 아니라 설치된 확장 폴더를 그대로
백업합니다.

## 6. 압축 없이 확장 폴더 복사

``` bash
cp -R ~/.vscode/extensions ~/Downloads/vscode-extensions-backup
```

확인:

``` bash
open ~/Downloads/vscode-extensions-backup
```

## 7. VSIX 자동 수집

저장 폴더 생성:

``` bash
mkdir -p ~/Downloads/vscode-vsix
```

설치된 확장과 버전 확인:

``` bash
code --list-extensions --show-versions
```

### download-vsix.sh 생성

``` bash
cat > ~/Downloads/download-vsix.sh <<'EOF'
#!/bin/zsh

OUT="$HOME/Downloads/vscode-vsix"

mkdir -p "$OUT"

code --list-extensions --show-versions | while IFS='@' read -r EXT VERSION
do
    PUBLISHER="${EXT%%.*}"
    NAME="${EXT#*.}"

    URL="https://marketplace.visualstudio.com/_apis/public/gallery/publishers/${PUBLISHER}/vsextensions/${NAME}/${VERSION}/vspackage"

    FILE="$OUT/${PUBLISHER}.${NAME}-${VERSION}.vsix"

    echo ""
    echo "======================================"
    echo "Downloading: $EXT"
    echo "Version    : $VERSION"
    echo "======================================"

    if curl -fL \
        -H "Accept: application/octet-stream" \
        "$URL" \
        -o "$FILE"
    then
        echo "OK: $FILE"
    else
        echo "FAILED: $EXT@$VERSION"
        rm -f "$FILE"
    fi
done

echo ""
echo "======================================"
echo "VSIX collection completed"
echo "Location: $OUT"
echo "======================================"

open "$OUT"
EOF

chmod +x ~/Downloads/download-vsix.sh
```

## 8. VSIX 다운로드 실행

``` bash
~/Downloads/download-vsix.sh
```

결과 예:

``` text
Downloads/
├── download-vsix.sh
└── vscode-vsix/
    ├── dbaeumer.vscode-eslint-3.0.16.vsix
    ├── esbenp.prettier-vscode-11.0.0.vsix
    ├── vue.volar-3.1.0.vsix
    └── continue.continue-2.0.0.vsix
```

## 9. Mac에서 VSIX 일괄 설치

``` bash
cd ~/Downloads/vscode-vsix
```

확인:

``` bash
ls *.vsix
```

설치:

``` bash
for file in *.vsix; do
    code --install-extension "$file"
done
```

강제 재설치:

``` bash
for file in *.vsix; do
    code --install-extension "$file" --force
done
```

## 10. `zsh: no matches found: *.vsix` 오류

현재 위치:

``` bash
pwd
```

VSIX 확인:

``` bash
ls *.vsix
```

다운로드 폴더로 이동:

``` bash
cd ~/Downloads/vscode-vsix
```

또는 경로 직접 지정:

``` bash
for file in ~/Downloads/vscode-vsix/*.vsix; do
    code --install-extension "$file"
done
```

# Windows

## 11. 현재 설치된 확장 프로그램 확인

PowerShell:

``` powershell
code --list-extensions
```

버전 포함:

``` powershell
code --list-extensions --show-versions
```

목록 저장:

``` powershell
code --list-extensions --show-versions > "$env:USERPROFILE\Downloads\extensions.txt"
```

## 12. VSIX 저장 폴더 생성

``` powershell
$OUT = "$env:USERPROFILE\Downloads\vscode-vsix"
New-Item -ItemType Directory -Force -Path $OUT
```

## 13. Windows VSIX 자동 수집

``` powershell
$OUT = "$env:USERPROFILE\Downloads\vscode-vsix"

New-Item -ItemType Directory -Force -Path $OUT | Out-Null

$extensions = code --list-extensions --show-versions

foreach ($item in $extensions) {

    if ($item -match '^(.+?)@(.+)$') {

        $extensionId = $matches[1]
        $version = $matches[2]

        $parts = $extensionId.Split('.', 2)

        $publisher = $parts[0]
        $name = $parts[1]

        $url = "https://marketplace.visualstudio.com/_apis/public/gallery/publishers/$publisher/vsextensions/$name/$version/vspackage"

        $file = Join-Path $OUT "$publisher.$name-$version.vsix"

        Write-Host ""
        Write-Host "======================================"
        Write-Host "Downloading : $extensionId"
        Write-Host "Version     : $version"
        Write-Host "======================================"

        try {
            Invoke-WebRequest `
                -Uri $url `
                -Headers @{
                    "Accept" = "application/octet-stream"
                } `
                -OutFile $file

            Write-Host "OK : $file"
        }
        catch {
            Write-Host "FAILED : $extensionId@$version"

            if (Test-Path $file) {
                Remove-Item $file
            }
        }
    }
}

Write-Host ""
Write-Host "======================================"
Write-Host "VSIX collection completed"
Write-Host "Location: $OUT"
Write-Host "======================================"

Start-Process explorer.exe $OUT
```

## 14. PowerShell 스크립트로 저장

위 코드를 다음 파일로 저장:

``` text
download-vscode-vsix.ps1
```

실행:

``` powershell
.\download-vscode-vsix.ps1
```

실행 정책 오류가 발생하면:

``` powershell
powershell -ExecutionPolicy Bypass -File .\download-vscode-vsix.ps1
```

## 15. Windows에서 VSIX 일괄 설치

``` powershell
cd "$env:USERPROFILE\Downloads\vscode-vsix"
```

확인:

``` powershell
Get-ChildItem *.vsix
```

설치:

``` powershell
Get-ChildItem *.vsix | ForEach-Object {
    code --install-extension $_.FullName
}
```

강제 설치:

``` powershell
Get-ChildItem *.vsix | ForEach-Object {
    Write-Host "Installing: $($_.Name)"
    code --install-extension $_.FullName --force
}
```

설치 확인:

``` powershell
code --list-extensions --show-versions
```

## 16. install-vsix.ps1

``` powershell
$VSIX = "$PSScriptRoot\vscode-vsix"

Get-ChildItem "$VSIX\*.vsix" | ForEach-Object {

    Write-Host ""
    Write-Host "Installing: $($_.Name)"

    code --install-extension $_.FullName --force
}

Write-Host ""
Write-Host "======================================"
Write-Host "VSIX installation completed"
Write-Host "======================================"

code --list-extensions --show-versions
```

폐쇄망 PC에서:

``` powershell
powershell -ExecutionPolicy Bypass -File .\install-vsix.ps1
```

# 17. Windows 인터넷 PC → 폐쇄망 PC

``` text
[인터넷 Windows PC]

VS Code
  ↓
설치된 확장 확인
  ↓
code --list-extensions --show-versions
  ↓
download-vscode-vsix.ps1
  ↓
vscode-vsix\
  ↓
VSIX 다운로드
  ↓
USB 또는 허용된 저장장치
  ↓

[폐쇄망 Windows PC]

vscode-vsix\
  ↓
install-vsix.ps1
  ↓
VS Code 확장 일괄 설치
```

Windows → Windows 방식은 플랫폼이 동일하기 때문에 권장됩니다.

# 18. Mac → Windows 이동 시 주의사항

일반적인 HTML/CSS/JavaScript 관련 확장은 플랫폼에 관계없이 동작하는
경우가 많지만 일부 확장은 네이티브 바이너리를 포함합니다.

플랫폼 예:

``` text
darwin-arm64
darwin-x64
win32-x64
win32-arm64
linux-x64
```

특히 다음 종류는 확인이 필요합니다.

-   AI 확장
-   Debugger
-   Remote 관련 확장
-   언어 서버
-   Native Module 포함 확장
-   터미널/시스템 연동 확장

가능하면 다음 방식으로 관리하는 것이 안전합니다.

``` text
Mac     → Mac
Windows → Windows
```

# 19. 권장 백업 폴더 구조

``` text
vscode-offline/
│
├── mac/
│   ├── vscode-vsix/
│   │   ├── eslint.vsix
│   │   ├── prettier.vsix
│   │   ├── volar.vsix
│   │   └── ...
│   ├── extensions.txt
│   ├── download-vsix.sh
│   └── install-vsix.sh
│
└── windows/
    ├── vscode-vsix/
    │   ├── eslint.vsix
    │   ├── prettier.vsix
    │   ├── volar.vsix
    │   └── ...
    ├── extensions.txt
    ├── download-vscode-vsix.ps1
    └── install-vsix.ps1
```

# 20. 전체 개발환경 백업 권장 구성

``` text
vscode-offline/
│
├── vscode-installer/
├── extensions/
│   ├── mac/
│   └── windows/
├── settings/
│   ├── settings.json
│   └── keybindings.json
├── snippets/
└── README.md
```

# 21. 핵심 명령어 요약

## Mac

설치 확장 확인:

``` bash
code --list-extensions --show-versions
```

설치 폴더 열기:

``` bash
open ~/.vscode/extensions
```

VSIX 다운로드:

``` bash
~/Downloads/download-vsix.sh
```

VSIX 설치:

``` bash
cd ~/Downloads/vscode-vsix

for file in *.vsix; do
    code --install-extension "$file"
done
```

## Windows

설치 확장 확인:

``` powershell
code --list-extensions --show-versions
```

설치 폴더 열기:

``` powershell
explorer "$env:USERPROFILE\.vscode\extensions"
```

VSIX 다운로드:

``` powershell
powershell -ExecutionPolicy Bypass -File .\download-vscode-vsix.ps1
```

VSIX 설치:

``` powershell
Get-ChildItem *.vsix | ForEach-Object {
    code --install-extension $_.FullName --force
}
```

# 22. 최종 권장 운영 방식

인터넷이 가능한 PC:

``` text
1. VS Code 확장 설치
   ↓
2. 확장 ID + 버전 추출
   ↓
3. VSIX 일괄 다운로드
   ↓
4. extensions.txt 저장
   ↓
5. VSIX 폴더 백업
   ↓
6. USB 등으로 폐쇄망 이동
```

폐쇄망 PC:

``` text
1. VS Code 설치
   ↓
2. vscode-vsix 폴더 복사
   ↓
3. VSIX 일괄 설치
   ↓
4. 설치된 확장 및 버전 확인
```

플랫폼별로 가능하면:

``` text
Mac     → Mac
Windows → Windows
```

방식으로 관리합니다.
