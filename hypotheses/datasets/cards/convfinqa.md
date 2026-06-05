---
dataset_id: convfinqa
dataset_name: ConvFinQA
paper_or_description_url: https://arxiv.org/abs/2210.03849
dataset_download_url: https://github.com/czyssrs/ConvFinQA
corpus_download_url: https://github.com/czyssrs/ConvFinQA
license: MIT
domain: financial_reports
document_source_type:
  - financial_reports
  - financial_tables
  - conversational_finance_qa
corpus_scope: "Conversational numerical QA over financial report text and tables, released in conversation-level and turn-level formats."
corpus_availability_status: full_processed_context_available
pilot_priority: 2
dataset_fetch_steps:
  - "Clone https://github.com/czyssrs/ConvFinQA."
  - "Download/use data.zip."
  - "Inspect both conversation-level and turn-level files."
corpus_fetch_steps:
  - "Use per-record pre_text, post_text and table fields."
  - "Verify whether original report or page identifiers are exposed."
data_format:
  - JSON
  - ZIP
splits:
  - train
  - dev
  - test
question_count: "3037 train conversations, 421 dev conversations, 434 test conversations; turn-level 11104/1490/1521"
document_count: "Financial report contexts inherited from FinQA-style examples; exact unique reports to verify"
record_fields:
  - pre_text
  - post_text
  - table
  - id
  - annotation
  - qa
answer_fields:
  - exe_ans_list
  - qa
  - exe_ans
evidence_fields:
  - gold_ind
  - turn_program
  - original_program
source_document_fields:
  - id
  - pre_text
  - post_text
  - table
document_content_availability: processed_table_and_text_context
metadata_fields:
  - id
  - turn_ind
  - cur_type
table_or_structured_data_fields:
  - table
  - turn_program
  - cur_program
existing_annotations:
  - reasoning_programs
  - dialogue_break
  - execution_answers
  - supporting_facts
unanswerable_or_ambiguous_policy: "Designed as answerable numerical reasoning conversations."
expected_grounding_classes:
  - textual_evidence
  - aggregation
  - metadata
normalization_risks:
  - "Conversational context adds a dialogue-history axis that is orthogonal to grounding sources."
  - "Like FinQA, source context may be pre-selected rather than full-document."
  - "Need decide whether to use conversation-level or turn-level rows."
pilot_value: "High as an extension of FinQA for sequential action plans and repeated grounding steps."
blocking_questions:
  - "Should this be used for hypothesis 1 labeling or later for agentic step decomposition?"
  - "Can original document metadata be recovered from ids?"
  - "How do gold_ind fields map to text/table evidence?"
sources:
  - https://github.com/czyssrs/ConvFinQA
  - https://arxiv.org/abs/2210.03849
---

# דאטהסט: ConvFinQA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2022.

הערכה למרכזיות בהערכות RAG רחבות: בינונית בתוך financial conversational QA, ונמוכה יותר כבנצ'מרק RAG כללי. ConvFinQA חשוב כי הוא מוסיף רצף שאלות ופעולות מעל דוחות פיננסיים, ולכן מתאים לחשיבה על agentic decomposition. הוא פחות נקי למחקר על מקור קרקוע בלבד בגלל ציר השיחה.

הדאטהסט ConvFinQA מוסיף ל-FinQA ממד חשוב: שאלות המשך ושרשרת שיחה. זה לא בהכרח מדמה QA ארגוני קלאסי, אבל הוא כן מדמה תהליך שבו אדם מפרק בעיה פיננסית לכמה צעדים. לכן הוא יכול להיות שימושי במיוחד כאשר נתחיל לפתח את הסוכן שמייצר "תוכנית פעולה".

## מבנה המידע

### הקורפוס

הקורפוס בכל רשומה כולל טקסט לפני טבלה, טבלה, וטקסט אחרי טבלה. כלומר, זהו מקור קרקוע מעובד ולא מסמך מלא. הערך שלו הוא לא ב-retrieval רחב, אלא בהבנת המעבר בין שאלה, טבלה, תוכנית חישוב ותשובה.

### הדאטהסט

יש שתי רמות: conversation-level ו-turn-level. ברמת השיחה יש 3,037 דוגמאות train, 421 dev ו-434 test. ברמת התור יש 11,104 train, 1,490 dev ו-1,521 test. השדות כוללים `pre_text`, `post_text`, `table`, `annotation`, `dialogue_break`, `turn_program`, `exe_ans_list`, ובגרסת turn גם `cur_program`, `cur_dial`, `gold_ind` ו-`turn_ind`.

### דגימות

לא נוספו דגימות מלאות בשלב זה. כשנגיע אליו, כדאי לבחור 5 דוגמאות turn-level משום שהן קרובות יותר לצעד יחיד בתוכנית פעולה.
