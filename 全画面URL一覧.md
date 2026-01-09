# まごころサポート - 全画面 URL 一覧（アプリ・API・Figma）

**作成日**: 2026-01-09
**対象**: 全43画面 + エラー画面

---

## 📋 クイックリンク

- [認証・アカウント管理](#認証アカウント管理)
- [ダッシュボード](#ダッシュボード)
- [顧客管理](#顧客管理)
- [案件管理](#案件管理)
- [作業報告](#作業報告)
- [パートナー管理](#パートナー管理)
- [コンシェルジュ管理](#コンシェルジュ管理)
- [マスタ管理](#マスタ管理)
- [エラー画面](#エラー画面)

---

## 認証・アカウント管理

### ログイン (Login)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/login` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=257-22106&t=h1plxwLq1DP5umKv-0 |
| **API** | `POST /api/auth/login` |
| **ユーザー** | 全員 |
| **デバイス** | PC / スマホ対応 |

### パスワード再設定 (Password Reset)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/password-reset` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=258-38012&t=h1plxwLq1DP5umKv-0 |
| **API** | `POST /api/auth/password-reset/request` (メール送信)<br>`POST /api/auth/password-reset/confirm` (パスワード更新) |
| **ユーザー** | 未ログイン |
| **デバイス** | PC / スマホ対応 |

### アカウント管理一覧 (Account Management List)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/accounts` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=394-93411&t=h1plxwLq1DP5umKv-0 |
| **API** | `GET /api/admin/accounts` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### アカウント発行 (Account Issuance Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/accounts` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=381-44244&t=h1plxwLq1DP5umKv-0 |
| **API** | `POST /api/admin/accounts` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

---

## ダッシュボード

### ダッシュボード - 管理者版 (Admin Dashboard)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/dashboard` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=414-40744&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/admin/dashboard` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### ダッシュボード - オペレーター版 (Operator Dashboard)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/operator/dashboard` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=414-40744&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/operator/dashboard` |
| **ユーザー** | オペレータ |
| **デバイス** | PC対応（Responsive） |

### ダッシュボード - パートナー版 (Partner Dashboard)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/dashboard` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=414-40744&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/partner/dashboard` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### ダッシュボード - コンシェルジュ版 (Concierge Dashboard)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/concierge/dashboard` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=424-58538&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/concierge/dashboard` |
| **ユーザー** | コンシェルジュ |
| **デバイス** | スマホ専用 |

---

## 顧客管理

### お客様一覧 - オペレーター版 (Customer List - Operator)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/operator/customers` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=550-36353&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/operator/customers` |
| **ユーザー** | オペレータ |
| **デバイス** | PC対応（Responsive） |

### お客様一覧 - パートナー版 (Customer List - Partner)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/customers` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=418-57925&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/partner/customers` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### お客様詳細 - オペレーター版 (Customer Detail - Operator)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/operator/customers/:id` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=414-40962&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/operator/customers/{id}` |
| **ユーザー** | オペレータ |
| **デバイス** | PC対応（Responsive） |

### お客様詳細 - パートナー版 (Customer Detail - Partner)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/customers/:id` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=645-73447&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/partner/customers/{id}` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### お客様作成 (Customer Creation Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/operator/customers` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=414-41122&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `POST /api/operator/customers` |
| **ユーザー** | オペレータ、パートナー、コンシェルジュ |
| **デバイス** | PC対応（Responsive） |

### お客様作成・編集 - パートナー版 (Customer Create/Edit - Partner Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/customers` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=418-58039&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `POST /api/partner/customers`<br>`PUT /api/partner/customers/{id}` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

---

## 案件管理

### 案件一覧 - オペレーター版 (Case List - Operator)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/operator/cases` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=645-75349&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/operator/cases` |
| **ユーザー** | オペレータ |
| **デバイス** | PC対応（Responsive） |

### 案件一覧 - パートナー版 (Case List - Partner)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/cases` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=418-53246&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/partner/cases` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### 案件一覧 - コンシェルジュ版 (Case List - Concierge)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/concierge/cases` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=486-43921&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/concierge/cases` |
| **ユーザー** | コンシェルジュ |
| **デバイス** | スマホ専用 |

### 案件詳細 - オペレーター版 (Case Detail - Operator)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/operator/cases/:id` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=645-20527&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/operator/cases/{id}`<br>`PUT /api/operator/cases/{id}`<br>`DELETE /api/operator/cases/{id}` |
| **ユーザー** | オペレータ |
| **デバイス** | PC対応（Responsive） |

### 案件詳細 - パートナー版 (Case Detail - Partner)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/cases/:id` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=645-20527&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/partner/cases/{id}`<br>`PUT /api/partner/cases/{id}`<br>`DELETE /api/partner/cases/{id}` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### 案件詳細 - コンシェルジュ版 (Case Detail - Concierge)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/concierge/cases/:id` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=486-106184&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/concierge/cases/{id}` |
| **ユーザー** | コンシェルジュ |
| **デバイス** | スマホ専用 |

### 案件作成・編集 - オペレーター版 (Case Create/Edit - Operator Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/operator/cases` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=414-40674&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `POST /api/operator/cases` (新規作成)<br>`POST /api/operator/cases/{id}/draft` (下書き保存)<br>`PUT /api/operator/cases/{id}` (更新) |
| **ユーザー** | オペレータ |
| **デバイス** | PC対応（Responsive） |

### 案件作成・編集 - パートナー版 (Case Create/Edit - Partner Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/cases` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=418-53246&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `POST /api/partner/cases` (新規作成)<br>`POST /api/partner/cases/{id}/draft` (下書き保存)<br>`PUT /api/partner/cases/{id}` (更新) |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### 案件作成・編集 - コンシェルジュ版 (Case Create/Edit - Concierge Screen)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/concierge/cases/new`, `/concierge/cases/:id/edit` (スクリーン遷移) |
| **Figma Design** | - |
| **API** | `POST /api/concierge/cases` (新規作成)<br>`POST /api/concierge/cases/{id}/draft` (下書き保存)<br>`PUT /api/concierge/cases/{id}` (更新) |
| **ユーザー** | コンシェルジュ |
| **デバイス** | スマホ専用 |

---

## 作業報告

### 作業報告 (Work Report - Concierge Mobile)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/concierge/cases/:id/report` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=446-93166&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `POST /api/concierge/cases/{id}/report` (報告完了)<br>`POST /api/concierge/cases/{id}/report/draft` (下書き保存) |
| **ユーザー** | コンシェルジュ |
| **デバイス** | スマホ専用 |

### 完了報告一覧 (Completion Report List - Concierge Mobile)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/concierge/reports` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=490-106770&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `GET /api/concierge/cases?status=unreported` |
| **ユーザー** | コンシェルジュ |
| **デバイス** | スマホ専用 |

---

## パートナー管理

### パートナー加盟店一覧 (Partner Store List)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/partners` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=394-86288&t=h1plxwLq1DP5umKv-0 |
| **API** | `GET /api/admin/partners` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### パートナー加盟店詳細 (Partner Store Detail)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/partners/:id` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=394-85853&t=h1plxwLq1DP5umKv-0 |
| **API** | `GET /api/admin/partners/{id}` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### パートナー加盟店登録・編集 (Partner Store Registration/Edit Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/partners` (モーダルで表示) |
| **Figma Design** | - |
| **API** | `POST /api/admin/partners` (新規登録)<br>`PUT /api/admin/partners/{id}` (編集) |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

---

## コンシェルジュ管理

### コンシェルジュ一覧 (Concierge List - Partner)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/concierges` |
| **Figma Design** | - |
| **API** | `GET /api/partner/concierges` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### コンシェルジュ詳細 (Concierge Detail - Partner)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/concierges/:id` |
| **Figma Design** | - |
| **API** | `GET /api/partner/concierges/{id}` |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### コンシェルジュ登録・編集 (Concierge Registration/Edit Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/concierges` (モーダルで表示) |
| **Figma Design** | - |
| **API** | `POST /api/partner/concierges` (新規登録)<br>`PUT /api/partner/concierges/{id}` (編集) |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

### 店舗情報詳細・編集 (Store Information Detail/Edit - Partner)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/partner/store` |
| **Figma Design** | - |
| **API** | `GET /api/partner/store` (取得)<br>`PUT /api/partner/store` (更新) |
| **ユーザー** | パートナー加盟店 |
| **デバイス** | PC対応（Responsive） |

---

## マスタ管理

### サービス一覧 (Service List)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/services` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=386-41647&t=h1plxwLq1DP5umKv-0 |
| **API** | `GET /api/admin/services` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### サービス詳細 (Service Detail)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/services/:id` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=387-42476&t=h1plxwLq1DP5umKv-0 |
| **API** | `GET /api/admin/services/{id}`<br>`PATCH /api/admin/services/{id}` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### サービス登録・編集 (Service Registration/Edit Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/services` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=390-36069&t=h1plxwLq1DP5umKv-0 |
| **API** | `POST /api/admin/services` (新規登録)<br>`PUT /api/admin/services/{id}` (編集) |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### サポート種別一覧 (Support Type List)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/master/support-types` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=567-36874&t=h1plxwLq1DP5umKv-0 |
| **API** | `GET /api/admin/master/support-types` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### サポート種別登録・編集 (Support Type Registration/Edit Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/master/support-types` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=570-39752&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `POST /api/admin/master/support-types` (新規登録)<br>`PUT /api/admin/master/support-types/{id}` (編集) |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### サービス種別一覧 (Service Category List)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/master/service-types` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=567-36874&t=h1plxwLq1DP5umKv-0 |
| **API** | `GET /api/admin/master/service-types` |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

### サービス種別登録・編集 (Service Category Registration/Edit Modal)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/admin/master/service-types` (モーダルで表示) |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=570-39752&t=q71JbxSPjtZZ7HBO-0 |
| **API** | `POST /api/admin/master/service-types` (新規登録)<br>`PUT /api/admin/master/service-types/{id}` (編集) |
| **ユーザー** | 管理者 |
| **デバイス** | PC対応（Responsive） |

---

## エラー画面

### エラー画面 (Error Screen)
| 項目 | 内容 |
|------|------|
| **アプリ URL** | `/error` |
| **Figma Design** | https://www.figma.com/design/mjSOs02H4hqf9kIsiFlm4e/%E3%83%87%E3%82%B6%E3%82%A4%E3%83%B3?node-id=265-133930&t=h1plxwLq1DP5umKv-0 |
| **API** | N/A |
| **ユーザー** | 全員 |
| **デバイス** | PC / スマホ対応 |

---

## 📊 統計情報

| 項目 | 数値 |
|------|------|
| **総画面数** | 43+ |
| **アプリ URL 定義済み** | 43 |
| **Figma URL 指定済み** | 35 |
| **API エンドポイント定義済み** | 50+ |
| **ユーザー種別** | 4 (管理者、オペレータ、パートナー、コンシェルジュ) |
| **デバイス対応** | 2 (PC Responsive / スマホ専用) |
| **モーダル画面** | 8 |
| **一覧画面** | 12 |
| **詳細画面** | 8 |
| **ダッシュボード** | 4 |

---

## 🔗 URL パターンガイド

### アプリ URL パターン

```
認証系
  /login
  /password-reset

管理者機能
  /admin/dashboard
  /admin/accounts
  /admin/partners
  /admin/partners/:id
  /admin/services
  /admin/services/:id
  /admin/master/support-types
  /admin/master/service-types

オペレータ機能
  /operator/dashboard
  /operator/customers
  /operator/customers/:id
  /operator/cases
  /operator/cases/:id

パートナー機能
  /partner/dashboard
  /partner/customers
  /partner/customers/:id
  /partner/cases
  /partner/cases/:id
  /partner/concierges
  /partner/concierges/:id
  /partner/store

コンシェルジュ機能
  /concierge/dashboard
  /concierge/cases
  /concierge/cases/:id
  /concierge/cases/:id/report
  /concierge/reports

その他
  /error
```

**注**: モーダル画面（新規作成・編集）は上記の一覧画面の URL で表示されます

---

## 🔧 開発時の使用方法

### フロントエンド開発者

```javascript
// React Router の設定例
const routes = [
  { path: '/login', component: LoginScreen },
  { path: '/admin/dashboard', component: AdminDashboard },
  { path: '/operator/customers', component: OperatorCustomerList },
  { path: '/operator/customers/:id', component: OperatorCustomerDetail },
  // ...
];
```

### バックエンド開発者

```yaml
# API エンドポイント実装リスト
POST /api/auth/login
POST /api/auth/password-reset/request
POST /api/auth/password-reset/confirm
GET /api/admin/dashboard
GET /api/admin/accounts
POST /api/admin/accounts
GET /api/operator/customers
GET /api/operator/customers/{id}
# ...
```

### QA テスト

1. アプリ URL でブラウザからアクセス
2. API エンドポイントで動作確認
3. Figma デザインと比較検証

---

**最終更新**: 2026-01-09
**管理者**: Claude Code
**バージョン**: 2.0 (アプリ URL追加版)
