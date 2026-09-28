# Code Signing Policy

## 日本語

2026年9月28日の1.1.0再公開版は、監査した公開ソースの固定候補から、管理された
ローカルWindows環境で生成したAnyCPUポータブル版です。Y-TEC製の最終EXE/DLLを
既存のY-TEC自己署名証明書でAuthenticode署名し、SHA-256のRFC 3161タイムスタンプ、
ファイルダイジェスト、署名者、署名の暗号学的整合性を検証してからZIPを確定します。
同梱Newtonsoft.Jsonは第三者の署名を保持し、別に検証します。

自己署名は商用CAによる標準信頼済み署名でもSignPath Foundation署名でもありません。
未信頼ルートによるWindowsの信頼警告は想定内ですが、破損、署名者不一致、
ダイジェスト不一致、タイムスタンプ欠落は公開阻害です。配布はPreviewとして案内し、
SmartScreen警告の解消を保証しません。公開鍵だけのCERは任意の検証補助物であり、
アプリやスクリプトから証明書ストアまたはTrusted Rootへ自動登録しません。

公式版は、1.0.0以降の公式バックアップとの互換性を維持する32バイトの既存互換鍵を
ビルド時にDLLリソースへ埋め込みます。鍵を生成・変更せず、公開ソース、ログ、
Workflow Artifact、配布物に単独ファイルとして含めません。公開ソースの標準ビルドは
公開開発鍵を使い警告を表示します。独自鍵のビルドは公式版と互換性がありません。
内蔵鍵は解析可能であり、高度な解析への秘匿性は保証しません。

`eng/New-PortableRelease.ps1`と`eng/Test-PortableRelease.ps1`は署名前の中間候補を
作成・検証する手順です。そのZIPを正式配布しません。最終署名後に内外のSHA-256と
ZIPを再生成し、日英マニュアル、NOTICE、第三者通知、版数と内容を再検査します。
GitHub Actionsは公開開発鍵による検証だけを実行し、署名、公式鍵へのアクセス、
Artifactアップロード、Release公開は行いません。公開は所有者の個別承認後に行います。

Store版は未公開です。旧Windowsを含むポータブル用途のため、ForgeとGitHub Releasesを
直接配布元とし、手動更新を案内します。アプリ自体に外部通信や自動更新はありません。
詳細は[プライバシーポリシー](PRIVACY.md)を参照してください。

## English

The September 28, 2026 republication of version 1.1.0 is an AnyCPU portable
Preview rebuilt locally from the audited, frozen public-source candidate.
Final Y-TEC EXE/DLL files receive Authenticode signatures using the existing
Y-TEC self-signed certificate and SHA-256 RFC 3161 timestamps. File digests,
signer identity and cryptographic signature integrity must pass verification.
The bundled Newtonsoft.Json library retains its independently verified upstream
signature. An untrusted self-signed root is expected; a damaged signature,
wrong signer, digest mismatch or missing timestamp blocks publication.

This is not a trusted commercial-CA or SignPath Foundation signature.
SmartScreen warnings may remain. The optional CER contains only the public
certificate; no program or script automatically installs it into certificate
stores or Trusted Root.

Official builds embed the existing 32-byte compatibility input as a DLL resource
to preserve compatibility with official backups since 1.0.0. No standalone key
file is published in source, logs, workflow artifacts or downloads. Standard
public-source builds use the documented public development key and show a
warning; custom-key builds are incompatible with official backups. Embedded
keys can be recovered by an analyst and are not a high-assurance secret boundary.

The portable-release scripts produce and validate an unsigned intermediate,
not a final download. After signing, the final ZIP and inner/outer SHA-256
manifests are regenerated and audited with both manuals and legal notices.
Actions validate public-source builds only; they do not access the official key,
sign, upload artifacts or publish releases. Publication requires owner approval.
Microsoft Store distribution is not available. Forge and GitHub Releases provide
manual-update portable downloads; the app has no network traffic or auto-updater.

Official pages: [日本語](https://ytec.cloudfree.jp/forge/projects/wifi-capsule/)
and [English](https://ytec.cloudfree.jp/forge/en/projects/wifi-capsule/).
Contact: [Y-TEC Forge](https://ytec.cloudfree.jp/forge/contact/).
Do not submit real Wi-Fi data.
