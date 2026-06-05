---
dataset_id: qasper
dataset_name: QASPER
paper_or_description_url: https://allenai.org/data/qasper
dataset_download_url: https://huggingface.co/datasets/allenai/qasper
corpus_download_url: https://huggingface.co/datasets/allenai/qasper
license: CC-BY-4.0
domain: scientific_papers
document_source_type:
  - scientific_papers
  - academic_articles
corpus_scope: "Question answering over full NLP research papers with supporting evidence annotations."
corpus_availability_status: full_corpus_available
pilot_priority: 3
dataset_fetch_steps:
  - "load_dataset('allenai/qasper')"
  - "Inspect train/validation/test splits and nested QA schema."
corpus_fetch_steps:
  - "Use full paper fields in the Hugging Face dataset."
  - "Map each QA to paper id and evidence paragraphs."
data_format:
  - HuggingFace dataset
  - JSON
splits:
  - train
  - validation
  - test
question_count: 5049
document_count: 1585
record_fields:
  - id
  - title
  - abstract
  - full_text
  - qas
answer_fields:
  - answer
  - yes_no
  - unanswerable
  - free_form_answer
  - extractive_spans
evidence_fields:
  - evidence
source_document_fields:
  - id
  - title
  - abstract
  - full_text
document_content_availability: full_paper_text_available
metadata_fields:
  - title
  - abstract
  - section_name
table_or_structured_data_fields:
  - tables_figures_not_primary
existing_annotations:
  - supporting_evidence
  - answer_type
  - unanswerable
unanswerable_or_ambiguous_policy: "Includes unanswerable questions; must filter or mark separately for our current assumptions."
expected_grounding_classes:
  - textual_evidence
  - metadata
normalization_risks:
  - "Scientific papers are not enterprise documents."
  - "Useful as long-document control, but weak for organizational ontology."
  - "Unanswerable examples must be filtered for hypothesis 1."
pilot_value: "Good control dataset for long-document QA and evidence selection, not a core enterprise proxy."
blocking_questions:
  - "Should unanswerable rows be excluded completely or tracked as out-of-scope?"
  - "How often do answers require figures/tables rather than text?"
  - "Does section metadata count as metadata grounding?"
sources:
  - https://huggingface.co/datasets/allenai/qasper
  - https://allenai.org/data/qasper
  - https://arxiv.org/abs/2105.03011
---

# דאטהסט: QASPER

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2021.

הערכה למרכזיות בהערכות RAG רחבות: בינונית-גבוהה כ-long-document QA/evidence benchmark, אך נמוכה יותר כמועמד Enterprise RAG. QASPER מופיע הרבה בהקשרים של QA על מסמכים ארוכים ומאמרים מדעיים, ולכן הוא טוב כבקרה. הוא פחות מייצג ארגון, ישויות ארגוניות או מסמכי מקור-אמת תפעוליים.

הדאטהסט QASPER הוא לא דאטהסט ארגוני, אבל הוא מועמד בקרה טוב מאוד: שאלות על מאמרים מדעיים מלאים, עם evidence ותשובות מסוגים שונים. הוא יכול לעזור להפריד בין "בעיה של מסמך ארוך" לבין "בעיה של ישויות ארגוניות".

## מבנה המידע

### הקורפוס

הקורפוס כולל 1,585 מאמרי NLP, עם כותרת, תקציר וטקסט מלא. זהו קורפוס מסמכי מקור-אמת במובן אקדמי: המאמר עצמו הוא המקור הסמכותי לתוכן שנשאל עליו.

### הדאטהסט

הדאטהסט כולל 5,049 שאלות שנכתבו על בסיס כותרת ותקציר, ונענו על ידי קוראים שקראו את המאמר המלא וסיפקו ראיות. יש בו תשובות extractive, abstractive, yes/no וגם unanswerable. לכן צריך לסנן או לסמן unanswerable לפני שימוש בהיפותזה 1.

### דגימות

לא נוספו דגימות מלאות בשלב זה. שלב הדגימה צריך לבחור 5 שאלות answerable בלבד, עם evidence טקסטואלי ולא figure/table.
