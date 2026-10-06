# MedStore Pharmacy Inventory & Billing System

A modular Python console application developed for the **Fundamentals of Computing** coursework at **Islington College** (affiliated with London Metropolitan University). The application demonstrates modular programming, file-based data persistence, transaction handling, input validation, and formatted invoice generation using standard Python.

---

## Overview

- **Author:** Om Dangol
- **Role:** Solo Developer (Coursework Project)
- **Language:** Python 3.10+
- **Dependencies:** None (Pure Python Standard Library)
- **Interface:** Interactive Console (CLI)
- **Persistence:** Comma-delimited text storage (`medicines.txt`)

---

## System Architecture

The application is structured into focused single-responsibility modules:

```
pharmacy-inventory-management-system/
├── main.py             # CLI entry point, main menu loop, error orchestration
├── inventory.py        # File I/O operations (load_inventory, save_inventory)
├── sales.py            # Sales transactions, stock decrements, invoice generation
├── restock.py          # Supplier restock intake, stock increments, restock notes
├── search.py           # Keyword search across medicine names and brands
├── display.py          # Formatted tabular display of current stock
├── utils.py            # Validated user inputs (integers, floats, non-empty strings)
├── medicines.txt       # Primary comma-separated inventory data store
├── .gitignore          # Ignores __pycache__, bytecode, and temp files
└── README.md           # Documentation
```

---

## Features

### 1. Stock Tracking & Synchronization
- Loads inventory records on startup from `medicines.txt`.
- Formats records with Name, Brand, Quantity, Tablet Price, Strip Price, and Tablets per Strip.
- Saves state atomically upon completion of any transaction.

### 2. Sales Processing & Invoicing
- Supports purchasing by individual tablets or full strips.
- Validates available stock before confirming any transaction.
- Automatically calculates subtotal, quantity-based discounts (5% on 2+ strips of the same medicine), and grand totals.
- Generates a timestamped text invoice saved locally (e.g., `sale_YYYYMMDD_XXXX.txt`).

### 3. Supplier Restocking
- Allows restocking existing medicine stock or registering new products.
- Updates unit pricing and pack sizes.
- Generates formatted restock notes for audit trails.

### 4. Search & Display
- Real-time substring search by generic medicine name or manufacturer brand.
- Clean tabular view of active inventory with pricing and packaging breakdown.

### 5. Input Validation & Resilience
- Safe input sanitization prevents application crashes on invalid numeric types.
- Missing file fallback gracefully initializes an empty repository.

---

## Implementation Status

### Implemented (Verified in Active Codebase)
- **File-Based CSV Persistence:** Atomically synchronizes stock levels to and from comma-separated text storage (`medicines.txt`).
- **Transactional Billing:** Decrements available stock, calculates 5% bulk discounts on 2+ strips of matching medicines, and outputs grand totals.
- **Invoice & Note Generation:** Emits timestamped, human-readable sales invoices (`sale_YYYYMMDD_XXXX.txt`) and supplier restock notes.
- **Supplier Restocking:** Adds new products or increments inventory quantities for existing catalogue items.
- **Search & Filter:** Keyword substring matching across generic drug names and pharmaceutical brands.
- **Input Sanitization:** Guarded CLI input functions prevent program termination on malformed types or empty values.

### In Progress
- *None (Academic Coursework Deliverable Complete).*

### Planned (Future Enhancements)
- **Relational Persistence:** Migrating from flat CSV files to an embedded SQLite or PostgreSQL backend with multi-process file locking.
- **Web Interface:** Constructing a lightweight FastAPI or Flask administrative dashboard.

---

## Quick Start

### Prerequisites
- Python 3.10 or higher.
- No third-party packages or virtual environment required.

### Running the Application

```bash
# Clone the repository
git clone https://github.com/omwe77/pharmacy-inventory-management-system.git
cd pharmacy-inventory-management-system

# Run the entry point
python main.py
```

---

## Data Schema (`medicines.txt`)

Records are stored in standard CSV format:
```text
MedicineName,BrandName,QuantityInTablets,PricePerTablet,PricePerStrip,TabletsPerStrip
```

Example:
```text
Paracetamol,ABC Pharma,200,2.5,25.0,10
Amoxicillin,MedLife,60,5.0,50.0,10
```

---

## Testing & Verification

The codebase can be syntax-checked across all modules:

```bash
python -m py_compile *.py
```

---

## Known Limitations

- **Concurrency:** Uses local file I/O intended for single-terminal operation; lacks file locking for multi-process concurrency.
- **Data Scale:** In-memory list operations suited for small-to-medium retail catalogs rather than large enterprise databases.
- **Interface:** Terminal-only CLI without a GUI or web frontend.

---

## License

Developed as academic coursework for Islington College / London Metropolitan University. Open for educational reference.
