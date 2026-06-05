---
dataset_id: finlongdocqa
dataset_name: FinLongDocQA
paper_or_description_url: https://arxiv.org/abs/2604.03664
dataset_download_url: https://huggingface.co/datasets/Amian/FinLongDocQA
corpus_download_url: https://huggingface.co/datasets/Amian/FinLongDocQA
license: "AI2Lab Source Code License, National Taiwan University"
domain: financial_reports
document_source_type:
  - annual_reports
  - financial_tables
  - narrative_financial_text
corpus_scope: "Long structured annual reports with questions requiring document-level numerical reasoning across single or multiple tables and text."
corpus_availability_status: full_corpus_available_to_verify
pilot_priority: 2
dataset_fetch_steps:
  - "load_dataset('Amian/FinLongDocQA')"
  - "Download linked annual reports if needed for full document context."
corpus_fetch_steps:
  - "Use provided report links or annual report download instructions from the dataset card."
  - "Verify mapping from company/year/page_numbers to report files."
data_format:
  - HuggingFace dataset
  - JSONL
  - annual reports
splits:
  - test_or_single_split_to_verify
question_count: 7527
document_count: "489 companies across fiscal years 2022, 2023, 2024; exact report count to verify"
record_fields:
  - id
  - company
  - year
  - question
  - type
  - thoughts
  - page_numbers
  - python_code
  - answer
answer_fields:
  - answer
evidence_fields:
  - page_numbers
  - thoughts
source_document_fields:
  - company
  - year
  - annual_report_file_to_verify
document_content_availability: full_annual_reports_linked_to_verify
metadata_fields:
  - company
  - year
  - type
  - page_numbers
table_or_structured_data_fields:
  - financial_tables
  - python_code
existing_annotations:
  - page_numbers
  - reasoning_trace
  - executable_python_code
unanswerable_or_ambiguous_policy: "Designed as answerable numerical QA; verify no unanswerable examples."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - aggregation
normalization_risks:
  - "License is more restrictive than standard permissive dataset licenses."
  - "Thoughts field may contain reasoning traces that should not be used as ground-truth labels without care."
  - "Need verify availability and naming of annual report files."
pilot_value: "High for document-level aggregation and page-level grounding in long annual reports."
blocking_questions:
  - "Are full annual reports downloadable in a reproducible way?"
  - "Do page_numbers align cleanly after PDF parsing?"
  - "Should reasoning traces be used for labeling or only as auxiliary information?"
sources:
  - https://huggingface.co/datasets/Amian/FinLongDocQA
  - https://arxiv.org/abs/2604.03664
---

# דאטהסט: FinLongDocQA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2026.

הערכה למרכזיות בהערכות RAG רחבות: נמוכה כרגע, משום שהוא חדש מאוד. יחד עם זאת, הוא רלוונטי מאוד למגמה של long-document RAG ו-financial document QA, במיוחד כאשר רוצים לבדוק האם המודל מצליח למצוא מקורות קרקוע בתוך annual reports ארוכים ולא רק לעבוד על הקשר קצר שנבחר מראש.

הדאטהסט FinLongDocQA הוא מועמד חשוב כי הוא מכוון בדיוק לבעיה שבה דוחות שנתיים ארוכים מכילים את המידע הנדרש, אבל הראיות מפוזרות על פני עמודים, טבלאות וטקסט. הוא פחות ארגוני במובן מוצרי/תמיכתי, אבל חזק מאוד לבדיקת מחלקת האגרגציה ולבדיקת השאלה האם RAG קלאסי נופל כאשר הקרקוע אינו צ'אנק מקומי.

## מבנה המידע

### הקורפוס

הקורפוס מבוסס על annual reports ארוכים מאוד. לפי כרטיס הדאטהסט, הדוחות יכולים לעבור 129k tokens, והשאלות מכוונות למצבים שבהם יש לאתר טבלאות רלוונטיות ולעיתים לשלב אותן עם טקסט נרטיבי.

### הדאטהסט

כל רשומה כוללת שאלה, תשובה, סוג שאלה (`table`, `text`, `mixed`), עמודים רלוונטיים, קוד Python לחישוב, ושרשרת מחשבה/הסבר. מבחינתנו, השדה החשוב ביותר הוא `page_numbers`, כי הוא מאפשר לבדוק האם הסוכן מזהה את מקורות הקרקוע הנכונים לפני שלב החישוב.

### דגימות

הדוגמא בכרטיס Hugging Face מציגה רשומה עם `company`, `year`, `question`, `type`, `thoughts`, `page_numbers`, `python_code`, ו-`answer`. בשלב הבא צריך למשוך 5 רשומות מתוך הדאטהסט ולבדוק האם אפשר למפות אותן לדוח השנתי המלא.
