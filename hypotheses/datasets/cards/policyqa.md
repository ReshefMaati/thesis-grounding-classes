---
dataset_id: policyqa
dataset_name: PolicyQA
paper_or_description_url: https://arxiv.org/abs/2010.02557
dataset_download_url: https://github.com/wasiahmad/PolicyQA
corpus_download_url: https://github.com/wasiahmad/PolicyQA
license: MIT_to_verify_for_data
domain: privacy_policies
document_source_type:
  - website_privacy_policies
  - legal_policy_documents
corpus_scope: "Reading-comprehension examples over 115 website privacy policies, derived from the OPP-115 privacy policy corpus."
corpus_availability_status: full_processed_corpus_available_to_verify
pilot_priority: 2
dataset_fetch_steps:
  - "Clone https://github.com/wasiahmad/PolicyQA."
  - "Inspect files under data/."
  - "Verify whether data is SQuAD-style and whether full policy texts are included."
corpus_fetch_steps:
  - "Use distributed policy documents or passages under data/."
  - "Map examples back to policy ids and spans."
data_format:
  - JSON
  - SQuAD_style_to_verify
splits:
  - train_to_verify
  - dev_to_verify
  - test_to_verify
question_count: "714 questions, 25017 reading-comprehension examples"
document_count: "115 website privacy policies"
record_fields:
  - question_to_verify
  - context_to_verify
  - answer_to_verify
  - policy_id_to_verify
answer_fields:
  - answer_span_to_verify
evidence_fields:
  - context
  - answer_span
source_document_fields:
  - policy_id
  - policy_text_to_verify
document_content_availability: full_or_passage_policy_text_to_verify
metadata_fields:
  - policy_id
  - question_category_to_verify
table_or_structured_data_fields: []
existing_annotations:
  - answer_spans
  - privacy_practice_categories_to_verify
unanswerable_or_ambiguous_policy: "Reading-comprehension style; verify whether no-answer examples exist."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
normalization_risks:
  - "Policies are source-of-truth legal documents, but not internal organizational operational docs."
  - "May be heavily span-based and therefore overrepresent local textual evidence."
  - "License and upstream OPP-115 terms should be checked before use."
pilot_value: "Strong policy-document candidate for source-of-truth long text and controlled legal/organizational terminology."
blocking_questions:
  - "Does the repo include complete policy documents or only passages?"
  - "Are question categories available and useful for grounding-class analysis?"
  - "What are the upstream data-use terms from OPP-115?"
sources:
  - https://github.com/wasiahmad/PolicyQA
  - https://arxiv.org/abs/2010.02557
  - https://wasiahmad.github.io/files/publications/2020/policyqa.pdf
---

# דאטהסט: PolicyQA

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2020.

הערכה למרכזיות בהערכות RAG רחבות: נמוכה-בינונית. PolicyQA מוכר בתחום QA על privacy policies ומסמכי מדיניות, אבל אינו benchmark מרכזי ברוב הערכות RAG הרחבות. מבחינת התזה הוא חשוב כ-control למסמכי מדיניות שהם מקור אמת, בעיקר כדי לבדוק שאלות ראייתיות ומטאדאטה במסמכים ארוכים יחסית.

הדאטהסט PolicyQA הוא מועמד טוב למשפחת מסמכי מדיניות ונהלים. מדיניות פרטיות היא מקור אמת משפטי/ארגוני של אתר או שירות, ולכן היא מתאימה יותר לתזה מאשר טקסט ויקיפדי או דיאלוג כללי. מצד שני, הוא כנראה יהיה מוטה לשאלות ראייתיות מקומיות, ולכן הערך שלו הוא בעיקר כ-control למסמכי מדיניות ארוכים.

## מבנה המידע

### הקורפוס

הקורפוס מבוסס על 115 privacy policies של אתרים, כנראה דרך OPP-115. אלה מסמכים ארוכים, פורמליים, עם סעיפים ותתי סעיפים. הם מתאימים לבדיקה של שימוש במטאדאטה, סעיף, קטגוריית privacy practice, והבחנה בין תוכן המדיניות לבין מקור המסמך.

### הדאטהסט

הדאטהסט כולל 25,017 דוגמאות reading-comprehension סביב 714 שאלות. צריך לבדוק את הסכימה המדויקת בקבצי `data/`, אבל הציפייה היא למבנה בסגנון שאלה, context, ותשובת span.

### דגימות

לא נוספו דגימות מלאות בשלב זה. כדאי למשוך 5 דוגמאות מתוך split קטן ולבדוק האם ניתן למפות כל דוגמה למדיניות מלאה, לא רק לפסקה.
