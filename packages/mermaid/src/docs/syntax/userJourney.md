# User Journey Diagram

flowchart TD
    Start([App Launch]) --> Auth{User Authenticated?}
    Auth -->|No| Login[Login/Sign Up]
    Auth -->|Yes| RoleCheck{Role Selection}
    
    Login --> SocialLogin[Social Login Options]
    Login --> EmailSignup[Email Registration]
    SocialLogin --> LocationAccess[Request Location Access]
    EmailSignup --> LocationAccess
    
    LocationAccess --> Preferences[Select Cuisine Preferences]
    Preferences --> RoleCheck
    
    RoleCheck --> Customer[Customer Journey]
    RoleCheck --> Chef[Chef Journey]
    
    %% Customer Journey
    Customer --> Timeline[Browse Chef Timeline]
    Timeline --> Search[Search Kitchens]
    Timeline --> PostClick[Click Chef Post]
    
    Search --> FilterType{Filter Options}
    FilterType --> Location[By Location]
    FilterType --> Cuisine[By Cuisine]
    FilterType --> Verified[Verified Only]
    
    Location --> KitchenList[Kitchen Results]
    Cuisine --> KitchenList
    Verified --> KitchenList
    
    KitchenList --> KitchenProfile[View Kitchen Profile]
    PostClick --> KitchenProfile
    
    KitchenProfile --> OrderType{Choose Order Type}
    OrderType --> OneTime[One-Time Order]
    OrderType --> Trial[Trial Meal]
    OrderType --> Subscription[Meal Plan Subscription]
    
    OneTime --> MenuSelect[Select Menu Items]
    Trial --> MenuSelect
    Subscription --> PlanSelect[Choose Plan Duration]
    
    PlanSelect --> MenuSelect
    
    MenuSelect --> Available{Item Available?}
    Available -->|No| OutOfStock[Show Out of Stock]
    Available -->|Yes| Customize[Customize Meal]
    
    OutOfStock --> MenuSelect
    
    Customize --> SpiceLevel[Spice Level]
    Customize --> Portion[Portion Size]
    Customize --> Ingredients[Special Ingredients]
    
    SpiceLevel --> Cart[Add to Cart]
    Portion --> Cart
    Ingredients --> Cart
    
    Cart --> Checkout[Checkout Process]
    Checkout --> Payment[Payment Gateway]
    
    Payment --> PaymentStatus{Payment Success?}
    PaymentStatus -->|No| PaymentRetry[Retry Payment]
    PaymentStatus -->|Yes| OrderConfirm[Order Confirmation]
    
    PaymentRetry --> Payment
    OrderConfirm --> Tracking[Order Tracking]
    
    %% Chef Journey
    Chef --> ChefDashboard[Chef Dashboard]
    ChefDashboard --> ProfileSetup[Complete Profile Setup]
    ChefDashboard --> TimelinePost[Create Timeline Post]
    ChefDashboard --> MenuManage[Manage Menu Items]
    ChefDashboard --> OrderManage[Manage Orders]
    
    ProfileSetup --> FSSAI[Upload FSSAI Certificate]
    FSSAI --> Verification[Await Verification]
    
    TimelinePost --> PostType{Post Type}
    PostType --> ImagePost[Image + Description]
    PostType --> VideoPost[Video Content]
    PostType --> OfferPost[Special Offers]
    
    ImagePost --> PublishPost[Publish to Timeline]
    VideoPost --> PublishPost
    OfferPost --> PublishPost
    
    MenuManage --> AddItem[Add Menu Item]
    MenuManage --> EditItem[Edit Existing Item]
    MenuManage --> SetAvailability[Set Availability]
    
    OrderManage --> NewOrders[View New Orders]
    OrderManage --> SubscriptionOrders[Manage Subscriptions]
    
    NewOrders --> AcceptOrder{Accept Order?}
    AcceptOrder -->|Yes| PrepareOrder[Prepare & Fulfill]
    AcceptOrder -->|No| DeclineOrder[Decline with Reason]
    
    %% Edge Cases & Special Flows
    Tracking --> CustomerSupport[Contact Support]
    DeclineOrder --> CustomerNotification[Notify Customer]
    
    Subscription --> PauseResume[Pause/Resume Options]
    PauseResume --> SameDayCheck{Same Day Request?}
    SameDayCheck -->|Yes| ShowError[Show Pause Rules]
    SameDayCheck -->|No| UpdateSubscription[Update Subscription]
    
    %% Styling
    classDef customerFlow fill:#e1f5fe
    classDef chefFlow fill:#f3e5f5
    classDef decisionPoint fill:#fff3e0
    classDef errorState fill:#ffebee
    
    class Customer,Timeline,Search,MenuSelect,Cart,Checkout customerFlow
    class Chef,ChefDashboard,TimelinePost,MenuManage,OrderManage chefFlow
    class Auth,RoleCheck,OrderType,Available,PaymentStatus decisionPoint
    class OutOfStock,PaymentRetry,ShowError errorState
