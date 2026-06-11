# Launch Review 議程（90 分鐘版）

> 適用：Falcon‑1（$1 Gumroad 上架）發射前評審會 
> 參與人數建議：6–10 人（兩披薩隊規模），超過就拆會。

### 會前（T‑24h，非會議時間）
- 文件：PR/FAQ（External）＋ Internal FAQ 放同一份 Doc（建議 Google Doc / Notion）。
- 主持人（Host）設定：會議邀請上寫清楚「本會議第一段為靜讀，請準時」。
- 會議目標寫死（放在文件最上方）： 
 - **目標**：決定是否在 X 日上架（Go / No‑Go / Conditional Go），並鎖定發射後 7 天的指標與 owner。

### 0:00–0:03（3m）開場規則宣示（Host）
- 今天不是來「推銷」或「辯贏」，是來**找真相與補洞**（truth‑seeking vs selling 的 PR/FAQ 精神）。
- 會議規則： 
 - 不看投影片；只看文件。 
 - 先寫再說：靜讀期間把問題打在文件上。 
 - 討論只處理「會影響決策」的問題。

### 0:03–0:23（20m）靜讀＋批註（Silent Reading）
- 全員靜音，開計時器 20 分鐘。 
- 每個人邊讀邊在文件上留言（用下方「批註標籤」格式）。
- 結束時，每人貼一句「Done reading」到會議聊天室（或在文件最上方打 ✅）。

### 0:23–0:28（5m）主持人彙整「必答清單」
Host 快速掃描留言，把問題分三類（只留最重的）：
1. **Blocking**：不解決就不能上線（例如交付不清、退款政策缺失、會造成信任崩壞的風險）。 
2. **Non‑blocking but important**：可上線，但必須排入 T+7 修正。 
3. **Nice to have**：先不討論，放 parking lot。

### 0:28–1:10（42m）逐頁 / 逐段質詢（Structured Q&A）
建議採「Page‑by‑page」或「Section‑by‑section」：PR → External FAQ → Internal FAQ。
規則：每個問題最多 3 分鐘，超時就變成 action item。
- PR 段：顧客定位是否清楚？價值主張是否可被驗證？ 
- External FAQ：是否誠實處理限制？是否降低退款風險？ 
- Internal FAQ：假設是否可驗證？定價上移是否合理？風險控管是否足夠？

### 1:10–1:20（10m）決策與條件（Decision Gate）
由 DRI（單一負責人）提出其中一個結論，並把條件寫進文件：
- **GO**：可上架，列出 T+7 的修正清單。 
- **CONDITIONAL GO**：達成 X 個 blocking items 後上架（例如 24h 內完成）。 
- **NO‑GO**：回去改第 N 版 PR/FAQ，下次再 review。

### 1:20–1:30（10m）行動清單＋Owner＋截止時間（Action Register）
把所有 action items 寫成固定格式，並立刻指派 owner 與 due date：
- [ ] **Action**：… 
- **Owner**：… 
- **Due**：… 
- **Why it matters**：對轉換率/信任/成本的影響

***

## 靜讀批註模板（直接複製貼上）

> 目的：讓每個留言都可被「分類→回答→結案」，避免散彈式評論。

### 批註標籤（請固定用這些開頭）
- [Q] 問題：我不理解/我需要澄清的是… 
- [ASSUMP] 假設：這裡依賴的假設是…；如何驗證？ 
- [RISK] 風險：如果這成立/不成立，最糟會發生什麼？ 
- [METRIC] 指標：上線後要用什麼衡量？門檻值是多少？ 
- [DECISION] 決策：這裡需要拍板（A/B/不做） 
- [SCOPE] 範圍：這是不是超出 MLP？要不要延後？ 
- [COPY] 文案：這句話會不會造成誤解/不夠 sharp？建議改成… 
- [OPS] 交付/客服：下載、格式、支援、退款會卡在哪？ 
- [LEGAL] 合規：收益暗示、誇大、授權條款有沒有雷？ 
- [PARK] 停車場：好點子但今天不討論，放這裡。

### 每則留言格式（請照填）
**[TAG] 一句話摘要：** 
**為什麼重要（1 句）：**（影響信任 / 轉換 / 成本 / 交付） 
**建議（可選）：**（寫出具體替代文字或 action） 
**需要決策？**（是/否；若是，選項 A/B） 

***

## 會議角色（強烈建議）
- **DRI（單一負責人）**：負責最後的 Go/No‑Go 與取捨。 
- **Host（主持人）**：控時、彙整 blocking items、維持規則。 
- **Scribe（紀錄官）**：會中只做一件事：把 action register 寫乾淨。 
- **Bar Raiser（品質挑刺手）**：專門抓「會傷害信任」的問題（交付、誤導、退款、限制）。 

***

## 會後輸出（必交付物）

1. **Decision Log**：GO / CONDITIONAL GO / NO‑GO（含理由與條件）。
2. **Action Register**：每條 action 有 owner + due date。 
3. **Launch Metrics**（上架後 7 天）：至少 3 個指標＋門檻（例如 CVR、退款率、回覆問題密度）。 
4. **Next Review Date**：下次 PR/FAQ review 時間（PR/FAQ 天生就會迭代多版）。
