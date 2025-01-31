# DataMasking at Scale
Code artifacts for Data Masking/Obfuscation

This project provides reusable code to mask existing big data and generate synthetic data at scale using PySpark (Fabric/Databricks).

Notebooks are developed on [Microsoft Fabric](https://www.microsoft.com/en-us/microsoft-fabric?msockid=243318f36141605817eb09166541669f).  
If running on a different platform, adjust paths and data locations accordingly.

Read more about the implementation at: [Link Placeholder]

---

## 📂 Repository Structure

### 1️⃣ `config.ipynb`
- **Purpose**: Defines PII columns, file locations, and Faker functions.
- **Modify**: Update `pii_column_mapping` to define new PII columns.

### 2️⃣ `Common Udfs.ipynb`
- **Purpose**: Implements PySpark UDFs using Faker to generate fake data.
- **Modify**: Add new UDFs if additional data types need masking.

### 3️⃣ `Runner - data masking utility.ipynb`
- **Purpose**: Loads data, applies transformations using UDFs, and writes masked data back.
- **Modify**: Adjust file paths or integrate with different storage formats.
- **Run**: Execute this notebook to apply data masking.

### 4️⃣ `PII Identifier using LLM.ipynb`
- **Purpose**: Uses LLM to identify PII columns and generate config mappings automatically.
- **Modify**: Adjust model parameters or extend functionality.
- **Run**: Execute this notebook to auto-generate `pii_column_mapping`.

---

## 🚀 Execution Steps

1. **Update** `config.ipynb` with the correct PII mappings and file locations.
2. **Modify** `Common Udfs.ipynb` if new masking functions are required.
3. **Run** `Runner - data masking utility.ipynb` to apply transformations.
4. *(Optional)* **Execute** `PII Identifier using LLM.ipynb` to generate the configuration automatically.

---

## 🔄 Maintaining Referential Integrity

- Use **consistent Faker functions and seed values** to generate repeatable fake data.
- Ensure **CustomerID or foreign keys** are masked consistently across related tables.

---

## 🛠️ Enhancements

- Store masking logic **within table metadata** instead of using a separate config file.
- **Automate PII detection** and config generation using LLMs.

---

## ▶️ How to Run

1. **Ensure dependencies** are installed (`PySpark`, `Faker`, LLM models if applicable).
2. **Execute** `Runner - data masking utility.ipynb` **after updating configurations**.

---

## 💡 Contributing

For issues or contributions, feel free to **submit a pull request** or **raise an issue**! 🚀
