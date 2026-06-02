# 🏥 醫療保費預測機器學習 (From Data to Dollars---Predicting Insurance Charges)

本專案旨在利用機器學習模型，透過客戶的個人健康特徵（如年齡、BMI、是否抽菸等）來預測其醫療保險費用，進而協助保險公司進行精準定價與風險評估。

健康保險公司需要精準評估新客戶的潛在醫療開銷。過去若僅憑人工經驗或簡單的統計，難以全面考量多個維度（如年齡、BMI、抽菸習慣、地區等）的交互影響，因此需要引進數據科學方法，建立自動化的保費預測模型，以實現客製化服務並精準控制成本。

* **目標**：利用歷史保單資料集（insurance.csv）訓練一個迴歸模型，用以預測新客戶的醫療保費。
* **評估基準**：模型在訓練集上的 R-Squared 分數必須超越 0.65 門檻。
* **商業限制**：將模型應用於新客戶名單（validation_dataset.csv）時，須嚴格遵守公司法規，確保預測出的基本保費最低不可低於 1,000 元。

為了達成上述目標，使用 Python 進行了完整的資料科學流程：
1. **資料清洗 (Data Cleaning)**：
   * 偵測並剔除資料集中的缺失值（NaN），避免模型訓練出錯。
   * 修正異常的資料型態：發現原始資料中的保費（charges）欄位混有字串符號（如 $ 與 ,），透過常規表示法將其清洗並成功轉換為 float 浮點數型態。
2. **特徵工程 (Feature Engineering)**：
   * 使用 pd.get_dummies() 進行標籤轉換（One-Hot Encoding），將性別、區域、抽菸與否等分類文字特徵轉為數值，使模型能夠讀取。
   * 對齊訓練集與驗證集的欄位結構，防止特徵數量不一致。
3. **模型建立與商業邏輯實作 (Modeling & Prediction)**：
   * 採用線性迴歸模型（Linear Regression）進行模型訓練。
   * 使用 np.where() 建立安全閥，將所有預測值低於 1,000 元的保費強制調整為 1,000 元，完美符合商業法規限制。

* **模型表現優異**：最終模型評估的 R-Squared 分數達到 0.6933，大幅超越專案規定的 0.65 及格基準線，證明模型具備良好的預測能力。
* **成功交付**：順利產出新客戶的保費預測欄位 predicted_charges 並匯出至 validation_data DataFrame，完成端到端的預測流程。

---

## 📂 檔案結構
* notebook.ipynb：主要的資料分析、清洗與模型訓練 Python 程式碼。
* insurance.csv：保險公司的歷史客戶訓練資料。
* validation_dataset.csv：未帶有保費標籤的新客戶驗證名單。

## ⚙️ 使用技術
* **Language**: Python
* **Libraries**: Pandas, NumPy, Scikit-learn (LinearRegression, metrics)
