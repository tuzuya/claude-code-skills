# claude-code-skills

Claude Code 用のスキル集です。プラグインのマーケットプレイスとしてそのまま追加できます。
（English below）

| スキル | 内容 |
|---|---|
| [coding-coach](plugins/coding-coach/skills/coding-coach/SKILL.md) | コードを書くのはあなた。Claude はコーチに徹して、役割の説明・文法カード・段階的なヒント・狭く速いチェックで伴走する |

## coding-coach

「動くコードを最速で手に入れる」ではなく、「自分の手で実装できるようになる」ためのモードです。
読むことはできるけど書いた経験が少ない言語・フレームワークを、実際のプロジェクトで書きながら覚えたい人向けです。

### 特徴

- **先に方向性を合意し、全体のステップ数を最初に示す**
- **各ステップの最初に「何のためのコードか」を見せる**（🗺）: ユーザーの操作から始まる流れの中で、
  今のステップがどこで動くか（★）と、後で書く呼び出し側のコードを先に見せます
- **文法は伏せない、伏せるのはロジックだけ**: 知らない文法は「📘 文法カード」（無関係な題材の短い例）で先に見せます。
  空欄になるのは、設計と判断の部分だけです
- **ヒントの強さは4段階**（Lv1 ファイルを指すだけ 〜 Lv4 ほぼ完成のコード。核心は必ず空欄）。途中でいつでも変えられます
- **チェックは今のステップの差分だけ**: 型チェック・lint・関係するテストだけを実行します。
  テストのステップでは「わざと壊した実装でも通ってしまわないか」も見ます
- **進み具合と習熟度をリポジトリに保存**: 次の会話や別の PC からでも、「続きから」で再開できます

### プロジェクトに作られるファイル

| ファイル | 内容 |
|---|---|
| `.coaching/knowledge.md` | 文法・イディオムの習熟度（使える / 説明すれば使える / 未習）と、学習の前提（書いた言語・読んだ言語・対比できる既知の技術） |
| `.coaching/progress.md` | 今のタスクで合意した方針・ステップ一覧・現在地 |

git にコミットしておくと、別の PC でも同じ状態から再開できます。場所を変えたい場合は、
プロジェクトの `CLAUDE.md` に `coding-coach の知識プロファイルは docs/coach/knowledge.md に置く` のように書いてください。

### インストール

**A. プラグインとして入れる（おすすめ）**

```
/plugin marketplace add tuzuya/claude-code-skills
/plugin install coding-coach@tuzuya-skills
```

**B. スキルのフォルダをコピーする**

`plugins/coding-coach/skills/coding-coach/` を、次のどちらかにコピーします。

- 全プロジェクトで使う: `~/.claude/skills/coding-coach/`
- 1つのプロジェクトだけで使う: `<プロジェクト>/.claude/skills/coding-coach/`

### 使い方

```
/coding-coach ログイン画面のバリデーションを実装したい。ヒントレベルは3で
```

または、普段の会話で「ヒントだけ出して」「自分で書きたい」「コーチモードで」などと言うと起動します。

- 書けたら `check` と言うと、そのステップだけをチェックします
- `レベル2で` / `もっとヒント`: ヒントの強さを変えます
- `このステップは答えを見せて`: そのステップだけ Claude が書きます（解説つき）。次のステップからはコーチに戻ります
- `続きから` / `ステップ5から`: `.coaching/progress.md` を読んで再開します

初めて使うときは、書いたことのある言語などを2〜3問だけ聞かれます。

---

## English

A collection of Claude Code skills, installable as a plugin marketplace.

### coding-coach

A mode for learning by building: **you write the code; Claude coaches.**
Aimed at people who can read a language or framework but haven't written much of it.

- Agrees on the approach first and shows the total number of steps
- Opens every step with **🗺 what this code is for** — where it runs in a flow that starts from a user
  action, and a preview of the code that will call it
- **Never hides syntax, only logic**: unfamiliar syntax is shown up front as **📘 syntax cards**
  (short examples on unrelated subjects); only design decisions are left blank
- **Four hint levels** (Lv1 points at files … Lv4 nearly complete code with the core left blank), changeable at any time
- **Narrow checks**: only this step's diff, type check, lint, and related tests — including
  "would a deliberately broken implementation still pass this test?"
- **Progress and proficiency are saved in your repo** (`.coaching/knowledge.md`, `.coaching/progress.md`),
  so you can say "continue" in a new session or on another machine

**Install**

```
/plugin marketplace add tuzuya/claude-code-skills
/plugin install coding-coach@tuzuya-skills
```

Or copy `plugins/coding-coach/skills/coding-coach/` into `~/.claude/skills/` (all projects) or
`<project>/.claude/skills/` (one project).

**Use**: `/coding-coach implement the login form validation, hint level 3`, or just say
"coach me through this" / "I want to write it myself". Say `check` when a step is done.

## License

MIT
