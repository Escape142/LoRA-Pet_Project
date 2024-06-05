
# LoRA-Pet_Project: Fine-tuning LLMs with LoRA 🚀

Welcome to the LoRA-Pet_Project! Our mission is to enhance the capabilities of large language models (LLMs) using LoRA (Low-Rank Adaptation) technology, specifically tailored for domain-specific tasks. This project focuses on the accurate interpretation and translation of mixed-language technical specifications into catalog entries.

## 📘 Project Overview

Our domain frequently encounters inputs that combine Russian and English terminology, along with precise technical specifications such as DN sizes, fittings, and ГОСТ standards. The primary challenge is to process these inputs accurately to provide detailed product information, including units of measurement, composition, length, and specific fittings.

### 🎯 Example Task

**Objective:** Efficiently translate detailed customer inquiries into accurate catalog positions.

#### Dataset Illustration:

- **Input:** `Рукав 15,9-110-1000-0,2-11/11-М27х1,5`
- **Output:**
  - **Ед. Изм. (Unit of Measurement):** шт. (piece)
  - **Простая/составная (Simple/Compound):** Составная (Compound)
  - **Продукт/рукав (Product/Hose):** 2SN DN16
  - **Длина (Length):** 1000
  - **Фитинг левый (Left Fitting):** DKOL27X1,5DN16
  - **Фитинг правый (Right Fitting):** DKOL27X1,5DN16

- **Input:** `РВД HDB520-PA420SF9V4A-90-920X/GEVS`
- **Output:**
  - **Ед. Изм. (Unit of Measurement):** шт. (piece)
  - **Простая/составная (Simple/Compound):** Составная (Compound)
  - **Продукт/рукав (Product/Hose):** 4SH DN19
  - **Длина (Length):** 920
  - **Фитинг левый (Left Fitting):** SFS41,3DN19
  - **Фитинг правый (Right Fitting):** SFS41,3(90)DN19

## 🤝 Contributing

We actively encourage community contributions. Whether it's refining algorithms, refining the dataset, or enhancing our tools, your input is invaluable. Interested in contributing? Check out our issues tab or submit a pull request.

## ⚖️ License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

Thank you for exploring the LoRA-Pet_Project. Together, we are advancing the frontiers of domain-specific language processing!
