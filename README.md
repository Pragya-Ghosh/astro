# SENSE: Signal Extraction and Noise Suppression Engine (Web)

SENSE is a full-stack web application built to process heavy astronomical data asynchronously. It allows users to upload massive datasets of noisy FITS images, processes them using memory-efficient stacking algorithms, and isolates true astronomical anomalies (such as pulsars) from background radiation.

By offloading the computationally heavy `binapprox` median stacking algorithm to a background task queue, the application processes gigabytes of high-resolution frames without blocking the web server or timing out the user's browser.

## Features

* **Asynchronous Processing Pipeline:** Upload FITS files via the web dashboard; processing is handled in the background by a dedicated worker.
* **Memory-Efficient Math:** Uses the `binapprox` algorithm to calculate the statistical median of pixel coordinates across time without overloading RAM.
* **Automated Anomaly Detection:** Applies $\sigma$-based thresholding to the master stacked image to catalog potential signal candidates.
* **Results Dashboard:** Visualizes the final noise-suppressed Master Frame and provides a clean data table of detected signal coordinates.

## Architecture

* **Frontend:** Clean web interface for drag-and-drop FITS ingestion and status tracking.
* **Backend API:** Handles HTTP requests, file storage routing, and database interactions.
* **Task Queue (Worker):** Asynchronously runs the heavy median-stacking engine and machine learning classification.
* **Database:** SQL database tracking job status, execution times, and detected signal metadata.

## Prerequisites

Ensure you have the following installed on your system:

* Python 3.10+ or Java (depending on backend implementation)
* A message broker for the task queue (e.g., Redis or RabbitMQ)
* A SQL database (e.g., PostgreSQL or SQLite for local dev)

## Setup and Installation

1. **Clone the repository:**
   ```bash
   git clone [https://github.com/yourusername/sense-web.git](https://github.com/yourusername/sense-web.git)
   cd sense-web
