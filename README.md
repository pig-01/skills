# skills

可透過 [skills CLI](https://github.com/vercel-labs/skills) 安裝的 agent skills。

## 可用 skills

| Skill | 用途 |
| --- | --- |
| [step-up](skills/step-up/SKILL.md) | 初始化工作目錄的簡單範例：建立 README、忽略規則、`src/` 與 `docs/`，並保留已有檔案。 |

## 安裝到 Codex

需要先安裝 [Node.js](https://nodejs.org/)（包含 npm / npx）與 [Git](https://git-scm.com/)。

```sh
npx -y skills@latest add pig-01/skills --skill step-up --agent codex --global --yes
```

- `--skill step-up`：選擇要安裝的 skill。
- `--agent codex`：指定 Codex。
- `--global`：安裝到使用者範圍，供各專案使用；省略時安裝到目前專案。
- 開頭的 `-y` 省略 npx 下載套件的確認；結尾的 `--yes` 省略 skills CLI 的安裝確認。

列出此 repository 可安裝的 skills：

```sh
npx -y skills@latest add pig-01/skills --list
```

安裝後可在 Codex 中使用：

```text
使用 $step-up 幫我初始化目前的工作目錄。
```

或指定目標路徑：

```text
使用 $step-up 在 ./my-project 建立一個新的工作目錄。
```

## 目錄結構

```text
skills/
└── step-up/
    └── SKILL.md
```

## 新增自己的 skill

在 `skills/<skill-name>/SKILL.md` 撰寫指示，檔案開頭需包含 YAML frontmatter：

```markdown
---
name: my-skill
description: 簡述此 skill 的用途與適用情境。
---

# My Skill

填入 agent 應遵循的具體工作方式與完成條件。
```

`name` 應與資料夾名稱一致，並且在此 repository 中唯一。安裝時的 `--skill` 對應 frontmatter 的 `name`。

推送到 GitHub 的預設分支後即可安裝：

```sh
npx -y skills@latest add pig-01/skills --skill my-skill --agent codex --global --yes
```

不需要發布 npm 套件或註冊套件名稱。`skills@latest` 是安裝工具；`pig-01/skills` 是存放 skill 的 GitHub repository。

本機修改後，可先確認 skills 能被辨識：

```sh
npx -y skills@latest add . --list
```
