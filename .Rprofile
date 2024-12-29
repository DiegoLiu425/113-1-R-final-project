library(tidyverse)
# 匯入 CSV 檔案
data <- read_csv("臺中市納骨塔使用情形.csv")

# 檢視資料
glimpse(data)

# 根據可使用櫃位數排序納骨塔（降序排列）
data <- data %>%
  arrange(desc(可使用櫃位數))

# 查看排序後的資料
print(head(data))

# 刪除「序號」和「縣市別代碼」欄位
data <- data %>%
  select(-序號, -縣市別代碼)

# 查看刪除後的資料
print(head(data))

# 重新命名欄位，刪除 "Slots"
data <- data %>%
  rename(
    `District in Taichung` = 納骨塔名稱,
    `Available` = 可使用櫃位數,
    `Used` = 已使用櫃位數,
    `Unused` = 未使用櫃位數,
    `Data Date` = 資料日期
  )

# 查看重新命名後的資料
print(head(data))

# 新增 "Used Rate" 欄位
data <- data %>%
  mutate(`Used Rate` = Used / Available)

# 查看新增欄位後的資料
print(head(data))

library(scales) # 用於百分比格式化

# 格式化 "Used Rate" 為百分比，並調整欄位順序
data <- data %>%
  mutate(`Used Rate` = Used / Available * 100) %>%
  select(`District in Taichung`, `Available`, `Used`, `Unused`, `Used Rate`, `Data Date`)

# 查看結果，確認 "Used Rate" 已為百分比格式
print(head(data))

# 新增 "saturation alert" 欄位，根據 Used Rate 分類
data <- data %>%
  mutate(
    `Saturation Alert` = case_when(
      `Used Rate` >= 90  ~ "Fully",
      `Used Rate` >= 80 & `Used Rate` < 90  ~ "Nearly",
      `Used Rate` >= 70 & `Used Rate` < 80  ~ "Moderately",
      `Used Rate` < 70                      ~ "Unsaturated"
    )
  )

# 查看更新後的資料
print(head(data))

# 刪除 "Used Rate Color" 和 "saturation alert" 欄位
data <- data %>%
  select(-`Used_Rate_Color`, -`saturation alert`)

# 查看刪除後的資料
print(head(data))

# 調整欄位順序，將 "Saturation Alert" 向左平移一欄
data <- data %>%
  select(`District in Taichung`, `Available`, `Used`, `Unused`,`Used Rate`, `Saturation Alert`, everything())

# 查看調整後的資料
print(head(data))

#保留「區」，僅刪除「區」後的文字
data <- data %>%
  mutate(`District in Taichung` = str_remove(`District in Taichung`, "區.*$") %>% paste0("區"))

# 查看結果
print(head(data))


