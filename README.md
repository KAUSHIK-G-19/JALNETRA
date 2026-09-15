# JALNETRA

### AI-powered geospatial intelligence for watershed development

JALNETRA is a geospatial dashboard for turning satellite imagery, watershed geometry, field observations, and water-resource data into practical decision support. It combines a FastAPI service layer with a browser-based dashboard for monitoring watershed health and prioritizing interventions.

## What it does

- Searches and resolves locations using geospatial services with resilient fallback handling.
- Delineates watershed polygons and calculates geodesic area.
- Maps nearby water resources such as check dams, farm ponds, percolation tanks, and contour bunds.
- Queries Copernicus Sentinel-2 scene metadata and multi-month telemetry.
- Calculates NDVI and NDWI indicators for vegetation and water monitoring.
- Classifies raster imagery with a PyTorch U-Net land-cover model.
- Compares before-and-after imagery for vegetation and water change detection.
- Captures EXIF-based field observations and supports intervention planning.
- Generates an officer-ready watershed assessment PDF.

## Technology

| Layer | Technology |
| --- | --- |
| Interface | HTML, CSS, JavaScript, Leaflet, Chart.js |
| API | Python, FastAPI, Uvicorn |
| Geospatial data | Copernicus Data Space, Sentinel-2, OpenStreetMap services |
| Machine learning | PyTorch U-Net segmentation |
| Raster and analysis | NumPy, Pillow |
| Reporting | ReportLab |

## Run locally

### 1. Create and activate a virtual environment

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
```

### 2. Install dependencies

```powershell
python -m pip install -r requirements.txt
```

### 3. Start the API and dashboard

```powershell
python -m uvicorn app:app --host 127.0.0.1 --port 8000
```

Open [http://127.0.0.1:8000](http://127.0.0.1:8000) in a browser.

The VS Code launch configuration also includes **Run JALNETRA Dashboard**.

## Optional Copernicus credentials

The application can use Copernicus Data Space credentials for authenticated Sentinel-2 queries. Set these variables in the shell before starting the server:

```powershell
$env:COPERNICUS_USERNAME = "your-email@example.com"
$env:COPERNICUS_PASSWORD = "your-password"
```

Do not commit credentials or `.env` files. They are excluded by `.gitignore`.

## API highlights

| Endpoint | Purpose |
| --- | --- |
| `GET /api/location/search` | Resolve a place name to coordinates |
| `GET /api/watersheds` | Retrieve a watershed polygon and area |
| `GET /api/water-resources` | Retrieve nearby water-resource features |
| `GET /api/sentinel/search` | Search Sentinel-2 scene metadata |
| `GET /api/ndvi` | Request vegetation index data |
| `GET /api/ndwi` | Request water index data |
| `POST /api/classification` | Classify an uploaded raster |
| `POST /api/change-detection` | Compare two raster images |
| `POST /api/field-observations` | Submit field evidence |
| `POST /api/reports/generate-officer-pdf` | Generate a PDF report |

Interactive API documentation is available at [http://127.0.0.1:8000/docs](http://127.0.0.1:8000/docs) while the server is running.

## Project structure

```text
.
├── app.py                         # FastAPI application and API routes
├── static/index.html              # Served dashboard interface
├── services/                      # Geospatial, satellite, and ML services
├── requirements.txt               # Python dependencies
├── .vscode/launch.json             # VS Code debug configuration
└── .gitignore
```

## Data and scientific integrity

JALNETRA presents remote-sensing outputs as decision support. Remote service availability, cloud coverage, image quality, and field verification can affect results. Recommendations should be validated by qualified watershed officers before implementation.

## License

No license has been selected for this project yet.