---
dataset_id: techqa
dataset_name: TechQA
paper_or_description_url: https://research.ibm.com/publications/the-techqa-dataset
dataset_download_url: https://github.com/IBM/techqa
corpus_download_url: https://huggingface.co/datasets/PrimeQA/TechQA
license: Apache-2.0
domain: technical_support
document_source_type:
  - ibm_technotes
  - technical_support_documents
corpus_scope: "Actual technical forum questions whose accepted answers appear in IBM Technotes; companion corpus of roughly 801,998 Technotes."
corpus_availability_status: full_corpus_available
pilot_priority: 1
dataset_fetch_steps:
  - "Use IBM/techqa GitHub for code and instructions."
  - "Download TechQA.tar.gz from the PrimeQA/TechQA Hugging Face repository."
  - "Extract train/dev QA files."
corpus_fetch_steps:
  - "Download the same TechQA.tar.gz package."
  - "Extract training_dev_technotes.json and related Technote corpus files."
data_format:
  - JSON
  - tar.gz archive
splits:
  - train
  - dev
  - evaluation
question_count: "600 train, 310 dev, 490 evaluation"
document_count: "801998 Technotes companion corpus"
record_fields:
  - question
  - answer
  - source_technote_references
  - to_verify_exact_schema
answer_fields:
  - accepted_answer
  - answer_span_or_text_to_verify
evidence_fields:
  - technote_reference
  - passage_context_to_verify
source_document_fields:
  - technote_id
  - title
  - content
  - to_verify_exact_fields
document_content_availability: full_technote_corpus_available_as_processed_json
metadata_fields:
  - technote_id
  - title
  - product_or_topic_to_verify
table_or_structured_data_fields: []
existing_annotations:
  - accepted_answers_from_forums
  - technote_grounding
unanswerable_or_ambiguous_policy: "Dataset focuses on answerable questions with accepted answers in Technotes; evaluation details need schema inspection."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
normalization_risks:
  - "Need inspect exact JSON schema after extraction."
  - "The QA question source is forum data, but answer grounding is in Technotes; keep Technotes as source-of-truth."
  - "Corpus is large; pilot should sample and build lightweight lookup first."
pilot_value: "Very high. Strongest technical-support candidate for entity/product/version style grounding."
blocking_questions:
  - "Does each QA row include a stable Technote id or only answer text?"
  - "Can the Technote corpus be filtered by product/version metadata?"
  - "How much document metadata is available beyond title/content?"
sources:
  - https://research.ibm.com/publications/the-techqa-dataset
  - https://github.com/IBM/techqa
  - https://huggingface.co/datasets/PrimeQA/TechQA
---

# דאטהסט: TechQA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2020, עם גרסת arXiv מוקדמת מ-2019.

הערכה למרכזיות בהערכות RAG רחבות: בינונית. TechQA אינו אחד מהבנצ'מרקים הכלליים הנפוצים ביותר בעבודות RAG רוחביות, אבל הוא מוכר מאוד כנציג חשוב של QA טכני ותמיכתי מעל מסמכי Technotes. מבחינת התזה הוא בעל חשיבות גבוהה במיוחד, כי הוא קרוב לעולם שבו יש מסמכי מקור-אמת טכניים, ישויות מוצריות ותקלות שמבוטאות במסמכים.

הדאטהסט TechQA הוא מועמד חזק מאוד לפיילוט בגלל הקרבה שלו לעולם תמיכה טכנית ארגונית: שאלות אמיתיות מפורומים טכניים, ותשובות שמופיעות ב-IBM Technotes. מבחינת התזה, ה-Technotes הם החלק החשוב: אלה מסמכי ידע טכניים שנועדו לטפל בבעיה, מוצר, רכיב, תצורה או מגבלה ידועה.

האמינות המחקרית טובה: הדאטסט פורסם ב-ACL 2020, יש עמוד IBM Research, ויש repository רשמי של IBM עם קוד, הוראות ורישיון Apache-2.0. בנוסף, יש חבילת Hugging Face שמרכזת את הקבצים. יתרון מרכזי הוא קורפוס ה-Technotes הגדול, שמאפשר לבדוק ניווט בתוך מאגר ידע טכני ולא רק בתוך evidence מקומי.

הסיכון המרכזי הוא שצריך לבדוק את הסכימה בפועל אחרי הורדה. לפי התיעוד, יש train/dev ושימוש בקובץ `training_dev_technotes.json`, אבל לפני החלטת פיילוט צריך לוודא בדיוק איך שאלה מקושרת למסמך, האם יש IDs יציבים, ומה יש במטאדאטה של המסמכים.

מבחינת מחלקות הקרקוע, TechQA חשוב במיוחד למחלקת אונטולוגיה ארגונית: מוצרים, גרסאות, רכיבים, תקלות, known issues ותצורות עשויים להתנהג כישויות ארגוניות שמבוטאות במסמכי Technote. הוא כנראה פחות חזק לאגרגציה, ולכן כדאי לצמד אותו לדאטסט פיננסי/טבלאי.

## מבנה המידע

### הקורפוס

הקורפוס של TechQA הוא אוסף IBM Technotes גדול מאוד: כ-801,998 מסמכי Technote שהיו זמינים ברשת נכון ל-4 באפריל 2019. מבחינת התזה, זה אחד הקורפוסים המעניינים ביותר כי Technote הוא מסמך ידע טכני שמטרתו לטפל בבעיה, רכיב, מוצר, תצורה או תקלה. זה אינו צ'אט ואינו פורום; הפורום משמש כמקור לשאלה, אבל מקור האמת למענה הוא ה-Technote.

לפי התיעוד, הקורפוס נמצא בתוך הארכיון `TechQA.tar.gz`, בקובץ כמו `training_dev_technotes.json`. לפני שנשתמש בו בפיילוט צריך לחלץ את הארכיון ולוודא את הסכימה בפועל, אך השדות הצפויים הם לפחות:

- מזהה Technote או מזהה מסמך פנימי.
- כותרת Technote.
- תוכן המסמך.
- ייתכן שמטאדאטה של מוצר, גרסה או נושא קיימת, אך זה דורש בדיקת סכימה לאחר חילוץ.

איכות הקורפוס גבוהה מבחינת הרעיון המחקרי: מדובר במסמכי תמיכה טכנית שנועדו להיות מקור ידע. החסם המרכזי הוא מעשי: הקובץ הרשמי הוא ארכיון גדול מאוד, בערך 2.96GB, ולכן לא נכון להוריד ולחלץ אותו רק בשביל דגימה ידנית בלי שלב עבודה מסודר.

### הדאטהסט

הדאטהסט TechQA נבנה משאלות אמיתיות שנשאלו בפורומים טכניים של IBM Developer ו-DeveloperWorks. נבחרו שאלות שיש להן accepted answer, כאשר התשובה מופיעה במסמך IBM Technote. לכן המבנה הרעיוני הוא:

- שאלה טבעית ממשתמש.
- תשובה או answer span מתוך Technote.
- קישור או ייחוס למסמך Technote.
- קורפוס Technotes גדול המשמש כמקור הקרקוע.

השדות הצפויים בקובצי QA לפי ה-README:

- `training_Q_A.json`: קובץ train.
- `dev_Q_A.json`: קובץ dev.
- `training_dev_technotes.json`: קורפוס Technotes עבור train/dev.

הסכימה המדויקת של רשומות QA עדיין צריכה אימות אחרי חילוץ. זהו שלב קריטי לפני הפיילוט, כי צריך לדעת האם הקישור למסמך הוא מזהה יציב, טקסט תשובה בלבד, רשימת candidate documents, או מבנה אחר.

### דגימות מהדאטהסט

לא הוספתי כאן 5 דגימות מלאות עדיין. הסיבה אינה מהותית אלא טכנית: הדאטהסט הרשמי נמצא בארכיון יחיד בגודל של כ-2.96GB, והדגימות המלאות דורשות הורדה וחילוץ של `TechQA.tar.gz`.

כדי להשלים את החלק הזה בפיילוט צריך לבצע:

1. להוריד את `TechQA.tar.gz` מ-Hugging Face.
2. לחלץ את `training_Q_A.json`, `dev_Q_A.json`, ו-`training_dev_technotes.json`.
3. לבחור 5 רשומות מ-`dev_Q_A.json` או `training_Q_A.json`.
4. לכל רשומה, למפות את ה-Technote הרלוונטי מתוך `training_dev_technotes.json`.
5. לעדכן כאן דגימות מלאות בפורמט:
   - `question`
   - `answer` או `answer_span`
   - מזהה/כותרת Technote
   - תקציר תוכן Technote
   - שדות מטאדאטה זמינים
   - הערת קרקוע ראשונית

מבחינת תכנון הפיילוט, TechQA עדיין נשאר בעדיפות 1, אבל צריך להקצות לו שלב הכנה נפרד של הורדה, חילוץ ובדיקת סכימה לפני שמתחילים תיוג.
