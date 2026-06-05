---
dataset_id: frames
dataset_name: FRAMES
review_status: quick_review
pilot_decision: defer
final_thesis_decision: likely_exclude_from_core
primary_reason: "Open-domain Wikipedia benchmark; טוב ל-reasoning RAG, חלש לתיחום מסמכי אמת ארגוניים."
relevance_summary: "יכול להיות control חיצוני, אבל לא core dataset לתזה."
domain: open_domain_wikipedia
source_type:
  - wikipedia_links
  - open_web_facts
  - multi_hop_questions
corpus_availability_status: links_only_not_closed_corpus
next_action: "לא לפתוח card מלא אלא אם מחליטים להוסיף open-domain control."
sources:
  - https://arxiv.org/abs/2409.12941
  - https://huggingface.co/datasets/google/frames-benchmark
---

# FRAMES

## שורה תחתונה

FRAMES קיים, והוא בנצ'מרק מעניין ל-RAG רב-שלבי: שאלות multi-hop, reasoning, factuality, וקישורי Wikipedia שמצביעים למקורות. אבל עבור התזה שלנו הוא חלש כמועמד core, כי הוא לא עובד על קורפוס מסמכי אמת סגור אלא על open-domain Wikipedia.

הדאטהסט כולל 824 שורות, עם prompt, answer, קישורי Wikipedia וסוגי reasoning. זה טוב להערכת יכולת חיפוש וריזונינג, אבל פחות טוב לשחזור מקור קרקוע בתוך מאגר ארגוני עם מטאדאטה, מבנה תיקיות, ישויות פנימיות או אגרגציה על מסמכי אמת.

## למה לא לפיילוט ראשון

1. הקורפוס אינו סגור; יש קישורי Wikipedia ולא מאגר מסמכים מוגדר שאפשר להתייחס אליו כ-source-of-truth ארגוני.
2. הרבה שאלות הן open-domain ויכולות להיות תלויות בזמן, למשל "as of August 2024".
3. הדאטהסט בודק reasoning ורטריבר, אבל לא בהכרח את סוגי מקורות הקרקוע שמעניינים את המחקר.
4. הוא פחות מתאים לבדוק אונטולוגיה ארגונית, מבנה מסמכים או ownership/versioning.

## למה הוא עדיין יכול להיות שימושי

FRAMES יכול להיות control חיצוני טוב אם נרצה לבדוק האם הסכמה שלנו מבחינה נכון בין multi-hop פתוח לבין שאלות ארגוניות. הוא יכול גם לעזור להראות ש-open-domain RAG אינו אותו דבר כמו QA מעל מסמכי אמת ארגוניים.

## למה אולי לא מצאת אותו בקבצים

סביר שהוא לא הופיע כי הסקירה התמקדה בדאטהסטים עם קורפוס מקור סגור או מקצועי. FRAMES נמצא מחוץ לליבה הזו: הוא חשוב לבנצ'מרקינג כללי של RAG, אבל פחות מתאים למטרת הפיילוט שהוגדרה כאן.
