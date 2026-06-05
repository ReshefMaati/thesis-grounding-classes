---
dataset_id: officeqa_pro
dataset_name: OfficeQA Pro
paper_or_description_url: https://arxiv.org/abs/2603.08655
dataset_download_url: https://huggingface.co/datasets/databricks/officeqa
corpus_download_url: https://huggingface.co/datasets/databricks/officeqa
license: to_verify
domain: government_financial_bulletins
document_source_type:
  - treasury_bulletins
  - official_government_reports
  - financial_tables
  - historical_bulletins
corpus_scope: "Historical U.S. Treasury Bulletin PDFs from 1939-2025, with parsed text files and QA over source documents."
corpus_availability_status: full_corpus_available_to_verify
pilot_priority: 1
dataset_fetch_steps:
  - "Clone https://github.com/databricks/officeqa."
  - "Load databricks/officeqa from Hugging Face."
  - "Start with officeqa_pro.csv before officeqa_full.csv."
corpus_fetch_steps:
  - "Use Hugging Face files for PDFs and parsed docs."
  - "Inspect treasury_bulletins_parsed/transformed/*.txt."
  - "Map source_files to parsed text and source_docs to Federal Reserve archive URLs."
data_format:
  - CSV
  - PDF
  - parsed TXT
splits:
  - train_or_single_split_to_verify
question_count: "OfficeQA Pro N=133 reported; full set to verify"
document_count: "Treasury Bulletin corpus from 1939-2025; exact file count to verify"
record_fields:
  - uid
  - question
  - answer
  - source_docs
  - source_files
  - difficulty
answer_fields:
  - answer
evidence_fields:
  - source_docs
  - source_files
source_document_fields:
  - source_file
  - source_url
  - parsed_text
  - original_pdf
document_content_availability: full_pdfs_and_parsed_text_to_verify
metadata_fields:
  - bulletin_date
  - source_file
  - difficulty
  - original_url
table_or_structured_data_fields:
  - financial_tables_in_pdfs
  - parsed_tables_to_verify
existing_annotations:
  - source_documents
  - source_files
  - difficulty
unanswerable_or_ambiguous_policy: "Appears designed as answerable benchmark; verify no unanswerable rows."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - aggregation
normalization_risks:
  - "Treasury Bulletins span many decades and formatting styles."
  - "Parsing quality may vary across PDFs, tables and charts."
  - "Small Pro split may be too small alone, but useful for feasibility."
pilot_value: "Very high as an official-document RAG benchmark with long historical reports and source files."
blocking_questions:
  - "Are all source_files directly resolvable to parsed text?"
  - "How much table structure is preserved in the parsed files?"
  - "Is OfficeQA Full available and usable under the same schema?"
sources:
  - https://github.com/databricks/officeqa
  - https://huggingface.co/datasets/databricks/officeqa
  - https://arxiv.org/abs/2603.08655
---

# דאטהסט: OfficeQA Pro

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2026.

הערכה למרכזיות בהערכות RAG רחבות: נמוכה כרגע בגלל החדשנות שלו, אבל עם פוטנציאל גבוה מאוד. OfficeQA Pro עדיין אינו benchmark קלאסי שחוזר בעבודות רבות, אבל הוא נראה חשוב במיוחד להערכה עתידית של RAG מעל מסמכים משרדיים/רשמיים ארוכים, בעיקר כי הוא עובד עם Treasury Bulletins, PDFs, קבצי טקסט parsed ומסמכי מקור רשמיים.

הדאטהסט OfficeQA Pro הוא מועמד חזק מאוד לפיילוט מורחב כי הוא עובד על מסמכים רשמיים מובהקים: U.S. Treasury Bulletins. אלה אינם התכתבויות או מסמכי עבודה פנימיים, אלא מסמכי מקור רשמיים שמכילים טקסט, טבלאות, תרשימים וערכים מספריים לאורך עשורים.

הדאטהסט מעניין במיוחד לתזה כי הוא מדמה בעיה ארגונית אמיתית מסוג אחר: מאגר ארוך-היסטוריה של מסמכים רשמיים, עם שינויי פורמט לאורך זמן, ועם שאלות שמצריכות לאתר מסמך נכון ולעיתים לבצע reasoning על נתונים מספריים.

## מבנה המידע

### הקורפוס

הקורפוס מבוסס על Treasury Bulletins היסטוריים מ-1939 עד 2025. לפי התיעוד, קיימים גם PDFs מקוריים וגם קבצי טקסט parsed. זה יתרון מעשי גדול: אפשר להתחיל בפיילוט מהטקסט המנורמל, ובהמשך לבדוק אם ה-PDF המקורי משנה את הקרקוע.

### הדאטהסט

הסכימה המתועדת כוללת `uid`, `question`, `answer`, `source_docs`, `source_files`, ו-`difficulty`. זו סכימה מצוינת לפיילוט כי היא מאפשרת למפות שאלה אל מסמכי מקור ספציפיים, ואז לבדוק האם הסוכן מזהה את הצורך במסמך, במטאדאטה של תאריך/קובץ, או באגרגציה על טבלאות.

### דגימות

לא הוכנסו עדיין דגימות מלאות. שלב הדגימה הבא צריך להיות הורדת `officeqa_pro.csv`, בחירת 5 רשומות, ומיפוי כל רשומה לקובץ parsed ול-PDF המקורי.
