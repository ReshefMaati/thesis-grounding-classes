---
dataset_id: financebench
dataset_name: FinanceBench
paper_or_description_url: https://arxiv.org/abs/2311.11944
dataset_download_url: https://huggingface.co/datasets/PatronusAI/financebench
corpus_download_url: https://github.com/patronus-ai/financebench/tree/main/pdfs
license: to_verify
domain: financial_reports
document_source_type:
  - sec_filings
  - earnings_reports
  - financial_disclosures
corpus_scope: "Open-source subset of FinanceBench over financial filings, with PDFs available in the GitHub repository; full benchmark is restricted/licensed."
corpus_availability_status: partial_corpus_available
pilot_priority: 2
dataset_fetch_steps:
  - "Use Hugging Face PatronusAI/financebench for the dataset card/files."
  - "Or clone/download patronus-ai/financebench from GitHub."
  - "Use data/financebench_open_source.jsonl for the open-source subset."
corpus_fetch_steps:
  - "Download PDFs from https://github.com/patronus-ai/financebench/tree/main/pdfs."
  - "For full benchmark, contact Patronus AI."
data_format:
  - JSONL
  - PDF
splits:
  - open_source_subset
question_count: "150 open-source questions; full benchmark restricted"
document_count: "PDFs available for open-source subset; full benchmark reported separately in paper/docs"
record_fields:
  - question
  - answer
  - evidence
  - document_name
  - to_verify_exact_schema
answer_fields:
  - answer
evidence_fields:
  - evidence
  - evidence_strings
source_document_fields:
  - document_name
  - pdf_filename
document_content_availability: full_pdfs_available_for_open_source_subset
metadata_fields:
  - company
  - filing_year_or_period
  - filing_type
  - page_or_section_to_verify
table_or_structured_data_fields:
  - financial_tables_in_pdfs
existing_annotations:
  - evidence_strings
  - document_references
unanswerable_or_ambiguous_policy: "Designed as clear open-book financial QA; need verify no unanswerable rows in open-source subset."
expected_grounding_classes:
  - textual_evidence
  - metadata
  - organizational_ontology
  - aggregation
normalization_risks:
  - "Full benchmark is restricted; pilot should start with open-source subset."
  - "PDF parsing quality may dominate if not normalized carefully."
  - "Need recover table/text evidence from PDFs, not only evidence strings."
pilot_value: "High as professional source-of-truth reports; useful bridge between realistic RAG and financial document grounding."
blocking_questions:
  - "What exact license applies to the open-source subset and PDFs?"
  - "Which fields exist in each JSONL row?"
  - "Can page-level or section-level evidence be reconstructed reliably?"
sources:
  - https://docs.patronus.ai/docs/research_and_differentiators/financebench
  - https://github.com/patronus-ai/financebench
  - https://huggingface.co/datasets/PatronusAI/financebench
  - https://arxiv.org/abs/2311.11944
---

# דאטהסט: FinanceBench

## רלוונטיות בהערכת RAG רחבה

שנת פרסום הדאטהסט: 2023.

הערכה למרכזיות בהערכות RAG רחבות: בינונית-גבוהה. FinanceBench הפך לאחד המועמדים המוכרים יותר להערכת RAG פיננסי מקצועי, בעיקר משום שהוא מדגיש שאלות שנראות כמו עבודה אמיתית של אנליסט על דוחות ו-filings. הוא אינו benchmark כללי לכל עולם ה-RAG, אבל הוא מרכזי יחסית בתוך הערכות RAG על מסמכים פיננסיים ומקור-אמת מקצועי.

הדאטהסט FinanceBench הוא מועמד טוב מאוד כ-proxy למסמכי אמת מקצועיים: שאלות פיננסיות על דוחות וחומרי גילוי של חברות ציבוריות. זה לא ארגון פנימי, אבל הדוחות עצמם הם מסמכים סמכותיים, עשירים בטבלאות, תקופות, חברות, סעיפים ומדדים.

האמינות טובה, אבל עם מגבלת זמינות ברורה. יש open-source subset ב-Hugging Face וב-GitHub, כולל קובץ JSONL ו-PDFs. לפי התיעוד של Patronus, הגרסה המלאה דורשת רישוי או פנייה אליהם. לכן בשלב הפיילוט צריך להתייחס לכרטיס הזה כאל FinanceBench open-source subset, ולא להניח שיש לנו את כל 10k השאלות.

מבחינת התזה, היתרון הוא שילוב של ריאליזם, ראיות ומסמכי מקור מלאים. זה מאפשר לבדוק שאלות שמערבות מטאדאטה כמו חברה, שנה וסוג דוח, וגם שאלות עם אגרגציה או השוואה על נתונים פיננסיים. החיסרון הוא שעבודת הנרמול עשויה להפוך לבעיית PDF parsing אם ננסה לחלץ מחדש את כל הטבלאות.

בפיילוט, FinanceBench מתאים כזרוע ריאליסטית של מסמכי אמת מקצועיים. הוא פחות “ארגוני” מ-WixQA או TechQA, אבל חשוב כדי לבדוק האם המחלקות שלנו מחזיקות גם בדומיין שבו מסמכים סמכותיים וטבלאות הן מקור מרכזי למענה.
