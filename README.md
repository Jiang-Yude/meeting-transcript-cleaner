# meeting-transcript-cleaner

把錄音變成可信賴的逐字稿，而不是一堆會騙人的錯字。

MacWhisper 之類的本地語音轉文字工具，對中文有系統性的同音字、人名、術語誤轉。最常見的坑是：轉完直接丟給 AI 叫它「幫我整理重點」，結果錯字被當成事實、關鍵字被洗掉，整段脈絡就歪了。

這個技能包是一條完整的逐字稿工作流：先把錯字修乾淨、把講者標對，再交給下游做摘要或改寫。clone 下來丟給 Claude Code 或 Codex 就能用。

## 為什麼做這個

「逐字稿沒清過，錯字會被當成事實，一路傳下去。」

語音轉文字的錯字有系統性：音近的詞會穩定地被換掉，而且 AI 摘要時完全看不出來。要讓逐字稿能用，順序很重要：先 L2 清理（修錯字、保結構、留脈絡），再餵下游，不能跳過。

## 它能做什麼

- **轉錄**：MacWhisper CLI 已驗證規格（路徑、模型清單、單檔／批次／背景轉錄指令）
- **講者校正**：從 MacWhisper 的 SQLite 撈逐字稿、用 Python 匯出、自動合併 diarization 多切出來的「假講者」
- **三等級教學組織**：課程逐字稿分超詳細／很詳細／1:1 三種保留率，長稿用「規劃→執行→抽查」三段分工避免壓縮過頭
- **清稿三大硬性規則**：字數一律用 Python 算、規則必加「主動修正聽錯」條款、跨家審稿防自審放水

## 它不做什麼

- 不做共識分析、會議策略、角色定位（那是會議分析工作流的事）
- 不改寫成文章或貼文（交給寫作工作流）
- 不提煉外部課程的思維框架（交給知識提煉工作流）

這個工作流只負責：轉錄、講者校正、原始逐字稿保存、清稿、品質檢查。清乾淨的稿子交出去，不做深度分析。

## 安裝

把整個資料夾放進你的 Agent 技能包目錄即可：

- **Claude Code**：放到 `~/.claude/skills/meeting-transcript-cleaner/`，或專案的 `.claude/skills/` 下
- **Codex / 其他支援 Agent Skills 的工具**：放到對應的 skills 目錄

放好之後，跟你的 AI 說「幫我清這份逐字稿」「這是 MacWhisper 的逐字稿，先存檔校正講者」就會觸發。

## 環境需求

- macOS（MacWhisper CLI 與 SQLite 流程針對 macOS）
- MacWhisper（轉錄與 SQLite 撈取）
- Python 3（匯出腳本與字數計算）

## 跟 AI 辦公室全家桶的關係

這是「AI 辦公室」系列裡的一位助理，可以單獨抓去用，也可以和其他助理（會議紀錄、順稿、3X4 資料整理等）組成完整工作流。全家桶見 [ai-office-workshop](https://github.com/Jiang-Yude/ai-office-workshop)。

## 授權

MIT License，見 [LICENSE](LICENSE)。

---

## 維護者

江昱德（Jiang Yude）<br>
隱性知識提煉師<br>
AI 知識架構師

[知識官網](https://jiangyude.com/) · [Threads](https://www.threads.com/@jiang_yude_coach)
