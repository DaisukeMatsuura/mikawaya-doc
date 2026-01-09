# まごころサポート - API エンドポイント完全定義書

**作成日**: 2026-01-09
**最終更新**: 2026-01-09
**ステータス**: 確定

---

## 📋 目次

- [認証・アカウント管理](#認証アカウント管理)
- [ダッシュボード](#ダッシュボード)
- [顧客管理](#顧客管理)
- [案件管理](#案件管理)
- [作業報告](#作業報告)
- [パートナー管理](#パートナー管理)
- [コンシェルジュ管理](#コンシェルジュ管理)
- [マスタ管理](#マスタ管理)
- [統計情報](#統計情報)

---

## 認証・アカウント管理

### 1. ログイン

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/auth/login` |
| **説明** | ユーザー認証、ログイン処理 |
| **リクエスト** | `{ email: string, password: string }` |
| **レスポンス** | `{ token: string, user: User }` |
| **ステータスコード** | 200: 成功 / 401: 認証失敗 |
| **認可** | 全員（未ログイン） |
| **備考** | ユーザー種別に応じたホーム画面へリダイレクト |

### 2. パスワード再設定リクエスト

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/auth/password-reset/request` |
| **説明** | パスワード再設定メール送信 |
| **リクエスト** | `{ email: string }` |
| **レスポンス** | `{ message: string, sent: boolean }` |
| **ステータスコード** | 200: 成功 / 400: メール未登録 |
| **認可** | 全員（未ログイン） |
| **備考** | メール送信処理非同期、24時間以内に確認必須 |

### 3. パスワード再設定確認

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/auth/password-reset/confirm` |
| **説明** | パスワード再設定トークン検証・新パスワード登録 |
| **リクエスト** | `{ token: string, newPassword: string }` |
| **レスポンス** | `{ message: string, success: boolean }` |
| **ステータスコード** | 200: 成功 / 400: トークン無効 |
| **認可** | 全員（未ログイン） |
| **備考** | トークン有効期限：24時間 |

### 4. アカウント管理一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/accounts` |
| **説明** | システム全体のアカウント一覧取得 |
| **リクエスト** | `?page=1&limit=20&search=keyword` |
| **レスポンス** | `{ total: number, items: Account[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | 管理者のみ |
| **備考** | ページネーション対応、検索・フィルター機能あり |

### 5. アカウント発行

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/admin/accounts` |
| **説明** | 新規アカウント（ユーザー）を発行 |
| **リクエスト** | `{ email: string, userType: "admin"\|"operator"\|"partner"\|"concierge", partnerStoreId?: number }` |
| **レスポンス** | `{ id: number, email: string, userType: string, createdAt: datetime }` |
| **ステータスコード** | 201: 作成成功 / 400: 無効なリクエスト / 409: メール重複 |
| **認可** | 管理者のみ |
| **備考** | 発行時に自動メール送信、初期パスワードは1回限定 |

---

## ダッシュボード

### 6. 管理者ダッシュボード

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/dashboard` |
| **説明** | システム全体の統計・ステータス情報取得 |
| **リクエスト** | `?period=month&year=2026&month=01` |
| **レスポンス** | `{ totalPartners: number, totalCases: number, ongoingCases: number, completedCases: number, charts: Dashboard }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | 管理者のみ |
| **備考** | 期間指定で推移データ取得可能、日次更新 |

### 7. オペレーターダッシュボード

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/operator/dashboard` |
| **説明** | オペレーター担当の案件ステータス・実績データ取得 |
| **リクエスト** | `?period=month` |
| **レスポンス** | `{ assignedCases: number, activeCases: number, completedThisMonth: number, statistics: Dashboard }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | オペレータのみ |
| **備考** | パーソナライズされたデータ、日次更新 |

### 8. パートナーダッシュボード

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/dashboard` |
| **説明** | パートナー加盟店の案件進捗・実績データ取得 |
| **リクエスト** | `?period=month` |
| **レスポンス** | `{ totalCases: number, activeCases: number, completedThisMonth: number, monthlyRevenue: number, statistics: Dashboard }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | パートナー加盟店のみ（自店舗データ） |
| **備考** | パーソナライズされたデータ、日次更新 |

### 9. コンシェルジュダッシュボード

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/concierge/dashboard` |
| **説明** | コンシェルジュの訪問予定・実績データ取得 |
| **リクエスト** | `?date=YYYY-MM-DD` |
| **レスポンス** | `{ todaySchedules: Case[], completedToday: number, pendingReports: number, statistics: Dashboard }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | コンシェルジュのみ |
| **備考** | 日別データ、当日スケジュール取得 |

---

## 顧客管理

### 10. お客様一覧取得（オペレーター）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/operator/customers` |
| **説明** | オペレーター側でのお客様情報一覧取得 |
| **リクエスト** | `?page=1&limit=20&search=keyword&sort=name` |
| **レスポンス** | `{ total: number, items: Customer[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | オペレータ、パートナー加盟店、コンシェルジュ |
| **備考** | ページネーション対応 |

### 11. お客様一覧取得（パートナー）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/customers` |
| **説明** | パートナー加盟店の顧客一覧取得（自店舗のみ） |
| **リクエスト** | `?page=1&limit=20&search=keyword&status=active` |
| **レスポンス** | `{ total: number, items: Customer[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | パートナー加盟店のみ（自店舗データ） |
| **備考** | ページネーション対応、ステータスフィルター機能 |

### 12. お客様詳細取得（オペレーター）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/operator/customers/{id}` |
| **説明** | 特定のお客様詳細情報取得（オペレーター） |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, name: string, phone: string, email: string, address: string, caseHistory: Case[] }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | オペレータ、パートナー加盟店、コンシェルジュ |
| **備考** | 案件履歴を含む |

### 13. お客様詳細取得（パートナー）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/customers/{id}` |
| **説明** | 特定のお客様詳細情報取得（パートナー） |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, name: string, phone: string, email: string, address: string, caseHistory: Case[] }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | パートナー加盟店のみ（自店舗顧客） |
| **備考** | パートナー自店舗の顧客のみ取得可能 |

### 14. お客様作成（オペレーター）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/operator/customers` |
| **説明** | 新規お客様登録（オペレーター） |
| **リクエスト** | `{ name: string, phone: string, email: string, address: string, prefecture: string }` |
| **レスポンス** | `{ id: number, name: string, createdAt: datetime }` |
| **ステータスコード** | 201: 作成成功 / 400: 無効なリクエスト / 409: 重複 |
| **認可** | オペレータ、パートナー加盟店、コンシェルジュ |
| **備考** | メールアドレス・電話番号の重複チェック実施 |

### 15. お客様作成・編集（パートナー）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/partner/customers` (作成)<br>`PUT /api/partner/customers/{id}` (編集) |
| **説明** | パートナー加盟店での顧客登録・更新 |
| **リクエスト** | `{ name: string, phone: string, email: string, address: string }` |
| **レスポンス** | `{ id: number, name: string, updatedAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 / 409: 重複 |
| **認可** | パートナー加盟店のみ |
| **備考** | 自店舗顧客のみ操作可能 |

---

## 案件管理

### 16. 案件一覧取得（オペレーター）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/operator/cases` |
| **説明** | オペレーター担当の案件一覧取得 |
| **リクエスト** | `?page=1&limit=20&status=active&sort=date` |
| **レスポンス** | `{ total: number, items: Case[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | オペレータのみ |
| **備考** | ステータスフィルター、ソート機能対応 |

### 17. 案件一覧取得（パートナー）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/cases` |
| **説明** | パートナー加盟店の案件一覧取得 |
| **リクエスト** | `?page=1&limit=20&status=active` |
| **レスポンス** | `{ total: number, items: Case[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | パートナー加盟店のみ（自店舗） |
| **備考** | 自店舗案件のみ表示 |

### 18. 案件一覧取得（コンシェルジュ）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/concierge/cases` |
| **説明** | コンシェルジュの担当案件一覧取得 |
| **リクエスト** | `?page=1&limit=20&status=assigned` |
| **レスポンス** | `{ total: number, items: Case[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | コンシェルジュのみ |
| **備考** | 担当案件のみ表示 |

### 19. 案件詳細取得（オペレーター）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/operator/cases/{id}` |
| **説明** | 特定の案件詳細情報取得（オペレーター） |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, customer: Customer, concierge: Concierge, status: string, details: CaseDetail }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | オペレータのみ |
| **備考** | 顧客情報・担当コンシェルジュ情報含む |

### 20. 案件詳細取得（パートナー）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/cases/{id}` |
| **説明** | 特定の案件詳細情報取得（パートナー） |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, customer: Customer, concierge: Concierge, status: string, details: CaseDetail }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | パートナー加盟店のみ（自店舗案件） |
| **備考** | 自店舗案件のみアクセス可能 |

### 21. 案件詳細取得（コンシェルジュ）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/concierge/cases/{id}` |
| **説明** | 特定の案件詳細情報取得（コンシェルジュ） |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, customer: Customer, schedule: datetime, details: CaseDetail }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | コンシェルジュのみ（担当案件） |
| **備考** | 担当案件のみアクセス可能 |

### 22. 案件作成・編集（オペレーター）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/operator/cases` (新規)<br>`POST /api/operator/cases/{id}/draft` (下書き)<br>`PUT /api/operator/cases/{id}` (更新) |
| **説明** | 案件の新規作成・下書き保存・更新 |
| **リクエスト** | `{ customerId: number, serviceType: string, serviceDetails: string, requestedDate: date, assignedConcierges: number[] }` |
| **レスポンス** | `{ id: number, status: string, createdAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 |
| **認可** | オペレータのみ |
| **備考** | 下書き保存で一時保存、更新で最終確定 |

### 23. 案件作成・編集（パートナー）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/partner/cases` (新規)<br>`POST /api/partner/cases/{id}/draft` (下書き)<br>`PUT /api/partner/cases/{id}` (更新) |
| **説明** | パートナー加盟店での案件登録・更新 |
| **リクエスト** | `{ customerId: number, serviceType: string, details: string, requestedDate: date }` |
| **レスポンス** | `{ id: number, status: string, createdAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 |
| **認可** | パートナー加盟店のみ |
| **備考** | 自店舗顧客・リソースのみ利用可能 |

### 24. 案件作成（コンシェルジュ）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/concierge/cases` (新規)<br>`POST /api/concierge/cases/{id}/draft` (下書き)<br>`PUT /api/concierge/cases/{id}` (更新) |
| **説明** | コンシェルジュの案件登録・更新 |
| **リクエスト** | `{ customerId: number, visitDate: date, details: string }` |
| **レスポンス** | `{ id: number, status: string, createdAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 |
| **認可** | コンシェルジュのみ |
| **備考** | 訪問予定日の案件新規作成 |

### 25. 案件削除（オペレーター）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `DELETE /api/operator/cases/{id}` |
| **説明** | 案件削除（オペレーター） |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ success: boolean, message: string }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | オペレータのみ |
| **備考** | 下書き状態の案件のみ削除可能 |

### 26. 案件削除（パートナー）

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `DELETE /api/partner/cases/{id}` |
| **説明** | 案件削除（パートナー） |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ success: boolean, message: string }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | パートナー加盟店のみ |
| **備考** | 下書き状態の案件のみ削除可能 |

---

## 作業報告

### 27. 未報告案件一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/concierge/cases?status=unreported` |
| **説明** | 完了した但し報告されていない案件一覧 |
| **リクエスト** | `?status=unreported&page=1&limit=20` |
| **レスポンス** | `{ total: number, items: Case[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | コンシェルジュのみ |
| **備考** | クエリパラメータ：status=unreported |

### 28. 作業報告提出

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/concierge/cases/{id}/report` |
| **説明** | 訪問完了報告書提出 |
| **リクエスト** | `{ caseId: number, completionDate: date, notes: string, photos: File[] }` |
| **レスポンス** | `{ reportId: number, status: "completed", submittedAt: datetime }` |
| **ステータスコード** | 201: 成功 / 400: 無効 / 409: 既に報告済み |
| **認可** | コンシェルジュのみ |
| **備考** | 完了報告書最終版 |

### 29. 作業報告下書き保存

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/concierge/cases/{id}/report/draft` |
| **説明** | 訪問完了報告書の下書き保存 |
| **リクエスト** | `{ caseId: number, completionDate: date, notes: string, photos: File[] }` |
| **レスポンス** | `{ draftId: number, status: "draft", savedAt: datetime }` |
| **ステータスコード** | 201: 成功 / 400: 無効 |
| **認可** | コンシェルジュのみ |
| **備考** | 下書きは複数回保存可能 |

### 30. 完了報告一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/concierge/reports` |
| **説明** | 提出済み報告書一覧取得 |
| **リクエスト** | `?page=1&limit=20&startDate=YYYY-MM-DD&endDate=YYYY-MM-DD` |
| **レスポンス** | `{ total: number, items: Report[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | コンシェルジュのみ |
| **備考** | 日付範囲フィルター対応 |

---

## パートナー管理

### 31. パートナー加盟店一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/partners` |
| **説明** | 全パートナー加盟店一覧取得 |
| **リクエスト** | `?page=1&limit=20&status=active&search=keyword` |
| **レスポンス** | `{ total: number, items: Partner[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | 管理者のみ |
| **備考** | ステータスフィルター、検索機能対応 |

### 32. パートナー加盟店詳細取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/partners/{id}` |
| **説明** | 特定パートナー加盟店の詳細情報取得 |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, name: string, contact: Contact, concierges: Concierge[] }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | 管理者のみ |
| **備考** | コンシェルジュ一覧を含む |

### 33. パートナー加盟店登録・編集

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/admin/partners` (登録)<br>`PUT /api/admin/partners/{id}` (編集) |
| **説明** | パートナー加盟店の新規登録・情報更新 |
| **リクエスト** | `{ name: string, contact: Contact, address: string, accountingInfo: AccountingInfo }` |
| **レスポンス** | `{ id: number, name: string, createdAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 / 409: 重複 |
| **認可** | 管理者のみ |
| **備考** | 帳簿情報・契約情報を含む |

### 34. パートナー店舗情報取得・更新

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/store` (取得)<br>`PUT /api/partner/store` (更新) |
| **説明** | パートナー加盟店が自店舗情報を取得・編集 |
| **リクエスト** | `{ storeName: string, address: string, phone: string, email: string }` |
| **レスポンス** | `{ id: number, storeInfo: StoreInfo, updatedAt: datetime }` |
| **ステータスコード** | 200: 成功 / 400: 無効 |
| **認可** | パートナー加盟店のみ |
| **備考** | 自店舗情報のみ操作可能 |

---

## コンシェルジュ管理

### 35. コンシェルジュ一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/concierges` |
| **説明** | パートナー加盟店のコンシェルジュ一覧取得 |
| **リクエスト** | `?page=1&limit=20&status=active&search=name` |
| **レスポンス** | `{ total: number, items: Concierge[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | パートナー加盟店のみ（自店舗） |
| **備考** | 自店舗コンシェルジュのみ表示 |

### 36. コンシェルジュ詳細取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/partner/concierges/{id}` |
| **説明** | 特定コンシェルジュの詳細情報取得 |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, name: string, phone: string, email: string, employmentInfo: EmploymentInfo, statistics: Statistics }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | パートナー加盟店のみ（自店舗） |
| **備考** | 実績・評価情報を含む |

### 37. コンシェルジュ登録・編集

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/partner/concierges` (登録)<br>`PUT /api/partner/concierges/{id}` (編集) |
| **説明** | コンシェルジュの登録・情報更新 |
| **リクエスト** | `{ name: string, furigana: string, phone: string, email: string, employmentType: string, hireDate: date, status: "active"\|"inactive" }` |
| **レスポンス** | `{ id: number, name: string, createdAt/updatedAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 / 409: 重複 |
| **認可** | パートナー加盟店のみ |
| **備考** | メールアドレス・電話番号の重複チェック |

---

## マスタ管理

### 38. サービス一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/services` |
| **説明** | 利用可能なサービス一覧取得 |
| **リクエスト** | `?page=1&limit=20&status=active` |
| **レスポンス** | `{ total: number, items: Service[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | 管理者のみ |
| **備考** | ステータスフィルター対応 |

### 39. サービス詳細取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/services/{id}` |
| **説明** | 特定サービスの詳細情報取得 |
| **リクエスト** | パスパラメータ：`id` |
| **レスポンス** | `{ id: number, name: string, description: string, price: number, details: ServiceDetail }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし / 404: 不在 |
| **認可** | 管理者のみ |
| **備考** | 詳細説明・価格情報を含む |

### 40. サービス登録・編集

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/admin/services` (登録)<br>`PUT /api/admin/services/{id}` (編集) |
| **説明** | サービスの新規登録・情報更新 |
| **リクエスト** | `{ name: string, description: string, price: number, category: string }` |
| **レスポンス** | `{ id: number, name: string, createdAt/updatedAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 |
| **認可** | 管理者のみ |
| **備考** | 価格・カテゴリー情報を含む |

### 41. サービスステータス更新

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `PATCH /api/admin/services/{id}` |
| **説明** | サービスの有効/無効切り替え |
| **リクエスト** | `{ status: "active"\|"inactive" }` |
| **レスポンス** | `{ id: number, status: string, updatedAt: datetime }` |
| **ステータスコード** | 200: 成功 / 400: 無効 / 404: 不在 |
| **認可** | 管理者のみ |
| **備考** | 部分更新（PATCH）でステータスのみ変更 |

### 42. サポート種別一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/master/support-types` |
| **説明** | サポート種別マスタ一覧取得 |
| **リクエスト** | `?page=1&limit=50` |
| **レスポンス** | `{ total: number, items: SupportType[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | 管理者のみ |
| **備考** | マスタデータ |

### 43. サポート種別登録・編集

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/admin/master/support-types` (登録)<br>`PUT /api/admin/master/support-types/{id}` (編集) |
| **説明** | サポート種別の新規登録・更新 |
| **リクエスト** | `{ name: string, code: string, description: string }` |
| **レスポンス** | `{ id: number, name: string, createdAt/updatedAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 / 409: コード重複 |
| **認可** | 管理者のみ |
| **備考** | コードの重複チェック |

### 44. サービス種別一覧取得

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `GET /api/admin/master/service-types` |
| **説明** | サービス種別マスタ一覧取得 |
| **リクエスト** | `?page=1&limit=50` |
| **レスポンス** | `{ total: number, items: ServiceType[], page: number }` |
| **ステータスコード** | 200: 成功 / 403: 権限なし |
| **認可** | 管理者のみ |
| **備考** | マスタデータ |

### 45. サービス種別登録・編集

| 項目 | 内容 |
|------|------|
| **エンドポイント** | `POST /api/admin/master/service-types` (登録)<br>`PUT /api/admin/master/service-types/{id}` (編集) |
| **説明** | サービス種別の新規登録・更新 |
| **リクエスト** | `{ name: string, code: string, description: string }` |
| **レスポンス** | `{ id: number, name: string, createdAt/updatedAt: datetime }` |
| **ステータスコード** | 201/200: 成功 / 400: 無効 / 409: コード重複 |
| **認可** | 管理者のみ |
| **備考** | コードの重複チェック |

---

## 統計情報

| 項目 | 数値 |
|------|------|
| **総エンドポイント数** | 45 |
| **GET リクエスト** | 26 |
| **POST リクエスト** | 14 |
| **PUT リクエスト** | 9 |
| **DELETE リクエスト** | 2 |
| **PATCH リクエスト** | 1 |

---

## 🔒 認可マトリックス

| API パターン | 管理者 | オペレータ | パートナー | コンシェルジュ |
|-------------|------|----------|----------|------------|
| `/api/admin/*` | ◯ | ✕ | ✕ | ✕ |
| `/api/operator/*` | ✕ | ◯ | △ | △ |
| `/api/partner/*` | ✕ | ✕ | ◯ | △ |
| `/api/concierge/*` | ✕ | ✕ | ✕ | ◯ |
| `/api/auth/*` | ◯ | ◯ | ◯ | ◯ |

**凡例**: ◯ = フルアクセス / △ = 限定アクセス（自身のリソースのみ） / ✕ = アクセス不可

---

## 📝 共通ルール

### レスポンス形式

すべての API レスポンスは以下の形式に統一：

```json
{
  "success": boolean,
  "data": object | array,
  "message": string,
  "timestamp": datetime
}
```

### エラーレスポンス

```json
{
  "success": false,
  "error": {
    "code": string,
    "message": string,
    "details": object
  },
  "timestamp": datetime
}
```

### ページネーション

リスト系 API は以下形式：

```json
{
  "total": number,
  "page": number,
  "limit": number,
  "items": array
}
```

### 認証

すべてのリクエストに以下ヘッダを含める：

```
Authorization: Bearer {token}
Content-Type: application/json
```

---

**最終確認**: 2026-01-09
**バージョン**: 1.0
**ステータス**: 開発チーム内確認済み
