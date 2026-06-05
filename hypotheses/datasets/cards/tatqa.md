---
dataset_id: tatqa
dataset_name: TAT-QA
paper_or_description_url: https://nextplusplus.github.io/TAT-QA/
dataset_download_url: https://github.com/NExTplusplus/TAT-QA
corpus_download_url: https://github.com/NExTplusplus/TAT-QA
license: CC-BY-4.0
domain: financial_reports
document_source_type:
  - financial_reports
  - financial_tables
  - narrative_financial_text
corpus_scope: "Hybrid table-and-text contexts from real-world financial reports."
corpus_availability_status: full_processed_context_available
pilot_priority: 2
dataset_fetch_steps:
  - "Clone https://github.com/NExTplusplus/TAT-QA."
  - "Use files under TAT-QA dataset."
  - "Inspect current train/dev/test JSON schema."
corpus_fetch_steps:
  - "Use per-context tables and paragraphs distributed in the dataset."
  - "Verify whether original report metadata or source files are available."
data_format:
  - JSON
splits:
  - train
  - dev
  - test
question_count: 16552
document_count: "2757 hybrid contexts from real-world financial reports"
record_fields:
  - table
  - paragraphs
  - questions
answer_fields:
  - answer
  - answer_type
evidence_fields:
  - derivation
  - facts_to_verify
  - scale_to_verify
source_document_fields:
  - context_id_to_verify
  - report_metadata_to_verify
document_content_availability: processed_table_and_text_context
metadata_fields:
  - context_id
  - scale
  - answer_type
table_or_structured_data_fields:
  - table
  - derivation
existing_annotations:
  - answer_type
  - derivation
  - scale
unanswerable_or_ambiguous_policy: "Designed as answerable table-text QA."
expected_grounding_classes:
  - textual_evidence
  - aggregation
  - metadata
normalization_risks:
  - "Context is pre-selected, so it is weaker for testing retrieval over full documents."
  - "Still valuable for isolating table/text aggregation once evidence is in scope."
  - "Need inspect exact evidence/facts fields in current release."
pilot_value: "High as a clean aggregation/control dataset for table-text financial QA."
blocking_questions:
  - "Are original document names or report metadata available?"
  - "How much evidence supervision exists beyond derivation?"
  - "Should it be used as pilot data or as a control for class 4?"
sources:
  - https://github.com/NExTplusplus/TAT-QA
  - https://nextplusplus.github.io/TAT-QA/
  - https://aclanthology.org/2021.acl-long.254/
---

# דאטהסט: TAT-QA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2021.

הערכה למרכזיות בהערכות RAG רחבות: בינונית-גבוהה בתוך table-text QA ו-financial numerical reasoning. TAT-QA הוא אחד הדאטהסטים המוכרים למחקר על שילוב טבלה וטקסט, ולכן הוא benchmark חשוב למחלקת האגרגציה. הוא פחות מתאים כבנצ'מרק RAG מלא כי ההקשר כבר נבחר מראש, אבל הוא מרכזי כ-control ליכולת reasoning מעל מקורות מובנים.

הדאטהסט TAT-QA הוא benchmark קלאסי לשאלות על שילוב טבלאות וטקסט בדוחות פיננסיים. הוא פחות מתאים לבדיקת retrieval מלא מעל מאגר מסמכים, כי ההקשר כבר נבחר מראש, אבל הוא חשוב מאוד לבדיקת מחלקת האגרגציה: מתי מקור הקרקוע הוא טבלה, טקסט, או שניהם.

## מבנה המידע

### הקורפוס

הקורפוס מחולק ל-hybrid contexts מתוך דוחות פיננסיים, עם טבלה ופסקאות סביבתיות. זה אינו מסמך מלא, ולכן הוא צריך להיחשב control או dataset משני, לא מועמד יחיד לפיילוט.

### הדאטהסט

כל context כולל שאלות, תשובות, טבלה, פסקאות, ולעיתים derivation או answer type. עבור התזה, השימוש העיקרי הוא לבדוק האם המתייג מזהה שהתשובה דורשת מקור קרקוע מובנה ולא רק ראיה טקסטואלית.

### דגימות

לא נוספו דגימות מלאות כרגע. השלב הבא הוא למשוך 5 דוגמאות מה-JSON הרשמי ולבדוק איך `derivation`, `answer_type` ו-`table` מתפקדים כראיות.
