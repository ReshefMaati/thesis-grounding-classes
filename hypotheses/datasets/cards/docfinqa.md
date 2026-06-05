---
dataset_id: docfinqa
dataset_name: DocFinQA
paper_or_description_url: https://aclanthology.org/2024.acl-short.42/
dataset_download_url: https://huggingface.co/datasets/kensho/DocFinQA
corpus_download_url: https://huggingface.co/datasets/kensho/DocFinQA
license: MIT
domain: financial_reports
document_source_type:
  - sec_filings
  - annual_reports
  - long_financial_documents
corpus_scope: "FinQA questions augmented with full-document SEC filing context, extending short financial QA into long-document QA."
corpus_availability_status: full_corpus_available_large_files
pilot_priority: 2
dataset_fetch_steps:
  - "Load kensho/DocFinQA from Hugging Face."
  - "Start with dev.json due to file size."
  - "Inspect exact JSON schema before full download."
corpus_fetch_steps:
  - "Use train/dev/test JSON files containing full document context."
  - "Avoid full train download until storage and parsing needs are clear."
data_format:
  - JSON
  - HuggingFace dataset
splits:
  - train
  - dev
  - test
question_count: 7437
document_count: "Full SEC filings linked to FinQA examples; exact unique filing count to verify"
record_fields:
  - question_to_verify
  - answer_to_verify
  - full_document_context_to_verify
  - finqa_fields_to_verify
answer_fields:
  - answer_to_verify
evidence_fields:
  - original_finqa_evidence_to_verify
  - full_document_context
source_document_fields:
  - filing_context
  - document_id_to_verify
document_content_availability: full_document_context_in_large_json_files
metadata_fields:
  - company_to_verify
  - filing_to_verify
  - split
table_or_structured_data_fields:
  - financial_tables_to_verify
  - numerical_reasoning_program_to_verify
existing_annotations:
  - finqa_qa_pairs
  - full_document_context
unanswerable_or_ambiguous_policy: "Derived from answerable FinQA questions; verify if any examples become unsupported after augmentation."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - aggregation
normalization_risks:
  - "Files are large: train is several GB."
  - "Need inspect whether tables are preserved in a useful structure."
  - "Because it derives from FinQA, question distribution may inherit FinQA's financial reasoning bias."
pilot_value: "High as a long-document version of FinQA; useful for testing whether full-document context changes grounding classification."
blocking_questions:
  - "What exact fields are exposed in the public JSON?"
  - "How are original FinQA evidence spans represented?"
  - "Can we sample dev without downloading the full train file?"
sources:
  - https://huggingface.co/datasets/kensho/DocFinQA
  - https://aclanthology.org/2024.acl-short.42/
  - https://arxiv.org/abs/2401.06915
---

# דאטהסט: DocFinQA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2024.

הערכה למרכזיות בהערכות RAG רחבות: בינונית בתוך long-document financial QA, ונמוכה יותר כבנצ'מרק RAG כללי. DocFinQA חשוב כי הוא מחזיר את FinQA להקשר מסמכי מלא, ולכן הוא רלוונטי מאוד לשאלת retrieval ו-grounding במסמכים ארוכים. הוא עדיין פחות מבוסס מ-FinQA או TAT-QA.

הדאטהסט DocFinQA הוא מועמד טבעי להרחבה כי הוא לוקח את FinQA, שכבר נמצא ברג'יסטר, ומוסיף לו את ההקשר המסמכי המלא של הדוחות. זה חשוב מאוד למחקר שלנו: FinQA עצמו עשוי להיות "קל מדי" מבחינת איתור מקור הקרקוע כי הוא מספק הקשר קצר יחסית; DocFinQA מחזיר את השאלה למצב שבו צריך לנווט במסמך ארוך.

## מבנה המידע

### הקורפוס

הקורפוס הוא full-document context של SEC filings/annual reports. זה הופך אותו למועמד טוב לבדיקת ההבדל בין "יש לי את קטע הראיה" לבין "אני צריך למצוא את המקור בתוך מסמך ארוך".

### הדאטהסט

הדאטהסט משמר את שאלות FinQA, אבל מוסיף מסמך מלא. הקבצים ב-Hugging Face גדולים מאוד, ולכן כדאי להתחיל מ-`dev.json`. צריך לבדוק את הסכימה המדויקת לפני שימוש: האם יש שדות מקור, האם טבלאות נשמרות, ואיך נראה הקשר בין השאלה לבין המסמך המלא.

### דגימות

לא נוספו דגימות מלאות בשלב זה בגלל גודל הקבצים. שלב הדגימה המומלץ הוא הורדת `dev.json`, בחירת 5 רשומות, והשוואתן מול כרטיס FinQA הקיים.
