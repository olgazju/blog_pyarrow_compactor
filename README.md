# PyArrow Parquet Compactor Demo

This is a demo repository for my blog post [“When Small Parquet Files Become a Big Problem”](#). It contains a simple, reproducible setup showing how to compact many small Parquet files using [PyArrow](https://arrow.apache.org/docs/python/), both with and without batching.

The demo is based on the January 2025 NYC Yellow Taxi trip dataset, which has been split into 696 small Parquet files to simulate a streaming pipeline that writes frequently.

## 📦 Setup

To run this demo:

1. Create a Python virtual environment using `pyenv`:

   ```bash
   pyenv virtualenv 3.12.2 blog_pyarrow_compactor
   pyenv local blog_pyarrow_compactor
   ```

2. Install the dependencies:

    ```bash
    pip install -r requirements.txt
    ```

3. Open the notebook:

    ```bash
    jupyter notebook compactor.ipynb
    ```

## 📁 Contents

- `demo_data/` — Folder containing ~700 small Parquet files, simulating microbatch output.
- `compactor.ipynb` — Jupyter notebook demonstrating two compaction approaches:
  - **Without batching** — a straightforward approach that reads all files at once.
  - **With batching** — a memory-safe method that processes files in chunks.
- `output_demo_data/` — Output folder for compacted files (created by the notebook).
- `requirements.txt` — Minimal Python dependencies needed to run the notebook.

## 📝 Notes

- To run this on S3 instead of local files, replace `fs.LocalFileSystem()` with `fs.S3FileSystem(region="your-region")` in the notebook.
- This demo uses the January 2025 Yellow Taxi Trip Parquet file from the [NYC Taxi & Limousine Commission](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page).
- If you run into memory issues using the non-batched version, that’s expected — it's meant to demonstrate what happens when PyArrow tries to load too many files at once.
