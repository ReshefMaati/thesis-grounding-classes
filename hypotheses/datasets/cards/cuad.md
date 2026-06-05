---
dataset_id: cuad
dataset_name: CUAD
paper_or_description_url: https://arxiv.org/abs/2103.06268
dataset_download_url: https://www.atticusprojectai.org/cuad/
corpus_download_url: https://github.com/TheAtticusProject/cuad
license: CC-BY-4.0
domain: legal_contracts
document_source_type:
  - commercial_contracts
  - legal_documents
corpus_scope: "510 commercial legal contracts with 13000+ expert labels across 41 clause types."
corpus_availability_status: full_corpus_available
pilot_priority: 3
dataset_fetch_steps:
  - "Use The Atticus Project CUAD page."
  - "Download from GitHub or Hugging Face links listed on the official page."
  - "Optionally use CUAD Q&A variant from Hugging Face if available."
corpus_fetch_steps:
  - "Clone/download TheAtticusProject/cuad repository."
  - "Use contract text files and annotation files from CUAD_v1."
data_format:
  - JSON
  - text_contracts
  - HuggingFace_dataset_to_verify
splits:
  - train
  - test
  - to_verify
question_count: "CUAD is primarily clause extraction; CUAD Q&A variant exists but exact QA count needs verification"
document_count: 510
record_fields:
  - contract_text
  - clause_type
  - annotated_spans
  - qa_fields_to_verify
answer_fields:
  - annotated_clause_span
  - yes_no_or_span_in_qa_variant_to_verify
evidence_fields:
  - expert_labeled_clause_spans
source_document_fields:
  - contract_id
  - contract_name
  - contract_text
document_content_availability: full_contract_text_available
metadata_fields:
  - contract_name
  - document_category_to_verify
  - clause_type
table_or_structured_data_fields:
  - clause_type_taxonomy
existing_annotations:
  - 41_clause_types
  - expert_labeled_spans
  - legal_review_annotations
unanswerable_or_ambiguous_policy: "Not primarily QA; negative/no-answer behavior depends on converted QA formulation."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
normalization_risks:
  - "Task is contract clause extraction/review, not natural QA by default."
  - "Need decide whether to use original CUAD or CUAD Q&A variant."
  - "Legal clause labels may create artificial ontology rather than hidden organizational ontology."
pilot_value: "Medium-high as legal source-of-truth corpus; better as boundary/control than first core pilot."
blocking_questions:
  - "Which version should be used: original CUAD or CUAD Q&A?"
  - "Can QA rows be reconstructed without distorting the task?"
  - "Do legal clause types help or distract from organizational ontology?"
sources:
  - https://www.atticusprojectai.org/cuad/
  - https://github.com/TheAtticusProject/cuad
  - https://huggingface.co/datasets/theatticusproject/cuad
  - https://arxiv.org/abs/2103.06268
---

# דאטהסט: CUAD

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2021.

הערכה למרכזיות בהערכות RAG רחבות: בינונית כמשאב משפטי, ונמוכה-בינונית כ-benchmark RAG כללי. CUAD מרכזי מאוד בתחום contract review ו-legal document understanding, אך הוא אינו QA/RAG קלאסי אלא בעיקר clause extraction. עבור המחקר שלנו הוא מתאים יותר כ-control או כמועמד גבול למסמכי מקור-אמת משפטיים.

הדאטהסט CUAD הוא דאטסט חוזים משפטיים: 510 חוזים מסחריים, יותר מ-13,000 תוויות מומחה, ו-41 סוגי סעיפים רלוונטיים לסקירת חוזים. מבחינת “מסמכי אמת”, זה מועמד חזק מאוד: חוזה הוא מקור סמכותי, סגור, בעל מבנה, ובעל ישויות ויחסים משפטיים.

האמינות שלו גבוהה: הדאטסט מתוחזק על ידי The Atticus Project, התקבל ב-NeurIPS Datasets and Benchmarks, והרישיון הרשמי הוא CC BY 4.0. יש גם GitHub וגם Hugging Face. זה הופך אותו לריאלי יחסית להבאה ולנרמול.

הסיכון הוא שהוא לא נולד כ-QA טבעי. המשימה המרכזית היא זיהוי סעיפים וסוגי סעיפים בחוזים, ולא שאלה חופשית של משתמש. לכן CUAD מתאים פחות לפתיחת הפיילוט אם אנחנו רוצים לבדוק “איך אדם עונה על שאלה” בצורה טבעית. מצד שני, הוא מצוין כמקרה גבול: האם מחלקות הקרקוע שלנו יודעות לעבוד גם מול מסמכי אמת משפטיים שבהם האונטולוגיה חלקית מוגדרת מראש דרך clause taxonomy.

בפיילוט, הייתי שם את CUAD אחרי WixQA, TechQA ואחד הדאטסטים הפיננסיים. הוא יכול לעזור לבדוק אונטולוגיה, מטאדאטה וראיות במסמכי מקור חזקים מאוד, אבל צריך להיזהר שלא להפוך את המחקר ל-clause extraction.
