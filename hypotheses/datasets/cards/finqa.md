---
dataset_id: finqa
dataset_name: FinQA
paper_or_description_url: https://arxiv.org/abs/2109.00122
dataset_download_url: https://github.com/czyssrs/FinQA
corpus_download_url: https://github.com/czyssrs/FinQA/tree/main/dataset
license: MIT
domain: financial_reports
document_source_type:
  - earnings_reports
  - financial_report_tables
  - financial_report_text
corpus_scope: "2.8k financial reports represented as table/text contexts for about 8k QA pairs."
corpus_availability_status: partial_corpus_available
pilot_priority: 2
dataset_fetch_steps:
  - "Clone https://github.com/czyssrs/FinQA."
  - "Use files under dataset/ such as train/dev/test JSON files."
corpus_fetch_steps:
  - "Use per-record pre_text, post_text and table fields in dataset JSON."
  - "Original full PDFs are not the primary available corpus in the repository; verify if report names can be traced externally."
data_format:
  - JSON
splits:
  - train
  - dev
  - test
  - private_test
question_count: "About 8k QA pairs"
document_count: "About 2.8k financial reports represented by extracted table/text contexts"
record_fields:
  - pre_text
  - post_text
  - table
  - id
  - qa
answer_fields:
  - qa.exe_ans
  - qa.program
  - qa.program_re
evidence_fields:
  - qa.gold_inds
source_document_fields:
  - id
  - report_name_embedded_in_id
document_content_availability: extracted_context_only
metadata_fields:
  - id
  - report_name_from_id
table_or_structured_data_fields:
  - table
  - qa.program
  - qa.program_re
existing_annotations:
  - gold_supporting_facts
  - reasoning_program
  - execution_answer
unanswerable_or_ambiguous_policy: "Private test has question only; public train/dev/test include references. No unanswerable focus."
expected_grounding_classes:
  - textual_evidence
  - aggregation
  - metadata
normalization_risks:
  - "Context is extracted around table/text, not necessarily the full report."
  - "Strong computation axis may dominate over source-grounding classification."
  - "Need map gold_inds to text/table facts carefully."
pilot_value: "High for aggregation and reasoning-program supervision; less strong for organizational ontology."
blocking_questions:
  - "Can we recover enough document-level metadata from id/report name?"
  - "Should FinQA be treated as source-grounding pilot or primarily aggregation/control?"
  - "How to separate grounding-source aggregation from computation program?"
sources:
  - https://finqasite.github.io/index.html
  - https://github.com/czyssrs/FinQA
  - https://arxiv.org/abs/2109.00122
---

# דאטהסט: FinQA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2021.

הערכה למרכזיות בהערכות RAG רחבות: בינונית. FinQA הוא benchmark מרכזי יחסית בתחום financial QA ו-numerical reasoning מעל טקסט וטבלאות, אבל פחות משמש כבנצ'מרק RAG כללי משום שההקשר לרוב כבר מעובד ומצומצם. מבחינת התזה הוא חשוב כבסיס למחלקת האגרגציה ולבחינת ההפרדה בין מקור הקרקוע לבין החישוב עליו.

הדאטהסט FinQA הוא דאטסט פיננסי קלאסי לאגרגציה וחישוב על דוחות. הוא מכיל שאלות שנכתבו על ידי מומחים פיננסיים, יחד עם הקשר טקסטואלי וטבלאי, supporting facts ותוכנית חישוב. מבחינת התזה, זה מועמד חזק מאוד למחלקה 4: לא מספיק למצוא קטע; צריך לאסוף ערכים ולהפעיל reasoning program.

האמינות המחקרית גבוהה: יש אתר רשמי, מאמר EMNLP 2021 ו-GitHub עם קוד ודאטה תחת MIT. התיעוד של ה-repository מציג את מבנה הרשומה: `pre_text`, `post_text`, `table`, `id`, ו-`qa` עם שאלה, תוכנית, supporting facts ותוצאת execution.

החיסרון המרכזי הוא שהקורפוס אינו בהכרח מסמכי הדוח המלאים, אלא הקשר מחולץ סביב טבלאות וטקסט. לכן הוא פחות טוב לשאלה “איך מביאים את כל מסמכי המקור”, אבל מצוין לשאלה “האם מחלקת אגרגציה על מידע מובנה קיימת ויציבה”.

בפיילוט, FinQA מתאים אם נרצה מהר מאוד לבדוק את הצד האגרגטיבי של הטקסונומיה. הוא כנראה לא מספיק לבדו, כי הוא לא מדמה היטב ניווט בישויות ארגוניות חבויות; לכן כדאי לצמד אותו ל-WixQA או TechQA.
