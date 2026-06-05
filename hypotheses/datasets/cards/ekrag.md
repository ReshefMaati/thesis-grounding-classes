---
dataset_id: ekrag
dataset_name: EKRAG
paper_or_description_url: https://aclanthology.org/2025.knowledgenlp-1.13/
dataset_download_url: to_verify
corpus_download_url: to_verify
license: to_verify
domain: enterprise_public_corporate_documents
document_source_type:
  - product_releases
  - corporate_technical_blogs
  - corporate_news_and_blogs
  - sec_reports
  - leadership_communications
corpus_scope: "Expert-curated enterprise-knowledge RAG benchmark over publicly available corporate documents in PDF, HTML, DOCX and TXT formats."
corpus_availability_status: availability_to_verify
pilot_priority: 2
dataset_fetch_steps:
  - "Locate official dataset release, if public."
  - "If no public release exists, use the paper as methodological reference rather than immediate pilot data."
corpus_fetch_steps:
  - "Verify whether the 5000 reference documents are distributed or only described."
  - "If distributed, inspect document ids, source urls, file formats and QA references."
data_format:
  - PDF
  - HTML
  - DOCX
  - TXT
  - QA_annotations_to_verify
splits:
  - to_verify
question_count: to_verify
document_count: "5000 reference documents reported in the paper"
record_fields:
  - question_to_verify
  - answer_to_verify
  - reference_documents_to_verify
  - evidence_to_verify
answer_fields:
  - answer_to_verify
evidence_fields:
  - reference_documents_to_verify
  - citations_to_verify
source_document_fields:
  - document_id_to_verify
  - url_to_verify
  - file_type_to_verify
  - document_category_to_verify
document_content_availability: to_verify
metadata_fields:
  - document_category
  - file_format
  - source_url
table_or_structured_data_fields:
  - financial_tables_in_sec_reports_to_verify
existing_annotations:
  - expert_curated_qa_to_verify
unanswerable_or_ambiguous_policy: "Unknown from current card; paper appears focused on factual enterprise QA."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
  - aggregation
normalization_risks:
  - "Public availability is not yet confirmed."
  - "Some leadership communications may be closer to public talks than source-of-truth operational documents."
  - "Corporate webpages and blogs need filtering against the stricter source-of-truth criterion."
pilot_value: "Very high conceptually, but blocked until dataset/corpus availability is verified."
blocking_questions:
  - "Is the actual EKRAG dataset downloadable?"
  - "Does each QA item expose source documents and evidence, or only final answers?"
  - "Which document categories satisfy the source-of-truth criterion after filtering?"
sources:
  - https://aclanthology.org/2025.knowledgenlp-1.13/
  - https://knowledge-nlp.github.io/naacl2025/papers/20.pdf
---

# דאטהסט: EKRAG

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2025.

הערכה למרכזיות בהערכות RAG רחבות: נמוכה-בינונית כרגע, עם פוטנציאל גבוה. EKRAG מכוון במפורש ל-Enterprise Knowledge RAG ולכן הוא קרוב מאוד למחקר שלנו מבחינת השאלה, אך הוא חדש ועדיין לא ברור עד כמה הדאטה זמין ועד כמה הוא אומץ בהערכות רחבות. אם יתברר שהקורפוס וה-QA זמינים, הוא יכול להפוך למועמד מרכזי מאוד.

הדאטהסט EKRAG הוא כנראה המועמד הרעיוני הכי קרוב לתזה מבחינת ניסוח הבעיה: benchmark ל-RAG מעל ידע ארגוני, עם מסמכים תאגידיים כמו product releases, technical blogs, SEC reports וקבצים בפורמטים משרדיים או מסמכיים. בניגוד להרבה דאטהסטים פיננסיים או מדעיים, כאן המוטיבציה עצמה היא Enterprise Knowledge QA.

עם זאת, כרגע הוא לא מועמד מיידי לפיילוט עד שנדע אם הדאטה עצמו זמין להורדה. אם הוא לא משוחרר בפועל, הוא עדיין חשוב מאוד כרפרנס בסקירת ספרות וכדוגמה לכך שהקהילה מתחילה לזהות את הפער, אבל לא כבסיס ניסויי ראשוני.

## מבנה המידע

### הקורפוס

הקורפוס מתואר במאמר כאוסף של כ-5,000 מסמכים תאגידיים ציבוריים. היתרון הוא ריבוי פורמטים שמזכיר סביבת ארגון אמיתית: PDF, HTML, DOCX ו-TXT. החיסרון הוא שהקטגוריות אינן כולן שוות מבחינת "מקור אמת": SEC reports ו-product releases חזקים מאוד; corporate blogs ו-leadership communications דורשים סינון זהיר.

### הדאטהסט

המאמר מתאר QA expert-curated על מסמכים תאגידיים, אך צריך לאמת אם יש קבצים זמינים, מה הסכימה, והאם קיימים מזהי מסמכים או ראיות. מבחינת התזה, השאלה החשובה היא האם כל רשומה מאפשרת לשחזר תוכנית פעולה: אילו מסמכים צריך למצוא, האם נדרש שימוש במטאדאטה, והאם השאלה בפועל נעה סביב ישות ארגונית כמו מוצר, גרסה, צוות או פעילות עסקית.

### דגימות

לא נוספו דגימות עד לאימות זמינות הדאטה. בשלב הבא צריך לחפש release רשמי או ליצור קשר עם המחברים. אם הדאטה זמין, זה יכול להיות אחד המועמדים הראשונים לבדיקה ידנית.
