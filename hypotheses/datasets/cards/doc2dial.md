---
dataset_id: doc2dial
dataset_name: Doc2Dial
paper_or_description_url: https://aclanthology.org/2020.emnlp-main.652/
dataset_download_url: https://doc2dial.github.io/data.html
corpus_download_url: https://doc2dial.github.io/data.html
license: CC-BY-3.0
domain: service_documents
document_source_type:
  - customer_care_documents
  - public_service_documents
  - procedural_documents
corpus_scope: "Goal-oriented document-grounded dialogues over more than 450 documents from four domains."
corpus_availability_status: full_corpus_available_to_verify
pilot_priority: 3
dataset_fetch_steps:
  - "Download Doc2Dial v1.0 from the official data page."
  - "Inspect document_domain, dialogue_domain and reading-comprehension files."
corpus_fetch_steps:
  - "Use document data with domain, title, content and span annotations."
  - "Map dialogue turns to grounding references."
data_format:
  - JSON
splits:
  - train_to_verify
  - validation_to_verify
  - test_to_verify
question_count: "Over 4500 dialogues; about 14 turns per dialogue"
document_count: "Over 450 documents from four domains"
record_fields:
  - dialogue_id
  - document_id
  - domain
  - turns
  - grounding_reference
answer_fields:
  - dialogue_turn_response
evidence_fields:
  - grounding_reference
  - span_id
  - span_content
source_document_fields:
  - document_id
  - domain
  - title
  - document_content
  - spans
document_content_availability: full_document_text_with_spans
metadata_fields:
  - domain
  - title
  - span_type
  - dialogue_act
table_or_structured_data_fields: []
existing_annotations:
  - grounding_spans
  - dialogue_acts
  - domain
unanswerable_or_ambiguous_policy: "Dialogue task may include clarification/conditional turns; not a pure single-turn QA dataset."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
normalization_risks:
  - "Dialogue history is an additional axis outside the current hypothesis."
  - "Some turns are not standalone questions."
  - "Still useful for document navigation and policy/procedure flows."
pilot_value: "Medium-high as a procedural document navigation benchmark, but not ideal as first QA-only dataset."
blocking_questions:
  - "Can we derive single-turn QA items cleanly from grounded dialogue turns?"
  - "Which domains satisfy the source-of-truth document criterion?"
  - "How stable are span ids across downloaded files?"
sources:
  - https://doc2dial.github.io/data.html
  - https://aclanthology.org/2020.emnlp-main.652/
  - https://arxiv.org/abs/2011.06623
---

# דאטהסט: Doc2Dial

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2020.

הערכה למרכזיות בהערכת RAG רחבה: בינונית בתחום document-grounded dialogue, ונמוכה-בינונית כ-QA/RAG כללי. Doc2Dial חשוב כי הוא עוסק בדיאלוגים שמקורקעים במסמכי שירות, אבל הוא מכניס ציר נוסף של שיחה, תורות ו-clarification. לכן הוא מועמד טוב להרחבה מאוחרת יותר, פחות לפיילוט ראשוני נקי.

הדאטהסט Doc2Dial הוא מועמד גבולי אבל חשוב: הוא לא QA חד-פעמי, אלא דיאלוגים מכווני מטרה שמקורקעים במסמכים. הוא רלוונטי כי המסמכים הם מסמכי שירות/נהלים, והדיאלוגים מראים כיצד משתמשים מנווטים במסמך כדי להשיג פתרון.

## מבנה המידע

### הקורפוס

הקורפוס כולל מסמכים עם domain, title, תוכן וספנים מסומנים. זה מאפשר לבדוק לא רק האם המודל מצא צ'אנק, אלא האם הוא הבין את הסעיף או התנאי הנכון בתוך מסמך פרוצדורלי.

### הדאטהסט

הדאטהסט כולל דיאלוגים, תורות, תפקידי דובר, dialog acts ו-grounding references. בשביל המחקר שלנו צריך להמיר בזהירות תורות מסוימות ליחידות QA, או להשתמש בו רק בשלב מאוחר יותר של סוכן שמייצר תוכנית פעולה.

### דגימות

לא נוספו דגימות מלאות בשלב זה. כדאי לדגום 5 turns שיש להם grounding span ברור ולבדוק אם הם עומדים בפני עצמם כשאלת QA.
