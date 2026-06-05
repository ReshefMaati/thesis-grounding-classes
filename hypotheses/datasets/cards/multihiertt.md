---
dataset_id: multihiertt
dataset_name: MultiHiertt
paper_or_description_url: https://arxiv.org/abs/2206.01347
dataset_download_url: https://github.com/psunlpgroup/MultiHiertt
corpus_download_url: https://github.com/psunlpgroup/MultiHiertt
license: MIT
domain: financial_reports
document_source_type:
  - financial_reports
  - hierarchical_tables
  - report_text
corpus_scope: "Financial report documents represented with paragraphs, multiple HTML tables, table descriptions, QA, reasoning programs and gold evidence."
corpus_availability_status: full_corpus_available
pilot_priority: 1
dataset_fetch_steps:
  - "Clone https://github.com/psunlpgroup/MultiHiertt."
  - "Download JSON dataset from the Google Drive link in the repository README."
  - "Place files under dataset/ as expected by the repository."
corpus_fetch_steps:
  - "Use the downloaded JSON files; each entry contains paragraphs and HTML tables."
  - "Original PDFs are not required for the first pilot unless we want to test document parsing."
data_format:
  - JSON
  - HTML tables embedded in JSON
splits:
  - train
  - dev
  - test
question_count: "10440 QA pairs reported in secondary summaries; verify exact split counts after download"
document_count: "2513 financial reports reported in secondary summaries; verify after download"
record_fields:
  - uid
  - paragraphs
  - tables
  - table_description
  - qa
answer_fields:
  - qa.answer
  - qa.program
evidence_fields:
  - qa.text_evidence
  - qa.table_evidence
source_document_fields:
  - uid
  - paragraphs
  - tables
document_content_availability: processed_document_paragraphs_and_html_tables
metadata_fields:
  - uid
  - table_description
table_or_structured_data_fields:
  - tables
  - table_description
  - qa.program
existing_annotations:
  - reasoning_program
  - text_evidence
  - table_evidence
  - table_descriptions
unanswerable_or_ambiguous_policy: "No explicit unanswerable focus observed; verify after dataset download."
expected_grounding_classes:
  - textual_evidence
  - aggregation
  - metadata
normalization_risks:
  - "Requires downloading dataset from Google Drive link, not directly stored in GitHub."
  - "HTML table normalization can be nontrivial."
  - "Strong arithmetic/reasoning axis may need separation from grounding-source labels."
pilot_value: "Very high for aggregation stress-test over multiple hierarchical tables and report text."
blocking_questions:
  - "Is the Google Drive download still accessible?"
  - "Are original report identities/metadata available beyond uid?"
  - "How many examples require multiple tables versus one table?"
sources:
  - https://arxiv.org/abs/2206.01347
  - https://github.com/psunlpgroup/MultiHiertt
  - https://huggingface.co/datasets/yilunzhao/MultiHiertt
---

# דאטהסט: MultiHiertt

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2022.

הערכה למרכזיות בהערכות RAG רחבות: בינונית-גבוהה בתוך משפחת table-text QA ו-numerical reasoning, ונמוכה יותר כבנצ'מרק RAG כללי. MultiHiertt מוכר כדאטהסט חזק לשאלות פיננסיות מעל טבלאות היררכיות וטקסט, ולכן הוא חשוב במיוחד למחלקת האגרגציה. הוא פחות מרכזי בעבודות RAG כלליות שמודדות בעיקר retrieval טקסטואלי, אבל חיוני אם רוצים לבדוק גבול בין קרקוע לבין חישוב.

הדאטהסט MultiHiertt הוא מועמד חזק מאוד לצד האגרגציה של הפיילוט. הוא בנוי על דוחות פיננסיים, אבל בניגוד לדאטסטים פשוטים יותר הוא מדגיש ריבוי טבלאות, טבלאות היררכיות, טקסט ארוך יותר ותוכניות reasoning. לכן הוא מתאים לבדוק האם מחלקת “אגרגציה על מידע מובנה” מוגדרת מספיק טוב גם במקרים שאינם רק חישוב נקודתי.

האמינות המחקרית טובה: מאמר ACL 2022, GitHub רשמי, רישיון MIT, ותיאור סכימה מפורט. לפי ה-README, כל רשומה כוללת `paragraphs`, `tables`, `table_description`, ו-`qa` עם שאלה, תשובה, תוכנית, evidence טקסטואלי ו-evidence טבלאי. זה נותן הרבה מאוד מידע לשחזור תוכנית פעולה.

החיסרון המרכזי הוא טכני: הדאטסט עצמו נמצא בקישור Google Drive מתוך ה-repository, ולכן צריך לוודא שההורדה עדיין זמינה. בנוסף, נרמול טבלאות HTML יכול להפוך לעבודה משמעותית. מצד שני, בשביל פיילוט קטן אפשר להתחיל מהפורמט המעובד כפי שהוא ולא לחזור ל-PDF.

ביחס לתזה, MultiHiertt כנראה פחות חזק לאונטולוגיה ארגונית במובן של מוצרים/גרסאות/תהליכים, אבל מצוין לבדוק מחלקה 4 ולנסח גבול נקי בין “מקור קרקוע אגרגטיבי” לבין “חישוב על המקור”.

## מבנה המידע

### הקורפוס

ב-MultiHiertt הקורפוס אינו נפרד לגמרי משורות ה-QA, אלא מיוצג בתוך כל רשומה. כל דוגמה כוללת פסקאות טקסט מתוך דוחות פיננסיים, כמה טבלאות HTML, ולעיתים גם תיאורי טבלה. זה הופך אותו למועמד מצוין לבדיקת מחלקת האגרגציה, כי מקור הקרקוע אינו רק קטע טקסט אלא שילוב של טקסט, טבלאות, תא טבלאי, ולעיתים חישוב.

השדות המרכזיים של הקורפוס בתוך רשומה:

- `paragraphs`: רשימת פסקאות מתוך הדוח. חלק מהפסקאות הן placeholders כגון `## Table 0 ##` שמסמנות מיקום טבלה.
- `tables`: רשימת טבלאות בפורמט HTML.
- `table_description`: מיפוי מתאי טבלה או מיקומים טבלאיים לתיאור טקסטואלי.
- `uid`: מזהה רשומה.

איכות הקורפוס טובה לצורך פיילוט מחקרי כי הוא כבר מנורמל לפורמט מכונה, אך זה גם סיכון: אנחנו לא בודקים כאן ingestion אמיתי מ-PDF אלא את שלב הקרקוע אחרי שהדוח כבר פורק לפסקאות וטבלאות. לכן כדאי להתייחס אליו כאל פיילוט למחלקת מקור הקרקוע, לא כפיילוט לנרמול מסמכים.

### הדאטהסט

רשומת QA ב-MultiHiertt כוללת אובייקט `qa` עם שדות שמאפשרים לשחזר תוכנית פעולה:

- `qa.question`: השאלה.
- `qa.answer`: התשובה.
- `qa.question_type`: סוג השאלה, למשל `span_selection` או `arithmetic`.
- `qa.program`: תוכנית חישוב כאשר השאלה דורשת reasoning מספרי.
- `qa.text_evidence`: אינדקסים לפסקאות הרלוונטיות.
- `qa.table_evidence`: מזהים של תאי טבלה או מיקומים טבלאיים רלוונטיים.

מבחינת התזה, זה מאפשר להפריד בין שני דברים: מקור הקרקוע הנדרש, למשל טבלה או פסקה, לבין פעולת החישוב שנעשית מעל המקור. ההפרדה הזו חשובה במיוחד כי המחקר שלנו לא מנסה לפתור את כל reasoning chain, אלא לסווג את סוגי מקורות הקרקוע הדרושים.

### דגימות מהדאטהסט

הדגימות הבאות נלקחו מתוך `multihiertt_data/dev.json` ב-Hugging Face. כדי לשמור על קריאות באובסידיאן, כל דגימה כוללת את כל שדות ה-QA, מזהי הראיות, וסיכום קצר של הקורפוס הרלוונטי במקום הדבקה מלאה של כל הטבלאות הארוכות.

#### דגימה 1

- `uid`: `7d840731012a4a09a735eeee286c364b`
- מספר פסקאות (`paragraphs_count`): 68
- מספר טבלאות (`tables_count`): 4
- שאלה (`question`): Which year is Total Revenues of Group retirement products the most?
- תשובה (`answer`): 2006
- `question_type`: `span_selection`
- `program`: ריק
- `text_evidence`: `0`
- `table_evidence`: `0-2-4`, `0-8-4`, `0-14-4`
- תקציר ראיה טקסטואלית: פתיחה של דיון ניהולי ב-American International Group על Domestic Retirement Services.
- תקציר טבלה: טבלת תוצאות לפי שנים עבור Group retirement products, Individual fixed annuities, Individual variable annuities ועוד.

#### דגימה 2

- `uid`: `63260a43bc4e4632a0317eb820caf964`
- מספר פסקאות (`paragraphs_count`): 74
- מספר טבלאות (`tables_count`): 4
- שאלה (`question`): What will Distribution fees reach in 2010 if it continues to grow at its current rate? (in millions)
- תשובה (`answer`): 1570.75785
- `question_type`: `arithmetic`
- `program`: `subtract(1733,1912), divide(#0,1912), add(const_1,#1), multiply(#2,1733)`
- `text_evidence`: `32`
- `table_evidence`: `2-5-1`, `2-5-2`
- תקציר ראיה טקסטואלית: משפט שמציג את תוצאות הפעילות של Advice & Wealth Management segment.
- הערת קרקוע: זו דוגמה טובה להפרדה בין מקור קרקוע טבלאי לבין חישוב אקסטרפולציה מעל הערכים.

#### דגימה 3

- `uid`: `7f9cd61fc4264c9bb81cdcfd2c5c4c38`
- מספר פסקאות (`paragraphs_count`): 78
- מספר טבלאות (`tables_count`): 4
- שאלה (`question`): What was the total amount of Amount in 2007 for Financial Services Businesses ? (in million)
- תשובה (`answer`): 8228
- `question_type`: `span_selection`
- `program`: ריק
- `text_evidence`: `62`
- `table_evidence`: `2-15-2`
- תקציר ראיה טקסטואלית: פסקה שמציגה טבלאות על income yield ו-investment income עבור קטגוריות השקעה.
- הערת קרקוע: השאלה נראית פשוטה, אבל הקרקוע בפועל הוא תא טבלאי בתוך הקשר פיננסי רחב.

#### דגימה 4

- `uid`: `b7642f569ac54d28af0a4a16683d3f35`
- מספר פסקאות (`paragraphs_count`): 57
- מספר טבלאות (`tables_count`): 4
- שאלה (`question`): Does the average value of Power purchase agreements in Entergy Arkansas greater than that in Entergy Louisiana?
- תשובה (`answer`): yes
- `question_type`: `span_selection`
- `program`: ריק
- `text_evidence`: `20`
- `table_evidence`: `1-5-1`, `1-5-3`
- תקציר ראיה טקסטואלית: פסקה שמציגה רכיבים של accumulated deferred income taxes and taxes accrued עבור Registrant Subsidiaries.
- הערת קרקוע: זו דוגמה שבה השאלה מנוסחת כהשוואה בין ישויות/יחידות, אך מקור הקרקוע המיידי הוא ערכים בטבלה.

#### דגימה 5

- `uid`: `5cc19228085048228131f5d77196655d`
- מספר פסקאות (`paragraphs_count`): 131
- מספר טבלאות (`tables_count`): 4
- שאלה (`question`): What is the ratio of Securities to the total for Net realized losses reclassified into earnings in 2008?
- תשובה (`answer`): 0.66977
- `question_type`: `arithmetic`
- `program`: `divide(1797,2683)`
- `text_evidence`: `86`, `88`
- `table_evidence`: `2-3-1`, `2-3-5`
- תקציר ראיה טקסטואלית: פסקאות על changes in accumulated OCI ועל reclassification of net realized losses into earnings.
- הערת קרקוע: דוגמה חזקה למחלקת אגרגציה/חישוב על מידע מובנה, עם ראיות גם מהטקסט וגם מהטבלה.
