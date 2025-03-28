# Micro Domain Platform (MDP)

MDP（**Micro Domain Platform**）是一個基於 **.NET** 的開發平台，旨在為各類應用程式（**WebSite**、**iOS App**、**Android App**）提供高效、模組化的架構支援。

<img src="https://raw.githubusercontent.com/MDPCore/.github/refs/heads/main/docs/MDPCore-平台架構.png" width="500"/>

MDP將應用系統切割為：模組、隔離、平台、函式庫四個分層，透過架構設計提供模組重用、參數調整、環境建置...等等面向的快速開發能力。

- 模組：企業的商業知識、共用的功能邏輯，在MDP裡會被開發成為一個一個的「模組」，方便開發人員依照商業需求，快速組合出應用系統。

- 隔離：MDP加入「隔離」的設計，並且模組開發遵循三層式架構設計， 以減少模組對於元件、平台、框架的直接依賴，方便開發人員依照技術需求，快速抽換相依元件。

- 平台：MDP透過「平台」的設計，提供一個開箱即用的執行平台，將參數調整、模組整合、環境調適...等等環境建設作業簡化封裝，方便開發人員依照專案需求，快速搭建執行環境。

- 函式庫：MDP 提供「函式庫」的設計，提供各種基礎功能及工具，像是檔案存取、實體取號、記憶體快取、非同步執行...等函式庫，方便開發人員依照專案需求，快速導入各種基礎功能。


## 程式架構

<img src="https://raw.githubusercontent.com/MDPCore/.github/refs/heads/main/docs/MDPCore-程式架構.png" width="500"/>

MDP遵循三層式架構，將模組開發切割為：系統展示、領域邏輯、資料存取三個分層，減少模組對於元件、平台、框架的直接依賴，提高模組自身的內聚力。

- 系統展示(Presentation)：與目標客戶互動、與遠端系統通訊...等等的功能邏輯，會被歸類在系統展示。例如，使用MessageBox通知使用者處理結果、提供API給遠端系統使用。

- 領域邏輯(Domain)：封裝商業知識的物件、流程、演算法...等等的功能邏輯，會被歸類在領域邏輯。例如，出勤系統的刷卡記錄物件、購物商城的折購計算規則。

- 資料存取(Accesses)：資料庫的新增修改、遠端服務的呼叫調用...等等的功能邏輯，會被歸類在資料存取。例如，將資料存放到SQL Server、或者是從遠端API取得資料。

MDP的模組程式遵循此分層，將每個模組拆解為五種類型的專案，依序命名為：

- Module001.csproj：領域邏輯專案。

- Module001.Web.csproj：系統展示專案。(前台&API)

- Module001.Admin.csproj：系統展示專案。(後台)

- Module001.Mocks.csproj：資料存取專案。(Mocks)

- Module001.Accesses.csproj：資料存取專案。(SQL、REST、Cache)

而在MDP的領域邏輯(Domain)裡，也加入了下列設計，來進一步提升程式開發速度。

- Entity：DDD領域模型的實例物件(Class)，用以定義資料物件的物件屬性，並可以封裝商業邏輯成為物件方法。

- Repository：資料庫存取的邊界介面(Interface)，用來定義實例物件(Entity)進出資料庫的介面方法。

- Provider：遠端系統調用的邊界介面(Interface)，用來定義實例物件(Entity)進出遠端系統的介面方法。

- Service：商業知識的流程即演算法的封裝物件(Class)，封裝商業邏輯成為物件方法。也可以設計為邊界介面(Interface)，將商業邏輯用實做注入的方式使用。

- Context：做為模組入口的根物件(Class)，遵循Facade Pattern設計的原則，將上述四種物件與介面進行收整。除了做為模組被註冊、注入、使用的根物件之外，也可以封裝商業邏輯成為物件方法。