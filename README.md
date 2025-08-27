# Fast React Pizza Co. 🍕

Fast React Pizza Co.は、認証不要でピザを注文できるReduxプロジェクトです。シンプルで使いやすいプラットフォームとして設計されており、ユーザーが迅速かつ簡単にピザを注文できるアプリケーションです。

## 🚀 プロジェクトの特徴

### 主要機能
- **認証不要**: アカウント作成やログイン不要。ユーザーは名前を入力するだけでアプリを使用開始
- **動的メニュー**: ピザメニューは変更される可能性があるため、APIから読み込み
- **ショッピングカート**: 注文前に複数のピザをカートに追加可能
- **優先注文オプション**: カート価格の20%追加で「優先」注文をマーク可能
- **位置情報サービス**: 配達を簡単にするためのGPS位置情報提供
- **注文追跡**: 各注文に一意のIDが付与され、後で注文を検索可能

### ユーザー体験の特徴
- 複数ページ、動的メニュー、効率的なカートシステム、スムーズな注文プロセス
- 動的バスケットシステムで、ユーザーはお気に入りのピザを追加し、数量を調整し、自動価格計算を楽しめる
- 位置情報と配達追跡機能

## 🛠 技術スタック

### フロントエンド技術
このプロジェクトは以下の技術を使用して構築されています：

| 技術 | 目的 |
|------|------|
| **React** | UIフレームワークとコンポーネントシステム |
| **Redux** | 状態管理とデータフロー |
| **React Router** | クライアントサイドルーティングとナビゲーション |
| **Tailwind CSS** | ユーティリティファーストCSSフレームワーク |

### アプリケーションアーキテクチャ

#### システムアーキテクチャ図

```mermaid
graph TB
    subgraph "Frontend - React SPA"
        A[React Components]
        B[Redux Store]
        C[React Router]
    end
    
    subgraph "State Management"
        B --> D[User Slice]
        B --> E[Cart Slice]
        B --> F[Menu Slice]
        B --> G[Order Slice]
    end
    
    subgraph "External Services"
        H[Pizza Menu API]
        I[Order API]
        J[Geolocation Service]
    end
    
    A --> B
    A --> C
    A --> H
    A --> I
    A --> J
    
    style A fill:#61DAFB
    style B fill:#764ABC
    style C fill:#CA4245
```

## 🏗 コンポーネント構造図

```mermaid
graph TD
    A[App.jsx] --> B[Home]
    A --> C[Menu]
    A --> D[Cart]
    A --> E[CreateOrder]
    A --> F[Order]
    
    subgraph "UI Components"
        G[Header]
        H[Loader]
        I[Button]
        J[LinkButton]
        K[AppLayout]
    end
    
    subgraph "Menu Feature"
        C --> L[MenuItem]
        C --> M[MenuLoader]
    end
    
    subgraph "Cart Feature"
        D --> N[CartItem]
        D --> O[EmptyCart]
    end
    
    subgraph "Order Feature"
        E --> P[CreateOrderForm]
        F --> Q[OrderItem]
        F --> R[UpdateOrder]
    end
    
    A --> G
    A --> H
    B --> I
    C --> I
    D --> I
    E --> I
    F --> I
    
    style A fill:#FF6B6B
    style C fill:#4ECDC4
    style D fill:#45B7D1
    style E fill:#96CEB4
    style F fill:#FFEAA7
```

## 📊 データフロー図

```mermaid
flowchart LR
    subgraph "User Actions"
        A[User Input] --> B{Action Type}
    end
    
    subgraph "Redux Actions"
        B --> C[Menu Actions]
        B --> D[Cart Actions]
        B --> E[Order Actions]
        B --> F[User Actions]
    end
    
    subgraph "API Calls"
        C --> G[Fetch Menu API]
        E --> H[Post Order API]
        E --> I[Get Order API]
    end
    
    subgraph "Redux Store"
        D --> J[Cart State]
        C --> K[Menu State]
        E --> L[Order State]
        F --> M[User State]
    end
    
    subgraph "UI Updates"
        J --> N[Cart Components]
        K --> O[Menu Components]
        L --> P[Order Components]
        M --> Q[User Components]
    end
    
    G --> K
    H --> L
    I --> L
    
    style J fill:#FFD93D
    style K fill:#6BCF7F
    style L fill:#4D96FF
    style M fill:#FF6B9D
```

## 📱 アプリケーションフロー

### ユーザージャーニー フローチャート

```mermaid
flowchart TD
    A[アプリ起動] --> B[ホームページ]
    B --> C{ユーザー名入力済み?}
    C -->|No| D[名前を入力]
    C -->|Yes| E[メニューページへ]
    D --> E
    
    E --> F[ピザメニュー表示]
    F --> G[ピザを選択]
    G --> H{カートに追加?}
    H -->|Yes| I[カートに追加]
    H -->|No| G
    
    I --> J{もっと注文?}
    J -->|Yes| G
    J -->|No| K[カートページ]
    
    K --> L{注文内容確認}
    L -->|修正| M[数量変更/削除]
    M --> L
    L -->|OK| N[注文フォーム]
    
    N --> O[配達情報入力]
    O --> P{優先注文?}
    P -->|Yes| Q[+20%料金]
    P -->|No| R[通常注文]
    Q --> S[注文送信]
    R --> S
    
    S --> T[注文ID発行]
    T --> U[注文追跡ページ]
    U --> V{注文ステータス}
    V -->|調理中| W[待機]
    V -->|配達中| X[配達追跡]
    V -->|完了| Y[注文完了]
    
    W --> V
    X --> V
    
    style A fill:#FF6B6B
    style E fill:#4ECDC4
    style K fill:#45B7D1
    style S fill:#96CEB4
    style Y fill:#FFEAA7
```
- アカウント作成不要
- 名前の入力のみで開始

### 注文処理の詳細フロー

#### 1. ユーザー登録
- アカウント作成不要
- 名前の入力のみで開始

#### 2. メニュー閲覧
- APIから動的に読み込まれるピザメニュー
- リアルタイムでの価格・在庫情報更新

#### 3. 注文プロセス
注文には以下の情報のみ必要：
- ユーザー名
- 電話番号
- 住所
- GPS位置情報（可能な場合）

### 4. 支払いシステム
支払いは配達時に行われるため、アプリ内での決済処理は不要

### 5. 注文管理
- APIへのPOSTリクエストで注文データ（ユーザーデータ + 選択されたピザ）を送信
- 一意の注文IDの発行
- 注文後でも「優先」注文へのアップグレード可能

## 🔧 セットアップと実行

### 必要条件
- Node.js
- npm または yarn

### インストール手順

プロジェクトを開始するには、GitHubリポジトリからファイルをダウンロードし、以下のコマンドを実行：

```bash
# 依存関係のインストール
npm i

# 開発サーバーの起動
npm run dev
```

## 🎯 プロジェクトの目標

このアプリケーションは、実際のピザ注文ウェブサイトをシミュレートするReactベースのプロジェクトとして設計されており、以下の点に重点を置いています：

- **シンプリシティ**: 複雑な認証システムを排除した直感的なUX
- **効率性**: 迅速な注文プロセスと自動化された価格計算
- **柔軟性**: 注文後の優先度変更とリアルタイム追跡
- **実用性**: GPS連携による配達の最適化

このプロジェクトは、現代的なReact開発のベストプラクティスを実証し、実用的なeコマースアプリケーションの構築方法を学習する優れたサンプルとなっています。
