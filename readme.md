# dbt Cloud Discovery API Cookbook

This repository contains a Python notebook for interacting with the dbt Cloud Discovery API to analyze models, test results, and metadata from your dbt Cloud projects.

## Setup Instructions

### Prerequisites

- Python 3.7+
- Cursor IDE (fork of VS Code) or any other Python IDE
- dbt Cloud account with API access
- GitHub account (for version control)

### Installation

1. **Clone the repository**

```bash
git clone https://github.com/yourusername/dbt-discovery-cookbook.git
cd dbt-discovery-cookbook
```

2. **Create a virtual environment**

```bash
python -m venv venv
```
or
```bash
python3 -m venv venv
```

3. **Activate the virtual environment**

On macOS/Linux:
```bash
source venv/bin/activate
```

On Windows:
```bash
venv\Scripts\activate
```

4. **Install required packages**

```bash
pip install -r requirements.txt
```

5. **Create a `.env` file**

Create a file named `.env` in the root directory with the following content:

```
# dbt Cloud API credentials
DBT_CLOUD_TOKEN=your_dbt_cloud_api_token_here
DBT_CLOUD_ACCOUNT_ID=your_account_id_here

# dbt Cloud Discovery API specifics
DBT_ENVIRONMENT_ID=your_environment_id_here
# Use the correct URL for your region:
DISCOVERY_API_URL=https://metadata.cloud.getdbt.com/graphql
# DISCOVERY_API_URL=https://metadata.emea.dbt.com/graphql
# DISCOVERY_API_URL=https://metadata.au.dbt.com/graphql
```

### Finding Your Credentials

1. **dbt Cloud API Token**:
   - Log in to dbt Cloud
   - Go to Account Settings → API Access
   - Create a Service Account token with "Metadata Only" permissions

2. **Account ID**:
   - Found in the URL when logged into dbt Cloud: `https://cloud.getdbt.com/accounts/[ACCOUNT_ID]/...`

3. **Environment ID**:
   - Found in the URL when viewing an environment: `https://cloud.getdbt.com/deploy/[ACCOUNT_ID]/projects/[PROJECT_ID]/environments/[ENVIRONMENT_ID]/`

4. **Discovery API URL**:
   - Use the appropriate URL for your region (see `.env` example)

## Running the Notebook

1. **Open the project in Cursor IDE**

```bash
cd dbt-discovery-cookbook
cursor .
```

2. **Open the notebook file**

Navigate to `dbt_discovery_cookbook.ipynb` in Cursor IDE and open it.

3. **Run the cells in order**

The notebook contains the following main sections:

- API connectivity setup
- Model discovery functions
- Test results analysis
- Coverage visualization

Run each cell in sequence, starting from the top.

## Key Functions

- `run_graphql_query(query, variables)` - Base function for GraphQL queries
- `get_models_discovery(limit=10)` - Retrieve models from dbt Cloud
- `get_test_results(limit=100)` - Retrieve test results
- `analyze_test_coverage(test_results_df, models_df)` - Generate test coverage metrics
- `visualize_test_results(test_results_df, coverage_analysis_df)` - Create visualizations

## Troubleshooting

If you encounter issues:

1. **Run the debug function**:
   ```python
   debug_test_results_query()
   ```

2. **Check common problems**:
   - Authentication: Make sure to use `Bearer` token format for Discovery API
   - Environment ID: Verify it's valid and accessible
   - API URL: Confirm you're using the correct URL for your region

3. **Query structure**:
   - Some environments require the `applied` node in queries
   - Others use a flat structure directly under `environment`
   - The debug function will help identify which to use

## GitHub Integration

To push changes to your GitHub repository:

```bash
git add .
git commit -m "Your commit message"
git push origin main
```

## License

[MIT License](LICENSE)
