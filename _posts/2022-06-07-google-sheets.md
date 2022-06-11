---
layout: post
title: Google Spread Sheets
---

Google Spread Sheetsをデータ置き場にすると何かと便利です。

#### 1. 必要なライブラリ

```python
pip install gspread oauth2client

```

#### 2. Google Could Platformでの作業

- 新規プロジェクトを作成する
- Google Drive APIを有効にする
- Google Spread Sheets APIを有効にする
- 認証情報を設定する
- 秘密鍵を生成し、"token.json"を保存する

#### 3. Google Spread Sheetsでの作業

- 新規スプレッドシートを作成する
- "token.json"の"client_email"に書かれているアドレスをコピーする
- スプレッドシートの共有を開き、コピーしたアドレスを"ユーザーやグループに追加"に記入する。
- スプレッドシートのグローバルアドレスからKEYを取得する

#### 4. Google Spread Sheetsへのアクセス

```python
import gspread
from google.oauth2.service_account import Credentials

SPREADSHEET_KEY = "x_x_5HTf7hMZjmgrgIjVMf9O13ixxxxxxxxxxxx"
JSON_FILE = "./token.json"

def connect_gspred():
    scope = ['https://www.googleapis.com/auth/spreadsheets','https://www.googleapis.com/auth/drive']
    credentials = Credentials.from_service_account_file(JSON_FILE, scopes=scope)
    gc = gspread.authorize(credentials)
    workbook = gc.open_by_key(SPREADSHEET_KEY)
    worksheets = workbook.worksheets()
    return worksheets


if __name__ == "__main__":

    worksheets = connect_gspred()
    ws = worksheets[0]

```

#### 5. 使い方

- [Repository](https://github.com/burnash/gspread)
- [Docs >> gspread](https://docs.gspread.org/en/latest/index.html)

```python
# Getting a Cell Value
value = worksheet.cell(1, 1).value
# Updating a Cell
worksheet.update_cell(1, 2, 'Bingo!')
# Append Rows
a = 1, 2, 3
worksheet.append_row(a)
# Clear the entire workshseet
worksheet.clear()

# Using gspread with pandas
import pandas as pd

dataframe = pd.DataFrame(worksheet.get_all_records())
worksheet.update([dataframe.columns.values.tolist()] + dataframe.values.tolist())

```

#### 6. Google Spread Sheets APIの制限

- 500 requests per 100 seconds per project
- 100 requests per 100 seconds per user 100リクエスト/100秒/1ユーザ

Spread Sheetsへの書き込みでループを回す場合、120秒のスリープを入れながら

```python
from time import sleep

for i, values in enumerate(data):
    if i and i%50 == 0:
      sleep(120)
    worksheet.append_row(values)

```
