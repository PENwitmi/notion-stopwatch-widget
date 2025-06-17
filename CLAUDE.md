# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# CLAUDE.md - Stopwatchプロジェクト専用ガイド

## 🚨 必須の共通ルール（全プロジェクト共通・変更禁止）

これらのルールはすべてのClaude Codeプロジェクトで必須です。プロジェクト固有のルールは「プロジェクト固有情報」セクションに記載してください。

### 1. GitHub自動プッシュ
**ALWAYS commit and push changes to GitHub after making updates.**
- After completing requested changes, immediately commit with a descriptive message
- Push to GitHub to keep the remote repository synchronized
- This ensures all work is backed up and accessible
- Don't wait for explicit requests to push - make it automatic

### 2. CLAUDE.md自動更新
**ALWAYS update CLAUDE.md to reflect current project status.**
- After significant changes, update relevant sections in CLAUDE.md
- Include: database statistics, file structures, new features, issues resolved
- Add timestamped entries to 更新履歴 (Update History) - format: YYYY-MM-DD HH:MM
- This ensures future Claude sessions have accurate project context
- Update immediately after major work - don't wait for requests

#### 更新が必要なタイミング:
- Major feature implementation
- Bug fixes and issue resolution
- Database schema or content changes
- File structure reorganization
- Performance improvements
- New dependencies or tools added

### 3. プロジェクト整理ルール
**When starting a NEW project, ALWAYS create a dedicated project folder first.**
- Example: For a new landing page, create `project-name/` folder first
- Then create all project files inside that folder
- This keeps the `/claude code/` directory organized
- Makes it easy to upload individual projects to GitHub
- CLAUDE.md stays in the root `/claude code/` directory
- Note: This applies only to NEW projects. When working on existing projects, work within their existing folders.

### 4. バックアップ戦略（重要・自動化）
**ALWAYS create backups before ANY file modifications.**

### Backup Process:
1. **Create project backup folder** - `_old_files/backup_YYYYMMDD_HHMM/` in _old_files directory
2. **Copy ALL files to be edited** - Before making ANY changes
3. **Never modify without backup** - This prevents data loss
4. **Keep multiple backups** - For major changes, create new backup folders
5. **Organize in _old_files** - Keep project directory clean

### Example:
```bash
# Before editing files in pharm-tutor-lp project
mkdir _old_files/backup_$(date +%Y%m%d_%H%M)
cp index.html _old_files/backup_$(date +%Y%m%d_%H%M)/
cp -r css/ _old_files/backup_$(date +%Y%m%d_%H%M)/
# Now safe to edit files
```

### Why This Matters:
- Prevents irreversible data loss
- Allows rollback to previous versions
- Maintains project history
- Protects against AI tool errors

### 5. 進捗レポート作成ルール（重要・必須）
**ALWAYS create a main progress tracker for multi-session projects.**

#### 進捗レポート作成判定:
**作成必須の条件（いずれか該当）:**
- 3回以上のセッションにわたる作業
- 複数のファイル・機能を扱う複雑なプロジェクト
- レポートが5個以上生成される見込み
- チームでの共有・引き継ぎが必要

#### 進捗レポートの必須要素:
1. **プロジェクト概要** - 目標・現状・次のステップ
2. **完了タスク・実行中タスク・待機中タスク**
3. **📋 関連重要レポート** - すべての関連ファイルへのパス
4. **技術的課題・解決状況**
5. **定量的成果・進捗指標**

#### ファイル配置・命名:
- **場所**: `reports/[project_name]_progress_tracker.md`
- **CLAUDE.mdでの記載**: 1行のみ（パスと簡潔な説明）
- **相対パス使用**: 関連レポートは同じreportsフォルダ内に配置

#### 例:
```
### プロジェクト管理
- **reports/database_expansion_progress_tracker.md** - 拡充進捗管理（関連レポート含む）
```

#### 防止される問題:
- レポートの迷子・セッション継続困難
- CLAUDE.mdの肥大化
- 重要情報への迷子アクセス

### 6. CSS開発のベストプラクティス
**NEVER let CSS files grow beyond 20-30KB without proper management.**

### Problems Identified:
1. **Uncontrolled CSS growth** - Single file grew to 94KB with massive unused code
2. **Copy-paste development** - Reusing templates without removing unused styles
3. **No CSS architecture** - Adding styles without structure or cleanup
4. **No automated tools** - Manual CSS management is error-prone and incomplete

### Mandatory Practices for Future Projects:
1. **Start with minimal CSS** - Build only what you need, when you need it
2. **Use CSS methodology** - BEM, OOCSS, or similar systematic approach
3. **Regular CSS audits** - Review and remove unused styles weekly
4. **Automated tools** - Integrate PurgeCSS, UnCSS, or similar in build process
5. **File size limits** - CSS files should not exceed 30KB without justification
6. **Component-based CSS** - Write styles per component, not monolithic files

### Tools to Use:
- PurgeCSS for automated unused CSS removal
- CSS Coverage in Chrome DevTools for analysis
- Build tools (Vite, Webpack) with CSS optimization
- Critical CSS extraction for performance

### Red Flags:
- CSS files over 50KB
- Hundreds of unused classes
- Copy-pasting CSS without cleanup
- No systematic naming convention

---

## 📋 プロジェクト固有情報（以下を編集してください）

### プロジェクト概要
- **プロジェクト名**: Notion Stopwatch Widget
- **タイプ**: Notion埋め込み用Webウィジェット
- **目的**: Notionページに埋め込み可能なストップウォッチウィジェットを開発し、時間計測、ラップタイム記録、計測履歴管理を提供する
- **ターゲット**: 
  - Notionを利用している個人ユーザー
  - チーム・組織でのタスク管理、時間管理を行うユーザー
  - 作業時間、会議時間、学習時間等の計測ニーズがあるユーザー

### ファイル構造
```
stopwatch/
├── CLAUDE.md                   # プロジェクト管理ファイル
├── stopwatch_definition.txt    # 要件定義書
├── definition_add.txt          # モバイル最適化追加要件定義書
├── add2.txt                    # Notion縮小問題対策追加要件定義書
├── index.html                  # メインファイル（HTML/CSS/JS統合、24KB）
├── README.md                   # 使用方法、Notion埋め込み手順
├── NOTION_EMBED_INSIGHTS.md    # Notion埋め込み問題の知見まとめ
└── .claude/
    └── settings.local.json
```

### 使用技術・依存関係
- **フロントエンド**: HTML5, CSS3, JavaScript (Vanilla JS)
- **ホスティング**: GitHub Pages
- **バージョン管理**: Git, GitHub
- **外部ライブラリ**: なし（Notion埋め込み制約のため）
- **対象ブラウザ**: Chrome 90+, Firefox 90+, Safari 14+, Edge 90+

### 重要な注意事項

#### 機能要件
- **時間計測機能**: 開始/停止/リセット、MM:SS.mm形式での表示（10ms精度）
  - 60分以上の場合: Hh MM:SS.mm形式（例: 1h 30:45.99）で表示
- **ラップタイム機能**: 最新5件まで表示
- **計測履歴機能**: 最新5件まで表示（セッション内のみ保存）

#### UI/UXデザイン仕様
- **レイアウト**: 横長（推奨: 幅700px × 高さ250px）
- **エリア構成**: メイン表示エリア（60%）+ データ表示エリア（40%）
- **デザインテイスト**: スタイリッシュ × シンプル（高級時計、Apple Watch UI風）
- **カラーパレット**:
  - メインカラー: ディープブルー (#1a365d)
  - アクセントカラー: ライトブルー (#3182ce)
  - テキストカラー: ダークグレー (#2d3748)
  - 背景色: ライトグレー (#f7fafc)

#### Notion埋め込み制約
- **iframe対応**: 必須
- **HTTPS通信**: 必須
- **外部リソース**: 制限あり（CDN使用不可）
- **ポップアップ**: 使用不可
- **ファイルサイズ**: HTML+CSS+JS合計で100KB以下

#### モバイル最適化（2025-06-17実装）
- **新ボタンレイアウト**: 600px以下でStartボタンを大型化（CSS Grid）
- **タッチ操作**: フィードバック強化、ズーム無効化、タッチエリア拡張
- **レスポンシブ対応**: 320px極小画面対応、画面向き対応
- **パフォーマンス**: GPU加速、60fps維持

#### Notion縮小問題対策（2025-06-17実装）
- **縮小検出システム**: コンテナ幅/画面幅から縮小を自動検出
- **スタイル拡大補正**: フォントサイズ1.5倍、ボタンサイズ1.4倍
- **全体スケール調整**: transform: scale(1.15)で追加補正
- **デバッグモード**: ?debug=1で検出結果を表示

### よくある作業・コマンド
```bash
# GitHubへのプッシュ
git add .
git commit -m "commit message"
git push origin main

# ローカルでのテスト（簡易HTTPサーバー）
python -m http.server 8000
# または
npx http-server

# GitHub Pagesの公開URL
# https://[username].github.io/[repository-name]/
```

### 価格・コンテンツ情報
- 無料のWebアプリケーション

### 更新履歴
- 2025-06-17 12:15: プロジェクト初期化、CLAUDE.md作成
- 2025-06-17 12:20: 要件定義書の内容を反映、詳細仕様を追加
- 2025-06-17 12:30: 開発完了、全機能実装完了（index.html 12KB、README.md作成）
- 2025-06-17 13:10: モバイル最適化実装完了（新ボタンレイアウト、タッチ操作最適化、画面向き対応、19KB）
- 2025-06-17 13:25: Notion縮小問題の根本的解決（縮小検出＋拡大補正、デバッグモード追加、24KB）
- 2025-06-17 14:00: 60分以上の時間表示機能追加（Hh MM:SS.mm形式、例: 1h 30:45.99）