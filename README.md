# Satellite Tracking Project

## Project Overview

Welcome to the Satellite Tracking Project! This project is designed to track the positions of satellites in space using TLE (Two-Line Element) data, convert their coordinates into Latitude, Longitude, and Altitude (LLA) format, and filter these positions based on a user-defined geographic region. The project is optimized for handling large datasets efficiently using GPU acceleration with CUDA.

## Features

- **Satellite Position Retrieval**: Extracts satellite positions using TLE data over a one-day period with one-minute intervals.
- **ECEF to LLA Conversion**: Converts satellite positions from Earth-Centered, Earth-Fixed (ECEF) coordinates to Latitude, Longitude, and Altitude (LLA).
- **Region-Based Filtering**: Filters satellite positions to only include those within a specified rectangular region.
- **Performance Optimization**: Utilizes CUDA for GPU acceleration to significantly reduce computation time, making it scalable for large datasets.

## How It Works

### Step 1: Satellite Position Retrieval
Using the `sgp4` library, the script reads TLE data and calculates the satellite positions (ECEF coordinates) at each minute for a 24-hour period. The positions are stored along with the corresponding velocities.

### Step 2: ECEF to LLA Conversion
The project uses a custom CUDA kernel to convert ECEF coordinates to LLA format efficiently on the GPU. This step ensures the data is in a human-readable format (latitude, longitude, altitude).

### Step 3: Region-Based Filtering
A CUDA-accelerated function filters the satellite positions to only include those within a user-defined rectangular geographic region. This is done using the ray-casting algorithm to determine if a point lies within the polygon.

### Step 4: Output Generation
Filtered positions are written to an output file, which includes the satellite name, timestamp, latitude, longitude, and altitude.

## Optimization Strategy

### 1. GPU Acceleration with CUDA
The most significant optimization is offloading computationally expensive tasks (like coordinate conversion and point-in-polygon checks) to the GPU using CUDA. This approach leverages parallel processing, which drastically reduces execution time compared to CPU-only processing.

### 2. Efficient Data Handling
Arrays are pre-allocated and data transfers between CPU and GPU are minimized to avoid unnecessary overhead. This ensures that the GPU resources are used efficiently.

### 3. Batch Processing
Satellite positions are processed in batches to ensure that the GPU's memory is used optimally, preventing bottlenecks due to memory constraints.

### 4. Modular Code Structure
The code is modularized, allowing for easy updates and maintenance. Functions are designed to be reusable, and the codebase is organized into distinct sections for reading data, processing, filtering, and outputting results.

## How to Run the Project

### Prerequisites
- **Python**: Ensure Python 3.x is installed.
- **CUDA**: Install CUDA Toolkit to enable GPU acceleration.
- **Libraries**: Install required libraries using pip:
  ```bash
  pip install numpy sgp4 pyproj shapely matplotlib numba
