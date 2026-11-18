# Anti-Defensive Chat (`anti-defensive-chat`)

> **Stop AI from hedging, fence-sitting, sycophantically folding, or preaching in daily chat.**  
> **消除日常聊天中的 AI 防御性回答：不叠免责甲、不和稀泥、无新证据不滑跪、有实锤错不圆场、零爹味说教。**

---

## Why This Exists (核心痛点)

Most LLMs are post-trained to be conflict-averse customer service agents. In everyday conversation, this produces five annoying **defensive behaviors**:

1. **Preemptive Disclaimers (预防性叠甲)**: Padding answers with *"It depends on many factors," "For informational purposes only,"* or *"Of course, there are exceptions"* just to avoid being wrong.
2. **Bothsidesism / Fence-Sitting (和稀泥不站队)**: Refusing to pick a winner between A and B (*"Both have their pros and cons, weigh your personal needs"*).
3. **Sycophantic Folding vs. Goalpost-Moving (被反问就滑跪 / 强行圆场)**: Instantly caving with *"You're absolutely right! My apologies!"* when challenged without evidence—or conversely, redefining terms to rationalize a real math/fact error.
4. **Preachy Moralizing (爹味说教与强行升华)**: Turning everyday venting or office-politics questions into unsolicited lectures on *"staying positive and communicating openly."*
5. **Shotgun List-Dumping (防御性穷举清单)**: Dumping 10 generic bullet points when a prompt is slightly ambiguous instead of giving the best default answer and asking one decisive question.

`anti-defensive-chat` fixes all five while **strictly preserving genuine epistemic uncertainty** (real evidence limits are stated plainly; verbal CYA padding is stripped).

---

## Repository Structure (目录结构)

```text
anti-defensive-chat/
├── plugin.json                             # Antigravity plugin manifest
├── .claude-plugin/
│   ├── plugin.json                         # Claude Code plugin manifest
│   └── marketplace.json                    # Claude Code marketplace catalog
├── .codex-plugin/
│   └── plugin.json                         # OpenAI Codex CLI plugin manifest
├── .agents/plugins/
│   └── marketplace.json                    # Codex / Agent marketplace catalog
├── skills/
│   ├── anti-defensive-chat/SKILL.md        # 中文完整版 Skill（含六大准则、正反例对照、三档切换）
│   └── anti-defensive-chat-en/SKILL.md     # English full Skill
├── rules/
│   └── AGENTS.md                           # Always-on compact rule block for persistent daily chat
└── prompts/
    ├── quick-prompt-zh.md                  # 零门槛粘贴版（适用于 ChatGPT / Claude Web 自定义指令）
    └── quick-prompt-en.md                  # Zero-install paste-in Custom Instructions (EN)
```

---

## Installation (安装方式)

### 1. Universal Agent Skills CLI (`npx skills`)
Works across Claude Code, Cursor, Codex, Gemini CLI, Antigravity, and other compatible agents:
```bash
npx skills add W-aPoint/anti-defensive-chat
```

### 2. Claude Code Plugin
```text
/plugin marketplace add W-aPoint/anti-defensive-chat
/plugin install anti-defensive-chat@w-apoint-anti-defensive-chat
```
Or copy the skills directly:
```bash
mkdir -p ~/.claude/skills
git clone --depth 1 https://github.com/W-aPoint/anti-defensive-chat.git /tmp/anti-defensive-chat
cp -r /tmp/anti-defensive-chat/skills/anti-defensive-chat ~/.claude/skills/
cp -r /tmp/anti-defensive-chat/skills/anti-defensive-chat-en ~/.claude/skills/
```

### 3. OpenAI Codex CLI
```bash
codex plugin marketplace add W-aPoint/anti-defensive-chat
```

### 4. Antigravity / Gemini CLI
Clone or copy the skills (on-demand) or the entire plugin (includes always-on `rules/AGENTS.md`):
```powershell
git clone --depth 1 https://github.com/W-aPoint/anti-defensive-chat.git "$env:TEMP\anti-defensive-chat"

# Install as standalone skills (按需触发 Skill)
Copy-Item -Recurse "$env:TEMP\anti-defensive-chat\skills\anti-defensive-chat" "$HOME\.gemini\config\skills\"
Copy-Item -Recurse "$env:TEMP\anti-defensive-chat\skills\anti-defensive-chat-en" "$HOME\.gemini\config\skills\"

# Or install as a full plugin (包含常驻规则 + 双语 Skill)
Copy-Item -Recurse "$env:TEMP\anti-defensive-chat" "$HOME\.gemini\config\plugins\anti-defensive-chat"
```

### 5. ChatGPT / Claude Web (Custom Instructions)
Copy the contents of [`prompts/quick-prompt-zh.md`](./prompts/quick-prompt-zh.md) or [`prompts/quick-prompt-en.md`](./prompts/quick-prompt-en.md) directly into your **Custom Instructions** / **Project Instructions**.

---

## Intensity Modes (三档强度口令)

Once loaded, you can switch intensity at any time during chat:
- `/direct lite` — **温和直给档**：保留日常聊天的自然语气，但砍掉免责叠甲、和稀泥与说教。
- `/direct full` *(Default)* — **标准平级档**：结论先行 + 拒绝端水 + 无新证据不滑跪 + 零寒暄零说教。
- `/direct frank` — **诤友交锋档**：默认开启压力测试（Adversarial Critique），主动攻击想法或计划中最薄弱的一环。

---

## Credits & Inspirations (参考与致谢)

Synthesized and refined from the best open-source anti-sycophancy, anti-hedging, and direct-communication projects on GitHub:
- [`andykear/Peer`](https://github.com/andykear/Peer) — Decide-first colleague persona & evidence-based pushback handling
- [`0xcjl/anti-sycophancy`](https://github.com/0xcjl/anti-sycophancy) — Premise testing & confirmation-bias interception (*Ask, Don't Tell*)
- [`huxleyli15/frank`](https://github.com/huxleyli15/frank) & [`itsryanlenk/candor`](https://github.com/itsryanlenk/candor) — Verdict-first structure, steelmanning, and intensity tiers
- [`feizhuzheng/antiaiaiclub`](https://github.com/feizhuzheng/antiaiaiclub) — Anti-bothsidesism & Chinese conversational de-fluffing
- [`JuliusBrussee/caveman`](https://github.com/JuliusBrussee/caveman) & [`wanshuiyin/HERO-Anti-OverDefense`](https://github.com/wanshuiyin/HERO-Anti-OverDefense) — Killing ceremony & defensive list-dumping
- [`Adkid-Zephyr/anti-defensive-writing-Skill`](https://github.com/Adkid-Zephyr/anti-defensive-writing-Skill) & [`op7418/Humanizer-zh`](https://github.com/op7418/Humanizer-zh) — Priority constraints & before/after boundary examples
