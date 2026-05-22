# 假新聞分類專案（Fake News Detection）

這個專案使用 `Fake.csv` 與 `True.csv` 兩份資料集，建立一個二元分類模型，用來判斷新聞內容是 **Fake** 還是 **Real**。

目前主要工作集中在：
- 資料前處理與標記
- 特徵工程與探索式分析（EDA）
- 文字向量化（TF-IDF）
- 模型訓練與比較（Logistic Regression、LinearSVC）
- 評估指標與視覺化（Confusion Matrix、ROC、PR Curve）

---

## 專案結構

```text
.
├─ Fake.csv
├─ True.csv
├─ Training.ipynb
├─ eda_analysis.png
├─ model_comparison.png
└─ roc_pr_curve.png
```

---

## 你目前完成了什麼

### 1. 資料讀取與標籤建立
- 載入兩份資料：`Fake.csv`、`True.csv`
- 新增 `label` 欄位：
  - `0` = Fake
  - `1` = Real
- 合併後隨機打散（固定 random_state）

### 2. 建立文本欄位
- 將 `title` 與 `text` 合併成 `content`，作為模型輸入文本

### 3. 特徵工程（EDA 用）
你額外建立了多個可解釋特徵來比較 Fake/Real 的文本風格：
- `text_len`：內文字元數
- `word_count`：詞數
- `title_len`：標題長度
- `exclaim_count`：驚嘆號數量
- `question_count`：問號數量
- `upper_ratio`：大寫字母比例

### 4. 視覺化分析
你建立了多張圖觀察資料分布與語言特徵差異，包含：
- Label Distribution（類別比例）
- Text Length Distribution
- Word Count Box Plot
- Exclamation Marks 使用差異
- Uppercase Ratio 分布
- Top Subjects（Fake vs Real）

輸出圖檔：
- `eda_analysis.png`

### 5. 訓練與測試資料切分
- 使用 `train_test_split`，測試集比例 `0.2`

### 6. 文字向量化
- 使用 `TfidfVectorizer`：
  - `max_features=10000`
  - `stop_words="english"`
  - `ngram_range=(1, 2)`

### 7. 模型訓練與比較
目前嘗試的模型：
- Logistic Regression
- LinearSVC（搭配 CalibratedClassifierCV，產生機率以便畫 ROC/PR）

並輸出：
- 每個模型的分類報告（Precision / Recall / F1 / Accuracy）
- Confusion Matrix
- ROC Curve（AUC）
- Precision-Recall Curve（AUPRC）

輸出圖檔：
- `roc_pr_curve.png`
- `model_comparison.png`

---

## 如何執行

1. 開啟 `Training.ipynb`
2. 依序執行所有 cells
3. 檢查輸出圖檔與模型評估結果

建議環境（至少需安裝）：
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

---

## 後續可以玩的方向

- 嘗試更多模型（如 MultinomialNB、XGBoost、LightGBM）
- 加入文字清理流程（去停用詞、詞形還原、正規化）
- 改變 TF-IDF 參數（min_df、max_df、ngram）
- 做交叉驗證（Cross Validation）取代單次切分
- 加入模型保存與推論函式（deployment-friendly）
- 做錯誤分析（看哪些樣本最容易被誤判）

---

## 進度表（可持續更新）

| 項目 | 狀態 | 說明 |
|---|---|---|
| 資料讀取與標記 | 已完成 | Fake/True 合併並建立 label |
| 基礎前處理 | 已完成 | 建立 content 欄位（title + text） |
| EDA 與特徵工程 | 已完成 | 長度、詞數、符號與大寫比例等特徵 |
| 視覺化輸出 | 已完成 | 已產出 EDA 與模型比較圖 |
| TF-IDF 向量化 | 已完成 | 使用 unigram + bigram |
| 模型訓練（LR / LinearSVC） | 已完成 | 完成訓練與推論 |
| 模型評估（ROC/PR/CM） | 已完成 | 含 AUC、AUPRC、Confusion Matrix |
| 超參數調整 | 進行中 | 可用 GridSearchCV / RandomizedSearchCV |
| 新模型擴充 | 未開始 | 待加入 Naive Bayes、Boosting 類模型 |
| 模型保存與推論 API | 未開始 | 待補 joblib 與推論流程 |
| 錯誤分析報告 | 未開始 | 待分析高信心誤判樣本 |

> 你之後每次做新實驗，可以直接更新這張表的「狀態」和「說明」。