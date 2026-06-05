---
dataset_id: ragbench
dataset_name: RAGBench
review_status: quick_review
pilot_decision: secondary_control
final_thesis_decision: possible_boundary_or_control
primary_reason: "Benchmark מאוחד שמאגד תתי-דאטהסטים; חזק מאוד להערכת RAG, אך פחות מתאים כיחידת קורפוס מקור יחידה."
relevance_summary: "שימושי כמקור משני, control או שכבת ולידציה רחבה; לא מומלץ כרגע כבסיס היחיד לתזה."
domain: multi_domain_rag_evaluation
source_type:
  - aggregated_benchmark
  - provided_contexts
  - response_support_labels
corpus_availability_status: provided_contexts_available
next_action: "להשתמש בכרטיס המלא ובסקירת העומק החדשה כדי להחליט על פיילוט RAGBench-only מול original-vs-wrapper."
sources:
  - https://arxiv.org/abs/2407.11005
  - https://huggingface.co/datasets/galileo-ai/ragbench
  - https://github.com/rungalileo/ragbench
---

# סקירה קצרה: RAGBench

## עדכון

נוצרו עבור RAGBench כרטיס מלא וסקירת עומק ייעודית:

כרטיס מלא: [[../cards/ragbench|ragbench]]

סקירת עומק: [[../ragbench-deep-review|ragbench-deep-review]]

## שורה תחתונה

הדאטהסט RAGBench קיים וזמין ב-Hugging Face, והוא משמעותי יותר ממה שהסקירה הראשונית תיארה. עדיין, הוא פחות מתאים להיות הבסיס היחיד לפיילוט הראשון. הסיבה היא שהוא לא קורפוס מקור אחד עם משימת QA אחת, אלא benchmark מאוחד של כ-100k דוגמאות RAG שמאגד 12 תתי-דאטהסטים.

חלק מתתי-הדאטהסטים שלו כבר קיימים אצלנו ככרטיסים מלאים או מועמדים: `techqa`, `finqa`, `cuad`. לכן הכנסה של RAGBench ככרטיס מלא עלולה ליצור כפילות: נחשוב שיש לנו עוד דאטהסט, אבל בפועל קיבלנו wrapper מעל דאטהסטים שכבר נבדקו.

## למה לא לפיילוט ראשון

הסיבה הראשונה היא שהוא מיועד בעיקר להערכת מערכות RAG ו-faithfulness, לא לבניית registry נקי של קורפוסים ומקורות אמת.

הסיבה השנייה היא שרשומות RAGBench מכילות contexts/מסמכים שהוכנו עבור הערכה, ולא תמיד את הקורפוס המקורי המלא או את דרך השחזור שלו.

הסיבה השלישית היא שהוא מערבב דומיינים וסכימות, ולכן קשה להשתמש בו כיחידת ניתוח אחת עבור שאלת התזה.

הסיבה הרביעית היא שהוא מכיל תתי-דאטהסטים שכבר מופיעים אצלנו, ולכן הוא עלול לנפח מלאכותית את ספירת הדאטהסטים.

## למה הוא עדיין יכול להיות שימושי

הדאטהסט RAGBench יכול להיות שימושי בשלב מאוחר יותר כ-control עבור מדדי faithfulness או כתשתית לבדיקת תיוג סוכני על contexts מוכנים. אם משתמשים בו, עדיף לעבוד ברמת תת-דאטהסט ולהשוות מול הגרסאות המקוריות של TechQA, FinQA, TAT-QA ו-CUAD כדי למדוד איבוד מידע.

## למה אולי לא מצאת אותו בקבצים

סביר שהוא לא הופיע כי הסקירה שלנו העדיפה את תתי-הדאטהסטים המקוריים על פני wrapper. במקום לפתוח כרטיס ל-RAGBench, פתחנו כרטיסים ל-TechQA, FinQA ו-CUAD, שהם חלק מהמרחב ש-RAGBench כולל.
