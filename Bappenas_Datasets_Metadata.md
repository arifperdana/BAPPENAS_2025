# Bappenas Indonesia Regional Economic Dataset - Metadata

## Dataset Overview

This collection contains economic, demographic, and spatial data for Indonesian provinces and cities, sourced from Bappenas (Ministry of National Development Planning). The dataset includes regional economic indicators, input-output analysis, and spatial characteristics across Indonesia's administrative regions.

**Data Source:** Bappenas (Badan Perencanaan Pembangunan Nasional)  
**Geographic Coverage:** Indonesia (34 provinces, 25 major cities)  
**Temporal Coverage:** 2015-2023  
**Last Updated:** 2023  
**Data Quality:** Clean, structured datasets with minimal missing values

---

## Dataset Files

### 1. Regional Economic Indicators (`bappenas_regional_clean.csv`)

**Description:** Time-series data of provincial economic indicators by sector from 2015-2023.

**Dimensions:**
- Rows: 360
- Columns: 10
- Time Period: 2015-2023 (9 years)
- Provinces: 10 provinces
- Sectors: 4 major sectors

**Columns:**

| Column Name | Data Type | Description | Unit | Missing Values |
|------------|-----------|-------------|------|----------------|
| `province` | String | Province name | - | 0 |
| `province_code` | Integer | Official province code | - | 0 |
| `year` | Integer | Year of observation | - | 0 |
| `sector` | String | Economic sector | - | 0 |
| `grdp` | Float | Gross Regional Domestic Product | Trillion IDR | 0 |
| `employment` | Float | Employment rate | Percentage (%) | 0 |
| `population` | Float | Population in sector | Percentage (%) | 0 |
| `sector_contribution` | Float | Sector contribution to GRDP | Percentage (%) | 0 |
| `poverty_rate` | Float | Provincial poverty rate | Percentage (%) | 0 |
| `grdp_growth` | Float | Year-over-year GRDP growth | Percentage (%) | 40 (11.1%) |

**Sectors Included:**
1. Agriculture
2. Manufacturing
3. Mining
4. Services

**Key Features:**
- Longitudinal data allowing trend analysis
- Multi-sector economic indicators
- Integration of demographic and economic metrics
- Missing values primarily in GRDP growth (first year of each series)

---

### 2. Inter-Regional Input-Output Summary (`bappenas_irio_summary.csv`)

**Description:** Input-output analysis summary showing inter-sectoral linkages and multiplier effects for the Indonesian economy.

**Dimensions:**
- Rows: 16
- Columns: 12
- Coverage: National-level sectoral analysis

**Columns:**

| Column Name | Data Type | Description | Unit | Missing Values |
|------------|-----------|-------------|------|----------------|
| `sector_code` | String | Sector identification code (S01-S16) | - | 0 |
| `sector_name` | String | Full sector name | - | 0 |
| `output` | Float | Total sector output | Trillion IDR | 0 |
| `intermediate_input` | Float | Intermediate consumption | Trillion IDR | 0 |
| `value_added` | Float | Value added by sector | Trillion IDR | 0 |
| `final_demand` | Float | Final demand for sector goods | Trillion IDR | 0 |
| `export` | Float | Export value | Trillion IDR | 0 |
| `import` | Float | Import value | Trillion IDR | 0 |
| `output_multiplier` | Float | Output multiplier effect | Ratio | 0 |
| `employment_multiplier` | Float | Employment multiplier effect | Ratio | 0 |
| `backward_linkage` | Float | Backward linkage index | Index | 0 |
| `forward_linkage` | Float | Forward linkage index | Index | 0 |

**Sectors Included:**
1. Agriculture, Forestry, Fishing (S01)
2. Mining and Quarrying (S02)
3. Manufacturing (S03)
4. Electricity, Gas, Water (S04)
5. Construction (S05)
6. Wholesale and Retail Trade (S06)
7. Transportation and Storage (S07)
8. Accommodation and Food Services (S08)
9. Information and Communication (S09)
10. Financial and Insurance (S10)
11. Real Estate (S11)
12. Business Services (S12)
13. Public Administration (S13)
14. Education (S14)
15. Health and Social Work (S15)
16. Other Services (S16)

**Key Features:**
- Comprehensive input-output analysis
- Multiplier effects for economic planning
- Linkage indices for sectoral interdependency analysis
- Trade balance indicators (export/import)

---

### 3. Provincial Spatial Data (`bappenas_province_spatial.csv`)

**Description:** Comprehensive spatial and socioeconomic indicators for all 34 Indonesian provinces in 2023.

**Dimensions:**
- Rows: 34 (all provinces)
- Columns: 19
- Reference Year: 2023

**Columns:**

| Column Name | Data Type | Description | Unit | Missing Values |
|------------|-----------|-------------|------|----------------|
| `province_code` | Integer | Official province code | - | 0 |
| `province` | String | Province name | - | 0 |
| `latitude` | Float | Geographic latitude | Degrees | 0 |
| `longitude` | Float | Geographic longitude | Degrees | 0 |
| `region` | String | Major regional grouping | - | 0 |
| `island_group` | String | Island group classification | - | 0 |
| `capital_distance_jkt` | Float | Distance from Jakarta | Kilometers (km) | 0 |
| `population_2023` | Float | Total population | Millions | 0 |
| `grdp_2023` | Float | Gross Regional Domestic Product | Trillion IDR | 0 |
| `grdp_per_capita_2023` | Float | GRDP per capita | Thousand IDR | 0 |
| `poverty_rate_2023` | Float | Poverty rate | Percentage (%) | 0 |
| `unemployment_rate_2023` | Float | Unemployment rate | Percentage (%) | 0 |
| `hdi_2023` | Float | Human Development Index | Index (0-1) | 0 |
| `literacy_rate_2023` | Float | Literacy rate | Percentage (%) | 0 |
| `infrastructure_index` | Float | Infrastructure development index | Index (0-1) | 0 |
| `agriculture_share` | Float | Agriculture sector share of GRDP | Percentage (%) | 0 |
| `manufacturing_share` | Float | Manufacturing sector share of GRDP | Percentage (%) | 0 |
| `services_share` | Float | Services sector share of GRDP | Percentage (%) | 0 |
| `mining_share` | Float | Mining sector share of GRDP | Percentage (%) | 0 |

**Regional Classifications:**
- **Regions:** Bali-Nusa Tenggara, Java, Kalimantan, Maluku-Papua, Sulawesi, Sumatra
- **Island Groups:** Bali, Java, Kalimantan, Maluku, Nusa Tenggara, Papua, Sulawesi, Sumatra

**Key Features:**
- Complete coverage of all Indonesian provinces
- Spatial coordinates for mapping and GIS analysis
- Multi-dimensional development indicators
- Sectoral composition of regional economies
- No missing values - complete dataset

---

### 4. City-Level Spatial Data (`bappenas_city_spatial.csv`)

**Description:** Detailed socioeconomic and infrastructure data for 25 major Indonesian cities in 2023.

**Dimensions:**
- Rows: 25 (major cities)
- Columns: 26
- Reference Year: 2023

**Columns:**

| Column Name | Data Type | Description | Unit | Missing Values |
|------------|-----------|-------------|------|----------------|
| `city_code` | String | City identification code | - | 0 |
| `city_name` | String | City name | - | 0 |
| `province` | String | Parent province | - | 0 |
| `province_code` | Integer | Province code | - | 0 |
| `type` | String | Administrative type | - | 0 |
| `latitude` | Float | Geographic latitude | Degrees | 0 |
| `longitude` | Float | Geographic longitude | Degrees | 0 |
| `region` | String | Major regional grouping | - | 0 |
| `island_group` | String | Island group | - | 0 |
| `population_2023` | Float | City population | Millions | 0 |
| `grdp_2023` | Float | City GRDP | Trillion IDR | 0 |
| `grdp_per_capita_2023` | Float | GRDP per capita | Thousand IDR | 0 |
| `poverty_rate_2023` | Float | Poverty rate | Percentage (%) | 0 |
| `unemployment_rate_2023` | Float | Unemployment rate | Percentage (%) | 0 |
| `hdi_2023` | Float | Human Development Index | Index (0-1) | 0 |
| `literacy_rate_2023` | Float | Literacy rate | Percentage (%) | 0 |
| `infrastructure_score` | Float | Overall infrastructure score | Index (0-1) | 0 |
| `digital_connectivity` | Float | Digital infrastructure index | Index (0-1) | 0 |
| `healthcare_facilities` | Integer | Number of healthcare facilities | Count | 0 |
| `schools` | Integer | Number of schools | Count | 0 |
| `industrial_zones` | Integer | Number of industrial zones | Count | 0 |
| `tourism_sites` | Integer | Number of tourism sites | Count | 0 |
| `average_income` | Float | Average income | Thousand IDR | 0 |
| `employment_services` | Float | Services sector employment | Percentage (%) | 0 |
| `employment_manufacturing` | Float | Manufacturing employment | Percentage (%) | 0 |
| `employment_agriculture` | Float | Agriculture employment | Percentage (%) | 0 |

**Key Features:**
- Granular city-level economic data
- Infrastructure and facility counts
- Employment distribution by sector
- Digital connectivity indicators
- Complete dataset with no missing values

---

### 5. Provincial Boundaries GeoJSON (`bappenas_provinces.geojson`)

**Description:** Geographic boundary data for Indonesian provinces in GeoJSON format for mapping and spatial analysis.

**Format:** GeoJSON FeatureCollection  
**Features:** 34 provinces  
**File Size:** 27 KB

**Structure:**
```json
{
  "type": "FeatureCollection",
  "features": [
    {
      "type": "Feature",
      "properties": {
        "province_code": "XX",
        "province": "Province Name",
        "region": "Region Name",
        "grdp_2023": float,
        "population_2023": float,
        "poverty_rate_2023": float,
        "hdi_2023": float
      },
      "geometry": {
        "type": "Polygon",
        "coordinates": [...]
      }
    }
  ]
}
```

**Properties Included:**
- Province code and name
- Regional classification
- Key 2023 indicators (GRDP, population, poverty, HDI)
- Polygon geometry for boundary visualization

**Key Features:**
- Standard GeoJSON format for GIS compatibility
- Integrated with economic indicators
- Ready for web mapping libraries (Leaflet, Mapbox, etc.)
- Compatible with spatial analysis tools (GeoPandas, QGIS, ArcGIS)

---

## Data Quality Notes

### Completeness
- **High Quality:** Most datasets are complete with no missing values
- **Minor Gaps:** GRDP growth rate has 40 missing values (11.1%) in the regional dataset, primarily for base years where growth cannot be calculated

### Data Validation
- Province codes follow official Indonesian administrative codes
- Geographic coordinates validated against known provincial capitals
- Economic indicators show reasonable ranges and distributions
- Temporal consistency maintained across years

### Known Limitations
1. Regional clean dataset covers only 10 provinces (not all 34)
2. GRDP growth missing for base year observations (2015)
3. City dataset limited to 25 major urban areas
4. GeoJSON boundaries are simplified polygons

---

## Use Cases

### Economic Analysis
- Regional economic disparity assessment
- Sectoral contribution analysis
- Economic growth trends and forecasting
- Input-output modeling and multiplier analysis

### Spatial Analysis
- Geographic visualization of economic indicators
- Distance-based analysis (proximity to Jakarta)
- Regional clustering and classification
- Urban-rural comparative studies

### Development Planning
- Infrastructure investment prioritization
- Poverty reduction strategy evaluation
- Human development assessment
- Regional development policy analysis

### Research Applications
- Regional economics research
- Development studies
- Geographic information systems (GIS) analysis
- Economic geography modeling

---

## Technical Specifications

### File Formats
- **CSV Files:** UTF-8 encoding, comma-separated
- **GeoJSON:** RFC 7946 compliant, WGS84 coordinate system (EPSG:4326)

### Coordinate Reference System
- **CRS:** WGS84 (EPSG:4326)
- **Format:** Decimal degrees
- **Coverage:** Indonesian archipelago (approximately 95°E to 141°E, 6°N to 11°S)

### Data Types
- **Numeric:** Float64 for economic indicators, Int64 for codes and counts
- **Text:** UTF-8 strings for names and classifications
- **Spatial:** GeoJSON polygons for boundaries

---

## Suggested Data Processing

### Python Libraries
```python
import pandas as pd
import geopandas as gpd
import matplotlib.pyplot as plt
import seaborn as sns
```

### Loading Data
```python
# Load CSV files
regional = pd.read_csv('bappenas_regional_clean.csv')
irio = pd.read_csv('bappenas_irio_summary.csv')
province_spatial = pd.read_csv('bappenas_province_spatial.csv')
city_spatial = pd.read_csv('bappenas_city_spatial.csv')

# Load GeoJSON
provinces_geo = gpd.read_file('bappenas_provinces.geojson')
```

### Data Joins
```python
# Join spatial data with time series
merged = regional.merge(province_spatial, 
                        on='province_code', 
                        suffixes=('', '_spatial'))

# Create geodataframe
geo_provinces = province_spatial.merge(provinces_geo, 
                                       on='province_code')
```
---

## Version History

- **v1.0 (2023):** Initial release with 2015-2023 data
- Last updated: 2023

---

## License & Usage Terms

Please refer to Bappenas official policies for data usage, attribution, and redistribution rights.

---

*This metadata document was generated based on analysis of the provided datasets. For official documentation, please refer to Bappenas publications.*
