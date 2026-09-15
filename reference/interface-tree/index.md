# Interface tree

```
TrendMinerClient
├── appliance
│   ├── get_version → str
│   ├── get_index_resolution → Timedelta
│   └── get_index_horizon → Timestamp
├── asset_framework
│   ├── create → AssetFramework
│   ├── search → PagedList[AssetFramework]
│   ├── from_identifier → AssetFramework
│   ├── from_name → AssetFramework
│   ├── asset
│   │   ├── create → Asset
│   │   ├── from_identifier → Asset
│   │   ├── from_hex_path → Asset
│   │   ├── from_path → Asset
│   │   └── search → PagedList[Asset]
│   └── attribute
│       ├── create → Attribute
│       ├── from_identifier → Attribute
│       └── search → PagedList[Attribute]
├── context
│   ├── view
│   │   ├── define → ContextHubViewDefinition
│   │   ├── create → ContextHubView
│   │   ├── from_identifier → ContextHubView
│   │   ├── from_name → ContextHubView
│   │   └── search → PagedList[ContextHubView]
│   ├── item
│   │   ├── create → None
│   │   ├── update → None
│   │   └── delete → None
│   ├── type
│   │   ├── create → ContextType
│   │   ├── from_key → ContextType
│   │   ├── from_name → ContextType
│   │   └── search → PagedList[ContextType]
│   ├── field
│   │   ├── create → ContextField
│   │   ├── from_identifier → ContextField
│   │   ├── from_key → ContextField
│   │   ├── from_name → ContextField
│   │   └── search → PagedList[ContextField]
│   ├── workflow
│   │   ├── create → ContextWorkflow
│   │   ├── from_identifier → ContextWorkflow
│   │   ├── from_name → ContextWorkflow
│   │   └── search → PagedList[ContextWorkflow]
│   └── filter
│       ├── approval
│       │   └── new → ContextApprovalFilter
│       ├── components
│       │   └── new → ContextComponentFilter
│       ├── context_types
│       │   └── new → ContextTypeFilter
│       ├── created_by
│       │   └── new → ContextCreatedByFilter
│       ├── creation_date
│       │   └── new → ContextCreationDateFilter
│       ├── description
│       │   └── new → ContextDescriptionFilter
│       ├── duration
│       │   └── new → ContextDurationFilter
│       ├── interval
│       │   └── new → ContextIntervalFilter
│       ├── keyword
│       │   └── new → ContextKeywordFilter
│       ├── period
│       │   └── new → ContextPeriodFilter
│       ├── state
│       │   └── new → ContextStateFilter
│       ├── enumeration_field
│       │   └── new → ContextEnumerationFieldFilter
│       ├── numeric_field
│       │   └── new → ContextNumericFieldFilter
│       └── string_field
│           └── new → ContextStringFieldFilter
├── dashboard
│   ├── config → DashboardConfiguration
│   ├── define → DashboardDefinition
│   ├── create → Dashboard
│   ├── from_identifier → Dashboard
│   ├── from_name → Dashboard
│   ├── search → PagedList[Dashboard]
│   ├── context
│   │   ├── config → ContextHubViewTileConfiguration
│   │   └── new → ContextHubViewTile
│   ├── external
│   │   ├── config → ExternalContentTileConfiguration
│   │   └── new → ExternalContentTile
│   ├── gauge
│   │   ├── config → GaugeTileConfiguration
│   │   └── new → GaugeTile
│   ├── monitor
│   │   ├── config → MonitorTileConfiguration
│   │   └── new → MonitorTile
│   ├── notebook
│   │   ├── config → NotebookTileConfiguration
│   │   └── new → NotebookTile
│   ├── text
│   │   ├── config → TextTileConfiguration
│   │   └── new → TextTile
│   ├── trend
│   │   ├── config → TrendHubViewTileConfiguration
│   │   └── new → TrendHubViewTile
│   └── value
│       ├── config → CurrentValueTileConfiguration
│       └── new → CurrentValueTile
├── datasource
│   ├── from_identifier → Datasource
│   ├── from_name → Datasource
│   ├── get_builtin → list[Datasource]
│   └── search → PagedList[Datasource]
├── filter
│   ├── define → FilterDefinition
│   ├── create → Filter
│   ├── from_identifier → Filter
│   ├── from_name → Filter
│   └── search → PagedList[Filter]
├── fingerprint
│   ├── define → FingerprintDefinition
│   ├── create → Fingerprint
│   ├── from_identifier → Fingerprint
│   ├── from_name → Fingerprint
│   ├── search → PagedList[Fingerprint]
│   └── layer
│       └── new → FingerprintLayer
├── monitor
│   ├── from_identifier → Monitor
│   ├── get_overview → DataFrame
│   └── search → list[Monitor]
├── notebook
│   ├── from_identifier → Notebook
│   ├── from_name → Notebook
│   ├── search → PagedList[Notebook]
│   └── pipeline
│       ├── from_identifier → Pipeline
│       ├── from_name → Pipeline
│       └── search → PagedList[Pipeline]
├── search
│   ├── value
│   │   ├── define → ValueBasedSearchDefinition
│   │   ├── create → ValueBasedSearch
│   │   ├── from_identifier → ValueBasedSearch
│   │   ├── from_name → ValueBasedSearch
│   │   └── search → PagedList[ValueBasedSearch]
│   ├── digital_step
│   │   ├── from_identifier → DigitalStepSearch
│   │   ├── from_name → DigitalStepSearch
│   │   └── search → PagedList[DigitalStepSearch]
│   ├── similarity
│   │   ├── from_identifier → SimilaritySearch
│   │   ├── from_name → SimilaritySearch
│   │   └── search → PagedList[SimilaritySearch]
│   └── area
│       ├── from_identifier → AreaSearch
│       ├── from_name → AreaSearch
│       └── search → PagedList[AreaSearch]
├── tag
│   ├── from_identifier → Tag
│   ├── from_name → Tag
│   ├── search → PagedList[Tag]
│   └── index_details
│       ├── from_name → IndexDetails
│       └── search → PagedList[IndexDetails]
├── tag_builder
│   ├── aggregation
│   │   ├── define → AggregationDefinition
│   │   ├── create → Aggregation
│   │   ├── from_identifier → Aggregation
│   │   ├── from_name → Aggregation
│   │   └── search → PagedList[Aggregation]
│   ├── custom_calculation
│   │   ├── define → CustomCalculationDefinition
│   │   ├── create → CustomCalculation
│   │   ├── from_identifier → CustomCalculation
│   │   ├── from_name → CustomCalculation
│   │   └── search → PagedList[CustomCalculation]
│   ├── formula
│   │   ├── define → FormulaDefinition
│   │   ├── create → Formula
│   │   ├── from_identifier → Formula
│   │   ├── from_name → Formula
│   │   └── search → PagedList[Formula]
│   ├── machine_learning_model
│   │   ├── from_identifier → MachineLearningModel
│   │   ├── from_name → MachineLearningModel
│   │   └── search → PagedList[MachineLearningModel]
│   ├── prediction
│   │   ├── create → Prediction
│   │   ├── from_identifier → Prediction
│   │   ├── from_name → Prediction
│   │   └── search → PagedList[Prediction]
│   └── imported
│       ├── create → None
│       ├── search → PagedList[TagImport]
│       └── from_name → TagImport
├── trend
│   ├── view
│   │   ├── define → TrendHubViewDefinition
│   │   ├── create → TrendHubView
│   │   ├── from_identifier → TrendHubView
│   │   ├── from_name → TrendHubView
│   │   └── search → PagedList[TrendHubView]
│   ├── layer
│   │   └── new → TrendHubLayer
│   └── group
│       └── new → TrendHubEntryGroup
├── user
│   ├── self → User
│   ├── from_identifier → User
│   ├── from_name → User
│   ├── all_client_users → PagedList[User]
│   ├── search → PagedList[User]
│   └── group
│       ├── from_identifier → UserGroup
│       ├── from_name → UserGroup
│       ├── search → PagedList[UserGroup]
│       └── everyone → UserGroup
└── work
    ├── transfer → None
    ├── folder
    │   ├── create → Folder
    │   ├── from_identifier → Folder
    │   ├── from_path → Folder
    │   ├── from_name → Folder
    │   ├── search → PagedList[Folder]
    │   ├── get_user_home → Folder
    │   └── get_users_root → Folder
    ├── my_work
    │   ├── search_contents → PagedList[SavedItem]
    │   └── get_item → SavedItem
    ├── shared
    │   ├── search_contents → PagedList[SavedItem]
    │   └── get_item → SavedItem
    └── favorites
        ├── search_contents → PagedList[SavedItem]
        └── get_item → SavedItem
```
