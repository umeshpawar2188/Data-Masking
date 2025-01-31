# Data-Masking
Code artefacts for Data masking/ Obfuscation

As part of this project developed reusable code to mask existing big data and generate synthetic data at Scale using PySpark (Fabric / Databricks)

Notebooks here are developed on Microsoft fabric - https://www.microsoft.com/en-us/microsoft-fabric?msockid=243318f36141605817eb09166541669f. If you are running it on different flatform make approproate changes to paths / location of the data.

Read more about the implementation at - 


Automating Data Obfuscation and Maintaining Data Integrity Using Gen-AI and a Configuration-Driven Approach

Introduction

Protecting Personally Identifiable Information (PII) is critical in modern data governance. This utility provides a structured, configuration-driven approach to data desensitization while ensuring referential integrity across related tables.

Sequence of Code Modifications and Execution

1. Configuration File (config.ipynb)

Defines PII columns, specifies Faker functions for data masking, and maintains referential integrity across tables.

Example Configuration:

config = {
    "table_list": ["dim_customer", "fact_sales"],
    "dimcustomer": {
        "pii_column_mapping": {
            "CustomerID": "random_int",
            "FirstName": "first_name",
            "LastName": "last_name",
            "Email": "email",
            "PhoneNumber": "phone_number",
            "DateOfBirth": "date_of_birth"
        },
        "location": "Files/synthetic_data/dim_customer_df",
        "file_format": "delta"
    },
    "factsales": {
        "pii_column_mapping": {
            "CustomerID": "random_int",
            "CustomerEmail": "email"
        },
        "location": "Files/synthetic_data/fact_sales_df",
        "file_format": "delta"
    }
}

Key Point: CustomerID is a primary key in dim_customer and a foreign key in fact_sales.

2. Data Synthesis Functions and UDFs (Common Udfs.ipynb)

Defining Fake Data Functions

Generates synthetic PII using the faker library.

Uses seed_instance(seedValue) to ensure consistent results.

Example Functions:

def get_fake_first_name(seedValue):
    fake.seed_instance(seedValue)
    return fake.first_name()

def get_fake_last_name(seedValue):
    fake.seed_instance(seedValue)
    return fake.last_name()

Registering UDFs in PySpark

get_fake_first_name_udf = udf(get_fake_first_name, StringType())
get_fake_last_name_udf = udf(get_fake_last_name, StringType())

Applying UDFs to a DataFrame

for column, fake_type in column_mapping.items():
    if fake_type == 'first_name':
        original_df = original_df.withColumn(column, get_fake_first_name_udf(original_df[column]))
    elif fake_type == 'last_name':
        original_df = original_df.withColumn(column, get_fake_last_name_udf(original_df[column]))

Significance of seedValue:

Ensures deterministic fake data.

Same seed value = same fake output across related tables.

Example Without and With Seed:
