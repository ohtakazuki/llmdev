python -m venv .venv
.venv/Scripts/activate
python -m pip install --upgrade pip
python -m pip install -r requirements.txt


$currentPath = [Environment]::GetEnvironmentVariable("Path", "Machine")
$newDir = (Get-Command cl.exe).Path | Split-Path
if (-not ($currentPath -split ";" | ForEach-Object { $_.Trim() } | Where-Object { $_ -eq $newDir })) {
    $newPath = "$currentPath;$newDir"
    [Environment]::SetEnvironmentVariable("Path", $newPath, "Machine")
}
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser

# サンドボックスの日本語化
Set-WinUserLanguageList -Force ja-JP      # 言語リストとプロパティを日本語に設定
Set-WinSystemLocale -SystemLocale ja-JP   # システムロケールを 日本 に変更
Set-WinUILanguageOverride -Language ja-JP # 表示言語と地域設定を 日本語 に変更
Set-WinHomeLocation 122                   # 国と地域を 日本 に変更
Restart-Computer                          # システムを再起動
