# Library Inventory Preprocessing Report

## Executive Summary
This document outlines the key findings and transformations applied during the preprocessing of the library inventory data. The preprocessing focused on handling missing values, standardizing inconsistent data, and improving overall data quality for analytical purposes.

Note that the inventory number is the identifier for a book in the library, we were authorised by the library keeper to drop any rows with a missing inventory number, but in this data set, the inventory number attribute was complete (0% missing values).

## Data Characteristics

### **Most Frequent Values by Category**
| **Category** | **Most Frequent Value** | **Implication** |
|--------------|------------------------|-----------------|
| **Author** | Hazi Mohammed | Single author dominates collection |
| **Editor** | OPU | Primary publisher of institutional materials |
| **Edition Location** | Alger | Most publications originate from capital |
| **Acquisition Mode** | Bought | Purchases are primary acquisition method |
| **Book Status** | Pret Externe | Most books are available for external loan |
| **Localisation** | ENSIA | Main storage location for collection |

## Key Findings & Patterns

### **1. Editor-Acquisition Mode Relationship**
**Critical Insight**: When analyzing editors by acquisition mode, **gifted passive books** are responsible for the majority of cases with **unavailable editor information**.

**Interpretation**:
- Gifted books often lack complete metadata
- Passive acquisition methods correlate with missing publisher data
- Requires special imputation strategy for gifted items

### **2. Data Completeness Assessment**
- **Titles**: 100% available (used as primary key for imputation)
- **Editors**: Significant missing values in gifted items
- **Authors/Details**: Scattered missing values across older acquisitions

## Preprocessing Strategy

### **Imputation Methodology**

#### **Primary Imputation (Title-Based Lookup)**
For books with missing: **editor, author, publication date, or edition location**