# 新勢力分會 · 綠燈追分儀表板

BNI **新勢力 Dynamics Chapter** 的攻綠燈計分工具。夥伴點連結即可看自己的紅綠燈進度；副主席每週把 PALMS 匯出檔上傳到 `data/`，夥伴重整就看到最新。

## 連結

- **夥伴看的網址**：https://geniusjohn0502.github.io/newforce-greenlight/
- **每週上傳 PALMS**：https://github.com/geniusjohn0502/newforce-greenlight/upload/main/data

## 每週更新流程（3 步）

1. 開上傳連結，把本週 PALMS 匯出檔拖進 `data/`
   - 可直接上傳 BNI 匯出的原始檔（`.xls` / XML）或 CSV，**檔名含日期**（如 `newforce-2026-07-21.csv` 或 BNI 原生 `21-07-2026`）系統會自動讀出基準日
2. Commit
3. 夥伴重整頁面即看到最新

## 計分邏輯（與大千版的差異）

- **開會日：每週二**（`MEETING_DAY = 2`）
- **分會 2026/4 成立**：未滿六個月採「按比例」計分，本期週數起點固定在成立日 4/1（`CHAPTER_START`）
- **十月起自動切滾動六個月**：分母寫死自動判斷，`起點 = 較晚者(成立日, 當月月底往前推六個月)`，並封頂在六個月開會日上限——即使 PALMS 仍匯「成立至今」全部場次，也會自動縮回六個月區間，不需手動改程式
- 紅綠燈門檻沿用 BNI 全國標準（綠燈 70 分）

## 本期週數算法

```
本期週數 = min( base ＋ 月底前剩餘週二 , 滾動六個月開會日上限 )
base = PALMS 全分會最高出席場次（成立至今實際開會數，自動跳過停會週）
```

例：2026-07-21 上傳 → base 10 ＋ 月底前 1 次週二（7/28）= 11 週。

## 技術

- 單一 `index.html`，純瀏覽器端運算，無後端。
- 開頁自動 `fetch` 本 repo `data/` 最新一份檔（GitHub API 列檔 + raw 下載）。
- 管理：灰哥（owner）維護 `index.html`；副主席為 collaborator，負責每週上傳。
