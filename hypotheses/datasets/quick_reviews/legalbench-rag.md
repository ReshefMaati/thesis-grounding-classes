---
dataset_id: legalbench-rag
dataset_name: LegalBench-RAG
review_status: quick_review
pilot_decision: defer
final_thesis_decision: possible_boundary_or_control
primary_reason: "IR/snippet benchmark משפטי; פחות מתאים לפיילוט ראשון של מחלקות קרקוע רחבות."
relevance_summary: "רלוונטי כמקרה גבול משפטי וכבדיקת retrieval מדויק, אבל לא כמועמד ראשון."
domain: legal_contracts
source_type:
  - legal_contracts
  - legal_corpus
  - retrieval_snippets
corpus_availability_status: corpus_download_link_available
next_action: "לחזור אליו רק אם נרצה control משפטי או השוואה מול CUAD."
sources:
  - https://arxiv.org/abs/2408.10343
  - https://github.com/zeroentropy-ai/legalbenchrag
---

# LegalBench-RAG

## שורה תחתונה

LegalBench-RAG כן קיים, ולכן הוא לא נפל בגלל חוסר זמינות עקרוני. הוא פשוט לא הוכנס לשכבת הכרטיסים המלאים כי הוא פחות מתאים לפיילוט הראשון שלנו מאשר WixQA, TechQA, MultiHiertt או FinanceBench.

הוא בנצ'מרק retrieval משפטי: המטרה היא לבדוק האם מערכת מחזירה snippet משפטי מדויק, עד רמת טווחי תווים. זה חשוב, אבל הוא מצמצם מראש את משימת הקרקוע לראיה טקסטואלית מקומית בתוך קורפוס משפטי. לכן הוא פחות טוב לשאלה הרחבה שלנו: האם שאלות QA/RAG דורשות גם מטאדאטה, אונטולוגיה ארגונית ואגרגציה.

## למה לא לפיילוט ראשון

1. הוא ממוקד IR ו-snippet retrieval, לא QA ארגוני רחב.
2. הדאטהסט כבר מקבע את הקרקוע כקטעי טקסט משפטיים, ולכן הוא עלול לחזק מלאכותית את מחלקת `textual_evidence`.
3. יש כפילות רעיונית עם CUAD, שכבר נמצא ככרטיס מלא. אם נרצה משפטי, עדיף קודם להחליט אם CUAD או LegalBench-RAG משרתים טוב יותר את שאלת המחקר.
4. הוא פחות מתאים לבדוק אונטולוגיה ארגונית ואגרגציה, שהן מחלקות שמעניינות אותנו במיוחד.

## למה הוא עדיין יכול להיות שימושי

LegalBench-RAG יכול להיות control משפטי טוב בהמשך: אם נרצה להראות שהטקסונומיה עובדת גם במצב שבו הקרקוע כמעט כולו evidence span, הוא מספק מקרה נקי ומבוקר. הוא גם יכול לעזור לנסח גבול בין "retrieval benchmark" לבין "dataset for grounding-source taxonomy".

## למה אולי לא מצאת אותו בקבצים

הקבצים הקיימים התמקדו בכרטיסי דאטהסטים שנבחרו כמועמדים מעשיים לפיילוט. LegalBench-RAG הופיע מאוחר יחסית בסקירה או לא עבר את סף הפיילוט הראשון, ולכן לא נפתח לו כרטיס מלא. בנוסף, אם חיפשת לפי LegalBench בלי RAG, קל להגיע ל-LegalBench הכללי, שהוא לא אותו דבר.
